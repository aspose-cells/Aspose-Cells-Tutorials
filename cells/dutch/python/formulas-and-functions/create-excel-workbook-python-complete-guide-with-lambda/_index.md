---
category: general
date: 2026-06-08
description: Maak een Excel-werkmap Python-voorbeeld dat laat zien hoe je lambda in
  Excel gebruikt, rijen optelt met BYROW en berekeningen automatiseert in een paar
  stappen.
draft: false
keywords:
- create excel workbook python
- how to use lambda
- how to sum rows
- use lambda excel
language: nl
og_description: Maak een Excel-werkmap met Python en leer hoe je lambda in Excel kunt
  gebruiken om rijen efficiënt op te tellen met BYROW-formules.
og_title: Excel-werkboek maken met Python – Complete gids
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook Python example that shows how to use lambda in
    Excel, sum rows with BYROW, and automate calculations in a few steps.
  headline: Create Excel Workbook Python – Complete Guide with Lambda
  type: TechArticle
tags:
- python
- excel
- automation
title: Excel-werkmap maken met Python – Complete gids met Lambda
url: /nl/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak Excel-werkmap Python – Complete gids met Lambda

Ever wondered how to **create Excel workbook Python** scripts that automate boring number‑crunching? You're not alone—many developers hit a wall when they need to generate a sheet, drop a formula in, and pull the results back into their code.  

In this tutorial we'll also show **how to use lambda** in Excel, explain **how to sum rows** with the modern `BYROW` function, and give you a tidy, end‑to‑end example that you can copy‑paste and run today.

## Wat je zult leren

- Maak een nieuwe werkmap aan vanuit Python zonder Excel handmatig te openen.  
- Vul een bereik met een 3 × 3‑matrix van getallen.  
- Voeg een `BYROW`‑formule in die de **use lambda excel**‑syntaxis gebruikt om elke rij op te tellen.  
- Herbereken het blad zodat de formule wordt geëvalueerd, en lees vervolgens de resultaten terug in Python.  

Aan het einde van deze gids heb je een zelfstandige script die je kunt aanpassen voor facturen, score‑kaarten, of elke situatie waarin je **sum rows** on‑the‑fly moet uitvoeren.

### Vereisten

- Python 3.8+ geïnstalleerd.  
- De `openpyxl`‑bibliotheek (of `xlwings` als je een COM‑gebaseerde aanpak verkiest). We gebruiken `openpyxl` omdat het pure‑Python is en op alle platformen werkt.  
- Een recente versie van Microsoft Excel (365 of 2021) die de `BYROW`‑functie en Lambda‑formules ondersteunt.  

Installeer de bibliotheek met:

```bash
pip install openpyxl
```

> **Pro tip:** Als je op Windows tegen machtigingsproblemen aanloopt, gebruik dan `python -m pip install --user openpyxl`.

---

## Excel-werkmap maken met Python – Werkmap initialiseren

Het eerste wat we nodig hebben is een gloednieuwe werkmap‑object dat volledig in het geheugen leeft. Met `openpyxl` is dit een één‑regel‑code:

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and grab the first worksheet
wb = Workbook()
ws = wb.active   # .active is the first sheet by default
```

Waarom gebruiken we `wb.active` in plaats van indexeren met `Worksheets[0]`? `openpyxl` maakt het actieve blad direct beschikbaar, wat duidelijker is en een extra lijst‑lookup voorkomt. Als je ooit met meerdere bladen moet werken, kun je ze altijd toevoegen met `wb.create_sheet(title="MySheet")`.

---

## Vul het werkblad met gegevens – Een eenvoudige 3×3‑matrix

Vervolgens vullen we het blad met een kleine matrix. Dit weerspiegelt het klassieke “sum each row”‑voorbeeld en houdt de code compact.

```python
# Step 2: Define a 3×3 matrix of numbers
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Import the matrix into the worksheet starting at cell A1
for r_idx, row in enumerate(matrix, start=1):
    for c_idx, value in enumerate(row, start=1):
        ws.cell(row=r_idx, column=c_idx, value=value)
