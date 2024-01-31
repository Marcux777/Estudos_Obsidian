# União de Conjuntos Disjuntos
Este artigo discute a estrutura de dados União de Conjuntos Disjuntos ou DSU. Muitas vezes também é chamada de Union Find por causa de suas duas principais operações.

Esta estrutura de dados fornece as seguintes capacidades. Recebemos vários elementos, cada um dos quais é um conjunto separado. Uma DSU terá uma operação para combinar quaisquer dois conjuntos, e será capaz de dizer em qual conjunto um elemento específico está. A versão clássica também introduz uma terceira operação, ela pode criar um conjunto a partir de um novo elemento.

Assim, a interface básica desta estrutura de dados consiste em apenas três operações:

- `make_set(v)` - cria um novo conjunto consistindo do novo elemento v
- `union_sets(a, b)` - mescla os dois conjuntos especificados (o conjunto no qual o elemento a está localizado, e o conjunto no qual o elemento b está localizado)
- `find_set(v)` - retorna o representante (também chamado de líder) do conjunto que contém o elemento v. Este representante é um elemento de seu conjunto correspondente. Ele é selecionado em cada conjunto pela própria estrutura de dados (e pode mudar ao longo do tempo, nomeadamente após chamadas `union_sets`). Este representante pode ser usado para verificar se dois elementos fazem parte do mesmo conjunto ou não. a e b estão exatamente no mesmo conjunto, se `find_set(a) == find_set(b)`. Caso contrário, eles estão em conjuntos diferentes.
Como descrito em mais detalhes mais tarde, a estrutura de dados permite que você faça cada uma dessas operações em quase  $O(1)$  tempo em média.

Também em uma das subseções, uma estrutura alternativa de uma DSU é explicada, que alcança uma complexidade média mais lenta de  $O(\log n)$ , mas pode ser mais poderosa do que a estrutura regular DSU.

## Construir uma estrutura de dados eficiente
Armazenaremos os conjuntos na forma de árvores: cada árvore corresponderá a um conjunto. E a raiz da árvore será o representante/líder do conjunto.

Na imagem a seguir, você pode ver a representação de tais árvores.

![[Pasted image 20240130193618.png]]

No início, cada elemento começa como um único conjunto, portanto cada vértice é sua própria árvore. Então combinamos o conjunto contendo o elemento 1 e o conjunto contendo o elemento 2. Depois combinamos o conjunto contendo o elemento 3 e o conjunto contendo o elemento 4. E no último passo, combinamos o conjunto contendo o elemento 1 e o conjunto contendo o elemento 3.

Para a implementação, isso significa que teremos que manter um array `parent` que armazena uma referência ao seu ancestral imediato na árvore.

### Implementação Ingênua
Já podemos escrever a primeira implementação da estrutura de dados União de Conjuntos Disjuntos. Será bastante ineficiente no início, mas depois podemos melhorá-la usando duas otimizações, de modo que levará quase um tempo constante para cada chamada de função.

Como dissemos, todas as informações sobre os conjuntos de elementos serão mantidas em um array `parent`.

Para criar um novo conjunto (operação `make_set(v)`), simplesmente criamos uma árvore com raiz no vértice v, o que significa que ele é seu próprio ancestral.

Para combinar dois conjuntos (operação `union_sets(a, b)`), primeiro encontramos o representante do conjunto no qual a está localizado, e o representante do conjunto no qual b está localizado. Se os representantes forem idênticos, não temos nada a fazer, os conjuntos já estão mesclados. Caso contrário, podemos simplesmente especificar que um dos representantes é o pai do outro representante - combinando assim as duas árvores.

Finalmente, a implementação da função encontrar representante (operação `find_set(v)`): simplesmente subimos os ancestrais do vértice v até chegarmos à raiz, ou seja, um vértice tal que a referência ao ancestral leva a si mesmo. Esta operação é facilmente implementada de forma recursiva.

```c++
void make_set(int v) {
    parent[v] = v;
}

int find_set(int v) {
    if (v == parent[v])
        return v;
    return find_set(parent[v]);
}

void union_sets(int a, int b) {
    a = find_set(a);
    b = find_set(b);
    if (a != b)
        parent[b] = a;
}
```
No entanto, esta implementação é ineficiente. É fácil construir um exemplo, de modo que as árvores degenerem em longas cadeias. Nesse caso, cada chamada `find_set(v)` pode levar  $O(n)$  tempo.

