
Variáveis aleatórias são elementos fundamentais em estatística e probabilidade, representando resultados de processos aleatórios. 
Elas podem ser **discretas**, com valores enumeráveis e probabilidades associadas, ou **contínuas**, com um espectro infinito de possíveis valores, onde as probabilidades são expressas através de uma função densidade de probabilidade. 
A distribuição de probabilidades de uma variável aleatória é um conceito central que descreve como as probabilidades são atribuídas aos seus possíveis valores, seja por meio de tabelas, gráficos ou funções matemáticas. 
Cada tipo de distribuição tem suas próprias hipóteses e é aplicável a situações que correspondam a essas premissas. A correta aplicação de uma distribuição de probabilidades depende da adequação entre as hipóteses da distribuição e as características observadas na realidade.

## MODELOS PARA VARIÁVEIS ALEATÓRIAS DISCRETAS

Uma variável aleatória discreta assume um número finito ou infinito enumerável de valores.

### Modelo Geral

- *Função de Probabilidade*, f(x): A probabilidade de que a variável X assuma um particular valor x, é a função de probabilidade de X que se representa por$f(x) = P(X = x)$. A função $f(x)$ determina a distribuição de probabilidades da variável aleatória e, pode ser expressa por uma tabela, gráfico ou fórmula. $$f(x) = P(X = x)$$Para uma variável aleatória discreta, os possíveis valores podem ser listados, com as correspondentes probabilidades. Isto não ocorre para uma variável aleatória contínua, pois o espaço amostral em questão é infinito não enumerável.

- A **Função de Distribuição Acumulada (FDA)**, também conhecida como função de repartição, é uma função que mapeia cada número real ( x ) para a probabilidade de que uma variável aleatória ( X ) assuma um valor menor ou igual a ( x ). Em termos matemáticos, é expressa como:
$$F(x) = P(X \leq x)F(x)=P(X≤x)$$

Para uma variável aleatória **discreta**, a FDA é uma função degrau, onde cada salto corresponde à probabilidade de ( X ) assumir um determinado valor. Para uma variável aleatória **contínua**, a FDA é uma função contínua e suave, geralmente obtida pela integração da função densidade de probabilidade.

- **Discreta**: A função é descontínua e assume valores específicos em pontos particulares.
- **Contínua**: A função é contínua e é definida para todos os valores reais.

$$F(x) = \int_{-\infty}^{x} f(t) dtF(x)$$

Onde ( f(t) ) é a função densidade de probabilidade da variável aleatória ( X ).

### CARACTERÍSTICAS NUMÉRICAS:

- O **Valor Esperado** de uma variável aleatória, também conhecido como **esperança** ou **expectância**, é uma medida que resume a distribuição de probabilidade dessa variável. Para uma variável aleatória discreta $( X )$ que assume valores $( x_1, x_2, ..., x_i, ... )$ com probabilidades correspondentes $( p_1, p_2, ..., p_i, ... )$, o valor esperado $( E(X) )$ é calculado como:$$ E(X) = \sum_{i=1}^{\infty} p_i x_i $$Se a função de probabilidade ($f(x_i)$) é conhecida, o valor esperado também pode ser expresso como:$$ E(X) = \sum x_i f(x_i) $$Essencialmente, o valor esperado é a média ponderada dos possíveis valores que a variável aleatória pode assumir, com as probabilidades atuando como os pesos.

- A **variância** de uma variável aleatória discreta $( \sigma^2 )$ é uma medida que indica a dispersão dos valores em torno da média (valor esperado). A variância é definida como a média dos quadrados das diferenças entre cada valor e a média da variável aleatória. Matematicamente, para uma variável aleatória discreta $( X )$, a variância $( \sigma^2 )$ é expressa como:$$\sigma^2 = V(X) = E(X_i - E(X))^2$$A fórmula operacional para calcular a variância é:$$\sigma^2 = V(X) = E(X^2) - [E(X)]^2$$Onde $( E(X^2) )$ é a média dos quadrados dos valores que $( X )$ pode assumir, e $( E(X) )$ é o valor esperado de $( X )$. Para uma variável aleatória discreta que assume valores $( x_i )$ com probabilidades $( p_i )$, temos:$$E(X^2) = \sum_{i=1}^{\infty} x_i^2 p_i =\sum_{i=1}^∞​xi^2​pi​$$
- E o **desvio padrão** $( \sigma )$ é a raiz quadrada da variância, fornecendo uma medida de dispersão na mesma unidade da variável aleatória:

$$\sigma = DP(X) = +\sqrt{V(X)}​$$


