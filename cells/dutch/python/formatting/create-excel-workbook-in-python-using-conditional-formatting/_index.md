---
category: general
date: 2026-09-21
description: Leer hoe je een Excel-werkmap maakt in Python, de achtergrondkleur van
  een cel instelt en datumgebaseerde voorwaardelijke opmaak toepast met Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- excel conditional formatting python
- date based conditional formatting
language: nl
lastmod: 2026-09-21
og_description: Maak een Excel-werkmap in Python, stel de achtergrondkleur van een
  cel in en pas datumgebaseerde voorwaardelijke opmaak toe met Aspose.Cells. Volg
  de stap‑voor‑stap‑gids.
og_image_alt: Screenshot of an Excel sheet showing a yellow‑green cell background
  for yesterday's dates
og_title: Maak Excel-werkmap in Python met voorwaardelijke opmaak
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
title: Maak een Excel-werkboek in Python met voorwaardelijke opmaak
url: /nl/python/formatting/create-excel-workbook-in-python-using-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak een Excel-werkmap in Python met voorwaardelijke opmaak

Als je **create Excel workbook python**‑scripts nodig hebt die datums automatisch markeren, laat deze gids je precies zien hoe. Je ziet hoe je **set cell background color** kunt instellen, een “Yesterday”-regel toevoegt en het bestand opslaat — allemaal met Aspose.Cells voor Python.

Werken met Excel-bestanden programmatisch betekent vaak dat je dezelfde opmaaklogica over veel bladen moet herhalen. Aan het einde van deze tutorial heb je een herbruikbaar patroon voor **excel conditional formatting python** dat je in elk project kunt gebruiken.

## Vereisten

- Python 3.8+ geïnstalleerd  
- `aspose-cells` pakket (`pip install aspose-cells`)  
- Basiskennis van Python-functies en de datetime‑module  

Er zijn geen extra bibliotheken nodig; Aspose.Cells verwerkt alle Excel‑bewerkingen.

## Stap 1: Maak de werkmap en krijg toegang tot het eerste werkblad

De eerste stap is om **create excel workbook python**‑objecten te maken en het standaardwerkblad te pakken. Dit geeft je een schoon canvas voor verdere opmaak.

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

*Waarom dit belangrijk is:* `Workbook()` maakt een Excel‑bestand in het geheugen. Toegang tot `worksheets[0]` voorkomt hard‑coderen van bladnamen en werkt zelfs als de standaardnaam verandert.

## Stap 2: Helper om een TIME_PERIOD voorwaardelijke opmaak toe te voegen

Om de code overzichtelijk te houden, wikkelen we de creatie van de voorwaardelijke opmaak in een helper. Deze ontvangt een celbereik, een achtergrondkleur en de gewenste tijdsperiode‑regel.

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

*Waarom dit belangrijk is:* De helper abstraheert de repetitieve stappen van het maken van een voorwaardelijke opmaak, waardoor het eenvoudig te hergebruiken is voor andere datum‑gebaseerde regels zoals “Today” of “Last Week”.

## Stap 3: Pas de “Yesterday”-regel toe op een bereik

Nu gebruiken we de helper om cellen te markeren die de datum van gisteren bevatten. Het bereik `I19:K20` wordt **medium sea green** wanneer aan de voorwaarde wordt voldaan.

```python
add_time_period(
    worksheet,
    "I19:K20",                # range to format
    Color.medium_sea_green,  # set cell background color
    TimePeriodType.YESTERDAY # date based conditional formatting
)
```

*Waarom dit belangrijk is:* `TimePeriodType.YESTERDAY` maakt deel uit van de ingebouwde enumeratie van Aspose.Cells, dus je hoeft datums niet handmatig te berekenen. De bibliotheek evalueert de regel elke keer dat de werkmap wordt geopend.

## Stap 4: Vul het bereik met voorbeelddatums

Om de regel in actie te zien, schrijven we twee datums — één die overeenkomt met “Yesterday” en één die dat niet doet. De `number`‑stijl `30` komt overeen met een ingebouwde datumopmaak.

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

*Waarom dit belangrijk is:* Door concrete datums in te voegen kun je verifiëren dat de voorwaardelijke opmaak werkt zonder het bestand op een specifieke dag te hoeven openen.

## Stap 5: Voeg een beschrijvend label toe en pas de kolombreedte automatisch aan

Een klein label verduidelijkt het doel van het opgemaakte bereik, en `auto_fit_column` maakt het blad leesbaar.

```python
# Add a label under the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Adjust column width for better visibility (column 12 = L)
worksheet.auto_fit_column(12)
```

## Stap 6: Sla de werkmap op

Tot slot schrijf je de werkmap naar schijf. De `os.makedirs`‑aanroep zorgt ervoor dat de doelmap bestaat.

```python
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)

# Save as XLSX – the most widely supported Excel format
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Wanneer je *TimePeriodDemo.xlsx* opent, zie je:

- Cel **I19** is gekleurd **medium sea green** omdat de waarde overeenkomt met de “Yesterday”-regel.  
- Cel **K20** behoudt de standaardachtergrond omdat de datum niet aan de voorwaarde voldoet.  

Dit demonstreert **format cells by date** met één regel Python‑code.

## Volledig, uitvoerbaar voorbeeld

Alle onderdelen samengevoegd, hier is het volledige script dat je kunt kopiëren‑plakken en uitvoeren:

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

Voer het script uit, open het resulterende bestand, en je ziet de voorwaardelijke opmaak in actie.

## Veelvoorkomende variaties en randgevallen

| Variatie | Hoe te implementeren | Wanneer te gebruiken |
|-----------|----------------------|----------------------|
| **Highlight “Today”** | Vervang `TimePeriodType.YESTERDAY` door `TimePeriodType.TODAY` | Real‑time dashboards |
| **Multiple ranges** | Roep `add_time_period` aan voor elk bereik, met verschillende kleuren | Complexe rapporten |
| **Dynamic date range** | Gebruik `TimePeriodType.LAST_7_DAYS` of `TimePeriodType.NEXT_MONTH` | Rullende rapporten |
| **Custom color** | Gebruik `Color.from_argb(255, r, g, b)` om elke tint te maken | Merkontvullende styling |

**Pro tip:** Stel altijd `condition.style.pattern = BackgroundType.SOLID` in wanneer je een effen vulling wilt; anders kan Excel een verloop weergeven dat er in verschillende versies inconsistent uitziet.

## Conclusie

Je weet nu hoe je **create Excel workbook python**‑scripts maakt die **set cell background color** instellen, **excel conditional formatting python** toepassen, en **format cells by date** gebruiken met Aspose.Cells. Het voorbeeld behandelt een **date based conditional formatting**‑scenario, maar hetzelfde patroon werkt voor elke tijdsperiode‑regel.

Volgende kun je verkennen:

- Het toevoegen van datastaven of pictogramsets (`FormatConditionType.DATA_BAR`)  
- Het combineren van meerdere voorwaardelijke regels op hetzelfde bereik  
- Het exporteren van de werkmap naar PDF (`SaveFormat.PDF`) voor rapportage  

Voel je vrij om te experimenteren met verschillende kleuren, bereiken en tijdsperiode‑typen om aan je specifieke rapportagebehoeften te voldoen. Veel plezier met coderen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Beheers Excel-celopmaak en werkmapbeheer met Aspose.Cells voor .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Excel-automatisering met Aspose.Cells .NET: Werkmap maken & externe koppelingen instellen](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Hoe maak je werkmap‑specifieke benoemde bereiken in Excel met Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}