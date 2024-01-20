
Outro método para encontrar o inverso modular é usar o teorema de Euler, que afirma que a seguinte congruência é verdadeira se  $a$  e  $m$  são primos entre si:

 
$$a^{\phi (m)} \equiv 1 \mod m$$ 
 
$\phi$  é a [[Função totiente de Euler]]. Novamente, note que  $a$  e  $m$  serem primos entre si também era a condição para a existência do inverso modular.

Se  $m$  é um número primo, isso simplifica para o [[pequeno teorema de Fermat]]:

$$a^{m - 1} \equiv 1 \mod m$$ 
Multiplique ambos os lados das equações acima por  
$a^{-1}$ , e obtemos:

- Para um módulo arbitrário (mas coprimo)  $m$ :  $a ^ {\phi (m) - 1} \equiv a ^{-1} \mod m$ 
- Para um módulo primo  $m$ :  $a ^ {m - 2} \equiv a ^ {-1} \mod m$ 

A partir desses resultados, podemos facilmente encontrar o inverso modular usando o [algoritmo de exponenciação binária](obsidian://open?vault=Algoritmos&file=algoritmos%2FArtigos%2FAlgebra%2FBinary%20Exponentiation%2FAlgoritmo%20-%20Binary%20Exponentiation), que funciona em  $O(\log m)$  tempo.

Embora este método seja mais fácil de entender do que o método descrito no parágrafo anterior, no caso em que  $m$  não é um número primo, precisamos calcular a função phi de Euler, que envolve a fatoração de  $m$ , o que pode ser muito difícil. Se a fatoração prima de  $m$  é conhecida, então a complexidade deste método é  $O(\log m)$ .