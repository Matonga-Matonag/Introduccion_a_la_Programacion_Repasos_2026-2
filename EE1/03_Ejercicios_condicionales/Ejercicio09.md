# Ejercicio 9: Clasificador de año

## Enunciado

Implementa un programa en Python que, dado un año ingresado por el usuario, lo clasifique según las siguientes reglas (que deben evaluarse en orden y de forma independiente entre sí):

**Regla 1 — ¿Es bisiesto?**
Un año es bisiesto si:
- Es divisible entre 4 **y** no es divisible entre 100, **o**
- Es divisible entre 400

**Regla 2 — ¿Es año de siglo?**
Un año es año de siglo si es divisible entre 100.

**Regla 3 — ¿Es año de milenio?**
Un año es año de milenio si es divisible entre 1000.

El programa debe mostrar para el año ingresado:
- Si es bisiesto o no
- Si es año de siglo o no
- Si es año de milenio o no

> Nota: estas tres clasificaciones **no son excluyentes** entre sí. Un mismo año puede cumplir varias a la vez (por ejemplo, el año 2000 es bisiesto, de siglo y de milenio). Por eso cada regla se evalúa de forma independiente con su propio `if`.

---

## Resolución paso a paso

### Paso 1 — Identificar entradas, proceso y salida

- **Entrada:** año (int)
- **Proceso:** evaluar tres reglas de forma independiente usando `%`, `and`, `or` y `not`
- **Salida:** tres mensajes indicando si el año cumple o no cada clasificación

### Paso 2 — Descomponer la regla de año bisiesto

La regla completa es:
```
(año % 4 == 0 and año % 100 != 0) or (año % 400 == 0)
```

Leída en lenguaje natural: es bisiesto si es divisible entre 4 pero no entre 100, **o** si es divisible entre 400 (la excepción a la excepción).

Una forma alternativa equivalente usando `not`:
```
año % 4 == 0 and (not año % 100 == 0 or año % 400 == 0)
```

Ambas expresiones son correctas. La primera suele ser más fácil de leer.

### Paso 3 — Las reglas de siglo y milenio son simples

- Año de siglo: `año % 100 == 0`
- Año de milenio: `año % 1000 == 0`

### Paso 4 — Usar `if` independientes, no `elif`

Como las tres clasificaciones son independientes, cada una va en su propio `if / else`. Si se usara `elif`, un año que cumple varias condiciones a la vez solo mostraría la primera que sea verdadera.

### Paso 5 — Escribir el programa

```python
def main():
    anio = int(input("Ingrese un año: "))

    # Regla 1: bisiesto
    if (anio % 4 == 0 and anio % 100 != 0) or (anio % 400 == 0):
        print(f"{anio} ES un año bisiesto")
    else:
        print(f"{anio} NO es un año bisiesto")

    # Regla 2: año de siglo
    if anio % 100 == 0:
        print(f"{anio} ES un año de siglo")
    else:
        print(f"{anio} NO es un año de siglo")

    # Regla 3: año de milenio
    if anio % 1000 == 0:
        print(f"{anio} ES un año de milenio")
    else:
        print(f"{anio} NO es un año de milenio")

main()
```

### Paso 6 — Verificar con ejemplos

**Ejemplo 1: año 2024**
- `2024 % 4 == 0` ✅ y `2024 % 100 != 0` ✅ → **bisiesto**
- `2024 % 100 == 0`? No → no es de siglo
- `2024 % 1000 == 0`? No → no es de milenio

Salida:
```
2024 ES un año bisiesto
2024 NO es un año de siglo
2024 NO es un año de milenio
```
✅

**Ejemplo 2: año 1900**
- `1900 % 4 == 0` ✅ pero `1900 % 100 != 0`? No (`1900 % 100 == 0`) ❌
- `1900 % 400 == 0`? No → **no es bisiesto**
- `1900 % 100 == 0` ✅ → **es de siglo**
- `1900 % 1000 == 0`? No → no es de milenio

Salida:
```
1900 NO es un año bisiesto
1900 ES un año de siglo
1900 NO es un año de milenio
```
✅

**Ejemplo 3: año 2000**
- `2000 % 4 == 0` ✅, `2000 % 100 != 0`? No. Pero `2000 % 400 == 0` ✅ → **bisiesto**
- `2000 % 100 == 0` ✅ → **de siglo**
- `2000 % 1000 == 0` ✅ → **de milenio**

Salida:
```
2000 ES un año bisiesto
2000 ES un año de siglo
2000 ES un año de milenio
```
✅

### Paso 7 — ¿Por qué `if` y no `elif` entre las tres reglas?

Si se hubiera escrito:

```python
if (anio % 4 == 0 and anio % 100 != 0) or (anio % 400 == 0):
    print("ES bisiesto")
elif anio % 100 == 0:
    print("ES de siglo")
elif anio % 1000 == 0:
    print("ES de milenio")
```

Para el año 2000, solo se mostraría `"ES bisiesto"` y las otras dos clasificaciones nunca se evaluarían. Las condiciones no son excluyentes, por lo que cada una merece su propio `if`.

---

> 💡 **Puntos clave de este ejercicio:**
> - Uso del operador `%` para comprobar divisibilidad.
> - Combinación de `and`, `or` y `not` en una expresión booleana compuesta.
> - Diferencia entre usar `if` independientes vs `elif`: cuándo corresponde cada uno.
> - Verificación con casos límite (1900, 2000) para confirmar que la lógica es correcta.
