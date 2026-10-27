# Ejercicio 9: Reporte de ventas semanal

## Enunciado

Una tienda registra sus ventas durante 7 días. Cada día se ingresan las **unidades vendidas** y el **precio unitario** del producto (que es el mismo todos los días). Implementa las siguientes funciones:

1. `calcular_venta_diaria(unidades, precio_unitario)`: **con retorno**. Calcula el monto bruto (`unidades * precio_unitario`) y aplica un descuento por volumen:
   - Si se vendieron **50 unidades o más**: 15% de descuento.
   - Si se vendieron **entre 10 y 49 unidades**: 10% de descuento.
   - Si se vendieron **menos de 10 unidades**: sin descuento.

   Devuelve el monto final redondeado a 2 decimales.

2. `es_fin_semana(dia)`: **con retorno booleano**. Recibe el número de día (1 a 7) y devuelve `True` si es sábado (6) o domingo (7).

3. `mostrar_linea_dia(dia, monto, fin_semana)`: **sin retorno**. Imprime una línea con el día y el monto. Si `fin_semana` es `True`, agrega al final el texto `"(fin de semana)"`.

4. `mostrar_resumen(total, dias)`: **sin retorno**. Imprime el total de ventas de la semana y el promedio diario redondeado a 2 decimales.

El programa principal debe usar un `for` de 1 a 7 y:
- Pedir las unidades vendidas en ese día (no negativas, con validación con `while`).
- Calcular el monto con `calcular_venta_diaria`.
- Mostrar la línea del día con `mostrar_linea_dia`.
- Acumular el total de la semana.

Al final, llamar a `mostrar_resumen`.

**Ejemplo de salida parcial con precio = 20, día 1 con 10 unidades y día 6 con 20 unidades:**
```
Día 1: S/. 180.0
Día 6: S/. 360.0 (fin de semana)
```
> Día 1: 10 unidades → bruto 200 → 10% de descuento → 180. Día 6: 20 unidades → bruto 400 → 10% de descuento → 360.

---

## Resolución paso a paso

### Paso 1 — Identificar las funciones y su tipo

| Función | Tipo | Responsabilidad |
|---|---|---|
| `calcular_venta_diaria` | Con retorno | Calcular el monto con descuento |
| `es_fin_semana` | Con retorno booleano | Responder si un día es fin de semana |
| `mostrar_linea_dia` | Sin retorno | Imprimir la línea del día |
| `mostrar_resumen` | Sin retorno | Imprimir el total y el promedio |

### Paso 2 — Descuento por volumen con `if/elif/else`

```python
def calcular_venta_diaria(unidades, precio_unitario):
    monto = unidades * precio_unitario

    if unidades >= 50:
        monto = monto * 0.85
    elif unidades >= 10:
        monto = monto * 0.90

    return round(monto, 2)
```

### Paso 3 — Función booleana

```python
def es_fin_semana(dia):
    return dia == 6 or dia == 7
```

### Paso 4 — Función sin retorno que usa otra función

```python
def mostrar_linea_dia(dia, monto, fin_semana):
    if fin_semana:
        print(f"Día {dia}: S/. {monto} (fin de semana)")
    else:
        print(f"Día {dia}: S/. {monto}")
```

En el programa principal, el valor de `fin_semana` se obtiene llamando a `es_fin_semana(dia)`.

### Paso 5 — Función sin retorno con cálculo derivado

```python
def mostrar_resumen(total, dias):
    promedio = total / dias
    print(f"Total de la semana: S/. {round(total, 2)}")
    print(f"Promedio diario:    S/. {round(promedio, 2)}")
```

### Paso 6 — Programa principal

```python
def main():
    precio = float(input("Ingrese el precio unitario del producto (S/.): "))
    total = 0

    for dia in range(1, 8):
        unidades = int(input(f"Unidades vendidas el día {dia}: "))
        while unidades < 0:
            print("Las unidades no pueden ser negativas.")
            unidades = int(input(f"Unidades vendidas el día {dia}: "))

        monto = calcular_venta_diaria(unidades, precio)
        total = total + monto
        mostrar_linea_dia(dia, monto, es_fin_semana(dia))

    mostrar_resumen(total, 7)

main()
```

> 💡 `mostrar_linea_dia(dia, monto, es_fin_semana(dia))` es una **llamada anidada**: primero se evalúa `es_fin_semana(dia)`, que devuelve `True` o `False`, y ese valor se pasa como argumento a `mostrar_linea_dia`.

### Paso 7 — Verificar el cálculo con precio = 20

| Unidades | Bruto (`unidades * 20`) | Descuento | Monto final |
|---|---|---|---|
| 5 | 100 | Ninguno (menos de 10) | `100.0` |
| 10 | 200 | 10% | `180.0` |
| 50 | 1000 | 15% | `850.0` |

Para el día 6 (sábado), con 10 unidades: `mostrar_linea_dia(6, 180.0, True)` imprime `Día 6: S/. 180.0 (fin de semana)` ✅

### Paso 8 — Puntos a revisar

**¿Por qué el descuento se aplica con `elif` y no con dos `if` seguidos?**
Porque un monto no puede recibir dos descuentos por volumen a la vez. Como las condiciones son excluyentes, `elif` deja claro que solo uno se aplica.

**¿Por qué `es_fin_semana` se llama dentro de la llamada a `mostrar_linea_dia`?**
Porque `mostrar_linea_dia` no debe conocer las reglas del calendario. Esa lógica queda en su propia función, y `mostrar_linea_dia` solo recibe el resultado.

**¿Qué pasaría si `total` no se inicializara en `0` antes del `for`?**
Python daría un error al intentar sumarle `monto` a una variable que no existe.

---

> 💡 **Puntos clave de este ejercicio:**
> - Función con retorno que aplica un descuento con `if/elif`.
> - Función booleana con `or`, usada como argumento de otra función.
> - Función sin retorno que recibe un booleano para decidir qué imprimir.
> - Llamadas anidadas: el resultado de una función es el argumento de otra.
> - Acumulador (`total`) actualizado dentro de un `for`.
