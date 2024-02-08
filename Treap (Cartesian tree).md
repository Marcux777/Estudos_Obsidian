# Treap (Árvore Cartesiana)
Um treap é uma estrutura de dados que combina árvore binária e heap binário (daí o nome: tree + heap  $\Rightarrow$  Treap).

Mais especificamente, treap é uma estrutura de dados que armazena pares  $(X, Y)$  em uma árvore binária de tal maneira que é uma árvore de busca binária por  $X$  e um heap binário por  $Y$ . Se algum nó da árvore contém valores  $(X_0, Y_0)$ , todos os nós na subárvore esquerda têm  $X \leq X_0$ , todos os nós na subárvore direita têm  $X_0 \leq X$ , e todos os nós em ambas as subárvores esquerda e direita têm  $Y \leq Y_0$ .

Um treap também é frequentemente referido como uma "árvore cartesiana", pois é fácil incorporá-la em um plano cartesiano:
![[Pasted image 20240207183644.png]]

**Treaps foram propostos por Raimund Siedel e Cecilia Aragon em 1989.**

## Vantagens de tal organização de dados
Nessa implementação,  $X$  valores são as chaves (e ao mesmo tempo os valores armazenados no treap), e  $Y$  valores são chamados de prioridades. Sem prioridades, o treap seria uma árvore de busca binária regular por  $X$ , e um conjunto de  $X$  valores poderia corresponder a muitas árvores diferentes, algumas delas degeneradas (por exemplo, na forma de uma lista vinculada), e, portanto, extremamente lentas (as operações principais teriam complexidade  $O(N)$ ).

Ao mesmo tempo, as prioridades (quando são únicas) permitem especificar de forma única a árvore que será construída (claro, não depende da ordem em que os valores são adicionados), o que pode ser provado usando o teorema correspondente. Obviamente, se você escolher as prioridades aleatoriamente, obterá árvores não degeneradas em média, o que garantirá a complexidade  $O(\log N)$  para as operações principais. Daí outro nome desta estrutura de dados - árvore de busca binária randomizada.

## Operações
Um treap fornece as seguintes operações:

- Inserir (X,Y) em  $O(\log N)$ .
	Adiciona um novo nó à árvore. Uma variante possível é passar apenas  $X$  e gerar  $Y$  aleatoriamente dentro da operação.
- Buscar (X) em  $O(\log N)$ .
	Procura um nó com o valor de chave especificado  $X$ . A implementação é a mesma que para uma árvore de busca binária comum.
- Apagar (X) em  $O(\log N)$ .
	Procura um nó com o valor de chave especificado  $X$  e o remove da árvore.
- Construir ( $X_1$ , ...,  $X_N$ ) em  $O(N)$ .
	Constrói uma árvore a partir de uma lista de valores. Isso pode ser feito em tempo linear (assumindo que  $X_1, ..., X_N$  estão ordenados).
- União ( $T_1$ ,  $T_2$ ) em  $O(M \log (N/M))$ .
	Mescla duas árvores, assumindo que todos os elementos são diferentes. É possível alcançar a mesma complexidade se elementos duplicados devem ser removidos durante a mesclagem.
- Interseção ( $T_1$ ,  $T_2$ ) em  $O(M \log (N/M))$ .
	Encontra a interseção de duas árvores (ou seja, seus elementos comuns). Não consideraremos a implementação desta operação aqui.

Além disso, devido ao fato de que um treap é uma árvore de busca binária, ele pode implementar outras operações, como encontrar o  $K$ -ésimo maior elemento ou encontrar o índice de um elemento.

## Descrição da Implementação
Em termos de implementação, cada nó contém  $X$ ,  $Y$  e ponteiros para a esquerda ( $L$ ) e direita ( $R$ ) filhos.

Implementaremos todas as operações necessárias usando apenas duas operações auxiliares: Dividir e Mesclar.

### Dividir

![[Pasted image 20240207184018.png]]

Dividir ( $T$ ,  $X$ ) separa a árvore  $T$  em 2 subárvores  $L$  e  $R$  (que são os valores de retorno de dividir) de modo que  $L$  contém todos os elementos com chave  $X_L \le X$ , e  $R$  contém todos os elementos com chave  $X_R > X$ . Esta operação tem complexidade  $O (\log N)$  e é implementada usando uma recursão limpa:

Se o valor do nó raiz (R) é  $\le X$ , então L consistiria pelo menos de R->L e R. Em seguida, chamamos dividir em R->R, e notamos seu resultado de divisão como L' e R'. Finalmente, L também conteria L', enquanto R = R'.
Se o valor do nó raiz (R) é  $> X$ , então R consistiria pelo menos de R e R->R. Em seguida, chamamos dividir em R->L, e notamos seu resultado de divisão como L' e R'. Finalmente, L=L', enquanto R também conteria R'.
Assim, o algoritmo de divisão é:

1. decidir a qual subárvore o nó raiz pertenceria (esquerda ou direita)
2. chamar recursivamente dividir em um de seus filhos
3. criar o resultado final reutilizando a chamada recursiva de dividir.

### Mesclar

![[Pasted image 20240207184448.png]]

Mesclar ( $T_1$ ,  $T_2$ ) combina duas subárvores  $T_1$  e  $T_2$  e retorna a nova árvore. Esta operação também tem complexidade  $O (\log N)$ . Ela funciona sob a suposição de que  $T_1$  e  $T_2$  estão ordenadas (todas as chaves  $X$  em  $T_1$  são menores que as chaves em  $T_2$ ). Assim, precisamos combinar essas árvores sem violar a ordem das prioridades  $Y$ . Para fazer isso, escolhemos como raiz a árvore que tem maior prioridade  $Y$  no nó raiz, e chamamos recursivamente Mesclar para a outra árvore e a subárvore correspondente do nó raiz selecionado.

### Inserir

![[Pasted image 20240207184543.png]]

Agora a implementação de Inserir ( $X$ ,  $Y$ ) se torna óbvia. Primeiro descemos na árvore (como em uma árvore de busca binária regular por X), e paramos no primeiro nó em que o valor de prioridade é menor que  $Y$ . Encontramos o lugar onde vamos inserir o novo elemento. Em seguida, chamamos Dividir (T, X) na subárvore começando no nó encontrado, e usamos as subárvores retornadas  $L$  e 
$R$  como filhos esquerdo e direito do novo nó.

Alternativamente, a inserção pode ser feita dividindo o treap inicial em  $X$  e fazendo  $2$  mesclagens com o novo nó (veja a figura).

### Apagar

![[Pasted image 20240207184558.png]]

A implementação de Apagar ( $X$ ) também é clara. Primeiro descemos na árvore (como em uma árvore de busca binária regular por  $X$ ), procurando o elemento que queremos deletar. Uma vez que o nó é encontrado, chamamos Mesclar em seus filhos e colocamos o valor de retorno da operação no lugar do elemento que estamos deletando.

Alternativamente, podemos fatorar a subárvore contendo  $X$  com  $2$  operações de divisão e mesclar os treaps restantes (veja a figura).

### Construir

Implementamos a operação Construir com complexidade  $O (N \log N)$  usando  
$N$  chamadas de Inserir.

### União

União ( $T_1$ ,  $T_2$ ) tem complexidade teórica  $O (M \log (N / M))$ , mas na prática funciona muito bem, provavelmente com uma constante oculta muito pequena. Vamos assumir sem perda de generalidade que  $T_1 \rightarrow Y > T_2 \rightarrow Y$ , ou seja, a raiz de  $T_1$  será a raiz do resultado. Para obter o resultado, precisamos mesclar as árvores  $T_1 \rightarrow L$ ,  $T_1 \rightarrow R$  e  $T_2$  em duas árvores que poderiam ser filhas da raiz  
$T_1$ . Para fazer isso, chamamos Dividir ( $T_2$ ,  $T_1\rightarrow X$ ), dividindo assim  $T_2$  em duas partes L e R, que então combinamos recursivamente com os filhos de  $T_1$ : União ( $T_1 \rightarrow L$ ,  $L$ ) e União ( $T_1 \rightarrow R$ ,  $R$ ), obtendo assim as subárvores esquerda e direita do resultado.

