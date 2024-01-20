Os números de Fibonacci são definidos da seguinte forma:

$$F_0 = 0, F_1 = 1, F_n = F_{n-1} + F_{n-2}$$
Os primeiros elementos da sequência (OEIS A000045) são:

$$0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, ...$$
### Propriedades
Os números de Fibonacci possuem muitas propriedades interessantes. Aqui estão algumas delas:

- Identidade de Cassini:
$$F_{n-1} F_{n+1} - F_n^2 = (-1)^n$$
- A regra da "adição":
$$F_{n+k} = F_k F_{n+1} + F_{k-1} F_n$$
- Aplicando a identidade anterior ao caso $k = n$, obtemos:
$$F_{2n} = F_n (F_{n+1} + F_{n-1})$$
- A partir disso, podemos provar por indução que para qualquer número inteiro positivo $k$, $F_{nk}$ é múltiplo de $F_n$.

- O inverso também é verdadeiro: se $F_m$ é múltiplo de $F_n$, então $m$ é múltiplo de $n.$

- Identidade do MDC:

$$GCD(F_m, F_n) = F_{GCD(m, n)}$$
- Os números de Fibonacci são as piores entradas possíveis para o algoritmo euclidiano (veja o teorema de Lame no [algoritmo euclidiano](obsidian://open?vault=Algoritmos&file=algoritmos%2FOne%20for%20All%2FArtigos%2FAlgebra%2FAlgoritmo%20de%20Euclides%20para%20calcular%20o%20maior%20divisor%20comum%2FAlgoritmo%20de%20Euclides%20para%20calcular%20o%20maior%20divisor%20comum)).

[[Fibonacci Coding]]
[[Fórmulas para o enésimo número de Fibonacci]]
[[Fibonacci em tempo linear]]
[[Forma Matricial - Número de Fibonacci]]
[[Periodicidade módulo p - Número de Fibonacci]]