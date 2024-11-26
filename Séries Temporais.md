 
 ## 1. Introdução às Séries Temporais
---
### Definição e Conceitos Básicos
---
**Uma série temporal é uma coleção de observações feitas sequencialmente ao longo do tempo**. Isso significa que cada observação está associada a um momento específico. Por exemplo, se você medir a temperatura de uma cidade a cada hora, obterá uma série temporal das temperaturas horárias dessa cidade.

Existem duas formas de registrar uma série temporal:

- **Discreta:** Em uma série temporal discreta, as observações são realizadas em pontos específicos no tempo. Por exemplo, os dados de temperatura horária descritos acima são uma série temporal discreta. Outros exemplos incluem o valor de fechamento diário de uma ação ou a taxa de desemprego mensal.
- **Contínua:** Em uma série temporal contínua, as observações são feitas continuamente ao longo do tempo. Por exemplo, um eletrocardiograma (ECG) que registra a atividade elétrica do coração é uma série temporal contínua.

A análise de dados de séries temporais frequentemente envolve:

- Identificar os **componentes** da série temporal, como tendência, sazonalidade e ruído.
- Desenvolver **modelos** para descrever o comportamento da série temporal.
- Usar esses modelos para **prever** valores futuros da série temporal.

### Séries Temporais Univariadas vs. Multivariadas
---

Séries temporais podem ser classificadas em univariadas ou multivariadas, dependendo do número de variáveis monitoradas ao longo do tempo. Uma **série temporal univariada** envolve o acompanhamento de uma única variável ao longo do tempo, como a temperatura diária de uma cidade. Já uma **série temporal multivariada** abrange o registro simultâneo de múltiplas variáveis, como temperatura, umidade e velocidade do vento em um local específico. 

A distinção fundamental entre essas abordagens está na complexidade e na natureza das inter-relações: enquanto séries temporais univariadas são relativamente diretas e focam em uma única dimensão temporal, séries multivariadas requerem técnicas mais sofisticadas para capturar e modelar as interdependências entre variáveis.

A análise de séries temporais univariadas concentra-se em técnicas relativamente simples e diretas, como o cálculo de médias, variâncias e a avaliação da distribuição dos dados. Em contrapartida, a análise de séries temporais multivariadas se aprofunda nas correlações e inter-relações entre diferentes variáveis, empregando métodos como análise de correlação cruzada e gráficos de dispersão multivariados.

A extração de características (features) pode ser realizada manualmente, baseada no conhecimento do domínio e em estudos prévios. Outra abordagem é automatizar a extração, utilizando algoritmos que identificam características relevantes nos dados, como as ferramentas Catch22 e HCTSA.

No que se refere à modelagem, séries temporais univariadas frequentemente utilizam modelos como ARIMA (AutoRegressive Integrated Moving Average) e Suavização Exponencial, que são eficazes para capturar as dependências temporais dentro de uma única variável. Em contraste, séries temporais multivariadas exigem modelos mais complexos, como Vetor Autorregressivo (VAR) e VARIMA, que são projetados para lidar com interações simultâneas e retroalimentações entre múltiplas variáveis ao longo do tempo.

A escolha do modelo depende das características da série temporal e dos objetivos específicos da análise. Séries univariadas são particularmente adequadas para prever o comportamento de uma única variável ao longo do tempo, como as vendas de um produto. Por outro lado, séries multivariadas são mais úteis para examinar como diferentes variáveis se influenciam mutuamente, por exemplo, a interação entre indicadores econômicos e o desempenho do mercado de ações.

Assim, a distinção entre séries temporais univariadas e multivariadas não reside apenas no número de variáveis analisadas, mas também na complexidade dos métodos analíticos e de modelagem necessários para capturar os padrões e interações subjacentes. A análise e modelagem de séries multivariadas requerem um nível mais elevado de sofisticação técnica para explorar as relações dinâmicas que podem existir entre as diferentes variáveis. 

Essa distinção é fundamental para a escolha da metodologia apropriada ao se abordar problemas práticos, especialmente em contextos como finanças, meteorologia e ciências ambientais, onde a interação entre variáveis pode ter implicações significativas para a previsão e a tomada de decisão.

### Importância e Aplicações Práticas de Séries Temporais
---
A análise de séries temporais é essencial para compreender a dinâmica de sistemas complexos, prever valores futuros e desenvolver estratégias de controle. Ao investigar padrões e tendências ao longo do tempo, obtém-se uma compreensão aprofundada dos mecanismos subjacentes que geram os dados, possibilitando uma análise mais precisa e fundamentada. 
Além disso, os modelos de séries temporais são fundamentais para previsões, fornecendo suporte à tomada de decisões estratégicas, como a estimativa da demanda futura de produtos em uma organização ou a previsão do crescimento econômico de um país.

Entender a dinâmica de uma série temporal não apenas permite previsões mais precisas, mas também possibilita o desenvolvimento de estratégias de controle do sistema gerador dos dados. Por exemplo, o controle de qualidade em processos de manufatura pode se beneficiar da análise de séries temporais para identificar padrões de variação e implementar intervenções corretivas. Da mesma forma, a gestão do fluxo de eletricidade em redes de energia requer o uso de séries temporais para prever a demanda e otimizar o fornecimento, garantindo estabilidade e eficiência no sistema.

A aplicação da análise de séries temporais abrange múltiplos domínios do conhecimento. Em economia e finanças, é amplamente utilizada para analisar tendências de preços de ativos, taxas de juros e indicadores econômicos, sendo essencial para a formulação de estratégias de investimento e políticas econômicas. Em oceanografia, meteorologia e ciências da Terra, a análise de séries temporais é empregada para investigar mudanças climáticas e padrões atmosféricos, fornecendo subsídios para a compreensão de fenômenos naturais e para a formulação de políticas ambientais.

