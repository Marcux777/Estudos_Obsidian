
Dado dois números inteiros não negativos $a$ e $b$, temos que encontrar o MDC (máximo divisor comum) deles, ou seja, o maior número que é divisor de ambos $a$ e $b$. Isso é comumente denotado por $\gcd(a, b)$. Matematicamente, é definido como:

$\gcd(a, b) = \max \{k > 0 : (k \mid a) \text{ e } (k \mid b) \}$

(aqui o símbolo $\mid$ denota divisibilidade, ou seja, “$k \mid a$” significa “$k$ divide $a$”)

Quando um dos números é zero e o outro não é, o máximo divisor comum deles, por definição, é o segundo número. Quando ambos os números são zero, o máximo divisor comum é indefinido (pode ser qualquer número arbitrariamente grande), mas é conveniente defini-lo como zero também para preservar a associatividade do $\gcd$. Isso nos dá uma regra simples: se um dos números é zero, o máximo divisor comum é o outro número.

O algoritmo de Euclides, discutido abaixo, permite encontrar o máximo divisor comum de dois números $a$ e $b$ em $O(\log \min(a, b))$.

O algoritmo foi descrito pela primeira vez nos “Elementos” de Euclides (por volta de 300 a.C.), mas é possível que o algoritmo tenha origens ainda mais antigas.

## Algoritmo

Originalmente, o algoritmo de Euclides foi formulado da seguinte maneira: subtraia o número menor do maior até que um dos números seja zero. De fato, se $g$ divide $a$ e $b$, ele também divide $a-b$. Por outro lado, se $g$ divide $a-b$ e $b$, então ele também divide $a = b + (a-b)$, o que significa que os conjuntos dos divisores comuns de $\{a, b\}$ e $\{b,a-b\}$ coincidem.

Note que $a$ permanece o número maior até que $b$ seja subtraído dele pelo menos $\left\lfloor\frac{a}{b}\right\rfloor$ vezes. Portanto, para acelerar as coisas, $a-b$ é substituído por $a-\left\lfloor\frac{a}{b}\right\rfloor b = a \bmod b$. Então, o algoritmo é formulado de uma maneira extremamente simples:

$$\gcd(a, b) = \begin{cases}a,&\text{se }b = 0 \\ \gcd(b, a \bmod b),&\text{caso contrário.}\end{cases}$$


## Implementação


Aqui está a implementação recursiva:
```cpp
int gcd (int a, int b) {
    if (b == 0)
        return a;
    else
        return gcd (b, a % b);
}
```

Usando o operador ternário em C++, podemos escrevê-lo em uma linha:
```cpp
int gcd (int a, int b) {
    return b ? gcd (b, a % b) : a;
}
```

E finalmente, aqui está uma implementação não recursiva:
```cpp
int gcd (int a, int b) {
    while (b) {
        a %= b;
        swap(a, b);
    }
    return a;
}
```

Note que desde o C++17, o gcd é implementado como uma função padrão em C++. Isso significa que você pode usar `std::gcd(a, b)` para calcular o máximo divisor comum de `a` e `b`.

## Complexidade de Tempo

O tempo de execução do algoritmo é estimado pelo teorema de Lamé, que estabelece uma conexão surpreendente entre o algoritmo de Euclides e a sequência de Fibonacci:

Se $a > b \geq 1$ e $b < F_n$ para algum $n$, o algoritmo de Euclides realiza no máximo $n-2$chamadas recursivas.

Além disso, é possível mostrar que o limite superior deste teorema é ótimo. Quando$a = F_neb = F_{n-1},\gcd(a, b)$ realizará exatamente $n-2$ chamadas recursivas. Em outras palavras, números consecutivos de Fibonacci são o pior caso de entrada para o algoritmo de Euclides.

Dado que os números de Fibonacci crescem exponencialmente, obtemos que o algoritmo de Euclides funciona em $O(\log \min(a, b))$.

Outra maneira de estimar a complexidade é notar que $a \bmod b$ para o caso $a \geq b$ é pelo menos $2$ vezes menor que $a$, então o número maior é reduzido pelo menos pela metade em cada iteração do algoritmo.


## Mínimo múltiplo comum
O cálculo do mínimo múltiplo comum (comumente denotado por MMC) pode ser reduzido ao cálculo do MDC com a seguinte fórmula simples:

$$\text{lcm}(a, b) = \frac{a \cdot b}{\gcd(a, b)}$$

Assim, o MMC pode ser calculado usando o algoritmo de Euclides com a mesma complexidade de tempo:

Uma possível implementação, que evita inteligentemente estouros de inteiro dividindo primeiro $a$ pelo MDC, é dada aqui:

```cpp
int lcm (int a, int b) {
    return a / gcd(a, b) * b;
}
```

## MDC Binário
O algoritmo de MDC binário é uma otimização do algoritmo de Euclides normal.

A parte lenta do algoritmo normal são as operações de módulo. As operações de módulo, embora as vejamos como $O(1)$, são muito mais lentas do que operações mais simples como adição, subtração ou operações bitwise. Portanto, seria melhor evitá-las.

Acontece que você pode projetar um algoritmo de MDC rápido que evita operações de módulo. Ele é baseado em algumas propriedades:

Se ambos os números são pares, então podemos fatorar um dois de ambos e calcular o MDC dos números restantes: $\gcd(2a, 2b) = 2 \gcd(a, b)$.
Se um dos números é par e o outro é ímpar, então podemos remover o fator 2 do par: $\gcd(2a, b) = \gcd(a, b)$ se $b$ é ímpar.
Se ambos os números são ímpares, então subtrair um número do outro não mudará o MDC: $\gcd(a, b) = \gcd(b, a-b)$
Usando apenas essas propriedades, e algumas funções bitwise rápidas do GCC, podemos implementar uma versão rápida:

```cpp
int gcd(int a, int b) {
    if (!a || !b)
        return a | b;
    unsigned shift = __builtin_ctz(a | b);
    a >>= __builtin_ctz(a);
    do {
        b >>= __builtin_ctz(b);
        if (a > b)
            swap(a, b);
        b -= a;
    } while (b);
    return a << shift;
}
```
Note que tal otimização geralmente não é necessária, e a maioria das linguagens de programação já tem uma função de MDC em suas bibliotecas padrão. Por exemplo, o C++17 tem uma função std::gcd no cabeçalho numérico.
