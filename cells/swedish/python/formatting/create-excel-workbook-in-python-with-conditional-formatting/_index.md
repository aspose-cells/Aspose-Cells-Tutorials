---
category: general
date: 2026-09-05
description: Skapa en Excel-arbetsbok i Python och lägg till villkorsstyrd formatering
  för att markera gårdagens celler. Lär dig hela koden och varför varje steg är viktigt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- add conditional formatting excel
- highlight cells based on date
- add conditional formatting range
- how to highlight yesterday cells
language: sv
lastmod: 2026-09-05
og_description: Skapa Excel‑arbetsbok i Python och lägg till villkorsstyrd formatering
  för att markera gårdagens celler. Följ den här steg‑för‑steg‑guiden för en komplett
  lösning.
og_image_alt: Screenshot of an Excel sheet where cells are highlighted after creating
  Excel workbook in Python
og_title: Skapa Excel-arbetsbok i Python – lägg till villkorsstyrd formatering
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
title: Skapa Excel-arbetsbok i Python med villkorsstyrd formatering
url: /sv/python/formatting/create-excel-workbook-in-python-with-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel-arbetsbok i Python med villkorsstyrd formatering

Om du behöver **create Excel workbook python** för en rapportuppgift, visar den här guiden hur du genererar en arbetsbok och tillämpar en villkorsstyrd formateringsregel som markerar gårdagens datum. Du får se den exakta koden, varför varje rad finns, och hur du anpassar lösningen för andra datumintervall.

Villkorsstyrd formatering är ett kraftfullt sätt att uppmärksamma data som uppfyller ett specifikt villkor. I den här handledningen använder vi Aspose.Cells-biblioteket för Python via .NET, som ger fullständigt stöd för Excel-funktioner utan att kräva Microsoft Office. I slutet av guiden har du en fil där celler i området *I19:K20* blir rosa när de innehåller gårdagens datum.

## Förutsättningar

* Python 3.9+ installerat
* `aspose-cells`-paket (installera med `pip install aspose-cells`)
* Grundläggande kunskap om Python-syntax
* Skrivbehörighet till den katalog där arbetsboken kommer att sparas

Koden fungerar på Windows, macOS och Linux så länge .NET-runtime är tillgänglig.

## Skapa Excel-arbetsbok i Python

Det första steget är att instansiera ett `Workbook`-objekt och hämta standardarbetsbladet. Detta objekt representerar hela Excel-filen i minnet.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Varför detta är viktigt*: `Workbook()` skapar en tom arbetsbok med ett enda arbetsblad. Genom att komma åt `worksheets[0]` får du ett handtag för att senare lägga till data, stilar och formatering.

## Lägg till område för villkorsstyrd formatering

Därefter definierar vi området som ska utvärderas av den villkorsstyrda regeln. Området `I19:K20` omfattar sex celler över två rader.

```python
# Define the range that will receive the conditional formatting rule
condition_collection = worksheet.conditional_formattings.add("I19:K20")
```

*Varför detta är viktigt*: Att lägga till en samling för villkorsstyrd formatering till ett specifikt område isolerar regeln, vilket förhindrar att den påverkar orelaterade celler. Detta uppfyller kravet **add conditional formatting range**.

## Definiera regeln: markera celler baserat på datum

Vi skapar nu ett villkor av typen `TIME_PERIOD`. Detta instruerar Excel att jämföra varje cells värde mot ett fördefinierat tidsfönster.

```python
from aspose.cells import FormatConditionType, TimePeriodType

# Add a TIME_PERIOD condition to the collection
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Set the time period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY
```

*Varför detta är viktigt*: `TIME_PERIOD` är den enda inbyggda typen som direkt stödjer “Yesterday”, “Today”, “Last Week” osv. Genom att sätta `condition.time_period` till `YESTERDAY` utvärderar regeln automatiskt varje cells datumvärde mot dagen före det aktuella datumet.

## Styla cellerna som uppfyller villkoret

Villkorsstyrd formatering behöver också en visuell stil. Här väljer vi en rosa solid fyllning för att få de matchande cellerna att sticka ut.

```python
from aspose.pydrawing import Color as DrawingColor
from aspose.cells import BackgroundType

# Apply a pink solid background to cells that satisfy the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID
```

*Varför detta är viktigt*: Stilobjektet definierar hur Excel kommer att rendera celler som uppfyller villkoret. Att använda en solid rosa fyllning uppfyller kravet **highlight cells based on date** och gör resultatet enkelt att verifiera.

## Fyll i exempeldatum för utvärdering

För att se regeln i aktion sätter vi in två datum—ett som faller på gårdagens datum och ett som inte gör det. `number`-formatet `30` motsvarar det inbyggda datumformatet `mm-dd-yy`.

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

*Varför detta är viktigt*: Att tillhandahålla både ett matchande och ett icke‑matchande datum låter dig verifiera att den villkorsstyrda formateringen fungerar korrekt. Justera datumen till den aktuella månaden när du kör skriptet, eller ersätt dem med dynamiska värden.

## Spara arbetsboken

Slutligen skriver vi filen till disk. Konstanten `SaveFormat.XLSX` säkerställer att utdata blir en modern Excel-fil.

```python
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

*Varför detta är viktigt*: Att spara arbetsboken låter dig öppna den i Excel, LibreOffice eller någon annan visare som stödjer XLSX. Den utskrivna sökvägen bekräftar var filen skrevs.

## Fullständigt skript

När alla delar sätts ihop ser det kompletta, körbara skriptet ut så här:

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

### Förväntat resultat

När du öppnar `TimePeriodExample.xlsx`:

* Cell **I19** visas med en rosa bakgrund eftersom dess värde matchar gårdagen.
* Cell **K20** behåller standardbakgrunden eftersom dess datum ligger utanför perioden.
* Etiketten **“Yesterday”** sitter i cell I20 för tydlighet.

## Vanliga varianter och kantfall

| Situation | Justering |
|-----------|------------|
| **Markera idag istället för gårdagen** | Ändra `condition.time_period = TimePeriodType.TODAY`. |
| **Applicera regeln på ett större område** | Uppdatera områdessträngen i `add("I19:K20")` till något liknande `"A1:Z100"`. |
| **Använd en annan fyllningsfärg** | Ersätt `DrawingColor.pink` med någon annan `DrawingColor` (t.ex. `DrawingColor.light_green`). |
| **Arbeta med dynamiska datum** | Beräkna `datetime.now() - timedelta(days=1)` för gårdagen och skriv in det värdet i cellerna innan regeln tillämpas. |

**Pro tip:** När du genererar arbetsboken programatiskt för många användare, håll definitionen av villkorsstyrd formatering separat från datainmatning. På så sätt kan du återanvända samma stil i flera blad utan att duplicera kod.

## Verifiera resultatet programatiskt (valfritt)

Om du vill bekräfta formateringen utan att öppna Excel kan du inspektera en cells stil efter att den sparats:



## Vad bör du lära dig härnäst?

De följande handledningarna täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Excel Automation&#58; Skapa en arbetsbok och lägg till en ListBox med Aspose.Cells för .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Skapa Excel-arbetsbok och lägg till etiketter med Aspose.Cells för Java](/cells/english/java/advanced-excel-charts/data-labeling/)
- [Excel Automation Skapa arbetsbok Lägg till Listbox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}