Semelhante aos inteiros, é possível definir a divisão longa para polinômios.

Definição

Para quaisquer polinômios  $A$  e  $B \neq 0$ , pode-se representar  $A$  como
 
$$ A = D \cdot B + R,~ \deg R < \deg B, $$ 
onde  $R$  é chamado de resto de  $A$  módulo  $B$  e  $D$  é chamado de quociente.

Denotando  $\deg A = n$  e  $\deg B = m$ , uma maneira ingênua de fazer isso é usar a divisão longa, durante a qual você multiplica  $B$  pelo monômio  $\frac{a_n}{b_m} x^{n - m}$  e subtrai isso de  $A$ , até que o grau de  $A$  seja menor que o de  $B$ . O que resta de  $A$  no final será o resto (daí o nome), e os polinômios pelos quais você multiplicou  $B$  no processo, somados juntos, formam o quociente.

Definição

Se  $A$  e  $B$  têm o mesmo resto módulo  $C$ , diz-se que são equivalentes módulo  $C$ , o que é denotado como 
$$ A \equiv B \pmod{C}. $$ 
A divisão longa de polinômios é útil devido às suas muitas propriedades importantes:

 
$A$  é um múltiplo de  $B$  se e somente se  $A \equiv 0 \pmod B$ .

Isso implica que  $A \equiv B \pmod C$  se e somente se  $A-B$  é um múltiplo de  $C$ .

Em particular,  $A \equiv B \pmod{C \cdot D}$  implica  $A \equiv B \pmod{C}$ .

Para qualquer polinômio linear  $x-r$ , vale que  $A(x) \equiv A(r) \pmod{x-r}$ .

Isso implica que  $A$  é um múltiplo de  $x-r$  se e somente se  $A(r)=0$ .

Para módulo sendo  $x^k$ , vale que  $A \equiv a_0 + a_1 x + \dots + a_{k-1} x^{k-1} \pmod{x^k}$ .

Observe que a divisão longa não pode ser adequadamente definida para séries formais de potências. Em vez disso, para qualquer  $A(x)$  tal que  $a_0 \neq 0$ , é possível definir uma série de potências formais inversa  $A^{-1}(x)$ , tal que  $A(x) A^{-1}(x) = 1$ . Esse fato, por sua vez, pode ser usado para calcular o resultado da divisão longa para polinômios.