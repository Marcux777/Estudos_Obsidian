### Definição

Em aritmética modular, um número  $g$  é chamado de raiz primitiva módulo  $n$  se todo número primo com  $n$  for congruente a uma potência de  $g$  módulo  $n$ . Matematicamente,  $g$  é uma raiz primitiva módulo  $n$  se e somente se, para qualquer número inteiro  $a$  tal que  $\gcd(a, n) = 1$ , existe um inteiro  $k$  tal que: 
$g^k \equiv a \pmod n$ 

$k$  é então chamado de índice ou logaritmo discreto de  $a$  na base  $g$  módulo  $n$ .  
$g$  também é chamado de gerador do grupo multiplicativo dos inteiros módulo  
$n$ .

Em particular, no caso em que  $n$  é um número primo, as potências da raiz primitiva percorrem todos os números de  $1$  a  $n-1$ .

### Existência

Uma raiz primitiva módulo  $n$  existe se e somente se:
- $n$  é 1, 2, 4, ou
 
- $n$  é uma potência de um número primo ímpar  $(n = p^k)$ , ou
 
- $n$  é o dobro de uma potência de um número primo ímpar  $(n = 2 \cdot p^k)$ .

Este teorema foi provado por Gauss em 1801.

### Relação com a Função de Euler

Seja  $g$  uma raiz primitiva módulo  $n$ . Podemos mostrar que o menor número  $k$  para o qual  
$g^k \equiv 1 \pmod n$  é igual a  $\phi (n)$ . Além disso, o inverso também é verdadeiro, e esse fato será usado neste artigo para encontrar uma raiz primitiva.

Além disso, o número de raízes primitivas módulo  $n$ , se existirem, é igual a  $\phi (\phi (n) )$ .

[[Algoritmo para encontrar uma raiz primitiva - Primitive Root]]
[[Implementação - Primitive Root]]
