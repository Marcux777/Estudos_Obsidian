## Strings

- Criação -> Strings podem ser escritas com aspas simples `'Olá'`, duplas `"Olá"` e triplas `'''Oxi, e a diferenca?'''`
- Acessando os caracteres -> As strings estão organizadas em posições, de 0 até n-1. No entanto, diferentemente de outras linguagens, como C++, elas possuem uma posição 'negativa', que começa pelo ultimo caractere. Por Exemplo:
	```
	Str = "Bora Pro volei"
	print("String: ")
	print(Str)
	
	print("Primeiro Caracter: ")
	print(Str[0])
	
	print("\nO ultimo é: ")
	print(Str[-1])
	```
	Ou até mesmo invertendo uma string ou pegando uma parte da string
	```
	Str = "Bora Pro volei"
	print("String: ") 
	print(Str) 
	
	print("Substring: ") 
	print(Str[3:7]) 
	
	print("\nInvertida: ") 
	print(Str[::-1]) 
	```
	Documentação: https://docs.python.org/3/library/string.html
## Numéricos
- ### Inteiros 
	Basicamente, valores do conjunto dos inteiros.

- ### Reais
	Basicamente, valores de ponto flutuantes.
	Exemplo no print:
	````
	num = 3.14159
	print('{:.2f}'.format(num))
	````
## Boleana 
-> Basicamente verdadeiro ou falso.
## List
->Basicamente, um vetor dinâmico. É uma coleção de itens, homogêneos ou não.
	Exemplo:
````
		List = [1, 2, 4, 4, 3, 3, 3, 6, 5]
		print("\nLista de inteiros: ")
		print(List) 
		
		List = [1, 2, 'Balela', 4, 'ok', 6, 'Triste']
		print("\nList com valores diversos: ")
		print(List)
````

Para pegar um valor em especifico, podemos dizer a posição que queremos
````
	List = ['Memories', 'is', 'Broken']
 
	print("Pegando um elemento: ")
	print(List[0])
	print(List[2])
````
E podemos fazer também um array multidimensional
````
	List = [['Memories', 'is', 'Broken'], ['The', 'truth', 'goes', 'unspoken'], ["I've", "even", 'forgotten', 'my', 'name']]
	
	print("Pegando um elemento: ")
	
	print(List[0][1])
	
	print(List[2][0])
````

Ou podemos pegar uma posição negativa, que pega "começa" pelo final da lista.
````
	List = [['Memories', 'is', 'Broken'], ['The', 'truth', 'goes', 'unspoken'], ["I've", "even", 'forgotten', 'my', 'name']]
	
	print("Pegando um elemento: ")
	print(List[0][-1])
	
	print(List[-2][0])
````

- Funções:
	- `append()` -> adiciona elementos diversos ao final da lista.
		````
		List = []
		print("Lista Inicial: ")
		print(List)			 
		List.append(1)
		List.append(2)
		List.append(4)
		print("\nLista depois de adicionados os 3 elementos: ")
		print(List)
		````
	- `insert()` -> Insere elementos em locais específicos da lista.
		````
		List = [1,2,3,4]
		print("Lista Inicial: ")
		print(List)
		
		List.insert(1, 12)
		print(List)
		````
	- `extend()` -> Insere múltiplos elementos ao final da lista.
		````
		List = [1, 2, 3, 4]
		print("Lista Inicial: ")
		print(List)
		 
		List.extend([8, 'Memories', 'Broken'])
		print("\nLista depois: ")
		print(List)
		````
	- `pop()` -> Remove e retorna, por padrão, o ultimo elemento da lista. Para especificar, só passar a posição do elemento como parâmetro.
		````
		List = [1, 2, 3, 4, 5]
	
		List.pop()
		print("\nLista após o pop: ")
		print(List)
		 
		List.pop(2)
		print("\nLista após o elemento especificado for excluido: ")
		print(List)
		````
	- ``Sort()`` -> Ordena em ordem crescente.
		````
		List = [5, 8 , 23, 235, 2, 234, 325, 32, 35]
		print("\nLista antes do sort: ")
		print(List)
		List.sort()
		print("\nLista após o sort: ")
		print(List)
		````

