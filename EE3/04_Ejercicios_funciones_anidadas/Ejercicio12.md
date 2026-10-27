# Ejercicio 12: Suma de factores primos

## Enunciado

Implementa las siguientes funciones:

1. `es_primo(n)`: **con retorno booleano**. Devuelve `True` si `n` es primo. Para determinarlo, cuenta cuántos divisores tiene `n` en el rango de 1 a `n` (con un `for`). Un primo tiene exactamente 2 divisores.

2. `suma_factores_primos(n)`: **con retorno**. Devuelve la suma de los **factores primos** de `n`, **sin incluir** el 1 ni el propio `n`. Para ello:
   - Recorre los posibles divisores `d` desde 2 hasta `n - 1` con un `while`.
   - Si `d` divide exactamente a `n` **y** `d` es primo, lo suma.
   - Para verificar que `d` es primo, **debe llamar a `es_primo`**.

   Ejemplo: `suma_factores_primos(20)` → factores primos 2 y 5 → devuelve `7`.

3. `mostrar_factores_primos(n)`: **sin retorno**. Llama a `suma_factores_primos` e imprime el resultado con el formato:
   `"La suma de los factores primos de <n> es <suma>."`

El programa principal debe pedir un límite `limite` (mayor o igual a 2, validado con `while`) y, usando un `for` de 2 a `limite`, llamar a `mostrar_factores_primos` para cada número.

**Ejemplos:**
- `suma_factores_primos(20)` → `7` (2 + 5)
- `suma_factores_primos(30)` → `10` (2 + 3 + 5)
- `suma_factores_primos(7)` → `0` (7 es primo, pero no se incluye a sí mismo)

---

## Resolución paso a paso

### Paso 1 — Entender la estructura

```
main (for de 2 a limite)
    └── mostrar_factores_primos
            └── suma_factores_primos  (while de 2 a n - 1)
                    └── es_primo  (for de 1 a d)
```

Hay un bucle dentro de una función que a su vez llama a otra función con otro bucle. Cada función tiene una tarea clara.

### Paso 2 — Escribir `es_primo` con `for`

```python
def es_primo(n):
    divisores = 0
    for i in range(1, n + 1):
        if n % i == 0:
            divisores = divisores + 1
    return divisores == 2
```

Esta es la misma idea del examen 2 (contar divisores), pero el resultado se devuelve como `True` o `False`.

### Paso 3 — Escribir `suma_factores_primos` con `while` y llamada a `es_primo`

```python
def suma_factores_primos(n):
    suma = 0
    divisor = 2
    while divisor < n:
        if n % divisor == 0 and es_primo(divisor):
            suma = suma + divisor
        divisor = divisor + 1
    return suma
```

Por qué la condición del `while` usa `divisor < n` y no `<=`: el enunciado excluye al propio `n` de la suma.

### Paso 4 — Escribir `mostrar_factores_primos` sin retorno

```python
def mostrar_factores_primos(n):
    suma = suma_factores_primos(n)
    print(f"La suma de los factores primos de {n} es {suma}.")
```

### Paso 5 — Programa principal

```python
def main():
    limite = int(input("Ingrese el límite: "))
    while limite < 2:
        print("El límite debe ser al menos 2.")
        limite = int(input("Ingrese el límite: "))

    for numero in range(2, limite + 1):
        mostrar_factores_primos(numero)

main()
```

### Paso 6 — Verificar `suma_factores_primos(20)`

| `divisor` | ¿Divide a 20? | ¿Es primo? (`es_primo`) | Se suma |
|---|---|---|---|
| 2 | Sí | Sí | +2 → `suma = 2` |
| 3 | No | — | — |
| 4 | Sí | No (divisible entre 2) | — |
| 5 | Sí | Sí | +5 → `suma = 7` |
| 6 | No | — | — |
| 10 | Sí | No | — |
| 19 | No | — | — |

Resultado: `7` ✅

### Paso 7 — Verificar `suma_factores_primos(7)`

El `while` recorre `divisor` de 2 a 6. Ninguno divide a 7 exactamente. Por tanto `suma = 0`.

Esto es correcto: 7 es primo, pero no se incluye a sí mismo en la suma. ✅

### Paso 8 — Puntos a revisar

**¿Por qué `es_primo(divisor)` se llama solo si `n % divisor == 0`?**
Con `and`, Python evalúa primero la condición de la izquierda. Si `n % divisor != 0`, no se llama a `es_primo`, porque el resultado ya sería `False`. Esto evita trabajo innecesario.

**¿Por qué `suma_factores_primos` no modifica `n`?**
Porque se usa `n` como referencia en todo el bucle. Si se cambiara su valor, la condición `divisor < n` cambiaría durante la ejecución. Mantener `n` constante hace la función más fácil de razonar.

**¿Por qué la función sin retorno `mostrar_factores_primos` guarda la suma en una variable antes de imprimirla?**
Solo mejora la legibilidad. Puede escribirse también como `print(f"... {suma_factores_primos(n)}.")`, con el mismo resultado.

**¿Cuántas veces se llama a `es_primo` en `suma_factores_primos(20)`?**
Solo cuando `20 % divisor == 0`, es decir, para `d = 2, 4, 5, 10`. Son 4 llamadas, no 18.

---

> 💡 **Puntos clave de este ejercicio:**
> - Función con `while` que llama a una función booleana dentro de un `and`.
> - Función booleana con `for` que cuenta divisores.
> - Función sin retorno que llama a una función con retorno.
> - Programa principal con `for` que llama a una función sin retorno en cada iteración.
> - Validación con `while` del límite ingresado.
