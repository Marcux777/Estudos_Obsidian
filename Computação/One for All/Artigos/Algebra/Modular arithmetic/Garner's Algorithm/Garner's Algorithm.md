
Uma consequência do Teorema Chinês dos Restos (CRT) é que podemos representar números grandes usando um array de inteiros pequenos. Por exemplo, deixe $p$ ser o produto dos primeiros $1000$ números primos. $p$ tem cerca de $3000$ dígitos.

Qualquer número $a$ menor que $p$ pode ser representado como um array $a_1, \ldots, a_k$, onde $a_i \equiv a \pmod{p_i}$. Mas para fazer isso, obviamente, precisamos saber como recuperar o número $a$ a partir de sua representação. Uma maneira de fazer isso é discutida no artigo sobre o Teorema Chinês dos Restos.

Neste artigo, discutimos uma alternativa, o Algoritmo de Garner, que também pode ser usado para esse fim.

## Representação de Base Mista
Podemos representar o número $a$ na representação de base mista:

$$a = x_1 + x_2 p_1 + x_3 p_1 p_2 + \ldots + x_k p_1 \cdots p_{k-1} \text{ com }x_i \in [0, p_i)$$

A representação de base mista é um sistema de numeração posicional que é uma generalização dos sistemas de numeração típicos, como o sistema binário ou o sistema decimal. Por exemplo, o sistema decimal é um sistema de numeração posicional com a base 10. Cada número é representado como uma sequência de dígitos $d_1 d_2 d_3 \dots d_n$ entre $0$ e $9$, e por exemplo, a sequência $415$ representa o número $4 \cdot 10^2 + 1 \cdot 10^1 + 5 \cdot 10^0$. Em geral, a sequência de dígitos $d_1 d_2 d_3 \dots d_n$ representa o número $d_1 b^{n-1} + d_2 b^{n-2} + \cdots + d_n b^0$ no sistema de numeração posicional com a base $b$.

Em um sistema de base mista, não temos mais uma base única. A base varia de posição para posição.

## Algoritmo de Garner
O Algoritmo de Garner calcula os dígitos $x_1, \ldots, x_k$. Observe que os dígitos são relativamente pequenos. O dígito $x_i$ é um número inteiro entre $0$ e $p_i - 1$.

Denote $r_{ij}$ como o inverso de $p_i$ modulo $p_j$:

$$r_{ij} = (p_i)^{-1} \pmod{p_j}$$

que pode ser encontrado usando o algoritmo descrito em Inverso Modular.

Substituindo $a$ da representação de base mista na primeira equação congruente, obtemos

$$a_1 \equiv x_1 \pmod{p_1}.$$

Substituindo na segunda equação, obtemos

$$a_2 \equiv x_1 + x_2 p_1 \pmod{p_2},$$

que pode ser reescrito subtraindo $x_1$ e dividindo por $p_1$ para obter

$$\begin{array}{rclr} a_2 - x_1 &\equiv& x_2 p_1 &\pmod{p_2} \\ (a_2 - x_1) r_{12} &\equiv& x_2 &\pmod{p_2} \\ x_2 &\equiv& (a_2 - x_1) r_{12} &\pmod{p_2} \end{array}$$

Da mesma forma, obtemos que

$$x_3 \equiv ((a_3 - x_1) r_{13} - x_2) r_{23} \pmod{p_3}.$$

Agora, podemos ver claramente um padrão emergente, que pode ser expresso pelo seguinte código:

```cpp
for (int i = 0; i < k; ++i) {
    x[i] = a[i];
    for (int j = 0; j < i; ++j) {
        x[i] = r[j][i] * (x[i] - x[j]);

        x[i] = x[i] % p[i];
        if (x[i] < 0)
            x[i] += p[i];
    }
}
```

Então, aprendemos como calcular os dígitos $x_i$ em $O(k^2)$ tempo. O número $a$ agora pode ser calculado usando a fórmula mencionada anteriormente:

$$a = x_1 + x_2 \cdot p_1 + x_3 \cdot p_1 \cdot p_2 + \ldots + x_k \cdot p_1 \cdots p_{k-1}$$

Vale ressaltar que, na prática, provavelmente precisaremos calcular a resposta $a$ usando Aritmética de Precisão Arbitrária, mas os dígitos $x_i$ (porque são pequenos) geralmente podem ser calculados usando tipos incorporados, e, portanto, o Algoritmo de Garner é muito eficiente.

## Implementação do Algoritmo de Garner
É conveniente implementar este algoritmo usando Java, pois possui suporte embutido para números grandes por meio da classe BigInteger.

Aqui mostramos uma implementação que pode armazenar números grandes na forma de um conjunto de equações de congruência. Ele suporta adição, subtração e multiplicação. E com o algoritmo de Garner, podemos converter o conjunto de equações no número inteiro único. Neste código, usamos 100 números primos maiores que $10^9$, o que permite representar números tão grandes quanto $10^{900}$.

```java
import java.math.BigInteger;

public class GarnerAlgorithm {
    final int SZ = 100;
    int pr[] = new int[SZ];
    int r[][] = new int[SZ][SZ];

    public void init() {
        for (int x = 1000 * 1000 * 1000, i = 0; i < SZ; ++x)
            if (BigInteger.valueOf(x).isProbablePrime(100))
                pr[i++] = x;

        for (int i = 0; i < SZ; ++i)
            for (int j = i + 1; j < SZ; ++j)
                r[i][j] =
                    BigInteger.valueOf(pr[i]).modInverse(BigInteger.valueOf(pr[j])).intValue();
    }

    public class Number {
        int a[] = new int[SZ];

        public Number() {
        }

        public Number(int n) {
            for (int i = 0; i < SZ; ++i)
                a[i] = n % pr[i];
        }

        public Number(BigInteger n) {
            for (int i = 0; i < SZ; ++i)
                a[i] = n.mod(BigInteger.valueOf(pr[i])).intValue();
        }

        public Number add(Number n) {
            Number result = new Number();
            for (int i = 0; i < SZ; ++i)
                result.a[i] = (a[i] + n.a[i]) % pr[i];
            return result;
        }

        public Number subtract(Number n) {
            Number result = new Number();
            for (int i = 0; i < SZ; ++i)
                result.a[i] = (a[i] - n.a[i] + pr[i]) % pr[i];
            return result;
        }

        public Number multiply(Number n) {
            Number result = new Number();
            for (int i = 0; i < SZ; ++i)
                result.a[i] = (int)((a[i] * 1L * n.a[i]) % pr[i]);
            return result;
        }

        public BigInteger bigIntegerValue(boolean can_be_negative) {
            BigInteger result = BigInteger.ZERO, mult = BigInteger.ONE;
            int x[] = new int[SZ];
            for (int i = 0; i < SZ; ++i) {
                x[i] = a[i];
                for (int j = 0; j < i; ++j) {
                    long cur = (x[i] - x[j]) * 1L * r[j][i];
                    x[i] = (int)((cur % pr[i] + pr[i]) % pr[i]);
                }
                result = result.add(mult.multiply(BigInteger.valueOf(x[i])));
                mult = mult.multiply(BigInteger.valueOf(pr[i]));
            }

            if (can_be_negative)
                if (result.compareTo(mult.shiftRight(1)) >= 0)
                    result = result.subtract(mult);

            return result;
        }
    }
}
```
