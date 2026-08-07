---
category: general
date: 2026-07-14
description: Crear código Python para un libro de Excel que establezca el color de
  fondo de las celdas, resalte celdas según un rango de fechas y guarde el libro como
  XLSX en minutos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- save workbook as xlsx
- highlight cells based on date range
- conditional formatting based on date
language: es
lastmod: 2026-07-14
og_description: Crea un libro de Excel con Python al instante. Aprende a establecer
  el color de fondo de las celdas, resaltar celdas según el rango de fechas y guardar
  el libro como XLSX con Aspose.Cells.
og_image_alt: Screenshot showing an Excel sheet created with Python highlighting yesterday's
  dates
og_title: Crear libro de Excel con Python – Formato condicional paso a paso
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Create Excel workbook Python code that sets cell background color,
    highlights cells based on date range, and saves workbook as XLSX in minutes.
  headline: Create Excel Workbook Python – Full Guide with Conditional Formatting
  type: TechArticle
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Crear libro de Excel con Python – Guía completa con formato condicional
url: /es/python/formatting/create-excel-workbook-python-full-guide-with-conditional-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear libro de Excel con Python – Guía completa con formato condicional

¿Alguna vez te has preguntado cómo **create excel workbook python** scripts que se vean pulidos sin abrir Excel manualmente? No estás solo. En muchos proyectos basados en datos necesitamos generar hojas de cálculo, colorear celdas y hasta marcar fechas que caen dentro de un rango específico, todo desde código Python puro.

En este tutorial recorreremos un ejemplo completo y listo para ejecutar que **creates an Excel workbook python** usando la biblioteca Aspose.Cells, **sets cell background color**, aplica **conditional formatting based on date** y finalmente **saves workbook as xlsx**. Al final tendrás un fragmento reutilizable que puedes insertar en cualquier canal de automatización.

## Lo que aprenderás

- Cómo inicializar un libro de trabajo y obtener la primera hoja de cálculo.  
- Una función auxiliar que agrega una colección de formato condicional para cualquier rango de celdas.  
- Uso de **conditional formatting based on date** para resaltar las entradas de ayer.  
- Ajustar el ancho de columnas para un diseño ordenado.  
- Persistir el resultado con **save workbook as xlsx**.  

No se requiere una instalación externa de Excel; Aspose.Cells maneja todo en memoria.

## Requisitos previos

- Python 3.8+ instalado.  
- `aspose-cells` paquete (`pip install aspose-cells`).  
- Familiaridad básica con funciones de Python y objetos datetime.  

Si nunca has usado Aspose.Cells, piénsalo como una API poderosa y pura de Python que imita el modelo de objetos de Excel. Es perfecta para generación del lado del servidor donde la suite Office no está disponible.

## Paso 1: Inicializar el libro de trabajo (Create Excel Workbook Python)

Lo primero: necesitamos **create excel workbook python** al estilo. Este paso crea un objeto de libro de trabajo vacío y nos dirige a la hoja de cálculo predeterminada.

```python
# Step 1 – create a fresh workbook and get the first sheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, Color, SaveFormat
from datetime import datetime

workbook = Workbook()                     # <-- creates a new Excel file in memory
worksheet = workbook.worksheets[0]        # the default (first) sheet
```

> **Por qué es importante:** La clase `Workbook` es el punto de entrada para cada operación de Excel. Al crearla programáticamente evitamos cualquier manipulación manual de archivos.

## Paso 2: Función auxiliar para agregar una colección de formato condicional (Set Cell Background Color)

El formato condicional vive dentro de una *colección* adjunta a un rango. Envolvamos ese código repetitivo en una pequeña función auxiliar que también nos permite **set cell background color** para todo el rango.

```python
def add_time_period_condition(cell_range: str, highlight_color: Color):
    """
    Adds a conditional‑formatting collection to `cell_range` and
    applies `highlight_color` as the base fill.
    """
    worksheet.conditional_formattings.add(cell_range)   # attach to the range
    cf = worksheet.conditional_formattings[-1]           # grab the newly added collection
    cf.style.background_color = highlight_color
    cf.style.pattern = BackgroundType.SOLID
    return cf
```

> **Consejo profesional:** Usar una función auxiliar mantiene tu flujo principal limpio y facilita reutilizar la misma lógica para varios rangos.

## Paso 3: Aplicar formato condicional basado en fecha (Highlight Cells Based on Date Range)

Ahora realmente **highlight cells based on date range**. El ejemplo se centra en “ayer”, pero puedes cambiar `TimePeriodType.YESTERDAY` por `TODAY`, `LAST_WEEK`, etc.

