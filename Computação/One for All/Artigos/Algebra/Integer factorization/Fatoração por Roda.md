
Esta é uma otimização da divisão de teste. A ideia é a seguinte. Uma vez que sabemos que o número não é divisível por 2, não precisamos verificar todos os outros números pares. Isso nos deixa com apenas  
$50\%$  dos números para verificar. Depois de verificar 2, podemos simplesmente começar com 3 e pular todos os outros números.

```cpp
vector<long long> trial_division2(long long n) {
    vector<long long> factorization;
    while (n % 2 == 0) {
        factorization.push_back(2);
        n /= 2;
    }
    for (long long d = 3; d * d <= n; d += 2) {
        while (n % d == 0) {
            factorization.push_back(d);
            n /= d;
        }
    }
    if (n > 1)
        factorization.push_back(n);
    return factorization;
}
```
Este método pode ser estendido. Se o número não for divisível por 3, também podemos ignorar todos os outros múltiplos de 3 nos cálculos futuros. Então, só precisamos verificar os números  
$5, 7, 11, 13, 17, 19, 23, \dots$ . Podemos observar um padrão desses números restantes. Precisamos verificar todos os números com  
$d \bmod 6 = 1$  e  
$d \bmod 6 = 5$ . Então, isso nos deixa com apenas  
$33.3\%$  por cento dos números para verificar. Podemos implementar isso verificando os primos 2 e 3 primeiro, e então começar a verificar com 5 e alternativamente pular 1 ou 3 números.

Podemos estender isso ainda mais. Aqui está uma implementação para o número primo 2, 3 e 5. É conveniente usar uma matriz para armazenar quanto temos que pular.

```cpp
vector<long long> trial_division3(long long n) {
    vector<long long> factorization;
    for (int d : {2, 3, 5}) {
        while (n % d == 0) {
            factorization.push_back(d);
            n /= d;
        }
    }
    static array<int, 8> increments = {4, 2, 4, 2, 4, 6, 2, 6};
    int i = 0;
    for (long long d = 7; d * d <= n; d += increments[i++]) {
        while (n % d == 0) {
            factorization.push_back(d);
            n /= d;
        }
        if (i == 8)
            i = 0;
    }
    if (n > 1)
        factorization.push_back(n);
    return factorization;
}
```
Se estendermos isso ainda mais com mais primos, podemos até alcançar melhores porcentagens. No entanto, as listas de pulo também ficarão muito maiores.