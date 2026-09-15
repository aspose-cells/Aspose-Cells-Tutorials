---
category: general
date: 2026-09-15
description: Aprende cómo aplicar formato condicional por período de tiempo y guardar
  el libro de trabajo como XLSX con Aspose.Cells en Python. Incluye código paso a
  paso.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- time period conditional formatting
- save workbook as xlsx
- how to create excel workbook python
- how to highlight yesterday in excel
- add conditional formatting python
language: es
lastmod: 2026-09-15
og_description: Aplica formato condicional de período de tiempo en Excel usando Python
  y guarda el libro de trabajo como XLSX. Sigue esta guía completa de Aspose.Cells.
og_image_alt: Screenshot of an Excel sheet where the cells for yesterday are highlighted
  in pink
og_title: Aplicar formato condicional de período de tiempo en Excel con Python
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  headline: How to apply time period conditional formatting in Excel using Python
  type: TechArticle
- description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  name: How to apply time period conditional formatting in Excel using Python
  steps:
  - name: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
    text: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
  - name: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
    text: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
  - name: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
    text: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
  - name: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
    text: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
  - name: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
    text: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
  - name: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
    text: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
  - name: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
    text: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
  - name: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
    text: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
  - name: The cell `I20` shows the text “Yesterday”.
    text: The cell `I20` shows the text “Yesterday”.
  - name: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
    text: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Cómo aplicar formato condicional de período de tiempo en Excel usando Python
url: /es/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo aplicar formato condicional de período de tiempo en Excel usando Python

Si necesitas **formato condicional de período de tiempo** en un archivo Excel, este tutorial te muestra exactamente cómo hacerlo con Python. Verás un ejemplo completo y ejecutable que crea un libro de trabajo, resalta las fechas de ayer y **guarda el libro de trabajo como XLSX** en solo unas pocas líneas de código.

El formato condicional es una forma poderosa de llamar la atención sobre datos que cumplen una regla específica. En esta guía nos enfocamos en el período de tiempo “Yesterday”, pero el mismo patrón funciona para otros períodos incorporados como Today, LastWeek y NextMonth. Al final del tutorial podrás **how to create excel workbook python**‑style scripts que estén listos para producción.

## Requisitos previos

- Python 3.8+ instalado  
- `aspose-cells` y paquetes `aspose-pydrawing` (`pip install aspose-cells aspose-pydrawing`)  
- Familiaridad básica con la sintaxis de Python  

No se requiere ninguna instalación adicional de Office porque Aspose.Cells maneja la generación del archivo internamente.

## Formato condicional de período de tiempo con Aspose.Cells en Python

Esta sección recorre cada línea de código necesaria para la tarea principal. El bloque de código a continuación es el script completo; los comentarios explican el propósito de cada paso.

