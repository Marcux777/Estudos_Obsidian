## Algoritmo de Dijkstra

Você recebe um grafo ponderado, direcionado ou não direcionado, com n vértices e m arestas. Os pesos de todas as arestas são não negativos. Você também recebe um vértice inicial s. Este artigo discute como encontrar os comprimentos dos caminhos mais curtos de um vértice inicial s para todos os outros vértices e como gerar os caminhos mais curtos.

Este problema também é chamado de **problema do caminho mais curto de origem única**.

## Algoritmo

Aqui está um algoritmo descrito pelo cientista da computação holandês Edsger W. Dijkstra em 1959.

Vamos criar um array d[] onde, para cada vértice v, armazenamos o comprimento atual do caminho mais curto de s a v em d[v]. Inicialmente, d[s]=0 e, para todos os outros vértices, esse comprimento é igual a infinito. Na implementação, um número suficientemente grande (que é garantido ser maior que qualquer comprimento de caminho possível) é escolhido como infinito.

d[v]=∞, v=s

Além disso, mantemos um array booleano u[] que armazena, para cada vértice v, se ele está marcado ou não. Inicialmente, todos os vértices estão desmarcados:

u[v]=false

O algoritmo de Dijkstra é executado por n iterações. Em cada iteração, um vértice v é escolhido como vértice não marcado que possui o menor valor d[v].

Evidentemente, na primeira iteração, o vértice inicial s será selecionado.

O vértice v selecionado é marcado. Em seguida, a partir do vértice v, **relaxamentos** são realizados: todas as arestas da forma (v,to) são consideradas e, para cada vértice to, o algoritmo tenta melhorar o valor d[to]. Se o comprimento da aresta atual for igual a len, o código para relaxamento é:

d[to]=min(d[to],d[v]+len)

Após todas essas arestas serem consideradas, a iteração atual termina. Finalmente, após <0>n iterações, todos os vértices serão marcados e o algoritmo termina. Afirmamos que os valores encontrados d[v] são os comprimentos dos caminhos mais curtos de s para todos os vértices v.

Observe que, se alguns vértices forem inalcançáveis a partir do vértice inicial s, os valores d[v] para eles permanecerão infinitos. Obviamente, as últimas iterações do algoritmo escolherão esses vértices, mas nenhum trabalho útil será feito para eles. Portanto, o algoritmo pode ser interrompido assim que o vértice selecionado tiver distância infinita.

### Restaurando Caminhos Mais Curtos

Normalmente, é necessário saber não apenas os comprimentos dos caminhos mais curtos, mas também os próprios caminhos mais curtos. Vamos ver como manter informações suficientes para restaurar o caminho mais curto de s para qualquer vértice. Manteremos um array de predecessores p[] no qual, para cada vértice v=s, p[v] é o penúltimo vértice no caminho mais curto de s a v. Aqui, usamos o fato de que, se pegarmos o caminho mais curto para algum vértice v e removermos v desse caminho, obteremos um caminho terminando no vértice p[v] e esse caminho será o mais curto para o vértice p[v]. Este array de predecessores pode ser usado para restaurar o caminho mais curto para qualquer vértice: começando com v, pegue repetidamente o predecessor do vértice atual até chegarmos ao vértice inicial s para obter o caminho mais curto necessário com os vértices listados em ordem inversa. Assim, o caminho mais curto P para o vértice v é igual a:

$$P=(s,…,p[p[p[v]]],p[p[v]],p[v],v)$$

Construir esse array de predecessores é muito simples: para cada relaxamento bem-sucedido, ou seja, quando para algum vértice selecionado v há uma melhoria na distância para algum vértice to, atualizamos o vértice predecessor para to com o vértice v:

$$p[to]=v$$