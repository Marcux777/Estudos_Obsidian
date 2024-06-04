# Ant Colony Optimization - Otimização Colonia de Formigas

  
  

## Introdução

  

### Inspiração e Princípios Básicos

  

O primeiro algoritmo ACO, o Ant System (AS), foi proposto em 1991 para resolver o problema do caixeiro viajante (TSP). Embora não fosse competitivo com os algoritmos TSP de última geração, o AS estimulou pesquisas adicionais sobre variantes algorítmicas e aplicações.

  

A Otimização por Colônia de Formigas (ACO) é um algoritmo metaheurístico inspirado no comportamento forrageiro de formigas reais. As formigas depositam rastros de feromônios enquanto se movem, guiando outras formigas para caminhos mais eficientes. A ACO imita esse comportamento usando uma população de "formigas artificiais" que constroem soluções para um problema de otimização. Cada formiga segue probabilisticamente um caminho baseado nos rastros de feromônios e em informações heurísticas.

  

### BioInspiração

  

A Otimização por Colônia de Formigas (ACO) é uma técnica de otimização computacional bioinspirada no comportamento de formigas reais. Os algoritmos ACO foram inspirados em um experimento realizado por Goss et al., no qual uma colônia de formigas argentinas (Iridomyrmex humilis) tinha acesso a uma fonte de alimento em uma arena conectada ao ninho por uma ponte com dois ramos de comprimentos diferentes. As formigas, ao se deslocarem entre o ninho e a fonte de alimento, precisavam escolher um dos ramos.

  

Observou-se que, após uma fase inicial de exploração, a maioria das formigas passava a utilizar o ramo mais curto. Além disso, a probabilidade de a colônia escolher o ramo mais curto aumentava com a diferença de comprimento entre os dois ramos. Esse comportamento de seleção do caminho mais curto pode ser explicado em termos de autocatálise (feedback positivo) e da diferença de comprimento do caminho.

As formigas argentinas, ao se deslocarem do ninho para a fonte de alimento e vice-versa, depositam uma substância química chamada feromônio no chão. Ao chegarem a um ponto de decisão, como a interseção entre os ramos esquerdo e direito, elas fazem uma escolha probabilística, influenciada pela quantidade de feromônio que sentem em cada ramo. Este comportamento tem um efeito autocatalítico, pois o próprio ato de escolher um caminho aumenta a probabilidade de ele ser escolhido novamente por formigas futuras. No início do experimento, não há feromônio em nenhum dos ramos, portanto, as formigas que saem do ninho em direção à fonte de alimento escolherão qualquer um dos dois ramos com igual probabilidade. Devido à diferença de comprimento dos ramos, as formigas que escolherem o ramo mais curto serão as primeiras a chegar à fonte de alimento. Ao retornarem para o ninho e chegarem ao ponto de decisão, elas verão um rastro de feromônio no caminho mais curto, o rastro que elas mesmas liberaram durante a viagem de ida, e o escolherão com maior probabilidade do que o caminho mais longo.

  

### Componentes Essenciais da ACO

  

- População de Formigas Artificiais: Um conjunto de formigas artificiais que constroem soluções para o problema de otimização.

  

- Rastros de Feromônios: Uma matriz que armazena a intensidade do feromônio em cada aresta do problema.

  

- Função de Avaliação: Uma função que mede a qualidade de uma solução construída por uma formiga artificial.

  

- Regras de Construção de Solução: Regras probabilísticas que guiam as formigas artificiais na construção de soluções, levando em consideração os rastros de feromônio e as informações heurísticas.

  

- Atualização de Feromônios: Um mecanismo que altera a intensidade dos rastros de feromônio com base na qualidade das soluções construídas.

  

### Caracteristicas da ACO

  

- ACO é baseado no comportamento coletivo das formigas: As formigas são capazes de encontrar boas fontes de alimento seguindo trilhas de feromônios deixadas por outras formigas. Os algoritmos ACO usam esse mesmo princípio para buscar boas soluções para problemas de otimização.

- Os algoritmos ACO são probabilísticos: Isso significa que há uma chance de uma formiga escolher um caminho que não é o melhor caminho. No entanto, com o tempo, as formigas têm mais probabilidade de escolher os melhores caminhos porque eles serão reforçados pelas trilhas de feromônios.

