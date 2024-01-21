
O método atual de transformar um número para o espaço de Montgomery é bastante lento. Existem maneiras mais rápidas.

Podemos observar a seguinte relação:
$$\bar{x} := x \cdot r \bmod n = x \cdot \frac{r^2}{r} = x \cdot r^2$$ 
Transformar um número para o espaço é apenas uma multiplicação dentro do espaço do número por  $r^2$ . Portanto, podemos pré-calcular  $r^2 \bmod n$  e apenas realizar uma multiplicação em vez de deslocar o número 128 vezes.

No código a seguir, inicializamos r2 com -n % n, que é equivalente a  $r - n \equiv r \bmod n$ , deslocamos isso 4 vezes para obter  $r \cdot 2^4 \bmod n$ . Este número pode ser interpretado como  $2^4$  no espaço de Montgomery. Se o elevamos ao quadrado  $5$  vezes, obtemos  $(2^4)^{2^5} = (2^4)^{32} = 2^{128} = r$  no espaço de Montgomery, que é exatamente  $r^2 \bmod n$ .

```cpp
struct Montgomery {
    Montgomery(u128 n) : mod(n), inv(1), r2(-n % n) {
        for (int i = 0; i < 7; i++)
            inv *= 2 - n * inv;

        for (int i = 0; i < 4; i++) {
            r2 <<= 1;
            if (r2 >= mod)
                r2 -= mod;
        }
        for (int i = 0; i < 5; i++)
            r2 = mul(r2, r2);
    }

    u128 init(u128 x) {
        return mult(x, r2);
    }

    u128 mod, inv, r2;
};
```

Essa implementação otimiza a transformação para o espaço de Montgomery usando  $r^2 \bmod n$  pré-computado, resultando em uma execução mais rápida.