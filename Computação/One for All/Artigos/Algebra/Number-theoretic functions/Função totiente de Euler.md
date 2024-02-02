
A função totiente de Euler, também conhecida como função phi  $\phi (n)$ , conta o número de inteiros entre 1 e  $n$  inclusivo, que são coprimos a  $n$ . Dois números são coprimos se o maior divisor comum deles for igual a  $1$  ( $1$  é considerado coprimo a qualquer número).

Aqui estão os valores de  $\phi(n)$  para os primeiros inteiros positivos:
 
$$\begin{array}{|c|c|c|c|c|c|c|c|c|c|c|c|c|c|c|c|c|c|c|c|c|c|} \hline n & 1 & 2 & 3 & 4 & 5 & 6 & 7 & 8 & 9 & 10 & 11 & 12 & 13 & 14 & 15 & 16 & 17 & 18 & 19 & 20 & 21 \\\\ \hline \phi(n) & 1 & 1 & 2 & 2 & 4 & 2 & 6 & 4 & 6 & 4 & 10 & 4 & 12 & 6 & 8 & 8 & 16 & 6 & 18 & 8 & 12 \\\\ \hline \end{array}$$ 
## Propriedades
As seguintes propriedades da função totiente de Euler são suficientes para calculá-la para qualquer número:

- Se  $p$  é um número primo, então  $\gcd(p, q) = 1$  para todos  $1 \le q < p$ . Portanto, temos:
 
$$\phi (p) = p - 1.$$ 
- Se  $p$  é um número primo e  $k \ge 1$ , então existem exatamente  $p^k / p$  números entre  $1$  e  $p^k$  que são divisíveis por  $p$ . O que nos dá:
 
$$\phi(p^k) = p^k - p^{k-1}.$$ 
- Se  $a$  e  $b$  são primos entre si, então:
$$\phi(a b) = \phi(a) \cdot \phi(b).$$ 
Essa relação não é trivial de se ver. Ela decorre do teorema chinês do resto. O teorema chinês do resto garante que, para cada  $0 \le x < a$  e cada  $0 \le y < b$ , existe um único  $0 \le z < a b$  com  $z \equiv x \pmod{a}$  e  $z \equiv y \pmod{b}$ . Não é difícil mostrar que  $z$  é coprimo a  $a b$  se e somente se  $x$  é coprimo a  $a$  e  $y$  é coprimo a  $b$ . Portanto, a quantidade de inteiros coprimos a  $a b$  é igual ao produto das quantidades de  $a$  e $b$ .

- Em geral, para  $a$  e  $b$  não coprimos, a equação
 
$$\phi(ab) = \phi(a) \cdot \phi(b) \cdot \dfrac{d}{\phi(d)}$$ 
com  $d = \gcd(a, b)$  é válida.

Assim, usando as três primeiras propriedades, podemos calcular  $\phi(n)$  através da fatoração de  $n$  (decomposição de  $n$  em um produto de seus fatores primos). Se  $n = {p_1}^{a_1} \cdot {p_2}^{a_2} \cdots {p_k}^{a_k}$ , onde  $p_i$  são fatores primos de  $n$ ,
 
 
$$\begin{align} \phi (n) &= \phi ({p_1}^{a_1}) \cdot \phi ({p_2}^{a_2}) \cdots \phi ({p_k}^{a_k}) \\\\ &= \left({p_1}^{a_1} - {p_1}^{a_1 - 1}\right) \cdot \left({p_2}^{a_2} - {p_2}^{a_2 - 1}\right) \cdots \left({p_k}^{a_k} - {p_k}^{a_k - 1}\right) \\\\ &= p_1^{a_1} \cdot \left(1 - \frac{1}{p_1}\right) \cdot p_2^{a_2} \cdot \left(1 - \frac{1}{p_2}\right) \cdots p_k^{a_k} \cdot \left(1 - \frac{1}{p_k}\right) \\\\ &= n \cdot \left(1 - \frac{1}{p_1}\right) \cdot \left(1 - \frac{1}{p_2}\right) \cdots \left(1 - \frac{1}{p_k}\right) \end{align}$$

