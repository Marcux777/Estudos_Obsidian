## Exponenciação Binária por Fatoração

Considere o problema de calcular  $ax^y \pmod{2^d}$ , dados os inteiros  $a$ ,  $x$ ,  $y$  e  $d \geq 3$ , onde  $x$  é ímpar.

O algoritmo abaixo permite resolver este problema com  $O(d)$  adições e operações binárias e uma única multiplicação por  $y$ .

Devido à estrutura do grupo multiplicativo módulo  $2^d$ , qualquer número  $x$  tal que  $x \equiv 1 \pmod 4$  pode ser representado como
 
$$ x \equiv b^{L(x)} \pmod{2^d}, $$ 
onde  $b \equiv 5 \pmod 8$ . Sem perda de generalidade, assumimos que  $x \equiv 1 \pmod 4$ , pois podemos reduzir  $x \equiv 3 \pmod 4$  para  $x \equiv 1 \pmod 4$  substituindo  $x \mapsto -x$  e  $a \mapsto (-1)^{y} a$ . Nesta noção,  $ax^y$  é representado como 
$$ a x^y \equiv a b^{yL(x)} \pmod{2^d}. $$ 
A ideia central do algoritmo é simplificar o cálculo de  $L(x)$  e  $b^{y L(x)}$  usando o fato de que estamos trabalhando módulo  $2^d$ . Por razões que ficarão aparentes mais tarde, estaremos trabalhando com  $4L(x)$  em vez de  $L(x)$ , mas tomado módulo  $2^d$  em vez de  $2^{d-2}$ .

Neste artigo, vamos abordar a implementação para inteiros de  
$32$  bits. Deixe
- mbin_log_32(r, x) ser uma função que calcula  $r+4L(x) \pmod{2^d}$ ;
- mbin_exp_32(r, x) ser uma função que calcula  $r b^{\frac{x}{4}} \pmod{2^d}$;
- mbin_power_odd_32(a, x, y) ser uma função que calcula  $ax^y \pmod{2^d}$ .

Então mbin_power_odd_32 é implementado da seguinte forma:

```c
uint32_t mbin_power_odd_32(uint32_t rem, uint32_t base, uint32_t exp) {
    if (base & 2) {
        /* divisor é considerado negativo */
        base = -base;
        /* verifica se o resultado deve ser negativo */
        if (exp & 1) {
            rem = -rem;
        }
    }
    return (mbin_exp_32(rem, mbin_log_32(0, base) * exp));
}
```

## Cálculo de 4L(x) a partir de x
Seja  $x$  um número ímpar tal que  $x \equiv 1 \pmod 4$ . Ele pode ser representado como 
$$ x \equiv (2^{a_1}+1)\dots(2^{a_k}+1) \pmod{2^d}, $$ 
onde  $1 < a_1 < \dots < a_k < d$ . Aqui  $L(\cdot)$  é bem definido para cada multiplicador, pois eles são iguais a  $1$  módulo  $4$ . Portanto,
$$ 4L(x) \equiv 4L(2^{a_1}+1)+\dots+4L(2^{a_k}+1) \pmod{2^{d}}. $$ 
Então, se pré-calculamos  $t_k = 4L(2^n+1)$  para todos $1 < k < d$ , seremos capazes de calcular  $4L(x)$  para qualquer número  $x$ .

Para inteiros de 32 bits, podemos usar a seguinte tabela:

```c
const uint32_t mbin_log_32_table[32] = {
    0x00000000, 0x00000000, 0xd3cfd984, 0x9ee62e18,
    0xe83d9070, 0xb59e81e0, 0xa17407c0, 0xce601f80,
    0xf4807f00, 0xe701fe00, 0xbe07fc00, 0xfc1ff800,
    0xf87ff000, 0xf1ffe000, 0xe7ffc000, 0xdfff8000,
    0xffff0000, 0xfffe0000, 0xfffc0000, 0xfff80000,
    0xfff00000, 0xffe00000, 0xffc00000, 0xff800000,
    0xff000000, 0xfe000000, 0xfc000000, 0xf8000000,
    0xf0000000, 0xe0000000, 0xc0000000, 0x80000000,
};
```
Na prática, é usada uma abordagem ligeiramente diferente da descrita acima. Em vez de encontrar a fatoração para  $x$ , multiplicaremos sucessivamente  $x$  com  $2^n+1$  até transformá-lo em  $1$  módulo  $2^d$ . Desta forma, encontraremos a representação de $x^{-1}$ , ou seja,
$$ x (2^{a_1}+1)\dots(2^{a_k}+1) \equiv 1 \pmod {2^d}. $$ 
Para fazer isso, iteramos sobre  $n$  tal que  $1 < n < d$ . Se o atual  $x$  tem o bit  $n$  definido, multiplicamos  $x$  com  $2^n+1$ , o que é convenientemente feito em C++ como x = x + (x << n). Isso não mudará os bits menores que  $n$ , mas transformará o bit  $n$  em zero, porque  $x$  é ímpar.

Com tudo isso em mente, a função mbin_log_32(r, x) é implementada da seguinte forma:

