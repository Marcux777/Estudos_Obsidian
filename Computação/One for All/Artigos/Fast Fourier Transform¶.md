
$$A(x) = a_0 x^0 + a_1 x^1 + \dots + a_{n-1} x^{n-1}$$ 
Dividimos o polinômio em dois polinômios menores, um contendo apenas os coeficientes das posições pares e outro contendo os coeficientes das posições ímpares:

$$
\begin{align}
A_0(x) &= a_0 x^0 + a_2 x^1 + \dots + a_{n-2} x^{\frac{n}{2}-1} \\
A_1(x) &= a_1 x^0 + a_3 x^1 + \dots + a_{n-1} x^{\frac{n}{2}-1}
\end{align}
$$
É fácil ver que

$$A(x) = A_0(x^2) + x A_1(x^2).$$
Os polinômios  $A_0$  e  $A_1$  têm apenas a metade dos coeficientes do polinômio  $A$ . Se pudermos calcular a  $\text{DFT}(A)$  em tempo linear usando  $\text{DFT}(A_0)$  e  $\text{DFT}(A_1)$ , então obtemos a recorrência  

$$T_{\text{DFT}}(n) = 2 T_{\text{DFT}}\left(\frac{n}{2}\right) + O(n)$$

para a complexidade de tempo, que resulta em  $T_{\text{DFT}}(n) = O(n \log n)$  pelo teorema mestre.

Vamos aprender como podemos fazer isso.

Suponha que tenhamos calculado os vetores  $\left(y_k^0\right)_{k=0}^{n/2-1} = \text{DFT}(A_0)$  e  $\left(y_k^1\right)_{k=0}^{n/2-1} = \text{DFT}(A_1)$ . Vamos encontrar uma expressão para  $\left(y_k\right)_{k=0}^{n-1} = \text{DFT}(A)$ .

Para os primeiros  
$\frac{n}{2}$  valores, podemos usar a equação anteriormente observada  $A(x) = A_0(x^2) + x A_1(x^2)$ :

$$y_k = y_k^0 + w_n^k y_k^1, \quad k = 0 \dots \frac{n}{2} - 1.$$

No entanto, para os segundos  $\frac{n}{2}$  valores, precisamos encontrar uma expressão um pouco diferente:

$$
\begin{align}
y_{k+n/2} &= A\left(w_n^{k+n/2}\right) \\
&= A_0\left(w_n^{2k+n}\right) + w_n^{k + n/2} A_1\left(w_n^{2k+n}\right) \\
&= A_0\left(w_n^{2k} w_n^n\right) + w_n^k w_n^{n/2} A_1\left(w_n^{2k} w_n^n\right) \\
&= A_0\left(w_n^{2k}\right) - w_n^k A_1\left(w_n^{2k}\right) \\
&= y_k^0 - w_n^k y_k^1
\end{align}
$$

Aqui usamos novamente  $A(x) = A_0(x^2) + x A_1(x^2)$  e as duas identidades  $w_n^n = 1$  e  $w_n^{n/2} = -1$ .

Portanto, obtemos as fórmulas desejadas para calcular todo o vetor  
$(y_k)$ :

$$
\begin{align}
y_k &= y_k^0 + w_n^k y_k^1, &\quad k = 0 \dots \frac{n}{2} - 1, \\
y_{k+n/2} &= y_k^0 - w_n^k y_k^1, &\quad k = 0 \dots \frac{n}{2} - 1.
\end{align}
$$

(Este padrão  $a + b$  e  $a - b$  é às vezes chamado de "borboleta".)

Assim, aprendemos como calcular a DFT em  $O(n \log n)$  tempo.