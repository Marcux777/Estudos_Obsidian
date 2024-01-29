

Uma fração contínua é uma representação de um número real como uma sequência convergente específica de números racionais. Elas são úteis em programação competitiva porque são fáceis de calcular e podem ser eficientemente usadas para encontrar a melhor aproximação racional possível do número real subjacente (entre todos os números cujo denominador não ultrapassa um determinado valor).

Além disso, as frações contínuas estão intimamente relacionadas ao algoritmo de Euclides, o que as torna úteis em uma série de problemas teóricos relacionados a números.

## Representação de fração contínua

#### Definição

Sejam  $a_0, a_1, \dots, a_k \in \mathbb Z$  e  $a_1, a_2, \dots, a_k \geq 1$ . Então, a expressão
$$r=a_0 + \frac{1}{a_1 + \frac{1}{\dots + \frac{1}{a_k}}},$$ 
é chamada de representação de fração contínua do número racional  $r$  e é denotada brevemente como  $r=[a_0;a_1,a_2,\dots,a_k]$ .

#### Exemplo

Seja  $r = \frac{5}{3}$ . Existem duas maneiras de representá-lo como uma fração contínua:
 
$$ \begin{align} r = [1;1,1,1] &= 1+\frac{1}{1+\frac{1}{1+\frac{1}{1}}},\\ r = [1;1,2] &= 1+\frac{1}{1+\frac{1}{2}}. \end{align} $$

Pode ser comprovado que qualquer número racional pode ser representado como uma fração contínua de exatamente  $2$  maneiras:

$$r = [a_0;a_1,\dots,a_k,1] = [a_0;a_1,\dots,a_k+1].$$ 
Além disso, o comprimento  $k$  de tal fração contínua é estimado como  $k = O(\log \min(p, q))$  para  $r=\frac{p}{q}$ .

A lógica por trás disso ficará clara quando nos aprofundarmos nos detalhes da construção da fração contínua.

#### Definição

Seja  $a_0,a_1,a_2, \dots$  uma sequência de inteiros tal que  $a_1, a_2, \dots \geq 1$ . Seja  $r_k = [a_0; a_1, \dots, a_k]$ . Então, a expressão
$$r = a_0 + \frac{1}{a_1 + \frac{1}{a_2+\dots}} = \lim\limits_{k \to \infty} r_k.$$ 
é chamada de representação de fração contínua do número irracional  $r$  e é denotada brevemente como  $r = [a_0;a_1,a_2,\dots]$ .

Note que para  $r=[a_0;a_1,\dots]$  e um número inteiro  $k$ , vale que  $r+k = [a_0+k; a_1, \dots]$ .

Outra observação importante é que  $\frac{1}{r}=[0;a_0, a_1, \dots]$  quando  $a_0 > 0$  e 
$\frac{1}{r} = [a_1; a_2, \dots]$  quando  $a_0 = 0$ .

#### Definição

Na definição acima, os números racionais  $r_0, r_1, r_2, \dots$  são chamados de convergentes de  $r$ .

Correspondentemente, o  $k$ -ésimo convergente individual  $r_k = [a_0; a_1, \dots, a_k] = \frac{p_k}{q_k}$  é chamado de  $k$ -ésimo convergente de  $r$ .

#### Exemplo

Considere  $r = [1; 1, 1, 1, \dots]$ . Pode ser comprovado por indução que  $r_k = \frac{F_{k+2}}{F_{k+1}}$, onde  $F_k$  é a sequência de Fibonacci definida como  $F_0 = 0$,  $F_1 = 1$  e  $F_{k} = F_{k-1} + F_{k-2}$ . Pela fórmula de Binet, é conhecido que
 
$$r_k = \frac{\phi^{k+2} - \psi^{k+2}}{\phi^{k+1} - \psi^{k+1}},$$ 
onde  $\phi = \frac{1+\sqrt{5}}{2} \approx 1.618$  é a proporção áurea e  $\psi = \frac{1-\sqrt{5}}{2} = -\frac{1}{\phi} \approx -0.618$ . Assim,
 
$$r = 1+\frac{1}{1+\frac{1}{1+\dots}}=\lim\limits_{k \to \infty} r_k = \phi = \frac{1+\sqrt{5}}{2}.$$ 
Observe que, neste caso específico, uma maneira alternativa de encontrar  $r$  seria resolver a equação

$$r = 1+\frac{1}{r} \implies r^2 = r + 1.$$ 

#### Definição

Seja  $r_k = [a_0; a_1, \dots, a_{k-1}, a_k]$ . Os números  $[a_0; a_1, \dots, a_{k-1}, t]$  para  $1 \leq t \leq a_k$  são chamados de semiconvergentes.

Normalmente nos referimos a (semi)convergentes que são maiores que  $r$  como (semi)convergentes superiores e àqueles que são menores que  $r$  como (semi)convergentes inferiores.

#### Definição

Complementar aos convergentes, definimos os quocientes completos como  $s_k = [a_k; a_{k+1}, a_{k+2}, \dots]$ .

Correspondentemente, chamaremos um  $s_k$  individual de  $k$ -ésimo quociente completo de  $r$ .

A partir das definições acima, pode-se concluir que  $s_k \geq 1$  para  $k \geq 1$ .

Tratando  $[a_0; a_1, \dots, a_k]$  como uma expressão algébrica formal e permitindo números reais arbitrários no lugar de  $a_i$ , obtemos

$$r = [a_0; a_1, \dots, a_{k-1}, s_k].$$ 
Em particular,  $r = [s_0] = s_0$ . Por outro lado, podemos expressar  $s_k$  como

$$s_k = [a_k; s_{k+1}] = a_k + \frac{1}{s_{k+1}},$$ 
o que significa que podemos calcular  $a_k = \lfloor s_k \rfloor$  e  $s_{k+1} = (s_k - a_k)^{-1}$  a partir de  $s_k$ .

A sequência  $a_0, a_1, \dots$  é bem definida, a menos que  $s_k=a_k$ , o que só acontece quando  $r$  é um número racional.

Assim, a representação de fração contínua é única para qualquer número irracional  $r$ .

### Implementação

Nos trechos de código, geralmente assumiremos frações contínuas finitas.

A partir de  $s_k$ , a transição para  $s_{k+1}$  parece com

 
$$s_k =\left\lfloor s_k \right\rfloor + \frac{1}{s_{k+1}}.$$ 
Desta expressão, o próximo quociente completo  $s_{k+1}$  é obtido como

 
$$s_{k+1} = \left(s_k-\left\lfloor s_k\right\rfloor\right)^{-1}.$$ 
Para  $s_k=\frac{p}{q}$  isso significa que

