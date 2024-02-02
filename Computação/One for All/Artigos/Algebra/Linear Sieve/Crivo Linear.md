Dado um número  $n$ , encontre todos os números primos em um segmento $[2;n]$ .

A maneira padrão de resolver uma tarefa é usar o [[Crivo de Eratóstenes]]. Este algoritmo é muito simples, mas tem tempo de execução $O(n \log \log n)$ .

Embora existam muitos algoritmos conhecidos com tempo de execução sublinear (ou seja, $o(n)$ ), o algoritmo descrito abaixo é interessante por sua simplicidade: não é mais complexo do que o crivo clássico de Eratóstenes.

Além disso, o algoritmo dado aqui calcula as fatorações de todos os números no segmento  $[2; n]$  como um efeito colateral, e isso pode ser útil em muitas aplicações práticas.

A fraqueza do algoritmo dado está em usar mais memória do que o crivo clássico de Eratóstenes: ele requer uma matriz de  $n$  números, enquanto para o crivo clássico de Eratóstenes é suficiente ter  $n$  bits de memória (que é 32 vezes menos).

Portanto, faz sentido usar o algoritmo descrito apenas para números da ordem de  $10^7$  e não maiores.

## Algoritmo
Nosso objetivo é calcular o menor fator primo  $lp [i]$  para cada número  $i$  no segmento  $[2; n]$ .

Além disso, precisamos armazenar a lista de todos os números primos encontrados - vamos chamá-la de  $pr []$ .

Inicializaremos os valores  $lp [i]$  com zeros, o que significa que assumimos que todos os números são primos. Durante a execução do algoritmo, essa matriz será preenchida gradualmente.

Agora vamos passar pelos números de 2 a  $n$ . Temos dois casos para o número atual  $i$ :

- $lp[i] = 0$  - isso significa que  $i$  é primo, ou seja, não encontramos fatores menores para ele. Portanto, atribuímos  $lp [i] = i$  e adicionamos $i$  ao final da lista  $pr[]$ .

- $lp[i] \neq 0$  - isso significa que  $i$  é composto, e seu menor fator primo é  $lp [i]$ .

Em ambos os casos, atualizamos os valores de  $lp []$  para os números que são divisíveis por  $i$ . No entanto, nosso objetivo é aprender a fazer isso de forma a definir um valor  $lp []$  no máximo uma vez para cada número. Podemos fazer isso da seguinte maneira:

Vamos considerar os números  $x_j = i \cdot p_j$ , onde  $p_j$  são todos os números primos menores ou iguais a  $lp [i]$  (é por isso que precisamos armazenar a lista de todos os números primos).

Definiremos um novo valor  $lp [x_j] = p_j$  para todos os números desta forma.

A prova de correção deste algoritmo e seu tempo de execução podem ser encontrados após a implementação.
## Implementação

```cpp
const int N = 10000000;
vector<int> lp(N+1);
vector<int> pr;

for (int i=2; i <= N; ++i) {
    if (lp[i] == 0) {
        lp[i] = i;
        pr.push_back(i);
    }
    for (int j = 0; i * pr[j] <= N; ++j) {
        lp[i * pr[j]] = pr[j];
        if (pr[j] == lp[i]) {
            break;
        }
    }
}
```

## Prova de Corretude
Precisamos provar que o algoritmo define todos os valores  $lp []$  corretamente, e que cada valor será definido exatamente uma vez. Portanto, o algoritmo terá tempo de execução linear, já que todas as demais ações do algoritmo, obviamente, funcionam para  $O (n)$ .

Observe que todo número  $i$  tem exatamente uma representação na forma:

 
$$i = lp [i] \cdot x,$$ 
onde  $lp [i]$  é o fator primo mínimo de  $i$ , e o número  $x$  não tem nenhum fator primo menor que  $lp [i]$ , ou seja,

 
$$lp [i] \le lp [x].$$ 
Agora, vamos comparar isso com as ações do nosso algoritmo: na verdade, para cada  $x$  ele passa por todos os números primos pelos quais poderia ser multiplicado, ou seja, todos os números primos até  $lp [x]$  inclusive, a fim de obter os números na forma dada acima.

Portanto, o algoritmo passará por cada número composto exatamente uma vez, definindo os valores corretos  $lp []$  [Q.E.D.](https://dicionario.priberam.org/QED).


## Tempo de Execução e Memória

Embora o tempo de execução de  $O(n)$  seja melhor do que  $O(n \log \log n)$  do crivo clássico de Eratóstenes, a diferença entre eles não é tão grande. Na prática, o crivo linear funciona quase tão rápido quanto uma implementação típica do crivo de Eratóstenes.

Em comparação com as versões otimizadas do crivo de Eratóstenes, por exemplo, o crivo segmentado, é muito mais lento.

Considerando os requisitos de memória deste algoritmo - um array  $lp []$  de comprimento $n$ , e um array de  $pr []$  de comprimento  $\frac n {\ln n}$ , este algoritmo parece ser pior do que o crivo clássico em todos os aspectos.

No entanto, sua qualidade redentora é que este algoritmo calcula um array  
$lp []$ , que nos permite encontrar a fatoração de qualquer número no segmento  
$[2; n]$  no tempo da ordem de tamanho dessa fatoração. Além disso, usando apenas um array extra, poderemos evitar divisões ao procurar a fatoração.

Conhecer as fatorações de todos os números é muito útil para algumas tarefas, e este algoritmo é um dos poucos que permitem encontrá-las em tempo linear.
