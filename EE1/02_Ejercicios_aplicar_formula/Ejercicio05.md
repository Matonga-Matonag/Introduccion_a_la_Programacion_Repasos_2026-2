# Ejercicio 5: Valor futuro de una inversión con aportes mensuales

## Enunciado

Una persona desea invertir en un fondo de ahorro. Cada mes realiza un **aporte fijo** y además ya cuenta con un **capital inicial** depositado. El fondo ofrece una **tasa de interés efectiva anual (TEA)**, que debe convertirse a tasa mensual para los cálculos.

La tasa de interés efectiva mensual (TEM) se obtiene así:

```
TEM = (1 + TEA) ^ (1/12) - 1
```

El valor futuro del capital inicial después de `n` meses es:

```
VF_capital = capital_inicial * (1 + TEM) ^ n
```

El valor futuro de los aportes mensuales fijos después de `n` meses es:

```
VF_aportes = aporte * ((1 + TEM) ^ n - 1) / TEM
```

El valor futuro total es:

```
VF_total = VF_capital + VF_aportes
```

Implementa un programa en Python que solicite al usuario el **capital inicial**, el **aporte mensual fijo**, la **TEA** (como porcentaje, por ejemplo `6` para 6%) y el **número de meses**, y muestre:

- La TEM calculada
- El valor futuro del capital inicial
- El valor futuro de los aportes
- El valor futuro total acumulado

---

## Resolución paso a paso

### Paso 1 — Identificar entradas, proceso y salida

- **Entradas:** capital inicial, aporte mensual, TEA en porcentaje, número de meses
- **Proceso:** convertir TEA a decimal y calcular TEM, luego calcular cada componente del valor futuro
- **Salida:** TEM, VF del capital, VF de los aportes, VF total

### Paso 2 — Convertir la TEA de porcentaje a decimal

Al igual que en el ejercicio anterior, el usuario ingresa la tasa como porcentaje:

```
TEA = TEA_pct / 100
```

### Paso 3 — Calcular la TEM

```
TEM = (1 + TEA) ** (1/12) - 1
```

> ⚠️ En Python, `1/12` es una división que devuelve un `float` (`0.0833...`), por lo que la potencia funciona correctamente.

### Paso 4 — Identificar variables intermedias útiles

La expresión `(1 + TEM) ** n` aparece en las dos fórmulas de valor futuro. Se puede guardar en una variable `factor` para no repetirla.

### Paso 5 — Escribir el programa

```python
def main():
    capital_inicial = float(input("Ingrese el capital inicial (S/.): "))
    aporte = float(input("Ingrese el aporte mensual fijo (S/.): "))
    TEA_pct = float(input("Ingrese la tasa de interés anual (%): "))
    n = int(input("Ingrese el número de meses: "))

    TEA = TEA_pct / 100
    TEM = (1 + TEA) ** (1 / 12) - 1

    factor = (1 + TEM) ** n

    VF_capital = capital_inicial * factor
    VF_aportes = aporte * (factor - 1) / TEM
    VF_total = VF_capital + VF_aportes

    print(f"TEM calculada:                {TEM}")
    print(f"Valor futuro del capital:     S/. {VF_capital}")
    print(f"Valor futuro de los aportes:  S/. {VF_aportes}")
    print(f"Valor futuro total:           S/. {VF_total}")

main()
```

### Paso 6 — Verificar con un ejemplo manual

Supongamos:
- `capital_inicial = 5000`, `aporte = 200`, `TEA_pct = 6` → `TEA = 0.06`, `n = 12`

Paso a paso:
- `TEM = (1 + 0.06) ** (1/12) - 1 = (1.06) ** 0.0833 - 1 ≈ 0.004868`
- `factor = (1 + 0.004868) ** 12 ≈ 1.06`
- `VF_capital = 5000 * 1.06 = 5300`
- `VF_aportes = 200 * (1.06 - 1) / 0.004868 = 200 * 0.06 / 0.004868 ≈ 2464.75`
- `VF_total ≈ 5300 + 2464.75 = 7764.75` ✅

### Paso 7 — Puntos a revisar en el código

**¿Por qué `n` es `int` y los demás son `float`?**
El número de meses es siempre entero. Los montos y tasas pueden tener decimales.

**¿Qué pasa si `aporte = 0`?**
`VF_aportes = 0`, lo que es correcto matemáticamente: si no hay aportes, solo crece el capital inicial.

**¿Por qué se almacena `factor` en una variable?**
Porque `(1 + TEM) ** n` se usa dos veces. Guardarlo evita recalcularlo y hace el código más legible.

---

> 💡 **Puntos clave de este ejercicio:**
> - Conversión de tipos con `float()` e `int()`.
> - Operador de potencia `**` con exponente fraccionario (`1/12`).
> - Variables intermedias para simplificar expresiones que se repiten.
> - F-strings para mostrar múltiples resultados con etiquetas claras.
