# Pregunta 3 — Ejercicio 2: Triángulo con símbolos alternados

## Enunciado

Implementa un programa en Python que solicite al usuario un número `n` e imprima un triángulo de `n` filas donde:

- Las filas **impares** (1, 3, 5, ...) se dibujan con asteriscos `*`.
- Las filas **pares** (2, 4, 6, ...) se dibujan con símbolos `#`.
- La fila `i` tiene exactamente `i` símbolos.

**Ejemplo con n = 5:**
```
*
# #
* * *
# # # #
* * * * *
```

---

## Resolución paso a paso

### Paso 1 — Identificar la estructura de bucles necesaria

- El bucle **externo** recorre las filas de 1 a `n`.
- El bucle **interno** imprime los símbolos de cada fila (tantos como el número de fila).
- Un `if/else` en el bucle externo (antes del interno) decide qué símbolo usar en esa fila.

### Paso 2 — Determinar el símbolo de cada fila

La fila `i` es impar si `i % 2 != 0`, y par si `i % 2 == 0`:

```python
if i % 2 != 0:
    simbolo = "*"
else:
    simbolo = "#"
```

### Paso 3 — Imprimir los símbolos sin salto de línea

Para imprimir varios símbolos en la misma línea se usa `print(simbolo, end=" ")`. Al terminar el bucle interno, un `print()` vacío produce el salto de línea.

### Paso 4 — Escribir el programa

```python
def main():
    n = int(input("Ingrese el número de filas: "))

    for i in range(1, n + 1):
        if i % 2 != 0:
            simbolo = "*"
        else:
            simbolo = "#"

        for j in range(i):
            print(simbolo, end=" ")
        print()

main()
```

### Paso 5 — Verificar con n = 5

| `i` | `i % 2` | Símbolo | `range(i)` | Salida |
|---|---|---|---|---|
| 1 | 1 (impar) | `*` | 0..0 (1 vez) | `*` |
| 2 | 0 (par) | `#` | 0..1 (2 veces) | `# #` |
| 3 | 1 (impar) | `*` | 0..2 (3 veces) | `* * *` |
| 4 | 0 (par) | `#` | 0..3 (4 veces) | `# # # #` |
| 5 | 1 (impar) | `*` | 0..4 (5 veces) | `* * * * *` |

Coincide con el ejemplo del enunciado ✅

### Paso 6 — Puntos a revisar en el código

**¿Por qué el bucle externo usa `range(1, n + 1)` y el interno usa `range(i)`?**
- El externo va de `1` a `n` porque las filas se numeran desde 1.
- El interno usa `range(i)` porque la fila `i` tiene exactamente `i` símbolos. `range(i)` genera `i` valores (de 0 a i-1), lo que produce exactamente `i` iteraciones.

**¿Por qué se asigna el símbolo a una variable antes del bucle interno en lugar de escribir el `if` dentro?**
Asignarlo antes del bucle interno es más eficiente: la decisión se toma una sola vez por fila, no en cada iteración del bucle interno. Si se pusiera dentro del `for j`, el `if` se evaluaría `i` veces por fila con el mismo resultado.

**¿Podría el `if/else` del símbolo ir dentro del bucle interno?**
Sí, funcionaría igual, pero sería menos eficiente. En este caso la diferencia es pequeña, pero es una buena práctica evitar cálculos innecesarios dentro de bucles.

---

> 💡 **Puntos clave de este ejercicio:**
> - Doble `for` donde el `range` del bucle interno depende de la variable del externo (`range(i)`).
> - `if/else` en el bucle externo para tomar una decisión **una vez por fila**.
> - `print(simbolo, end=" ")` para imprimir en la misma línea y `print()` para el salto al final de cada fila.
> - `i % 2` para determinar la paridad de la fila.
