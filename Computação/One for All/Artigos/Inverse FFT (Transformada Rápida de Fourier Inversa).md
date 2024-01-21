
Dado o vetor  $(y_0, y_1, \dots y_{n-1})$  - os valores do polinômio  $A$  de grau  $n - 1$  nos pontos  $x = w_n^k$  - seja dado. Queremos restaurar os coeficientes  $(a_0, a_1, \dots, a_{n-1})$  do polinômio. Este problema conhecido é chamado de interpolação, e existem algoritmos gerais para resolvê-lo. Mas, neste caso especial (já que conhecemos os valores nos pontos das raízes da unidade), podemos obter um algoritmo muito mais simples (que é praticamente o mesmo que a FFT direta).

Podemos escrever a DFT, de acordo com sua definição, na forma de matriz:

$$
\begin{pmatrix}
w_n^0 & w_n^0 & w_n^0 & w_n^0 & \cdots & w_n^0 \\
w_n^0 & w_n^1 & w_n^2 & w_n^3 & \cdots & w_n^{n-1} \\
w_n^0 & w_n^2 & w_n^4 & w_n^6 & \cdots & w_n^{2(n-1)} \\
w_n^0 & w_n^3 & w_n^6 & w_n^9 & \cdots & w_n^{3(n-1)} \\
\vdots & \vdots & \vdots & \vdots & \ddots & \vdots \\
w_n^0 & w_n^{n-1} & w_n^{2(n-1)} & w_n^{3(n-1)} & \cdots & w_n^{(n-1)(n-1)}
\end{pmatrix}
\begin{pmatrix}
a_0 \\
a_1 \\
a_2 \\
a_3 \\
\vdots \\
a_{n-1}
\end{pmatrix}
=
\begin{pmatrix}
y_0 \\
y_1 \\
y_2 \\
y_3 \\
\vdots \\
y_{n-1}
\end{pmatrix}
$$

Esta matriz é chamada de matriz de Vandermonde.

Assim, podemos calcular o vetor  $(a_0, a_1, \dots, a_{n-1})$  multiplicando o vetor  $(y_0, y_1, \dots y_{n-1})$  à esquerda pela inversa da matriz:

$$
\begin{pmatrix}
a_0 \\
a_1 \\
a_2 \\
a_3 \\
\vdots \\
a_{n-1}
\end{pmatrix}
=
\begin{pmatrix}
w_n^0 & w_n^0 & w_n^0 & w_n^0 & \cdots & w_n^0 \\
w_n^0 & w_n^1 & w_n^2 & w_n^3 & \cdots & w_n^{n-1} \\
w_n^0 & w_n^2 & w_n^4 & w_n^6 & \cdots & w_n^{2(n-1)} \\
w_n^0 & w_n^3 & w_n^6 & w_n^9 & \cdots & w_n^{3(n-1)} \\
\vdots & \vdots & \vdots & \vdots & \ddots & \vdots \\
w_n^0 & w_n^{n-1} & w_n^{2(n-1)} & w_n^{3(n-1)} & \cdots & w_n^{(n-1)(n-1)}
\end{pmatrix}^{-1}
\begin{pmatrix}
y_0 \\
y_1 \\
y_2 \\
y_3 \\
\vdots \\
y_{n-1}
\end{pmatrix}
$$

Uma verificação rápida pode verificar que a inversa da matriz tem a seguinte forma:

$$
\frac{1}{n}
\begin{pmatrix}
w_n^0 & w_n^0 & w_n^0 & w_n^0 & \cdots & w_n^0 \\
w_n^0 & w_n^{-1} & w_n^{-2} & w_n^{-3} & \cdots & w_n^{-(n-1)} \\
w_n^0 & w_n^{-2} & w_n^{-4} & w_n^{-6} & \cdots & w_n^{-2(n-1)} \\
w_n^0 & w_n^{-3} & w_n^{-6} & w_n^{-9} & \cdots & w_n^{-3(n-1)} \\
\vdots & \vdots & \vdots & \vdots & \ddots & \vdots \\
w_n^0 & w_n^{-(n-1)} & w_n^{-2(n-1)} & w_n

^{-3(n-1)} & \cdots & w_n^{-(n-1)(n-1)}
\end{pmatrix}
$$

Assim, obtemos a fórmula:

$$
a_k = \frac{1}{n} \sum_{j=0}^{n-1} y_j w_n^{-k j}
$$

Comparando isso com a fórmula para  $y_k$ 

$$
y_k = \sum_{j=0}^{n-1} a_j w_n^{k j},
$$

notamos que esses problemas são quase iguais, então os coeficientes  $a_k$  podem ser encontrados pelo mesmo algoritmo de divisão e conquista, assim como a FFT direta, apenas em vez de  $w_n^k$ , precisamos usar  $w_n^{-k}$ , e no final precisamos dividir os coeficientes resultantes por  
$n$ .

Portanto, o cálculo da inversa da DFT é quase o mesmo que o cálculo da DFT direta, e também pode ser realizado em  $O(n \log n)$  tempo.