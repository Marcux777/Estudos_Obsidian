### Série de Potências Formais

**Definição**

Uma série de potências formais é uma soma infinita  
$A(x) = a_0 + a_1 x + a_2 x^2 + \dots$ , considerada independentemente de suas propriedades de convergência.

Em outras palavras, quando consideramos, por exemplo, uma soma  
$1+\frac{1}{2}+\frac{1}{4}+\frac{1}{8}+\dots=2$ , estamos implicando que ela converge para  
$2$  à medida que o número de termos se aproxima do infinito. No entanto, séries formais são consideradas apenas em termos de sequências que as definem.

**Definição**

O produto de duas séries de potências formais  $A(x)$  e  $B(x)$  também é definido por meio da expansão como uma expressão aritmética:
$$ A(x) B(x) = \left(\sum\limits_{i=0}^\infty a_i x^i \right)\left(\sum\limits_{j=0}^\infty b_j x^j\right) = \sum\limits_{i,j} a_i b_j x^{i+j} = \sum\limits_{k=0}^{\infty} c_k x^k = C(x), $$ 
onde os coeficientes  $c_0, c_1, \dots$  são definidos como somas finitas

$$ c_k = \sum\limits_{i=0}^k a_i b_{k-i}. $$ 
A sequência  $c_0, c_1, \dots$  também é chamada de convolução de  $a_0, a_1, \dots$  e  $b_0, b_1, \dots$ , generalizando o conceito para sequências infinitas.

Assim, polinômios podem ser considerados séries de potências formais, mas com um número finito de coeficientes.

Séries de potências formais desempenham um papel crucial na combinatorial enumerativa, onde são estudadas como funções geradoras para várias sequências. Uma explicação detalhada de funções geradoras e a intuição por trás delas estarão, infelizmente, fora do escopo deste artigo. Portanto, o leitor curioso é referenciado, por exemplo, [aqui](https://en.wikipedia.org/wiki/Generating_function#Formal_power_series) para detalhes sobre o significado combinatório.

No entanto, mencionaremos muito brevemente que se  $A(x)$  e  $B(x)$  são funções geradoras para sequências que enumeram objetos pelo número de "átomos" neles (por exemplo, árvores pelo número de vértices), então o produto  $A(x) B(x)$  enumera objetos que podem ser descritos como pares de objetos dos tipos  $A$  e  $B$ , enumerados pelo número total de "átomos" no par.

**Exemplo**

Suponha que 
$$
\
A(x) = \sum\limits_{i=0}^\infty 2^i x^i
\
$$

enumere conjuntos de pedras, cada pedra colorida em uma de  $2$  cores (ou seja, há  
$2^i$  desses conjuntos de tamanho  $i$ ), e que 

$$
\
B(x) = \sum\limits_{j=0}^{\infty} 3^j x^j
\
$$

enumere conjuntos de pedras, cada pedra colorida em uma de  $3$  cores. Então 

\
C(x) = A(x) B(x) = \sum\limits_{k=0}^\infty c_k x^k
\

enumeraria objetos que podem ser descritos como "dois conjuntos de pedras, primeiro conjunto apenas de pedras do tipo  
$A$ , segundo conjunto apenas de pedras do tipo  
$B$ , com número total de pedras sendo  
$k$ " para  
$c_k$ .

De maneira semelhante, há um significado intuitivo para algumas outras funções sobre séries de potências formais.