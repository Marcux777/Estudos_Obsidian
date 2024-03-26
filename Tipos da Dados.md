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
	->Basicamente, um vetor dinâmico. É uma coleção de itens.
		````
			
```