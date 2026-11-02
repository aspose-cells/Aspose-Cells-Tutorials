---
category: general
date: 2026-09-05
description: Crear un libro de Excel en Python y añadir formato condicional para resaltar
  las celdas de ayer. Aprende el código completo y por qué cada paso es importante.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- add conditional formatting excel
- highlight cells based on date
- add conditional formatting range
- how to highlight yesterday cells
language: es
lastmod: 2026-09-05
og_description: Crea un libro de Excel en Python y agrega formato condicional para
  resaltar las celdas de ayer. Sigue esta guía paso a paso para una solución completa.
og_image_alt: Screenshot of an Excel sheet where cells are highlighted after creating
  Excel workbook in Python
og_title: Crear libro de Excel en Python – agregar formato condicional
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create Excel workbook in Python and add conditional formatting to highlight
    yesterday cells. Learn the full code and why each step matters.
  headline: Create Excel workbook in Python with conditional formatting
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Crear libro de Excel en Python con formato condicional
url: /es/python/formatting/create-excel-workbook-in-python-with-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear libro de Excel en Python con formato condicional

Si necesitas **create Excel workbook python** para una tarea de informes, esta guía te muestra cómo generar un libro de trabajo y aplicar una regla de formato condicional que resalta las fechas de ayer. Verás el código exacto, por qué existe cada línea y cómo adaptar la solución a otros rangos de fechas.

El formato condicional es una forma poderosa de llamar la atención sobre datos que cumplen una condición específica. En este tutorial usamos la biblioteca Aspose.Cells para Python a través de .NET, que brinda soporte completo de funciones de Excel sin requerir Microsoft Office. Al final de la guía tendrás un archivo donde las celdas del rango *I19:K20* se vuelven rosadas cuando contienen la fecha de ayer.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* Python 3.9+ instalado
* Paquete `aspose-cells` (instalar con `pip install aspose-cells`)
* Familiaridad básica con la sintaxis de Python
* Permiso de escritura en el directorio donde se guardará el libro de trabajo

El código funciona en Windows, macOS y Linux siempre que el runtime de .NET esté disponible.

## Crear libro de Excel en Python

El primer paso es instanciar un objeto `Workbook` y obtener la hoja de cálculo predeterminada. Este objeto representa todo el archivo de Excel en memoria.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Por qué es importante*: `Workbook()` crea un libro vacío con una sola hoja. Acceder a `worksheets[0]` te brinda un manejador para agregar datos, estilos y formato más adelante.

## Añadir rango de formato condicional

A continuación definimos el área que será evaluada por la regla condicional. El rango `I19:K20` cubre seis celdas en dos filas.

```python
# Define the range that will receive the conditional formatting rule
condition_collection = worksheet.conditional_formattings.add("I19:K20")
```

*Por qué es importante*: Añadir una colección de formato condicional a un rango específico aísla la regla, evitando que afecte celdas no relacionadas. Esto cumple con el requisito de **add conditional formatting range**.

## Definir la regla: resaltar celdas según la fecha

Ahora creamos una condición del tipo `TIME_PERIOD`. Esto indica a Excel que compare el valor de cada celda con una ventana de tiempo predefinida.

```python
from aspose.cells import FormatConditionType, TimePeriodType

# Add a TIME_PERIOD condition to the collection
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Set the time period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY
```

*Por qué es importante*: `TIME_PERIOD` es el único tipo incorporado que admite directamente “Yesterday”, “Today”, “Last Week”, etc. Al establecer `condition.time_period` a `YESTERDAY`, la regla evalúa automáticamente el valor de fecha de cada celda contra el día anterior a la fecha actual.

## Estilizar las celdas que cumplen la condición

El formato condicional también necesita un estilo visual. Aquí elegimos un relleno sólido rosado para que las celdas coincidentes destaquen.

```python
from aspose.pydrawing import Color as DrawingColor
from aspose.cells import BackgroundType

# Apply a pink solid background to cells that satisfy the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID
```

