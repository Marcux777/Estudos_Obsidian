
Considere a equação:
$$a^x \equiv b \pmod m,$$ 
onde  $a$  e  $m$  são primos entre si.

Seja  $x = np - q$ , onde  $n$  é uma constante pré-selecionada (vamos descrever como selecionar  
$n$  mais tarde).  $p$  é conhecido como o "passo gigante" ("giant step"), já que aumentá-lo em um aumenta  $x$  por  $n$ . Da mesma forma,  $q$  é conhecido como o "passo pequeno" ("baby step").

Obviamente, qualquer número  $x$  no intervalo  $[0; m)$  pode ser representado dessa forma, onde  
$p \in [1; \lceil \frac{m}{n} \rceil ]$  e  $q \in [0; n]$ .

Então, a equação se torna:
$$a^{np - q} \equiv b \pmod m.$$ 
Usando o fato de que  $a$  e  $m$  são primos entre si, obtemos:
$$a^{np} \equiv ba^q \pmod m$$ 
Esta nova equação pode ser reescrita de forma simplificada:
$$f_1(p) = f_2(q).$$ 
Esse problema pode ser resolvido usando o método meet-in-the-middle da seguinte maneira:

-  Calcule  $f_1$  para todos os possíveis argumentos  $p$ . Ordene o array de pares valor-argumento.
-  Para todos os possíveis argumentos  $q$ , calcule  $f_2$  e procure pelo  $p$  correspondente no array ordenado usando busca binária.