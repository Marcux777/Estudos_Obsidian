## Operações em Polinômios e Séries

Problemas em programação competitiva, especialmente aqueles envolvendo enumeração de algum tipo, são frequentemente resolvidos ao reduzir o problema para o cálculo de algo em polinômios e séries formais de potências.

Isso inclui conceitos como multiplicação de polinômios, interpolação e operações mais complicadas, como logaritmos e exponenciais de polinômios. Neste artigo, é apresentada uma visão geral breve dessas operações e das abordagens comuns para resolvê-las.

## Noções Básicas e Fatos

Nesta seção, focamos mais nas definições e propriedades "intuitivas" de várias operações polinomiais. Os detalhes técnicos de implementação e complexidades serão abordados em seções posteriores.

### Multiplicação de Polinômios

**Definição**

Um polinômio univariado é uma expressão da forma  $A(x) = a_0 + a_1 x + \dots + a_n x^n$ .

Os valores  $a_0, \dots, a_n$  são coeficientes do polinômio, geralmente retirados de algum conjunto de números ou estruturas semelhantes a números. Neste artigo, assumimos que os coeficientes são retirados de algum campo, o que significa que as operações de adição, subtração, multiplicação e divisão são bem definidas para eles (exceto para a divisão por  $0$ ) e geralmente se comportam de maneira semelhante aos números reais.

Exemplo típico desse campo é o campo dos restos da divisão por um número primo  
$p$ .

Por simplicidade, vamos omitir o termo univariado, pois este é o único tipo de polinômios que consideramos neste artigo. Também escreveremos  $A$  em vez de  $A(x)$  sempre que possível, o que será compreensível a partir do contexto. Assume-se que ou  $a_n \neq 0$  ou  $A(x)=0$ .

**Definição**

	O produto de dois polinômios é definido expandindo-o como uma expressão aritmética:
	
	 
	$$ A(x) B(x) = \left(\sum\limits_{i=0}^n a_i x^i \right)\left(\sum\limits_{j=0}^m b_j x^j\right) = \sum\limits_{i,j} a_i b_j x^{i+j} = \sum\limits_{k=0}^{n+m} c_k x^k = C(x). $$ 
	
	A sequência  $c_0, c_1, \dots, c_{n+m}$  dos coeficientes de  $C(x)$  é chamada de convolução de  $a_0, \dots, a_n$  e  $b_0, \dots, b_m$ .

**Definição**

	O grau de um polinômio  $A$  com  $a_n \neq 0$  é definido como  $\deg A = n$ .
	
	Para consistência, o grau de  $A(x) = 0$  é definido como  $\deg A = -\infty$ .

Nesta noção,  $\deg AB = \deg A + \deg B$  para quaisquer polinômios  $A$  e  $B$ .

As convoluções são a base para resolver muitos problemas enumerativos.

#### Exemplo

	Você tem  $n$  objetos do primeiro tipo e  $m$  objetos do segundo tipo.
	
	Objetos do primeiro tipo têm valores  $a_1, \dots, a_n$ , e objetos do segundo tipo têm valores
	$b_1, \dots, b_m$ .
	
	Você escolhe um único objeto do primeiro tipo e um único objeto do segundo tipo. Quantas maneiras existem de obter o valor total  $k$ ?

**Solução**

	Considere o produto  
	$(x^{a_1} + \dots + x^{a_n})(x^{b_1} + \dots + x^{b_m})$ . Se você expandi-lo, cada monômio corresponderá ao par  
	$(a_i, b_j)$  e contribuirá para o coeficiente próximo a  
	$x^{a_i+b_j}$ . Em outras palavras, a resposta é o coeficiente próximo a  
	$x^k$  no produto.

#### Exemplo

	Você joga um dado de  $6$  lados  $n$  vezes e soma os resultados de todos os lançamentos. Qual é a probabilidade de obter uma soma de  $k$ ?

**Solução**

	A resposta é o número de resultados que têm a soma  $k$ , dividido pelo número total de resultados, que é  $6^n$ .
	
	Qual é o número de resultados que têm a soma  $k$ ? Para  $n=1$ , pode ser representado por um polinômio  $A(x) = x^1+x^2+\dots+x^6$ .
	
	Para  $n=2$ , usando a mesma abordagem do exemplo acima, concluímos que é representado pelo polinômio  $(x^1+x^2+\dots+x^6)^2$ .
	
	Dito isso, a resposta para o problema é o coeficiente  $k$ -ésimo de  $(x^1+x^2+\dots+x^6)^n$ , dividido por  $6^n$ .


O coeficiente próximo a  $x^k$  no polinômio  $A(x)$  é denotado brevemente como  $[x^k]A$ .

### Série de Potências Formais

**Definição**
<p>Uma série de potências formais é uma soma infinita  
<math xmlns="http://www.w3.org/1998/Math/MathML">
  <mi>A</mi>
  <mo stretchy="false">(</mo>
  <mi>x</mi>
  <mo stretchy="false">)</mo>
  <mo>=</mo>
  <msub>
    <mi>a</mi>
    <mn>0</mn>
  </msub>
  <mo>+</mo>
  <msub>
    <mi>a</mi>
    <mn>1</mn>
  </msub>
  <mi>x</mi>
  <mo>+</mo>
  <msub>
    <mi>a</mi>
    <mn>2</mn>
  </msub>
  <msup>
    <mi>x</mi>
    <mn>2</mn>
  </msup>
  <mo>+</mo>
  <mo>&#x2026;</mo>