$$ s_{k+1} = \left(\frac{p}{q}-\left\lfloor \frac{p}{q} \right\rfloor\right)^{-1} = \frac{q}{p-q\cdot \lfloor \frac{p}{q} \rfloor} = \frac{q}{p \bmod q}. $$ 
Assim, o cálculo de uma representação de fração contínua para  $r=\frac{p}{q}$  segue os passos do algoritmo de Euclides para  $p$  e  $q$ .

Dessa forma, também segue que  
$\gcd(p_k, q_k) = 1$  para  
$\frac{p_k}{q_k} = [a_0; a_1, \dots, a_k]$ . Portanto, os convergentes são sempre irreduzíveis.

C++:

```cpp

tuple<int, int> fraction(int p, int q) {
    vector<int> a;
    while(q) {
        a.push_back(p / q);
        tie(p, q) = make_tuple(q, p % q);
    }
    return make_tuple(a);
}
```


## Resultados-chave
Para fornecer alguma motivação para o estudo adicional de frações contínuas, apresentamos agora alguns fatos-chave.
#### Recorrência
Para os convergentes  $r_k = \frac{p_k}{q_k}$ , vale a seguinte recorrência, permitindo seu cálculo rápido:
 
$$\frac{p_k}{q_k}=\frac{a_k p_{k-1} + p_{k-2}}{a_k q_{k-1} + q_{k-2}},$$ 
onde  $\frac{p_{-1}}{q_{-1}}=\frac{1}{0}$  e  $\frac{p_{-2}}{q_{-2}}=\frac{0}{1}$ .

#### Desvios
O desvio de  $r_k = \frac{p_k}{q_k}$  em relação a  $r$  pode ser geralmente estimado como
 
$$\left|\frac{p_k}{q_k}-r\right| \leq \frac{1}{q_k q_{k+1}} \leq \frac{1}{q_k^2}.$$ 
Multiplicando ambos os lados por  $q_k$ , obtemos uma estimativa alternativa:
 
$$|p_k - q_k r| \leq \frac{1}{q_{k+1}}.$$ 
A partir da recorrência acima, segue-se que  $q_k$  cresce pelo menos tão rapidamente quanto os números de Fibonacci.

Na imagem abaixo, você pode ver a visualização de como os convergentes  $r_k$  se aproximam de  
$r=\frac{1+\sqrt 5}{2}$ :

![[Pasted image 20240126185817.png]]

 
A linha pontilhada azul representa  $r=\frac{1+\sqrt 5}{2}$ . Os convergentes ímpares se aproximam de cima e os convergentes pares se aproximam de baixo.

#### Envoltórios de retículas
Considere envoltórios convexos de pontos acima e abaixo da linha  $y=rx$ .

Os convergentes ímpares  $(q_k;p_k)$  são os vértices do envoltório superior, enquanto os convergentes pares  $(q_k;p_k)$  são os vértices do envoltório inferior.

Todos os vértices inteiros nos envoltórios são obtidos como  $(q;p)$  tal que

$$\frac{p}{q} = \frac{tp_{k-1} + p_{k-2}}{tq_{k-1} + q_{k-2}}$$ 
para  $t$  inteiro tal que  $0 \leq t \leq a_k$ . Em outras palavras, o conjunto de pontos de retícula nos envoltórios corresponde ao conjunto de semiconvergentes.

Na imagem abaixo, você pode ver os convergentes e semiconvergentes (pontos cinza intermediários) de  $r=\frac{9}{7}$ :

![[Pasted image 20240126185928.png]]

#### Melhores aproximações
Seja  $\frac{p}{q}$  a fração para minimizar  $\left|r-\frac{p}{q}\right|$  sujeita a  $q \leq x$  para algum  $x$ .

Então  $\frac{p}{q}$  é uma semiconvergente de  $r$ .

O último fato permite encontrar as melhores aproximações racionais de  
$r$  verificando suas semiconvergentes.

A seguir, você encontrará uma explicação mais detalhada, bem como um pouco de intuição e interpretação para esses fatos.



## Convergentes
Vamos dar uma olhada mais de perto nos convergentes que foram definidos anteriormente. Para  
$r=[a_0, a_1, a_2, \dots]$ , seus convergentes são
 
$$\begin{gather} r_0=[a_0],\\r_1=[a_0, a_1],\\ \dots,\\ r_k=[a_0, a_1, \dots, a_k]. \end{gather}$$ 
Os convergentes são o conceito central das frações contínuas, portanto, é importante estudar suas propriedades.

Para o número  $r$ , seu  $k$ -ésimo convergente  $r_k = \frac{p_k}{q_k}$  pode ser calculado como
 
$$r_k = \frac{P_k(a_0,a_1,\dots,a_k)}{P_{k-1}(a_1,\dots,a_k)} = \frac{a_k p_{k-1} + p_{k-2}}{a_k q_{k-1} + q_{k-2}},$$ 
onde  $P_k(a_0,\dots,a_k)$  é o continuante, um polinômio multivariado definido como
 
$$P_k(x_0,x_1,\dots,x_k) = \det \begin{bmatrix} x_k & 1 & 0 & \dots & 0 \\ -1 & x_{k-1} & 1 & \dots & 0 \\ 0 & -1 & x_2 & . & \vdots \\ \vdots & \vdots & . & \ddots & 1 \\ 0 & 0 & \dots & -1 & x_0 \end{bmatrix}_{\textstyle .}$$ 
Assim,  $r_k$  é uma mediant ponderada de  $r_{k-1}$  e  $r_{k-2}$ .

Para consistência, dois convergentes adicionais  $r_{-1} = \frac{1}{0}$  e  $r_{-2} = \frac{0}{1}$  são definidos.

#### Explicação Detalhada
O numerador e o denominador de  $r_k$  podem ser vistos como polinômios multivariados de  $a_0, a_1, \dots, a_k$ :

$$r_k = \frac{P_k(a_0, a_1, \dots, a_k)}{Q_k(a_0,a_1, \dots, a_k)}.$$ 
A partir da definição de convergentes,

$$r_k = a_0 + \frac{1}{[a_1;a_2,\dots, a_k]}= a_0 + \frac{Q_{k-1}(a_1, \dots, a_k)}{P_{k-1}(a_1, \dots, a_k)} = \frac{a_0 P_{k-1}(a_1, \dots, a_k) + Q_{k-1}(a_1, \dots, a_k)}{P_{k-1}(a_1, \dots, a_k)}.$$ 
Daí segue que  $Q_k(a_0, \dots, a_k) = P_{k-1}(a_1, \dots, a_k)$ . Isso gera a relação

$$P_k(a_0, \dots, a_k) = a_0 P_{k-1}(a_1, \dots, a_k) + P_{k-2}(a_2, \dots, a_k).$$ 
Inicialmente,  $r_0 = \frac{a_0}{1}$  e  $r_1 = \frac{a_0 a_1 + 1}{a_1}$ , assim
 
