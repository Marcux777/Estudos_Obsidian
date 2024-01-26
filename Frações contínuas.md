

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

## Árvores de frações contínuas¶
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

### Comparando frações contínuas

Você recebe  $A=[a_0; a_1, \dots, a_n]$  e  $B=[b_0; b_1, \dots, b_m]$ . Qual fração é menor?

#### Solução
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

