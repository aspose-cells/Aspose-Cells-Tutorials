---
category: general
date: 2026-06-21
description: Guardar libro de trabajo como PDF usando Flask y Aspose.Cells en Python
  – aprende cómo convertir XLSX a PDF, ajustar automáticamente las columnas de Excel
  y devolver el archivo con flask send_file pdf.
draft: false
keywords:
- save workbook as pdf
- convert xlsx to pdf
- python excel to pdf
- auto fit excel columns
- flask send_file pdf
language: es
og_description: Guardar libro de trabajo como PDF en Python usando Flask. Este tutorial
  paso a paso muestra cómo convertir XLSX a PDF, ajustar automáticamente las columnas
  de Excel y servir el resultado con flask send_file pdf.
og_title: Guardar libro de trabajo como PDF con Flask – Guía completa de Python
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Save workbook as PDF using Flask and Aspose.Cells in Python – learn
    how to convert XLSX to PDF, auto‑fit Excel columns, and return the file with flask
    send_file pdf.
  headline: Save Workbook as PDF with Flask – Python Excel to PDF Guide
  type: TechArticle
- description: Save workbook as PDF using Flask and Aspose.Cells in Python – learn
    how to convert XLSX to PDF, auto‑fit Excel columns, and return the file with flask
    send_file pdf.
  name: Save Workbook as PDF with Flask – Python Excel to PDF Guide
  steps:
  - name: Why Each Piece Matters
    text: '- **`request.files.get("file")`** – Safely fetches the uploaded file; using
      `.get` avoids a `KeyError` if the field is missing. - **`io.BytesIO`** – Keeps
      everything in RAM, so we never write temporary files to disk. This is crucial
      for scalability. - **`auto_fit_columns()`** – Without this, column '
  - name: Manual Test with cURL
    text: '```bash curl -X POST http://localhost:5000/convert  -F "file=@sample.xlsx"  -o
      result.pdf ```'
  - name: Automated Test with Python’s `requests`
    text: '```python import requests'
  type: HowTo
tags:
- flask
- python
- excel
- pdf
- aspose-cells
title: 'Guardar libro de trabajo como PDF con Flask – Guía de Python: de Excel a PDF'
url: /es/python/import-and-export/save-workbook-as-pdf-with-flask-python-excel-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Guardar libro de Excel como PDF con Flask – Guía de Python Excel a PDF

¿Necesitas **guardar un libro como PDF** desde un servicio web? No eres el único que se pregunta cómo convertir un archivo Excel subido en un PDF elegante al instante. En esta guía recorreremos cómo guardar un libro como PDF usando Flask y Aspose.Cells, cubriendo también cómo **convertir XLSX a PDF**, ajustar automáticamente las columnas de Excel y, finalmente, entregar el resultado con `flask send_file pdf`.

Comenzaremos con un proyecto Flask nuevo, añadiremos algunos consejos de buenas prácticas y terminaremos con un endpoint completamente funcional que cualquier cliente puede invocar. Cuando termines, podrás transformar cualquier hoja de cálculo en un PDF con solo unas pocas líneas de código Python.

## Lo que necesitarás

- **Python 3.8+** (el código funciona en 3.9, 3.10 y versiones posteriores)
- **Flask** (`pip install flask`) – el framework web ligero que potencia nuestra API
- **Aspose.Cells for Python via .NET** (`pip install aspose-cells`) – la biblioteca que realmente lee XLSX y escribe PDF
- Un entendimiento básico de peticiones HTTP `POST` (nada complicado)

Si ya tienes estos componentes, genial—¡vamos al código! Si no, el paso “Instalar dependencias” te pondrá en marcha.

## Paso 1 – Configurar el proyecto Flask

Primero, crea una nueva carpeta para el proyecto y genera un entorno virtual. Esto mantiene nuestras dependencias ordenadas.

```bash
mkdir flask_excel_pdf && cd flask_excel_pdf
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate
pip install flask aspose-cells
```

