### Tópicos de Currículo para Aprendizado de Máquina

Aqui estão alguns tópicos para um curso de Aprendizado de Máquina, começando com material introdutório até conceitos mais avançados:

### **Parte I - Fundamentos**

* **[[Introdução ao Aprendizado de Máquina]]**:
    * O que é Aprendizado de Máquina?
    * Tipos de aprendizado de máquina: Aprendizado Supervisionado, Aprendizado Não Supervisionado, Aprendizado por Reforço.
    * Terminologia básica: features, atributos, covariáveis, variáveis de resposta.
    * Fluxo de trabalho típico de um projeto de aprendizado de máquina.
* [[**Fundamentos Matemáticos]]**:
    * **Álgebra Linear**:
        * Escalares, Vetores, Matrizes e Tensores.
        * Operações com matrizes: multiplicação, inversão, etc.
        * Matrizes especiais: matriz identidade, matriz diagonal, etc.
        * Dependência linear, espaço vetorial, normas.
    * **Probabilidade e Estatística**:
        * Conceitos básicos de probabilidade: eventos, variáveis aleatórias, distribuições de probabilidade.
        * Distribuições comuns: Gaussiana, Bernoulli, Multinomial.
        * Estatísticas descritivas: média, variância, desvio padrão.
        * Estatísticas inferenciais: testes de hipóteses, intervalos de confiança.
        * Estatística Bayesiana.
        * Teoria da informação.
    * **Cálculo**:
        * Derivadas e gradientes.
        * Otimização: encontrar mínimos e máximos de funções.
        * Regra da cadeia.
    * **Cálculo Numérico**:
        * Métodos para resolver problemas matemáticos iterativamente.
        * Tratamento de precisão numérica e estabilidade.
* **Conceitos Básicos de Aprendizado de Máquina**:
    * **Modelo Formal de Aprendizado**:
        * O que é aprendizado? Como definimos um problema de aprendizado?
        * Estrutura do Aprendizado Estatístico.
        * Aprendizado PAC, Aprendizado Agnóstico PAC.
        * Escopo dos problemas de aprendizado modelados.
    * **Minimização de Risco Empírico (ERM)**:
        * Overfitting e como evitá-lo.
        * Viés indutivo: o papel das suposições no aprendizado.
        * Complexidade computacional do aprendizado.
        * Implementação eficiente de ERM para diferentes classes de hipóteses.
    * **Algoritmos de Aprendizado**:
        * Algoritmos de aprendizado supervisionado:
            * **Classificação**:
                * Classificador não paramétrico simples: K-Vizinhos Mais Próximos.
                * Modelos paramétricos para classificação: Regressão Linear e Regressão Logística.
            * **Regressão**:
                * Regressão Linear.
                * Regressão Polinomial.
        * Algoritmos de aprendizado não supervisionado:
            * Agrupamento: K-means, agrupamento hierárquico.
            * Redução de dimensionalidade: PCA, SVD.
    * **Seleção e Avaliação de Modelos**:
        * Métricas de desempenho: acurácia, precisão, recall, F1-score, etc.
        * Validação cruzada: validação cruzada k-fold.
        * Curvas de aprendizado e curvas de validação.
        * Otimização de hiperparâmetros: busca em grade, busca aleatória.
        * A maldição da dimensionalidade.
        * Teorema do No Free Lunch.
    * **O Compromisso entre Viés e Complexidade**:
        * Balancear a complexidade do modelo com a capacidade de generalização.
    * **A Dimensão VC**:
        * Medindo a capacidade de uma classe de hipóteses.

**Parte II: Redes Neurais Profundas: Práticas Modernas**

* **Redes Neurais Feedforward Profundas**:
    * Arquitetura: Perceptrons Multicamadas (MLPs), funções de ativação (ReLU, sigmoid, tanh).
    * Algoritmo de retropropagação para treinar redes profundas.
    * Otimizadores: Descida de Gradiente, Descida de Gradiente Estocástica (SGD), Adam, etc.
    * Técnicas de regularização: Dropout, decaimento de peso, etc.
    * Gradientes em desaparecimento e explodindo.
* **Redes Neurais Convolucionais (CNNs)**:
    * Arquitetura: camadas convolucionais, camadas de pooling, camadas totalmente conectadas.
    * Aplicações: classificação de imagens, detecção de objetos, etc.
