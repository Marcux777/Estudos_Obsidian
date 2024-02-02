# Árvore de Segmentos
Uma Árvore de Segmentos é uma estrutura de dados que armazena informações sobre intervalos de array como uma árvore. Isso permite responder consultas de intervalo em um array de maneira eficiente, enquanto ainda é flexível o suficiente para permitir a rápida modificação do array. Isso inclui encontrar a soma de elementos consecutivos do array  $a[l \dots r]$ , ou encontrar o elemento mínimo em um intervalo desse tipo em  $O(\log n)$  tempo. Entre responder a essas consultas, a Árvore de Segmentos permite modificar o array substituindo um elemento, ou mesmo alterando os elementos de todo um subsegmento (por exemplo, atribuindo todos os elementos  $a[l \dots r]$  a qualquer valor, ou adicionando um valor a todos os elementos no subsegmento).

Em geral, uma Árvore de Segmentos é uma estrutura de dados muito flexível, e um grande número de problemas pode ser resolvido com ela. Além disso, também é possível aplicar operações mais complexas e responder a consultas mais complexas (veja versões avançadas de Árvores de Segmentos). Em particular, a Árvore de Segmentos pode ser facilmente generalizada para dimensões maiores. Por exemplo, com uma Árvore de Segmentos bidimensional, você pode responder a consultas de soma ou mínimo sobre algum sub-retângulo de uma matriz dada em apenas  
$O(\log^2 n)$  tempo.

Uma propriedade importante das Árvores de Segmentos é que elas requerem apenas uma quantidade linear de memória. A Árvore de Segmentos padrão requer 
$4n$  vértices para trabalhar em um array de tamanho  $n$ .

## Forma mais simples de uma Árvore de Segmentos
Para começar fácil, consideramos a forma mais simples de uma Árvore de Segmentos. Queremos responder eficientemente a consultas de soma. A definição formal de nossa tarefa é: Dado um array  $a[0 \dots n-1]$ , a Árvore de Segmentos deve ser capaz de encontrar a soma dos elementos entre os índices  $l$  e  
$r$  (ou seja, calcular a soma  $\sum_{i=l}^r a[i]$ ), e também lidar com a mudança de valores dos elementos no array (ou seja, realizar atribuições do tipo  $a[i] = x$ ). A Árvore de Segmentos deve ser capaz de processar ambas as consultas em  $O(\log n)$  tempo.

Isso é uma melhoria em relação às abordagens mais simples. Uma implementação de array ingênua - apenas usando um array simples - pode atualizar elementos em  
$O(1)$ , mas requer  $O(n)$  para calcular cada consulta de soma. E somas de prefixos pré-computadas podem calcular consultas de soma em  $O(1)$ , mas a atualização de um elemento do array requer  $O(n)$  alterações nas somas de prefixos.

### Estrutura da Árvore de Segmentos
Podemos adotar uma abordagem de dividir para conquistar quando se trata de segmentos de array. Calculamos e armazenamos a soma dos elementos de todo o array, ou seja, a soma do segmento  $a[0 \dots n-1]$ . Em seguida, dividimos o array em duas metades  $a[0 \dots n/2-1]$  e  $a[n/2 \dots n-1]$  e calculamos a soma de cada metade e armazenamos. Cada uma dessas duas metades por sua vez são divididas pela metade, e assim por diante até que todos os segmentos atinjam o tamanho  
$1$ .

Podemos ver esses segmentos como formando uma árvore binária: a raiz desta árvore é o segmento  $a[0 \dots n-1]$ , e cada vértice (exceto vértices folha) tem exatamente dois vértices filhos. É por isso que a estrutura de dados é chamada de "Árvore de Segmentos", mesmo que na maioria das implementações a árvore não seja construída explicitamente (veja Implementação).

Aqui está uma representação visual de uma Árvore de Segmentos sobre o array  
$a = [1, 3, -2, 8, -7]$ :

![[Pasted image 20240202044455.png]]

A partir desta breve descrição da estrutura de dados, já podemos concluir que uma Árvore de Segmentos requer apenas um número linear de vértices. O primeiro nível da árvore contém um único nó (a raiz), o segundo nível conterá dois vértices, no terceiro conterá quatro vértices, até que o número de vértices atinja  $n$ . Assim, o número de vértices no pior caso pode ser estimado pela soma  
$1 + 2 + 4 + \dots + 2^{\lceil\log_2 n\rceil} \lt 2^{\lceil\log_2 n\rceil + 1} \lt 4n$ .

Vale a pena notar que sempre que  $n$  não é uma potência de dois, nem todos os níveis da Árvore de Segmentos serão completamente preenchidos. Podemos ver esse comportamento na imagem. Por enquanto, podemos esquecer esse fato, mas ele se tornará importante mais tarde durante a implementação.

A altura da Árvore de Segmentos é  $O(\log n)$ , porque ao descer da raiz para as folhas o tamanho dos segmentos diminui aproximadamente pela metade.

### Construção
Antes de construir a árvore de segmentos, precisamos decidir:

o valor que é armazenado em cada nó da árvore de segmentos. Por exemplo, em uma árvore de segmentos de soma, um nó armazenaria a soma dos elementos em seu intervalo  $[l, r]$ .
a operação de mesclagem que mescla dois irmãos em uma árvore de segmentos. Por exemplo, em uma árvore de segmentos de soma, os dois nós correspondentes aos intervalos  $a[l_1 \dots r_1]$  e  $a[l_2 \dots r_2]$  seriam mesclados em um nó correspondente ao intervalo  $a[l_1 \dots r_2]$  adicionando os valores dos dois nós.
Note que um vértice é um "vértice folha", se seu segmento correspondente cobre apenas um valor no array original. Ele está presente no nível mais baixo de uma árvore de segmentos. Seu valor seria igual ao elemento correspondente  $a[i]$ .

Agora, para a construção da árvore de segmentos, começamos no nível inferior (os vértices folha) e atribuímos a eles seus respectivos valores. Com base nesses valores, podemos calcular os valores do nível anterior, usando a função de mesclagem. E com base nesses, podemos calcular os valores do anterior, e repetir o procedimento até chegarmos ao vértice raiz.

É conveniente descrever essa operação recursivamente na outra direção, ou seja, do vértice raiz para os vértices folha. O procedimento de construção, se chamado em um vértice não folha, faz o seguinte:

constrói recursivamente os valores dos dois vértices filhos mescla os valores computados desses filhos.
Começamos a construção no vértice raiz e, portanto, somos capazes de calcular toda a árvore de segmentos.

A complexidade de tempo desta construção é  $O(n)$ , supondo que a operação de mesclagem é constante no tempo (a operação de mesclagem é chamada  $n$  vezes, que é igual ao número de nós internos na árvore de segmentos).

### Consultas de soma
Por enquanto, vamos responder a consultas de soma. Como entrada, recebemos dois inteiros  $l$  e  $r$ , e temos que calcular a soma do segmento  $a[l \dots r]$  em  $O(\log n)$  tempo.

Para fazer isso, vamos percorrer a Árvore de Segmentos e usar as somas pré-calculadas dos segmentos. Vamos supor que estamos atualmente no vértice que cobre o segmento  $a[tl \dots tr]$ . Existem três casos possíveis.

