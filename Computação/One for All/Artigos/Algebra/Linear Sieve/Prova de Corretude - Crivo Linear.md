Precisamos provar que o algoritmo define todos os valores  $lp []$  corretamente, e que cada valor será definido exatamente uma vez. Portanto, o algoritmo terá tempo de execução linear, já que todas as demais ações do algoritmo, obviamente, funcionam para  $O (n)$ .

Observe que todo número  $i$  tem exatamente uma representação na forma:

 
$$i = lp [i] \cdot x,$$ 
onde  $lp [i]$  é o fator primo mínimo de  $i$ , e o número  $x$  não tem nenhum fator primo menor que  $lp [i]$ , ou seja,

 
$$lp [i] \le lp [x].$$ 
Agora, vamos comparar isso com as ações do nosso algoritmo: na verdade, para cada  $x$  ele passa por todos os números primos pelos quais poderia ser multiplicado, ou seja, todos os números primos até  $lp [x]$  inclusive, a fim de obter os números na forma dada acima.

Portanto, o algoritmo passará por cada número composto exatamente uma vez, definindo os valores corretos  $lp []$  [Q.E.D.](https://dicionario.priberam.org/QED).

