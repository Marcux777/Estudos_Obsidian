## Tabela Esparsa
A Tabela Esparsa é uma estrutura de dados que permite responder consultas de intervalos. Ela pode responder à maioria das consultas de intervalos em  
$O(\log n)$ , mas seu verdadeiro poder está em responder consultas de mínimo de intervalo (ou consultas máximas de intervalo equivalentes). Para essas consultas, ela pode calcular a resposta em  
$O(1)$ .

A única desvantagem dessa estrutura de dados é que ela só pode ser usada em arrays imutáveis. Isso significa que o array não pode ser alterado entre duas consultas. Se qualquer elemento no array mudar, a estrutura de dados completa terá que ser recalculada.

### Intuição
Qualquer número não negativo pode ser representado de forma única como uma soma de potências decrescentes de dois. Isso é apenas uma variante da representação binária de um número. Por exemplo,  $13 = (1101)_2 = 8 + 4 + 1$ . Para um número  $x$ , pode haver no máximo  $\lceil \log_2 x \rceil$  parcelas.

Pelo mesmo raciocínio, qualquer intervalo pode ser representado de forma única como uma união de intervalos com comprimentos que são potências decrescentes de dois. Por exemplo,  $[2, 14] = [2, 9] \cup [10, 13] \cup [14, 14]$ , onde o intervalo completo tem comprimento 13, e os intervalos individuais têm os comprimentos 8, 4 e 1, respectivamente. E também aqui a união consiste em no máximo  $\lceil \log_2(\text{comprimento do intervalo}) \rceil$  muitos intervalos.

A ideia principal por trás das Tabelas Esparsas é pré-calcular todas as respostas para consultas de intervalo com comprimento de potência de dois. Depois, uma consulta de intervalo diferente pode ser respondida dividindo o intervalo em intervalos com comprimentos de potência de dois, procurando as respostas pré-calculadas e combinando-as para receber uma resposta completa.

### Pré-computação
Usaremos um array bidimensional para armazenar as respostas para as consultas pré-computadas.  $\text{st}[i][j]$  armazenará a resposta para o intervalo  $[j, j + 2^i - 1]$  de comprimento  $2^i$ . O tamanho do array bidimensional será  $(K + 1) \times \text{MAXN}$ , onde  $\text{MAXN}$  é o maior comprimento possível do array.  
$\text{K}$  deve satisfazer  $\text{K} \ge \lfloor \log_2 \text{MAXN} \rfloor$ , porque  $2^{\lfloor \log_2 \text{MAXN} \rfloor}$  é o maior intervalo de potência de dois que temos que suportar. Para arrays com comprimento razoável ( $\le 10^7$  elementos),  $K = 25$  é um bom valor.

A dimensão  $\text{MAXN}$  é a segunda para permitir acessos consecutivos à memória (amigáveis ao cache).

```c++
int st[K + 1][MAXN];
```
Como o intervalo  $[j, j + 2^i - 1]$  de comprimento  $2^i$  se divide bem nos intervalos  $[j, j + 2^{i - 1} - 1]$  e  $[j + 2^{i - 1}, j + 2^i - 1]$ , ambos de comprimento  $2^{i - 1}$ , podemos gerar a tabela de forma eficiente usando programação dinâmica:

```c++
std::copy(array.begin(), array.end(), st[0]);

for (int i = 1; i <= K; i++)
    for (int j = 0; j + (1 << i) <= N; j++)
        st[i][j] = f(st[i - 1][j], st[i - 1][j + (1 << (i - 1))]);
```
A função  $f$  dependerá do tipo de consulta. Para consultas de soma de intervalo, ela calculará a soma, para consultas de mínimo de intervalo, ela calculará o mínimo.

A complexidade de tempo da pré-computação é  $O(\text{N} \log \text{N})$ .

### Consultas de Soma de Intervalo
Para este tipo de consultas, queremos encontrar a soma de todos os valores em um intervalo. Portanto, a definição natural da função  $f$  é  $f(x, y) = x + y$ . Podemos construir a estrutura de dados com:

