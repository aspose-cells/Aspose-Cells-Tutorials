---
category: general
date: 2026-08-24
description: Create conditional formatting rule in Python using Aspose.Cells to highlight
  dates, with auto‑fit column and background color formatting.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting rule
- auto fit column
- conditional formatting by date
- background color conditional format
- date based conditional format
language: es
lastmod: 2026-08-24
og_description: Create conditional formatting rule in Python with Aspose.Cells. Learn
  how to highlight dates, set background colors, and auto‑fit columns in just a few
  lines of code.
og_image_alt: Screenshot of an Excel sheet where yesterday's date cells are highlighted
  in pink
og_title: Create a conditional formatting rule for dates in Python – step‑by‑step
  guide
schemas:
- author: Aspose
  dateModified: '2026-08-24'
  description: Create conditional formatting rule in Python using Aspose.Cells to
    highlight dates, with auto‑fit column and background color formatting.
  headline: How to create conditional formatting rule for dates in Python
  type: TechArticle
tags:
- Aspose.Cells
- Python
- Excel automation
- Conditional formatting
title: How to create conditional formatting rule for dates in Python
url: /es/python/formatting/how-to-create-conditional-formatting-rule-for-dates-in-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear una regla de formato condicional para fechas en Python

Si necesitas **crear una regla de formato condicional** que reaccione a fechas, esta guía te muestra exactamente cómo hacerlo con Aspose.Cells para Python. Ya sea que estés construyendo un panel de informes o una hoja de cálculo automatizada, verás cómo resaltar las fechas de ayer, aplicar un color de fondo personalizado y **ajustar automáticamente el ancho de columna** para que el resultado se vea pulido.

En este tutorial cubriremos **formato condicional por fecha**, demostraremos un **formato condicional de color de fondo**, y terminaremos guardando el libro de trabajo como un archivo XLSX. Al final tendrás una función auxiliar reutilizable que podrás adaptar a cualquier **formato condicional basado en fechas** que necesites.

## Lo que aprenderás

* Configurar un libro de trabajo y una hoja de cálculo usando Aspose.Cells.  
* Escribir una función auxiliar que añada un **formato condicional basado en fechas** a cualquier rango de celdas.  
* Poblar celdas con fechas de ejemplo para que la regla pueda evaluarse.  
* Aplicar **ajuste automático de columna** para que el contenido sea legible.  
* Guardar el libro de trabajo y verificar las celdas resaltadas.

El único requisito previo es un entorno Python funcional con el paquete `aspose-cells` instalado.

## Requisitos previos

| Requisito | Detalles |
|-----------|----------|
| Python | 3.8+ |
| Aspose.Cells for Python via Java | `pip install aspose-cells` |
| Conocimientos básicos de conceptos de Excel | worksheets, cells, formatting |
| Opcional: IDE (VS Code, PyCharm, etc.) | any editor that can run Python scripts |

## Paso 1: Crear un libro de trabajo y obtener la primera hoja de cálculo

El primer paso es crear objetos listos para **crear regla de formato condicional**: un `Workbook` y su `Worksheet` predeterminado. Estos objetos son el punto de entrada para todas las operaciones posteriores.

```python
# Step 1 – initialize workbook and worksheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create a new, empty workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Por qué es importante:* El `Workbook` contiene todo el archivo Excel, mientras que el `Worksheet` es donde aplicas celdas, estilos y **formato condicional por fecha**. Sin estos objetos el resto del código no tiene dónde actuar.

## Paso 2: Construir una función auxiliar para añadir un formato condicional TIME_PERIOD

En lugar de repetir el mismo código base para cada rango, encapsulamos la lógica en una función auxiliar. Esta función adjunta un **formato condicional de color de fondo** que colorea celdas según un `TimePeriodType` (p. ej., Yesterday, Today, LastWeek).

```python
def add_time_period_condition(cell_range: str, bg_color: Color, period: TimePeriodType):
    """
    Attach a TIME_PERIOD conditional format to `cell_range`.
    The rule highlights cells that fall within `period` using `bg_color`.

    Args:
        cell_range: A1‑style range string, e.g., "I19:K20".
        bg_color:   Desired background color for matching cells.
        period:     Aspose.Cells TimePeriodType enum value.
    Returns:
        The FormatConditionCollection for further customization if needed.
    """
    # 1️⃣ Attach a new ConditionalFormatting block to the specified range
    worksheet.conditional_formattings.add(cell_range)

    # 2️⃣ Grab the collection of conditions for that block
    conditions = worksheet.conditional_formattings[-1].format_conditions

    # 3️⃣ (Optional) Set a default background for the whole range
    conditions.back_color = bg_color

    # 4️⃣ Add a TIME_PERIOD condition and configure its appearance
    idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[idx]

    # Apply the visual style – pink background in this example
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Define which period triggers the formatting
    condition.time_period = period

    return conditions
