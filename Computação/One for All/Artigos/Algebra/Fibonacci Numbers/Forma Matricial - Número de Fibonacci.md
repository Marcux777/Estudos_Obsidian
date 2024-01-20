É fácil provar a seguinte relação:

$$\begin{pmatrix} 1 & 1 \cr 1 & 0 \cr\end{pmatrix} ^ n = \begin{pmatrix} F_{n+1} & F_{n} \cr F_{n} & F_{n-1} \cr\end{pmatrix}$$
Assim, para encontrar $F_n$ em tempo $O(\log n)$, devemos elevar a matriz a n. (Veja Exponenciação Binária)

```cpp
struct matrix {
    long long mat[2][2];
    matrix friend operator *(const matrix &a, const matrix &b){
        matrix c;
        for (int i = 0; i < 2; i++) {
          for (int j = 0; j < 2; j++) {
              c.mat[i][j] = 0;
              for (int k = 0; k < 2; k++) {
                  c.mat[i][j] += a.mat[i][k] * b.mat[k][j];
              }
          }
        }
        return c;
    }
};

matrix matpow(matrix base, long long n) {
    matrix ans{ {
      {1, 0},
      {0, 1}
    } };
    while (n) {
        if(n&1)
            ans = ans*base;
        base = base*base;
        n >>= 1;
    }
    return ans;
}

long long fib(int n) {
    matrix base{ {
      {1, 1},
      {1, 0}
    } };
    return matpow(base, n).mat[0][1];
}
```

# Método de Duplicação Rápida
Expandindo a expressão matricial acima para $n = 2\cdot k$

$$ \begin{pmatrix} F_{2k+1} & F_{2k}\\ F_{2k} & F_{2k-1} \end{pmatrix} = \begin{pmatrix} 1 & 1\\ 1 & 0 \end{pmatrix}^{2k} = \begin{pmatrix} F_{k+1} & F_{k}\\ F_{k} & F_{k-1} \end{pmatrix} ^2 $$
podemos encontrar estas equações mais simples:

$$ \begin{align} F_{2k+1} &= F_{k+1}^2 + F_{k}^2 \\ F_{2k} &= F_k(F_{k+1}+F_{k-1}) = F_k (2F_{k+1} - F_{k})\\ \end{align}.$$
Assim, usando as duas equações acima, os números de Fibonacci podem ser facilmente calculados pelo seguinte código:

```cpp
pair<int, int> fib (int n) {
    if (n == 0)
        return {0, 1};

    auto p = fib(n >> 1);
    int c = p.first * (2 * p.second - p.first);
    int d = p.first * p.first + p.second * p.second;
    if (n & 1)
        return {d, c + d};
    else
        return {c, d};
}
```
O código acima retorna $F_n$ e $F_{n+1}$ como um par.
