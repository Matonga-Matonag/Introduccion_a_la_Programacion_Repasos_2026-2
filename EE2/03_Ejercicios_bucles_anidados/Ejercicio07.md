# Ejercicio 7: Tablas de multiplicar filtradas

## Enunciado

Implementa un programa en Python que imprima las tablas de multiplicar del 1 al 10, pero que **solo muestre las multiplicaciones cuyo resultado sea divisible entre 3**.

Al finalizar cada tabla, imprime cuántos resultados de esa tabla fueron divisibles entre 3.

**Ejemplo (extracto de la tabla del 2):**
```
--- Tabla del 2 ---
2 x 3 = 6
2 x 6 = 12
2 x 9 = 18
Resultados divisibles entre 3 en la tabla del 2: 3
```

---

## Resolución paso a paso

### Paso 1 — Identificar la estructura de bucles necesaria

- El bucle **externo** recorre los números del 1 al 10 (el multiplicador de cada tabla).
- El bucle **interno** recorre los factores del 1 al 10 para cada tabla.
- Dentro del bucle interno, un `if` filtra solo los resultados divisibles entre 3.

### Paso 2 — Detectar divisibilidad entre 3

Un número es divisible entre 3 si su resto al dividir entre 3 es 0:

```python
if (i * j) % 3 == 0:
```

### Paso 3 — Contar los resultados divisibles por tabla

Se necesita un contador que se **reinicie a 0 en cada iteración del bucle externo** (antes de que arranque el bucle interno), para llevar la cuenta de cada tabla por separado.

```python
for i in range(1, 11):       # bucle externo: tabla del i
    contador = 0             # se reinicia para cada tabla
    for j in range(1, 11):   # bucle interno: factor j
        if (i * j) % 3 == 0:
            contador = contador + 1
            ...
```

### Paso 4 — Escribir el programa

```python
def main():
    for i in range(1, 11):
        print(f"--- Tabla del {i} ---")
        contador = 0
        for j in range(1, 11):
            resultado = i * j
            if resultado % 3 == 0:
                print(f"{i} x {j} = {resultado}")
                contador = contador + 1
        print(f"Resultados divisibles entre 3 en la tabla del {i}: {contador}")
        print()

main()
```

### Paso 5 — Verificar con la tabla del 2

| `j` | `2 * j` | `% 3 == 0`? | Se imprime |
|---|---|---|---|
| 1 | 2 | No | — |
| 2 | 4 | No | — |
| 3 | 6 | Sí | `2 x 3 = 6` |
| 4 | 8 | No | — |
| 5 | 10 | No | — |
| 6 | 12 | Sí | `2 x 6 = 12` |
| 7 | 14 | No | — |
| 8 | 16 | No | — |
| 9 | 18 | Sí | `2 x 9 = 18` |
| 10 | 20 | No | — |

- `contador = 3` → `"Resultados divisibles entre 3 en la tabla del 2: 3"` ✅

### Paso 6 — ¿Cuántos resultados divisibles entre 3 tiene cada tabla?

Toda tabla del 1 al 10 tiene exactamente **3** resultados divisibles entre 3 (los factores 3, 6 y 9), porque `i * 3`, `i * 6` e `i * 9` siempre son múltiplos de 3 independientemente de `i`. La tabla del 3, del 6 y del 9 tendrán más, porque todos sus múltiplos son divisibles entre 3.

### Paso 7 — Puntos a revisar en el código

**¿Por qué `contador = 0` está dentro del bucle externo y no fuera?**
Si estuviera fuera, acumularía los resultados de todas las tablas sin reiniciarse. Al colocarlo dentro del bucle externo (pero fuera del interno), se reinicia en cada tabla nueva.

**¿Por qué se guarda `i * j` en `resultado` en lugar de calcular `i * j` dos veces?**
Para no repetir la multiplicación en el `if` y en el `print`. Guardarla en una variable intermedia es más eficiente y legible.

---

> 💡 **Puntos clave de este ejercicio:**
> - Doble `for` con `range(1, 11)` para recorrer todas las combinaciones de la tabla.
> - `if` dentro del bucle interno para filtrar resultados.
> - Contador reiniciado en cada iteración del bucle externo para contar por tabla.
> - Variable intermedia `resultado` para no calcular `i * j` dos veces.