- Os algoritmos ACO são distribuídos: As formigas não precisam ter nenhum controle central. Eles podem simplesmente seguir as trilhas de feromônios uns aos outros.

- Os algoritmos ACO são robustos: Podem funcionar bem mesmo quando o problema é grande ou complexo.

  

### Aplicações da ACO

  

A ACO foi aplicada com sucesso a uma ampla gama de problemas de otimização, incluindo:

  

- Problema do Caixeiro Viajante (TSP): Encontrar o caminho mais curto para visitar um conjunto de cidades.

  

- Problema de Roteamento de Veículos (VRP): Planejar rotas eficientes para uma frota de veículos.

  

- Problemas de Agendamento: Atribuir tarefas a recursos com o objetivo de minimizar o tempo de conclusão ou maximizar a utilização dos recursos.

  

- Agrupamento de Dados: Dividir um conjunto de dados em grupos distintos com base em características comuns.

  

- Classificação de Dados: Prever a classe a que um novo dado pertence.

  

## Definição Formal

  

O primeiro passo para a aplicação do ACO a um problema de otimização combinatória (COP) consiste em definir um modelo do COP como uma trinca $(S,Ω,f)$, onde:

  

- $S$ é um espaço de busca definido sobre um conjunto finito de variáveis de decisão discretas;

  

- $Ω$ é um conjunto de restrições entre as variáveis; e

  

- $f:S→R+0$ é uma função objetivo a ser minimizada (como maximizar sobre $f$ é o mesmo que minimizar sobre $-f$, todo COP pode ser descrito como um problema de minimização).

  

O espaço de busca $S$ é definido da seguinte forma. Um conjunto de variáveis discretas $X_i$, $i=1,…,n$, com valores $v_{i}^{j} ∈ Di={v^1_i,…,v^{|Di|}_i}$, é dado. Elementos de S são atribuições completas, ou seja, atribuições nas quais cada variável $X_i$ tem um valor $v^j_i$ atribuído de seu domínio $D_i$. O conjunto de soluções viáveis $S_Ω$ é dado pelos elementos de $S$ que satisfazem todas as restrições no conjunto $Ω$.

  

Uma solução $s^{∗}∈ S_{Ω}$ é chamada de ótimo global se e somente se

<font size="3">

$$f(s^{∗})≤f(s) ∀s∈S_{Ω}$$

</font>

O conjunto de todas as soluções globalmente ótimas é denotado por $S^{*}_Ω⊆S_Ω$. Resolver um COP requer encontrar pelo menos um $s^{∗}∈S^∗_Ω$.

  

## Algoritmo

  

### Ant System (AS)

  

O Ant System (AS) é o primeiro algoritmo ACO proposto na literatura.

No AS, formigas artificiais constroem iterativamente soluções (caminhos em um grafo) e depositam feromônios nas arestas que percorreram. A quantidade de feromônio depositada é inversamente proporcional ao custo da solução (comprimento do caminho). As arestas com feromônio mais alto são mais propensas a serem escolhidas pelas formigas nas próximas iterações.

  

O AS tem duas fases principais:

  

1. Construção da Solução: Formigas artificiais constroem soluções incrementalmente, escolhendo a próxima cidade a visitar com base em uma regra de probabilidade que leva em conta a trilha de feromônio e informações heurísticas (como a distância entre as cidades).

  

2. Atualização do Feromônio: Após todas as formigas terem construído suas soluções, as trilhas de feromônio são atualizadas. Primeiro, o feromônio em todas as arestas evapora a uma taxa fixa. Em seguida, as formigas depositam feromônio nas arestas que percorreram, com a quantidade de feromônio depositada sendo inversamente proporcional ao comprimento do caminho percorrido.

  

A regra de probabilidade para a escolha da próxima cidade é:
<font size="4">

$$ p(c_i^j | s_p) = \frac{{\tau_{ij}^\alpha * [\eta(c_i^j)]^\beta}}{{\sum {\tau_{il}^\alpha * [\eta(c_i^l)]^\beta}}}, \forall c_i^j \in N(s_p) $$

</font>

Onde:

  

- $p(c_i^j | s_p)$ é a probabilidade de escolher a cidade $j$ dado o estado atual $s_p$.

- $\tau_{ij}$ é a quantidade de feromônio na aresta entre as cidades $i$ e $j$.

