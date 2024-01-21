
Considere dois polinômios  $A$  e  $B$ . Calculamos a DFT para cada um deles:  
$\text{DFT}(A)$  e  $\text{DFT}(B)$ .

O que acontece se multiplicarmos esses polinômios? Obviamente, em cada ponto, os valores são simplesmente multiplicados, ou seja,

$$(A \cdot B)(x) = A(x) \cdot B(x).$$ 
Isso significa que, se multiplicarmos os vetores  $\text{DFT}(A)$  e  $\text{DFT}(B)$  - multiplicando cada elemento de um vetor pelo elemento correspondente do outro vetor - obtemos nada menos que a DFT do polinômio  $\text{DFT}(A \cdot B)$ :

$$\text{DFT}(A \cdot B) = \text{DFT}(A) \cdot \text{DFT}(B)$$ 
Finalmente, aplicando a DFT inversa, obtemos:

 
$$A \cdot B = \text{InverseDFT}(\text{DFT}(A) \cdot \text{DFT}(B))$$ 
Na parte direita, o produto das duas DFTs refere-se ao produto em pares dos elementos do vetor. Isso pode ser calculado em  $O(n)$  tempo. Se pudermos calcular a DFT e a DFT inversa em  $O(n \log n)$ , então podemos calcular o produto dos dois polinômios (e consequentemente também de dois números longos) com a mesma complexidade de tempo.

Deve-se observar que os dois polinômios devem ter o mesmo grau. Caso contrário, os dois vetores resultantes da DFT terão comprimentos diferentes. Podemos alcançar isso adicionando coeficientes com o valor  $0$ .

Além disso, como o resultado do produto de dois polinômios é um polinômio de grau  $2 (n - 1)$ , precisamos dobrar os graus de cada polinômio (novamente preenchendo com  $0$ s). A partir de um vetor com  $n$  valores, não podemos reconstruir o polinômio desejado com  $2n - 1$  coeficientes.

