Muitos algoritmos em teoria dos números, como teste de primalidade ou fatoração de inteiros, e em criptografia, como o RSA, exigem muitas operações módulo um número grande. Uma multiplicação como  $x y \bmod{n}$  é bastante lenta de ser calculada com os algoritmos típicos, pois requer uma divisão para saber quantas vezes  $n$  precisa ser subtraído do produto. E a divisão é uma operação realmente cara, especialmente com números grandes.

A multiplicação modular de Montgomery é um método que permite calcular essas multiplicações de maneira mais rápida. Em vez de dividir o produto e subtrair  $n$  várias vezes, ela adiciona múltiplos de  
$n$  para cancelar os bits mais baixos e depois simplesmente descarta esses bits mais baixos.

[[Representação de Montgomery]]
[[Redução de Montgomery]]
[[Fast inverse trick]]
[[Implementação - Montgomery Multiplication]]
[[Transformação Rápida]]