</math> , considerada independentemente de suas propriedades de convergência. </p>

Em outras palavras, quando consideramos, por exemplo, uma soma  
$1+\frac{1}{2}+\frac{1}{4}+\frac{1}{8}+\dots=2$ , estamos implicando que ela converge para  
$2$  à medida que o número de termos se aproxima do infinito. No entanto, séries formais são consideradas apenas em termos de sequências que as definem.

**Definição**
<p> O produto de duas séries de potências formais  <math xmlns="http://www.w3.org/1998/Math/MathML">
  <mi>A</mi>
  <mo stretchy="false">(</mo>
  <mi>x</mi>
  <mo stretchy="false">)</mo>
</math>  e  <math xmlns="http://www.w3.org/1998/Math/MathML">
  <mi>B</mi>
  <mo stretchy="false">(</mo>
  <mi>x</mi>
  <mo stretchy="false">)</mo>
</math>  também é definido por meio da expansão como uma expressão aritmética:
	<math xmlns="http://www.w3.org/1998/Math/MathML" display="block">
  <mi>A</mi>
  <mo stretchy="false">(</mo>
  <mi>x</mi>
  <mo stretchy="false">)</mo>
  <mi>B</mi>
  <mo stretchy="false">(</mo>
  <mi>x</mi>
  <mo stretchy="false">)</mo>
  <mo>=</mo>
  <mrow data-mjx-texclass="INNER">
    <mo data-mjx-texclass="OPEN">(</mo>
    <munderover>
      <mo data-mjx-texclass="OP" movablelimits="false">&#x2211;</mo>
      <mrow data-mjx-texclass="ORD">
        <mi>i</mi>
        <mo>=</mo>
        <mn>0</mn>
      </mrow>
      <mi mathvariant="normal">&#x221E;</mi>
    </munderover>
    <msub>
      <mi>a</mi>
      <mi>i</mi>
    </msub>
    <msup>
      <mi>x</mi>
      <mi>i</mi>
    </msup>
    <mo data-mjx-texclass="CLOSE">)</mo>
  </mrow>
  <mrow data-mjx-texclass="INNER">
    <mo data-mjx-texclass="OPEN">(</mo>
    <munderover>
      <mo data-mjx-texclass="OP" movablelimits="false">&#x2211;</mo>
      <mrow data-mjx-texclass="ORD">
        <mi>j</mi>
        <mo>=</mo>
        <mn>0</mn>
      </mrow>
      <mi mathvariant="normal">&#x221E;</mi>
    </munderover>
    <msub>
      <mi>b</mi>
      <mi>j</mi>
    </msub>
    <msup>
      <mi>x</mi>
      <mi>j</mi>
    </msup>
    <mo data-mjx-texclass="CLOSE">)</mo>
  </mrow>
  <mo>=</mo>
  <munder>
    <mo data-mjx-texclass="OP" movablelimits="false">&#x2211;</mo>
    <mrow data-mjx-texclass="ORD">
      <mi>i</mi>
      <mo>,</mo>
      <mi>j</mi>
    </mrow>
  </munder>
  <msub>
    <mi>a</mi>
    <mi>i</mi>
  </msub>
  <msub>
    <mi>b</mi>
    <mi>j</mi>
  </msub>
  <msup>
    <mi>x</mi>
    <mrow data-mjx-texclass="ORD">
      <mi>i</mi>
      <mo>+</mo>
      <mi>j</mi>
    </mrow>
  </msup>
  <mo>=</mo>
  <munderover>
    <mo data-mjx-texclass="OP" movablelimits="false">&#x2211;</mo>
    <mrow data-mjx-texclass="ORD">
      <mi>k</mi>
      <mo>=</mo>
      <mn>0</mn>
    </mrow>
    <mrow data-mjx-texclass="ORD">
      <mi mathvariant="normal">&#x221E;</mi>
    </mrow>
  </munderover>
  <msub>
    <mi>c</mi>
    <mi>k</mi>
  </msub>
  <msup>
    <mi>x</mi>
    <mi>k</mi>
  </msup>
  <mo>=</mo>
  <mi>C</mi>
  <mo stretchy="false">(</mo>
  <mi>x</mi>
  <mo stretchy="false">)</mo>
  <mo>,</mo>
</math>
onde os coeficientes<math xmlns="http://www.w3.org/1998/Math/MathML">
  <msub>
    <mi>c</mi>
    <mn>0</mn>
  </msub>
  <mo>,</mo>
  <msub>
    <mi>c</mi>
    <mn>1</mn>
  </msub>
  <mo>,</mo>
  <mo>&#x2026;</mo>
</math> são definidos como somas finitas

<math xmlns="http://www.w3.org/1998/Math/MathML" display="block">
  <msub>
    <mi>c</mi>
    <mi>k</mi>
  </msub>
  <mo>=</mo>
  <munderover>
    <mo data-mjx-texclass="OP" movablelimits="false">&#x2211;</mo>
    <mrow data-mjx-texclass="ORD">
      <mi>i</mi>
      <mo>=</mo>
      <mn>0</mn>
    </mrow>
    <mi>k</mi>
  </munderover>
  <msub>
    <mi>a</mi>
    <mi>i</mi>
  </msub>
  <msub>
    <mi>b</mi>
    <mrow data-mjx-texclass="ORD">
      <mi>k</mi>
      <mo>&#x2212;</mo>
      <mi>i</mi>
    </mrow>
  </msub>
  <mo>.</mo>
