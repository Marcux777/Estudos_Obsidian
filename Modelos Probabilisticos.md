
## MODELOS PARA VARIÁVEIS ALEATÓRIAS DISCRETAS

### *DISTRIBUIÇÃO DE BERNOULLI* 
Experimento de Bernoulli – é um experimento onde só podem correr dois resultados: “sucesso” ou “fracasso”. A probabilidade de sucesso é p e a probabilidade de fracasso é q = 1 – p.
#### CARACTERÍSTICAS NUMÉRICAS: 
- Média: 
	$E(X) = \sum^n_{i=1} p_i.x_i$
	$E(X) = P$
- Variância V(X): 
	${\sigma}^2 = V(X) = E(X^2) - [E(X)]^2 = p - p^2 = p(1-p) = p.q$  
	$V(X) = p.q$
- Desvio padrão: 
	DP(X)= + $\sqrt{p.q}$

### *DISTRIBUIÇÃO BINOMIAL ($X: B(n, p)$)*

- **Fórmula da Probabilidade Binomial**:$$ P(X = k) = \binom{n}{k} p^k (1-p)^{n-k} $$
- **Coeficiente Binomial**:$$ \binom{n}{k} = \frac{n!}{k!(n-k)!} $$
- **Número de ensaios** ($n$): Número total de experimentos realizados.
- **Número de sucessos** ($k$): Número de vezes que o resultado desejado ocorre.
- **Probabilidade de sucesso** ($p$): Probabilidade de um sucesso em um único ensaio.
- **Probabilidade de fracasso** ($q$ ): Probabilidade de um fracasso em um único ensaio, onde $q = 1 - p$.

#### CARACTERÍSTICAS NUMÉRICAS:

- Média:
	$E(X) = n.p$
- Variância:
	$V(X) = n.p.q$
- Desvio Padrão:
	$DP(x) = +\sqrt{n.p.q}$

### **DISTRIBUIÇÃO DE POISSON**

A distribuição de Poisson é útil para descrever as probabilidades do número de ocorrências num campo ou intervalo contínuo (em geral tempo ou espaço).

A utilização da distribuição de Poisson baseia-se nas seguintes hipóteses:  
- A probabilidade de uma ocorrência é a mesma em todo o campo de observação.
-  A probabilidade de mais de uma ocorrência num único ponto é aproximadamente zero. 
- O número de ocorrências em qualquer intervalo é independente do número de ocorrências em outros intervalos. 

Se uma v.a. é descrita por uma distribuição de Poisson, então a probabilidade de realizar (observar) qualquer número dado de ocorrências por unidade de medida (minuto, hora, centímetro, etc.) é dada pela fórmula:$$ P(X = k) = \frac{e^{-\lambda} \lambda^k}{k!} $$
#### CARACTERÍSTICAS NUMÉRICAS:

- Média: 
	$\mu = E(X) = \lambda$
- Variância:
	$\sigma^2 = V(X) = \lambda$
- Desvio Padrão:
	$\sigma = DP(X) = +\sqrt\lambda$

#### Aproximação de Poisson para eventos binomiais raros: 
A probabilidade de ocorrência de um valor x de uma distribuição Binomial, no caso limite; ou seja, quando n é muito grande ( $n → \infty$) e p muito pequeno ( $p → 0$), pode ser calculada por uma aproximação de Poisson, dada por:

  A probabilidade de ( $k$) sucessos é dada por:
  $$ P(X = k) = \frac{e^{-\lambda} \lambda^k}{k!}, onde \lambda = n.p$$

## MODELOS PARA VARIÁVEIS ALEATÓRIAS CONTÍNUAS

### DISTRIBUIÇÃO UNIFORME
Quando uma variável aleatória pode tomar qualquer valor numa escala contínua entre dois pontos a e b de tal maneira que nenhum valor seja mais provável que outro, então as probabilidades associadas à variável podem ser descritas pela distribuição uniforme.
- A função *densidade de probabilidade*, f(x), é dada por:$$
f(x) = 
\begin{cases} 
\frac{1}{b-a} & \text{se } a \leq x \leq b \\
0 & \text{se } x < a \text{ ou } x > b
\end{cases}
$$
- A função de distribuição acumulada, F(x), é dada por:$$
F(x) = P(X = x) = \int^x_{-\infty}\frac{1}{b-a}du = 
\begin{cases} 
0; & \text{se } x < a \\
\frac{x-a}{b-a}; & \text{se } a \leq x \leq b \\
1; & \text{se } x > b 
\end{cases}
$$
#### CARACTERÍSTICAS NUMÉRICAS:
- Média: 
	$$E(X) = \int^\infty_{-\infty} x.f(x)dx = \int^{b}_{a} x.\frac{1}{b-a}dx$$