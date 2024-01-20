Embora o tempo de execução de  $O(n)$  seja melhor do que  $O(n \log \log n)$  do crivo clássico de Eratóstenes, a diferença entre eles não é tão grande. Na prática, o crivo linear funciona quase tão rápido quanto uma implementação típica do crivo de Eratóstenes.

Em comparação com as versões otimizadas do crivo de Eratóstenes, por exemplo, o crivo segmentado, é muito mais lento.

Considerando os requisitos de memória deste algoritmo - um array  $lp []$  de comprimento $n$ , e um array de  $pr []$  de comprimento  $\frac n {\ln n}$ , este algoritmo parece ser pior do que o crivo clássico em todos os aspectos.

No entanto, sua qualidade redentora é que este algoritmo calcula um array  
$lp []$ , que nos permite encontrar a fatoração de qualquer número no segmento  
$[2; n]$  no tempo da ordem de tamanho dessa fatoração. Além disso, usando apenas um array extra, poderemos evitar divisões ao procurar a fatoração.

Conhecer as fatorações de todos os números é muito útil para algumas tarefas, e este algoritmo é um dos poucos que permitem encontrá-las em tempo linear.