## Implementação
```cpp
struct item {
    int key, prior;
    item *l, *r;
    item () { }
    item (int key) : key(key), prior(rand()), l(NULL), r(NULL) { }
    item (int key, int prior) : key(key), prior(prior), l(NULL), r(NULL) { }
};
typedef item* pitem;
```
Esta é a definição do nosso item. Note que existem dois ponteiros filhos, e uma chave inteira (para a BST) e uma prioridade inteira (para o heap). A prioridade é atribuída usando um gerador de números aleatórios.

```cpp
void split (pitem t, int key, pitem & l, pitem & r) {
    if (!t)
        l = r = NULL;
    else if (t->key <= key)
        split (t->r, key, t->r, r),  l = t;
    else
        split (t->l, key, l, t->l),  r = t;
}
```
``t`` é o treap a ser dividido, e key é o valor BST pelo qual dividir. Note que não retornamos os valores de resultado em lugar algum, em vez disso, apenas os usamos assim:

```cpp
pitem l = nullptr, r = nullptr;
split(t, 5, l, r);
if (l) cout << "Tamanho da subárvore esquerda: " << (l->size) << endl;
if (r) cout << "Tamanho da subárvore direita: " << (r->size) << endl;
```
Esta função de divisão pode ser difícil de entender, pois tem ambos os ponteiros (``pitem``) bem como referência para esses ponteiros ``(pitem &l)``. Vamos entender em palavras o que a chamada de função ``split(t, k, l, r)`` pretende: "dividir treap t por valor ``k`` em dois treaps, e armazenar os treaps esquerdos em ``l`` e treap direito em ``r``". Ótimo! Agora, vamos aplicar esta definição às duas chamadas recursivas, usando o trabalho de caso que analisamos na seção anterior: (A primeira condição if é um caso base trivial para um treap vazio)

1. Quando o valor do nó raiz é  $\le$  key, chamamos ``split (t->r, key, t->r``, r), o que significa: "dividir treap ``t->r`` (subárvore direita de t) por valor key e armazenar a subárvore esquerda em ``t->r`` e subárvore direita em r". Depois disso, definimos ``l = t``. Note agora que o valor de resultado ``l`` contém ``t->l``, t bem como ``t->r`` (que é o resultado da chamada recursiva que fizemos) todos já mesclados na ordem correta! Você deve pausar para garantir que este resultado de ``l`` e ``r`` corresponda exatamente ao que discutimos anteriormente em Descrição da Implementação.
2. Quando o valor do nó raiz é maior que key, chamamos split ``(t->l, key, l, t->l)``, o que significa: "dividir treap ``t->l`` (subárvore esquerda de t) por valor key e armazenar a subárvore esquerda em l e subárvore direita em ``t->l``. Depois disso, definimos ``r = t``. Note agora que o valor de resultado r contém ``t->l`` (que é o resultado da chamada recursiva que fizemos), t bem como ``t->r``, todos já mesclados na ordem correta! Você deve pausar para garantir que este resultado de ``l`` e ``r`` corresponda exatamente ao que discutimos anteriormente em Descrição da Implementação.
Se você ainda está tendo problemas para entender a implementação, você deve olhar para ela indutivamente, ou seja: não tente quebrar as chamadas recursivas repetidamente. Assuma que a implementação de divisão funciona corretamente em treap vazio, então tente executá-la para um treap de nó único, então um treap de dois nós, e assim por diante, reutilizando cada vez o seu conhecimento de que a divisão em treaps menores funciona.

```cpp
void insert (pitem & t, pitem it) {
    if (!t)
        t = it;
    else if (it->prior > t->prior)
        split (t, it->key, it->l, it->r),  t = it;
    else
        insert (t->key <= it->key ? t->r : t->l, it);
}

void merge (pitem & t, pitem l, pitem r) {
    if (!l || !r)
        t = l ? l : r;
    else if (l->prior > r->prior)
        merge (l->r, l->r, r),  t = l;
    else
        merge (r->l, l, r->l),  t = r;
}

void erase (pitem & t, int key) {
    if (t->key == key) {
        pitem th = t;
        merge (t, t->l, t->r);
        delete th;
    }
    else
        erase (key < t->key ? t->l : t->r, key);
}

pitem unite (pitem l, pitem r) {
    if (!l || !r)  return l ? l : r;
    if (l->prior < r->prior)  swap (l, r);
    pitem lt, rt;
    split (r, l->key, lt, rt);
    l->l = unite (l->l, lt);
    l->r = unite (l->r, rt);
    return l;
}
```



