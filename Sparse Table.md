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


