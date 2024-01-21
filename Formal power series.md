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