```

*Por qué usamos una función auxiliar:* Aísla la lógica del **formato condicional basado en fechas**, haciendo que el código sea más fácil de leer, probar y reutilizar en múltiples hojas o proyectos.

## Paso 3: Aplicar la regla de formato condicional a un rango específico

Ahora usamos la función auxiliar para resaltar celdas que contienen “Yesterday”. Este es el núcleo de nuestra operación de **crear regla de formato condicional**.

```python
# Step 3 – highlight cells I19:K20 that contain “Yesterday”
add_time_period_condition(
    cell_range="I19:K20",
    bg_color=Color.medium_sea_green,   # optional default background for the whole range
    period=TimePeriodType.YESTERDAY   # the date‑based trigger
)
```

Cuando se abre el libro de trabajo, cualquier celda en `I19:K20` cuya fecha sea igual a la de ayer aparecerá con un relleno rosa (el estilo que establecimos en la función auxiliar). El argumento `bg_color` muestra cómo puedes superponer un fondo predeterminado detrás del color condicional si lo deseas.

## Paso 4: Poblar el rango con fechas de ejemplo

Una regla condicional solo se vuelve visible después de que la hoja de cálculo contenga datos que cumplan la condición. Insertaremos dos fechas: una que coincida con “Yesterday” y otra que quede fuera del período.

```python
# Step 4 – insert sample dates for demonstration

# Cell I19 will match the YESTERDAY period
yesterday_cell = worksheet.cells.get("I19")
yesterday_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008 is “yesterday” relative to 31‑Jul‑2008
yesterday_cell.get_style().number = 30          # 30 = built‑in date format
yesterday_cell.set_style(yesterday_cell.get_style())

# Cell K20 will NOT match the period (it’s a later date)
outside_cell = worksheet.cells.get("K20")
outside_cell.put_value(datetime(2008, 8, 3))     # 03‑Aug‑2008 is outside “Yesterday”
outside_cell.get_style().number = 30
outside_cell.set_style(outside_cell.get_style())

# Optional label for clarity – not part of the rule
worksheet.cells.get("I20").put_value("Yesterday")
```

*Por qué es importante:* Al usar objetos `datetime` aseguramos que Excel trate los valores como fechas reales, lo cual es necesario para que el **formato condicional por fecha** funcione correctamente. El formato numérico (`30`) garantiza que las celdas se muestren como fechas reconocibles.

## Paso 5: Ajustar automáticamente la columna y guardar el libro de trabajo

Una vez que los datos y el formato están en su lugar, el toque final es **ajustar automáticamente el ancho de columna** para que las fechas sean completamente visibles. Luego escribimos el archivo en disco.

```python
# Step 5 – adjust column width and save the file

# Auto‑fit column 12 (the column that contains our sample data)
worksheet.auto_fit_column(12)

# Save the workbook as an XLSX file
output_path = "YOUR_DIRECTORY/TimePeriodDemo.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

La llamada `auto_fit_column` examina el contenido más largo en la columna 12 (que corresponde a la columna **L** en Excel) y amplía el ancho en consecuencia. Este pequeño paso evita que las fechas se truncen y hace que el **formato condicional de color de fondo** sea claramente visible.

### Resultado esperado

Cuando abras `TimePeriodDemo.out.xlsx`:

| I19 (fecha) | I20 (etiqueta) | K20 (fecha) |
|------------|------------|------------|
| 30‑Jul‑2008 (resaltado en rosa) | Ayer | 03‑Aug‑2008 (sin resaltado) |

* La celda con la fecha de ayer muestra un fondo rosa porque la **crear regla de formato condicional** coincidió con el período `YESTERDAY`.  
* Todas las demás celdas conservan el fondo predeterminado (o el `medium_sea_green` opcional que proporcionaste).  
* La columna L se amplía automáticamente, por lo que las fechas son completamente legibles.

## Variaciones comunes y casos límite

| Situación | Cómo adaptar el código |
|-----------|-----------------------|
| **Resaltar “Today” en lugar de “Yesterday”** | Reemplaza `TimePeriodType.YESTERDAY` con `TimePeriodType.TODAY`. |
| **Usar un color de fondo diferente** | Cambia `condition.style.background_color = Color.pink` a cualquier otro `Color` (p. ej., `Color.light_sky_blue`). |
| **Aplicar la regla a un rango no contiguo** | Llama a `add_time_period_condition` varias veces con diferentes cadenas `cell_range` (p. ej., `"A1:A10", "C1:C10"`). |
| **Trabajar con un libro de trabajo preexistente** | Carga el archivo con `Workbook("myfile.xlsx")` en lugar de crear uno nuevo. |
| **Múltiples condiciones basadas en fechas en el mismo rango** | Después de la primera llamada a `add_time_period_condition`, añade otra condición con `conditions.add_condition(FormatConditionType.TIME_PERIOD)` y establece un `time_period` diferente. |

## Conclusión

Ahora sabes cómo **crear regla de formato condicional** que reacciona a fechas, aplicar un **formato condicional de color de fondo**, y **ajustar automáticamente el ancho de columna** usando Aspose.Cells para Python. La función auxiliar abstrae la lógica, permitiéndote reutilizar el mismo patrón para cualquier escenario de **formato condicional por fecha**, ya sea “Yesterday”, “LastWeek” o un rango personalizado.

Después, podrías explorar:

* Añadir **conjuntos de íconos** o **barras de datos** junto a reglas de fechas.  
* Generar informes dinámicos que obtengan fechas de una base de datos.  
* Combinar múltiples reglas de **formato condicional basado en fechas** en una sola hoja.

Siéntete libre de experimentar con diferentes colores, períodos y rangos para adaptarlos a las necesidades de tu proyecto. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Domina el formato condicional en Excel usando Aspose.Cells .NET: Guía completa](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Cómo extraer colores de formato condicional usando Aspose.Cells para .NET](/cells/english/net/formatting/extract-conditional-formatting-colors-aspose-cells-net/)
- [Domina el formato condicional con fuentes personalizadas en Excel usando Aspose.Cells para .NET y C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}