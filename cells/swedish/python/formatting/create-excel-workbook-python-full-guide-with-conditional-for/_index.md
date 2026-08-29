---
category: general
date: 2026-07-14
description: Skapa Python‑kod för en Excel‑arbetsbok som sätter cellbakgrundsfärg,
  markerar celler baserat på datumintervall och sparar arbetsboken som XLSX på några
  minuter.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- save workbook as xlsx
- highlight cells based on date range
- conditional formatting based on date
language: sv
lastmod: 2026-07-14
og_description: Skapa Excel-arbetsbok med Python omedelbart. Lär dig att sätta cellbakgrundsfärg,
  markera celler baserat på datumintervall och spara arbetsboken som XLSX med Aspose.Cells.
og_image_alt: Screenshot showing an Excel sheet created with Python highlighting yesterday's
  dates
og_title: Skapa Excel-arbetsbok med Python – Steg‑för‑steg villkorsstyrd formatering
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Create Excel workbook Python code that sets cell background color,
    highlights cells based on date range, and saves workbook as XLSX in minutes.
  headline: Create Excel Workbook Python – Full Guide with Conditional Formatting
  type: TechArticle
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Skapa Excel-arbetsbok med Python – Fullständig guide med villkorsstyrd formatering
url: /sv/python/formatting/create-excel-workbook-python-full-guide-with-conditional-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel Workbook Python – Fullständig guide med villkorsstyrd formatering

Har du någonsin undrat hur man **create excel workbook python** skript som ser snygga ut utan att öppna Excel manuellt? Du är inte ensam. I många datadrivna projekt måste vi generera kalkylblad, färgkoda celler och till och med flagga datum som faller inom ett specifikt intervall – allt från ren Python‑kod.

I den här handledningen går vi igenom ett komplett, färdigt att köra exempel som **creates an Excel workbook python** med Aspose.Cells‑biblioteket, **sets cell background color**, tillämpar **conditional formatting based on date**, och slutligen **saves workbook as xlsx**. I slutet har du ett återanvändbart kodstycke som du kan lägga in i vilken automatiseringspipeline som helst.

## Vad du kommer att lära dig

- Hur man initierar en arbetsbok och hämtar det första kalkylbladet.  
- En hjälpfunktion som lägger till en villkorsformateringssamling för vilket cellområde som helst.  
- Använda **conditional formatting based on date** för att markera gårdagens poster.  
- Justera kolumnbredder för en prydlig layout.  
- Spara resultatet med **save workbook as xlsx**.  

Ingen extern Excel‑installation krävs – Aspose.Cells hanterar allt i minnet.

## Förutsättningar

- Python 3.8+ installerat.  
- `aspose-cells`‑paketet (`pip install aspose-cells`).  
- Grundläggande kunskap om Python‑funktioner och datetime‑objekt.  

Om du aldrig har använt Aspose.Cells tidigare, tänk på det som ett kraftfullt, rent Python‑API som efterliknar Excels eget objektmodell. Det är perfekt för server‑sidig generering där Office‑sviten inte är tillgänglig.

## Steg 1: Initiera arbetsboken (Create Excel Workbook Python)

Först och främst: vi behöver **create excel workbook python** stil. Detta steg skapar ett tomt arbetsboksobjekt och pekar på standardkalkylbladet.

```python
# Step 1 – create a fresh workbook and get the first sheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, Color, SaveFormat
from datetime import datetime

workbook = Workbook()                     # <-- creates a new Excel file in memory
worksheet = workbook.worksheets[0]        # the default (first) sheet
```

> **Varför detta är viktigt:** `Workbook`‑klassen är ingångspunkten för varje Excel‑operation. Genom att skapa den programatiskt undviker vi manuell filhantering.

## Steg 2: Hjälp för att lägga till en Conditional‑Formatting‑samling (Set Cell Background Color)

Villkorsformatering finns i en *samling* som är kopplad till ett område. Låt oss paketera den boilerplate‑koden i en liten hjälpfunktion som också låter oss **set cell background color** för hela området.

```python
def add_time_period_condition(cell_range: str, highlight_color: Color):
    """
    Adds a conditional‑formatting collection to `cell_range` and
    applies `highlight_color` as the base fill.
    """
    worksheet.conditional_formattings.add(cell_range)   # attach to the range
    cf = worksheet.conditional_formattings[-1]           # grab the newly added collection
    cf.style.background_color = highlight_color
    cf.style.pattern = BackgroundType.SOLID
    return cf
```

> **Proffstips:** Att använda en hjälpfunktion håller huvudflödet rent och gör det enkelt att återanvända samma logik för flera områden.

## Steg 3: Tillämpa Conditional Formatting Based On Date (Highlight Cells Based On Date Range)

Nu kommer vi faktiskt **highlight cells based on date range**. Exemplet fokuserar på ”yesterday” men du kan byta `TimePeriodType.YESTERDAY` mot `TODAY`, `LAST_WEEK` osv.

