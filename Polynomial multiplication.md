
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

### Exemplo

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

### Exemplo

	Você joga um dado de  $6$  lados  $n$  vezes e soma os resultados de todos os lançamentos. Qual é a probabilidade de obter uma soma de  $k$ ?

**Solução**

	A resposta é o número de resultados que têm a soma  $k$ , dividido pelo número total de resultados, que é  $6^n$ .
	
	Qual é o número de resultados que têm a soma  $k$ ? Para  $n=1$ , pode ser representado por um polinômio  $A(x) = x^1+x^2+\dots+x^6$ .
	
	Para  $n=2$ , usando a mesma abordagem do exemplo acima, concluímos que é representado pelo polinômio  $(x^1+x^2+\dots+x^6)^2$ .
	
	Dito isso, a resposta para o problema é o coeficiente  $k$ -ésimo de  $(x^1+x^2+\dots+x^6)^n$ , dividido por  $6^n$ .


O coeficiente próximo a  $x^k$  no polinômio  $A(x)$  é denotado brevemente como  $[x^k]A$ .