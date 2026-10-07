---
category: general
date: 2026-10-07
description: Erstelle eine Excel‑Arbeitsmappe in Python, setze die Hintergrundfarbe
  einer Zelle, passe die Spaltenbreite automatisch an und fülle Excel mit Datumswerten
  – alles mit einem kurzen Codebeispiel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- auto fit excel columns
- populate dates in excel
- how to create excel
language: de
lastmod: 2026-10-07
og_description: Erstelle eine Excel‑Arbeitsmappe in Python, setze anschließend die
  Zellhintergrundfarbe, passe die Spaltenbreite automatisch an und fülle Datumswerte
  in Excel ein. Befolge diese Schritt‑für‑Schritt‑Anleitung, um die Datei TimePeriodDemo.xlsx
  zu erstellen.
og_image_alt: Screenshot of a Python‑generated Excel workbook with pink highlighted
  cells
og_title: Excel‑Arbeitsmappe in Python erstellen – Hintergrund setzen & automatisch
  anpassen
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
title: Excel‑Arbeitsmappe in Python erstellen und Zellenhintergrund festlegen
url: /de/python/import-and-export/create-excel-workbook-in-python-and-set-cell-background/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-Arbeitsmappe in Python erstellen und Zellhintergrund festlegen

Erstellen Sie eine Excel-Arbeitsmappe in Python und wenden Sie bedingte Formatierung mit nur wenigen Codezeilen an. Dieses Tutorial zeigt Ihnen **wie man Excel**-Dateien programmgesteuert erstellt, den Zellhintergrund färbt, Excel‑Spalten automatisch anpasst und Daten in Excel mit der Aspose.Cells‑Bibliothek einfügt.

Sie lernen, wie Sie:
* Eine Arbeitsmappe initialisieren und das erste Arbeitsblatt erhalten.  
* Ein bedingtes Format definieren, das „Gestern“-Datumswerte hervorhebt.  
* Beispiel‑Datumswerte in bestimmte Zellen einfügen.  
* Spalten automatisch anpassen, damit die Daten klar sichtbar sind.  
* Die Arbeitsmappe in einem gewünschten Ordner speichern.

Die einzige Voraussetzung ist eine funktionierende Python 3‑Umgebung mit den Paketen `aspose-cells` und `aspose-pydrawing`, die installiert sind:

```bash
pip install aspose-cells aspose-pydrawing
```

---

## Excel-Arbeitsmappe in Python erstellen – Schritt für Schritt

Die folgenden Abschnitte zerlegen den Prozess in handhabbare Schritte. Jeder Schritt enthält den erforderlichen Code, eine Erklärung **warum** er wichtig ist, und einen Hinweis, um häufige Stolperfallen zu vermeiden.

### Schritt 1: Erforderliche Namespaces importieren und Hilfsfunktion definieren

```python
# Step 1: Import Aspose.Cells classes and supporting modules
from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime
import os
```

*Warum das wichtig ist*: Durch das Importieren der richtigen Klassen erhalten Sie Zugriff auf die Erstellung von Arbeitsmappen, bedingte Formatierung und Farbverwaltung.  
**Pro‑Tipp**: Halten Sie Importe am Anfang der Datei; das macht das Skript leichter lesbar und verhindert zirkuläre Import‑Fehler.

### Schritt 2: Die Arbeitsmappe erstellen und das erste Arbeitsblatt holen

```python
def create_workbook():
    # Step 2: Instantiate a new workbook (empty Excel file)
    book = Workbook()
    # Aspose.Cells creates a default worksheet; we retrieve it for further work
    sheet = book.worksheets[0]
    return book, sheet
```

Der Konstruktor `Workbook()` erzeugt eine leere Excel‑Arbeitsmappe im Speicher.  
**Warum**: Der Start mit einer frischen Arbeitsmappe stellt sicher, dass keine Formatierungen von vorherigen Durchläufen übrig bleiben.

### Schritt 3: Zellhintergrundfarbe mit einer bedingten Formatierung festlegen

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

*Warum*: Durch die Verwendung einer **time period**‑Bedingung wird automatisch jede Zelle hervorgehoben, die das gestrige Datum enthält, wodurch manuelle Datumsprüfungen entfallen.  
**Hinweis**: `Color.pink` ist nur ein Beispiel; Sie können jedes `Color`‑Objekt verwenden (`Color.yellow`, `Color.light_green` usw.).

### Schritt 4: Datumswerte in Excel einfügen

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

Hier **fügen wir Datumswerte in Excel** in die Zellen `I19` und `K20` ein. Das erste Datum löst die bedingte Formatierung aus, das zweite nicht.  
**Warum das wichtig ist**: Das Zeigen sowohl von passenden als auch von nicht passenden Werten hilft Ihnen zu überprüfen, dass die Regel wie erwartet funktioniert.

### Schritt 5: Excel‑Spalten automatisch anpassen für bessere Sichtbarkeit

```python
def auto_fit_columns(sheet):
    # Auto‑fit column L (index 12) so the content is fully visible
    sheet.auto_fit_column(12)   # <-- auto fit excel columns
```

`auto_fit_column` passt die Spaltenbreite anhand des längsten Zellwerts an.  
**Hinweis**: Rufen Sie diese Methode auf, nachdem Sie alle Daten geschrieben haben; sonst könnte die Breite auf unvollständigem Inhalt basieren.

### Schritt 6: Die Arbeitsmappe speichern

```python
def save_workbook(book, filename="TimePeriodDemo.xlsx"):
    out_path = os.path.join("YOUR_DIRECTORY", filename)
    os.makedirs(os.path.dirname(out_path), exist_ok=True)
    book.save(out_path, SaveFormat.XLSX)
    print(f"Workbook saved to: {out_path}")
```

Das Speichern der Datei schreibt die im Speicher befindliche Arbeitsmappe im modernen XLSX‑Format auf die Festplatte.  

### Vollständiges Skript – alles zusammenführen

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

**Erwartete Ausgabe**

```
Workbook saved to: YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Öffnen Sie die erzeugte Datei in Excel – die Zellen `I19:K20` zeigen einen pinken Hintergrund für das Datum, das auf „Gestern“ fällt, und Spalte L ist breit genug, um die Beschriftung ohne Abschneiden anzuzeigen.

---

## Warum dieser Ansatz am besten funktioniert

* **Single‑Pass‑Workflow** – Alle Vorgänge erfolgen auf derselben `Workbook`‑Instanz, wodurch unnötige I/O‑Operationen vermieden werden.  
* **Bedingte Formatierung** – Die Verwendung von `FormatConditionType.TIME_PERIOD` lässt Excel die Datumslogik übernehmen, was zuverlässiger ist als eigene Python‑Datumsprüfungen.  
* **Explizites Styling** – Das Setzen von `background_color` und `pattern` garantiert das visuelle Ergebnis über verschiedene Excel‑Versionen hinweg.  
* **Auto‑Fit nach Daten

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Excel‑Arbeitsmappe in Python erstellen – Vollständige Anleitung](/cells/english/python/import-and-export/create-excel-workbook-python-full-guide/)
- [Excel‑Arbeitsmappe in Python erstellen – Komplett‑Schritt‑für‑Schritt‑Anleitung](/cells/english/python/import-and-export/create-excel-workbook-python-complete-step-by-step-guide/)
- [Excel‑Arbeitsmappe in Python erstellen – Komplett‑Anleitung mit Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}