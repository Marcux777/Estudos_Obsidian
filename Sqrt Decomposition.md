# Decomposição Sqrt
A Decomposição Sqrt é um método (ou uma estrutura de dados) que permite realizar algumas operações comuns (encontrar a soma dos elementos do sub-array, encontrar o elemento mínimo/máximo, etc.) em  $O(\sqrt n)$  operações, o que é muito mais rápido do que  $O(n)$  para o algoritmo trivial.

Primeiro descrevemos a estrutura de dados para uma das aplicações mais simples dessa ideia, depois mostramos como generalizá-la para resolver alguns outros problemas, e finalmente olhamos para um uso um pouco diferente dessa ideia: dividir as solicitações de entrada em blocos sqrt.

## Estrutura de dados baseada em decomposição sqrt
Dado um array  $a[0 \dots n-1]$ , implemente uma estrutura de dados que permita encontrar a soma dos elementos  $a[l \dots r]$  para  $l$  e  $r$  arbitrários em  
$O(\sqrt n)$  operações.

### Descrição
A ideia básica da decomposição sqrt é o pré-processamento. Vamos dividir o array  
$a$  em blocos de comprimento aproximadamente  $\sqrt n$ , e para cada bloco  $i$  vamos pré-calcular a soma dos elementos nele  $b[i]$ .

Podemos supor que tanto o tamanho do bloco quanto o número de blocos são iguais a  
$\sqrt n$  arredondado para cima:

$$ s = \lceil \sqrt n \rceil $$ 
Então o array  $a$  é dividido em blocos da seguinte maneira:
 
$$ \underbrace{a[0], a[1], \dots, a[s-1]}_{\text{b[0]}}, \underbrace{a[s], \dots, a[2s-1]}_{\text{b[1]}}, \dots, \underbrace{a[(s-1) \cdot s], \dots, a[n-1]}_{\text{b[s-1]}} $$ 
O último bloco pode ter menos elementos do que os outros (se $n$  não for múltiplo de  
$s$ ), isso não é importante para a discussão (pois pode ser facilmente tratado). Assim, para cada bloco  
$k$ , sabemos a soma dos elementos nele  $b[k]$ :
$$ b[k] = \sum\limits_{i=k\cdot s}^{\min {(n-1,(k+1)\cdot s - 1})} a[i] $$ 
Então, calculamos os valores de  $b[k]$  (isso exigiu  $O(n)$  operações). Como eles podem nos ajudar a responder a cada consulta  $[l, r]$  ? Observe que se o intervalo  $[l, r]$  for longo o suficiente, ele conterá vários blocos inteiros, e para esses blocos podemos encontrar a soma dos elementos neles em uma única operação. Como resultado, o intervalo  $[l, r]$  conterá partes de apenas dois blocos, e teremos que calcular a soma dos elementos nessas partes de maneira trivial.

Assim, para calcular a soma dos elementos no intervalo  $[l, r]$ , só precisamos somar os elementos das duas "caudas":  $[l\dots (k + 1)\cdot s-1]$  e  $[p\cdot s\dots r]$  , e somar os valores  $b[i]$  em todos os blocos de  $k + 1$  a  $p-1$ :

$$ \sum\limits_{i=l}^r a[i] = \sum\limits_{i=l}^{(k+1) \cdot s-1} a[i] + \sum\limits_{i=k+1}^{p-1} b[i] + \sum\limits_{i=p\cdot s}^r a[i] $$ 
Nota: Quando  $k = p$ , ou seja,  $l$  e  $r$  pertencem ao mesmo bloco, a fórmula não pode ser aplicada, e a soma deve ser calculada de maneira trivial.

Esta abordagem nos permite reduzir significativamente o número de operações. De fato, o tamanho de cada "cauda" não excede o comprimento do bloco  $s$ , e o número de blocos na soma não excede  
$s$ . Como escolhemos  $s \approx \sqrt n$ , o número total de operações necessárias para encontrar a soma dos elementos no intervalo  $[l, r]$  é  $O(\sqrt n)$ .

Implementação¶
Vamos começar com a implementação mais simples:

