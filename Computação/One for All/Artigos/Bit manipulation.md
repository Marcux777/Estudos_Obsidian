## Número Binário

Um número binário é um número expresso no sistema numeral binário ou sistema numeral binário, é um método de expressão matemática que usa apenas dois símbolos: geralmente "0" (zero) e "1" (um).

Dizemos que um determinado bit está definido se for um e desativado se for zero.

O número binário  $(a_k a_{k-1} \dots a_1 a_0)_2$  representa o número:

 
$$(a_k a_{k-1} \dots a_1 a_0)_2 = a_k \cdot 2^k + a_{k-1} \cdot 2^{k-1} + \dots + a_1 \cdot 2^1 + a_0 \cdot 2^0.$$ 

Por exemplo, o número binário  $1101_2$  representa o número  $13$ :

 
$$\begin{align} 1101_2 &= 1 \cdot 2^3 + 1 \cdot 2^2 + 0 \cdot 2^1 + 1 \cdot 2^0 \\ &= 1\cdot 8 + 1 \cdot 4 + 0 \cdot 2 + 1 \cdot 1 = 13 \end{align}$$ 

Os computadores representam inteiros como números binários. Inteiros positivos (tanto assinados quanto não assinados) são representados apenas com seus dígitos binários, e números assinados negativos (que podem ser positivos e negativos) geralmente são representados com o [complemento de dois.]

```cpp
unsigned int unsigned_number = 13;
assert(unsigned_number == 0b1101);

int positive_signed_number = 13;
assert(positive_signed_number == 0b1101);

int negative_signed_number = -13;
assert(negative_signed_number == 0b1111'1111'1111'1111'1111'1111'1111'0011);
```

As CPUs são muito rápidas ao manipular esses bits com operações específicas. Para alguns problemas, podemos aproveitar essas representações de números binários para acelerar o tempo de execução. E para alguns problemas (tipicamente em combinatorial ou programação dinâmica) onde queremos rastrear quais objetos já escolhemos de um conjunto dado de objetos, podemos simplesmente usar um número inteiro grande o suficiente onde cada dígito representa um objeto e, dependendo se escolhemos ou descartamos o objeto, definimos ou desativamos o dígito.

## Operadores de Bits

Todos esses operadores introduzidos são instantâneos (mesma velocidade que uma adição) em uma CPU para inteiros de comprimento fixo.

### Operadores Bit a Bit: 

- $\&$ : O operador AND bit a bit compara cada bit do primeiro operando com o bit correspondente do segundo operando. Se ambos os bits forem 1, o bit de resultado correspondente é definido como 1. Caso contrário, o bit de resultado correspondente é definido como 0.

 
- $|$ : O operador OR inclusivo bit a bit compara cada bit do primeiro operando com o bit correspondente do segundo operando. Se um dos dois bits for 1, o bit de resultado correspondente é definido como 1. Caso contrário, o bit de resultado correspondente é definido como 0.

 
- $\wedge$ : O operador XOR (OU exclusivo) bit a bit compara cada bit do primeiro operando com o bit correspondente do segundo operando. Se um bit for 0 e o outro bit for 1, o bit de resultado correspondente é definido como 1. Caso contrário, o bit de resultado correspondente é definido como 0.

 
- $\sim$ : O operador de complemento bit a bit (NÃO) inverte cada bit de um número; se um bit estiver definido, o operador o limpará, se estiver limpo, o operador o definirá.

Exemplos:

```cpp
n         = 01011000
n-1       = 01010111
--------------------
n & (n-1) = 01010000

n         = 01011000
n-1       = 01010111
--------------------
n | (n-1) = 01011111

n         = 01011000
n-1       = 01010111
--------------------
n ^ (n-1) = 00001111

n         = 01011000
--------------------
~n        = 10100111
```

### Operadores de Deslocamento:

 
- $\gg$ : Desloca um número para a direita removendo os últimos dígitos binários do número. Cada deslocamento por um representa uma divisão inteira por 2; portanto, um deslocamento para a direita por  $k$  representa uma divisão inteira por  $2^k$ .

	Por exemplo,  $5 \gg 2 = 101_2 \gg 2 = 1_2 = 1$ , o que é o mesmo que  $\frac{5}{2^2} = \frac{5}{4} = 1$ . No entanto, para um computador, deslocar alguns bits é muito mais rápido do que fazer divisões.

 
- $\ll$ : Desloca um número para a esquerda acrescentando dígitos zero. De maneira semelhante a um deslocamento para a direita por  $k$ , um deslocamento para a esquerda por  $k$  representa uma multiplicação por  $2^k$ .
	Por exemplo,  $5 \ll 3 = 101_2 \ll 3 = 101000_2 = 40$ , o que é o mesmo que  $5 \cdot 2^3 = 5 \cdot 8 = 40$ .

Observe, no entanto, que para um inteiro de comprimento fixo, isso significa descartar os dígitos mais à esquerda, e se você deslocar demais, acabará com o número  
$0$ .

## Truques Úteis

### Definir/Inverter/Limpar um Bit

Usando deslocamentos de bits e algumas operações básicas de bits, podemos facilmente definir, inverter ou limpar um bit.  
$1 \ll x$  é um número com apenas o  $x$ -ésimo bit definido, enquanto  $\sim(1 \ll x)$  é um número com todos os bits definidos, exceto o  $x$ -ésimo bit.

 
- $n ~|~ (1 \ll x)$  define o  $x$ -ésimo bit no número  $n$ 
 
