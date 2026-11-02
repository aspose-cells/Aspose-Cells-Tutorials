---
category: general
date: 2026-10-04
description: Maak een Excel-werkmap in Python met Aspose.Cells. Leer Excel-voorwaardelijke
  opmaak in Python, celachtergrondkleur in Python en datumopmaak van cellen in Python
  in een volledig voorbeeld.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create Excel workbook python
- excel conditional formatting python
- cell background color python
- format cells date python
language: nl
lastmod: 2026-10-04
og_description: Maak een Excel-werkmap in Python met Aspose.Cells. Deze tutorial toont
  Excel-voorwaardelijke opmaak in Python, celachtergrondkleur in Python en het opmaken
  van datumcellen in Python stap voor stap.
og_image_alt: Screenshot of an Excel workbook created with Python showing highlighted
  yesterday dates
og_title: Excel-werkmap maken met Python – volledige gids met voorwaardelijke opmaak
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
title: Maak een Excel-werkboek in Python met voorwaardelijke opmaak en celachtergrondkleur
url: /nl/python/formulas-and-functions/create-excel-workbook-python-with-conditional-formatting-and/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak Excel workbook python met voorwaardelijke opmaak en celachtergrondkleur

Als je snel een **Excel workbook python** wilt maken, laat deze gids je precies zien hoe. Je ziet een compleet, uitvoerbaar voorbeeld dat **excel conditional formatting python** toevoegt, de **cell background color python** wijzigt, en **format cells date python** voor een “Yesterday” markering.

In veel rapportagescenario's maakt de visuele aanwijzing van een gekleurde cel de gegevens direct begrijpelijk. Deze tutorial leidt je door elke regel code, legt uit waarom elke stap belangrijk is, en geeft je een kant‑klaar script dat je kunt aanpassen aan je eigen projecten.

## Wat je zult bereiken

1. **create Excel workbook python** met behulp van de Aspose.Cells bibliotheek.  
2. Pas **excel conditional formatting python** toe die automatisch datums markeert die op “Yesterday” vallen.  
3. Stel de **cell background color python** in op roze (of elke gewenste kleur).  
4. **format cells date python** zodat de datums verschijnen in de standaard Excel‑datumstijl.  

Ervaring met Aspose.Cells is niet vereist—alleen een werkende Python 3‑omgeving en pip-toegang.

## Vereisten

- Python 3.8 of nieuwer geïnstalleerd.  
- Pakketten `aspose-cells` en `aspose-pydrawing` geïnstalleerd via `pip install aspose-cells aspose-pydrawing`.  
- Basiskennis van Python‑syntaxis en Excel‑concepten (werkboeken, werkbladen, cellen).  

> **Pro tip:** Als je het script in een virtuele omgeving uitvoert, vermijd je versieconflicten met andere projecten.

## Stap 1: Zet het project op en importeer vereiste klassen

De eerste stap bij het **create Excel workbook python** is het importeren van de Aspose.Cells‑klassen die je nodig hebt. Deze klassen geven je directe toegang tot het maken van werkboeken, voorwaardelijke opmaak en styling.

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

*Waarom dit belangrijk is:* Alleen de benodigde symbolen importeren houdt de namespace overzichtelijk en maakt het script makkelijker leesbaar. `Workbook` is het toegangspunt voor **create Excel workbook python**, terwijl `FormatConditionType` en `TimePeriodType` essentieel zijn voor **excel conditional formatting python**.

## Stap 2: Maak een nieuw werkboek en verkrijg het eerste werkblad

Nu **create Excel workbook python** we daadwerkelijk. De `Workbook()`‑constructor geeft je een leeg Excel‑bestand met een standaard werkblad.

```python
# Step 2: Initialize a new workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Uitleg:* Elk Excel‑bestand begint met ten minste één werkblad. Standaard noemt Aspose.Cells dit “Sheet1”. Je kunt later meer bladen toevoegen, maar voor deze demonstratie houdt één blad het voorbeeld gefocust.

## Stap 3: Definieer het doelbereik voor voorwaardelijke opmaak

Voorwaardelijke opmaak werkt op een rechthoekig bereik. Hier kiezen we het bereik `I19:K20`, dat ons drie kolommen en twee rijen geeft om mee te werken.

```python
# Define the range that will receive conditional formatting
target_range = "I19:K20"

