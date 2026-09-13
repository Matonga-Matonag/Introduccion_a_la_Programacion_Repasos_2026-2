# Repaso: Introducción a la Programación con Python

> Hola, soy Matías, el Asistente de Cátedra (ayudante del profe) del curso. Les preparé un material de repaso para el primer examen del curso. Espero que les sirva mucho para estudiar. ¡Éxitos!

---

## Tabla de contenidos

1. [¿Qué es Python?](#1-qué-es-python)
2. [Estructura base de un programa](#2-estructura-base-de-un-programa)
3. [Pseudocódigo](#3-pseudocódigo)
4. [Variables](#4-variables)
5. [Tipos de datos comunes](#5-tipos-de-datos-comunes)
6. [La función `print()`](#6-la-función-print)
7. [La función `input()`](#7-la-función-input)
8. [Operaciones con números](#8-operaciones-con-números)
9. [Operadores de comparación](#11-operadores-de-comparación)
10. [Estructuras selectivas](#12-estructuras-selectivas)
11. [Operadores lógicos](#13-operadores-lógicos)
12. [Recursos adicionales](#14-recursos-adicionales)

---

## 1. ¿Qué es Python?

Python es un lenguaje de programación de propósito general conocido por su simplicidad y facilidad de uso. Se utiliza en muchas áreas como ciencia de datos, desarrollo web, automatización, entre otras.

---

## 2. Estructura base de un programa

Todo programa en Python debe guardarse en un archivo con extensión `.py` y seguir esta estructura base:

```python
def main():
    # Código a implementar...
    pass

main()
```

- **`def main():`** define la función principal del programa.
- Todo el código del programa va **dentro** de `main()`, respetando la indentación.
- **`main()`** al final es la llamada que ejecuta el programa.

> ➡ **Indentación:** El cuerpo de cualquier estructura en Python (funciones, condicionales) debe estar indentado con espacios o tabulaciones respecto al nivel anterior. Python usa la indentación para delimitar bloques de código.

> 💡 **Nota para el EE1:** Si bien no es obligatorio que utilicen la estructura `def main():` para este examen, les recomiendo que se acostumbren a utilizarla para el resto del curso.

---

## 3. Pseudocódigo

El pseudocódigo es una forma de representar un algoritmo usando lenguaje natural con palabras imperativas. No tiene una sintaxis obligatoria estricta, pero debe ser claro, ordenado y fácil de traducir a código.

Un **algoritmo** es una secuencia de instrucciones que representan la solución a un problema, las cuales deben ejecutarse en el orden indicado. Todo algoritmo debe ser:

- **Preciso:** cada paso claramente especificado, sin ambigüedad.
- **Definido:** con las mismas entradas, siempre produce el mismo resultado.
- **Finito:** termina después de un número determinado de pasos.
- **Produce un resultado:** toda ejecución entrega una salida.

### Elementos de un algoritmo

| Elemento | Descripción | Pregunta clave |
|---|---|---|
| **Entrada** | Datos necesarios para ejecutar los pasos | ¿Qué necesita el algoritmo para funcionar? |
| **Proceso** | Pasos que transforman la entrada en la salida | ¿Qué operaciones se realizan? |
| **Salida** | Resultado obtenido al final | ¿Qué entrega el algoritmo? |

### Cómo construir un algoritmo

1. Definir el problema a resolver
2. Identificar las **entradas** del algoritmo
3. Identificar la **salida** del algoritmo
4. Definir los **pasos** para convertir las entradas en la salida
5. Seguir los pasos y comprobar que el algoritmo sea correcto
6. Revisar y hacer correcciones si es necesario

### Ejemplo: calcular el precio de una manzana

* **Problema:** calcular el precio de una manzana dado el precio por kilo (K) y el peso en gramos (P).
* **Entradas:** K (precio en soles del kilo), P (peso en gramos de la manzana)  
* **Salida:** M (precio en soles de una manzana)

```
INICIO
    INGRESAR valor de K y P
    CALCULAR G = K / 1000       (precio por gramo)
    CALCULAR M = G x P          (precio de la manzana)
    MOSTRAR el valor de M
FIN
```

### Pseudocódigo con condicionales

Las estructuras selectivas también se representan en pseudocódigo:

```
INICIO
    LEER celsius
    SI celsius <= 17:
        MOSTRAR "Es un día frío"
    SINO SI celsius <= 25:
        MOSTRAR "Es un día caluroso"
    SINO:
        MOSTRAR "Está quemando"
FIN
```

---

## 4. Variables

Una variable es un espacio en memoria donde se almacena un dato. Para declarar una variable en Python, se escribe el nombre (a la izquierda), el operador de asignación (`=`) y el valor (a la derecha).

```python
nombre = 'Ana'
edad = 20
altura = 1.65
```

### Reglas para nombres de variables

- Solo pueden comenzar con una **letra** o **guion bajo** (`_`), nunca con un número.
- Solo pueden contener caracteres alfanuméricos (`a-z`, `A-Z`, `0-9`) y guiones bajos.
- Son **sensibles a mayúsculas y minúsculas**: `edad`, `Edad` y `EDAD` son variables distintas.
- No pueden ser palabras reservadas de Python (`if`, `else`, `def`, `while`, etc.).
- Las variables con múltiples palabras se separan con guion bajo: `nombre_completo` (estilo *snake_case*).

---

## 5. Tipos de datos comunes

Python es un lenguaje **dinámicamente tipado**: el tipo de dato de una variable se determina a partir del valor que se le asigna, no hay que declararlo.

### Entero (`int`)

Número entero sin decimales.

```python
edad = 20
print(edad)  # 20
```

### Flotante (`float`)

Número con decimales.

```python
precio = 4.50
print(precio)  # 4.5
```

### Cadena de texto (`str`)

Secuencia de caracteres entre comillas simples o dobles.

```python
nombre = 'Ana'
ciudad = "Lima"
```

### Booleano (`bool`)

Valor que representa verdadero o falso.

```python
aprobado = True
desaprobado = False
```

### Conversión entre tipos

Es muy común necesitar convertir el tipo de un dato, especialmente al leer datos del usuario con `input()` (que siempre devuelve un `str`).

```python
# Convertir a entero
edad = int("20")       # 20
edad = int(20.9)       # 20 (trunca los decimales)

# Convertir a flotante
precio = float("4.5")  # 4.5
precio = float(20)     # 20.0

# Convertir a texto
texto = str(100)       # "100"
```

---

## 6. La función `print()`

Permite mostrar datos en la pantalla (salida estándar).

```python
print("Hola mundo")          # Hola mundo
print(2 + 5)                 # 7
print("2 + 5 =", 2 + 5)      # 2 + 5 = 7
```

### F-strings (cadenas formateadas)

Permiten insertar variables dentro de un texto de forma clara y compacta.

```python
nombre = 'Ana'
edad = 20
print(f"Me llamo {nombre} y tengo {edad} años.")
# Me llamo Ana y tengo 20 años.
```

---

## 7. La función `input()`

Permite solicitar datos al usuario. **Siempre devuelve un `str`**, por lo que si se necesita un número hay que convertirlo.

```python
nombre = input("¿Cuál es tu nombre? ")
print("Hola,", nombre)
```

```python
# Leer un número entero
edad = int(input("¿Cuántos años tienes? "))

# Leer un número flotante
altura = float(input("¿Cuánto mides (en metros)? "))
```

---

## 8. Operaciones con números

### Operaciones básicas

| Operación | Operador | Ejemplo | Resultado |
|---|---|---|---|
| Suma | `+` | `5 + 3` | `8` |
| Resta | `-` | `5 - 3` | `2` |
| Multiplicación | `*` | `5 * 3` | `15` |
| División | `/` | `5 / 2` | `2.5` |
| División entera | `//` | `5 // 2` | `2` |
| Módulo (resto) | `%` | `5 % 2` | `1` |
| Potencia | `**` | `2 ** 3` | `8` |

> ⚠️ Al dividir con `/`, el resultado **siempre es `float`**, aunque la división sea exacta (`4 / 2` devuelve `2.0`).

### Asignaciones aumentadas

Permiten actualizar el valor de una variable combinando operación y asignación en un solo paso.

```python
contador = 0
contador += 1   # equivale a: contador = contador + 1  → 1
contador -= 1   # equivale a: contador = contador - 1  → 0
precio = 100
precio *= 2     # equivale a: precio = precio * 2      → 200
precio /= 4     # equivale a: precio = precio / 4      → 50.0
```

---

## 9. Operadores de comparación

Las comparaciones evalúan una condición y devuelven `True` o `False`.

| Operador Python | Significado matemático | Ejemplo | Resultado |
|---|---|---|---|
| `==` | Igual a | `3 == 3` | `True` |
| `!=` | Distinto de | `3 != 4` | `True` |
| `>` | Mayor que | `5 > 3` | `True` |
| `<` | Menor que | `2 < 1` | `False` |
| `>=` | Mayor o igual que | `3 >= 3` | `True` |
| `<=` | Menor o igual que | `2 <= 1` | `False` |

> 💡 **Nota:** No confundir el uso de `=` (asignación) con `==` (comparación). El primero se utiliza para asignarle un valor a una variable, mientras que el segundo para comparar dos valores (retornando `True` si son iguales y `False` si son distintos).

---

## 10. Estructuras selectivas

Las estructuras selectivas permiten que el programa tome decisiones y siga distintos caminos de ejecución según el cumplimiento de condiciones.

### Estructura `if` (una sola vía)

Ejecuta el bloque solo si la condición es verdadera.

```python
if <condicion>:
    <sentencias>
```

```python
def main():
    celsius = float(input("Ingrese temperatura en Celsius: "))
    if celsius <= 17:
        print("Es un día frío")

main()
```

### Estructura `if / else` (dos vías)

Si la condición es verdadera se ejecuta el bloque del `if`; si es falsa, el del `else`. Son mutuamente excluyentes: siempre se ejecuta exactamente uno de los dos.

```python
if <condicion>:
    <sentencias>
else:
    <sentencias>
```

```python
def main():
    celsius = float(input("Ingrese temperatura en Celsius: "))
    if celsius <= 17:
        print("Es un día frío")
    else:
        print("Es un día caluroso")

main()
```

### Estructura `if / elif / else` (múltiples vías)

Permite encadenar varias condiciones. Python las evalúa en orden y ejecuta el bloque de la **primera** condición verdadera, ignorando el resto. El `else` final es opcional y actúa como caso por defecto.

```python
if <condicion1>:
    <sentencias>
elif <condicion2>:
    <sentencias>
elif <condicion3>:
    <sentencias>
...
else:
    <sentencias por defecto>
```

```python
def main():
    celsius = float(input("Ingrese temperatura en Celsius: "))
    if celsius > 25:
        print("Está quemando")
    elif celsius > 17:
        print("Es un día caluroso")
    elif celsius > 0:
        print("Es un día frío")
    else:
        print("Está helando")

main()
```

> ⚠️ Cuidado con encadenar `if` tras `if`: si escribes varios `if` seguidos (en lugar de `elif`), Python evaluará todos sin excepción, aunque ya haya encontrado una condición verdadera. Esto puede producir resultados inesperados cuando las condiciones no son mutuamente excluyentes.

```python
# ❌ Usando if tras if — se evalúan los tres
nota = 15
if nota >= 11:
    print("Aprobado")
if nota >= 13:
    print("Notable")
if nota >= 16:
    print("Excelente")
# Imprime "Aprobado" y "Notable" a la vez

# ✅ Usando elif — solo se ejecuta el primero que sea verdadero
nota = 15
if nota >= 16:
    print("Excelente")
elif nota >= 13:
    print("Notable")
elif nota >= 11:
    print("Aprobado")
# Imprime únicamente "Notable"
```

---

## 11. Operadores lógicos

Permiten combinar múltiples condiciones para crear lógica de decisión más compleja.

### `and`

Devuelve `True` solo si **ambas** condiciones son verdaderas.

```python
edad = 20
es_estudiante = True

if edad >= 18 and es_estudiante:
    print("Accede al descuento universitario")
```

### `or`

Devuelve `True` si **al menos una** condición es verdadera.

```python
edad = 15
es_estudiante = True

if edad < 18 or es_estudiante:
    print("Accede al descuento")
```

### `not`

Invierte el valor booleano de una condición.

```python
es_admin = False

if not es_admin:
    print("Acceso denegado")
```

### Tabla de verdad

| `a` | `b` | `a and b` | `a or b` | `not a` |
|---|---|---|---|---|
| `True` | `True` | `True` | `True` | `False` |
| `True` | `False` | `False` | `True` | `False` |
| `False` | `True` | `False` | `True` | `True` |
| `False` | `False` | `False` | `False` | `True` |

---

## 12. Recursos adicionales

Para profundizar más en Python y continuar practicando, les recomiendo el curso gratuito de Python de **freeCodeCamp**. Yo lo llevé antes de llevar Introducción a la Programación (y por si acaso veinteé 😉). Les servirá para profundizar más allá de lo que verán en el curso de la universidad, además de que al completarlo tendrán una certificación gratuita. Les dejaré a continuación los links tanto al curso como a la plataforma de **freeCodeCamp**, donde podrán aprender muchas cosas más sobre programación y desarrollo de software:

- 🐍 **Curso de Python (freeCodeCamp):** https://www.freecodecamp.org/learn/scientific-computing-with-python/
- 🌐 **freeCodeCamp (más cursos gratuitos):** https://www.freecodecamp.org/

**freeCodeCamp** ofrece cursos completamente gratuitos y en línea sobre programación, desarrollo web, ciencia de datos y mucho más, con certificaciones incluidas.

---

> Muchos éxitos a todos y todas en su examen. ¡Confién en ustedes! 🦾

> Elaborado como material de repaso para el curso de Introducción a la Programación · Matías Gonzalo Villar Córdova Alva
