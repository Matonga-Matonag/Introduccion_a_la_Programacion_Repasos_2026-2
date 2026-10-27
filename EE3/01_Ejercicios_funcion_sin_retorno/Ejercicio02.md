# Ejercicio 2: Verificación de acceso

## Enunciado

Implementa una función **sin retorno** llamada `verificar_acceso(usuario, clave_correcta="1234", max_intentos=3)`. La función debe pedir la clave al usuario mientras:
- No haya ingresado la clave correcta, **y**
- No haya agotado los intentos permitidos.

En cada intento, antes de pedir la clave, debe mostrar cuántos intentos le quedan. Si la clave es incorrecta, debe mostrar `"Clave incorrecta."`.

Al terminar, si el acceso fue concedido, debe imprimir `"Bienvenido, <usuario>."`. Si no, debe imprimir `"Acceso bloqueado para <usuario>."`.

El programa principal debe llamar a la función dos veces:
1. `verificar_acceso("Ana")` (usa los valores por defecto).
2. `verificar_acceso("Luis", "9999", max_intentos=2)` (argumentos posicionales y nombrados combinados).

**Ejemplo de salida para `verificar_acceso("Ana")` si el usuario ingresa `0000` y luego `1234`:**
```
Ana, ingrese su clave (3 intento(s) restante(s)): 0000
Clave incorrecta.
Ana, ingrese su clave (2 intento(s) restante(s)): 1234
Bienvenido, Ana.
```

---

## Resolución paso a paso

### Paso 1 — Identificar las condiciones del `while`

El bucle debe continuar mientras se cumplan **ambas** condiciones:
1. Quedan intentos: `intentos < max_intentos`
2. El acceso aún no fue concedido: `not acceso`

```python
while intentos < max_intentos and not acceso:
```

### Paso 2 — Inicializar las variables

- `intentos = 0`: contador de intentos realizados.
- `acceso = False`: bandera que se vuelve `True` cuando la clave es correcta.

### Paso 3 — Calcular los intentos restantes antes de pedir la clave

Los intentos restantes son `max_intentos - intentos`. Se calculan **antes** de incrementar el contador, de modo que el mensaje sea correcto en cada solicitud.

### Paso 4 — Escribir la función

```python
def verificar_acceso(usuario, clave_correcta="1234", max_intentos=3):
    intentos = 0
    acceso = False

    while intentos < max_intentos and not acceso:
        clave = input(f"{usuario}, ingrese su clave ({max_intentos - intentos} intento(s) restante(s)): ")
        intentos = intentos + 1

        if clave == clave_correcta:
            acceso = True
        else:
            print("Clave incorrecta.")

    if acceso:
        print(f"Bienvenido, {usuario}.")
    else:
        print(f"Acceso bloqueado para {usuario}.")
```

### Paso 5 — Programa principal

```python
def main():
    verificar_acceso("Ana")
    print()
    verificar_acceso("Luis", "9999", max_intentos=2)

main()
```

### Paso 6 — Verificar los casos

**Caso A: `verificar_acceso("Ana")`, con entradas `0000` y `1234`**

| Iteración | `intentos` antes | Restantes mostrados | Clave | `acceso` después |
|---|---|---|---|---|
| 1 | 0 | 3 | `0000` (incorrecta) | `False` |
| 2 | 1 | 2 | `1234` (correcta) | `True` |

Al salir del `while`, `acceso` es `True` → `"Bienvenido, Ana."` ✅

**Caso B: `verificar_acceso("Luis", "9999", max_intentos=2)`, con entradas `1111` y `2222`**

Tras 2 intentos fallidos, `intentos = 2`. La condición `2 < 2` es `False` → el bucle termina con `acceso = False`.

Salida: `"Acceso bloqueado para Luis."` ✅

### Paso 7 — Puntos a revisar

**¿Por qué `and` y no `or` en la condición del `while`?**
Se debe seguir solo mientras **ambas** condiciones sean verdaderas. Con `or`, el bucle continuaría aunque ya se hubieran agotado los intentos, lo cual sería incorrecto.

**¿Por qué la función no devuelve `True` o `False`?**
Su propósito es interactuar con el usuario y mostrar un mensaje. Es una función sin retorno.

---

> 💡 **Puntos clave de este ejercicio:**
> - `while` con `and` y `not` para combinar el límite de intentos con el estado de acceso.
> - Parámetros por defecto y argumentos nombrados en la llamada.
> - Contador que se incrementa dentro del bucle y se usa en el mensaje.
> - Mensaje final distinto según el valor de una bandera.