## Implementation

Aqui está uma implementação usando fatoração em  $O(\sqrt{n})$ :
```c++
int phi(int n) {
    int result = n;
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            while (n % i == 0)
                n /= i;
            result -= result / i;
        }
    }
    if (n > 1)
        result -= result / n;
    return result;
}
```


## Função totiente de Euler de $1 a  n$ em  $O(n loglogn)$

Se precisarmos de todos os totientes de todos os números entre  $1$  e  $n$ , então fatorar todos os números  
$n$  não é eficiente. Podemos usar a mesma ideia do [[Crivo de Eratóstenes]]. Ainda se baseia na propriedade mostrada acima, mas em vez de atualizar o resultado temporário para cada fator primo para cada número, encontramos todos os números primos e para cada um atualizamos os resultados temporários de todos os números que são divisíveis por esse número primo.

Como essa abordagem é basicamente idêntica ao Crivo de Eratóstenes, a complexidade também será a mesma:  $O(n \log \log n)$ 

```c++
void phi_1_to_n(int n) {
    vector<int> phi(n + 1);
    for (int i = 0; i <= n; i++)
        phi[i] = i;

    for (int i = 2; i <= n; i++) {
        if (phi[i] == i) {
            for (int j = i; j <= n; j += i)
                phi[j] -= phi[j] / i;
        }
    }
}
```


## Propriedade da soma dos divisores

Esta interessante propriedade foi estabelecida por Gauss:
 
$$ \sum_{d|n} \phi{(d)} = n$$ 
Aqui a soma é sobre todos os divisores positivos  
$d$  de  $n$ .
Por exemplo, os divisores de 10 são 1, 2, 5 e 10. Portanto  $\phi{(1)} + \phi{(2)} + \phi{(5)} + \phi{(10)} = 1 + 1 + 4 + 4 = 10$ .

## Encontrando o totiente de 1 a n usando a propriedade da soma dos divisores

A propriedade da soma dos divisores também nos permite calcular o totiente de todos os números entre 1 e  $n$ . Esta implementação é um pouco mais simples do que a implementação anterior baseada no Crivo de Eratóstenes, no entanto, tem uma complexidade um pouco pior:  $O(n \log n)$ 

```c++
void phi_1_to_n(int n) {
    vector<int> phi(n + 1);
    phi[0] = 0;
    phi[1] = 1;
    for (int i = 2; i <= n; i++)
        phi[i] = i - 1;

    for (int i = 2; i <= n; i++)
        for (int j = 2 * i; j <= n; j += i)
              phi[j] -= phi[i];
}
```

# [[Aplicação no teorema de Euler]]
A propriedade mais famosa e importante da função totiente de Euler é expressa no teorema de Euler:
$$a^{\phi(m)} \equiv 1 \pmod m \quad \text{se } a \text{ e } m \text{ são primos entre si.}$$ 
No caso particular em que  $m$  é primo, o teorema de Euler se transforma no pequeno teorema de Fermat:

$$a^{m - 1} \equiv 1 \pmod m$$ 
O teorema de Euler e a função totiente de Euler ocorrem com bastante frequência em aplicações práticas, por exemplo, ambos são usados para calcular o inverso multiplicativo modular.

Como consequência imediata, também obtemos a equivalência:

$$a^n \equiv a^{n \bmod \phi(m)} \pmod m$$ 
Isso permite calcular  $x^n \bmod m$  para $n$  muito grande, especialmente se  $n$  é o resultado de outro cálculo, pois permite calcular  $n$  sob um módulo.

# Teoria dos Grupos

