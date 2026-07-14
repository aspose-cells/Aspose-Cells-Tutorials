---
category: general
date: 2026-07-14
description: Maak Python-code voor een Excel-werkboek die de celachtergrondkleur instelt,
  cellen markeert op basis van een datumbereik en het werkboek binnen enkele minuten
  opslaat als XLSX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- save workbook as xlsx
- highlight cells based on date range
- conditional formatting based on date
language: nl
lastmod: 2026-07-14
og_description: Maak direct een Excel-werkmap in Python. Leer hoe je de achtergrondkleur
  van cellen instelt, cellen markeert op basis van een datumbereik, en de werkmap
  opslaat als XLSX met Aspose.Cells.
og_image_alt: Screenshot showing an Excel sheet created with Python highlighting yesterday's
  dates
og_title: Excel‑werkboek maken met Python – Stapsgewijze voorwaardelijke opmaak
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
title: Excel-werkmap maken met Python – Volledige gids met voorwaardelijke opmaak
url: /nl/python/formatting/create-excel-workbook-python-full-guide-with-conditional-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-werkboek maken met Python – Volledige gids met voorwaardelijke opmaak

Heb je je ooit afgevraagd hoe je **create excel workbook python**‑scripts kunt maken die er gepolijst uitzien zonder Excel handmatig te openen? Je bent niet de enige. In veel data‑gedreven projecten moeten we spreadsheets genereren, cellen kleuren en zelfs datums markeren die binnen een specifiek bereik vallen — allemaal vanuit pure Python‑code.

In deze tutorial lopen we een compleet, kant‑klaar voorbeeld door dat **creates an Excel workbook python** gebruikt met de Aspose.Cells‑bibliotheek, **sets cell background color**, **conditional formatting based on date** toepast, en uiteindelijk **saves workbook as xlsx**. Aan het einde heb je een herbruikbare code‑fragment die je in elke automatiserings‑pipeline kunt plaatsen.

## Wat je zult leren

- Hoe je een werkboek initialiseert en het eerste werkblad oppakt.  
- Een hulpfunctie die een voorwaardelijke‑opmaakcollectie toevoegt voor elk celbereik.  
- Gebruik van **conditional formatting based on date** om de invoer van gisteren te markeren.  
- Kolombreedtes aanpassen voor een nette lay‑out.  
- Het resultaat behouden met **save workbook as xlsx**.  

Er is geen externe Excel‑installatie vereist — Aspose.Cells verwerkt alles in het geheugen.

## Vereisten

- Python 3.8+ geïnstalleerd.  
- `aspose-cells`‑pakket (`pip install aspose-cells`).  
- Basiskennis van Python‑functies en datetime‑objecten.  

Als je Aspose.Cells nog nooit hebt gebruikt, beschouw het dan als een krachtige, pure‑Python API die het objectmodel van Excel nabootst. Het is perfect voor server‑side generatie waar de Office‑suite niet beschikbaar is.

## Stap 1: Initialise the Workbook (Create Excel Workbook Python)

Allereerst: we moeten **create excel workbook python**‑stijl een leeg werkboekobject maken en ons richten op het standaard werkblad.

```python
# Step 1 – create a fresh workbook and get the first sheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, Color, SaveFormat
from datetime import datetime

workbook = Workbook()                     # <-- creates a new Excel file in memory
worksheet = workbook.worksheets[0]        # the default (first) sheet
```

> **Why this matters:** De `Workbook`‑klasse is het toegangspunt voor elke Excel‑bewerking. Door deze programmatisch te maken vermijden we handmatige bestandsafhandeling.

## Stap 2: Helper om een Conditional‑Formatting‑collectie toe te voegen (Set Cell Background Color)

Voorwaardelijke opmaak bevindt zich in een *collectie* die aan een bereik is gekoppeld. Laten we die boilerplate in een kleine helper wikkelen die ons ook **set cell background color** voor het hele bereik laat toepassen.

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

> **Pro tip:** Het gebruik van een helper houdt je hoofdflow schoon en maakt het gemakkelijk om dezelfde logica voor meerdere bereiken te hergebruiken.

## Stap 3: Conditional Formatting toepassen op basis van datum (Highlight Cells Based on Date Range)

