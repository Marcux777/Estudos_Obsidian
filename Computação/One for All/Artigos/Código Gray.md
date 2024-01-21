

O código Gray é um sistema numérico binário no qual dois valores sucessivos diferem apenas em um bit.

Por exemplo, a sequência de códigos Gray para números de 3 bits é: 000, 001, 011, 010, 110, 111, 101, 100, então  $G(4) = 6$ .

Esse código foi inventado por Frank Gray em 1953.

## Encontrando o Código Gray¶

Vamos observar os bits do número  $n$  e os bits do número  $G(n)$ . Observe que o  $i$ -ésimo bit de  
$G(n)$  é igual a 1 apenas quando o  $i$ -ésimo bit de  $n$  é igual a 1 e o  $i + 1$ -ésimo bit é igual a 0, ou vice-versa ( $i$ -ésimo bit igual a 0 e  $i + 1$ -ésimo bit igual a 1). Assim,  $G(n) = n \oplus (n >> 1)$ :

```cpp
int g(int n) {
    return n ^ (n >> 1);
}
```

## Encontrando o Inverso do Código Gray

Dado o código Gray  $g$ , restaure o número original  $n$ .

Vamos percorrer os bits mais significativos até os menos significativos (o bit menos significativo tem índice 1 e o bit mais significativo tem índice  $k$ ). A relação entre os bits  $n_i$  do número  $n$  e os bits  $g_i$  do número  $g$ :

$$\begin{align} n_k &= g_k, \\ n_{k-1} &= g_{k-1} \oplus n_k = g_k \oplus g_{k-1}, \\ n_{k-2} &= g_{k-2} \oplus n_{k-1} = g_k \oplus g_{k-1} \oplus g_{k-2}, \\ n_{k-3} &= g_{k-3} \oplus n_{k-2} = g_k \oplus g_{k-1} \oplus g_{k-2} \oplus g_{k-3}, \vdots \end{align}$$

A maneira mais fácil de expressar isso em código é:

```cpp
int rev_g(int g) {
  int n = 0;
  for (; g; g >>= 1)
    n ^= g;
  return n;
}
```

## Aplicações Práticas

Os códigos Gray têm algumas aplicações úteis, às vezes bastante inesperadas:

-  O código Gray de  $n$  bits forma um ciclo hamiltoniano em um hipercubo, onde cada bit corresponde a uma dimensão.

- Os códigos Gray são usados para minimizar os erros na conversão de sinais digitais para analógicos (por exemplo, em sensores).

- O código Gray pode ser usado para resolver o problema das Torres de Hanói. Deixe  $n$  denotar o número de discos. Comece com o código Gray de comprimento  $n$  que consiste em todos os zeros ( $G(0)$ ) e mova-se entre códigos Gray consecutivos (de  $G(i)$  para  $G(i+1)$ ). Deixe o  $i$ -ésimo bit do código Gray atual representar o  $n$ -ésimo disco (o bit menos significativo corresponde ao menor disco e o bit mais significativo ao maior disco). Como exatamente um bit muda em cada etapa, podemos tratar a mudança do  $i$ -ésimo bit como o movimento do  $i$ -ésimo disco. Observe que há exatamente uma opção de movimento para cada disco (exceto o menor) em cada etapa (exceto nas posições inicial e final). Sempre há duas opções de movimento para o menor disco, mas existe uma estratégia que sempre levará à resposta: se  $n$  é ímpar, então a sequência de movimentos do menor disco parece  $f \to t \to r \to f \to t \to r \to ...$ , onde  $f$  é a haste inicial,  $t$  é a haste terminal e  $r$  é a haste restante; e se  $n$  é par:  $f \to r \to t \to f \to r \to t \to ...$ .

- Os códigos Gray também são usados na teoria de algoritmos genéticos.