## Manutenção dos tamanhos das subárvores
Para estender a funcionalidade do treap, muitas vezes é necessário armazenar o número de nós na subárvore de cada nó - campo ``int cnt`` na estrutura do ``item``. Por exemplo, ele pode ser usado para encontrar o K-ésimo maior elemento da árvore em  $O (\log N)$ , ou para encontrar o índice do elemento na lista ordenada com a mesma complexidade. A implementação dessas operações será a mesma que para a árvore de busca binária regular.

Quando uma árvore muda (nós são adicionados ou removidos etc.), ``cnt`` de alguns nós deve ser atualizado de acordo. Vamos criar duas funções: ``cnt()`` retornará o valor atual de ``cnt`` ou ``0`` se o nó não existir, e ``upd_cnt()`` atualizará o valor de cnt para este nó assumindo que para seus filhos ``L`` e ``R`` os valores de ``cnt`` já foram atualizados. Evidentemente, é suficiente adicionar chamadas de ``upd_cnt()`` ao final de inserir, apagar, dividir e mesclar para manter os valores de ``cnt`` atualizados.

```cpp
int cnt (pitem t) {
    return t ? t->cnt : 0;
}

void upd_cnt (pitem t) {
    if (t)
        t->cnt = 1 + cnt(t->l) + cnt (t->r);
}
```

## Construindo um Treap em  $O (N)$  no modo offline
Dada uma lista ordenada de chaves, é possível construir um treap mais rápido do que inserindo as chaves uma de cada vez, o que leva  $O(N \log N)$ . Como as chaves estão ordenadas, uma árvore de busca binária balanceada pode ser facilmente construída em tempo linear. Os valores do heap  $Y$  são inicializados aleatoriamente e então podem ser transformados em heap independentemente das chaves  $X$  para construir o heap em  $O(N)$ .

```cpp
void heapify (pitem t) {
    if (!t) return;
    pitem max = t;
    if (t->l != NULL && t->l->prior > max->prior)
        max = t->l;
    if (t->r != NULL && t->r->prior > max->prior)
        max = t->r;
    if (max != t) {
        swap (t->prior, max->prior);
        heapify (max);
    }
}

pitem build (int * a, int n) {
    // Construir um treap nos valores {a[0], a[1], ..., a[n - 1]}
    if (n == 0) return NULL;
    int mid = n / 2;
    pitem t = new item (a[mid], rand ());
    t->l = build (a, mid);
    t->r = build (a + mid + 1, n - mid - 1);
    heapify (t);
    upd_cnt(t)
    return t;
}
```
Nota: chamar ``upd_cnt(t)`` é necessário apenas se você precisar dos tamanhos das subárvores.

A abordagem acima sempre fornece uma árvore perfeitamente balanceada, o que geralmente é bom para fins práticos, mas ao custo de não preservar as prioridades que foram inicialmente atribuídas a cada nó. Assim, esta abordagem não é viável para resolver o seguinte problema:

>- acmsguru - Árvore Cartesiana
	Dada uma sequência de pares  $(x_i, y_i)$ , construa uma árvore cartesiana sobre eles. Todos  $x_i$  e todos  $y_i$  são únicos.

Note que neste problema as prioridades não são aleatórias, portanto, apenas inserir vértices um por um poderia fornecer uma solução quadrática.

Uma das possíveis soluções aqui é encontrar para cada elemento os elementos mais próximos à esquerda e à direita que têm uma prioridade menor do que este elemento. Entre esses dois elementos, aquele com a maior prioridade deve ser o pai do elemento atual.

Este problema é resolvível com uma modificação de pilha mínima em tempo linear:

```cpp
void connect(auto from, auto to) {
    vector<pitem> st;
    for(auto it: ranges::subrange(from, to)) {
        while(!st.empty() && st.back()->prior > it->prior) {
            st.pop_back();
        }
        if(!st.empty()) {
            if(!it->p || it->p->prior < st.back()->prior) {
                it->p = st.back();
            }
        }
        st.push_back(it);
    }
}

pitem build(int *x, int *y, int n) {
    vector<pitem> nodes(n);
    for(int i = 0; i < n; i++) {
        nodes[i] = new item(x[i], y[i]);
    }
    connect(nodes.begin(), nodes.end());
    connect(nodes.rbegin(), nodes.rend());
    for(int i = 0; i < n; i++) {
        if(nodes[i]->p) {
            if(nodes[i]->p->key < nodes[i]->key) {
                nodes[i]->p->r = nodes[i];
            } else {
                nodes[i]->p->l = nodes[i];
            }
        }
    }
    return nodes[min_element(y, y + n) - y];
}
```
## Treaps Implícitos
Treap implícito é uma simples modificação do treap regular que é uma estrutura de dados muito poderosa. Na verdade, o treap implícito pode ser considerado como um array com os seguintes procedimentos implementados (todos em  $O (\log N)$  no modo online):

- Inserção de um elemento no array em qualquer local
- Remoção de um elemento arbitrário
- Encontrar soma, elemento mínimo/máximo etc. em um intervalo arbitrário
- Adição, pintura em um intervalo arbitrário
- Reversão de elementos em um intervalo arbitrário
A ideia é que as chaves devem ser índices baseados em nulo dos elementos no array. Mas não armazenaremos esses valores explicitamente (caso contrário, por exemplo, a inserção de um elemento causaria mudanças da chave em  $O (N)$  nós da árvore).

Note que a chave de um nó é o número de nós menores que ele (tais nós podem estar presentes não apenas em sua subárvore esquerda, mas também nas subárvores esquerdas de seus ancestrais). Mais especificamente, a chave implícita para algum nó T é o número de vértices  $cnt (T \rightarrow L)$  na subárvore esquerda deste nó mais valores similares  $cnt (P \rightarrow L) + 1$  para cada ancestral P do nó T, se T está na subárvore direita de P.

Agora está claro como calcular rapidamente a chave implícita do nó atual. Como em todas as operações chegamos a qualquer nó descendo na árvore, podemos apenas acumular essa soma e passá-la para a função. Se formos para a subárvore esquerda, a soma acumulada não muda, se formos para a subárvore direita ela aumenta por  $cnt (T \rightarrow L) +1$ .

Aqui estão as novas implementações de Dividir e Mesclar:

```cpp
void merge (pitem & t, pitem l, pitem r) {
    if (!l || !r)
        t = l ? l : r;
    else if (l->prior > r->prior)
        merge (l->r, l->r, r),  t = l;
    else
        merge (r->l, l, r->l),  t = r;
    upd_cnt (t);
}

void split (pitem t, pitem & l, pitem & r, int key, int add = 0) {
    if (!t)
        return void( l = r = 0 );
    int cur_key = add + cnt(t->l); //implicit key
    if (key <= cur_key)
        split (t->l, l, t->l, key, add),  r = t;
    else
        split (t->r, t->r, r, key, add + 1 + cnt(t->l)),  l = t;
    upd_cnt (t);
}
```

Na implementação acima, após a chamada de $split(T, T_1, T_2, k)$, a árvore $T_1$ consistirá nos primeiros $k$ elementos de $T$ (ou seja, elementos que têm sua chave implícita menor que $k$) e $T_2$ consistirá em todos os demais.

Agora vamos considerar a implementação de várias operações em treaps implícitos:

- Inserir elemento.
	Suponha que precisamos inserir um elemento na posição $pos$. Dividimos o treap em duas partes, que correspondem aos arrays $[0..pos-1]$ e $[pos..sz]$; para fazer isso, chamamos $split(T, T_1, T_2, pos)$. Então podemos combinar a árvore $T_1$ com o novo vértice chamando $merge(T_1, T_1, \text{new item})$ (é fácil ver que todas as pré-condições são atendidas). Finalmente, combinamos as árvores $T_1$ e $T_2$ de volta em $T$ chamando $merge(T, T_1, T_2)$.