</math>
A sequência <math xmlns="http://www.w3.org/1998/Math/MathML">
  <msub>
    <mi>c</mi>
    <mn>0</mn>
  </msub>
  <mo>,</mo>
  <msub>
    <mi>c</mi>
    <mn>1</mn>
  </msub>
  <mo>,</mo>
  <mo>&#x2026;</mo>
</math>  também é chamada de convolução de <math xmlns="http://www.w3.org/1998/Math/MathML">
  <msub>
    <mi>a</mi>
    <mn>0</mn>
  </msub>
  <mo>,</mo>
  <msub>
    <mi>a</mi>
    <mn>1</mn>
  </msub>
  <mo>,</mo>
  <mo>&#x2026;</mo>
</math> e <math xmlns="http://www.w3.org/1998/Math/MathML">
  <msub>
    <mi>b</mi>
    <mn>0</mn>
  </msub>
  <mo>,</mo>
  <msub>
    <mi>b</mi>
    <mn>1</mn>
  </msub>
  <mo>,</mo>
  <mo>&#x2026;</mo>
</math> , generalizando o conceito para sequências infinitas. </p>

Assim, polinômios podem ser considerados séries de potências formais, mas com um número finito de coeficientes.

Séries de potências formais desempenham um papel crucial na combinatorial enumerativa, onde são estudadas como funções geradoras para várias sequências. Uma explicação detalhada de funções geradoras e a intuição por trás delas estarão, infelizmente, fora do escopo deste artigo. Portanto, o leitor curioso é referenciado, por exemplo, [aqui](https://en.wikipedia.org/wiki/Generating_function#Formal_power_series) para detalhes sobre o significado combinatório.

No entanto, mencionaremos muito brevemente que se  $A(x)$  e  $B(x)$  são funções geradoras para sequências que enumeram objetos pelo número de "átomos" neles (por exemplo, árvores pelo número de vértices), então o produto  $A(x) B(x)$  enumera objetos que podem ser descritos como pares de objetos dos tipos  $A$  e  $B$ , enumerados pelo número total de "átomos" no par.

**Exemplo**
<p>Suponha que

<math xmlns="http://www.w3.org/1998/Math/MathML">
  <mi>A</mi>
  <mo stretchy="false">(</mo>
  <mi>x</mi>
  <mo stretchy="false">)</mo>
  <mo>=</mo>
  <munderover>
    <mo data-mjx-texclass="OP" movablelimits="false">&#x2211;</mo>
    <mrow data-mjx-texclass="ORD">
      <mi>i</mi>
      <mo>=</mo>
      <mn>0</mn>
    </mrow>
    <mi mathvariant="normal">&#x221E;</mi>
  </munderover>
  <msup>
    <mn>2</mn>
    <mi>i</mi>
  </msup>
  <msup>
    <mi>x</mi>
    <mi>i</mi>
  </msup>
</math>

enumere conjuntos de pedras, cada pedra colorida em uma de 2 cores (ou seja, há<math xmlns="http://www.w3.org/1998/Math/MathML">
  <msup>
    <mn>2</mn>
    <mi>i</mi>
  </msup>
</math> desses conjuntos de tamanho <math xmlns="http://www.w3.org/1998/Math/MathML">
  <mi>i</mi>
</math>)), e que 

<math xmlns="http://www.w3.org/1998/Math/MathML">
  <mi>B</mi>
  <mo stretchy="false">(</mo>
  <mi>x</mi>
  <mo stretchy="false">)</mo>
  <mo>=</mo>
  <munderover>
    <mo data-mjx-texclass="OP" movablelimits="false">&#x2211;</mo>
    <mrow data-mjx-texclass="ORD">
      <mi>j</mi>
      <mo>=</mo>
      <mn>0</mn>
    </mrow>
    <mrow data-mjx-texclass="ORD">
      <mi mathvariant="normal">&#x221E;</mi>
    </mrow>
  </munderover>
  <msup>
    <mn>3</mn>
    <mi>j</mi>
  </msup>
  <msup>
    <mi>x</mi>
    <mi>j</mi>
  </msup>
</math>

enumere conjuntos de pedras, cada pedra colorida em uma de 3 cores. Então 

<math xmlns="http://www.w3.org/1998/Math/MathML">
  <mi>C</mi>
  <mo stretchy="false">(</mo>
  <mi>x</mi>
  <mo stretchy="false">)</mo>
  <mo>=</mo>
  <mi>A</mi>
  <mo stretchy="false">(</mo>
  <mi>x</mi>
  <mo stretchy="false">)</mo>
  <mi>B</mi>
  <mo stretchy="false">(</mo>
  <mi>x</mi>
  <mo stretchy="false">)</mo>
  <mo>=</mo>
  <munderover>
    <mo data-mjx-texclass="OP" movablelimits="false">&#x2211;</mo>
    <mrow data-mjx-texclass="ORD">
      <mi>k</mi>
      <mo>=</mo>
      <mn>0</mn>
    </mrow>
    <mi mathvariant="normal">&#x221E;</mi>
  </munderover>
  <msub>
    <mi>c</mi>
    <mi>k</mi>
  </msub>
  <msup>
    <mi>x</mi>
    <mi>k</mi>
  </msup>
</math>

enumeraria objetos que podem ser descritos como "dois conjuntos de pedras, primeiro conjunto apenas de pedras do tipo <math xmlns="http://www.w3.org/1998/Math/MathML">
  <mi>A</mi>
</math>, segundo conjunto apenas de pedras do tipo <math xmlns="http://www.w3.org/1998/Math/MathML">
  <mi>B</mi>
