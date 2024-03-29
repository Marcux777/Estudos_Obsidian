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

## Tuplas

São muito parecidas com Listas, diferenciando em 2 aspectos:
	1° - Tuplas são imutáveis, uma vez criadas, os valores não podem ser alterados.
	2° - A Sintaxe, tuplas são criadas com ``()``, enquanto listas são com `[]`

- Exemplo:
	~~~
	Tuple1 = ()
	print("Tupla Inicial: ")
	print(Tuple1)
	
	
	Tuple1 = ('Vi', 'Tu')
	print("\nTupla com as strings: ")
	print(Tuple1)
	
	
	list1 = [1, 2, 4, 5, 6]
	print("\nTuple usando List: ")
	print(tuple(list1))
	
	Tuple1 = tuple('I... AM... ATOMIC!!!!!!!!')
	print("\nTuple com o uso da função: ")
	print(Tuple1)
	~~~~

### Criando uma Tupla com Tipos de Dados Mistos.
As tuplas podem conter qualquer número de elementos e de qualquer tipo de dados (como strings, inteiros, listas, etc.). As tuplas também podem ser criadas com um único elemento, mas é um pouco complicado. Ter um elemento entre parênteses não é suficiente, deve haver uma 'vírgula' no final para torná-lo uma tupla.

~~~~
	Tuple1 = (5, 'Ué', 7, 'Puts')
	print("\nTuple com dados mixos: ")
	print(Tuple1)
	
	Tuple1 = (0, 1, 2, 3)
	Tuple2 = ('python', 'gordola')
	Tuple3 = (Tuple1, Tuple2)
	print("\nTuple com tuplas aninhadas: ")
	print(Tuple3)
	
	Tuple1 = ('Geeks',) * 3
	print("\nTuple com repetição: ")
	print(Tuple1)
	
	Tuple1 = ('Geeks')
	n = 5
	print("\nTuple com um loop")
	for i in range(int(n)):
		Tuple1 = (Tuple1,)
		print(Tuple1)
~~~~

#### Acessando Tuplas
As tuplas são imutáveis e geralmente contêm uma sequência de elementos heterogêneos que são acessados por meio de desempacotamento ou indexação (ou mesmo por atributo, no caso de tuplas nomeadas). As listas são mutáveis e seus elementos são geralmente homogêneos e são acessados por meio de iteração sobre a lista.

~~~~
Tuple1 = ("Vasco", "da", "Gama")

a, b, c = Tuple1
print("\nValues depois de separados: ")
print(a)
print(b)
print(c)
~~~~

## Sets
Em Python, um Conjunto é uma coleção não ordenada de tipos de dados que é iterável, mutável e não tem elementos duplicados. A ordem dos elementos em um conjunto é indefinida, embora possa consistir em vários elementos. A principal vantagem de usar um conjunto, em oposição a uma lista, é que ele tem um método altamente otimizado para verificar se um elemento específico está contido no conjunto.

~~~~
set1 = set()
print("Conjunto inicial em branco: ")
print(set1)

set1 = set("GeeksForGeeks")
print("\nConjunto com o uso de String: ")
print(set1)

String = 'GeeksForGeeks'
set1 = set(String)
print("\nConjunto com o uso de um Objeto: ")
print(set1)


set1 = set(["Geeks", "For", "Geeks"])
print("\nConjunto com o uso de Lista: ")
print(set1)

# Criando um Conjunto com
# o uso de uma tupla
t=("Geeks","for","Geeks")
print("\nConjunto com o uso de Tupla: ")
print(set(t))

# Criando um Conjunto com
# o uso de um dicionário
d={"Geeks":1,"for":2,"Geeks":3}
print("\nConjunto com o uso de Dicionário: ")
print(set(d))
~~~~

Um conjunto contém apenas elementos únicos, mas no momento da criação do conjunto, vários valores duplicados também podem ser passados. A ordem dos elementos em um conjunto é indefinida e é inalterável. O tipo de elementos em um conjunto não precisa ser o mesmo, vários valores de tipos de dados diferentes também podem ser passados para o conjunto.

### Usando o método remove() ou o método discard(): 
Elementos podem ser removidos do Conjunto usando a função integrada remove(), mas um KeyError surge se o elemento não existir no conjunto. Para remover elementos de um conjunto sem KeyError, use discard(), se o elemento não existir no conjunto, ele permanece inalterado.

~~~~
# Programa Python para demonstrar
# Remoção de elementos em um Conjunto

# Criando um Conjunto
set1 = set([1, 2, 3, 4, 5, 6,
            7, 8, 9, 10, 11, 12])