O caso mais fácil é quando o segmento  $a[l \dots r]$  é igual ao segmento correspondente do vértice atual (ou seja,  $a[l \dots r] = a[tl \dots tr]$ ), então terminamos e podemos retornar a soma pré-calculada que está armazenada no vértice.

Alternativamente, o segmento da consulta pode cair completamente no domínio do filho à esquerda ou à direita. Lembre-se de que o filho à esquerda cobre o segmento $a[tl \dots tm]$  e o vértice à direita cobre o segmento  $a[tm + 1 \dots tr]$  com  $tm = (tl + tr) / 2$ . Neste caso, podemos simplesmente ir para o vértice filho, cujo segmento correspondente cobre o segmento da consulta, e executar o algoritmo descrito aqui com esse vértice.

E então há o último caso, o segmento da consulta intersecta com ambos os filhos. Neste caso, não temos outra opção a não ser fazer duas chamadas recursivas, uma para cada filho. Primeiro vamos para o filho à esquerda, calculamos uma resposta parcial para este vértice (ou seja, a soma dos valores da interseção entre o segmento da consulta e o segmento do filho à esquerda), depois vamos para o filho à direita, calculamos a resposta parcial usando esse vértice, e então combinamos as respostas somando-as. Em outras palavras, como o filho à esquerda representa o segmento  $a[tl \dots tm]$  e o filho à direita o segmento  $a[tm+1 \dots tr]$ , calculamos a consulta de soma  $a[l \dots tm]$  usando o filho à esquerda, e a consulta de soma  $a[tm+1 \dots r]$  usando o filho à direita.

Portanto, o processamento de uma consulta de soma é uma função que chama a si mesma recursivamente uma vez com o filho à esquerda ou à direita (sem alterar os limites da consulta), ou duas vezes, uma vez para o filho à esquerda e uma vez para o filho à direita (dividindo a consulta em duas subconsultas). E a recursão termina, sempre que os limites do segmento de consulta atual coincidem com os limites do segmento do vértice atual. Nesse caso, a resposta será o valor pré-calculado da soma deste segmento, que está armazenado na árvore.

Em outras palavras, o cálculo da consulta é uma travessia da árvore, que se espalha por todos os ramos necessários da árvore, e usa os valores de soma pré-calculados dos segmentos na árvore.

Obviamente, começaremos a travessia a partir do vértice raiz da Árvore de Segmentos.

O procedimento é ilustrado na seguinte imagem. Novamente, o array  $a = [1, 3, -2, 8, -7]$  é usado, e aqui queremos calcular a soma  $\sum_{i=2}^4 a[i]$ . Os vértices coloridos serão visitados, e usaremos os valores pré-calculados dos vértices verdes. Isso nos dá o resultado  $-2 + 1 = -1$ .

![[Pasted image 20240202044844.png]]

Por que a complexidade deste algoritmo é  $O(\log n)$ ? Para mostrar essa complexidade, olhamos para cada nível da árvore. Acontece que, para cada nível, visitamos no máximo quatro vértices. E como a altura da árvore é  $O(\log n)$ , obtemos o tempo de execução desejado.

Podemos mostrar que essa proposição (no máximo quatro vértices em cada nível) é verdadeira por indução. No primeiro nível, visitamos apenas um vértice, o vértice raiz, então aqui visitamos menos de quatro vértices. Agora vamos olhar para um nível arbitrário. Por hipótese de indução, visitamos no máximo quatro vértices. Se visitarmos no máximo dois vértices, o próximo nível terá no máximo quatro vértices. Isso é trivial, porque cada vértice só pode causar no máximo duas chamadas recursivas. Então, vamos supor que visitamos três ou quatro vértices no nível atual. A partir desses vértices, analisaremos os vértices do meio com mais cuidado. Como a consulta de soma pede a soma de um subarray contínuo, sabemos que os segmentos correspondentes aos vértices visitados no meio serão completamente cobertos pelo segmento da consulta de soma. Portanto, esses vértices não farão nenhuma chamada recursiva. Portanto, apenas o vértice mais à esquerda e o vértice mais à direita terão o potencial de fazer chamadas recursivas. E esses só criarão no máximo quatro chamadas recursivas, então também o próximo nível satisfará a afirmação. Podemos dizer que um ramo se aproxima do limite esquerdo da consulta, e o segundo ramo se aproxima do direito.

Portanto, visitamos no máximo  $4 \log n$  vértices no total, e isso é igual a um tempo de execução de  $O(\log n)$ .

Em conclusão, a consulta funciona dividindo o segmento de entrada em vários subsegmentos para os quais todas as somas já estão pré-calculadas e armazenadas na árvore. E se pararmos de particionar sempre que o segmento de consulta coincidir com o segmento do vértice, então precisamos apenas de  $O(\log n)$  tais segmentos, o que dá a eficácia da Árvore de Segmentos.

### Consultas de atualização
Agora queremos modificar um elemento específico no array, digamos que queremos fazer a atribuição  $a[i] = x$ . E temos que reconstruir a Árvore de Segmentos, de forma que ela corresponda ao novo array modificado.

Esta consulta é mais fácil do que a consulta de soma. Cada nível de uma Árvore de Segmentos forma uma partição do array. Portanto, um elemento  $a[i]$  contribui apenas para um segmento de cada nível. Assim, apenas  $O(\log n)$  vértices precisam ser atualizados.

É fácil ver que a solicitação de atualização pode ser implementada usando uma função recursiva. A função recebe o vértice da árvore atual e chama a si mesma recursivamente com um dos dois vértices filhos (aquele que contém  $a[i]$  em seu segmento), e depois disso recalcula seu valor de soma, de forma semelhante à como é feito no método de construção (ou seja, como a soma de seus dois filhos).

Novamente, aqui está uma visualização usando o mesmo array. Aqui realizamos a atualização  $a[2] = 3$ . Os vértices verdes são os vértices que visitamos e atualizamos.

![[Pasted image 20240202045138.png]]

### Implementação
A principal consideração é como armazenar a Árvore de Segmentos. Claro que podemos definir uma estrutura  $\text{Vertex}$  e criar objetos, que armazenam os limites do segmento, sua soma e adicionalmente também ponteiros para seus vértices filhos. No entanto, isso requer armazenar muitas informações redundantes na forma de ponteiros. Vamos usar um truque simples para tornar isso muito mais eficiente usando uma estrutura de dados implícita: apenas armazenando as somas em um array. (Um método semelhante é usado para heaps binários). A soma do vértice raiz no índice 1, as somas de seus dois vértices filhos nos índices 2 e 3, as somas dos filhos desses dois vértices nos índices 4 a 7, e assim por diante. Com a indexação 1, convenientemente o filho à esquerda de um vértice no índice  $i$  é armazenado no índice  $2i$ , e o direito no índice  $2i + 1$ . Equivalentemente, o pai de um vértice no índice  $i$  é armazenado em  $i/2$  (divisão inteira).

Isso simplifica muito a implementação. Não precisamos armazenar a estrutura da árvore na memória. Ela é definida implicitamente. Precisamos apenas de um array que contém as somas de todos os segmentos.

Como observado antes, precisamos armazenar no máximo  $4n$  vértices. Pode ser menos, mas por conveniência sempre alocamos um array de tamanho  $4n$ . Haverá alguns elementos no array de soma, que não corresponderão a nenhum vértice na árvore real, mas isso não complica a implementação.

