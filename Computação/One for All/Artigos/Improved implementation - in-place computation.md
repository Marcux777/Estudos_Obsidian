
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