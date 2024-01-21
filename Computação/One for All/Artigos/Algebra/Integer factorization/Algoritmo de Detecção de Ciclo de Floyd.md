
Este algoritmo encontra um ciclo usando dois ponteiros. Esses ponteiros se movem pela sequência em velocidades diferentes. Em cada iteração, o primeiro ponteiro avança para o próximo elemento, mas o segundo ponteiro avança dois elementos. Não é difícil ver que, se existir um ciclo, o segundo ponteiro fará pelo menos um ciclo completo e então encontrará o primeiro ponteiro durante os próximos loops de ciclo. Se o comprimento do ciclo for  $\lambda$  e o  $\mu$  for o primeiro índice em que o ciclo começa, então o algoritmo será executado em $O(\lambda + \mu)$  tempo.

Este algoritmo também é conhecido como o [[algoritmo da Tartaruga e da Lebre]], baseado no conto em que uma tartaruga (aqui um ponteiro lento) e uma lebre (aqui um ponteiro mais rápido) fazem uma corrida.

Na verdade, é possível determinar o parâmetro  $\lambda$  e  $\mu$  usando este algoritmo (também em  $O(\lambda + \mu)$  tempo e  $O(1)$  espaço), mas aqui está apenas a versão simplificada para encontrar o ciclo em geral. O algoritmo retorna verdadeiro assim que detecta um ciclo. Se a sequência não tiver um ciclo, então a função nunca vai parar. No entanto, isso não pode acontecer durante o algoritmo rho de Pollard.

```python
function floyd(f, x0):
    tortoise = x0
    hare = f(x0)
    while tortoise != hare:
        tortoise = f(tortoise)
        hare = f(f(hare))
    return true
```

[[Implementação - Algoritmo de Detecção de Ciclo de Floyd]]


