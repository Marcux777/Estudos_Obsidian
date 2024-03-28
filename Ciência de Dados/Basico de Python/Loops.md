# Loops em Python

Python fornece duas maneiras principais de criar loops: `for` e `while`.

## For Loop

O loop `for` em Python é usado para iterar sobre uma sequência (que pode ser uma lista, uma tupla, um dicionário, um conjunto ou uma string) ou outros objetos iteráveis.

Aqui está a sintaxe básica de um loop `for`:

```python
for valor in sequencia:
    # bloco de código
```

Por exemplo, aqui está um loop `for` que itera sobre uma lista:

```python
numeros = [1, 2, 3, 4, 5]
for numero in numeros:
    print(numero)
```

## While Loop

O loop `while` em Python é usado para iterar sobre um bloco de código enquanto a condição de teste (expressão) é verdadeira.

Aqui está a sintaxe básica de um loop `while`:

```python
while condicao:
    # bloco de código
```

Por exemplo, aqui está um loop `while` que conta de 1 a 5:

```python
contador = 1
while contador <= 5:
    print(contador)
    contador += 1
```

## Controle de Loop

Python fornece as seguintes declarações de controle de loop que você pode usar em seus loops:

- `break`: Termina o loop atual e retoma a execução na próxima instrução após o loop.
- `continue`: Pula o restante do corpo do loop para a próxima iteração.
- `pass`: É usado quando uma declaração é necessária sintaticamente, mas o programa não requer nenhuma ação.