$$\begin{align}P_0(a_0)&=a_0,\\ P_1(a_0, a_1) &= a_0 a_1 + 1.\end{align}$$ 
Para consistência, é conveniente definir  $P_{-1} = 1$  e  $P_{-2}=0$  e dizer formalmente que  $r_{-1} = \frac{1}{0}$  e  $r_{-2}=\frac{0}{1}$ .

Da análise numérica, é conhecido que o determinante de uma matriz tridiagonal arbitrária

 
$$T_k = \det \begin{bmatrix} a_0 & b_0 & 0 & \dots & 0 \\ c_0 & a_1 & b_1 & \dots & 0 \\ 0 & c_1 & a_2 & . & \vdots \\ \vdots & \vdots & . & \ddots & c_{k-1} \\ 0 & 0 & \dots & b_{k-1} & a_k \end{bmatrix}$$ 
pode ser calculado recursivamente como  $T_k = a_k T_{k-1} - b_{k-1} c_{k-1} T_{k-2}$ . Comparando-o com  $P_k$ , obtemos uma expressão direta
 
$$P_k = \det \begin{bmatrix} x_k & 1 & 0 & \dots & 0 \\ -1 & x_{k-1} & 1 & \dots & 0 \\ 0 & -1 & x_2 & . & \vdots \\ \vdots & \vdots & . & \ddots & 1 \\ 0 & 0 & \dots & -1 & x_0 \end{bmatrix}_{\textstyle .}$$ 
Esse polinômio também é conhecido como continuante devido à sua relação próxima com frações contínuas. O continuante não mudará se a sequência na diagonal principal for invertida. Isso fornece uma fórmula alternativa para calculá-lo:

$$P_k(a_0, \dots, a_k) = a_k P_{k-1}(a_0, \dots, a_{k-1}) + P_{k-2}(a_0, \dots, a_{k-2}).$$ 
### Implementação
Vamos calcular os convergentes como um par de sequências  $p_{-2}, p_{-1}, p_0, p_1, \dots, p_k$  e  $q_{-2}, q_{-1}, q_0, q_1, \dots, q_k$ :

C++
```cpp
pair<vector<int>, vector<int>> convergents(vector<int> a) {
    vector<int> p = {0, 1};
    vector<int> q = {1, 0};
    for (auto it : a) {
        p.push_back(p[p.size() - 1] * it + p[p.size() - 2]);
        q.push_back(q[q.size() - 1] * it + q[q.size() - 2]);
    }
    return make_pair(p, q);
}
```

## Árvores de frações contínuas
Existem duas maneiras principais de unir todas as frações contínuas possíveis em estruturas de árvores úteis.

### Árvore de Stern-Brocot
A árvore de Stern-Brocot é uma árvore de busca binária que contém todos os números racionais positivos distintos.

A árvore geralmente parece o seguinte:

![[Pasted image 20240126191203.png]]
*A imagem de Aaron Rotenberg é licenciada sob CC BY-SA 3.0*

Frações  $\frac{0}{1}$  e  $\frac{1}{0}$  são "virtualmente" mantidas nos lados esquerdo e direito da árvore, respectivamente.

Então, a fração em um nó é uma medianta  $\frac{a+c}{b+d}$  de duas frações  $\frac{a}{b}$  e  $\frac{c}{d}$  acima dela.

A recorrência  $\frac{p_k}{q_k}=\frac{a_k p_{k-1} + p_{k-2}}{a_k q_{k-1} + q_{k-2}}$  significa que a representação da fração contínua codifica o caminho para  $\frac{p_k}{q_k}$  na árvore. Para encontrar  $[a_0; a_1, \dots, a_{k}, 1]$ , é necessário fazer  $a_0$  movimentos para a direita,  $a_1$  movimentos para a esquerda,  $a_2$  movimentos para a direita e assim por diante até  
$a_k$ .

O pai de  $[a_0; a_1, \dots, a_k,1]$  então é a fração obtida dando um passo de volta na direção usada por último.

Em outras palavras, é  $[a_0; a_1, \dots, a_k-1,1]$  quando  $a_k > 1$  e  $[a_0; a_1, \dots, a_{k-1}, 1]$  quando  $a_k = 1$ .

Assim, os filhos de  $[a_0; a_1, \dots, a_k, 1]$  são  $[a_0; a_1, \dots, a_k+1, 1]$  e  $[a_0; a_1, \dots, a_k, 1, 1]$ .

Vamos indexar a árvore de Stern-Brocot. O vértice raiz é atribuído um índice  $1$ . Então, para um vértice  $v$ , o índice de seu filho à esquerda é atribuído alterando o bit principal de  $v$  de  $1$  para  $10$ , e para o filho à direita, é atribuído alterando o bit principal de  $1$  para  $11$ :

![[Pasted image 20240126191343.png]]

Nessa indexação, a representação de fração contínua de um número racional especifica a codificação de comprimento de execução de seu índice binário.

Para  $\frac{5}{2} = [2;2] = [2;1,1]$ , seu índice é  $1011_2$  e sua codificação de comprimento de execução, considerando bits em ordem crescente, é  $[2;1,1]$ .

Outro exemplo é  $\frac{2}{5} = [0;2,2]=[0;2,1,1]$ , que tem índice  $1100_2$  e sua codificação de comprimento de execução é, de fato,  $[0;2,2]$ .

Vale ressaltar que a árvore de Stern-Brocot é, na verdade, uma treap. Ou seja, é uma árvore de busca binária por  $\frac{p}{q}$ , mas é uma heap tanto por  $p$  quanto por  $q$ .

#### Comparando frações contínuas

Você recebe  $A=[a_0; a_1, \dots, a_n]$  e  $B=[b_0; b_1, \dots, b_m]$ . Qual fração é menor?

##### Solução
Assuma por enquanto que  $A$  e  $B$  são irracionais e suas representações de frações contínuas denotam uma descida infinita na árvore de Stern-Brocot.

Como já mencionamos, nessa representação  $a_0$  denota o número de giros à direita na descida,  $a_1$  denota o número de giros à esquerda consecutivos e assim por diante. Portanto, ao comparar  
$a_k$  e $b_k$ , se  $a_k = b_k$ , devemos simplesmente passar para a comparação de  $a_{k+1}$  e  $b_{k+1}$ . Caso contrário, se estivermos em descidas para a direita, devemos verificar se  $a_k < b_k$  e se estivermos em descidas para a esquerda, devemos verificar se  $a_k > b_k$  para determinar se  $A < B$ .

Em outras palavras, para irracionais  $A$  e  $B$ , seria  $A < B$  se e somente se  $(a_0, -a_1, a_2, -a_3, \dots) < (b_0, -b_1, b_2, -b_3, \dots)$  com comparação lexicográfica.

