# Ejercicio 6: Costo de envío por tramos

## Enunciado

Una empresa de courier calcula el costo de un envío con las siguientes reglas:

**Cargo base:** S/. 10.00 por envío.

**Cargo por peso (`peso_kg`):**
- Si el peso es **menor o igual a 1 kg**: sin cargo adicional.
- Si el peso es **mayor que 1 kg y menor o igual a 5 kg**: S/. 5.00 adicionales.
- Si el peso es **mayor a 5 kg**: S/. 5.00 más S/. 2.00 por cada kilo que exceda los 5 kg.

**Cargo por distancia (`distancia_km`):** S/. 0.50 por cada kilómetro.

**Descuento:** si la distancia es **mayor a 100 km** y el envío **no** es express, se aplica un 10% de descuento sobre el total.

**Recargo express:** si el envío es express, el total final se multiplica por 1.5. El descuento de distancia **no** aplica a envíos express.

Implementa la función **con retorno** `calcular_costo_envio(peso_kg, distancia_km, express=False)` que devuelva el costo final redondeado a 2 decimales.

El programa principal debe pedir peso, distancia y si el envío es express (`s` o `n`), y mostrar el costo. Debe repetir la consulta mientras el usuario quiera calcular otro envío (respuesta `s`).

**Ejemplos:**
- `calcular_costo_envio(3, 50)` → `40.0`
- `calcular_costo_envio(2, 150)` → `81.0`
- `calcular_costo_envio(7, 120, express=True)` → `118.5`

---

## Resolución paso a paso

### Paso 1 — Descomponer el cálculo en partes

El costo se construye en etapas. Cada etapa se almacena en una variable:

1. Base: `costo = 10`
2. Peso: se suma el cargo por tramo de peso
3. Distancia: se suma `distancia_km * 0.5`
4. Descuento: solo si corresponde
5. Express: solo si corresponde

### Paso 2 — Cargo por peso con `if/elif/else`

```python
if peso_kg <= 1:
    cargo_peso = 0
elif peso_kg <= 5:
    cargo_peso = 5
else:
    cargo_peso = 5 + (peso_kg - 5) * 2
```

Los tramos se evalúan en orden: el primer `if` cubre hasta 1 kg, el `elif` de 1 a 5 kg, y el `else` todo lo que supere 5 kg.

### Paso 3 — Descuento y express

Hay dos reglas que dependen de `express`:
- El descuento solo aplica si la distancia es mayor a 100 **y** el envío no es express → `distancia_km > 100 and not express`
- El recargo solo aplica si es express → `if express:`

### Paso 4 — Escribir la función

```python
def calcular_costo_envio(peso_kg, distancia_km, express=False):
    costo = 10

    if peso_kg <= 1:
        cargo_peso = 0
    elif peso_kg <= 5:
        cargo_peso = 5
    else:
        cargo_peso = 5 + (peso_kg - 5) * 2

    costo = costo + cargo_peso
    costo = costo + distancia_km * 0.5

    if distancia_km > 100 and not express:
        costo = costo * 0.9

    if express:
        costo = costo * 1.5

    return round(costo, 2)
```

### Paso 5 — Programa principal

```python
def main():
    continuar = "s"
    while continuar == "s":
        peso = float(input("Ingrese el peso en kg: "))
        distancia = float(input("Ingrese la distancia en km: "))
        respuesta = input("¿Es express? (s/n): ")
        express = respuesta == "s"

        costo = calcular_costo_envio(peso, distancia, express)
        print(f"Costo del envío: S/. {costo}")

        continuar = input("¿Desea calcular otro envío? (s/n): ")

main()
```

> 💡 `express = respuesta == "s"` guarda directamente un `True` o `False`, porque la comparación devuelve un valor booleano.

### Paso 6 — Verificar los tres ejemplos

**`calcular_costo_envio(3, 50)`:**
- Base: `10`
- Peso 3 kg (entre 1 y 5): `+5` → `15`
- Distancia: `50 * 0.5 = 25` → `40`
- ¿Distancia > 100? No → sin descuento
- No es express
- Resultado: `40.0` ✅

**`calcular_costo_envio(2, 150)`:**
- Base `10`, peso 2 kg: `+5` → `15`
- Distancia: `150 * 0.5 = 75` → `90`
- ¿`150 > 100 and not False`? Sí → `90 * 0.9 = 81.0`
- Resultado: `81.0` ✅

**`calcular_costo_envio(7, 120, express=True)`:**
- Base `10`, peso 7 kg (mayor a 5): `5 + (7 - 5) * 2 = 9` → `19`
- Distancia: `120 * 0.5 = 60` → `79`
- ¿`120 > 100 and not True`? No → sin descuento
- Express: `79 * 1.5 = 118.5`
- Resultado: `118.5` ✅

### Paso 7 — Puntos a revisar

**¿Por qué el descuento y el recargo express nunca se aplican a la vez?**
Porque el descuento tiene la condición `not express`. Si el envío es express, el primer `if` es falso y solo se aplica el recargo de 1.5.

**¿Por qué el `if` de descuento usa `and not express`?**
Porque son dos condiciones que deben cumplirse al mismo tiempo: distancia mayor a 100 **y** que no sea express.

---

> 💡 **Puntos clave de este ejercicio:**
> - Función con retorno que construye un resultado por etapas.
> - `if/elif/else` para cargos por tramos.
> - `and` y `not` combinados en una condición.
> - Parámetro por defecto (`express=False`).
> - Programa principal con `while` controlado por una respuesta del usuario.
