
Neste artigo, listamos vários algoritmos para fatorar inteiros, cada um deles pode ser tanto rápido quanto lento (alguns mais lentos que outros) dependendo de sua entrada.

Observe que, se o número que você deseja fatorar é na verdade um número primo, a maioria dos algoritmos, especialmente o algoritmo de fatoração de Fermat, p-1 de Pollard, o algoritmo rho de Pollard será muito lento. Portanto, faz sentido realizar um teste de primalidade probabilístico (ou um determinístico rápido) antes de tentar fatorar o número.

## Divisão de Teste

Este é o algoritmo mais básico para encontrar uma fatoração prima.

Dividimos por cada divisor possível  $d$ . Podemos notar que é impossível que todos os fatores primos de um número composto  $n$  sejam maiores que  $\sqrt{n}$ . Portanto, só precisamos testar os divisores  $2 \le d \le \sqrt{n}$ , o que nos dá a fatoração prima em $O(\sqrt{n})$ . (Este é o [[tempo pseudo-polinomial]], ou seja, polinomial no valor da entrada, mas exponencial no número de bits da entrada.)

O menor divisor tem que ser um número primo. Removemos o fator do número e repetimos o processo. Se não conseguirmos encontrar nenhum divisor no intervalo  
$[2; \sqrt{n}]$ , então o próprio número deve ser primo.

```cpp
vector<long long> trial_division1(long long n) {
    vector<long long> factorization;
    for (long long d = 2; d * d <= n; d++) {
        while (n % d == 0) {
            factorization.push_back(d);
            n /= d;
        }
    }
    if (n > 1)
        factorization.push_back(n);
    return factorization;
}
```
Este é um exemplo de implementação do algoritmo de divisão de teste para encontrar a fatoração prima de um número. Ele divide o número por cada divisor possível e verifica se o número é divisível por ele. Se for, o divisor é adicionado à fatoração e o número é dividido por ele. O processo é repetido até que não se possa encontrar mais divisores. Se o número restante for maior que 1, ele é adicionado à fatoração, pois deve ser um número primo. O algoritmo tem complexidade de tempo $O(\sqrt{n})$, o que o torna eficiente para números pequenos, mas menos eficiente para números muito grandes.

### Fatoração por Roda

Esta é uma otimização da divisão de teste. A ideia é a seguinte. Uma vez que sabemos que o número não é divisível por 2, não precisamos verificar todos os outros números pares. Isso nos deixa com apenas  
$50\%$  dos números para verificar. Depois de verificar 2, podemos simplesmente começar com 3 e pular todos os outros números.

```cpp
vector<long long> trial_division2(long long n) {
    vector<long long> factorization;
    while (n % 2 == 0) {
        factorization.push_back(2);
        n /= 2;
    }
    for (long long d = 3; d * d <= n; d += 2) {
        while (n % d == 0) {
            factorization.push_back(d);
            n /= d;
        }
    }
    if (n > 1)
        factorization.push_back(n);
    return factorization;
}
```
Este método pode ser estendido. Se o número não for divisível por 3, também podemos ignorar todos os outros múltiplos de 3 nos cálculos futuros. Então, só precisamos verificar os números  
$5, 7, 11, 13, 17, 19, 23, \dots$ . Podemos observar um padrão desses números restantes. Precisamos verificar todos os números com  
$d \bmod 6 = 1$  e  
$d \bmod 6 = 5$ . Então, isso nos deixa com apenas  
$33.3\%$  por cento dos números para verificar. Podemos implementar isso verificando os primos 2 e 3 primeiro, e então começar a verificar com 5 e alternativamente pular 1 ou 3 números.

Podemos estender isso ainda mais. Aqui está uma implementação para o número primo 2, 3 e 5. É conveniente usar uma matriz para armazenar quanto temos que pular.

