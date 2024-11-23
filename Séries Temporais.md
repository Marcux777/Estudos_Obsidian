## 1. Introdução às Séries Temporais

### Definição e Conceitos Básicos

**Uma série temporal é uma coleção de observações feitas sequencialmente ao longo do tempo**. Isso significa que cada observação está associada a um momento específico. Por exemplo, se você medir a temperatura de uma cidade a cada hora, obterá uma série temporal das temperaturas horárias dessa cidade.

Existem duas formas de registrar uma série temporal:

- **Discreta:** Em uma série temporal discreta, as observações são realizadas em pontos específicos no tempo. Por exemplo, os dados de temperatura horária descritos acima são uma série temporal discreta. Outros exemplos incluem o valor de fechamento diário de uma ação ou a taxa de desemprego mensal.
- **Contínua:** Em uma série temporal contínua, as observações são feitas continuamente ao longo do tempo. Por exemplo, um eletrocardiograma (ECG) que registra a atividade elétrica do coração é uma série temporal contínua.

A análise de dados de séries temporais frequentemente envolve:

- Identificar os **componentes** da série temporal, como tendência, sazonalidade e ruído.
- Desenvolver **modelos** para descrever o comportamento da série temporal.
- Usar esses modelos para **prever** valores futuros da série temporal.

### Importância e Aplicações Práticas

A análise de séries temporais é importante porque permite:

- **Compreender a dinâmica do sistema subjacente**: Estudando os padrões e tendências em uma série temporal, é possível obter insights sobre os mecanismos que geram os dados.
- **Prever valores futuros**: Os modelos de séries temporais podem ser usados para fazer previsões sobre os valores futuros da série, o que pode ser útil para decisões futuras. Por exemplo, uma empresa pode usar um modelo de série temporal para prever vendas no próximo trimestre, ou um governo pode utilizá-lo para prever o crescimento econômico.
- **Controlar o sistema**: Compreendendo a dinâmica de uma série temporal, é possível desenvolver estratégias para controlar o sistema que gera os dados. Por exemplo, uma empresa de manufatura pode usar um modelo de série temporal para controlar a qualidade de seus produtos, ou uma companhia elétrica pode usá-lo para controlar o fluxo de eletricidade em sua rede.

A análise de séries temporais é amplamente utilizada em uma variedade de domínios:

- **Economia e finanças**: Analisar tendências de preços de ações, taxas de juros, taxas de câmbio e indicadores econômicos.
- **Oceanografia, meteorologia e outras ciências da Terra**: Investigar mudanças climáticas, padrões climáticos e correntes oceânicas.
- **Engenharia e medicina**: Monitorar e controlar processos industriais, compreender a progressão de doenças.
- **Neurologia**: Examinar dados de ondas cerebrais para diagnosticar distúrbios neurológicos.

### Exemplos de Séries Temporais em Diferentes Domínios

- **Finanças**: O valor de fechamento diário da Bolsa de Valores de São Paulo (BOVESPA) ao longo de um período.
- **Meteorologia**: A pressão atmosférica mensal em Fortaleza, CE, Brasil.
- **Meio Ambiente**: A concentração diária de um poluente em Azusa, CA, EUA.

Estes são apenas alguns exemplos dos diversos tipos de dados de séries temporais encontrados em diferentes disciplinas. Os métodos específicos para analisar dados de séries temporais dependem das características dos dados e dos objetivos da análise.

## 2. **Componentes de uma Série Temporal**

As fontes fornecem uma riqueza de informações sobre os componentes de uma série temporal. Esses componentes representam padrões distintos que contribuem para o comportamento geral de uma série temporal, sendo fundamentais para análises e previsões precisas. Abaixo está um detalhamento de cada componente:

