
No entanto, a multiplicação de Montgomery não ocorre de graça. O algoritmo funciona apenas no espaço de Montgomery. E precisamos transformar nossos números nesse espaço antes de começarmos a multiplicar.

Para o espaço, precisamos de um número inteiro positivo  $r \ge n$  coprimo com  
$n$ , ou seja,  $\gcd(n, r) = 1$ . Na prática, sempre escolhemos  $r$  para ser  $2^m$  para um número inteiro positivo  $m$ , já que multiplicações, divisões e operações de módulo  $r$  podem ser eficientemente implementadas usando deslocamentos e outras operações de bits.  $n$  será um número ímpar em praticamente todas as aplicações, já que não é difícil fatorar um número par. Portanto, cada potência de  $2$  será coprima com  $n$ .

O representante  $\bar{x}$  de um número  $x$  no espaço de Montgomery é definido como:

$$\bar{x} := x \cdot r \bmod n$$ 
Observe que a transformação é na verdade uma multiplicação que queremos otimizar. Portanto, esta ainda é uma operação cara. No entanto, você só precisa transformar um número uma vez para o espaço. Assim que estiver no espaço de Montgomery, você pode realizar quantas operações quiser de maneira eficiente. E no final, você transforma o resultado final de volta. Portanto, enquanto estiver fazendo muitas operações módulo  $n$ , isso não será um problema.

Dentro do espaço de Montgomery, ainda é possível realizar a maioria das operações normalmente. Você pode adicionar dois elementos ( $x \cdot r + y \cdot r \equiv (x + y) \cdot r \bmod n$ ), subtrair, verificar igualdade e até mesmo calcular o maior divisor comum de um número com  $n$  (já que  $\gcd(n, r) = 1$ ). Tudo com os algoritmos usuais.

No entanto, isso não é o caso para a multiplicação.

Esperamos que o resultado seja:
$$\bar{x} * \bar{y} = \overline{x \cdot y} = (x \cdot y) \cdot r \bmod n.$$ 
Mas a multiplicação normal nos dará:
$$\bar{x} \cdot \bar{y} = (x \cdot y) \cdot r \cdot r \bmod n.$$ 
Portanto, a multiplicação no espaço de Montgomery é definida como:
$$\bar{x} * \bar{y} := \bar{x} \cdot \bar{y} \cdot r^{-1} \bmod n.$$ 