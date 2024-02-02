Muitos algoritmos em teoria dos números, como teste de primalidade ou fatoração de inteiros, e em criptografia, como o RSA, exigem muitas operações módulo um número grande. Uma multiplicação como  $x y \bmod{n}$  é bastante lenta de ser calculada com os algoritmos típicos, pois requer uma divisão para saber quantas vezes  $n$  precisa ser subtraído do produto. E a divisão é uma operação realmente cara, especialmente com números grandes.

A multiplicação modular de Montgomery é um método que permite calcular essas multiplicações de maneira mais rápida. Em vez de dividir o produto e subtrair  $n$  várias vezes, ela adiciona múltiplos de  
$n$  para cancelar os bits mais baixos e depois simplesmente descarta esses bits mais baixos.

## Representação de Montgomery
No entanto, a multiplicação de Montgomery não ocorre de graça. O algoritmo funciona apenas no espaço de Montgomery. E precisamos transformar nossos números nesse espaço antes de começarmos a multiplicar.

Para o espaço, precisamos de um número inteiro positivo  $r \ge n$  coprimo com  
$n$ , ou seja,  $\gcd(n, r) = 1$ . Na prática, sempre escolhemos  $r$  para ser  $2^m$  para um número inteiro positivo  $m$ , já que multiplicações, divisões e operações de módulo  $r$  podem ser eficientemente implementadas usando deslocamentos e outras operações de bits.  $n$  será um número ímpar em praticamente todas as aplicações, já que não é difícil fatorar um número par. Portanto, cada potência de  $2$  será coprima com  $n$ .

O representante  $\bar{x}$  de um número  $x$  no espaço de Montgomery é definido como:

$$\bar{x} := x \cdot r \bmod n$$ 
Observe que a transformação é na verdade uma multiplicação que queremos otimizar. Portanto, esta ainda é uma operação cara. No entanto, você só precisa transformar um número uma vez para o espaço. Assim que estiver no espaço de Montgomery, você pode realizar quantas operações quiser de maneira eficiente. E no final, você transforma o resultado final de volta. Portanto, enquanto estiver fazendo muitas operações módulo  $n$ , isso não será um problema.

Dentro do espaço de Montgomery, ainda é possível realizar a maioria das operações normalmente. Você pode adicionar dois elementos ( $x \cdot r + y \cdot r \equiv (x + y) \cdot r \bmod n$ ), subtrair, verificar igualdade e até mesmo calcular o maior divisor comum de um número com  $n$  (já que  $\gcd(n, r) = 1$ ). Tudo com os algoritmos usuais.

No entanto, isso não é o caso para a multiplicação.

Esperamos que o resultado seja:
$$\bar{x} * \bar{y} = \overline{x \cdot y} = (x \cdot y) \cdot r \bmod n.$$ 
Mas a multiplicação normal nos dará:
$$\bar{x} \cdot \bar{y} = (x \cdot y) \cdot r \cdot r \bmod n.$$ 
Portanto, a multiplicação no espaço de Montgomery é definida como:
$$\bar{x} * \bar{y} := \bar{x} \cdot \bar{y} \cdot r^{-1} \bmod n.$$ 
## Redução de Montgomery
A multiplicação de dois números no espaço de Montgomery requer um cálculo eficiente de  
$x \cdot r^{-1} \bmod n$ . Essa operação é chamada de redução de Montgomery e também é conhecida como o algoritmo REDC.

Como  $\gcd(n, r) = 1$ , sabemos que existem dois números  $r^{-1}$  e  $n^{\prime}$  com  $0 < r^{-1}, n^{\prime} < n$ , com
$$r \cdot r^{-1} + n \cdot n^{\prime} = 1.$$ 
Ambos  $r^{-1}$  e  $n^{\prime}$  podem ser calculados usando o [algoritmo estendido de Euclides].

Usando essa identidade, podemos escrever  $x \cdot r^{-1}$  como:
 
$$\begin{aligned} x \cdot r^{-1} &= x \cdot r \cdot r^{-1} / r = x \cdot (-n \cdot n^{\prime} + 1) / r \\ &= (-x \cdot n \cdot n^{\prime} + x) / r \equiv (-x \cdot n \cdot n^{\prime} + l \cdot r \cdot n + x) / r \bmod n\\ &\equiv ((-x \cdot n^{\prime} + l \cdot r) \cdot n + x) / r \bmod n \end{aligned}$$ 
As equivalências valem para qualquer número inteiro arbitrário  $l$ . Isso significa que podemos adicionar ou subtrair um múltiplo arbitrário de  $r$  a  $x \cdot n^{\prime}$ , ou em outras palavras, podemos calcular  $q := x \cdot n^{\prime}$  módulo  $r$ .

Isso nos dá o seguinte algoritmo para calcular  $x \cdot r^{-1} \bmod n$ :

```python
def reduce(x):
    q = (x % r) * n_prime % r
    a = (x - q * n) // r
    if a < 0:
        a += n
    return a
```

Como  $x < n \cdot n < r \cdot n$  (mesmo se  $x$  for o produto de uma multiplicação) e  $q \cdot n < r \cdot n$ , sabemos que  $-n < (x - q \cdot n) / r < n$ . Portanto, a operação final de módulo é implementada usando uma única verificação e uma adição.

Como vemos, podemos realizar a redução de Montgomery sem nenhuma operação de módulo pesada. Se escolhermos  $r$  como uma potência de  $2$ , as operações de módulo e divisões no algoritmo podem ser calculadas usando mascaramento e deslocamento de bits.

