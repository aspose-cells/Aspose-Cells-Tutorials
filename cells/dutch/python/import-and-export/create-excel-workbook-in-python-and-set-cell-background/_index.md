---
category: general
date: 2026-10-07
description: Maak een Excel-werkmap in Python, stel de achtergrondkleur van cellen
  in, pas de kolombreedte automatisch aan en vul datums in Excel in met een beknopt
  codevoorbeeld.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- auto fit excel columns
- populate dates in excel
- how to create excel
language: nl
lastmod: 2026-10-07
og_description: Maak een Excel-werkmap in Python, stel vervolgens de achtergrondkleur
  van cellen in, pas de kolombreedte automatisch aan en vul datums in Excel. Volg
  deze stapsgewijze handleiding om een TimePeriodDemo.xlsx‑bestand te genereren.
og_image_alt: Screenshot of a Python‑generated Excel workbook with pink highlighted
  cells
og_title: Excel-werkboek maken in Python – achtergrond instellen & automatisch aanpassen
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  headline: Create Excel workbook in Python and set cell background
  type: TechArticle
- description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  name: Create Excel workbook in Python and set cell background
  steps:
  - name: Import required namespaces and define a helper function
    text: '```python # Step 1: Import Aspose.Cells classes and supporting modules
      from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType,
      SaveFormat from aspose.pydrawing import Color from datetime import datetime
      import os ```'
  - name: Create the workbook and get the first worksheet
    text: '```python def create_workbook(): # Step 2: Instantiate a new workbook (empty
      Excel file) book = Workbook() # Aspose.Cells creates a default worksheet; we
      retrieve it for further work sheet = book.worksheets[0] return book, sheet ```'
  - name: Set cell background color with a conditional format
    text: '```python def add_yesterday_rule(sheet): # Define a conditional format
      for the range I19:K20 (Yesterday) conds = sheet.get_range("I19:K20").format_conditions
      idx = conds.add_condition(FormatConditionType.TIME_PERIOD) cond = conds[idx]'
  - name: Populate dates in Excel
    text: '```python def populate_sample_dates(sheet): # Insert a date that falls
      on yesterday relative to the demo data cell = sheet.cells.get("I19") cell.put_value(datetime(2008,
      7, 30)) # sample date cell.style.number = 30 # Excel’s date format ID cell.set_style(cell.style)'
  - name: Auto‑fit Excel columns for better visibility
    text: '```python def auto_fit_columns(sheet): # Auto‑fit column L (index 12) so
      the content is fully visible sheet.auto_fit_column(12) # <-- auto fit excel
      columns ```'
  - name: Save the workbook
    text: '```python def save_workbook(book, filename="TimePeriodDemo.xlsx"): out_path
      = os.path.join("YOUR_DIRECTORY", filename) os.makedirs(os.path.dirname(out_path),
      exist_ok=True) book.save(out_path, SaveFormat.XLSX) print(f"Workbook saved to:
      {out_path}") ```'
  - name: Full script – putting it all together
    text: '```python def main(): # Create workbook and obtain the first worksheet
      book, sheet = create_workbook()'
  type: HowTo
tags:
- Excel
- Python
- Aspose.Cells
title: Maak een Excel-werkboek in Python en stel de celachtergrond in
url: /nl/python/import-and-export/create-excel-workbook-in-python-and-set-cell-background/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak Excel-werkmap in Python en stel celachtergrond in

Maak een Excel-werkmap in Python en pas voorwaardelijke opmaak toe met slechts een paar regels code. Deze tutorial laat je zien **hoe je Excel**‑bestanden programmatically maakt, de celachtergrondkleur instelt, Excel‑kolommen automatisch aanpast, en datums in Excel invoegt met behulp van de Aspose.Cells‑bibliotheek.

Je leert hoe je:
* Een werkmap initialiseert en het eerste werkblad verkrijgt.  
* Een voorwaardelijke opmaak definieert die “Gisteren”‑datums markeert.  
* Voorbeelddatums in specifieke cellen invoegt.  
* Kolommen automatisch aanpast zodat de gegevens duidelijk zichtbaar zijn.  
* De werkmap opslaat in een gekozen map.

De enige voorwaarde is een werkende Python 3‑omgeving met de `aspose-cells` en `aspose-pydrawing` pakketten geïnstalleerd:

```bash
pip install aspose-cells aspose-pydrawing
```

---

## Maak Excel-werkmap in Python – stap voor stap

De volgende secties splitsen het proces in beheersbare stappen. Elke stap bevat de benodigde code, een uitleg **waarom** het belangrijk is, en een tip om veelvoorkomende valkuilen te vermijden.

### Stap 1: Importeer vereiste namespaces en definieer een hulpfunctie

```python
# Step 1: Import Aspose.Cells classes and supporting modules
from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime
import os
```

*Waarom dit belangrijk is*: Het importeren van de juiste klassen geeft je toegang tot het maken van werkmappen, voorwaardelijke opmaak en kleurbeheer.  
**Pro tip**: Houd imports bovenaan het bestand; dit maakt het script makkelijker leesbaar en voorkomt circulaire import‑fouten.

### Stap 2: Maak de werkmap en haal het eerste werkblad op

```python
def create_workbook():
    # Step 2: Instantiate a new workbook (empty Excel file)
    book = Workbook()
    # Aspose.Cells creates a default worksheet; we retrieve it for further work
    sheet = book.worksheets[0]
    return book, sheet
```

De `Workbook()`‑constructor maakt een lege Excel‑werkmap in het geheugen.  
**Waarom**: Beginnen met een verse werkmap zorgt ervoor dat er geen overgebleven opmaak van eerdere runs aanwezig is.

### Stap 3: Stel celachtergrondkleur in met een voorwaardelijke opmaak

```python
def add_yesterday_rule(sheet):
    # Define a conditional format for the range I19:K20 (Yesterday)
    conds = sheet.get_range("I19:K20").format_conditions
    idx = conds.add_condition(FormatConditionType.TIME_PERIOD)
    cond = conds[idx]

    # Apply visual style – this is where we set the cell background color
    cond.style.background_color = Color.pink          # <-- set cell background color
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

*Waarom*: Het gebruik van een **tijdperiode**‑conditie markeert automatisch elke cel die de datum van gisteren bevat, waardoor handmatige datumcontroles overbodig worden.  
**Tip**: `Color.pink` is slechts een voorbeeld; je kunt elk `Color`‑object gebruiken (`Color.yellow`, `Color.light_green`, etc.).

### Stap 4: Datums invoegen in Excel

```python
def populate_sample_dates(sheet):
    # Insert a date that falls on yesterday relative to the demo data
    cell = sheet.cells.get("I19")
    cell.put_value(datetime(2008, 7, 30))   # sample date
    cell.style.number = 30                 # Excel’s date format ID
    cell.set_style(cell.style)

    # Insert another date outside the “Yesterday” range
    cell = sheet.cells.get("K20")
    cell.put_value(datetime(2008, 8, 3))
    cell.style.number = 30
    cell.set_style(cell.style)

    # Add a label for the rule
    sheet.cells.get("I20").put_value("Yesterday")
```

Hier **voegen we datums in Excel** in de cellen `I19` en `K20`. De eerste datum zal de voorwaardelijke opmaak activeren, terwijl de tweede dat niet zal doen.  
**Waarom dit belangrijk is**: Het demonstreren van zowel overeenkomende als niet‑overeenkomende waarden helpt je te verifiëren dat de regel werkt zoals verwacht.

### Stap 5: Kolommen automatisch aanpassen voor betere zichtbaarheid

```python
def auto_fit_columns(sheet):
    # Auto‑fit column L (index 12) so the content is fully visible
    sheet.auto_fit_column(12)   # <-- auto fit excel columns
```

`auto_fit_column` past de kolombreedte aan op basis van de langste celwaarde.  
**Tip**: Roep dit aan nadat je alle gegevens hebt geschreven; anders kan de breedte worden berekend op basis van onvolledige inhoud.

### Stap 6: De werkmap opslaan

```python
def save_workbook(book, filename="TimePeriodDemo.xlsx"):
    out_path = os.path.join("YOUR_DIRECTORY", filename)
    os.makedirs(os.path.dirname(out_path), exist_ok=True)
    book.save(out_path, SaveFormat.XLSX)
    print(f"Workbook saved to: {out_path}")
```

Het opslaan van het bestand schrijft de werkmap in het geheugen naar schijf in het moderne XLSX‑formaat.

### Volledig script – alles samenvoegen

```python
def main():
    # Create workbook and obtain the first worksheet
    book, sheet = create_workbook()

    # Apply conditional formatting (set cell background color)
    add_yesterday_rule(sheet)

    # Populate the demo dates (populate dates in excel)
    populate_sample_dates(sheet)

    # Auto‑fit the relevant column (auto fit excel columns)
    auto_fit_columns(sheet)

    # Persist the file
    save_workbook(book)

if __name__ == "__main__":
    main()
```

**Verwachte output**

```
Workbook saved to: YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Open het gegenereerde bestand in Excel – cellen `I19:K20` tonen een roze achtergrond voor de datum die op “Gisteren” valt, en kolom L is breed genoeg om het label zonder afsnijden weer te geven.

---

## Waarom deze aanpak het beste werkt

* **Single‑pass workflow** – Alle bewerkingen gebeuren op dezelfde `Workbook`‑instantie, waardoor onnodige I/O wordt vermeden.  
* **Conditional formatting** – Het gebruik van `FormatConditionType.TIME_PERIOD` laat Excel de datumlogica afhandelen, wat betrouwbaarder is dan zelfgeschreven Python‑datumcontroles.  
* **Explicit styling** – Het instellen van `background_color` en `pattern` garandeert het visuele resultaat in verschillende Excel‑versies.  
* **Auto‑fit after data** – (vervolg van de bullet, behouden zoals origineel)

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Create Excel Workbook Python – Full Guide](/cells/english/python/import-and-export/create-excel-workbook-python-full-guide/)
- [Create Excel Workbook Python – Complete Step‑by‑Step Guide](/cells/english/python/import-and-export/create-excel-workbook-python-complete-step-by-step-guide/)
- [Create Excel Workbook Python – Complete Guide with Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}