Nu gaan we daadwerkelijk **highlight cells based on date range**. Het voorbeeld richt zich op “yesterday”, maar je kunt `TimePeriodType.YESTERDAY` vervangen door `TODAY`, `LAST_WEEK`, enz.

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

> **What’s happening?**  
> 1. We geven eerst het hele bereik een neutrale groene achtergrond.  
> 2. Vervolgens voegen we een `TIME_PERIOD`‑conditie toe die de vulling overschrijft met roze **alleen** wanneer de datum van de cel gelijk is aan gisteren.  
> 3. De `TimePeriodType`‑enum abstraheert de datumcalculatie, zodat je geen aangepaste logica hoeft te schrijven.

## Stap 4: Voorbeelddata invullen (So the Rule Can Be Evaluated)

Om de regel in actie te zien, voegen we een paar datums toe aan het blad. Eén valt binnen het “yesterday”‑venster, de andere niet.

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

> **Edge case note:** Als je werkboek in verschillende locales wordt geopend, overweeg dan `date_style.custom = "dd‑mm‑yyyy"` te gebruiken om een consistente weergave af te dwingen.

## Stap 5: Layout opruimen (Auto‑Fit Columns)

Een krappe spreadsheet ziet er onprofessioneel uit. Laten we **adjust column width for a tidy output**.

```python
# Auto‑fit column L (index 12) to show the full content without truncation
worksheet.auto_fit_column(12)
```

> **Why auto‑fit?** Het zorgt ervoor dat lange labels of datums volledig zichtbaar zijn, wat vooral belangrijk is wanneer je het bestand deelt met niet‑technische belanghebbenden.

## Stap 6: Werkboek opslaan (Save Workbook As XLSX)

Tot slot **save workbook as xlsx** we naar een locatie naar keuze. De constante `SaveFormat.XLSX` vertelt Aspose.Cells om het moderne OpenXML‑formaat te schrijven.

```python
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Result you should see:**  
> - Cellen I19 en K20 bevatten datums.  
> - I19 (gisteren) is gemarkeerd in roze, terwijl K20 groen blijft.  
> - Kolom L wordt automatisch vergroot om het label “Yesterday” te passen.  

Als je `TimePeriodDemo.xlsx` in Excel opent, is de voorwaardelijke opmaak al toegepast — er zijn geen extra stappen nodig.

---

![Excel sheet showing highlighted yesterday date](https://example.com/images/excel-demo.png "Screenshot of the generated Excel file with highlighted cells")

*De bovenstaande afbeelding illustreert het uiteindelijke werkboek; let op de roze markering op de cel met de datum van gisteren.*

## Samenvatting: Wat we hebben bereikt

- **Created an Excel workbook python** vanaf nul met Aspose.Cells.  
- **Set cell background color** voor een heel bereik om het blad een visuele aanwijzing te geven.  
- Voorwaardelijke opmaak toegepast **conditional formatting based on date** om automatisch de invoer van gisteren te markeren.  
- **Saved workbook as xlsx**, klaar voor distributie of verdere verwerking.  

Dit alles werd gedaan in minder dan 60 regels Python, en de code werkt op elk platform dat de Aspose.Cells‑runtime ondersteunt.

## Volgende stappen & gerelateerde onderwerpen

Als je dit nuttig vond, wil je misschien ook verkennen:

- **set cell background color** voor volledige rijen op basis van statuswaarden (bijv. “Completed”, “Pending”).  
- Gebruik van **highlight cells based on date range** om rollende vensters te maken (laatste 7 dagen, huidige maand).  
- Exporteren naar andere formaten zoals **CSV** of **PDF** met `SaveFormat.CSV` of `SaveFormat.PDF`.  
- **charts** programmatisch toevoegen om de gegevens die je zojuist hebt opgemaakt te visualiseren.  

Voel je vrij om de datummethode aan te passen, het kleurenpalet te verwisselen, of het bereik uit te breiden tot volledige kolommen. Het patroon blijft hetzelfde: maak een werkboek, voeg een conditional‑formatting‑collectie toe, definieer de regel, en sla op.

Heb je vragen over een specifiek gebruiks‑scenario? Laat een reactie achter hieronder, en happy coding!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Excel‑automatisering met Aspose.Cells .NET: Werkboek maken & externe koppelingen instellen](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Excel‑werkboek maken en opslaan Aspose Cells Java](/cells/hongkong/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Excel‑werkboek maken en opslaan Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}