*Por qué es importante*: El objeto de estilo define cómo Excel renderizará las celdas que cumplen la condición. Usar un relleno sólido rosado satisface el requisito de **highlight cells based on date** y facilita la verificación del resultado.

## Poblar fechas de muestra para la evaluación

Para ver la regla en acción insertamos dos fechas: una que corresponde a la fecha de ayer y otra que no. El formato `number` `30` corresponde al formato de fecha incorporado `mm-dd-yy`.

```python
from datetime import datetime

# Cell I19: a date that matches “Yesterday”
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Example date; adjust as needed
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

# Cell K20: a date outside the “Yesterday” period
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Example date; adjust as needed
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Optional label for the range
worksheet.cells.get("I20").put_value("Yesterday")
```

*Por qué es importante*: Proporcionar tanto una fecha coincidente como una no coincidente te permite verificar que el formato condicional funciona correctamente. Ajusta las fechas al mes actual al ejecutar el script, o reemplázalas con valores dinámicos.

## Guardar el libro de trabajo

Finalmente escribimos el archivo en disco. La constante `SaveFormat.XLSX` garantiza que la salida sea un archivo Excel moderno.

```python
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

*Por qué es importante*: Persistir el libro permite abrirlo en Excel, LibreOffice o cualquier visor que soporte XLSX. La ruta impresa confirma dónde se escribió el archivo.

## Script completo

Uniendo todas las piezas, el script completo y ejecutable se ve así:

```python
# -*- coding: utf-8 -*-
"""
Create an Excel workbook in Python, add a conditional formatting rule,
and highlight yesterday's cells.
"""

from aspose.cells import (
    Workbook, SaveFormat, FormatConditionType,
    BackgroundType, TimePeriodType
)
from aspose.pydrawing import Color as DrawingColor
from datetime import datetime

# Step 1: Create a new workbook and access the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Add a conditional formatting rule for the range I19:K20
condition_collection = worksheet.conditional_formattings.add("I19:K20")
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Step 3: Define the visual style for cells that meet the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID

# Step 4: Set the time‑period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Step 5: Populate sample dates for evaluation
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # yesterday relative to the example
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # outside the period
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Step 6: Add a label for the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### Resultado esperado

Al abrir `TimePeriodExample.xlsx`:

* La celda **I19** aparece con un fondo rosado porque su valor coincide con ayer.
* La celda **K20** mantiene el fondo predeterminado porque su fecha está fuera del período.
* La etiqueta **“Yesterday”** se encuentra en la celda I20 para mayor claridad.

## Variaciones comunes y casos límite

| Situación | Ajuste |
|-----------|--------|
| **Resaltar hoy en lugar de ayer** | Cambiar `condition.time_period = TimePeriodType.TODAY`. |
| **Aplicar la regla a un área más grande** | Actualizar la cadena de rango en `add("I19:K20")` a algo como `"A1:Z100"`. |
| **Usar un color de relleno diferente** | Reemplazar `DrawingColor.pink` por cualquier otro `DrawingColor` (p.ej., `DrawingColor.light_green`). |
| **Trabajar con fechas dinámicas** | Calcular `datetime.now() - timedelta(days=1)` para ayer y escribir ese valor en las celdas antes de aplicar la regla. |

**Consejo profesional:** Cuando generas el libro de trabajo programáticamente para muchos usuarios, mantén la definición del formato condicional separada de la inserción de datos. Así podrás reutilizar el mismo estilo en varias hojas sin duplicar código.

## Verificar el resultado programáticamente (opcional)

Si deseas confirmar el formato sin abrir Excel, puedes inspeccionar el estilo de una celda después de guardar:



## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Automatización de Excel&#58; Crear un libro de trabajo y agregar un ListBox usando Aspose.Cells para .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Crear libro de Excel y agregar etiquetas con Aspose.Cells para Java](/cells/english/java/advanced-excel-charts/data-labeling/)
- [Automatización de Excel: crear libro de trabajo y agregar ListBox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}