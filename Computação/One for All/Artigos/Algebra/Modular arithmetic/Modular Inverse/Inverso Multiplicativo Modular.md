
Um inverso multiplicativo modular de um inteiro  $a$  é um inteiro  $x$  tal que  $a \cdot x$  é congruente a  $1$  modular algum módulo  $m$ . Para escrever de uma maneira formal: queremos encontrar um inteiro  
$x$  de modo que
$$a \cdot x \equiv 1 \mod m.$$ 
Também denotaremos  $x$  simplesmente com  $a^{-1}$ .

Devemos notar que o inverso modular nem sempre existe. Por exemplo, deixe  $m = 4$ ,  $a = 2$ . Ao verificar todos os possíveis valores modulo  $m$ , deve ficar claro que não podemos encontrar  $a^{-1}$  satisfazendo a equação acima. Pode ser provado que o inverso modular existe se e somente se  
$a$  e  $m$  são primos entre si (ou seja,  $\gcd(a, m) = 1$ ).
Neste artigo, apresentamos dois métodos para encontrar o inverso modular caso ele exista, e um método para encontrar o inverso modular para todos os números em tempo linear.

- [[Encontrando o Inverso Modular usando o Algoritmo Euclidiano Estendido]]
- [[Encontrando o Inverso Modular usando Exponenciação Binária]]
- [[Encontrando o inverso modular para módulos primos usando a Divisão Euclidiana]]
- [[Encontrando o inverso modular para um array de números módulo  m]]

