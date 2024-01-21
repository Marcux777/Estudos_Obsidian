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

