---
category: general
date: 2026-08-08
description: Crear libro de Excel con Python y agregar formato condicional basado
  en la fecha. Guía paso a paso usando Aspose.Cells para resaltar las celdas de ayer.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- conditional formatting based on date
- Aspose.Cells Python example
- Excel date formatting Python
- Python Excel automation
language: es
lastmod: 2026-08-08
og_description: Crea un libro de Excel con Python y Aspose.Cells y aplica formato
  condicional basado en la fecha para hojas de cálculo dinámicas.
og_image_alt: Screenshot of an Excel sheet created with Python showing cells highlighted
  by date conditional formatting
og_title: Crear libro de Excel con Python – formato condicional de fechas
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Create Excel workbook Python and add conditional formatting based on
    date. Step‑by‑step guide using Aspose.Cells to highlight yesterday’s cells.
  headline: Create Excel workbook Python date conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Crear libro de Excel con formato condicional de fechas en Python
url: /es/python/formatting/create-excel-workbook-python-date-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear libro de Excel con Python y formato condicional de fecha

Si necesitas **create Excel workbook Python** y resaltar automáticamente celdas que coincidan con una fecha específica, este tutorial te muestra exactamente cómo. Aprenderás a aplicar **conditional formatting based on date** para que las fechas de ayer se iluminen en rosa, usando la biblioteca Aspose.Cells.

La guía recorre cada paso—desde la instalación del SDK hasta guardar el archivo .xlsx final—para que puedas copiar y pegar un ejemplo funcional en tu propio proyecto. No se requiere documentación externa; todo el código y las explicaciones están autocontenidos.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* Python 3.8 o superior instalado.
* Paquete `aspose-cells` (el contenedor Python para Aspose.Cells). Instálalo con:
  ```bash
  pip install aspose-cells
  ```
* Familiaridad básica con Python y conceptos de Excel como hojas de cálculo y estilos de celda.

> **Consejo profesional:** Aspose.Cells funciona sin necesidad de tener Microsoft Excel instalado, lo que lo hace ideal para automatización del lado del servidor.

## Paso 1: Crear el libro de Excel en Python

La primera tarea es instanciar un nuevo libro de trabajo y obtener la hoja de cálculo predeterminada. Este objeto representa todo el archivo de Excel y brinda acceso a filas, columnas y APIs de formato.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook – this automatically adds one worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]   # reference to the first (default) sheet
```

Crear el libro de trabajo es la base para cualquier manipulación posterior, ya sea que estés añadiendo datos, fórmulas o reglas de formato.

## Paso 2: Definir un formato condicional basado en fecha

Ahora añadimos **conditional formatting based on date**. El enumerado `FormatConditionType.TIME_PERIOD` nos permite especificar períodos de tiempo incorporados como Yesterday, Today o LastWeek.

```python
from aspose.cells import FormatConditionType, BackgroundType, TimePeriodType
from aspose.pydrawing import Color

# Target range I19:K20 – three columns by two rows
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions

# Add a new time‑period condition (e.g., Yesterday)
condition_index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[condition_index]

# Set the visual style: pink solid background
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Specify that the condition should trigger for "Yesterday"
condition.time_period = TimePeriodType.YESTERDAY
```

Por qué este paso es importante: Excel evalúa la condición para cada celda del rango. Cuando el valor de una celda cae dentro del período definido (ayer), el estilo que asignamos se aplica automáticamente.

## Paso 3: Poblar el rango con fechas de ejemplo

Para ver la regla en acción, escribimos un par de objetos `datetime` en las celdas objetivo. Uno de ellos se establece deliberadamente en la fecha de ayer según el sistema interno de fechas del libro de trabajo.

```python
from datetime import datetime

# Cell I19 – yesterday’s date (will be highlighted)
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # This date matches the "Yesterday" rule
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel’s built‑in date format
cell_i19.set_style(style_i19)

# Cell K20 – a random later date (no highlight)
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Not yesterday, so no formatting
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

La línea `number = 30` indica a Excel que muestre el valor usando su formato de fecha corta estándar. Puedes cambiar este índice a cualquier formato numérico incorporado si prefieres una presentación diferente.

## Paso 4: Ajustar el ancho de columna para mayor legibilidad

Ajustar automáticamente la columna que contiene las fechas facilita la lectura del resultado, especialmente cuando el libro se abre en Excel o en un visor.

