---
category: general
date: 2026-07-03
description: Tutorial de Aspose Cells GridJs que muestra cómo exportar datos de Excel
  a JSON y exportar la hoja de cálculo a JSON de manera eficiente usando carga diferida.
draft: false
keywords:
- aspose cells gridjs tutorial
- export excel data json
- export worksheet to json
language: es
og_description: El tutorial de Aspose Cells GridJs explica cómo exportar datos de
  Excel a JSON y exportar la hoja de cálculo a JSON con carga diferida para hojas
  de cálculo grandes.
og_title: Tutorial de Aspose Cells GridJs – Exportar datos de Excel a JSON
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Aspose Cells GridJs tutorial showing how to export Excel data JSON
    and export worksheet to JSON efficiently using lazy loading.
  headline: Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading
  type: TechArticle
- description: Aspose Cells GridJs tutorial showing how to export Excel data JSON
    and export worksheet to JSON efficiently using lazy loading.
  name: Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed locally. - `asposecells` package (you can `pip
      install aspose-cells`). - A sizeable Excel file (e.g., `large-data.xlsx`) placed
      in a known directory. - Basic familiarity with Python and web development concepts.'
  - name: Exporting a specific worksheet
    text: 'The example above always uses the first worksheet (`Worksheets[0]`). To
      export a different sheet, simply change the index or use the sheet name:'
  - name: Changing the chunk size for massive files
    text: For files with millions of rows, a chunk size of 500 may still be too small,
      causing many round‑trips. You can increase it to 2000 or more, but remember
      that larger chunks consume more bandwidth per request.
  - name: Exporting to a stream instead of a file
    text: 'If your API returns the JSON directly, you don’t need to write to disk:'
  - name: Handling formulas and formatting
    text: 'By default, `ExportGridJsJson` includes the calculated values of formulas.
      If you need raw formulas instead, set:'
  type: HowTo
tags:
- Aspose.Cells
- Python
- GridJs
- JSON export
title: Tutorial de Aspose Cells GridJs – Exportar datos de Excel a JSON con carga
  diferida
url: /es/python/import-and-export/aspose-cells-gridjs-tutorial-export-excel-data-to-json-with/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutorial de Aspose Cells GridJs – Exportar datos de Excel a JSON con carga diferida

¿Alguna vez te has preguntado cómo **exportar datos de Excel a JSON** desde una hoja de cálculo masiva sin colapsar el navegador? En este tutorial de Aspose Cells GridJs recorreremos una solución completa, lista para ejecutar, que te permite **exportar la hoja de cálculo a JSON** usando carga diferida, de modo que solo se obtengan las filas que necesitas bajo demanda.

Si has estado lidiando con archivos `.xlsx` enormes y el lado del cliente se congela, no estás solo. ¿La buena noticia? El enfoque que presentamos aquí es ligero y escalable, y puedes incorporarlo en cualquier proyecto Python que ya utilice la biblioteca Aspose.Cells.

## Qué cubre esta guía

En los próximos minutos aprenderás a:

1. Cargar un libro de trabajo grande con Aspose.Cells.  
2. Activar la carga diferida de GridJs para que el servidor transmita filas en bloques.  
3. Exportar la configuración de GridJs a un archivo JSON que el front‑end pueda consumir.  
4. Ajustar el tamaño del bloque para un rendimiento óptimo.  
5. Verificar la salida e integrarla con una página HTML sencilla.

Sin servicios externos, sin trucos ocultos—solo Python puro y la API de Aspose.Cells. Al final tendrás una **pipeline completa para exportar hoja de cálculo a JSON** que podrás adaptar a dashboards, herramientas de informes o cualquier componente de cuadrícula de datos.

### Requisitos previos

- Python 3.8+ instalado localmente.  
- Paquete `asposecells` (puedes `pip install aspose-cells`).  
- Un archivo Excel de tamaño considerable (p. ej., `large-data.xlsx`) colocado en un directorio conocido.  
- Familiaridad básica con Python y conceptos de desarrollo web.

