# Ejercicio 7: Calculadora con validación

## Enunciado

Implementa en Python una calculadora que soporte las cuatro operaciones básicas: suma (`+`), resta (`-`), multiplicación (`*`) y división (`/`).

El programa debe:

1. Solicitar al usuario **dos números** (pueden ser decimales) y el **operador** como texto (`"+"`, `"-"`, `"*"` o `"/"`).
2. Si el operador es `"/"` y el segundo número es `0`, mostrar el mensaje `"Error: no se puede dividir entre cero"`.
3. Si el operador ingresado no es ninguno de los cuatro válidos, mostrar `"Error: operador no reconocido"`.
4. En cualquier otro caso, mostrar el resultado de la operación con el formato:
```
<num1> <operador> <num2> = <resultado>
```

---

## Resolución paso a paso

### Paso 1 — Identificar entradas, proceso y salida

- **Entradas:** dos números (`float`), un operador (`str`)
- **Proceso:** validar el operador y el divisor, luego realizar la operación correspondiente
- **Salida:** resultado de la operación, o mensaje de error

### Paso 2 — Identificar los casos posibles

Hay que distinguir cuatro situaciones:
1. Operador válido y operación sin problema → calcular y mostrar
2. Operador `"/"` pero segundo número es `0` → error de división
3. Operador no reconocido → error de operador
4. División normal (operador `"/"` y divisor distinto de `0`) → calcular

El caso de división entre cero debe evaluarse **antes** de intentar realizar la operación, para evitar que el programa falle.

### Paso 3 — Pensar el orden de las condiciones

Una forma de estructurarlo es:

- Primero verificar si el operador es `"/"` **y** el divisor es `0` → error
- Luego, para cada operador válido, calcular el resultado
- Al final, el `else` captura cualquier operador no reconocido

### Paso 4 — Escribir el programa

```python
def main():
    num1 = float(input("Ingrese el primer número: "))
    num2 = float(input("Ingrese el segundo número: "))
    operador = input("Ingrese el operador (+, -, *, /): ")

    if operador == "/" and num2 == 0:
        print("Error: no se puede dividir entre cero")
    elif operador == "+":
        resultado = num1 + num2
        print(f"{num1} + {num2} = {resultado}")
    elif operador == "-":
        resultado = num1 - num2
        print(f"{num1} - {num2} = {resultado}")
    elif operador == "*":
        resultado = num1 * num2
        print(f"{num1} * {num2} = {resultado}")
    elif operador == "/":
        resultado = num1 / num2
        print(f"{num1} / {num2} = {resultado}")
    else:
        print("Error: operador no reconocido")

main()
```

### Paso 5 — Verificar con ejemplos

**Ejemplo 1:** `num1 = 10`, `num2 = 4`, `operador = "+"`
- ¿`operador == "/" and num2 == 0`? No.
- ¿`operador == "+"`? **Sí** → `resultado = 14`
- Salida: `10.0 + 4.0 = 14.0` ✅

**Ejemplo 2:** `num1 = 8`, `num2 = 0`, `operador = "/"`
- ¿`operador == "/" and num2 == 0`? **Sí** → `"Error: no se puede dividir entre cero"` ✅

**Ejemplo 3:** `num1 = 5`, `num2 = 2`, `operador = "/"`
- ¿`operador == "/" and num2 == 0`? `num2 == 0` → **Falso**, así que la condición completa es Falsa.
- ¿`operador == "+"`? No. ¿`operador == "-"`? No. ¿`operador == "*"`? No.
- ¿`operador == "/"`? **Sí** → `resultado = 2.5`
- Salida: `5.0 / 2.0 = 2.5` ✅

**Ejemplo 4:** `operador = "^"`
- Ninguna condición se cumple → `"Error: operador no reconocido"` ✅

### Paso 6 — ¿Por qué la validación de división entre cero va primero?

Si se colocara el `elif operador == "/"` antes de la validación, el programa intentaría ejecutar `num1 / num2` con `num2 = 0`, lo que causaría un error en tiempo de ejecución. Al poner la validación primero, el programa la detecta antes y muestra un mensaje controlado.

### Paso 7 — ¿Por qué `operador` se lee con `input()` sin conversión?

Porque el operador es texto (`str`), y `input()` ya devuelve un `str` por defecto. No necesita conversión.

---

> 💡 **Puntos clave de este ejercicio:**
> - Comparación de strings con `==`.
> - Uso de `and` para combinar dos condiciones en la validación de la división.
> - Importancia del orden de las condiciones: la validación de división entre cero debe ir antes de la rama que realiza la división.
> - El `else` final como capturador de entradas inválidas.
