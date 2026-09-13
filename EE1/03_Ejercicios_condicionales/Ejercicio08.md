# Ejercicio 8: Sistema de tarifas de estacionamiento

## Enunciado

Un estacionamiento cobra según las siguientes reglas:

- Si el tiempo de estacionamiento es **menor o igual a 30 minutos** → **gratis**
- Si el tiempo es **mayor a 30 minutos y hasta 2 horas** → tarifa fija de **S/. 5.00**
- Si el tiempo supera las **2 horas**:
  - Se cobra la tarifa base de **S/. 5.00** por las primeras 2 horas
  - Más **S/. 3.00 por cada hora adicional o fracción** a partir de la tercera hora

Adicionalmente, si el vehículo es una **moto** (el usuario lo indica con `"s"` para sí o `"n"` para no), se aplica un **descuento del 30%** sobre el monto total calculado.

El programa debe solicitar el tiempo en **horas** y **minutos** por separado, y si el vehículo es moto. Debe mostrar el monto a pagar.

---

## Resolución paso a paso

### Paso 1 — Identificar entradas, proceso y salida

- **Entradas:** horas (int), minutos (int), es moto (`str`: `"s"` o `"n"`)
- **Proceso:** convertir todo a minutos, determinar el tramo tarifario y calcular el costo; aplicar descuento si corresponde
- **Salida:** monto a pagar

### Paso 2 — Convertir el tiempo a una sola unidad

Trabajar con horas y minutos por separado complica las comparaciones. Es más sencillo convertir todo a **minutos totales**:

```
total_minutos = horas * 60 + minutos
```

### Paso 3 — Calcular las horas adicionales con fracción

Para el tercer tramo (más de 2 horas), se necesita saber cuántas horas adicionales hay a partir de la tercera, contando las fracciones como hora completa.

Los minutos que exceden las primeras 2 horas son:
```
minutos_extra = total_minutos - 120
```

Para convertir esos minutos extra en horas completas **redondeando hacia arriba** (cada fracción cuenta como hora completa), se puede usar división entera y el operador módulo:

```
horas_extra = minutos_extra // 60
fraccion = minutos_extra % 60
```

Si `fraccion > 0`, hay una fracción de hora que también se cobra, así que se suma 1:
```
si fraccion > 0:
    horas_extra = horas_extra + 1
```

### Paso 4 — Escribir el programa

```python
def main():
    horas = int(input("Ingrese las horas de estacionamiento: "))
    minutos = int(input("Ingrese los minutos adicionales: "))
    es_moto = input("¿El vehículo es una moto? (s/n): ")

    total_minutos = horas * 60 + minutos

    if total_minutos <= 30:
        monto = 0
        print("El estacionamiento es gratuito")
    elif total_minutos <= 120:
        monto = 5.00
    else:
        minutos_extra = total_minutos - 120
        horas_extra = minutos_extra // 60
        fraccion = minutos_extra % 60
        if fraccion > 0:
            horas_extra = horas_extra + 1
        monto = 5.00 + horas_extra * 3.00

    if total_minutos > 30:
        if es_moto == "s":
            descuento = monto * 0.30
            monto = monto - descuento
            print(f"Descuento de moto aplicado: S/. {descuento}")
        print(f"Monto a pagar: S/. {monto}")

main()
```

### Paso 5 — Verificar con ejemplos

**Ejemplo 1:** `horas = 0`, `minutos = 20`, `es_moto = "n"`
- `total_minutos = 20`
- ¿`20 <= 30`? **Sí** → `monto = 0`, salida: `"El estacionamiento es gratuito"` ✅

**Ejemplo 2:** `horas = 1`, `minutos = 30`, `es_moto = "n"`
- `total_minutos = 90`
- ¿`90 <= 30`? No. ¿`90 <= 120`? **Sí** → `monto = 5.00`
- No es moto → salida: `"Monto a pagar: S/. 5.0"` ✅

**Ejemplo 3:** `horas = 3`, `minutos = 45`, `es_moto = "s"`
- `total_minutos = 225`
- ¿`225 <= 30`? No. ¿`225 <= 120`? No → tramo extra
- `minutos_extra = 225 - 120 = 105`
- `horas_extra = 105 // 60 = 1`, `fraccion = 105 % 60 = 45`
- `fraccion > 0` → `horas_extra = 1 + 1 = 2`
- `monto = 5.00 + 2 * 3.00 = 11.00`
- Es moto → `descuento = 11.00 * 0.30 = 3.30`, `monto = 11.00 - 3.30 = 7.70`
- Salida: `"Descuento de moto aplicado: S/. 3.3"` / `"Monto a pagar: S/. 7.7"` ✅

### Paso 6 — Puntos a revisar en el código

**¿Por qué se usa `//` y `%` para las horas extra?**
- `//` (división entera) da el número de horas completas.
- `%` (módulo) da los minutos sobrantes. Si ese resto es mayor a 0, hay una fracción que se cobra como hora completa.

**¿Por qué el bloque del descuento y el `print` del monto están dentro de `if total_minutos > 30`?**
Si el estacionamiento es gratuito, ya se mostró el mensaje correspondiente y no corresponde mostrar `"Monto a pagar: S/. 0"`. Este `if` evita ese caso.

---

> 💡 **Puntos clave de este ejercicio:**
> - Conversión de unidades como paso previo a las comparaciones.
> - Uso de `//` y `%` para descomponer una cantidad en partes enteras y resto.
> - Condicional anidado dentro de una rama para aplicar el descuento de moto.
> - Comparación de string con `==` para interpretar la respuesta del usuario.
