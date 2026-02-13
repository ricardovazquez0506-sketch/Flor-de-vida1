# Flor-de-vida1
Perfecto 👍 Aquí tienes una explicación **línea por línea**, redactada para que puedas incluirla directamente en el `README.md` de tu repositorio en GitHub.

---

# 📖 Explicación del Código – Generación de Flor en Blender

Este script fue desarrollado en Python utilizando la API de Blender (`bpy`) para generar una figura similar a una flor mediante la creación de círculos distribuidos simétricamente.

---

## 🔹 1. Importación de módulos

```python
import bpy
import math
```

* `import bpy`
  Importa el módulo principal de Blender para manipular objetos, escenas y geometría mediante código.

* `import math`
  Importa funciones matemáticas necesarias para trabajar con ángulos y trigonometría (seno y coseno).

---

## 🔹 2. Limpiar la escena

```python
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()
```

* `select_all(action='SELECT')`
  Selecciona todos los objetos presentes en la escena actual.

* `delete()`
  Elimina todos los objetos seleccionados.
  👉 Esto garantiza que el script comience con una escena vacía.

---

## 🔹 3. Parámetros de la figura

```python
radio = 3
angulo_actual = 0
paso_angular = 40  # 360 / 6
```

* `radio = 3`
  Define el tamaño de los círculos y también la distancia desde el centro hacia los círculos exteriores.

* `angulo_actual = 0`
  Variable que controla el ángulo inicial en grados.

* `paso_angular = 40`
  Define cuánto aumentará el ángulo en cada iteración.
  Como el ciclo llega hasta 360°, esto generará 9 círculos periféricos (360 / 40 = 9).

---

## 🔹 4. Creación del círculo central

```python
bpy.ops.mesh.primitive_circle_add(
    radius=radio,
    location=(0, 0, 0),
    vertices=64
)
```

* `primitive_circle_add()`
  Crea un círculo en la escena.

Parámetros:

* `radius=radio` → Tamaño del círculo.
* `location=(0, 0, 0)` → Se coloca en el centro del plano.
* `vertices=64` → Define el nivel de suavidad (más vértices = círculo más detallado).

Este será el **centro de la flor**.

---

## 🔹 5. Creación de los círculos periféricos (estructura tipo flor)

```python
while angulo_actual < 360:
```

Se crea un ciclo `while` que se ejecutará hasta completar 360 grados alrededor del centro.

---

### 🔸 Conversión de grados a radianes

```python
rad = math.radians(angulo_actual)
```

Las funciones trigonométricas (`sin` y `cos`) trabajan en radianes, por eso se convierte el ángulo actual de grados a radianes.

---

### 🔸 Conversión de coordenadas polares a cartesianas

```python
x = radio * math.cos(rad)
y = radio * math.sin(rad)
```

Aquí se aplican fórmulas matemáticas:

* `x = r * cos(θ)`
* `y = r * sin(θ)`

Esto permite calcular la posición exacta de cada círculo alrededor del centro.

👉 Gracias a esto, los círculos se distribuyen de manera simétrica formando los pétalos.

---

### 🔸 Creación del círculo en la nueva posición

```python
bpy.ops.mesh.primitive_circle_add(
    radius=radio,
    location=(x, y, 0),
    vertices=64
)
```

Se crea un nuevo círculo:

* Con el mismo radio.
* En la posición calculada `(x, y, 0)`.
* Manteniendo el mismo nivel de detalle.

---

### 🔸 Incremento del ángulo

```python
angulo_actual += paso_angular
```

Aumenta el ángulo en 40° para la siguiente iteración, permitiendo generar el siguiente “pétalo”.

---

# 🎯 Resultado Final

El script genera:

* 1 círculo central
* 9 círculos distribuidos alrededor
* Una figura simétrica similar a una flor
