---
category: general
date: 2026-09-15
description: Leer hoe je tijdsperiode-voorwaardelijke opmaak toepast en een werkmap
  opslaat als XLSX met Aspose.Cells in Python. Inclusief stap‑voor‑stap code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- time period conditional formatting
- save workbook as xlsx
- how to create excel workbook python
- how to highlight yesterday in excel
- add conditional formatting python
language: nl
lastmod: 2026-09-15
og_description: Pas voorwaardelijke opmaak voor tijdsperioden toe in Excel met Python
  en sla het werkboek op als XLSX. Volg deze volledige gids voor Aspose.Cells.
og_image_alt: Screenshot of an Excel sheet where the cells for yesterday are highlighted
  in pink
og_title: Voorwaardelijke opmaak voor tijdsperioden toepassen in Excel met Python
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
title: Hoe voorwaardelijke opmaak voor tijdsperioden toe te passen in Excel met Python
url: /nl/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe tijdsperiode voorwaardelijke opmaak toe te passen in Excel met Python

Als je **time period conditional formatting** in een Excel‑bestand nodig hebt, laat deze tutorial je precies zien hoe je dit doet met Python. Je ziet een compleet, uitvoerbaar voorbeeld dat een werkmap maakt, de datums van gisteren markeert, en **save workbook as XLSX** in slechts een paar regels code.

Voorwaardelijke opmaak is een krachtige manier om aandacht te vestigen op gegevens die aan een specifieke regel voldoen. In deze gids richten we ons op de “Yesterday” tijdsperiode, maar hetzelfde patroon werkt voor andere ingebouwde periodes zoals Today, LastWeek en NextMonth. Aan het einde van de tutorial kun je **how to create excel workbook python**‑style scripts maken die klaar zijn voor productie.

## Prerequisites

- Python 3.8+ geïnstalleerd  
- `aspose-cells` en `aspose-pydrawing` pakketten (`pip install aspose-cells aspose-pydrawing`)  
- Basiskennis van Python‑syntaxis  

Er is geen extra Office‑installatie vereist omdat Aspose.Cells de bestandsgeneratie intern afhandelt.

## Time period conditional formatting with Aspose.Cells in Python

Deze sectie loopt stap voor stap door elke regel code die nodig is voor de primaire taak. Het code‑blok hieronder is het volledige script; commentaren leggen het doel van elke stap uit.

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

### Why each step matters

1. **Creating the workbook** geeft je een Excel‑bestand in het geheugen dat je kunt manipuleren zonder Excel te openen.  
2. **Defining the range** (`I19:K20`) vertelt Aspose.Cells waar de regel van toepassing is, waardoor de logica geïsoleerd blijft.  
3. **Adding a TIME_PERIOD condition** gebruikt Aspose’s ingebouwde enumeratie `TimePeriodType.YESTERDAY`. Dit voorkomt handmatige datumcalculaties en werkt automatisch bij wanneer het bestand op een andere dag wordt geopend.  
4. **Setting the style** (`background_color` en `pattern`) bepaalt hoe de gemarkeerde cellen eruitzien. Het gebruik van `Color.pink` maakt de regel gemakkelijk te herkennen.  
5. **Writing sample dates** met getalformaat 30 zorgt ervoor dat Excel ze weergeeft als korte datums in plaats van serienummers.  
6. **Auto‑fitting the column** verbetert de leesbaarheid voor iedereen die het bestand later opent.  
7. **Saving as XLSX** produceert een breed compatibel bestand dat geopend kan worden in Excel, Google Sheets of elk modern spreadsheet‑programma.

## How to create Excel workbook Python‑style with Aspose.Cells

Het script hierboven demonstreert al de minimale stappen om **how to create excel workbook python**. In de praktijk wil je misschien:

- Voeg meerdere werkbladen toe (`workbook.worksheets.add("Report")`).  
- Vul grote datatabellen met lussen of pandas DataFrames (`worksheet.cells.import_data_table`).  
- Pas extra opmaak toe (lettertypen, randen) met `cell.get_style()`.

Al deze handelingen volgen hetzelfde patroon: verkrijg het object, wijzig de eigenschappen, en roep `set_style` of `save` aan.

## Add conditional formatting Python – other useful patterns

Naast het “Yesterday” voorbeeld ondersteunt Aspose.Cells verschillende soorten voorwaardelijke opmaak:

