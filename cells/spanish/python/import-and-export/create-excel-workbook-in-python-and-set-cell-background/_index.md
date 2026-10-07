---
category: general
date: 2026-10-07
description: Crear un libro de Excel en Python, establecer el color de fondo de una
  celda, ajustar automáticamente el ancho de las columnas y rellenar fechas en Excel
  con un ejemplo de código conciso.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- auto fit excel columns
- populate dates in excel
- how to create excel
language: es
lastmod: 2026-10-07
og_description: Crea un libro de Excel en Python, luego establece el color de fondo
  de las celdas, ajusta automáticamente el ancho de las columnas y rellena fechas
  en Excel. Sigue esta guía paso a paso para generar un archivo TimePeriodDemo.xlsx.
og_image_alt: Screenshot of a Python‑generated Excel workbook with pink highlighted
  cells
og_title: Crear libro de Excel en Python – establecer fondo y ajuste automático
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  headline: Create Excel workbook in Python and set cell background
  type: TechArticle
- description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  name: Create Excel workbook in Python and set cell background
  steps:
  - name: Import required namespaces and define a helper function
    text: '```python # Step 1: Import Aspose.Cells classes and supporting modules
      from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType,
      SaveFormat from aspose.pydrawing import Color from datetime import datetime
      import os ```'
  - name: Create the workbook and get the first worksheet
    text: '```python def create_workbook(): # Step 2: Instantiate a new workbook (empty
      Excel file) book = Workbook() # Aspose.Cells creates a default worksheet; we
      retrieve it for further work sheet = book.worksheets[0] return book, sheet ```'
  - name: Set cell background color with a conditional format
    text: '```python def add_yesterday_rule(sheet): # Define a conditional format
      for the range I19:K20 (Yesterday) conds = sheet.get_range("I19:K20").format_conditions
      idx = conds.add_condition(FormatConditionType.TIME_PERIOD) cond = conds[idx]'
  - name: Populate dates in Excel
    text: '```python def populate_sample_dates(sheet): # Insert a date that falls
      on yesterday relative to the demo data cell = sheet.cells.get("I19") cell.put_value(datetime(2008,
      7, 30)) # sample date cell.style.number = 30 # Excel’s date format ID cell.set_style(cell.style)'
  - name: Auto‑fit Excel columns for better visibility
    text: '```python def auto_fit_columns(sheet): # Auto‑fit column L (index 12) so
      the content is fully visible sheet.auto_fit_column(12) # <-- auto fit excel
      columns ```'
  - name: Save the workbook
    text: '```python def save_workbook(book, filename="TimePeriodDemo.xlsx"): out_path
      = os.path.join("YOUR_DIRECTORY", filename) os.makedirs(os.path.dirname(out_path),
      exist_ok=True) book.save(out_path, SaveFormat.XLSX) print(f"Workbook saved to:
      {out_path}") ```'
  - name: Full script – putting it all together
    text: '```python def main(): # Create workbook and obtain the first worksheet
      book, sheet = create_workbook()'
  type: HowTo
tags:
- Excel
- Python
- Aspose.Cells
title: Crear libro de Excel en Python y establecer el fondo de la celda
url: /es/python/import-and-export/create-excel-workbook-in-python-and-set-cell-background/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear libro de Excel en Python y establecer el fondo de la celda

Crea un libro de Excel en Python y aplica formato condicional con solo unas pocas líneas de código. Este tutorial te muestra **cómo crear archivos excel** de forma programática, establecer el color de fondo de una celda, ajustar automáticamente el ancho de columnas de Excel y rellenar fechas en Excel usando la biblioteca Aspose.Cells.

Aprenderás a:
* Inicializar un libro de trabajo y obtener la primera hoja de cálculo.  
* Definir un formato condicional que resalte las fechas de “Yesterday”.  
* Insertar fechas de ejemplo en celdas específicas.  
* Ajustar automáticamente el ancho de columnas para que los datos se vean claramente.  
* Guardar el libro de trabajo en una carpeta elegida.

El único requisito previo es un entorno Python 3 funcionando con los paquetes `aspose-cells` y `aspose-pydrawing` instalados:

```bash
pip install aspose-cells aspose-pydrawing
```

---

## Crear libro de Excel en Python – paso a paso

Las siguientes secciones dividen el proceso en pasos manejables. Cada paso incluye el código necesario, una explicación de **por qué** es importante y un consejo para evitar errores comunes.

### Paso 1: Importar los espacios de nombres requeridos y definir una función auxiliar

```python
# Step 1: Import Aspose.Cells classes and supporting modules
from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime
import os
```

*Por qué es importante*: Importar las clases correctas te da acceso a la creación del libro de trabajo, al formato condicional y al manejo de colores.  
**Consejo profesional**: Mantén las importaciones al inicio del archivo; facilita la lectura del script y previene errores de importación circular.

### Paso 2: Crear el libro de trabajo y obtener la primera hoja de cálculo

```python
def create_workbook():
    # Step 2: Instantiate a new workbook (empty Excel file)
    book = Workbook()
    # Aspose.Cells creates a default worksheet; we retrieve it for further work
    sheet = book.worksheets[0]
    return book, sheet
```

El constructor `Workbook()` crea un libro de Excel vacío en memoria.  
**Por qué**: Empezar con un libro nuevo garantiza que no haya formatos residuales de ejecuciones anteriores.

### Paso 3: Establecer el color de fondo de la celda con un formato condicional

```python
def add_yesterday_rule(sheet):
    # Define a conditional format for the range I19:K20 (Yesterday)
    conds = sheet.get_range("I19:K20").format_conditions
    idx = conds.add_condition(FormatConditionType.TIME_PERIOD)
    cond = conds[idx]

    # Apply visual style – this is where we set the cell background color
    cond.style.background_color = Color.pink          # <-- set cell background color
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

*Por qué*: Usar una condición de **periodo de tiempo** resalta automáticamente cualquier celda que contenga la fecha de ayer, eliminando la necesidad de verificaciones manuales de fechas.  
**Consejo**: `Color.pink` es solo un ejemplo; puedes usar cualquier objeto `Color` (`Color.yellow`, `Color.light_green`, etc.).

### Paso 4: Rellenar fechas en Excel

```python
def populate_sample_dates(sheet):
    # Insert a date that falls on yesterday relative to the demo data
    cell = sheet.cells.get("I19")
    cell.put_value(datetime(2008, 7, 30))   # sample date
    cell.style.number = 30                 # Excel’s date format ID
    cell.set_style(cell.style)

    # Insert another date outside the “Yesterday” range
    cell = sheet.cells.get("K20")
    cell.put_value(datetime(2008, 8, 3))
    cell.style.number = 30
    cell.set_style(cell.style)

    # Add a label for the rule
    sheet.cells.get("I20").put_value("Yesterday")
```

Aquí **rellenamos fechas en Excel** en las celdas `I19` y `K20`. La primera fecha activará el formato condicional, mientras que la segunda no lo hará.  
**Por qué es importante**: Demostrar valores que coinciden y que no coinciden te ayuda a verificar que la regla funciona como se espera.

### Paso 5: Ajustar automáticamente el ancho de columnas de Excel para mejor visibilidad

```python
def auto_fit_columns(sheet):
    # Auto‑fit column L (index 12) so the content is fully visible
    sheet.auto_fit_column(12)   # <-- auto fit excel columns
```

`auto_fit_column` ajusta el ancho de la columna según el valor de celda más largo.  
**Consejo**: Llama a este método después de haber escrito todos los datos; de lo contrario, el ancho podría calcularse sobre contenido incompleto.

### Paso 6: Guardar el libro de trabajo

```python
def save_workbook(book, filename="TimePeriodDemo.xlsx"):
    out_path = os.path.join("YOUR_DIRECTORY", filename)
    os.makedirs(os.path.dirname(out_path), exist_ok=True)
    book.save(out_path, SaveFormat.XLSX)
    print(f"Workbook saved to: {out_path}")
```

Guardar el archivo escribe el libro de trabajo en memoria en el disco en el formato XLSX moderno.

### Script completo – juntándolo todo

```python
def main():
    # Create workbook and obtain the first worksheet
    book, sheet = create_workbook()

    # Apply conditional formatting (set cell background color)
    add_yesterday_rule(sheet)

    # Populate the demo dates (populate dates in excel)
    populate_sample_dates(sheet)

    # Auto‑fit the relevant column (auto fit excel columns)
    auto_fit_columns(sheet)

    # Persist the file
    save_workbook(book)

if __name__ == "__main__":
    main()
```

**Salida esperada**

```
Workbook saved to: YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Abre el archivo generado en Excel – las celdas `I19:K20` mostrarán un fondo rosa para la fecha que corresponde a “Yesterday”, y la columna L será lo suficientemente ancha para mostrar la etiqueta sin recortes.

---

## Por qué este enfoque funciona mejor

* **Flujo de trabajo de una sola pasada** – Todas las operaciones se realizan sobre la misma instancia de `Workbook`, evitando I/O innecesario.  
* **Formato condicional** – Usar `FormatConditionType.TIME_PERIOD` permite que Excel maneje la lógica de fechas, lo que es más fiable que escribir verificaciones de fechas personalizadas en Python.  
* **Estilizado explícito** – Configurar `background_color` y `pattern` garantiza el resultado visual en todas las versiones de Excel.  
* **Auto‑fit después de los datos**

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Crear libro de Excel Python – Guía completa](/cells/english/python/import-and-export/create-excel-workbook-python-full-guide/)
- [Crear libro de Excel Python – Guía paso a paso completa](/cells/english/python/import-and-export/create-excel-workbook-python-complete-step-by-step-guide/)
- [Crear libro de Excel Python – Guía completa con Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}