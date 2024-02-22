Teoria apenas
## Espaço amostral e Evento

A ferramenta de trabalho matemática para probabilidade é construída em volta de conjuntos.

O espaço amostral $S$ de um experimento é o conjunto de todas os possíveis resultados de um experimento. Um evento $A$ é um subconjunto de um espaço amostral $S$, e dizemos que o evento ocorreu se pertencer ao subconjunto $A$. 

O espaço amostral de um experimento pode ser finito, infinito contável ou infinito não contável.

Teoria dos conjuntos é bem útil em probabilidade, desde que isso expresse uma rica linguagem de e trabalho com os eventos.

**Exemplo 1.2.2 (Lançamento de moedas).** Uma moeda é lançada 10 vezes. Escrevendo "Heads" como H e "Tails" como T, um possível resultado (pérola) é HHHT HHT T HT e o espaço amostral é o conjunto de todas as sequências possíveis de comprimento 10 de H's e T's. Podemos (e iremos) codificar H como 1 e T como 0, de modo que um resultado seja uma sequência (s1, . . . , s10) com $s_{j}$ ∈ {0, 1}, e o espaço amostral é o conjunto de todas essas sequências. Agora, vamos analisar alguns eventos:

1. Seja A1 o evento de que o primeiro lançamento é "Heads". Como um conjunto, $A1 = \{(1, s2, . . . , s10)$ : $s_{j}$ ∈ ${0, 1}$ ${ para }$ 2 ≤ j ≤ 10\}$ . Isso é um subconjunto do espaço amostral, portanto, é de fato um evento; dizer que A1 ocorre é a mesma coisa que dizer que o primeiro lançamento é "Heads". Da mesma forma, seja $A_{j}$ o evento de que o $j$-ésimo lançamento é "Heads" para $j = 2, 3, . . . , 10.$

2. Seja B o evento de que pelo menos um lançamento foi "Heads". Como um conjunto, $[B = \bigcup_{j=1}^{10} Aj.]$

3. Seja C o evento de que todos os lançamentos foram "Heads". Como um conjunto, $[C = \bigcap_{j=1}^{10} Aj.]$

4. Seja D o evento de que houve pelo menos dois "Heads" consecutivos. Como um conjunto, $[D = \bigcup_{j=1}^{9} (Aj ∩ Aj+1).]$

## Definição ingênua de probabilidade

Historicamente, a forma mais simples de definir probabilidade de um evento é contar o numero de ocorrências de um evento e dividir pelo total de resultados possíveis do experimento. 

Seja $A$ um evento de um experimento com um espaço amostral finito denominado $S$. A probabilidade ingênua de $A$ seria:
$P_{\text{naive}}(A) = \frac{|A|}{|S|}$
onde:
- \(|A|\) é o número de resultados favoráveis a \(A\).
- \(|S|\) é o número total de resultados em \(S\).

Uma boa estratégia ao tentar encontrar a probabilidade de um evento é começar pensando se será mais fácil encontrar a probabilidade do evento ou a probabilidade do seu complemento. As leis de De Morgan são especialmente úteis nesse contexto, pois pode ser mais fácil trabalhar com uma interseção do que com uma união, ou vice-versa.

# Como contar

## Regra da Multiplicação

Considerando dois sub-experimentos, um experimento $A$ e um experimento $B$. Supondo que $A$ tenha $a$ possíveis resultados e $B$ tenha $b$ possíveis resultados, então esse experimento terá $ab$ possíveis resultados. 

### Exemplo 1.4.3 (Corredores). 
Suponha que 10 pessoas estão correndo uma corrida. Assuma que empates não são possíveis e que todos os 10 completarão a corrida, então haverá bem definidos primeiro, segundo e terceiro lugares. Quantas possibilidades existem para os vencedores do primeiro, segundo e terceiro lugar?
Solução: Existem 10 possibilidades para quem fica em primeiro lugar, então, uma vez que isso é fixado, existem 9 possibilidades para quem fica em segundo lugar, e uma vez que ambos são fixados.

![[Pasted image 20240206172609.png]]



### Amostragem com reposição

Considerando n objetos e fazendo k escolhas dentre eles, uma de cada vez com reposição (ou seja, escolher um determinado objeto não impede que ele seja escolhido novamente). Disso são $n^{k}$ possiveis resultados. 

### Amostragem sem reposição

Considerando $n$ objetos e fazendo $k$ escolhas dentre eles, uma de cada vez sem reposição (ou seja, escolher um determinado objeto impede que ele seja escolhido novamente). Então, há$n(n−1)⋅⋅⋅(n−k+1)$ possíveis resultados para $1 ≤ k ≤ n$, e $0$ possibilidades para $k > n$ (onde a ordem importa). Por convenção, $n(n − 1) · · · (n − k + 1) = n$ para $k = 1$.

### Permutação 


