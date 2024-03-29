
O logaritmo discreto é um número inteiro  $x$  que satisfaz a equação
$$a^x \equiv b \pmod m$$ 
para inteiros dados  $a$ ,  $b$  e  $m$ .

O logaritmo discreto nem sempre existe, por exemplo, não há solução para  $2^x \equiv 3 \pmod 7$ . Não há uma condição simples para determinar se o logaritmo discreto existe.

Neste artigo, descrevemos o algoritmo Baby-step giant-step, um algoritmo para calcular o logaritmo discreto proposto por Shanks em 1971, que possui complexidade de tempo  
$O(\sqrt{m})$ . Este é um algoritmo meet-in-the-middle porque usa a técnica de dividir as tarefas ao meio.

## Algoritmo
Considere a equação:
$$a^x \equiv b \pmod m,$$ 
onde  $a$  e  $m$  são primos entre si.

Seja  $x = np - q$ , onde  $n$  é uma constante pré-selecionada (vamos descrever como selecionar  
$n$  mais tarde).  $p$  é conhecido como o "passo gigante" ("giant step"), já que aumentá-lo em um aumenta  $x$  por  $n$ . Da mesma forma,  $q$  é conhecido como o "passo pequeno" ("baby step").

Obviamente, qualquer número  $x$  no intervalo  $[0; m)$  pode ser representado dessa forma, onde  
$p \in [1; \lceil \frac{m}{n} \rceil ]$  e  $q \in [0; n]$ .

Então, a equação se torna:
$$a^{np - q} \equiv b \pmod m.$$ 
Usando o fato de que  $a$  e  $m$  são primos entre si, obtemos:
$$a^{np} \equiv ba^q \pmod m$$ 
Esta nova equação pode ser reescrita de forma simplificada:
$$f_1(p) = f_2(q).$$ 
Esse problema pode ser resolvido usando o método meet-in-the-middle da seguinte maneira:

-  Calcule  $f_1$  para todos os possíveis argumentos  $p$ . Ordene o array de pares valor-argumento.
-  Para todos os possíveis argumentos  $q$ , calcule  $f_2$  e procure pelo  $p$  correspondente no array ordenado usando busca binária.
## Complexidade

Podemos calcular  $f_1(p)$  em  $O(\log m)$  usando o algoritmo de exponenciação binária. De forma semelhante para  
$f_2(q)$ .

Na primeira etapa do algoritmo, precisamos calcular  $f_1$  para cada possível argumento  $p$  e, em seguida, ordenar os valores. Assim, esta etapa tem complexidade:
  
$$O\left(\left\lceil \frac{m}{n} \right\rceil \left(\log m + \log \left\lceil \frac{m}{n} \right\rceil \right)\right) = O\left( \left\lceil \frac {m}{n} \right\rceil \log m\right)$$ 
Na segunda etapa do algoritmo, precisamos calcular  
$f_2(q)$  para cada possível argumento  
$q$  e, em seguida, realizar uma busca binária no array de valores de  
$f_1$ , assim esta etapa tem complexidade:
 
$$O\left(n \left(\log m + \log \frac{m}{n} \right) \right) = O\left(n \log m\right).$$ 
Agora, quando adicionamos essas duas complexidades, obtemos  $\log m$  multiplicado pela soma de  $n$  e  $m/n$ , que é mínima quando  $n = m/n$ , o que significa que, para obter desempenho ótimo,  
$n$  deve ser escolhido de forma que:
$$n = \sqrt{m}.$$ 
Então, a complexidade do algoritmo torna-se:
$$O(\sqrt {m} \log m).$$ 
## Implementação

### A implementação mais simples
No código a seguir, a função powmod calcula  $a^b \pmod m$  e a função solve produz uma solução adequada para o problema. Ela retorna  $-1$  se não houver solução e retorna uma das soluções possíveis, caso contrário.

```cpp
int powmod(int a, int b, int m) {
    int res = 1;
    while (b > 0) {
        if (b & 1) {
            res = (res * 1ll * a) % m;
        }
        a = (a * 1ll * a) % m;
        b >>= 1;
    }
    return res;
}

int solve(int a, int b, int m) {
    a %= m, b %= m;
    int n = sqrt(m) + 1;
    map<int, int> vals;
    for (int p = 1; p <= n; ++p)
        vals[powmod(a, p * n, m)] = p;
    for (int q = 0; q <= n; ++q) {
        int cur = (powmod(a, q, m) * 1ll * b) % m;
        if (vals.count(cur)) {
            int ans = vals[cur] * n - q;
            return ans;
        }
    }
    return -1;
}
```

Neste código, usamos `map` da biblioteca padrão do C++ para armazenar os valores de  
$f_1$ . Internamente, o `map` usa uma árvore rubro-negra para armazenar os valores. Portanto, este código é um pouco mais lento do que se tivéssemos usado um array e realizado a busca binária, mas é muito mais fácil de escrever.

