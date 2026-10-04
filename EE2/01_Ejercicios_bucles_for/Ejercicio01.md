# Ejercicio 1: Factorial de un número

## Enunciado

Implementa un programa en Python que solicite al usuario un número entero positivo `n` y calcule su **factorial**. El factorial de `n` se define como:

```
n! = 1 × 2 × 3 × ... × n
```

Por convención, `0! = 1`.

Al finalizar, el programa debe indicar si el resultado es **par** o **impar**.

**Ejemplos:**
- `n = 5` → `5! = 120` → `120 es par`
- `n = 3` → `3! = 6` → `6 es par`
- `n = 1` → `1! = 1` → `1 es impar`

---

## Resolución paso a paso

### Paso 1 — Identificar entradas, proceso y salida

- **Entrada:** un número entero `n`
- **Proceso:** multiplicar todos los enteros desde 1 hasta `n` usando un acumulador; luego verificar si el resultado es par o impar
- **Salida:** el valor del factorial y si es par o impar

### Paso 2 — Reconocer el patrón: acumulador multiplicativo

El factorial es un acumulador, pero en lugar de sumar, **multiplica**. La lógica es la misma que un acumulador de sumas, solo cambia el operador y el valor inicial:

- Un acumulador de sumas empieza en `0` (el neutro de la suma).
- Un acumulador de productos empieza en `1` (el neutro de la multiplicación).

```python
# Acumulador de suma        # Acumulador de producto
s = 0                       f = 1
s = s + n                   f = f * i
```

### Paso 3 — Elegir el bucle correcto

Se sabe exactamente cuántas veces hay que multiplicar: desde `1` hasta `n`. Eso indica un `for` con `range(1, n + 1)`.

> ⚠️ `range(1, n + 1)` y no `range(1, n)` porque el valor `fin` de `range` no se incluye, y necesitamos que `n` sí participe en la multiplicación.

### Paso 4 — Verificar la paridad

Un número es par si su resto al dividir entre 2 es 0: `resultado % 2 == 0`.

### Paso 5 — Escribir el programa

```python
def main():
    n = int(input("Ingrese un número entero positivo: "))

    factorial = 1
    for i in range(1, n + 1):
        factorial = factorial * i

    print(f"{n}! = {factorial}")

    if factorial % 2 == 0:
        print(f"{factorial} es par")
    else:
        print(f"{factorial} es impar")

main()
```

### Paso 6 — Verificar con ejemplos

**Ejemplo 1: `n = 5`**
- `i = 1` → `factorial = 1 * 1 = 1`
- `i = 2` → `factorial = 1 * 2 = 2`
- `i = 3` → `factorial = 2 * 3 = 6`
- `i = 4` → `factorial = 6 * 4 = 24`
- `i = 5` → `factorial = 24 * 5 = 120`
- `120 % 2 == 0` → par ✅

**Ejemplo 2: `n = 0`**
- `range(1, 1)` no genera ningún valor → el bucle no se ejecuta
- `factorial` conserva su valor inicial: `1`
- `0! = 1`, `1 % 2 != 0` → impar ✅

### Paso 7 — ¿Por qué `factorial` empieza en `1` y no en `0`?

Si empezara en `0`, la primera multiplicación daría `0 * 1 = 0`, y todas las siguientes también serían `0`. El acumulador multiplicativo **debe inicializarse en 1** para no destruir los valores que se vayan acumulando.

---

> 💡 **Puntos clave de este ejercicio:**
> - `for` con `range(1, n + 1)` para recorrer de 1 a n inclusive.
> - Acumulador multiplicativo inicializado en `1`.
> - Condicional post-bucle para clasificar el resultado con `%`.
> - Caso borde `n = 0`: el bucle no se ejecuta y el acumulador conserva su valor inicial.