Ahora crea un archivo llamado `app.py`. Aquí residirá toda la lógica de **save workbook as pdf**.

## Paso 2 – Inicializar la aplicación Flask

Empezamos importando los elementos que necesitamos y creando el objeto de la aplicación Flask. Observa lo conciso que es el bloque de importación—no hay módulos sin usar, lo que mantiene bajo el tiempo de arranque.

```python
# app.py
from flask import Flask, request, send_file
import aspose.cells as cells
import io

app = Flask(__name__)
```

> **Consejo profesional:** Mantén `app = Flask(__name__)` al inicio del archivo; facilita las pruebas posteriores con herramientas como `pytest-flask`.

## Paso 3 – Construir el endpoint de conversión (convert xlsx to pdf)

Este es el corazón del tutorial: un endpoint que acepta una hoja de cálculo vía `POST`, la carga en un libro de Aspose.Cells y la prepara para exportarla a PDF.

```python
@app.route("/convert", methods=["POST"])
def convert():
    # 1️⃣ Grab the uploaded file from the request
    uploaded = request.files.get("file")
    if not uploaded:
        return {"error": "No file provided"}, 400

    # 2️⃣ Read the file into memory (binary)
    file_bytes = uploaded.read()

    # 3️⃣ Load the spreadsheet into a workbook object
    workbook = cells.Workbook(io.BytesIO(file_bytes))

    # 4️⃣ Auto‑fit all columns in the first sheet (auto fit excel columns)
    workbook.worksheets[0].auto_fit_columns()

    # 5️⃣ Save the workbook as PDF into an in‑memory stream
    pdf_stream = io.BytesIO()
    workbook.save(pdf_stream, cells.SaveFormat.PDF)
    pdf_stream.seek(0)

    # 6️⃣ Return the PDF using flask send_file pdf
    return send_file(
        pdf_stream,
        mimetype="application/pdf",
        as_attachment=True,
        download_name="output.pdf"
    )
```

### Por qué cada pieza es importante

- **`request.files.get("file")`** – Obtiene de forma segura el archivo subido; usar `.get` evita un `KeyError` si el campo falta.
- **`io.BytesIO`** – Mantiene todo en RAM, de modo que nunca escribimos archivos temporales en disco. Esto es crucial para la escalabilidad.
- **`auto_fit_columns()`** – Sin esto, el ancho de las columnas suele quedar apretado en el PDF. El método expande cada columna para que se ajuste a su celda más larga, ofreciendo un aspecto profesional.
- **`workbook.save(..., cells.SaveFormat.PDF)`** – Esta única llamada realiza la conversión pesada de XLSX a PDF. Aspose.Cells gestiona fórmulas, gráficos e incluso celdas combinadas.
- **`flask send_file pdf`** – Envía el PDF de vuelta al cliente con los encabezados adecuados, provocando una descarga con el nombre `output.pdf`.

## Paso 4 – Ejecutar el servidor Flask

Añade la típica “guardia de ejecución” al final de `app.py` para que el script pueda ejecutarse directamente.

```python
if __name__ == "__main__":
    # Listening on all interfaces makes testing from Docker or another machine easy
    app.run(host="0.0.0.0", port=5000, debug=True)
```

Ejecutar `python app.py` iniciará el servidor en `http://localhost:5000`. La bandera `debug=True` es útil durante el desarrollo; recuerda desactivarla en producción.

## Paso 5 – Probar el endpoint (Manual y Automatizado)

### Prueba manual con cURL

```bash
curl -X POST http://localhost:5000/convert \
  -F "file=@sample.xlsx" \
  -o result.pdf
```

Si todo salió bien, `result.pdf` contendrá una versión bien formateada de `sample.xlsx`, con todas las columnas auto‑ajustadas.

### Prueba automatizada con `requests` de Python

