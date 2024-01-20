
Vamos primeiro considerar um caso mais simples onde  $a$  e  $n$  são coprimos ( $\gcd(a, n) = 1$ ). Então, pode-se encontrar o [inverso](obsidian://open?vault=Algoritmos&file=algoritmos%2FArtigos%2FAlgebra%2FModular%20arithmetic%2FModular%20Inverse%2FInverso%20Multiplicativo%20Modular) de  $a$ , e multiplicando ambos os lados da equação pelo inverso, podemos obter uma solução única.
 
$$x \equiv b \cdot a ^ {- 1} \pmod n$$ 
Agora, considere o caso em que  $a$  e  $n$  não são coprimos ( $\gcd(a, n) \ne 1$ ). Nesse caso, a solução nem sempre existirá (por exemplo,  
$2 \cdot x \equiv 1 \pmod 4$  não tem solução).

Seja  $g = \gcd(a, n)$ , ou seja, o [maior divisor comum](obsidian://open?vault=Algoritmos&file=algoritmos%2FArtigos%2FAlgebra%2FAlgoritmo%20de%20Euclides%20para%20calcular%20o%20maior%20divisor%20comum%2FAlgoritmo%20-%20Algoritmo%20de%20Euclides%20para%20calcular%20o%20maior%20divisor%20comum) de  $a$  e  $n$  (que neste caso é maior que um).

Então, se  $b$  não é divisível por  $g$ , não há solução. De fato, para qualquer  $x$ , o lado esquerdo da equação  $a \cdot x \pmod n$  , é sempre divisível por  $g$ , enquanto o lado direito não é divisível por ele, portanto, segue-se que não há soluções.

Se  $g$  divide  $b$ , então, dividindo ambos os lados da equação por  $g$  (ou seja, dividindo  $a$ ,  $b$  e  $n$  por  $g$ ), recebemos uma nova equação:
 
$$a^\prime \cdot x \equiv b^\prime \pmod{n^\prime}$$ 
na qual  $a^\prime$  e  $n^\prime$  já são primos entre si, e já aprendemos como lidar com tal equação. Obtemos  $x^\prime$  como solução para  $x$ .

É claro que este  $x^\prime$  também será uma solução da equação original. No entanto, não será a única solução. Pode-se mostrar que a equação original tem exatamente  $g$  soluções, e elas serão assim:

$$x_i \equiv (x^\prime + i\cdot n^\prime) \pmod n \quad \text{para } i = 0 \ldots g-1$$ 
Resumindo, podemos dizer que o número de soluções da equação congruente linear é igual a  $g = \gcd(a, n)$  ou a zero.