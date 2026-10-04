# Ejercicio 12: Detector de números primos

## Enunciado

Implementa un programa en Python que solicite al usuario un número `n` y, para cada número del 2 hasta `n`, determine si es **primo** o no. Al finalizar, muestra cuántos números primos se encontraron en ese rango.

Un número es **primo** si solo es divisible entre 1 y él mismo. Para verificarlo, se debe buscar si existe algún divisor entre 2 y `numero - 1`:
- Si se encuentra al menos uno → **no es primo**.
- Si no se encuentra ninguno → **es primo**.

**Ejemplo con n = 10:**
```
2 es primo
3 es primo
4 no es primo (divisible entre 2)
5 es primo
6 no es primo (divisible entre 2)
7 es primo
8 no es primo (divisible entre 2)
9 no es primo (divisible entre 3)
10 no es primo (divisible entre 2)
Primos encontrados entre 2 y 10: 4
```

---

## Resolución paso a paso

### Paso 1 — Identificar la estructura de bucles

- El `for` externo recorre los números del 2 a `n`.
- El `while` interno, para cada número, busca un divisor entre 2 y `numero - 1`.
- Un contador global `total_primos` acumula los primos encontrados a lo largo de todo el `for`.

### Paso 2 — Diseñar el `while` interno

El `while` debe continuar mientras **no se haya encontrado un divisor** y **aún queden candidatos por probar**:

```python
divisor = 2
es_primo = True
while divisor < numero and es_primo:
    if numero % divisor == 0:
        es_primo = False
    else:
        divisor = divisor + 1
```

Hay dos condiciones unidas con `and`:
1. `divisor < numero`: quedan candidatos por revisar.
2. `es_primo`: todavía no se ha encontrado ningún divisor.

En cuanto se encuentra un divisor (`es_primo = False`), la segunda condición se vuelve `False` y el `while` se detiene sin seguir buscando. Esto es importante: no tiene sentido seguir buscando más divisores una vez que ya se sabe que el número no es primo.

### Paso 3 — Registrar el primer divisor encontrado

Para mostrar el mensaje `"no es primo (divisible entre X)"`, hay que guardar el divisor que rompió la condición. Como `divisor` se deja de incrementar en cuanto `es_primo` se vuelve `False`, al salir del `while` `divisor` ya contiene ese valor.

### Paso 4 — Escribir el programa

```python
def main():
    n = int(input("Ingrese el valor de n: "))

    total_primos = 0

    for numero in range(2, n + 1):
        divisor = 2
        es_primo = True

        while divisor < numero and es_primo:
            if numero % divisor == 0:
                es_primo = False
            else:
                divisor = divisor + 1

        if es_primo:
            print(f"{numero} es primo")
            total_primos = total_primos + 1
        else:
            print(f"{numero} no es primo (divisible entre {divisor})")

    print(f"Primos encontrados entre 2 y {n}: {total_primos}")

main()
```

### Paso 5 — Verificar con ejemplos

**Para `numero = 7`:**

| `divisor` | `7 % divisor` | `es_primo` | Continúa |
|---|---|---|---|
| 2 | `7 % 2 = 1` ≠ 0 | `True` | Sí → `divisor = 3` |
| 3 | `7 % 3 = 1` ≠ 0 | `True` | Sí → `divisor = 4` |
| 4 | `7 % 4 = 3` ≠ 0 | `True` | Sí → `divisor = 5` |
| 5 | `7 % 5 = 2` ≠ 0 | `True` | Sí → `divisor = 6` |
| 6 | `divisor < numero` → `6 < 7` Sí, pero `divisor = 6`, `7 % 6 = 1` ≠ 0 | `True` | `divisor = 7` |
| 7 | `divisor < numero` → `7 < 7` **Falso** | — | Sale del `while` |

- `es_primo = True` → `"7 es primo"` ✅

**Para `numero = 9`:**

| `divisor` | `9 % divisor` | `es_primo` | Continúa |
|---|---|---|---|
| 2 | `9 % 2 = 1` ≠ 0 | `True` | Sí → `divisor = 3` |
| 3 | `9 % 3 = 0` | `False` | No → sale |

- `es_primo = False`, `divisor = 3` → `"9 no es primo (divisible entre 3)"` ✅

### Paso 6 — Verificar el conteo con n = 10

Primos entre 2 y 10: 2, 3, 5, 7 → `total_primos = 4` ✅

### Paso 7 — Puntos a revisar en el código

**¿Por qué `es_primo` y `divisor` se reinician dentro del `for` y no fuera?**
Porque son específicos de cada número analizado. Si se declararan fuera, `es_primo` podría conservar el valor `False` de un número anterior, haciendo que todos los siguientes se marquen incorrectamente como no primos.

**¿Por qué el `while` tiene dos condiciones con `and` y no solo `divisor < numero`?**
Si solo se usara `divisor < numero`, el bucle seguiría probando divisores incluso después de haber encontrado uno. Agregar `and es_primo` hace que el bucle se detenga en cuanto se confirma que el número no es primo, sin trabajo innecesario.

**¿Por qué el rango empieza en 2 y no en 1?**
El 1 no se considera número primo por definición. Además, si `numero = 1`, el `while` no se ejecutaría (`divisor = 2` no es `< 1`) y quedaría marcado como primo incorrectamente.

---

> 💡 **Puntos clave de este ejercicio:**
> - `for` externo con `range(2, n + 1)` para analizar cada número del rango.
> - `while` interno con `and` entre una condición de rango (`divisor < numero`) y una condición de estado (`es_primo`).
> - Variable booleana `es_primo` como bandera que controla tanto el `while` como el `if` posterior.
> - `divisor` y `es_primo` reiniciados dentro del `for` para que cada número empiece desde cero.
> - Contador global `total_primos` acumulado a lo largo de todas las iteraciones del `for`.