Isso está longe da complexidade que queremos ter (tempo quase constante). Portanto, consideraremos duas otimizações que permitirão acelerar significativamente o trabalho.

### Otimização de Compressão de Caminho
Esta otimização é projetada para acelerar `find_set`.

Se chamarmos `find_set(v)` para algum vértice v, na verdade encontramos o representante p para todos os vértices que visitamos no caminho entre v e o representante real p. O truque é tornar os caminhos para todos esses nós mais curtos, definindo o pai de cada vértice visitado diretamente para p.

Você pode ver a operação na seguinte imagem. À esquerda, há uma árvore, e à direita, há a árvore comprimida após chamar `find_set(7)`, que encurta os caminhos para os nós visitados 7, 5, 3 e 2.

![[Pasted image 20240130200911.png]]

A nova implementação de `find_set` é a seguinte:

```c++
int find_set(int v) {
    if (v == parent[v])
        return v;
    return parent[v] = find_set(parent[v]);
}
```
A implementação simples faz o que se pretendia: primeiro encontra o representante do conjunto (vértice raiz), e então, no processo de desenrolar da pilha, os nós visitados são anexados diretamente ao representante.

Esta simples modificação da operação já atinge a complexidade de tempo  $O(\log n)$  por chamada em média (aqui sem prova). Há uma segunda modificação, que a tornará ainda mais rápida.

### Otimização por Tamanho / Classificação
Nesta otimização, vamos alterar a operação `union_set`. Para ser preciso, vamos mudar qual árvore é anexada à outra. Na implementação ingênua, a segunda árvore sempre era anexada à primeira. Na prática, isso pode levar a árvores contendo cadeias de comprimento  $O(n)$ . Com essa otimização, evitaremos isso escolhendo com muito cuidado qual árvore será anexada.

Existem muitas heurísticas possíveis que podem ser usadas. As duas abordagens mais populares são: na primeira abordagem, usamos o tamanho das árvores como classificação, e na segunda, usamos a profundidade da árvore (mais precisamente, o limite superior na profundidade da árvore, porque a profundidade diminuirá quando aplicarmos a compressão de caminho).

Em ambas as abordagens, a essência da otimização é a mesma: anexamos a árvore com a classificação mais baixa àquela com a classificação maior.

Aqui está a implementação da união por tamanho:

```c++
void make_set(int v) {
    parent[v] = v;
    size[v] = 1;
}

void union_sets(int a, int b) {
    a = find_set(a);
    b = find_set(b);
    if (a != b) {
        if (size[a] < size[b])
            swap(a, b);
        parent[b] = a;
        size[a] += size[b];
    }
}
```
E aqui está a implementação da união por classificação baseada na profundidade das árvores:

```c++
void make_set(int v) {
    parent[v] = v;
    rank[v] = 0;
}

void union_sets(int a, int b) {
    a = find_set(a);
    b = find_set(b);
    if (a != b) {
        if (rank[a] < rank[b])
            swap(a, b);
        parent[b] = a;
        if (rank[a] == rank[b])
            rank[a]++;
    }
}
```
Ambas as otimizações são equivalentes em termos de complexidade de tempo e espaço. Portanto, na prática, você pode usar qualquer uma delas.

### Complexidade de Tempo
Como mencionado antes, se combinarmos ambas as otimizações - compressão de caminho com união por tamanho / classificação - alcançaremos consultas de tempo quase constante. Acontece que a complexidade de tempo amortizada final é  
$O(\alpha(n))$ , onde  
$\alpha(n)$  é a função inversa de Ackermann, que cresce muito lentamente. Na verdade, ela cresce tão lentamente, que não excede  
$4$  para todos os  
$n$  razoáveis (aproximadamente  
$n < 10^{600}$ ).

A complexidade amortizada é o tempo total por operação, avaliada ao longo de uma sequência de várias operações. A ideia é garantir o tempo total de toda a sequência, enquanto permite que operações individuais sejam muito mais lentas do que o tempo amortizado. Por exemplo, em nosso caso, uma única chamada pode levar  
$O(\log n)$  no pior caso, mas se fizermos  
$m$  tais chamadas consecutivas, acabaremos com um tempo médio de  
$O(\alpha(n))$ .

Também não apresentaremos uma prova para essa complexidade de tempo, pois ela é bastante longa e complicada.

Além disso, vale a pena mencionar que DSU com união por tamanho / classificação, mas sem compressão de caminho, funciona em  
$O(\log n)$  tempo por consulta.

