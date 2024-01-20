
Por definição, um número primo não tem nenhum divisor além de  $1$  e ele mesmo. Um número composto tem pelo menos um divisor adicional, vamos chamá-lo de $d$ . Naturalmente  $\frac{n}{d}$  também é um divisor de  $n$ . É fácil ver que, ou $d \le \sqrt{n}$  ou $\frac{n}{d} \le \sqrt{n}$ , portanto, um dos divisores $d$  e  $\frac{n}{d}$  é  $\le \sqrt{n}$ . Podemos usar essa informação para verificar a primalidade.

Tentamos encontrar um divisor não trivial, verificando se algum dos números entre $2$  e  $\sqrt{n}$  é um divisor de  $n$ . Se for um divisor, então  $n$  definitivamente não é primo, caso contrário, é.

```cpp
bool isPrime(int x) {
    for (int d = 2; d * d <= x; d++) {
        if (x % d == 0)
            return false;
    }
    return x >= 2;
}
```

Esta é a forma mais simples de verificar a primalidade. Você pode otimizar bastante essa função, por exemplo, verificando apenas todos os números ímpares no loop, já que o único número primo par é 2. Várias dessas otimizações são descritas no artigo sobre fatoração de inteiros.