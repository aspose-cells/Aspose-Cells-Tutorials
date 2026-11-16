---
category: general
date: 2026-11-16
description: Crea formato condicional en Excel usando Python. Aprende a agregar un
  rango de formato condicional, resaltar fechas y crear un libro de trabajo programáticamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting
- create excel workbook python
- how to highlight dates
- add conditional formatting range
- add conditional formatting python
language: es
lastmod: 2026-11-16
og_description: Crea formato condicional en Excel con Python. Este tutorial muestra
  cómo agregar un rango de formato condicional, resaltar fechas y generar un libro
  de trabajo.
og_image_alt: Screenshot of Excel sheet with conditional formatting applied using
  Python
og_title: Crear formato condicional en Excel con Python – guía paso a paso
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create conditional formatting in Excel using Python. Learn to add a
    conditional formatting range, highlight dates, and build a workbook programmatically.
  headline: How to create conditional formatting in Excel with Python
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Cómo crear formato condicional en Excel con Python
url: /es/python/formatting/how-to-create-conditional-formatting-in-excel-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear formato condicional en Excel con Python

Si necesitas **crear formato condicional** en un archivo Excel mientras trabajas en Python, esta guía te muestra exactamente cómo hacerlo. Aprenderás a **crear excel workbook python**‑style, definir un rango de formato y resaltar fechas sin salir del IDE.

El formato condicional te permite señalar visualmente celdas que cumplen criterios específicos—perfecto para paneles, informes o hojas de validación de datos. Al final de este tutorial tendrás un libro de trabajo completamente funcional que colorea de rosa las celdas con fecha “Yesterday” mientras el resto del rango permanece verde.

## Lo que lograrás

* Construir un nuevo libro de trabajo desde cero.  
* Añadir una colección de formato‑condicional para un bloque de celdas específico.  
* Aplicar una regla **TIME_PERIOD** que resalta fechas (el escenario “cómo resaltar fechas”).  
* Guardar el archivo como un libro XLSX listo para procesamiento posterior.

**Requisitos previos**  
* Python 3.8+  
* Paquete Python `aspose-cells` (`pip install aspose-cells`)  
* Familiaridad básica con el módulo `datetime` de Python  

---

## Cómo crear formato condicional en Python

El primer paso es configurar el libro de trabajo y la hoja que alojará las reglas de formato.

```python
# Step 1: Import required classes and create a new workbook
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Instantiate a blank workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Optional: auto‑fit column 12 (L) to make the output readable
worksheet.auto_fit_column(12)
```

**Por qué es importante** – `Workbook` es el punto de entrada para todas las operaciones de Excel. Crear el libro de trabajo programáticamente reemplaza el paso manual “Archivo → Nuevo”, habilitando pipelines de informes automatizados.

---

## Preparando la colección de formato‑condicional – añadir rango de formato condicional

A continuación definimos el bloque de celdas que recibirá la regla. En este ejemplo el rango es **I19:K20**.

```python
# Step 2: Create a conditional‑format collection for the target range
conds = worksheet.conditional_formattings.add("I19:K20")

# Apply a base style (green background) that will show when no rule matches
conds[0].style.background_color = Color.medium_sea_green
conds[0].style.pattern = BackgroundType.SOLID
```

**Explicación** – `conditional_formattings.add` registra una nueva colección vinculada a la cadena de dirección. La primera condición (`conds[0]`) funciona como estilo “predeterminado”; la regla posterior lo sobrescribirá cuando se cumplan sus criterios.

---

## Añadiendo una condición TIME_PERIOD – cómo resaltar fechas

Ahora añadimos la lógica que identifica fechas “Yesterday” y las pinta de rosa.

```python
# Step 3: Add a TIME_PERIOD condition that highlights cells dated “Yesterday”
idx = conds.add_condition(FormatConditionType.TIME_PERIOD)   # returns the new index
condition = conds[idx]

# Define the visual style for cells that satisfy the condition
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Set the rule to the built‑in YESTERDAY period
condition.time_period = TimePeriodType.YESTERDAY
```

