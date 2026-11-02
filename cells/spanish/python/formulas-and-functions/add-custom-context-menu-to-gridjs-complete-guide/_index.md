---
category: general
date: 2026-06-08
description: Añade un menú contextual personalizado a GridJs y exporta la cuadrícula
  a CSV con un blob de archivo CSV descargable. Sigue este tutorial paso a paso para
  un ejemplo completamente funcional.
draft: false
keywords:
- add custom context menu
- export grid to csv
- download csv file blob
- GridJs context menu
- Flask CSV export
language: es
og_description: Agrega un menú contextual personalizado a GridJs y exporta la cuadrícula
  a CSV con un blob de archivo CSV para descargar. Aprende la implementación completa
  en menos de 10 minutos.
og_title: Agregar menú contextual personalizado a GridJs – Guía completa
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Add custom context menu to GridJs and export grid to CSV with a download
    CSV file blob. Follow this step‑by‑step tutorial for a fully working example.
  headline: Add Custom Context Menu to GridJs – Complete Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- Python
- Flask
title: Agregar menú contextual personalizado a GridJs – Guía completa
url: /es/python/formulas-and-functions/add-custom-context-menu-to-gridjs-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Añadir menú contextual personalizado a GridJs – Guía completa

¿Quieres **añadir un menú contextual personalizado** a un componente GridJs? En este tutorial te guiaremos paso a paso y te mostraremos cómo **exportar la cuadrícula a CSV** usando un **blob de archivo CSV para descargar**. Ya sea que estés construyendo un panel de administración rápido o un completo panel de informes, un menú de clic derecho que permita a los usuarios extraer datos como CSV puede ser un gran impulso de productividad.

Cubrirémos todo lo que necesitas: la parte de Python con Flask, el manejador JavaScript que crea el Blob y el HTML/JS que genera GridJs. Al final tendrás un ejemplo autónomo que puedes integrar en cualquier proyecto.

---

## Qué necesitarás

Antes de profundizar, asegúrate de tener:

- **Python 3.9+** y **Flask** instalados (`pip install flask`).
- El **wrapper de gridjs** para Python (o la biblioteca JavaScript directamente) – para esta guía asumiremos un wrapper ligero de Python que refleja la API de JavaScript.
- Un entendimiento básico de **JavaScript asíncrono** (`fetch`, `Promise`) – pero no te preocupes, explicaremos cada línea.
- Un editor que te guste (VS Code, PyCharm, o incluso un editor de texto simple).

Eso es todo. Sin herramientas de compilación front‑end adicionales, sin el baile de Node npm. Simplemente Flask sirviendo el HTML que genera GridJs.

---

## Añadir menú contextual personalizado a GridJs

Lo primero que debes hacer es indicarle a GridJs que deseas un menú de clic derecho personalizado. Por defecto, GridJs incluye un conjunto mínimo (copiar, pegar, etc.), pero puedes reemplazarlo por completo.

```python
# Step 1: Create a new workbook that will be displayed in the grid
workbook = Workbook()

# Step 2: Initialise the GridJs component with the workbook
grid_js = GridJs(workbook)

# Step 3: Define a custom context‑menu that includes an "Export CSV" command
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]
```

**Por qué es importante:**  
Configurar `CustomContextMenu` reemplaza la lista predeterminada con la que proporciones. La cadena `"Export CSV"` es solo una etiqueta – el trabajo real ocurre cuando el usuario hace clic en ella, lo cual conectaremos en el siguiente paso.

> *Consejo profesional:* Mantén la lista corta. Un menú contextual desordenado anula el propósito de acciones rápidas.

---

## Exportar la cuadrícula a CSV con una descarga de Blob

Ahora que el elemento del menú existe, necesitamos un manejador JavaScript que se comunique con el servidor, obtenga el CSV, lo convierta en un **Blob** y fuerce la descarga. Aquí es donde aparece la frase **download CSV file blob**.

```python
# Step 4: Attach a JavaScript handler that runs when "Export CSV" is chosen.
#         The handler sends an AJAX request to a server endpoint,
#         receives the CSV file as a Blob, and triggers a download.
grid_js.CustomContextMenuHandler = """
function(action, cell) {
    if (action === "Export CSV") {
        fetch('/export/csv?sheet=' + cell.sheetName)
            .then(r => r.blob())
            .then(b => {
                const url = URL.createObjectURL(b);
                const a = document.createElement('a');
                a.href = url;
                a.download = cell.sheetName + ".csv";
                a.click();
            });
    }
}
"""
```

### Desglosando el manejador

| Línea | Qué hace |
|------|--------------|
| `fetch('/export/csv?sheet=' + cell.sheetName)` | Llama a una ruta Flask (`/export/csv`) pasando el nombre de la hoja como cadena de consulta. |
| `.then(r => r.blob())` | Convierte la respuesta HTTP a un **Blob** – esencialmente un contenedor binario para los datos CSV. |
| `URL.createObjectURL(b)` | Genera una URL temporal que el navegador puede tratar como un archivo. |
| `a.download = cell.sheetName + ".csv"` | Establece el nombre de archivo que el usuario verá en el cuadro de descarga. |
| `a.click()` | Hace clic programáticamente en el ancla oculta, provocando que el navegador descargue el Blob. |

