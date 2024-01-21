Aritmética de Precisão Arbitrária, também conhecida como "bignum" ou simplesmente "aritmética longa", é um conjunto de estruturas de dados e algoritmos que permite processar números muito maiores do que os que podem ser acomodados em tipos de dados padrão. Aqui estão vários tipos de aritmética de precisão arbitrária.

## Aritmética Longa para Inteiros Clássicos

A ideia principal é que o número é armazenado como uma matriz de seus "dígitos" em alguma base. Algumas bases mais frequentemente usadas são decimal, potências de decimal ( $10^4$  ou  $10^9$ ) e binária.

Operações em números nessa forma são realizadas usando algoritmos "escolares" de adição, subtração, multiplicação e divisão de colunas. Também é possível usar algoritmos rápidos de multiplicação, como a transformada rápida de Fourier e o algoritmo de Karatsuba.

Aqui, descrevemos a aritmética longa apenas para inteiros não negativos. Para estender os algoritmos para lidar com inteiros negativos, é necessário introduzir e manter uma bandeira adicional de "número negativo" ou usar a representação de inteiro em complemento de dois.

### Estrutura de Dados

Vamos armazenar números como um vetor<int>, em que cada elemento é um único "dígito" do número.

```
typedef vector<int> lnum;
```

Para melhorar o desempenho, usaremos  $10^9$  como a base, de modo que cada "dígito" do número contenha 9 dígitos decimais de uma vez.

```cpp
const int base = 1000*1000*1000;
```

Os dígitos serão armazenados em ordem do menos significativo para o mais significativo. Todas as operações serão implementadas de forma que, após cada uma delas, o resultado não tenha nenhum zero à esquerda, desde que os operandos também não tenham nenhum zero à esquerda. Todas as operações que podem resultar em um número com zeros à esquerda devem ser seguidas por código que os remove. Observe que, nesta representação, existem duas notações válidas para o número zero: um vetor vazio e um vetor com um único dígito zero.

### Saída
Imprimir o número inteiro longo é a operação mais fácil. Primeiro, imprimimos o último elemento do vetor (ou 0 se o vetor estiver vazio), seguido pelos demais elementos preenchidos com zeros à esquerda, se necessário, para que tenham exatamente 9 dígitos.

```cpp
printf ("%d", a.empty() ? 0 : a.back());
for (int i=(int)a.size()-2; i>=0; --i)
    printf ("%09d", a[i]);
```

Observe que fazemos um cast de a.size() para inteiro para evitar underflow de inteiro sem sinal caso o vetor contenha menos de 2 elementos.

### Entrada

Para ler um número inteiro longo, leia sua notação em uma string e, em seguida, converta-a para "dígitos":

```cpp
for (int i=(int)s.length(); i>0; i-=9)
    if (i < 9)
        a.push_back (atoi (s.substr (0, i).c_str()));
    else
        a.push_back (atoi (s.substr (i-9, 9).c_str()));
```

Se usarmos um array de char em vez de uma string, o código será ainda mais curto:

```cpp
for (int i=(int)strlen(s); i>0; i-=9) {
    s[i] = 0;
    a.push_back (atoi (i>=9 ? s+i-9 : s));
}
```

Se a entrada puder conter zeros à esquerda, eles podem ser removidos da seguinte forma:

```cpp
while (a.size() > 1 && a.back() == 0)
    a.pop_back();
```

### Adição
Incremente o número inteiro longo  $a$  por  $b$  e armazene o resultado em  $a$ :

```cpp
int carry = 0;
for (size_t i=0; i<max(a.size(),b.size()) || carry; ++i) {
    if (i == a.size())
        a.push_back (0);
    a[i] += carry + (i < b.size() ? b[i] : 0);
    carry = a[i] >= base;
    if (carry)  a[i] -= base;
}
```

### Subtração
Decrementar o número inteiro longo $a$  por  $b$  ( $a \ge b$ ) e armazenar o resultado em  $a$ :

```cpp
int carry = 0;
for (size_t i=0; i<b.size() || carry; ++i) {
    a[i] -= carry + (i < b.size() ? b[i] : 0);
    carry = a[i] < 0;
    if (carry)  a[i] += base;
}
while (a.size() > 1 && a.back() == 0)
    a.pop_back();
```

Observe que, após realizar a subtração, removemos os zeros à esquerda para manter a premissa de que nossos números inteiros longos não têm zeros à esquerda.

### Multiplicação por número inteiro curto
Multiplique o número inteiro longo  $a$  por um número inteiro curto  $b$  ( $b < base$ ) e armazene o resultado em  $a$ :

```cpp
int carry = 0;
for (size_t i=0; i<a.size() || carry; ++i) {
    if (i == a.size())
        a.push_back (0);
    long long cur = carry + a[i] * 1ll * b;
    a[i] = int (cur % base);
    carry = int (cur / base);
}
while (a.size() > 1 && a.back() == 0)
    a.pop_back();
```

