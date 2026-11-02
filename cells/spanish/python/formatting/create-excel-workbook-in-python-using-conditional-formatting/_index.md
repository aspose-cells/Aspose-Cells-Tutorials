---
category: general
date: 2026-09-21
description: Aprende cómo crear un libro de Excel en Python, establecer el color de
  fondo de una celda y aplicar formato condicional basado en fechas con Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- excel conditional formatting python
- date based conditional formatting
language: es
lastmod: 2026-09-21
og_description: Crea un libro de Excel en Python, establece el color de fondo de la
  celda y aplica formato condicional basado en fechas usando Aspose.Cells. Sigue la
  guía paso a paso.
og_image_alt: Screenshot of an Excel sheet showing a yellow‑green cell background
  for yesterday's dates
og_title: Crear libro de Excel en Python con formato condicional
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to create Excel workbook in Python, set cell background color,
    and apply date based conditional formatting with Aspose.Cells.
  headline: Create Excel workbook in Python using conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Crear libro de Excel en Python usando formato condicional
url: /es/python/formatting/create-excel-workbook-in-python-using-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear libro de Excel en Python usando formato condicional

Si necesitas **create Excel workbook python** scripts que resalten fechas automáticamente, esta guía te muestra exactamente cómo. Verás cómo **set cell background color**, agregar una regla “Yesterday” y guardar el archivo, todo con Aspose.Cells para Python.

Trabajar con archivos Excel programáticamente a menudo implica repetir la misma lógica de formato en muchas hojas. Al final de este tutorial tendrás un patrón reutilizable para **excel conditional formatting python** que podrás incorporar en cualquier proyecto.

## Requisitos previos

- Python 3.8+ instalado  
- paquete `aspose-cells` (`pip install aspose-cells`)  
- Familiaridad básica con funciones de Python y el módulo datetime  

No se requieren bibliotecas adicionales; Aspose.Cells maneja todas las operaciones de Excel.

## Paso 1: Crear el libro y acceder a la primera hoja de cálculo

El primer paso es **create excel workbook python** objetos y obtener la hoja de cálculo predeterminada. Esto te brinda un lienzo limpio para aplicar más estilos.

```python
# Import required Aspose.Cells classes
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# Create a new workbook; the first worksheet is at index 0
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Por qué es importante:* `Workbook()` crea un archivo Excel en memoria. Acceder a `worksheets[0]` evita codificar nombres de hoja y funciona incluso si el nombre predeterminado cambia.

## Paso 2: Helper para agregar un formato condicional TIME_PERIOD

Para mantener el código ordenado, envolvemos la creación del formato condicional en un helper. Recibe un rango de celdas, un color de fondo y la regla de período de tiempo deseada.

```python
def add_time_period(sheet, cell_range, bg_color, period_type):
    """
    Adds a TIME_PERIOD conditional formatting rule to `cell_range`.
    The rule paints the cells with `bg_color` when the date matches `period_type`.
    """
    # Retrieve (or create) the ConditionalFormatting collection for the range
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)

    # Insert a TIME_PERIOD condition and configure its style
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color          # set cell background color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type                # e.g., TimePeriodType.YESTERDAY
```

*Por qué es importante:* El helper abstrae los pasos repetitivos de crear un formato condicional, facilitando su reutilización para otras reglas basadas en fechas como “Today” o “Last Week”.

## Paso 3: Aplicar la regla “Yesterday” a un rango

Ahora usamos el helper para resaltar celdas que contienen la fecha de ayer. El rango `I19:K20` se volverá **medium sea green** cuando se cumpla la condición.

```python
add_time_period(
    worksheet,
    "I19:K20",                # range to format
    Color.medium_sea_green,  # set cell background color
    TimePeriodType.YESTERDAY # date based conditional formatting
)
```

*Por qué es importante:* `TimePeriodType.YESTERDAY` forma parte de la enumeración incorporada de Aspose.Cells, por lo que no necesitas calcular fechas manualmente. La biblioteca evalúa la regla cada vez que se abre el libro.

## Paso 4: Poblar el rango con fechas de ejemplo

Para ver la regla en acción, escribimos dos fechas—una que coincide con “Yesterday” y otra que no. El estilo `number` `30` corresponde a un formato de fecha incorporado.

```python
# Cell I19 gets a date that is exactly yesterday (relative to the sample data)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))   # 30 July 2008
cell.style.number = 30                # date format