* **Redes Neurais Recorrentes (RNNs)**:
    * Arquitetura: camadas recorrentes, LSTM, GRU.
    * Aplicações: processamento de linguagem natural, análise de séries temporais, etc.
* **Modelagem de Sequências**:
    * Desdobramento de grafos computacionais.
    * Redes recorrentes e redes recursivas.
* **Metodologia Prática**:
    * **Escopo do Projeto**:
        * Identificação dos objetivos de negócio e de aprendizado de máquina.
        * Definição de requisitos para o sistema de aprendizado de máquina.
        * Identificação e envolvimento de stakeholders.
        * Estimativa e alocação de recursos.
    * **Coleta e Preparação de Dados**:
        * Engenharia de features: criação de features significativas a partir de dados brutos.
        * Tratamento de dados ausentes, outliers e ruído.
        * Divisão de dados: conjuntos de treinamento, validação e teste.
        * Aumento de dados: ampliação do tamanho e diversidade dos dados de treinamento.
    * **Treinamento e Depuração de Modelos**:
        * Escolha da arquitetura e hiperparâmetros do modelo.
        * Monitoramento do progresso do treinamento e identificação de problemas.
        * Estratégias de depuração para problemas comuns (overfitting, underfitting, etc.).
    * **Implantação e Monitoramento de Modelos**:
        * Implantação de modelos em ambientes de produção.
        * Monitoramento de desempenho e detecção de desvios nos dados.
        * Retreinamento de modelos e atualização de implantações.
    * **Análise de Erros**:
        * Análise de erros do modelo para identificar áreas de melhoria.
    * **Métricas de Desempenho**:
        * Escolha de métricas apropriadas para avaliar o desempenho do modelo.
    * **Modelos Básicos Padrão**:
        * Estabelecimento de modelos de referência para comparação.
    * **Determinar a Necessidade de Mais Dados**:
        * Análise do custo-benefício entre coleta de dados e desempenho do modelo.
    * **Seleção de Hiperparâmetros**:
        * Técnicas para otimização de hiperparâmetros do modelo.
* **Infraestrutura e Ferramentas para MLOps**:
    * Considerações sobre hardware: CPUs, GPUs, TPUs.
    * Ferramentas e bibliotecas de software: TensorFlow, PyTorch, scikit-learn, etc.
    * Plataformas em nuvem para aprendizado de máquina: AWS, Azure, GCP.
    * Boas práticas de MLOps para automação e gerenciamento do ciclo de vida de ML.
* **O Lado Humano do Aprendizado de Máquina**:
    * **Considerações Éticas**:
        * Justiça, viés e responsabilidade no aprendizado de máquina.
        * Impacto do aprendizado de máquina na sociedade e no mercado de trabalho.
    * **Interação com o Usuário**:
        * Design de interfaces para sistemas de aprendizado de máquina.
        * Explicação das previsões do modelo para os usuários.
    * **Colaboração em Equipe**:
        * Construção e gerenciamento de equipes de aprendizado de máquina.
        * Comunicação entre cientistas de dados, engenheiros e stakeholders.

**Parte III: Pesquisa em Aprendizado Profundo**

* **Arquiteturas Avançadas**:
    * Autoencoders: Autoencoders Variacionais (VAEs), autoencoders de denoising.
    * Redes Generativas Adversariais (GANs).
    * Transformers.
* **Aprendizado de Representação**:
    * Aprendizado de características significativas a partir de dados.
    * Transferência de aprendizado: aproveitamento de modelos pré-treinados para novas tarefas.
    * Adaptação de domínios: adaptação de modelos a diferentes distribuições de dados.
* **Modelos Probabilísticos Estruturados**:
    * Modelos gráficos: redes bayesianas, campos aleatórios de Markov.
    * Algoritmos de inferência: propagação de crenças, inferência variacional.
* **Métodos de Monte Carlo**:
    * Técnicas de amostragem para aproximação de distribuições complexas.
    * Cadeias de Markov Monte Carlo (MCMC).
* **Aprendizado por Reforço**:
    * Processos de Decisão de Markov (MDPs).
    * Iteração de valor, iteração de política.
    * Q-learning, aprendizado profundo por reforço.