Portanto, armazenamos a Árvore de Segmentos simplesmente como um array  
$t[]$  com um tamanho quatro vezes o tamanho da entrada  $n$ :
```cpp
int n, t[4*MAXN];
```

O procedimento para construir a Árvore de Segmentos a partir de um array dado  
$a[]$  é assim: é uma função recursiva com os parâmetros  $a[]$  (o array de entrada),  $v$  (o índice do vértice atual), e os limites  $tl$  e  $tr$  do segmento atual. No programa principal, esta função será chamada com os parâmetros do vértice raiz:  $v = 1$ ,  $tl = 0$ , e  $tr = n - 1$ .

```cpp
void build(int a[], int v, int tl, int tr) {
    if (tl == tr) {
        t[v] = a[tl];
    } else {
        int tm = (tl + tr) / 2;
        build(a, v*2, tl, tm);
        build(a, v*2+1, tm+1, tr);
        t[v] = t[v*2] + t[v*2+1];
    }
}
```

Além disso, a função para responder a consultas de soma também é uma função recursiva, que recebe como parâmetros informações sobre o vértice/segmento atual (ou seja, o índice  $v$  e os limites  $tl$  e  $tr$ ) e também as informações sobre os limites da consulta,  $l$  e  $r$ . Para simplificar o código, esta função sempre faz duas chamadas recursivas, mesmo que apenas uma seja necessária - nesse caso, a chamada recursiva supérflua terá  $l > r$ , e isso pode ser facilmente capturado usando uma verificação adicional no início da função.

```cpp
int sum(int v, int tl, int tr, int l, int r) {
    if (l > r) 
        return 0;
    if (l == tl && r == tr) {
        return t[v];
    }
    int tm = (tl + tr) / 2;
    return sum(v*2, tl, tm, l, min(r, tm))
           + sum(v*2+1, tm+1, tr, max(l, tm+1), r);
}
```
Finalmente a consulta de atualização. A função também receberá informações sobre o vértice/segmento atual, e adicionalmente também o parâmetro da consulta de atualização (ou seja, a posição do elemento e seu novo valor).
```cpp
void update(int v, int tl, int tr, int pos, int new_val) {
    if (tl == tr) {
        t[v] = new_val;
    } else {
        int tm = (tl + tr) / 2;
        if (pos <= tm)
            update(v*2, tl, tm, pos, new_val);
        else
            update(v*2+1, tm+1, tr, pos, new_val);
        t[v] = t[v*2] + t[v*2+1];
    }
}
```



### Implementação Eficiente em Memória
A maioria das pessoas usa a implementação da seção anterior. Se você olhar para o array t, verá que ele segue a numeração dos nós da árvore na ordem de uma travessia BFS (travessia em nível). Usando esta travessia, os filhos do vértice  $v$  são 
$2v$  e $2v + 1$  respectivamente. No entanto, se  $n$  não for uma potência de dois, este método pulará alguns índices e deixará algumas partes do array t não utilizadas. O consumo de memória é limitado por  $4n$ , mesmo que uma Árvore de Segmentos de um array de  $n$  elementos requer apenas  $2n - 1$  vértices.

No entanto, isso pode ser reduzido. Nós renumeramos os vértices da árvore na ordem de uma travessia de Euler (travessia em pré-ordem), e escrevemos todos esses vértices um ao lado do outro.

Vamos olhar para um vértice no índice  $v$ , e deixá-lo ser responsável pelo segmento  $[l, r]$ , e deixar  $mid = \dfrac{l + r}{2}$ . É óbvio que o filho à esquerda terá o índice  $v + 1$ . O filho à esquerda é responsável pelo segmento  $[l, mid]$ , ou seja, no total haverá 
$2 * (mid - l + 1) - 1$  vértices na subárvore do filho à esquerda. Assim, podemos calcular o índice do filho à direita de  $v$ . O índice será  $v + 2 * (mid - l + 1)$ . Com essa numeração, alcançamos uma redução da memória necessária para  $2n$ .





## Versões Avançadas de Árvores de Segmentos
Uma Árvore de Segmentos é uma estrutura de dados muito flexível e permite variações e extensões em muitas direções diferentes. Vamos tentar categorizá-las abaixo.
### Consultas mais complexas
Pode ser bastante fácil mudar a Árvore de Segmentos em uma direção, de forma que ela compute consultas diferentes (por exemplo, calcular o mínimo / máximo em vez da soma), mas também pode ser muito não trivial.

#### Encontrando o máximo
Vamos alterar ligeiramente a condição do problema descrito acima: em vez de consultar a soma, agora faremos consultas máximas.

A árvore terá exatamente a mesma estrutura que a árvore descrita acima. Só precisamos mudar a maneira como  $t[v]$  é calculado nas funções  $\text{build}$  e  $\text{update}$ .  $t[v]$  agora armazenará o máximo do segmento correspondente. E também precisamos mudar o cálculo do valor retornado da função  $\text{sum}$  (substituindo a soma pelo máximo).

Claro que este problema pode ser facilmente transformado em calcular o mínimo em vez do máximo.

Em vez de mostrar uma implementação para este problema, a implementação será dada para uma versão mais complexa deste problema na próxima seção.

#### Encontrando o máximo e o número de vezes que ele aparece
Esta tarefa é muito semelhante à anterior. Além de encontrar o máximo, também temos que encontrar o número de ocorrências do máximo.

Para resolver este problema, armazenamos um par de números em cada vértice na árvore: Além do máximo, também armazenamos o número de ocorrências dele no segmento correspondente. Determinar o par correto para armazenar em  $t[v]$  ainda pode ser feito em tempo constante usando as informações dos pares armazenados nos vértices filhos. Combinar dois desses pares deve ser feito em uma função separada, pois esta será uma operação que faremos ao construir a árvore, ao responder consultas máximas e ao realizar modificações.

```cpp
pair<int, int> t[4*MAXN];

pair<int, int> combine(pair<int, int> a, pair<int, int> b) {
    if (a.first > b.first) 
        return a;
    if (b.first > a.first)
        return b;
    return make_pair(a.first, a.second + b.second);
}

void build(int a[], int v, int tl, int tr) {
    if (tl == tr) {
        t[v] = make_pair(a[tl], 1);
    } else {
        int tm = (tl + tr) / 2;
        build(a, v*2, tl, tm);
        build(a, v*2+1, tm+1, tr);
        t[v] = combine(t[v*2], t[v*2+1]);
    }
}

pair<int, int> get_max(int v, int tl, int tr, int l, int r) {
    if (l > r)
        return make_pair(-INF, 0);
    if (l == tl && r == tr)
        return t[v];
    int tm = (tl + tr) / 2;
    return combine(get_max(v*2, tl, tm, l, min(r, tm)), 
                   get_max(v*2+1, tm+1, tr, max(l, tm+1), r));
}

void update(int v, int tl, int tr, int pos, int new_val) {
    if (tl == tr) {
        t[v] = make_pair(new_val, 1);
    } else {
        int tm = (tl + tr) / 2;
        if (pos <= tm)
            update(v*2, tl, tm, pos, new_val);
        else
            update(v*2+1, tm+1, tr, pos, new_val);
        t[v] = combine(t[v*2], t[v*2+1]);
    }
}
```
#### Calcular o maior divisor comum / mínimo múltiplo comum
Neste problema, queremos calcular o MDC / MMC de todos os números de intervalos dados do array.

