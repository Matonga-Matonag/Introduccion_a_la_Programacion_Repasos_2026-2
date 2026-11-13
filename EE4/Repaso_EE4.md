# Repaso: Recursividad y Listas

> Material de repaso para el cuarto examen del curso. Basado en los contenidos vistos en clase durante las semanas 10, 11 y 12.

---

## Tabla de contenidos

1. [¿Qué es la recursividad?](#1-qué-es-la-recursividad)
2. [Del bucle a la recursión: el factorial](#2-del-bucle-a-la-recursión-el-factorial)
3. [La pila de llamadas (traza)](#3-la-pila-de-llamadas-traza)
4. [Partes de una función recursiva](#4-partes-de-una-función-recursiva)
5. [Cómo diseñar una función recursiva](#5-cómo-diseñar-una-función-recursiva)
6. [Ejemplos clásicos de recursión](#6-ejemplos-clásicos-de-recursión)
7. [Recursión vs iteración](#7-recursión-vs-iteración)
8. [¿Qué es una lista?](#8-qué-es-una-lista)
9. [Recorrer una lista](#9-recorrer-una-lista)
10. [Funciones útiles con listas](#10-funciones-útiles-con-listas)
11. [Métodos de las listas](#11-métodos-de-las-listas)
12. [Búsqueda en listas](#12-búsqueda-en-listas)
13. [Alias y copias](#13-alias-y-copias)
14. [Slicing](#14-slicing)
15. [Cadenas como secuencias](#15-cadenas-como-secuencias)
16. [Listas dentro de funciones](#16-listas-dentro-de-funciones)
17. [Errores frecuentes](#17-errores-frecuentes)

---

## 1. ¿Qué es la recursividad?

La **recursividad** (o recursión) consiste en definir una operación en términos de sí misma: una función se llama a sí misma para resolver una versión **más pequeña** del mismo problema.

```python
def cuenta_regresiva(n):
    if n == 0:
        print("¡Despegue!")
    else:
        print(n)
        cuenta_regresiva(n - 1)

cuenta_regresiva(3)
```

Salida:
```
3
2
1
¡Despegue!
```

Cada llamada resuelve una parte pequeña (imprimir `n`) y delega el resto a una llamada más simple (`cuenta_regresiva(n - 1)`).

> 💡 Una función recursiva sigue siendo una función con nombre, parámetros y `return` o `print`, como las vistas en el examen 3. Lo que cambia es que en su cuerpo aparece una llamada a sí misma.

---

## 2. Del bucle a la recursión: el factorial

El factorial de `n` se define como `n! = n · (n−1) · … · 2 · 1`, con `0! = 1`.

**Versión iterativa (con bucle):**
```python
def factorial(numero):
    incremental = 1
    factorial = 1
    while incremental <= numero:
        factorial = factorial * incremental
        incremental = incremental + 1
    return factorial
```

**Versión recursiva (sin bucle):** la definición se usa directamente.

```
n! = n · (n−1)!
```

```python
def factorial(n):
    if n == 0:
        return 1                        # caso base
    else:
        return n * factorial(n - 1)     # caso recursivo
```

Cada línea del pseudocódigo tiene su equivalente directo en Python: `si` → `if`, `retornar` → `return`.

---

## 3. La pila de llamadas (traza)

Cada llamada a una función se guarda en la **pila de llamadas** (*call stack*) como un **marco** que contiene sus parámetros y su punto de retorno. Hay dos fases:

- **Bajada:** las llamadas se van apilando hasta llegar al caso base.
- **Subida:** cada llamada devuelve su resultado a la que la invocó.

Traza de `factorial(3)`:

| Fase | Llamada | Resultado |
|---|---|---|
| Bajada | `factorial(3)` llama a `factorial(2)` | pendiente: `3 * ?` |
| Bajada | `factorial(2)` llama a `factorial(1)` | pendiente: `2 * ?` |
| Bajada | `factorial(1)` llama a `factorial(0)` | pendiente: `1 * ?` |
| Caso base | `factorial(0)` retorna `1` | `1` |
| Subida | `factorial(1)` retorna `1 * 1` | `1` |
| Subida | `factorial(2)` retorna `2 * 1` | `2` |
| Subida | `factorial(3)` retorna `3 * 2` | **`6`** |

> 💡 La última llamada en entrar es la primera en resolverse (LIFO: *last in, first out*). Para visualizar la pila paso a paso puedes usar pythontutor.com.

---

## 4. Partes de una función recursiva

Toda función recursiva tiene **dos partes**:

1. **Caso base:** el punto donde el problema es tan simple que se resuelve **sin** llamada recursiva (por ejemplo, `n == 0`).
2. **Caso recursivo:** la función se llama a sí misma con una versión **más pequeña** del problema (por ejemplo, `factorial(n - 1)`).

### ¿Qué pasa sin caso base?

```python
def factorial(n):
    return n * factorial(n - 1)   # ¡sin caso base!

factorial(3)
```

La función se llama sin parar: `3, 2, 1, 0, −1, −2…`. Python la detiene con un error:

```
RecursionError: maximum recursion depth exceeded
```

Por defecto Python permite unas **1000 llamadas anidadas** (`sys.getrecursionlimit()`).

> ⚠️ **Regla de seguridad:** verifica siempre el caso base **antes** de hacer la llamada recursiva. Un caso recursivo sin caso base es el equivalente recursivo de un bucle infinito.

---

## 5. Cómo diseñar una función recursiva

Receta en tres pasos:

1. **Encuentra el caso base:** el caso más simple, resuelto sin recursión.
2. **Encuentra un subproblema más simple:** cada llamada debe acercarse al caso base (`n - 1`).
3. **Combina:** usa el resultado del subproblema para resolver el problema (`n * factorial(n - 1)`).

> 💡 **El "salto de fe":** al escribir la llamada recursiva, confía en que ya funciona para el caso más pequeño. Tu única preocupación es combinar bien el resultado.

---

## 6. Ejemplos clásicos de recursión

### Suma de los primeros n números

```python
def suma_hasta(n):
    if n == 0:
        return 0
    return n + suma_hasta(n - 1)

print(suma_hasta(4))   # 4 + 3 + 2 + 1 + 0 = 10
```

### Potencia

Se usa la definición `bᵉ = b × bᵉ⁻¹` y `b⁰ = 1`:

```python
def potencia(base, exp):
    if exp == 0:
        return 1
    return base * potencia(base, exp - 1)

print(potencia(2, 10))   # 1024
```

### Suma de dígitos

Se toma el último dígito con `% 10` y se suma el resultado de quitarlo con `// 10`:

```python
def suma_digitos(n):
    if n < 10:              # caso base: un solo dígito
        return n
    return n % 10 + suma_digitos(n // 10)

print(suma_digitos(2026))   # 6 + 2 + 0 + 2 = 10
```

### Fibonacci

Definición: `F(0) = 0`, `F(1) = 1`, `F(i) = F(i−1) + F(i−2)` para `i > 1`.

```python
def fibonacci(n):
    if n == 0:              # primer caso base
        return 0
    if n == 1:              # segundo caso base
        return 1
    return fibonacci(n - 1) + fibonacci(n - 2)   # dos llamadas recursivas

print(fibonacci(8))   # 21
```

> ⚠️ **Hay dos casos base** porque la definición necesita dos valores iniciales. Si solo se pusiera `n == 0`, `fibonacci(1)` seguiría llamando a `fibonacci(0)` y a `fibonacci(-1)`, y nunca terminaría.

### Árbol de llamadas de fibonacci(4)

```
fib(4)
├── fib(3)
│   ├── fib(2)
│   │   ├── fib(1)
│   │   └── fib(0)
│   └── fib(1)
└── fib(2)
    ├── fib(1)
    └── fib(0)
```

Son **9 llamadas** para calcular `fib(4)`. Observa que `fib(2)` se calcula dos veces: la recursión es elegante, pero puede repetir trabajo. Para `fib(30)` se hacen más de dos millones de llamadas.

---

## 7. Recursión vs iteración

| Aspecto | Iteración (bucle) | Recursión |
|---|---|---|
| Legibilidad | Clara en recorridos simples | Natural en problemas que se dividen en subproblemas iguales |
| Memoria | Constante | Un marco en la pila por cada llamada |
| Límite | Ninguno especial | Alrededor de 1000 llamadas en Python |
| Error típico | Bucle infinito | `RecursionError` |

Comparación con la suma de `1` a `n`:

```python
# Iterativa
def suma_hasta(n):
    total = 0
    i = 1
    while i <= n:
        total = total + i
        i = i + 1
    return total

# Recursiva
def suma_hasta(n):
    if n == 0:
        return 0
    return n + suma_hasta(n - 1)
```

> 💡 Ambas resuelven lo mismo. Usa recursión cuando el problema se puede describir en términos de una versión más pequeña de sí mismo (como factorial o los árboles); usa bucles cuando el problema es un recorrido lineal simple.

---

## 8. ¿Qué es una lista?

Una **lista** es una secuencia **ordenada** de elementos que se guardan bajo un solo nombre. Cada elemento se identifica por su **índice**, que empieza en `0`.

```python
notas = [15, 12, 18, 9, 14]
print(notas[0])     # 15  (primer elemento)
print(notas[-1])    # 14  (último elemento, contando desde el final)
print(notas[1])     # 12
```

| Índice positivo | 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|---|
| **Valor** | 15 | 12 | 18 | 9 | 14 |
| **Índice negativo** | -5 | -4 | -3 | -2 | -1 |

El último índice positivo es `len(lista) − 1`.

### Listas vs arreglos

| | Arreglos (C, Java) | Listas de Python |
|---|---|---|
| Tamaño | Fijo | Dinámico: crecen y se reducen |
| Tipos | Homogéneos | Pueden mezclar tipos |

```python
edades = [18, 19, 20]              # todos enteros
mixta = ["Ana", 18, True, 1.65]    # tipos distintos
```

### Crear una lista vacía

```python
numeros = []   # lista vacía, lista para llenar con append
```

---

## 9. Recorrer una lista

Hay tres formas principales de recorrer una lista:

### Por índice (`for` + `range`)

Se usa cuando se necesita la **posición**.

```python
frutas = ["mango", "lúcuma", "chirimoya"]

for i in range(len(frutas)):
    print(i, frutas[i])
```

### Por elemento (`for-each`)

Se usa cuando solo interesan los **valores**.

```python
for fruta in frutas:
    print(fruta)
```

### Con `while`

Se usa cuando se necesita **detenerse** al encontrar algo.

```python
i = 0
while i < len(frutas):
    print(frutas[i])
    i = i + 1
```

| Necesito... | Uso |
|---|---|
| La posición | `for i in range(len(lista))` |
| Solo los valores | `for x in lista` |
| Detenerme al encontrar algo | `while` |

---

## 10. Funciones útiles con listas

```python
notas = [15, 12, 18, 9, 14]

print(len(notas))                 # 5    → cantidad de elementos
print(sum(notas))                 # 68   → suma de todos
print(min(notas))                 # 9    → menor valor
print(max(notas))                 # 18   → mayor valor
print(sum(notas) / len(notas))    # 13.6 → promedio
```

Estas funciones resuelven en una línea lo que antes se hacía con un bucle.

### `sorted` vs `sort`

Ambas ordenan, pero de forma distinta:

```python
notas = [15, 12, 18, 9, 14]

nueva = sorted(notas)     # devuelve una lista NUEVA ordenada
print(nueva)              # [9, 12, 14, 15, 18]
print(notas)              # [15, 12, 18, 9, 14]  → la original no cambia

notas.sort()             # ordena la MISMA lista
print(notas)              # [9, 12, 14, 15, 18]

resultado = notas.sort()
print(resultado)          # None → sort no devuelve la lista
```

| | `sorted(lista)` | `lista.sort()` |
|---|---|---|
| Modifica la original | No | Sí |
| Devuelve | Una lista nueva | `None` |

> ⚠️ No uses los nombres `list`, `sum`, `len`, `min` o `max` para tus variables: ocultan las funciones de Python y producen errores difíciles de encontrar.

---

## 11. Métodos de las listas

Los métodos se llaman con un punto, por ejemplo `notas.append(18)`. **Modifican la lista original** y no devuelven una lista nueva.

```python
notas = [15, 12]

notas.append(18)      # agrega al final       → [15, 12, 18]
notas.insert(0, 10)   # inserta en posición 0 → [10, 15, 12, 18]
notas.remove(12)      # quita la PRIMERA aparición de 12 → [10, 15, 18]
ultimo = notas.pop()  # quita y devuelve el último → ultimo = 18, notas = [10, 15]
notas.sort(reverse=True)   # ordena de mayor a menor → [15, 10]
```

| Método | Qué hace |
|---|---|
| `append(x)` | Agrega `x` al final |
| `insert(i, x)` | Inserta `x` en la posición `i` |
| `remove(x)` | Quita la primera aparición de `x` |
| `pop()` | Quita y devuelve el último elemento |
| `pop(i)` | Quita y devuelve el elemento en la posición `i` |
| `sort()` | Ordena la lista original |
| `copy()` | Devuelve una copia independiente |

### Ejemplo: llenar una lista hasta recibir un cero

```python
def main():
    numeros = []
    n = int(input("Número: "))
    while n != 0:
        numeros.append(n)
        n = int(input("Número: "))
    print(numeros)

main()
```

Prueba de escritorio con entradas `5`, `3`, `0`: `[]` → `[5]` → `[5, 3]`.

---

## 12. Búsqueda en listas

### Búsqueda secuencial

Se recorre la lista hasta encontrar el elemento o llegar al final:

```python
nombres = ["Life", "The Universe", "Everything", "Jack", "Jill", "Life", "Jill"]
buscar = "Jill"

contador = 0
while contador < len(nombres) and nombres[contador] != buscar:
    contador = contador + 1

if contador < len(nombres):
    print("Encontrado en la posición", contador)   # 4
else:
    print("No encontrado")
```

> ⚠️ El orden de las condiciones importa: `contador < len(nombres)` debe ir **primero**. Si se invirtiera, `nombres[contador]` podría intentar acceder a una posición que no existe.

### Uso de `in`

```python
"Jill" in nombres          # True   → ¿está?
```

---

## 13. Alias y copias

Asignar una lista a otra variable **no crea una copia**: ambos nombres apuntan a la misma lista.

```python
a = [1, 2, 3]
b = a              # alias: a y b son la MISMA lista
b.append(4)
print(a)           # [1, 2, 3, 4]  → a también cambió
```

Para crear una copia independiente:

```python
c = a.copy()       # copia con método
d = a[:]           # copia con slicing
c.append(5)
print(a)           # [1, 2, 3, 4]  → a no cambia
```

> 💡 Como las listas son **mutables** (se pueden modificar), un cambio por cualquiera de los nombres se ve en todos los que apuntan a esa lista.

---

## 14. Slicing

El operador `:` (rodajas) toma una porción de la lista. **El índice final no se incluye.**

```python
meses = ["Enero", "Febrero", "Marzo", "Abril", "Mayo", "Junio"]

print(meses[1:4])    # ['Febrero', 'Marzo', 'Abril']  → posiciones 1, 2 y 3
print(meses[3:])     # ['Abril', 'Mayo', 'Junio']     → desde 3 hasta el final
print(meses[:2])     # ['Enero', 'Febrero']           → desde el inicio hasta 1
print(meses[:])      # todos los elementos (es una copia)
```

### Paso (tercer parámetro)

```python
print(meses[::2])    # ['Enero', 'Marzo', 'Mayo']     → de dos en dos
print(meses[::-1])   # invertida
```

| Expresión | Resultado |
|---|---|
| `s[m:n]` | Desde `m` hasta `n − 1` |
| `s[m:]` | Desde `m` hasta el final |
| `s[:n]` | Desde el inicio hasta `n − 1` |
| `s[:]` | Todos (una copia) |
| `s * 4` | Repite la lista 4 veces |
| `s[::paso]` | Salta de `paso` en `paso`; `-1` invierte |

---

## 15. Cadenas como secuencias

Una cadena se recorre igual que una lista, con índices y `for`:

```python
cadena = "ABC"
for i in range(len(cadena)):
    print(cadena[i])        # A, B, C
```

Para invertirla, se recorre de atrás hacia adelante:

```python
cadena = "ABC"
respuesta = ""
for i in range(len(cadena) - 1, -1, -1):
    respuesta = respuesta + cadena[i]
print(respuesta)            # CBA
```

Atajo con slicing: `cadena[::-1]` → `"CBA"`.

> ⚠️ **Las cadenas son inmutables:** no tienen `append`, `insert` ni `pop`. Para "modificar" una cadena hay que crear una nueva.

---

## 16. Listas dentro de funciones

Una lista puede enviarse a una función. Según lo que haga, la función **modifica** la lista original o **devuelve** una nueva.

### Función que devuelve una lista nueva

```python
def suma_acumulada(numeros):
    resultado = []
    total = 0
    for n in numeros:
        total = total + n
        resultado.append(total)
    return resultado

print(suma_acumulada([1, 2, 3]))   # [1, 3, 6]
```

La lista original no se modifica.

### Función que modifica la lista original (sin `return`)

```python
def agregar_nota(notas, nota):
    notas.append(nota)

lista_notas = [12, 15]
agregar_nota(lista_notas, 18)
print(lista_notas)                 # [12, 15, 18]
```

### Eliminar elementos mientras se recorre: el error clásico

Si se elimina un elemento y se avanza el índice al mismo tiempo, **se salta el elemento siguiente**:

```python
def eliminar_negativos_mal(datos):
    for i in range(len(datos)):
        if datos[i] < 0:
            datos.pop(i)

datos = [-1, -2, 3]
eliminar_negativos_mal(datos)
print(datos)   # [-2, 3]  ❌ el -2 no se eliminó
```

Al eliminar `-1` en la posición 0, `-2` pasa a la posición 0, pero el bucle ya avanzó a la posición 1 y lo salta.

**Solución:** recorrer **de atrás hacia adelante**. Así, al eliminar un elemento, los que quedan delante de él no cambian de posición.

```python
def eliminar_negativos(datos):
    for i in range(len(datos) - 1, -1, -1):
        if datos[i] < 0:
            datos.pop(i)

datos = [10, -5, 20, -1, 0, -8]
eliminar_negativos(datos)
print(datos)   # [10, 20, 0]  ✅
```

Esta función no tiene `return`: modifica la lista recibida.

### Posiciones de un valor máximo

```python
def posiciones_del_maximo(numeros):
    if len(numeros) == 0:
        return []
    maximo = numeros[0]
    for n in numeros:
        if n > maximo:
            maximo = n
    posiciones = []
    for i in range(len(numeros)):
        if numeros[i] == maximo:
            posiciones.append(i)
    return posiciones

print(posiciones_del_maximo([5, 9, 2, 9, 9]))   # [1, 3, 4]
```

### Rotación con slicing

```python
def rotar_izquierda(lista, k):
    if len(lista) == 0:
        return []
    k = k % len(lista)                 # k puede ser mayor que el tamaño
    return lista[k:] + lista[:k]

print(rotar_izquierda([1, 2, 3, 4, 5], 2))   # [3, 4, 5, 1, 2]
print(rotar_izquierda([1, 2, 3, 4, 5], 7))   # [3, 4, 5, 1, 2]
```

### Eliminar duplicados (lista nueva)

```python
def eliminar_duplicados(lista):
    unicos = []
    for x in lista:
        if x not in unicos:
            unicos.append(x)
    return unicos

print(eliminar_duplicados([1, 2, 2, 3, 1]))   # [1, 2, 3]
```

---

## 17. Errores frecuentes

Antes de entregar tu examen, revisa estos puntos:

- [ ] ¿Mi función recursiva tiene **caso base** y verifico el caso base **antes** de la llamada recursiva?
- [ ] ¿Cada llamada recursiva se acerca al caso base (`n - 1`, `n // 10`, etc.)?
- [ ] ¿Usé dos casos base en fibonacci?
- [ ] ¿Accedo a índices válidos (de `0` a `len(lista) - 1`)?
- [ ] ¿Usé `len(lista)` y no `len(lista) + 1` en un `range` de índices?
- [ ] ¿Verifiqué `in` antes de usar `index`?
- [ ] ¿Entiendo si una función modifica la lista original o devuelve una nueva?
- [ ] ¿Recorro de atrás hacia adelante si elimino elementos mientras recorro la lista?
- [ ] ¿Sé que `sort()` devuelve `None` y que `sorted()` devuelve una lista nueva?
- [ ] ¿Creé una copia real (`copy()` o `[:]`) cuando lo necesitaba?
- [ ] ¿Recuerdo que `append` modifica la lista y no devuelve nada?
- [ ] ¿Evité usar `list`, `sum`, `len` como nombres de variables?

---

> Elaborado como material de repaso para el curso de Introducción a la Programación · Universidad de Lima · Ciclo 2026-2