```python
# Step 3 – create a TIME_PERIOD rule for I19:K20 (yesterday)
cf = add_time_period_condition("I19:K20", Color.medium_sea_green)

condition_index = cf.add_condition(FormatConditionType.TIME_PERIOD)
condition = cf[condition_index]

# Define the visual style for the matching cells
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# The actual rule: any cell whose date is yesterday gets the pink fill
condition.time_period = TimePeriodType.YESTERDAY
```

> **¿Qué está sucediendo?**  
> 1. Primero damos a todo el rango un fondo verde neutro.  
> 2. Luego agregamos una condición `TIME_PERIOD` que sobrescribe el relleno con rosa **solo** cuando la fecha de la celda es igual a ayer.  
> 3. El enum `TimePeriodType` abstrae el cálculo de la fecha, por lo que no necesitas escribir lógica personalizada.

## Paso 4: Poblar fechas de ejemplo (Para que la regla pueda evaluarse)

Para ver la regla en acción, insertaremos un par de fechas en la hoja. Una cae dentro del rango de “ayer”, la otra no.

```python
# Populate I19 with a date that is yesterday (relative to the hard‑coded date)
date_cell = worksheet.cells.get("I19")
date_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008
date_style = date_cell.get_style()
date_style.number = 30                     # Excel’s built‑in date format
date_cell.set_style(date_style)

# Populate K20 with a date that is NOT yesterday
date_cell = worksheet.cells.get("K20")
date_cell.put_value(datetime(2008, 8, 3))    # 03‑Aug‑2008
date_style = date_cell.get_style()
date_style.number = 30
date_cell.set_style(date_style)

# Add a label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

> **Nota de caso límite:** Si tu libro de trabajo se abrirá en diferentes configuraciones regionales, considera usar `date_style.custom = "dd‑mm‑yyyy"` para imponer una visualización consistente.

## Paso 5: Ordenar el diseño (Auto‑Fit Columns)

Una hoja de cálculo apretada se ve poco profesional. Vamos a **adjust column width for a tidy output**.

```python
# Auto‑fit column L (index 12) to show the full content without truncation
worksheet.auto_fit_column(12)
```

> **¿Por qué auto‑fit?** Garantiza que cualquier etiqueta larga o fecha sea completamente visible, lo cual es especialmente importante cuando compartes el archivo con partes interesadas no técnicas.

## Paso 6: Guardar el libro de trabajo (Save Workbook As XLSX)

Finalmente, **save workbook as xlsx** a una ubicación de tu elección. La constante `SaveFormat.XLSX` indica a Aspose.Cells que escriba en el formato moderno OpenXML.

```python
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Resultado que deberías ver:**  
> - Las celdas I19 y K20 contienen fechas.  
> - I19 (ayer) está resaltada en rosa, mientras que K20 permanece verde.  
> - La columna L se expande automáticamente para ajustarse a la etiqueta “Yesterday”.  

Si abres `TimePeriodDemo.xlsx` en Excel, el formato condicional ya estará aplicado—no se necesitan pasos adicionales.

---

![Hoja de Excel que muestra la fecha de ayer resaltada](https://example.com/images/excel-demo.png "Captura de pantalla del archivo Excel generado con celdas resaltadas")

*La imagen anterior ilustra el libro de trabajo final; observa el resaltado rosa en la celda que contiene la fecha de ayer.*

## Recapitulación: Lo que logramos

- **Created an Excel workbook python** desde cero usando Aspose.Cells.  
- **Set cell background color** para todo un rango para dar a la hoja una pista visual.  
- Aplicó **conditional formatting based on date** para marcar automáticamente las entradas de ayer.  
- **Saved workbook as xlsx**, listo para distribución o procesamiento adicional.  

Todo esto se hizo en menos de 60 líneas de Python, y el código funciona en cualquier plataforma que soporte el runtime de Aspose.Cells.

## Próximos pasos y temas relacionados

Si encontraste esto útil, también podrías explorar:

- **set cell background color** para filas completas según valores de estado (p.ej., “Completed”, “Pending”).  
- Usando **highlight cells based on date range** para crear ventanas móviles (últimos 7 días, mes actual).  
- Exportando a otros formatos como **CSV** o **PDF** con `SaveFormat.CSV` o `SaveFormat.PDF`.  
- Agregando **charts** programáticamente para visualizar los datos que acabas de formatear.  

Siéntete libre de ajustar la lógica de fechas, cambiar la paleta de colores o expandir el rango para cubrir columnas completas. El patrón sigue siendo el mismo: crear un libro de trabajo, adjuntar una colección de formato condicional, definir la regla y guardar.

¿Tienes preguntas sobre un caso de uso específico? Deja un comentario abajo, ¡y feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Automatización de Excel con Aspose.Cells .NET: Crear libro de trabajo y establecer enlaces externos](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Crear y guardar libro de Excel Aspose Cells Java](/cells/hongkong/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Crear y guardar libro de Excel Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}