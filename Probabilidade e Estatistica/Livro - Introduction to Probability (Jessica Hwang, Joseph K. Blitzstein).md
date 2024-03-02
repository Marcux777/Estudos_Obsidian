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

### Definição 1.4.14 (Coeficiente binomial). 
Para quaisquer inteiros não negativos k e n, o coeficiente binomial $$\binom{n}{k}$$, lido como "n escolhe k", é o número de subconjuntos de tamanho k para um conjunto de tamanho n.

Por exemplo, $$\binom{4}{2} = 6$$, conforme mostrado no Exemplo 1.4.13. O coeficiente binomial $$\binom{n}{k}$$ às vezes é chamado de combinação, mas não usamos essa terminologia aqui, pois "combinação" é uma palavra de uso geral muito útil. Algebricamente, os coeficientes binomiais podem ser calculados da seguinte maneira.

### Teorema 1.4.15 (Fórmula do coeficiente binomial). 
Para k ≤ n, temos
$$\binom{n}{k} = \frac{n(n - 1) \cdot \ldots \cdot (n - k + 1)}{k!} = \frac{n!}{(n - k)!k!}.$$

Para k > n, temos $$\binom{n}{k} = 0$$.

Prova. Seja A um conjunto com |A| = n. Qualquer subconjunto de A tem tamanho no máximo n, então $$\binom{n}{k} = 0$$para k > n. Agora, deixe k ≤ n. Pelo Teorema 1.4.8, existem n(n - 1) · · · (n - k + 1) maneiras de fazer uma escolha ordenada de k elementos sem reposição. Isso superconta cada subconjunto de interesse por um fator de k! (já que não nos importamos com a ordem desses elementos), então podemos obter a contagem correta dividindo por k!.

### Observação 1.4.16. 
O coeficiente binomial $$\binom{n}{k}$$ é frequentemente definido em termos de fatoriais, mas lembre-se de que $$\binom{n}{k} = 0$$ se k > n, mesmo que o fatorial de um número negativo seja indefinido. Além disso, a expressão do meio no Teorema 1.4.15 é frequentemente melhor para cálculo do que a expressão com fatoriais, pois os fatoriais crescem extremamente rápido. Por exemplo, $$\binom{100}{2} = \frac{100 \cdot 99}{2} = 4950$$ pode até ser feito à mão, enquanto calcular $$\binom{100}{2} = \frac{100!}{98!\cdot2!}$$ calculando primeiro 100! e 98! seria desperdício e possivelmente perigoso por causa dos números extremamente grandes envolvidos ($100! ≈ 9.33 × 10^{157}$).

### Exemplo 1.4.19 (Teorema Binomial). 
O teorema binomial afirma que
$$(x + y)^n = \sum_{k=0}^{n} {n \choose k} x^k y^{n-k},$$

Para qualquer inteiro não negativo `n`. Para provar o teorema binomial, expanda o produto
$$(x + y)(x + y) \ldots (x + y)$$
Assim como $(a + b)(c + d) = ac + ad + bc + bd$ é a soma dos termos onde escolhemos `a` ou `b` do primeiro fator (mas não ambos) e `c` ou `d` do segundo fator (mas não ambos), os termos de $(x + y)^n$ são obtidos escolhendo `x` ou `y` (mas não ambos) de cada fator. Existem ${n \choose k}$ maneiras de escolher exatamente `k` dos `x's`, e cada uma dessas escolhas produz o termo $x^k y^{n-k}$. O teorema binomial segue.

Podemos usar coeficientes binomiais para calcular probabilidades em muitos problemas para os quais a definição ingênua se aplica.

#### Exemplo 1.4.20 (Full house no pôquer). 
Uma mão de 5 cartas é distribuída de um baralho padrão de 52 cartas, bem embaralhado. A mão é chamada de full house no pôquer se consiste em três cartas de algum naipe e duas cartas de outro naipe, por exemplo, três 7's e dois 10's (em qualquer ordem). Qual é a probabilidade de um full house?

Solução:
Todas as ${52 \choose 5}$ mãos possíveis são igualmente prováveis por simetria, então a definição ingênua é aplicável. Para encontrar o número de mãos de full house, use a regra da multiplicação (e imagine a árvore). Existem 13 escolhas para o naipe do qual temos três cartas; para concretizar, suponha que temos três 7's e foque nesse ramo da árvore. Existem ${4 \choose 3}$ maneiras de escolher quais 7's temos. Então, existem 12 escolhas para o naipe do qual temos duas cartas, digamos 10's para concretizar, e ${4 \choose 2}$ maneiras de escolher dois 10's. Assim,
$$P(\text{full house}) = \frac{13{4 \choose 3}12{4 \choose 2}}{{52 \choose 5}} = \frac{3744}{2598960} \approx 0.00144.$$
A aproximação decimal é mais útil ao jogar pôquer, mas a resposta em termos de coeficientes binomiais é exata e autoanotada (ver ${52 \choose 5}$ é uma dica muito maior sobre sua origem do que ver 2598960).

