
Podemos calcular  $f_1(p)$  em  $O(\log m)$  usando o algoritmo de exponenciação binária. De forma semelhante para  
$f_2(q)$ .

Na primeira etapa do algoritmo, precisamos calcular  $f_1$  para cada possível argumento  $p$  e, em seguida, ordenar os valores. Assim, esta etapa tem complexidade:
  
$$O\left(\left\lceil \frac{m}{n} \right\rceil \left(\log m + \log \left\lceil \frac{m}{n} \right\rceil \right)\right) = O\left( \left\lceil \frac {m}{n} \right\rceil \log m\right)$$ 
Na segunda etapa do algoritmo, precisamos calcular  
$f_2(q)$  para cada possível argumento  
$q$  e, em seguida, realizar uma busca binária no array de valores de  
$f_1$ , assim esta etapa tem complexidade:
 
$$O\left(n \left(\log m + \log \frac{m}{n} \right) \right) = O\left(n \log m\right).$$ 
Agora, quando adicionamos essas duas complexidades, obtemos  $\log m$  multiplicado pela soma de  $n$  e  $m/n$ , que é mínima quando  $n = m/n$ , o que significa que, para obter desempenho ótimo,  
$n$  deve ser escolhido de forma que:
$$n = \sqrt{m}.$$ 
Então, a complexidade do algoritmo torna-se:
$$O(\sqrt {m} \log m).$$ 