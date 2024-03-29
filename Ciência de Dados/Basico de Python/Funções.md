# Funções em Python

Funções são um dos principais blocos de construção de um programa em Python.

## Definindo uma Função

Em Python, usamos a palavra-chave `def` para definir uma função. A sintaxe é a seguinte:

```python
def nome_da_funcao():
    # código da função
```

Aqui está um exemplo de uma função simples em Python:

```python
def cumprimentar():
    print("Olá, mundo!")
```

Esta função, quando chamada, imprimirá a frase "Olá, mundo!".

## Chamando uma Função

Para chamar uma função em Python, você usa o nome da função seguido por parênteses. Por exemplo, aqui está como você chamaria a função `cumprimentar` que definimos acima:

```python
cumprimentar()
```

## Parâmetros e Argumentos

Você pode passar valores para uma função em Python. Esses valores são chamados de parâmetros. Na definição da função, você especifica os parâmetros entre parênteses:

```python
def cumprimentar(nome):
    print(f"Olá, {nome}!")
```

Quando você chama a função, os valores que você passa são chamados de argumentos:

```python
cumprimentar("Alice")
```

## Valores de Retorno

Uma função pode retornar um valor que você pode usar em seu programa. Para fazer isso, usamos a palavra-chave `return`:

```python
def quadrado(numero):
    return numero ** 2
```

Você pode usar o valor retornado em expressões:

```python
x = quadrado(3)
print(x)  # Saída: 9
```

---
# Recursividade em Python

Recursividade é um conceito fundamental na programação que permite que uma função chame a si mesma. É uma ferramenta poderosa para resolver problemas que podem ser divididos em subproblemas mais simples de natureza semelhante.

## O Que é Recursividade?

Em Python, uma função recursiva é aquela que é capaz de invocar a si mesma durante sua execução. Para entender a recursividade, é essencial compreender dois conceitos principais: o caso base e o caso recursivo.

### Caso Base

O caso base é a condição que interrompe a recursão, evitando que a função se chame infinitamente. É o cenário mais simples que pode ser resolvido sem recursão.

### Caso Recursivo

O caso recursivo é onde a função se chama com um subconjunto do problema original, aproximando-se do caso base a cada chamada.

## Exemplo de Recursividade: O Fatorial

Um exemplo clássico de recursividade é o cálculo do fatorial de um número. O fatorial de um número `n`, denotado por `n!`, é o produto de todos os números inteiros positivos de 1 até `n`.

Aqui está uma função recursiva para calcular o fatorial:

```python
def fatorial(n):
    # Caso base: fatorial de 1 é 1
    if n == 1:
        return 1
    # Caso recursivo: fatorial de n é n multiplicado pelo fatorial de n-1
    else:
        return n * fatorial(n - 1)

# Testando a função
print(fatorial(5))  # Saída: 120
```

## Pilha de Chamadas

Quando uma função recursiva é chamada, Python usa uma estrutura de dados chamada pilha de chamadas para controlar as funções que foram invocadas mas ainda não foram concluídas. Cada chamada recursiva adiciona um novo quadro à pilha até que o caso base seja alcançado. Depois disso, a pilha começa a se desfazer, retornando os valores até a primeira chamada.

## Recursividade e Iteração

Embora a recursividade possa ser elegante e uma solução natural para certos problemas, ela não é sempre a abordagem mais eficiente. Problemas resolvidos recursivamente podem muitas vezes ser reformulados como iterações, que são geralmente mais eficientes em termos de uso de memória e velocidade de execução.

