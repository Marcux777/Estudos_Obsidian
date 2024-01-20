
Brent usa um algoritmo semelhante ao de Floyd. Ele também usa dois ponteiros. Mas, em vez de avançar os ponteiros por um e dois respectivamente, avançamos eles em potências de dois. Assim que  $2^i$  for maior que  $\lambda$  e  $\mu$ , encontraremos o ciclo.

```python
function floyd(f, x0):
    tortoise = x0
    hare = f(x0)
    l = 1
    while tortoise != hare:
        tortoise = hare
        repeat l times:
            hare = f(hare)
            if tortoise == hare:
                return true
        l *= 2
    return true
```
O algoritmo de Brent também é executado em tempo linear, mas geralmente é mais rápido que o algoritmo de Floyd, pois usa menos avaliações da função  $f$ .

[[Implementação - Algoritmo de Brent]]
