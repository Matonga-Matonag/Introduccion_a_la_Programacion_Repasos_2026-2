# Ejercicio 5: Simulador de caja registradora

## Enunciado

Implementa un programa en Python que simule una caja registradora. El programa debe:

1. Pedir al usuario el precio de cada producto uno por uno.
2. Continuar pidiendo precios hasta que el usuario ingrese `0` (que indica que no hay más productos).
3. Llevar la cuenta de **cuántos productos** se registraron.
4. Al finalizar, calcular el **total de la compra** y aplicar las siguientes reglas:
   - Si el total supera **S/. 100**, aplicar un **15% de descuento**.
   - Si el total supera **S/. 200**, aplicar un **25% de descuento**.
   - Si el total es **S/. 100 o menos**, no hay descuento.
5. Mostrar el total original, el descuento aplicado (si hay) y el total final a pagar.

> ⚠️ Solo se aplica **uno** de los descuentos (el mayor que corresponda), no ambos.

---

## Resolución paso a paso

### Paso 1 — Identificar entradas, proceso y salida

- **Entradas:** precios de productos (el usuario ingresa `0` para terminar)
- **Proceso:** acumular el total y contar productos mientras el precio ingresado sea distinto de `0`; luego determinar el descuento
- **Salida:** cantidad de productos, total original, descuento y total final

### Paso 2 — Elegir el bucle correcto

No se sabe cuántos productos ingresará el usuario → `while` con centinela. El valor centinela es `0`.

El patrón es: leer antes del bucle, procesar dentro, leer de nuevo al final de cada iteración.

### Paso 3 — Determinar el descuento con `if/elif/else`

Las condiciones deben evaluarse de mayor a menor para que el descuento más alto tenga prioridad:

```python
if total > 200:
    descuento_pct = 0.25
elif total > 100:
    descuento_pct = 0.15
else:
    descuento_pct = 0.0
```

### Paso 4 — Escribir el programa

```python
def main():
    total = 0.0
    num_productos = 0

    precio = float(input("Ingrese el precio del producto (0 para terminar): "))

    while precio != 0:
        total = total + precio
        num_productos = num_productos + 1
        precio = float(input("Ingrese el precio del siguiente producto (0 para terminar): "))

    print(f"\nProductos registrados: {num_productos}")
    print(f"Total original: S/. {total}")

    if total > 200:
        descuento_pct = 0.25
    elif total > 100:
        descuento_pct = 0.15
    else:
        descuento_pct = 0.0

    descuento = total * descuento_pct
    total_final = total - descuento

    if descuento_pct > 0:
        print(f"Descuento ({descuento_pct * 100}%): S/. {descuento}")
    else:
        print("Sin descuento.")

    print(f"Total a pagar: S/. {total_final}")

main()
```

### Paso 5 — Verificar con ejemplos

**Ejemplo 1:** productos de S/. 45, S/. 30, S/. 60 → total = 135

- `135 > 200`? No. `135 > 100`? Sí → `descuento_pct = 0.15`
- `descuento = 135 * 0.15 = 20.25`
- `total_final = 135 - 20.25 = 114.75` ✅

**Ejemplo 2:** productos de S/. 80, S/. 90, S/. 50 → total = 220

- `220 > 200`? Sí → `descuento_pct = 0.25`
- `descuento = 220 * 0.25 = 55`
- `total_final = 220 - 55 = 165` ✅

**Ejemplo 3:** producto de S/. 40 → total = 40

- `40 > 200`? No. `40 > 100`? No → `descuento_pct = 0.0`
- Sin descuento, `total_final = 40` ✅

**Ejemplo 4:** el usuario ingresa `0` de inmediato

- El bucle no se ejecuta, `total = 0`, `num_productos = 0`
- No hay descuento, `total_final = 0` ✅

### Paso 6 — Puntos a revisar en el código

**¿Por qué se lee `precio` antes del `while` y también al final de cada iteración?**
Porque la condición del `while` necesita evaluar `precio` antes de entrar. Si se leyera solo dentro del bucle, la primera iteración arrancaría sin saber el primer precio.

**¿Por qué las condiciones del descuento van de mayor a menor (`> 200` antes que `> 100`)?**
Si se pusiera primero `total > 100`, un total de S/. 220 entraría en esa rama y recibiría solo 15% en lugar del 25% que le corresponde. Al evaluar primero la condición más exigente, se garantiza el descuento correcto.

---

> 💡 **Puntos clave de este ejercicio:**
> - `while` con centinela: el bucle se detiene cuando el usuario ingresa un valor especial (`0`).
> - Patrón de lectura: leer antes del `while` y al final de cada iteración.
> - Acumulador de suma y contador de productos actualizados dentro del bucle.
> - Condicional post-bucle con condiciones ordenadas de mayor a menor para determinar el descuento correcto.
