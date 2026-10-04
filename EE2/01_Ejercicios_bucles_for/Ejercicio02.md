# Ejercicio 2: Crecimiento de capital mes a mes

## Enunciado

Un banco ofrece una cuenta de ahorros con una tasa de interés mensual fija. Implementa un programa que solicite al usuario:

- El **capital inicial** (en soles)
- La **tasa de interés mensual** (como porcentaje, por ejemplo `3` para 3%)
- El **número de meses** a simular
- Un **umbral** de capital (en soles)

El programa debe imprimir, mes a mes, el capital acumulado al final de cada mes. Si en algún mes el capital **supera el umbral por primera vez**, debe imprimir además el mensaje `"*** ¡Umbral superado! ***"` junto a ese mes.

Al finalizar, debe mostrar el capital total acumulado al término de todos los meses.

**Ejemplo con capital = 1000, tasa = 5%, meses = 4, umbral = 1100:**
```
Mes 1: S/. 1050.0
Mes 2: S/. 1102.5
*** ¡Umbral superado! ***
Mes 3: S/. 1157.625
Mes 4: S/. 1215.50625
Capital final: S/. 1215.50625
```

---

## Resolución paso a paso

### Paso 1 — Identificar entradas, proceso y salida

- **Entradas:** capital inicial, tasa mensual (%), número de meses, umbral
- **Proceso:** en cada mes, calcular el nuevo capital aplicando la tasa; verificar si se superó el umbral
- **Salida:** capital de cada mes, aviso cuando se supera el umbral, capital final

### Paso 2 — Convertir la tasa a decimal

El usuario ingresa la tasa como porcentaje. Para aplicarla como multiplicador:

```python
tasa = tasa_pct / 100
capital_nuevo = capital * (1 + tasa)
```

### Paso 3 — Manejar el aviso del umbral

El aviso debe mostrarse **solo la primera vez** que se supera el umbral, no en todos los meses siguientes. Para eso se usa una variable booleana `umbral_superado` que empieza en `False` y se pone en `True` en cuanto se detecta la primera superación.

```python
umbral_superado = False
# ...
if capital > umbral and not umbral_superado:
    print("*** ¡Umbral superado! ***")
    umbral_superado = True
```

### Paso 4 — Elegir el bucle correcto

Se sabe exactamente cuántos meses simular → `for` con `range(1, meses + 1)`.

### Paso 5 — Escribir el programa

```python
def main():
    capital = float(input("Ingrese el capital inicial (S/.): "))
    tasa_pct = float(input("Ingrese la tasa de interés mensual (%): "))
    meses = int(input("Ingrese el número de meses: "))
    umbral = float(input("Ingrese el umbral de capital (S/.): "))

    tasa = tasa_pct / 100
    umbral_superado = False

    for mes in range(1, meses + 1):
        capital = capital * (1 + tasa)
        print(f"Mes {mes}: S/. {capital}")
        if capital > umbral and not umbral_superado:
            print("*** ¡Umbral superado! ***")
            umbral_superado = True

    print(f"Capital final: S/. {capital}")

main()
```

### Paso 6 — Verificar con el ejemplo del enunciado

- `capital = 1000`, `tasa = 0.05`, `meses = 4`, `umbral = 1100`, `umbral_superado = False`

| Mes | Capital | ¿Supera umbral? | `umbral_superado` |
|---|---|---|---|
| 1 | `1000 * 1.05 = 1050.0` | No | `False` |
| 2 | `1050 * 1.05 = 1102.5` | Sí (primera vez) → aviso | `True` |
| 3 | `1102.5 * 1.05 = 1157.625` | Sí, pero ya fue avisado | `True` |
| 4 | `1157.625 * 1.05 = 1215.506` | Sí, pero ya fue avisado | `True` |

Salida: coincide con el ejemplo ✅

### Paso 7 — Puntos a revisar en el código

**¿Por qué `capital` se actualiza directamente (`capital = capital * ...`) en lugar de usar una variable nueva?**
Porque en cada mes el nuevo capital es la base para calcular el siguiente. Si se usara una variable separada sin actualizar `capital`, el cálculo siempre partiría del capital inicial.

**¿Qué pasa si el umbral nunca se supera?**
`umbral_superado` permanece en `False` y el aviso nunca se imprime. El programa termina mostrando solo el capital de cada mes y el capital final, lo cual es correcto.

---

> 💡 **Puntos clave de este ejercicio:**
> - `for` con `range(1, meses + 1)` para numerar los meses desde 1.
> - Variable booleana como bandera para disparar un aviso **solo una vez** dentro del bucle.
> - `and not umbral_superado` para evitar repetir el mensaje en iteraciones posteriores.
> - Actualización del acumulador `capital` dentro del bucle como base para el siguiente cálculo.