</math>, com número total de pedras sendo <math xmlns="http://www.w3.org/1998/Math/MathML">
  <mi>k</mi>
</math>" para <math xmlns="http://www.w3.org/1998/Math/MathML">
  <msub>
    <mi>c</mi>
    <mi>k</mi>
  </msub>
</math>.</p>

De maneira semelhante, há um significado intuitivo para algumas outras funções sobre séries de potências formais.

### Long polynomial division
Semelhante aos inteiros, é possível definir a divisão longa para polinômios.

Definição

Para quaisquer polinômios  $A$  e  $B \neq 0$ , pode-se representar  $A$  como
 
$$ A = D \cdot B + R,~ \deg R < \deg B, $$ 
onde  $R$  é chamado de resto de  $A$  módulo  $B$  e  $D$  é chamado de quociente.

Denotando  $\deg A = n$  e  $\deg B = m$ , uma maneira ingênua de fazer isso é usar a divisão longa, durante a qual você multiplica  $B$  pelo monômio  $\frac{a_n}{b_m} x^{n - m}$  e subtrai isso de  $A$ , até que o grau de  $A$  seja menor que o de  $B$ . O que resta de  $A$  no final será o resto (daí o nome), e os polinômios pelos quais você multiplicou  $B$  no processo, somados juntos, formam o quociente.

Definição

Se  $A$  e  $B$  têm o mesmo resto módulo  $C$ , diz-se que são equivalentes módulo  $C$ , o que é denotado como 
$$ A \equiv B \pmod{C}. $$ 
A divisão longa de polinômios é útil devido às suas muitas propriedades importantes:

 
$A$  é um múltiplo de  $B$  se e somente se  $A \equiv 0 \pmod B$ .

Isso implica que  $A \equiv B \pmod C$  se e somente se  $A-B$  é um múltiplo de  $C$ .

Em particular,  $A \equiv B \pmod{C \cdot D}$  implica  $A \equiv B \pmod{C}$ .

Para qualquer polinômio linear  $x-r$ , vale que  $A(x) \equiv A(r) \pmod{x-r}$ .

Isso implica que  $A$  é um múltiplo de  $x-r$  se e somente se  $A(r)=0$ .

Para módulo sendo  $x^k$ , vale que  $A \equiv a_0 + a_1 x + \dots + a_{k-1} x^{k-1} \pmod{x^k}$ .

Observe que a divisão longa não pode ser adequadamente definida para séries formais de potências. Em vez disso, para qualquer  $A(x)$  tal que  $a_0 \neq 0$ , é possível definir uma série de potências formais inversa  $A^{-1}(x)$ , tal que  $A(x) A^{-1}(x) = 1$ . Esse fato, por sua vez, pode ser usado para calcular o resultado da divisão longa para polinômios.

## Basic implementation

Aqui está a implementação básica da álgebra de polinômios.

Ela suporta todas as operações triviais e alguns outros métodos úteis. A classe principal é `poly<T>` para polinômios com coeficientes do tipo T.

Todas as operações aritméticas +, -, *, % e / são suportadas, % e / representando o resto e o quociente na divisão euclidiana.

Também há a classe `modular<m>` para realizar operações aritméticas em restos módulo um número primo m.

Outras funções úteis:

- `deriv()`: calcula a derivada  $P'(x)$  de  $P(x)$ .
- `integr()`: calcula a integral indefinida  $Q(x) = \int P(x)$  de  $P(x)$  tal que  $Q(0)=0$ .
- `inv(size_t n)`: calcula os primeiros  $n$  coeficientes de  $P^{-1}(x)$  em  $O(n \log n)$ .
- `log(size_t n)`: calcula os primeiros  $n$  coeficientes de  $\ln P(x)$  em  $O(n \log n)$ .
- `exp(size_t n)`: calcula os primeiros  $n$  coeficientes de  $\exp P(x)$  em  $O(n \log n)$ .
- `pow(size_t k, size_t n)`: calcula os primeiros  $n$  coeficientes para  $P^{k}(x)$  em  $O(n \log nk)$ .
- `deg()`: retorna o grau de  $P(x)$ .
- `lead()`: retorna o coeficiente de  $x^{\deg P(x)}$ .
- `resultant(poly<T> a, poly<T> b)`: calcula o resultado de  $a$  e  $b$  em  $O(|a| \cdot |b|)$ .
- `bpow(T x, size_t n)`: calcula  $x^n$ .
- `bpow(T x, size_t n, T m)`: calcula  $x^n \pmod{m}$ .
- `chirpz(T z, size_t n)`: calcula $P(1), P(z), P(z^2), \dots, P(z^{n-1})$  em  $O(n \log n)$ .
- `vector<T> eval(vector<T> x)`: avalia  $P(x_1), \dots, P(x_n)$  em  $O(n \log^2 n)$ .
- `poly<T> inter(vector<T> x, vector<T> y)`: interpola um polinômio por um conjunto de pares  $P(x_i) = y_i$  em  $O(n \log^2 n)$ .

E mais algumas, sinta-se à vontade para explorar o código!



## Arithmetic
### Multiplication
A operação fundamental é a multiplicação de dois polinômios. Ou seja, dados os polinômios  $A$  e  $B$ :
 