Esta interessante variação da Árvore de Segmentos pode ser resolvida exatamente da mesma maneira que as Árvores de Segmentos que derivamos para consultas de soma / mínimo / máximo: basta armazenar o MDC / MMC do vértice correspondente em cada vértice da árvore. Combinar dois vértices pode ser feito calculando o MDC / MMC de ambos os vértices.

#### Contando o número de zeros, procurando pelo  $k$ -ésimo zero
Neste problema, desejamos encontrar o número de zeros em um intervalo dado e, adicionalmente, encontrar o índice do  $k$ -ésimo zero usando uma segunda função.

Novamente, precisamos ajustar um pouco os valores armazenados na árvore: desta vez, armazenaremos o número de zeros em cada segmento em  $t[]$ . É bastante claro como implementar as funções  $\text{build}$ ,  $\text{update}$  e <math xmlns="http://www.w3.org/1998/Math/MathML">
  <mtext>count_zero</mtext>
</math>; podemos simplesmente usar as ideias do problema de consulta de soma. Assim, resolvemos a primeira parte do problema.

Agora aprendemos como resolver o problema de encontrar o  $k$ -ésimo zero no array  $a[]$ . Para realizar essa tarefa, descemos na Árvore de Segmentos, começando no vértice raiz, e movendo-nos a cada vez para o filho esquerdo ou direito, dependendo de qual segmento contém o  $k$ -ésimo zero. Para decidir para qual filho precisamos ir, é suficiente olhar para o número de zeros que aparecem no segmento correspondente ao vértice esquerdo. Se esta contagem precomputada for maior ou igual a  $k$ , é necessário descer para o filho esquerdo; caso contrário, desça para o filho direito. Observe que, se escolhermos o filho direito, precisamos subtrair o número de zeros do filho esquerdo de  $k$ .

Na implementação, podemos lidar com o caso especial de  $a[]$  conter menos de  
$k$  zeros, retornando -1.

```cpp
int find_kth(int v, int tl, int tr, int k) {
    if (k > t[v])
        return -1;
    if (tl == tr)
        return tl;
    int tm = (tl + tr) / 2;
    if (t[v*2] >= k)
        return find_kth(v*2, tl, tm, k);
    else 
        return find_kth(v*2+1, tm+1, tr, k - t[v*2]);
}
```

#### Procurando por um prefixo de array com uma quantidade dada
A tarefa é a seguinte: para um valor dado  $x$ , precisamos encontrar rapidamente o menor índice  $i$  tal que a soma dos primeiros  $i$  elementos do array  $a[]$  seja maior ou igual a  $x$  (assumindo que o array  $a[]$  contém apenas valores não negativos).

Essa tarefa pode ser resolvida usando a busca binária, computando a soma dos prefixos com a Árvore de Segmentos. No entanto, isso levará a uma solução  
$O(\log^2 n)$ .

Em vez disso, podemos usar a mesma ideia da seção anterior e encontrar a posição descendo na árvore: movendo-nos a cada vez para a esquerda ou para a direita, dependendo da soma do filho esquerdo. Assim, encontramos a resposta em  
$O(\log n)$  tempo.

#### Procurando pelo primeiro elemento maior que uma quantidade dada
A tarefa é a seguinte: para um valor dado  $x$  e um intervalo  $a[l \dots r]$ , encontrar o menor  $i$  no intervalo  $a[l \dots r]$ , tal que  $a[i]$  seja maior que  $x$ .

Essa tarefa pode ser resolvida usando a busca binária sobre consultas de prefixo máximo com a Árvore de Segmentos. No entanto, isso levará a uma solução  $O(\log^2 n)$ .

Em vez disso, podemos usar a mesma ideia das seções anteriores e encontrar a posição descendo na árvore: movendo-nos a cada vez para a esquerda ou para a direita, dependendo do valor máximo do filho esquerdo. Assim, encontramos a resposta em  $O(\log n)$  tempo.

```cpp
int get_first(int v, int tl, int tr, int l, int r, int x) {
    if(tl > r || tr < l) return -1;
    if(t[v] <= x) return -1;

    if (tl== tr) return tl;

    int tm = tl + (tr-tl)/2;
    int left = get_first(2*v, tl, tm, l, r, x);
    if(left != -1) return left;
    return get_first(2*v+1, tm+1, tr, l ,r, x);
}
```

#### Encontrando subsegmentos com a soma máxima
Aqui novamente recebemos um intervalo  $a[l \dots r]$  para cada consulta, e desta vez precisamos encontrar um subsegmento  $a[l^\prime \dots r^\prime]$  tal que  $l \le l^\prime$  e  $r^\prime \le r$  e a soma dos elementos deste segmento seja máxima. Como antes, também queremos ser capazes de modificar elementos individuais do array. Os elementos do array podem ser negativos, e o subsegmento ótimo pode ser vazio (por exemplo, se todos os elementos forem negativos).

Este problema é um uso não trivial de uma Árvore de Segmentos. Desta vez, armazenaremos quatro valores para cada vértice: a soma do segmento, a soma máxima do prefixo, a soma máxima do sufixo e a soma do subsegmento máximo nele. Em outras palavras, para cada segmento da Árvore de Segmentos, a resposta já está precomputada, assim como as respostas para segmentos que tocam as fronteiras esquerda e direita do segmento.

Como construir uma árvore com esses dados? Novamente, a construímos de maneira recursiva: primeiro calculamos os quatro valores para o filho esquerdo e direito, e então os combinamos para obter os quatro valores para o vértice atual. Note que a resposta para o vértice atual é:

- a resposta do filho esquerdo, o que significa que o subsegmento ótimo está totalmente colocado no segmento do filho esquerdo,
- a resposta do filho direito, o que significa que o subsegmento ótimo está totalmente colocado no segmento do filho direito,
- a soma da soma máxima do sufixo do filho esquerdo e a soma máxima do prefixo do filho direito, o que significa que o subsegmento ótimo se intersecta com ambos os filhos.

Portanto, a resposta para o vértice atual é o máximo desses três valores. Calcular a soma máxima do prefixo/sufixo é ainda mais fácil. Aqui está a implementação da função  $\text{combine}$ , que recebe apenas dados do filho esquerdo e direito e retorna os dados do vértice atual.

```cpp
struct data {
    int sum, pref, suff, ans;
};

data combine(data l, data r) {
    data res;
    res.sum = l.sum + r.sum;
    res.pref = max(l.pref, l.sum + r.pref);
    res.suff = max(r.suff, r.sum + l.suff);
    res.ans = max(max(l.ans, r.ans), l.suff + r.pref);
    return res;
}
```

Usando a função  $\text{combine}$ , é fácil construir a Árvore de Segmentos. Podemos implementá-la exatamente da mesma maneira que nas implementações anteriores. Para inicializar os vértices folha, criamos a função auxiliar  <math xmlns="http://www.w3.org/1998/Math/MathML">
  <mtext>make_data</mtext>
</math> , que retornará um objeto  $\text{data}$  contendo as informações de um único valor.