Na engenharia, séries temporais são usadas para monitorar processos industriais, enquanto na medicina, são aplicadas para entender a progressão de doenças e analisar dados fisiológicos, como sinais cardíacos e respiratórios. No campo da neurologia, a análise de séries temporais desempenha um papel crítico na avaliação de dados de eletroencefalogramas, auxiliando no diagnóstico e tratamento de distúrbios neurológicos.

Exemplos concretos de séries temporais incluem o valor de fechamento diário da Bolsa de Valores de São Paulo (BOVESPA) no contexto financeiro, a pressão atmosférica mensal em Fortaleza na área da meteorologia, e a concentração diária de poluentes atmosféricos nos Estados Unidos no campo ambiental. Esses exemplos ilustram a ampla variedade de fenômenos que podem ser investigados por meio da análise de séries temporais, com métodos específicos adaptados conforme as características dos dados e os objetivos da análise.

Na Imagem, tem o clássico exemplo da Série Temporal AirPassengers.

![[Pasted image 20241124162511.png]]
## 2. Componentes de uma Série Temporal
---
Os componentes de uma série temporal representam padrões distintos que contribuem para o comportamento geral de uma série, sendo fundamentais para análises e previsões precisas. Abaixo está um detalhamento de cada componente:

- **Tendência (Trend):** A tendência representa o **movimento de longo prazo** de uma série temporal. Ela indica a direção geral dos dados ao longo do tempo, seja crescente, decrescente ou relativamente constante. As tendências podem ser **lineares ou não lineares**, sendo a forma mais simples uma linha reta. Por exemplo, o aquecimento global, caracterizado pelo aumento das temperaturas globais ao longo de décadas, exemplifica uma tendência crescente. Reconhecer a tendência é essencial para compreender mudanças de longo prazo e fazer previsões informadas sobre o futuro.

- **Sazonalidade (Seasonality):** A sazonalidade refere-se a **flutuações periódicas** que ocorrem em **intervalos regulares dentro de um ano**. Esses padrões geralmente estão ligados a eventos de calendário, como feriados, estações do ano ou dias específicos da semana. A sazonalidade pode ser **aditiva** (quando o efeito sazonal é constante) ou **multiplicativa** (quando o efeito sazonal varia proporcionalmente ao nível da série temporal). Identificar a sazonalidade é vital para empresas e organizações tomarem decisões informadas sobre estoque, alocação de pessoal e campanhas de marketing.

- **Ciclicidade (Cycles):** Diferentemente da sazonalidade, os ciclos são padrões que se repetem em **períodos superiores a um ano**. Esses ciclos podem ser **irregulares em sua duração e magnitude** e não estão necessariamente relacionados a eventos de calendário. Fatores que contribuem para a ciclicidade incluem ciclos econômicos, mudanças demográficas ou fenômenos como variações de manchas solares. Compreender a ciclicidade é essencial para o planejamento de longo prazo e para decisões estratégicas, especialmente em áreas como economia e finanças.

- **Irregularidade ou Ruído (Irregularity or Noise):** A irregularidade ou o ruído representam as **flutuações aleatórias** em uma série temporal que **não podem ser explicadas pelos outros componentes**. O ruído pode surgir de diversas fontes, como erros de medição, eventos aleatórios ou flutuações imprevisíveis no sistema em análise. Embora o ruído possa obscurecer padrões subjacentes, é importante reconhecer que ele é uma parte inerente de muitas séries temporais do mundo real.

Ilustrando isso, temos a seguinte decomposição da Série Temporal AirPassangers
![[Pasted image 20241124174818.png]]
## 3. Estacionariedade
---
### Conceito de Estacionariedade
---
Uma série temporal é considerada **estacionária** se suas propriedades estatísticas permanecem constantes ao longo do tempo. Isso significa que a média, a variância e a autocorrelação da série não mudam com o tempo. Em outras palavras, um processo estacionário pode ser entendido como um processo em equilíbrio estatístico.

Muitos modelos de séries temporais assumem que os dados são estacionários, pois a estacionariedade simplifica a análise e permite o uso de uma gama mais ampla de métodos estatísticos. Caso uma série temporal não seja estacionária, ela pode frequentemente ser transformada em uma série estacionária utilizando diferenciação ou outros métodos.

### Testes para Estacionariedade
---
Existem diversos testes estatísticos que podem ser usados para avaliar a estacionariedade de uma série temporal. Um dos testes mais comuns é o **teste de Dickey-Fuller**. Esse teste baseia-se na ideia de que um processo com raiz unitária (um processo não estacionário) terá um coeficiente autorregressivo igual a 1. O teste de Dickey-Fuller examina a hipótese nula de que o coeficiente autorregressivo é igual a 1. Se a hipótese nula for rejeitada, a série temporal é considerada estacionária.

Há várias variações do teste de Dickey-Fuller, incluindo:

- **Teste de Dickey-Fuller Aumentado (Augmented Dickey-Fuller)**: Este teste inclui valores defasados da primeira diferença da série temporal como variáveis explicativas na equação de regressão, para levar em conta a correlação serial nos dados.

A escolha do teste dependerá das características específicas dos dados da série temporal.

Para os dados da tabela AirPassagers, podemos usar da seguinte forma

![[Pasted image 20241124162511.png]]

