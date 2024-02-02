Em alguns casos, é necessário considerar fórmulas complexas módulo algum primo $p$, contendo fatoriais tanto no numerador quanto no denominador, como as que você encontra na fórmula para coeficientes binomiais. Consideramos o caso em que $p$ é relativamente pequeno. Este problema só faz sentido quando os fatoriais aparecem tanto no numerador quanto no denominador de frações. Caso contrário, $p!$ e os termos subsequentes serão reduzidos a zero. Mas nas frações, os fatores de $p$ podem ser cancelados, e a expressão resultante será diferente de zero módulo $p$.

Assim, formalmente a tarefa é: Você quer calcular $n! \bmod p$, sem levar em conta todos os múltiplos fatores de $p$ que aparecem no fatorial. Imagine que você escreva a fatoração prima de $n!$, remova todos os fatores $p$, e compute o produto módulo $p$. Denotaremos este fatorial modificado com $n!_{\%p}$. Por exemplo,

$7!_{\%p} \equiv 1 \cdot 2 \cdot \underbrace{1}_{3} \cdot 4 \cdot 5 \underbrace{2}_{6} \cdot 7 \equiv 2 \bmod 3$.

Aprender a calcular efetivamente este fatorial modificado nos permite calcular rapidamente o valor das várias fórmulas combinatórias (por exemplo, coeficientes binomiais).

## Algoritmo
Vamos escrever este fatorial modificado explicitamente.

$$
\begin{eqnarray}
n!_{\%p} &=& 1 \cdot 2 \cdot 3 \cdot \ldots \cdot (p-2) \cdot (p-1) \cdot \underbrace{1}_{p} \cdot (p+1) \cdot (p+2) \cdot \ldots \cdot (2p-1) \cdot \underbrace{2}_{2p} \\\
 & &\quad \cdot (2p+1) \cdot \ldots \cdot (p^2-1) \cdot \underbrace{1}_{p^2} \cdot (p^2 +1) \cdot \ldots \cdot n \pmod{p} \\\\
&=& 1 \cdot 2 \cdot 3 \cdot \ldots \cdot (p-2) \cdot (p-1) \cdot \underbrace{1}_{p} \cdot 1 \cdot 2 \cdot \ldots \cdot (p-1) \cdot \underbrace{2}_{2p} \cdot 1 \cdot 2 \\\
& &\quad \cdot \ldots \cdot (p-1) \cdot \underbrace{1}_{p^2} \cdot 1 \cdot 2 \cdot \ldots \cdot (n \bmod p) \pmod{p}
\end{eqnarray}

$$

Claramente, pode-se ver que o fatorial é dividido em vários blocos de mesmo comprimento, exceto pelo último.
$$
\begin{eqnarray}
n!_{\%p}&=& \underbrace{1 \cdot 2 \cdot 3 \cdot \ldots \cdot (p-2) \cdot (p-1) \cdot 1}_{1\text{st}} \cdot \underbrace{1 \cdot 2 \cdot 3 \cdot \ldots \cdot (p-2) \cdot (p-1) \cdot 2}_{2\text{nd}} \cdot \ldots \\\\
& & \cdot \underbrace{1 \cdot 2 \cdot 3 \cdot \ldots \cdot (p-2) \cdot (p-1) \cdot 1}_{p\text{th}} \cdot \ldots \cdot \quad \underbrace{1 \cdot 2 \cdot \cdot \ldots \cdot (n \bmod p)}_{\text{tail}} \pmod{p}.
\end{eqnarray}
$$
A parte principal dos blocos é fácil de contar - é apenas  $(p-1)!\ \mathrm{mod}\ p$ . Podemos calcular isso programaticamente ou simplesmente aplicar o teorema de Wilson, que afirma que  $(p-1)! \bmod p = -1$  para qualquer número primo  $p$ .

Temos exatamente  $\lfloor \frac{n}{p} \rfloor$  desses blocos, portanto precisamos elevar  $-1$  à potência de  $\lfloor \frac{n}{p} \rfloor$ . Isso pode ser feito em tempo logarítmico usando Exponenciação Binária; no entanto, você também pode notar que o resultado alternará entre  $-1$  e  $1$ , então só precisamos olhar para a paridade do expoente e multiplicar por  $-1$  se a paridade for ímpar. E em vez de uma multiplicação, também podemos apenas subtrair o resultado atual de  $p$ .

