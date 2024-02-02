## Enumeração de Todas as Submáscaras de uma Máscara Dada

Dada uma máscara de bits  $m$ , você deseja percorrer eficientemente todas as suas submáscaras, ou seja, máscaras  $s$  nas quais apenas os bits que foram incluídos na máscara  $m$  estão definidos.

Considere a implementação desse algoritmo, baseado em truques com operações de bits:

```cpp
int s = m;
while (s > 0) {
    // ... você pode usar s ...
    s = (s-1) & m;
}
```

ou, usando uma instrução 'for' mais compacta:

```cpp
for (int s=m; s; s=(s-1)&m) {
    // ... você pode usar s ...
}
```

Em ambas as variantes do código, a submáscara igual a zero não será processada. Podemos processá-la fora do loop ou usar um design menos elegante, por exemplo:

```cpp
for (int s=m; ; s=(s-1)&m) {
    // ... você pode usar s ...
    if (s == 0) break;
}
```

Vamos examinar por que o código acima visita todas as submáscaras de  $m$ , sem repetições e em ordem decrescente.

Suponha que temos uma máscara atual  $s$ , e queremos passar para a próxima máscara. Subtraindo um da máscara  $s$ , removeremos o bit definido mais à direita e todos os bits à direita se tornarão 1. Em seguida, removemos todos os bits "extras" que não estão incluídos na máscara  $m$  e, portanto, não podem fazer parte de uma submáscara. Fazemos essa remoção usando a operação bitwise (s-1) & m. Como resultado, "cortamos" a máscara  $s-1$  para determinar o valor mais alto que ela pode assumir, ou seja, a próxima submáscara após  $s$  em ordem decrescente.

Assim, esse algoritmo gera todas as submáscaras dessa máscara em ordem decrescente, realizando apenas duas operações por iteração.

Um caso especial é quando  $s = 0$ . Após a execução de  $s-1$ , obtemos uma máscara em que todos os bits estão definidos (representação de bit de -1), e após (s-1) & m, teremos que  $s$  será igual a  
$m$ . Portanto, com a máscara  $s = 0$ , tome cuidado — se o loop não terminar em zero, o algoritmo pode entrar em um loop infinito.

## Iterando por Todas as Máscaras com Suas Submáscaras. Complexidade  $O(3^n)$ 

Em muitos problemas, especialmente aqueles que usam programação dinâmica com bitmasks, você deseja iterar por todas as bitmasks e, para cada máscara, iterar por todas as suas submáscaras:

```cpp
for (int m=0; m<(1<<n); ++m)
    for (int s=m; s; s=(s-1)&m)
        // ... s e m ...
```

Vamos provar que o loop interno executará um total de  $O(3^n)$  iterações.

Primeira prova: Considere o  $i$ -ésimo bit. Existem exatamente três opções para ele:

1. não está incluído na máscara  $m$  (e, portanto, não está incluído na submáscara  $s$ ),
2. está incluído em  $m$ , mas não está incluído em  $s$ , ou
3. está incluído tanto em  $m$  quanto em  $s$ .
Como há um total de  $n$  bits, haverá  $3^n$  combinações diferentes.

Segunda prova: Observe que se a máscara  $m$  tem  $k$  bits ativados, então ela terá  $2^k$  submáscaras. Como temos um total de  $\binom{n}{k}$  máscaras com  $k$  bits ativados (veja coeficientes binomiais), então o número total de combinações para todas as máscaras será:

 
$$\sum_{k=0}^n \binom{n}{k} \cdot 2^k$$ 

Para calcular esse número, observe que a soma acima é igual à expansão de  $(1+2)^n$  usando o teorema binomial. Portanto, temos  $3^n$  combinações, como queríamos provar.