Deve ser óbvio que a fatoração prima de um divisor  $d$  tem que ser um subconjunto da fatoração prima de  $n$ , por exemplo, $6 = 2 \cdot 3$  é um divisor de  $60 = 2^2 \cdot 3 \cdot 5$ . Portanto, só precisamos encontrar todos os diferentes subconjuntos da fatoração prima de  $n$ .

Normalmente, o número de subconjuntos é  $2^x$  para um conjunto com  $x$  elementos. No entanto, isso não é mais verdade se houver elementos repetidos no conjunto. No nosso caso, alguns fatores primos podem aparecer várias vezes na fatoração prima de  $n$ .

Se um fator primo  $p$  aparece  $e$  vezes na fatoração prima de  $n$ , então podemos usar o fator  $p$  até  $e$  vezes no subconjunto. O que significa que temos  $e+1$  escolhas.

Portanto, se a fatoração prima de  $n$  é  $p_1^{e_1} \cdot p_2^{e_2} \cdots p_k^{e_k}$ , onde  $p_i$  são números primos distintos, então o número de divisores é:
$$d(n) = (e_1 + 1) \cdot (e_2 + 1) \cdots (e_k + 1)$$ 
Uma maneira de pensar sobre isso é a seguinte:

Se houver apenas um divisor primo distinto  $n = p_1^{e_1}$ , então obviamente existem $e_1 + 1$  divisores ( $1, p_1, p_1^2, \dots, p_1^{e_1}$ ).

Se houver dois divisores primos distintos  $n = p_1^{e_1} \cdot p_2^{e_2}$ , então você pode organizar todos os divisores na forma de uma tabela.
 
$$\begin{array}{c|ccccc} & 1 & p_2 & p_2^2 & \dots & p_2^{e_2} \\\\\hline 1 & 1 & p_2 & p_2^2 & \dots & p_2^{e_2} \\\\ p_1 & p_1 & p_1 \cdot p_2 & p_1 \cdot p_2^2 & \dots & p_1 \cdot p_2^{e_2} \\\\ p_1^2 & p_1^2 & p_1^2 \cdot p_2 & p_1^2 \cdot p_2^2 & \dots & p_1^2 \cdot p_2^{e_2} \\\\ \vdots & \vdots & \vdots & \vdots & \ddots & \vdots \\\\ p_1^{e_1} & p_1^{e_1} & p_1^{e_1} \cdot p_2 & p_1^{e_1} \cdot p_2^2 & \dots & p_1^{e_1} \cdot p_2^{e_2} \\\\ \end{array}$$ 
Portanto, o número de divisores é trivialmente $(e_1 + 1) \cdot (e_2 + 1)$ .

Um argumento semelhante pode ser feito se houver mais de dois fatores primos distintos.
```c++
long long numberOfDivisors(long long num) {
    long long total = 1;
    for (int i = 2; (long long)i * i <= num; i++) {
        if (num % i == 0) {
            int e = 0;
            do {
                e++;
                num /= i;
            } while (num % i == 0);
            total *= e + 1;
        }
    }
    if (num > 1) {
        total *= 2;
    }
    return total;
}
```


