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

Considerando $n$ objetos e fazendo $k$ escolhas dentre eles, uma de cada vez com reposição (ou seja, escolher um determinado objeto não impede que ele seja escolhido novamente). Disso são $n^{k}$ possíveis resultados. 

### Amostragem sem reposição

Considerando $n$ objetos e fazendo $k$ escolhas dentre eles, uma de cada vez sem reposição (ou seja, escolher um determinado objeto impede que ele seja escolhido novamente). Então, há$n(n−1)⋅⋅⋅(n−k+1)$ possíveis resultados para $1 ≤ k ≤ n$, e $0$ possibilidades para $k > n$ (onde a ordem importa). Por convenção, $n(n − 1) · · · (n − k + 1) = n$ para $k = 1$.

### Exemplo 1.4.10 (Problema do aniversário). 
Existem k pessoas em uma sala. Suponha que o aniversário de cada pessoa seja igualmente provável de ser qualquer um dos 365 dias do ano (excluímos 29 de fevereiro), e que os aniversários das pessoas são independentes (definiremos independência formalmente mais tarde, mas intuitivamente significa que saber os aniversários de algumas pessoas não nos dá nenhuma informação sobre os aniversários de outras pessoas; isso não seria válido se, por exemplo, soubéssemos que duas das pessoas são gêmeas). Qual é a probabilidade de que pelo menos um par de pessoas no grupo tenha o mesmo aniversário?

O problema do aniversário é um problema clássico de probabilidade. Aqui está a solução:

Existem $365^{k}$ maneiras de atribuir aniversários às pessoas na sala, já que podemos imaginar os 365 dias do ano sendo amostrados k vezes, com reposição. Por suposição, todas essas possibilidades são igualmente prováveis, então a definição ingênua de probabilidade se aplica.

Usada diretamente, a definição ingênua diz que só precisamos contar o número de maneiras de atribuir aniversários a k pessoas de modo que haja duas pessoas que compartilham um aniversário.

Mas esse problema de contagem é difícil, já que poderia ser Emma e Steve que compartilham um aniversário, ou Steve e Naomi, ou todos os três, ou os três poderiam compartilhar um aniversário enquanto duas outras pessoas no grupo compartilham um aniversário diferente, ou várias outras possibilidades.

Em vez disso, vamos contar o complemento: o número de maneiras de atribuir aniversários a k pessoas de modo que nenhuma dupla de pessoas compartilhe um aniversário. Isso equivale a amostrar os 365 dias do ano sem reposição, então o número de possibilidades é 365 · 364 · 363 · · · (365 - k + 1) para k ≤ 365. Portanto, a probabilidade de não haver correspondências de aniversário em um grupo de k pessoas é

$$P (\text{sem correspondência de aniversário}) = \frac{365 · 364 · · · (365 - k + 1)}{365^k}$$

e a probabilidade de pelo menos uma correspondência de aniversário é

$$P (\text{pelo menos 1 correspondência de aniversário}) = 1 - \frac{365 · 364 · · · (365 - k + 1)}{365^k}$$

O primeiro valor de k para o qual a probabilidade de uma correspondência excede 0,5 é k = 23. Assim, em um grupo de 23 pessoas, há uma chance maior que 50% de que haja pelo menos uma correspondência de aniversário. Em k = 57, a probabilidade de uma correspondência já excede 99%.

![[Pasted image 20240226173805.png]]

Claro, para k = 366, temos garantia de uma correspondência, mas é surpreendente que mesmo com um número muito menor de pessoas, é extremamente provável que haja uma correspondência de aniversário. Para uma intuição rápida de por que isso não deve ser tão surpreendente, note que com 23 pessoas existem (23 escolhe 2) = 253 pares de pessoas, qualquer um dos quais poderia ser uma correspondência de aniversário.

Os problemas 26 e 27 mostram que o problema do aniversário é muito mais do que um jogo divertido de festa e muito mais do que uma maneira de construir intuição sobre coincidências; também existem aplicações importantes em estatística e ciência da computação. O problema 62 explora o cenário mais geral em que a probabilidade não é necessariamente 1/365 para cada dia. Acontece que no caso de probabilidade não igual, ter pelo menos uma correspondência se torna ainda mais provável.

### 1.4.2 Ajustando para supercontagem
Em muitos problemas de contagem, não é fácil contar cada possibilidade uma vez e apenas uma vez. No entanto, se formos capazes de contar cada possibilidade exatamente c vezes para algum c, então podemos ajustar dividindo por c. Por exemplo, se tivermos contado exatamente cada possibilidade duas vezes, podemos dividir por 2 para obter a contagem correta. Chamamos isso de ajuste para supercontagem.

