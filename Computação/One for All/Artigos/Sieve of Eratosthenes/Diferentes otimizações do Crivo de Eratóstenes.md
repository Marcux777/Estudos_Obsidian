
A maior fraqueza do algoritmo é que ele “caminha” pela memória várias vezes, manipulando apenas elementos individuais. Isso não é muito amigável para o cache. E por causa disso, a constante que está oculta em $O(nloglogn)$ é comparativamente grande.
Além disso, a memória consumida é um gargalo para grandes n.
Os métodos apresentados abaixo nos permitem reduzir a quantidade de operações realizadas, bem como reduzir notavelmente a memória consumida.

[[Peneirando até a raiz]]
[[Peneirando apenas pelos números ímpares]]
[[Consumo de Memória e Velocidade das Operações]]
[[Segmented Sieve]]