Agora, formalmente, usando  $\infty$  como um elemento da representação de fração contínua, é possível emular números irracionais  
$A-\varepsilon$  e  $A+\varepsilon$ , isto é, elementos que são menores (maiores) que  $A$ , mas maiores (menores) que qualquer outro número real. Especificamente, para  $A=[a_0; a_1, \dots, a_n]$ , um desses dois elementos pode ser emulado como  $[a_0; a_1, \dots, a_n, \infty]$  e o outro pode ser emulado como  $[a_0; a_1, \dots, a_n - 1, 1, \infty]$ .

Qual corresponde a  $A-\varepsilon$  e qual corresponde a  $A+\varepsilon$  pode ser determinado pela paridade de  $n$  ou comparando-os como números irracionais.


```Python
# verifica se a < b assumindo que a[-1] = b[-1] = infty e a != b
def less(a, b):
    a = [(-1)**i*a[i] for i in range(len(a))]
    b = [(-1)**i*b[i] for i in range(len(b))]
    return a < b

# [a0; a1, ..., ak] -> [a0, a1, ..., ak-1, 1]
def expand(a):
    if a: # a vazio = inf
        a[-1] -= 1
        a.append(1)
    return a

# retorna a-eps, a+eps
def pm_eps(a):
    b = expand(a.copy())
    a.append(float('inf'))
    b.append(float('inf'))
    return (a, b) if less(a, b) else (b, a)
```

#### Melhor ponto interno

Dado  $\frac{0}{1} \leq \frac{p_0}{q_0} < \frac{p_1}{q_1} \leq \frac{1}{0}$ . Encontre o número racional  $\frac{p}{q}$  de modo que  $(q; p)$  seja lexicograficamente o menor e  $\frac{p_0}{q_0} < \frac{p}{q} < \frac{p_1}{q_1}$ .

##### Solução
Em termos da árvore de Stern-Brocot, isso significa que precisamos encontrar o AncesRealSternBrocottor Comum (LCA) de  $\frac{p_0}{q_0}$  e  $\frac{p_1}{q_1}$ . Devido à conexão entre a árvore de Stern-Brocot e a fração contínua, esse LCA corresponderia aproximadamente ao maior prefixo comum das representações de frações contínuas para  $\frac{p_0}{q_0}$  e  $\frac{p_1}{q_1}$ .

Portanto, se  $\frac{p_0}{q_0} = [a_0; a_1, \dots, a_{k-1}, a_k, \dots]$  e  $\frac{p_1}{q_1} = [a_0; a_1, \dots, a_{k-1}, b_k, \dots]$  são números irracionais, o LCA é  $[a_0; a_1, \dots, \min(a_k, b_k)+1]$ .

Para  $r_0$  e  $r_1$  racionais, um deles pode ser o LCA em si, o que exigiria um tratamento especial. Para simplificar a solução para  $r_0$  e  $r_1$  racionais, é possível usar a representação de fração contínua de  
$r_0 + \varepsilon$  e  $r_1 - \varepsilon$  que foi derivada no problema anterior.

```Python
# encontra lexicograficamente o menor (q, p)
# tal que p0/q0 < p/q < p1/q1
def meio(p0, q0, p1, q1):
    a0 = pm_eps(fraction(p0, q0))[1]
    a1 = pm_eps(fraction(p1, q1))[0]
    a = []
    for i in range(min(len(a0), len(a1))):
        a.append(min(a0[i], a1[i]))
        if a0[i] != a1[i]:
            break
    a[-1] += 1
    p, q = convergents(a)
    return p[-1], q[-1]
```

#### GCJ 2019, Round 2 - Novos Elementos: Parte 2

Você recebe  $N$  pares de números inteiros positivos  $(C_i, J_i)$ . Você precisa encontrar um par de inteiros positivos  $(x, y)$  tal que  $C_i x + J_i y$  seja uma sequência estritamente crescente.

Dentre esses pares, encontre o menor lexicograficamente.

##### Solução
Reformulando o enunciado,  $A_i x + B_i y$  deve ser positivo para todos os  $i$ , onde  $A_i = C_i - C_{i-1}$  e  $B_i = J_i - J_{i-1}$ .

Dentre tais equações, temos quatro grupos significativos para  $A_i x + B_i y > 0$ :

1. $A_i, B_i > 0$  podem ser ignorados, já que estamos procurando  $x, y > 0$ .
 
2. $A_i, B_i \leq 0$  forneceriam "IMPOSSIBLE" como resposta.

3. $A_i > 0$ ,  $B_i \leq 0$ . Tais restrições são equivalentes a $\frac{y}{x} < \frac{A_i}{-B_i}$ .
 
4. $A_i \leq 0$ , $B_i > 0$ . Tais restrições são equivalentes a  $\frac{y}{x} > \frac{-A_i}{B_i}$ .

Seja  $\frac{p_0}{q_0}$  o maior $\frac{-A_i}{B_i}$  do quarto grupo e  $\frac{p_1}{q_1}$  o menor $\frac{A_i}{-B_i}$  do terceiro grupo.

O problema agora é, dado $\frac{p_0}{q_0} < \frac{p_1}{q_1}$ , encontrar uma fração   $\frac{p}{q}$  tal que  $(q;p)$  seja lexicograficamente o menor e $\frac{p_0}{q_0} < \frac{p}{q} < \frac{p_1}{q_1}$ .


```Python
    def resolver():
    n = int(input())
    C = [0] * n
    J = [0] * n
    # p0/q0 < y/x < p1/q1
    p0, q0 = 0, 1
    p1, q1 = 1, 0
    falha = False
    for i in range(n):
        C[i], J[i] = map(int, input().split())
        if i > 0:
            A = C[i] - C[i-1]
            B = J[i] - J[i-1]
            if A <= 0 and B <= 0:
                falha = True
            elif B > 0 and A < 0: # y/x > (-A)/B if B > 0
                if (-A)*q0 > p0*B:
                    p0, q0 = -A, B
            elif B < 0 and A > 0: # y/x < A/(-B) if B < 0
                if A*q1 < p1*(-B):
                    p1, q1 = A, -B
    if p0*q1 >= p1*q0 or falha:
        return 'IMPOSSIBLE'

    p, q = meio(p0, q0, p1, q1)
    return str(q) + ' ' + str(p)
    ```



### Árvore de Calkin-Wilf
Uma maneira um pouco mais simples de organizar frações contínuas em uma árvore binária é a árvore de Calkin-Wilf.

A árvore geralmente se parece com isto:

![[Pasted image 20240126194921.png]]

*A imagem de Olli Niemitalo, Proz está licenciada sob CC0 1.0*

Na raiz da árvore, o número  $\frac{1}{1}$  está localizado. Então, para o vértice com o número $\frac{p}{q}$ , seus filhos são
$\frac{p}{p+q}$  e  $\frac{p+q}{q}$ .

Ao contrário da árvore de Stern-Brocot, a árvore de Calkin-Wilf não é uma árvore de busca binária, portanto, não pode ser usada para realizar uma busca binária racional.