```

Je vraagt je misschien af waarom we handmatig loopen in plaats van `ws.append()` of `ws.values` te gebruiken. De expliciete lussen geven ons volledige controle over de startcel en maken het gemakkelijk om later offsets aan te passen—handig wanneer je een koprij of -kolom leeg wilt laten.

---

## Hoe Lambda te gebruiken in Excel‑formules

Excel’s **use lambda excel**‑functie laat je anonieme functies direct in een cel schrijven. Beschouw het als Python’s `lambda` maar dan binnen de spreadsheet‑engine. De syntaxis is:

```
=LAMBDA(parameter1, parameter2, …, calculation)
```

Wanneer gecombineerd met `BYROW`, kun je die lambda toepassen op elke rij van een bereik, waardoor een kolom met resultaten ontstaat. Dit is de kern van onze **how to sum rows**‑truc.

```python
# Step 3: Insert a BYROW formula that sums each row using a Lambda
ws["D1"] = "=BYROW(A1:C3, LAMBDA(r, SUM(r)))"
```

Wat gebeurt er onder de motorkap?

- `A1:C3` is het bronbereik (onze matrix).  
- `LAMBDA(r, SUM(r))` definieert een tijdelijke functie die een enkele rij (`r`) ontvangt en de som ervan retourneert.  
- `BYROW` voert die lambda uit voor **elke rij** en verspreidt de resultaten naar kolom D, beginnend bij `D1`.  

Omdat `BYROW` een *dynamic array*‑functie is, vult Excel automatisch `D1:D3` met de drie sommen.

> **Opmerking:** `BYROW` en Lambda‑formules zijn alleen beschikbaar in Excel 365/2021 en later. Als je een oudere versie gebruikt, moet je terugvallen op traditionele `SUM`‑formules of VBA.

---

## Hoe rijen op te tellen met BYROW en Lambda

Nu de formule in het blad staat, moeten we Excel laten evalueren. `openpyxl` zelf berekent geen formules; het leest/schrijft ze alleen. Om een berekening te starten kunnen we:

1. Sla de werkmap op en open deze in Excel (handmatig).  
2. Gebruik de `xlwings` COM‑engine om herberekening af te dwingen (vereist geïnstalleerde Excel).  

Voor een pure‑Python‑oplossing gebruiken we `xlwings` alleen voor de berekeningsstap—niets meer.

```python
import xlwings as xw

# Step 4: Recalculate the workbook so the BYROW formula is evaluated
# Save the workbook to a temporary file first
temp_path = "temp_workbook.xlsx"
wb.save(temp_path)

# Open the file with xlwings, force a calculation, then close
app = xw.App(visible=False)
book = app.books.open(temp_path)
book.api.CalculateFull()          # Full recalculation
book.save()
book.close()
app.quit()
```

Waarom niet `wb.calculate()` aanroepen? `openpyxl` mist een eigen engine, dus leunen we op Excel zelf via `xlwings`. De overhead is minimaal voor kleine bladen en geeft ons het exacte resultaat dat Excel zou weergeven.

---

## Herbereken en haal resultaten op – Haal de sommen terug in Python

Tot slot lezen we de verspreide resultaten uit kolom D. `openpyxl` maakt dit eenvoudig:

```python
# Step 5: Load the recalculated workbook and grab the results
wb = Workbook()  # re‑open the saved file
wb = xw.Book(temp_path).api  # alternative: use xlwings again to read values

# Using xlwings to fetch the range values as a Python list
results = xw.Range('D1:D3').value
print(results)   # Expected output: [6, 15, 24]
```

Als je liever binnen `openpyxl` blijft, kun je de cellen lezen na de Excel‑herberekening:

```python
from openpyxl import load_workbook

wb = load_workbook(temp_path, data_only=True)  # data_only reads calculated values
ws = wb.active
results = [ws[f"D{row}"].value for row in range(1, 4)]
print(results)   # -> [6, 15, 24]
```

Beide benaderingen geven je dezelfde lijst `[6, 15, 24]`, wat bevestigt dat **how to sum rows** met `BYROW` + Lambda werkt zoals geadverteerd.

---

## Randgevallen & Veelvoorkomende valkuilen

| Situatie | Waar op te letten | Oplossing |
|-----------|-------------------|-----|
| Excel‑versie ouder dan 365 | `BYROW` en `LAMBDA` verschijnen als `#NAME?` | Gebruik klassieke `=SUM(A1:C1)` handmatig gekopieerd naar beneden, of upgrade Excel. |
| Grote matrices (10 k+ rijen) | Herberekening kan traag worden | Roep `book.api.CalculateFullRebuild()` slechts één keer aan, of splits de werkmap. |
| Uitvoeren op een headless server zonder Excel | `xlwings` kan Excel niet starten | Schakel over naar een pure‑Python‑bibliotheek zoals `pandas` + `numpy` voor berekeningen, en schrijf vervolgens de resultaten. |
| Locale‑problemen (komma vs. puntkomma) | Formule kan worden afgewezen | Gebruik `ws["D1"].value = "=BYROW(A1:C3; LAMBDA(r; SUM(r)))"` voor locales die `;` gebruiken. |

---

## Volledig werkend voorbeeld (klaar om te kopiëren‑plakken)



## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Maak Excel-werkmap met Aspose.Cells Java - Complete gids](/cells/english/java/automation-batch-processing/excel-automation-aspose-cells-java-guide/)
- [Maak Excel-werkmap & automatiseer rapporten met Aspose.Cells](/cells/english/java/automation-batch-processing/aspose-cells-java-two-three-color-scales/)
- [Hoe een Excel-werkmap te maken en op te slaan als ODS met Aspose.Cells voor .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}