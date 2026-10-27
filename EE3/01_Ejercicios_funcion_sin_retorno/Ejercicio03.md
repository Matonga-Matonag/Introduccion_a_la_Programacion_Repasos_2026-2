# Ejercicio 3: Resumen de una serie de números

## Enunciado

Implementa las siguientes funciones **sin retorno**:

1. `mostrar_linea()`: imprime una línea de 30 guiones `-`.
2. `mostrar_resumen_numeros(cantidad)`: pide `cantidad` números enteros al usuario con un `for`. Por cada número:
   - Indica si es **par** o **impar** (usando `%`).
   - Lo clasifica en **positivo**, **negativo** o **cero** (usando `if/elif/else`).

   Al terminar, llama a `mostrar_linea()` y muestra el conteo de positivos, negativos y ceros, seguido de la suma total de los números.

El programa principal debe pedir cuántos números ingresará el usuario (mínimo 1, con validación con `while`) y llamar a `mostrar_resumen_numeros`.

**Ejemplo con cantidad = 3, números: 4, -3, 0:**
```
Número 1: 4 es par y es positivo.
Número 2: -3 es impar y es negativo.
Número 3: 0 es par y es cero.
------------------------------
Positivos: 1
Negativos: 1
Ceros: 1
Suma total: 1
```

---

## Resolución paso a paso

### Paso 1 — Identificar qué hace cada función

| Función | Tipo | Qué hace |
|---|---|---|
| `mostrar_linea()` | Sin retorno | Imprime una línea decorativa |
| `mostrar_resumen_numeros(cantidad)` | Sin retorno | Pide datos, clasifica e imprime el resumen |

`mostrar_resumen_numeros` **llama** a `mostrar_linea`: esto es composición de funciones sin retorno.

### Paso 2 — Paridad con `%`

Un número es par si `numero % 2 == 0`. Esto también funciona con negativos en Python (por ejemplo, `-4 % 2` vale `0`, y `-3 % 2` vale `1`).

### Paso 3 — Clasificación con `if/elif/else`

```python
if numero > 0:
    positivos = positivos + 1
elif numero < 0:
    negativos = negativos + 1
else:
    ceros = ceros + 1
```

### Paso 4 — Escribir las funciones

```python
def mostrar_linea():
    print("-" * 30)

def mostrar_resumen_numeros(cantidad):
    positivos = 0
    negativos = 0
    ceros = 0
    suma = 0

    for i in range(cantidad):
        numero = int(input(f"Ingrese el número {i + 1}: "))
        suma = suma + numero

        if numero % 2 == 0:
            paridad = "par"
        else:
            paridad = "impar"

        if numero > 0:
            signo = "positivo"
            positivos = positivos + 1
        elif numero < 0:
            signo = "negativo"
            negativos = negativos + 1
        else:
            signo = "cero"
            ceros = ceros + 1

        print(f"Número {i + 1}: {numero} es {paridad} y es {signo}.")

    mostrar_linea()
    print(f"Positivos: {positivos}")
    print(f"Negativos: {negativos}")
    print(f"Ceros: {ceros}")
    print(f"Suma total: {suma}")
```

### Paso 5 — Programa principal con validación

```python
def main():
    cantidad = int(input("¿Cuántos números desea ingresar? "))
    while cantidad < 1:
        print("Debe ingresar al menos un número.")
        cantidad = int(input("¿Cuántos números desea ingresar? "))

    mostrar_resumen_numeros(cantidad)

main()
```

### Paso 6 — Verificar con el ejemplo

Números: `4, -3, 0`

| `numero` | `% 2 == 0` | Signo | `positivos` | `negativos` | `ceros` | `suma` |
|---|---|---|---|---|---|---|
| 4 | Sí → par | positivo | 1 | 0 | 0 | 4 |
| -3 | No → impar | negativo | 1 | 1 | 0 | 1 |
| 0 | Sí → par | cero | 1 | 1 | 1 | 1 |

Salida final: `Positivos: 1`, `Negativos: 1`, `Ceros: 1`, `Suma total: 1` ✅

### Paso 7 — Puntos a revisar

**¿Por qué `mostrar_linea` es una función separada?**
Porque es una tarea pequeña y reutilizable. Si se quisiera cambiar el estilo de la línea, solo habría que modificar un lugar.

**¿Por qué `suma` se actualiza para todos los números?**
La suma no depende de la clasificación: incluye positivos, negativos y ceros. Por eso se actualiza fuera de los `if/elif/else`.

---

> 💡 **Puntos clave de este ejercicio:**
> - Composición: una función sin retorno llama a otra sin retorno.
> - Bucle `for` con número de iteraciones conocido.
> - `%` para determinar la paridad, incluso con números negativos.
> - `if/elif/else` para clasificar, con varios contadores y acumuladores dentro del bucle.