Na árvore de Calkin-Wilf, o pai direto de uma fração $\frac{p}{q}$  é $\frac{p-q}{q}$  quando  $p>q$  e $\frac{p}{q-p}$  caso contrário.

Para a árvore de Stern-Brocot, usamos a recorrência para convergentes. Para estabelecer a conexão entre a fração contínua e a árvore de Calkin-Wilf, devemos lembrar a recorrência para quocientes completos. Se $s_k = \frac{p}{q}$ , então $s_{k+1} = \frac{q}{p \mod q} = \frac{q}{p-\lfloor p/q \rfloor \cdot q}$ .

Por outro lado, se continuarmos indo de $s_k = \frac{p}{q}$  para o seu pai na árvore de Calkin-Wilf quando $p > q$ , acabaremos em  $\frac{p \mod q}{q} = \frac{1}{s_{k+1}}$ . Se continuarmos fazendo isso, acabaremos em  $s_{k+2}$ , então $\frac{1}{s_{k+3}}$  e assim por diante. A partir disso, podemos deduzir que:

1. Quando  $a_0> 0$ , o pai direto de  $[a_0; a_1, \dots, a_k]$  na árvore de Calkin-Wilf é    $\frac{p-q}{q}=[a_0 - 1; a_1, \dots, a_k]$ .
2. Quando  $a_0 = 0$  e  $a_1 > 1$ , seu pai direto é $\frac{p}{q-p} = [0; a_1 - 1, a_2, \dots, a_k]$ .
3. E quando  $a_0 = 0$  e  $a_1 = 1$ , seu pai direto é $\frac{p}{q-p} = [a_2; a_3, \dots, a_k]$ .
Correspondentemente, os filhos de  $\frac{p}{q} = [a_0; a_1, \dots, a_k]$  são 
1. $\frac{p+q}{q}=1+\frac{p}{q}$ , que é  $[a_0+1; a_1, \dots, a_k]$ ,
2. $\frac{p}{p+q} = \frac{1}{1+\frac{q}{p}}$ , que é  $[0, 1, a_0, a_1, \dots, a_k]$  para  $a_0 > 0$  e  $[0, a_1+1, a_2, \dots, a_k]$  para  $a_0=0$ .
Vale ressaltar que, se enumerarmos os vértices da árvore de Calkin-Wilf na ordem de busca em largura (ou seja, a raiz tem um número  $1$ , e os filhos do vértice  $v$  têm índices  $2v$  e  $2v+1$  correspondentes), o índice do número racional na árvore de Calkin-Wilf seria o mesmo que na árvore de Stern-Brocot.

Assim, os números nos mesmos níveis das árvores de Stern-Brocot e Calkin-Wilf são os mesmos, mas a ordem deles difere por meio da permutação de inversão de bits.



## Convergência
Para o número  $r$  e sua  $k$-ésima convergente  $r_k=\frac{p_k}{q_k}$ , a seguinte fórmula é válida:

$$r_k = a_0 + \sum\limits_{i=1}^k \frac{(-1)^{i-1}}{q_i q_{i-1}}.$$ 
Em particular, isso significa que
 
$$r_k - r_{k-1} = \frac{(-1)^{k-1}}{q_k q_{k-1}}$$ 
e
 
$$p_k q_{k-1} - p_{k-1} q_k = (-1)^{k-1}.$$ 
A partir disso, podemos concluir que
 
$$\left| r-\frac{p_k}{q_k} \right| \leq \frac{1}{q_{k+1}q_k} \leq \frac{1}{q_k^2}.$$ 
A última desigualdade se deve ao fato de que  $r_k$  e  $r_{k+1}$  geralmente estão localizados em lados diferentes de  $r$ , assim

$$|r-r_k| = |r_k-r_{k+1}|-|r-r_{k+1}| \leq |r_k - r_{k+1}|.$$ 
#### Explicação Detalhada
Para estimar  $|r-r_k|$ , começamos estimando a diferença entre convergentes adjacentes. Pela definição,
 
$$\frac{p_k}{q_k} - \frac{p_{k-1}}{q_{k-1}} = \frac{p_k q_{k-1} - p_{k-1} q_k}{q_k q_{k-1}}.$$ 
Substituindo  $p_k$  e  $q_k$  no numerador por suas recorrências, obtemos
 
$$\begin{align} p_k q_{k-1} - p_{k-1} q_k &= (a_k p_{k-1} + p_{k-2}) q_{k-1} - p_{k-1} (a_k q_{k-1} + q_{k-2}) \\&= p_{k-2} q_{k-1} - p_{k-1} q_{k-2},\end{align}$$ 
assim o numerador de  $r_k - r_{k-1}$  é sempre o numerador negado de  $r_{k-1} - r_{k-2}$ . Isso, por sua vez, é igual a  $1$  para

$$r_1 - r_0=\left(a_0+\frac{1}{a_1}\right)-a_0=\frac{1}{a_1},$$ 
portanto
$$r_k - r_{k-1} = \frac{(-1)^{k-1}}{q_k q_{k-1}}.$$ 
Isso proporciona uma representação alternativa de  $r_k$  como uma soma parcial de uma série infinita:

$$r_k = (r_k - r_{k-1}) + \dots + (r_1 - r_0) + r_0 = a_0 + \sum\limits_{i=1}^k \frac{(-1)^{i-1}}{q_i q_{i-1}}.$$ 
Da relação recorrente, segue que  $q_k$  aumenta monotonamente pelo menos tão rapidamente quanto os números de Fibonacci, portanto

$$r = \lim\limits_{k \to \infty} r_k = a_0 + \sum\limits_{i=1}^\infty \frac{(-1)^{i-1}}{q_i q_{i-1}}$$ 
é sempre bem definido, já que a série subjacente sempre converge. Vale ressaltar que a série residual

$$r-r_k = \sum\limits_{i=k+1}^\infty \frac{(-1)^{i-1}}{q_i q_{i-1}}$$ 
tem o mesmo sinal que  $(-1)^k$  devido à rapidez com que  $q_i q_{i-1}$  diminui. Portanto, convergentes de índice par  $r_k$  se aproximam de  $r$  por baixo, enquanto convergentes de índice ímpar se aproximam de cima:

![[Pasted image 20240126195657.png]]

**Convergentes de  $r=\phi = \frac{1+\sqrt{5}}{2}=[1;1,1,\dots]$  e sua distância de  $r$ .**

A partir desta imagem, podemos ver que

$$|r-r_k| = |r_k - r_{k+1}| - |r-r_{k+1}| \leq |r_k - r_{k+1}|,$$ 
portanto, a distância entre  $r$  e  $r_k$  nunca é maior do que a distância entre  $r_k$  e  $r_{k+1}$ :
 
