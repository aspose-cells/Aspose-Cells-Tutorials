---
category: general
date: 2026-06-30
description: Agregar un menú contextual personalizado a una cuadrícula de Excel en
  Python y escribir un valor en la celda de Excel mientras se guarda el archivo actualizado.
  Aprende a crear un menú de clic derecho y actualizar el valor de la celda al estilo
  Python.
draft: false
keywords:
- add custom context menu
- write value to excel cell
- create right‑click menu
- update cell value python
- save updated excel file
language: es
og_description: Agregar menú contextual personalizado en Python para escribir un valor
  en una celda de Excel y guardar el archivo de Excel actualizado. Esta guía le muestra
  cómo crear un menú de clic derecho con GridJs.
og_title: Agregar menú contextual personalizado en Python – Tutorial paso a paso
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu to a Python Excel grid and write value to excel
    cell while saving the updated file. Learn to create right‑click menu and update
    cell value python style.
  headline: Add Custom Context Menu in Python – Complete Guide
  type: TechArticle
tags:
- Python
- Excel Automation
- GridJs
- Context Menu
title: Agregar menú contextual personalizado en Python – Guía completa
url: /es/python/integration-and-interoperability/add-custom-context-menu-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Añadir Menú Contextual Personalizado en Python – Guía Completa

¿Alguna vez te has preguntado cómo **añadir elementos de menú contextual personalizados** a una cuadrícula de hoja de cálculo que sirves desde Python? Tal vez necesites un rápido botón “Marcar como Revisado” que aparezca cuando un usuario haga clic derecho en una celda, escriba un valor en la celda de Excel y luego guarde el libro actualizado, todo sin salir de la interfaz web.  

En este tutorial construiremos exactamente eso: un **menú de clic derecho personalizado** impulsado por GridJs, un manejador del lado del servidor que **escribe valor en la celda de Excel**, y un paso final que **guarda el archivo Excel actualizado** en disco. Al final tendrás un patrón reutilizable que podrás incorporar en cualquier proyecto Flask, FastAPI o Django.

> **¿Por qué importa?**  
> Añadir un menú contextual personalizado agiliza los flujos de trabajo de revisión de datos, reduce la copia‑pega manual y brinda a los usuarios finales una experiencia de tipo nativo directamente dentro de la cuadrícula. Además, verás cómo **actualizar el valor de una celda al estilo python**, una habilidad esencial para cualquier tarea de automatización de Excel.

## Prerrequisitos

- Python 3.9+ (el código también funciona en 3.10)  
- `openpyxl` para el manejo de archivos Excel  
- Wrapper Python de `gridjs` (o la biblioteca JS si prefieres el front‑end)  
- Un framework web básico (se muestra un ejemplo con Flask)  
- Un archivo de libro de trabajo llamado `sample.xlsx` en la carpeta de tu proyecto  

Si te falta alguno de estos, ejecuta:

```bash
pip install openpyxl flask gridjs
```

Ahora vamos a profundizar.

---

## Paso 1 – Añadir Menú Contextual Personalizado: Inicializar GridJs y Vincular la Hoja de Trabajo

Lo primero que necesitas hacer es iniciar una instancia de `GridJs` y apuntarla a la hoja de trabajo con la que planeas trabajar. Aquí es donde la frase **add custom context menu** aparece por primera vez en nuestro código, y establece la base para todo lo demás.

```python
# step_1_initialize.py
import openpyxl
from gridjs import GridJs

# Load the workbook – this could be any .xlsx file you own
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]                     # Grab the sheet you’ll display

# Create the GridJs object and bind it to the worksheet
grid = GridJs()
grid.set_worksheet(ws)                # <-- add custom context menu works on this sheet
```

**¿Qué está pasando?**  
`grid.set_worksheet(ws)` le indica a GridJs que use los datos de `ws` como su fuente de datos. A partir de ahora, cualquier modificación del menú contextual que añadamos apuntará automáticamente a la misma hoja, manteniendo la UI y el archivo sincronizados.

> **Consejo profesional:** Mantén tu libro abierto en modo lectura/escritura solo una vez. Abrirlo repetidamente dentro de un manejador de peticiones puede causar problemas de bloqueo de archivos en Windows.

---

## Paso 2 – Escribir Valor en la Celda de Excel: Definir la Acción para el Elemento del Menú

Ahora que la cuadrícula está lista, necesitamos **write value to excel cell** cuando el usuario seleccione nuestro comando personalizado. Añadiremos una entrada de menú llamada “Mark as Reviewed” y le daremos el identificador `markReviewed`. El identificador es lo que el JavaScript del cliente enviará de vuelta al servidor.

```python
# step_2_menu_item.py
# Append a custom item to the right‑click context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",      # Text shown in the UI
    "action": "markReviewed",        # Identifier used on the client side
    "icon": "check_circle"           # Optional Material‑Icons name
})
```

**¿Por qué usar un identificador personalizado?**  
El identificador desacopla el texto de la UI de la lógica del servidor, permitiéndote cambiar la etiqueta sin tocar el código backend. También hace que la operación **create right‑click menu** sea explícita y reutilizable.

---

## Paso 3 – Crear Menú de Clic Derecho: Registrar el Manejador del Lado del Servidor

Con el elemento de menú en su lugar, debemos indicarle a GridJs qué hacer cuando el usuario haga clic en él. Aquí es donde implementamos la funcionalidad **create right‑click menu** que realmente dispara una solicitud de vuelta a Python.