- $n ~\wedge~ (1 \ll x)$  inverte o  $x$ -ésimo bit no número  $n$ 
 
- $n ~\&~ \sim(1 \ll x)$  limpa o  $x$ -ésimo bit no número  $n$ 
### Verificar se um bit está definido

O valor do  $x$ -ésimo bit pode ser verificado deslocando o número  $x$  posições para a direita, de modo que o  $x$ -ésimo bit esteja na posição das unidades, após o qual podemos extraí-lo realizando um E bit a bit com 1.

```cpp
bool is_set(unsigned int number, int x) {
    return (number >> x) & 1;
}
```

### Verificar se o número é divisível por uma potência de 2

Usando a operação "and", podemos verificar se um número  $n$  é par, porque  $n ~\&~ 1 = 0$  se  $n$  é par, e $n ~\&~ 1 = 1$  se  $n$  é ímpar. Mais geralmente,  $n$  é divisível por $2^{k}$  exatamente quando  $n ~\&~ (2^{k} − 1) = 0$ .

```cpp
bool isDivisibleByPowerOf2(int n, int k) {
    int powerOf2 = 1 << k;
    return (n & (powerOf2 - 1)) == 0;
}
```

Podemos calcular  $2^{k}$  deslocando 1 para a esquerda por  $k$  posições. O truque funciona porque  $2^k - 1$  é um número que consiste exatamente em  $k$  uns. E um número que é divisível por  $2^k$  deve ter zeros exatamente nesses lugares.

### Verificar se um inteiro é uma potência de 2

Uma potência de dois é um número que tem apenas um único bit definido (por exemplo,  $32 = 0010~0000_2$ ), enquanto o predecessor desse número tem esse dígito não definido e todos os dígitos após ele definidos ( $31 = 0001~1111_2$ ). Portanto, a operação bit a bit AND de um número com seu predecessor sempre será 0, já que eles não têm nenhum dígito em comum definido. Você pode facilmente verificar que isso só acontece para as potências de dois e para o número  
$0$ , que já não tem nenhum dígito definido.

```cpp
bool isPowerOfTwo(unsigned int n) {
    return n && !(n & (n - 1));
}
```

### Limpar o bit mais à direita definido

A expressão  $n ~\&~ (n-1)$  pode ser usada para desativar o bit mais à direita definido de um número  $n$ . Isso funciona porque a expressão  $n-1$  inverte todos os bits após o bit mais à direita definido de  $n$ , incluindo o bit mais à direita definido. Assim, todos esses dígitos são diferentes do número original, e, fazendo um AND bit a bit, todos são definidos como 0, dando-lhe o número original  $n$  com o bit mais à direita definido invertido.

Por exemplo, considere o número  $52 = 0011~0100_2$ :

```cpp
n         = 00110100
n-1       = 00110011
--------------------
n & (n-1) = 00110000
```

### Algoritmo de Brian Kernighan

Podemos contar o número de bits definidos com a expressão acima.

A ideia é considerar apenas os bits definidos de um número desativando seu bit mais à direita (depois de contá-lo), para que a próxima iteração do loop considere o próximo bit mais à direita.

```cpp
int countSetBits(int n)
{
    int count = 0;
    while (n)
    {
        n = n & (n - 1);
        count++;
    }
    return count;
}
```

### Truques adicionais

 
- $n ~\&~ (n + 1)$  limpa todos os uns finais:  $0011~0111_2 \rightarrow 0011~0000_2$ .
 
- $n ~|~ (n + 1)$  define o último bit limpo:  $0011~0101_2 \rightarrow 0011~0111_2$ .
 
- $n ~\&~ -n$  extrai o último bit definido:  $0011~0100_2 \rightarrow 0000~0100_2$ .

Muitos outros podem ser encontrados no livro "Hacker's Delight".

### Suporte da Linguagem e do Compilador
O C++ oferece suporte a algumas dessas operações desde o C++20 por meio da biblioteca padrão bit:

- `has_single_bit`: verifica se o número é uma potência de dois
- `bit_ceil` / `bit_floor`: arredonda para cima/para baixo para a próxima potência de dois
- `rotl` / `rotr`: rotaciona os bits no número
- `countl_zero` / `countr_zero` / `countl_one` / `countr_one`: conta os zeros/uns principais/finais
- `popcount`: conta o número de bits definidos
Além disso, existem também funções predefinidas em alguns compiladores que ajudam a trabalhar com bits. Por exemplo, o GCC define uma lista em Funções Internas Fornecidas pelo GCC que também funcionam em versões mais antigas do C++:

- `__builtin_popcount(unsigned int)`: retorna o número de bits definidos (`__builtin_popcount(0b0001'0010'1100) == 4`)
- `__builtin_ffs(int)`: encontra o índice do primeiro bit definido (mais à direita) (`__builtin_ffs(0b0001'0010'1100) == 3`)
- `__builtin_clz(unsigned int)`: a contagem de zeros à esquerda (`__builtin_clz(0b0001'0010'1100) == 23`)
- `__builtin_ctz(unsigned int)`: a contagem de zeros à direita (`__builtin_ctz(0b0001'0010'1100) == 2`)
- `__builtin_parity(x)`: a paridade (par ou ímpar) do número de uns na representação binária
Observe que algumas das operações (tanto as funções do C++20 quanto as incorporadas do compilador) podem ser bastante lentas no GCC se você não ativar um alvo específico do compilador com `#pragma GCC target("popcnt")`.