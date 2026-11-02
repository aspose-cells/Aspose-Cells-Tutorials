---
category: general
date: 2026-10-04
description: Skapa Excel-arbetsbok i Python med Aspose.Cells. Lär dig Excel villkorsstyrd
  formatering i Python, cellbakgrundsfärg i Python och formatering av datum i celler
  i Python i ett komplett exempel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create Excel workbook python
- excel conditional formatting python
- cell background color python
- format cells date python
language: sv
lastmod: 2026-10-04
og_description: Skapa Excel-arbetsbok med Python och Aspose.Cells. Den här handledningen
  visar Excel villkorsstyrd formatering med Python, cellbakgrundsfärg med Python och
  formatering av datumceller med Python steg för steg.
og_image_alt: Screenshot of an Excel workbook created with Python showing highlighted
  yesterday dates
og_title: Skapa Excel-arbetsbok med Python – komplett guide med villkorsstyrd formatering
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  headline: Create Excel workbook python with conditional formatting and cell background
    color
  type: TechArticle
- description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  name: Create Excel workbook python with conditional formatting and cell background
    color
  steps:
  - name: '**create Excel workbook python** using the Aspose.Cells library.'
    text: '**create Excel workbook python** using the Aspose.Cells library.'
  - name: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
    text: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
  - name: Set the **cell background color python** to pink (or any color you prefer).
    text: Set the **cell background color python** to pink (or any color you prefer).
  - name: '**format cells date python** so the dates appear in the standard Excel
      date style.'
    text: '**format cells date python** so the dates appear in the standard Excel
      date style.'
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Skapa Excel-arbetsbok i Python med villkorsstyrd formatering och cellbakgrundsfärg
url: /sv/python/formulas-and-functions/create-excel-workbook-python-with-conditional-formatting-and/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel-arbetsbok python med villkorsstyrd formatering och cellbakgrundsfärg

Om du snabbt behöver **create Excel workbook python**, visar den här guiden exakt hur. Du får se ett komplett, körbart exempel som lägger till **excel conditional formatting python**, ändrar **cell background color python**, och **format cells date python** för en “Yesterday”-markering.  

I många rapporteringsscenarier gör den visuella ledtråden av en färgad cell data omedelbart begripliga. Den här handledningen går igenom varje kodrad, förklarar varför varje steg är viktigt, och ger dig ett färdigt skript som du kan anpassa till dina egna projekt.

## Vad du kommer att uppnå

1. **create Excel workbook python** med Aspose.Cells-biblioteket.  
2. Tillämpa **excel conditional formatting python** som automatiskt markerar datum som faller på “Yesterday”.  
3. Sätt **cell background color python** till rosa (eller någon annan färg du föredrar).  
4. **format cells date python** så att datumen visas i standard Excel-datumformat.  

Ingen tidigare erfarenhet av Aspose.Cells krävs – bara en fungerande Python 3‑miljö och pip‑åtkomst.

## Förutsättningar

- Python 3.8 eller nyare installerat.  
- `aspose-cells` och `aspose-pydrawing` paket installerade via `pip install aspose-cells aspose-pydrawing`.  
- Grundläggande kunskap om Python‑syntax och Excel‑koncept (arbetsböcker, kalkylblad, celler).  

> **Pro tip:** Om du kör skriptet i en virtuell miljö undviker du versionskonflikter med andra projekt.

## Steg 1: Ställ in projektet och importera nödvändiga klasser

Det första steget när du **create Excel workbook python** är att importera de Aspose.Cells‑klasser du behöver. Dessa klasser ger dig direkt åtkomst till skapande av arbetsböcker, villkorsstyrd formatering och styling.

```python
# Import Aspose.Cells core classes
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)

# Import Aspose.PyDrawing for color handling
from aspose.pydrawing import Color

# Standard library for date values
from datetime import datetime
```

*Varför detta är viktigt:* Att bara importera de symboler som behövs håller namnrymden ren och gör skriptet lättare att läsa. `Workbook` är ingångspunkten för **create Excel workbook python**, medan `FormatConditionType` och `TimePeriodType` är väsentliga för **excel conditional formatting python**.

## Steg 2: Skapa en ny arbetsbok och hämta det första kalkylbladet

Nu **create Excel workbook python** på riktigt. Konstruktorn `Workbook()` ger dig en tom Excel‑fil med ett standardkalkylblad.

```python
# Step 2: Initialize a new workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Förklaring:* Varje Excel‑fil börjar med minst ett kalkylblad. Som standard heter det “Sheet1”. Du kan lägga till fler blad senare, men för den här demonstrationen håller ett enda blad exemplet fokuserat.

## Steg 3: Definiera målområdet för villkorsstyrd formatering

Villkorsstyrd formatering fungerar på ett rektangulärt område. Här väljer vi området `I19:K20`, vilket ger oss tre kolumner och två rader att arbeta med.

```python
# Define the range that will receive conditional formatting
target_range = "I19:K20"

# Retrieve (or create) the ConditionalFormatting collection for that range
conditional_formatting = worksheet.conditional_formattings.get(target_range)
```

*Varför vi gör detta:* Metoden `get` returnerar ett `ConditionalFormatting`‑objekt knutet till det angivna området. Om området ännu inte har någon formatering skapar Aspose.Cells automatiskt en ny samling.

## Steg 4: Lägg till ett TIME_PERIOD‑villkor och sätt bakgrundsfärgen

Detta är kärnan i **excel conditional formatting python**. Vi lägger till ett `TIME_PERIOD`‑regel som markerar celler som innehåller datum som faller på “Yesterday”.

```python
# Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Access the newly created condition
condition = conditional_formatting[condition_index]