``` python
# Baixamos a biblioteca contendo as funções que queremos
%pip install statsmodels
# importa a função para realizar o teste
from statsmodels.tsa.stattools import adfuller

X = data['#Passengers'] # dataframe contendo os dados

result = adfuller(X) # teste aumentdado de Dickey-Fuller

print('ADF Estatíticas: %f' % result[0])  

print('Valor de P: %f' % result[1])

print('Valores Críticos:')

for key, value in result[4].items():
   print('\t%s: %.3f' % (key, value))
```
Obteremos a seguinte saída
```markdown
ADF Estatíticas: 0.815369 
Valor de P: 0.991880 
Valores Críticos: 
1%: -3.482 
5%: -2.884 
10%: -2.579
```
O teste ADF é usado para verificar se uma série temporal é estacionária. 
Se o valor $p$ for menor que um nível de significância (por exemplo, 0.05), rejeitamos a hipótese nula de que a série temporal tem uma raiz unitária (não é estacionária), indicando que a série é estacionária.
- ADF Estatísticas: 0.815369:
		Este é o valor da estatística do teste ADF. Ele é positivo e maior que todos os valores críticos fornecidos.
- Valor de P: 0.991880:
		Este é o valor p do teste. Um valor p de 0.991880 é muito alto, indicando que não há evidência suficiente para rejeitar a hipótese nula de que a série temporal tem uma raiz unitária (não é estacionária).
- Valores Críticos:
		1%: -3.482
		5%: -2.884
		10%: -2.579
	
Estes são os valores críticos para diferentes níveis de significância. Eles são usados para comparar com a estatística do teste ADF.

Com base nesses resultados, não podemos rejeitar a hipótese nula de que a série temporal tem uma raiz unitária. Isso significa que a série temporal não é estacionária. Em outras palavras, a série temporal possui tendências ou padrões que mudam ao longo do tempo, e não tem uma média constante, variância constante e autocorrelação constante ao longo do tempo.

### Métodos para Tornar uma Série Temporal Estacionária
---
Se uma série temporal for identificada como não estacionária, existem diversos métodos que podem ser utilizados para transformá-la em uma série estacionária. Alguns métodos comuns incluem:

- **Diferenciação (Differencing):** Consiste em subtrair observações consecutivas. Por exemplo, a primeira diferença de uma série temporal é calculada subtraindo o valor no tempo _$t-1$_ do valor no tempo _$t$_. A diferenciação pode remover tendências e sazonalidade de uma série temporal.
    
- **Transformação Logarítmica:** Envolve o uso do logaritmo natural da série temporal, o que pode ajudar a estabilizar a variância da série.
    
- **Ajuste Sazonal:** Consiste em remover o componente sazonal de uma série temporal. Isso pode ser feito usando métodos como médias móveis ou variáveis dummy.

A escolha do método dependerá das características específicas da série temporal e da natureza da não estacionariedade. Vale notar que esses métodos são descritos no contexto de dados econômicos, mas sua aplicação a outros domínios pode exigir considerações adicionais.

No caso da AirPassagers, aceitamos a hipótese nula de que ela é não estacionária, pois o valor de $p$ é muito superior ao nível de significância $0.05$. Assim, devemos fazer a transformação da série em estacionaria.
Aplicando a transformação logarítmica:
``` python
import numpy as np
import matplotlib.pylab as plt
d_log=np.log(data) # lista contendo os dados transformados com log do numpy

plt.plot(d_log)

plt.show()
```

![[Pasted image 20241125184710.png]]

Podemos vê uma diminuição da escala do grafico
```python
from statsmodels.tsa.stattools import adfuller

result = adfuller(d_log) # Fazendo a verificação da Estacionariedade
print('Valor de P: %f' % result[1])
```
Obteremos
```markdown
Valor de P: 0.422367
```

Podemos chegar a seguinte conclusão: 
Mesmo após a transformação logarítmica, a série temporal ainda não é estacionária, pois o valor p é maior que o nível de significância comum (0.05). Isso significa que a série ainda possui tendências ou padrões que mudam ao longo do tempo.
## 4. Modelos de Séries Temporais
---
### 4.1. Modelos Autorregressivos (AR) na Análise de Séries Temporais
---
Os modelos autorregressivos (AR) são uma classe fundamental de modelos de séries temporais usados para prever valores futuros com base em observações passadas. A característica definidora de um modelo AR é expressar o valor atual de uma série temporal como uma combinação linear de seus próprios valores passados, somados a um termo de erro aleatório.

#### Estrutura dos Modelos AR

Um modelo AR de ordem *p*, denotado como AR(*p*), pode ser matematicamente representado como:

$$Y_t = c + φ_1 Y_{t-1} + φ_2 Y_{t-2} + … + φ_p Y_{t-p} + ε_t$$

Onde:

- **$Y_t$** é o valor da série temporal no tempo *t*
- **$c$** é o termo constante (intercepto)
- **$φ_1, φ_2, …, φ_p$** são os coeficientes autorregressivos que determinam a influência dos valores passados
- **$Y_{t-1}, Y_{t-2}, …, Y_{t-p}$** representam os valores da série temporal em passos de tempo anteriores (defasagens)
- **$ε_t$** é o termo de erro aleatório, geralmente assumido como ruído branco (sequência de variáveis independentes e identicamente distribuídas com média zero e variância constante)

#### Ordem dos Modelos AR

A ordem de um modelo AR (*p*) indica quantos valores defasados são usados para prever o valor atual. Por exemplo:

- Um modelo **AR(1)** usa apenas o valor do passo de tempo anterior (uma defasagem).
- Um modelo **AR(2)** utiliza os valores dos dois passos de tempo anteriores (duas defasagens).

