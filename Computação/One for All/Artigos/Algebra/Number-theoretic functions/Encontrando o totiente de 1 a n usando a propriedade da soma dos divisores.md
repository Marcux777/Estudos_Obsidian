A propriedade da soma dos divisores também nos permite calcular o totiente de todos os números entre 1 e  $n$ . Esta implementação é um pouco mais simples do que a implementação anterior baseada no Crivo de Eratóstenes, no entanto, tem uma complexidade um pouco pior:  $O(n \log n)$ 

```c++
void phi_1_to_n(int n) {
    vector<int> phi(n + 1);
    phi[0] = 0;
    phi[1] = 1;
    for (int i = 2; i <= n; i++)
        phi[i] = i - 1;

    for (int i = 2; i <= n; i++)
        for (int j = 2 * i; j <= n; j += i)
              phi[j] -= phi[i];
}
```
