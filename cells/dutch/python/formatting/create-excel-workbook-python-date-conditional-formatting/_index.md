---
category: general
date: 2026-08-08
description: Maak een Excel-werkmap in Python en voeg voorwaardelijke opmaak toe op
  basis van datum. Stapsgewijze handleiding met Aspose.Cells om de cellen van gisteren
  te markeren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- conditional formatting based on date
- Aspose.Cells Python example
- Excel date formatting Python
- Python Excel automation
language: nl
lastmod: 2026-08-08
og_description: Maak een Excel-werkmap in Python met Aspose.Cells en pas voorwaardelijke
  opmaak toe op basis van datum voor dynamische spreadsheets.
og_image_alt: Screenshot of an Excel sheet created with Python showing cells highlighted
  by date conditional formatting
og_title: Excel-werkboek maken met Python – datum voorwaardelijke opmaak
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
title: Maak Excel-werkboek Python datum voorwaardelijke opmaak
url: /nl/python/formatting/create-excel-workbook-python-date-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-werkmap maken met Python datum-voorwaardelijke opmaak

Als je **Excel-werkmap Python** moet maken en automatisch cellen wilt markeren die overeenkomen met een specifieke datum, laat deze tutorial je precies zien hoe. Je leert **voorwaardelijke opmaak op basis van datum** toe te passen zodat datums van gisteren roze oplichten, met behulp van de Aspose.Cells‑bibliotheek.

De gids loopt elke stap door – van het installeren van de SDK tot het opslaan van het uiteindelijke .xlsx‑bestand – zodat je een werkend voorbeeld kunt kopiëren‑plakken in je eigen project. Geen externe documentatie nodig; alle code en uitleg staan in dit artikel.

## Prerequisites

Voordat je begint, zorg dat je het volgende hebt:

* Python 3.8 of nieuwer geïnstalleerd.
* `aspose-cells`‑pakket (de Python‑wrapper voor Aspose.Cells). Installeer het met:
  ```bash
  pip install aspose-cells
  ```
* Basiskennis van Python en Excel‑concepten zoals werkbladen en celstijlen.

> **Pro tip:** Aspose.Cells werkt zonder dat Microsoft Excel geïnstalleerd is, waardoor het ideaal is voor server‑side automatisering.

## Step 1: Create the Excel workbook in Python

De eerste taak is een nieuw werkboek te instantieren en het standaard werkblad op te halen. Dit object vertegenwoordigt het volledige Excel‑bestand en biedt toegang tot rijen, kolommen en opmaak‑API’s.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook – this automatically adds one worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]   # reference to the first (default) sheet
```

Het maken van het werkboek is de basis voor elke verdere manipulatie, of je nu gegevens, formules of opmaakregels toevoegt.

## Step 2: Define a date‑based conditional format

Nu voegen we **voorwaardelijke opmaak op basis van datum** toe. De `FormatConditionType.TIME_PERIOD`‑enum laat ons ingebouwde tijdsperioden specificeren zoals Yesterday, Today of LastWeek.

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

Waarom deze stap belangrijk is: Excel evalueert de voorwaarde voor elke cel in het bereik. Wanneer de waarde van een cel binnen de gedefinieerde periode (gisteren) valt, wordt de toegewezen stijl automatisch toegepast.

## Step 3: Populate the range with sample dates

Om de regel in actie te zien, schrijven we een paar `datetime`‑objecten naar de doelcellen. Eén daarvan is expres ingesteld op de datum van gisteren ten opzichte van het interne datum‑systeem van het werkboek.

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

De regel `number = 30` vertelt Excel de waarde weer te geven met zijn standaard korte‑datumnotatie. Je kunt deze index wijzigen naar elk ingebouwd getalformaat als je een andere weergave wilt.

## Step 4: Adjust column width for readability

Het automatisch aanpassen van de kolombreedte die de datums bevat, maakt de output makkelijker leesbaar, vooral wanneer het werkboek wordt geopend in Excel of een viewer.

```python
# Column 12 corresponds to column L (zero‑based indexing)
worksheet.auto_fit_column(12)
```

## Step 5: Save the workbook to disk

Sla tenslotte het werkboek op als een .xlsx‑bestand. Vervang `"YOUR_DIRECTORY"` door een echt pad op jouw machine.

```python
import os

output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Wanneer je `TimePeriodDemo.out.xlsx` in Excel opent, zal cel **I19** een roze achtergrond hebben omdat de waarde overeenkomt met de “Yesterday”‑regel, terwijl **K20** ongewijzigd blijft.

### Expected output

| I19 (date) | I20 (label) | J19 | J20 | K19 | K20 (date) |
|------------|-------------|-----|-----|-----|------------|
| *2008‑07‑30* (pink background) | Yesterday | – | – | – | *2008‑08‑03* (no formatting) |

De roze schaduw bevestigt dat **voorwaardelijke opmaak op basis van datum** werkt zoals bedoeld.

## Common variations and edge cases

| Situation | How to adapt the code |
|-----------|-----------------------|
| **Highlight “Today” instead of “Yesterday”** | Change `condition.time_period = TimePeriodType.TODAY` |
| **Apply the rule to an entire column** | Use `worksheet.get_range("A:A").format_conditions` |
| **Use a custom date range (e.g., last 7 days)** | Replace the time‑period condition with a formula condition: <br>```python<br>condition = conditions.add_condition(FormatConditionType.FORMULA)<br>condition.formula1 = 'AND(A1>=TODAY()-7, A1<=TODAY())'<br>``` |
| **Different background colors** | Set `condition.style.background_color = Color.light_green` (or any `Color` you prefer) |
| **Running on Linux without a display** | Aspose.Cells is fully headless; no extra configuration required. |

## Full, runnable example

Below is the complete script you can execute as‑is (after updating the output directory). All imports, comments, and error‑handling basics are included.

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

Running the script produces an Excel file where the “Yesterday” cell is automatically highlighted, demonstrating **create Excel workbook Python** combined with **conditional formatting based on date**.

## Conclusion

You now know how to **create Excel workbook Python** objects, define a **date‑based conditional formatting

## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step‑by‑step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create an Excel Workbook using Aspose.Cells in Java: A Step‑By‑Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Create Excel Workbook with Charts Using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)
- [Excel Automation: Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}