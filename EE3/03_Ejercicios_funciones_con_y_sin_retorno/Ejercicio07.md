# Ejercicio 7: Cajero automático con comisión

## Enunciado

Un cajero automático cobra una comisión por cada retiro, según el monto solicitado:

| Monto retirado | Comisión |
|---|---|
| Hasta S/. 1000 (inclusive) | 2% del monto |
| Más de S/. 1000 y hasta S/. 5000 (inclusive) | 1.5% del monto |
| Más de S/. 5000 | 1% del monto + S/. 5.00 fijos |

Implementa:

1. `calcular_comision(monto)`: **con retorno**. Devuelve la comisión redondeada a 2 decimales.
2. `mostrar_recibo(monto, comision)`: **sin retorno**. Imprime un recibo con el monto retirado, la comisión y el total a debitar (monto + comisión), todo redondeado a 2 decimales. El recibo debe estar delimitado por una línea de 30 signos `=` al inicio y al final.

El programa principal debe pedir montos en un `while` con centinela `0`:
- Si el monto es negativo, mostrar `"Monto no válido."`.
- Si el monto es positivo, calcular la comisión con `calcular_comision`, y mostrar el recibo con `mostrar_recibo`.
- Termina cuando el usuario ingresa `0`.

**Ejemplo:** retiro de S/. 3000:
```
==============================
Monto retirado:   S/. 3000.0
Comisión:         S/. 45.0
Total a debitar:  S/. 3045.0
==============================
```

---

## Resolución paso a paso

### Paso 1 — Identificar qué es con retorno y qué es sin retorno

| Función | Tipo | Motivo |
|---|---|---|
| `calcular_comision(monto)` | Con retorno | El resultado se usa para mostrar el recibo y calcular el total |
| `mostrar_recibo(monto, comision)` | Sin retorno | Solo imprime información |

Separar el cálculo de la presentación permite cambiar la forma del recibo sin tocar la lógica de la comisión.

### Paso 2 — Escribir `calcular_comision` con `if/elif/else`

```python
def calcular_comision(monto):
    if monto <= 1000:
        comision = monto * 0.02
    elif monto <= 5000:
        comision = monto * 0.015
    else:
        comision = monto * 0.01 + 5

    return round(comision, 2)
```

> ⚠️ Los tramos se escriben con `<=` y `elif`. Como el primer `if` ya cubre todo lo que es menor o igual a 1000, el `elif` solo se evalúa cuando el monto es mayor a 1000.

### Paso 3 — Escribir `mostrar_recibo` sin retorno

```python
def mostrar_recibo(monto, comision):
    total = monto + comision
    print("=" * 30)
    print(f"Monto retirado:   S/. {round(monto, 2)}")
    print(f"Comisión:         S/. {round(comision, 2)}")
    print(f"Total a debitar:  S/. {round(total, 2)}")
    print("=" * 30)
```

> 💡 `round(total, 2)` se usa porque la suma de decimales puede producir resultados como `3045.0000000001`.

### Paso 4 — Programa principal con centinela

El patrón es el mismo que en el examen 2: leer antes del `while` y al final de cada iteración.

```python
def main():
    monto = float(input("Ingrese el monto a retirar (0 para salir): "))

    while monto != 0:
        if monto < 0:
            print("Monto no válido.")
        else:
            comision = calcular_comision(monto)
            mostrar_recibo(monto, comision)

        monto = float(input("Ingrese el monto a retirar (0 para salir): "))

    print("Gracias por usar el cajero.")

main()
```

### Paso 5 — Verificar los casos

| Monto | Tramo | Cálculo | Comisión | Total a debitar |
|---|---|---|---|---|
| 800 | Hasta 1000 | `800 * 0.02` | `16.0` | `816.0` |
| 3000 | Entre 1000 y 5000 | `3000 * 0.015` | `45.0` | `3045.0` |
| 10000 | Más de 5000 | `10000 * 0.01 + 5` | `105.0` | `10105.0` |
| -50 | — | — | — | Se muestra `"Monto no válido."` |
| 0 | — | — | — | Termina el programa |

### Paso 6 — Puntos a revisar

**¿Por qué `calcular_comision` no imprime nada?**
Porque su única tarea es calcular. Si imprimiera el valor, no se podría usar para calcular el total sin mostrar también ese mensaje.

**¿Por qué `mostrar_recibo` recibe la comisión como parámetro en vez de calcularla?**
Así cada función hace una sola cosa. `mostrar_recibo` se ocupa de mostrar, y la comisión la calcula la otra función. Esto además permite probar `mostrar_recibo` con cualquier comisión.

**¿Qué pasaría si `monto` fuera 0 dentro del `while`?**
No pasaría nada, porque el `while` termina antes de procesarlo: la condición `monto != 0` es falsa.

---

> 💡 **Puntos clave de este ejercicio:**
> - Diferencia entre función con retorno (calcular) y función sin retorno (mostrar).
> - `if/elif/else` con tramos de valores.
> - Función con retorno usada dentro del programa principal para alimentar a una función sin retorno.
> - `while` con centinela y validación de montos negativos.
> - `round()` para evitar errores de precisión en decimales.
