Neste artigo, discutiremos um algoritmo que nos permite multiplicar dois polinômios de comprimento  $n$  em  $O(n \log n)$ , o que é melhor do que a multiplicação trivial que leva  $O(n^2)$ . Obviamente, a multiplicação de dois números longos também pode ser reduzida à multiplicação de polinômios, então dois números longos podem ser multiplicados em  $O(n \log n)$  (onde  $n$  é o número de dígitos nos números).

A descoberta da Transformada Rápida de Fourier (FFT) é atribuída a Cooley e Tukey, que publicaram um algoritmo em 1965. No entanto, de fato, a FFT foi descoberta repetidamente antes, mas a importância dela não foi compreendida antes das invenções dos computadores modernos. Alguns pesquisadores atribuem a descoberta da FFT a Runge e König em 1924. No entanto, Gauss desenvolveu tal método já em 1805, mas nunca o publicou.

Observe que o algoritmo FFT apresentado aqui é executado em  $O(n \log n)$ , mas não funciona para multiplicar polinômios grandes arbitrários com coeficientes grandes ou para multiplicar inteiros grandes arbitrários. Ele pode facilmente lidar com polinômios de tamanho  $10^5$  com coeficientes pequenos ou multiplicar dois números de tamanho  $10^6$ , mas em algum momento, a amplitude e a precisão dos números de ponto flutuante usados não serão mais suficientes para fornecer resultados precisos. Isso geralmente é suficiente para resolver problemas de programação competitiva, mas também existem variações mais complexas que podem realizar multiplicações de polinômios/inteiros arbitrariamente grandes. Por exemplo, em 1971, Schönhage e Strasser desenvolveram uma variação para multiplicar números grandes arbitrários que aplica a FFT recursivamente em estruturas de anéis com complexidade  $O(n \log n \log \log n)$ . E recentemente (em 2019), Harvey e van der Hoeven publicaram um algoritmo que roda em  $O(n \log n)$  verdadeiro.

## Transformada Discreta de Fourier

Considere um polinômio de grau  $n - 1$ :
$$A(x) = a_0 x^0 + a_1 x^1 + \dots + a_{n-1} x^{n-1}$$ 
Sem perda de generalidade, assumimos que  $n$  - o número de coeficientes - é uma potência de  $2$ . Se  $n$  não é uma potência de  $2$ , então simplesmente adicionamos os termos ausentes  $a_i x^i$  e definimos os coeficientes  $a_i$  como  $0$ .

A teoria dos números complexos nos diz que a equação  $x^n = 1$  tem  $n$  soluções complexas (chamadas  $n$ -ésimas raízes da unidade), e as soluções têm a forma  $w_{n, k} = e^{\frac{2 k \pi i}{n}}$  com  $k = 0 \dots n-1$ . Além disso, esses números complexos têm propriedades muito interessantes: por exemplo, a principal  $n$ -ésima raiz  $w_n = w_{n, 1} = e^{\frac{2 \pi i}{n}}$  pode ser usada para descrever todas as outras raízes  
$n$ -ésimas:  $w_{n, k} = (w_n)^k$ .

