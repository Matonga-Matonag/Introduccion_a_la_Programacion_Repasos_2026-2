# Ejercicio 1: Pirámide centrada

## Enunciado

Implementa una función **sin retorno** llamada `mostrar_piramide(altura, simbolo="*")` que dibuje en pantalla una pirámide centrada de `altura` filas. La fila `i` (empezando en 1) debe tener `2 * i - 1` símbolos, precedidos por los espacios necesarios para centrarla.

El programa principal debe pedir la altura al usuario y repetir la solicitud mientras la altura sea menor que 1. Luego dibuja la pirámide con `*` y, a continuación, una segunda pirámide de altura 3 usando `#` como símbolo.

**Ejemplo con altura = 3 y símbolo `*`:**
```
  *
 ***
*****
```

---

## Resolución paso a paso

### Paso 1 — Identificar la cantidad de espacios por fila

Para una pirámide de `altura` filas, la fila `i` necesita:
- Espacios a la izquierda: `altura - i`
- Símbolos: `2 * i - 1`

| Fila (`i`) | Espacios (`altura - i`) | Símbolos (`2*i - 1`) |
|---|---|---|
| 1 | 2 | 1 |
| 2 | 1 | 3 |
| 3 | 0 | 5 |

### Paso 2 — Usar bucles anidados sin salto de línea

El bucle externo recorre las filas. Cada bucle interno imprime caracteres **sin salto de línea** con `end=""`. Al terminar la fila, un `print()` vacío produce el salto.

```python
def mostrar_piramide(altura, simbolo="*"):
    for fila in range(1, altura + 1):
        for espacio in range(altura - fila):
            print(" ", end="")
        for caracter in range(2 * fila - 1):
            print(simbolo, end="")
        print()
```

> 💡 `range(altura - fila)` genera `range(0)` en la última fila. En ese caso el bucle no imprime nada, lo cual es correcto.

### Paso 3 — Programa principal con validación

La función es sin retorno, así que el programa principal solo la llama. La validación de la altura se hace con un `while` en `main`:

```python
def main():
    altura = int(input("Ingrese la altura de la pirámide: "))
    while altura < 1:
        print("La altura debe ser al menos 1.")
        altura = int(input("Ingrese la altura de la pirámide: "))

    mostrar_piramide(altura)
    print()
    mostrar_piramide(3, "#")

main()
```

### Paso 4 — Verificar con altura = 3

- **Fila 1:** `range(2)` imprime 2 espacios; `range(1)` imprime 1 `*` → `  *`
- **Fila 2:** `range(1)` imprime 1 espacio; `range(3)` imprime 3 `*` → ` ***`
- **Fila 3:** `range(0)` no imprime espacios; `range(5)` imprime 5 `*` → `*****`

Coincide con el ejemplo del enunciado ✅

### Paso 5 — Puntos a revisar

**¿Por qué la función no tiene `return`?**
Su propósito es dibujar en pantalla. Como no necesita entregar un valor, es una función sin retorno y devuelve `None` automáticamente.

**¿Por qué el parámetro `simbolo` tiene valor por defecto?**
Así se puede llamar `mostrar_piramide(5)` (usa `*`) o `mostrar_piramide(5, "#")` para cambiar el símbolo. Los parámetros con valor por defecto van al final de la definición.

---

> 💡 **Puntos clave de este ejercicio:**
> - Función sin retorno que solo produce un efecto (imprimir).
> - Bucles anidados con `print(..., end="")` para imprimir en la misma línea.
> - Parámetro por defecto (`simbolo="*"`).
> - Validación con `while` dentro de `main`.
