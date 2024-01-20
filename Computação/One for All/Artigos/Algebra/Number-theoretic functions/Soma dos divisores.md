Podemos usar o mesmo argumento da seção anterior.

Se houver apenas um divisor primo distinto $n = p_1^{e_1}$ , então a soma é:
$$1 + p_1 + p_1^2 + \dots + p_1^{e_1} = \frac{p_1^{e_1 + 1} - 1}{p_1 - 1}$$ 
Se houver dois divisores primos distintos  $n = p_1^{e_1} \cdot p_2^{e_2}$ , então podemos fazer a mesma tabela de antes. A única diferença é que agora queremos calcular a soma em vez de contar os elementos. É fácil ver que a soma de cada combinação pode ser expressa como:
 
$$\left(1 + p_1 + p_1^2 + \dots + p_1^{e_1}\right) \cdot \left(1 + p_2 + p_2^2 + \dots + p_2^{e_2}\right)$$
$$ = \frac{p_1^{e_1 + 1} - 1}{p_1 - 1} \cdot \frac{p_2^{e_2 + 1} - 1}{p_2 - 1}$$ 
Em geral, para  $n = p_1^{e_1} \cdot p_2^{e_2} \cdots p_k^{e_k}$  recebemos a fórmula:
 
$$\sigma(n) = \frac{p_1^{e_1 + 1} - 1}{p_1 - 1} \cdot \frac{p_2^{e_2 + 1} - 1}{p_2 - 1} \cdots \frac{p_k^{e_k + 1} - 1}{p_k - 1}$$ 
```c++
long long SumOfDivisors(long long num) {
    long long total = 1;

    for (int i = 2; (long long)i * i <= num; i++) {
        if (num % i == 0) {
            int e = 0;
            do {
                e++;
                num /= i;
            } while (num % i == 0);

            long long sum = 0, pow = 1;
            do {
                sum += pow;
                pow *= i;
            } while (e-- > 0);
            total *= sum;
        }
    }
    if (num > 1) {
        total *= (1 + num);
    }
    return total;
}
```