- **Tendência (Trend):** A tendência representa o **movimento de longo prazo** de uma série temporal. Indica a direção geral dos dados ao longo do tempo, seja crescente, decrescente ou relativamente constante. As tendências podem ser **lineares ou não lineares**, sendo a forma mais simples uma linha reta. Por exemplo, o aquecimento global, caracterizado pelo aumento das temperaturas globais ao longo de décadas, exemplifica uma tendência crescente. Reconhecer a tendência é essencial para compreender mudanças de longo prazo e fazer previsões informadas sobre o futuro.
    
- **Sazonalidade (Seasonality):** A sazonalidade refere-se a **flutuações periódicas** que ocorrem em **intervalos regulares dentro de um ano**. Esses padrões geralmente estão ligados a eventos de calendário, como feriados, estações do ano ou dias específicos da semana. A sazonalidade pode ser **aditiva** (quando o efeito sazonal é constante) ou **multiplicativa** (quando o efeito sazonal varia proporcionalmente ao nível da série temporal). Identificar a sazonalidade é vital para empresas e organizações tomarem decisões informadas sobre estoque, alocação de pessoal e campanhas de marketing.
    
- **Ciclicidade (Cycles):** Diferentemente da sazonalidade, os ciclos são padrões que se repetem em **períodos superiores a um ano**. Esses ciclos podem ser **irregulares em sua duração e magnitude** e não estão necessariamente relacionados a eventos de calendário. Fatores que contribuem para a ciclicidade incluem ciclos econômicos, mudanças demográficas ou fenômenos como variações de manchas solares. Compreender a ciclicidade é essencial para o planejamento de longo prazo e decisões estratégicas, especialmente em áreas como economia e finanças.
    
- **Irregularidade ou Ruído (Irregularity or Noise):** A irregularidade ou o ruído representam as **flutuações aleatórias** em uma série temporal que **não podem ser explicadas pelos outros componentes**. O ruído pode surgir de diversas fontes, como erros de medição, eventos aleatórios ou flutuações imprevisíveis no sistema em análise. Embora o ruído possa obscurecer padrões subjacentes, é importante reconhecer que ele é uma parte inerente de muitas séries temporais do mundo real.
    
## 3. **Estacionariedade**

### O Conceito de Estacionariedade

Uma série temporal é considerada **estacionária** se suas propriedades estatísticas permanecem constantes ao longo do tempo. Isso significa que a média, a variância e a autocorrelação da série não mudam com o tempo. Um processo estacionário pode ser entendido como um processo em equilíbrio estatístico.

Muitos modelos de séries temporais assumem que os dados são estacionários. Isso ocorre porque a estacionariedade simplifica a análise e permite o uso de uma gama mais ampla de métodos estatísticos. Se uma série temporal não for estacionária, ela pode frequentemente ser transformada em uma série estacionária utilizando diferenciação ou outros métodos.

### Testes para Estacionariedade

Existem diversos testes estatísticos que podem ser usados para avaliar a estacionariedade de uma série temporal. Um dos testes mais comuns é o **teste de Dickey-Fuller**. Esse teste baseia-se na ideia de que um processo com raiz unitária (um processo não estacionário) terá um coeficiente autorregressivo igual a 1. O teste de Dickey-Fuller examina a hipótese nula de que o coeficiente autorregressivo é igual a 1. Se a hipótese nula for rejeitada, a série temporal é considerada estacionária.

As fontes mencionam várias variações do teste de Dickey-Fuller, incluindo:

- **Teste de Dickey-Fuller Aumentado (Augmented Dickey-Fuller):** Este teste inclui valores defasados da primeira diferença da série temporal como variáveis explicativas na equação de regressão. Isso é feito para levar em conta a correlação serial nos dados.
- **Teste de Phillips-Perron:** Um teste não paramétrico que é robusto à heterocedasticidade e autocorrelação nos dados.

A escolha do teste dependerá das características específicas dos dados da série temporal.

### Métodos para Tornar uma Série Temporal Estacionária

Se uma série temporal for identificada como não estacionária, existem diversos métodos que podem ser utilizados para transformá-la em uma série estacionária. Alguns métodos comuns incluem:

- **Diferenciação (Differencing):** Consiste em subtrair observações consecutivas. Por exemplo, a primeira diferença de uma série temporal é calculada subtraindo o valor no tempo _t_-1 do valor no tempo _t_. A diferenciação pode remover tendências e sazonalidade de uma série temporal.
- **Transformação Logarítmica:** Envolve o uso do logaritmo natural da série temporal. Isso pode ajudar a estabilizar a variância de uma série temporal.
- **Ajuste Sazonal:** Consiste em remover o componente sazonal de uma série temporal. Isso pode ser feito usando métodos como médias móveis ou variáveis dummy.

A escolha do método dependerá das características específicas da série temporal e da natureza da não estacionariedade. Vale notar que as fontes descrevem esses métodos no contexto de dados econômicos, e sua aplicação a outros domínios pode exigir considerações adicionais.

## 4. **Modelos de Séries Temporais**

## 4. 1. Modelos Autorregressivos (AR) na Análise de Séries Temporais

Os modelos autorregressivos (AR) são uma classe fundamental de modelos de séries temporais usados para prever valores futuros com base em observações passadas. A característica definidora de um modelo AR é expressar o valor atual de uma série temporal como uma combinação linear de seus próprios valores passados, somados a um termo de erro aleatório.

### Estrutura dos Modelos AR

Um modelo AR de ordem _p_, denotado como AR(_p_), pode ser matematicamente representado como:
$$Yt = c + φ1Yt-1 + φ2Yt-2 + ... + φpYt-p + εt$$

Onde:

- $Yt$ é o valor da série temporal no tempo _$t$
- **$c$** é o termo constante (intercepto)
- **$φ1, φ2, ..., φp$** são os coeficientes autorregressivos que determinam a influência dos valores passados
- **$Yt-1, Yt-2, ..., Yt-p$** representam os valores da série temporal em passos de tempo anteriores (defasagens)
- **$εt$** é o termo de erro aleatório, geralmente assumido como ruído branco (sequência de variáveis independentes e identicamente distribuídas com média zero e variância constante)

### Ordem dos Modelos AR

A ordem de um modelo AR (_p_) indica quantos valores defasados são usados para prever o valor atual. Por exemplo:

- Um modelo **AR(1)** usa apenas o valor do passo de tempo anterior (uma defasagem).
- Um modelo **AR(2)** utiliza os valores dos dois passos de tempo anteriores (duas defasagens).

A escolha da ordem apropriada é crucial e geralmente determinada por análises das funções de autocorrelação e autocorrelação parcial da série temporal.

### Estacionariedade

Um pressuposto-chave em muitos modelos de séries temporais, incluindo os AR, é que os dados sejam estacionários. Uma série estacionária possui propriedades estatísticas, como média, variância e autocorrelação, que permanecem constantes ao longo do tempo.

A estacionariedade de um processo AR depende dos parâmetros autorregressivos. Se as raízes da equação característica (formada pelos coeficientes AR) estiverem fora do círculo unitário, o processo AR é considerado estacionário. Essa condição garante que a influência de choques passados decaia com o tempo, levando a um processo estável.
### Aplicações

Os modelos AR têm ampla aplicação em várias áreas, como:

- **Previsão de valores futuros:** Prever valores futuros de uma série temporal com base no comportamento passado.
- **Entendimento das dinâmicas subjacentes:** Identificar padrões e relações nos dados, como a persistência de choques ou a presença de ciclos.
- **Modelagem e simulação de sistemas:** Criar modelos que capturam o comportamento de sistemas complexos ao longo do tempo.

## 4.2. Explorando Modelos de Média Móvel (MA)

Os modelos de média móvel (MA) constituem outra família fundamental de modelos de séries temporais. Em contraste com os modelos AR, que se baseiam nas defasagens da própria variável, os modelos MA expressam o valor atual como uma função linear dos valores presentes e passados de um termo de erro aleatório. Este termo de erro, frequentemente chamado de "ruído branco", é assumido como uma sequência de variáveis independentes e identicamente distribuídas, com média zero e variância constante.

