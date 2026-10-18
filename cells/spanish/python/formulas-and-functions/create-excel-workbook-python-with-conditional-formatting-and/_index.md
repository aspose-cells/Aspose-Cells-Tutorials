---
category: general
date: 2026-10-04
description: Crear libro de Excel con Python usando Aspose.Cells. Aprende formato
  condicional de Excel con Python, color de fondo de celda con Python y formato de
  fecha de celdas con Python en un ejemplo completo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create Excel workbook python
- excel conditional formatting python
- cell background color python
- format cells date python
language: es
lastmod: 2026-10-04
og_description: Crear un libro de Excel con Python y Aspose.Cells. Este tutorial muestra
  formato condicional en Excel con Python, color de fondo de celda con Python y formato
  de fechas en celdas con Python paso a paso.
og_image_alt: Screenshot of an Excel workbook created with Python showing highlighted
  yesterday dates
og_title: Crear libro de Excel con Python – guía completa con formato condicional
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  headline: Create Excel workbook python with conditional formatting and cell background
    color
  type: TechArticle
- description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  name: Create Excel workbook python with conditional formatting and cell background
    color
  steps:
  - name: '**create Excel workbook python** using the Aspose.Cells library.'
    text: '**create Excel workbook python** using the Aspose.Cells library.'
  - name: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
    text: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
  - name: Set the **cell background color python** to pink (or any color you prefer).
    text: Set the **cell background color python** to pink (or any color you prefer).
  - name: '**format cells date python** so the dates appear in the standard Excel
      date style.'
    text: '**format cells date python** so the dates appear in the standard Excel
      date style.'
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Crear libro de Excel en Python con formato condicional y color de fondo de
  celda
url: /es/python/formulas-and-functions/create-excel-workbook-python-with-conditional-formatting-and/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear Excel workbook python con formato condicional y color de fondo de celda

Si necesitas **create Excel workbook python** rápidamente, esta guía te muestra exactamente cómo. Verás un ejemplo completo y ejecutable que agrega **excel conditional formatting python**, cambia el **cell background color python**, y **format cells date python** para resaltar “Yesterday”.  

En muchos escenarios de informes, la pista visual de una celda coloreada hace que los datos sean instantáneamente comprensibles. Este tutorial te guía a través de cada línea de código, explica por qué cada paso es importante y te brinda un script listo‑para‑ejecutar que puedes adaptar a tus propios proyectos.

## Lo que lograrás

1. **create Excel workbook python** usando la biblioteca Aspose.Cells.  
2. Aplicar **excel conditional formatting python** que resalta automáticamente las fechas que caen en “Yesterday”.  
3. Establecer el **cell background color python** a rosa (o cualquier color que prefieras).  
4. **format cells date python** para que las fechas aparezcan en el estilo de fecha estándar de Excel.  

No se requiere experiencia previa con Aspose.Cells — solo un entorno Python 3 funcional y acceso a pip.

## Requisitos previos

- Python 3.8 o superior instalado.  
- `aspose-cells` y `aspose-pydrawing` paquetes instalados mediante `pip install aspose-cells aspose-pydrawing`.  
- Familiaridad básica con la sintaxis de Python y conceptos de Excel (workbooks, worksheets, cells).  

> **Consejo profesional:** Si ejecutas el script en un entorno virtual, evitas conflictos de versiones con otros proyectos.

## Paso 1: Configurar el proyecto e importar las clases requeridas

El primer paso cuando **create Excel workbook python** es importar las clases de Aspose.Cells que necesitarás. Estas clases te dan acceso directo a la creación de libros, formato condicional y estilo.

```python
# Import Aspose.Cells core classes
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)

# Import Aspose.PyDrawing for color handling
from aspose.pydrawing import Color

# Standard library for date values
from datetime import datetime
```

*Por qué es importante:* Importar solo los símbolos necesarios mantiene el espacio de nombres ordenado y hace que el script sea más fácil de leer. `Workbook` es el punto de entrada para **create Excel workbook python**, mientras que `FormatConditionType` y `TimePeriodType` son esenciales para **excel conditional formatting python**.

## Paso 2: Crear un nuevo libro y obtener la primera hoja de cálculo

Ahora realmente **create Excel workbook python**. El constructor `Workbook()` te brinda un archivo Excel vacío con una hoja de cálculo predeterminada.

```python
# Step 2: Initialize a new workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Explicación:* Cada archivo Excel comienza con al menos una hoja de cálculo. Por defecto Aspose.Cells la nombra “Sheet1”. Puedes agregar más hojas más tarde, pero para esta demostración una sola hoja mantiene el ejemplo enfocado.

## Paso 3: Definir el rango objetivo para el formato condicional

El formato condicional funciona sobre un rango rectangular. Aquí elegimos el rango `I19:K20`, que nos brinda tres columnas y dos filas para trabajar.

```python
# Define the range that will receive conditional formatting
target_range = "I19:K20"

