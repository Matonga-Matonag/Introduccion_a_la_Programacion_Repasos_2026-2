# Ejercicio 3: Clasificador de números ingresados

## Enunciado

Implementa un programa en Python que solicite al usuario cuántos números desea ingresar (`n`). Luego, dentro de un bucle, pide los `n` números uno a uno y al finalizar muestra:

- La **cantidad de números positivos** ingresados
- La **cantidad de números negativos** ingresados
- La **cantidad de ceros** ingresados
- La **suma total** de todos los números
- El **promedio** de todos los números

Si todos los números ingresados son cero, en lugar del promedio mostrar el mensaje `"Todos los números son cero."`.

**Ejemplo con n = 5, números: 4, -2, 0, 7, -3:**
```
Positivos: 2
Negativos: 2
Ceros: 1
Suma total: 6
Promedio: 1.2
```

---

## Resolución paso a paso

### Paso 1 — Identificar entradas, proceso y salida

- **Entradas:** cantidad de números `n`, luego `n` números del usuario
- **Proceso:** clasificar cada número en el bucle usando `if/elif/else`; acumular la suma; contar cada categoría
- **Salida:** conteos, suma total y promedio (o mensaje especial)

### Paso 2 — Identificar los contadores y acumuladores necesarios

Se necesitan cuatro variables que se actualizan dentro del bucle:

| Variable | Tipo | Valor inicial | Se actualiza cuando... |
|---|---|---|---|
| `positivos` | Contador | `0` | El número es `> 0` |
| `negativos` | Contador | `0` | El número es `< 0` |
| `ceros` | Contador | `0` | El número es `== 0` |
| `suma` | Acumulador | `0` | Siempre (con cualquier número) |

### Paso 3 — Elegir el bucle correcto

Se sabe exactamente cuántos números se van a ingresar (`n`) → `for` con `range(n)`.

### Paso 4 — Calcular el promedio con precaución

El promedio es `suma / n`. Sin embargo, si todos los números son cero, `suma` será `0` y la división daría `0.0`, lo cual matemáticamente es válido pero el enunciado pide un mensaje especial. La condición para detectarlo es que `ceros == n` (todos fueron cero).

### Paso 5 — Escribir el programa

```python
def main():
    n = int(input("¿Cuántos números desea ingresar? "))

    positivos = 0
    negativos = 0
    ceros = 0
    suma = 0

    for i in range(n):
        num = float(input(f"Ingrese el número {i + 1}: "))
        suma = suma + num
        if num > 0:
            positivos = positivos + 1
        elif num < 0:
            negativos = negativos + 1
        else:
            ceros = ceros + 1

    print(f"Positivos: {positivos}")
    print(f"Negativos: {negativos}")
    print(f"Ceros: {ceros}")
    print(f"Suma total: {suma}")

    if ceros == n:
        print("Todos los números son cero.")
    else:
        promedio = suma / n
        print(f"Promedio: {promedio}")

main()
```

### Paso 6 — Verificar con el ejemplo del enunciado

Números ingresados: `4, -2, 0, 7, -3`

| Iteración | `num` | `suma` | `positivos` | `negativos` | `ceros` |
|---|---|---|---|---|---|
| 1 | 4 | 4 | 1 | 0 | 0 |
| 2 | -2 | 2 | 1 | 1 | 0 |
| 3 | 0 | 2 | 1 | 1 | 1 |
| 4 | 7 | 9 | 2 | 1 | 1 |
| 5 | -3 | 6 | 2 | 2 | 1 |

- `ceros (1) == n (5)`? No → se calcula el promedio
- `promedio = 6 / 5 = 1.2` ✅

### Paso 7 — Verificar el caso especial

Si `n = 3` y todos los números son `0`:
- `ceros = 3`, `suma = 0`
- `ceros == n` → `True` → `"Todos los números son cero."` ✅

### Paso 8 — Detalle sobre `i + 1` en el `input`

`range(n)` genera valores de `0` a `n - 1`. Para que el mensaje le diga al usuario "Ingrese el número 1:", "Ingrese el número 2:", etc. (en lugar de empezar en 0), se usa `i + 1` solo dentro del f-string del mensaje. El valor de `i` en sí no se usa para ningún cálculo.

---

> 💡 **Puntos clave de este ejercicio:**
> - `for` con `range(n)` cuando se conoce de antemano la cantidad de iteraciones.
> - Múltiples contadores actualizados con `if/elif/else` dentro del bucle.
> - Acumulador de suma que se actualiza **siempre**, independientemente de la rama del condicional.
> - Condicional post-bucle para manejar el caso especial del promedio.
> - `i + 1` en el mensaje para mostrar numeración desde 1 al usuario.
