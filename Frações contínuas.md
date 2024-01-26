

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
O desvio de  $r_k = \frac{p_k}{q_k}$  em relação a  
$r$  pode ser geralmente estimado como

 
$$\left|\frac{p_k}{q_k}-r\right| \leq \frac{1}{q_k q_{k+1}} \leq \frac{1}{q_k^2}.$$ 
Multiplicando ambos os lados por  
$q_k$ , obtemos uma estimativa alternativa:

 
$$|p_k - q_k r| \leq \frac{1}{q_{k+1}}.$$ 
A partir da recorrência acima, segue-se que  
$q_k$  cresce pelo menos tão rapidamente quanto os números de Fibonacci.

Na imagem abaixo, você pode ver a visualização de como os convergentes  
$r_k$  se aproximam de  
$r=\frac{1+\sqrt 5}{2}$ :

 

A linha pontilhada azul representa  
$r=\frac{1+\sqrt 5}{2}$ . Os convergentes ímpares se aproximam de cima e os convergentes pares se aproximam de baixo.