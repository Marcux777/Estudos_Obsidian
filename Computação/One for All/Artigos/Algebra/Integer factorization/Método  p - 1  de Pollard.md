
É muito provável que pelo menos um fator de um número seja  $B$ -powersmooth para pequenos  $B$ .  
$B$ -powersmooth significa que cada potência prima  $d^k$  que divide  $p-1$  é no máximo  $B$ . Por exemplo, a fatoração prima de  $4817191$  é $1303 \cdot 3697$ . E os fatores são respectivamente  $31$ -powersmooth e $16$ -powersmooth, porque  
$1303 - 1 = 2 \cdot 3 \cdot 7 \cdot 31$  e  $3697 - 1 = 2^4 \cdot 3 \cdot 7 \cdot 11$ . Em 1974, John Pollard inventou um método para extrair fatores  $B$ -powersmooth de um número composto.

A ideia vem do [[pequeno teorema de Fermat]]. Seja uma fatoração de  $n$  como  $n = p \cdot q$ . Ele diz que se  $a$  é coprimo com  $p$ , a seguinte afirmação é válida:

$$a^{p - 1} \equiv 1 \pmod{p}$$ 
Isso também significa que
$$a^{(p - 1)^k} \equiv a^{k \cdot (p - 1)} \equiv 1 \pmod{p}.$$ 
Portanto, para qualquer $M$  com  $p - 1 ~|~ M$  sabemos que  $a^M \equiv 1$ . Isso significa que  $a^M - 1 = p \cdot r$ , e por causa disso também  $p ~|~ \gcd(a^M - 1, n)$ .

Portanto, se  $p - 1$  para um fator $p$  de  $n$  divide  $M$ , podemos extrair um fator usando o [algoritmo de Euclides](obsidian://open?vault=Estudos_Obsidian&file=Computa%C3%A7%C3%A3o%2FOne%20for%20All%2FArtigos%2FAlgebra%2FAlgoritmo%20de%20Euclides%20para%20calcular%20o%20maior%20divisor%20comum%2FAlgoritmo%20-%20Algoritmo%20de%20Euclides%20para%20calcular%20o%20maior%20divisor%20comum).

É claro que o menor  $M$  que é um múltiplo de todo número  $B$ -powersmooth é  $\text{lcm}(1,~2~,3~,4~,~\dots,~B)$ . Ou alternativamente:
 
$$M = \prod_{\text{primo } q \le B} q^{\lfloor \log_q B \rfloor}$$ 
Note que, se  $p-1$  divide  $M$  para todos os fatores primos  $p$  de  $n$ , então  $\gcd(a^M - 1, n)$  será apenas  $n$ . Neste caso, não recebemos um fator. Portanto, tentaremos realizar o  
$\gcd$  várias vezes, enquanto calculamos  $M$ .

Alguns números compostos não têm fatores  
$B$ -powersmooth para pequenos  
$B$ . Por exemplo, os fatores do número composto  
$100~000~000~000~000~493 = 763~013 \cdot 131~059~365~961$  são  $190~753$ -powersmooth e  
$1~092~161~383$ -powersmooth. Teríamos que escolher $B >= 190~753$  para fatorar o número.

Na seguinte implementação, começamos com  $B = 10$  e aumentamos  $B$  após cada iteração.

```cpp
long long pollards_p_minus_1(long long n) {
    int B = 10;
    long long g = 1;
    while (B <= 1000000 && g < n) {
        long long a = 2 + rand() %  (n - 3);
        g = gcd(a, n);
        if (g > 1)
            return g;

        // compute a^M
        for (int p : primes) {
            if (p >= B)
                continue;
            long long p_power = 1;
            while (p_power * p <= B)
                p_power *= p;
            a = power(a, p_power, n);

            g = gcd(a - 1, n);
            if (g > 1 && g < n)
                return g;
        }
        B *= 2;
    }
    return 1;
}
```
Note que, este é um algoritmo probabilístico. Pode acontecer que o algoritmo não encontre um fator.

A complexidade é  $O(B \log B \log^2 n)$  por iteração.
