
Este é o algoritmo mais básico para encontrar uma fatoração prima.

Dividimos por cada divisor possível  $d$ . Podemos notar que é impossível que todos os fatores primos de um número composto  $n$  sejam maiores que  $\sqrt{n}$ . Portanto, só precisamos testar os divisores  $2 \le d \le \sqrt{n}$ , o que nos dá a fatoração prima em $O(\sqrt{n})$ . (Este é o [[tempo pseudo-polinomial]], ou seja, polinomial no valor da entrada, mas exponencial no número de bits da entrada.)

O menor divisor tem que ser um número primo. Removemos o fator do número e repetimos o processo. Se não conseguirmos encontrar nenhum divisor no intervalo  
$[2; \sqrt{n}]$ , então o próprio número deve ser primo.

```cpp
vector<long long> trial_division1(long long n) {
    vector<long long> factorization;
    for (long long d = 2; d * d <= n; d++) {
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
Este é um exemplo de implementação do algoritmo de divisão de teste para encontrar a fatoração prima de um número. Ele divide o número por cada divisor possível e verifica se o número é divisível por ele. Se for, o divisor é adicionado à fatoração e o número é dividido por ele. O processo é repetido até que não se possa encontrar mais divisores. Se o número restante for maior que 1, ele é adicionado à fatoração, pois deve ser um número primo. O algoritmo tem complexidade de tempo $O(\sqrt{n})$, o que o torna eficiente para números pequenos, mas menos eficiente para números muito grandes.

[[Fatoração por Roda]]
[[Primos Pré-computados]]
