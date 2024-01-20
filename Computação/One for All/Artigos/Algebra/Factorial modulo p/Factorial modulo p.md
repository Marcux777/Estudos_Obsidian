Em alguns casos, é necessário considerar fórmulas complexas módulo algum primo $p$, contendo fatoriais tanto no numerador quanto no denominador, como as que você encontra na fórmula para coeficientes binomiais. Consideramos o caso em que $p$ é relativamente pequeno. Este problema só faz sentido quando os fatoriais aparecem tanto no numerador quanto no denominador de frações. Caso contrário, $p!$ e os termos subsequentes serão reduzidos a zero. Mas nas frações, os fatores de $p$ podem ser cancelados, e a expressão resultante será diferente de zero módulo $p$.

Assim, formalmente a tarefa é: Você quer calcular $n! \bmod p$, sem levar em conta todos os múltiplos fatores de $p$ que aparecem no fatorial. Imagine que você escreva a fatoração prima de $n!$, remova todos os fatores $p$, e compute o produto módulo $p$. Denotaremos este fatorial modificado com $n!_{\%p}$. Por exemplo,

$7!_{\%p} \equiv 1 \cdot 2 \cdot \underbrace{1}_{3} \cdot 4 \cdot 5 \underbrace{2}_{6} \cdot 7 \equiv 2 \bmod 3$.

Aprender a calcular efetivamente este fatorial modificado nos permite calcular rapidamente o valor das várias fórmulas combinatórias (por exemplo, coeficientes binomiais).

[[Algoritmo]]
[[Implementação]]
[[Multiplicity of  p]]