A escolha da ordem apropriada é crucial e geralmente determinada por análises das funções de autocorrelação e autocorrelação parcial da série temporal.

#### Estacionariedade

Um pressuposto-chave em muitos modelos de séries temporais, incluindo os AR, é que os dados sejam estacionários.

A estacionariedade de um processo AR depende dos parâmetros autorregressivos. Se as raízes da equação característica (formada pelos coeficientes AR) estiverem fora do círculo unitário, o processo AR é considerado estacionário. Essa condição garante que a influência de choques passados decaia com o tempo, levando a um processo estável.

#### Aplicações

Os modelos AR têm ampla aplicação em várias áreas, como:

- **Previsão de valores futuros:** Prever valores futuros de uma série temporal com base no comportamento passado.
- **Entendimento das dinâmicas subjacentes:** Identificar padrões e relações nos dados, como a persistência de choques ou a presença de ciclos.
- **Modelagem e simulação de sistemas:** Criar modelos que capturam o comportamento de sistemas complexos ao longo do tempo.

### 4.2. Explorando Modelos de Média Móvel (MA)
---
Os modelos de média móvel (MA) constituem outra família fundamental de modelos de séries temporais. Em contraste com os modelos AR, que se baseiam nas defasagens da própria variável, os modelos MA expressam o valor atual como uma função linear dos valores presentes e passados de um termo de erro aleatório. Este termo de erro, frequentemente chamado de "ruído branco", é assumido como uma sequência de variáveis independentes e identicamente distribuídas, com média zero e variância constante.

#### Estrutura dos Modelos MA

Um modelo MA de ordem *q*, denotado como MA(*q*), é representado matematicamente como:

$$Y_t = μ + ε_t + θ_1 ε_{t-1} + θ_2 ε_{t-2} + … + θ_q ε_{t-q}$$

Onde:

- **$Y_t$** é o valor da série temporal no tempo *t*
- **$μ$** é a média do processo
- **$θ_1, θ_2, …, θ_q$** são os coeficientes MA
- **$ε_t, ε_{t-1}, …, ε_{t-q}$** representam os termos de erro (ruído branco) nos tempos *t, t-1, t-2, …, t-q*

#### Ordem dos Modelos MA

A ordem de um modelo MA (*q*) indica o número de termos de erro defasados usados no modelo. Por exemplo:

- Um modelo **MA(1)** usa apenas o termo de erro atual e o termo de erro do passo de tempo anterior.
- Um modelo **MA(2)** considera o termo de erro atual e os termos de erro dos dois passos de tempo anteriores.

A escolha da ordem apropriada é geralmente feita com base na análise das funções de autocorrelação (ACF) e autocorrelação parcial (PACF) da série temporal.

#### Invertibilidade

A **invertibilidade** é um conceito importante nos modelos MA. Ela garante que um modelo MA possa ser representado como um modelo AR de ordem infinita. Essa característica é essencial para a estimativa única dos parâmetros e para a seleção do modelo mais adequado para uma série temporal.

#### Previsão

Ao prever com um modelo MA, os termos de erro estimados (obtidos durante o ajuste do modelo) são usados para calcular os valores futuros da série. Para horizontes de previsão maiores que a ordem do componente MA, as previsões tendem para a média do processo.

#### Aplicações

Os modelos MA são ferramentas valiosas na análise de séries temporais, úteis para:

- **Identificar padrões:** Detectar padrões nos dados causados por choques ou distúrbios aleatórios.
- **Suavizar dados:** Reduzir flutuações nos dados para destacar tendências subjacentes.
- **Realizar previsões:** Prever valores futuros da série após o ajuste do modelo.

#### Pontos Adicionais sobre Modelos MA

- **Estimação por Máxima Verossimilhança:** Os parâmetros de um modelo MA podem ser estimados usando o método de máxima verossimilhança, assumindo erros normalmente distribuídos.
- **Verificação Diagnóstica:** Após ajustar um modelo MA, é fundamental realizar uma análise diagnóstica para avaliar sua adequação. Técnicas como análise de resíduos e exame das funções de autocorrelação ajudam a verificar se as suposições do modelo são atendidas.

#### Dados Não Estacionários e Seleção do Modelo

- **Dados Não Estacionários:** Os modelos MA geralmente são projetados para dados estacionários. Se os dados apresentarem tendência ou sazonalidade, podem ser necessárias transformações, como diferenciação, para alcançar a estacionariedade antes de aplicar o modelo.
- **Seleção do Modelo:** Escolher a ordem apropriada para um modelo MA é crucial. Isso pode ser orientado pela análise das funções de autocorrelação (ACF) e critérios de informação, como AIC ou BIC.

Os modelos MA, junto com os modelos AR, formam a base para o entendimento de modelos mais complexos, como ARMA, ARIMA e SARIMA. Compreender sua estrutura e propriedades é essencial para a análise eficaz de séries temporais.

---
### 4.3. Modelos Autorregressivos de Média Móvel (ARMA)
---
Os modelos ARMA são um conceito central na análise de séries temporais, oferecendo uma estrutura poderosa para modelar e prever dados com dependências temporais. Eles combinam os recursos dos modelos autorregressivos (AR) e de média móvel (MA), permitindo uma representação mais flexível e abrangente do processo gerador dos dados.

#### Estrutura e Definição

Um modelo ARMA, denotado como ARMA(*p, q*), é um modelo linear que utiliza tanto os valores defasados da série temporal (componente AR) quanto os valores defasados do termo de erro (componente MA). Matematicamente, um processo ARMA(*p, q*) é definido como:

