
Se quisermos calcular um coeficiente binomial módulo  $p$ , então precisamos adicionalmente da multiplicidade do  $p$  em  $n$ , ou seja, o número de vezes que  $p$  ocorre na fatoração prima de  $n$ , ou o número de vezes que apagamos  $p$  durante o cálculo do fatorial modificado.

A fórmula de Legendre nos dá uma maneira de calcular isso em $O(\log_p n)$  tempo. A fórmula fornece a multiplicidade  $\nu_p$  como:
$$\nu_p(n!) = \sum_{i=1}^{\infty} \left\lfloor \frac{n}{p^i} \right\rfloor$$ 
Assim, obtemos a implementação:

```cpp
int multiplicity_factorial(int n, int p) {
    int count = 0;
    do {
        n /= p;
        count += n;
    } while (n);
    return count;
}
```

Esta fórmula pode ser facilmente comprovada usando as mesmas ideias que utilizamos nas seções anteriores. Remova todos os elementos que não contêm o fator  $p$ . Isso deixa  $\lfloor n/p \rfloor$  elementos restantes. Se removermos o fator  $p$  de cada um deles, obtemos o produto  $1 \cdot 2 \cdots \lfloor n/p \rfloor = \lfloor n/p \rfloor !$ , e novamente temos uma recursão.