---
category: general
date: 2026-07-20
description: Crear libro de Excel con Python y Aspose.Cells, establecer el color de
  fondo de la celda y añadir formato condicional en Python para dar estilo a las celdas
  según la fecha.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- aspose cells conditional formatting
- add conditional formatting python
language: es
lastmod: 2026-07-20
og_description: Crea un libro de Excel con Python usando Aspose.Cells. Aprende cómo
  establecer el color de fondo de una celda y agregar formato condicional en Python
  para formatear celdas por fecha.
og_image_alt: Screenshot of an Excel workbook created with Python showing conditional
  formatting applied to date cells
og_title: Crear libro de Excel con Python – Añadir formato condicional
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Create Excel workbook Python with Aspose.Cells, set cell background
    color, and add conditional formatting python to style cells by date.
  headline: Create Excel Workbook Python – Conditional Formatting Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Change `"I19:K20"` to any A1‑style range, and adjust the sample
      dates accordingly.
    question: Can I target a different date range?
  - answer: Use `FormatConditionType.FORMULA` and set `condition.formula1 = "YOUR_FORMULA"`—for
      example, `=TODAY()-A1=1` to mimic yesterday.
    question: What if I need a custom formula instead of `YESTERDAY`?
  - answer: Call `conditions.add_condition` again with a different `FormatConditionType`.
      The order matters; later rules can override earlier ones.
    question: How do I apply multiple rules to the same range?
  - answer: Yes—modify `condition.style.font.color = Color.white` (or any other `Color`).
    question: Is there a way to set font colour together with background?
  type: FAQPage
tags:
- Aspose.Cells
- Python
- Excel Automation
title: Crear libro de Excel con Python – Guía de formato condicional
url: /es/python/formatting/create-excel-workbook-python-conditional-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear Libro de Excel con Python – Guía de Formato Condicional

¿Alguna vez te has preguntado cómo **crear libro de Excel con Python** desde cero y lograr que se vea pulido sin abrir la UI? No estás solo. Muchos desarrolladores se topan con un obstáculo cuando necesitan **establecer color de fondo de celda** o aplicar estilos basados en fechas de forma programática.  

En este tutorial recorreremos un ejemplo completo y ejecutable que usa Aspose.Cells para **add conditional formatting python** reglas, formatear celdas por fecha y guardar el resultado como un archivo XLSX moderno. Al final tendrás un script autónomo que puedes insertar en cualquier proyecto.

## Lo que aprenderás

- Cómo inicializar un libro de trabajo y obtener la primera hoja.  
- Formas de **establecer color de fondo de celda** para un rango completo.  
- Usar **aspose cells conditional formatting** para resaltar fechas de “Yesterday”.  
- Ajuste automático de columnas y persistencia del archivo en disco.  

No se requiere configuración externa—solo Python 3 y el paquete Aspose.Cells. Si ya instalaste `aspose-cells`, estás listo; de lo contrario, un rápido `pip install aspose-cells` será suficiente.

## Requisitos previos

- Python 3.8+ (el código funciona en 3.9, 3.10 y versiones más recientes).  
- Aspose.Cells para Python vía .NET (`aspose-cells` wrapper de NuGet).  
- Familiaridad básica con conceptos de Excel (celdas, rangos, formato).  

¿Los tienes? Genial—¡vamos a sumergirnos!

## Crear Libro de Excel con Python – Configuración y Hoja de Trabajo

Lo primero: necesitamos un objeto de libro de trabajo nuevo y una referencia a la hoja de cálculo predeterminada. Este es el lienzo donde se realizarán todas las operaciones posteriores.

```python
# Import the necessary Aspose.Cells classes
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and grab the first sheet
workbook = Workbook()                     # create excel workbook python
worksheet = workbook.worksheets[0]        # default is the first worksheet
```

> **Por qué es importante:** `Workbook()` construye un archivo Excel en memoria, eliminando la necesidad de archivos temporales. La variable `worksheet` es nuestro punto de entrada para acciones a nivel de celda.

## Establecer Color de Fondo de Celda

Antes de añadir cualquier regla, es conveniente dar al rango objetivo un color base para que el formato condicional destaque. El asistente a continuación recupera (o crea) una `FormatConditionCollection` para un rango dado y pinta las celdas con un fondo sólido.

```python
def get_format_condition(cell_range: str, base_color: Color):
    """
    Obtain (or create) a FormatConditionCollection for `cell_range`.
    Also set a base background colour for the whole range.
    """
    # Retrieve or add a conditional formatting entry for the range
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    # Apply the base colour to every cell in the range
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color          # set cell background color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection
```

> **Consejo profesional:** Si planeas reutilizar el mismo rango con múltiples reglas, llama a este asistente una sola vez y conserva la colección devuelta; ahorra algunas llamadas a la API.

