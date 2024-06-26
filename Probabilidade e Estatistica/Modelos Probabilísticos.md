
## MODELOS PARA VARIÁVEIS ALEATÓRIAS DISCRETAS

### *DISTRIBUIÇÃO DE BERNOULLI* $(X: Ber(p))$ 
Experimento de Bernoulli – é um experimento onde só podem correr dois resultados: “sucesso” ou “fracasso”. A probabilidade de sucesso é p e a probabilidade de fracasso é q = 1 – p.
#### CARACTERÍSTICAS NUMÉRICAS: 
- Média: 
	$\large E(X) = \sum^n_{i=1} p_i.x_i$
	$\large E(X) = P$
- Variância V(X): 
	$\large {\sigma}^2 = V(X) = E(X^2) - [E(X)]^2 = p - p^2 = p(1-p) = p.q$  
	$\large V(X) = p.q$
- Desvio padrão: 
	DP(X)= + $\large \sqrt{p.q}$

### *DISTRIBUIÇÃO BINOMIAL ($X: B(n, p)$)*

- **Fórmula da Probabilidade Binomial**:$$\large P(X = k) = \binom{n}{k} p^k (1-p)^{n-k} $$
- **Coeficiente Binomial**:$$\large \binom{n}{k} = \frac{n!}{k!(n-k)!} $$
- **Número de ensaios** ($n$): Número total de experimentos realizados.
- **Número de sucessos** ($k$): Número de vezes que o resultado desejado ocorre.
- **Probabilidade de sucesso** ($p$): Probabilidade de um sucesso em um único ensaio.
- **Probabilidade de fracasso** ($q$ ): Probabilidade de um fracasso em um único ensaio, onde $q = 1 - p$.

#### CARACTERÍSTICAS NUMÉRICAS:

- Média:
	$\large E(X) = n.p$
- Variância:
	$\large V(X) = n.p.q$
- Desvio Padrão:
	$\large DP(x) = +\sqrt{n.p.q}$


### DISTRIBUIÇÃO HIPERGEOMÉTRICA $(X: hip(N,r,n))$
Essa é adequada quando consideramos extrações casuais feitas sem reposição de uma população dividida segundo dois atributos. 
A exemplo, considere uma população de $N$ objetos, $r$ dos quais têm o atributo $A$ e $N - r$ têm o atributo B. Um grupo de $n$ elementos é escolhido ao acaso, sem reposição. Estamos interessados em calcular a probabilidade de que esse grupo contenha $k$ elementos com o atributo $A$. Usando  principio multiplicativo, essa probabilidade é dada por $$\Large P_k = \frac{\binom{r}{k}.\binom{N - r}{n-k}}{\binom{N}{n}}$$
onde $\large max(0, n-N+r) \leq k \leq min(r, n)$

- Média:$$\large E(X) = n.p$$
- Variância: $$\large V(X) = n.p(1 - p)\frac{N-n}{N-1}$$
### **DISTRIBUIÇÃO DE POISSON**

A distribuição de Poisson é útil para descrever as probabilidades do número de ocorrências num campo ou intervalo contínuo (em geral tempo ou espaço).

A utilização da distribuição de Poisson baseia-se nas seguintes hipóteses:  
- A probabilidade de uma ocorrência é a mesma em todo o campo de observação.
-  A probabilidade de mais de uma ocorrência num único ponto é aproximadamente zero. 
- O número de ocorrências em qualquer intervalo é independente do número de ocorrências em outros intervalos. 

Se uma v.a. é descrita por uma distribuição de Poisson, então a probabilidade de realizar (observar) qualquer número dado de ocorrências por unidade de medida (minuto, hora, centímetro, etc.) é dada pela fórmula:$$\large P(X = k) = \frac{e^{-\lambda} \lambda^k}{k!} $$
#### CARACTERÍSTICAS NUMÉRICAS:

- Média: 
	$\large \mu = E(X) = \lambda$
- Variância:
	$\large \sigma^2 = V(X) = \lambda$
- Desvio Padrão:
	$\large \sigma = DP(X) = +\sqrt\lambda$

#### Aproximação de Poisson para eventos binomiais raros: 
A probabilidade de ocorrência de um valor x de uma distribuição Binomial, no caso limite; ou seja, quando n é muito grande ( $n → \infty$) e p muito pequeno ( $p → 0$), pode ser calculada por uma aproximação de Poisson, dada por:

  A probabilidade de ($k$) sucessos é dada por:
  $$\large P(X = k) = \frac{e^{-\lambda} \lambda^k}{k!}, onde \lambda = n.p$$

## MODELOS PARA VARIÁVEIS ALEATÓRIAS CONTÍNUAS