### Estrutura dos Modelos MA

Um modelo MA de ordem _q_, denotado como MA(_q_), é representado matematicamente como:
$$Yt = μ + εt + θ1εt-1 + θ2εt-2 + ... + θqεt-q$$
Onde:

- **$Yt$** é o valor da série temporal no tempo $t$
- **$μ$** é a média do processo
- **$θ1, θ2, ..., θq$** são os coeficientes MA
- **$εt, εt-1, ..., εt-q$** representam os termos de erro (ruído branco) nos tempos _$t, t-1, t-2,... t-q$_

### Ordem dos Modelos MA

A ordem de um modelo MA (_q_) indica o número de termos de erro defasados usados no modelo. Por exemplo:

- Um modelo **MA(1)** usa apenas o termo de erro atual e o termo de erro do passo de tempo anterior.
- Um modelo **MA(2)** considera o termo de erro atual e os termos de erro dos dois passos de tempo anteriores.

A escolha da ordem apropriada é geralmente feita com base na análise das funções de autocorrelação (ACF) e autocorrelação parcial (PACF) da série temporal.

### Invertibilidade

A **invertibilidade** é um conceito importante nos modelos MA. Ela garante que um modelo MA possa ser representado como um modelo AR de ordem infinita. Essa característica é essencial para a estimativa única dos parâmetros e para a seleção do modelo mais adequado para uma série temporal.

### Previsão

Ao prever com um modelo MA, os termos de erro estimados (obtidos durante o ajuste do modelo) são usados para calcular os valores futuros da série. Para horizontes de previsão maiores que a ordem do componente MA, as previsões tendem para a média do processo.
### Aplicações

Os modelos MA são ferramentas valiosas na análise de séries temporais, úteis para:

- **Identificar padrões:** Detectar padrões nos dados causados por choques ou distúrbios aleatórios.
- **Suavizar dados:** Reduzir flutuações nos dados para destacar tendências subjacentes.
- **Realizar previsões:** Prever valores futuros da série após o ajuste do modelo.

### Pontos Adicionais sobre Modelos MA

- **Estimação por Máxima Verossimilhança:** Os parâmetros de um modelo MA podem ser estimados usando o método de máxima verossimilhança, assumindo erros normalmente distribuídos.
- **Verificação Diagnóstica:** Após ajustar um modelo MA, é fundamental realizar uma análise diagnóstica para avaliar sua adequação. Técnicas como análise de resíduos e exame das funções de autocorrelação ajudam a verificar se as suposições do modelo são atendidas.

### Dados Não Estacionários e Seleção do Modelo

- **Dados Não Estacionários:** Os modelos MA geralmente são projetados para dados estacionários. Se os dados apresentarem tendência ou sazonalidade, podem ser necessárias transformações, como diferenciação, para alcançar a estacionariedade antes de aplicar o modelo.
- **Seleção do Modelo:** Escolher a ordem apropriada para um modelo MA é crucial. Isso pode ser orientado pela análise das funções de autocorrelação (ACF) e critérios de informação, como AIC ou BIC.

Os modelos MA, junto com os modelos AR, formam a base para o entendimento de modelos mais complexos, como ARMA, ARIMA e SARIMA. Compreender sua estrutura e propriedades é essencial para a análise eficaz de séries temporais.

## 4.3. Modelos Autorregressivos de Média Móvel (ARMA)

Os modelos ARMA são um conceito central na análise de séries temporais, oferecendo uma estrutura poderosa para modelar e prever dados com dependências temporais. Eles combinam os recursos dos modelos autorregressivos (AR) e de média móvel (MA), permitindo uma representação mais flexível e abrangente do processo gerador dos dados.

### Estrutura e Definição

