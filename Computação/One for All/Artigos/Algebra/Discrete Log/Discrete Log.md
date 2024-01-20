
O logaritmo discreto é um número inteiro  $x$  que satisfaz a equação
$$a^x \equiv b \pmod m$$ 
para inteiros dados  $a$ ,  $b$  e  $m$ .

O logaritmo discreto nem sempre existe, por exemplo, não há solução para  $2^x \equiv 3 \pmod 7$ . Não há uma condição simples para determinar se o logaritmo discreto existe.

Neste artigo, descrevemos o algoritmo Baby-step giant-step, um algoritmo para calcular o logaritmo discreto proposto por Shanks em 1971, que possui complexidade de tempo  
$O(\sqrt{m})$ . Este é um algoritmo meet-in-the-middle porque usa a técnica de dividir as tarefas ao meio.

[[Algoritmo - Discrete Log]]
[[Complexidade - Discrete Log]]
[[Implementação - Discrete Log]]
[[Quando a e  m não são coprimos]]