- $\eta(c_i^j)$ é a informação heurística (por exemplo, o inverso da distância) associada à escolha da cidade $j$.

- $\alpha$ e $\beta$ são parâmetros que controlam a importância relativa do feromônio e da informação heurística.

  

A atualização do feromônio é feita da seguinte forma:

<font size="5">

$$τ_ij = (1 - ρ) * τ_ij + ΣΔτ_ij^k$$

</font>

Onde:

  

- $\rho$ é a taxa de evaporação do feromônio.

- $\Delta\tau_{ij}^k$ é a quantidade de feromônio depositada pela formiga $k$ na aresta $(i, j)$.

  

### Ant Colony System (ACS)

  

O Ant Colony System (ACS) é uma variante do algoritmo Ant System (AS) que busca melhorar o desempenho da otimização por colônia de formigas, aumentando a importância da exploração da informação coletada por formigas anteriores em relação à exploração do espaço de busca. Ele introduz duas modificações principais em relação ao AS:

  

1.  **Regra de Escolha Pseudo-Aleatória Proporcional:** As formigas escolhem o próximo componente da solução (por exemplo, a próxima cidade a visitar no problema do caixeiro viajante) usando a regra pseudo-aleatória proporcional. Com uma probabilidade $q_0$ (onde $0 \le q_0 < 1$), elas se movem para o componente com o maior produto entre a trilha de feromônio e a informação heurística. Com probabilidade $1 - q_0$, elas realizam uma exploração tendenciosa, usando a mesma regra de decisão probabilística do AS.

  

2.  **Atualização Local do Feromônio:** As formigas atualizam as trilhas de feromônio enquanto constroem suas soluções. Ao visitar uma aresta, elas "consomem" parte do feromônio, diminuindo a probabilidade de que outras formigas sigam o mesmo caminho. Isso favorece a exploração, equilibrando a tendência à exploração das outras modificações.

  

Além dessas modificações, o ACS geralmente utiliza uma estratégia elitista, onde apenas a melhor formiga (a melhor da iteração ou a melhor global) deposita feromônio após cada iteração. A quantidade de feromônio depositada é proporcional à qualidade da solução encontrada.

  

A regra de atualização global do feromônio no ACS é a seguinte:

<span style="font-size: 150%;">
$$ \tau_{ij} = (1 - \rho) * \tau_{ij} + \rho/f(s_{gb}) $$
</span>

  

Onde:

  

*   $\tau_{ij}$ é a quantidade de feromônio na aresta $(i, j)$.

*   $\rho$ é a taxa de evaporação do feromônio.

*   $f(s_{gb})$ é o custo da melhor solução global encontrada até o momento.

  

O ACS também costuma ser combinado com algoritmos de busca local para otimizar as soluções encontradas pelas formigas. Essa combinação de construção probabilística de soluções com otimização local tem se mostrado eficaz em muitas aplicações.

  

### O MAX-MIN Ant System (MMAS)

  

O MAX-MIN Ant System (MMAS) é uma variante do algoritmo Ant System (AS) que introduz algumas modificações importantes para melhorar o desempenho e evitar a estagnação da busca.

  

**Principais Características:**

  

1.  **Exploração e Intensificação:** O MMAS equilibra a exploração de novas soluções com a intensificação da busca em torno das melhores soluções encontradas. Isso é feito através de:

    *   **Limites de Feromônio:** O MMAS impõe limites inferior e superior para os valores de feromônio em cada aresta. O limite superior evita a convergência prematura para soluções subótimas, enquanto o limite inferior garante um nível mínimo de exploração.

    *   **Inicialização e Reinicialização do Feromônio:** As trilhas de feromônio são inicializadas com o limite superior, promovendo a exploração no início. A reinicialização ocasional das trilhas ajuda a evitar a estagnação e a explorar novas regiões do espaço de busca.

2.  **Atualização do Feromônio Elitista:** Apenas a melhor formiga (a melhor da iteração ou a melhor global) é permitida a depositar feromônio após cada iteração. Isso intensifica a busca em torno das soluções mais promissoras.

3.  **Atualização do Feromônio:** A atualização do feromônio no MMAS é semelhante ao AS, mas com a adição dos limites de feromônio. A equação de atualização é:
<span style="font-size: 150%;">
$$τ_ij = (1 - ρ) * τ_ij + Δτ_ij^best$$

</span>