```cpp
data make_data(int val) {
    data res;
    res.sum = val;
    res.pref = res.suff = res.ans = max(0, val);
    return res;
}

void build(int a[], int v, int tl, int tr) {
    if (tl == tr) {
        t[v] = make_data(a[tl]);
    } else {
        int tm = (tl + tr) / 2;
        build(a, v*2, tl, tm);
        build(a, v*2+1, tm+1, tr);
        t[v] = combine(t[v*2], t[v*2+1]);
    }
}

void update(int v, int tl, int tr, int pos, int new_val) {
    if (tl == tr) {
        t[v] = make_data(new_val);
    } else {
        int tm = (tl + tr) / 2;
        if (pos <= tm)
            update(v*2, tl, tm, pos, new_val);
        else
            update(v*2+1, tm+1, tr, pos, new_val);
        t[v] = combine(t[v*2], t[v*2+1]);
    }
}
```

Resta apenas saber como calcular a resposta para uma consulta. Para respondê-la, descemos na árvore como antes, dividindo a consulta em vários subsegmentos que coincidem com os segmentos da Árvore de Segmentos, e combinamos as respostas neles em uma única resposta para a consulta. Em seguida, deve ficar claro que o trabalho é exatamente o mesmo que na Árvore de Segmentos simples, mas em vez de somar/minimizar/maximizar os valores, usamos a função  $\text{combine}$ .

```cpp
data query(int v, int tl, int tr, int l, int r) {
    if (l > r) 
        return make_data(0);
    if (l == tl && r == tr) 
        return t[v];
    int tm = (tl + tr) / 2;
    return combine(query(v*2, tl, tm, l, min(r, tm)), 
                   query(v*2+1, tm+1, tr, max(l, tm+1), r));
}
```



### Salvando subconjuntos inteiros em cada vértice
Esta é uma subseção separada que se destaca das outras, porque em cada vértice da Árvore de Segmentos não armazenamos informações sobre o segmento correspondente em forma comprimida (soma, mínimo, máximo, ...), mas armazenamos todos os elementos do segmento. Assim, a raiz da Árvore de Segmentos armazenará todos os elementos do array, o vértice filho esquerdo armazenará a primeira metade do array, o vértice filho direito a segunda metade, e assim por diante.

Na aplicação mais simples dessa técnica, armazenamos os elementos em ordem ordenada. Em versões mais complexas, os elementos não são armazenados em listas, mas em estruturas de dados mais avançadas (conjuntos, mapas, ...). Mas todos esses métodos têm o fator comum de que cada vértice requer memória linear (ou seja, proporcional ao comprimento do segmento correspondente).

A primeira pergunta natural, ao considerar essas Árvores de Segmentos, é sobre o consumo de memória. Intuitivamente, isso pode parecer como  $O(n^2)$  de memória, mas acontece que a árvore completa precisará apenas de  $O(n \log n)$  de memória. Por quê? Muito simplesmente, porque cada elemento do array cai em  $O(\log n)$  segmentos (lembre-se de que a altura da árvore é  $O(\log n)$ ).

Assim, apesar da aparente extravagância de tal Árvore de Segmentos, ela consome apenas um pouco mais de memória do que a Árvore de Segmentos usual.

Abaixo estão descritas várias aplicações típicas dessa estrutura de dados. Vale ressaltar a semelhança dessas Árvores de Segmentos com estruturas de dados 2D (na verdade, esta é uma estrutura de dados 2D, mas com capacidades bastante limitadas).

#### Encontrar o menor número maior ou igual a um número especificado. Sem consultas de modificação.
Queremos responder a consultas da seguinte forma: para três números dados  $(l, r, x)$ , temos que encontrar o número mínimo no segmento  $a[l \dots r]$  que é maior ou igual a  $x$ .

Construímos uma Árvore de Segmentos. Em cada vértice, armazenamos uma lista ordenada de todos os números que ocorrem no segmento correspondente, como descrito acima. Como construir uma Árvore de Segmentos dessa forma da maneira mais eficaz possível? Como sempre, abordamos esse problema de forma recursiva: suponha que as listas dos filhos esquerdo e direito já tenham sido construídas, e queremos construir a lista para o vértice atual. Dessa perspectiva, a operação agora é trivial e pode ser realizada em tempo linear: só precisamos combinar as duas listas ordenadas em uma, o que pode ser feito iterando sobre elas usando dois ponteiros. A STL do C++ já tem uma implementação desse algoritmo.

Devido à estrutura da Árvore de Segmentos e às semelhanças com o algoritmo de ordenação merge sort, essa estrutura de dados é frequentemente chamada de "Merge Sort Tree".

```cpp
vector<int> t[4*MAXN];

void build(int a[], int v, int tl, int tr) {
    if (tl == tr) {
        t[v] = vector<int>(1, a[tl]);
    } else { 
        int tm = (tl + tr) / 2;
        build(a, v*2, tl, tm);
        build(a, v*2+1, tm+1, tr);
        merge(t[v*2].begin(), t[v*2].end(), t[v*2+1].begin(), t[v*2+1].end(),
              back_inserter(t[v]));
    }
}
```

Já sabemos que a Árvore de Segmentos construída dessa forma precisará de  $O(n \log n)$  de memória. E graças a essa implementação, sua construção também leva  $O(n \log n)$  de tempo, afinal, cada lista é construída em tempo linear em relação ao seu tamanho.

Agora considere a resposta à consulta. Desceremos na árvore, como na Árvore de Segmentos regular, dividindo nosso segmento  $a[l \dots r]$  em vários subsegmentos (no máximo  $O(\log n)$  partes). É claro que a resposta de toda a consulta é o mínimo de cada uma das subconsultas. Então agora só precisamos entender como responder a uma consulta em um desses subsegmentos que corresponde a algum vértice da árvore.

Estamos em algum vértice da Árvore de Segmentos e queremos calcular a resposta para a consulta, ou seja, encontrar o número mínimo maior ou igual a um dado número  $x$ . Como o vértice contém a lista de elementos em ordem ordenada, podemos simplesmente realizar uma busca binária nessa lista e retornar o primeiro número maior ou igual a  $x$ .

Assim, a resposta à consulta em um segmento da árvore leva  $O(\log n)$  de tempo, e a consulta inteira é processada em  $O(\log^2 n)$ .

```cpp
int query(int v, int tl, int tr, int l, int r, int x) {
    if (l > r)
        return INF;
    if (l == tl && r == tr) {
        vector<int>::iterator pos = lower_bound(t[v].begin(), t[v].end(), x);
        if (pos != t[v].end())
            return *pos;
        return INF;
    }
    int tm = (tl + tr) / 2;
    return min(query(v*2, tl, tm, l, min(r, tm), x), 
               query(v*2+1, tm+1, tr, max(l, tm+1), r, x));
}
```

A constante  $\text{INF}$  é igual a algum número grande que é maior do que todos os números no array. Seu uso significa que não há nenhum número maior ou igual a  $x$  no segmento. Isso tem o significado de "não há resposta no intervalo fornecido".

#### Encontrar o menor número maior ou igual a um número especificado. Com consultas de modificação.
Esta tarefa é semelhante à anterior. A última abordagem tem uma desvantagem, não era possível modificar o array entre as respostas das consultas. Agora queremos fazer exatamente isso: uma consulta de modificação realizará a atribuição  $a[i] = y$ .

A solução é semelhante à solução do problema anterior, mas em vez de listas em cada vértice da Árvore de Segmentos, armazenaremos uma lista equilibrada que permite procurar rapidamente números, excluir números e inserir novos números. Como o array pode conter um número repetido, a escolha ideal é a estrutura de dados  $\text{multiset}$ .