Uma segunda aplicação da redução de Montgomery é transferir um número de volta do espaço de Montgomery para o espaço normal.
[[Fast inverse trick]]

Para calcular a inversa  $n^{\prime} := n^{-1} \bmod r$  de maneira eficiente, podemos usar o seguinte truque (inspirado no método de Newton):
$$a \cdot x \equiv 1 \bmod 2^k \Longrightarrow a \cdot x \cdot (2 - a \cdot x) \equiv 1 \bmod 2^{2k}$$ 
Isso pode ser facilmente comprovado. Se tivermos  $a \cdot x = 1 + m \cdot 2^k$ , então teremos:
$$\begin{aligned} a \cdot x \cdot (2 - a \cdot x) &= 2 \cdot a \cdot x - (a \cdot x)^2 \\ &= 2 \cdot (1 + m \cdot 2^k) - (1 + m \cdot 2^k)^2 \\ &= 2 + 2 \cdot m \cdot 2^k - 1 - 2 \cdot m \cdot 2^k - m^2 \cdot 2^{2k} \\ &= 1 - m^2 \cdot 2^{2k} \\ &\equiv 1 \bmod 2^{2k}. \end{aligned}$$ 
Isso significa que podemos começar com  $x = 1$  como a inversa de  $a$  módulo $2^1$ , aplicar o truque algumas vezes e em cada iteração dobramos o número de bits corretos de  $x$ .
## Implementação
Usando o compilador GCC, ainda podemos calcular  
$x \cdot y \bmod n$  de maneira eficiente quando os três números são inteiros de 64 bits, já que o compilador suporta inteiros de 128 bits com os tipos __int128 e __uint128.

```cpp
long long result = (__int128)x * y % n;
```

No entanto, não existe um tipo para inteiros de 256 bits. Portanto, aqui mostraremos uma implementação para uma multiplicação de 128 bits.

```cpp
using u64 = uint64_t;
using u128 = __uint128_t;
using i128 = __int128_t;

struct u256 {
    u128 high, low;

    static u256 mult(u128 x, u128 y) {
        u64 a = x >> 64, b = x;
        u64 c = y >> 64, d = y;
        // (a*2^64 + b) * (c*2^64 + d) =
        // (a*c) * 2^128 + (a*d + b*c)*2^64 + (b*d)
        u128 ac = (u128)a * c;
        u128 ad = (u128)a * d;
        u128 bc = (u128)b * c;
        u128 bd = (u128)b * d;
        u128 carry = (u128)(u64)ad + (u128)(u64)bc + (bd >> 64u);
        u128 high = ac + (ad >> 64u) + (bc >> 64u) + (carry >> 64u);
        u128 low = (ad << 64u) + (bc << 64u) + bd;
        return {high, low};
    }
};

struct Montgomery {
    Montgomery(u128 n) : mod(n), inv(1) {
        for (int i = 0; i < 7; i++)
            inv *= 2 - n * inv;
    }

    u128 init(u128 x) {
        x %= mod;
        for (int i = 0; i < 128; i++) {
            x <<= 1;
            if (x >= mod)
                x -= mod;
        }
        return x;
    }

    u128 reduce(u256 x) {
        u128 q = x.low * inv;
        i128 a = x.high - u256::mult(q, mod).high;
        if (a < 0)
            a += mod;
        return a;
    }

    u128 mult(u128 a, u128 b) {
        return reduce(u256::mult(a, b));
    }

    u128 mod, inv;
};
```

Esta implementação inclui uma multiplicação de 128 bits (u256::mult) e uma implementação de Montgomery para realizar operações eficientes em módulos. O truque da inversa rápida também é utilizado para calcular a inversa eficientemente.
## Transformação Rápida
O método atual de transformar um número para o espaço de Montgomery é bastante lento. Existem maneiras mais rápidas.

Podemos observar a seguinte relação:
$$\bar{x} := x \cdot r \bmod n = x \cdot \frac{r^2}{r} = x \cdot r^2$$ 
Transformar um número para o espaço é apenas uma multiplicação dentro do espaço do número por  $r^2$ . Portanto, podemos pré-calcular  $r^2 \bmod n$  e apenas realizar uma multiplicação em vez de deslocar o número 128 vezes.

No código a seguir, inicializamos r2 com -n % n, que é equivalente a  $r - n \equiv r \bmod n$ , deslocamos isso 4 vezes para obter  $r \cdot 2^4 \bmod n$ . Este número pode ser interpretado como  $2^4$  no espaço de Montgomery. Se o elevamos ao quadrado  $5$  vezes, obtemos  $(2^4)^{2^5} = (2^4)^{32} = 2^{128} = r$  no espaço de Montgomery, que é exatamente  $r^2 \bmod n$ .

```cpp
struct Montgomery {
    Montgomery(u128 n) : mod(n), inv(1), r2(-n % n) {
        for (int i = 0; i < 7; i++)
            inv *= 2 - n * inv;

        for (int i = 0; i < 4; i++) {
            r2 <<= 1;
            if (r2 >= mod)
                r2 -= mod;
        }
        for (int i = 0; i < 5; i++)
            r2 = mul(r2, r2);
    }

    u128 init(u128 x) {
        return mult(x, r2);
    }

    u128 mod, inv, r2;
};
```

Essa implementação otimiza a transformação para o espaço de Montgomery usando  $r^2 \bmod n$  pré-computado, resultando em uma execução mais rápida.