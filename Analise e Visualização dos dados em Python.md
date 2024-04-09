
## Analise de dados
Processamento de Dados é a tarefa de converter dados de uma forma dada para uma forma muito mais utilizável e desejada, ou seja, torná-los mais significativos e informativos. A saída desse processo completo pode estar em qualquer forma desejada, como gráficos, vídeos, tabelas, imagens e muitos mais, dependendo da tarefa que estamos realizando e dos requisitos da máquina.

Os principais passos envolvidos no processamento de dados normalmente incluem:

1. **Coleta de dados**: Este é o processo de coleta de dados de várias fontes, como sensores, bancos de dados ou outros sistemas. Os dados podem ser estruturados ou não estruturados e podem vir em vários formatos, como texto, imagens ou áudio.
    
2. **Pré-processamento de dados**: Esta etapa envolve a limpeza, filtragem e transformação dos dados para torná-los adequados para análises posteriores. Isso pode incluir a remoção de valores ausentes, escalonamento ou normalização dos dados, ou a conversão para um formato diferente.
    
3. **Análise de dados**: Nesta etapa, os dados são analisados usando várias técnicas, como análise estatística, algoritmos de aprendizado de máquina ou visualização de dados. O objetivo desta etapa é obter insights ou conhecimentos a partir dos dados.
    
4. **Interpretação de dados**: Esta etapa envolve a interpretação dos resultados da análise de dados e a elaboração de conclusões com base nos insights obtidos. Também pode envolver a apresentação das descobertas de maneira clara e concisa, como por meio de relatórios, painéis ou outras visualizações.
    
5. **Armazenamento e gerenciamento de dados**: Uma vez que os dados foram processados e analisados, eles devem ser armazenados e gerenciados de uma maneira que seja segura e facilmente acessível. Isso pode envolver o armazenamento dos dados em um banco de dados, armazenamento em nuvem ou outros sistemas, e a implementação de estratégias de backup e recuperação para proteger contra a perda de dados.
    
6. **Visualização de dados e relatórios**: Finalmente, os resultados da análise de dados são apresentados aos interessados em um formato que seja facilmente compreensível e acionável. Isso pode envolver a criação de visualizações, relatórios ou painéis que destacam as principais descobertas e tendências nos dados.


### Analisando Dados Numéricos com NumPy
NumPy é um pacote de processamento de array em Python e fornece um objeto de array multidimensional de alto desempenho e ferramentas para trabalhar com esses arrays. É o pacote fundamental para computação científica com Python.

#### Arrays no NumPy 
O Array NumPy é uma tabela de elementos (geralmente números), todos do mesmo tipo, indexados por uma tupla de inteiros positivos. No NumPy, o número de dimensões do array é chamado de rank do array. Uma tupla de inteiros que dá o tamanho do array ao longo de cada dimensão é conhecida como a forma do array.

#### Criando Array NumPy 
Os arrays NumPy podem ser criados de várias maneiras, com várias dimensões (ranks). Também pode ser criado com o uso de diferentes tipos de dados, como listas, tuplas, etc, mas, diferente da lista em Python, os arrays NumPy são homogêneos. O tipo do array resultante é deduzido a partir do tipo de elementos nas sequências. O NumPy oferece várias funções para criar arrays com conteúdo inicial de espaço reservado. Isso minimiza a necessidade de aumentar arrays, uma operação cara.

~~~~ Python3
import numpy as np
 
b = np.empty(2, dtype = int)
print("Matrix b : \n", b)
 
a = np.empty([2, 2], dtype = int)
print("\nMatrix a : \n", a)
 
c = np.empty([3, 3])
print("\nMatrix c : \n", c)
~~~~

****Output:****

~~~~
	Matrix b : 
	 [0 0]
	
	Matrix a : 
	 [[0 0]
	 [0 0]]
	
	Matrix c : 
	 [[0. 0. 0.]
	 [0. 0. 0.]
	 [0. 0. 0.]]
~~~~

Documentação da biblioteca, para entender os métodos:
https://numpy.org/doc/stable/user/index.html#user
### Pandas
Pandas é uma biblioteca de código aberto que é construída sobre a biblioteca NumPy. É um pacote Python que oferece várias estruturas de dados e operações para manipular dados numéricos e séries temporais. É principalmente popular para importar e analisar dados de maneira muito mais fácil. Pandas é rápido e tem alto desempenho e produtividade para os usuários.

Documentação da Biblioteca:
https://pandas.pydata.org/docs/index.html
## Limpeza de Dados
A limpeza de dados é um componente integral da ciência de dados, desempenhando um papel fundamental na garantia da precisão e confiabilidade dos conjuntos de dados. No campo da ciência de dados, onde insights e previsões são extraídos de conjuntos de dados vastos e complexos, a qualidade dos dados de entrada influencia significativamente a validade dos resultados analíticos. A limpeza de dados envolve a identificação e correção sistemática de erros, inconsistências e imprecisões dentro de um conjunto de dados, abrangendo tarefas como o tratamento de valores ausentes, remoção de duplicatas e tratamento de outliers. Este processo meticuloso é essencial para melhorar a integridade das análises, promover uma modelagem mais precisa e, finalmente, facilitar a tomada de decisões informadas com base em dados confiáveis e de alta qualidade.



## Visualização de dados

A Visualização de Dados é o processo de apresentar dados na forma de gráficos ou tabelas. Ela ajuda a entender grandes e complexas quantidades de dados de maneira muito fácil. Permite que os tomadores de decisão tomem decisões de maneira muito eficiente e também lhes permite identificar novas tendências e padrões com muita facilidade. Também é usada na análise de dados de alto nível para Aprendizado de Máquina e Análise Exploratória de Dados (EDA). A visualização de dados pode ser feita com várias ferramentas como Tableau, Power BI, Python.

Matplotlib é uma biblioteca de baixo nível do Python que é usada para visualização de dados. É fácil de usar e emula gráficos e visualizações como MATLAB. Esta biblioteca é construída sobre arrays NumPy e consiste em vários gráficos como gráfico de linhas, gráfico de barras, histograma, etc. Ela oferece muita flexibilidade, mas ao custo de escrever mais código.

Pyplot é um módulo Matplotlib que fornece uma interface semelhante ao MATLAB. Matplotlib é projetado para ser tão utilizável quanto o MATLAB, com a capacidade de usar Python e a vantagem de ser gratuito e de código aberto. Cada função pyplot faz alguma alteração em uma figura: por exemplo, cria uma figura, cria uma área de plotagem em uma figura, plota algumas linhas em uma área de plotagem, decora o gráfico com rótulos, etc. Os vários gráficos que podemos utilizar usando Pyplot são Gráfico de Linhas, Histograma, Dispersão, Gráfico 3D, Imagem, Contorno e Polar.

Documentação da Biblioteca:
https://matplotlib.org/stable/index.html