A Transformada Discreta de Fourier (DFT) do polinômio  $A(x)$  (ou equivalentemente, o vetor de coeficientes  $(a_0, a_1, \dots, a_{n-1})$  é definida como os valores do polinômio nos pontos  $x = w_{n, k}$ , ou seja, é o vetor:
$$\begin{align} \text{DFT}(a_0, a_1, \dots, a_{n-1}) &= (y_0, y_1, \dots, y_{n-1}) \\ &= (A(w_{n, 0}), A(w_{n, 1}), \dots, A(w_{n, n-1})) \\ &= (A(w_n^0), A(w_n^1), \dots, A(w_n^{n-1})) \end{align}$$ 
Da mesma forma, a transformada discreta inversa de Fourier é definida: A DFT inversa dos valores do polinômio  $(y_0, y_1, \dots, y_{n-1})$  são os coeficientes do polinômio  $(a_0, a_1, \dots, a_{n-1})$ .

$$\text{InverseDFT}(y_0, y_1, \dots, y_{n-1}) = (a_0, a_1, \dots, a_{n-1})$$ 
Assim, se uma DFT direta calcula os valores do polinômio nos pontos das  $n$ -ésimas raízes, a DFT inversa pode restaurar os coeficientes do polinômio usando esses valores.

### Aplicação da DFT: multiplicação rápida de polinômios
Considere dois polinômios  $A$  e  $B$ . Calculamos a DFT para cada um deles:  
$\text{DFT}(A)$  e  $\text{DFT}(B)$ .

O que acontece se multiplicarmos esses polinômios? Obviamente, em cada ponto, os valores são simplesmente multiplicados, ou seja,

$$(A \cdot B)(x) = A(x) \cdot B(x).$$ 
Isso significa que, se multiplicarmos os vetores  $\text{DFT}(A)$  e  $\text{DFT}(B)$  - multiplicando cada elemento de um vetor pelo elemento correspondente do outro vetor - obtemos nada menos que a DFT do polinômio  $\text{DFT}(A \cdot B)$ :

$$\text{DFT}(A \cdot B) = \text{DFT}(A) \cdot \text{DFT}(B)$$ 
Finalmente, aplicando a DFT inversa, obtemos:

 
$$A \cdot B = \text{InverseDFT}(\text{DFT}(A) \cdot \text{DFT}(B))$$ 
Na parte direita, o produto das duas DFTs refere-se ao produto em pares dos elementos do vetor. Isso pode ser calculado em  $O(n)$  tempo. Se pudermos calcular a DFT e a DFT inversa em  $O(n \log n)$ , então podemos calcular o produto dos dois polinômios (e consequentemente também de dois números longos) com a mesma complexidade de tempo.

Deve-se observar que os dois polinômios devem ter o mesmo grau. Caso contrário, os dois vetores resultantes da DFT terão comprimentos diferentes. Podemos alcançar isso adicionando coeficientes com o valor  $0$ .

Além disso, como o resultado do produto de dois polinômios é um polinômio de grau  $2 (n - 1)$ , precisamos dobrar os graus de cada polinômio (novamente preenchendo com  $0$ s). A partir de um vetor com  $n$  valores, não podemos reconstruir o polinômio desejado com  $2n - 1$  coeficientes.


### Fast Fourier Transform
$$A(x) = a_0 x^0 + a_1 x^1 + \dots + a_{n-1} x^{n-1}$$ 
Dividimos o polinômio em dois polinômios menores, um contendo apenas os coeficientes das posições pares e outro contendo os coeficientes das posições ímpares:

$$
\begin{align}
A_0(x) &= a_0 x^0 + a_2 x^1 + \dots + a_{n-2} x^{\frac{n}{2}-1} \\
A_1(x) &= a_1 x^0 + a_3 x^1 + \dots + a_{n-1} x^{\frac{n}{2}-1}
\end{align}
$$
É fácil ver que

$$A(x) = A_0(x^2) + x A_1(x^2).$$
Os polinômios  $A_0$  e  $A_1$  têm apenas a metade dos coeficientes do polinômio  $A$ . Se pudermos calcular a  $\text{DFT}(A)$  em tempo linear usando  $\text{DFT}(A_0)$  e  $\text{DFT}(A_1)$ , então obtemos a recorrência  

$$T_{\text{DFT}}(n) = 2 T_{\text{DFT}}\left(\frac{n}{2}\right) + O(n)$$

para a complexidade de tempo, que resulta em  $T_{\text{DFT}}(n) = O(n \log n)$  pelo teorema mestre.

Vamos aprender como podemos fazer isso.

Suponha que tenhamos calculado os vetores  $\left(y_k^0\right)_{k=0}^{n/2-1} = \text{DFT}(A_0)$  e  $\left(y_k^1\right)_{k=0}^{n/2-1} = \text{DFT}(A_1)$ . Vamos encontrar uma expressão para  $\left(y_k\right)_{k=0}^{n-1} = \text{DFT}(A)$ .

Para os primeiros  
$\frac{n}{2}$  valores, podemos usar a equação anteriormente observada  $A(x) = A_0(x^2) + x A_1(x^2)$ :

$$y_k = y_k^0 + w_n^k y_k^1, \quad k = 0 \dots \frac{n}{2} - 1.$$

No entanto, para os segundos  $\frac{n}{2}$  valores, precisamos encontrar uma expressão um pouco diferente:

$$
\begin{align}
y_{k+n/2} &= A\left(w_n^{k+n/2}\right) \\
&= A_0\left(w_n^{2k+n}\right) + w_n^{k + n/2} A_1\left(w_n^{2k+n}\right) \\
&= A_0\left(w_n^{2k} w_n^n\right) + w_n^k w_n^{n/2} A_1\left(w_n^{2k} w_n^n\right) \\
&= A_0\left(w_n^{2k}\right) - w_n^k A_1\left(w_n^{2k}\right) \\
&= y_k^0 - w_n^k y_k^1
\end{align}
$$

Aqui usamos novamente  $A(x) = A_0(x^2) + x A_1(x^2)$  e as duas identidades  $w_n^n = 1$  e  $w_n^{n/2} = -1$ .

Portanto, obtemos as fórmulas desejadas para calcular todo o vetor  
$(y_k)$ :

$$
\begin{align}
y_k &= y_k^0 + w_n^k y_k^1, &\quad k = 0 \dots \frac{n}{2} - 1, \\
y_{k+n/2} &= y_k^0 - w_n^k y_k^1, &\quad k = 0 \dots \frac{n}{2} - 1.
\end{align}
$$

(Este padrão  $a + b$  e  $a - b$  é às vezes chamado de "borboleta".)

Assim, aprendemos como calcular a DFT em  $O(n \log n)$  tempo.
### Inverse FFT (Transformada Rápida de Fourier Inversa)
Dado o vetor  $(y_0, y_1, \dots y_{n-1})$  - os valores do polinômio  $A$  de grau  $n - 1$  nos pontos  $x = w_n^k$  - seja dado. Queremos restaurar os coeficientes  $(a_0, a_1, \dots, a_{n-1})$  do polinômio. Este problema conhecido é chamado de interpolação, e existem algoritmos gerais para resolvê-lo. Mas, neste caso especial (já que conhecemos os valores nos pontos das raízes da unidade), podemos obter um algoritmo muito mais simples (que é praticamente o mesmo que a FFT direta).

Podemos escrever a DFT, de acordo com sua definição, na forma de matriz:

$$
\begin{pmatrix}
w_n^0 & w_n^0 & w_n^0 & w_n^0 & \cdots & w_n^0 \\
w_n^0 & w_n^1 & w_n^2 & w_n^3 & \cdots & w_n^{n-1} \\
w_n^0 & w_n^2 & w_n^4 & w_n^6 & \cdots & w_n^{2(n-1)} \\
w_n^0 & w_n^3 & w_n^6 & w_n^9 & \cdots & w_n^{3(n-1)} \\
\vdots & \vdots & \vdots & \vdots & \ddots & \vdots \\
w_n^0 & w_n^{n-1} & w_n^{2(n-1)} & w_n^{3(n-1)} & \cdots & w_n^{(n-1)(n-1)}
\end{pmatrix}
\begin{pmatrix}
a_0 \\
a_1 \\
a_2 \\
a_3 \\
\vdots \\
a_{n-1}
\end{pmatrix}
=
\begin{pmatrix}
y_0 \\
y_1 \\
y_2 \\
y_3 \\
\vdots \\
y_{n-1}
\end{pmatrix}
$$

Esta matriz é chamada de matriz de Vandermonde.

Assim, podemos calcular o vetor  $(a_0, a_1, \dots, a_{n-1})$  multiplicando o vetor  $(y_0, y_1, \dots y_{n-1})$  à esquerda pela inversa da matriz:

$$
\begin{pmatrix}
a_0 \\
a_1 \\
a_2 \\
a_3 \\
\vdots \\
a_{n-1}
\end{pmatrix}
=
\begin{pmatrix}
w_n^0 & w_n^0 & w_n^0 & w_n^0 & \cdots & w_n^0 \\
w_n^0 & w_n^1 & w_n^2 & w_n^3 & \cdots & w_n^{n-1} \\
w_n^0 & w_n^2 & w_n^4 & w_n^6 & \cdots & w_n^{2(n-1)} \\
w_n^0 & w_n^3 & w_n^6 & w_n^9 & \cdots & w_n^{3(n-1)} \\
\vdots & \vdots & \vdots & \vdots & \ddots & \vdots \\
w_n^0 & w_n^{n-1} & w_n^{2(n-1)} & w_n^{3(n-1)} & \cdots & w_n^{(n-1)(n-1)}
\end{pmatrix}^{-1}
\begin{pmatrix}
y_0 \\
y_1 \\
y_2 \\
y_3 \\
\vdots \\
y_{n-1}
\end{pmatrix}
$$

Uma verificação rápida pode verificar que a inversa da matriz tem a seguinte forma:

$$
\frac{1}{n}
\begin{pmatrix}
w_n^0 & w_n^0 & w_n^0 & w_n^0 & \cdots & w_n^0 \\
w_n^0 & w_n^{-1} & w_n^{-2} & w_n^{-3} & \cdots & w_n^{-(n-1)} \\
w_n^0 & w_n^{-2} & w_n^{-4} & w_n^{-6} & \cdots & w_n^{-2(n-1)} \\
w_n^0 & w_n^{-3} & w_n^{-6} & w_n^{-9} & \cdots & w_n^{-3(n-1)} \\
\vdots & \vdots & \vdots & \vdots & \ddots & \vdots \\
w_n^0 & w_n^{-(n-1)} & w_n^{-2(n-1)} & w_n

^{-3(n-1)} & \cdots & w_n^{-(n-1)(n-1)}
\end{pmatrix}
$$

Assim, obtemos a fórmula:

$$
a_k = \frac{1}{n} \sum_{j=0}^{n-1} y_j w_n^{-k j}
$$

Comparando isso com a fórmula para  $y_k$ 

$$
y_k = \sum_{j=0}^{n-1} a_j w_n^{k j},
$$

notamos que esses problemas são quase iguais, então os coeficientes  $a_k$  podem ser encontrados pelo mesmo algoritmo de divisão e conquista, assim como a FFT direta, apenas em vez de  $w_n^k$ , precisamos usar  $w_n^{-k}$ , e no final precisamos dividir os coeficientes resultantes por  
$n$ .

Portanto, o cálculo da inversa da DFT é quase o mesmo que o cálculo da DFT direta, e também pode ser realizado em  $O(n \log n)$  tempo.
### Implementação
Aqui apresentamos uma implementação recursiva simples da FFT e da FFT inversa, ambas em uma única função, já que a diferença entre a FFT direta e a FFT inversa é tão mínima. Para armazenar os números complexos, usamos o tipo complex na STL do C++.

```cpp
using cd = complex<double>;
const double PI = acos(-1);

void fft(vector<cd> & a, bool invert) {
    int n = a.size();
    if (n == 1)
        return;

    vector<cd> a0(n / 2), a1(n / 2);
    for (int i = 0; 2 * i < n; i++) {
        a0[i] = a[2*i];
        a1[i] = a[2*i+1];
    }
    fft(a0, invert);
    fft(a1, invert);

    double ang = 2 * PI / n * (invert ? -1 : 1);
    cd w(1), wn(cos(ang), sin(ang));
    for (int i = 0; 2 * i < n; i++) {
        a[i] = a0[i] + w * a1[i];
        a[i + n/2] = a0[i] - w * a1[i];
        if (invert) {
            a[i] /= 2;
            a[i + n/2] /= 2;
        }
        w *= wn;
    }
}
```

A função recebe um vetor de coeficientes, e a função calculará a FFT ou FFT inversa e armazenará o resultado novamente neste vetor. O argumento  $\text{invert}$  indica se a FFT direta ou inversa deve ser calculada. Dentro da função, primeiro verificamos se o comprimento do vetor é igual a um; se for o caso, não precisamos fazer nada. Caso contrário, dividimos o vetor  $a$  em dois vetores
$a0$  e  $a1$  e calculamos a FFT para ambos recursivamente. Em seguida, inicializamos o valor  $wn$  e uma variável  $w$ , que conterá a potência atual de  $wn$ . Em seguida, os valores da FFT resultante são calculados usando as fórmulas acima.

Se a bandeira  $\text{invert}$  estiver definida, substituímos  $wn$  por  $wn^{-1}$ , e cada um dos valores do resultado é dividido por  $2$  (já que isso será feito em cada nível da recursão, isso acabará dividindo os valores finais por  $n$ ).

Usando essa função, podemos criar uma função para multiplicar dois polinômios:

```cpp
vector<int> multiply(vector<int> const& a, vector<int> const& b) {
    vector<cd> fa(a.begin(), a.end()), fb(b.begin(), b.end());
    int n = 1;
    while (n < a.size() + b.size()) 
        n <<= 1;
    fa.resize(n);
    fb.resize(n);

    fft(fa, false);
    fft(fb, false);
    for (int i = 0; i < n; i++)
        fa[i] *= fb[i];
    fft(fa, true);

    vector<int> result(n);
    for (int i = 0; i < n; i++)
        result[i] = round(fa[i].real());
    return result;
}
```

Esta função funciona com polinômios com coeficientes inteiros, no entanto, você também pode ajustá-la para trabalhar com outros tipos. Como há algum erro ao trabalhar com números complexos, precisamos arredondar os coeficientes resultantes no final.

Finalmente, a função para multiplicar dois números longos praticamente não difere da função para multiplicar polinômios. A única coisa que precisamos fazer depois é normalizar o número:

```cpp
    int carry = 0;
    for (int i = 0; i < n; i++) {
        result[i] += carry;
        carry = result[i] / 10;
        result[i] %= 10;
    }
```

Como o comprimento do produto de dois números nunca excede o comprimento total de ambos os números, o tamanho do vetor é suficiente para realizar todas as operações de transporte.


### Improved implementation - in-place computation
Para aumentar a eficiência, vamos mudar da implementação recursiva para uma implementação iterativa. Na implementação recursiva acima, separamos explicitamente o vetor  
$a$  em dois vetores - os elementos nas posições pares foram atribuídos a um vetor temporário, e os elementos nas posições ímpares a outro. No entanto, se reorganizarmos os elementos de uma certa maneira, não precisamos criar esses vetores temporários (ou seja, todos os cálculos podem ser feitos "in-place", diretamente no vetor  $A$ ).

Observe que, no primeiro nível de recursão, os elementos cujo bit mais baixo da posição era zero foram atribuídos ao vetor  $a_0$ , e aqueles com um como o bit mais baixo da posição foram atribuídos a  $a_1$ . No segundo nível de recursão, a mesma coisa acontece, mas com o segundo bit mais baixo, etc. Portanto, se invertermos os bits da posição de cada coeficiente e os ordenarmos por esses valores invertidos, obtemos a ordem desejada (chamada de permutação de inversão de bits).

Por exemplo, a ordem desejada para  $n = 8$  tem a forma:

 
$$a = \bigg\{ \Big[ (a_0, a_4), (a_2, a_6) \Big], \Big[ (a_1, a_5), (a_3, a_7) \Big] \bigg\}$$ 
Na verdade, no primeiro nível de recursão (entre chaves), o vetor é dividido em duas partes  $[a_0, a_2, a_4, a_6]$  e  $[a_1, a_3, a_5, a_7]$ . Como vemos, na permutação de inversão de bits, isso corresponde a simplesmente dividir o vetor em duas metades: os primeiros  $\frac{n}{2}$  elementos e os últimos $\frac{n}{2}$  elementos. Em seguida, há uma chamada recursiva para cada metade. Suponha que o DFT resultante para cada uma delas seja retornado no lugar dos próprios elementos (ou seja, a primeira metade e a segunda metade do vetor  $a$ , respectivamente).

 
$$a = \bigg\{ \Big[y_0^0, y_1^0, y_2^0, y_3^0\Big], \Big[y_0^1, y_1^1, y_2^1, y_3^1 \Big] \bigg\}$$ 
Agora queremos combinar os dois DFTs em um para o vetor completo. A ordem dos elementos é ideal, e também podemos realizar a união diretamente neste vetor. Podemos pegar os elementos  
$y_0^0$  e  $y_0^1$  e realizar a transformação butterfly. O lugar dos dois valores resultantes é o mesmo que o lugar dos dois valores iniciais, então obtemos:

 
$$a = \bigg\{ \Big[y_0^0 + w_n^0 y_0^1, y_1^0, y_2^0, y_3^0\Big], \Big[y_0^0 - w_n^0 y_0^1, y_1^1, y_2^1, y_3^1\Big] \bigg\}$$ 
Da mesma forma, podemos calcular a transformação da borboleta de  $y_1^0$  e  $y_1^1$  e colocar os resultados em seus lugares, e assim por diante. Como resultado, obtemos:

 
$$a = \bigg\{ \Big[y_0^0 + w_n^0 y_0^1, y_1^0 + w_n^1 y_1^1, y_2^0 + w_n^2 y_2^1, y_3^0 + w_n^3 y_3^1\Big], \Big[y_0^0 - w_n^0 y_0^1, y_1^0 - w_n^1 y_1^1, y_2^0 - w_n^2 y_2^1, y_3^0 - w_n^3 y_3^1\Big] \bigg\}$$ 
Assim, calculamos o DFT necessário a partir do vetor  $a$ .

Aqui descrevemos o processo de calcular o DFT apenas no primeiro nível de recursão, mas o mesmo funciona obviamente também para todos os outros níveis. Portanto, após aplicar a permutação de inversão de bits, podemos

 calcular o DFT no local, sem nenhuma memória adicional.

Isso permite eliminar a recursão. Começamos no nível mais baixo, ou seja, dividimos o vetor em pares e aplicamos a transformação da borboleta a eles. Isso resulta no vetor  $a$  com o trabalho do último nível aplicado. Na próxima etapa, dividimos o vetor em vetores de tamanho  $4$  e novamente aplicamos a transformação da borboleta, o que nos dá o DFT para cada bloco de tamanho  $4$ . E assim por diante. Finalmente, na última etapa, obtivemos o resultado dos DFTs de ambas as metades de  $a$ , e aplicando a transformação da borboleta, obtemos o DFT para o vetor completo  $a$ .

```cpp
using cd = complex<double>;
const double PI = acos(-1);

int reverse(int num, int lg_n) {
    int res = 0;
    for (int i = 0; i < lg_n; i++) {
        if (num & (1 << i))
            res |= 1 << (lg_n - 1 - i);
    }
    return res;
}

void fft(vector<cd> & a, bool invert) {
    int n = a.size();
    int lg_n = 0;
    while ((1 << lg_n) < n)
        lg_n++;

    for (int i = 0; i < n; i++) {
        if (i < reverse(i, lg_n))
            swap(a[i], a[reverse(i, lg_n)]);
    }

    for (int len = 2; len <= n; len <<= 1) {
        double ang = 2 * PI / len * (invert ? -1 : 1);
        cd wlen(cos(ang), sin(ang));
        for (int i = 0; i < n; i += len) {
            cd w(1);
            for (int j = 0; j < len / 2; j++) {
                cd u = a[i+j], v = a[i+j+len/2] * w;
                a[i+j] = u + v;
                a[i+j+len/2] = u - v;
                w *= wlen;
            }
        }
    }

    if (invert) {
        for (cd & x : a)
            x /= n;
    }
}
```

No início, aplicamos a permutação de inversão de bits, trocando cada elemento pelo elemento da posição invertida. Em seguida, para os  $\log n - 1$  estágios do algoritmo, calculamos o DFT para cada bloco do tamanho correspondente  $\text{len}$ . Para todos esses blocos, temos a mesma raiz de unidade  
$\text{wlen}$ . Iteramos por todos os blocos e aplicamos a transformação da borboleta em cada um deles.

Podemos otimizar ainda mais a inversão dos bits. Na implementação anterior, iteramos todos os bits do índice e criamos o índice inverso bitwise. No entanto, podemos inverter os bits de uma maneira diferente.

Suponha que  $j$  já contenha a inversão de  $i$ . Então, para ir para  $i + 1$ , precisamos incrementar  
$i$ , e também precisamos incrementar  $j$ , mas em um sistema de números "invertido". Adicionar um no sistema binário convencional é equivalente a inverter todos os uns finais em zeros e inverter o zero imediatamente antes deles em um. Equivalentemente, no sistema de números "invertido", invertemos todos os uns principais e também o próximo zero.

Assim, obtemos a seguinte implementação:

```cpp
using cd = complex<double>;
const double PI = acos(-1);

void fft(vector<cd> & a, bool invert) {
    int n = a.size();

    for (int i = 1, j = 0; i < n; i++) {
        int bit = n >> 1;
        for (; j & bit; bit >>= 1)
            j ^= bit;
        j ^= bit;

        if (i < j)
            swap(a[i], a[j]);
    }

    for (int len = 2; len <= n; len <<= 1) {
        double ang = 2 * PI / len * (invert ? -1 : 1);
        cd wlen(cos(ang), sin(ang));
        for (int i = 0; i < n; i += len) {
            cd w(1);
            for (int j = 0; j < len / 2; j++) {
                cd u = a[i+j], v = a[i+j+len/2] * w;
                a[i+j] = u + v;
                a[i+j+len/2] = u - v;
                w *= wlen;
            }
        }
    }

    if (invert) {
        for (cd & x : a)
            x /= n;
    }
}
```

Além disso, podemos pré-calcular a permutação de inversão de bits antecipadamente. Isso é especialmente útil quando o tamanho  $n$  é o mesmo para todas as chamadas. Mas mesmo quando temos apenas três chamadas (que são necessárias para multiplicar dois polinômios), o efeito é perceptível. Também podemos pré-calcular todas as raízes da unidade e suas potências.

## Number theoretic transform
Agora vamos mudar um pouco o objetivo. Ainda queremos multiplicar dois polinômios em  
$O(n \log n)$  tempo, mas desta vez queremos calcular os coeficientes módulo algum número primo  
$p$ . Claro que, para essa tarefa, podemos usar a transformada discreta de Fourier normal (DFT) e aplicar o operador módulo ao resultado. No entanto, fazer isso pode levar a erros de arredondamento, especialmente ao lidar com números grandes. A transformada teórica de números (NTT) tem a vantagem de que só funciona com números inteiros, e, portanto, os resultados são garantidos de estar corretos.

A transformada discreta de Fourier é baseada em números complexos e nas  $n$ -ésimas raízes da unidade. Para calcular eficientemente a DFT, usamos extensivamente as propriedades das raízes (por exemplo, que há uma raiz que gera todas as outras raízes por exponenciação).

Mas as mesmas propriedades valem para as  $n$ -ésimas raízes da unidade na aritmética modular. Uma  $n$ -ésima raiz da unidade em um campo primitivo é tal número  $w_n$  que satisfaz:
$$\begin{align} (w_n)^n &= 1 \pmod{p}, \\ (w_n)^k &\ne 1 \pmod{p}, \quad 1 \le k < n. \end{align}$$ 
As outras  $n-1$  raízes podem ser obtidas como potências da raiz  $w_n$ .

Para aplicá-lo no algoritmo de transformada rápida de Fourier, precisamos que uma raiz exista para algum  $n$ , que é uma potência de  $2$ , e também para todas as potências menores. Podemos notar a seguinte propriedade interessante:
 
$$\begin{align} (w_n^2)^m = w_n^n &= 1 \pmod{p}, \quad \text{com } m = \frac{n}{2}\\ (w_n^2)^k = w_n^{2k} &\ne 1 \pmod{p}, \quad 1 \le k < m. \end{align}$$ 
Assim, se  $w_n$  é uma  $n$ -ésima raiz da unidade, então  $w_n^2$  é uma  $\frac{n}{2}$ -ésima raiz da unidade. E, consequentemente, para todas as potências menores de dois, existem raízes da ordem requerida, e elas podem ser calculadas usando  $w_n$ .

Para calcular a inversa da DFT, precisamos da inversa  $w_n^{-1}$  de  $w_n$ . Mas para um módulo primo, a inversa sempre existe.

Assim, todas as propriedades que precisamos das raízes complexas também estão disponíveis na aritmética modular, desde que tenhamos um módulo  $p$  grande o suficiente para o qual exista uma  $n$ -ésima raiz da unidade.

Por exemplo, podemos pegar os seguintes valores: módulo  $p = 7340033$ ,  $w_{2^{20}} = 5$ . Se esse módulo não for suficiente, precisamos encontrar um par diferente. Podemos usar o fato de que, para módulos da forma  $p = c 2^k + 1$  (e  $p$  é primo), sempre existe a  $2^k$ -ésima raiz da unidade. Pode-se mostrar que  $g^c$  é tal  $2^k$ -ésima raiz da unidade, onde  $g$  é uma [raiz primitiva] de  $p$ .

```cpp
const int mod = 7340033;
const int root = 5;
const int root_1 = 4404020;
const int root_pw = 1 << 20;

void fft(vector<int> & a, bool invert) {
    int n = a.size();

    for (int i = 1, j = 0; i < n; i++) {
        int bit = n >> 1;
        for (; j & bit; bit >>= 1)
            j ^= bit;
        j ^= bit;

        if (i < j)
            swap(a[i], a[j]);
    }

    for (int len = 2; len <= n; len <<= 1) {
        int wlen = invert ? root_1 : root;
        for (int i = len; i < root_pw; i <<= 1)
            wlen = (int)(1LL * wlen * wlen % mod);

        for (int i = 0; i < n; i += len) {
            int w = 1;
            for (int j = 0; j < len / 2; j++) {
                int u = a[i+j], v = (int)(1LL * a[i+j+len/2] * w % mod);
                a[i+j] = u + v < mod ? u + v : u + v - mod;
                a[i+j+len/2] = u - v >= 0 ? u - v : u - v + mod;
                w = (int)(1LL * w * wlen % mod);
            }
        }
    }

    if (invert) {
        int n_1 = inverse(n, mod);
        for (int & x : a)
            x = (int)(1LL * x * n_1 % mod);
    }
}
```
Aqui, a função inverse calcula a inversa modular (consulte [Inverso Multiplicativo Modular]). As constantes mod, root, root_pw determinam o módulo e a raiz, e root_1 é a inversa de root módulo mod.

Na prática, esta implementação é mais lenta do que a implementação usando números complexos (devido ao grande número de operações de módulo), mas possui algumas vantagens, como menor uso de memória e nenhum erro de arredondamento.

## Multiplicação com módulo arbitrário
Aqui queremos alcançar o mesmo objetivo da seção anterior. Multiplicar dois polinômios  $A(x)$  e  
$B(x)$ , e calcular os coeficientes módulo algum número  $M$ . A transformada teórica de números só funciona para certos números primos. E se o módulo não estiver na forma desejada?

Uma opção seria realizar várias transformadas teóricas de números com diferentes números primos da forma  
$c 2^k + 1$ , e depois aplicar o Teorema Chinês dos Restos para calcular os coeficientes finais.

Outra opção é distribuir os polinômios  $A(x)$  e  $B(x)$  em dois polinômios menores cada:

  
 
 
$$\begin{align} A(x) &= A_1(x) + A_2(x) \cdot C \\ B(x) &= B_1(x) + B_2(x) \cdot C \end{align}$$ 
com  $C \approx \sqrt{M}$ .

Então, o produto de $A(x)$  e  $B(x)$  pode ser representado como:

$$A(x) \cdot B(x) = A_1(x) \cdot B_1(x) + \left(A_1(x) \cdot B_2(x) + A_2(x) \cdot B_1(x)\right)\cdot C + \left(A_2(x) \cdot B_2(x)\right)\cdot C^2$$ 
Os polinômios  $A_1(x)$ ,  $A_2(x)$ ,  $B_1(x)$  e  $B_2(x)$  contêm apenas coeficientes menores que  
$\sqrt{M}$ , portanto, os coeficientes de todos os produtos que aparecem são menores que  
$M \cdot n$ , o que geralmente é pequeno o suficiente para lidar com os tipos típicos de ponto flutuante.

Portanto, essa abordagem requer calcular os produtos de polinômios com coeficientes menores (usando a FFT normal e a FFT inversa), e então o produto original pode ser restaurado usando adição e multiplicação modulares em  $O(n)$  tempo.

## Aplicações

A Transformada Discreta de Fourier (DFT) pode ser usada em uma variedade enorme de outros problemas, que à primeira vista não têm nada a ver com a multiplicação de polinômios.

### Todas as Somas Possíveis
Dadas duas listas  $a[]$  e  $b[]$ , queremos encontrar todas as somas possíveis  $a[i] + b[j]$ , e, para cada soma, contar quantas vezes ela aparece.

Por exemplo, para  $a = [1,~ 2,~ 3]$  e  $b = [2,~ 4]$ , obtemos: a soma  $3$  pode ser obtida de  $1$  maneira, a soma  $4$  também em  $1$ ,  $5$  em $2$ ,  $6$  em  $1$ ,  $7$  em  $1$ .

Construímos para as listas  $a$  e  $b$  dois polinômios  $A$  e  $B$ . Os números na lista atuarão como os expoentes no polinômio ( $a[i] \Rightarrow x^{a[i]}$ ); e os coeficientes deste termo indicarão quantas vezes o número aparece na lista.

Então, multiplicando esses dois polinômios em  $O(n \log n)$  tempo, obtemos um polinômio  $C$ , onde os expoentes nos dirão quais somas podem ser obtidas, e os coeficientes indicarão quantas vezes. Para demonstrar isso no exemplo:
$$(1 x^1 + 1 x^2 + 1 x^3) (1 x^2 + 1 x^4) = 1 x^3 + 1 x^4 + 2 x^5 + 1 x^6 + 1 x^7$$ 
### Todos os Produtos Escalares Possíveis

Dadas duas listas  $a[]$  e  $b[]$  de comprimento  $n$ . Queremos calcular os produtos de  $a$  com cada deslocamento cíclico de  $b$ .

Geramos duas novas listas de tamanho  $2n$ : Invertemos  $a$  e acrescentamos  $n$  zeros a ele. E simplesmente acrescentamos  $b$  a si mesmo. Quando multiplicamos essas duas listas como polinômios, e olhamos para os coeficientes  $c[n-1],~ c[n],~ \dots,~ c[2n-2]$  do produto  $c$ , obtemos:
 
$$c[k] = \sum_{i+j=k} a[i] b[j]$$ 
E como todos os elementos  $a[i] = 0$  para  $i \ge n$ :

$$c[k] = \sum_{i=0}^{n-1} a[i] b[k-i]$$ 
É fácil ver que essa soma é apenas o produto escalar do vetor  $a$  com o  $(k - (n - 1))$ -ésimo deslocamento cíclico para a esquerda de  $b$ . Assim, esses coeficientes são a resposta para o problema, e ainda conseguimos obtê-la em  $O(n \log n)$  tempo. Note que  
$c[2n-1]$  também nos dá o  $n$ -ésimo deslocamento cíclico, mas isso é o mesmo que o  $0$ -ésimo deslocamento cíclico, então não precisamos considerar isso separadamente em nossa resposta.

### Duas Faixas

Dadas duas faixas booleanas (listas cíclicas de valores  $0$  e  $1$ )  $a$  e  $b$ . Queremos encontrar todas as maneiras de anexar a primeira faixa à segunda, de modo que em nenhuma posição tenhamos um  
$1$  da primeira faixa ao lado de um  $1$  da segunda faixa.

O problema na verdade não difere muito do problema anterior. Anexar duas faixas significa apenas que realizamos um deslocamento cíclico na segunda lista, e podemos anexar as duas faixas se o produto escalar das duas listas for  $0$ .

### Casamento de Strings

Dadas duas strings, um texto  $T$  e um padrão  $P$ , consistindo de letras minúsculas. Temos que calcular todas as ocorrências do padrão no texto.

Criamos um polinômio para cada string ( $T[i]$  e  $P[I]$  são números entre  $0$  e  $25$  correspondendo às  $26$  letras do alfabeto):
$$A(x) = a_0 x^0 + a_1 x^1 + \dots + a_{n-1} x^{n-1}, \quad n = |T|$$ 
com
 
$$a_i = \cos(\alpha_i) + i \sin(\alpha_i), \quad \alpha_i = \frac{2 \pi T[i]}{26}.$$ 
E

$$B(x) = b_0 x^0 + b_1 x^1 + \dots + b_{m-1} x^{m-1}, \quad m = |P|$$ 
com

$$b_i = \cos(\beta_i) - i \sin(\beta_i), \quad \beta_i = \frac{2 \pi P[m-i-1]}{26}.$$ 
Observe que com a expressão  $P[m-i-1]$  revertemos explicitamente o padrão.

Os coeficientes  $(m-1+i)$ th do produto dos dois polinômios  $C(x) = A(x) \cdot B(x)$  nos dirão se o padrão aparece no texto na posição  $i$ .

$$c_{m-1+i} = \sum_{j = 0}^{m-1} a_{i+j} \cdot b_{m-1-j} = \sum_{j=0}^{m-1} \left(\cos(\alpha_{i+j}) + i \sin(\alpha_{i+j})\right) \cdot \left(\cos(\beta_j) - i \sin(\beta_j)\right)$$ 
com  $\alpha_{i+j} = \frac{2 \pi T[i+j]}{26}$  e   $\beta_j = \frac{2 \pi P[j]}{26}$ 

Se houver uma correspondência, então  $T[i+j] = P[j]$ , e, portanto,  $\alpha_{i+j} = \beta_j$ . Isso dá (usando a identidade trigonométrica de Pitágoras):

$$\begin{align} c_{m-1+i} &= \sum_{j = 0}^{m-1} \left(\cos(\alpha_{i+j}) + i \sin(\alpha_{i+j})\right) \cdot \left(\cos(\alpha_{i+j}) - i \sin(\alpha_{i+j})\right) \\ &= \sum_{j = 0}^{m-1} \cos(\alpha_{i+j})^2 + \sin(\alpha_{i+j})^2 = \sum_{j = 0}^{m-1} 1 = m \end{align}$$ 
Se não houver uma correspondência, então pelo menos um caractere é diferente, o que leva a um dos produtos  $a_{i+1} \cdot b_{m-1-j}$  não ser igual a  $1$ , o que leva ao coeficiente  $c_{m-1+i} \ne m$ .

### Casamento de Strings com curingas

Esta é uma extensão do problema anterior. Desta vez, permitimos que o padrão contenha o caractere curinga  $\*$ , que pode corresponder a qualquer letra possível. Por exemplo, o padrão  $a*c$  aparece no texto  $abccaacc$  exatamente em três posições, nos índices  $0$ ,  $4$  e  $5$ .

Criamos os mesmos polinômios, exceto que definimos  $b_i = 0$  se $P[m-i-1] = *$ . Se  $x$  é o número de curingas em  $P$ , então teremos uma correspondência de  $P$  em  $T$  no índice  $i$  se  $c_{m-1+i} = m - x$ .
