---
category: general
date: 2026-08-08
description: Skapa Excel-arbetsbok i Python och lägg till villkorsstyrd formatering
  baserat på datum. Steg‑för‑steg‑guide med Aspose.Cells för att markera gårdagens
  celler.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- conditional formatting based on date
- Aspose.Cells Python example
- Excel date formatting Python
- Python Excel automation
language: sv
lastmod: 2026-08-08
og_description: Skapa Excel-arbetsbok i Python med Aspose.Cells och tillämpa villkorsstyrd
  formatering baserad på datum för dynamiska kalkylblad.
og_image_alt: Screenshot of an Excel sheet created with Python showing cells highlighted
  by date conditional formatting
og_title: Skapa Excel-arbetsbok i Python – datumvillkorsstyrd formatering
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
title: Skapa Excel‑arbetsbok med Python‑datum villkorsstyrd formatering
url: /sv/python/formatting/create-excel-workbook-python-date-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel‑arbetsbok Python datum villkorsstyrd formatering

Om du behöver **create Excel workbook Python** och automatiskt markera celler som matchar ett specifikt datum, visar den här handledningen exakt hur. Du kommer att lära dig att tillämpa **conditional formatting based on date** så att gårdagens datum lyser upp i rosa, med Aspose.Cells‑biblioteket.

Guiden går igenom varje steg—från installation av SDK till sparande av den slutliga .xlsx‑filen—så att du kan kopiera‑klistra in ett fungerande exempel i ditt eget projekt. Ingen extern dokumentation behövs; all kod och förklaringar är självständiga.

## Förutsättningar

Innan du börjar, se till att du har:

* Python 3.8 eller nyare installerat.
* `aspose-cells`‑paketet (Python‑omslaget för Aspose.Cells). Installera det med:
  ```bash
  pip install aspose-cells
  ```
* Grundläggande kunskap om Python och Excel‑koncept som arbetsblad och cellstilar.

> **Pro tip:** Aspose.Cells fungerar utan att Microsoft Excel är installerat, vilket gör det idealiskt för server‑sidig automatisering.

## Steg 1: Skapa Excel‑arbetsboken i Python

Den första uppgiften är att instansiera en ny arbetsbok och hämta standardarbetsbladet. Detta objekt representerar hela Excel‑filen och ger åtkomst till rader, kolumner och formaterings‑API:er.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook – this automatically adds one worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]   # reference to the first (default) sheet
```

Att skapa arbetsboken är grunden för all vidare manipulation, oavsett om du lägger till data, formler eller formateringsregler.

## Steg 2: Definiera ett datum‑baserat villkorsformat

Nu lägger vi till **conditional formatting based on date**. `FormatConditionType.TIME_PERIOD`‑enumet låter oss ange inbyggda tidsperioder såsom Yesterday, Today eller LastWeek.

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

Varför detta steg är viktigt: Excel utvärderar villkoret för varje cell i intervallet. När en cells värde faller inom den definierade perioden (igår) appliceras den stil vi har tilldelat automatiskt.

## Steg 3: Fyll intervallet med exempel‑datum

För att se regeln i aktion skriver vi några `datetime`‑objekt till mål‑cellerna. Ett av dem är medvetet satt till gårdagens datum i förhållande till arbetsbokens interna datumssystem.

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

Raden `number = 30` talar om för Excel att visa värdet med sitt standardkort‑datumformat. Du kan ändra detta index till vilket inbyggt talformat som helst om du föredrar en annan presentation.

## Steg 4: Justera kolumnbredd för läsbarhet

Att automatiskt anpassa bredden på kolumnen som innehåller datumen gör utskriften lättare att läsa, särskilt när arbetsboken öppnas i Excel eller en visare.

```python
# Column 12 corresponds to column L (zero‑based indexing)
worksheet.auto_fit_column(12)
```

## Steg 5: Spara arbetsboken till disk

Till sist sparar du arbetsboken som en .xlsx‑fil. Ersätt `"YOUR_DIRECTORY"` med en riktig sökväg på din maskin.

```python
import os

output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

När du öppnar `TimePeriodDemo.out.xlsx` i Excel kommer cell **I19** att visas med rosa bakgrund eftersom dess värde matchar “Yesterday”-regeln, medan **K20** förblir oförändrad.

### Förväntat resultat

| I19 (datum) | I20 (etikett) | J19 | J20 | K19 | K20 (datum) |
|------------|---------------|-----|-----|-----|------------|
| *2008‑07‑30* (rosa bakgrund) | Igår | – | – | – | *2008‑08‑03* (ingen formatering) |

Den rosa skuggningen bekräftar att **conditional formatting based on date** fungerar som avsett.

## Vanliga variationer och edge cases

| Situation | Hur du anpassar koden |
|-----------|-----------------------|
| **Markera “Idag” istället för “Igår”** | Ändra `condition.time_period = TimePeriodType.TODAY` |
| **Applicera regeln på en hel kolumn** | Använd `worksheet.get_range("A:A").format_conditions` |
| **Använd ett anpassat datumintervall (t.ex. de senaste 7 dagarna)** | Ersätt tidsperiod‑villkoret med ett formel‑villkor: <br>```python<br>condition = conditions.add_condition(FormatConditionType.FORMULA)<br>condition.formula1 = 'AND(A1>=TODAY()-7, A1<=TODAY())'<br>``` |
| **Olika bakgrundsfärger** | Sätt `condition.style.background_color = Color.light_green` (eller någon `Color` du föredrar) |
| **Kör på Linux utan en display** | Aspose.Cells är helt huvudlöst; ingen extra konfiguration krävs. |

## Fullt, körbart exempel

Nedan är det kompletta skriptet som du kan köra som‑om det vore färdigt (efter att du uppdaterat utdatamappen). Alla import‑satser, kommentarer och grundläggande felhantering är inkluderade.

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

När du kör skriptet får du en Excel‑fil där “Igår”-cellen automatiskt markeras, vilket demonstrerar **create Excel workbook Python** kombinerat med **conditional formatting based on date**.

## Slutsats

Du vet nu hur du **create Excel workbook Python**‑objekt, definierar ett **date‑based conditional formatting**


## Vad bör du lära dig härnäst?


Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Create an Excel Workbook using Aspose.Cells in Java: A Step‑By‑Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Create Excel Workbook with Charts Using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)
- [Excel Automation: Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}