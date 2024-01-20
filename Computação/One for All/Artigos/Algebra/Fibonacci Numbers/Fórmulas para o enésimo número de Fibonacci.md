# Fórmulas para o $n^{\text{ésimo}}$ número de Fibonacci
## Expressão de forma fechada
Existe uma fórmula conhecida como "Fórmula de Binet", embora já fosse conhecida por Moivre:

$$F_n = \frac{\left(\frac{1 + \sqrt{5}}{2}\right)^n - \left(\frac{1 - \sqrt{5}}{2}\right)^n}{\sqrt{5}}$$
Esta fórmula é fácil de provar por indução, mas pode ser deduzida com a ajuda do conceito de funções geradoras ou resolvendo uma equação funcional.

Você pode notar imediatamente que o valor absoluto do segundo termo é sempre menor que $1$, e também diminui muito rapidamente (exponencialmente). Portanto, o valor do primeiro termo sozinho é "quase" $F_n$. Isso pode ser escrito estritamente como:

$$F_n = \left[\frac{\left(\frac{1 + \sqrt{5}}{2}\right)^n}{\sqrt{5}}\right]$$
onde os colchetes denotam arredondamento para o inteiro mais próximo.

Como essas duas fórmulas exigiriam uma precisão muito alta ao trabalhar com números fracionários, elas têm pouco uso em cálculos práticos.