Dado um número  
$n$ , encontre todos os números primos em um segmento $[2;n]$ .

A maneira padrão de resolver uma tarefa é usar o [[Crivo de Eratóstenes]]. Este algoritmo é muito simples, mas tem tempo de execução $O(n \log \log n)$ .

Embora existam muitos algoritmos conhecidos com tempo de execução sublinear (ou seja, $o(n)$ ), o algoritmo descrito abaixo é interessante por sua simplicidade: não é mais complexo do que o crivo clássico de Eratóstenes.

Além disso, o algoritmo dado aqui calcula as fatorações de todos os números no segmento  $[2; n]$  como um efeito colateral, e isso pode ser útil em muitas aplicações práticas.

A fraqueza do algoritmo dado está em usar mais memória do que o crivo clássico de Eratóstenes: ele requer uma matriz de  $n$  números, enquanto para o crivo clássico de Eratóstenes é suficiente ter  $n$  bits de memória (que é 32 vezes menos).

Portanto, faz sentido usar o algoritmo descrito apenas para números da ordem de  
$10^7$  e não maiores.

[[Algoritmo - Crivo Linear]]
[[Implementação - Crivo Linear]]
[[Prova de Corretude - Crivo Linear]]
[[Tempo de Execução e Memória - Crivo Linear]]
