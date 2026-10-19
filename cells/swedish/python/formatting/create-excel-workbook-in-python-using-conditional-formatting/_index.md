---
category: general
date: 2026-09-21
description: Lär dig hur du skapar en Excel-arbetsbok i Python, sätter cellbakgrundsfärg
  och tillämpar datumbaserad villkorsstyrd formatering med Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- excel conditional formatting python
- date based conditional formatting
language: sv
lastmod: 2026-09-21
og_description: Skapa Excel-arbetsbok i Python, sätt cellbakgrundsfärg och tillämpa
  datumbaserad villkorsformatering med Aspose.Cells. Följ den steg‑för‑steg‑guiden.
og_image_alt: Screenshot of an Excel sheet showing a yellow‑green cell background
  for yesterday's dates
og_title: Skapa Excel-arbetsbok i Python med villkorsstyrd formatering
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
title: Skapa Excel‑arbetsbok i Python med villkorsstyrd formatering
url: /sv/python/formatting/create-excel-workbook-in-python-using-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel-arbetsbok i Python med villkorsstyrd formatering

Om du behöver **create Excel workbook python**-skript som automatiskt markerar datum, visar den här guiden exakt hur. Du kommer att se hur du **set cell background color**, lägger till en “Yesterday”-regel och sparar filen—allt med Aspose.Cells för Python.

Att arbeta med Excel-filer programatiskt innebär ofta att upprepa samma formateringslogik över många blad. I slutet av den här handledningen har du ett återanvändbart mönster för **excel conditional formatting python** som du kan släppa in i vilket projekt som helst.

## Förutsättningar

- Python 3.8+ installerat  
- `aspose-cells`-paketet (`pip install aspose-cells`)  
- Grundläggande kunskap om Python-funktioner och datetime-modulen  

Inga ytterligare bibliotek krävs; Aspose.Cells hanterar alla Excel‑operationer.

## Steg 1: Skapa arbetsboken och öppna det första kalkylbladet

Det första steget är att **create excel workbook python**-objekt och hämta standardkalkylbladet. Detta ger dig en ren canvas för vidare styling.

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

*Varför detta är viktigt:* `Workbook()` skapar en Excel‑fil i minnet. Att komma åt `worksheets[0]` undviker hårdkodade bladnamn och fungerar även om standardnamnet ändras.

## Steg 2: Hjälpfunktion för att lägga till ett TIME_PERIOD‑villkorsformat

För att hålla koden prydlig omsluter vi skapandet av villkorsformatet i en hjälpfunktion. Den tar emot ett cellområde, en bakgrundsfärg och den önskade tidsperiodregeln.

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

*Varför detta är viktigt:* Hjälpfunktionen abstraherar de repetitiva stegen för att skapa ett villkorsformat, vilket gör det enkelt att återanvända för andra datumbaserade regler som “Today” eller “Last Week”.

## Steg 3: Tillämpa “Yesterday”-regeln på ett område

Nu använder vi hjälpfunktionen för att markera celler som innehåller gårdagens datum. Området `I19:K20` blir **medium sea green** när villkoret uppfylls.

```python
add_time_period(
    worksheet,
    "I19:K20",                # range to format
    Color.medium_sea_green,  # set cell background color
    TimePeriodType.YESTERDAY # date based conditional formatting
)
```

*Varför detta är viktigt:* `TimePeriodType.YESTERDAY` är en del av Aspose.Cells inbyggda uppräkning, så du behöver inte beräkna datum manuellt. Biblioteket utvärderar regeln varje gång arbetsboken öppnas.

## Steg 4: Fyll området med exempeldatum

För att se regeln i aktion skriver vi två datum—ett som matchar “Yesterday” och ett som inte gör det. `number`‑stilen `30` motsvarar ett inbyggt datumformat.

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

*Varför detta är viktigt:* Genom att infoga konkreta datum kan du verifiera att villkorsformateringen fungerar utan att behöva öppna filen på en specifik dag.

## Steg 5: Lägg till en beskrivande etikett och auto‑fit kolumnen

En liten etikett förtydligar syftet med det formaterade området, och `auto_fit_column` gör bladet läsbart.

```python
# Add a label under the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Adjust column width for better visibility (column 12 = L)
worksheet.auto_fit_column(12)
```

## Steg 6: Spara arbetsboken

Slutligen skriver du arbetsboken till disk. Anropet `os.makedirs` säkerställer att målmappen finns.

```python
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)

# Save as XLSX – the most widely supported Excel format
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

När du öppnar *TimePeriodDemo.xlsx* kommer du att se:

- Cell **I19** skuggad **medium sea green** eftersom dess värde matchar “Yesterday”-regeln.  
- Cell **K20** behåller standardbakgrunden eftersom dess datum inte uppfyller villkoret.  

Detta demonstrerar **format cells by date** med en enda rad Python‑kod.

## Fullt, körbart exempel

När alla delar sätts ihop, här är det kompletta skriptet som du kan kopiera‑klistra in och köra:

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

Kör skriptet, öppna den resulterande filen, och du kommer att se villkorsformateringen i aktion.

## Vanliga variationer och kantfall

| Variation | Hur man implementerar | När man använder |
|-----------|----------------------|------------------|
| **Markera “Today”** | Byt ut `TimePeriodType.YESTERDAY` mot `TimePeriodType.TODAY` | Real‑time‑instrumentpanel |
| **Flera områden** | Anropa `add_time_period` för varje område och skicka olika färger | Komplexa rapporter |
| **Dynamiskt datumintervall** | Använd `TimePeriodType.LAST_7_DAYS` eller `TimePeriodType.NEXT_MONTH` | Rullande rapporter |
| **Anpassad färg** | Använd `Color.from_argb(255, r, g, b)` för att skapa vilken nyans som helst | Varumärkeskonsekvent styling |

**Pro tip:** Sätt alltid `condition.style.pattern = BackgroundType.SOLID` när du vill ha en solid fyllning; annars kan Excel visa en gradient som ser inkonsekvent ut mellan versioner.

## Slutsats

Du vet nu hur du skapar **create Excel workbook python**‑skript som **set cell background color**, tillämpar **excel conditional formatting python** och **format cells by date** med Aspose.Cells. Exemplet täcker ett **date based conditional formatting**‑scenario, men samma mönster fungerar för vilken tidsperiodregel som helst.

Nästa steg kan du utforska:

- Lägga till databars eller ikonsätt (`FormatConditionType.DATA_BAR`)  
- Kombinera flera villkorsregler på samma område  
- Exportera arbetsboken till PDF (`SaveFormat.PDF`) för rapportering  

Känn dig fri att experimentera med olika färger, områden och tidsperiodtyper för att passa dina specifika rapporteringsbehov. Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Behärska Excel-cellformatering och arbetsbokshantering med Aspose.Cells för .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Excel‑automatisering med Aspose.Cells .NET&#58; Skapa arbetsbok och ange externa länkar](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Hur man skapar arbetsboks‑specifika namngivna områden i Excel med Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}