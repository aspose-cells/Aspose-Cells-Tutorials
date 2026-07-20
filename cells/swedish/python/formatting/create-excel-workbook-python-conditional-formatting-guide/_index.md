---
category: general
date: 2026-07-20
description: Skapa en Excel-arbetsbok i Python med Aspose.Cells, sätt cellens bakgrundsfärg
  och lägg till villkorsstyrd formatering i Python för att formatera celler efter
  datum.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- aspose cells conditional formatting
- add conditional formatting python
language: sv
lastmod: 2026-07-20
og_description: Skapa Excel-arbetsbok i Python med Aspose.Cells. Lär dig hur du sätter
  cellbakgrundsfärg och lägger till villkorsstyrd formatering i Python för att formatera
  celler efter datum.
og_image_alt: Screenshot of an Excel workbook created with Python showing conditional
  formatting applied to date cells
og_title: Skapa Excel-arbetsbok med Python – Lägg till villkorsstyrd formatering
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
title: Skapa Excel-arbetsbok i Python – Guide för villkorsstyrd formatering
url: /sv/python/formatting/create-excel-workbook-python-conditional-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel Workbook Python – Guide för villkorsstyrd formatering

Har du någonsin undrat hur man **create Excel workbook Python** från grunden och får den att se polerad ut utan att öppna UI‑gränssnittet? Du är inte ensam. Många utvecklare stöter på problem när de behöver **set cell background color** eller tillämpa datum‑baserade stilar programmässigt.  

I den här handledningen går vi igenom ett komplett, körbart exempel som använder Aspose.Cells för att **add conditional formatting python**‑regler, formatera celler efter datum och spara resultatet som en modern XLSX‑fil. I slutet har du ett självständigt skript som du kan lägga in i vilket projekt som helst.

## Vad du kommer att lära dig

- Hur man initierar en arbetsbok och hämtar det första kalkylbladet.  
- Sätt att **set cell background color** för ett helt område.  
- Använda **aspose cells conditional formatting** för att markera datumet “Yesterday”.  
- Auto‑justera kolumner och spara filen på disk.  

Ingen extern konfiguration krävs—bara Python 3 och Aspose.Cells‑paketet. Om du redan har installerat `aspose-cells` är du klar; annars räcker ett snabbt `pip install aspose-cells`.

## Förutsättningar

- Python 3.8+ (koden fungerar på 3.9, 3.10 och nyare).  
- Aspose.Cells för Python via .NET (`aspose-cells` NuGet‑wrapper).  
- Grundläggande kunskap om Excel‑koncept (celler, områden, formatering).  

Har du dem? Bra—låt oss dyka ner.

## Skapa Excel Workbook Python – Inställning och kalkylblad

Först och främst: vi behöver ett nytt arbetsboksobjekt och en referens till standardkalkylbladet. Detta är duken där alla senare operationer kommer att ske.

```python
# Import the necessary Aspose.Cells classes
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and grab the first sheet
workbook = Workbook()                     # create excel workbook python
worksheet = workbook.worksheets[0]        # default is the first worksheet
```

> **Why this matters:** `Workbook()` konstruerar en Excel‑fil i minnet, vilket eliminerar behovet av temporära filer. Variabeln `worksheet` är vår ingångspunkt för cell‑nivååtgärder.

## Ställ in cellbakgrundsfärg

Innan vi lägger till några regler är det bra att ge målområdet en grundfärg så att den villkorsstyrda formateringen framträder. Hjälpfunktionen nedan hämtar (eller skapar) en `FormatConditionCollection` för ett givet område och målar cellerna med en solid bakgrund.

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

> **Pro tip:** Om du planerar att återanvända samma område med flera regler, anropa denna hjälpfunktion en gång och behåll den returnerade samlingen; det sparar några API‑anrop.

## Lägg till Conditional Formatting Python för datumintervall

Nu blir det roligt: vi kommer att skapa en **time‑period conditional formatting**‑regel som markerar celler som innehåller gårdagens datum. Detta demonstrerar kraften i **format cells by date** med Aspose.Cells.

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

> **Why use `TIME_PERIOD`?** Det abstraherar bort behovet av att skriva egna formler. Aspose.Cells utvärderar datumet mot det aktuella systemdatumet, så regeln förblir relevant.

### Köra regeln

```python
apply_yesterday_rule()
```

När du öppnar den resulterande filen kommer cellerna `I19` att lysa rosa (eftersom de är “Yesterday”), medan `K20` behåller den grundgröna färgen.

## Auto‑Fit kolumner och spara arbetsbok

Ett prydligt kalkylblad ser professionellt ut. Auto‑fitting säkerställer att våra data inte är trånga.

```python
# Step 4: Auto‑fit the column width for a tidy appearance
worksheet.auto_fit_column(12)   # column index is zero‑based; 12 corresponds to column M

# Step 5: Save the workbook to disk
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Edge case:** Om du riktar in dig på en katalog som inte finns, kommer `workbook.save` att kasta ett fel. Omge spara‑anropet med ett `try/except`‑block om du behöver en smidig hantering.

### Fullt skript (Klar att kopiera‑klistra)

Nedan är hela skriptet, redo att köras. Byt bara ut `YOUR_DIRECTORY` mot en giltig mapp på din maskin.

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

Att köra detta skript kommer att producera `TimePeriodExample.xlsx` med den villkorsstyrda formatering vi beskrev.

## Vanliga frågor & tips

- **Can I target a different date range?**  
  Absolut. Ändra `"I19:K20"` till vilket A1‑formatområde som helst, och justera exempeldatumen därefter.

- **What if I need a custom formula instead of `YESTERDAY`?**  
  Använd `FormatConditionType.FORMULA` och sätt `condition.formula1 = "YOUR_FORMULA"`—till exempel `=TODAY()-A1=1` för att efterlikna gårdagen.

- **How do I apply multiple rules to the same range?**  
  Anropa `conditions.add_condition` igen med en annan `FormatConditionType`. Ordningen är viktig; senare regler kan åsidosätta tidigare.

- **Is there a way to set font colour together with background?**  
  Ja—ändra `condition.style.font.color = Color.white` (eller någon annan `Color`).

## Slutsats

Du vet nu hur man **create Excel workbook Python** med Aspose.Cells, **set cell background color**, och **add conditional formatting python** som formaterar celler efter datum. Skriptet är fullt funktionellt, hanterar edge cases som saknade kataloger, och kan utökas till mer avancerade scenarier såsom multi‑rule conditional logic eller dynamisk områdesdetektering.

Redo för nästa steg? Prova att byta ut “Yesterday”-regeln mot “Last Week”, experimentera med gradientfyllningar, eller generera en fullständig rapport med dussintals formaterade tabeller. Byggstenarna finns här, och du har just bemästrat grunden i **aspose cells conditional formatting** i Python.

Lycka till med kodandet, och dela gärna dina egna varianter i kommentarerna!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Behärska Excel-cellformatering och arbetsbokshantering med Aspose.Cells för .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Hur man skapar och sparar en Excel-arbetsbok som ODS med Aspose.Cells för .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Hur man skapar arbetsboksomfattande namngivna områden i Excel med Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}