```python
# Column 12 corresponds to column L (zero‑based indexing)
worksheet.auto_fit_column(12)
```

## Paso 5: Guardar el libro en disco

Finalmente, guarda el libro como un archivo .xlsx. Reemplaza `"YOUR_DIRECTORY"` con una ruta real en tu máquina.

```python
import os

output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Cuando abras `TimePeriodDemo.out.xlsx` en Excel, la celda **I19** aparecerá con un fondo rosa porque su valor coincide con la regla “Yesterday”, mientras que **K20** permanecerá sin cambios.

### Resultado esperado

| I19 (fecha) | I20 (etiqueta) | J19 | J20 | K19 | K20 (fecha) |
|------------|-------------|-----|-----|-----|------------|
| *2008‑07‑30* (fondo rosa) | Yesterday | – | – | – | *2008‑08‑03* (sin formato) |

El sombreado rosa confirma que **conditional formatting based on date** funciona como se espera.

## Variaciones comunes y casos límite

| Situación | Cómo adaptar el código |
|-----------|-----------------------|
| **Resaltar “Today” en lugar de “Yesterday”** | Change `condition.time_period = TimePeriodType.TODAY` |
| **Aplicar la regla a una columna completa** | Use `worksheet.get_range("A:A").format_conditions` |
| **Usar un rango de fechas personalizado (p.ej., últimos 7 días)** | Replace the time‑period condition with a formula condition: <br>```python<br>condition = conditions.add_condition(FormatConditionType.FORMULA)<br>condition.formula1 = 'AND(A1>=TODAY()-7, A1<=TODAY())'<br>``` |
| **Colores de fondo diferentes** | Set `condition.style.background_color = Color.light_green` (or any `Color` you prefer) |
| **Ejecutar en Linux sin pantalla** | Aspose.Cells es totalmente sin cabeza; no se requiere configuración adicional. |

## Ejemplo completo y ejecutable

A continuación se muestra el script completo que puedes ejecutar tal cual (después de actualizar el directorio de salida). Todas las importaciones, comentarios y conceptos básicos de manejo de errores están incluidos.

```python
# -*- coding: utf-8 -*-
"""
Create Excel workbook Python with date conditional formatting.
Demonstrates how to highlight yesterday’s dates using Aspose.Cells.
"""

import os
from datetime import datetime
from aspose.cells import (
    Workbook, SaveFormat,
    FormatConditionType, BackgroundType,
    TimePeriodType
)
from aspose.pydrawing import Color

# ----------------------------------------------------------------------
# 1️⃣ Initialize workbook
# ----------------------------------------------------------------------
workbook = Workbook()
worksheet = workbook.worksheets[0]

# ----------------------------------------------------------------------
# 2️⃣ Add conditional formatting for "Yesterday"
# ----------------------------------------------------------------------
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions
cond_idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[cond_idx]

# Visual style: pink solid fill
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
condition.time_period = TimePeriodType.YESTERDAY

# ----------------------------------------------------------------------
# 3️⃣ Populate sample dates
# ----------------------------------------------------------------------
# Cell that should match the condition
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Yesterday relative to demo data
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel short‑date format
cell_i19.set_style(style_i19)

# Cell that does NOT match
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label
worksheet.cells.get("I20").put_value("Yesterday")

# ----------------------------------------------------------------------
# 4️⃣ Auto‑fit column for better visibility
# ----------------------------------------------------------------------
worksheet.auto_fit_column(12)   # Column L (0‑based index)

# ----------------------------------------------------------------------
# 5️⃣ Save workbook
# ----------------------------------------------------------------------
output_dir = "YOUR_DIRECTORY"   # <-- replace with a real folder
os.makedirs(output_dir, exist_ok=True)
output_path = os.path.join(output_dir, "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Ejecutar el script genera un archivo Excel donde la celda “Yesterday” se resalta automáticamente, demostrando **create Excel workbook Python** combinado con **conditional formatting based on date**.

## Conclusión

Ahora sabes cómo **create Excel workbook Python** objetos, definir un **date‑based conditional formatting**.

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Crear un libro de Excel usando Aspose.Cells en Java: Guía paso a paso](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Crear libro de Excel con gráficos usando Aspose.Cells .NET \| Guía paso a paso](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)
- [Automatización de Excel: crear un libro y añadir un ListBox usando Aspose.Cells para .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}