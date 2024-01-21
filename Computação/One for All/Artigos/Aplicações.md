
A Transformada Discreta de Fourier (DFT) pode ser usada em uma variedade enorme de outros problemas, que à primeira vista não têm nada a ver com a multiplicação de polinômios.

### Todas as Somas Possíveis
Dadas duas listas  $a[]$  e  $b[]$ , queremos encontrar todas as somas possíveis  $a[i] + b[j]$ , e, para cada soma, contar quantas vezes ela aparece.

Por exemplo, para  $a = [1,~ 2,~ 3]$  e  $b = [2,~ 4]$ , obtemos: a soma  $3$  pode ser obtida de  $1$  maneira, a soma  $4$  também em  $1$ ,  $5$  em $2$ ,  $6$  em  $1$ ,  $7$  em  $1$ .

Construímos para as listas  $a$  e  $b$  dois polinômios  $A$  e  $B$ . Os números na lista atuarão como os expoentes no polinômio ( $a[i] \Rightarrow x^{a[i]}$ ); e os coeficientes deste termo indicarão quantas vezes o número aparece na lista.

Então, multiplicando esses dois polinômios em  $O(n \log n)$  tempo, obtemos um polinômio  $C$ , onde os expoentes nos dirão quais somas podem ser obtidas, e os coeficientes indicarão quantas vezes. Para demonstrar isso no exemplo:
$$(1 x^1 + 1 x^2 + 1 x^3) (1 x^2 + 1 x^4) = 1 x^3 + 1 x^4 + 2 x^5 + 1 x^6 + 1 x^7$$ 
### Todos os Produtos Escalares Possíveis

Dadas duas listas  $a[]$  e  $b[]$  de comprimento  $n$ . Queremos calcular os produtos de  $a$  com cada deslocamento cíclico de  $b$ .

Geramos duas novas listas de tamanho  $2n$ : Invertemos  $a$  e acrescentamos  $n$  zeros a ele. E simplesmente acrescentamos  $b$  a si mesmo. Quando multiplicamos essas duas listas como polinômios, e olhamos para os coeficientes  $c[n-1],~ c[n],~ \dots,~ c[2n-2]$  do produto  $c$ , obtemos:
 
$$c[k] = \sum_{i+j=k} a[i] b[j]$$ 
E como todos os elementos  $a[i] = 0$  para  $i \ge n$ :

$$c[k] = \sum_{i=0}^{n-1} a[i] b[k-i]$$ 
É fácil ver que essa soma é apenas o produto escalar do vetor  $a$  com o  $(k - (n - 1))$ -ésimo deslocamento cíclico para a esquerda de  $b$ . Assim, esses coeficientes são a resposta para o problema, e ainda conseguimos obtê-la em  $O(n \log n)$  tempo. Note que  
$c[2n-1]$  também nos dá o  $n$ -ésimo deslocamento cíclico, mas isso é o mesmo que o  $0$ -ésimo deslocamento cíclico, então não precisamos considerar isso separadamente em nossa resposta.

### Duas Faixas

Dadas duas faixas booleanas (listas cíclicas de valores  $0$  e  $1$ )  $a$  e  $b$ . Queremos encontrar todas as maneiras de anexar a primeira faixa à segunda, de modo que em nenhuma posição tenhamos um  
$1$  da primeira faixa ao lado de um  $1$  da segunda faixa.

O problema na verdade não difere muito do problema anterior. Anexar duas faixas significa apenas que realizamos um deslocamento cíclico na segunda lista, e podemos anexar as duas faixas se o produto escalar das duas listas for  $0$ .

### Casamento de Strings

Dadas duas strings, um texto  $T$  e um padrão  $P$ , consistindo de letras minúsculas. Temos que calcular todas as ocorrências do padrão no texto.

Criamos um polinômio para cada string ( $T[i]$  e  $P[I]$  são números entre  $0$  e  $25$  correspondendo às  $26$  letras do alfabeto):
$$A(x) = a_0 x^0 + a_1 x^1 + \dots + a_{n-1} x^{n-1}, \quad n = |T|$$ 
com
 
$$a_i = \cos(\alpha_i) + i \sin(\alpha_i), \quad \alpha_i = \frac{2 \pi T[i]}{26}.$$ 
E

$$B(x) = b_0 x^0 + b_1 x^1 + \dots + b_{m-1} x^{m-1}, \quad m = |P|$$ 
com

$$b_i = \cos(\beta_i) - i \sin(\beta_i), \quad \beta_i = \frac{2 \pi P[m-i-1]}{26}.$$ 
Observe que com a expressão  $P[m-i-1]$  revertemos explicitamente o padrão.

Os coeficientes  $(m-1+i)$ th do produto dos dois polinômios  $C(x) = A(x) \cdot B(x)$  nos dirão se o padrão aparece no texto na posição  $i$ .

$$c_{m-1+i} = \sum_{j = 0}^{m-1} a_{i+j} \cdot b_{m-1-j} = \sum_{j=0}^{m-1} \left(\cos(\alpha_{i+j}) + i \sin(\alpha_{i+j})\right) \cdot \left(\cos(\beta_j) - i \sin(\beta_j)\right)$$ 
com  $\alpha_{i+j} = \frac{2 \pi T[i+j]}{26}$  e   $\beta_j = \frac{2 \pi P[j]}{26}$ 

Se houver uma correspondência, então  $T[i+j] = P[j]$ , e, portanto,  $\alpha_{i+j} = \beta_j$ . Isso dá (usando a identidade trigonométrica de Pitágoras):

$$\begin{align} c_{m-1+i} &= \sum_{j = 0}^{m-1} \left(\cos(\alpha_{i+j}) + i \sin(\alpha_{i+j})\right) \cdot \left(\cos(\alpha_{i+j}) - i \sin(\alpha_{i+j})\right) \\ &= \sum_{j = 0}^{m-1} \cos(\alpha_{i+j})^2 + \sin(\alpha_{i+j})^2 = \sum_{j = 0}^{m-1} 1 = m \end{align}$$ 
Se não houver uma correspondência, então pelo menos um caractere é diferente, o que leva a um dos produtos  $a_{i+1} \cdot b_{m-1-j}$  não ser igual a  $1$ , o que leva ao coeficiente  $c_{m-1+i} \ne m$ .

### Casamento de Strings com curingas

Esta é uma extensão do problema anterior. Desta vez, permitimos que o padrão contenha o caractere curinga  $\*$ , que pode corresponder a qualquer letra possível. Por exemplo, o padrão  $a*c$  aparece no texto  $abccaacc$  exatamente em três posições, nos índices  $0$ ,  $4$  e  $5$ .

Criamos os mesmos polinômios, exceto que definimos  $b_i = 0$  se $P[m-i-1] = *$ . Se  $x$  é o número de curingas em  $P$ , então teremos uma correspondência de  $P$  em  $T$  no índice  $i$  se  $c_{m-1+i} = m - x$ .