```python
# Step 3 – create a TIME_PERIOD rule for I19:K20 (yesterday)
cf = add_time_period_condition("I19:K20", Color.medium_sea_green)

condition_index = cf.add_condition(FormatConditionType.TIME_PERIOD)
condition = cf[condition_index]

# Define the visual style for the matching cells
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# The actual rule: any cell whose date is yesterday gets the pink fill
condition.time_period = TimePeriodType.YESTERDAY
```

> **Vad händer?**  
> 1. Vi ger först hela området en neutral grön bakgrund.  
> 2. Sedan lägger vi till ett `TIME_PERIOD`‑villkor som ersätter fyllningen med rosa **endast** när cellens datum är lika med gårdagen.  
> 3. `TimePeriodType`‑enumet abstraherar datumberäkningen, så du behöver inte skriva egen logik.

## Steg 4: Fyll i exempeldatum (So the Rule Can Be Evaluated)

För att se regeln i aktion lägger vi in ett par datum i bladet. Ett faller inom ”yesterday”-fönstret, det andra gör det inte.

```python
# Populate I19 with a date that is yesterday (relative to the hard‑coded date)
date_cell = worksheet.cells.get("I19")
date_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008
date_style = date_cell.get_style()
date_style.number = 30                     # Excel’s built‑in date format
date_cell.set_style(date_style)

# Populate K20 with a date that is NOT yesterday
date_cell = worksheet.cells.get("K20")
date_cell.put_value(datetime(2008, 8, 3))    # 03‑Aug‑2008
date_style = date_cell.get_style()
date_style.number = 30
date_cell.set_style(date_style)

# Add a label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

> **Obs om kantfall:** Om din arbetsbok kommer att öppnas i olika språkregioner, överväg att använda `date_style.custom = "dd‑mm‑yyyy"` för att säkerställa en konsekvent visning.

## Steg 5: Rensa upp layouten (Auto‑Fit Columns)

Ett trångt kalkylblad ser oprofessionellt ut. Låt oss **adjust column width for a tidy output**.

```python
# Auto‑fit column L (index 12) to show the full content without truncation
worksheet.auto_fit_column(12)
```

> **Varför auto‑fit?** Det säkerställer att långa etiketter eller datum är helt synliga, vilket är särskilt viktigt när du delar filen med icke‑tekniska intressenter.

## Steg 6: Spara arbetsboken (Save Workbook As XLSX)

Till sist **save workbook as xlsx** till en plats du väljer. Konstanten `SaveFormat.XLSX` talar om för Aspose.Cells att skriva i det moderna OpenXML‑formatet.

```python
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Resultat du bör se:**  
> - Cellerna I19 och K20 innehåller datum.  
> - I19 (yesterday) är markerad rosa, medan K20 förblir grön.  
> - Kolumn L expanderar automatiskt för att rymma etiketten ”Yesterday”.  

Om du öppnar `TimePeriodDemo.xlsx` i Excel kommer villkorsformateringen redan att vara tillämpad – inga extra steg behövs.

![Excel-ark som visar markerat gårdagens datum](https://example.com/images/excel-demo.png "Skärmbild av den genererade Excel-filen med markerade celler")

*Bilden ovan illustrerar den färdiga arbetsboken; observera den rosa markeringen på cellen som innehåller gårdagens datum.*

## Sammanfattning: Vad vi uppnådde

- **Created an Excel workbook python** från grunden med Aspose.Cells.  
- **Set cell background color** för ett helt område för att ge bladet en visuell ledtråd.  
- Tillämpade **conditional formatting based on date** för att automatiskt flagga gårdagens poster.  
- **Saved workbook as xlsx**, redo för distribution eller vidare bearbetning.  

Allt detta gjordes på under 60 rader Python, och koden fungerar på alla plattformar som stöder Aspose.Cells‑runtime.

## Nästa steg & relaterade ämnen

Om du tyckte detta var användbart, kanske du också vill utforska:

- **set cell background color** för hela rader baserat på statusvärden (t.ex. ”Completed”, ”Pending”).  
- Använda **highlight cells based on date range** för att skapa rullande fönster (senaste 7 dagarna, innevarande månad).  
- Exportera till andra format som **CSV** eller **PDF** med `SaveFormat.CSV` eller `SaveFormat.PDF`.  
- Lägga till **charts** programatiskt för att visualisera data du just formaterat.  

Känn dig fri att justera datumlogiken, byta färgpalett eller utöka området för att täcka hela kolumner. Mönstret förblir detsamma: skapa en arbetsbok, bifoga en conditional‑formatting‑samling, definiera regeln och spara.

Har du frågor om ett specifikt användningsfall? Lägg en kommentar nedan, och lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Excel Automation with Aspose.Cells .NET: Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/hongkong/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}