A construção de uma Árvore de Segmentos desse tipo é feita de maneira bastante semelhante à do problema anterior, apenas agora precisamos combinar  $\text{multiset}$ s e não listas ordenadas. Isso leva a um tempo de construção de  $O(n \log^2 n)$  (em geral, mesclar duas árvores vermelho-negras pode ser feito em tempo linear, mas a STL do C++ não garante essa complexidade de tempo).

A função  $\text{query}$  também é praticamente equivalente, apenas agora a função  <math xmlns="http://www.w3.org/1998/Math/MathML">
  <mtext>lower_bound</mtext>
</math>  do  $\text{multiset}$  deve ser chamada ( <math xmlns="http://www.w3.org/1998/Math/MathML">
  <mtext>std::lower_bound</mtext>
</math>  só funciona em  $O(\log n)$  de tempo se usado com iteradores de acesso aleatório).

Finalmente, a solicitação de modificação. Para processá-la, devemos percorrer a árvore e modificar todos os  $\text{multiset}$  dos segmentos correspondentes que contêm o elemento afetado. Simplesmente excluímos o valor antigo desse elemento (mas apenas uma ocorrência) e inserimos o novo valor.

```cpp
void update(int v, int tl, int tr, int pos, int new_val) {
    t[v].erase(t[v].find(a[pos]));
    t[v].insert(new_val);
    if (tl != tr) {
        int tm = (tl + tr) / 2;
        if (pos <= tm)
            update(v*2, tl, tm, pos, new_val);
        else
            update(v*2+1, tm+1, tr, pos, new_val);
    } else {
        a[pos] = new_val;
    }
}
```

O processamento dessa consulta de modificação também leva  $O(\log^2 n)$  de tempo.

#### Encontrar o menor número maior ou igual a um número especificado. Aceleração com "fractional cascading".
Temos a mesma descrição do problema; queremos encontrar o número mínimo maior ou igual a  
$x$  em um segmento, mas desta vez em  $O(\log n)$  tempo. Vamos melhorar a complexidade de tempo usando a técnica "fractional cascading".

Fractional cascading é uma técnica simples que permite melhorar o tempo de execução de várias buscas binárias conduzidas ao mesmo tempo. Nossa abordagem anterior para a consulta de pesquisa foi dividir a tarefa em várias subtarefas, cada uma das quais é resolvida com uma busca binária. Fractional cascading permite substituir todas essas buscas binárias por apenas uma.

O exemplo mais simples e óbvio de fractional cascading é o seguinte problema: existem  $k$  listas ordenadas de números, e devemos encontrar em cada lista o primeiro número maior ou igual ao número dado.

Em vez de realizar uma busca binária para cada lista, poderíamos mesclar todas as listas em uma única lista grande ordenada. Além disso, para cada elemento  $y$ , armazenamos uma lista de resultados da busca por  $y$  em cada uma das  $k$  listas. Portanto, se quisermos encontrar o menor número maior ou igual a  $x$ , precisamos realizar apenas uma única busca binária, e a partir da lista de índices, podemos determinar o menor número em cada lista. No entanto, essa abordagem requer  
$O(n \cdot k)$  de tempo ( $n$  é o comprimento das listas combinadas), o que pode ser bastante ineficiente.

Fractional cascading reduz essa complexidade de memória para  $O(n)$  de memória, criando a partir das  $k$  listas de entrada  $k$  novas listas, em que cada lista contém a lista correspondente e, adicionalmente, cada segundo elemento da lista seguinte. Usando essa estrutura, só é necessário armazenar dois índices, o índice do elemento na lista original e o índice do elemento na lista seguinte. Assim, essa abordagem usa apenas  $O(n)$  de memória e ainda pode responder às consultas usando uma única busca binária.

Mas para nossa aplicação, não precisamos da potência total do fractional cascading. Em nossa Árvore de Segmentos, um vértice conterá a lista ordenada de todos os elementos que ocorrem nos subconjuntos à esquerda ou à direita (como na Árvore de Classificação por Mergulho). Além dessa lista ordenada, armazenamos duas posições para cada elemento. Para um elemento  
$y$ , armazenamos o menor índice  $i$ , tal que o  $i$ -ésimo elemento na lista ordenada do subconjunto à esquerda é maior ou igual a  $y$ . E armazenamos o menor índice  $j$ , tal que o  $j$ -ésimo elemento na lista ordenada do subconjunto à direita é maior ou igual a  $y$ . Esses valores podem ser calculados em paralelo à etapa de mesclagem quando construímos a árvore.

Como isso acelera as consultas?

Lembre-se, na solução normal fizemos uma busca binária em cada nó. Mas com essa modificação, podemos evitar todas, exceto uma.

Para responder a uma consulta, simplesmente fazemos uma busca binária no nó raiz. Isso nos dá o menor elemento  $y \ge x$  no array completo, mas também nos dá duas posições. O índice do menor elemento maior ou igual a  $x$  no subconjunto à esquerda e o índice do menor elemento  
$y$  no subconjunto à direita. Observe que  $\ge y$  é o mesmo que  $\ge x$ , já que nosso array não contém nenhum elemento entre  $x$  e  $y$ . Na solução normal da Árvore de Classificação por Mergulho, calcularíamos esses índices por meio de busca binária,

 mas com a ajuda dos valores pré-computados, podemos simplesmente consultá-los em  
$O(1)$ . E podemos repetir isso até visitarmos todos os nós que cobrem nosso intervalo de consulta.

Para resumir, como de costume, tocamos  $O(\log n)$  nós durante uma consulta. No nó raiz, fazemos uma busca binária e, em todos os outros nós, fazemos apenas trabalho constante. Isso significa que a complexidade para responder a uma consulta é  $O(\log n)$ .

Mas observe que isso usa três vezes mais memória do que uma Árvore de Classificação por Mergulho normal, que já usa muita memória ( $O(n \log n)$ ).

É direto aplicar essa técnica a um problema que não requer consultas de modificação. As duas posições são apenas inteiros e podem ser facilmente calculadas contando ao mesclar as duas sequências ordenadas.

Ainda é possível permitir consultas de modificação, mas isso complica todo o código. Em vez de inteiros, você precisa armazenar o array ordenado como multiconjunto, e em vez de índices, precisa armazenar iteradores. E você precisa trabalhar com muito cuidado para incrementar ou decrementar os iteradores corretos durante uma consulta de modificação.

#### Outras variações possíveis
Essa técnica implica em uma nova classe inteira de aplicações possíveis. Em vez de armazenar um  
$\text{vector}$  ou um  $\text{multiset}$  em cada vértice, podem ser usadas outras estruturas de dados: outras Árvores de Segmentos (um pouco discutidas em Generalização para dimensões superiores), Árvores de Fenwick, Árvores Cartesianas, etc.

### **Range updates (Lazy Propagation)**

Todos os problemas nas seções anteriores discutiram consultas de modificação que afetavam apenas um único elemento do array cada vez. No entanto, a Árvore de Segmentos permite a aplicação de consultas de modificação a um segmento inteiro de elementos contíguos e realizar a consulta no mesmo tempo   $O(\log n)$ .

#### **Adição em segmentos**

Começamos considerando problemas da forma mais simples: a consulta de modificação deve adicionar um número   $x$  a todos os números no segmento   $a[l \dots r]$ . A segunda consulta, que se espera responder, pede simplesmente o valor de   $a[i]$ .

