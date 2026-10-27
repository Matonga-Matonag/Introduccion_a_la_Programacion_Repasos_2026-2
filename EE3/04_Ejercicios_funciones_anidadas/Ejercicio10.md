# Ejercicio 10: Validador de fechas en tres niveles

## Enunciado

Implementa las siguientes funciones, donde unas llaman a otras:

1. `es_bisiesto(anio)`: **con retorno booleano**. Un año es bisiesto si es divisible entre 4 y no entre 100, o si es divisible entre 400.

2. `dias_del_mes(mes, anio)`: **con retorno**. Devuelve cuántos días tiene el mes indicado (1 a 12). Para febrero, **debe llamar a `es_bisiesto`** y devolver 29 si el año es bisiesto o 28 si no lo es. Los meses 4, 6, 9 y 11 tienen 30 días. Los demás tienen 31.

3. `validar_fecha(dia, mes, anio)`: **con retorno booleano**. Devuelve `True` si la fecha es válida, es decir:
   - El mes está entre 1 y 12.
   - El día está entre 1 y el número de días del mes, obtenido **llamando a `dias_del_mes`**.

4. `mostrar_resultado_fecha(dia, mes, anio)`: **sin retorno**. Llama a `validar_fecha` e imprime `"Fecha válida"` o `"Fecha inválida"`.

El programa principal debe pedir una fecha (día, mes y año), mostrar el resultado y preguntar si se desea validar otra fecha (`s` o `n`).

**Ejemplos:**
| Fecha | Resultado | Motivo |
|---|---|---|
| 29/02/2024 | Válida | 2024 es bisiesto |
| 29/02/1900 | Inválida | 1900 no es bisiesto (divisible entre 100 pero no entre 400) |
| 31/04/2025 | Inválida | Abril tiene 30 días |
| 31/12/2025 | Válida | Diciembre tiene 31 días |

---

## Resolución paso a paso

### Paso 1 — Dibujar la cadena de llamadas

```
mostrar_resultado_fecha
    └── validar_fecha
            └── dias_del_mes
                    └── es_bisiesto
```

Cada función resuelve una parte del problema y confía en la siguiente. Esta organización se llama **descomposición en capas**.

### Paso 2 — Escribir `es_bisiesto`

```python
def es_bisiesto(anio):
    return (anio % 4 == 0 and anio % 100 != 0) or anio % 400 == 0
```

Esta es la misma regla vista en el examen 1 y en la guía de semana 8, pero ahora devuelve un valor en lugar de imprimir.

### Paso 3 — Escribir `dias_del_mes` con llamada a `es_bisiesto`

```python
def dias_del_mes(mes, anio):
    if mes == 2:
        if es_bisiesto(anio):
            return 29
        return 28
    elif mes == 4 or mes == 6 or mes == 9 or mes == 11:
        return 30
    else:
        return 31
```

> ⚠️ Aquí se usa `return` dentro de cada rama. Como `return` termina la función, no hace falta un `else` para el caso de febrero: si el `if` interno devuelve `29`, la función ya terminó; si no, pasa a `return 28`.

### Paso 4 — Escribir `validar_fecha` con llamada a `dias_del_mes`

```python
def validar_fecha(dia, mes, anio):
    if mes < 1 or mes > 12:
        return False
    if dia < 1 or dia > dias_del_mes(mes, anio):
        return False
    return True
```

Las dos condiciones se unen con `or` porque basta con que una sea verdadera para que la fecha sea inválida.

### Paso 5 — Escribir `mostrar_resultado_fecha` sin retorno

```python
def mostrar_resultado_fecha(dia, mes, anio):
    if validar_fecha(dia, mes, anio):
        print("Fecha válida")
    else:
        print("Fecha inválida")
```

### Paso 6 — Programa principal

```python
def main():
    continuar = "s"
    while continuar == "s":
        dia = int(input("Día: "))
        mes = int(input("Mes: "))
        anio = int(input("Año: "))

        mostrar_resultado_fecha(dia, mes, anio)

        continuar = input("¿Validar otra fecha? (s/n): ")

main()
```

### Paso 7 — Verificar los cuatro ejemplos

**29/02/2024:**
- `validar_fecha`: `mes = 2` está en rango. `dias_del_mes(2, 2024)` → `es_bisiesto(2024)`: `2024 % 4 == 0` y `2024 % 100 != 0` → `True` → devuelve `29`
- `29 > 29`? No → `True` → "Fecha válida" ✅

**29/02/1900:**
- `dias_del_mes(2, 1900)` → `es_bisiesto(1900)`: `1900 % 4 == 0` es `True`, pero `1900 % 100 != 0` es `False`. Como `1900 % 400 == 0` también es `False` → `False` → devuelve `28`
- `29 > 28`? Sí → `False` → "Fecha inválida" ✅

**31/04/2025:**
- `dias_del_mes(4, 2025)` → `mes == 4` → `30`
- `31 > 30`? Sí → `False` → "Fecha inválida" ✅

**31/12/2025:**
- `dias_del_mes(12, 2025)` → no es 2, 4, 6, 9 ni 11 → `31`
- `31 > 31`? No → `True` → "Fecha válida" ✅

### Paso 8 — Puntos a revisar

**¿Por qué `validar_fecha` no tiene un `else`?**
Porque cada `return False` termina la función. Si ninguna condición de invalidez se cumple, la ejecución llega a `return True`.

**¿Por qué `dias_del_mes` no valida el mes?**
Porque su responsabilidad es devolver los días de un mes conocido. La validación del rango de meses le corresponde a `validar_fecha`. Separar estas responsabilidades hace cada función más simple.

**¿Qué pasa si se cambia el orden de las dos condiciones de `validar_fecha`?**
Si el mes fuera inválido (por ejemplo, 13) y se llamara primero a `dias_del_mes(13, anio)`, la función devolvería `31` (cae en el `else`), y la validación del día no daría un resultado confiable. Por eso se valida el mes antes.

---

> 💡 **Puntos clave de este ejercicio:**
> - Cadena de llamadas de tres niveles: cada función llama a la siguiente.
> - Función booleana (`es_bisiesto`) usada dentro de una función con retorno (`dias_del_mes`).
> - Función con retorno (`dias_del_mes`) usada dentro de una función booleana (`validar_fecha`).
> - Función sin retorno (`mostrar_resultado_fecha`) al final de la cadena.
> - `or` para detectar fechas inválidas y `if/elif/else` con `return` en cada rama.