print("Conjunto inicial: ")
print(set1)

# Removendo elementos do Conjunto
# usando o método Remove()
set1.remove(5)
set1.remove(6)
print("\nConjunto após a remoção de dois elementos: ")
print(set1)

# Removendo elementos do Conjunto
# usando o método Discard()
set1.discard(8)
set1.discard(9)
print("\nConjunto após descartar dois elementos: ")
print(set1)

# Removendo elementos do Conjunto
# usando o método iterador
for i in range(1, 5):
    set1.remove(i)
print("\nConjunto após remover uma série de elementos: ")
print(set1)
~~~~

Vantagens:
- Elementos Únicos: Conjuntos só podem conter elementos únicos, então eles podem ser úteis para remover duplicatas de uma coleção de dados.
- Teste de Membro Rápido: Conjuntos são otimizados para teste de membro rápido, então eles podem ser úteis para determinar se um valor está em uma coleção ou não.
- Operações de Conjunto Matemático: Conjuntos suportam operações de conjunto matemático como união, interseção e diferença, que podem ser úteis para trabalhar com conjuntos de dados.
- Mutável: Conjuntos são mutáveis, o que significa que você pode adicionar ou remover elementos de um conjunto depois que ele foi criado.

Desvantagens:
- Não Ordenado: Conjuntos são não ordenados, o que significa que você não pode confiar na ordem dos dados no conjunto. Isso pode dificultar o acesso ou processamento de dados em uma ordem específica.
- Funcionalidade Limitada: Conjuntos têm funcionalidade limitada em comparação com listas, pois eles não suportam métodos como append() ou pop(). Isso pode dificultar a modificação ou manipulação de dados armazenados em um conjunto.
- Uso de Memória: Conjuntos podem consumir mais memória do que listas, especialmente para pequenos conjuntos de dados. Isso ocorre porque cada elemento em um conjunto requer memória adicional para armazenar um valor de hash.
- Menos Comumente Usado: Conjuntos são menos comumente usados do que listas e dicionários em Python, o que significa que pode haver menos recursos ou bibliotecas disponíveis para trabalhar com eles. Isso pode dificultar a busca de soluções para problemas ou obter ajuda com a depuração.

## Dictionaries
Dicionários em Python são uma estrutura de dados, usada para armazenar valores no formato chave: valor. Isso o torna diferente de listas, tuplas e arrays, pois em um dicionário cada chave tem um valor associado.
~~~~
# Dicionário em Python
Dict = {1: 'Geeks', 2: 'For', 3: 'Geeks'}
print("\nDicionário com o uso de Chaves Inteiras: ")
print(Dict)

Dict = {'Name': 'Geeks', 1: [1, 2, 3, 4]}
print("\nDicionário com o uso de Chaves Mistas: ")
print(Dict)
~~~~

### Adicionando Elementos a um Dicionário
A adição de elementos pode ser feita de várias maneiras. Um valor de cada vez pode ser adicionado a um Dicionário definindo o valor junto com a chave, por exemplo, Dict[Chave] = 'Valor'.

Atualizar um valor existente em um Dicionário pode ser feito usando o método integrado update(). Valores de chaves aninhadas também podem ser adicionados a um Dicionário existente.

Nota - Ao adicionar um valor, se o par chave-valor já existir, o valor é atualizado, caso contrário, uma nova Chave com o valor é adicionada ao Dicionário.

Exemplo: Adicionar Itens a um Dicionário Python com Diferentes Tipos de Dados

O código começa com um dicionário vazio e então adiciona pares de chave-valor a ele. Ele demonstra a adição de elementos com vários tipos de dados, atualizando o valor de uma chave e até mesmo aninhando dicionários dentro do dicionário principal. O código mostra como manipular dicionários em Python.

~~~~
# Dicionário em Python
Dict = {}
print("Dicionário Vazio: ")
print(Dict)

# Adicionando elementos ao dicionário
Dict[0] = 'Geeks'
Dict[2] = 'For'
Dict[3] = 1
print("\nDicionário após adicionar 3 elementos: ")
print(Dict)

# Adicionando conjunto de valores
# à chave simples
Dict['Value_set'] = 2, 3, 4
print("\nDicionário após adicionar 3 elementos: ")
print(Dict)

# Atualizando valor existente
Dict[2] = 'Welcome'
print("\nValor da chave atualizado: ")
print(Dict)

# Adicionando chave aninhada
Dict[5] = {'Nested': {'1': 'Life', '2': 'Geeks'}}
print("\nAdicionando uma Chave Aninhada: ")
print(Dict)
~~~~