$$\left|r-\frac{p_k}{q_k}\right| \leq \frac{1}{q_k q_{k+1}} \leq \frac{1}{q_k^2}.$$ 
#### Solução Estendida de Euclides?

Dado  $A, B, C \in \mathbb Z$ . Encontre  $x, y \in \mathbb Z$  tal que  $Ax + By = C$ .

##### Solução
Embora este problema seja tipicamente resolvido com o algoritmo estendido de Euclides, existe uma solução simples e direta usando frações contínuas.

Seja  $\frac{A}{B}=[a_0; a_1, \dots, a_k]$ . Já foi demonstrado anteriormente que $p_k q_{k-1} - p_{k-1} q_k = (-1)^{k-1}$ . Substituindo  $p_k$  e  $q_k$  por  $A$  e  $B$ , obtemos
$$Aq_{k-1} - Bp_{k-1} = (-1)^{k-1} g,$$ 
onde  $g = \gcd(A, B)$ . Se  $C$  é divisível por  $g$ , então a solução é  $x = (-1)^{k-1}\frac{C}{g} q_{k-1}$  e  $y = (-1)^{k}\frac{C}{g} p_{k-1}$.

```Python
# retorna (x, y) tal que Ax+By=C
# assume que tal (x, y) existe
def dio(A, B, C):
    p, q = convergents(fraction(A, B))
    C //= A // p[-1] # dividir por gcd(A, B)
    t = (-1) if len(p) % 2 else 1
    return t*C*q[-2], -t*C*p[-2]
```

## Transformações Lineares Fracionárias
Outro conceito importante para frações contínuas são as chamadas transformações lineares fracionárias.

> # Definição
>Uma transformação linear fracionária é uma função  $f : \mathbb R \to \mathbb R$  tal que  $f(x) = \frac{ax+b}{cx+d}$  para alguns  $a, b, c, d \in \mathbb R$

Uma composição  $(L_0 \circ L_1)(x) = L_0(L_1(x))$  de transformações lineares fracionárias  $L_0(x)=\frac{a_0 x + b_0}{c_0 x + d_0}$  e  $L_1(x)=\frac{a_1 x + b_1}{c_1 x + d_1}$  é ela própria uma transformação linear fracionária:
$$\frac{a_0\frac{a_1 x + b_1}{c_1 x + d_1} + b_0}{c_0 \frac{a_1 x + b_1}{c_1 x + d_1} + d_0} = \frac{a_0(a_1 x + b_1) + b_0 (c_1 x + d_1)}{c_0 (a_1 x + b_1) + d_0 (c_1 x + d_1)} = \frac{(a_0 a_1 + b_0 c_1) x + (a_0 b_1 + b_0 d_1)}{(c_0 a_1 + d_0 c_1) x + (c_0 b_1 + d_0 d_1)}.$$ 
O inverso de uma transformação linear fracionária também é uma transformação linear fracionária:
 
$$y = \frac{ax+b}{cx+d} \iff y(cx+d) = ax + b \iff x = -\frac{dy-b}{cy-a}.$$ 
> # DMOPC '19 Contest 7 P4 - Bob e Frações Contínuas
>Dado um array de inteiros positivos  $a_1, \dots, a_n$ , você precisa responder a  $m$  consultas. Cada consulta consiste em calcular  $[a_l; a_{l+1}, \dots, a_r]$ .
>
> # Solução
> Podemos resolver este problema com uma árvore de segmento se formos capazes de concatenar frações contínuas.
> É geralmente verdade que $[a_0; a_1, \dots, a_k, b_0, b_1, \dots, b_k] = [a_0; a_1, \dots, a_k, [b_1; b_2, \dots, b_k]]$ .
>Vamos denotar  $L_{k}(x) = [a_k; x] = a_k + \frac{1}{x} = \frac{a_k\cdot x+1}{1\cdot x + 0}$ . Note que  $L_k(\infty) = a_k$ . Nessa notação, vale a pena observar que
>$$[a_0; a_1, \dots, a_k, x] = [a_0; [a_1; [\dots; [a_k; x]]]] = (L_0 \circ L_1 \circ \dots \circ L_k)(x) = \frac{p_k x + p_{k-1}}{q_k x + q_{k-1}}.$$
>Assim, o problema se resume ao cálculo de
>$$(L_l \circ L_{l+1} \circ \dots \circ L_r)(\infty).$$ 
>A composição de transformações é associativa, portanto, é possível calcular em cada nó de uma árvore de segmento a composição de transformações em sua subárvore.

> # Transformação Linear Fracionária de uma Fração Contínua
> Seja  $L(x) = \frac{ax+b}{cx+d}$ . Calcule a representação de fração contínua  $[b_0; b_1, \dots, b_m]$  de  $L(A)$  para  $A=[a_0; a_1, \dots, a_n]$ .
> 
> Isso permite calcular  $A + \frac{p}{q} = \frac{qA + p}{q}$  e  $A \cdot \frac{p}{q} = \frac{p A}{q}$  para qualquer  $\frac{p}{q}$ .
> 
> # Solução
> Como observado anteriormente,  $[a_0; a_1, \dots, a_k] = (L_{a_0} \circ L_{a_1} \circ \dots \circ L_{a_k})(\infty)$ , portanto  $L([a_0; a_1, \dots, a_k]) = (L \circ L_{a_0} \circ L_{a_1} \circ \dots L_{a_k})(\infty)$ .
> 
> Assim, adicionando consequentemente  $L_{a_0}$ ,  $L_{a_1}$  e assim por diante, poderíamos calcular
>$$(L \circ L_{a_0} \circ \dots \circ L_{a_k})(x) = L\left(\frac{p_k x + p_{k-1}}{q_k x + q_{k-1}}\right)=\frac{a_k x + b_k}{c_k x + d_k}.$$ 
> Uma vez que  $L(x)$  é invertível, ela também é monótona em  $x$ . Portanto, para qualquer  $x \geq 0$ , vale que  $L(\frac{p_k x + p_{k-1}}{q_k x + q_{k-1}})$  está entre  $L(\frac{p_k}{q_k}) = \frac{a_k}{c_k}$  e  $L(\frac{p_{k-1}}{q_{k-1}}) = \frac{b_k}{d_k}$ .
> 
>Além disso, para  $x=[a_{k+1}; \dots, a_n]$ , isso é igual a  $L(A)$ . Portanto,  $b_0 = \lfloor L(A) \rfloor$  está entre  $\lfloor L(\frac{p_k}{q_k}) \rfloor$  e  $\lfloor L(\frac{p_{k-1}}{q_{k-1}}) \rfloor$ . Quando eles são iguais, eles também são iguais a  $b_0$ .
>
>Observe que  $L(A) = (L_{b_0} \circ L_{b_1} \circ \dots \circ L_{b_m})(\infty)$ . Sabendo  $b_0$ , podemos compor  $L_{b_0}^{-1}$  com a transformação atual e continuar adicionando  $L_{a_{k+1}}$ ,  $L_{a_{k+2}}$  e assim por diante, procurando novos pisos para concordar, a partir dos quais seríamos capazes de deduzir  $b_1$  e assim por diante até recuperar todos os valores de  $[b_0; b_1, \dots, b_m]$ .