Observe que nosso código assume  $0^0 = 1$ , ou seja, o código calculará  $0$  como solução para a equação  $0^x \equiv 1 \pmod m$  e também como solução para  $0^x \equiv 0 \pmod 1$ . Esta é uma convenção frequentemente usada na álgebra, mas também não é universalmente aceita em todas as áreas. Às vezes,  $0^0$  é simplesmente indefinido. Se você não gostar da nossa convenção, precisará tratar o caso  $a=0$  separadamente:

```cpp
if (a == 0)
    return b == 0 ? 1 : -1;
```

Outra coisa a observar é que, se houver vários argumentos  $p$  que mapeiam para o mesmo valor de  $f_1$ , armazenamos apenas um desses argumentos. Isso funciona neste caso porque só queremos retornar uma possível solução. Se precisarmos retornar todas as soluções possíveis, precisamos alterar `map<int, int>` para, por exemplo, `map<int, vector<int>>`. Também precisamos ajustar a segunda etapa de acordo.

## Implementação melhorada

Uma possível melhoria é eliminar a exponenciação binária. Isso pode ser feito mantendo uma variável que é multiplicada por  $a$  cada vez que aumentamos  $q$  e uma variável que é multiplicada por  $a^n$  cada vez que aumentamos  $p$ . Com essa alteração, a complexidade do algoritmo ainda é a mesma, mas agora o fator  $\log$  é apenas para o mapa. Em vez de um mapa, também podemos usar uma tabela de hash (unordered_map em C++), que tem complexidade de tempo média  
$O(1)$  para inserção e busca.

Problemas frequentemente pedem o mínimo  
$x$  que satisfaz a solução.
É possível obter todas as respostas e pegar a mínima, ou reduzir a primeira resposta encontrada usando o teorema de Euler, mas podemos ser inteligentes sobre a ordem em que calculamos os valores e garantir que a primeira resposta que encontramos seja a mínima.

```cpp
// Returns minimum x for which a ^ x % m = b % m, a and m are coprime.
int solve(int a, int b, int m) {
    a %= m, b %= m;
    int n = sqrt(m) + 1;

    int an = 1;
    for (int i = 0; i < n; ++i)
        an = (an * 1ll * a) % m;

    unordered_map<int, int> vals;
    for (int q = 0, cur = b; q <= n; ++q) {
        vals[cur] = q;
        cur = (cur * 1ll * a) % m;
    }

    for (int p = 1, cur = 1; p <= n; ++p) {
        cur = (cur * 1ll * an) % m;
        if (vals.count(cur)) {
            int ans = n * p - vals[cur];
            return ans;
        }
    }
    return -1;
}
```

A complexidade é  $O(\sqrt{m})$  usando unordered_map.
## Quando $a$ e  $m$ não são coprimos
Seja  $g = \gcd(a, m)$ , e  $g > 1$ . Claramente  $a^x \bmod m$  para todo  $x \ge 1$  será divisível por  $g$ .

Se  $g \nmid b$ , não há solução para  $x$ .

Se  $g \mid b$ , seja  $a = g \alpha, b = g \beta, m = g \nu$ .
$$ \begin{aligned} a^x & \equiv b \mod m \\\ (g \alpha) a^{x - 1} & \equiv g \beta \mod g \nu \\\ \alpha a^{x-1} & \equiv \beta \mod \nu \end{aligned} $$ 
O algoritmo baby-step giant-step pode ser facilmente estendido para resolver  $ka^{x} \equiv b \pmod m$  para  $x$ .

```cpp
// Returns minimum x for which a ^ x % m = b % m.
int solve(int a, int b, int m) {
    a %= m, b %= m;
    int k = 1, add = 0, g;
    while ((g = gcd(a, m)) > 1) {
        if (b == k)
            return add;
        if (b % g)
            return -1;
        b /= g, m /= g, ++add;
        k = (k * 1ll * a / g) % m;
    }

    int n = sqrt(m) + 1;
    int an = 1;
    for (int i = 0; i < n; ++i)
        an = (an * 1ll * a) % m;

    unordered_map<int, int> vals;
    for (int q = 0, cur = b; q <= n; ++q) {
        vals[cur] = q;
        cur = (cur * 1ll * a) % m;
    }

    for (int p = 1, cur = k; p <= n; ++p) {
        cur = (cur * 1ll * an) % m;
        if (vals.count(cur)) {
            int ans = n * p - vals[cur] + add;
            return ans;
        }
    }
    return -1;
}
```

A complexidade de tempo continua sendo  $O(\sqrt{m})$  como antes, uma vez que a redução inicial para  $a$  e  $m$  primos entre si é feita em  $O(\log^2 m)$ .