Otimização adicional: Se o tempo de execução for extremamente importante, você pode tentar substituir duas divisões por uma, encontrando apenas o resultado inteiro da divisão (variável carry) e depois usá-lo para encontrar o resto usando a multiplicação. Isso geralmente torna o código mais rápido, embora não dramaticamente.

### Multiplicação por número inteiro longo
Multiplique os números inteiros longos  $a$  e  $b$  e armazene o resultado em  $c$ :

```cpp
lnum c (a.size()+b.size());
for (size_t i=0; i<a.size(); ++i)
    for (int j=0, carry=0; j<(int)b.size() || carry; ++j) {
        long long cur = c[i+j] + a[i] * 1ll * (j < (int)b.size() ? b[j] : 0) + carry;
        c[i+j] = int (cur % base);
        carry = int (cur / base);
    }
while (c.size() > 1 && c.back() == 0)
    c.pop_back();
```

### Divisão por número inteiro curto
Divida o número inteiro longo  $a$  pelo número inteiro curto  $b$  ( $b < base$ ), armazenando o resultado inteiro em  $a$  e o resto em carry:

```cpp
int carry = 0;
for (int i=(int)a.size()-1; i>=0; --i) {
    long long cur = a[i] + carry * 1ll * base;
    a[i] = int (cur / b);
    carry = int (cur % b);
}
while (a.size() > 1 && a.back() == 0)
    a.pop_back();
```

## Aritmética de Números Inteiros Longos para Representação de Fatorização
A ideia é armazenar o número como sua fatoração, ou seja, as potências dos números primos que o dividem.

Essa abordagem é muito fácil de implementar e permite fazer multiplicação e divisão facilmente (assintoticamente mais rápido do que o método clássico), mas não permite adição ou subtração. Além disso, é muito eficiente em termos de memória em comparação com a abordagem clássica.

Essa técnica é frequentemente usada para cálculos módulo um número não primo M; nesse caso, um número é armazenado como potências dos divisores de M que dividem o número, além do resto módulo M.

## Aritmética de Números Inteiros Longos em módulos primos (Algoritmo de Garner)
A ideia é escolher um conjunto de números primos (geralmente pequenos o suficiente para caber em um tipo de dados inteiro padrão) e armazenar um número como um vetor de restos da divisão do número por cada um desses primos.

O teorema chinês do resto afirma que essa representação é suficiente para restaurar unicamente qualquer número de 0 até o produto desses primos menos um. O algoritmo de Garner permite restaurar o número a partir dessa representação para um número inteiro normal.

Essa abordagem permite economizar memória em comparação com a abordagem clássica (embora a economia não seja tão dramática quanto na representação de fatorização). Além disso, permite realizar adição, subtração e multiplicação rapidamente, proporcionalmente ao número de primos usados como módulos (consulte o artigo sobre o teorema chinês do resto para implementação).

A desvantagem é que converter o número de volta para a forma normal é bastante trabalhoso e requer a implementação de aritmética clássica de precisão arbitrária com multiplicação. Além disso, essa abordagem não suporta divisão.

## Aritmética Fracionária de Precisão Arbitrária¶
Frações ocorrem com menos frequência em competições de programação do que inteiros, e a aritmética de longos é muito mais complicada de implementar para frações. Portanto, competições de programação apresentam apenas um pequeno subconjunto da aritmética fracionária de precisão arbitrária.

### Aritmética em Frações Irredutíveis¶
Um número é representado como uma fração irredutível  $\frac{a}{b}$ , onde  $a$  e  $b$  são inteiros. Todas as operações em frações podem ser representadas como operações nos numeradores e denominadores inteiros dessas frações. Geralmente, isso requer o uso de aritmética clássica de precisão arbitrária para armazenar numerador e denominador, mas às vezes um tipo de dado inteiro embutido de 64 bits é suficiente.

### Armazenar a Posição de Ponto Flutuante como Tipo Separado¶
Às vezes, um problema exige lidar com números muito pequenos ou muito grandes sem permitir estouro ou subfluxo. O tipo de dado double embutido usa 8-10 bytes e permite valores do expoente no intervalo  $[-308; 308]$ , o que às vezes pode ser insuficiente.

A abordagem é muito simples: uma variável inteira separada é usada para armazenar o valor do expoente, e após cada operação, o número de ponto flutuante é normalizado, ou seja, devolvido ao intervalo  $[0.1; 1)$  ajustando o expoente de acordo.

Quando dois desses números são multiplicados ou divididos, seus expoentes devem ser adicionados ou subtraídos, respectivamente. Quando os números são adicionados ou subtraídos, eles precisam ser trazidos para um expoente comum primeiro, multiplicando um deles por 10 elevado à potência igual à diferença dos valores dos expoentes.

Como nota final, a base do expoente não precisa ser igual a 10. Com base na representação interna de números de ponto flutuante, faz mais sentido usar 2 como base do expoente.