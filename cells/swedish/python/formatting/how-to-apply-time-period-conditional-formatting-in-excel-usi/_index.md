---
category: general
date: 2026-09-15
description: Lär dig hur du tillämpar villkorsstyrd formatering för tidsperioder och
  sparar arbetsboken som XLSX med Aspose.Cells i Python. Inkluderar steg‑för‑steg‑kod.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- time period conditional formatting
- save workbook as xlsx
- how to create excel workbook python
- how to highlight yesterday in excel
- add conditional formatting python
language: sv
lastmod: 2026-09-15
og_description: Tillämpa villkorsstyrd formatering för tidsperioder i Excel med Python
  och spara arbetsboken som XLSX. Följ den här kompletta guiden för Aspose.Cells.
og_image_alt: Screenshot of an Excel sheet where the cells for yesterday are highlighted
  in pink
og_title: Tillämpa villkorsstyrd formatering för tidsperioder i Excel med Python
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  headline: How to apply time period conditional formatting in Excel using Python
  type: TechArticle
- description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  name: How to apply time period conditional formatting in Excel using Python
  steps:
  - name: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
    text: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
  - name: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
    text: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
  - name: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
    text: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
  - name: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
    text: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
  - name: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
    text: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
  - name: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
    text: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
  - name: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
    text: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
  - name: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
    text: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
  - name: The cell `I20` shows the text “Yesterday”.
    text: The cell `I20` shows the text “Yesterday”.
  - name: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
    text: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Hur man tillämpar tidsperiodvillkorsformatering i Excel med Python
url: /sv/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så applicerar du tidsperiodvillkorformattering i Excel med Python

Om du behöver **time period conditional formatting** i en Excel‑fil, visar den här handledningen exakt hur du gör det med Python. Du får ett komplett, körbart exempel som skapar en arbetsbok, markerar gårdagens datum och **save workbook as XLSX** på bara några kodrader.

Villkorsformatering är ett kraftfullt sätt att uppmärksamma data som uppfyller ett specifikt villkor. I den här guiden fokuserar vi på tidsperioden “Yesterday”, men samma mönster fungerar för andra inbyggda perioder såsom Today, LastWeek och NextMonth. I slutet av handledningen kommer du att kunna skapa **how to create excel workbook python**‑stil‑skript som är redo för produktion.

## Förutsättningar

- Python 3.8+ installerat  
- `aspose-cells` och `aspose-pydrawing` paket (`pip install aspose-cells aspose-pydrawing`)  
- Grundläggande kunskap om Python‑syntax  

Ingen extra Office‑installation krävs eftersom Aspose.Cells hanterar filgenereringen internt.

## Tidsperiodvillkorformattering med Aspose.Cells i Python

Detta avsnitt går igenom varje kodrad som behövs för huvuduppgiften. Kodblocket nedan är hela skriptet; kommentarer förklarar syftet med varje steg.