Onde:

  

*   $\tau_{ij}$ é a quantidade de feromônio na aresta $(i, j)$.

*   $\rho$ é a taxa de evaporação do feromônio.

*   $\Delta\tau_{ij}^{best}$ é a quantidade de feromônio depositada pela melhor formiga.

  

**Benefícios:**

  

*   **Melhora do Desempenho:** O MMAS geralmente supera o AS em termos de qualidade da solução e velocidade de convergência.

*   **Prevenção da Estagnação:** Os mecanismos de limites de feromônio e reinicialização ajudam a evitar a estagnação da busca em ótimos locais.

*   **Flexibilidade:** O MMAS pode ser adaptado para diferentes problemas de otimização combinatória, ajustando os parâmetros e a forma como a informação heurística é utilizada.

  

O MMAS tem sido aplicado com sucesso em várias áreas, incluindo problemas de roteamento de veículos, sequenciamento e problemas de atribuição. Ele é uma ferramenta poderosa para encontrar soluções de alta qualidade para problemas complexos de otimização.

  

## Implementação

  

[Ant Colony Optimization](/Heuristicas%20Classicas/Ant_Colony_Optimization.py)

  

## BanchMark

**Obs: Notação Americana**

| Cidade | Instâncias | Custo Ótimo | Tempo Convergência | Custo Encontrado |

|---|---|---|---|---|

| Argentina | 9152 cidades | 837479 | | |

| Burma |  33708 cidades | 959304 | | |

| China | 71009 cidades | 4566563 | | |

| Djibouti | 38 cidades | 6656 | 3.54 segundos | 7148.31 |

| Egypt | 7146 cidades | 172387 |

| Finland | 10639 cidades | 520527 | | |

| Greece | 9882 cidades | 300899 | | |

| Honduras | 14473 cidades | 177105 | | |

| Ireland |

| Japan |

| Kazakhstan |

| Luxenburgo| 980 cidades | 11340 | 2298.47 segundos | 12083.53 |

| Morocco |

| Nicaragua |

| Oman |

| Panama |

| Qatar | 194 cidades |  9352 | 91.29 segundos | 9480.83 |

| Rwanda | 1621 cidades | 26051 | 7110.96 segundos | 27456.62 |

| Sweden | 24978 cidades | 855597 |

| Tanzania | 6117 cidades | 394718 |

| Uruguay | 734 cidades | 79114 | 1278.15 segundos | 85550.71 |

| Vietnam | 22775 cidades | 569288

| Western Sahara | 29 cidades | 27603 | 3.72 segundos | 25706.57 |

| Yemen | 7663 cidades | 238314 |

| Zimbabwe | 929 cidades | 95345 | 2057.08 segundos |100790.92

  
  

## Referências

  

- Dorigo, Marco & Di Caro, Gianni. (1999). The Ant Colony Optimization Meta-Heuristic. New Ideas in Optimization. (https://www.researchgate.net/publication/2831286_The_Ant_Colony_Optimization_Meta-Heuristic)

  

- Dorigo, Marco & Stützle, Thomas. (2010). Ant Colony Optimization: Overview and Recent Advances. (https://www.researchgate.net/publication/225265937_Ant_Colony_Optimization_Overview_and_Recent_Advances)

  

- http://www.scholarpedia.org/article/Ant_colony_optimization

  

- M. Dorigo, L. M. Gambardella, M. Middendorf and T. Stutzle, "Guest editorial: special section on ant colony optimization," in IEEE Transactions on Evolutionary Computation, vol. 6, no. 4, pp. 317-319, Aug. 2002, doi: 10.1109/TEVC.2002.802446.(https://ieeexplore.ieee.org/document/1027743)

  

- Xu, Ben-Lian & Zhu, Jihong & Chen, Qinlan. (2010). Ant Colony Optimization. 10.5772/9389. (https://www.researchgate.net/publication/221907664_Ant_Colony_Optimization)

  

- M. Dorigo, M. Birattari and T. Stutzle, "Ant colony optimization," in IEEE Computational Intelligence Magazine, vol. 1, no. 4, pp. 28-39, Nov. 2006, doi: 10.1109/MCI.2006.329691. (https://ieeexplore.ieee.org/document/4129846)

  

- (https://www.sciencedirect.com/science/article/pii/S095219761200067X?via%3Dihub)