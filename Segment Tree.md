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

