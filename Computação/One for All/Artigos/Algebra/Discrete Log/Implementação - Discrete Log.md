
### A implementação mais simples
No código a seguir, a função powmod calcula  $a^b \pmod m$  e a função solve produz uma solução adequada para o problema. Ela retorna  $-1$  se não houver solução e retorna uma das soluções possíveis, caso contrário.

```cpp
int powmod(int a, int b, int m) {
    int res = 1;
    while (b > 0) {
        if (b & 1) {
            res = (res * 1ll * a) % m;
        }
        a = (a * 1ll * a) % m;
        b >>= 1;
    }
    return res;
}

int solve(int a, int b, int m) {
    a %= m, b %= m;
    int n = sqrt(m) + 1;
    map<int, int> vals;
    for (int p = 1; p <= n; ++p)
        vals[powmod(a, p * n, m)] = p;
    for (int q = 0; q <= n; ++q) {
        int cur = (powmod(a, q, m) * 1ll * b) % m;
        if (vals.count(cur)) {
            int ans = vals[cur] * n - q;
            return ans;
        }
    }
    return -1;
}
```

Neste código, usamos `map` da biblioteca padrão do C++ para armazenar os valores de  
$f_1$ . Internamente, o `map` usa uma árvore rubro-negra para armazenar os valores. Portanto, este código é um pouco mais lento do que se tivéssemos usado um array e realizado a busca binária, mas é muito mais fácil de escrever.

Observe que nosso código assume  $0^0 = 1$ , ou seja, o código calculará  $0$  como solução para a equação  $0^x \equiv 1 \pmod m$  e também como solução para  $0^x \equiv 0 \pmod 1$ . Esta é uma convenção frequentemente usada na álgebra, mas também não é universalmente aceita em todas as áreas. Às vezes,  $0^0$  é simplesmente indefinido. Se você não gostar da nossa convenção, precisará tratar o caso  $a=0$  separadamente:

```cpp
if (a == 0)
    return b == 0 ? 1 : -1;
```

Outra coisa a observar é que, se houver vários argumentos  $p$  que mapeiam para o mesmo valor de  $f_1$ , armazenamos apenas um desses argumentos. Isso funciona neste caso porque só queremos retornar uma possível solução. Se precisarmos retornar todas as soluções possíveis, precisamos alterar `map<int, int>` para, por exemplo, `map<int, vector<int>>`. Também precisamos ajustar a segunda etapa de acordo.

### Implementação melhorada

Uma possível melhoria é eliminar a exponenciação binária. Isso pode ser feito mantendo uma variável que é multiplicada por  $a$  cada vez que aumentamos  $q$  e uma variável que é multiplicada por  $a^n$  cada vez que aumentamos  $p$ . Com essa alteração, a complexidade do algoritmo ainda é a mesma, mas agora o fator  $\log$  é apenas para o mapa. Em vez de um mapa, também podemos usar uma tabela de hash (unordered_map em C++), que tem complexidade de tempo média  
$O(1)$  para inserção e busca.

Problemas frequentemente pedem o mínimo  
$x$  que satisfaz a solução.
É possível obter todas as respostas e pegar a mínima, ou reduzir a primeira resposta encontrada usando o teorema de Euler, mas podemos ser inteligentes sobre a ordem em que calculamos os valores e garantir que a primeira resposta que encontramos seja a mínima.

```cpp
// Returns minimum x for which a ^ x % m = b % m, a and m are coprime.
int solve(int a, int b, int m) {
    a %= m, b %= m;
    int n = sqrt(m) + 1;

    int an = 1;
    for (int i = 0; i < n; ++i)
        an = (an * 1ll * a) % m;

    unordered_map<int, int> vals;
    for (int q = 0, cur = b; q <= n; ++q) {
        vals[cur] = q;
        cur = (cur * 1ll * a) % m;
    }

    for (int p = 1, cur = 1; p <= n; ++p) {
        cur = (cur * 1ll * an) % m;
        if (vals.count(cur)) {
            int ans = n * p - vals[cur];
            return ans;
        }
    }
    return -1;
}
```

A complexidade é  $O(\sqrt{m})$  usando unordered_map.