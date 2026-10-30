# Repaso: Descomposición y Modularidad (Funciones)

> Material de repaso para el tercer examen del curso. Basado en los contenidos vistos en clase durante las semanas 7, 8 y 9.

---

## Tabla de contenidos

1. [¿Por qué descomponer un programa?](#1-por-qué-descomponer-un-programa)
2. [¿Qué es una función?](#2-qué-es-una-función)
3. [Parámetros y argumentos](#3-parámetros-y-argumentos)
4. [Funciones sin retorno](#4-funciones-sin-retorno)
5. [Funciones con retorno](#5-funciones-con-retorno)
6. [Llamadas a funciones dentro de otras funciones](#6-llamadas-a-funciones-dentro-de-otras-funciones)
7. [Parámetros por defecto](#7-parámetros-por-defecto)
8. [Parámetros nombrados](#8-parámetros-nombrados)
9. [Funciones booleanas](#9-funciones-booleanas)
10. [Variables locales y globales](#10-variables-locales-y-globales)
11. [Buenas prácticas](#11-buenas-prácticas)
12. [Errores frecuentes](#12-errores-frecuentes)

---

## 1. ¿Por qué descomponer un programa?

Un programa grande es difícil de leer, mantener y probar. **Descomponer** significa dividirlo en piezas pequeñas (funciones), cada una con una tarea concreta. A esto se le llama **modularidad**.

Las ventajas principales son:

- **Legibilidad:** el programa principal se lee como un índice de tareas.
- **Reutilización:** una función se escribe una vez y se llama las veces que haga falta.
- **Depuración:** si algo falla, el error queda aislado en una función.

> 💡 Principio de diseño: **una función = una tarea**, con un nombre que la describa.

---

## 2. ¿Qué es una función?

Una función es un bloque de código con **nombre**, que puede recibir **datos de entrada** (argumentos) y puede entregar un **valor de salida**. Se define una vez y se llama tantas veces como sea necesario.

```python
def nombre_funcion(parametro1, parametro2):
    """Descripción opcional de lo que hace la función."""
    # cuerpo de la función (indentado con 4 espacios)
```

- **`def`** inicia la definición.
- **El nombre** debe estar en minúsculas y describir la acción (un verbo, p. ej. `calcular_igv`).
- **Los parámetros** van entre paréntesis (pueden ser ninguno).
- **El cuerpo** va indentado.

### Estructura de un programa con funciones

Las funciones auxiliares se definen primero, y `main()` las llama. Este formato es el que se usa en el curso:

```python
def mostrar_linea():
    print("-" * 20)

def mostrar_titulo(texto):
    mostrar_linea()
    print(texto.upper())
    mostrar_linea()

def main():
    mostrar_titulo("menú")
    print("Fin")

main()
```

> ⚠️ Python lee las definiciones (`def`) pero **no ejecuta su cuerpo** hasta que la función es llamada.

---

## 3. Parámetros y argumentos

Son dos conceptos distintos que suelen confundirse:

- **Parámetros:** las variables que la función declara entre paréntesis en su definición.
- **Argumentos:** los valores concretos que se envían en la llamada.

```python
def area_rectangulo(base, altura):   # parámetros
    return base * altura

area = area_rectangulo(4, 3)         # argumentos: 4 y 3
print(area)                          # 12
```

Una función también puede no tener parámetros:

```python
def mostrar_menu():
    print("1. Depositar")
    print("2. Retirar")
    print("3. Salir")

mostrar_menu()
```

---

## 4. Funciones sin retorno

Una función **sin retorno** realiza una **acción** (mostrar en pantalla, modificar una lista, registrar un dato), pero no entrega un valor a quien la llama. Su propósito es **hacer**, no **calcular**.

```python
def saludar(nombre):
    print("Hola,", nombre)

saludar("Ana")    # Hola, Ana
saludar("Luis")   # Hola, Luis
```

### ¿Qué devuelve una función sin retorno?

En Python, **toda función devuelve algo**. Si no hay `return`, devuelve automáticamente `None` (el valor "nada"):

```python
resultado = saludar("María")   # Imprime: Hola, María
print(resultado)               # None
```

En otros lenguajes (C, C++, Java) estas funciones se declaran con `void`.

### Regla para decidir: ¿`print` o `return`?

| Pregunta | Tipo de función |
|---|---|
| ¿Voy a usar el resultado después (guardarlo, compararlo, operar con él)? | **Con retorno** (`return`) |
| ¿Solo necesito que algo ocurra (mostrar, guardar, dibujar)? | **Sin retorno** (`print`) |

### El error clásico: `print` no es `return`

```python
def mostrar_suma(a, b):
    print(a + b)

total = mostrar_suma(3, 4)   # imprime 7, pero total vale None
print(total * 2)             # ❌ TypeError: unsupported operand type(s) for *: 'NoneType' and 'int'
```

`print` **muestra** el 7 en pantalla, pero el valor se pierde. Si necesitas el valor para seguir operando, la función debe usar `return`:

```python
def sumar(a, b):
    return a + b

total = sumar(3, 4)
print(total * 2)   # 14 ✅
```

> 🧩 **Reto:** ¿qué imprime `print(print(1), print(2))`? Piénsalo antes de ejecutarlo.
> *(Respuesta: `1`, luego `2`, y finalmente `None None`. Cada `print` interno se ejecuta primero y devuelve `None`.)*

---

## 5. Funciones con retorno

Una función **con retorno** calcula un valor y lo entrega mediante la palabra clave `return`. Ese valor puede guardarse en una variable, compararse o usarse dentro de otra operación.

```python
def calcular_igv(precio):
    igv = precio * 0.18
    return igv              # entrega el valor a quien llamó

monto = calcular_igv(100)   # monto vale 18.0
print(monto + 100)          # 118.0
```

Al llamar `calcular_igv(100)`, la llamada **se reemplaza por su resultado** (`18.0`).

### `return` termina la función

Todo lo que esté escrito después de un `return` **no se ejecuta**:

```python
def clasificar(n):
    if n >= 0:
        return "positivo"
        print("esta línea nunca se muestra")
    return "negativo"
```

### Patrón recomendado

1. Calcular el resultado y guardarlo en una variable.
2. Usar `return` al final de la función.

```python
def estado(promedio, minimo=11):
    resultado = "Desaprobado"
    if promedio >= minimo:
        resultado = "Aprobado"
    return resultado
```

### Funciones con varios datos de entrada

```python
def calcular_promedio(nota1, nota2):
    promedio = (nota1 + nota2) / 2
    return promedio

print(calcular_promedio(12, 15))   # 13.5
```

### Redondeo con `round()`

Cuando el resultado tiene muchos decimales, puede redondearse con `round(valor, cantidad_de_decimales)`:

```python
def precio_con_igv(precio):
    return round(precio * 1.1857, 2)

print(precio_con_igv(90))   # 106.71 y no 106.713
```

---

## 6. Llamadas a funciones dentro de otras funciones

Una función puede llamar a otra. Esto se llama **composición**, y es la base para construir programas complejos a partir de piezas simples.

### Flujo de ejecución paso a paso

```python
def mostrar_linea():
    print("-" * 20)

def mostrar_titulo(texto):
    mostrar_linea()           # 2. se llama otra función
    print(texto.upper())
    mostrar_linea()

mostrar_titulo("menú")        # 1. llamada desde el programa principal
print("Fin")
```

Salida:
```
--------------------
MENÚ
--------------------
Fin
```

El orden de ejecución es:
1. La llamada `mostrar_titulo("menú")` salta al cuerpo de la función, con `texto = "menú"`.
2. Dentro, se llama a `mostrar_linea()`, que se ejecuta por completo.
3. Al terminar, el control regresa al punto de llamada y continúa con `print(texto.upper())`.
4. Al terminar `mostrar_titulo`, el control regresa al programa principal y continúa con `print("Fin")`.

### Composición con valores de retorno

Cuando cada función devuelve un valor, la salida de una puede ser la entrada de otra. La expresión se evalúa **de adentro hacia afuera**:

```python
def subtotal(precio, cantidad):
    return precio * cantidad

def aplicar_descuento(monto, porcentaje=0):
    return monto * (1 - porcentaje / 100)

def total_con_igv(monto):
    return round(monto * 1.18, 2)

total = total_con_igv(aplicar_descuento(subtotal(25, 4), 10))
print(total)   # 106.2
```

Evaluación paso a paso:
1. `subtotal(25, 4)` → `100`
2. `aplicar_descuento(100, 10)` → `90.0`
3. `total_con_igv(90.0)` → `106.2`

> 💡 Si una línea es difícil de leer, guarda cada resultado en una variable intermedia:
> ```python
> base = subtotal(25, 4)
> con_descuento = aplicar_descuento(base, 10)
> total = total_con_igv(con_descuento)
> ```

---

## 7. Parámetros por defecto

Un parámetro puede tener un **valor por defecto**. Si la llamada no envía ese argumento, la función usa el valor predeterminado.

```python
def precio_final(precio, descuento=0, igv=0.18):
    total = precio * (1 - descuento) * (1 + igv)
    return round(total, 2)

print(precio_final(100))        # 118.0  (sin descuento, IGV por defecto)
print(precio_final(100, 0.1))   # 106.2  (10% de descuento)
```

> ⚠️ **Regla:** los parámetros con valor por defecto deben ir **al final** de la definición.
>
> ```python
> def ejemplo(a=1, b):   # ❌ SyntaxError
> def ejemplo(b, a=1):   # ✅
> ```

Los valores por defecto sirven para configurar casos comunes sin obligar a repetir datos, como el IGV del 18%.

---

## 8. Parámetros nombrados

Al llamar una función, los argumentos pueden enviarse **por nombre**, lo que hace la llamada más legible y permite cambiar el orden:

```python
def mostrar_info(nombre, edad, ciudad):
    print(f"{nombre} tiene {edad} años y vive en {ciudad}.")

mostrar_info("Ana", 20, "Lima")                     # posicional
mostrar_info(nombre="Ana", edad=20, ciudad="Lima")  # nombrados
mostrar_info(ciudad="Lima", nombre="Ana", edad=20)  # nombrados, otro orden
mostrar_info("Ana", edad=20, ciudad="Lima")         # combinados
```

> ⚠️ **Regla:** primero los argumentos **posicionales** y después los **nombrados**:
>
> ```python
> mostrar_info("Ana", edad=20, ciudad="Lima")   # ✅
> mostrar_info(nombre="Ana", "Lima", 20)        # ❌ SyntaxError: positional argument follows keyword argument
> ```

---

## 9. Funciones booleanas

Una función puede devolver `True` o `False`. Su nombre suele empezar con `es_`, `esta_` o `tiene_` para indicar la pregunta que responde:

```python
def es_vocal(caracter):
    return caracter.lower() in "aeiou"

print(es_vocal("A"))   # True
print(es_vocal("b"))   # False
```

Como devuelven un valor lógico, se usan directamente en condicionales:

```python
def es_primo(n):
    divisores = 0
    for i in range(1, n + 1):
        if n % i == 0:
            divisores = divisores + 1
    return divisores == 2

def main():
    numero = int(input("Ingrese un número: "))
    if es_primo(numero):
        print(f"{numero} es primo")
    else:
        print(f"{numero} no es primo")

main()
```

> 💡 Esta función combina dos conceptos: un **bucle** que cuenta divisores (ya visto en la semana 5 y 6) y un **return** que entrega el resultado de una comparación.

---

## 10. Variables locales y globales

- **Variable local:** se crea dentro de una función y solo existe dentro de ella. Los parámetros también son locales.
- **Variable global:** se crea fuera de las funciones.

```python
IGV = 0.18                         # global

def calcular_total(subtotal):
    total = subtotal * (1 + IGV)   # total es local
    return total

print(calcular_total(100))         # 118.0
```

> ⚠️ Una función debe recibir lo que necesita **por parámetros** y devolver el resultado con `return`, en lugar de modificar variables globales. Evitarlo hace el programa más fácil de entender y de probar.
>
> ```python
> # ❌ Depende de una variable global que puede cambiar
> total = 0
> def sumar_total(n):
>     global total
>     total = total + n
>
> # ✅ Recibe y devuelve datos
> def sumar_total(total, n):
>     return total + n
> ```

---

## 11. Buenas prácticas

| Práctica | ✗ Evita | ✓ Prefiere |
|---|---|---|
| Nombre descriptivo con un verbo | `def datos(x):` | `def mostrar_datos(x):` |
| Una función = una tarea | `def procesar_todo():` | `def leer_notas():`<br>`def mostrar_reporte():` |
| Separar cálculo de presentación | `def promedio(n): print(sum(n)/len(n))` | `def promedio(n): return sum(n)/len(n)` |
| Usar `return` en funciones de cálculo | `def doble(x): print(x * 2)` | `def doble(x): return x * 2` |
| Documentar con docstring | `def igv(p): return p * 0.18` | `def igv(p):`<br>`    """Devuelve el IGV de p."""`<br>`    return p * 0.18` |
| Pasar datos por parámetros | `global total` | `def mostrar_total(total):` |

### Función pura

Una **función pura** siempre devuelve el mismo resultado para el mismo argumento y no produce efectos secundarios (no imprime ni modifica nada externo). Son las más fáciles de probar y reutilizar:

```python
def cuadrado(x):
    return x * x     # pura: no imprime ni modifica nada externo
```

### Estilo de nombres

Usa minúsculas con guion bajo (`calcular_igv`, `num_a`), como recomienda la guía de estilo PEP 8.

---

## 12. Errores frecuentes

Antes de entregar tu examen, revisa estos puntos:

- [ ] ¿Usé `return` cuando necesito el valor después, o solo `print` cuando solo debo mostrar algo?
- [ ] ¿Intenté usar el resultado de una función sin retorno? (Recuerda: devuelve `None`.)
- [ ] ¿Escribí código después de un `return` que nunca se ejecutaría?
- [ ] ¿Los parámetros con valor por defecto están al final?
- [ ] ¿En una llamada con nombres, los argumentos posicionales van primero?
- [ ] ¿Llamé a la función con la cantidad correcta de argumentos?
- [ ] ¿El nombre de mi función describe la acción que realiza?
- [ ] ¿La función hace una sola tarea?
- [ ] ¿Estoy usando una variable global en lugar de un parámetro?
- [ ] ¿Llamé a `main()` al final del archivo?

---

> Elaborado como material de repaso para el curso de Introducción a la Programación · Universidad de Lima · Ciclo 2026-2
