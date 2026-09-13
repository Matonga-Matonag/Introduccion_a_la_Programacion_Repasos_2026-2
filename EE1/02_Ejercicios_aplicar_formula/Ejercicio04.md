# Ejercicio 4: Cuota mensual de un préstamo

## Enunciado

Cuando una persona solicita un préstamo en un banco, la cuota mensual fija que debe pagar se calcula con la siguiente fórmula de **amortización francesa**:

```
C = P * (TEM * (1 + TEM)^n) / ((1 + TEM)^n - 1)
```

Donde:
- `C` = cuota mensual a pagar (en soles)
- `P` = monto del préstamo (en soles)
- `TEM` = tasa de interés efectiva mensual (en decimal; por ejemplo, 2% → 0.02)
- `n` = número de cuotas (meses)

Implementa un programa en Python que solicite al usuario el monto del préstamo, la tasa de interés mensual (como porcentaje, por ejemplo `2` para 2%) y el número de cuotas, y que muestre:

- La cuota mensual
- El total a pagar al finalizar el préstamo
- El total de intereses pagados

---

## Resolución paso a paso

### Paso 1 — Identificar entradas, proceso y salida

- **Entradas:** monto del préstamo (`P`), tasa de interés mensual en porcentaje (`TEM_pct`), número de cuotas (`n`)
- **Proceso:** convertir la tasa a decimal, aplicar la fórmula y calcular totales
- **Salida:** cuota mensual (`C`), total a pagar, total de intereses

### Paso 2 — Convertir la tasa de porcentaje a decimal

El usuario ingresará la tasa como porcentaje (por ejemplo, `2`), pero la fórmula requiere el valor en decimal (es decir, `0.02`). La conversión es:

```
TEM = TEM_pct / 100
```

### Paso 3 — Identificar las operaciones necesarias

La fórmula requiere:
- Potenciación: `(1 + TEM) ** n`
- Multiplicación y división entre esos resultados intermedios

Conviene guardar `(1 + TEM) ** n` en una variable intermedia para no calcularlo dos veces.

### Paso 4 — Escribir el programa

```python
def main():
    P = float(input("Ingrese el monto del préstamo (S/.): "))
    TEM_pct = float(input("Ingrese la tasa de interés mensual (%): "))
    n = int(input("Ingrese el número de cuotas (meses): "))

    TEM = TEM_pct / 100

    factor = (1 + TEM) ** n
    C = P * (TEM * factor) / (factor - 1)

    total_pagar = C * n
    total_intereses = total_pagar - P

    print(f"Cuota mensual:        S/. {C}")
    print(f"Total a pagar:        S/. {total_pagar}")
    print(f"Total en intereses:   S/. {total_intereses}")

main()
```

### Paso 5 — Verificar con un ejemplo manual

Supongamos:
- `P = 10000`, `TEM_pct = 2` → `TEM = 0.02`, `n = 12`

Calculamos paso a paso:
- `factor = (1 + 0.02) ** 12 = (1.02) ** 12 ≈ 1.2682`
- `C = 10000 * (0.02 * 1.2682) / (1.2682 - 1)`
- `C = 10000 * 0.025364 / 0.2682`
- `C ≈ 10000 * 0.09456 ≈ 945.60`
- `total_pagar = 945.60 * 12 ≈ 11347.20`
- `total_intereses = 11347.20 - 10000 = 1347.20`

Ejecutando el programa con esos valores se obtiene el mismo resultado ✅

### Paso 6 — Puntos a revisar en el código

**¿Por qué `n` se lee con `int()` y no con `float()`?**
El número de cuotas es siempre un entero (no tiene sentido pagar 12.5 meses), por lo que se usa `int(input(...))`.

**¿Por qué se guarda `(1 + TEM) ** n` en `factor`?**
Esa expresión aparece dos veces en la fórmula. Guardarla en una variable evita calcularla dos veces y hace el código más legible.

**¿Por qué se usa `float()` para `P` y `TEM_pct`?**
Porque `input()` siempre devuelve un `str`, y se necesita operar matemáticamente con esos valores.

---

> 💡 **Puntos clave de este ejercicio:**
> - Conversión de tipos: `int(input(...))` y `float(input(...))`.
> - Uso del operador de potencia `**`.
> - Uso de variables intermedias para simplificar fórmulas complejas.
> - Uso de f-strings para mostrar resultados con texto y variables en la misma línea.
