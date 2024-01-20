
Este é um teste probabilístico.

O pequeno teorema de Fermat (veja também a função totiente de Euler) afirma que, para um número primo  $p$  e um inteiro coprimo  $a$ , a seguinte equação é válida:
$$a^{p-1} \equiv 1 \bmod p$$ 
Em geral, este teorema não é válido para números compostos.

Isso pode ser usado para criar um teste de primalidade. Escolhemos um inteiro  
$2 \le a \le p - 2$ , e verificamos se a equação é válida ou não. Se não for válida, por exemplo,  $a^{p-1} \not\equiv 1 \bmod p$ , sabemos que  $p$  não pode ser um número primo. Neste caso, chamamos a base  $a$  de testemunha de Fermat para a composição de  $p$ .

No entanto, também é possível que a equação seja válida para um número composto. Então, se a equação for válida, não temos uma prova de primalidade. Só podemos dizer que  $p$  é provavelmente primo. Se acontecer de o número ser realmente composto, chamamos a base  $a$  de mentiroso de Fermat.

Ao executar o teste para todas as bases possíveis  $a$ , podemos realmente provar que um número é primo. No entanto, isso não é feito na prática, pois é muito mais esforço do que apenas fazer a divisão de teste. Em vez disso, o teste será repetido várias vezes com escolhas aleatórias para  $a$ . Se não encontrarmos nenhuma testemunha para a composição, é muito provável que o número seja de fato primo.

```cpp
bool probablyPrimeFermat(int n, int iter=5) {
    if (n < 4)
        return n == 2 || n == 3;

    for (int i = 0; i < iter; i++) {
        int a = 2 + rand() % (n - 3);
        if (binpower(a, n - 1, n) != 1)
            return false;
    }
    return true;
}
```
Usamos a Exponenciação Binária para calcular eficientemente a potência  $a^{p-1}$ .

No entanto, há uma má notícia: existem alguns números compostos onde  $a^{n-1} \equiv 1 \bmod n$  é válido para todos  $a$  coprimos a  $n$ , por exemplo, para o número  $561 = 3 \cdot 11 \cdot 17$ . Tais números são chamados de números de Carmichael. O teste de primalidade de Fermat pode identificar esses números apenas se tivermos muita sorte e escolhermos uma base  $a$  com  $\gcd(a, n) \ne 1$ .

O teste de Fermat ainda é usado na prática, pois é muito rápido e os números de Carmichael são muito raros. Por exemplo, existem apenas 646 desses números abaixo de  $10^9$ .