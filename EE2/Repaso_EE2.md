# Repaso: Estructuras Repetitivas y Bucles Anidados

> Material de repaso para el segundo examen del curso. Basado en los contenidos vistos en clase durante las semanas 5 y 6.

---

## Tabla de contenidos

1. [¿Qué es la repetición?](#1-qué-es-la-repetición)
2. [Contadores y acumuladores](#2-contadores-y-acumuladores)
3. [El bucle `while`](#3-el-bucle-while)
4. [El bucle `for` con `range()`](#4-el-bucle-for-con-range)
5. [Bucles infinitos](#5-bucles-infinitos)
6. [Condicionales dentro de bucles](#6-condicionales-dentro-de-bucles)
7. [Bucles dentro de condicionales](#7-bucles-dentro-de-condicionales)
8. [Bucles anidados](#8-bucles-anidados)
9. [Análisis de bucles](#9-análisis-de-bucles)

---

## 1. ¿Qué es la repetición?

Una estructura repetitiva (o bucle) permite ejecutar un bloque de instrucciones **más de una vez**, evitando tener que escribir el mismo código repetidamente.

**Sin repetición** — imprimir "Python" 5 veces:
```python
print("Python")
print("Python")
print("Python")
print("Python")
print("Python")
```

**Con repetición** — lo mismo en dos líneas:
```python
for i in range(5):
    print("Python")
```

En Python existen dos tipos de bucle:
- `while`: repite **mientras** una condición sea verdadera. Se usa cuando no se sabe de antemano cuántas veces se va a repetir.
- `for`: repite una cantidad **fija y conocida** de veces. En este curso se usa siempre con `range()`.

---

## 2. Contadores y acumuladores

Antes de ver los bucles en detalle, es importante entender dos patrones que aparecen constantemente dentro de ellos.

### Contador

Una variable que **suma 1** en cada iteración para llevar la cuenta de cuántas veces ha ocurrido algo.

```python
# Pseudocódigo
c ← 1
mientras condición sea verdadera:
    imprimir c
    c ← c + 1
```

```python
# Python
c = 1
while c <= 5:
    print(c)
    c = c + 1
# Imprime: 1, 2, 3, 4, 5
```

### Acumulador

Una variable que **acumula una suma** (u otra operación) a lo largo de las iteraciones.

```python
# Pseudocódigo
s ← 0
mientras condición sea verdadera:
    ingresar n
    s ← s + n
    imprimir s
```

```python
# Python
s = 0
n = int(input("Ingrese un número (0 para terminar): "))
while n != 0:
    s = s + n
    n = int(input("Ingrese otro número (0 para terminar): "))
print("Suma total:", s)
```

> 💡 La diferencia clave: un **contador** siempre suma 1; un **acumulador** suma el valor de una variable que puede ser cualquier número.

---

## 3. El bucle `while`

Repite un bloque de instrucciones **mientras** su condición sea verdadera. Cuando la condición se vuelve falsa, el bucle termina y el programa continúa con lo que sigue.

```python
while <condicion>:
    <sentencias>
```

> ⚠️ La condición se evalúa **antes** de cada iteración. Si es falsa desde el principio, el cuerpo del bucle no se ejecuta ni una sola vez.

### Ejemplo: crecimiento de precio de un inmueble

```python
def main():
    precio = 100000
    cuenta_m = 1
    while cuenta_m <= 12:
        precio_inc = precio * 1.05
        print("Mes:", cuenta_m, "Precio:", precio_inc)
        precio = precio_inc
        cuenta_m = cuenta_m + 1

main()
```

### Ejemplo: bucle con condición de parada por valor ingresado

```python
def main():
    n = int(input("Ingrese un número (0 para salir): "))
    while n != 0:
        print("Número ingresado:", n)
        n = int(input("Ingrese otro número (0 para salir): "))
    print("Se ingresó un 0. Fin del programa.")

main()
```

### Partes de un `while` bien construido

Para que un bucle `while` funcione correctamente necesita tres cosas:

1. **Inicialización:** la variable que controla la condición debe tener un valor antes del bucle.
2. **Condición:** la expresión que se evalúa antes de cada iteración.
3. **Actualización:** dentro del bucle, la variable de control debe modificarse para que en algún momento la condición se vuelva falsa.

```python
cuenta = 1                  # 1. Inicialización
while cuenta <= 10:         # 2. Condición
    print(cuenta)
    cuenta = cuenta + 1     # 3. Actualización
```

---

## 4. El bucle `for` con `range()`

Repite un bloque un **número fijo de veces**, recorriendo una secuencia de valores generada por `range()`.

```python
for <variable> in range(<inicio>, <fin>, <paso>):
    <sentencias>
```

La función `range()` puede usarse de tres formas:

| Forma | Significado | Valores generados |
|---|---|---|
| `range(n)` | De 0 hasta n-1, de 1 en 1 | `0, 1, 2, ..., n-1` |
| `range(inicio, fin)` | De `inicio` hasta `fin-1`, de 1 en 1 | `inicio, inicio+1, ..., fin-1` |
| `range(inicio, fin, paso)` | De `inicio` hasta `fin-1`, de `paso` en `paso` | `inicio, inicio+paso, ...` |

> ⚠️ El valor `fin` **nunca se incluye** en la secuencia.

### Ejemplos de `range()`

```python
# Contar del 0 al 4
for i in range(5):
    print(i)
# 0, 1, 2, 3, 4

# Contar del 1 al 5
for i in range(1, 6):
    print(i)
# 1, 2, 3, 4, 5

# Contar de 2 en 2
for i in range(0, 10, 2):
    print(i)
# 0, 2, 4, 6, 8

# Contar hacia atrás
for i in range(5, 0, -1):
    print(i)
# 5, 4, 3, 2, 1
```

### Ejemplo: tabla de multiplicar del 5

```python
def main():
    for i in range(1, 11):
        print(f"5 x {i} = {5 * i}")

main()
```

### ¿Cuándo usar `for` y cuándo `while`?

| Situación | Bucle recomendado |
|---|---|
| Se sabe exactamente cuántas veces repetir | `for` |
| Se repite hasta que el usuario ingrese un valor concreto | `while` |
| Se repite mientras se cumpla una condición variable | `while` |
| Se recorre una secuencia de números generada con `range()` | `for` |

---

## 5. Bucles infinitos

Un bucle infinito es aquel cuya condición **nunca se vuelve falsa**, por lo que el programa se queda ejecutando el bucle para siempre.

Las causas más comunes son:

- **Olvidar actualizar la variable de control** dentro del bucle.
- **Condición mal planteada** que nunca puede volverse falsa.
- **Error de lógica** en la actualización que no acerca la variable al límite.

```python
# ❌ Bucle infinito — se olvidó actualizar cuenta
cuenta = 1
while cuenta <= 10:
    print(cuenta)
    # cuenta nunca cambia → la condición siempre es True

# ✅ Correcto
cuenta = 1
while cuenta <= 10:
    print(cuenta)
    cuenta = cuenta + 1
```

> 💡 Antes de ejecutar un `while`, pregúntate: **¿en qué momento esta condición se volverá falsa?** Si no tienes una respuesta clara, es probable que el bucle sea infinito.

---

## 6. Condicionales dentro de bucles

Es completamente válido (y muy común) usar `if`, `elif` y `else` dentro de un bucle. El condicional se evalúa en **cada iteración**.

### Ejemplo: clasificar números del 1 al 10 como pares o impares

```python
def main():
    for i in range(1, 11):
        if i % 2 == 0:
            print(i, "es par")
        else:
            print(i, "es impar")

main()
```

### Ejemplo: sumar números hasta superar 100

```python
def main():
    suma = 0
    n = int(input("Ingrese un número: "))
    while suma <= 100:
        suma = suma + n
        n = int(input("Ingrese otro número: "))
    print("La suma superó 100. Total:", suma)

main()
```

### Ejemplo: menú con validación

Un patrón muy común es mostrar un menú en bucle y salir solo cuando el usuario elige la opción correcta:

```python
def main():
    opcion = 0
    while opcion != 3:
        print("1. Saludar")
        print("2. Mostrar mensaje")
        print("3. Salir")
        opcion = int(input("Elige una opción: "))
        if opcion == 1:
            print("¡Hola!")
        elif opcion == 2:
            print("Bienvenido al programa.")
        elif opcion != 3:
            print("Opción no válida.")
    print("Hasta luego.")

main()
```

---

## 7. Bucles dentro de condicionales

Así como se pueden poner condicionales dentro de bucles, también es posible colocar un bucle **dentro de una rama de un `if`**. El bucle solo se ejecutará si la condición del `if` es verdadera.

```python
if <condicion>:
    for/while ...:
        <sentencias>
```

### Ejemplo: imprimir la tabla de multiplicar solo si el número es positivo

```python
def main():
    n = int(input("Ingrese un número: "))
    if n > 0:
        for i in range(1, 11):
            print(f"{n} x {i} = {n * i}")
    else:
        print("El número debe ser positivo.")

main()
```

Si el usuario ingresa un número negativo o cero, el bucle nunca llega a ejecutarse.

### Ejemplo: validar una respuesta y luego repetir una acción

```python
def main():
    confirmar = input("¿Desea ver la cuenta regresiva? (s/n): ")
    if confirmar == "s":
        for i in range(10, 0, -1):
            print(i)
        print("¡Despegue!")
    else:
        print("Operación cancelada.")

main()
```

> 💡 La diferencia con las secciones anteriores es el **nivel donde vive el bucle**: en la sección 6 el condicional está dentro del bucle (se evalúa en cada iteración); aquí el bucle está dentro del condicional (puede no ejecutarse en absoluto si la condición es falsa).

---

## 8. Bucles anidados

Un bucle anidado es un bucle que se encuentra **dentro de otro bucle**. Por cada iteración del bucle externo, el bucle interno se ejecuta **completo**.

```python
for i in range(3):
    for j in range(3):
        print(i, j)
```

La tabla de valores que genera:

| `i` | `j` |
|---|---|
| 0 | 0 |
| 0 | 1 |
| 0 | 2 |
| 1 | 0 |
| 1 | 1 |
| 1 | 2 |
| 2 | 0 |
| 2 | 1 |
| 2 | 2 |

Cuando `i = 0`, `j` recorre todos sus valores (0, 1, 2). Luego `i` avanza a 1 y `j` vuelve a recorrer desde 0. Y así sucesivamente.

### Ejemplo: tablas de multiplicar del 1 al 3

```python
def main():
    for i in range(1, 4):
        for j in range(1, 11):
            print(f"{i} x {j} = {i * j}")
        print()   # línea en blanco entre tablas

main()
```

### Ejemplo: dibujar un cuadrado de n × n con asteriscos

```python
def main():
    n = int(input("Ingrese el tamaño del cuadrado: "))
    for i in range(n):
        for j in range(n):
            print("*", end=" ")
        print()   # salto de línea al terminar cada fila

main()
```

> 💡 `print("*", end=" ")` imprime el asterisco **sin saltar de línea**, usando un espacio como separador. El `print()` vacío al final de la fila exterior es el que produce el salto de línea.

### Ejemplo: triángulo de números creciente

```python
def main():
    n = int(input("Ingrese el número de filas: "))
    for i in range(1, n + 1):
        for j in range(1, i + 1):
            print(j, end=" ")
        print()

main()
# Con n=4:
# 1
# 1 2
# 1 2 3
# 1 2 3 4
```

### Bucles anidados `while`

También es posible anidar bucles `while`:

```python
def main():
    i = 1
    while i <= 3:
        j = 1
        while j <= 3:
            print(i, j)
            j = j + 1
        i = i + 1

main()
```

> ⚠️ En los bucles `while` anidados hay que inicializar y actualizar **ambos** contadores. Un error frecuente es olvidar reinicializar la variable del bucle interno (`j = 1` antes del `while` interno), lo que puede causar que el bucle interno no se ejecute en las iteraciones siguientes del externo.

---

## 9. Análisis de bucles

El número de veces que se ejecuta un bucle tiene un impacto directo en el tiempo que tarda un programa. Esto se conoce como **análisis de complejidad**.

### Bucle simple

Un bucle simple que recorre `n` elementos ejecuta sus instrucciones internas **n veces**. Su complejidad es **O(n)** (lineal): si los datos se duplican, el tiempo también se duplica aproximadamente.

```python
for i in range(n):
    pass   # se ejecuta n veces
```

### Bucle anidado

En un doble bucle anidado donde ambos recorren `n` elementos, las instrucciones del interior se ejecutan **n × n = n²** veces. Su complejidad es **O(n²)** (cuadrática).

```python
for i in range(n):
    for j in range(n):
        pass   # se ejecuta n² veces
```

> ⚠️ La diferencia entre O(n) y O(n²) se vuelve crítica con datos grandes. Con n = 1000, un bucle simple ejecuta 1 000 instrucciones; un doble bucle ejecuta 1 000 000.

### Mejor caso y peor caso

Cuando un bucle puede terminar antes dependiendo de una condición (por ejemplo, encontrar un valor buscado), se distinguen dos escenarios:

- **Mejor caso:** el elemento se encuentra en la primera posición → el bucle se ejecuta 1 vez.
- **Peor caso:** el elemento está en la última posición o no existe → el bucle se ejecuta `n` veces.

```python
# Búsqueda de un dígito: puede terminar antes con break
for i in range(1, n + 1):
    digito_actual = (num // 10 ** (n - i)) % 10
    if digito_actual == digito_buscar:
        pos = i
        break
```

---

> Elaborado como material de repaso para el curso de Introducción a la Programación · Universidad de Lima · Ciclo 2026-2
