
Existe uma versão menos conhecida da última equivalência, que permite calcular  
$x^n \bmod m$  de forma eficiente para  $x$  e  $m$  não coprimos. Para  $x, m$  arbitrários e  $n \geq \log_2 m$ :

 
$$x^{n}\equiv x^{\phi(m)+[n \bmod \phi(m)]} \mod m$$ 
Prova:

Sejam  $p_1, \dots, p_t$  os divisores primos comuns de $x$  e  $m$ , e  $k_i$  seus expoentes em  $m$ . Com esses, definimos  $a = p_1^{k_1} \dots p_t^{k_t}$ , o que faz  $\frac{m}{a}$  ser coprimo a  $x$ . E seja  $k$  o menor número tal que  $a$  divide  $x^k$ . Supondo  $n \ge k$ , podemos escrever:
$$\begin{align}x^n \bmod m &= \frac{x^k}{a}ax^{n-k}\bmod m \\ &= \frac{x^k}{a}\left(ax^{n-k}\bmod m\right) \bmod m \\ &= \frac{x^k}{a}\left(ax^{n-k}\bmod a \frac{m}{a}\right) \bmod m \\ &=\frac{x^k}{a} a \left(x^{n-k} \bmod \frac{m}{a}\right)\bmod m \\ &= x^k\left(x^{n-k} \bmod \frac{m}{a}\right)\bmod m \end{align}$$ 
A equivalência entre a terceira e a quarta linha segue do fato de que  $ab \bmod ac = a(b \bmod c)$ . De fato, se  $b = cd + r$  com  $r < c$ , então  $ab = acd + ar$  com  $ar < ac$ .

Como  $x$  e  $\frac{m}{a}$  são coprimos, podemos aplicar o teorema de Euler e obter a fórmula eficiente (já que  $k$  é muito pequeno; de fato $k \le \log_2 m$ ):
$$x^n \bmod m = x^k\left(x^{n-k \bmod \phi(\frac{m}{a})} \bmod \frac{m}{a}\right)\bmod m.$$ 
Esta fórmula é difícil de aplicar, mas podemos usá-la para analisar o comportamento de  $x^n \bmod m$ . Podemos ver que a sequência de potências  
$(x^1 \bmod m, x^2 \bmod m, x^3 \bmod m, \dots)$  entra em um ciclo de comprimento  $\phi\left(\frac{m}{a}\right)$  após os primeiros  $k$  (ou menos) elementos. $\phi\left(\frac{m}{a}\right)$  divide  $\phi(m)$  (porque
$a$  e $\frac{m}{a}$  são coprimos temos $\phi(a) \cdot \phi\left(\frac{m}{a}\right) = \phi(m)$ ), portanto, também podemos dizer que o período tem comprimento  $\phi(m)$ . E como $\phi(m) \ge \log_2 m \ge k$ , podemos concluir a fórmula desejada, muito mais simples:
$$ x^n \equiv x^{\phi(m)} x^{(n - \phi(m)) \bmod \phi(m)} \bmod m \equiv x^{\phi(m)+[n \bmod \phi(m)]} \mod m.$$