Um modelo ARMA, denotado como ARMA(_p, q_), é um modelo linear que utiliza tanto os valores defasados da série temporal (componente AR) quanto os valores defasados do termo de erro (componente MA). Matematicamente, um processo ARMA(_p, q_) é definido como:
$$Yt = c + φ1Yt-1 + φ2Yt-2 + ... + φpYt-p + εt + θ1εt-1 + θ2εt-2 + ... + θqεt-q$$

Onde:

- **$Yt$** é o valor da série temporal no tempo _$t$_.
- **$c$** é um termo constante.
- **$φ1, φ2, ..., φp$** são os coeficientes AR, representando a influência de valores passados da série temporal.
- **$εt, εt-1, ..., εt-q$** são os termos de erro (ruído branco) nos tempos _$t, t-1, ..., t-q$_.
- **$θ1, θ2, ..., θq$** são os coeficientes MA, refletindo a influência de choques passados nos valores atuais.

### Estacionariedade

A estacionariedade em processos ARMA depende exclusivamente do componente AR. O processo é estacionário se as raízes da equação característica:

**$1 - φ1z - φ2z² - ... - φpzp = 0$**

estiverem fora do círculo unitário. Isso garante que o processo tenha média e variância constantes ao longo do tempo.

### Invertibilidade

A **invertibilidade** é uma propriedade relacionada ao componente MA. Ela assegura que o componente MA possa ser expresso como uma representação AR de ordem infinita, permitindo a estimação única dos parâmetros. Por exemplo, um processo MA(1) é invertível se o valor absoluto do coeficiente MA (|**θ1**|) for menor que 1.

### Autocovariância e Autocorrelação

As funções de autocovariância e autocorrelação de processos ARMA são essenciais para compreender a estrutura de dependência temporal dos dados e identificar o modelo adequado.

### Estimação de Parâmetros

Os parâmetros de um modelo ARMA são geralmente estimados por **máxima verossimilhança**, assumindo erros normalmente distribuídos. Esse método maximiza a função de verossimilhança para obter estimativas dos coeficientes AR, MA e da variância do termo de erro.

### Previsão

Modelos ARMA ajustados podem ser usados para prever valores futuros da série. Eles utilizam os parâmetros estimados e informações sobre valores e erros passados para gerar previsões para pontos futuros.

### Identificação e Seleção do Modelo

A seleção das ordens _p_ (AR) e _q_ (MA) é feita analisando as funções de autocorrelação (ACF) e autocorrelação parcial (PACF). Critérios de informação, como **AIC** e **BIC**, também ajudam na comparação de modelos, penalizando aqueles com mais parâmetros.

### Exemplos e Aplicações

Os modelos ARMA são amplamente aplicados em diversas áreas, incluindo:

- **Economia e Finanças:** Modelagem de séries temporais financeiras, como preços de ações e taxas de câmbio.
- **Ciências Naturais:** Previsão de padrões climáticos e processos geofísicos.
- **Engenharia:** Monitoramento e controle de processos industriais.

Um exemplo prático é o modelo ARMA(1, 1), que combina um único termo AR e um único termo MA:

**Yt = c + φ1Yt-1 + εt + θ1εt-1**

### Extensões e Considerações

- **Extensões:** Os modelos ARMA servem como base para modelos mais avançados, como ARIMA (para dados não estacionários) e SARIMA (para dados sazonais).
- **Estacionariedade:** Antes de aplicar ARMA, é fundamental verificar se os dados são estacionários. Caso contrário, transformações como diferenciação podem ser necessárias.
- **Implementação Prática:** Embora as fontes se concentrem nos fundamentos teóricos, ferramentas como Python (bibliotecas `statsmodels` e `pmdarima`) e R (pacote `forecast`) são úteis para a implementação prática.

Os modelos ARMA são componentes essenciais da análise de séries temporais, fornecendo um equilíbrio entre simplicidade e poder preditivo. A escolha do modelo ideal deve sempre considerar as características dos dados, os diagnósticos do modelo e o objetivo da análise.

## 4.4. Modelos autorregressivos integrados de médias móveis (ARIMA)