```cpp
vector<long long> trial_division3(long long n) {
    vector<long long> factorization;
    for (int d : {2, 3, 5}) {
        while (n % d == 0) {
            factorization.push_back(d);
            n /= d;
        }
    }
    static array<int, 8> increments = {4, 2, 4, 2, 4, 6, 2, 6};
    int i = 0;
    for (long long d = 7; d * d <= n; d += increments[i++]) {
        while (n % d == 0) {
            factorization.push_back(d);
            n /= d;
        }
        if (i == 8)
            i = 0;
    }
    if (n > 1)
        factorization.push_back(n);
    return factorization;
}
```
Se estendermos isso ainda mais com mais primos, podemos até alcançar melhores porcentagens. No entanto, as listas de pulo também ficarão muito maiores.

### Primos Pré-computados

Estender a fatoração por roda com mais e mais primos deixará exatamente os primos para verificar. Portanto, uma boa maneira de verificar é apenas pré-computar todos os números primos com o [[Crivo de Eratóstenes]] até  $\sqrt{n}$  e testá-los individualmente.

```cpp
vector<long long> primes;

vector<long long> trial_division4(long long n) {
    vector<long long> factorization;
    for (long long d : primes) {
        if (d * d > n)
            break;
        while (n % d == 0) {
            factorization.push_back(d);
            n /= d;
        }
    }
    if (n > 1)
        factorization.push_back(n);
    return factorization;
}
```



## Método de Fatoração de Fermat

Podemos escrever um número composto ímpar  $n = p \cdot q$  como a diferença de dois quadrados  $n = a^2 - b^2$ :
$$n = \left(\frac{p + q}{2}\right)^2 - \left(\frac{p - q}{2}\right)^2$$ 
O método de fatoração de Fermat tenta explorar esse fato, adivinhando o primeiro quadrado  $a^2$ , e verifica se a parte restante  $b^2 = a^2 - n$  também é um número quadrado. Se for, então encontramos os fatores  $a - b$  e  $a + b$  de  $n$ .
```cpp
int fermat(int n) {
    int a = ceil(sqrt(n));
    int b2 = a*a - n;
    int b = round(sqrt(b2));
    while (b * b != b2) {
        a = a + 1;
        b2 = a*a - n;
        b = round(sqrt(b2));
    }
    return a - b;
}
```
Note que, este método de fatoração pode ser muito rápido, se a diferença entre os dois fatores  $p$  e  $q$  for pequena. O algoritmo funciona em  $O(|p - q|)$  tempo. No entanto, como é muito lento, uma vez que os fatores estão distantes, raramente é usado na prática.

No entanto, ainda existem um grande número de otimizações para essa abordagem. Por exemplo, ao olhar para os quadrados  $a^2$  módulo um número pequeno fixo, você pode notar que não precisa olhar para certos valores  $a$ , pois eles não podem produzir um número quadrado  $a^2 - n$ .

## Método  $p - 1$  de Pollard

É muito provável que pelo menos um fator de um número seja  $B$ -powersmooth para pequenos  $B$ .  
$B$ -powersmooth significa que cada potência prima  $d^k$  que divide  $p-1$  é no máximo  $B$ . Por exemplo, a fatoração prima de  $4817191$  é $1303 \cdot 3697$ . E os fatores são respectivamente  $31$ -powersmooth e $16$ -powersmooth, porque  
$1303 - 1 = 2 \cdot 3 \cdot 7 \cdot 31$  e  $3697 - 1 = 2^4 \cdot 3 \cdot 7 \cdot 11$ . Em 1974, John Pollard inventou um método para extrair fatores  $B$ -powersmooth de um número composto.

A ideia vem do [[pequeno teorema de Fermat]]. Seja uma fatoração de  $n$  como  $n = p \cdot q$ . Ele diz que se  $a$  é coprimo com  $p$ , a seguinte afirmação é válida:

$$a^{p - 1} \equiv 1 \pmod{p}$$ 
Isso também significa que
$$a^{(p - 1)^k} \equiv a^{k \cdot (p - 1)} \equiv 1 \pmod{p}.$$ 
Portanto, para qualquer $M$  com  $p - 1 ~|~ M$  sabemos que  $a^M \equiv 1$ . Isso significa que  $a^M - 1 = p \cdot r$ , e por causa disso também  $p ~|~ \gcd(a^M - 1, n)$ .