```cpp
// dados de entrada
int n;
vector<int> a (n);

// pré-processamento
int len = (int) sqrt (n + .0) + 1; // tamanho do bloco e número de blocos
vector<int> b (len);
for (int i=0; i<n; ++i)
    b[i / len] += a[i];

// respondendo as consultas
for (;;) {
    int l, r;
  // ler dados de entrada para a próxima consulta
    int sum = 0;
    for (int i=l; i<=r; )
        if (i % len == 0 && i + len - 1 <= r) {
            // se o bloco inteiro começando em i pertence a [l, r]
            sum += b[i / len];
            i += len;
        }
        else {
            sum += a[i];
            ++i;
        }
}
```
Esta implementação tem um número irracionalmente grande de operações de divisão (que são muito mais lentas do que outras operações aritméticas). Em vez disso, podemos calcular os índices dos blocos  
$c_l$  e  
$c_r$  que contêm índices  
$l$  e  
$r$ , e percorrer os blocos  
$c_l+1 \dots c_r-1$  com processamento separado das "caudas" nos blocos  
$c_l$  e  
$c_r$ . Esta abordagem corresponde à última fórmula na descrição, e faz do caso  
$c_l = c_r$  um caso especial.

```cpp
int sum = 0;
int c_l = l / len,   c_r = r / len;
if (c_l == c_r)
    for (int i=l; i<=r; ++i)
        sum += a[i];
else {
    for (int i=l, end=(c_l+1)*len-1; i<=end; ++i)
        sum += a[i];
    for (int i=c_l+1; i<=c_r-1; ++i)
        sum += b[i];
    for (int i=c_r*len; i<=r; ++i)
        sum += a[i];
}
```
Outros problemas¶
Até agora estávamos discutindo o problema de encontrar a soma dos elementos de um subarray contínuo. Este problema pode ser estendido para permitir atualizar elementos individuais do array. Se um elemento  
$a[i]$  muda, é suficiente atualizar o valor de  
$b[k]$  para o bloco ao qual este elemento pertence ( 
$k = i / s$ ) em uma operação:

 
$$ b[k] += a_{new}[i] - a_{old}[i] $$ 
Por outro lado, a tarefa de encontrar a soma dos elementos pode ser substituída pela tarefa de encontrar o elemento mínimo/máximo de um subarray. Se este problema tiver que lidar também com atualizações de elementos individuais, a atualização do valor de  
$b[k]$  também é possível, mas exigirá a iteração através de todos os valores do bloco  
$k$  em  
$O(s) = O(\sqrt{n})$  operações.

A decomposição sqrt pode ser aplicada de maneira semelhante a uma classe inteira de outros problemas: encontrar o número de elementos zero, encontrar o primeiro elemento não zero, contar elementos que satisfazem uma determinada propriedade, etc.

Outra classe de problemas aparece quando precisamos atualizar elementos do array em intervalos: incrementar elementos existentes ou substituí-los por um valor dado.

Por exemplo, digamos que podemos fazer dois tipos de operações em um array: adicionar um valor dado  
$\delta$  a todos os elementos do array no intervalo  
$[l, r]$  ou consultar o valor do elemento  
$a[i]$ . Vamos armazenar o valor que tem que ser adicionado a todos os elementos do bloco  
$k$  em  
$b[k]$  (inicialmente todos  
$b[k] = 0$ ). Durante cada operação de "adição" precisamos adicionar  
$\delta$  a  
$b[k]$  para todos os blocos que pertencem ao intervalo  
$[l, r]$  e adicionar  
$\delta$  a  
$a[i]$  para todos os elementos que pertencem às "caudas" do intervalo. A resposta à consulta  
$i$  é simplesmente  
$a[i] + b[i/s]$ . Desta forma, a operação de "adição" tem complexidade  
$O(\sqrt{n})$ , e responder a uma consulta tem complexidade  
$O(1)$ .

Finalmente, essas duas classes de problemas podem ser combinadas se a tarefa exigir fazer atualizações de elementos em um intervalo e consultas em um intervalo. Ambas as operações podem ser feitas com complexidade  
$O(\sqrt{n})$ . Isso exigirá dois arrays de blocos  
$b$  e  
$c$ : um para acompanhar as atualizações de elementos e outro para acompanhar as respostas à consulta.

Existem outros problemas que podem ser resolvidos usando decomposição sqrt, por exemplo, um problema sobre manter um conjunto de números que permitiria adicionar/excluir números, verificar se um número pertence ao conjunto e encontrar o  
$k$ -ésimo maior número. Para resolver isso, é preciso armazenar números em ordem crescente, divididos em vários blocos com  
$\sqrt{n}$  números em cada. Toda vez que um número é adicionado/