$$Y_t = c + φ_1 Y_{t-1} + φ_2 Y_{t-2} + … + φ_p Y_{t-p} + ε_t + θ_1 ε_{t-1} + θ_2 ε_{t-2} + … + θ_q ε_{t-q}$$

Onde:

- **$Y_t$** é o valor da série temporal no tempo *t*.
- **$c$** é um termo constante.
- **$φ_1, φ_2, …, φ_p$** são os coeficientes AR, representando a influência de valores passados da série temporal.
- **$ε_t, ε_{t-1}, …, ε_{t-q}$** são os termos de erro (ruído branco) nos tempos *t, t-1, …, t-q*.
- **$θ_1, θ_2, …, θ_q$** são os coeficientes MA, refletindo a influência de choques passados nos valores atuais.

#### Estacionariedade

A estacionariedade em processos ARMA depende exclusivamente do componente AR. O processo é estacionário se as raízes da equação característica:
**$$1 - φ_1 z - φ_2 z^2 - … - φ_p z^p = 0$$**

estiverem fora do círculo unitário. Isso garante que o processo tenha média e variância constantes ao longo do tempo.

#### Invertibilidade

A **invertibilidade** é uma propriedade relacionada ao componente MA. Ela assegura que o componente MA possa ser expresso como uma representação AR de ordem infinita, permitindo a estimação única dos parâmetros. Por exemplo, um processo MA(1) é invertível se o valor absoluto do coeficiente MA (|**$θ_1$**|) for menor que 1.

#### Autocovariância e Autocorrelação

As funções de autocovariância e autocorrelação de processos ARMA são essenciais para compreender a estrutura de dependência temporal dos dados e identificar o modelo adequado.

#### Estimação de Parâmetros

Os parâmetros de um modelo ARMA são geralmente estimados por **máxima verossimilhança**, assumindo erros normalmente distribuídos. Esse método maximiza a função de verossimilhança para obter estimativas dos coeficientes AR, MA e da variância do termo de erro.

#### Previsão

Modelos ARMA ajustados podem ser usados para prever valores futuros da série. Eles utilizam os parâmetros estimados e informações sobre valores e erros passados para gerar previsões para pontos futuros.

#### Identificação e Seleção do Modelo

A seleção das ordens *p* (AR) e *q* (MA) é feita analisando as funções de autocorrelação (ACF) e autocorrelação parcial (PACF). Critérios de informação, como **AIC** e **BIC**, também ajudam na comparação de modelos, penalizando aqueles com mais parâmetros.

#### Exemplos e Aplicações

Os modelos ARMA são amplamente aplicados em diversas áreas, incluindo:

- **Economia e Finanças:** Modelagem de séries temporais financeiras, como preços de ações e taxas de câmbio.
- **Ciências Naturais:** Previsão de padrões climáticos e processos geofísicos.
- **Engenharia:** Monitoramento e controle de processos industriais.

Um exemplo prático é o modelo ARMA(1, 1), que combina um único termo AR e um único termo MA:
**$$Y_t = c + φ_1 Y_{t-1} + ε_t + θ_1 ε_{t-1}$$**

#### Extensões e Considerações

- **Extensões:** Os modelos ARMA servem como base para modelos mais avançados, como ARIMA (para dados não estacionários) e SARIMA (para dados sazonais).
- **Estacionariedade:** Antes de aplicar ARMA, é fundamental verificar se os dados são estacionários. Caso contrário, transformações como diferenciação podem ser necessárias.
- **Implementação Prática:** Embora as fontes se concentrem nos fundamentos teóricos, ferramentas como Python (bibliotecas `statsmodels` e `pmdarima`) e R (pacote `forecast`) são úteis para a implementação prática.

Os modelos ARMA são componentes essenciais da análise de séries temporais, fornecendo um equilíbrio entre simplicidade e poder preditivo. A escolha do modelo ideal deve sempre considerar as características dos dados, os diagnósticos do modelo e o objetivo da análise.

---
### 4.4. Modelos Autorregressivos Integrados de Médias Móveis (ARIMA)

---

Os modelos ARIMA são uma classe de modelos estatísticos amplamente utilizados para a previsão de séries temporais, especialmente úteis para séries não estacionárias, cujas propriedades estatísticas, como média e variância, mudam ao longo do tempo. O acrônimo ARIMA representa três componentes principais: Autoregressivo (AR), Integrado (I) e Média Móvel (MA).

O componente **Autoregressivo (AR)** utiliza valores passados da série temporal para prever valores futuros, onde o número de valores defasados usados é denotado por *p*. Por exemplo, um modelo AR(1) usa apenas o valor anterior da série, enquanto um modelo AR(2) utiliza os dois valores anteriores. Já o componente **Integrado (I)** lida com a não estacionariedade da série, envolvendo a diferenciação dos dados para remover tendências ou sazonalidades. A ordem de diferenciação é indicada por *d*, e uma série que se torna estacionária após ser diferenciada uma vez é classificada como I(1). O componente **Média Móvel (MA)** utiliza erros de previsão passados para prever valores futuros, com o número de termos de erro defasados indicado por *q*. Um modelo MA(1) considera apenas o erro do período anterior, enquanto MA(2) utiliza os dois erros anteriores.

Um modelo ARIMA é denotado como **ARIMA(p, d, q)**. Ao aplicar diferenças de ordem *d* a um processo ARIMA(p, d, q), ele se torna um processo estacionário ARMA(p, q). A seleção dos parâmetros *p*, *d* e *q* é crucial para o sucesso do modelo, e métodos como a análise das funções de autocorrelação (ACF) e autocorrelação parcial (PACF), testes de raiz unitária (como o Dickey-Fuller) e critérios de informação (AIC e BIC) são úteis para identificar os valores mais adequados.

