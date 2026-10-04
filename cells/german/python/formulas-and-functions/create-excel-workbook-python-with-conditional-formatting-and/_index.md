---
category: general
date: 2026-10-04
description: Erstelle ein Excel-Arbeitsbuch in Python mit Aspose.Cells. Lerne Excel-Bedingte
  Formatierung in Python, Zellenhintergrundfarbe in Python und das Formatieren von
  Datumszellen in Python in einem vollständigen Beispiel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create Excel workbook python
- excel conditional formatting python
- cell background color python
- format cells date python
language: de
lastmod: 2026-10-04
og_description: Erstellen Sie ein Excel‑Arbeitsbuch mit Python und Aspose.Cells. Dieses
  Tutorial zeigt Excel‑Bedingte Formatierung mit Python, Zellhintergrundfarbe mit
  Python und das Formatieren von Zellen nach Datum mit Python Schritt für Schritt.
og_image_alt: Screenshot of an Excel workbook created with Python showing highlighted
  yesterday dates
og_title: Excel-Arbeitsmappe mit Python erstellen – vollständige Anleitung mit bedingter
  Formatierung
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
title: Excel-Arbeitsmappe mit Python erstellen, bedingte Formatierung und Zellhintergrundfarbe
url: /de/python/formulas-and-functions/create-excel-workbook-python-with-conditional-formatting-and/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel‑Arbeitsmappe mit Python erstellen mit bedingter Formatierung und Zellhintergrundfarbe

Wenn Sie schnell **create Excel workbook python** benötigen, zeigt Ihnen dieser Leitfaden genau, wie es geht. Sie sehen ein vollständiges, ausführbares Beispiel, das **excel conditional formatting python** hinzufügt, die **cell background color python** ändert und **format cells date python** für eine „Yesterday“-Markierung.

In vielen Reporting‑Szenarien macht das visuelle Signal einer farbigen Zelle die Daten sofort verständlich. Dieses Tutorial führt Sie durch jede Code‑Zeile, erklärt, warum jeder Schritt wichtig ist, und liefert Ihnen ein sofort ausführbares Skript, das Sie an Ihre eigenen Projekte anpassen können.

## Was Sie erreichen werden

1. **create Excel workbook python** mit der Aspose.Cells‑Bibliothek verwenden.  
2. **excel conditional formatting python** anwenden, das automatisch Daten hervorhebt, die auf „Yesterday“ fallen.  
3. Die **cell background color python** auf Pink (oder jede gewünschte Farbe) setzen.  
4. **format cells date python** anwenden, sodass die Daten im Standard‑Excel‑Datumsformat angezeigt werden.  

Vorkenntnisse mit Aspose.Cells sind nicht erforderlich – Sie benötigen lediglich eine funktionierende Python 3‑Umgebung und pip‑Zugriff.

## Voraussetzungen

- Python 3.8 oder neuer installiert.  
- `aspose-cells` und `aspose-pydrawing` Pakete über `pip install aspose-cells aspose-pydrawing` installiert.  
- Grundlegende Vertrautheit mit Python‑Syntax und Excel‑Konzepten (Arbeitsmappen, Arbeitsblätter, Zellen).  

> **Pro tip:** Wenn Sie das Skript in einer virtuellen Umgebung ausführen, vermeiden Sie Versionskonflikte mit anderen Projekten.

## Schritt 1: Projekt einrichten und erforderliche Klassen importieren

Der erste Schritt, wenn Sie **create Excel workbook python** durchführen, besteht darin, die benötigten Aspose.Cells‑Klassen zu importieren. Diese Klassen geben Ihnen direkten Zugriff auf die Erstellung von Arbeitsmappen, bedingte Formatierung und Styling.

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

*Why this matters:* Das Importieren nur der benötigten Symbole hält den Namensraum übersichtlich und macht das Skript leichter lesbar. `Workbook` ist der Einstiegspunkt für **create Excel workbook python**, während `FormatConditionType` und `TimePeriodType` für **excel conditional formatting python** unverzichtbar sind.

## Schritt 2: Neue Arbeitsmappe erstellen und erstes Arbeitsblatt erhalten

Jetzt **create Excel workbook python** wir tatsächlich. Der Konstruktor `Workbook()` liefert Ihnen eine leere Excel‑Datei mit einem Standard‑Arbeitsblatt.

```python
# Step 2: Initialize a new workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Explanation:* Jede Excel‑Datei beginnt mit mindestens einem Arbeitsblatt. Standardmäßig nennt Aspose.Cells es „Sheet1“. Sie können später weitere Blätter hinzufügen, aber für diese Demonstration hält ein einzelnes Blatt das Beispiel fokussiert.

## Schritt 3: Zielbereich für die bedingte Formatierung festlegen

Bedingte Formatierung wirkt auf einen rechteckigen Bereich. Hier wählen wir den Bereich `I19:K20`, der uns drei Spalten und zwei Zeilen zum Spielen gibt.

```python
# Define the range that will receive conditional formatting
target_range = "I19:K20"

