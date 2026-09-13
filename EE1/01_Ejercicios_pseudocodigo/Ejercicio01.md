# Ejercicio 1: Sistema de cobro de peaje

## Enunciado

Una autopista tiene un sistema de cobro de peaje que varía según el **tipo de vehículo** y la **hora del día**. Las reglas son las siguientes:

| Tipo de vehículo | Tarifa normal | Tarifa nocturna (entre 10 pm y 6 am) |
|---|---|---|
| Moto (`1`) | S/. 2.00 | S/. 1.00 |
| Auto (`2`) | S/. 5.00 | S/. 3.00 |
| Camión (`3`) | S/. 12.00 | S/. 8.00 |

El programa debe solicitar el **tipo de vehículo** (1, 2 o 3) y la **hora actual** (en formato de 0 a 23). Si el tipo de vehículo ingresado no es válido, debe mostrarse el mensaje `"Tipo de vehículo no reconocido"`.

Escribe el **pseudocódigo** que resuelva este problema.

---

## Resolución paso a paso

### Paso 1 — Identificar entradas, proceso y salida

Antes de escribir cualquier pseudocódigo, hay que tener claro qué necesita el algoritmo y qué debe producir.

- **Entradas:** tipo de vehículo (entero: 1, 2 o 3), hora actual (entero: 0 a 23)
- **Proceso:** determinar si la hora es nocturna y, según el tipo de vehículo, asignar la tarifa correspondiente
- **Salida:** la tarifa que debe pagar el vehículo

### Paso 2 — Identificar las condiciones

Hay dos niveles de decisión:

1. ¿Es horario nocturno? → la hora es **menor que 6** o **mayor o igual que 22**
2. ¿Qué tipo de vehículo es? → según eso, se asigna una tarifa u otra

### Paso 3 — Escribir el pseudocódigo

```
INICIO
    LEER tipo_vehiculo
    LEER hora

    SI hora < 6 o hora >= 22:
        es_nocturno = Verdadero
    SINO:
        es_nocturno = Falso

    SI tipo_vehiculo == 1 y es_nocturno == Verdadero:
        tarifa = 1.00
    SINO SI tipo_vehiculo == 1:
        tarifa = 2.00
    SINO SI tipo_vehiculo == 2 y es_nocturno == Verdadero:
        tarifa = 3.00
    SINO SI tipo_vehiculo == 2:
        tarifa = 5.00
    SINO SI tipo_vehiculo == 3 y es_nocturno == Verdadero:
        tarifa = 8.00
    SINO SI si tipo_vehiculo == 3:
        tarifa = 12.00
    SINO:
        MOSTRAR "Tipo de vehículo no reconocido"
        FIN

    MOSTRAR "La tarifa a pagar es S/.", tarifa
FIN
```

### Paso 4 — Verificar con un ejemplo

Supongamos que el usuario ingresa:
- `tipo_vehiculo = 2` (auto)
- `hora = 23` (las 11 pm)

Seguimos el pseudocódigo:
- ¿Es nocturno? `23 >= 22` → **Verdadero**
- ¿`tipo_vehiculo == 1`? No.
- ¿`tipo_vehiculo == 2 y es_nocturno == Verdadero`? **Sí** → `tarifa = 3.00`
- Salida: `"La tarifa a pagar es S/. 3.00"` ✅

### Paso 5 — Verificar el caso inválido

Si el usuario ingresa `tipo_vehiculo = 5`:
- Ninguna de las condiciones anteriores se cumple → se ejecuta el `Si no` final
- Salida: `"Tipo de vehículo no reconocido"` ✅

---

> 💡 **Puntos clave de este ejercicio:**
> - Uso de `o` (`or`) para combinar dos condiciones en la detección del horario nocturno.
> - Uso de `y` (`and`) para combinar el tipo de vehículo con la condición de horario.
> - Uso del caso `Si no` final como mecanismo de validación de entrada.