# Configure the condition to target “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Set the cell background color – this is the cell background color python part
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
```

*Djupdykning:*  
- `FormatConditionType.TIME_PERIOD` talar om för Excel att utvärdera datum relativt till det aktuella datumet.  
- `TimePeriodType.YESTERDAY` är en inbyggd enum som automatiskt uppdateras varje dag, så arbetsboken alltid markerar den senaste “Yesterday”.  
- Genom att sätta `background_color` till `Color.pink` och mönstret till `SOLID` uppnår vi **cell background color python**‑effekten utan extra VBA‑kod.

## Steg 5: Fyll i området med exempeldatum och tillämpa datumformat

För att se den villkorsstyrda formateringen i aktion behöver vi riktiga datumvärden. Vi måste också **format cells date python** så att Excel behandlar dem som datum snarare än rena siffror.

```python
# Helper function to set a cell's date style and value
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    # Excel’s built‑in date format code 30 = "m/d/yy"
    style.number = 30
    cell.set_style(style)
    cell.put_value(date_value)

# Populate I19 with a date that is “yesterday” relative to the sample data
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”

# Populate K20 with another arbitrary date
set_date("K20", datetime(2008, 8, 3))    # Not “yesterday”
```

*Förklaring:*  
- Raden `style.number = 30` är steget **format cells date python**. Formatkod 30 motsvarar kort datumformat (`m/d/yy`).  
- Att använda en hjälpfunktion håller koden DRY (Don’t Repeat Yourself) och gör det enkelt att lägga till fler datum senare.

## Steg 6: Lägg till en beskrivande etikett

En liten etikett hjälper alla som öppnar arbetsboken att förstå varför cellerna är färgade.

```python
# Place a label next to the formatted range
worksheet.cells.get("I20").put_value("Yesterday")
```

## Steg 7: Spara arbetsboken till disk

Slutligen **create Excel workbook python** på disk genom att anropa `save`. Konstanten `SaveFormat.XLSX` säkerställer att filen är i det moderna Office Open XML‑formatet.

```python
# Define the output path – replace YOUR_DIRECTORY with a real folder
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"

# Save the workbook
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

När du öppnar `TimePeriodDemo.xlsx` i Excel kommer du att se:

- Cellerna `I19` och `K20` innehåller datum.  
- Cellen som matchar “Yesterday” (i detta statiska exempel, `I19`) är markerad rosa.  
- Etiketten “Yesterday” visas i `I20`.  

> **Tip:** Om du kör skriptet på en annan dag markerar den villkorsstyrda formateringen fortfarande cellen vars datum är exakt en dag före det aktuella systemdatumet – inga kodändringar behövs.

## Fullt skript – redo att kopiera och köra

Nedan är det kompletta, självständiga programmet som innehåller alla stegen ovan. Kopiera det till en fil med namnet `conditional_format_demo.py`, justera `YOUR_DIRECTORY`, och kör med `python conditional_format_demo.py`.

```python
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the cell range that will receive the conditional format
target_range = "I19:K20"
conditional_formatting = worksheet.conditional_formattings.get(target_range)

# Step 3: Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Step 4: Configure the condition to highlight “Yesterday” dates
condition = conditional_formatting[condition_index]
condition.time_period = TimePeriodType.YESTERDAY
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Helper to set date value and style
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    style.number = 30          # Excel date format code 30 = short date
    cell.set_style(style)
    cell.put_value(date_value)

# Step 5: Populate the range with sample dates (excel conditional formatting python)
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”
set_date("K20", datetime(2008, 8, 3))    # Another sample date

# Step 6: Add a label describing the condition
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### Förväntat resultat

Att köra skriptet skriver ut en bekräftelsesats:

```
Workbook saved to YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Att öppna den genererade filen visar den rosa bakgrunden på den cell som matchar “Yesterday”-regeln, vilket bekräftar att **excel conditional formatting python** och **cell background color python** fungerar tillsammans.

## Vanliga variationer och kantfall

| Situation | Hur du anpassar koden |
|-----------|-----------------------|
| **Olika markeringsfärg** | Ändra `Color.pink` till någon annan `Color`‑konstant, t.ex. `Color.light_green`. |
| **Markera “Today” istället för “Yesterday”** | Sätt `condition.time_period = TimePeriodType.TODAY`. |
| **Tillämpa formatering på en hel kolumn** | Använd ett område som `"A:A"` och justera variabeln `target_range` därefter. |
| **Använd ett eget datumformat** | Ersätt `style.number = 30` med `style.custom = "dd-mmm-yyyy"` för ett mer läsbart format. |
| **Flera villkor på samma område** |  |

## Vad bör du lära dig härnäst?

De följande handledningarna täcker närliggande ämnen som bygger vidare på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Skapa Excel Workbook Python – Komplett guide med Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)
- [Skapa och spara Excel-arbetsbok som PDF i ASP.NET med Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Hur man skapar och sparar en Excel-arbetsbok som ODS med Aspose.Cells för .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}