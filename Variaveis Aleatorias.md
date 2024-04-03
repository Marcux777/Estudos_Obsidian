
Variáveis aleatórias são elementos fundamentais em estatística e probabilidade, representando resultados de processos aleatórios. 
Elas podem ser **discretas**, com valores enumeráveis e probabilidades associadas, ou **contínuas**, com um espectro infinito de possíveis valores, onde as probabilidades são expressas através de uma função densidade de probabilidade. 
A distribuição de probabilidades de uma variável aleatória é um conceito central que descreve como as probabilidades são atribuídas aos seus possíveis valores, seja por meio de tabelas, gráficos ou funções matemáticas. 
Cada tipo de distribuição tem suas próprias hipóteses e é aplicável a situações que correspondam a essas premissas. A correta aplicação de uma distribuição de probabilidades depende da adequação entre as hipóteses da distribuição e as características observadas na realidade.

## MODELOS PARA VARIÁVEIS ALEATÓRIAS DISCRETAS

Uma variável aleatória discreta assume um número finito ou infinito enumerável de valores.

### Modelo Geral:

- *Função de Probabilidade*, f(x): A probabilidade de que a variável X assuma um particular valor x, é a função de probabilidade de X que se representa por$f(x) = P(X = x)$. A função $f(x)$ determina a distribuição de probabilidades da variável aleatória e, pode ser expressa por uma tabela, gráfico ou fórmula. $$f(x) = P(X = x)$$
- A **Função de Distribuição Acumulada (FDA)**, também conhecida como função de repartição, é uma função que mapeia cada número real ( x ) para a probabilidade de que uma variável aleatória ( X ) assuma um valor menor ou igual a ( x ). Em termos matemáticos, é expressa como:
$$F(x) = P(X \leq x)F(x)=P(X≤x)$$

Para uma variável aleatória **discreta**, a FDA é uma função degrau, onde cada salto corresponde à probabilidade de ( X ) assumir um determinado valor. Para uma variável aleatória **contínua**, a FDA é uma função contínua e suave, geralmente obtida pela integração da função densidade de probabilidade.

- **Discreta**: A função é descontínua e assume valores específicos em pontos particulares.
- **Contínua**: A função é contínua e é definida para todos os valores reais.

$$F(x) = \int_{-\infty}^{x} f(t) dtF(x)=∫−∞x​f(t)dt$$

Onde ( f(t) ) é a função densidade de probabilidade da variável aleatória ( X ).