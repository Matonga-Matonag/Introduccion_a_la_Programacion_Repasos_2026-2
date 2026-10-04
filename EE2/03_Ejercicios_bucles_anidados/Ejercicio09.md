# Pregunta 3 — Ejercicio 3: Tablas de multiplicar con suma y ranking

## Enunciado

Implementa un programa en Python que, usando **tres bucles `for` anidados**, realice lo siguiente:

1. El bucle más externo recorre los números del 1 al 5 (las tablas a imprimir).
2. El bucle intermedio recorre los factores del 1 al 10 e imprime cada multiplicación.
3. El bucle más interno calcula la **suma de todos los resultados** de esa tabla (es decir, suma `i*1 + i*2 + ... + i*10`) usando un tercer bucle separado.

Al finalizar cada tabla, muestra la suma de sus resultados. Al finalizar todas las tablas, muestra cuál fue la tabla con la **mayor suma**.

**Ejemplo de salida (extracto):**
```
--- Tabla del 1 ---
1 x 1 = 1
...
1 x 10 = 10
Suma de resultados: 55

--- Tabla del 2 ---
2 x 1 = 2
...
Suma de resultados: 110
...
Tabla con mayor suma: 5 (suma = 275)
```

---

## Resolución paso a paso

### Paso 1 — Identificar los tres bucles necesarios

- **Bucle externo (`i`):** recorre las tablas del 1 al 5.
- **Bucle intermedio (`j`):** imprime las multiplicaciones de cada tabla (factores 1 al 10).
- **Bucle interno (`k`):** calcula la suma de todos los resultados de la tabla `i` recorriendo los mismos factores del 1 al 10.

> 💡 Los bucles intermedio e interno son **hermanos** (no están uno dentro del otro): el intermedio imprime la tabla, y el interno la recorre de nuevo para sumar. Ambos viven dentro del bucle externo.

```
for i (tablas 1..5):
    for j (factores 1..10):   ← imprime
        ...
    for k (factores 1..10):   ← suma
        ...
```

### Paso 2 — Rastrear la tabla con mayor suma

Se necesita una variable `max_suma` que se actualice cada vez que la suma de la tabla actual supere la registrada hasta ese momento, y `tabla_max` que recuerde a qué tabla pertenece.

```python
if suma > max_suma:
    max_suma = suma
    tabla_max = i
```

Estas variables se inicializan **antes** del bucle externo.

### Paso 3 — Escribir el programa

```python
def main():
    max_suma = 0
    tabla_max = 0

    for i in range(1, 6):
        print(f"--- Tabla del {i} ---")

        for j in range(1, 11):
            print(f"{i} x {j} = {i * j}")

        suma = 0
        for k in range(1, 11):
            suma = suma + (i * k)

        print(f"Suma de resultados: {suma}")
        print()

        if suma > max_suma:
            max_suma = suma
            tabla_max = i

    print(f"Tabla con mayor suma: {tabla_max} (suma = {max_suma})")

main()
```

### Paso 4 — Verificar las sumas

La suma de los resultados de la tabla del `i` es:
```
i*1 + i*2 + ... + i*10 = i * (1 + 2 + ... + 10) = i * 55
```

| Tabla | Suma esperada |
|---|---|
| 1 | `1 * 55 = 55` |
| 2 | `2 * 55 = 110` |
| 3 | `3 * 55 = 165` |
| 4 | `4 * 55 = 220` |
| 5 | `5 * 55 = 275` |

La tabla con mayor suma es siempre la del 5 → `tabla_max = 5`, `max_suma = 275` ✅

### Paso 5 — Verificar el seguimiento de la mayor suma

| `i` | `suma` | `suma > max_suma` | `max_suma` | `tabla_max` |
|---|---|---|---|---|
| (inicio) | — | — | 0 | 0 |
| 1 | 55 | `55 > 0` → Sí | 55 | 1 |
| 2 | 110 | `110 > 55` → Sí | 110 | 2 |
| 3 | 165 | `165 > 110` → Sí | 165 | 3 |
| 4 | 220 | `220 > 165` → Sí | 220 | 4 |
| 5 | 275 | `275 > 220` → Sí | 275 | 5 |

✅

### Paso 6 — Puntos a revisar en el código

**¿Por qué el bucle de suma usa `k` y no `j`?**
Porque `j` ya está siendo usado en el bucle intermedio. Aunque en este caso los dos bucles no están anidados (son hermanos), es buena práctica usar nombres de variables distintos para cada bucle para evitar confusión.

**¿Por qué `max_suma` se inicializa en `0` y no en el resultado de la primera tabla?**
Porque al iniciarla en `0`, la primera tabla (con suma `55`) ya la supera y queda registrada correctamente. Es un patrón estándar: inicializar el máximo en un valor que cualquier resultado válido supere.

**¿En qué se diferencia esta estructura de un bucle triple completamente anidado?**
En un bucle triple completamente anidado, el bucle más interno está dentro del intermedio. Aquí, el bucle de suma (`k`) está al mismo nivel que el de impresión (`j`), ambos dentro del externo. Eso significa que primero se imprime toda la tabla y luego se recorre de nuevo para sumar.

---

> 💡 **Puntos clave de este ejercicio:**
> - Tres bucles `for`: dos al mismo nivel (hermanos) dentro del bucle externo.
> - Acumulador `suma` reiniciado en cada iteración del bucle externo.
> - Variables `max_suma` y `tabla_max` actualizadas con un `if` dentro del bucle externo para rastrear el máximo.
> - Inicialización del máximo en `0` para que cualquier resultado válido lo supere desde la primera iteración.
