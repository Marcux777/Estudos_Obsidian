
## Tornar Gramatica livre de ε

1. Identificação de regras que geram ε:
	O primeiro passo é identificar todas as regras da gramática que podem gerar a cadeia vazia (ε). Isso pode ser feito manualmente ou utilizando ferramentas automatizadas de análise de gramáticas.

2. Remoção de regras que geram ε:
	Após identificar as regras que geram ε, estas devem ser removidas da gramática. No entanto, é importante ter cuidado para não remover regras que são essenciais para a geração de outras cadeias válidas.

3. Redefinição de regras que podem gerar ε:
	Algumas regras podem gerar ε indiretamente, mesmo que não o façam de forma direta. Isso pode acontecer quando uma regra permite a produção de uma sequência de símbolos que, por sua vez, podem gerar ε através de outras regras. Para lidar com isso, é necessário redefinir essas regras de forma que não permitam a produção de ε.

4. Verificação da consistência da gramática:
	Após remover e redefinir as regras, é importante verificar se a gramática ainda é consistente e expressiva. Isso pode ser feito manualmente ou utilizando ferramentas automatizadas de análise de gramáticas.

5. Simplificação da gramática:
	Após garantir a consistência da gramática, é possível realizar etapas de simplificação para remover regras redundantes ou desnecessárias, tornando a gramática mais compacta e eficiente.

## Fatorar uma gramática
Os conceitos de fatoração à esquerda, fatoração à direita e eliminação de recursão à esquerda estão corretos, mas a aplicação desses conceitos nos exemplos apresentados precisa de alguns ajustes. Vamos corrigir:

1. **Fatoração à esquerda:**
    
    - **Regra:** A -> αB | αC, onde α é qualquer sequência de símbolos não terminais e B, C são símbolos não terminais.
    - **Substituição:** Substituir a regra A -> αB | αC por um conjunto de regras:
        - A -> αX
        - X -> B | C
2. **Fatoração à direita:**
    
    - **Regra:** A -> Bα | Cα, onde α é qualquer sequência de símbolos não terminais e B, C são símbolos não terminais.
    - **Substituição:** Substituir a regra A -> Bα | Cα por um conjunto de regras:
        - A -> Xα
        - X -> B | C
3. **Eliminação de recursão à esquerda:**
    
    - **Regra:** A -> Aα | β, onde α e β são quaisquer sequências de símbolos não terminais e A é um símbolo não terminal.
    - **Substituição:** Substituir a regra A -> Aα | β por um conjunto de regras:
        - A -> βX
        - X -> αX | ε

# LL(1)
## O que é LL(1)?

**LL(1)**, sigla para **Left to right, Left-most derivation, 1 symbol lookahead**, é um tipo de gramática formal que pode ser analisada por um **analisador sintático descendente** usando apenas um único símbolo futuro ("lookahead") para tomar decisões de análise. Isso significa que o analisador pode ler a entrada da esquerda para a direita e deduzir a estrutura da sentença sem precisar voltar atrás ou usar recursividade.

**Características das gramáticas LL(1):**

* **Sem ambiguidade:** A gramática não pode gerar duas derivações diferentes para a mesma sentença de entrada.
* **Sem recursão à esquerda:** A gramática não pode conter regras onde um símbolo não terminal aparece no lado esquerdo e direito da mesma regra.
* **Propriedade First/Follow:** Para cada símbolo não terminal A e símbolo terminal a, os conjuntos First(A) e Follow(A) devem ser disjuntos, a menos que A possa gerar ε (a cadeia vazia).

**Vantagens das gramáticas LL(1):**

* **Analisadores simples e eficientes:** Gramáticas LL(1) podem ser facilmente analisadas por analisadores descendentes, que são simples de implementar e eficientes em termos de tempo e espaço.
* **Fácil de depurar:** Erros de análise em gramáticas LL(1) são geralmente fáceis de identificar e depurar, pois o analisador sempre segue um caminho único durante a análise.
* **Ampla aplicabilidade:** Gramáticas LL(1) são utilizadas em diversas áreas da computação, como compiladores, intérpretes, editores de texto e ferramentas de análise de linguagem.

**Exemplos de gramáticas LL(1):**

* A gramática para expressões aritméticas simples:
    ```
	   PROG -> CMD ; PROG 
	   PROG -> CMD -> id = EXP 
	   CMD -> print EXP 
	   EXP -> id 
	   EXP -> num 
	   EXP -> ( EXP + EXP )
    ```

**Limitações das gramáticas LL(1):**

Nem todas as gramáticas formais podem ser expressas como gramáticas LL(1). Gramáticas que contêm ambiguidade ou recursão à esquerda não podem ser analisadas por um analisador LL(1). Nesses casos, podem ser necessários outros tipos de analisadores sintáticos, como analisadores LR ou SLR.

Na análise sintática LL(1), a tabela é fundamental no processo de **análise descendente**. Ela orienta o **analisador sintático**, indicando qual ação deve ser tomada (**reduzir**, **deslocar** ou **aceitar**) para cada símbolo de entrada e símbolo no topo da pilha.

A tabela LL(1) é composta por linhas e colunas, onde cada linha representa um símbolo não terminal da gramática e cada coluna representa um símbolo terminal ou o símbolo especial $ (fim da entrada). Cada célula da tabela contém uma entrada que indica a ação a ser tomada pelo analisador sintático.

**Entradas da tabela LL(1):**

- **Redução:** Se a célula contiver uma regra gramatical (A -> α), o analisador deve **reduzir** a pilha, substituindo o símbolo não terminal A no topo da pilha pelos símbolos do lado direito da regra (α).
- **Deslocamento:** Se a célula contiver um símbolo terminal a, o analisador deve **deslocar** o símbolo a da entrada para a pilha.
- **Aceitação:** Se a célula contiver o símbolo especial $ e o símbolo de topo da pilha for o símbolo inicial da gramática, o analisador deve **aceitar** a entrada como uma sentença válida da linguagem.
- **Erro:** Se a célula estiver vazia e o símbolo de entrada não for $ ou o símbolo de topo da pilha não for um símbolo terminal, o analisador deve **sinalizar um erro** de análise.

**Construção da tabela LL(1):**

A construção da tabela LL(1) envolve a utilização dos conceitos de **First** e **Follow** de cada símbolo não terminal da gramática. O conjunto **First(A)** contém todos os símbolos terminais que podem iniciar uma derivação à esquerda a partir do símbolo não terminal A. O conjunto **Follow(A)** contém todos os símbolos terminais que podem aparecer após A em qualquer derivação à esquerda.

A partir dos conjuntos First e Follow, é possível determinar as entradas da tabela LL(1) para cada combinação de símbolo não terminal e símbolo terminal ou $. Essa construção garante que o analisador LL(1) possa tomar decisões corretas durante a análise da entrada, evitando ambiguidades e erros.
