
Outro algoritmo de fatoração de John Pollard.

Deixe a fatoração prima de um número ser  $n = p q$ . O algoritmo olha para uma sequência pseudo-aleatória  $\{x_i\} = \{x_0,~f(x_0),~f(f(x_0)),~\dots\}$  onde  $f$  é uma função polinomial, geralmente  $f(x) = (x^2 + c) \bmod n$  é escolhida com  $c = 1$ .

Na verdade, não estamos muito interessados na sequência  $\{x_i\}$ , estamos mais interessados na sequência  $\{x_i \bmod p\}$ . Como  $f$  é uma função polinomial e todos os valores estão no intervalo  $[0;~p)$ , esta sequência começará a se repetir mais cedo ou mais tarde. O paradoxo do aniversário sugere que o número esperado de elementos é  $O(\sqrt{p})$  até que a repetição comece. Se  
$p$  for menor que  $\sqrt{n}$ , a repetição começará muito provavelmente em  $O(\sqrt[4]{n})$ .

Aqui está uma visualização de tal sequência  $\{x_i \bmod p\}$  com  $n = 2206637$ ,  $p = 317$ ,  $x_0 = 2$  e  $f(x) = x^2 + 1$ . A partir da forma da sequência, você pode ver claramente por que o algoritmo é chamado de algoritmo rho de Pollard.

![[Pasted image 20240119130130.png]]


Ainda há uma grande questão em aberto. Ainda não sabemos  $p$ , então como podemos argumentar sobre a sequência  $\{x_i \bmod p\}$ ?

Na verdade, é bem fácil. Há um ciclo na sequência  $\{x_i \bmod p\}_{i \le j}$  se e somente se existem dois índices  $s, t \le j$  tais que  $x_s \equiv x_t \bmod p$ . Esta equação pode ser reescrita como  $x_s - x_t \equiv 0 \bmod p$  que é o mesmo que  $p ~|~ \gcd(x_s - x_t, n)$ .

Portanto, se encontrarmos dois índices  $s$  e  $t$  com  $g = \gcd(x_s - x_t, n) > 1$ , encontramos um ciclo e também um fator  $g$  de  $n$ . Note que é possível que  $g = n$ . Neste caso, não encontramos um fator adequado e temos que repetir o algoritmo com parâmetros diferentes (valor inicial diferente  $x_0$ , constante diferente  $c$  na função polinomial  $f$ ).

Para encontrar o ciclo, podemos usar qualquer algoritmo comum de detecção de ciclo.

[[Algoritmo de Detecção de Ciclo de Floyd]]
[[Algoritmo de Brent]]

