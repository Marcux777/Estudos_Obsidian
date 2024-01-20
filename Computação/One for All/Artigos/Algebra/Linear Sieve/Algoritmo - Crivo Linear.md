Nosso objetivo é calcular o menor fator primo  $lp [i]$  para cada número  $i$  no segmento  $[2; n]$ .

Além disso, precisamos armazenar a lista de todos os números primos encontrados - vamos chamá-la de  $pr []$ .

Inicializaremos os valores  $lp [i]$  com zeros, o que significa que assumimos que todos os números são primos. Durante a execução do algoritmo, essa matriz será preenchida gradualmente.

Agora vamos passar pelos números de 2 a  $n$ . Temos dois casos para o número atual  $i$ :

- $lp[i] = 0$  - isso significa que  $i$  é primo, ou seja, não encontramos fatores menores para ele. Portanto, atribuímos  $lp [i] = i$  e adicionamos $i$  ao final da lista  $pr[]$ .

- $lp[i] \neq 0$  - isso significa que  $i$  é composto, e seu menor fator primo é  $lp [i]$ .

Em ambos os casos, atualizamos os valores de  $lp []$  para os números que são divisíveis por  $i$ . No entanto, nosso objetivo é aprender a fazer isso de forma a definir um valor  $lp []$  no máximo uma vez para cada número. Podemos fazer isso da seguinte maneira:

Vamos considerar os números  $x_j = i \cdot p_j$ , onde  $p_j$  são todos os números primos menores ou iguais a  $lp [i]$  (é por isso que precisamos armazenar a lista de todos os números primos).

Definiremos um novo valor  $lp [x_j] = p_j$  para todos os números desta forma.

A prova de correção deste algoritmo e seu tempo de execução podem ser encontrados após a implementação.