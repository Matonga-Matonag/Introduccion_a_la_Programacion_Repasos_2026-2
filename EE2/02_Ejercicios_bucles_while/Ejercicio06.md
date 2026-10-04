# Pregunta 2 — Ejercicio 3: Suscripción a servicio de streaming

## Enunciado

Una plataforma de streaming ofrece tres planes de suscripción:

| Plan | Precio mensual |
|---|---|
| 1 — Básico | S/. 30.00 |
| 2 — Estándar | S/. 50.00 |
| 3 — Premium | S/. 80.00 |

Implementa un programa en Python que:

1. Solicite al usuario que elija un plan (1, 2 o 3). Si ingresa una opción inválida, volver a pedirla **hasta que ingrese una válida**.
2. Solicite cuántos **meses** desea suscribirse.
3. Calcule el costo total, aplicando un **20% de descuento** si la suscripción es de **12 meses o más**.
4. Muestre el plan elegido, el precio mensual, el total sin descuento, el descuento aplicado (si hay) y el total final.

---

## Resolución paso a paso

### Paso 1 — Identificar entradas, proceso y salida

- **Entradas:** opción de plan (1, 2 o 3), número de meses
- **Proceso:** validar el plan con un `while`; asignar el precio mensual según el plan; calcular el total y aplicar descuento si corresponde
- **Salida:** resumen de la suscripción con todos los montos

### Paso 2 — Validar el plan con `while`

El plan es inválido si no es 1, 2 ni 3. La condición para seguir pidiendo es que la opción ingresada **no sea ninguna de las válidas**:

```python
while plan != 1 and plan != 2 and plan != 3:
```

Para que el bucle arranque, `plan` debe inicializarse con un valor que no sea 1, 2 ni 3:

```python
plan = 0
```

### Paso 3 — Asignar el precio con `if/elif`

Una vez validado el plan, se asigna el precio mensual:

```python
if plan == 1:
    precio_mensual = 30.0
    nombre_plan = "Básico"
elif plan == 2:
    precio_mensual = 50.0
    nombre_plan = "Estándar"
else:
    precio_mensual = 80.0
    nombre_plan = "Premium"
```

### Paso 4 — Calcular el descuento post-bucle

```python
total_sin_descuento = precio_mensual * meses

if meses >= 12:
    descuento = total_sin_descuento * 0.20
else:
    descuento = 0.0

total_final = total_sin_descuento - descuento
```

### Paso 5 — Escribir el programa

```python
def main():
    plan = 0
    while plan != 1 and plan != 2 and plan != 3:
        plan = int(input("Elija su plan (1=Básico S/.30, 2=Estándar S/.50, 3=Premium S/.80): "))
        if plan != 1 and plan != 2 and plan != 3:
            print("Opción no válida. Intente de nuevo.")

    meses = int(input("¿Cuántos meses desea suscribirse? "))

    if plan == 1:
        precio_mensual = 30.0
        nombre_plan = "Básico"
    elif plan == 2:
        precio_mensual = 50.0
        nombre_plan = "Estándar"
    else:
        precio_mensual = 80.0
        nombre_plan = "Premium"

    total_sin_descuento = precio_mensual * meses

    if meses >= 12:
        descuento = total_sin_descuento * 0.20
    else:
        descuento = 0.0

    total_final = total_sin_descuento - descuento

    print(f"\nPlan elegido:        {nombre_plan}")
    print(f"Precio mensual:      S/. {precio_mensual}")
    print(f"Meses:               {meses}")
    print(f"Total sin descuento: S/. {total_sin_descuento}")
    if descuento > 0:
        print(f"Descuento (20%):     S/. {descuento}")
    print(f"Total a pagar:       S/. {total_final}")

main()
```

### Paso 6 — Verificar con ejemplos

**Ejemplo 1:** plan inválido primero, luego plan 2, 8 meses

- Usuario ingresa `5` → inválido → pide de nuevo
- Usuario ingresa `2` → válido → sale del `while`
- `precio_mensual = 50.0`, `nombre_plan = "Estándar"`
- `total_sin_descuento = 50 * 8 = 400`
- `8 >= 12`? No → `descuento = 0`
- `total_final = 400` ✅

**Ejemplo 2:** plan 3, 12 meses

- `precio_mensual = 80.0`, `nombre_plan = "Premium"`
- `total_sin_descuento = 80 * 12 = 960`
- `12 >= 12`? Sí → `descuento = 960 * 0.20 = 192`
- `total_final = 960 - 192 = 768` ✅

### Paso 7 — Puntos a revisar en el código

**¿Por qué `plan = 0` antes del `while`?**
La condición del `while` evalúa `plan` antes de entrar. Si `plan` no tuviera valor, Python daría un error. El valor `0` garantiza que la condición sea `True` y el bucle arranque.

**¿Por qué la condición del `while` usa `and` y no `or`?**
Se quiere continuar mientras el plan **no sea 1 Y no sea 2 Y no sea 3** (ninguna de las tres opciones válidas). Si se usara `or`, el bucle continuaría incluso cuando el plan es válido (por ejemplo, con `plan = 1`: `1 != 2` es `True` → el `or` haría la condición `True` y seguiría pidiendo).

---

> 💡 **Puntos clave de este ejercicio:**
> - `while` de validación con `and` para rechazar entradas que no correspondan a ninguna opción válida.
> - Inicialización de la variable de control en un valor inválido (`0`) para garantizar que el bucle arranque.
> - `if/elif/else` post-bucle para asignar valores según la opción elegida.
> - Condicional para aplicar el descuento solo si se cumple la condición de meses.
