
Dado um módulo primo  $m > a$  (ou podemos aplicar o módulo para torná-lo menor em 1 passo), de acordo com a [Divisão Euclidiana](https://en.wikipedia.org/wiki/Euclidean_division)
$$m = k \cdot a + r$$ 
onde $k = \left\lfloor \frac{m}{a} \right\rfloor$  e  $r = m \bmod a$ , então
$$ \begin{align*} & \implies & 0 & \equiv k \cdot a + r & \mod m \\ & \iff & r & \equiv -k \cdot a & \mod m \\ & \iff & r \cdot a^{-1} & \equiv -k & \mod m \\ & \iff & a^{-1} & \equiv -k \cdot r^{-1} & \mod m \end{align*} $$ 
Note que este raciocínio não se mantém se  $m$  não for primo, pois a existência de  $a^{-1}$  não implica a existência de  $r^{-1}$  no caso geral. Para ver isso, vamos tentar calcular  $5^{-1}$  módulo  $12$  com a fórmula acima. Gostaríamos de chegar a  $5$ , já que  $5 \cdot 5 \equiv 1 \bmod 12$ . No entanto,  $12 = 2 \cdot 5 + 2$ , e temos  $k=2$  e  $r=2$ , com  $2$  não sendo invertível módulo  $12$ .

No entanto, se o módulo for primo, todos  $a$  com  $0 < a < m$  são invertíveis módulo  $m$ , e podemos ter a seguinte função recursiva (em C++) para calcular o inverso modular para o número  $a$  em relação a  $m$ 

```c++
int inv(int a) {
  return a <= 1 ? a : m - (long long)(m/a) * inv(m % a) % m;
}
```
A complexidade exata do tempo desta recursão não é conhecida. Está em algum lugar entre $O(\frac{\log m}{\log\log m})$  e   $O(m^{\frac{1}{3} - \frac{2}{177} + \epsilon})$ . Veja Sobre o [comprimento das expansões de Pierce](https://arxiv.org/abs/2211.08374). Na prática, esta implementação é rápida, por exemplo, para o módulo  $10^9 + 7$  sempre terminará em menos de 50 iterações.

Aplicando esta fórmula, também podemos pré-calcular o inverso modular para cada número no intervalo  $[1, m-1]$  em  $O(m)$ .

```c++
inv[1] = 1;
for(int a = 2; a < m; ++a)
    inv[a] = m - (long long)(m/a) * inv[m%a] % m;
```