# Retrieve (or create) the ConditionalFormatting collection for that range
conditional_formatting = worksheet.conditional_formattings.get(target_range)
```

*Why we do this:* Die Methode `get` gibt ein `ConditionalFormatting`‑Objekt zurück, das an den angegebenen Bereich gebunden ist. Wenn der Bereich noch keine Formatierung hat, erstellt Aspose.Cells automatisch eine neue Sammlung.

## Schritt 4: Eine TIME_PERIOD‑Bedingung hinzufügen und die Hintergrundfarbe setzen

Dies ist der Kern von **excel conditional formatting python**. Wir fügen eine `TIME_PERIOD`‑Regel hinzu, die Zellen hervorhebt, die Daten enthalten, die auf „Yesterday“ fallen.

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

*Deep dive:*  
- `FormatConditionType.TIME_PERIOD` weist Excel an, Daten relativ zum aktuellen Datum zu bewerten.  
- `TimePeriodType.YESTERDAY` ist ein eingebauter Enum, der sich täglich automatisch aktualisiert, sodass die Arbeitsmappe stets das neueste „Yesterday“ hervorhebt.  
- Durch das Setzen von `background_color` auf `Color.pink` und das Muster auf `SOLID` erzielen wir den **cell background color python**‑Effekt ohne zusätzlichen VBA‑Code.

## Schritt 5: Den Bereich mit Beispieldaten füllen und Datumsformatierung anwenden

Um die bedingte Formatierung in Aktion zu sehen, benötigen wir echte Datumswerte. Außerdem müssen wir **format cells date python** anwenden, damit Excel sie als Datum und nicht als reine Zahl behandelt.

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

*Explanation:*  
- Die Zeile `style.number = 30` ist der **format cells date python**‑Schritt. Formatcode 30 entspricht dem kurzen Datumsformat (`m/d/yy`).  
- Die Verwendung einer Hilfsfunktion hält den Code DRY (Don’t Repeat Yourself) und erleichtert das spätere Hinzufügen weiterer Daten.

## Schritt 6: Beschriftung hinzufügen

Eine kleine Beschriftung hilft jedem, der die Arbeitsmappe öffnet, zu verstehen, warum die Zellen eingefärbt sind.

```python
# Place a label next to the formatted range
worksheet.cells.get("I20").put_value("Yesterday")
```

## Schritt 7: Arbeitsmappe auf Festplatte speichern

Schließlich **create Excel workbook python** wir auf die Festplatte, indem wir `save` aufrufen. Die Konstante `SaveFormat.XLSX` stellt sicher, dass die Datei im modernen Office Open XML‑Format vorliegt.

```python
# Define the output path – replace YOUR_DIRECTORY with a real folder
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"

# Save the workbook
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Wenn Sie `TimePeriodDemo.xlsx` in Excel öffnen, sehen Sie:

- Die Zellen `I19` und `K20` enthalten Daten.  
- Die Zelle, die „Yesterday“ entspricht (in diesem statischen Beispiel `I19`), ist pink hervorgehoben.  
- Die Beschriftung „Yesterday“ erscheint in `I20`.  

> **Tip:** Wenn Sie das Skript an einem anderen Tag ausführen, hebt die bedingte Formatierung weiterhin die Zelle hervor, deren Datum genau einen Tag vor dem aktuellen Systemdatum liegt – ohne Code‑Änderungen.

## Vollständiges Skript – zum Kopieren und Ausführen bereit

Unten finden Sie das komplette, eigenständige Programm, das alle oben genannten Schritte integriert. Kopieren Sie es in eine Datei namens `conditional_format_demo.py`, passen Sie `YOUR_DIRECTORY` an und führen Sie es mit `python conditional_format_demo.py` aus.

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

### Erwartete Ausgabe

Das Ausführen des Skripts gibt eine Bestätigungszeile aus:

```
Workbook saved to YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Das Öffnen der erzeugten Datei zeigt den pinken Hintergrund in der Zelle, die der „Yesterday“-Regel entspricht, und bestätigt, dass **excel conditional formatting python** und **cell background color python** zusammenarbeiten.

## Häufige Varianten und Sonderfälle

| Situation | Wie man den Code anpasst |
|-----------|--------------------------|
| **Andere Hervorhebungsfarbe** | Ändern Sie `Color.pink` zu einer anderen `Color`‑Konstante, z. B. `Color.light_green`. |
| **„Heute“ statt „Gestern“ hervorheben** | Setzen Sie `condition.time_period = TimePeriodType.TODAY`. |
| **Formatierung auf eine gesamte Spalte anwenden** | Verwenden Sie einen Bereich wie `"A:A"` und passen Sie die Variable `target_range` entsprechend an. |
| **Ein benutzerdefiniertes Datumsformat verwenden** | Ersetzen Sie `style.number = 30` durch `style.custom = "dd-mmm-yyyy"` für ein lesbarereres Format. |
| **Mehrere Bedingungen für denselben Bereich** |  |

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Excel‑Arbeitsmappe mit Python erstellen – Komplett‑Leitfaden mit Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)
- [Excel‑Arbeitsmappe erstellen und als PDF in ASP.NET mit Aspose.Cells speichern](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Excel‑Arbeitsmappe als ODS mit Aspose.Cells für .NET erstellen und speichern](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}