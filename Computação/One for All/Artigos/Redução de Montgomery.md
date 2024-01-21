
A multiplicação de dois números no espaço de Montgomery requer um cálculo eficiente de  
$x \cdot r^{-1} \bmod n$ . Essa operação é chamada de redução de Montgomery e também é conhecida como o algoritmo REDC.

Como  $\gcd(n, r) = 1$ , sabemos que existem dois números  $r^{-1}$  e  $n^{\prime}$  com  $0 < r^{-1}, n^{\prime} < n$ , com
$$r \cdot r^{-1} + n \cdot n^{\prime} = 1.$$ 
Ambos  $r^{-1}$  e  $n^{\prime}$  podem ser calculados usando o [algoritmo estendido de Euclides].

Usando essa identidade, podemos escrever  $x \cdot r^{-1}$  como:
 
$$\begin{aligned} x \cdot r^{-1} &= x \cdot r \cdot r^{-1} / r = x \cdot (-n \cdot n^{\prime} + 1) / r \\ &= (-x \cdot n \cdot n^{\prime} + x) / r \equiv (-x \cdot n \cdot n^{\prime} + l \cdot r \cdot n + x) / r \bmod n\\ &\equiv ((-x \cdot n^{\prime} + l \cdot r) \cdot n + x) / r \bmod n \end{aligned}$$ 
As equivalências valem para qualquer número inteiro arbitrário  $l$ . Isso significa que podemos adicionar ou subtrair um múltiplo arbitrário de  $r$  a  $x \cdot n^{\prime}$ , ou em outras palavras, podemos calcular  $q := x \cdot n^{\prime}$  módulo  $r$ .

Isso nos dá o seguinte algoritmo para calcular  $x \cdot r^{-1} \bmod n$ :

```python
def reduce(x):
    q = (x % r) * n_prime % r
    a = (x - q * n) // r
    if a < 0:
        a += n
    return a
```

Como  $x < n \cdot n < r \cdot n$  (mesmo se  $x$  for o produto de uma multiplicação) e  $q \cdot n < r \cdot n$ , sabemos que  $-n < (x - q \cdot n) / r < n$ . Portanto, a operação final de módulo é implementada usando uma única verificação e uma adição.

Como vemos, podemos realizar a redução de Montgomery sem nenhuma operação de módulo pesada. Se escolhermos  $r$  como uma potência de  $2$ , as operações de módulo e divisões no algoritmo podem ser calculadas usando mascaramento e deslocamento de bits.

Uma segunda aplicação da redução de Montgomery é transferir um número de volta do espaço de Montgomery para o espaço normal.