```c++
long long st[K + 1][MAXN];

std::copy(array.begin(), array.end(), st[0]);

for (int i = 1; i <= K; i++)
    for (int j = 0; j + (1 << i) <= N; j++)
        st[i][j] = st[i - 1][j] + st[i - 1][j + (1 << (i - 1))];
```
Para responder à consulta de soma para o intervalo  $[L, R]$ , iteramos sobre todas as potências de dois, começando pela maior. Assim que uma potência de dois  $2^i$  for menor ou igual ao comprimento do intervalo ( $= R - L + 1$ ), processamos a primeira parte do intervalo  $[L, L + 2^i - 1]$ , e continuamos com o intervalo restante  $[L + 2^i, R]$ .

```c++
long long sum = 0;
for (int i = K; i >= 0; i--) {
    if ((1 << i) <= R - L + 1) {
        sum += st[i][L];
        L += 1 << i;
    }
}
```
A complexidade de tempo para uma Consulta de Soma de Intervalo é  $O(K) = O(\log \text{MAXN})$ .

### Consultas de Mínimo de Intervalo (RMQ)
Estas são as consultas onde a Tabela Esparsa brilha. Ao calcular o mínimo de um intervalo, não importa se processamos um valor no intervalo uma ou duas vezes. Portanto, em vez de dividir um intervalo em vários intervalos, também podemos dividir o intervalo em apenas dois intervalos sobrepostos com comprimento de potência de dois. Por exemplo, podemos dividir o intervalo  $[1, 6]$  nos intervalos  $[1, 4]$  e  $[3, 6]$ . O mínimo do intervalo  $[1, 6]$  é claramente o mesmo que o mínimo do mínimo do intervalo  $[1, 4]$  e o mínimo do intervalo  $[3, 6]$ . Então, podemos calcular o mínimo do intervalo  $[L, R]$  com:
 
$$\min(\text{st}[i][L], \text{st}[i][R - 2^i + 1]) \quad \text{ onde } i = \log_2(R - L + 1)$$ 
Isso requer que possamos calcular  $\log_2(R - L + 1)$  rapidamente. Você pode conseguir isso pré-computando todos os logaritmos:

```c++
int lg[MAXN+1];
lg[1] = 0;
for (int i = 2; i <= MAXN; i++)
    lg[i] = lg[i/2] + 1;
```
Alternativamente, o log pode ser calculado em tempo e espaço constantes:
```c++
// C++20
[[include]] <bit>
int log2_floor(unsigned long i) {
    return std::bit_width(i) - 1;
}

// pré C++20
int log2_floor(unsigned long long i) {
    return i ? __builtin_clzll(1) - __builtin_clzll(i) : -1;
}
```
Este benchmark mostra que usar o array lg é mais lento devido a falhas de cache.
Depois, precisamos pré-computar a estrutura da Tabela Esparsa. Desta vez, definimos  $f$  com  $f(x, y) = \min(x, y)$ .

```c++
int st[K + 1][MAXN];

std::copy(array.begin(), array.end(), st[0]);

for (int i = 1; i <= K; i++)
    for (int j = 0; j + (1 << i) <= N; j++)
        st[i][j] = min(st[i - 1][j], st[i - 1][j + (1 << (i - 1))]);
```
E o mínimo de um intervalo  $[L, R]$  pode ser calculado com:

```c++
int i = lg[R - L + 1];
int minimum = min(st[i][L], st[i][R - (1 << i) + 1]);
```
A complexidade de tempo para uma Consulta de Mínimo de Intervalo é  
$O(1)$ .

### Estruturas de dados semelhantes que suportam mais tipos de consultas
Uma das principais fraquezas da abordagem  $O(1)$  discutida na seção anterior é que essa abordagem só suporta consultas de funções idempotentes. Ou seja, funciona muito bem para consultas de mínimo de intervalo, mas não é possível responder a consultas de soma de intervalo usando essa abordagem.

Existem estruturas de dados semelhantes que podem lidar com qualquer tipo de funções associativas e responder a consultas de intervalo em  $O(1)$ . Uma delas é chamada de Tabela Esparsa Disjunta. Outra seria a Árvore Sqrt.