O numerador e o denominador de  $r_k$  podem ser vistos como polinômios multivariados de  $a_0, a_1, \dots, a_k$ :

$$r_k = \frac{P_k(a_0, a_1, \dots, a_k)}{Q_k(a_0,a_1, \dots, a_k)}.$$ 
A partir da definição de convergentes,

$$r_k = a_0 + \frac{1}{[a_1;a_2,\dots, a_k]}= a_0 + \frac{Q_{k-1}(a_1, \dots, a_k)}{P_{k-1}(a_1, \dots, a_k)} = \frac{a_0 P_{k-1}(a_1, \dots, a_k) + Q_{k-1}(a_1, \dots, a_k)}{P_{k-1}(a_1, \dots, a_k)}.$$ 
Daí segue que  $Q_k(a_0, \dots, a_k) = P_{k-1}(a_1, \dots, a_k)$ . Isso gera a relação

$$P_k(a_0, \dots, a_k) = a_0 P_{k-1}(a_1, \dots, a_k) + P_{k-2}(a_2, \dots, a_k).$$ 
Inicialmente,  $r_0 = \frac{a_0}{1}$  e  $r_1 = \frac{a_0 a_1 + 1}{a_1}$ , assim
 
$$\begin{align}P_0(a_0)&=a_0,\\ P_1(a_0, a_1) &= a_0 a_1 + 1.\end{align}$$ 
Para consistência, é conveniente definir  $P_{-1} = 1$  e  $P_{-2}=0$  e dizer formalmente que  $r_{-1} = \frac{1}{0}$  e  $r_{-2}=\frac{0}{1}$ .

Da análise numérica, é conhecido que o determinante de uma matriz tridiagonal arbitrária

 
$$T_k = \det \begin{bmatrix} a_0 & b_0 & 0 & \dots & 0 \\ c_0 & a_1 & b_1 & \dots & 0 \\ 0 & c_1 & a_2 & . & \vdots \\ \vdots & \vdots & . & \ddots & c_{k-1} \\ 0 & 0 & \dots & b_{k-1} & a_k \end{bmatrix}$$ 
pode ser calculado recursivamente como  $T_k = a_k T_{k-1} - b_{k-1} c_{k-1} T_{k-2}$ . Comparando-o com  $P_k$ , obtemos uma expressão direta
 
$$P_k = \det \begin{bmatrix} x_k & 1 & 0 & \dots & 0 \\ -1 & x_{k-1} & 1 & \dots & 0 \\ 0 & -1 & x_2 & . & \vdots \\ \vdots & \vdots & . & \ddots & 1 \\ 0 & 0 & \dots & -1 & x_0 \end{bmatrix}_{\textstyle .}$$ 
Esse polinômio também é conhecido como continuante devido à sua relação próxima com frações contínuas. O continuante não mudará se a sequência na diagonal principal for invertida. Isso fornece uma fórmula alternativa para calculá-lo:

$$P_k(a_0, \dots, a_k) = a_k P_{k-1}(a_0, \dots, a_{k-1}) + P_{k-2}(a_0, \dots, a_{k-2}).$$ 