**¿Por qué usar TIME_PERIOD?** – Aspose.Cells proporciona enumeraciones integradas como `YESTERDAY`, `TODAY` y `LAST_WEEK`. Evalúan el valor de fecha de la celda contra la fecha del sistema actual, eliminando la necesidad de fórmulas personalizadas.

---

## Poblando datos de ejemplo – demostrar la regla

Para ver el formato en acción insertamos una fecha que coincide con la regla y otra que no.

```python
# Step 4: Populate sample dates so the rule can be seen

# Cell I19 gets a date that is “yesterday” relative to 2008‑07‑31
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))  # yesterday for the example
style = cell_i19.get_style()
style.number = 30                         # full date format (e.g., 7/30/2008)
cell_i19.set_style(style)

# Cell K20 gets a later date – it should stay green
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))   # a future date
style = cell_k20.get_style()
style.number = 30
cell_k20.set_style(style)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

**Nota sobre casos límite** – La regla `TIME_PERIOD` funciona solo con fechas *reales*. Si una celda contiene texto (p. ej., “N/A”), la regla se ignora, evitando cambios de color inesperados.

---

## Guardando el libro de trabajo – add conditional formatting python

Finalmente, escribe el libro de trabajo en disco. El archivo puede abrirse en cualquier programa de hojas de cálculo para verificar los colores.

```python
# Step 5: Save the workbook
output_path = "TimePeriodExample.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

**Resultado esperado**  

| I19 (green → pink) | J19 (green) | K19 (green) |
|--------------------|------------|------------|
| 7/30/2008 (yesterday) | – | – |
| **I20**: “Yesterday” label | – | – |
| I21‑K21 (green)    | – | – |

La celda **I19** aparece con fondo rosa porque su fecha coincide con el período “Yesterday”, mientras que **K20** permanece verde.

---

## Preguntas frecuentes y consejos prácticos

* **¿Puedo usar un rango de fechas personalizado en lugar de un período incorporado?**  
  Sí. Reemplaza `condition.time_period` por `condition.formula1 = "TODAY()-1"` y establece `condition.type = FormatConditionType.FORMULA`.

* **¿Qué pasa si mi libro de trabajo ya contiene datos?**  
  Usa `worksheet.cells.import_data` para cargar datos en bloque antes de añadir la colección de formato condicional.

* **¿Rendimiento con hojas grandes?**  
  Añadir muchas condiciones puede ralentizar el renderizado. Agrupa celdas con la misma regla en un solo rango (p. ej., “A1:C1000”) para mantener bajo el número de condiciones.

* **¿Compatibilidad multiplataforma?**  
  El archivo XLSX generado sigue el estándar Office Open XML, por lo que funciona en aplicaciones de hojas de cálculo en Windows, macOS y Linux.

---

## Conclusión

Ahora sabes cómo **crear formato condicional** en un libro de trabajo Excel usando Python. El tutorial cubrió la creación del libro, la definición de un **add conditional formatting range**, la aplicación de una regla **how to highlight dates**, y el guardado del archivo—todo con el enfoque **add conditional formatting python** proporcionado por Aspose.Cells.

A partir de aquí puedes:

* Extender el conjunto de reglas con otros valores `TimePeriodType` (p. ej., `TODAY`, `LAST_MONTH`).  
* Combinar múltiples condiciones en el mismo rango para obtener indicaciones visuales más ricas.  
* Integrar este flujo de trabajo en pipelines de informes automatizados o servicios web.

¡Feliz codificación, y siéntete libre de experimentar con diferentes colores, rangos y lógica de fechas para adaptar tus necesidades de reporte!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Create Excel workbook Python date conditional formatting](/cells/english/python/formatting/create-excel-workbook-python-date-conditional-formatting/)
- [How to apply time period conditional formatting in Excel using Python](/cells/english/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/)
- [Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting](/cells/english/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}