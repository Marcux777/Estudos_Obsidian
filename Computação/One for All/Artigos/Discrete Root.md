O problema de encontrar uma raiz discreta é definido da seguinte forma. Dado um número primo  
$n$  e dois inteiros  $a$  e  $k$ , encontrar todos os  $x$  para os quais:

$x^k \equiv a \pmod n$ 

## Algoritmo
Resolveremos este problema reduzindo-o ao problema do logaritmo discreto.

Vamos aplicar o conceito de uma raiz primitiva módulo  $n$ . Seja  $g$  uma raiz primitiva módulo  
$n$ . Note que, uma vez que  $n$  é primo, ela deve existir, e pode ser encontrada em  $O(Ans \cdot \log \phi (n) \cdot \log n) = O(Ans \cdot \log^2 n)$  mais o tempo de fatoração de  $\phi (n)$ .

Podemos descartar facilmente o caso em que  $a = 0$ . Nesse caso, obviamente, há apenas uma resposta:   $x = 0$ .

Como sabemos que  $n$  é um número primo e que qualquer número entre 1 e  $n-1$  pode ser representado como uma potência da raiz primitiva, podemos representar o problema da raiz discreta da seguinte forma:

$(g^y)^k \equiv a \pmod n$ 

onde

$x \equiv g^y \pmod n$ 

Isso, por sua vez, pode ser reescrito como
 
$(g^k)^y \equiv a \pmod n$ 

Agora temos um desconhecido  $y$ , que é um problema de logaritmo discreto. A solução pode ser encontrada usando o algoritmo "baby-step giant-step" de Shanks em  $O(\sqrt {n} \log n)$  (ou podemos verificar se não há soluções).

Tendo encontrado uma solução  $y_0$ , uma das soluções do problema da raiz discreta será  $x_0 = g^{y_0} \pmod n$ .

## Encontrando todas as soluções a partir de uma solução conhecida
Para resolver o problema dado por completo, precisamos encontrar todas as soluções conhecendo uma delas:  $x_0 = g^{y_0} \pmod n$ .

Vamos lembrar o fato de que uma raiz primitiva sempre tem ordem de  
$\phi (n)$ , ou seja, a menor potência de  $g$  que resulta em 1 é  $\phi (n)$ . Portanto, se adicionarmos o termo  $\phi (n)$  ao exponencial, ainda obtemos o mesmo valor:
 
$x^k \equiv g^{ y_0 \cdot k + l \cdot \phi (n)} \equiv a \pmod n \forall l \in Z$ 

Assim, todas as soluções têm a forma:
 
$x = g^{y_0 + \frac {l \cdot \phi (n)}{k}} \pmod n \forall l \in Z$ .

onde  $l$  é escolhido de tal forma que a fração deve ser um número inteiro. Para que isso seja verdade, o numerador precisa ser divisível pelo mínimo múltiplo comum de  $\phi (n)$  e  $k$ . Lembre-se de que o mínimo múltiplo comum de dois números  $lcm(a, b) = \frac{a \cdot b}{gcd(a, b)}$ ; teremos
 
$x = g^{y_0 + i \frac {\phi (n)}{gcd(k, \phi (n))}} \pmod n \forall i \in Z$ .

Esta é a fórmula final para todas as soluções do problema da raiz discreta.
## Implementação
Aqui está uma implementação completa, incluindo procedimentos para encontrar a raiz primitiva, logaritmo discreto e encontrar e imprimir todas as soluções.

```cpp
int gcd(int a, int b) {
    return a ? gcd(b % a, a) : b;
}

int powmod(int a, int b, int p) {
    int res = 1;
    while (b > 0) {
        if (b & 1) {
            res = res * a % p;
        }
        a = a * a % p;
        b >>= 1;
    }
    return res;
}

// Finds the primitive root modulo p
int generator(int p) {
    vector<int> fact;
    int phi = p-1, n = phi;
    for (int i = 2; i * i <= n; ++i) {
        if (n % i == 0) {
            fact.push_back(i);
            while (n % i == 0)
                n /= i;
        }
    }
    if (n > 1)
        fact.push_back(n);

    for (int res = 2; res <= p; ++res) {
        bool ok = true;
        for (int factor : fact) {
            if (powmod(res, phi / factor, p) == 1) {
                ok = false;
                break;
            }
        }
        if (ok) return res;
    }
    return -1;
}

// This program finds all numbers x such that x^k = a (mod n)
int main() {
    int n, k, a;
    scanf("%d %d %d", &n, &k, &a);
    if (a == 0) {
        puts("1\n0");
        return 0;
    }

    int g = generator(n);

    // Baby-step giant-step discrete logarithm algorithm
    int sq = (int) sqrt (n + .0) + 1;
    vector<pair<int, int>> dec(sq);
    for (int i = 1; i <= sq; ++i)
        dec[i-1] = {powmod(g, i * sq * k % (n - 1), n), i};
    sort(dec.begin(), dec.end());
    int any_ans = -1;
    for (int i = 0; i < sq; ++i) {
        int my = powmod(g, i * k % (n - 1), n) * a % n;
        auto it = lower_bound(dec.begin(), dec.end(), make_pair(my, 0));
        if (it != dec.end() && it->first == my) {
            any_ans = it->second * sq - i;
            break;
        }
    }
    if (any_ans == -1) {
        puts("0");
        return 0;
    }

    // Print all possible answers
    int delta = (n-1) / gcd(k, n-1);
    vector<int> ans;
    for (int cur = any_ans % delta; cur < n-1; cur += delta)
        ans.push_back(powmod(g, cur, n));
    sort(ans.begin(), ans.end());
    printf("%d\n", ans.size());
    for (int answer : ans)
        printf("%d ", answer);
}
```