```python
# -*- coding: utf-8 -*-
"""
Apply time period conditional formatting to highlight yesterday's dates
and save the workbook as XLSX using Aspose.Cells for Python.
"""

from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the range that will receive the conditional formatting rule
cell_range = "I19:K20"
cond_format = worksheet.conditional_formattings.add(cell_range)

# Step 3: Add a TIME_PERIOD condition for “Yesterday” and style it
condition_index = cond_format.add_condition(FormatConditionType.TIME_PERIOD)
condition = cond_format[condition_index]
condition.style.background_color = Color.pink          # Highlight colour
condition.style.pattern = BackgroundType.SOLID        # Solid fill
condition.time_period = TimePeriodType.YESTERDAY      # Built‑in “Yesterday” period

# Step 4: Populate the range with sample dates (Excel number format 30 = short date)
date_cells = ["I19", "K20"]                           # Cells that will contain dates
sample_dates = [datetime(2008, 7, 30), datetime(2008, 8, 3)]
for cell_ref, date_val in zip(date_cells, sample_dates):
    cell = worksheet.cells.get(cell_ref)
    cell.put_value(date_val)                         # Write the Python datetime
    style = cell.get_style()
    style.number = 30                                 # Excel short date format
    cell.set_style(style)

# Step 5: Add a label so the user knows what the rule represents
worksheet.cells.get("I20").put_value("Yesterday")

# Step 6: Auto‑fit the column for better readability (column L is index 12)
worksheet.auto_fit_column(12)

# Step 7: Save the workbook – this demonstrates “save workbook as xlsx”
output_path = "TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

### Por qué cada paso es importante

1. **Creating the workbook** te brinda un archivo Excel en memoria que puedes manipular sin abrir Excel.  
2. **Defining the range** (`I19:K20`) indica a Aspose.Cells dónde se aplica la regla, manteniendo la lógica aislada.  
3. **Adding a TIME_PERIOD condition** utiliza la enumeración incorporada de Aspose `TimePeriodType.YESTERDAY`. Esto evita cálculos manuales de fechas y se actualiza automáticamente cuando el archivo se abre en un día diferente.  
4. **Setting the style** (`background_color` y `pattern`) determina cómo aparecen las celdas resaltadas. Usar `Color.pink` hace que la regla sea fácil de detectar.  
5. **Writing sample dates** con el formato numérico 30 asegura que Excel los muestre como fechas cortas en lugar de números de serie.  
6. **Auto‑fitting the column** mejora la legibilidad para cualquiera que abra el archivo más tarde.  
7. **Saving as XLSX** produce un archivo ampliamente compatible que puede abrirse en Excel, Google Sheets o cualquier programa de hoja de cálculo moderno.

## Cómo crear un libro de trabajo Excel al estilo Python con Aspose.Cells

El script anterior ya demuestra los pasos mínimos para **how to create excel workbook python**. En la práctica, podrías querer:

- Agregar varias hojas de cálculo (`workbook.worksheets.add("Report")`).  
- Poblar grandes tablas de datos con bucles o pandas DataFrames (`worksheet.cells.import_data_table`).  
- Aplicar formato adicional (fuentes, bordes) usando `cell.get_style()`.

Todas estas acciones siguen el mismo patrón: obtener el objeto, modificar sus propiedades y llamar a `set_style` o `save`.

## Añadir formato condicional Python – otros patrones útiles

Más allá del ejemplo “Yesterday”, Aspose.Cells admite varios tipos de formato condicional:

| FormatConditionType | Caso de uso típico |
|---------------------|--------------------|
| `FORMAT_CONDITION_TYPE_EXPRESSION` | Custom formulas (`=A1>100`) |
| `FORMAT_CONDITION_TYPE_CELL_VALUE` | Simple comparisons (`>`, `<`, `=`) |
| `FORMAT_CONDITION_TYPE_COLOR_SCALE` | Gradient colour scales |
| `FORMAT_CONDITION_TYPE_DATA_BAR`   | In‑cell bar visualisation |

Para **add conditional formatting python** para un umbral numérico, deberías reemplazar `FormatConditionType.TIME_PERIOD` por `FormatConditionType.CELL_VALUE` y establecer `condition.operator_type` y `condition.formula1`.

```python
# Example: highlight values greater than 500
idx = cond_format.add_condition(FormatConditionType.CELL_VALUE)
cond = cond_format[idx]
cond.operator_type = ConditionOperatorType.GREATER_THAN
cond.formula1 = "500"
cond.style.background_color = Color.light_green
```

## Guardar libro de trabajo como XLSX – mejores prácticas

Al **save workbook as xlsx**, considera:

- **Specifying the correct `SaveFormat`** (`SaveFormat.XLSX`) para evitar formatos heredados.  
- **Using a deterministic file name** si el script se ejecuta en un bucle (`f"report_{datetime.now():%Y%m%d}.xlsx"`).  
- **Closing resources** (`workbook.dispose()`) en servicios de larga duración para liberar memoria nativa.  

El ejemplo ya usa `SaveFormat.XLSX`, que produce un libro de trabajo moderno basado en zip que conserva todas las reglas de formato condicional.

## Resaltar ayer en Excel – pasos de verificación

Después de ejecutar el script, abre `TimePeriodExample.xlsx`:

1. Las celdas `I19` y `K20` contienen las fechas `30‑07‑2008` y `03‑08‑2008`.  
2. La celda `I20` muestra el texto “Yesterday”.  
3. Si cambias la fecha del sistema a **July 30 2008** y vuelves a abrir el archivo, las celdas con fechas coincidentes se rellenan automáticamente de rosa.  
4. Cambiar la fecha del sistema a cualquier otro día elimina el relleno rosa, confirmando que la regla reacciona a la lógica de **time period conditional formatting**.

## Errores comunes y cómo evitarlos

- **Missing `aspose-pydrawing`** – la clase `Color` se encuentra en este paquete; olvidar instalarlo genera un `ImportError`.  
- **Incorrect number format** – usar el formato General predeterminado muestra números de serie (p.ej., 39822). Siempre establece `style.number = 30` para fechas cortas.  
- **Range mismatch** – el rango de formato condicional debe incluir las celdas que deseas resaltar; de lo contrario la regla no tiene efecto.

## Consejo profesional: reutilizar la rutina de formato

Si necesitas la misma regla “Yesterday” en varios libros de trabajo, envuelve la lógica en una función auxiliar:

```python
def apply_yesterday_highlight(worksheet, address):
    cf = worksheet.conditional_formattings.add(address)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    cond = cf[idx]
    cond.style.background_color = Color.pink
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

Llama a `apply_yesterday_highlight(worksheet, "A1:A10")` donde sea necesario.

## Conclusión

Esta guía te mostró cómo implementar **time period conditional formatting** en Excel usando Python, cómo **save workbook as XLSX**, y cómo **highlight yesterday in Excel** con un único script reutilizable. Ahora tienes una base sólida para añadir código **add conditional formatting python** a cualquier proyecto de automatización, ya sea generando informes diarios, construyendo paneles de control o preparando exportaciones de datos.

**Próximos pasos**

- Explora otros valores de `TimePeriodType` como `TODAY` o `LAST_WEEK`.  
- Combina múltiples reglas condicionales en el mismo rango para obtener indicaciones visuales más ricas.  
- Integra la generación del libro de trabajo en un servicio web o trabajo programado.

¡Feliz codificación, y disfruta de la claridad visual que el formato condicional aporta a tu automatización de Excel!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Dominar el formato condicional en Excel usando Aspose.Cells .NET: una guía completa](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Dominar Aspose.Cells .NET: aplicar formato condicional a filas alternas en Excel](/cells/english/net/formatting/aspose-cells-net-conditional-formatting-alternate-rows/)
- [Dominar el formato condicional con fuentes personalizadas en Excel usando Aspose.Cells para .NET y C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}