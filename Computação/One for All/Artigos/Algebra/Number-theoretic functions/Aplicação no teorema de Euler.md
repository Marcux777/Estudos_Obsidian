A propriedade mais famosa e importante da função totiente de Euler é expressa no teorema de Euler:
$$a^{\phi(m)} \equiv 1 \pmod m \quad \text{se } a \text{ e } m \text{ são primos entre si.}$$ 
No caso particular em que  $m$  é primo, o teorema de Euler se transforma no pequeno teorema de Fermat:

$$a^{m - 1} \equiv 1 \pmod m$$ 
O teorema de Euler e a função totiente de Euler ocorrem com bastante frequência em aplicações práticas, por exemplo, ambos são usados para calcular o inverso multiplicativo modular.

Como consequência imediata, também obtemos a equivalência:

$$a^n \equiv a^{n \bmod \phi(m)} \pmod m$$ 
Isso permite calcular  $x^n \bmod m$  para $n$  muito grande, especialmente se  $n$  é o resultado de outro cálculo, pois permite calcular  $n$  sob um módulo.

[[Teoria dos Grupos]]
