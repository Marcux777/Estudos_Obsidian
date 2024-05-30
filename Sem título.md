O primeiro passo para a aplicação do ACO a um problema de otimização combinatória (COP) consiste em definir um modelo do COP como uma trinca (S,Ω,f), onde:

  

- **S** é um espaço de busca definido sobre um conjunto finito de variáveis de decisão discretas;

- **Ω** é um conjunto de restrições entre as variáveis; e

- **f:S→R+0** é uma função objetivo a ser minimizada (como maximizar sobre f é o mesmo que minimizar sobre -f, todo COP pode ser descrito como um problema de minimização).

  

O espaço de busca **S** é definido da seguinte forma. Um conjunto de variáveis discretas **$Xi$**, i=1,…,n, com valores **$v^{j}_{i}∈Di={v^{1}_{i},…,v^{|Di|}_{i}}$**, é dado. Elementos de **S** são atribuições completas, ou seja, atribuições nas quais cada variável $X_i$ tem um valor **$v^{j}_{i}$** atribuído de seu domínio **$D_i$**. O conjunto de soluções viáveis **S_Ω** é dado pelos elementos de **S** que satisfazem todas as restrições no conjunto **Ω**.

  

Uma solução $s^{∗}∈S_{Ω}$ é chamada de ótimo global se e somente se

$$f(s^{∗})≤f(s) ∀s∈S_{Ω}$$.

O conjunto de todas as soluções globalmente ótimas é denotado por $S∗Ω⊆SΩ$. Resolver um COP requer encontrar pelo menos um $s^{∗}∈S∗Ω$.