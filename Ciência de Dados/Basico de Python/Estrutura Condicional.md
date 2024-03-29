
---

# Estruturas Condicionais em Python

As estruturas condicionais são fundamentais na programação, permitindo que o código reaja de maneiras diferentes dependendo das condições fornecidas.

## A Estrutura `if`

A estrutura `if` é a mais básica das estruturas condicionais. Ela avalia uma condição e, se essa condição for verdadeira (`True`), executa um bloco de código.

```python
idade = 18
if idade >= 18:
    print("Você é maior de idade.")
```

Neste exemplo, se `idade` for maior ou igual a 18, a mensagem "Você é maior de idade." será impressa na tela.

## A Estrutura `else`

A estrutura `else` complementa o `if`, sendo executada quando a condição do `if` não é verdadeira.

```python
idade = 16
if idade >= 18:
    print("Você é maior de idade.")
else:
    print("Você ainda é menor de idade.")
```

Se `idade` for menor que 18, a mensagem "Você ainda é menor de idade." será impressa.

## A Estrutura `elif`

A estrutura `elif` (abreviação de "else if") permite verificar múltiplas condições em sequência.

```python
idade = 16
if idade >= 18:
    print("Você é maior de idade.")
elif idade == 17:
    print("Quase lá! Você tem 17 anos.")
else:
    print("Você ainda é menor de idade.")
```

Se `idade` for exatamente 17, a mensagem "Quase lá! Você tem 17 anos." será impressa.

## Condicional Ternária

Python também suporta a condicional ternária, que é uma maneira de escrever um `if-else` em uma única linha.

```python
idade = 18
status = "maior" if idade >= 18 else "menor"
print(f"Você é {status} de idade.")
```

Este código atribui "maior" ou "menor" à variável `status`, dependendo da idade, e depois imprime a mensagem correspondente.

---

# Conectivos Lógicos em Python

## Conectivos Lógicos

Os conectivos lógicos em Python são `and`, `or` e `not`. Eles são usados para combinar condições booleanas.

### O Conectivo `and`

O `and` é um operador lógico que retorna `True` se todas as condições que ele une forem verdadeiras.

```python
idade = 25
tem_carteira_de_motorista = True

if idade >= 18 and tem_carteira_de_motorista:
    print("Você pode dirigir.")
else:
    print("Você não pode dirigir.")
```

### O Conectivo `or`

O `or` retorna `True` se pelo menos uma das condições for verdadeira.

```python
dia = "Sábado"
clima = "Chuvoso"

if dia == "Sábado" or clima == "Ensolarado":
    print("Vamos à praia!")
else:
    print("Vamos ficar em casa.")
```

### O Conectivo `not`

O `not` inverte o resultado de uma condição: se a condição é `True`, o resultado será `False` e vice-versa.

```python
senha_correta = False

if not senha_correta:
    print("Acesso negado.")
else:
    print("Bem-vindo!")
```