```python
# step_3_handler.py
def on_custom_command(request):
    """
    Server‑side handler for the 'markReviewed' custom command.
    It receives a JSON payload like {"cell": "C12"}.
    """
    # Extract the cell address from the incoming request
    cell_address = request["cell"]           # e.g., "C12"

    # Write the word "Reviewed" into that cell
    ws[cell_address] = "Reviewed"            # <-- write value to excel cell

    # Persist the change to disk (see next step)
    # We'll return a simple JSON response to the client
    return {"status": "ok"}
```

Algunas cosas a notar:

1. **`ws[cell_address] = "Reviewed"`** es la forma más directa de **update cell value python**. En segundo plano, `openpyxl` traduce la dirección estilo A1 a índices de fila/columna.
2. El manejador devuelve una pequeña carga JSON. GridJs espera un indicador de estado; podrías ampliarlo para incluir mensajes de error si fuera necesario.

Ahora vinculamos el identificador al manejador:

```python
# step_3_register.py
grid.register_custom_command("markReviewed", on_custom_command)
```

**¿Qué pasa si la celda está vacía o protegida?**  
- Las celdas vacías no son problema—`openpyxl` las creará sobre la marcha.  
- Para hojas protegidas, deberás desproteger primero (`ws.protection.sheet = False`) o capturar un `PermissionError`.

---

## Paso 4 – Actualizar Valor de Celda en Python: Persistir el Cambio Guardando el Libro

Escribir un valor es solo la mitad de la historia; debes **save updated excel file** para que el cambio sobreviva más allá de la sesión actual. Aquí completamos el ciclo de ida y vuelta de la UI al disco.

```python
# step_4_save.py
def on_custom_command(request):
    cell_address = request["cell"]
    ws[cell_address] = "Reviewed"

    # Save the workbook to a known location
    wb.save("output/sample-updated.xlsx")   # <-- save updated excel file
    return {"status": "ok"}
```

**¿Por qué una carpeta separada?**  
Guardar en un directorio `output/` mantiene la plantilla original intacta, lo cual es útil para auditorías. Ajusta la ruta según tu entorno de despliegue.

> **Cuidado:** Si sirves a muchos usuarios concurrentes, considera usar un bloqueo seguro para hilos (`threading.Lock`) alrededor de `wb.save()` para evitar condiciones de carrera.

---

## Paso 5 – Generar JSON de Configuración del Cliente y Conectar Todo

Finalmente, necesitamos producir el JSON que la instancia front‑end de GridJs consumirá. Este JSON contiene los datos de la hoja **y** la definición del menú personalizado.

```python
# step_5_config.py
config_json = grid.get_client_config()
print(config_json)   # You can pipe this to your template engine
```

Cuando incrustes `config_json` en tu página HTML, GridJs renderizará la cuadrícula con la entrada “Mark as Reviewed” disponible al hacer clic derecho en cualquier celda.

### Ejemplo Completo con Flask

A continuación tienes una aplicación Flask mínima que reúne todas las piezas. Ejecútala, abre `http://localhost:5000` y haz clic derecho en cualquier celda para ver el menú personalizado en acción.

```python
# app.py
from flask import Flask, request, jsonify, render_template_string
import openpyxl
from gridjs import GridJs

app = Flask(__name__)

# Load workbook once at startup
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]
grid = GridJs()
grid.set_worksheet(ws)

# ---- Add custom context menu item ----
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed",
    "icon": "check_circle"
})

# ---- Server‑side handler ----
def on_custom_command(req):
    cell = req["cell"]
    ws[cell] = "Reviewed"
    wb.save("output/sample-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", on_custom_command)

# ---- Routes ----
@app.route("/")
def index():
    config = grid.get_client_config()
    # Simple inline template; in production use a separate .html file
    html = f"""
    <!doctype html>
    <html>
      <head>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
      </head>
      <body>
        <div id="wrapper"></div>
        <script>
          const config = {config};
          new gridjs.Grid(config).render(document.getElementById("wrapper"));
        </script>
      </body>
    </html>
    """
    return render_template_string(html)

@app.route("/custom-command", methods=["POST"])
def custom_command():
    payload = request.get_json()
    result = on_custom_command(payload)
    return jsonify(result)

if __name__ == "__main__":
    app.run(debug=True)
```

**Resultado esperado:**  
- Haz clic derecho en cualquier celda → aparece “Mark as Reviewed”.  
- Haz clic en ella → el contenido de la celda cambia a “Reviewed”.  
- El libro `output/sample-updated.xlsx` ahora contiene el nuevo valor.

---

## Preguntas Frecuentes y Casos Límite

| Pregunta | Respuesta |
|----------|-----------|
| *¿Qué pasa si necesito múltiples acciones personalizadas?* | Simplemente añade más objetos a `grid.settings.context_menu.custom_items` y registra cada uno con su propio identificador. |
| *¿Puedo pasar datos extra (p. ej., ID de fila) al manejador?* | Sí. Incluye claves adicionales en la carga JSON del cliente y luego léelas desde `request` en `on_custom_command`. |
| *¿Este enfoque es compatible con frameworks async?* | Absolutamente—solo convierte `on_custom_command` en una función async y usa `await wb.save(...)` si cambias a `aiofiles` u otra librería similar. |
| *¿Cómo estilo el ícono del menú?* | Proporciona cualquier nombre de Material‑Icons (`"icon": "edit"`). El front‑end carga automáticamente la fuente del ícono. |
| *¿Qué ocurre con libros de gran tamaño?* | Carga solo la hoja requerida y considera transmitir filas con `openpyxl.iter_rows()` para mantener bajo el uso de memoria. |

## ¿Qué Deberías Aprender a Continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar funcionalidades adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Preserve Single Quote Prefix of Cell Value or Range in Excel](/cells/english/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/german/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/french/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}