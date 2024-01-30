## Pilha Mínima / Fila Mínima¶
Neste artigo, vamos considerar três problemas: primeiro, vamos modificar uma pilha de maneira que nos permita encontrar o menor elemento da pilha em  
$O(1)$ , depois faremos o mesmo com uma fila, e finalmente usaremos essas estruturas de dados para encontrar o mínimo em todos os subconjuntos de um comprimento fixo em um array em  
$O(n)$ .

### Modificação da Pilha
Queremos modificar a estrutura de dados da pilha de tal forma que seja possível encontrar o menor elemento na pilha em  
$O(1)$ , mantendo o mesmo comportamento assintótico para adicionar e remover elementos da pilha. Lembrete rápido, em uma pilha, apenas adicionamos e removemos elementos em uma extremidade.

Para fazer isso, não apenas armazenaremos os elementos na pilha, mas os armazenaremos em pares: o próprio elemento e o mínimo na pilha a partir deste elemento e abaixo.

```c++
stack<pair<int, int>> st;
```
Está claro que encontrar o mínimo em toda a pilha consiste apenas em olhar o valor `stack.top().second`.

Também é óbvio que adicionar ou remover um novo elemento à pilha pode ser feito em tempo constante.

Implementação:

- Adicionando um elemento:
```c++
int new_min = st.empty() ? new_elem : min(new_elem, st.top().second);
st.push({new_elem, new_min});
```
- Removendo um elemento:
```c++
int removed_element = st.top().first;
st.pop();
```
- Encontrando o mínimo:
```c++
int minimum = st.top().second;
```

### Modificação da Fila (método 1)
Agora queremos realizar as mesmas operações com uma fila, ou seja, queremos adicionar elementos no final e removê-los da frente.

Aqui consideramos um método simples para modificar uma fila. No entanto, ele tem uma grande desvantagem, porque a fila modificada na verdade não armazenará todos os elementos.

A ideia principal é armazenar apenas os itens na fila que são necessários para determinar o mínimo. Ou seja, manteremos a fila em ordem não decrescente (ou seja, o valor mais pequeno será armazenado na cabeça), e claro, não de qualquer maneira arbitrária, o mínimo real tem que estar sempre contido na fila. Desta forma, o menor elemento estará sempre na cabeça da fila. Antes de adicionar um novo elemento à fila, basta fazer um "corte": removeremos todos os elementos finais da fila que são maiores que o novo elemento, e depois adicionaremos o novo elemento à fila. Desta forma, não quebramos a ordem da fila, e também não perderemos o elemento atual se ele for o mínimo em qualquer etapa subsequente. Todos os elementos que removemos nunca podem ser um mínimo em si, então essa operação é permitida. Quando queremos extrair um elemento da cabeça, ele pode não estar lá (porque o removemos anteriormente ao adicionar um elemento menor). Portanto, ao excluir um elemento de uma fila, precisamos conhecer o valor do elemento. Se a cabeça da fila tiver o mesmo valor, podemos removê-la com segurança, caso contrário, não fazemos nada.

Considere as implementações das operações acima:

```c++
deque<int> q;
```
- Encontrando o mínimo:
```c++
int minimum = q.front();
```
- Adicionando um elemento:
```c++
while (!q.empty() && q.back() > new_element)
    q.pop_back();
q.push_back(new_element);
```
- Removendo um elemento:
```c++
if (!q.empty() && q.front() == remove_element)
    q.pop_front();
```
Está claro que, em média, todas essas operações levam apenas  $O(1)$  tempo (porque cada elemento só pode ser empurrado e estourado uma vez).

### Modificação da Fila (método 2)
Esta é uma modificação do método 1. Queremos ser capazes de remover elementos sem saber qual elemento temos que remover. Podemos conseguir isso armazenando o índice de cada elemento na fila. E também lembramos quantos elementos já adicionamos e removemos.

```c++
deque<pair<int, int>> q;
int cnt_added = 0;
int cnt_removed = 0;
```
- Encontrando o mínimo:
```c++
int minimum = q.front().first;
```
- Adicionando um elemento:
```c++
while (!q.empty() && q.back().first > new_element)
    q.pop_back();
q.push_back({new_element, cnt_added});
cnt_added++;
```
- Removendo um elemento:
```c++
if (!q.empty() && q.front().second == cnt_removed) 
    q.pop_front();
cnt_removed++;
```

### Modificação da Fila (método 3)
Aqui consideramos outra maneira de modificar uma fila para encontrar o mínimo em  
$O(1)$ . Esta maneira é um pouco mais complicada de implementar, mas desta vez realmente armazenamos todos os elementos. E também podemos remover um elemento da frente sem conhecer seu valor.

A ideia é reduzir o problema ao problema das pilhas, que já resolvemos. Portanto, só precisamos aprender como simular uma fila usando duas pilhas.

Criamos duas pilhas, s1 e s2. Claro que essas pilhas serão da forma modificada, para que possamos encontrar o mínimo em  
$O(1)$ . Adicionaremos novos elementos à pilha s1 e removeremos elementos da pilha s2. Se em algum momento a pilha s2 estiver vazia, movemos todos os elementos de s1 para s2 (o que essencialmente inverte a ordem desses elementos). Finalmente, encontrar o mínimo em uma fila envolve apenas encontrar o mínimo de ambas as pilhas.

Assim, realizamos todas as operações em  $O(1)$  em média (cada elemento será adicionado uma vez à pilha s1, transferido uma vez para s2 e estourado uma vez de s2)

Implementação:

```c++
stack<pair<int, int>> s1, s2;
```
- Encontrando o mínimo:
```c++
if (s1.empty() || s2.empty()) 
    minimum = s1.empty() ? s2.top().second : s1.top().second;
else
    minimum = min(s1.top().second, s2.top().second);
```
- Adicionando um elemento:
```c++
int minimum = s1.empty() ? new_element : min(new_element, s1.top().second);
s1.push({new_element, minimum});
```
- Removendo um elemento:
```c++
if (s2.empty()) {
    while (!s1.empty()) {
        int element = s1.top().first;
        s1.pop();
        int minimum = s2.empty() ? element : min(element, s2.top().second);
        s2.push({element, minimum});
    }
}
int remove_element = s2.top().first;
s2.pop();
```

### Encontrando o mínimo para todos os subconjuntos de comprimento fixo
Suponha que temos um array  $A$  de comprimento  $N$  e um dado  $M \le N$ . Temos que encontrar o mínimo de cada subconjunto de comprimento  $M$  neste array, ou seja, temos que encontrar:
 
$$\min_{0 \le i \le M-1} A[i], \min_{1 \le i \le M} A[i], \min_{2 \le i \le M+1} A[i],~\dots~, \min_{N-M \le i \le N-1} A[i]$$ 
Temos que resolver este problema em tempo linear, ou seja,  $O(n)$ .

Podemos usar qualquer uma das três filas modificadas para resolver o problema. As soluções devem ser claras: adicionamos os primeiros  $M$  elementos do array, encontramos e exibimos seu mínimo, depois adicionamos o próximo elemento à fila e removemos o primeiro elemento do array, encontramos e exibimos seu mínimo, etc. Como todas as operações com a fila são realizadas em tempo constante em média, a complexidade do algoritmo inteiro será  $O(n)$ .