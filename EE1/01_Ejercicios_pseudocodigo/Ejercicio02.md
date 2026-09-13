# Ejercicio 2: Clasificador de riesgo crediticio

## Enunciado

Un banco clasifica el riesgo crediticio de sus clientes antes de otorgar un préstamo. Para ello considera tres factores:

- **Ingresos mensuales** (en soles)
- **Deuda actual** (en soles)
- **Antigüedad laboral** (en años)

Las reglas de clasificación son:

- Si los ingresos son **mayores a S/. 5000** y la deuda es **menor a S/. 2000** y la antigüedad es **mayor o igual a 2 años** → riesgo **BAJO**
- Si los ingresos son **mayores a S/. 3000** y la deuda es **menor a S/. 5000** y la antigüedad es **mayor o igual a 1 año** → riesgo **MEDIO**
- Si los ingresos son **menores o iguales a S/. 1000** o la deuda es **mayor o igual a S/. 10000** → riesgo **MUY ALTO**
- Cualquier otro caso → riesgo **ALTO**

Escribe el **pseudocódigo** que solicite los tres datos al usuario y muestre la clasificación de riesgo correspondiente.

---

## Resolución paso a paso

### Paso 1 — Identificar entradas, proceso y salida

- **Entradas:** ingresos (número real), deuda (número real), antigüedad (número real)
- **Proceso:** evaluar las condiciones en el orden correcto para determinar la categoría de riesgo
- **Salida:** la clasificación de riesgo (`BAJO`, `MEDIO`, `ALTO` o `MUY ALTO`)

### Paso 2 — Determinar el orden de evaluación

Este es el punto más importante del ejercicio: las condiciones deben evaluarse **de la más específica (favorable) a la más general (desfavorable)**. Si se evalúa primero `MEDIO`, un cliente que califica para `BAJO` podría quedar clasificado incorrectamente.

El orden correcto es:
1. `BAJO` (condición más exigente y favorable)
2. `MEDIO`
3. `MUY ALTO` (condición de alarma, independiente de ingresos o antigüedad)
4. `ALTO` (caso por defecto)

### Paso 3 — Escribir el pseudocódigo

```
INICIO
    LEER ingresos
    LEER deuda
    LEER antiguedad

    SI ingresos > 5000 y deuda < 2000 y antiguedad >= 2:
        MOSTRAR "Riesgo: BAJO"
    SINO SI ingresos > 3000 y deuda < 5000 y antiguedad >= 1:
        MOSTRAR "Riesgo: MEDIO"
    SINO SI ingresos <= 1000 o deuda >= 10000:
        MOSTRAR "Riesgo: MUY ALTO"
    SINO:
        MOSTRAR "Riesgo: ALTO"
FIN
```

### Paso 4 — Verificar con ejemplos

**Ejemplo 1:**
- `ingresos = 6000`, `deuda = 1500`, `antiguedad = 3`
- ¿`6000 > 5000 y 1500 < 2000 y 3 >= 2`? **Sí** → `"Riesgo: BAJO"` ✅

**Ejemplo 2:**
- `ingresos = 4000`, `deuda = 3000`, `antiguedad = 1`
- ¿Cumple `BAJO`? `4000 > 5000` → **No**
- ¿`4000 > 3000 y 3000 < 5000 y 1 >= 1`? **Sí** → `"Riesgo: MEDIO"` ✅

**Ejemplo 3:**
- `ingresos = 800`, `deuda = 3000`, `antiguedad = 5`
- ¿Cumple `BAJO`? No. ¿Cumple `MEDIO`? `800 > 3000` → No.
- ¿`800 <= 1000 o 3000 >= 10000`? `800 <= 1000` → **Sí** → `"Riesgo: MUY ALTO"` ✅

**Ejemplo 4:**
- `ingresos = 2500`, `deuda = 4000`, `antiguedad = 1`
- No cumple ninguna de las tres condiciones anteriores → `"Riesgo: ALTO"` ✅

### Paso 5 — Reflexión sobre el orden

¿Qué pasaría si intercambiáramos `BAJO` y `MEDIO`? Con el ejemplo 1 (`ingresos = 6000`, `deuda = 1500`, `antiguedad = 3`):
- ¿Cumple `MEDIO`? `6000 > 3000 y 1500 < 5000 y 3 >= 1` → **Sí** → clasificaría como `MEDIO` ❌

Un cliente que debería ser `BAJO` quedaría mal clasificado. Por eso el orden de los `SINO SI` importa.

---

> 💡 **Puntos clave de este ejercicio:**
> - Uso de `y` (`and`) para combinar múltiples condiciones en una misma rama.
> - Uso de `o` (`or`) para detectar cualquiera de dos situaciones de alarma.
> - El orden de evaluación en una cadena `SI / SINO SI / SINO` es determinante para la corrección del algoritmo.