### Ligação por Índice / Ligação por Sorteio
Tanto a união por classificação quanto a união por tamanho exigem que você armazene dados adicionais para cada conjunto e mantenha esses valores durante cada operação de união. Existe também um algoritmo randomizado, que simplifica um pouco a operação de união: ligação por índice.

Atribuímos a cada conjunto um valor aleatório chamado índice, e anexamos o conjunto com o índice menor ao que tem o índice maior. É provável que um conjunto maior tenha um índice maior do que o conjunto menor, portanto, essa operação está intimamente relacionada à união por tamanho. Na verdade, pode ser provado que essa operação tem a mesma complexidade de tempo que a união por tamanho. No entanto, na prática, é um pouco mais lento do que a união por tamanho.

Você pode encontrar uma prova da complexidade e até mais técnicas de união aqui.

```c++
void make_set(int v) {
    parent[v] = v;
    index[v] = rand();
}

void union_sets(int a, int b) {
    a = find_set(a);
    b = find_set(b);
    if (a != b) {
        if (index[a] < index[b])
            swap(a, b);
        parent[b] = a;
    }
}
```
É um equívoco comum que apenas jogar uma moeda, para decidir qual conjunto anexamos ao outro, tem a mesma complexidade. No entanto, isso não é verdade. O artigo vinculado acima conjectura que a ligação por sorteio combinada com a compressão de caminho tem complexidade  $\Omega\left(n \frac{\log n}{\log \log n}\right)$ . E nos benchmarks, ele se sai muito pior do que a união por tamanho/classificação ou ligação por índice.

```c++
void union_sets(int a, int b) {
    a = find_set(a);
    b = find_set(b);
    if (a != b) {
        if (rand() % 2)
            swap(a, b);
        parent[b] = a;
    }
}
```
## Aplicações e várias melhorias
Nesta seção, consideramos várias aplicações da estrutura de dados, tanto os usos triviais quanto algumas melhorias na estrutura de dados.

### Componentes Conectados em um Grafo
Esta é uma das aplicações óbvias do DSU.

Formalmente, o problema é definido da seguinte maneira: Inicialmente, temos um grafo vazio. Temos que adicionar vértices e arestas não direcionadas e responder a consultas do tipo  $(a, b)$  - "os vértices  $a$  e  $b$  estão no mesmo componente conectado do grafo?"

Aqui podemos aplicar diretamente a estrutura de dados e obter uma solução que lida com a adição de um vértice ou uma aresta e uma consulta em tempo quase constante na média.

Esta aplicação é bastante importante, porque quase o mesmo problema aparece no algoritmo de Kruskal para encontrar uma árvore geradora mínima. Usando DSU, podemos melhorar a complexidade  $O(m \log n + n^2)$  para  $O(m \log n)$ .

### Busca por Componentes Conectados em uma Imagem
Uma das aplicações do DSU é a seguinte tarefa: existe uma imagem de  $n \times m$  pixels. Originalmente todos são brancos, mas então alguns pixels pretos são desenhados. Você quer determinar o tamanho de cada componente conectado branco na imagem final.

Para a solução, simplesmente iteramos sobre todos os pixels brancos na imagem, para cada célula iteramos sobre seus quatro vizinhos, e se o vizinho for branco chamamos `union_sets`. Assim, teremos um DSU com  $n m$  nós correspondentes aos pixels da imagem. As árvores resultantes no DSU são os componentes conectados desejados.

O problema também pode ser resolvido por DFS ou BFS, mas o método descrito aqui tem uma vantagem: ele pode processar a matriz linha por linha (ou seja, para processar uma linha, só precisamos da linha anterior e da linha atual, e só precisamos de um DSU construído para os elementos de uma linha) em  $O(\min(n, m))$  de memória.

### Armazenar Informações Adicionais para Cada Conjunto
O DSU permite armazenar facilmente informações adicionais nos conjuntos.

Um exemplo simples é o tamanho dos conjuntos: o armazenamento dos tamanhos já foi descrito na seção União por Tamanho (a informação foi armazenada pelo representante atual do conjunto).

Da mesma forma - armazenando-o nos nós representantes - você também pode armazenar qualquer outra informação sobre os conjuntos.

### Comprimir Saltos ao Longo de um Segmento / Pintar Subarrays Offline
Uma aplicação comum do DSU é a seguinte: Existe um conjunto de vértices, e cada vértice tem uma aresta de saída para outro vértice. Com o DSU, você pode encontrar o ponto final, para o qual chegamos após seguir todas as arestas a partir de um determinado ponto de partida, em tempo quase constante.