### DISTRIBUIÇÃO UNIFORME ($X: U(a,b)$)
Quando uma variável aleatória pode tomar qualquer valor numa escala contínua entre dois pontos a e b de tal maneira que nenhum valor seja mais provável que outro, então as probabilidades associadas à variável podem ser descritas pela distribuição uniforme.
- A função *densidade de probabilidade*, f(x), é dada por:$$\large
f(x) = 
\begin{cases} 
\frac{1}{b-a} & \text{se } a \leq x \leq b \\
0 & \text{se } x < a \text{ ou } x > b
\end{cases}
$$
- A função de distribuição acumulada, F(x), é dada por:$$\large
F(x) = P(X = x) = \int^x_{-\infty}\frac{1}{b-a}du = 
\begin{cases} 
0; & \text{se } x < a \\
\frac{x-a}{b-a}; & \text{se } a \leq x \leq b \\
1; & \text{se } x > b 
\end{cases}
$$
#### CARACTERÍSTICAS NUMÉRICAS $(X: \mu(\alpha, \beta))$:
- Média: $$\large E(X) = \int^\infty_{-\infty} x.f(x)dx = \int^{\beta}_{\alpha} x.\frac{1}{\beta-\alpha}dx$$$$E(X) = \frac{\alpha+\beta}{2}$$
- Variância:$$\large V(X) = \int^{\infty}_{-\infty} x^2.\frac{1}{b-a}dx - [E(X)]^2$$$$\large V(X) = \frac{(b-a)^2}{12}$$
- Desvio Padrão:$$\large \sigma = DP(X) = +\sqrt{V(X)}$$
### DISTRIBUIÇÃO EXPONENCIAL:
A distribuição exponencial envolve probabilidades ao longo do tempo ou da distância entre ocorrências num intervalo contínuo. Por exemplo, a exponencial descreve em sistemas de filas de espera o comportamento de variáveis tais como tempo médio entre as chegadas e tempo de serviço.

- **Função de densidade de probabilidade,** $f(x)$, é dada por:$$\large\begin{cases} 
0 & \text{, para } x < 0 \\
\lambda.e^{-\lambda.x}; & \text{, para } x \geq 0, \lambda > 0 
\end{cases}$$
- **função de distribuição acumulada,** $F(X)$, é dada por:$$\large\begin{cases}
0, x < 0; \\
\\
\int^{x}_{0}\lambda.e^{-\lambda.x}dx = 1-e^{-\lambda.x}, t>0
\\
\end{cases}
$$
### DISTRIBUIÇÃO NORMAL $(X: N(\mu, \sigma^2))$:
A distribuição normal é a mais importante distribuição de probabilidades, não apenas na teoria estatística, como também nas aplicações industriais. Tem uma posição única na teoria das probabilidades, pois pode ser utilizada como aproximação de outras distribuições. Por outro lado, a distribuição normal representa o resultado da atuação conjunta de causas aleatórias e, por isso, é fundamental no controle estatístico de processos, particularmente na teoria dos gráficos de controle de fabricação. Sua origem remontam a Gauss em seus trabalhos sobre erros de observações astronômicas, dando o nome de *distribuição gaussiana*.
- Definição: 
	Dizemos que a v.a. X tem distribuição normal com parâmetros $\mu$ e $\sigma^2$, $-\infty < \mu < +\infty$ e $0 < \sigma^2 < \infty$, se sua densidade é dada por $$\Large f(x; \mu, \sigma^2) = \frac{1}{\sigma\sqrt{2\pi}} e^{\frac{-(x - \mu)^2}{2\sigma^2}}$$
	Pode-se provar que $\large \int^\infty_{-\infty}f(x; \mu, \sigma^2)dx = 1$ e $\large f(x; \mu, \sigma^2) \geq 0$


![[Pasted image 20240407124816.png]]

- Média: $$\large E(X) = \mu$$
- Variância: $$\large V(X) = \sigma^2$$

Além disso, quando $\large f(x; \mu; \sigma^2) \rightarrow 0$, quando $\large x \rightarrow \pm \infty$, $\large \mu - \sigma$ e $\large \mu + \sigma$ são pontos de inflexão de $\large f(x; \mu, \sigma^2)$, $\large x = \mu$ é ponto de máximo de $\large f(x; \mu, \sigma^2)$, e o valor máximo é $\large \frac{1}{\sigma\sqrt{2\pi}}$. A densidade $\large f(x; \mu, \sigma^2)$ é simétrica em relação a reta $\large x = \mu$ , $$\Large f(\mu + x; \mu, \sigma^2) = f(\mu - x; \mu, \sigma^2)$$para todo $x$ real.

Usando a notação $X: N(\mu, \sigma^2)$.

Quando $\mu = 0$ e $\sigma^2 = 1$, temos uma distribuição *padrão* ou *reduzida*, ou, $N(0, 1)$. Para essa função de densidade $$\Large \phi(Z) = \frac{1}{\sqrt{2\pi}}e^{\frac{-Z^2}{2}}, -\infty < Z < \infty.$$
Se $X: N(\mu; \sigma^2)$, então v.a. definida por $$\Large Z = \frac{X - \mu}{\sigma}$$
Suponha, então, que X: $N(\mu, \sigma^2)$ e que queiramos $$\large P(a < X < b) = \int^b_af(x)dx$$
![[Pasted image 20240407140246.png]]

A integral não pode ser calculada analiticamente, e portanto a probabilidade
indicada só poderá ser obtida, aproximadamente, por meio de integração numérica.
No entanto, para cada valor de $μ$ e cada valor de $σ$, teríamos de obter $P(a < X < b)$ para
diversos valores de $a$ e $b$. Essa tarefa é facilitada através do uso de $\Large Z = \frac{X - \mu}{\sigma}$, de sorte que
somente é necessário construir uma tabela para a distribuição normal padrão.

Por exemplo, temos a transformação de $P(2 \leq X \leq 5)$ para $P(-0,25 \leq Z \leq 0,5)$

![[Pasted image 20240407141106.png]]

