---
category: general
date: 2026-07-06
description: Crear libro de Excel en Python con código para establecer el color de
  fondo de una celda, aplicar estilo a la celda programáticamente y añadir formato
  condicional en Python para resaltar la fecha de hoy.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- set cell style programmatically
- highlight today date excel
- add conditional formatting python
language: es
lastmod: 2026-07-06
og_description: Crea un libro de Excel con Python al instante. Aprende a establecer
  el color de fondo de una celda, aplicar estilo a la celda programáticamente y añadir
  formato condicional en Python para resaltar la fecha de hoy.
og_image_alt: Screenshot of an Excel workbook created with Python showing colored
  cells and today’s date highlighted
og_title: Crear libro de Excel con Python – Estilizar celdas y resaltar hoy
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: Create Excel workbook Python with code to set cell background color,
    set cell style programmatically, and add conditional formatting python for highlighting
    today’s date.
  headline: Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting
  type: TechArticle
- description: Create Excel workbook Python with code to set cell background color,
    set cell style programmatically, and add conditional formatting python for highlighting
    today’s date.
  name: Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting
  steps:
  - name: Converting a range like `"A1:C3"` into a `CellArea`.
    text: Converting a range like `"A1:C3"` into a `CellArea`.
  - name: Filling every cell in that area with a sequential number (just for demo
      purposes).
    text: Filling every cell in that area with a sequential number (just for demo
      purposes).
  - name: Applying a solid **set cell background color**.
    text: Applying a solid **set cell background color**.
  - name: Adding a conditional rule that **highlight today date excel**.
    text: Adding a conditional rule that **highlight today date excel**.
  type: HowTo
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Crear libro de Excel con Python – Guía completa de estilo y formato condicional
url: /es/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear libro de Excel con Python – Guía completa de estilo y formato condicional

¿Alguna vez te has preguntado cómo **crear libro de Excel con Python** desde cero sin abrir Excel tú mismo? No estás solo. Muchos desarrolladores necesitan generar informes, paneles o incluso simples registros de datos al vuelo, y hacerlo programáticamente ahorra horas de trabajo manual.

En este tutorial recorreremos todo el proceso: desde crear un libro de trabajo nuevo, hasta **establecer color de fondo de celda**, **establecer estilo de celda programáticamente**, y finalmente **resaltar fecha de hoy en Excel** usando **añadir formato condicional python**. Al final tendrás un script listo para ejecutar que produce un archivo .xlsx pulido en segundos.

---

## Lo que construirás

- Un archivo de Excel nuevo con algunas celdas pobladas.
- Celdas coloreadas con un fondo personalizado.
- Valores numéricos y de fecha formateados con un estilo numérico específico.
- Una regla condicional que resalta automáticamente la celda que contiene la fecha de hoy.

No se requiere una instalación externa de Excel—Aspose.Cells para Python vía .NET realiza todo el trabajo pesado.

---

## Prerequisitos

| Requisito | Por qué es importante |
|-------------|------------------------|
| Python 3.8+ | Sintaxis moderna y anotaciones de tipo |
| `aspose-cells` package | Biblioteca central para la manipulación de libros de trabajo |
| `aspose-pydrawing` (instalado con Aspose.Cells) | Proporciona la clase `Color` |
| Familiaridad básica con conceptos de Excel (celdas, rangos, formato) | Hace que el tutorial fluya con mayor facilidad |

Instala la biblioteca con:

```bash
pip install aspose-cells
```

---

## Paso 1: Inicializar el libro de trabajo y la hoja de cálculo

Lo primero que haces cuando **creas libro de Excel con Python** es instanciar un objeto `Workbook` y obtener la hoja de cálculo predeterminada. Piensa en el libro de trabajo como todo el archivo de Excel, mientras que la hoja de cálculo es una sola pestaña dentro de él.

```python
from aspose.cells import Workbook

# Create a new workbook – this is our empty Excel file
book = Workbook()

# Grab the first (default) worksheet
sheet = book.worksheets[0]
```

> **Consejo profesional:** Si necesitas varias hojas, usa `book.worksheets.add("MySheet")` para añadir más pestañas.

---

## Paso 2: Clase auxiliar para estilo y formato condicional

A continuación tienes una clase compacta pero completa `ConditionalFormatting`. Envuelve las tareas repetitivas de:

1. Convertir un rango como `"A1:C3"` en un `CellArea`.
2. Rellenar cada celda en esa área con un número secuencial (solo para demostración).
3. Aplicar un sólido **establecer color de fondo de celda**.
4. Añadir una regla condicional que **resaltar fecha de hoy en Excel**.

```python
from aspose.cells import (
    CellArea, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat, CellsHelper
)
from aspose.pydrawing import Color
from datetime import datetime

class ConditionalFormatting:
    """
    Utility class that demonstrates how to:
    • set cell background color
    • set cell style programmatically
    • add conditional formatting python
    """
    def __init__(self, worksheet):
        self._sheet = worksheet

    def get_format_condition(self, cell_range: str, color: Color):
        """
        Creates a conditional formatting object for the given range
        and fills the range with a background color.
        """
        index = self._sheet.conditional_formattings.add()
        cf = self._sheet.conditional_formattings[index]

        # Convert "A1:C3" → CellArea object
        area = self.get_cell_area_by_name(cell_range)
        cf.add_area(area)

        # Paint the whole area with the supplied color
        self.fill_cell(cell_range, color)
        return cf

    def fill_cell(self, cell_range: str, color: Color):
        """
        Populates each cell in the range with an incrementing integer
        and applies the supplied background color.
        """
        area = self.get_cell_area_by_name(cell_range)
        counter = 0
        for col in range(area.start_column, area.end_column + 1):
            for row in range(area.start_row, area.end_row + 1):
                cell = self._sheet.cells.get(row, col)

                # Apply background only if a real color is supplied
                if color != Color.empty:
                    style = cell.get_style()
                    style.foreground_color = color
                    style.pattern = BackgroundType.SOLID
                    cell.set_style(style)

                cell.put_value(counter)
                counter += 1

    @staticmethod
    def get_cell_area_by_name(name: str) -> CellArea:
        """
        Parses an Excel‑style address (e.g. "B2:D4") into a CellArea.
        """
        area = CellArea()
        parts = name.replace("$", "").split(':')

        start_row, start_col = CellsHelper.cell_name_to_index(parts[0])
        area.start_row = start_row
        area.start_column = start_col

        if len(parts) == 2:
            end_row, end_col = CellsHelper.cell_name_to_index(parts[1])
            area.end_row = end_row
            area.end_column = end_col
        else:
            area.end_row = start_row
            area.end_column = start_col
        return area

    # -----------------------------------------------------------------
    # Step 2: Add conditional formatting for TODAY
    # -----------------------------------------------------------------
    def add_time_period_1(self):
        """
        Demonstrates add conditional formatting python that highlights
        cells containing today’s date.
        """
        # 1️⃣ Create a formatting range and give it a neutral background
        cf = self.get_format_condition("I1:K2", Color.light_slate_gray)

        # 2️⃣ Add a TIME_PERIOD condition (Today)
        idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
        cond = cf[idx]
        cond.time_period = TimePeriodType.TODAY
        cond.style.background_color = Color.pink
        cond.style.pattern = BackgroundType.SOLID

        # 3️⃣ Populate the cells with date values
        # Cell I1 – today’s date, formatted as a date
        cell = self._sheet.cells.get("I1")
        style = cell.get_style()
        style.number = 30               # 30 = “mm-dd-yy” style in Aspose
        cell.set_style(style)
        cell.put_value(datetime.today())

        # Cell K2 – an arbitrary past date for contrast
        self._sheet.cells.get("K2").put_value(datetime(2008, 7, 30))

        # Cell I2 – a label so the reader knows what’s being highlighted
        self._sheet.cells.get("I2").put_value("Today")
```

### ¿Por qué una clase auxiliar?

- **Reusabilidad:** Puedes llamar a `add_time_period_1()` para cualquier hoja de cálculo sin reescribir la lógica.
- **Claridad:** Cada método hace una sola cosa – una característica del código limpio.
- **Extensibilidad:** ¿Quieres añadir más reglas? Simplemente agrega otro método siguiendo el mismo patrón.

---

## Paso 3: Aplicar el formato y guardar el archivo

Ahora unimos todo: instanciamos la clase auxiliar, ejecutamos la rutina de formato y finalmente escribimos el libro de trabajo en disco.