## MODELOS PARA VARIÁVEIS ALEATÓRIAS CONTÍNUAS

### Modelo Geral

- A **Função Densidade de Probabilidade (f.d.p.)**, $f(x)$ para uma variável aleatória contínua $X$ é uma função que atende às seguintes condições:

1. $f(x) \geq 0$ para todo $( x )$ no conjunto de todos os números reais ($\mathbb{R}_x$).
2. A integral de $f(x)$ sobre $\mathbb{R}_x$ é igual a 1:$$\int_{\mathbb{R}_x} f(x) \, dx = 1$$
3. A função $f(x)$ não fornece diretamente valores de probabilidade. Para calcular a probabilidade de $X$  estar entre dois valores $x_1$ e $x_2$, calculamos a integral definida da função $f(x)$ entre $x_1$ e $x_2$:
$$    P(x_1 < X < x_2) = \int_{x_1}^{x_2} f(x) \, dx$$A probabilidade calculada é a área sob a curva de $f(x)$ entre $X = x_1$ e  $X = x_2$, com $x_1 < x_2$.

- A **Função de Distribuição Acumulada (FDA)**, $F(x)$ , para uma variável aleatória $X$, é definida como a probabilidade de $X$ ser menor ou igual a um valor $x$ . Matematicamente, é representada pela integral da função densidade de probabilidade $f(x)$ de $-\infty$ até $x$:$$F(x) = P(X \leq x) = \int_{-\infty}^{x} f(x) \, dx$$$$F(x) = \frac{d}{dx}F(X)$$As propriedades da FDA são:
- $( 0 \leq F(X) \leq 1 )$
- $\lim_{{x \to +\infty}} F(x) = 1$, ou seja, $F(+\infty) = 1$
- $\lim_{x \to -\infty} F(x) = 0$, ou seja, $F(-\infty) = 0$
- $F(X)$ é uma função não decrescente, portanto, se $( a < b )$, então $( F(a) \leq F(b) ).$

### Características Numéricas

- **Valor Esperado (E(X))**:$$ E(X) = \int_{-\infty}^{\infty} x \cdot f(x) \, dx $$

- **Variância (\( \sigma^2 \) ou V(X))**: $$ V(X) = E(X^2) - [E(X)]^2 = \int_{-\infty}^{\infty} x^2 \cdot f(x) \, dx - \left[] \int_{-\infty}^{\infty} x \cdot f(x) \, dx \right]^2 $$
- **Desvio Padrão (DP(X) ou $\sigma$**:$$ \sigma = DP(X) = \sqrt{V(X)} $$

Essas fórmulas são usadas para calcular as medidas de tendência central e dispersão de uma variável aleatória contínua, fornecendo informações importantes sobre a distribuição de probabilidade da variável.

## PROPRIEDADES DA MÉDIA E DA VARIÂNCIA DE VARIÁVEIS ALEATÓRIAS

#### **Média (E(X)):**
1. A média de uma constante ( k ) é a própria constante:
$$    E(k) = k$$
2. Multiplicando uma variável aleatória ( X ) por uma constante ( k ), a média é multiplicada pela constante:$$    E(kX) = kE(X)$$
3. Adicionando ou subtraindo uma constante ( k ) de uma variável aleatória ( X ), a média é somada ou subtraída pela constante:$$    E(X \pm k) = E(X) \pm k$$
4. A média da soma ou diferença de duas variáveis aleatórias ( X ) e ( Y ) é a soma ou diferença das médias:$$    E(X \pm Y) = E(X) \pm E(Y)$$
5. A média do produto de duas variáveis aleatórias independentes ( X ) e ( Y ) é o produto das médias:$$    E(XY) = E(X)E(Y)$$
#### **Variância (V(X)):**
1. A variância de uma constante é zero:$$    V(k) = 0$$
2. Multiplicando uma variável aleatória ( X ) por uma constante ( k ), a variância é multiplicada pelo quadrado da constante:
$$    V(kX) = k^2V(X)$$
3. Adicionando ou subtraindo uma constante ( k ) de uma variável aleatória ( X ), a variância não se altera:$$    V(X \pm k) = V(X)$$
4. A variância da soma ou diferença de duas variáveis aleatórias independentes ( X ) e ( Y ) é a soma das variâncias:$$    V(X \pm Y) = V(X) + V(Y)$$
5. A variância do produto de duas variáveis aleatórias independentes não é simplesmente o produto das variâncias (a menos que uma delas seja uma constante). Para variáveis não constantes, essa propriedade não se aplica diretamente.

Essas propriedades são úteis para simplificar cálculos e entender como diferentes operações afetam a distribuição de uma variável aleatória.