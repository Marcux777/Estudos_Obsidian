
Elevar $a$ à potência de $n$ é expresso de forma ingênua como multiplicação por $a$ feita $n-1$ vezes: $a^{n} = a \cdot a \cdot \ldots \cdot a$. No entanto, essa abordagem não é prática para valores grandes de $a$ ou $n$.

$(a^{b+c} = a^b \cdot a^c)$ e $(a^{2b} = a^b \cdot a^b = (a^b)^2).$

A ideia da exponenciação binária é dividir o trabalho usando a representação binária do expoente.

Vamos escrever $n$ na base 2, por exemplo:

$3^{13} = 3^{1101_{2}} = 3^{8} . 3^{4} . 3^{1}$

Dado que o número $n$ possui exatamente $(\lfloor \log_2 n \rfloor + 1)$ dígitos na base 2, só precisamos realizar $(O(\log n))$ multiplicações, se soubermos as potências $(a^1, a^2, a^4, a^8, \dots, a^{2^{\lfloor \log n \rfloor}}).$

Portanto, só precisamos conhecer uma maneira rápida de calcular essas potências. Felizmente, isso é muito fácil, uma vez que um elemento na sequência é simplesmente o quadrado do elemento anterior.

$$\begin{align} 3^1 &= 3 \\ 3^2 &= \left(3^1\right)^2 = 3^2 = 9 \\ 3^4 &= \left(3^2\right)^2 = 9^2 = 81 \\ 3^8 &= \left(3^4\right)^2 = 81^2 = 6561 \end{align}$$ 
Portanto, para obter a resposta final para
$3^{13}$ , precisamos apenas multiplicar três deles (pulando
$3^2$  porque o bit correspondente em
$n$  não está definido):
$3^{13} = 6561 \cdot 81 \cdot 3 = 1594323$ 

A complexidade final deste algoritmo é
$O(\log n)$ : precisamos calcular
$\log n$  potências de
$a$ , e então temos que fazer no máximo
$\log n$  multiplicações para obter a resposta final delas.

A seguinte abordagem recursiva expressa a mesma ideia:

$$a^n = \begin{cases}
1 &\text{se } n == 0 \\
\left(a^{\frac{n}{2}}\right)^2 &\text{se } n > 0 \text{ e } n \text{ par}\\
\left(a^{\frac{n - 1}{2}}\right)^2 \cdot a &\text{se } n > 0 \text{ e } n \text{ ímpar}\\
\end{cases}$$