```c
uint32_t mbin_log_32(uint32_t r, uint32_t x) {
    uint8_t n;

    for (n = 2; n < 32; n++) {
        if (x & (1 << n)) {
            x = x + (x << n);
            r -= mbin_log_32_table[n];
        }
    }

    return r;
}
```
Note que  $4L(x) = -4L(x^{-1})$ , então, em vez de adicionar  $4L(2^n+1)$ , subtraímos de  $r$ , que inicialmente é igual a  $0$ .

## Cálculo de x a partir de 4L(x)
Note que para  $k \geq 1$  vale que 
$$ (a 2^{k}+1)^2 = a^2 2^{2k} +a 2^{k+1}+1 = b2^{k+1}+1, $$ 
a partir do qual (por quadratura repetida) podemos deduzir que
 
$$ (2^a+1)^{2^b} \equiv 1 \pmod{2^{a+b}}. $$ 
Aplicando este resultado a  $a=2^n+1$  e  $b=d-k$  deduzimos que a ordem multiplicativa de  $2^n+1$  é um divisor de  $2^{d-n}$ .

Isso, por sua vez, significa que  $L(2^n+1)$  deve ser divisível por  $2^{n}$ , pois a ordem de  
$b$  é  $2^{d-2}$  e a ordem de  $b^y$  é  $2^{d-2-v}$ , onde  $2^v$  é a maior potência de  $2$  que divide  
$y$ , então precisamos 
$$ 2^{d-k} \equiv 0 \pmod{2^{d-2-v}}, $$ 
assim  $v$  deve ser maior ou igual a  $k-2$ . Isso é um pouco feio e para mitigar isso dissemos no início que multiplicamos  $L(x)$  por  $4$ . Agora, se conhecemos  $4L(x)$ , podemos decompor de forma única em uma soma de  $4L(2^n+1)$  verificando consequentemente os bits em  $4L(x)$ . Se o bit  $n$  estiver definido como  $1$ , multiplicaremos o resultado com  $2^n+1$  e reduziremos o atual  $4L(x)$  por  $4L(2^n+1)$ .

Assim, mbin_exp_32 é implementado da seguinte forma:

```c
uint32_t mbin_exp_32(uint32_t r, uint32_t x) {
    uint8_t n;

    for (n = 2; n < 32; n++) {
        if (x & (1 << n)) {
            r = r + (r << n);
            x -= mbin_log_32_table[n];
        }
    }

    return r;
}
```



## Otimizações Adicionais

É possível reduzir pela metade o número de iterações se você observar que  $4L(2^{d-1}+1)=2^{d-1}$  e que para  $2k \geq d$  vale que 
$$ (2^n+1)^2 \equiv 2^{2n} + 2^{n+1}+1 \equiv 2^{n+1}+1 \pmod{2^d}, $$ 
o que permite deduzir que  $4L(2^n+1)=2^n$  para  $2n \geq d$ . Assim, você poderia simplificar o algoritmo indo apenas até  $\frac{d}{2}$  e então usar o fato acima para calcular a parte restante com operações bitwise:

```c
uint32_t mbin_log_32(uint32_t r, uint32_t x) {
    uint8_t n;

    for (n = 2; n != 16; n++) {
        if (x & (1 << n)) {
            x = x + (x << n);
            r -= mbin_log_32_table[n];
        }
    }

    r -= (x & 0xFFFF0000);

    return r;
}

uint32_t mbin_exp_32(uint32_t r, uint32_t x) {
    uint8_t n;

    for (n = 2; n != 16; n++) {
        if (x & (1 << n)) {
            r = r + (r << n);
            x -= mbin_log_32_table[n];
        }
    }

    r *= 1 - (x & 0xFFFF0000);

    return r;
}
```



## Cálculo da tabela de logaritmos

Para calcular a tabela de logaritmos, pode-se modificar o algoritmo de Pohlig-Hellman para o caso em que o módulo é uma potência de  
$2$ .

Nossa principal tarefa aqui é calcular  $x$  tal que  $g^x \equiv y \pmod{2^d}$ , onde  
$g=5$  e  $y$  é um número do tipo  $2^n+1$ .

Elevando ambos os lados ao quadrado  $k$  vezes, chegamos a 
$$ g^{2^k x} \equiv y^{2^k} \pmod{2^d}. $$ 
Note que a ordem de  $g$  não é maior que  $2^{d}$  (na verdade, que  $2^{d-2}$ , mas vamos nos ater a  $2^d$  por conveniência), portanto, usando  $k=d-1$  teremos ou  $g^1$  ou  $g^0$  no lado esquerdo, o que nos permite determinar o bit mais pequeno de  $x$  comparando  $y^{2^k}$  com  $g$ . Agora suponha que  $x=x_0 + 2^k x_1$ , onde  $x_0$  é uma parte conhecida e  $x_1$  ainda não é conhecido. Então 
$$ g^{x_0+2^k x_1} \equiv y \pmod{2^d}. $$ 
Multiplicando ambos os lados por  $g^{-x_0}$ , obtemos 
$$ g^{2^k x_1} \equiv (g^{-x_0} y) \pmod{2^d}. $$ 
Agora, elevando ambos os lados ao quadrado  $d-k-1$  vezes, podemos obter o próximo bit de  $x$ , recuperando eventualmente todos os seus bits.