Um bom exemplo desta aplicação é o problema de pintar subarrays. Temos um segmento de comprimento  $L$ , cada elemento inicialmente tem a cor 0. Temos que repintar o subarray  $[l, r]$  com a cor  $c$  para cada consulta  $(l, r, c)$ . No final, queremos encontrar a cor final de cada célula. Supomos que conhecemos todas as consultas antecipadamente, ou seja, a tarefa é offline.

Para a solução, podemos fazer um DSU, que para cada célula armazena um link para a próxima célula não pintada. Assim, inicialmente, cada célula aponta para si mesma. Depois de pintar uma repintura solicitada de um segmento, todas as células desse segmento apontarão para a célula após o segmento.

Agora, para resolver este problema, consideramos as consultas na ordem inversa: de última a primeira. Desta forma, quando executamos uma consulta, só temos que pintar exatamente as células não pintadas no subarray  $[l, r]$ . Todas as outras células já contêm sua cor final. Para iterar rapidamente sobre todas as células não pintadas, usamos o DSU. Encontramos a célula não pintada mais à esquerda dentro de um segmento, repintamos e, com o ponteiro, movemos para a próxima célula vazia à direita.

Aqui podemos usar o DSU com compressão de caminho, mas não podemos usar união por classificação / tamanho (porque é importante quem se torna o líder após a fusão). Portanto, a complexidade será  $O(\log n)$  por união (que também é bastante rápido).

Implementação:

```c++
for (int i = 0; i <= L; i++) {
    make_set(i);
}

for (int i = m-1; i >= 0; i--) {
    int l = query[i].l;
    int r = query[i].r;
    int c = query[i].c;
    for (int v = find_set(l); v <= r; v = find_set(v)) {
        answer[v] = c;
        parent[v] = v + 1;
    }
}
```
Existe uma otimização: Podemos usar união por classificação, se armazenarmos a próxima célula não pintada em um array adicional `end[]`. Então podemos mesclar dois conjuntos em um classificado de acordo com suas heurísticas, e obtemos a solução em  $O(\alpha(n))$ .

### Suporte a distâncias até o representante
Às vezes, em aplicações específicas do DSU, você precisa manter a distância entre um vértice e o representante de seu conjunto (ou seja, o comprimento do caminho na árvore do nó atual até a raiz da árvore).

Se não usarmos a compressão de caminho, a distância é apenas o número de chamadas recursivas. Mas isso será ineficiente.

No entanto, é possível fazer a compressão de caminho, se armazenarmos a distância até o pai como informação adicional para cada nó.

Na implementação, é conveniente usar um array de pares para `parent[]` e a função `find_set` agora retorna dois números: o representante do conjunto e a distância até ele.

```c++
void make_set(int v) {
    parent[v] = make_pair(v, 0);
    rank[v] = 0;
}

pair<int, int> find_set(int v) {
    if (v != parent[v].first) {
        int len = parent[v].second;
        parent[v] = find_set(parent[v].first);
        parent[v].second += len;
    }
    return parent[v];
}

void union_sets(int a, int b) {
    a = find_set(a).first;
    b = find_set(b).first;
    if (a != b) {
        if (rank[a] < rank[b])
            swap(a, b);
        parent[b] = make_pair(a, 1);
        if (rank[a] == rank[b])
            rank[a]++;
    }
}
```
### Suporte à paridade do comprimento do caminho / Verificação de bipartição online
Da mesma forma que o cálculo do comprimento do caminho até o líder, é possível manter a paridade do comprimento do caminho antes dele. Por que esta aplicação está em um parágrafo separado?

A exigência incomum de armazenar a paridade do caminho surge na seguinte tarefa: inicialmente, nos é dado um grafo vazio, podem ser adicionadas arestas, e temos que responder a consultas do tipo "o componente conectado contendo este vértice é bipartido?".

Para resolver este problema, fazemos um DSU para armazenar os componentes e armazenar a paridade do caminho até o representante para cada vértice. Assim, podemos verificar rapidamente se a adição de uma aresta leva a uma violação da bipartição ou não: ou seja, se as extremidades da aresta estão no mesmo componente conectado e têm o mesmo comprimento de paridade até o líder, então a adição desta aresta produzirá um ciclo de comprimento ímpar, e o componente perderá a propriedade de bipartição.