### Exemplo 1.4.21 (Problema de Newton-Pepys). 
Isaac Newton foi consultado sobre o seguinte problema por Samuel Pepys, que queria a informação para fins de jogo. Qual dos seguintes eventos tem a maior probabilidade?
A: Pelo menos um 6 aparece quando 6 dados justos são lançados.
B: Pelo menos dois 6's aparecem quando 12 dados justos são lançados.
C: Pelo menos três 6's aparecem quando 18 dados justos são lançados.

Solução:
Os três experimentos têm $6^6$, $6^{12}$ e $6^{18}$ resultados possíveis, respectivamente, e por simetria, a definição ingênua se aplica em todos os três experimentos.
A: Em vez de contar o número de maneiras de obter pelo menos um 6, é mais fácil contar o número de maneiras de não obter nenhum 6. Não obter nenhum 6 é equivalente a amostrar os números de 1 a 5 com reposição 6 vezes, então $5^6$ resultados são favoráveis a $A^c$ (e $6^6 - 5^6$ são favoráveis a A). Assim,
$$P(A) = 1 - \frac{5^6}{6^6} \approx 0.67.$$
B: Novamente, contamos primeiro os resultados em $B^c$. Existem 5^12 maneiras de não obter nenhum 6 em 12 lançamentos de dados. Existem ${12 \choose 1}5^{11}$ maneiras de obter exatamente um 6: primeiro escolhemos qual dado cairá 6, depois amostramos os números de 1 a 5 com reposição para os outros 11 dados. Somando estes, obtemos o número de maneiras de falhar em obter pelo menos dois 6's. Então,
$$P(B) = 1 - \frac{5^{12} + {12 \choose 1}5^{11}}{6^{12}} \approx 0.62.$$
C: Contamos os resultados em $C^c$, ou seja, o número de maneiras de obter zero, um ou dois 6's em 18 lançamentos de dados. Existem $5^{18}$ maneiras de não obter nenhum 6, ${18 \choose 1}5^{17}$ maneiras de obter exatamente um 6, e ${18 \choose 2}5^{16}$ maneiras de obter exatamente dois 6's (escolha quais dois dados cairão 6, depois decida como os outros 16 dados cairão).
$$P(C) = 1 - \frac{5^{18} + {18 \choose 1}5^{17} + {18 \choose 2}5^{16}}{6^{18}} \approx 0.60.$$
Portanto, A tem a maior probabilidade.
Newton chegou à resposta correta usando cálculos semelhantes. Newton também forneceu a Pepys um argumento intuitivo de por que A era o mais provável dos três; no entanto, sua intuição era inválida. Como explicado em Stigler [24], o uso de dados carregados poderia resultar em uma ordenação diferente de A, B, C, mas o argumento intuitivo de Newton não dependia dos dados serem justos.
Neste livro, nos importamos com a contagem não por si só, mas porque às vezes nos ajuda a encontrar probabilidades. Aqui está um exemplo de um problema de contagem elegante, mas traiçoeiro; a solução é elegante, mas é raro que o resultado possa ser usado com a definição ingênua de probabilidade.

### Exemplo 1.4.22 (Bose-Einstein). 
Quantas maneiras existem de escolher `k` vezes de um conjunto de `n` objetos com reposição, se a ordem não importa (só nos importamos com quantas vezes cada objeto foi escolhido, não a ordem em que foram escolhidos)?
Solução:
Quando a ordem importa, a resposta é $n^k$ pela regra da multiplicação, mas este problema é muito mais difícil. Vamos resolvê-lo resolvendo um problema isomorfo (o mesmo problema sob uma forma diferente).
Vamos encontrar o número de maneiras de colocar `k` partículas indistinguíveis em `n` caixas distinguíveis. Ou seja, trocar as partículas de qualquer maneira não é considerado uma possibilidade separada: tudo o que importa são as contagens de quantas partículas estão em cada caixa.
Este cenário é conhecido como um problema de Bose-Einstein, uma vez que os físicos Satyendra Nath Bose e Albert Einstein estudaram problemas relacionados sobre partículas indistinguíveis na década de 1920, usando suas ideias para prever com sucesso a existência de um estranho estado da matéria conhecido como condensado de Bose-Einstein.