Portanto, se  $p - 1$  para um fator $p$  de  $n$  divide  $M$ , podemos extrair um fator usando o [algoritmo de Euclides](obsidian://open?vault=Estudos_Obsidian&file=Computa%C3%A7%C3%A3o%2FOne%20for%20All%2FArtigos%2FAlgebra%2FAlgoritmo%20de%20Euclides%20para%20calcular%20o%20maior%20divisor%20comum%2FAlgoritmo%20-%20Algoritmo%20de%20Euclides%20para%20calcular%20o%20maior%20divisor%20comum).

É claro que o menor  $M$  que é um múltiplo de todo número  $B$ -powersmooth é  $\text{lcm}(1,~2~,3~,4~,~\dots,~B)$ . Ou alternativamente:
 
$$M = \prod_{\text{primo } q \le B} q^{\lfloor \log_q B \rfloor}$$ 
Note que, se  $p-1$  divide  $M$  para todos os fatores primos  $p$  de  $n$ , então  $\gcd(a^M - 1, n)$  será apenas  $n$ . Neste caso, não recebemos um fator. Portanto, tentaremos realizar o  
$\gcd$  várias vezes, enquanto calculamos  $M$ .

Alguns números compostos não têm fatores  
$B$ -powersmooth para pequenos  
$B$ . Por exemplo, os fatores do número composto  
$100~000~000~000~000~493 = 763~013 \cdot 131~059~365~961$  são  $190~753$ -powersmooth e  
$1~092~161~383$ -powersmooth. Teríamos que escolher $B >= 190~753$  para fatorar o número.

Na seguinte implementação, começamos com  $B = 10$  e aumentamos  $B$  após cada iteração.

```cpp
long long pollards_p_minus_1(long long n) {
    int B = 10;
    long long g = 1;
    while (B <= 1000000 && g < n) {
        long long a = 2 + rand() %  (n - 3);
        g = gcd(a, n);
        if (g > 1)
            return g;

        // compute a^M
        for (int p : primes) {
            if (p >= B)
                continue;
            long long p_power = 1;
            while (p_power * p <= B)
                p_power *= p;
            a = power(a, p_power, n);

            g = gcd(a - 1, n);
            if (g > 1 && g < n)
                return g;
        }
        B *= 2;
    }
    return 1;
}
```
Note que, este é um algoritmo probabilístico. Pode acontecer que o algoritmo não encontre um fator.

A complexidade é  $O(B \log B \log^2 n)$  por iteração.

## Algoritmo Rho de Pollard

Outro algoritmo de fatoração de John Pollard.

Deixe a fatoração prima de um número ser  $n = p q$ . O algoritmo olha para uma sequência pseudo-aleatória  $\{x_i\} = \{x_0,~f(x_0),~f(f(x_0)),~\dots\}$  onde  $f$  é uma função polinomial, geralmente  $f(x) = (x^2 + c) \bmod n$  é escolhida com  $c = 1$ .

Na verdade, não estamos muito interessados na sequência  $\{x_i\}$ , estamos mais interessados na sequência  $\{x_i \bmod p\}$ . Como  $f$  é uma função polinomial e todos os valores estão no intervalo  $[0;~p)$ , esta sequência começará a se repetir mais cedo ou mais tarde. O paradoxo do aniversário sugere que o número esperado de elementos é  $O(\sqrt{p})$  até que a repetição comece. Se  
$p$  for menor que  $\sqrt{n}$ , a repetição começará muito provavelmente em  $O(\sqrt[4]{n})$ .

Aqui está uma visualização de tal sequência  $\{x_i \bmod p\}$  com  $n = 2206637$ ,  $p = 317$ ,  $x_0 = 2$  e  $f(x) = x^2 + 1$ . A partir da forma da sequência, você pode ver claramente por que o algoritmo é chamado de algoritmo rho de Pollard.

![[Pasted image 20240119130130.png]]


Ainda há uma grande questão em aberto. Ainda não sabemos  $p$ , então como podemos argumentar sobre a sequência  $\{x_i \bmod p\}$ ?

Na verdade, é bem fácil. Há um ciclo na sequência  $\{x_i \bmod p\}_{i \le j}$  se e somente se existem dois índices  $s, t \le j$  tais que  $x_s \equiv x_t \bmod p$ . Esta equação pode ser reescrita como  $x_s - x_t \equiv 0 \bmod p$  que é o mesmo que  $p ~|~ \gcd(x_s - x_t, n)$ .

Portanto, se encontrarmos dois índices  $s$  e  $t$  com  $g = \gcd(x_s - x_t, n) > 1$ , encontramos um ciclo e também um fator  $g$  de  $n$ . Note que é possível que  $g = n$ . Neste caso, não encontramos um fator adequado e temos que repetir o algoritmo com parâmetros diferentes (valor inicial diferente  $x_0$ , constante diferente  $c$  na função polinomial  $f$ ).

Para encontrar o ciclo, podemos usar qualquer algoritmo comum de detecção de ciclo.

### Algoritmo de Detecção de Ciclo de Floyd

Este algoritmo encontra um ciclo usando dois ponteiros. Esses ponteiros se movem pela sequência em velocidades diferentes. Em cada iteração, o primeiro ponteiro avança para o próximo elemento, mas o segundo ponteiro avança dois elementos. Não é difícil ver que, se existir um ciclo, o segundo ponteiro fará pelo menos um ciclo completo e então encontrará o primeiro ponteiro durante os próximos loops de ciclo. Se o comprimento do ciclo for  $\lambda$  e o  $\mu$  for o primeiro índice em que o ciclo começa, então o algoritmo será executado em $O(\lambda + \mu)$  tempo.

Este algoritmo também é conhecido como o [[algoritmo da Tartaruga e da Lebre]], baseado no conto em que uma tartaruga (aqui um ponteiro lento) e uma lebre (aqui um ponteiro mais rápido) fazem uma corrida.

Na verdade, é possível determinar o parâmetro  $\lambda$  e  $\mu$  usando este algoritmo (também em  $O(\lambda + \mu)$  tempo e  $O(1)$  espaço), mas aqui está apenas a versão simplificada para encontrar o ciclo em geral. O algoritmo retorna verdadeiro assim que detecta um ciclo. Se a sequência não tiver um ciclo, então a função nunca vai parar. No entanto, isso não pode acontecer durante o algoritmo rho de Pollard.

```python
function floyd(f, x0):
    tortoise = x0
    hare = f(x0)
    while tortoise != hare:
        tortoise = f(tortoise)
        hare = f(f(hare))
    return true
```

#### Implementação - Algoritmo de Detecção de Ciclo de Floyd

Primeiro, aqui está uma implementação usando o algoritmo de detecção de ciclo de Floyd. O algoritmo é executado (geralmente) em  
$O(\sqrt[4]{n} \log(n))$  tempo.

```cpp
long long mult(long long a, long long b, long long mod) {
    return (__int128)a * b % mod;
}

long long f(long long x, long long c, long long mod) {
    return (mult(x, x, mod) + c) % mod;
}

long long rho(long long n, long long x0=2, long long c=1) {
    long long x = x0;
    long long y = x0;
    long long g = 1;
    while (g == 1) {
        x = f(x, c, n);
        y = f(y, c, n);
        y = f(y, c, n);
        g = gcd(abs(x - y), n);
    }
    return g;
}
```
A tabela a seguir mostra os valores de  $x$  e  $y$  durante o algoritmo para  
$n = 2206637$ ,  $x_0 = 2$  e  $c = 1$ .
 
$$ \newcommand\T{\Rule{0pt}{1em}{.3em}} \begin{array}{|l|l|l|l|l|l|} \hline i & x_i \bmod n & x_{2i} \bmod n & x_i \bmod 317 & x_{2i} \bmod 317 & \gcd(x_i - x_{2i}, n) \\ \hline 0 & 2 & 2 & 2 & 2 & - \\ 1 & 5 & 26 & 5 & 26 & 1 \\ 2 & 26 & 458330 & 26 & 265 & 1 \\ 3 & 677 & 1671573 & 43 & 32 & 1 \\ 4 & 458330 & 641379 & 265 & 88 & 1 \\ 5 & 1166412 & 351937 & 169 & 67 & 1 \\ 6 & 1671573 & 1264682 & 32 & 169 & 1 \\ 7 & 2193080 & 2088470 & 74 & 74 & 317 \\ \hline \end{array}$$ 
A implementação usa uma função mult, que multiplica dois inteiros  $\le 10^{18}$  sem estouro usando um tipo __int128 do GCC para inteiros de 128 bits. Se o GCC não estiver disponível, você pode usar uma ideia semelhante à [[Binary Exponentiation]].

```cpp
long long mult(long long a, long long b, long long mod) {
    long long result = 0;
    while (b) {
        if (b & 1)
            result = (result + a) % mod;
        a = (a + a) % mod;
        b >>= 1;
    }
    return result;
}
```
Alternativamente, você também pode implementar a [multiplicação de Montgomery](obsidian://open?vault=Estudos_Obsidian&file=Computa%C3%A7%C3%A3o%2FOne%20for%20All%2FArtigos%2FMontgomery%20Multiplication).

Como já observado acima: se  $n$  é composto e o algoritmo retorna  $n$  como fator, você deve repetir o procedimento com parâmetro diferente  $x_0$  e  $c$ . Por exemplo, a escolha  $x_0 = c = 1$  não fatorará  $25 = 5 \cdot 5$ . O algoritmo apenas retornará  $25$ . No entanto, a escolha  $x_0 = 1$ ,  $c = 2$  irá fatorá-lo.

### Algoritmo de Brent

Brent usa um algoritmo semelhante ao de Floyd. Ele também usa dois ponteiros. Mas, em vez de avançar os ponteiros por um e dois respectivamente, avançamos eles em potências de dois. Assim que  $2^i$  for maior que  $\lambda$  e  $\mu$ , encontraremos o ciclo.

```python
function floyd(f, x0):
    tortoise = x0
    hare = f(x0)
    l = 1
    while tortoise != hare:
        tortoise = hare
        repeat l times:
            hare = f(hare)
            if tortoise == hare:
                return true
        l *= 2
    return true
```
O algoritmo de Brent também é executado em tempo linear, mas geralmente é mais rápido que o algoritmo de Floyd, pois usa menos avaliações da função  $f$ .

#### Implementação - Algoritmo de Brent
A implementação direta usando os algoritmos de Brent pode ser acelerada ao perceber que podemos omitir os termos  $x_l - x_k$  se  $k < \frac{3 \cdot l}{2}$ . Além disso, em vez de realizar o cálculo do  $\gcd$  a cada passo, multiplicamos os termos e fazemos isso a cada poucos passos e voltamos atrás se ultrapassarmos.

```cpp
long long brent(long long n, long long x0=2, long long c=1) {
    long long x = x0;
    long long g = 1;
    long long q = 1;
    long long xs, y;

    int m = 128;
    int l = 1;
    while (g == 1) {
        y = x;
        for (int i = 1; i < l; i++)
            x = f(x, c, n);
        int k = 0;
        while (k < l && g == 1) {
            xs = x;
            for (int i = 0; i < m && i < l - k; i++) {
                x = f(x, c, n);
                q = mult(q, abs(y - x), n);
            }
            g = gcd(q, n);
            k += m;
        }
        l *= 2;
    }
    if (g == n) {
        do {
            xs = f(xs, c, n);
            g = gcd(abs(xs - y), n);
        } while (g == 1);
    }
    return g;
}
```
A combinação de uma divisão de teste para números primos pequenos juntamente com a versão de Brent do algoritmo rho de Pollard fará um algoritmo de fatoração muito poderoso.
