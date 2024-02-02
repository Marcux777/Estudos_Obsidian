
Esta equação é da forma:

$$a \cdot x \equiv b \pmod n,$$ 
onde  $a$ ,  $b$  e  $n$  são inteiros dados e  $x$  é um inteiro desconhecido.

É necessário encontrar o valor de  $x$  no intervalo  $[0, n-1]$  (claramente, em toda a reta numérica, pode haver infinitas soluções que diferem entre si em  $n \cdot k$  , onde  $k$  é qualquer inteiro). Se a solução não for única, então consideraremos como obter todas as soluções.

## Solução encontrando o elemento inverso
Vamos primeiro considerar um caso mais simples onde  $a$  e  $n$  são coprimos ( $\gcd(a, n) = 1$ ). Então, pode-se encontrar o [inverso](obsidian://open?vault=Algoritmos&file=algoritmos%2FArtigos%2FAlgebra%2FModular%20arithmetic%2FModular%20Inverse%2FInverso%20Multiplicativo%20Modular) de  $a$ , e multiplicando ambos os lados da equação pelo inverso, podemos obter uma solução única.
 
$$x \equiv b \cdot a ^ {- 1} \pmod n$$ 
Agora, considere o caso em que  $a$  e  $n$  não são coprimos ( $\gcd(a, n) \ne 1$ ). Nesse caso, a solução nem sempre existirá (por exemplo,  
$2 \cdot x \equiv 1 \pmod 4$  não tem solução).

Seja  $g = \gcd(a, n)$ , ou seja, o [maior divisor comum](obsidian://open?vault=Algoritmos&file=algoritmos%2FArtigos%2FAlgebra%2FAlgoritmo%20de%20Euclides%20para%20calcular%20o%20maior%20divisor%20comum%2FAlgoritmo%20-%20Algoritmo%20de%20Euclides%20para%20calcular%20o%20maior%20divisor%20comum) de  $a$  e  $n$  (que neste caso é maior que um).

Então, se  $b$  não é divisível por  $g$ , não há solução. De fato, para qualquer  $x$ , o lado esquerdo da equação  $a \cdot x \pmod n$  , é sempre divisível por  $g$ , enquanto o lado direito não é divisível por ele, portanto, segue-se que não há soluções.

Se  $g$  divide  $b$ , então, dividindo ambos os lados da equação por  $g$  (ou seja, dividindo  $a$ ,  $b$  e  $n$  por  $g$ ), recebemos uma nova equação:
 
$$a^\prime \cdot x \equiv b^\prime \pmod{n^\prime}$$ 
na qual  $a^\prime$  e  $n^\prime$  já são primos entre si, e já aprendemos como lidar com tal equação. Obtemos  $x^\prime$  como solução para  $x$ .

É claro que este  $x^\prime$  também será uma solução da equação original. No entanto, não será a única solução. Pode-se mostrar que a equação original tem exatamente  $g$  soluções, e elas serão assim:

$$x_i \equiv (x^\prime + i\cdot n^\prime) \pmod n \quad \text{para } i = 0 \ldots g-1$$ 
Resumindo, podemos dizer que o número de soluções da equação congruente linear é igual a  $g = \gcd(a, n)$  ou a zero.

## Solução com o Algoritmo Euclidiano Estendido
Podemos reescrever a congruência linear para a seguinte equação diofantina:
$$a \cdot x + n \cdot k = b,$$ 
onde  $x$  e  $k$  são inteiros desconhecidos.

O método de resolução desta equação é descrito no artigo correspondente sobre [[Equações Diofantinas Lineares]] e consiste na aplicação do [Algoritmo Euclidiano Estendido](obsidian://open?vault=Estudos_Obsidian&file=Computa%C3%A7%C3%A3o%2FOne%20for%20All%2FArtigos%2FAlgebra%2FAlgoritmo%20de%20Euclides%20Estendido%2FAlgoritmo%20de%20Euclides%20Estendido).

Ele também descreve o método de obtenção de todas as soluções desta equação a partir de uma solução encontrada, e incidentalmente este método, quando cuidadosamente considerado, é absolutamente equivalente ao método descrito na seção anterior.