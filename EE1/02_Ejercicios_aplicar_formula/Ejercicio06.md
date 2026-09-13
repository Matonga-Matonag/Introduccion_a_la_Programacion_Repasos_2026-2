# Ejercicio 6: Consumo y costo de combustible de un viaje

## Enunciado

Una empresa de transporte necesita calcular el costo de combustible de sus rutas. Para ello dispone de los siguientes datos por viaje:

- **Distancia del viaje** (en kilómetros)
- **Rendimiento del vehículo** (en km por litro)
- **Precio del combustible** (en soles por litro)
- **Número de pasajeros** a bordo

Con esos datos el programa debe calcular:

1. Los **litros de combustible** necesarios para el viaje:
```
litros = distancia / rendimiento
```

2. El **costo total de combustible** del viaje:
```
costo_total = litros * precio_litro
```

3. El **costo por pasajero** (cuánto debería aportar cada uno):
```
costo_por_pasajero = costo_total / num_pasajeros
```

4. El **costo por kilómetro recorrido**:
```
costo_por_km = costo_total / distancia
```

Implementa el programa en Python que solicite los cuatro datos al usuario y muestre los cuatro resultados indicados.

---

## Resolución paso a paso

### Paso 1 — Identificar entradas, proceso y salida

- **Entradas:** distancia (float), rendimiento (float), precio por litro (float), número de pasajeros (int)
- **Proceso:** aplicar las cuatro fórmulas en orden, ya que cada resultado puede depender del anterior
- **Salida:** litros necesarios, costo total, costo por pasajero, costo por kilómetro

### Paso 2 — Identificar el orden de los cálculos

Las fórmulas tienen dependencias entre sí:

- `litros` depende solo de las entradas → se calcula primero
- `costo_total` depende de `litros` → se calcula segundo
- `costo_por_pasajero` y `costo_por_km` dependen de `costo_total` → se calculan al final

### Paso 3 — Decidir los tipos de datos

- `distancia`, `rendimiento` y `precio_litro` → `float`, porque pueden tener decimales
- `num_pasajeros` → `int`, porque siempre es un entero

### Paso 4 — Escribir el programa

```python
def main():
    distancia = float(input("Ingrese la distancia del viaje (km): "))
    rendimiento = float(input("Ingrese el rendimiento del vehículo (km/litro): "))
    precio_litro = float(input("Ingrese el precio del combustible (S/. por litro): "))
    num_pasajeros = int(input("Ingrese el número de pasajeros: "))

    litros = distancia / rendimiento
    costo_total = litros * precio_litro
    costo_por_pasajero = costo_total / num_pasajeros
    costo_por_km = costo_total / distancia

    print(f"Litros necesarios:      {litros} L")
    print(f"Costo total:            S/. {costo_total}")
    print(f"Costo por pasajero:     S/. {costo_por_pasajero}")
    print(f"Costo por kilómetro:    S/. {costo_por_km}")

main()
```

### Paso 5 — Verificar con un ejemplo manual

Supongamos:
- `distancia = 350`, `rendimiento = 12.5`, `precio_litro = 6.80`, `num_pasajeros = 4`

Paso a paso:
- `litros = 350 / 12.5 = 28`
- `costo_total = 28 * 6.80 = 190.40`
- `costo_por_pasajero = 190.40 / 4 = 47.60`
- `costo_por_km = 190.40 / 350 ≈ 0.544`

Salida esperada:
```
Litros necesarios:      28.0 L
Costo total:            S/. 190.4
Costo por pasajero:     S/. 47.6
Costo por kilómetro:    S/. 0.544
```
✅

### Paso 6 — Puntos a revisar en el código

**¿Por qué `num_pasajeros` es `int` y no `float`?**
No tiene sentido tener 4.5 pasajeros. Usar `int` refleja correctamente la naturaleza del dato.

**¿Podría haber un error si el usuario ingresa `0` pasajeros o `0` de rendimiento?**
Sí: en ambos casos se produciría una división entre cero. Ese tipo de validación se resuelve con condicionales, que es el tema del tercer grupo de ejercicios.

**¿Por qué se calcula `litros` antes que `costo_total`?**
Porque `costo_total` depende de `litros`. Si se intentara calcular `costo_total` primero, Python daría un error porque `litros` aún no existiría como variable.

---

> 💡 **Puntos clave de este ejercicio:**
> - Uso correcto de `float()` e `int()` según la naturaleza de cada dato.
> - Respeto del orden de los cálculos cuando hay dependencias entre variables.
> - Operador de división `/` que siempre devuelve `float`.
> - F-strings para mostrar resultados con unidades y etiquetas.
