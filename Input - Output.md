
- Entrada -> Comando ``input()``, aqui será pego a entrada de dados. Pode-se colocar textos dentro do input. 
	exemplo: ``input("Digite seu nome")``
	Todo e qualquer dado que for digitado numa linha será lido como uma string.
	
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