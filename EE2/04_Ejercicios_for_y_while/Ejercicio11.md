# Ejercicio 11: Registro de notas con validación

## Enunciado

Implementa un programa en Python que solicite al usuario cuántos estudiantes desea registrar (`n`). Para cada estudiante, el programa debe:

1. Pedir su **nombre**.
2. Pedir su **nota**. Si la nota no está entre **0 y 20** (inclusive), volver a pedirla hasta que sea válida.
3. Indicar si el estudiante **aprobó** (nota >= 11) o **desaprobó**.

Al finalizar todos los registros, mostrar:
- El **promedio general** del grupo.
- El **nombre del estudiante con la nota más alta**.

---

## Resolución paso a paso

### Paso 1 — Identificar la estructura de bucles

- El `for` externo recorre los `n` estudiantes.
- El `while` interno valida la nota de cada estudiante: se repite mientras la nota esté fuera del rango válido.

### Paso 2 — Diseñar el `while` de validación

La nota es inválida si es menor a 0 **o** mayor a 20:

```python
nota = float(input("Ingrese la nota: "))
while nota < 0 or nota > 20:
    print("Nota inválida. Debe estar entre 0 y 20.")
    nota = float(input("Ingrese la nota nuevamente: "))
```

### Paso 3 — Rastrear el máximo

Para encontrar al estudiante con la nota más alta se necesitan dos variables:
- `max_nota`: la nota más alta vista hasta el momento (inicializada en `-1` para que cualquier nota válida la supere).
- `nombre_max`: el nombre del estudiante que la obtuvo.

```python
if nota > max_nota:
    max_nota = nota
    nombre_max = nombre
```

### Paso 4 — Calcular el promedio

Se acumula la suma de notas durante el `for` y se divide entre `n` al terminar.

### Paso 5 — Escribir el programa

```python
def main():
    n = int(input("¿Cuántos estudiantes desea registrar? "))

    suma_notas = 0.0
    max_nota = -1
    nombre_max = ""

    for i in range(n):
        print(f"\n--- Estudiante {i + 1} ---")
        nombre = input("Nombre del estudiante: ")

        nota = float(input("Nota (0-20): "))
        while nota < 0 or nota > 20:
            print("Nota inválida. Debe estar entre 0 y 20.")
            nota = float(input("Nota (0-20): "))

        suma_notas = suma_notas + nota

        if nota >= 11:
            print(f"{nombre} aprobó con {nota}.")
        else:
            print(f"{nombre} desaprobó con {nota}.")

        if nota > max_nota:
            max_nota = nota
            nombre_max = nombre

    promedio = suma_notas / n
    print(f"\nPromedio general: {promedio}")
    print(f"Mejor nota: {nombre_max} con {max_nota}")

main()
```

### Paso 6 — Verificar con un ejemplo

**3 estudiantes: Ana (15), Luis (-3 → inválido → 8), María (18)**

| Estudiante | Nota ingresada | Válida | `suma_notas` | `max_nota` | `nombre_max` |
|---|---|---|---|---|---|
| Ana | 15 | Sí | 15 | 15 | Ana |
| Luis | -3 → 8 | No → Sí | 23 | 15 | Ana |
| María | 18 | Sí | 41 | 18 | María |

- `promedio = 41 / 3 ≈ 13.67`
- Mejor nota: María con 18 ✅

### Paso 7 — Puntos a revisar en el código

**¿Por qué `max_nota` se inicializa en `-1` y no en `0`?**
Porque `0` es una nota válida. Si un estudiante saca exactamente `0`, la condición `0 > 0` sería falsa y no quedaría registrado como máximo. Con `-1`, cualquier nota válida (desde 0) supera el valor inicial.

**¿Por qué la condición del `while` usa `or` y no `and`?**
La nota es inválida si es menor a 0 **o** si es mayor a 20. Basta con que se cumpla una de las dos para que sea inválida. Con `and`, solo se rechazaría si fuera simultáneamente negativa y mayor a 20, lo cual es imposible.

**¿Qué pasa si `n = 1`?**
El `for` se ejecuta una sola vez. El promedio es la nota de ese único estudiante, y es también la nota más alta. El programa funciona correctamente.

---

> 💡 **Puntos clave de este ejercicio:**
> - `for` externo para recorrer un número conocido de estudiantes.
> - `while` interno con `or` para validar que la nota esté dentro del rango permitido.
> - Acumulador de suma y variables de máximo actualizadas dentro del `for`.
> - `max_nota` inicializada en `-1` para que cualquier nota válida la supere desde el primer estudiante.
