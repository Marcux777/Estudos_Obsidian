Neste artigo, discutiremos um algoritmo que nos permite multiplicar dois polinômios de comprimento  $n$  em  $O(n \log n)$ , o que é melhor do que a multiplicação trivial que leva  $O(n^2)$ . Obviamente, a multiplicação de dois números longos também pode ser reduzida à multiplicação de polinômios, então dois números longos podem ser multiplicados em  $O(n \log n)$  (onde  $n$  é o número de dígitos nos números).

A descoberta da Transformada Rápida de Fourier (FFT) é atribuída a Cooley e Tukey, que publicaram um algoritmo em 1965. No entanto, de fato, a FFT foi descoberta repetidamente antes, mas a importância dela não foi compreendida antes das invenções dos computadores modernos. Alguns pesquisadores atribuem a descoberta da FFT a Runge e König em 1924. No entanto, Gauss desenvolveu tal método já em 1805, mas nunca o publicou.

Observe que o algoritmo FFT apresentado aqui é executado em  $O(n \log n)$ , mas não funciona para multiplicar polinômios grandes arbitrários com coeficientes grandes ou para multiplicar inteiros grandes arbitrários. Ele pode facilmente lidar com polinômios de tamanho  $10^5$  com coeficientes pequenos ou multiplicar dois números de tamanho  $10^6$ , mas em algum momento, a amplitude e a precisão dos números de ponto flutuante usados não serão mais suficientes para fornecer resultados precisos. Isso geralmente é suficiente para resolver problemas de programação competitiva, mas também existem variações mais complexas que podem realizar multiplicações de polinômios/inteiros arbitrariamente grandes. Por exemplo, em 1971, Schönhage e Strasser desenvolveram uma variação para multiplicar números grandes arbitrários que aplica a FFT recursivamente em estruturas de anéis com complexidade  $O(n \log n \log \log n)$ . E recentemente (em 2019), Harvey e van der Hoeven publicaram um algoritmo que roda em  $O(n \log n)$  verdadeiro.

[[Transformada Discreta de Fourier]]

[[Number theoretic transform]]

[[Multiplicação com módulo arbitrário]]

[[Aplicações]]