O valor do último bloco parcial pode ser calculado separadamente em  
$O(p)$ .

Isso deixa apenas o último elemento de cada bloco. Se escondermos os elementos já tratados, podemos ver o seguinte padrão:

$$n!_{\%p} = \underbrace{ \ldots \cdot 1 } \cdot \underbrace{ \ldots \cdot 2} \cdot \ldots \cdot \underbrace{ \ldots \cdot (p-1)} \cdot \underbrace{ \ldots \cdot 1 } \cdot \underbrace{ \ldots \cdot 1} \cdot \underbrace{ \ldots \cdot 2} \cdots$$

Isso novamente é um fatorial modificado, mas com uma dimensão muito menor. É  
$\lfloor n / p \rfloor !_{\%p}$ .

Assim, durante o cálculo do fatorial modificado  $n\!_{\%p}$ , realizamos  $O(p)$  operações e restamos com o cálculo de  $\lfloor n / p \rfloor !_{\%p}$ . Temos uma fórmula recursiva. A profundidade da recursão é  $O(\log_p n)$  e, portanto, o comportamento assintótico completo do algoritmo é  $O(p \log_p n)$ .

Observe que, se você pré-calcular os fatoriais  $0!,~ 1!,~ 2!,~ \dots,~ (p-1)!$  módulo  $p$ , então a complexidade será apenas  $O(\log_p n)$ .


## Implementação
Não precisamos de recursão porque este é um caso de recursão de cauda e, portanto, pode ser facilmente implementado usando iteração. Na seguinte implementação, pré-calculamos os fatoriais  $0!,~ 1!,~ \dots,~ (p-1)!$  e, assim, temos um tempo de execução de  $O(p + \log_p n)$ . Se você precisar chamar a função várias vezes, pode fazer o pré-cálculo fora da função e calcular  $n!_{\%p}$  em  $O(\log_p n)$  tempo.

```cpp
int factmod(int n, int p) {
    vector<int> f(p);
    f[0] = 1;
    for (int i = 1; i < p; i++)
        f[i] = f[i-1] * i % p;

    int res = 1;
    while (n > 1) {
        if ((n/p) % 2)
            res = p - res;
        res = res * f[n%p] % p;
        n /= p;
    }
    return res;
}
```

Alternativamente, se você tiver limitação de memória e não puder armazenar todos os fatoriais, também pode apenas lembrar os fatoriais necessários, ordená-los e depois calculá-los de uma vez, computando os fatoriais  $0!,~ 1!,~ 2!,~ \dots,~ (p-1)!$  em um loop sem armazená-los explicitamente.
## Multiplicity of  $p$

Se quisermos calcular um coeficiente binomial módulo  $p$ , então precisamos adicionalmente da multiplicidade do  $p$  em  $n$ , ou seja, o número de vezes que  $p$  ocorre na fatoração prima de  $n$ , ou o número de vezes que apagamos  $p$  durante o cálculo do fatorial modificado.

A fórmula de Legendre nos dá uma maneira de calcular isso em $O(\log_p n)$  tempo. A fórmula fornece a multiplicidade  $\nu_p$  como:
$$\nu_p(n!) = \sum_{i=1}^{\infty} \left\lfloor \frac{n}{p^i} \right\rfloor$$ 
Assim, obtemos a implementação:

```cpp
int multiplicity_factorial(int n, int p) {
    int count = 0;
    do {
        n /= p;
        count += n;
    } while (n);
    return count;
}
```

Esta fórmula pode ser facilmente comprovada usando as mesmas ideias que utilizamos nas seções anteriores. Remova todos os elementos que não contêm o fator  $p$ . Isso deixa  $\lfloor n/p \rfloor$  elementos restantes. Se removermos o fator  $p$  de cada um deles, obtemos o produto  $1 \cdot 2 \cdots \lfloor n/p \rfloor = \lfloor n/p \rfloor !$ , e novamente temos uma recursão.