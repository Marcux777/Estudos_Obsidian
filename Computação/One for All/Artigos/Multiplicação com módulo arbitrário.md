
Aqui queremos alcançar o mesmo objetivo da seção anterior. Multiplicar dois polinômios  $A(x)$  e  
$B(x)$ , e calcular os coeficientes módulo algum número  $M$ . A transformada teórica de números só funciona para certos números primos. E se o módulo não estiver na forma desejada?

Uma opção seria realizar várias transformadas teóricas de números com diferentes números primos da forma  
$c 2^k + 1$ , e depois aplicar o Teorema Chinês dos Restos para calcular os coeficientes finais.

Outra opção é distribuir os polinômios  $A(x)$  e  $B(x)$  em dois polinômios menores cada:

  
 
 
$$\begin{align} A(x) &= A_1(x) + A_2(x) \cdot C \\ B(x) &= B_1(x) + B_2(x) \cdot C \end{align}$$ 
com  $C \approx \sqrt{M}$ .

Então, o produto de $A(x)$  e  $B(x)$  pode ser representado como:

$$A(x) \cdot B(x) = A_1(x) \cdot B_1(x) + \left(A_1(x) \cdot B_2(x) + A_2(x) \cdot B_1(x)\right)\cdot C + \left(A_2(x) \cdot B_2(x)\right)\cdot C^2$$ 
Os polinômios  $A_1(x)$ ,  $A_2(x)$ ,  $B_1(x)$  e  $B_2(x)$  contêm apenas coeficientes menores que  
$\sqrt{M}$ , portanto, os coeficientes de todos os produtos que aparecem são menores que  
$M \cdot n$ , o que geralmente é pequeno o suficiente para lidar com os tipos típicos de ponto flutuante.

Portanto, essa abordagem requer calcular os produtos de polinômios com coeficientes menores (usando a FFT normal e a FFT inversa), e então o produto original pode ser restaurado usando adição e multiplicação modulares em  $O(n)$  tempo.