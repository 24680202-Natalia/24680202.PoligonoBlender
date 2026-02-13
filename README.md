# TecNM Cuautla 
# 24680202 Natalia Reyes Baños 4° Semestre Grupo 3

# Crear un polígono paso a paso en blender

### 1. Descargar e instalar Blender
Si aún no tienes el software, descarga la versión más reciente desde el sitio oficial:
*   **Enlace:** [https://www.blender.org](https://www.blender.org)
*   Sigue las instrucciones de instalación para tu sistema operativo (Windows, macOS o Linux).
  <img width="1890" height="902" alt="image" src="https://github.com/user-attachments/assets/2b43ffbb-8f31-434c-9f41-68327eb2e80d" />


### 2. Acceder al entorno de Scripting
Una vez abierto Blender, debemos ir al espacio de trabajo diseñado para código:
1. En la barra de menús superior, busca la pestaña llamada **Scripting**.
2. Al hacer clic, la interfaz cambiará. Verás un editor de texto grande en el centro.
3. Haz clic en el botón **+ New** (Nuevo) que aparece en la parte superior del editor para crear un archivo vacío.
   <img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/855dce65-e0de-4960-b85b-073cd8f6fcc9" />


### 3. Copiar y pegar el código
Copia el siguiente script y pégalo directamente en el editor de texto de Blender:

```python
import bpy
import math

def crear_poligono_2d(nombre, lados, radio):
    # Crear una nueva malla y un nuevo objeto
    malla = bpy.data.meshes.new(nombre)
    objeto = bpy.data.objects.new(nombre, malla)
    
    # Vincular el objeto a la escena actual
    bpy.context.collection.objects.link(objeto)
    
    vertices = []
    aristas = []
    
    # Cálculo de vértices usando coordenadas polares a cartesianas
    for i in range(lados):
        angulo = 2 * math.pi * i / lados
        x = radio * math.cos(angulo)
        y = radio * math.sin(angulo)
        vertices.append((x, y, 0)) # Z = 0 para mantenerlo en 2D
        
    # Definir las conexiones (aristas) entre los vértices
    for i in range(lados):
        aristas.append((i, (i + 1) % lados))
        
    # Cargar los datos en la malla
    malla.from_pydata(vertices, aristas, [])
    malla.update()

# Limpiar la escena antes de empezar (Borra los objetos actuales)
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()

# LLAMADA A LA FUNCIÓN:
# Aquí puedes cambiar 'lados' para crear un triángulo (3), cuadrado (4), etc.
crear_poligono_2d("Poligono2D", lados=6, radio=5)
```
### 4. Resultado final
Una vez ejecutado, deberías ver algo similar a esto en tu vista 3D:
<img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/55096f13-133f-4d47-b0a1-b5784e026dc1" />


