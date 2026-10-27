# Ejercicio 11: Factura con IGV y ahorro por descuento

## Enunciado

Una tienda calcula el precio de sus productos con las siguientes funciones:

1. `subtotal(precio, cantidad)`: **con retorno**. Devuelve `precio * cantidad`.

2. `aplicar_descuento(monto, porcentaje)`: **con retorno**. Devuelve el monto reducido en el porcentaje indicado. Por ejemplo, `aplicar_descuento(200, 10)` devuelve `180.0`.

3. `precio_final(precio, cantidad, porcentaje_desc=0)`: **con retorno**. Calcula el precio final con el siguiente proceso:
   - Obtiene el subtotal **llamando a `subtotal`**.
   - Aplica el descuento **llamando a `aplicar_descuento`**.
   - Agrega el IGV del 18% y devuelve el resultado redondeado a 2 decimales.

4. `mostrar_factura(producto, precio, cantidad, porcentaje_desc=0)`: **sin retorno**. Imprime:
   - El nombre del producto y el precio final.
   - El **ahorro** obtenido, calculado como la diferencia entre el precio final **sin descuento** y el precio final **con descuento**. Ambos valores se obtienen llamando a `precio_final`.

El programa principal debe pedir la cantidad de productos a registrar y, para cada uno, su nombre, precio, cantidad y porcentaje de descuento. Luego llama a `mostrar_factura`.

**Ejemplo:** producto "Lápiz", precio 50, cantidad 4, descuento 10%:
```
Producto: Lápiz
Precio final: S/. 212.4
Ahorro: S/. 23.6
```

---

## Resolución paso a paso

### Paso 1 — Dibujar la composición

```
mostrar_factura
    ├── precio_final  (se llama DOS veces)
    │       ├── subtotal
    │       └── aplicar_descuento
```

`mostrar_factura` no hace cálculos complejos: delega el cálculo a `precio_final`, que a su vez delega en `subtotal` y `aplicar_descuento`.

### Paso 2 — Escribir las funciones básicas

```python
def subtotal(precio, cantidad):
    return precio * cantidad

def aplicar_descuento(monto, porcentaje):
    return monto * (1 - porcentaje / 100)
```

### Paso 3 — Escribir `precio_final`

```python
def precio_final(precio, cantidad, porcentaje_desc=0):
    base = subtotal(precio, cantidad)
    con_descuento = aplicar_descuento(base, porcentaje_desc)
    return round(con_descuento * 1.18, 2)
```

Como `porcentaje_desc` tiene valor por defecto, la función también puede llamarse sin descuento: `precio_final(50, 4)`.

### Paso 4 — Escribir `mostrar_factura` llamando dos veces a `precio_final`

```python
def mostrar_factura(producto, precio, cantidad, porcentaje_desc=0):
    total = precio_final(precio, cantidad, porcentaje_desc)
    sin_descuento = precio_final(precio, cantidad)
    ahorro = round(sin_descuento - total, 2)

    print(f"Producto: {producto}")
    print(f"Precio final: S/. {total}")
    print(f"Ahorro: S/. {ahorro}")
```

> 💡 Se llama a `precio_final` dos veces: una con el descuento y otra sin él. Esto permite calcular el ahorro sin repetir la fórmula del IGV en `mostrar_factura`.

### Paso 5 — Programa principal

```python
def main():
    n = int(input("¿Cuántos productos desea registrar? "))

    for i in range(n):
        print(f"\n--- Producto {i + 1} ---")
        nombre = input("Nombre: ")
        precio = float(input("Precio unitario (S/.): "))
        cantidad = int(input("Cantidad: "))
        descuento = float(input("Descuento (%): "))

        mostrar_factura(nombre, precio, cantidad, descuento)

main()
```

### Paso 6 — Verificar el ejemplo

**`precio_final(50, 4, 10)`:**
1. `subtotal(50, 4)` → `200`
2. `aplicar_descuento(200, 10)` → `200 * (1 - 0.10)` → `180.0`
3. `180.0 * 1.18` → `212.4` → `round(212.4, 2)` → `212.4`

**`precio_final(50, 4)`** (sin descuento):
1. `subtotal(50, 4)` → `200`
2. `aplicar_descuento(200, 0)` → `200.0`
3. `200.0 * 1.18` → `236.0`

**Ahorro:** `236.0 - 212.4` → `23.6` ✅

### Paso 7 — Puntos a revisar

**¿Por qué `aplicar_descuento` se llama con `porcentaje_desc=0` cuando no hay descuento?**
Porque `aplicar_descuento(monto, 0)` devuelve el mismo monto (`1 - 0/100 = 1`). Así la misma función sirve con o sin descuento.

**¿Por qué no se calcula el ahorro como `200 * 0.10 * 1.18`?**
Podría hacerse, pero entonces `mostrar_factura` repetiría la lógica de cálculo. Llamar a `precio_final` garantiza que el ahorro siempre use la misma fórmula que el precio final. Si el IGV cambiara, solo habría que modificar `precio_final`.

**¿Por qué `mostrar_factura` no devuelve el ahorro?**
Porque su tarea es mostrar la factura. Si el ahorro se necesitara para otra operación, se podría crear una función con retorno que lo calcule.

---

> 💡 **Puntos clave de este ejercicio:**
> - Composición de tres niveles: `mostrar_factura` → `precio_final` → `subtotal` / `aplicar_descuento`.
> - Una misma función (`precio_final`) llamada dos veces con argumentos distintos.
> - Parámetros por defecto que permiten llamadas con y sin descuento.
> - Función sin retorno que orquesta cálculos hechos por funciones con retorno.
> - `round()` para el resultado final.