> # Aritmética de Frações Contínuas
> Seja  $A=[a_0; a_1, \dots, a_n]$  e  $B=[b_0; b_1, \dots, b_m]$ . Calcule as representações de fração contínua de  $A+B$  e  $A \cdot B$ .
> 
>Solução A ideia aqui é semelhante ao problema anterior, mas em vez de   $L(x) = \frac{ax+b}{cx+d}$ , você deve considerar a transformação fracionária bilinear   $L(x, y) = \frac{axy+bx+cy+d}{exy+fx+gy+h}$ .
>
>Em vez de   $L(x) \mapsto L(L_{a_k}(x))$ , você mudaria sua transformação atual para   $L(x, y) \mapsto L(L_{a_k}(x), y)$  ou   $L(x, y) \mapsto L(x, L_{b_k}(y))$ .
>
> Então, você verifica se  $\lfloor \frac{a}{e} \rfloor = \lfloor \frac{b}{f} \rfloor = \lfloor \frac{c}{g} \rfloor = \lfloor \frac{d}{h} \rfloor$  e, se todos concordarem, você usa esse valor como  $c_k$  na fração resultante e altera a transformação para$$L(x, y) \mapsto \frac{1}{L(x, y) - c_k}.$$

> # Definição
>Uma fração contínua  $x = [a_0; a_1, \dots]$  é dita ser periódica se  $x = [a_0; a_1, \dots, a_k, x]$  para algum  $k$ .
>
>Uma fração contínua  $x = [a_0; a_1, \dots]$  é dita ser eventualmente periódica se  $x = [a_0; a_1, \dots, a_k, y]$ , onde  $y$  é periódica.

Para  $x = [1; 1, 1, \dots]$ , temos que  $x = 1 + \frac{1}{x}$ , assim  $x^2 = x + 1$ . Existe uma conexão genérica entre frações contínuas periódicas e equações quadráticas. Considere a seguinte equação:
$$ x = [a_0; a_1, \dots, a_k, x].$$ 
Por um lado, essa equação significa que a representação da fração contínua de  $x$  é periódica com o período  $k+1$ .

Por outro lado, usando a fórmula para convergentes, essa equação significa que
$$x = \frac{p_k x + p_{k-1}}{q_k x + q_{k-1}}.$$ 
Ou seja,  $x$  é uma transformação linear fracionária de si mesma. Da equação, segue que  
$x$  é uma raiz da equação de segundo grau:

$$q_k x^2 + (q_{k-1}-p_k)x - p_{k-1} = 0.$$ 
Raciocínio semelhante se aplica a frações contínuas que são eventualmente periódicas, ou seja,  
$x = [a_0; a_1, \dots, a_k, y]$  para  $y=[b_0; b_1, \dots, b_k, y]$ . De fato, da primeira equação derivamos que  
$x = L_0(y)$  e da segunda equação que  $y = L_1(y)$ , onde  $L_0$  e  $L_1$  são transformações lineares fracionárias. Portanto,
$$x = (L_0 \circ L_1)(y) = (L_0 \circ L_1 \circ L_0^{-1})(x).$$ 
Pode-se ainda provar (e foi feito primeiramente por Lagrange) que, para qualquer equação quadrática  $ax^2+bx+c=0$  com coeficientes inteiros, sua solução  $x$  é uma fração contínua eventualmente periódica.

> # Quadratic Irracionalidade
> 
> Encontre a fração contínua de  $\alpha = \frac{x+y\sqrt{n}}{z}$ , onde  $x, y, z, n \in \mathbb Z$  e  $n > 0$  não é um quadrado perfeito.

> # Solução
>Para o  $k$ -ésimo quociente completo  $s_k$  do número, geralmente vale que
$$\alpha = [a_0; a_1, \dots, a_{k-1}, s_k] = \frac{s_k p_{k-1} + p_{k-2}}{s_k q_{k-1} + q_{k-2}}.$$ 
>Portanto,
$$s_k = -\frac{\alpha q_{k-1} - p_{k-1}}{\alpha q_k - p_k} = -\frac{q_{k-1} y \sqrt n + (x q_{k-1} - z p_{k-1})}{q_k y \sqrt n + (xq_k-zp_k)}.$$ 
>Multiplicando o numerador e o denominador por  $(xq_k - zp_k) - q_k y \sqrt n$ , nos livramos de  $\sqrt n$  no denominador, assim, os quocientes completos são da forma
$$s_k = \frac{x_k + y_k \sqrt n}{z_k}.$$. 
>Vamos encontrar  $s_{k+1}$ , assumindo que  $s_k$  é conhecido.
>
>Primeiramente,  $a_k = \lfloor s_k \rfloor = \left\lfloor \frac{x_k + y_k \lfloor \sqrt n \rfloor}{z_k} \right\rfloor$ . Então, 
$$s_{k+1} = \frac{1}{s_k-a_k} = \frac{z_k}{(x_k - z_k a_k) + y_k \sqrt n} = \frac{z_k (x_k - y_k a_k) - y_k z_k \sqrt n}{(x_k - y_k a_k)^2 - y_k^2 n}.$$ 
>Assim, se denotarmos  $t_k = x_k - y_k a_k$ , valerá que
$$\begin{align}x_{k+1} &=& z_k t_k, \\ y_{k+1} &=& -y_k z_k, \\ z_{k+1} &=& t_k^2 - y_k^2 n.\end{align}$$ 
>A coisa boa sobre essa representação é que, se reduzirmos  $x_{k+1}, y_{k+1}, z_{k+1}$  pelo seu maior divisor comum, o resultado será único. Portanto, podemos usá-lo para verificar se o estado atual já se repetiu e também para verificar onde foi o índice anterior que teve esse estado.
>
Abaixo está o código para calcular a representação da fração contínua para  
$\alpha = \sqrt n$ :

```Python
# compute the continued fraction of sqrt(n)
def sqrt(n):
    n0 = math.floor(math.sqrt(n))
    x, y, z = 1, 0, 1
    a = []
    def step(x, y, z):
        a.append((x * n0 + y) // z)
        t = y - a[-1]*z
        x, y, z = -z*x, z*t, t**2 - n*x**2
        g = math.gcd(x, math.gcd(y, z))
        return x // g, y // g, z // g

    used = dict()
    for i in range(n):
        used[x, y, z] = i
        x, y, z = step(x, y, z)
        if (x, y, z) in used:
            return a

Usando a mesma função de passo, mas diferentes  
$x$ ,  
$y$  e  
$z$  iniciais, é possível calcular para  
$\frac{x+y \sqrt{n}}{z}$  arbitrário.

```

