## União de Conjuntos Disjuntos
Este artigo discute a estrutura de dados União de Conjuntos Disjuntos ou DSU. Muitas vezes também é chamada de Union Find por causa de suas duas principais operações.

Esta estrutura de dados fornece as seguintes capacidades. Recebemos vários elementos, cada um dos quais é um conjunto separado. Uma DSU terá uma operação para combinar quaisquer dois conjuntos, e será capaz de dizer em qual conjunto um elemento específico está. A versão clássica também introduz uma terceira operação, ela pode criar um conjunto a partir de um novo elemento.

Assim, a interface básica desta estrutura de dados consiste em apenas três operações:

- `make_set(v)` - cria um novo conjunto consistindo do novo elemento v
- `union_sets(a, b)` - mescla os dois conjuntos especificados (o conjunto no qual o elemento a está localizado, e o conjunto no qual o elemento b está localizado)
- `find_set(v)` - retorna o representante (também chamado de líder) do conjunto que contém o elemento v. Este representante é um elemento de seu conjunto correspondente. Ele é selecionado em cada conjunto pela própria estrutura de dados (e pode mudar ao longo do tempo, nomeadamente após chamadas `union_sets`). Este representante pode ser usado para verificar se dois elementos fazem parte do mesmo conjunto ou não. a e b estão exatamente no mesmo conjunto, se `find_set(a) == find_set(b)`. Caso contrário, eles estão em conjuntos diferentes.
Como descrito em mais detalhes mais tarde, a estrutura de dados permite que você faça cada uma dessas operações em quase  $O(1)$  tempo em média.

Também em uma das subseções, uma estrutura alternativa de uma DSU é explicada, que alcança uma complexidade média mais lenta de  $O(\log n)$ , mas pode ser mais poderosa do que a estrutura regular DSU.

### Construir uma estrutura de dados eficiente
Armazenaremos os conjuntos na forma de árvores: cada árvore corresponderá a um conjunto. E a raiz da árvore será o representante/líder do conjunto.

Na imagem a seguir, você pode ver a representação de tais árvores.

![[Pasted image 20240130193618.png]]

No início, cada elemento começa como um único conjunto, portanto cada vértice é sua própria árvore. Então combinamos o conjunto contendo o elemento 1 e o conjunto contendo o elemento 2. Depois combinamos o conjunto contendo o elemento 3 e o conjunto contendo o elemento 4. E no último passo, combinamos o conjunto contendo o elemento 1 e o conjunto contendo o elemento 3.

Para a implementação, isso significa que teremos que manter um array `parent` que armazena uma referência ao seu ancestral imediato na árvore.