Para tornar a consulta de adição eficiente, armazenamos em cada vértice na Árvore de Segmentos a quantidade que devemos adicionar a todos os números no segmento correspondente. Por exemplo, se vier a consulta "adicionar 3 a todo o array   $a[0 \dots n-1]$ ", então colocamos o número 3 na raiz da árvore. Em geral, temos que colocar esse número em vários segmentos, que formam uma partição do segmento da consulta. Assim, não precisamos alterar todos os   $O(n)$  valores, mas apenas   $O(\log n)$  deles.

Se agora vier uma consulta que pergunta pelo valor atual de uma entrada específica do array, é suficiente percorrer a árvore e somar todos os valores encontrados ao longo do caminho.

```cpp
void build(int a[], int v, int tl, int tr) {
    if (tl == tr) {
        t[v] = a[tl];
    } else {
        int tm = (tl + tr) / 2;
        build(a, v*2, tl, tm);
        build(a, v*2+1, tm+1, tr);
        t[v] = 0;
    }
}

void update(int v, int tl, int tr, int l, int r, int add) {
    if (l > r)
        return;
    if (l == tl && r == tr) {
        t[v] += add;
    } else {
        int tm = (tl + tr) / 2;
        update(v*2, tl, tm, l, min(r, tm), add);
        update(v*2+1, tm+1, tr, max(l, tm+1), r, add);
    }
}

int get(int v, int tl, int tr, int pos) {
    if (tl == tr)
        return t[v];
    int tm = (tl + tr) / 2;
    if (pos <= tm)
        return t[v] + get(v*2, tl, tm, pos);
    else
        return t[v] + get(v*2+1, tm+1, tr, pos);
}
```

#### **Atribuição em segmentos**

Suponha agora que a consulta de modificação peça para atribuir a cada elemento de um determinado segmento   $a[l \dots r]$  um valor específico   $p$ . Como segunda consulta, vamos considerar novamente a leitura do valor do array   $a[i]$ .

Para realizar essa consulta de modificação em um segmento inteiro, é necessário armazenar em cada vértice da Árvore de Segmentos se o segmento correspondente é coberto inteiramente pelo mesmo valor ou não. Isso nos permite fazer uma atualização "preguiçosa": em vez de alterar todos os segmentos na árvore que cobrem o segmento da consulta, alteramos apenas alguns e deixamos outros inalterados. Um vértice marcado significará que todos os elementos do segmento correspondente são atribuídos a esse valor e, na verdade, a subárvore completa também deve conter apenas esse valor. Em certo sentido, somos preguiçosos e adiamos a escrita do novo valor para todos esses vértices. Podemos fazer essa tarefa tediosa mais tarde, se for necessário.

Assim, após a execução da consulta de modificação, algumas partes da árvore se tornam irrelevantes - algumas modificações permanecem não cumpridas nela.

Por exemplo, se uma consulta de modificação "atribuir um número ao array inteiro   $a[0 \dots n-1]$ " for executada, na Árvore de Segmentos apenas uma única mudança é feita - o número é colocado na raiz da árvore e este vértice é marcado. Os segmentos restantes permanecem inalterados, embora na verdade o número deveria ser colocado em toda a árvore.

Suponha agora que a segunda consulta de modificação diz que a primeira metade do array   $a[0 \dots n/2]$  deve ser atribuída com algum outro número. Para processar esta consulta, devemos atribuir a cada elemento do subconjunto à esquerda da raiz com esse número. Mas antes de fazermos isso, devemos primeiro resolver o vértice da raiz. A sutileza aqui é que a met

ade direita do array ainda deve ser atribuída ao valor da primeira consulta, e no momento não há informação armazenada para a metade direita.

A maneira de resolver isso é empurrar a informação da raiz para seus filhos, ou seja, se a raiz da árvore foi atribuída a algum número, atribuímos os vértices filhos esquerdo e direito com este número e removemos a marca da raiz. Depois disso, podemos atribuir ao filho esquerdo o novo valor, sem perder nenhuma informação necessária.

Resumindo, obtemos: para qualquer consulta (uma consulta de modificação ou leitura) durante a descida ao longo da árvore, devemos sempre empurrar informações do vértice atual para ambos os seus filhos. Podemos entender isso de tal forma que, ao descermos pela árvore, aplicamos modificações atrasadas, mas exatamente o necessário (para não degradar a complexidade para   $O(\log n)$ ).

Para a implementação, precisamos fazer uma função   $\text{push}$ , que receberá o vértice atual, e empurrará as informações para ambos os seus filhos. Chamaremos essa função no início das funções de consulta (mas não a chamaremos das folhas, porque não há necessidade de empurrar informações delas mais adiante).

```cpp
void push(int v) {
    if (marked[v]) {
        t[v*2] = t[v*2+1] = t[v];
        marked[v*2] = marked[v*2+1] = true;
        marked[v] = false;
    }
}

void update(int v, int tl, int tr, int l, int r, int new_val) {
    if (l > r) 
        return;
    if (l == tl && tr == r) {
        t[v] = new_val;
        marked[v] = true;
    } else {
        push(v);
        int tm = (tl + tr) / 2;
        update(v*2, tl, tm, l, min(r, tm), new_val);
        update(v*2+1, tm+1, tr, max(l, tm+1), r, new_val);
    }
}

int get(int v, int tl, int tr, int pos) {
    if (tl == tr) {
        return t[v];
    }
    push(v);
    int tm = (tl + tr) / 2;
    if (pos <= tm) 
        return get(v*2, tl, tm, pos);
    else
        return get(v*2+1, tm+1, tr, pos);
}
```

**Observação:** A função   $\text{get}$  também pode ser implementada de maneira diferente: não realizar atualizações atrasadas, mas retornar imediatamente o valor   $t[v]$  se   $marked[v]$  for verdadeiro.

#### **Adição em segmentos, consulta para máximo**

Agora, a consulta de modificação é adicionar um número a todos os elementos em um intervalo, e a consulta de leitura é encontrar o máximo em um intervalo.

Portanto, para cada vértice da Árvore de Segmentos, devemos armazenar o máximo do subintervalo correspondente. A parte interessante é como recalcular esses valores durante uma consulta de modificação.

Para este propósito, mantemos armazenado um valor adicional para cada vértice. Neste valor, armazenamos os incrementos que não propagamos para os vértices filhos. Antes de ir para um vértice filho, chamamos   $\text{push}$  e propagamos o valor para ambos os filhos. Temos que fazer isso tanto na função   $\text{update}$  quanto na função   $\text{query}$ .

```cpp
void build(int a[], int v, int tl, int tr) {
    if (tl == tr) {
        t[v] = a[tl];
    } else {
        int tm = (tl + tr) / 2;
        build(a, v*2, tl, tm);
        build(a, v*2+1, tm+1, tr);
        t[v] = max(t[v*2], t[v*2 + 1]);
    }
}

void push(int v) {
    t[v*2] += lazy[v];
    lazy[v*2] += lazy[v];
    t[v*2+1] += lazy[v];
    lazy[v*2+1] += lazy[v];
    lazy[v] = 0;
}

void update(int v, int tl,

 int tr, int l, int r, int addend) {
    if (l > r) 
        return;
    if (l == tl && tr == r) {
        t[v] += addend;
        lazy[v] += addend;
    } else {
        push(v);
        int tm = (tl + tr) / 2;
        update(v*2, tl, tm, l, min(r, tm), addend);
        update(v*2+1, tm+1, tr, max(l, tm+1), r, addend);
        t[v] = max(t[v*2], t[v*2+1]);
    }
}

int query(int v, int tl, int tr, int l, int r) {
    if (l > r)
        return -INF;
    if (l == tl && tr == r)
        return t[v];
    push(v);
    int tm = (tl + tr) / 2;
    return max(query(v*2, tl, tm, l, min(r, tm)), 
               query(v*2+1, tm+1, tr, max(l, tm+1), r));
}
```