- Deletar elemento.
	Esta operação é ainda mais fácil: encontre o elemento a ser deletado $T$, realize a fusão de seus filhos $L$ e $R$, e substitua o elemento $T$ pelo resultado da fusão. Na verdade, a exclusão de elementos no treap implícito é exatamente a mesma que no treap regular.

- Encontrar soma / mínimo, etc. no intervalo.
	Primeiro, crie um campo adicional $F$ na estrutura do item para armazenar o valor da função alvo para a subárvore deste nó. Este campo é fácil de manter de forma semelhante à manutenção dos tamanhos das subárvores: crie uma função que calcula este valor para um nó com base nos valores de seus filhos e adicione chamadas desta função no final de todas as funções que modificam a árvore.
	Segundo, precisamos saber como processar uma consulta para um intervalo arbitrário $[A; B]$.
	Para obter uma parte da árvore que corresponde ao intervalo $[A; B]$, precisamos chamar $split(T, T_2, T_3, B+1)$, e então $split(T_2, T_1, T_2, A)$: após isso, $T_2$ consistirá em todos os elementos no intervalo $[A; B]$, e apenas neles. Portanto, a resposta à consulta será armazenada no campo $F$ da raiz de $T_2$. Após a consulta ser respondida, a árvore deve ser restaurada chamando $merge(T, T_1, T_2)$ e $merge(T, T, T_3)$.

- Adição / pintura no intervalo.
	Agimos de maneira semelhante ao parágrafo anterior, mas em vez do campo F, armazenaremos um campo add que conterá o valor adicionado para a subárvore (ou o valor para o qual a subárvore é pintada). Antes de realizar qualquer operação, temos que "empurrar" este valor corretamente - ou seja, mudar $T \rightarrow L \rightarrow add$ e $T \rightarrow R \rightarrow add$, e limpar add no nó pai. Desta forma, após quaisquer alterações na árvore, a informação não será perdida.

- Reverter no intervalo.
	Isso é novamente semelhante à operação anterior: temos que adicionar uma flag booleana rev e definir como true quando a subárvore do nó atual precisa ser revertida. "Empurrar" este valor é um pouco complicado - trocamos os filhos deste nó e definimos esta flag como true para eles.

Aqui está uma implementação de exemplo do treap implícito com reversão no intervalo. Para cada nó, armazenamos um campo chamado value que é o valor real do elemento do array na posição atual. Também fornecemos a implementação da função ``output()``, que produz um array que corresponde ao estado atual do treap implícito.

```cpp
typedef struct item * pitem;
struct item {
    int prior, value, cnt;
    bool rev;
    pitem l, r;
};

int cnt (pitem it) {
    return it ? it->cnt : 0;
}

void upd_cnt (pitem it) {
    if (it)
        it->cnt = cnt(it->l) + cnt(it->r) + 1;
}

void push (pitem it) {
    if (it && it->rev) {
        it->rev = false;
        swap (it->l, it->r);
        if (it->l)  it->l->rev ^= true;
        if (it->r)  it->r->rev ^= true;
    }
}

void merge (pitem & t, pitem l, pitem r) {
    push (l);
    push (r);
    if (!l || !r)
        t = l ? l : r;
    else if (l->prior > r->prior)
        merge (l->r, l->r, r),  t = l;
    else
        merge (r->l, l, r->l),  t = r;
    upd_cnt (t);
}

void split (pitem t, pitem & l, pitem & r, int key, int add = 0) {
    if (!t)
        return void( l = r = 0 );
    push (t);
    int cur_key = add + cnt(t->l);
    if (key <= cur_key)
        split (t->l, l, t->l, key, add),  r = t;
    else
        split (t->r, t->r, r, key, add + 1 + cnt(t->l)),  l = t;
    upd_cnt (t);
}

void reverse (pitem t, int l, int r) {
    pitem t1, t2, t3;
    split (t, t1, t2, l);
    split (t2, t2, t3, r-l+1);
    t2->rev ^= true;
    merge (t, t1, t2);
    merge (t, t, t3);
}

void output (pitem t) {
    if (!t)  return;
    push (t);
    output (t->l);
    printf ("%d ", t->value);
    output (t->r);
}
```