```python
# Instantiate the helper with our worksheet
formatter = ConditionalFormatting(sheet)

# Fill a demo range with numbers and a light blue background
formatter.get_format_condition("A1:C3", Color.light_sky_blue)

# Add the “today” conditional rule
formatter.add_time_period_1()

# Save the workbook – choose any location you like
output_path = "styled_workbook.xlsx"
book.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

Cuando abras *styled_workbook.xlsx* deberías ver:

- Celdas **A1:C3** numeradas del 0‑8 con un relleno azul cielo claro.
- Celda **I1** mostrando la fecha de hoy con fondo rosa (gracias a la regla condicional).
- Celda **K2** mostrando la fecha estática *2008‑07‑30* para comparación.
- Celda **I2** contiene el texto “Today”.

Esa pista visual es exactamente lo que solicita el requisito de **resaltar fecha de hoy en Excel**.

---

## Paso 4: Profundizar – Personalizar estilos

Si necesitas ajustar fuentes, bordes o formatos numéricos, puedes extender el método `fill_cell` o crear una nueva clase auxiliar:

```python
def apply_custom_style(cell, font_name="Calibri", font_size=11, bold=False):
    style = cell.get_style()
    style.font.name = font_name
    style.font.size = font_size
    style.font.bold = bold
    cell.set_style(style)
```

Podrías entonces llamar a `apply_custom_style(cell, bold=True)` dentro del bucle para **establecer estilo de celda programáticamente** para cada celda en un rango.

---

## Problemas comunes y cómo evitarlos

| Síntoma | Causa probable | Solución |
|---------|----------------|----------|
| Las celdas permanecen blancas a pesar de `Color.light_sky_blue` | El estilo no se aplicó después de establecer `foreground_color` | Siempre llama a `cell.set_style(style)` después de modificar el objeto de estilo. |
| La regla condicional nunca se activa | `style.number` no está configurado para celdas de fecha, por lo que Excel trata el valor como una cadena | Establece `style.number = 30` (o cualquier formato de fecha) antes de `cell.put_value(datetime…)`. |
| El libro se guarda como .xls a pesar de `SaveFormat.XLSX` | Versión antigua de Aspose que por defecto usa el formato legado | Actualiza al último paquete `aspose-cells`. |
| Rango como `"A1"` genera un error de índice | Usar `cells.get("A1")` en una hoja que no ha sido inicializada | Asegúrate de que la hoja de cálculo exista (existe justo después de `Workbook()`), o usa `cells.get(row, col)` con índices basados en cero. |

---

## Script completo para copiar y pegar

A continuación tienes el **script completo** que puedes colocar en un archivo llamado `create_excel.py` y ejecutar de inmediato.

```python
# create_excel.py
from aspose.cells import (
    Workbook, CellArea, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat, CellsHelper
)
from aspose.pydrawing import Color
from datetime import datetime

class ConditionalFormatting:
    """Utility for styling cells and adding conditional formatting."""
    def __init__(self, worksheet):
        self._sheet = worksheet

    def get_format_condition(self, cell_range: str, color: Color):
        index = self._sheet.conditional_formattings.add()
        cf = self._sheet.conditional_formattings[index]
        area = self.get_cell_area_by_name(cell_range)
        cf.add_area(area)
        self.fill_cell(cell_range, color)
        return cf

    def fill_cell(self, cell_range: str, color: Color):
        area = self.get_cell_area_by_name(cell_range)
        counter = 0
        for col in range(area.start_column, area.end_column + 1):
            for row in range(area.start_row, area.end_row + 1):
                cell = self._sheet.cells.get(row, col)
                if color != Color.empty:
                    style = cell.get_style()
                    style.foreground_color = color
                    style.pattern = BackgroundType.SOLID
                    cell.set_style(style)
                cell.put_value(counter)
                counter += 1

    @staticmethod
    def get_cell_area_by_name(name:


## ¿Qué deberías aprender a continuación?


Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Automatización de Excel con Aspose.Cells .NET: crear libro de trabajo y establecer enlaces externos](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Domina el formato de celdas de Excel y la gestión de libros de trabajo con Aspose.Cells para .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Automatización de Excel: crear un libro de trabajo y añadir un ListBox usando Aspose.Cells para .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}