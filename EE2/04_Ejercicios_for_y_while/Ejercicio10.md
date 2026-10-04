# Pregunta 4 — Ejercicio 1: Primer múltiplo que supera 50

## Enunciado

Implementa un programa en Python que, para cada número del 1 al 8, encuentre el **primer múltiplo de ese número que sea estrictamente mayor a 50**, usando un bucle `for` externo y un bucle `while` interno.

Para cada número, muestra:
- El número analizado
- El primer múltiplo mayor a 50
- Cuántas multiplicaciones fueron necesarias para encontrarlo

**Ejemplo de salida (extracto):**
```
Número: 1 → primer múltiplo > 50: 51 (factor: 51, intentos: 51)
Número: 2 → primer múltiplo > 50: 52 (factor: 26, intentos: 26)
Número: 7 → primer múltiplo > 50: 56 (factor: 8, intentos: 8)
```

---

## Resolución paso a paso

### Paso 1 — Identificar la estructura de bucles

- El `for` externo recorre los números del 1 al 8.
- El `while` interno, para cada número `i`, multiplica `i * factor` e incrementa `factor` hasta que el resultado supere 50.

### Paso 2 — Diseñar el `while` interno

El `while` debe continuar mientras el múltiplo actual **no supere** 50:

```python
factor = 1
while i * factor <= 50:
    factor = factor + 1
```

Cuando el `while` termina, `i * factor` es el primer múltiplo de `i` mayor a 50, y `factor` es el número de multiplicaciones realizadas.

### Paso 3 — Escribir el programa

```python
def main():
    for i in range(1, 9):
        factor = 1
        while i * factor <= 50:
            factor = factor + 1

        multiplo = i * factor
        print(f"Número: {i} → primer múltiplo > 50: {multiplo} (factor: {factor}, intentos: {factor})")

main()
```

### Paso 4 — Verificar con ejemplos

**Para `i = 7`:**
- `factor = 1`: `7 * 1 = 7 <= 50` → incrementa
- `factor = 2`: `7 * 2 = 14 <= 50` → incrementa
- ...
- `factor = 7`: `7 * 7 = 49 <= 50` → incrementa
- `factor = 8`: `7 * 8 = 56 > 50` → sale del `while`
- Resultado: `56`, factor `8`, intentos `8` ✅

**Para `i = 1`:**
- El `while` avanza hasta `factor = 51` (pues `1 * 50 = 50 <= 50` todavía continúa)
- `factor = 51`: `1 * 51 = 51 > 50` → sale
- Resultado: `51`, factor `51`, intentos `51` ✅

**Para `i = 8`:**
- `factor = 6`: `8 * 6 = 48 <= 50` → incrementa
- `factor = 7`: `8 * 7 = 56 > 50` → sale
- Resultado: `56`, factor `7`, intentos `7` ✅

### Paso 5 — Tabla completa de resultados

| `i` | Primer múltiplo > 50 | Factor |
|---|---|---|
| 1 | 51 | 51 |
| 2 | 52 | 26 |
| 3 | 51 | 17 |
| 4 | 52 | 13 |
| 5 | 55 | 11 |
| 6 | 54 | 9 |
| 7 | 56 | 8 |
| 8 | 56 | 7 |

### Paso 6 — Puntos a revisar en el código

**¿Por qué `factor` se inicializa en `1` dentro del `for` y no fuera?**
Porque debe reiniciarse para cada número `i`. Si se inicializara fuera del `for`, al llegar al segundo número `i = 2`, `factor` ya tendría el valor con el que terminó para `i = 1`, y el resultado sería incorrecto.

**¿Por qué la condición del `while` es `<= 50` y no `< 50`?**
Porque se busca el primer múltiplo **estrictamente mayor** a 50. Si se usara `< 50`, el bucle se detendría en 50, que no es mayor a 50.

---

> 💡 **Puntos clave de este ejercicio:**
> - `for` externo con `range(1, 9)` para recorrer los números del 1 al 8.
> - `while` interno con condición sobre el múltiplo calculado en cada iteración.
> - `factor` reiniciado dentro del `for` para que cada número empiece desde 1.
> - La variable de control del `while` (`factor`) actúa simultáneamente como contador de intentos y como multiplicador.