```python
# -*- coding: utf-8 -*-
"""
Apply time period conditional formatting to highlight yesterday's dates
and save the workbook as XLSX using Aspose.Cells for Python.
"""

from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the range that will receive the conditional formatting rule
cell_range = "I19:K20"
cond_format = worksheet.conditional_formattings.add(cell_range)

# Step 3: Add a TIME_PERIOD condition for “Yesterday” and style it
condition_index = cond_format.add_condition(FormatConditionType.TIME_PERIOD)
condition = cond_format[condition_index]
condition.style.background_color = Color.pink          # Highlight colour
condition.style.pattern = BackgroundType.SOLID        # Solid fill
condition.time_period = TimePeriodType.YESTERDAY      # Built‑in “Yesterday” period

# Step 4: Populate the range with sample dates (Excel number format 30 = short date)
date_cells = ["I19", "K20"]                           # Cells that will contain dates
sample_dates = [datetime(2008, 7, 30), datetime(2008, 8, 3)]
for cell_ref, date_val in zip(date_cells, sample_dates):
    cell = worksheet.cells.get(cell_ref)
    cell.put_value(date_val)                         # Write the Python datetime
    style = cell.get_style()
    style.number = 30                                 # Excel short date format
    cell.set_style(style)

# Step 5: Add a label so the user knows what the rule represents
worksheet.cells.get("I20").put_value("Yesterday")

# Step 6: Auto‑fit the column for better readability (column L is index 12)
worksheet.auto_fit_column(12)

# Step 7: Save the workbook – this demonstrates “save workbook as xlsx”
output_path = "TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

### Varför varje steg är viktigt

1. **Creating the workbook** ger dig en Excel‑fil i minnet som du kan manipulera utan att öppna Excel.  
2. **Defining the range** (`I19:K20`) talar om för Aspose.Cells var regeln gäller, vilket håller logiken isolerad.  
3. **Adding a TIME_PERIOD condition** använder Aspose:s inbyggda uppräkning `TimePeriodType.YESTERDAY`. Detta undviker manuella datumberäkningar och uppdateras automatiskt när filen öppnas på en annan dag.  
4. **Setting the style** (`background_color` och `pattern`) bestämmer hur de markerade cellerna ser ut. Att använda `Color.pink` gör regeln lätt att upptäcka.  
5. **Writing sample dates** med talformat 30 säkerställer att Excel visar dem som korta datum istället för serienummer.  
6. **Auto‑fitting the column** förbättrar läsbarheten för den som öppnar filen senare.  
7. **Saving as XLSX** skapar en brett kompatibel fil som kan öppnas i Excel, Google Sheets eller något modernt kalkylprogram.

## Så skapar du Excel‑arbetsbok i Python‑stil med Aspose.Cells

Skriptet ovan demonstrerar redan de minimala stegen för **how to create excel workbook python**. I praktiken kan du vilja:

- Lägg till flera arbetsblad (`workbook.worksheets.add("Report")`).  
- Fyll stora datatabeller med loopar eller pandas DataFrames (`worksheet.cells.import_data_table`).  
- Applicera ytterligare formatering (typsnitt, kanter) med `cell.get_style()`.

Alla dessa åtgärder följer samma mönster: hämta objektet, modifiera dess egenskaper och anropa `set_style` eller `save`.

## Lägg till villkorsformatering i Python – andra användbara mönster

Utöver “Yesterday”-exemplet stödjer Aspose.Cells flera typer av villkorsformatering:

| FormatConditionType | Typiskt användningsområde |
|---------------------|---------------------------|
| `FORMAT_CONDITION_TYPE_EXPRESSION` | Anpassade formler (`=A1>100`) |
| `FORMAT_CONDITION_TYPE_CELL_VALUE` | Enkla jämförelser (`>`, `<`, `=`) |
| `FORMAT_CONDITION_TYPE_COLOR_SCALE` | Gradientfärgs skalor |
| `FORMAT_CONDITION_TYPE_DATA_BAR`   | Visualisering med staplar i cellen |

För att **add conditional formatting python** för ett numeriskt tröskelvärde, skulle du ersätta `FormatConditionType.TIME_PERIOD` med `FormatConditionType.CELL_VALUE` och sätta `condition.operator_type` och `condition.formula1`.

```python
# Example: highlight values greater than 500
idx = cond_format.add_condition(FormatConditionType.CELL_VALUE)
cond = cond_format[idx]
cond.operator_type = ConditionOperatorType.GREATER_THAN
cond.formula1 = "500"
cond.style.background_color = Color.light_green
```

## Spara arbetsbok som XLSX – bästa praxis

När du **save workbook as xlsx**, bör du tänka på:

- **Specifying the correct `SaveFormat`** (`SaveFormat.XLSX`) för att undvika äldre format.  
- **Using a deterministic file name** om skriptet körs i en loop (`f"report_{datetime.now():%Y%m%d}.xlsx"`).  
- **Closing resources** (`workbook.dispose()`) i långvariga tjänster för att frigöra inbyggt minne.  

Exemplet använder redan `SaveFormat.XLSX`, vilket skapar en modern, zip‑baserad arbetsbok som behåller alla villkorsformateringsregler.

## Markera gårdagen i Excel – verifieringssteg

Efter att ha kört skriptet, öppna `TimePeriodExample.xlsx`:

1. Cellerna `I19` och `K20` innehåller datumen `30‑07‑2008` och `03‑08‑2008`.  
2. Cellen `I20` visar texten “Yesterday”.  
3. Om du ändrar systemdatumet till **July 30 2008** och öppnar filen igen, fylls cellerna med matchande datum automatiskt med rosa.  
4. Att ändra systemdatumet till någon annan dag tar bort den rosa fyllningen, vilket bekräftar att regeln reagerar på **time period conditional formatting**‑logiken.

## Vanliga fallgropar och hur du undviker dem

- **Missing `aspose-pydrawing`** – `Color`‑klassen finns i detta paket; att glömma att installera det ger ett `ImportError`.  
- **Incorrect number format** – att använda standardformatet General visar serienummer (t.ex. 39822). Sätt alltid `style.number = 30` för korta datum.  
- **Range mismatch** – området för villkorsformatering måste inkludera de celler du vill markera; annars har regeln ingen effekt.

## Proffstips: återanvänd formateringsrutinen

Om du behöver samma “Yesterday”-regel i flera arbetsböcker, paketera logiken i en hjälpfunktion:

```python
def apply_yesterday_highlight(worksheet, address):
    cf = worksheet.conditional_formattings.add(address)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    cond = cf[idx]
    cond.style.background_color = Color.pink
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

Anropa `apply_yesterday_highlight(worksheet, "A1:A10")` där det behövs.

## Slutsats

Denna guide visade hur du implementerar **time period conditional formatting** i Excel med Python, hur du **save workbook as XLSX**, och hur du **highlight yesterday in Excel** med ett enda återanvändbart skript. Du har nu en solid grund för att **add conditional formatting python**‑kod i alla automationsprojekt, oavsett om du genererar dagliga rapporter, bygger instrumentpaneler eller förbereder dataexport.

**Nästa steg**

- Utforska andra `TimePeriodType`‑värden som `TODAY` eller `LAST_WEEK`.  
- Kombinera flera villkorsregler på samma område för rikare visuella ledtrådar.  
- Integrera arbetsboksgenereringen i en webbtjänst eller ett schemalagt jobb.

Lycka till med kodningen, och njut av den visuella tydlighet som villkorsformatering ger till din Excel‑automation!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Mästra villkorsformatering i Excel med Aspose.Cells .NET : En omfattande guide](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Mästra Aspose.Cells .NET : Applicera villkorsformatering på alternerande rader i Excel](/cells/english/net/formatting/aspose-cells-net-conditional-formatting-alternate-rows/)
- [Mästra villkorsformatering med anpassade typsnitt i Excel med Aspose.Cells för .NET och C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}