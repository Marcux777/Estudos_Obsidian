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