# Retrieve (or create) the ConditionalFormatting collection for that range
conditional_formatting = worksheet.conditional_formattings.get(target_range)
```

*Waarom we dit doen:* De `get`‑methode retourneert een `ConditionalFormatting`‑object dat aan het opgegeven bereik is gekoppeld. Als het bereik nog geen opmaak heeft, maakt Aspose.Cells automatisch een nieuwe collectie aan.

## Stap 4: Voeg een TIME_PERIOD‑conditie toe en stel de achtergrondkleur in

Dit is de kern van **excel conditional formatting python**. We voegen een `TIME_PERIOD`‑regel toe die cellen markeert met datums die op “Yesterday” vallen.

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

*Diepgaande uitleg:*  
- `FormatConditionType.TIME_PERIOD` vertelt Excel om datums te evalueren ten opzichte van de huidige datum.  
- `TimePeriodType.YESTERDAY` is een ingebouwde enum die elke dag automatisch wordt bijgewerkt, zodat het werkboek altijd de meest recente “Yesterday” markeert.  
- Door `background_color` in te stellen op `Color.pink` en het patroon op `SOLID`, bereiken we het **cell background color python**‑effect zonder extra VBA‑code.

## Stap 5: Vul het bereik met voorbeelddatums en pas datumopmaak toe

Om de voorwaardelijke opmaak in actie te zien, hebben we echte datumwaarden nodig. We moeten ook **format cells date python** toepassen zodat Excel ze als datums behandelt in plaats van als gewone getallen.

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

*Uitleg:*  
- De regel `style.number = 30` is de **format cells date python** stap. Opmaakcode 30 komt overeen met het korte datumformaat (`m/d/yy`).  
- Het gebruik van een hulpfunctie houdt de code DRY (Don’t Repeat Yourself) en maakt het eenvoudig om later meer datums toe te voegen.

## Stap 6: Voeg een beschrijvend label toe

```python
# Place a label next to the formatted range
worksheet.cells.get("I20").put_value("Yesterday")
```

## Stap 7: Sla het werkboek op schijf

Tot slot **create Excel workbook python** we op schijf door `save` aan te roepen. De constante `SaveFormat.XLSX` zorgt ervoor dat het bestand in het moderne Office Open XML‑formaat staat.

```python
# Define the output path – replace YOUR_DIRECTORY with a real folder
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"

# Save the workbook
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Wanneer je `TimePeriodDemo.xlsx` in Excel opent, zie je:

- Cellen `I19` en `K20` bevatten datums.  
- De cel die overeenkomt met “Yesterday” (in dit statische voorbeeld, `I19`) is roze gemarkeerd.  
- Het label “Yesterday” verschijnt in `I20`.  

> **Tip:** Als je het script op een andere dag uitvoert, markeert de voorwaardelijke opmaak nog steeds de cel waarvan de datum precies één dag vóór de huidige systeemdatum ligt—geen codewijzigingen nodig.

## Volledig script – klaar om te kopiëren en uit te voeren

Hieronder staat het volledige, zelfstandige programma dat alle bovenstaande stappen bevat. Kopieer het naar een bestand genaamd `conditional_format_demo.py`, pas `YOUR_DIRECTORY` aan, en voer uit met `python conditional_format_demo.py`.

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

### Verwachte output

Het uitvoeren van het script geeft een bevestigingsregel weer:

```
Workbook saved to YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Het openen van het gegenereerde bestand toont de roze achtergrond op de cel die overeenkomt met de “Yesterday”‑regel, waarmee wordt bevestigd dat **excel conditional formatting python** en **cell background color python** samenwerken.

## Veelvoorkomende variaties en randgevallen

| Situatie | Hoe de code aan te passen |
|-----------|---------------------------|
| **Andere markeerkleur** | Verander `Color.pink` naar een andere `Color`‑constante, bijv. `Color.light_green`. |
| **Markeer “Today” in plaats van “Yesterday”** | Stel `condition.time_period = TimePeriodType.TODAY` in. |
| **Pas opmaak toe op een hele kolom** | Gebruik een bereik zoals `"A:A"` en pas de variabele `target_range` dienovereenkomstig aan. |
| **Gebruik een aangepast datumformaat** | Vervang `style.number = 30` door `style.custom = "dd-mmm-yyyy"` voor een beter leesbaar formaat. |
| **Meerdere voorwaarden op hetzelfde bereik** |  |

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Create Excel Workbook Python – Complete Guide with Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)
- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}