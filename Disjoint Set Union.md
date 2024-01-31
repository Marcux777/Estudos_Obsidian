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
