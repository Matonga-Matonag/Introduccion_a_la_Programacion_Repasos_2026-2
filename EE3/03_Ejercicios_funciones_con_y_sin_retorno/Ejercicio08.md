# Ejercicio 8: Boletas de calificaciones

## Enunciado

Una institución registra las notas de sus alumnos en tres evaluaciones: **práctica** (peso 30%), **parcial** (peso 30%) y **final** (peso 40%). Implementa las siguientes funciones:

1. `pedir_nota(alumno, evaluacion)`: **con retorno**. Pide una nota para el alumno y la evaluación indicada, y valida con un `while` que esté entre 0 y 20. Devuelve la nota válida.

2. `calcular_promedio(practica, parcial, final)`: **con retorno**. Devuelve el promedio ponderado redondeado a 1 decimal.

3. `aprueba(promedio)`: **con retorno booleano**. Devuelve `True` si el promedio es mayor o igual a 11, y `False` en caso contrario.

4. `mostrar_boleta(alumno, promedio)`: **sin retorno**. Imprime el nombre del alumno, su promedio y `"APROBADO"` o `"DESAPROBADO"` según la función `aprueba`.

El programa principal debe:
- Pedir cuántos alumnos se van a registrar (mínimo 1).
- Para cada alumno, pedir su nombre y sus tres notas con `pedir_nota`, calcular su promedio y mostrar su boleta.

**Ejemplo para "Ana" con notas 12, 14, 16:**
```
Ana - Promedio: 14.2 - APROBADO
```

---

## Resolución paso a paso

### Paso 1 — Identificar las funciones y su tipo

| Función | Tipo | Devuelve |
|---|---|---|
| `pedir_nota` | Con retorno | Un número (la nota) |
| `calcular_promedio` | Con retorno | Un número (el promedio) |
| `aprueba` | Con retorno (booleano) | `True` o `False` |
| `mostrar_boleta` | Sin retorno | Nada (`None`) |

### Paso 2 — Validación dentro de una función con retorno

`pedir_nota` debe devolver siempre una nota válida. El `while` garantiza que no se retorne nada fuera de rango:

```python
def pedir_nota(alumno, evaluacion):
    nota = float(input(f"Nota de {alumno} en {evaluacion} (0-20): "))
    while nota < 0 or nota > 20:
        print("Nota inválida.")
        nota = float(input(f"Nota de {alumno} en {evaluacion} (0-20): "))
    return nota
```

### Paso 3 — Promedio ponderado

```python
def calcular_promedio(practica, parcial, final):
    promedio = practica * 0.3 + parcial * 0.3 + final * 0.4
    return round(promedio, 1)
```

### Paso 4 — Función booleana

```python
def aprueba(promedio):
    return promedio >= 11
```

Como `promedio >= 11` ya produce `True` o `False`, no hace falta un `if`.

### Paso 5 — Función sin retorno que usa otras funciones

```python
def mostrar_boleta(alumno, promedio):
    if aprueba(promedio):
        estado = "APROBADO"
    else:
        estado = "DESAPROBADO"
    print(f"{alumno} - Promedio: {promedio} - {estado}")
```

> 💡 `mostrar_boleta` llama a `aprueba`, que es una función con retorno. Así, la lógica de aprobación queda en un solo lugar.

### Paso 6 — Programa principal

```python
def main():
    n = int(input("¿Cuántos alumnos se van a registrar? "))
    while n < 1:
        print("Debe registrar al menos un alumno.")
        n = int(input("¿Cuántos alumnos se van a registrar? "))

    for i in range(n):
        nombre = input(f"\nNombre del alumno {i + 1}: ")
        practica = pedir_nota(nombre, "práctica")
        parcial = pedir_nota(nombre, "parcial")
        final = pedir_nota(nombre, "final")

        promedio = calcular_promedio(practica, parcial, final)
        mostrar_boleta(nombre, promedio)

main()
```

### Paso 7 — Verificar con Ana (12, 14, 16)

- `calcular_promedio(12, 14, 16)`: `12 * 0.3 + 14 * 0.3 + 16 * 0.4 = 3.6 + 4.2 + 6.4 = 14.2`
- `round(14.2, 1)` → `14.2`
- `aprueba(14.2)` → `14.2 >= 11` → `True`
- Salida: `Ana - Promedio: 14.2 - APROBADO` ✅

**Caso de desaprobado:** notas 8, 9, 10 → `8*0.3 + 9*0.3 + 10*0.4 = 2.4 + 2.7 + 4.0 = 9.1` → `aprueba(9.1)` es `False` → `DESAPROBADO` ✅

### Paso 8 — Puntos a revisar

**¿Por qué `pedir_nota` devuelve la nota y no la imprime?**
Porque el programa necesita el valor para calcular el promedio. Si `pedir_nota` solo mostrara la nota, las otras funciones no podrían usarla.

**¿Por qué `aprueba` no se escribe con `if`?**
Porque la comparación ya devuelve `True` o `False`. Un `if` que devuelva `True` o `False` sería redundante.

**¿Por qué `mostrar_boleta` no devuelve la boleta como texto?**
El enunciado pide mostrarla. Si se quisiera devolver el texto para guardarlo o reutilizarlo, la función tendría que usar `return` en lugar de `print`.

---

> 💡 **Puntos clave de este ejercicio:**
> - Función con retorno que valida su entrada con `while` antes de devolver.
> - Función con retorno booleano usada en un `if`.
> - Función sin retorno que llama a una función con retorno.
> - Programa principal con un `for` que llama repetidamente a varias funciones.
> - `round()` para mostrar el promedio con un decimal.
