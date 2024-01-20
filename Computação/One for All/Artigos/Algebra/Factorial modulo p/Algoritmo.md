Vamos escrever este fatorial modificado explicitamente.

$$
\begin{eqnarray}
n!_{\%p} &=& 1 \cdot 2 \cdot 3 \cdot \ldots \cdot (p-2) \cdot (p-1) \cdot \underbrace{1}_{p} \cdot (p+1) \cdot (p+2) \cdot \ldots \cdot (2p-1) \cdot \underbrace{2}_{2p} \\\
 & &\quad \cdot (2p+1) \cdot \ldots \cdot (p^2-1) \cdot \underbrace{1}_{p^2} \cdot (p^2 +1) \cdot \ldots \cdot n \pmod{p} \\\\
&=& 1 \cdot 2 \cdot 3 \cdot \ldots \cdot (p-2) \cdot (p-1) \cdot \underbrace{1}_{p} \cdot 1 \cdot 2 \cdot \ldots \cdot (p-1) \cdot \underbrace{2}_{2p} \cdot 1 \cdot 2 \\\
& &\quad \cdot \ldots \cdot (p-1) \cdot \underbrace{1}_{p^2} \cdot 1 \cdot 2 \cdot \ldots \cdot (n \bmod p) \pmod{p}
\end{eqnarray}

$$

Claramente, pode-se ver que o fatorial é dividido em vários blocos de mesmo comprimento, exceto pelo último.
$$
\begin{eqnarray}
n!_{\%p}&=& \underbrace{1 \cdot 2 \cdot 3 \cdot \ldots \cdot (p-2) \cdot (p-1) \cdot 1}_{1\text{st}} \cdot \underbrace{1 \cdot 2 \cdot 3 \cdot \ldots \cdot (p-2) \cdot (p-1) \cdot 2}_{2\text{nd}} \cdot \ldots \\\\
& & \cdot \underbrace{1 \cdot 2 \cdot 3 \cdot \ldots \cdot (p-2) \cdot (p-1) \cdot 1}_{p\text{th}} \cdot \ldots \cdot \quad \underbrace{1 \cdot 2 \cdot \cdot \ldots \cdot (n \bmod p)}_{\text{tail}} \pmod{p}.
\end{eqnarray}
$$
A parte principal dos blocos é fácil de contar - é apenas  $(p-1)!\ \mathrm{mod}\ p$ . Podemos calcular isso programaticamente ou simplesmente aplicar o teorema de Wilson, que afirma que  $(p-1)! \bmod p = -1$  para qualquer número primo  $p$ .

Temos exatamente  $\lfloor \frac{n}{p} \rfloor$  desses blocos, portanto precisamos elevar  $-1$  à potência de  $\lfloor \frac{n}{p} \rfloor$ . Isso pode ser feito em tempo logarítmico usando Exponenciação Binária; no entanto, você também pode notar que o resultado alternará entre  $-1$  e  $1$ , então só precisamos olhar para a paridade do expoente e multiplicar por  $-1$  se a paridade for ímpar. E em vez de uma multiplicação, também podemos apenas subtrair o resultado atual de  $p$ .

O valor do último bloco parcial pode ser calculado separadamente em  
$O(p)$ .

Isso deixa apenas o último elemento de cada bloco. Se escondermos os elementos já tratados, podemos ver o seguinte padrão:

$$n!_{\%p} = \underbrace{ \ldots \cdot 1 } \cdot \underbrace{ \ldots \cdot 2} \cdot \ldots \cdot \underbrace{ \ldots \cdot (p-1)} \cdot \underbrace{ \ldots \cdot 1 } \cdot \underbrace{ \ldots \cdot 1} \cdot \underbrace{ \ldots \cdot 2} \cdots$$

Isso novamente é um fatorial modificado, mas com uma dimensão muito menor. É  
$\lfloor n / p \rfloor !_{\%p}$ .

Assim, durante o cálculo do fatorial modificado  $n\!_{\%p}$ , realizamos  $O(p)$  operações e restamos com o cálculo de  $\lfloor n / p \rfloor !_{\%p}$ . Temos uma fórmula recursiva. A profundidade da recursão é  $O(\log_p n)$  e, portanto, o comportamento assintótico completo do algoritmo é  $O(p \log_p n)$ .

Observe que, se você pré-calcular os fatoriais  $0!,~ 1!,~ 2!,~ \dots,~ (p-1)!$  módulo  $p$ , então a complexidade será apenas  $O(\log_p n)$ .

