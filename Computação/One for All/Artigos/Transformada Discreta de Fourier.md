
Considere um polinômio de grau  $n - 1$ :
$$A(x) = a_0 x^0 + a_1 x^1 + \dots + a_{n-1} x^{n-1}$$ 
Sem perda de generalidade, assumimos que  $n$  - o número de coeficientes - é uma potência de  $2$ . Se  $n$  não é uma potência de  $2$ , então simplesmente adicionamos os termos ausentes  $a_i x^i$  e definimos os coeficientes  $a_i$  como  $0$ .

A teoria dos números complexos nos diz que a equação  $x^n = 1$  tem  $n$  soluções complexas (chamadas  $n$ -ésimas raízes da unidade), e as soluções têm a forma  $w_{n, k} = e^{\frac{2 k \pi i}{n}}$  com  $k = 0 \dots n-1$ . Além disso, esses números complexos têm propriedades muito interessantes: por exemplo, a principal  $n$ -ésima raiz  $w_n = w_{n, 1} = e^{\frac{2 \pi i}{n}}$  pode ser usada para descrever todas as outras raízes  
$n$ -ésimas:  $w_{n, k} = (w_n)^k$ .

A Transformada Discreta de Fourier (DFT) do polinômio  $A(x)$  (ou equivalentemente, o vetor de coeficientes  $(a_0, a_1, \dots, a_{n-1})$  é definida como os valores do polinômio nos pontos  $x = w_{n, k}$ , ou seja, é o vetor:
$$\begin{align} \text{DFT}(a_0, a_1, \dots, a_{n-1}) &= (y_0, y_1, \dots, y_{n-1}) \\ &= (A(w_{n, 0}), A(w_{n, 1}), \dots, A(w_{n, n-1})) \\ &= (A(w_n^0), A(w_n^1), \dots, A(w_n^{n-1})) \end{align}$$ 
Da mesma forma, a transformada discreta inversa de Fourier é definida: A DFT inversa dos valores do polinômio  $(y_0, y_1, \dots, y_{n-1})$  são os coeficientes do polinômio  $(a_0, a_1, \dots, a_{n-1})$ .

$$\text{InverseDFT}(y_0, y_1, \dots, y_{n-1}) = (a_0, a_1, \dots, a_{n-1})$$ 
Assim, se uma DFT direta calcula os valores do polinômio nos pontos das  $n$ -ésimas raízes, a DFT inversa pode restaurar os coeficientes do polinômio usando esses valores.

[[Aplicação da DFT - multiplicação rápida de polinômios]]
[[Fast Fourier Transform¶]]
[[Inverse FFT (Transformada Rápida de Fourier Inversa)]]
[[Implementação - Discrete Fourier transform]]
[[Improved implementation - in-place computation]]