Os modelos ARIMA apresentam propriedades importantes, como **estacionariedade**, que depende dos parâmetros AR, e **invertibilidade**, que garante que um modelo MA possa ser representado como um modelo AR de ordem infinita, assegurando a unicidade na estimativa dos parâmetros. 

Modelos ARIMA são amplamente usados para **previsão**, utilizando dados históricos para ajustar os parâmetros e prever valores futuros. A combinação dos componentes AR e MA pode resultar em modelos mais complexos, como ARMA(p, q). A **estimação de máxima verossimilhança** é frequentemente utilizada para ajustar os parâmetros, assumindo erros normalmente distribuídos. Além disso, a **representação em espaço de estados** oferece uma forma conveniente de representar sistemas dinâmicos e permite o uso do filtro de Kalman para estimativa e previsão.

Há várias **extensões e conceitos relacionados** aos modelos ARIMA. A **integração fracionária** lida com memórias longas, onde os efeitos dos choques persistem por longos períodos. Os **modelos VAR (Vetores Autorregressivos)** estendem os princípios dos modelos AR para séries multivariadas, capturando as relações entre múltiplas variáveis. Já a **cointegração** analisa equilíbrios de longo prazo entre variáveis não estacionárias, sendo um conceito fundamental para entender relações entre diferentes séries temporais.

Na prática, ferramentas como `statsmodels` em Python e o pacote `forecast` em R são amplamente utilizadas para ajustar modelos ARIMA, realizar diagnósticos e prever valores futuros, facilitando a aplicação prática e a interpretação dos resultados. Essas ferramentas permitem análises robustas de séries temporais, sendo amplamente aplicáveis em áreas como finanças, economia e ciências ambientais. A escolha do modelo ideal depende das características dos dados, do objetivo da análise e dos diagnósticos realizados, garantindo a melhor performance preditiva e interpretação dos resultados.

---
## 5. Decomposição de Séries Temporais
---
A decomposição de séries temporais é uma técnica estatística avançada que permite desagregar uma série temporal em seus componentes fundamentais, como tendência, sazonalidade e ruído. Essa abordagem é essencial para entender a dinâmica subjacente dos dados, possibilitando uma análise mais precisa e a construção de modelos preditivos mais robustos.

### Métodos Fundamentais de Decomposição

Dois métodos principais são amplamente utilizados na decomposição de séries temporais: a abordagem aditiva e a multiplicativa. Cada método é adequado para diferentes tipos de séries, dependendo da natureza dos componentes envolvidos.

#### Decomposição Aditiva

A decomposição aditiva pressupõe que a série temporal é a soma dos componentes de tendência, sazonalidade e ruído:
$$Yt​=Tt​+St​+Rt​$$

Onde:

- **$Y_t$**: Valor observado da série temporal no tempo _t_.
    
- **$T_t$**: Componente de tendência no tempo _t_.
    
- **$S_t$**: Componente sazonal no tempo _t_.
    
- **$R_t$**: Componente residual ou ruído no tempo _t_.
    

Este método é ideal para séries temporais nas quais as flutuações sazonais têm uma magnitude relativamente constante, independentemente do nível da tendência. Por exemplo, se uma loja vende consistentemente 100 unidades adicionais de um produto em dezembro, independentemente de um crescimento ou declínio geral nas vendas, a decomposição aditiva seria mais apropriada.

#### Decomposição Multiplicativa

A decomposição multiplicativa, por outro lado, assume que a série temporal é o produto dos componentes de tendência, sazonalidade e ruído: $$Yt​=Tt​×St​×Rt​$$

Essa abordagem é recomendada quando a magnitude das flutuações sazonais é proporcional ao nível da tendência. Ou seja, os efeitos sazonais aumentam ou diminuem em proporção direta ao valor da tendência. Por exemplo, se as vendas de uma loja aumentam em 20% a cada dezembro e esse aumento é proporcional ao volume total de vendas, o modelo multiplicativo capturará essa relação de forma mais precisa.

### Critérios para Escolha entre Métodos Aditivo e Multiplicativo

A escolha entre os modelos aditivo e multiplicativo depende principalmente da natureza dos padrões sazonais da série temporal:

- **Modelo Aditivo**: Deve ser utilizado quando os padrões sazonais são constantes em termos de amplitude, independentemente do nível da tendência.
    
- **Modelo Multiplicativo**: É mais adequado quando os padrões sazonais variam proporcionalmente ao nível da tendência.
    

Visualizar a série temporal frequentemente oferece insights valiosos sobre qual abordagem de decomposição é mais apropriada, facilitando a escolha do método correto para a análise.

### Decomposição Clássica de Séries Temporais

A decomposição clássica de séries temporais é um método padrão para desagregar uma série em componentes básicos que ajudam a identificar padrões persistentes nos dados.

#### Componentes da Decomposição Clássica

1. **Tendência ($T_t$)**: Reflete o padrão de longo prazo da série, indicando a direção geral (crescente, decrescente ou estável) ao longo do tempo.
    
2. **Sazonalidade ($S_t$)**: Representa padrões que se repetem em intervalos regulares, como meses ou trimestres, geralmente associados a ciclos anuais ou mensais.
    
3. **Ciclicidade ($C_t$)**: Flutuações de longo prazo que não possuem uma frequência fixa, muitas vezes relacionadas a ciclos econômicos ou de mercado.
    
