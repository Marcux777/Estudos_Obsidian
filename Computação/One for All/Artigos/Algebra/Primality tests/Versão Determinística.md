
Miller mostrou que é possível tornar o algoritmo determinístico apenas verificando todas as bases  $\le O((\ln n)^2)$ . Bach mais tarde deu um limite concreto, só é necessário testar todas as bases  $a \le 2 \ln(n)^2$ .

Este ainda é um número bastante grande de bases. Então, as pessoas investiram bastante poder de computação para encontrar limites inferiores. Acontece que, para testar um inteiro de 32 bits, só é necessário verificar as primeiras 4 bases primas: 2, 3, 5 e 7. O menor número composto que falha neste teste é  $3,215,031,751 = 151 \cdot 751 \cdot 28351$ . E para testar um inteiro de 64 bits, basta verificar as primeiras 12 bases primas: 2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31 e 37.

Isso resulta na seguinte implementação determinística:

```cpp
bool MillerRabin(u64 n) { // retorna verdadeiro se n é primo, caso contrário, retorna falso.
    if (n < 2)
        return false;

    int r = 0;
    u64 d = n - 1;
    while ((d & 1) == 0) {
        d >>= 1;
        r++;
    }

    for (int a : {2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37}) {
        if (n == a)
            return true;
        if (check_composite(n, a, d, r))
            return false;
    }
    return true;
}
```
Também é possível fazer a verificação com apenas 7 bases: 2, 325, 9375, 28178, 450775, 9780504 e 1795265022. No entanto, como esses números (exceto 2) não são primos, você precisa verificar adicionalmente se o número que você está verificando é igual a qualquer divisor primo dessas bases: 2, 3, 5, 13, 19, 73, 193, 407521, 299210837.