### Generalização para Dimensões Superiores

Uma Árvore de Segmentos pode ser generalizada de maneira bastante natural para dimensões superiores. Se no caso unidimensional dividimos os índices do array em segmentos, então no caso bidimensional construímos uma Árvore de Segmentos comum com relação aos primeiros índices, e para cada segmento, construímos uma Árvore de Segmentos comum com relação aos segundos índices.

#### Árvore de Segmentos 2D Simples

É fornecida uma matriz $a[0 \dots n-1, 0 \dots m-1]$, e precisamos encontrar a soma (ou mínimo/máximo) em alguma submatriz $a[x_1 \dots x_2, y_1 \dots y_2]$, além de realizar modificações nos elementos individuais da matriz (ou seja, consultas da forma $a[x][y] = p$).

Assim, construímos uma Árvore de Segmentos 2D: primeiro a Árvore de Segmentos usando a primeira coordenada $(x)$, depois a segunda $(y)$.

Para tornar o processo de construção mais compreensível, podemos esquecer por um momento que a matriz é bidimensional e considerar apenas a primeira coordenada. Construiremos uma Árvore de Segmentos unidimensional usando apenas a primeira coordenada. Mas, em vez de armazenar um número em um segmento, armazenamos uma Árvore de Segmentos inteira: ou seja, neste momento, lembramos que também temos uma segunda coordenada; mas, como neste momento a primeira coordenada já está fixa em algum intervalo $[l \dots r]$, efetivamente trabalhamos com uma faixa $a[l \dots r, 0 \dots m-1]$ e construímos uma Árvore de Segmentos para ela.

Aqui está a implementação da construção de uma Árvore de Segmentos 2D. Representa na verdade dois blocos separados: a construção de uma Árvore de Segmentos ao longo da coordenada $x$ <math xmlns="http://www.w3.org/1998/Math/MathML">
  <msub>
    <mtext>build</mtext>
    <mi>x</mi>
  </msub>
</math>, e a coordenada $y$ (\(\text{build}_y\)). Para os nós folha em \(\text{build}_y\), temos que separar dois casos: quando o segmento atual da primeira coordenada \([tlx \dots trx]\) tem comprimento 1, e quando tem um comprimento maior que um. No primeiro caso, simplesmente pegamos o valor correspondente da matriz, e no segundo caso podemos combinar os valores de duas Árvores de Segmentos dos filhos esquerdo e direito na coordenada \(x\).

```cpp
void build_y(int vx, int lx, int rx, int vy, int ly, int ry) {
    if (ly == ry) {
        if (lx == rx)
            t[vx][vy] = a[lx][ly];
        else
            t[vx][vy] = t[vx*2][vy] + t[vx*2+1][vy];
    } else {
        int my = (ly + ry) / 2;
        build_y(vx, lx, rx, vy*2, ly, my);
        build_y(vx, lx, rx, vy*2+1, my+1, ry);
        t[vx][vy] = t[vx][vy*2] + t[vx][vy*2+1];
    }
}

void build_x(int vx, int lx, int rx) {
    if (lx != rx) {
        int mx = (lx + rx) / 2;
        build_x(vx*2, lx, mx);
        build_x(vx*2+1, mx+1, rx);
    }
    build_y(vx, lx, rx, 1, 0, m-1);
}
```

Essa Árvore de Segmentos ainda utiliza uma quantidade linear de memória, mas com uma constante maior: \(16nm\). É claro que o procedimento descrito em \(\text{build}_x\) também funciona em tempo linear.

Agora, passamos para o processamento de consultas. Responderemos à consulta bidimensional usando o mesmo princípio: primeiro dividir a consulta na primeira coordenada e, para cada vértice alcançado, chamar a Árvore de Segmentos correspondente da segunda coordenada.

```cpp
int sum_y(int vx, int vy, int tly, int try_, int ly, int ry) {
    if (ly > ry) 
        return 0;
    if (ly == tly && try_ == ry)
        return t[vx][vy];
    int tmy = (tly + try_) / 2;
    return sum_y(vx, vy*2, tly, tmy, ly, min(ry, tmy))
         + sum_y(vx, vy*2+1, tmy+1, try_, max(ly, tmy+1), ry);
}

int sum_x(int vx, int tlx, int trx, int lx, int rx, int ly, int ry) {
    if (lx > rx)
        return 0;
    if (lx == tlx && trx == rx)
        return sum_y(vx, 1, 0, m-1, ly, ry);
    int tmx = (tlx + trx) / 2;
    return sum_x(vx*2, tlx, tmx, lx, min(rx, tmx), ly, ry)
         + sum_x(vx*2+1, tmx+1, trx,

 max(lx, tmx+1), rx, ly, ry);
}
```

Esta função funciona em \(O(\log n \log m)\) tempo, pois primeiro desce a árvore na primeira coordenada e, para cada vértice percorrido na árvore, faz uma consulta na Árvore de Segmentos correspondente na segunda coordenada.

Finalmente, consideramos a consulta de modificação. Queremos aprender como modificar a Árvore de Segmentos de acordo com a alteração no valor de algum elemento \(a[x][y] = p\). É claro que as alterações ocorrerão apenas nos vértices da primeira Árvore de Segmentos que cobrem a coordenada \(x\) (e tais serão \(O(\log n)\)), e para as Árvores de Segmentos correspondentes a elas, as alterações ocorrerão apenas nos vértices que cobrem a coordenada \(y\) (e tais serão \(O(\log m)\)). Portanto, a implementação não será muito diferente do caso unidimensional, apenas agora descemos primeiro na primeira coordenada e, em seguida, na segunda.

```cpp
void update_y(int vx, int lx, int rx, int vy, int ly, int ry, int x, int y, int new_val) {
    if (ly == ry) {
        if (lx == rx)
            t[vx][vy] = new_val;
        else
            t[vx][vy] = t[vx*2][vy] + t[vx*2+1][vy];
    } else {
        int my = (ly + ry) / 2;
        if (y <= my)
            update_y(vx, lx, rx, vy*2, ly, my, x, y, new_val);
        else
            update_y(vx, lx, rx, vy*2+1, my+1, ry, x, y, new_val);
        t[vx][vy] = t[vx][vy*2] + t[vx][vy*2+1];
    }
}

void update_x(int vx, int lx, int rx, int x, int y, int new_val) {
    if (lx != rx) {
        int mx = (lx + rx) / 2;
        if (x <= mx)
            update_x(vx*2, lx, mx, x, y, new_val);
        else
            update_x(vx*2+1, mx+1, rx, x, y, new_val);
    }
    update_y(vx, lx, rx, 1, 0, m-1, x, y, new_val);
}
```