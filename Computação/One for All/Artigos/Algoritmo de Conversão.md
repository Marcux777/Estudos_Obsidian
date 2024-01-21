
É fácil representar um número dado em ternário equilibrado convertendo-o temporariamente para o sistema normal de numeração ternária. Quando o valor está em ternário padrão, seus dígitos são 0, 1 ou 2. Iterando a partir do dígito menos significativo, podemos ignorar com segurança quaisquer 0s e 1s, no entanto, os 2s devem ser transformados em Z, adicionando 1 ao próximo dígito. Dígitos 3 devem ser transformados em 0 nos mesmos termos - esses dígitos não estão presentes inicialmente, mas podem ser encontrados após o aumento de alguns 2s.

Exemplo 1: Vamos converter 64 para ternário equilibrado. Primeiro, usamos o ternário normal para reescrever o número:

$$ 64_{10} = 02101_{3} $$ 
Vamos processar a partir do dígito menos significativo (à direita):

1, 0 e 1 são ignorados, pois são permitidos no ternário equilibrado.
2 é transformado em Z, aumentando o dígito à sua esquerda, então obtemos 1Z101.
O resultado final é 1Z101.

Vamos convertê-lo de volta para o sistema decimal adicionando os valores posicionais ponderados:

$$ 1Z101 = 81 \cdot 1 + 27 \cdot (-1) + 9 \cdot 1 + 3 \cdot 0 + 1 \cdot 1 = 64_{10} $$

Exemplo 2: Vamos converter 237 para ternário equilibrado. Primeiro, usamos o ternário normal para reescrever o número:

$$ 237_{10} = 22210_{3} $$ 
Vamos processar a partir do dígito menos significativo (à direita):

0 e 1 são ignorados, pois são permitidos no ternário equilibrado.
2 é transformado em Z, aumentando o dígito à sua esquerda, então obtemos 23Z10.
3 é transformado em 0, aumentando o dígito à sua esquerda, então obtemos 30Z10.
3 é transformado em 0, aumentando o dígito à sua esquerda (que é por padrão 0), e assim obtemos 100Z10.
O resultado final é 100Z10.

Vamos convertê-lo de volta para o sistema decimal adicionando os valores posicionais ponderados:

$$ 100Z10 = 243 \cdot 1 + 81 \cdot 0 + 27 \cdot 0 + 9 \cdot (-1) + 3 \cdot 1 + 1 \cdot 0 = 237_{10} $$ 