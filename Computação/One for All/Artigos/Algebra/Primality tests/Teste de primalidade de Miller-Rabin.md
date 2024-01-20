
O teste de Miller-Rabin estende as ideias do teste de Fermat.

Para um número ímpar  
$n$ ,  $n-1$  é par e podemos fatorar todas as potências de 2. Podemos escrever:

$$n - 1 = 2^s \cdot d,~\text{com}~d~\text{ímpar}.$$ 
Isso nos permite fatorar a equação do pequeno teorema de Fermat:
 
$$\begin{array}{rl} a^{n-1} \equiv 1 \bmod n &\Longleftrightarrow a^{2^s d} - 1 \equiv 0 \bmod n \\\\ &\Longleftrightarrow (a^{2^{s-1} d} + 1) (a^{2^{s-1} d} - 1) \equiv 0 \bmod n \\\\ &\Longleftrightarrow (a^{2^{s-1} d} + 1) (a^{2^{s-2} d} + 1) (a^{2^{s-2} d} - 1) \equiv 0 \bmod n \\\\ &\quad\vdots \\\\ &\Longleftrightarrow (a^{2^{s-1} d} + 1) (a^{2^{s-2} d} + 1) \cdots (a^{d} + 1) (a^{d} - 1) \equiv 0 \bmod n \\\\ \end{array}$$ 
Se  $n$  é primo, então  $n$  tem que dividir um desses fatores. E no teste de primalidade de Miller-Rabin, verificamos exatamente essa afirmação, que é uma versão mais rigorosa da afirmação do teste de Fermat. Para uma base  $2 \le a \le n-2$ , verificamos se

$$a^d \equiv 1 \bmod n$$ 
é válido ou
 
$$a^{2^r d} \equiv -1 \bmod n$$ 
é válido para algum  $0 \le r \le s - 1$ .

Se encontrarmos uma base  $a$  que não satisfaça nenhuma das igualdades acima, então encontramos uma testemunha para a composição de  $n$ . Neste caso, provamos que  $n$  não é um número primo.

Semelhante ao teste de Fermat, também é possível que o conjunto de equações seja satisfeito para um número composto. Nesse caso, a base  $a$  é chamada de forte mentirosa. Se uma base  $a$  satisfaz as equações (uma delas),  $n$  é apenas um forte provável primo. No entanto, não existem números como os números de Carmichael, onde todas as bases não triviais mentem. Na verdade, é possível mostrar que, no máximo,  $\frac{1}{4}$  das bases podem ser fortes mentirosas. Se  $n$  é composto, temos uma probabilidade de  $\ge 75\%$  de que uma base aleatória nos dirá que é composto. Ao fazer várias iterações, escolhendo diferentes bases aleatórias, podemos dizer com muita probabilidade se o número é realmente primo ou se é composto.

Aqui está uma implementação para inteiros de 64 bits.

```cpp
using u64 = uint64_t;
using u128 = __uint128_t;

u64 binpower(u64 base, u64 e, u64 mod) {
    u64 result = 1;
    base %= mod;
    while (e) {
        if (e & 1)
            result = (u128)result * base % mod;
        base = (u128)base * base % mod;
        e >>= 1;
    }
    return result;
}

bool check_composite(u64 n, u64 a, u64 d, int s) {
    u64 x = binpower(a, d, n);
    if (x == 1 || x == n - 1)
        return false;
    for (int r = 1; r < s; r++) {
        x = (u128)x * x % n;
        if (x == n - 1)
            return false;
    }
    return true;
};

bool MillerRabin(u64 n, int iter=5) { // retorna verdadeiro se n é provavelmente primo, caso contrário, retorna falso.
    if (n < 4)
        return n == 2 || n == 3;

    int s = 0;
    u64 d = n - 1;
    while ((d & 1) == 0) {
        d >>= 1;
        s++;
    }

    for (int i = 0; i < iter; i++) {
        int a = 2 + rand() % (n - 3);
        if (check_composite(n, a, d, s))
            return false;
    }
    return true;
}
```
Antes do teste de Miller-Rabin, você pode testar adicionalmente se um dos primeiros números primos é um divisor. Isso pode acelerar muito o teste, já que a maioria dos números compostos tem divisores primos muito pequenos. Por exemplo,  $88\%$  de todos os números têm um fator primo menor que  $100$ .

[[Versão Determinística]]
