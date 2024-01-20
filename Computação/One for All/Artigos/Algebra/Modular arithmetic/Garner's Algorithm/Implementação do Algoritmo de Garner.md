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