| FormatConditionType | Typical use case |
|---------------------|------------------|
| `FORMAT_CONDITION_TYPE_EXPRESSION` | Aangepaste formules (`=A1>100`) |
| `FORMAT_CONDITION_TYPE_CELL_VALUE` | Eenvoudige vergelijkingen (`>`, `<`, `=`) |
| `FORMAT_CONDITION_TYPE_COLOR_SCALE` | Gradient kleurenschalen |
| `FORMAT_CONDITION_TYPE_DATA_BAR`   | In‑cell balkvisualisatie |

Om **add conditional formatting python** voor een numerieke drempel te gebruiken, vervang je `FormatConditionType.TIME_PERIOD` door `FormatConditionType.CELL_VALUE` en stel je `condition.operator_type` en `condition.formula1` in.

```python
# Example: highlight values greater than 500
idx = cond_format.add_condition(FormatConditionType.CELL_VALUE)
cond = cond_format[idx]
cond.operator_type = ConditionOperatorType.GREATER_THAN
cond.formula1 = "500"
cond.style.background_color = Color.light_green
```

## Save workbook as XLSX – best practices

Wanneer je **save workbook as xlsx**, overweeg dan:

- **Specifying the correct `SaveFormat`** (`SaveFormat.XLSX`) om verouderde formaten te vermijden.  
- **Using a deterministic file name** als het script in een lus draait (`f"report_{datetime.now():%Y%m%d}.xlsx"`).  
- **Closing resources** (`workbook.dispose()`) in langdurige services om native geheugen vrij te maken.

Het voorbeeld gebruikt al `SaveFormat.XLSX`, wat een modern, zip‑gebaseerd werkboek oplevert dat alle voorwaardelijke‑opmaakregels behoudt.

## Highlight yesterday in Excel – verification steps

Na het uitvoeren van het script, open `TimePeriodExample.xlsx`:

1. Cellen `I19` en `K20` bevatten de datums `30‑07‑2008` en `03‑08‑2008`.  
2. De cel `I20` toont de tekst “Yesterday”.  
3. Als je de systeemtijd wijzigt naar **30 juli 2008** en het bestand opnieuw opent, worden de cellen met overeenkomende datums automatisch roze ingevuld.  
4. Het wijzigen van de systeemtijd naar een andere dag verwijdert de roze vulling, wat bevestigt dat de regel reageert op de **time period conditional formatting**‑logica.

## Common pitfalls and how to avoid them

- **Missing `aspose-pydrawing`** – de `Color`‑klasse zit in dit pakket; vergeten om het te installeren veroorzaakt een `ImportError`.  
- **Incorrect number format** – het gebruik van het standaard General‑formaat toont serienummers (bijv. 39822). Stel altijd `style.number = 30` in voor korte datums.  
- **Range mismatch** – het bereik voor voorwaardelijke opmaak moet de cellen bevatten die je wilt markeren; anders heeft de regel geen effect.

## Pro tip: reuse the formatting routine

Als je dezelfde “Yesterday” regel in meerdere werkboeken nodig hebt, wikkel je de logica in een hulpfunctie:

```python
def apply_yesterday_highlight(worksheet, address):
    cf = worksheet.conditional_formattings.add(address)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    cond = cf[idx]
    cond.style.background_color = Color.pink
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

Roep `apply_yesterday_highlight(worksheet, "A1:A10")` aan waar nodig.

## Conclusion

Deze gids heeft je laten zien hoe je **time period conditional formatting** in Excel implementeert met Python, hoe je **save workbook as XLSX** uitvoert, en hoe je **highlight yesterday in Excel** doet met één herbruikbaar script. Je hebt nu een solide basis om **add conditional formatting python** code toe te voegen aan elk automatiseringsproject, of je nu dagelijkse rapporten genereert, dashboards bouwt, of data‑exports voorbereidt.

**Next steps**

- Verken andere `TimePeriodType`‑waarden zoals `TODAY` of `LAST_WEEK`.  
- Combineer meerdere voorwaardelijke regels op hetzelfde bereik voor rijkere visuele aanwijzingen.  
- Integreer de werkmapgeneratie in een webservice of geplande taak.

Happy coding, and enjoy the visual clarity that conditional formatting brings to your Excel automation!

## What Should You Learn Next?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Master Conditional Formatting in Excel Using Aspose.Cells .NET : A Comprehensive Guide](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Master Aspose.Cells .NET : Apply Conditional Formatting to Alternate Rows in Excel](/cells/english/net/formatting/aspose-cells-net-conditional-formatting-alternate-rows/)
- [Master Conditional Formatting with Custom Fonts in Excel using Aspose.Cells for .NET and C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}