$$A = a_0 + a_1 x + \dots + a_n x^n$$ 
$$B = b_0 + b_1 x + \dots + b_m x^m$$ 
Você precisa calcular o polinômio  $C = A \cdot B$ , que é definido como
$$\boxed{C = \sum\limits_{i=0}^n \sum\limits_{j=0}^m a_i b_j x^{i+j}} = c_0 + c_1 x + \dots + c_{n+m} x^{n+m}.$$ 
Isso pode ser calculado em  $O(n \log n)$  através da Transformada Rápida de Fourier, e quase todos os métodos aqui a utilizarão como sub-rotina.

### Série inversa
Se  $A(0) \neq 0$ , sempre existe uma série de potências formais infinita  $A^{-1}(x) = q_0+q_1 x + q_2 x^2 + \dots$  tal que  $A^{-1} A = 1$ . Frequentemente, é útil calcular primeiro  $k$  coeficientes de  $A^{-1}$  (ou seja, calculá-lo módulo  $x^k$ ). Existem duas principais maneiras de calculá-lo.

#### Dividir e conquistar

Este algoritmo foi mencionado no artigo de Schönhage e é inspirado no método de Graeffe. Sabe-se que para  $B(x)=A(x)A(-x)$  vale que  $B(x)=B(-x)$ , ou seja,  $B(x)$  é um polinômio par. Isso significa que ele só possui coeficientes não nulos com números pares e pode ser representado como  
$B(x)=T(x^2)$ . Assim, podemos fazer a seguinte transição:
 
$$A^{-1}(x) \equiv \frac{1}{A(x)} \equiv \frac{A(-x)}{A(x)A(-x)} \equiv \frac{A(-x)}{T(x^2)} \pmod{x^k}$$ 
Observe que  
$T(x)$  pode ser calculado com uma única multiplicação, após o que estamos interessados apenas na primeira metade dos coeficientes de sua série inversa. Isso efetivamente reduz o problema inicial de calcular  
$A^{-1} \pmod{x^k}$  para calcular  
$T^{-1} \pmod{x^{\lfloor k / 2 \rfloor}}$ .

A complexidade desse método pode ser estimada como

 
$$T(n) = T(n/2) + O(n \log n) = O(n \log n).$$ 
#### Algoritmo Sieveking–Kung
O processo genérico descrito aqui é conhecido como elevação de Hensel, conforme decorre do lema de Hensel. Abordaremos isso com mais detalhes mais adiante, mas por enquanto, vamos nos concentrar na solução ad hoc. A parte de "elevação" aqui significa que começamos com a aproximação  $B_0=q_0=a_0^{-1}$ , que é  $A^{-1} \pmod x$ , e então elevamos iterativamente de  $\bmod x^a$  para  $\bmod x^{2a}$ .

Seja  $B_k \equiv A^{-1} \pmod{x^a}$ . A próxima aproximação precisa seguir a equação  $A B_{k+1} \equiv 1 \pmod{x^{2a}}$  e pode ser representada como  $B_{k+1} = B_k + x^a C$ . Daí segue a equação

$$A(B_k + x^{a}C) \equiv 1 \pmod{x^{2a}}.$$ 
Seja  $A B_k \equiv 1 + x^a D \pmod{x^{2a}}$ , então a equação acima implica

$$x^a(D+AC) \equiv 0 \pmod{x^{2a}} \implies D \equiv -AC \pmod{x^a} \implies C \equiv -B_k D \pmod{x^a}.$$ 
Dessa forma, pode-se obter a fórmula final, que é
 
$$x^a C \equiv -B_k x^a D \equiv B_k(1-AB_k) \pmod{x^{2a}} \implies \boxed{B_{k+1} \equiv B_k(2-AB_k) \pmod{x^{2a}}}$$ 
Assim, começando com  $B_0 \equiv a_0^{-1} \pmod x$ , computaremos a sequência  $B_k$  tal que  $AB_k \equiv 1 \pmod{x^{2^k}}$  com complexidade
 
$$T(n) = T(n/2) + O(n \log n) = O(n \log n).$$ 
O algoritmo aqui pode parecer um pouco mais complicado do que o primeiro, mas possui um raciocínio muito sólido e prático por trás dele, bem como um grande potencial de generalização se observado de uma perspectiva diferente, como será explicado mais adiante.

### Divisão euclidiana
Considere dois polinômios $A(x)$  e  $B(x)$  de graus  $n$  e  $m$ . Como mencionado anteriormente, você pode reescrever  $A(x)$  como
 
$$A(x) = B(x) D(x) + R(x), \deg R < \deg B.$$ 
Suponha que  $n \geq m$ , o que implicaria que  $\deg D = n - m$  e os  $n-m+1$  coeficientes principais de  
$A$  não influenciam  $R$ . Isso significa que você pode recuperar  $D(x)$  dos maiores  $n-m+1$  coeficientes de  $A(x)$  e  $B(x)$  se você o considerar como um sistema de equações.

O sistema de equações lineares do qual estamos falando pode ser escrito na seguinte forma:
 
 
$$\begin{bmatrix} a_n \\ \vdots \\ a_{m+1} \\ a_{m} \end{bmatrix} = \begin{bmatrix} b_m & \dots & 0 & 0 \\ \vdots & \ddots & \vdots & \vdots \\ \dots & \dots & b_m & 0 \\ \dots & \dots & b_{m-1} & b_m \end{bmatrix} \begin{bmatrix}d_{n-m} \\ \vdots \\ d_1 \\ d_0\end{bmatrix}$$ 
Pela aparência, podemos concluir que, com a introdução de polinômios reversos

$$A^R(x) = x^nA(x^{-1})= a_n + a_{n-1} x + \dots + a_0 x^n$$
 
