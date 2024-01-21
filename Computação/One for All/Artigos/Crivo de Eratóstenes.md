Cunha de Eratóstenes é um algoritmo para encontrar todos os números primos em um segmento $[1;n]$ usando $O(n \log \log n)$ operações.

O algoritmo é muito simples: no início, escrevemos todos os números entre 2 e $n$. Marcamos todos os múltiplos próprios de 2 (já que 2 é o menor número primo) como compostos. Um múltiplo próprio de um número $x$, é um número maior que $x$ e divisível por $x$. Então encontramos o próximo número que não foi marcado como composto, neste caso é 3. Isso significa que 3 é primo, e marcamos todos os múltiplos próprios de 3 como compostos. O próximo número não marcado é 5, que é o próximo número primo, e marcamos todos os múltiplos próprios dele. E continuamos este procedimento até termos processado todos os números na linha.

Na imagem a seguir, você pode ver uma visualização do algoritmo para calcular todos os números primos no intervalo $[1; 16]$. Pode-se ver que, com bastante frequência, marcamos números como compostos várias vezes.

![[Pasted image 20240118170010.png]]

A ideia por trás é esta: um número é primo, se nenhum dos números primos menores o divide. Como iteramos sobre os números primos em ordem, já marcamos todos os números, que são divisíveis por pelo menos um dos números primos, como divisíveis. Portanto, se chegarmos a uma célula e ela não estiver marcada, então ela não é divisível por nenhum número primo menor e, portanto, deve ser primo.

[[Implementação - Crivo de Eratóstenes]]
[[Análise Assintótica - Crivo de Eratóstenes]]
[[Diferentes otimizações do Crivo de Eratóstenes]]
[[Encontrar primos no intervalo - Crivo de Eratóstenes]]
[[Modificação em Tempo Linear - Crivo de Eratóstenes]]