## Añadir Formato Condicional Python para Rangos de Fechas

Ahora la parte divertida: crearemos una regla de **formato condicional de período de tiempo** que resalta celdas que contienen la fecha de ayer. Esto demuestra el poder de **format cells by date** usando Aspose.Cells.

```python
def apply_yesterday_rule():
    """
    Apply a “Yesterday” conditional formatting rule to the range I19:K20.
    Cells that match will turn pink; others stay with the base colour.
    """
    # Obtain the condition collection for the target range
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)

    # Create a TIME_PERIOD condition (this is the aspose cells conditional formatting type we need)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]

    # Define the appearance for cells that meet the condition
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Set the time period to “Yesterday”
    condition.time_period = TimePeriodType.YESTERDAY

    # Populate sample dates to demonstrate the rule
    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))   # matches “Yesterday”
    cell_i19.style.number = 30                 # Excel number format for dates
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))    # does NOT match
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    # Add a label for clarity
    worksheet.cells.get("I20").put_value("Yesterday")
```

> **¿Por qué usar `TIME_PERIOD`?** Abstrae la necesidad de escribir fórmulas personalizadas. Aspose.Cells evalúa la fecha contra la fecha del sistema actual, por lo que la regla siempre permanece relevante.

### Ejecutando la Regla

```python
apply_yesterday_rule()
```

Al abrir el archivo resultante, las celdas `I19` se iluminarán en rosa (porque son “Yesterday”), mientras que `K20` mantiene el color verde base.

## Ajustar Automáticamente Columnas y Guardar Libro

Una hoja de cálculo ordenada se ve profesional. El ajuste automático garantiza que nuestros datos no estén apretados.

```python
# Step 4: Auto‑fit the column width for a tidy appearance
worksheet.auto_fit_column(12)   # column index is zero‑based; 12 corresponds to column M

# Step 5: Save the workbook to disk
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Caso límite:** Si apuntas a un directorio que no existe, `workbook.save` generará un error. Envuelve la llamada a save en un bloque `try/except` si necesitas un manejo elegante.

### Script Completo (Listo para Copiar‑Pegar)

A continuación está el script completo, listo para ejecutarse. Simplemente reemplaza `YOUR_DIRECTORY` con una carpeta válida en tu máquina.

```python
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create the workbook and worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

def get_format_condition(cell_range: str, base_color: Color):
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection

def apply_yesterday_rule():
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = TimePeriodType.YESTERDAY

    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))
    cell_i19.style.number = 30
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    worksheet.cells.get("I20").put_value("Yesterday")

apply_yesterday_rule()
worksheet.auto_fit_column(12)

output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Ejecutar este script generará `TimePeriodExample.xlsx` con el formato condicional que describimos.

## Preguntas Frecuentes y Consejos

- **¿Puedo apuntar a un rango de fechas diferente?**  
  Por supuesto. Cambia `"I19:K20"` a cualquier rango estilo A1 y ajusta las fechas de ejemplo en consecuencia.

- **¿Qué pasa si necesito una fórmula personalizada en lugar de `YESTERDAY`?**  
  Usa `FormatConditionType.FORMULA` y establece `condition.formula1 = "YOUR_FORMULA"`—por ejemplo, `=TODAY()-A1=1` para imitar ayer.

- **¿Cómo aplico múltiples reglas al mismo rango?**  
  Llama a `conditions.add_condition` nuevamente con un `FormatConditionType` diferente. El orden importa; las reglas posteriores pueden sobrescribir a las anteriores.

- **¿Hay una forma de establecer el color de fuente junto con el fondo?**  
  Sí—modifica `condition.style.font.color = Color.white` (o cualquier otro `Color`).

## Conclusión

Ahora sabes cómo **create Excel workbook Python** usando Aspose.Cells, **set cell background color**, y **add conditional formatting python** que formatea celdas por fecha. El script es totalmente funcional, maneja casos límite como directorios inexistentes, y puede ampliarse a escenarios más sofisticados como lógica condicional de múltiples reglas o detección de rangos dinámicos.

¿Listo para el siguiente paso? Prueba cambiar la regla “Yesterday” por “Last Week”, experimenta con rellenos degradados, o genera un informe completo con docenas de tablas formateadas. Los bloques de construcción están aquí, y acabas de dominar el núcleo de **aspose cells conditional formatting** en Python.

¡Feliz codificación, y siéntete libre de compartir tus propias variantes en los comentarios!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Domina el Formato de Celdas de Excel y la Gestión de Libros con Aspose.Cells para .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Cómo crear y guardar un libro de Excel como ODS usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Cómo crear rangos con nombre con alcance de libro en Excel usando Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}