# Retrieve (or create) the ConditionalFormatting collection for that range
conditional_formatting = worksheet.conditional_formattings.get(target_range)
```

*Por qué lo hacemos:* El método `get` devuelve un objeto `ConditionalFormatting` vinculado al rango especificado. Si el rango aún no tiene formato, Aspose.Cells crea una nueva colección automáticamente.

## Paso 4: Añadir una condición TIME_PERIOD y establecer el color de fondo

Este es el núcleo de **excel conditional formatting python**. Añadimos una regla `TIME_PERIOD` que resalta celdas que contienen fechas que caen en “Yesterday”.

```python
# Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Access the newly created condition
condition = conditional_formatting[condition_index]

# Configure the condition to target “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Set the cell background color – this is the cell background color python part
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
```

*Profundización:*  
- `FormatConditionType.TIME_PERIOD` indica a Excel que evalúe fechas relativas a la fecha actual.  
- `TimePeriodType.YESTERDAY` es un enum incorporado que se actualiza automáticamente cada día, de modo que el libro siempre resalta el “Yesterday” más reciente.  
- Al establecer `background_color` a `Color.pink` y el patrón a `SOLID`, logramos el efecto **cell background color python** sin código VBA adicional.

## Paso 5: Poblar el rango con fechas de muestra y aplicar formato de fecha

Para ver el formato condicional en acción, necesitamos valores de fecha reales. También necesitamos **format cells date python** para que Excel los trate como fechas y no como números simples.

```python
# Helper function to set a cell's date style and value
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    # Excel’s built‑in date format code 30 = "m/d/yy"
    style.number = 30
    cell.set_style(style)
    cell.put_value(date_value)

# Populate I19 with a date that is “yesterday” relative to the sample data
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”

# Populate K20 with another arbitrary date
set_date("K20", datetime(2008, 8, 3))    # Not “yesterday”
```

*Explicación:*  
- La línea `style.number = 30` es el paso **format cells date python**. El código de formato 30 corresponde al formato de fecha corta (`m/d/yy`).  
- Usar una función auxiliar mantiene el código DRY (Don’t Repeat Yourself) y facilita agregar más fechas más adelante.

## Paso 6: Añadir una etiqueta descriptiva

Una pequeña etiqueta ayuda a cualquiera que abra el libro a entender por qué las celdas están coloreadas.

```python
# Place a label next to the formatted range
worksheet.cells.get("I20").put_value("Yesterday")
```

## Paso 7: Guardar el libro en disco

Finalmente, **create Excel workbook python** en disco llamando a `save`. La constante `SaveFormat.XLSX` garantiza que el archivo esté en el formato moderno Office Open XML.

```python
# Define the output path – replace YOUR_DIRECTORY with a real folder
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"

# Save the workbook
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Cuando abras `TimePeriodDemo.xlsx` en Excel, verás:

- Las celdas `I19` y `K20` contienen fechas.  
- La celda que coincide con “Yesterday” (en este ejemplo estático, `I19`) está resaltada en rosa.  
- La etiqueta “Yesterday” aparece en `I20`.  

> **Consejo:** Si ejecutas el script en un día diferente, el formato condicional sigue resaltando la celda cuya fecha es exactamente un día antes de la fecha actual del sistema — no se requieren cambios en el código.

## Script completo – listo para copiar y ejecutar

A continuación está el programa completo y autónomo que incorpora todos los pasos anteriores. Cópialo en un archivo llamado `conditional_format_demo.py`, ajusta `YOUR_DIRECTORY` y ejecútalo con `python conditional_format_demo.py`.

```python
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the cell range that will receive the conditional format
target_range = "I19:K20"
conditional_formatting = worksheet.conditional_formattings.get(target_range)

# Step 3: Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Step 4: Configure the condition to highlight “Yesterday” dates
condition = conditional_formatting[condition_index]
condition.time_period = TimePeriodType.YESTERDAY
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Helper to set date value and style
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    style.number = 30          # Excel date format code 30 = short date
    cell.set_style(style)
    cell.put_value(date_value)

# Step 5: Populate the range with sample dates (excel conditional formatting python)
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”
set_date("K20", datetime(2008, 8, 3))    # Another sample date

# Step 6: Add a label describing the condition
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### Salida esperada

Ejecutar el script imprime una línea de confirmación:

```
Workbook saved to YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Abrir el archivo generado muestra el fondo rosa en la celda que coincide con la regla “Yesterday”, confirmando que **excel conditional formatting python** y **cell background color python** están funcionando juntos.

## Variaciones comunes y casos límite

| Situation | How to adapt the code |
|-----------|-----------------------|
| **Color de resaltado diferente** | Cambiar `Color.pink` a cualquier otra constante `Color`, p.ej., `Color.light_green`. |
| **Resaltar “Today” en lugar de “Yesterday”** | Establecer `condition.time_period = TimePeriodType.TODAY`. |
| **Aplicar formato a una columna completa** | Usar un rango como `"A:A"` y ajustar la variable `target_range` en consecuencia. |
| **Usar un formato de fecha personalizado** | Reemplazar `style.number = 30` con `style.custom = "dd-mmm-yyyy"` para un formato más legible. |
| **Múltiples condiciones en el mismo rango** |  |

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Create Excel Workbook Python – Complete Guide with Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)
- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}