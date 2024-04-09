NumPy é um pacote de processamento de array em Python e fornece um objeto de array multidimensional de alto desempenho e ferramentas para trabalhar com esses arrays. É o pacote fundamental para computação científica com Python.

#### Arrays no NumPy 
O Array NumPy é uma tabela de elementos (geralmente números), todos do mesmo tipo, indexados por uma tupla de inteiros positivos. No NumPy, o número de dimensões do array é chamado de rank do array. Uma tupla de inteiros que dá o tamanho do array ao longo de cada dimensão é conhecida como a forma do array.

#### Criando Array NumPy 
Os arrays NumPy podem ser criados de várias maneiras, com várias dimensões. Também pode ser criado com o uso de diferentes tipos de dados, como listas, tuplas, etc, mas, diferente da lista em Python, os arrays NumPy são homogêneos. O tipo do array resultante é deduzido a partir do tipo de elementos nas sequências. O NumPy oferece várias funções para criar arrays com conteúdo inicial de espaço reservado. Isso minimiza a necessidade de aumentar arrays, uma operação cara.

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
