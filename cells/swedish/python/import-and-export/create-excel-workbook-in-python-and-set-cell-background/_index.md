---
category: general
date: 2026-10-07
description: Skapa en Excel-arbetsbok i Python, sätt cellbakgrundsfärg, anpassa kolumnbredder
  automatiskt och fyll i datum i Excel med ett kort kodexempel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- auto fit excel columns
- populate dates in excel
- how to create excel
language: sv
lastmod: 2026-10-07
og_description: Skapa en Excel-arbetsbok i Python, sätt sedan cellbakgrundsfärg, anpassa
  kolumnbredd automatiskt och fyll i datum i Excel. Följ den här steg‑för‑steg‑guiden
  för att generera en TimePeriodDemo.xlsx‑fil.
og_image_alt: Screenshot of a Python‑generated Excel workbook with pink highlighted
  cells
og_title: Skapa Excel‑arbetsbok i Python – sätt bakgrund och auto‑anpassa
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
title: Skapa Excel-arbetsbok i Python och sätt cellbakgrund
url: /sv/python/import-and-export/create-excel-workbook-in-python-and-set-cell-background/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel-arbetsbok i Python och sätt cellbakgrund

Skapa en Excel-arbetsbok i Python och tillämpa villkorsstyrd formatering med bara några rader kod. Denna handledning visar dig **hur du skapar excel**-filer programatiskt, sätter cellbakgrundsfärg, auto‑fit Excel‑kolumner och fyller i datum i Excel med hjälp av Aspose.Cells‑biblioteket.

Du kommer att lära dig att:
* Initiera en arbetsbok och hämta det första kalkylbladet.  
* Definiera ett villkorligt format som markerar “Yesterday”-datum.  
* Infoga exempeldatum i specifika celler.  
* Auto‑anpassa kolumner så att data är tydligt synligt.  
* Spara arbetsboken i en vald mapp.

Det enda förutsättningen är en fungerande Python 3-miljö med paketen `aspose-cells` och `aspose-pydrawing` installerade:

```bash
pip install aspose-cells aspose-pydrawing
```

---

## Skapa Excel-arbetsbok i Python – steg för steg

Följande avsnitt delar upp processen i hanterbara steg. Varje steg innehåller den nödvändiga koden, en förklaring till **varför** det är viktigt, och ett tips för att undvika vanliga fallgropar.

### Steg 1: Importera nödvändiga namnrymder och definiera en hjälpfunktion

```python
# Step 1: Import Aspose.Cells classes and supporting modules
from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime
import os
```

*Varför detta är viktigt*: Att importera rätt klasser ger dig tillgång till skapande av arbetsbok, villkorsstyrd formatering och färghantering.  
**Proffstips**: Håll importerna högst upp i filen; det gör skriptet lättare att läsa och förhindrar cirkulära importfel.

### Steg 2: Skapa arbetsboken och hämta det första kalkylbladet

```python
def create_workbook():
    # Step 2: Instantiate a new workbook (empty Excel file)
    book = Workbook()
    # Aspose.Cells creates a default worksheet; we retrieve it for further work
    sheet = book.worksheets[0]
    return book, sheet
```

`Workbook()`‑konstruktorn skapar en tom Excel‑arbetsbok i minnet.  
**Varför**: Att börja med en ny arbetsbok säkerställer att ingen tidigare formatering finns kvar från tidigare körningar.

### Steg 3: Sätt cellbakgrundsfärg med ett villkorligt format

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

*Varför*: Att använda ett **time period**‑villkor markerar automatiskt varje cell som innehåller gårdagens datum, vilket eliminerar manuella datumkontroller.  
**Tips**: `Color.pink` är bara ett exempel; du kan använda vilket `Color`‑objekt som helst (`Color.yellow`, `Color.light_green`, etc.).

### Steg 4: Fyll i datum i Excel

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

Här **fyller vi i datum i Excel**‑cellerna `I19` och `K20`. Det första datumet kommer att utlösa den villkorliga formateringen, medan det andra inte gör det.  
**Varför detta är viktigt**: Att demonstrera både matchande och icke‑matchande värden hjälper dig att verifiera att regeln fungerar som förväntat.

### Steg 5: Auto‑anpassa Excel-kolumner för bättre synlighet

```python
def auto_fit_columns(sheet):
    # Auto‑fit column L (index 12) so the content is fully visible
    sheet.auto_fit_column(12)   # <-- auto fit excel columns
```

`auto_fit_column` justerar kolumnbredden baserat på det längsta cellvärdet.  
**Tips**: Anropa detta efter att du har skrivit all data; annars kan bredden beräknas på ofullständigt innehåll.

### Steg 6: Spara arbetsboken

```python
def save_workbook(book, filename="TimePeriodDemo.xlsx"):
    out_path = os.path.join("YOUR_DIRECTORY", filename)
    os.makedirs(os.path.dirname(out_path), exist_ok=True)
    book.save(out_path, SaveFormat.XLSX)
    print(f"Workbook saved to: {out_path}")
```

Att spara filen skriver den minnesbaserade arbetsboken till disk i det moderna XLSX‑formatet.  

### Fullt skript – sätt ihop allt

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

**Förväntat resultat**

```
Workbook saved to: YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Öppna den genererade filen i Excel – cellerna `I19:K20` kommer att visa en rosa bakgrund för datumet som faller på “Yesterday”, och kolumn L kommer att vara tillräckligt bred för att visa etiketten utan att klippa.

---

## Varför detta tillvägagångssätt fungerar bäst

* **Enkel‑passarbetsflöde** – Alla operationer sker på samma `Workbook`‑instans, vilket undviker onödig I/O.  
* **Villkorsstyrd formatering** – Att använda `FormatConditionType.TIME_PERIOD` låter Excel hantera datumlogik, vilket är mer pålitligt än att skriva egna Python‑datumkontroller.  
* **Explicit styling** – Att sätta `background_color` och `pattern` garanterar det visuella resultatet i alla Excel‑versioner.  
* **Auto‑fit efter data**

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Create Excel Workbook Python – Full Guide](/cells/english/python/import-and-export/create-excel-workbook-python-full-guide/)
- [Create Excel Workbook Python – Complete Step‑by‑Step Guide](/cells/english/python/import-and-export/create-excel-workbook-python-complete-step-by-step-guide/)
- [Create Excel Workbook Python – Complete Guide with Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}