4. **Irregularidade ($I_t$)**: Componente residual que captura flutuações aleatórias ou eventos imprevisíveis, muitas vezes considerados ruído.
    

#### Modelos Aditivo e Multiplicativo na Decomposição Clássica

- **Modelo Aditivo**: Usado quando as flutuações sazonais têm amplitude constante.
    
- **Modelo Multiplicativo**: Adequado quando a magnitude da sazonalidade varia proporcionalmente ao nível da tendência.
    

#### Etapas da Decomposição Clássica

1. **Estimativa da Tendência**: A tendência pode ser estimada por métodos como médias móveis ou regressão linear, fornecendo uma visão clara do comportamento de longo prazo.
    
2. **Estimativa da Sazonalidade**: A sazonalidade é determinada removendo a tendência da série original e tomando a média dos valores correspondentes de ciclos repetidos, como meses ou estações do ano.
    
3. **Estimativa da Ciclicidade**: A separação da ciclicidade pode ser desafiadora, e muitas vezes ela é agrupada com o componente de irregularidade.
    
4. **Estimativa da Irregularidade**: O componente residual é obtido subtraindo os componentes de tendência, sazonalidade e ciclicidade da série original.
    

#### Limitações da Decomposição Clássica

- **Assume Relações Simples**: A decomposição clássica depende de uma relação estritamente aditiva ou multiplicativa entre os componentes, o que pode não capturar a complexidade de séries mais sofisticadas.
    
- **Sensibilidade a Outliers**: Valores atípicos podem distorcer as estimativas dos componentes, reduzindo a precisão do modelo.
    
- **Incapacidade de Lidar com Padrões Não Lineares**: Séries temporais com padrões altamente não lineares podem não ser bem representadas pela decomposição clássica.
    

#### Alternativas Modernas

- **STL (Seasonal and Trend Decomposition using Loess)**: Uma abordagem mais flexível e robusta que permite capturar padrões não lineares de forma eficaz.
    
- **Método X-11**: Um método iterativo avançado que ajusta sazonalidade e tendência repetidamente até uma convergência satisfatória, oferecendo uma análise mais detalhada dos componentes.
    

A decomposição de séries temporais desempenha um papel crucial na análise exploratória, auxiliando na compreensão dos padrões subjacentes e na preparação dos dados para técnicas de modelagem mais avançadas. A escolha do método de decomposição adequado depende das características da série e do objetivo específico da análise.
## 6. Previsão em Análise de Séries Temporais

### O que é Previsão?

**A previsão em séries temporais é o processo de estimativa de valores futuros de uma variável com base em seu comportamento e padrões passados.** Esse processo envolve a modelagem das interações temporais que determinam a evolução de sistemas dinâmicos, sendo um elemento central da análise de séries temporais, com aplicações em disciplinas como economia, finanças, meteorologia, entre outras.

- A previsão transcende a simples extrapolação, incorporando as dinâmicas inerentes e as incertezas dos dados históricos.
- Pode ser realizada exclusivamente com base nos valores históricos da série temporal ou integrar outras variáveis exógenas relevantes ao modelo.
- As técnicas de previsão variam de métodos estatísticos de ajuste de curvas a algoritmos sofisticados de aprendizado de máquina, dependendo das características e da complexidade dos dados.

### Importância da Previsão

- **Compreensão de Sistemas Complexos**: A análise de dados de séries temporais permite compreender a dinâmica e prever a evolução futura de sistemas complexos, sendo valiosa para decisões estratégicas, alocação de recursos, gestão de riscos e formulação de políticas.

- **Insights Baseados em Dados**: À medida que o volume de dados cresce exponencialmente, há uma demanda crescente por técnicas robustas de previsão de séries temporais para extrair insights significativos e antecipar tendências.

- **Aplicações em Diversas Disciplinas**:
  - **Meteorologia**: A previsão de padrões climáticos é essencial para mitigar riscos de desastres naturais, além de apoiar atividades econômicas como agricultura e logística.
  - **Finanças**: Previsão de preços de ativos, tendências de mercado e indicadores macroeconômicos são fundamentais para a tomada de decisões de investimento e planejamento financeiro.
  - **Ciências Ambientais**: Estimativas sobre mudanças climáticas, níveis de poluição e disponibilidade de recursos são críticas para políticas públicas e práticas sustentáveis.

### Métodos de Previsão

Os métodos de previsão destacam-se em uma ampla gama, abrangendo desde abordagens clássicas até técnicas modernas de aprendizado de máquina:

- **Médias Móveis (MA)**: Calcula a média de valores anteriores em uma janela temporal específica para suavizar flutuações e prever valores futuros. Essa técnica é particularmente eficaz em horizontes de curto prazo.

- **Modelos Autorregressivos (AR)**: Utilizam valores passados da série temporal como preditores de valores futuros, baseando-se em relações lineares entre as observações.

- **Modelos ARMA e ARIMA**: Combinam componentes autorregressivos (AR) e de médias móveis (MA), enquanto o ARIMA inclui diferenciação para tratar séries não estacionárias.

- **Suavização Exponencial**: Atribui pesos decrescentes exponencialmente às observações passadas, dando maior importância aos dados mais recentes, sendo útil para séries com tendências e sazonalidades.

- **Modelo Theta**: Disponível na biblioteca `statsmodels` do Python, oferece uma abordagem flexível e eficiente para modelar séries temporais com diferentes padrões.

- **Silverkite**: Desenvolvido pelo LinkedIn, é capaz de capturar sazonalidades e tendências complexas em séries temporais.

- **Prophet**: Desenvolvido pelo Facebook, este modelo permite incorporar sazonalidades, tendências e efeitos de feriados, fornecendo uma abordagem prática e flexível para dados com padrões complexos.