Si alguno de estos puntos te resulta desconocido, no te alarmes—cada paso incluye una breve explicación del “por qué” para que comprendas la lógica detrás del código.

---

## Paso 1: Instalar e importar Aspose.Cells

Primero lo primero, necesitamos la biblioteca Aspose.Cells. Es un producto comercial, pero una prueba gratuita funciona para desarrollo.

```bash
pip install aspose-cells
```

Ahora importa las clases necesarias en tu script.

```python
# Step 1: Import the Aspose.Cells workbook class
import asposecells
from asposecells import Workbook
```

> **Por qué es importante:** Importar `Workbook` te brinda acceso al motor de alto rendimiento que lee archivos Excel directamente en memoria, evitando el método más lento `openpyxl`.

## Paso 2: Cargar el libro de trabajo que contiene el conjunto de datos grande

Con la biblioteca lista, indícale tu archivo Excel. La ruta puede ser absoluta o relativa; solo asegúrate de que el archivo exista.

```python
# Step 2: Load the workbook that contains a large data set
workbook = Workbook("YOUR_DIRECTORY/large-data.xlsx")
```

> **Consejo profesional:** Si tu libro de trabajo supera algunos cientos de megabytes, considera aumentar el límite de memoria del proceso Python o usar un intérprete de 64 bits para evitar `MemoryError`.

## Paso 3: Habilitar la carga diferida de GridJs

GridJs es el componente de cuadrícula JavaScript de Aspose. La carga diferida indica al servidor que envíe solo un subconjunto de filas—perfecto para hojas enormes.

```python
# Step 3: Enable lazy loading so the client fetches rows on demand
grid_options = workbook.Worksheets[0].Cells.GridJsOptions
grid_options.LazyLoading = True                 # fetch rows/columns only when needed
grid_options.LazyLoadingChunkSize = 500         # rows per server request
```

> **¿Por qué carga diferida?** Sin ella, toda la hoja de cálculo se serializaría a JSON de una sola vez, lo que fácilmente puede superar los límites de memoria del navegador. Al establecer `LazyLoadingChunkSize` en 500, cada solicitud lleva una carga manejable.

## Paso 4: Exportar la configuración de GridJs a JSON

Ahora le pedimos a Aspose que genere el JSON que el componente GridJs del front‑end espera. Este es el núcleo de la operación **exportar datos de Excel a JSON**.

```python
# Step 4: Export the GridJs configuration to a JSON file for the client side
grid_json = workbook.Worksheets[0].Cells.ExportGridJsJson()
```

El método `ExportGridJsJson` devuelve un objeto `bytes` que contiene la representación JSON de la hoja de cálculo, listo para guardarse o transmitirse.

## Paso 5: Escribir el JSON en un archivo (o transmitirlo)

Para una prueba rápida, escribe el JSON en disco. En una API de producción lo devolverías directamente desde un endpoint Flask/Django.

```python
# Step 5: Persist the JSON to a file
output_path = "YOUR_DIRECTORY/lazygrid.json"
with open(output_path, "wb") as f:
    f.write(grid_json)

print(f"✅ GridJs JSON exported successfully to {output_path}")
```

> **Lo que verás:** Al abrir `lazygrid.json` se revela una estructura con `columns`, `rows` y metadatos de paginación. El arreglo `rows` estará inicialmente vacío; GridJs solicitará el primer bloque cuando la página se cargue.

## Paso 6: Vincular el JSON a una página HTML sencilla (opcional)

Si deseas ver la cuadrícula en acción, crea un pequeño archivo HTML que cargue GridJs desde un CDN y lo apunte al JSON generado.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Lazy‑Loaded GridJs Demo</title>
    <link href="https://unpkg.com/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
    <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
</head>
<body>
    <div id="wrapper"></div>
    <script>
        // Fetch the lazy‑loaded JSON and initialize GridJs
        fetch('lazygrid.json')
            .then(r => r.json())
            .then(config => {
                new gridjs.Grid({
                    ...config,
                    server: {
                        url: 'lazygrid.json',
                        then: data => data
                    }
                }).render(document.getElementById('wrapper'));
            });
    </script>