$\phi(n)$  é a ordem do grupo multiplicativo mod n  $(\mathbb Z / n\mathbb Z)^\times$ , ou seja, o grupo das unidades (elementos com inversos multiplicativos). Os elementos com inversos multiplicativos são precisamente aqueles coprimos a  $n$ .

A ordem multiplicativa de um elemento  $a$  mod  $n$ , denotada por $\operatorname{ord}_n(a)$ , é o menor $k>0$  tal que  $a^k \equiv 1 \pmod m$ .  $\operatorname{ord}_n(a)$  é o tamanho do subgrupo gerado por  $a$ , então pelo Teorema de Lagrange, a ordem multiplicativa de qualquer  $a$  deve dividir $\phi(n)$ . Se a ordem multiplicativa de  $a$  é  $\phi(n)$ , a maior possível, então  $a$  é uma raiz primitiva e o grupo é cíclico por definição.

# Generalização

Existe uma versão menos conhecida da última equivalência, que permite calcular  
$x^n \bmod m$  de forma eficiente para  $x$  e  $m$  não coprimos. Para  $x, m$  arbitrários e  $n \geq \log_2 m$ :

 
$$x^{n}\equiv x^{\phi(m)+[n \bmod \phi(m)]} \mod m$$ 
Prova:

Sejam  $p_1, \dots, p_t$  os divisores primos comuns de $x$  e  $m$ , e  $k_i$  seus expoentes em  $m$ . Com esses, definimos  $a = p_1^{k_1} \dots p_t^{k_t}$ , o que faz  $\frac{m}{a}$  ser coprimo a  $x$ . E seja  $k$  o menor número tal que  $a$  divide  $x^k$ . Supondo  $n \ge k$ , podemos escrever:
$$\begin{align}x^n \bmod m &= \frac{x^k}{a}ax^{n-k}\bmod m \\ &= \frac{x^k}{a}\left(ax^{n-k}\bmod m\right) \bmod m \\ &= \frac{x^k}{a}\left(ax^{n-k}\bmod a \frac{m}{a}\right) \bmod m \\ &=\frac{x^k}{a} a \left(x^{n-k} \bmod \frac{m}{a}\right)\bmod m \\ &= x^k\left(x^{n-k} \bmod \frac{m}{a}\right)\bmod m \end{align}$$ 
A equivalência entre a terceira e a quarta linha segue do fato de que  $ab \bmod ac = a(b \bmod c)$ . De fato, se  $b = cd + r$  com  $r < c$ , então  $ab = acd + ar$  com  $ar < ac$ .

Como  $x$  e  $\frac{m}{a}$  são coprimos, podemos aplicar o teorema de Euler e obter a fórmula eficiente (já que  $k$  é muito pequeno; de fato $k \le \log_2 m$ ):
$$x^n \bmod m = x^k\left(x^{n-k \bmod \phi(\frac{m}{a})} \bmod \frac{m}{a}\right)\bmod m.$$ 
Esta fórmula é difícil de aplicar, mas podemos usá-la para analisar o comportamento de  $x^n \bmod m$ . Podemos ver que a sequência de potências  
$(x^1 \bmod m, x^2 \bmod m, x^3 \bmod m, \dots)$  entra em um ciclo de comprimento  $\phi\left(\frac{m}{a}\right)$  após os primeiros  $k$  (ou menos) elementos. $\phi\left(\frac{m}{a}\right)$  divide  $\phi(m)$  (porque
$a$  e $\frac{m}{a}$  são coprimos temos $\phi(a) \cdot \phi\left(\frac{m}{a}\right) = \phi(m)$ ), portanto, também podemos dizer que o período tem comprimento  $\phi(m)$ . E como $\phi(m) \ge \log_2 m \ge k$ , podemos concluir a fórmula desejada, muito mais simples:
$$ x^n \equiv x^{\phi(m)} x^{(n - \phi(m)) \bmod \phi(m)} \bmod m \equiv x^{\phi(m)+[n \bmod \phi(m)]} \mod m.$$