># Tavrida NU Akai Contest - Fração Contínua
>
>Você recebe  $x$  e  $k$ , onde  $x$  não é um quadrado perfeito. Seja  $\sqrt x = [a_0; a_1, \dots]$ , encontre  $\frac{p_k}{q_k}=[a_0; a_1, \dots, a_k]$  para  $0 \leq k \leq 10^9$ .

> # Solução
>Após calcular o período de  $\sqrt x$ , é possível calcular  $a_k$  usando a exponenciação binária na transformação linear fracionária induzida pela representação da fração contínua. Para encontrar a transformação resultante, você comprime o período de tamanho  $T$  em uma única transformação e repete  $\lfloor \frac{k-1}{T}\rfloor$  vezes, após o qual você a combina manualmente com as transformações restantes.

```python
x, k = map(int, input().split())

mod = 10**9+7

# combine (A[0]*x + A[1]) / (A[2]*x + A[3]) and (B[0]*x + B[1]) / (B[2]*x + B[3])
def combine(A, B):
    return [t % mod for t in [A[0]*B[0]+A[1]*B[2], A[0]*B[1]+A[1]*B[3], A[2]*B[0]+A[3]*B[2], A[2]*B[1]+A[3]*B[3]]]

A = [1, 0, 0, 1] # (x + 0) / (0*x + 1) = x

a = sqrt(x)

T = len(a) - 1 # período de a

# aplicar ak + 1/x = (ak*x+1)/(1x+0) a (Ax + B) / (Cx + D)
for i in reversed(range(1, len(a))):
    A = combine([a[i], 1, 1, 0], A)

def bpow(A, n):
    return [1, 0, 0, 1] if not n else combine(A, bpow(A, n-1)) if n % 2 else bpow(combine(A, A), n // 2)


C = (0, 1, 0, 0) # = 1 / 0
while k % T:
    i = k % T
    C = combine([a[i], 1, 1, 0], C)
    k -= 1

C = combine(bpow(A, k // T), C)
C = combine([a[0], 1, 1, 0], C)
print(str(C[1]) + '/' + str(C[3]))
```

## Interpretação geométrica
Seja  $\vec r_k = (q_k;p_k)$  para o convergente  $r_k = \frac{p_k}{q_k}$ . Então, a seguinte recorrência é válida: 
$$\vec r_k = a_k \vec r_{k-1} + \vec r_{k-2}.$$ 
Seja  $\vec r = (1;r)$ . Então, cada vetor  $(x;y)$  corresponde ao número que é igual ao seu coeficiente angular  $\frac{y}{x}$ .

Com a noção de produto pseudoscalar  $(x_1;y_1) \times (x_2;y_2) = x_1 y_2 - x_2 y_1$ , pode ser mostrado (veja a explicação abaixo) que
$$s_k = -\frac{\vec r_{k-2} \times \vec r}{\vec r_{k-1} \times \vec r} = \left|\frac{\vec r_{k-2} \times \vec r}{\vec r_{k-1} \times \vec r}\right|.$$ 
A última equação é devido ao fato de que  $r_{k-1}$  e $r_{k-2}$  estão em lados diferentes de  $r$ , assim os produtos pseudoscalares de  $\vec r_{k-1}$  e  $\vec r_{k-2}$  com  $\vec r$  têm sinais distintos. Com  $a_k = \lfloor s_k \rfloor$  em mente, a fórmula para  $\vec r_k$  agora parece 
$$\vec r_k = \vec r_{k-2} + \left\lfloor \left| \frac{\vec r \times \vec r_{k-2}}{\vec r \times \vec r_{k-1}}\right|\right\rfloor \vec r_{k-1}.$$ 
Note que  $\vec r_k \times r = (q;p) \times (1;r) = qr - p$ , assim   
$$a_k = \left\lfloor \left| \frac{q_{k-1}r-p_{k-1}}{q_{k-2}r-p_{k-2}} \right| \right\rfloor.$$

> # Explicação
	Como já observamos,  $a_k = \lfloor s_k \rfloor$ , onde  $s_k = [a_k; a_{k+1}, a_{k+2}, \dots]$ . Por outro lado, da recorrência convergente, derivamos que 
	$$r = [a_0; a_1, \dots, a_{k-1}, s_k] = \frac{s_k p_{k-1} + p_{k-2}}{s_k q_{k-1} + q_{k-2}}.$$
	Na forma vetorial, reescreve-se como $$\vec r \parallel s_k \vec r_{k-1} + \vec r_{k-2},$$
	significando que  $\vec r$  e  $s_k \vec r_{k-1} + \vec r_{k-2}$  são colineares (ou seja, têm o mesmo coeficiente angular). Tomando o produto pseudoscalar de ambas as partes com  $\vec r$ , obtemos  $$0 = s_k (\vec r_{k-1} \times \vec r) + (\vec r_{k-2} \times \vec r),$$ 
	o que nos dá a fórmula final $$s_k = -\frac{\vec r_{k-2} \times \vec r}{\vec r_{k-1} \times \vec r}.$$

> # Algoritmo de esticamento do nariz
>	Cada vez que você adiciona  $\vec r_{k-1}$  ao vetor  $\vec p$ , o valor de  $\vec p \times \vec r$  é aumentado por  	$\vec r_{k-1} \times \vec r$ .
>	Assim,  $a_k=\lfloor s_k \rfloor$  é o número máximo inteiro de vetores  $\vec r_{k-1}$  que podem ser adicionados a  $\vec r_{k-2}$  sem alterar o sinal do produto vetorial com $\vec r$ .
>	Em outras palavras,  $a_k$  é o número máximo inteiro de vezes que você pode adicionar  $\vec r_{k-1}$  a  $\vec r_{k-2}$  sem cruzar a linha definida por  $\vec r$ :
>	![[Pasted image 20240129153352.png]]
>	Convergentes de  $r=\frac{7}{9}=[0;1,3,2]$ . Semiconvergentes correspondem a pontos intermediários entre as setas cinzas.
>	Na imagem acima,  $\vec r_2 = (4;3)$  é obtido adicionando repetidamente  $\vec r_1 = (1;1)$  a  $\vec r_0 = (1;0)$ .
>	Quando não é possível adicionar mais  $\vec r_1$  a  $\vec r_0$  sem cruzar a linha  $y=rx$ , vamos para o outro lado e adicionamos repetidamente  $\vec r_2$  a  $\vec r_1$  para obter  $\vec r_3 = (9;7)$ .
>	Este procedimento gera vetores exponencialmente mais longos, que se aproximam da linha.
>	Por esta propriedade, o procedimento de geração de vetores convergentes consecutivos foi apelidado de algoritmo de esticamento do nariz por Boris Delaunay.

