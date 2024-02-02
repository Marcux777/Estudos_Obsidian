Cunha de Eratóstenes é um algoritmo para encontrar todos os números primos em um segmento $[1;n]$ usando $O(n \log \log n)$ operações.

O algoritmo é muito simples: no início, escrevemos todos os números entre 2 e $n$. Marcamos todos os múltiplos próprios de 2 (já que 2 é o menor número primo) como compostos. Um múltiplo próprio de um número $x$, é um número maior que $x$ e divisível por $x$. Então encontramos o próximo número que não foi marcado como composto, neste caso é 3. Isso significa que 3 é primo, e marcamos todos os múltiplos próprios de 3 como compostos. O próximo número não marcado é 5, que é o próximo número primo, e marcamos todos os múltiplos próprios dele. E continuamos este procedimento até termos processado todos os números na linha.

Na imagem a seguir, você pode ver uma visualização do algoritmo para calcular todos os números primos no intervalo $[1; 16]$. Pode-se ver que, com bastante frequência, marcamos números como compostos várias vezes.

![[Pasted image 20240118170010.png]]

A ideia por trás é esta: um número é primo, se nenhum dos números primos menores o divide. Como iteramos sobre os números primos em ordem, já marcamos todos os números, que são divisíveis por pelo menos um dos números primos, como divisíveis. Portanto, se chegarmos a uma célula e ela não estiver marcada, então ela não é divisível por nenhum número primo menor e, portanto, deve ser primo.

## Implementação

```cpp
int n;
vector<bool> is_prime(n+1, true);
is_prime[0] = is_prime[1] = false;
for (int i = 2; i <= n; i++) {
    if (is_prime[i] && (long long)i * i <= n) {
        for (int j = i * i; j <= n; j += i)
            is_prime[j] = false;
    }
}
```
Este código primeiro marca todos os números exceto zero e um como potenciais números primos, então começa o processo de peneirar números compostos. Para isso, itera sobre todos os números de $2$ a $n$. Se o número atual $i$ é um número primo, marca todos os números que são múltiplos de $i$ como números compostos, começando de $i^2$. Isso já é uma otimização sobre a maneira ingênua de implementá-lo, e é permitido já que todos os números menores que são múltiplos de $i$ necessariamente também têm um fator primo que é menor que $i$, então todos eles já foram peneirados anteriormente. Como $i^2$ pode facilmente estourar o tipo int, a verificação adicional é feita usando o tipo long long antes do segundo loop aninhado.

Usando essa implementação, o algoritmo consome $O(n)$ de memória (obviamente) e executa $O(n \log \log n)$ (veja a próxima seção).

[[Análise Assintótica - Crivo de Eratóstenes]]

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

[[Diferentes otimizações do Crivo de Eratóstenes]]
[[Encontrar primos no intervalo - Crivo de Eratóstenes]]
[[Modificação em Tempo Linear - Crivo de Eratóstenes]]
