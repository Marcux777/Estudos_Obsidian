
- Entrada -> Comando ``input()``, aqui será pego a entrada de dados. Pode-se colocar textos dentro do input. 
	exemplo: ``input("Digite seu nome")``
	Todo e qualquer dado que for digitado numa linha será lido como uma string.
	- Pegando Múltiplas entradas em Python -> Diferente das linguagens como C/C++, Python lê toda  a linha como string. 
		Por exemplo, a entrada `7 8 9` será uma string com esse valores. 
		Para pegar cada um deles para que possamos manipular como valores, vamos usar o método `split()` após o input. Ele irá quebrar a entrada em uma lista de strings e converte-los para inteiros.
		````
```x, y = input("Etre com dois valores: ").split()

x = int(x)
y = int(y)
print("{} + {} = {}".format(x, y, x+y))``
```
		Aqui pegamos a entrada, cortamos em uma lista e convertemos para inteiro e armazenamos nas variáveis, indo a posição `0` para o `x` e a posição `1` para o `y`
- Saída -> comando ``print("Não importa se aqui é aspas simples ou duplas" )`` e ele sempre coloca uma quebra após imprimir.
	- Parâmetro `end` no Print -> o que for colocado para o parâmetro receber, será colocar no final do print. Por exemplo 
	````
		print("Welcome to", end = '_')
		print("Python", end = ' ')
	
	
		Welcome to_Python
		```
	````
	
	-  Parâmetro `sep` no Print -> Separa os parametros do print
	````
		print("OLÁ", "Tenha", "um", "bom", "dia", sep = '-')
		```
		OLÁ-Tenha-um-bom-dia
		```
	````
	
	- Output formatado -> É possivel formatar a saida utilizando de máscaras `{}`
		````
		print('I love {} for{}!'.format('Paçoquinha','ever'))
		
		
		I love Paçoquinha forever!
		````
		
- Comentários -> ``# Utilizamos aqui a hashtag mesmo até o fim da linha``. 
``### aqui é para pegar uma ou mais de uma linha ###``