
Dado dois números inteiros não negativos $a$ e $b$, temos que encontrar o MDC (máximo divisor comum) deles, ou seja, o maior número que é divisor de ambos $a$ e $b$. Isso é comumente denotado por $\gcd(a, b)$. Matematicamente, é definido como:

$\gcd(a, b) = \max \{k > 0 : (k \mid a) \text{ e } (k \mid b) \}$

(aqui o símbolo $\mid$ denota divisibilidade, ou seja, “$k \mid a$” significa “$k$ divide $a$”)

Quando um dos números é zero e o outro não é, o máximo divisor comum deles, por definição, é o segundo número. Quando ambos os números são zero, o máximo divisor comum é indefinido (pode ser qualquer número arbitrariamente grande), mas é conveniente defini-lo como zero também para preservar a associatividade do $\gcd$. Isso nos dá uma regra simples: se um dos números é zero, o máximo divisor comum é o outro número.

O algoritmo de Euclides, discutido abaixo, permite encontrar o máximo divisor comum de dois números $a$ e $b$ em $O(\log \min(a, b))$.

O algoritmo foi descrito pela primeira vez nos “Elementos” de Euclides (por volta de 300 a.C.), mas é possível que o algoritmo tenha origens ainda mais antigas.

[[Algoritmo - Algoritmo de Euclides para calcular o maior divisor comum]]
[[Implementação - Algoritmo de Euclides para calcular o maior divisor comum]]