</body>
</html>
```

> **¿Por qué incluir esto?** Demuestra el recorrido completo: Python crea el JSON, el navegador lo recupera y GridJs renderiza los datos bloque a bloque. Ahora puedes experimentar con diferentes valores de `LazyLoadingChunkSize` para encontrar el punto óptimo para tu red.

## Paso 7: Verificar y solucionar problemas

Ejecuta el script Python:

```bash
python export_lazy_grid.py
```

Deberías ver el mensaje de éxito y un archivo `lazygrid.json`. Abre el archivo HTML en un navegador; la cuadrícula debería mostrar las primeras 500 filas al instante, con controles de paginación para cargar más.

Si la cuadrícula aparece vacía:

- **Verifica el tamaño del archivo JSON** – un archivo de cero bytes suele indicar que la ruta del libro de trabajo es incorrecta.  
- **Confirma que la carga diferida está habilitada** – la bandera `LazyLoading` debe ser `True`.  
- **Inspecciona la consola del navegador** – cualquier error CORS o 404 indica que el JSON no se está sirviendo correctamente.

---

## Variaciones comunes y casos límite

### Exportar una hoja de cálculo específica

El ejemplo anterior siempre usa la primera hoja (`Worksheets[0]`). Para exportar una hoja distinta, simplemente cambia el índice o usa el nombre de la hoja:

```python
sheet = workbook.Worksheets["DataSheet"]   # by name
grid_options = sheet.Cells.GridJsOptions
grid_json = sheet.Cells.ExportGridJsJson()
```

### Cambiar el tamaño del bloque para archivos masivos

Para archivos con millones de filas, un tamaño de bloque de 500 puede seguir siendo demasiado pequeño, provocando muchos viajes de ida y vuelta. Puedes aumentarlo a 2000 o más, pero recuerda que los bloques más grandes consumen más ancho de banda por solicitud.

```python
grid_options.LazyLoadingChunkSize = 2000
```

### Exportar a un flujo en lugar de a un archivo

Si tu API devuelve el JSON directamente, no necesitas escribirlo en disco:

```python
from flask import Flask, Response
app = Flask(__name__)

@app.route("/api/gridjson")
def gridjson():
    json_bytes = workbook.Worksheets[0].Cells.ExportGridJsJson()
    return Response(json_bytes, mimetype="application/json")
```

### Manejo de fórmulas y formato

Por defecto, `ExportGridJsJson` incluye los valores calculados de las fórmulas. Si necesitas las fórmulas sin calcular, establece:

```python
grid_options.ExportFormulas = True
```

---

## Conclusión

En este **tutorial de Aspose Cells GridJs** cubrimos todo lo necesario para **exportar datos de Excel a JSON** y **exportar hoja de cálculo a JSON** con carga diferida. Desde la instalación de Aspose.Cells, la activación de la carga diferida, la generación del JSON, hasta su integración con una página HTML sencilla, ahora dispones de un patrón full‑stack que escala con elegancia frente a hojas de cálculo masivas.

Pruébalo—ajusta el tamaño del bloque, apunta a distintas hojas, o integra el endpoint en una aplicación Flask o Django. Las posibilidades son infinitas y las mejoras de rendimiento son inmediatas.

¿Listo para el siguiente paso? Prueba añadir ordenación de columnas, renderizadores de celdas personalizados o incluso filtrado del lado del servidor para que tu cuadrícula GridJs sea realmente interactiva. Si encuentras algún obstáculo, deja un comentario abajo; ¡feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Import JSON Data into Excel Using Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Load CSV & Export to JSON Using Aspose.Cells for .NET&#58; A Comprehensive Guide](/cells/english/net/import-export/load-csv-export-json-aspose-cells-dotnet/)
- [Export Excel Data Using Aspose.Cells .NET&#58; A Complete Guide for Seamless Data Export](/cells/english/net/import-export/export-excel-data-aspose-cells-net-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}