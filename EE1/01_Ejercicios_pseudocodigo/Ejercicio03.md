# Ejercicio 3: Sistema de descuentos en una tienda

## Enunciado

Una tienda aplica descuentos según el **tipo de cliente** y la **cantidad de unidades** compradas. Las reglas son:

- Si el cliente es **VIP** (tipo `1`):
  - Si compra **más de 20 unidades** → 25% de descuento
  - Si compra **entre 10 y 20 unidades** (inclusive) → 15% de descuento
  - Si compra **menos de 10 unidades** → 8% de descuento
- Si el cliente es **regular** (tipo `2`):
  - Si compra **más de 20 unidades** → 10% de descuento
  - En cualquier otro caso → sin descuento (0%)
- Cualquier otro tipo de cliente → mostrar `"Tipo de cliente no válido"` y terminar

El programa debe solicitar el **tipo de cliente**, la **cantidad de unidades** y el **precio unitario**. Debe mostrar el monto original, el monto del descuento y el monto final a pagar.

Escribe el **pseudocódigo** que resuelva este problema.

---

## Resolución paso a paso

### Paso 1 — Identificar entradas, proceso y salida

- **Entradas:** tipo de cliente (entero), cantidad de unidades (entero), precio unitario (número real)
- **Proceso:** calcular el monto original, determinar el porcentaje de descuento según las reglas y calcular el monto final
- **Salida:** monto original, monto del descuento, monto final a pagar

### Paso 2 — Separar los cálculos de las decisiones

Una buena práctica al construir un algoritmo es separar claramente dos fases:

1. **Decidir** el porcentaje de descuento según las condiciones.
2. **Calcular** los montos una sola vez al final, usando ese porcentaje.

Esto evita repetir los mismos cálculos dentro de cada rama y hace el pseudocódigo más limpio.

### Paso 3 — Escribir el pseudocódigo

```
Inicio
    Leer tipo_cliente
    Leer cantidad
    Leer precio_unitario

    monto_original = cantidad * precio_unitario

    Si tipo_cliente == 1 y cantidad > 20:
        descuento_pct = 0.25
    Si no, si tipo_cliente == 1 y cantidad >= 10:
        descuento_pct = 0.15
    Si no, si tipo_cliente == 1:
        descuento_pct = 0.08
    Si no, si tipo_cliente == 2 y cantidad > 20:
        descuento_pct = 0.10
    Si no, si tipo_cliente == 2:
        descuento_pct = 0.00
    Si no:
        Mostrar "Tipo de cliente no válido"
        Fin

    monto_descuento = monto_original * descuento_pct
    monto_final = monto_original - monto_descuento

    Mostrar "Monto original: S/.", monto_original
    Mostrar "Descuento:       S/.", monto_descuento
    Mostrar "Monto a pagar:   S/.", monto_final
Fin
```

### Paso 4 — Verificar con ejemplos

**Ejemplo 1:** cliente VIP, 25 unidades, precio S/. 10
- `monto_original = 25 * 10 = 250`
- ¿`tipo_cliente == 1 y 25 > 20`? **Sí** → `descuento_pct = 0.25`
- `monto_descuento = 250 * 0.25 = 62.50`
- `monto_final = 250 - 62.50 = 187.50` ✅

**Ejemplo 2:** cliente regular, 15 unidades, precio S/. 10
- `monto_original = 15 * 10 = 150`
- ¿`tipo_cliente == 1`? No. ¿`tipo_cliente == 2 y 15 > 20`? No.
- ¿`tipo_cliente == 2`? **Sí** → `descuento_pct = 0.00`
- `monto_descuento = 0`, `monto_final = 150` ✅

**Ejemplo 3:** tipo de cliente `5`
- Ninguna condición se cumple → `"Tipo de cliente no válido"` ✅

### Paso 5 — ¿Por qué no repetimos los cálculos dentro de cada rama?

Podría haberse escrito así para el primer caso:

```
Si tipo_cliente == 1 y cantidad > 20:
    monto_descuento = monto_original * 0.25
    monto_final = monto_original - monto_descuento
    Mostrar ...
Si no, si tipo_cliente == 1 y cantidad >= 10:
    monto_descuento = monto_original * 0.15
    ...
```

Esto funciona, pero repite los mismos cálculos en cada rama. Si en el futuro cambia la fórmula del descuento, habría que modificarla en todos los lugares. Separar la decisión del cálculo es una práctica más clara y mantenible.

---

> 💡 **Puntos clave de este ejercicio:**
> - Uso de `y` (`and`) para combinar tipo de cliente y cantidad en una misma condición.
> - Separación entre la fase de **decisión** (qué porcentaje aplica) y la fase de **cálculo** (aplicar ese porcentaje).
> - Uso del `Si no` final como validación del tipo de cliente.
> - Las condiciones para el cliente VIP van de mayor a menor cantidad, para que el `Si no, si` las evalúe en el orden correcto.