$$B^R(x) = x^m B(x^{-1}) = b_m + b_{m-1} x + \dots + b_0 x^m$$ 
$$D^R(x) = x^{n-m}D(x^{-1}) = d_{n-m} + d_{n-m-1} x + \dots + d_0 x^{n-m}$$ 
o sistema pode ser reescrito como

$$A^R(x) \equiv B^R(x) D^R(x) \pmod{x^{n-m+1}}.$$ 
Com isso, você pode recuperar unicamente todos os coeficientes de  $D(x)$ :
 
$$\boxed{D^R(x) \equiv A^R(x) (B^R(x))^{-1} \pmod{x^{n-m+1}}}$$ 
E a partir disso, por sua vez, você pode recuperar  $R(x)$  como  $R(x) = A(x) - B(x)D(x)$ .

Observe que a matriz acima é uma matriz de Toeplitz triangular, e, como vemos aqui, resolver um sistema de equações lineares com uma matriz de Toeplitz arbitrária é, na verdade, equivalente à inversão de polinômios. Além disso, a matriz inversa dela também seria uma matriz de Toeplitz triangular e seus elementos, nos termos usados acima, são os coeficientes de  
$(B^R(x))^{-1} \pmod{x^{n-m+1}}$ .



## Calculating functions of polynomial

### Método de Newton
Vamos generalizar o algoritmo Sieveking–Kung. Considere a equação  $F(P) = 0$  onde  $P(x)$  deve ser um polinômio e  $F(x)$  é alguma função polinomial definida como

$$F(x) = \sum\limits_{i=0}^\infty \alpha_i (x-\beta)^i,$$ 
onde  $\beta$  é alguma constante. Pode-se provar que, se introduzirmos uma nova variável formal  $y$ , podemos expressar  $F(x)$  como

 
$$F(x) = F(y) + (x-y)F'(y) + (x-y)^2 G(x,y),$$
onde  $F'(x)$  é a série de potências formais da derivada definida como

$$F'(x) = \sum\limits_{i=0}^\infty (i+1)\alpha_{i+1}(x-\beta)^i,$$ 
e $G(x, y)$  é alguma série de potências formais de  $x$  e  $y$ . Com esse resultado, podemos encontrar a solução de maneira iterativa.

Seja  $F(Q_k) \equiv 0 \pmod{x^{a}}$ . Precisamos encontrar  $Q_{k+1} \equiv Q_k + x^a C \pmod{x^{2a}}$  tal que  $F(Q_{k+1}) \equiv 0 \pmod{x^{2a}}$ .

Substituindo  $x = Q_{k+1}$  e  $y=Q_k$  na fórmula acima, obtemos

$$F(Q_{k+1}) \equiv F(Q_k) + (Q_{k+1} - Q_k) F'(Q_k) + (Q_{k+1} - Q_k)^2 G(x, y) \pmod x^{2a}.$$ 
Como  $Q_{k+1} - Q_k \equiv 0 \pmod{x^a}$ , também vale que  $(Q_{k+1} - Q_k)^2 \equiv 0 \pmod{x^{2a}}$ , assim