# Cell K20 gets a date that is outside the rule
cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))    # 3 August 2008
cell.style.number = 30
```

*Por qué es importante:* Al insertar fechas concretas puedes verificar que el formato condicional funciona sin necesidad de abrir el archivo en un día específico.

## Paso 5: Agregar una etiqueta descriptiva y auto‑ajustar la columna

Una pequeña etiqueta aclara el propósito del rango formateado, y `auto_fit_column` hace que la hoja sea legible.

```python
# Add a label under the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Adjust column width for better visibility (column 12 = L)
worksheet.auto_fit_column(12)
```

## Paso 6: Guardar el libro

Finalmente, escribe el libro en disco. La llamada `os.makedirs` asegura que la carpeta de destino exista.

```python
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)

# Save as XLSX – the most widely supported Excel format
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Cuando abras *TimePeriodDemo.xlsx* verás:

- La celda **I19** sombreada **medium sea green** porque su valor coincide con la regla “Yesterday”.  
- La celda **K20** mantiene el fondo predeterminado porque su fecha no satisface la condición.  

Esto demuestra **format cells by date** usando una sola línea de código Python.

## Ejemplo completo y ejecutable

Juntando todas las piezas, aquí tienes el script completo que puedes copiar‑pegar y ejecutar:

```python
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# 1️⃣ Create workbook and get first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# 2️⃣ Helper to add TIME_PERIOD conditional formatting
def add_time_period(sheet, cell_range, bg_color, period_type):
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type

# 3️⃣ Apply “Yesterday” rule (set cell background color)
add_time_period(
    worksheet,
    "I19:K20",
    Color.medium_sea_green,
    TimePeriodType.YESTERDAY
)

# 4️⃣ Fill sample dates (format cells by date)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))
cell.style.number = 30

cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))
cell.style.number = 30

# 5️⃣ Add label and auto‑fit column
worksheet.cells.get("I20").put_value("Yesterday")
worksheet.auto_fit_column(12)

# 6️⃣ Save the workbook
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Ejecuta el script, abre el archivo resultante y verás el formato condicional en acción.

## Variaciones comunes y casos límite

| Variación | Cómo implementar | Cuándo usar |
|-----------|------------------|-------------|
| **Resaltar “Today”** | Replace `TimePeriodType.YESTERDAY` with `TimePeriodType.TODAY` | Paneles en tiempo real |
| **Múltiples rangos** | Call `add_time_period` for each range, passing different colors | Informes complejos |
| **Rango de fechas dinámico** | Use `TimePeriodType.LAST_7_DAYS` or `TimePeriodType.NEXT_MONTH` | Informes continuos |
| **Color personalizado** | Use `Color.from_argb(255, r, g, b)` to create any shade | Estilo coherente con la marca |

**Consejo profesional:** Siempre establece `condition.style.pattern = BackgroundType.SOLID` cuando deseas un relleno sólido; de lo contrario Excel puede mostrar un degradado que parece inconsistente entre versiones.

## Conclusión

Ahora sabes cómo crear scripts **create Excel workbook python** que **set cell background color**, apliquen **excel conditional formatting python**, y **format cells by date** usando Aspose.Cells. El ejemplo cubre un escenario de **date based conditional formatting**, pero el mismo patrón funciona para cualquier regla de período de tiempo.

A continuación, podrías explorar:

- Agregar barras de datos o conjuntos de íconos (`FormatConditionType.DATA_BAR`)  
- Combinar múltiples reglas condicionales en el mismo rango  
- Exportar el libro a PDF (`SaveFormat.PDF`) para informes  

Siéntete libre de experimentar con diferentes colores, rangos y tipos de períodos de tiempo para adaptarlos a tus necesidades específicas de informes. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Domina el formato de celdas de Excel y la gestión de libros con Aspose.Cells para .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Automatización de Excel con Aspose.Cells .NET&#58; Crear libro y establecer enlaces externos](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Cómo crear rangos con nombre con alcance de libro en Excel usando Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}