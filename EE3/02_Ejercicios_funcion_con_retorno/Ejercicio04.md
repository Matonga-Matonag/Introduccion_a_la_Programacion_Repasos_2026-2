# Ejercicio 4: Depreciación de un activo

## Enunciado

Una empresa deprecia sus activos con el método de **saldo decreciente**: cada año, el valor del activo baja un porcentaje fijo sobre su valor del año anterior. La fórmula es:

```
valor = valor_inicial * (1 - tasa) ^ anios
```

Implementa una función **con retorno** llamada `calcular_depreciacion(valor_inicial, tasa_anual_pct=10, anios=1)` que devuelva el valor del activo después de `anios` años, redondeado a 2 decimales con `round()`.

El programa principal debe:
1. Pedir al usuario el valor inicial del activo, la tasa anual (%) y el número de años.
2. Mostrar el valor del activo **al final de cada año**, desde el año 1 hasta el último año ingresado.
3. Mostrar además el valor que se obtendría usando la tasa por defecto (10%) en el año 3, llamando a la función con **argumentos nombrados**: `calcular_depreciacion(valor_inicial, anios=3)`.

**Ejemplo:** activo de S/. 5000, tasa 10%, 3 años:
```
Año 1: S/. 4500.0
Año 2: S/. 4050.0
Año 3: S/. 3645.0
```

---

## Resolución paso a paso

### Paso 1 — Convertir la tasa a decimal dentro de la función

El parámetro `tasa_anual_pct` se recibe en porcentaje (como `10`). Para usarlo en la fórmula se divide entre 100:

```python
tasa = tasa_anual_pct / 100
```

### Paso 2 — Aplicar la fórmula con `**`

```python
valor = valor_inicial * (1 - tasa) ** anios
```

> ⚠️ El `**` tiene mayor precedencia que la multiplicación, por lo que `(1 - tasa) ** anios` se calcula primero. Los paréntesis alrededor de `1 - tasa` son obligatorios.

### Paso 3 — Devolver el valor redondeado

```python
return round(valor, 2)
```

### Paso 4 — Escribir la función

```python
def calcular_depreciacion(valor_inicial, tasa_anual_pct=10, anios=1):
    tasa = tasa_anual_pct / 100
    valor = valor_inicial * (1 - tasa) ** anios
    return round(valor, 2)
```

### Paso 5 — Programa principal

```python
def main():
    valor_inicial = float(input("Ingrese el valor inicial del activo (S/.): "))
    tasa = float(input("Ingrese la tasa anual de depreciación (%): "))
    anios = int(input("Ingrese el número de años: "))

    for anio in range(1, anios + 1):
        valor = calcular_depreciacion(valor_inicial, tasa, anio)
        print(f"Año {anio}: S/. {valor}")

    valor_defecto = calcular_depreciacion(valor_inicial, anios=3)
    print(f"Valor en el año 3 con la tasa por defecto (10%): S/. {valor_defecto}")

main()
```

### Paso 6 — Verificar con el ejemplo

Con `valor_inicial = 5000`, `tasa = 10`:

| Año (`anios`) | Cálculo | Resultado |
|---|---|---|
| 1 | `5000 * 0.9 ** 1` | `4500.0` |
| 2 | `5000 * 0.9 ** 2` | `4050.0` |
| 3 | `5000 * 0.9 ** 3` | `3645.0` |

Coincide con el ejemplo del enunciado ✅

### Paso 7 — Puntos a revisar

**¿Por qué la función recibe la tasa en porcentaje y no en decimal?**
Porque así es más natural para el usuario (`10` en lugar de `0.1`). La conversión se hace dentro de la función, en un solo lugar.

**¿Por qué se usa `anios=3` como argumento nombrado?**
Porque `tasa_anual_pct` tiene valor por defecto. Al nombrar `anios`, se omite la tasa sin tener que escribir su valor y la llamada queda clara.

**¿Por qué la función devuelve el valor en lugar de imprimirlo?**
Porque el programa principal lo necesita para mostrarlo en el formato del año y para reutilizarlo en el bucle. Una función con retorno es más flexible.

---

> 💡 **Puntos clave de este ejercicio:**
> - Función con retorno que calcula y entrega un valor con `return`.
> - Operador `**` con paréntesis para controlar el orden de la operación.
> - `round(valor, 2)` para redondear el resultado.
> - Parámetros por defecto y argumentos nombrados en la llamada.
> - Llamadas repetidas a la función dentro de un `for`.
