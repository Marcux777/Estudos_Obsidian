Considere a sequência de Fibonacci módulo $p$. Vamos provar que a sequência é periódica.

Vamos provar isso por contradição. Considere os primeiros $p^2 + 1$ pares de números de Fibonacci tomados módulo $p$:

$$(F_0,\ F_1),\ (F_1,\ F_2),\ \ldots,\ (F_{p^2},\ F_{p^2 + 1})$$
Só pode haver $p$ restos diferentes módulo $p$, e no máximo $p^2$ pares diferentes de restos, então há pelo menos dois pares idênticos entre eles. Isso é suficiente para provar que a sequência é periódica, pois um número de Fibonacci é determinado apenas por seus dois predecessores. Portanto, se dois pares de números consecutivos se repetem, isso também significaria que os números após o par se repetirão da mesma maneira.

Agora escolhemos dois pares de restos idênticos com os menores índices na sequência. Deixe os pares serem $(F_a,\ F_{a + 1})$ e $(F_b,\ F_{b + 1})$. Vamos provar que $a = 0$. Se isso fosse falso, haveria dois pares anteriores $(F_{a-1},\ F_a)$ e $(F_{b-1},\ F_b)$, que, pela propriedade dos números de Fibonacci, também seriam iguais. No entanto, isso contradiz o fato de termos escolhido pares com os menores índices, completando nossa prova de que não há pré-período (ou seja, os números são periódicos a partir de $F_0$).