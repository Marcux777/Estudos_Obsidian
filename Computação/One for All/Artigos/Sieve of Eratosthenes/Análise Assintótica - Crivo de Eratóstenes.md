
É simples provar um tempo de execução de $O(n \log n)$ sem saber nada sobre a distribuição de primos - ignorando a verificação is_prime, o loop interno executa (no máximo) $n/i$ vezes para $i = 2, 3, 4, \dots$, levando o número total de operações no loop interno a ser uma soma harmônica como $n(1/2 + 1/3 + 1/4 + \cdots)$, que é limitada por $O(n \log n)$.

Vamos provar que o tempo de execução do algoritmo é $O(n \log \log n)$. O algoritmo executará $\frac{n}{p}$ operações para cada primo $p \le n$ no loop interno. Portanto, precisamos avaliar a próxima expressão:

$$\sum_{\substack{p \le n, \\\ p \text{ primo}}} \frac n p = n \cdot \sum_{\substack{p \le n, \\\ p \text{ primo}}} \frac 1 p.$$ 
Vamos relembrar dois fatos conhecidos.

O número de números primos menores ou iguais a $n$ é aproximadamente $\frac n {\ln n}$.
O $k$-ésimo número primo é aproximadamente igual a $k \ln k$ (isso segue imediatamente do fato anterior).
Assim, podemos escrever a soma da seguinte maneira:

$$\sum_{\substack{p \le n, \\\ p \text{ primo}}} \frac 1 p \approx \frac 1 2 + \sum_{k = 2}^{\frac n {\ln n}} \frac 1 {k \ln k}.$$ 
Aqui extraímos o primeiro número primo 2 da soma, porque $k = 1$ na aproximação $k \ln k$ é $0$ e causa uma divisão por zero.

Agora, vamos avaliar essa soma usando a integral de uma mesma função sobre $k$ de $2$ a $\frac n {\ln n}$ (podemos fazer tal aproximação porque, de fato, a soma está relacionada à integral como sua aproximação usando o método do retângulo):

$$\sum_{k = 2}^{\frac n {\ln n}} \frac 1 {k \ln k} \approx \int_2^{\frac n {\ln n}} \frac 1 {k \ln k} dk.$$ 
A antiderivada para o integrando é $\ln \ln k$. Usando uma substituição e removendo termos de ordem inferior, obteremos o resultado:

$$\int_2^{\frac n {\ln n}} \frac 1 {k \ln k} dk = \ln \ln \frac n {\ln n} - \ln \ln 2 = \ln(\ln n - \ln \ln n) - \ln \ln 2 \approx \ln \ln n.$$ 
Agora, retornando à soma original, obteremos sua avaliação aproximada:

$$\sum_{\substack{p \le n, \\\ p\ é\ primo}} \frac n p \approx n \ln \ln n + o(n).$$ 
Você pode encontrar uma prova mais rigorosa (que dá uma avaliação mais precisa que é precisa dentro de multiplicadores constantes) no livro de Hardy & Wright "An Introduction to the Theory of Numbers" (p. 349).