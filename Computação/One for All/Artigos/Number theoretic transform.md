
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