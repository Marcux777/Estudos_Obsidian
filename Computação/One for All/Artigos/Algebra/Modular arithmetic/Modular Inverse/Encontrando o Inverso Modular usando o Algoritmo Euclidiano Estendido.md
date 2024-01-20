
Considere a seguinte equação (com  $x$  e  $y$  desconhecidos):
$$a \cdot x + m \cdot y = 1$$ 
Esta é uma equação diofantina linear em duas variáveis. Como mostrado no artigo vinculado, quando  $\gcd(a, m) = 1$ , a equação tem uma solução que pode ser encontrada usando o algoritmo euclidiano estendido. Note que  $\gcd(a, m) = 1$  também é a condição para o inverso modular existir.

Agora, se tomarmos o módulo  $m$  de ambos os lados, podemos nos livrar de  $m \cdot y$ , e a equação se torna:
$$a \cdot x \equiv 1 \mod m$$ 
Assim, o inverso modular de  $a$  é  $x$ .

A implementação é a seguinte:

```c++
int x, y;
int g = extended_euclidean(a, m, x, y);
if (g != 1) {
    cout << "No solution!";
}
else {
    x = (x % m + m) % m;
    cout << x << endl;
}
```
Observe a maneira como modificamos x. O x resultante do algoritmo euclidiano estendido pode ser negativo, então x % m também pode ser negativo, e primeiro temos que adicionar m para torná-lo positivo.