- **Aprendizado Supervisionado**: Algoritmos como XGBoost, que utilizam técnicas de gradient boosting, podem ser aplicados à previsão de séries temporais tratando-a como um problema de aprendizado supervisionado.

- **Aprendizado Profundo**: Arquiteturas como DeepAR são amplamente utilizadas em previsão de séries temporais multivariadas, especialmente devido à sua capacidade de capturar dependências complexas entre múltiplas variáveis ao longo do tempo.

### Avaliação da Precisão da Previsão

A avaliação da precisão das previsões é fundamental e pode ser feita por meio de várias métricas de erro. Uma métrica comum é o **erro de previsão (ou resíduo)**, definido como: $$e_t = yt − f(xt​)$$
- **$e_t$**: Erro de previsão no tempo $t$.
- **$y_t$**: Valor real no tempo $t$.
- **$f(x_t)$**: Valor previsto pelo modelo no tempo $t$.

Outras métricas, como a soma dos erros ao quadrado (SSE) e o erro quadrático médio (MSE), são amplamente utilizadas para quantificar a precisão das previsões e comparar o desempenho de diferentes modelos.

## Considerações Importantes

- **Pré-processamento de Dados**: Dados de séries temporais geralmente requerem tratamento prévio, como limpeza, tratamento de valores ausentes e remoção de outliers, para garantir a qualidade das previsões.

- **Seleção do Modelo**: A escolha do método de previsão mais adequado depende das características específicas da série temporal, como estacionaridade, sazonalidade e o horizonte de previsão desejado.

- **Ajuste de Parâmetros**: Muitos métodos de previsão requerem ajuste cuidadoso de parâmetros para otimizar a performance do modelo. Técnicas de validação cruzada e otimização bayesiana podem ser usadas para determinar os melhores hiperparâmetros.

- **Estimativa de Incerteza**: É crucial considerar a incerteza inerente às previsões e fornecer intervalos de confiança ou previsão, a fim de comunicar a confiabilidade das estimativas.

A compreensão profunda dos princípios, métodos e desafios envolvidos na previsão de séries temporais permite uma modelagem mais precisa e a geração de estimativas informadas sobre o comportamento futuro de sistemas dinâmicos. A seleção e aplicação das técnicas de previsão devem sempre ser adaptadas às características particulares dos dados e aos objetivos da análise em questão.


---
## 7. **Detecção de Anomalias**

A **detecção de anomalias** em séries temporais é o processo de identificar observações que se desviam significativamente do comportamento esperado dos dados ao longo do tempo. Essas anomalias podem resultar de erros de medição, mudanças no comportamento ou eventos inesperados.

Para detectar anomalias em séries temporais, é essencial compreender as propriedades estatísticas da série e aplicar modelos adequados. Em séries estacionárias, as anomalias podem ser identificadas como pontos que se desviam significativamente do comportamento esperado. Em séries não estacionárias, pode ser necessário transformá-las em estacionárias antes de aplicar métodos de detecção de anomalias. A escolha do método de detecção dependerá das características específicas dos dados e do tipo de anomalia que se busca identificar.

### Média moveis

As médias móveis são ferramentas estatísticas amplamente utilizadas na análise de séries temporais para suavizar flutuações e destacar tendências subjacentes nos dados. Embora as fontes consultadas não abordem diretamente o uso de médias móveis para detecção de anomalias, sua aplicação pode ser relevante nesse contexto.

#### Médias Móveis e Tendências

- **Suavização**: As médias móveis ajudam a reduzir as irregularidades de curto prazo, facilitando a visualização de padrões de longo prazo na série temporal.
    
- **Identificação de Tendências**: Ao suavizar os dados, as médias móveis permitem identificar desvios significativos da tendência esperada, que podem indicar a presença de anomalias.
    

#### Médias Móveis e Ruído

- **Redução de Ruído**: Séries temporais frequentemente contêm ruído que dificulta a detecção de anomalias. As médias móveis reduzem o impacto desse ruído, tornando os desvios reais mais evidentes.
    
1. **Definição de Limiares**: Médias móveis podem ser utilizadas para estabelecer limiares dinâmicos na detecção de anomalias. Pontos de dados que excedem a média móvel por uma margem definida podem ser sinalizados como potenciais anomalias.
    

#### Aplicação de Médias Móveis na Detecção de Anomalias

Uma abordagem conceitual seria:

1. **Calcular a Média Móvel**: Escolher um tamanho de janela adequado e calcular a média móvel da série temporal.
    
2. **Estabelecer um Limiar**: Determinar um limiar com base na variação típica em torno da média móvel, que pode ser um valor fixo ou múltiplo do desvio padrão dos dados.
    
3. **Identificar Anomalias**: Sinalizar pontos de dados que ultrapassam o limiar definido como possíveis anomalias.
    

#### Considerações

- **Tamanho da Janela**: A escolha do tamanho da janela é crucial. Janelas menores são mais sensíveis a flutuações de curto prazo, enquanto janelas maiores são mais robustas ao ruído, mas podem não detectar anomalias de curta duração.
    
- **Definição de Limiar**: O limiar deve ser definido cuidadosamente para equilibrar sensibilidade e especificidade, evitando falsos positivos ou negativos.

### Usando Exponencial Smoothing

Nesse caso, pode-se usar a técnica de Exponencial Smoothing para prever toda a série temporal, assim, podemos utilizar dessa previsão para detectar as anomalias.

### Usando o Seasonal-Trend decomposition (STD)

### Usando o modelo Arima