```python
import requests

with open("sample.xlsx", "rb") as f:
    response = requests.post(
        "http://localhost:5000/convert",
        files={"file": f}
    )
    response.raise_for_status()
    with open("downloaded.pdf", "wb") as out:
        out.write(response.content)

print("PDF saved as downloaded.pdf")
```

Ambos enfoques demuestran el flujo completo de **python excel to pdf**—desde la carga hasta la descarga—sin tocar nunca el sistema de archivos del servidor.

## Paso 6 – Casos límite y errores comunes

| Situación | Qué vigilar | Solución |
|-----------|-------------|----------|
| Archivos XLSX grandes ( > 50 MB ) | Presión de memoria en el servidor | Transmitir la carga a un archivo temporal y usar `Workbook(file_path)` en lugar de `BytesIO`. |
| Libro protegido con contraseña | `Workbook` lanza una excepción | Pasar la contraseña al constructor de `Workbook`: `Workbook(io.BytesIO(file_bytes), cells.LoadOptions(password="secret"))`. |
| Falta `auto_fit_columns()` | Las columnas del PDF aparecen truncadas | Siempre llama a `auto_fit_columns()` **antes** de `save()`. |
| El cliente espera un error en JSON | Flask devuelve una página HTML de error | Devuelve un diccionario JSON con el código de estado adecuado como se muestra en el endpoint (línea `return {"error": "No file provided"}, 400`). |

Anticipando estos escenarios, tu API se mantiene robusta y fácil de usar.

## Paso 7 – Desplegar en producción

Cuando estés listo para lanzar, considera estos ajustes de nivel producción:

- **Usar un servidor WSGI** como `gunicorn` (`gunicorn -w 4 app:app`) en lugar del servidor integrado de Flask.
- **Habilitar HTTPS** mediante un proxy inverso (NGINX) para proteger las cargas de archivos.
- **Establecer un límite de tamaño de petición** (`app.config["MAX_CONTENT_LENGTH"] = 20 * 1024 * 1024`) para evitar ataques de denegación de servicio.
- **Registrar errores** con un logger estructurado (p. ej., `structlog`) para poder rastrear fallos de conversión.

Todos estos pasos conservan la lógica central de **save workbook as pdf** mientras hacen que el servicio esté listo para producción.

## Salida esperada

Al invocar el endpoint `/convert` con un archivo XLSX válido, la respuesta:

1. Tendrá un encabezado `Content-Type: application/pdf`.
2. Pedirá al navegador (o cliente) descargar un archivo llamado `output.pdf`.
3. Renderizará la hoja de cálculo con columnas dimensionadas automáticamente a su contenido, gracias a la llamada `auto fit excel columns`.

Abre el PDF descargado—deberías ver cada columna completamente visible, fórmulas evaluadas y cualquier imagen incrustada preservada.

## Conclusión

Ahora dispones de un ejemplo completo y listo para producción que **save workbook as pdf** usando Flask, Aspose.Cells y puro Python. El tutorial cubrió todo, desde la configuración del entorno, **convert xlsx to pdf**, ajuste automático de columnas, y la entrega del resultado con `flask send_file pdf`.

A continuación, podrías explorar agregar **estilos personalizados**, combinar celdas o incluso convertir varias hojas de cálculo en un único PDF multipágina. El mismo patrón funciona para otros tipos de archivo—solo cambia el enum `SaveFormat`.

¿Tienes preguntas sobre casos límite o despliegue? Deja un comentario abajo, ¡y feliz codificación!

## ¿Qué deberías aprender después?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques alternativos en tus propios proyectos.

- [Cómo guardar páginas específicas de un archivo Excel como PDF usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/save-specific-excel-pages-pdf-aspose-cells-net/)
- [Guardar libro de Excel como PDF con fuentes personalizadas usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/save-excel-workbook-pdf-custom-fonts-aspose-cells-net/)
- [Convertir Excel a PDF con ajuste de columnas en Java usando Aspose.Cells](/cells/english/java/workbook-operations/convert-excel-to-pdf-fit-columns-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}