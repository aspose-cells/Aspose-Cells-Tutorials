---
category: general
date: 2026-09-05
description: Maak een Excel-werkmap in Python en voeg voorwaardelijke opmaak toe om
  cellen van gisteren te markeren. Leer de volledige code en waarom elke stap belangrijk
  is.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- add conditional formatting excel
- highlight cells based on date
- add conditional formatting range
- how to highlight yesterday cells
language: nl
lastmod: 2026-09-05
og_description: Maak een Excel‑werkmap in Python en voeg voorwaardelijke opmaak toe
  om cellen van gisteren te markeren. Volg deze stapsgewijze handleiding voor een
  volledige oplossing.
og_image_alt: Screenshot of an Excel sheet where cells are highlighted after creating
  Excel workbook in Python
og_title: Maak een Excel‑werkboek in Python – voeg voorwaardelijke opmaak toe
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
title: Maak Excel-werkmap in Python met voorwaardelijke opmaak
url: /nl/python/formatting/create-excel-workbook-in-python-with-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-werkmap maken in Python met voorwaardelijke opmaak

Als je een **Excel-werkmap in Python maken** moet voor een rapportagetaken, laat deze gids je zien hoe je een werkmap genereert en een voorwaardelijke opmaakregel toepast die de datums van gisteren markeert. Je ziet de exacte code, waarom elke regel bestaat, en hoe je de oplossing kunt aanpassen voor andere datumbereiken.

Voorwaardelijke opmaak is een krachtige manier om aandacht te vestigen op gegevens die aan een specifieke voorwaarde voldoen. In deze tutorial gebruiken we de Aspose.Cells‑bibliotheek voor Python via .NET, die volledige Excel‑functionaliteit biedt zonder Microsoft Office te vereisen. Aan het einde van de gids heb je een bestand waarin cellen in het bereik *I19:K20* roze worden wanneer ze de datum van gisteren bevatten.

## Voorvereisten

Voordat je begint, zorg dat je het volgende hebt:

* Python 3.9+ geïnstalleerd
* `aspose-cells`‑pakket (installeren met `pip install aspose-cells`)
* Basiskennis van Python‑syntaxis
* Schrijfrechten in de map waar de werkmap wordt opgeslagen

De code werkt op Windows, macOS en Linux zolang de .NET‑runtime beschikbaar is.

## Excel-werkmap maken in Python

De eerste stap is het instantieren van een `Workbook`‑object en het ophalen van het standaardwerkblad. Dit object vertegenwoordigt het volledige Excel‑bestand in het geheugen.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Waarom dit belangrijk is*: `Workbook()` maakt een lege werkmap met één werkblad. Toegang tot `worksheets[0]` geeft je een referentie om later gegevens, stijlen en opmaak toe te voegen.

## Voorwaardelijke opmaakbereik toevoegen

Vervolgens definiëren we het gebied dat door de voorwaardelijke regel wordt geëvalueerd. Het bereik `I19:K20` omvat zes cellen over twee rijen.

```python
# Define the range that will receive the conditional formatting rule
condition_collection = worksheet.conditional_formattings.add("I19:K20")
```

*Waarom dit belangrijk is*: Het toevoegen van een voorwaardelijke opmaakcollectie aan een specifiek bereik isoleert de regel, zodat deze geen invloed heeft op niet‑gerelateerde cellen. Dit voldoet aan de **add conditional formatting range**‑vereiste.

## Regel definiëren: cellen markeren op basis van datum

We maken nu een voorwaarde van het type `TIME_PERIOD`. Dit vertelt Excel om de waarde van elke cel te vergelijken met een vooraf gedefinieerd tijdvenster.

```python
from aspose.cells import FormatConditionType, TimePeriodType

# Add a TIME_PERIOD condition to the collection
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Set the time period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY
```

*Waarom dit belangrijk is*: `TIME_PERIOD` is het enige ingebouwde type dat direct “Yesterday”, “Today”, “Last Week”, enz. ondersteunt. Door `condition.time_period` in te stellen op `YESTERDAY`, evalueert de regel automatisch de datumwaarde van elke cel ten opzichte van de dag vóór de huidige datum.

## Stijl toepassen op de cellen die aan de voorwaarde voldoen

Voorwaardelijke opmaak heeft ook een visuele stijl nodig. Hier kiezen we een roze effen vulling zodat de overeenkomende cellen opvallen.

```python
from aspose.pydrawing import Color as DrawingColor
from aspose.cells import BackgroundType

# Apply a pink solid background to cells that satisfy the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID
```

*Waarom dit belangrijk is*: Het stijlobject bepaalt hoe Excel cellen weergeeft die aan de voorwaarde voldoen. Het gebruik van een effen roze vulling voldoet aan de **highlight cells based on date**‑vereiste en maakt het resultaat gemakkelijk te verifiëren.

## Voorbeelddata invoegen voor evaluatie

Om de regel in werking te zien, voegen we twee datums in – één die op gisteren valt en één die dat niet doet. Het getalformaat `30` komt overeen met het ingebouwde datumformaat `mm-dd-yy`.

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

*Waarom dit belangrijk is*: Het aanbieden van zowel een overeenkomende als een niet‑overeenkomende datum stelt je in staat te controleren of de voorwaardelijke opmaak correct werkt. Pas de datums aan op de huidige maand wanneer je het script uitvoert, of vervang ze door dynamische waarden.

## Werkmap opslaan

Tot slot schrijven we het bestand naar schijf. De constante `SaveFormat.XLSX` zorgt ervoor dat de output een modern Excel‑bestand is.

```python
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

*Waarom dit belangrijk is*: Het bewaren van de werkmap stelt je in staat deze te openen in Excel, LibreOffice of elke viewer die XLSX ondersteunt. Het afgedrukte pad bevestigt waar het bestand is weggeschreven.

## Volledig script

Alle onderdelen samengevoegd, ziet het complete, uitvoerbare script er als volgt uit:

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

### Verwachte output

Wanneer je `TimePeriodExample.xlsx` opent:

* Cel **I19** heeft een roze achtergrond omdat de waarde overeenkomt met gisteren.
* Cel **K20** behoudt de standaardachtergrond omdat de datum buiten de periode valt.
* Het label **“Yesterday”** staat in cel I20 voor duidelijkheid.

## Veelvoorkomende variaties en randgevallen

| Situatie | Aanpassing |
|-----------|------------|
| **Vandaag markeren in plaats van gisteren** | Verander `condition.time_period = TimePeriodType.TODAY`. |
| **De regel toepassen op een groter gebied** | Werk de bereik‑string in `add("I19:K20")` bij naar bijvoorbeeld `"A1:Z100"`. |
| **Een andere vulkleur gebruiken** | Vervang `DrawingColor.pink` door een andere `DrawingColor` (bijv. `DrawingColor.light_green`). |
| **Werken met dynamische datums** | Bereken `datetime.now() - timedelta(days=1)` voor gisteren en schrijf die waarde naar de cellen voordat je de regel toepast. |

**Pro tip:** Wanneer je de werkmap programmatisch voor veel gebruikers genereert, houd de definitie van de voorwaardelijke opmaak gescheiden van het invoegen van gegevens. Zo kun je dezelfde stijl hergebruiken in meerdere bladen zonder code te dupliceren.

## Het resultaat programmatisch verifiëren (optioneel)

Wil je de opmaak bevestigen zonder Excel te openen, dan kun je de stijl van een cel inspecteren na het opslaan:



## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Excel Automation&#58; Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Create Excel Workbook and Add Labels with Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/data-labeling/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}