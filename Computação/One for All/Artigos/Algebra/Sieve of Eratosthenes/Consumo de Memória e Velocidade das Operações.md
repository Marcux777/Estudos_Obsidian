
Devemos notar que essas duas implementações da Crivo de Eratóstenes usam$n$  bits de memória usando a estrutura de dados vector. vector não é um contêiner regular que armazena uma série de bool (como na maioria das arquiteturas de computador, um bool ocupa um byte de memória). É uma especialização de otimização de memória de vector, que consome apenas
$\frac{N}{8}$  bytes de memória.

As arquiteturas de processadores modernos trabalham muito mais eficientemente com bytes do que com bits, pois geralmente não podem acessar bits diretamente. Portanto, por baixo, o vector armazena os bits em uma grande memória contínua, acessa a memória em blocos de alguns bytes e extrai/define os bits com operações de bits como mascaramento de bits e deslocamento de bits.

Por causa disso, há um certo overhead quando você lê ou escreve bits com um vector, e muitas vezes usar um vector (que usa 1 byte para cada entrada, então 8x a quantidade de memória) é mais rápido.

No entanto, para as implementações simples da Crivo de Eratóstenes, usar um vector é mais rápido. Você é limitado pela rapidez com que pode carregar os dados no cache e, portanto, usar menos memória dá uma grande vantagem. Um benchmark (link) mostra que usar um vector é entre 1,4x e 1,7x mais rápido do que usar um vector.

As mesmas considerações também se aplicam a bitset. É também uma maneira eficiente de armazenar bits, semelhante ao vector, portanto, ocupa apenas$\frac{N}{8}$  bytes de memória, mas é um pouco mais lento no acesso aos elementos. No benchmark acima, o bitset tem um desempenho um pouco pior do que o vector. Outra desvantagem do bitset é que você precisa saber o tamanho no momento da compilação.