$$0 \equiv F(Q_{k+1}) \equiv F(Q_k) + (Q_{k+1} - Q_k) F'(Q_k) \pmod{x^{2a}}.$$ 
A última fórmula nos dá o valor de  $Q_{k+1}$ :
$$\boxed{Q_{k+1} = Q_k - \dfrac{F(Q_k)}{F'(Q_k)} \pmod{x^{2a}}}$$ 
Assim, sabendo como inverter polinômios e como calcular  $F(Q_k)$ , podemos encontrar  $n$  coeficientes de  $P$  com complexidade

$$T(n) = T(n/2) + f(n),$$ 
onde  $f(n)$  é o tempo necessário para calcular  $F(Q_k)$  e  $F'(Q_k)^{-1}$ , que geralmente é  $O(n \log n)$ .

A regra iterativa acima é conhecida na análise numérica como Método de Newton.

#### Hensel's lemma

Como mencionado anteriormente, formalmente e genericamente, esse resultado é conhecido como o lema de Hensel e pode ser utilizado de fato de maneira mais ampla quando trabalhamos com uma série de anéis aninhados. Neste caso específico, trabalhamos com uma sequência de restos de polinômios módulo  $x$ ,  $x^2$ ,  $x^3$  e assim por diante.

Outro exemplo em que a elevação de Hensel pode ser útil são os chamados números p-ádicos, nos quais, de fato, trabalhamos com a sequência de restos inteiros módulo  $p$ ,  $p^2$ ,  $p^3$  e assim por diante. Por exemplo, o método de Newton pode ser usado para encontrar todos os números automórficos possíveis (números que terminam neles mesmos quando elevados ao quadrado) com uma determinada base numérica. O problema fica como um exercício para o leitor. Você pode considerar esse problema para verificar se sua solução funciona para números na base  $10$ .

### Logaritmo
Para a função  $\ln P(x)$ , é conhecido que:

$$ \boxed{(\ln P(x))' = \dfrac{P'(x)}{P(x)}} $$ 
Assim, podemos calcular  $n$  coeficientes de  $\ln P(x)$  em  $O(n \log n)$ .


### Série inversa
Acontece que podemos obter a fórmula para  $A^{-1}$  usando o método de Newton. Para isso, tomamos a equação  $A=Q^{-1}$ , assim:
 
$$F(Q) = Q^{-1} - A$$ 
$$F'(Q) = -Q^{-2}$$
$$\boxed{Q_{k+1} \equiv Q_k(2-AQ_k) \pmod{x^{2^{k+1}}}}$$

### Expoente
Vamos aprender a calcular  $e^{P(x)}=Q(x)$ . Deve valer que  $\ln Q = P$ , assim:
 
$$F(Q) = \ln Q - P$$
 
$$F'(Q) = Q^{-1}$$ 
$$\boxed{Q_{k+1} \equiv Q_k(1 + P - \ln Q_k) \pmod{x^{2^{k+1}}}}$$ 


### $k$ -ésima Potência  

Agora precisamos calcular  $P^k(x)=Q$ . Isso pode ser feito através da seguinte fórmula:
 
$$Q = \exp\left[k \ln P(x)\right]$$ 
Observe, no entanto, que você só pode calcular os logaritmos e exponenciais corretamente se puder encontrar algum  $Q_0$  inicial.

Para encontrá-lo, você deve calcular o logaritmo ou a exponencial do coeficiente constante do polinômio.

Mas a única maneira razoável de fazer isso é se  $P(0)=1$  para  $Q = \ln P$ , então  $Q(0)=0$  e se  $P(0)=0$  para  $Q = e^P$ , então  $Q(0)=1$ .

Assim, você pode usar a fórmula acima apenas se  $P(0) = 1$ . Caso contrário, se  $P(x) = \alpha x^t T(x)$  onde  $T(0)=1$ , você pode escrever que:
 
$$\boxed{P^k(x) = \alpha^kx^{kt} \exp[k \ln T(x)]}$$ 
Observe que você também pode calcular alguma raiz  $k$ -ésima de um polinômio se puder calcular  $\sqrt[k]{\alpha}$ , por exemplo, para  $\alpha=1$ .

## Avaliação e Interpolação
### Transformada Chirp-z
Para o caso específico em que você precisa avaliar um polinômio nos pontos  $x_r = z^{2r}$ , você pode fazer o seguinte:

$$A(z^{2r}) = \sum\limits_{k=0}^n a_k z^{2kr}$$ 
Vamos substituir  $2kr = r^2+k^2-(r-k)^2$ . Então, esta soma se reescreve como:

$$\boxed{A(z^{2r}) = z^{r^2}\sum\limits_{k=0}^n (a_k z^{k^2}) z^{-(r-k)^2}}$$ 
O que é, até o fator  $z^{r^2}$ , igual à convolução das sequências  $u_k = a_k z^{k^2}$  e  $v_k = z^{-k^2}$ .

Observe que  $u_k$  tem índices de  $0$  a  $n$  aqui e  $v_k$  tem índices de  $-n$  a  $m$ , onde  $m$  é a potência máxima de  $z$  que você precisa.

Agora, se você precisar avaliar um polinômio nos pontos  $x_r = z^{2r+1}$ , você pode reduzi-lo à tarefa anterior pela transformação  $a_k \to a_k z^k$ .

Isso nos dá um algoritmo  $O(n \log n)$  quando você precisa calcular valores em potências de  
$z$ , assim você pode calcular a Transformada Discreta de Fourier (DFT) para números que não são potências de dois.

Outra observação é que  $kr = \binom{k+r}{2} - \binom{k}{2} - \binom{r}{2}$ . Então, temos

$$\boxed{A(z^r) = z^{-\binom{r}{2}}\sum\limits_{k=0}^n \left(a_k z^{-\binom{k}{2}}\right)z^{\binom{k+r}{2}}}$$ 
O coeficiente de $x^{n+r}$  do produto dos polinômios  $A_0(x) = \sum\limits_{k=0}^n a_{n-k}z^{-\binom{n-k}{2}}x^k$  e    $A_1(x) = \sum\limits_{k\geq 0}z^{\binom{k}{2}}x^k$  é igual a  $z^{\binom{r}{2}}A(z^r)$ . Você pode usar a fórmula  $z^{\binom{k+1}{2}}=z^{\binom{k}{2}+k}$  para calcular os coeficientes de  $A_0(x)$  e  $A_1(x)$ .

### Avaliação em Múltiplos Pontos
Suponha que você precise calcular  $A(x_1), \dots, A(x_n)$ . Como mencionado anteriormente,  $A(x) \equiv A(x_i) \pmod{x-x_i}$ . Assim, você pode fazer o seguinte:

1. Calcule uma árvore de segmentos de modo que no segmento  $[l,r)$  esteja o produto  $P_{l, r}(x) = (x-x_l)(x-x_{l+1})\dots(x-x_{r-1})$ .
2. Começando com  $l=1$  e  $r=n+1$  na raiz da árvore, deixe  $m=\lfloor(l+r)/2\rfloor$ . Mova-se para baixo até  $[l,m)$  com o polinômio  $A(x) \pmod{P_{l,m}(x)}$ .
3. Isso calculará recursivamente  $A(x_l), \dots, A(x_{m-1})$ . Agora faça o mesmo para  $[m,r)$  com  $A(x) \pmod{P_{m,r}(x)}$ .
4. Concatene os resultados da primeira e segunda chamadas recursivas e retorne-os.

O procedimento inteiro será executado em  $O(n \log^2 n)$ .

### Interpolação
Existe uma fórmula direta de Lagrange para interpolar um polinômio, dado um conjunto de pares  
$(x_i, y_i)$ :
$$\boxed{A(x) = \sum\limits_{i=1}^n y_i \prod\limits_{j \neq i}\dfrac{x-x_j}{x_i - x_j}}$$ 
Calcular isso diretamente é uma tarefa difícil, mas acontece que podemos calculá-lo em  $O(n \log^2 n)$  com uma abordagem de dividir e conquistar:

Considere  $P(x) = (x-x_1)\dots(x-x_n)$ . Para conhecer os coeficientes dos denominadores em  
$A(x)$ , devemos calcular produtos como:

$$ P_i = \prod\limits_{j \neq i} (x_i-x_j) $$ 
Mas se você considerar a derivada  $P'(x)$ , descobrirá que  $P'(x_i) = P_i$ . Assim, você pode calcular os  $P_i$  via avaliação em  $O(n \log^2 n)$ .

Agora, considere o algoritmo recursivo feito na mesma árvore de segmentos que na avaliação em vários pontos. Ele começa nas folhas com o valor  $\dfrac{y_i}{P_i}$  em cada folha.

Quando retornamos da recursão, devemos mesclar os resultados dos vértices esquerdo e direito como  $A_{l,r} = A_{l,m}P_{m,r} + P_{l,m} A_{m,r}$ .

Dessa forma, quando você retornar à raiz, terá exatamente  $A(x)$  nela. O procedimento total também funciona em  $O(n \log^2 n)$ .

## Máximo Divisor Comum (MDC) e Resultantes
Suponha que você tenha os polinômios  $A(x) = a_0 + a_1 x + \dots + a_n x^n$  e  $B(x) = b_0 + b_1 x + \dots + b_m x^m$ .

Deixe  $\lambda_0, \dots, \lambda_n$  serem as raízes de  $A(x)$  e deixe  $\mu_0, \dots, \mu_m$  serem as raízes de  $B(x)$  contadas com suas multiplicidades.

Você deseja saber se  $A(x)$  e  $B(x)$  têm alguma raiz em comum. Existem duas maneiras interconectadas de fazer isso.

### Algoritmo de Euclides
Bem, já temos um artigo sobre isso. Para um domínio arbitrário, você pode escrever o algoritmo de Euclides tão facilmente quanto:

```cpp
template<typename T>
T gcd(const T &a, const T &b) {
    return b == T(0) ? a : gcd(b, a % b);
}
```
Pode ser comprovado que, para polinômios  $A(x)$  e  $B(x)$ , isso funcionará em  $O(nm)$ .

### Resultante
Vamos calcular o produto  $A(\mu_0)\cdots A(\mu_m)$ . Isso será igual a zero se e somente se algum  $\mu_i$  for raiz de  $A(x)$ .

Para simetria, também podemos multiplicá-lo por  $b_m^n$  e reescrever o produto inteiro na seguinte forma:
 
$$\boxed{\mathcal{R}(A, B) = b_m^n\prod\limits_{j=0}^m A(\mu_j) = b_m^n a_m^n \prod\limits_{i=0}^n \prod\limits_{j=0}^m (\mu_j - \lambda_i)= (-1)^{mn}a_n^m \prod\limits_{i=0}^n B(\lambda_i)}$$ 
O valor definido acima é chamado de resultante dos polinômios  $A(x)$  e  $B(x)$ . Da definição, você pode encontrar as seguintes propriedades:
 
1. $\mathcal R(A, B) = (-1)^{nm} \mathcal R(B, A)$ .
 
2. $\mathcal R(A, B)= a_n^m b_m^n$  quando  $n=0$  ou  $m=0$ .
3. Se  $b_m=1$ , então  $\mathcal R(A - CB, B) = \mathcal R(A, B)$  para um polinômio arbitrário  $C(x)$  e  $n,m \geq 1$ .
4. Daqui segue que  $\mathcal R(A, B) = b_m^{\deg(A) - \deg(A-CB)}\mathcal R(A - CB, B)$  para  $A(x)$ ,  $B(x)$  e  $C(x)$  arbitrários.

Milagrosamente, isso significa que a resultante de dois polinômios é sempre do mesmo anel que seus coeficientes!

Essas propriedades também nos permitem calcular a resultante junto com o algoritmo de Euclides, que funciona em  $O(nm)$ .

```cpp
template<typename T>
T resultant(poly<T> a, poly<T> b) {
    if(b.is_zero()) {
        return 0;
    } else if(b.deg() == 0) {
        return bpow(b.lead(), a.deg());
    } else {
        int pw = a.deg();
        a %= b;
        pw -= a.deg();
        base mul = bpow(b.lead(), pw) * base((b.deg() & a.deg() & 1) ? -1 : 1);
        base ans = resultant(b, a);
        return ans * mul;
    }
}
```



### Algoritmo Half-GCD
Existe uma maneira de calcular o MDC e as resultantes em  $O(n \log^2 n)$ .

O procedimento para fazer isso implementa uma transformação linear de  $2 \times 2$  que mapeia um par de polinômios  $a(x)$ ,  $b(x)$  em outro par  $c(x), d(x)$  de modo que  $\deg d(x) \leq \frac{\deg a(x)}{2}$ . Se você for cuidadoso o suficiente, pode calcular o meio-MDC de qualquer par de polinômios com no máximo  $2$  chamadas recursivas aos polinômios que são pelo menos  $2$  vezes menores.

Os detalhes específicos do algoritmo são um tanto tediosos de explicar, no entanto, você pode encontrar sua implementação na biblioteca, como a função `half_gcd`.

Após a implementação do half-GCD, você pode aplicá-lo repetidamente a polinômios até ser reduzido ao par  $\gcd(a, b)$  e  $0$ .