A única dificuldade que enfrentamos é calcular a paridade no método `union_find`.

Se adicionarmos uma aresta  $(a, b)$  que conecta dois componentes conectados em um, então, quando você anexa uma árvore a outra, precisamos ajustar a paridade.

Vamos derivar uma fórmula, que calcula a paridade emitida para o líder do conjunto que será anexado a outro conjunto. Deixe  $x$  ser a paridade do comprimento do caminho do vértice  $a$  até seu líder  $A$ , e  $y$  como a paridade do comprimento do caminho do vértice  $b$  até seu líder  $B$ , e  $t$  a paridade desejada que temos que atribuir a  $B$  após a fusão. O caminho contém as três partes: de  $B$  para  $b$ , de  $b$  para  $a$ , que é conectado por uma aresta e, portanto, tem paridade  $1$ , e de  $a$  para  $A$ . Portanto, recebemos a fórmula ( $\oplus$  denota a operação XOR):
$$t = x \oplus y \oplus 1$$ 
Assim, independentemente de quantas junções realizamos, a paridade das arestas é transportada de um líder para outro.

Damos a implementação do DSU que suporta paridade. Como na seção anterior, usamos um par para armazenar o ancestral e a paridade. Além disso, para cada conjunto, armazenamos no array `bipartite[]` se ainda é bipartido ou não.

```c++
void make_set(int v) {
    parent[v] = make_pair(v, 0);
    rank[v] = 0;
    bipartite[v] = true;
}

pair<int, int> find_set(int v) {
    if (v != parent[v].first) {
        int parity = parent[v].second;
        parent[v] = find_set(parent[v].first);
        parent[v].second ^= parity;
    }
    return parent[v];
}

void add_edge(int a, int b) {
    pair<int, int> pa = find_set(a);
    a = pa.first;
    int x = pa.second;

    pair<int, int> pb = find_set(b);
    b = pb.first;
    int y = pb.second;

    if (a == b) {
        if (x == y)
            bipartite[a] = false;
    } else {
        if (rank[a] < rank[b])
            swap (a, b);
        parent[b] = make_pair(a, x^y^1);
        bipartite[a] &= bipartite[b];
        if (rank[a] == rank[b])
            ++rank[a];
    }
}

bool is_bipartite(int v) {
    return bipartite[find_set(v).first];
}
```


### Consulta de Mínimo em Intervalo Offline (RMQ) em  $O(\alpha(n))$  em média / Truque de Arpa
Recebemos um array a[] e temos que calcular alguns mínimos em segmentos dados do array.

A ideia para resolver este problema com DSU é a seguinte: Vamos iterar sobre o array e quando estivermos no elemento i, responderemos a todas as consultas (L, R) com R == i. Para fazer isso de forma eficiente, manteremos um DSU usando os primeiros i elementos com a seguinte estrutura: o pai de um elemento é o próximo elemento menor à direita dele. Então, usando essa estrutura, a resposta para uma consulta será a[find_set(L)], o número menor à direita de L.

Esta abordagem obviamente só funciona offline, ou seja, se soubermos todas as consultas antecipadamente.

É fácil ver que podemos aplicar a compressão de caminho. E também podemos usar a União por classificação, se armazenarmos o líder real em um array separado.

```c++
struct Query {
    int L, R, idx;
};

vector<int> answer;
vector<vector<Query>> container;
container[i] contém todas as consultas com R == i.

stack<int> s;
for (int i = 0; i < n; i++) {
    while (!s.empty() && a[s.top()] > a[i]) {
        parent[s.top()] = i;
        s.pop();
    }
    s.push(i);
    for (Query q : container[i]) {
        answer[q.idx] = a[find_set(q.L)];
    }
}
```
Hoje em dia, este algoritmo é conhecido como truque de Arpa. Ele recebeu o nome de AmirReza Poorakhavan, que descobriu e popularizou esta técnica de forma independente. Embora este algoritmo já existisse antes de sua descoberta.

Ancestral Comum Mais Baixo Offline (LCA) em uma árvore em  
$O(\alpha(n))$  em média¶
O algoritmo para encontrar o LCA é discutido no artigo Ancestral Comum Mais Baixo - Algoritmo offline de Tarjan. Este algoritmo se compara favoravelmente com outros algoritmos para encontrar o LCA devido à sua simplicidade (especialmente em comparação com um algoritmo ótimo como o de Farach-Colton e Bender).