> **¿Por qué usar un Blob?**  
> Los navegadores no pueden descargar directamente texto sin procesar devuelto por `fetch` sin convertirlo en algo similar a un archivo. El truco del Blob‑URL es la forma más fiable y compatible entre navegadores de activar un **download CSV file blob** sin refrescar la página.

---

## Configurar el backend Flask

El manejador del front‑end espera un endpoint en `/export/csv`. Aquí tienes una vista Flask mínima que toma el nombre de la hoja, extrae los datos del libro de trabajo y devuelve un CSV en streaming.

```python
from flask import Flask, request, Response
import csv
import io

app = Flask(__name__)

# Assume `workbook` is a global object we created earlier
# (in a real app you’d probably fetch it from a database or session)
@app.route('/export/csv')
def export_csv():
    sheet_name = request.args.get('sheet', 'default')
    # Retrieve the sheet data – this is pseudo‑code; replace with your actual API
    sheet = workbook.get_sheet(sheet_name)

    # Convert rows to CSV in memory
    output = io.StringIO()
    writer = csv.writer(output)
    writer.writerow(sheet.headers)          # Header row
    writer.writerows(sheet.rows)            # Data rows

    # Create a Flask response with the correct MIME type
    csv_bytes = output.getvalue().encode('utf-8')
    return Response(
        csv_bytes,
        mimetype='text/csv',
        headers={'Content-Disposition': f'attachment;filename={sheet_name}.csv'}
    )
```

### Puntos clave

- **`io.StringIO`** nos permite crear el CSV en memoria sin tocar el sistema de archivos.
- **`Content‑Disposition`** indica al navegador que el archivo es un adjunto y sugiere un nombre de archivo. Aunque el front‑end también establece `a.download`, tenerlo del lado del servidor ofrece una alternativa para clientes sin JavaScript.
- La ruta es deliberadamente simple; puedes añadir autenticación, verificaciones de permisos o streaming para conjuntos de datos muy grandes más adelante.

---

## Renderizar la cuadrícula en el cliente

Con el menú contextual y el backend listos, la pieza final es renderizar el componente GridJs y enviar el HTML/JS al navegador.

```python
# Step 5: Render the grid to obtain the full HTML/JS needed on the client side
html_output = grid_js.Render()
print(html_output)   # Sends the HTML/JS to the client (e.g., in a Flask view)
```

En una vista Flask típicamente harías:

```python
@app.route('/')
def index():
    html_output = grid_js.Render()
    return f"""
    <!doctype html>
    <html>
    <head>
        <title>Grid with Custom Context Menu</title>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
    </head>
    <body>
        {html_output}
    </body>
    </html>
    """
```

Cuando la página se carga, GridJs construye la tabla, inyecta el menú contextual personalizado y el manejador JavaScript que definimos antes está listo para ejecutarse. Haz clic derecho en cualquier celda, elige **Export CSV**, y observa cómo el navegador descarga un archivo con el nombre de la hoja.

---

## Ejemplo completo funcional (Todos los archivos)

A continuación tienes el código completo y ejecutable que puedes copiar y pegar en una nueva carpeta. Instala Flask (`pip install flask`) y ejecuta `python app.py`.

**`app.py`**

```python
from flask import Flask, request, Response
import csv, io

# Mock classes to simulate the GridJs wrapper – replace with the real library
class Workbook:
    def __init__(self):
        self.sheets = {"Sheet1": Sheet()}
    def get_sheet(self, name):
        return self.sheets.get(name, self.sheets["Sheet1"])

class Sheet:
    def __init__(self):
        self.headers = ["ID", "Name", "Score"]
        self.rows = [
            [1, "Alice", 85],
            [2, "Bob", 92],
            [3, "Charlie", 78],
        ]

class GridJs:
    def __init__(self, workbook):
        self.workbook = workbook
        self.CustomContextMenu = []
        self.CustomContextMenuHandler = ""
    def Render(self):
        # Very simplified HTML – real GridJs would generate a lot more
        return f'''
        <div id="grid"></div>
        <script>
            const grid = new gridjs.Grid({{
                columns: {self.workbook.get_sheet("Sheet1").headers},
                data: {self.workbook.get_sheet("Sheet1").rows},
                search: true,
                pagination: true,
                customContextMenu: {self.CustomContextMenu},
                customContextMenuHandler: {self.CustomContextMenuHandler}
            }}).render(document.getElementById("grid"));
        </script>
        '''

app = Flask(__name__)

# Initialise workbook and grid
workbook = Workbook()
grid_js = GridJs(workbook)

# ==== Step 3: Custom context menu ====
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]

# ==== Step 4: Handler that downloads a CSV blob ====
grid_js.CustomContextMenuHandler = """
function(action, cell) {
    if (action === "Export CSV") {
        fetch('/export/csv?sheet=' + cell.sheetName)
            .then(r => r.blob())
            .then(b => {
                const url = URL.createObjectURL(b);
                const a = document.createElement('a');
                a.href = url;
                a.download = cell.sheetName + ".csv";
                a.click();
            });
    }
}
"""

@app.route('/')
def index():
    html_output = grid_js.Render()
    return f'''
    <!doctype html>
    <html>
    <head>


## ¿Qué deberías aprender a continuación?


Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cargar archivos CSV con analizadores personalizados Aspose Cells Java](/cells/hindi/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)
- [Exportar CSV código Java](/cells/hindi/java/excel-import-export/csv-export-java-code/)
- [Exportar Excel CSV filas en blanco Aspose Cells Net](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}