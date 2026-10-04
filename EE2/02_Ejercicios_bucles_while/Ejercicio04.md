# Pregunta 2 — Ejercicio 1: Adivina el número secreto

## Enunciado

Implementa un programa en Python en el que el programador define un **número secreto** al inicio del código (guardado en una variable). Luego, el programa permite que el usuario intente adivinarlo con un **máximo de 5 intentos**.

En cada intento, el programa debe indicar si el número ingresado es:
- **Mayor** que el número secreto
- **Menor** que el número secreto
- **Correcto**

Si el usuario adivina el número, debe mostrar el mensaje `"¡Correcto! Lo lograste en X intento(s)."` y terminar. Si agota los 5 intentos sin acertar, debe mostrar `"Lo siento, el número era X."`.

---

## Resolución paso a paso

### Paso 1 — Identificar entradas, proceso y salida

- **Entradas:** número secreto (definido en el código), intentos del usuario
- **Proceso:** repetir mientras el usuario no acierte **y** no haya agotado los intentos; comparar cada intento con el número secreto
- **Salida:** pistas en cada intento, mensaje de éxito o derrota al finalizar

### Paso 2 — Identificar la condición del `while`

El bucle debe continuar mientras se cumplan **dos condiciones simultáneamente**:
1. El usuario no ha adivinado: `intento != secreto`
2. Quedan intentos disponibles: `intentos_usados < 5`

Ambas deben ser verdaderas para continuar → se unen con `and`:

```python
while intento != secreto and intentos_usados < 5:
```

### Paso 3 — Inicializar las variables antes del bucle

- `intento`: necesita un valor inicial que garantice que el bucle arranque. Como el número secreto es positivo, inicializarlo en `-1` asegura que la condición `intento != secreto` sea verdadera desde el principio.
- `intentos_usados`: empieza en `0`.

### Paso 4 — Determinar qué pasó al salir del bucle

Cuando el `while` termina, puede ser por dos razones distintas. Para saber cuál ocurrió, se compara `intento` con `secreto`:

```python
if intento == secreto:
    print(f"¡Correcto! Lo lograste en {intentos_usados} intento(s).")
else:
    print(f"Lo siento, el número era {secreto}.")
```

### Paso 5 — Escribir el programa

```python
def main():
    secreto = 37
    max_intentos = 5

    intento = -1
    intentos_usados = 0

    while intento != secreto and intentos_usados < max_intentos:
        intento = int(input(f"Intento {intentos_usados + 1}/{max_intentos} — Ingrese su número: "))
        intentos_usados = intentos_usados + 1

        if intento < secreto:
            print("El número secreto es mayor.")
        elif intento > secreto:
            print("El número secreto es menor.")

    if intento == secreto:
        print(f"¡Correcto! Lo lograste en {intentos_usados} intento(s).")
    else:
        print(f"Lo siento, el número era {secreto}.")

main()
```

### Paso 6 — Verificar con ejemplos

**Caso 1: el usuario adivina en el 3er intento (secreto = 37)**

| Intento | Valor | Condición del while | Mensaje |
|---|---|---|---|
| 1 | 20 | `20 != 37 and 1 < 5` → continúa | "El número secreto es mayor." |
| 2 | 50 | `50 != 37 and 2 < 5` → continúa | "El número secreto es menor." |
| 3 | 37 | `37 != 37` → **Falso**, sale | (sin pista) |

- Post-bucle: `intento == secreto` → `"¡Correcto! Lo lograste en 3 intento(s)."` ✅

**Caso 2: el usuario agota los 5 intentos sin acertar**

Al 5º intento, `intentos_usados` llega a `5`. La condición `intentos_usados < 5` se vuelve `False` → sale del bucle.

- Post-bucle: `intento != secreto` → `"Lo siento, el número era 37."` ✅

### Paso 7 — ¿Por qué no se pone el `print` de "Correcto" dentro del `while`?

Si se pusiera dentro, habría que usar una estructura más compleja para evitar que también se ejecute el mensaje de pista. Manejarlo fuera del bucle, verificando la condición de salida, es más limpio y claro.

---

> 💡 **Puntos clave de este ejercicio:**
> - `while` con dos condiciones unidas por `and`: el bucle continúa solo si **ambas** son verdaderas.
> - Variable de inicialización (`intento = -1`) para garantizar que el bucle arranque.
> - Contador de intentos actualizado dentro del bucle.
> - Condicional post-bucle para distinguir entre las dos posibles causas de salida.
