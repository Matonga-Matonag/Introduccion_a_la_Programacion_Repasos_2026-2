# Ejercicio 5: Máximo común divisor y mínimo común múltiplo

## Enunciado

Implementa dos funciones **con retorno**:

1. `calcular_mcd(a, b)`: devuelve el **máximo común divisor** de dos enteros positivos. Debe calcularse con el **algoritmo de Euclides** usando un `while` (no recursión):
   - Mientras `b` sea distinto de `0`: el residuo es `a % b`, luego `a` toma el valor de `b` y `b` toma el valor del residuo.
   - Cuando `b` llega a `0`, el resultado es `a`.

2. `calcular_mcm(a, b)`: devuelve el **mínimo común múltiplo**, usando la relación:
   ```
   mcm(a, b) = (a * b) // mcd(a, b)
   ```
   Esta función debe **llamar a `calcular_mcd`** para obtener el mcd.

El programa principal debe pedir dos números enteros positivos (con validación con `while`: si alguno es menor que 1, volver a pedirlo) y mostrar el mcd y el mcm.

**Ejemplo con a = 12, b = 18:**
```
MCD: 6
MCM: 36
```

---

## Resolución paso a paso

### Paso 1 — Comprender el algoritmo de Euclides

Para calcular el mcd de 48 y 18, el proceso es:

| `a` | `b` | `residuo = a % b` | Nuevo `a` | Nuevo `b` |
|---|---|---|---|---|
| 48 | 18 | 12 | 18 | 12 |
| 18 | 12 | 6 | 12 | 6 |
| 12 | 6 | 0 | 6 | 0 |

Como `b` llegó a `0`, el mcd es `a = 6` ✅

### Paso 2 — Escribir `calcular_mcd` con `while`

```python
def calcular_mcd(a, b):
    while b != 0:
        residuo = a % b
        a = b
        b = residuo
    return a
```

> ⚠️ El orden de las asignaciones importa. Primero se guarda el residuo, luego se actualiza `a` y, por último, `b`. Si se cambiara el orden, se perdería un valor.

### Paso 3 — Escribir `calcular_mcm` llamando a `calcular_mcd`

```python
def calcular_mcm(a, b):
    mcd = calcular_mcd(a, b)
    return (a * b) // mcd
```

Se usa `//` (división entera) porque el resultado debe ser un entero.

### Paso 4 — Validación en el programa principal

```python
def main():
    a = int(input("Ingrese el primer número entero positivo: "))
    while a < 1:
        print("El número debe ser positivo.")
        a = int(input("Ingrese el primer número entero positivo: "))

    b = int(input("Ingrese el segundo número entero positivo: "))
    while b < 1:
        print("El número debe ser positivo.")
        b = int(input("Ingrese el segundo número entero positivo: "))

    print(f"MCD: {calcular_mcd(a, b)}")
    print(f"MCM: {calcular_mcm(a, b)}")

main()
```

### Paso 5 — Verificar con a = 12, b = 18

**MCD:**

| `a` | `b` | `residuo = a % b` | Nuevo `a` | Nuevo `b` |
|---|---|---|---|---|
| 12 | 18 | 12 | 18 | 12 |
| 18 | 12 | 6 | 12 | 6 |
| 12 | 6 | 0 | 6 | 0 |

MCD = `6` ✅

**MCM:** `(12 * 18) // 6 = 216 // 6 = 36` ✅

### Paso 6 — Puntos a revisar

**¿Por qué `calcular_mcm` no repite el algoritmo de Euclides?**
Porque ya existe una función que resuelve ese problema. Reutilizarla evita duplicar código y, si se corrige el mcd, el mcm se corrige automáticamente. Esto es composición de funciones con retorno.

**¿Qué pasa si `a` es menor que `b`?**
No hay problema. En la primera iteración, `a % b` será `a` (porque `a < b`), y en la siguiente iteración los valores se intercambian de forma natural. Por ejemplo, `calcular_mcd(6, 18)` devuelve `6`.

**¿Por qué se usa `//` y no `/` en el mcm?**
`/` devuelve un `float` (por ejemplo, `36.0`), mientras que `//` devuelve un entero (`36`).

---

> 💡 **Puntos clave de este ejercicio:**
> - `while` con una condición que depende de una variable que cambia en cada iteración.
> - Uso de `%` para obtener el residuo.
> - Función con retorno que llama a otra función con retorno.
> - Diferencia entre `/` (float) y `//` (entero).
> - Validación de entrada con `while` en `main`.
