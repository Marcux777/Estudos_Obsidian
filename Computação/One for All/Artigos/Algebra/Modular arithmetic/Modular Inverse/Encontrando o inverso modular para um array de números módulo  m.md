
Suponha que nos é dado um array e queremos encontrar o inverso modular para todos os números nele (todos eles são invertíveis). Em vez de calcular o inverso para cada número, podemos expandir a fração pelo produto do prefixo (excluindo-se) e produto do sufixo (excluindo-se), e acabamos calculando apenas um único inverso.
$$ \begin{align} x_i^{-1} &= \frac{1}{x_i} = \frac{\overbrace{x_1 \cdot x_2 \cdots x_{i-1}}^{\text{prefixo}_{i-1}} \cdot ~1~ \cdot \overbrace{x_{i+1} \cdot x_{i+2} \cdots x_n}^{\text{sufixo}_{i+1}}}{x_1 \cdot x_2 \cdots x_{i-1} \cdot x_i \cdot x_{i+1} \cdot x_{i+2} \cdots x_n} \\ &= \text{prefixo}_{i-1} \cdot \text{sufixo}_{i+1} \cdot \left(x_1 \cdot x_2 \cdots x_n\right)^{-1} \end{align} $$ 
No código, podemos apenas fazer um array de produto de prefixo (excluindo-se, começando pelo elemento identidade), calcular o inverso modular para o produto de todos os números e então multiplicá-lo pelo produto de prefixo e produto de sufixo (excluindo-se). O produto de sufixo é calculado iterando de trás para frente.

```c++
std::vector<int> invs(const std::vector<int> &a, int m) {
    int n = a.size();
    if (n == 0) return {};
    std::vector<int> b(n);
    int v = 1;
    for (int i = 0; i != n; ++i) {
        b[i] = v;
        v = static_cast<long long>(v) * a[i] % m;
    }
    int x, y;
    extended_euclidean(v, m, x, y);
    x = (x % m + m) % m;
    for (int i = n - 1; i >= 0; --i) {
        b[i] = static_cast<long long>(x) * b[i] % m;
        x = static_cast<long long>(x) * a[i] % m;
    }
    return b;
}
```