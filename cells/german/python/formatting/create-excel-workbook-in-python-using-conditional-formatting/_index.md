---
category: general
date: 2026-09-21
description: Erfahren Sie, wie Sie in Python eine Excel‑Arbeitsmappe erstellen, die
  Hintergrundfarbe von Zellen festlegen und datumsbasierte bedingte Formatierung mit
  Aspose.Cells anwenden.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- excel conditional formatting python
- date based conditional formatting
language: de
lastmod: 2026-09-21
og_description: Erstellen Sie eine Excel‑Arbeitsmappe in Python, setzen Sie die Hintergrundfarbe
  einer Zelle und wenden Sie datumsbasierte bedingte Formatierung mit Aspose.Cells
  an. Folgen Sie der Schritt‑für‑Schritt‑Anleitung.
og_image_alt: Screenshot of an Excel sheet showing a yellow‑green cell background
  for yesterday's dates
og_title: Excel-Arbeitsmappe in Python mit bedingter Formatierung erstellen
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
title: Excel-Arbeitsmappe in Python mit bedingter Formatierung erstellen
url: /de/python/formatting/create-excel-workbook-in-python-using-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-Arbeitsmappe in Python mit bedingter Formatierung erstellen

Wenn Sie **Excel‑Arbeitsmappe Python**‑Skripte benötigen, die Daten automatisch hervorheben, zeigt Ihnen diese Anleitung genau, wie das geht. Sie sehen, wie Sie **Zellenhintergrundfarbe setzen**, eine „Gestern“-Regel hinzufügen und die Datei speichern – alles mit Aspose.Cells für Python.

Die programmgesteuerte Arbeit mit Excel‑Dateien bedeutet häufig, dieselbe Formatierungslogik über viele Tabellen hinweg zu wiederholen. Am Ende dieses Tutorials besitzen Sie ein wiederverwendbares Muster für **excel conditional formatting python**, das Sie in jedes Projekt einbinden können.

## Voraussetzungen

- Python 3.8+ installiert  
- `aspose-cells`‑Paket (`pip install aspose-cells`)  
- Grundkenntnisse in Python‑Funktionen und dem `datetime`‑Modul  

Weitere Bibliotheken sind nicht nötig; Aspose.Cells übernimmt alle Excel‑Operationen.

## Schritt 1: Arbeitsmappe erstellen und erstes Arbeitsblatt öffnen

Der erste Schritt besteht darin, **excel workbook python**‑Objekte zu **erstellen** und das Standard‑Arbeitsblatt zu holen. So haben Sie eine leere Leinwand für weitere Formatierungen.

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

*Warum das wichtig ist:* `Workbook()` erzeugt eine Excel‑Datei im Speicher. Der Zugriff auf `worksheets[0]` vermeidet das Hard‑Coden von Blattnamen und funktioniert auch, wenn der Standardname geändert wird.

## Schritt 2: Hilfsfunktion zum Hinzufügen einer TIME_PERIOD‑bedingten Formatierung

Um den Code übersichtlich zu halten, kapseln wir die Erstellung der bedingten Formatierung in einer Hilfsfunktion ein. Sie erhält einen Zellbereich, eine Hintergrundfarbe und die gewünschte Zeit‑Perioden‑Regel.

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

*Warum das wichtig ist:* Die Hilfsfunktion abstrahiert die wiederholenden Schritte zur Erstellung einer bedingten Formatierung und lässt sich leicht für weitere datumsbasierte Regeln wie „Heute“ oder „Letzte Woche“ wiederverwenden.

## Schritt 3: Die „Gestern“-Regel auf einen Bereich anwenden

Jetzt nutzen wir die Hilfsfunktion, um Zellen zu markieren, die das Datum von gestern enthalten. Der Bereich `I19:K20` wird **medium sea green** eingefärbt, wenn die Bedingung erfüllt ist.

```python
add_time_period(
    worksheet,
    "I19:K20",                # range to format
    Color.medium_sea_green,  # set cell background color
    TimePeriodType.YESTERDAY # date based conditional formatting
)
```

*Warum das wichtig ist:* `TimePeriodType.YESTERDAY` ist Teil der integrierten Aufzählung von Aspose.Cells, sodass Sie keine Datumsberechnungen selbst durchführen müssen. Die Bibliothek wertet die Regel bei jedem Öffnen der Arbeitsmappe aus.

## Schritt 4: Den Bereich mit Beispieldaten füllen

Um die Regel zu sehen, schreiben wir zwei Daten – eines, das „Gestern“ entspricht, und eines, das nicht entspricht. Der `number`‑Stil `30` entspricht einem integrierten Datumsformat.

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

*Warum das wichtig ist:* Durch das Einfügen konkreter Daten können Sie überprüfen, dass die bedingte Formatierung funktioniert, ohne die Datei an einem bestimmten Tag öffnen zu müssen.

## Schritt 5: Beschriftung hinzufügen und Spalte automatisch anpassen

Eine kurze Beschriftung erklärt den Zweck des formatierten Bereichs, und `auto_fit_column` sorgt für Lesbarkeit des Blatts.

```python
# Add a label under the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Adjust column width for better visibility (column 12 = L)
worksheet.auto_fit_column(12)
```

## Schritt 6: Arbeitsmappe speichern

Zum Schluss schreiben wir die Arbeitsmappe auf die Festplatte. Der Aufruf `os.makedirs` stellt sicher, dass das Zielverzeichnis existiert.

```python
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)

# Save as XLSX – the most widely supported Excel format
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Wenn Sie *TimePeriodDemo.xlsx* öffnen, sehen Sie:

- Zelle **I19** ist **medium sea green** gefärbt, weil ihr Wert der „Gestern“-Regel entspricht.  
- Zelle **K20** behält den Standard‑Hintergrund, weil ihr Datum die Bedingung nicht erfüllt.  

Damit wird **format cells by date** mit nur einer einzigen Python‑Zeile demonstriert.

## Vollständiges, ausführbares Beispiel

Alle Teile zusammengefügt, hier das komplette Skript zum Kopieren und Ausführen:

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

Führen Sie das Skript aus, öffnen Sie die resultierende Datei und Sie sehen die bedingte Formatierung in Aktion.

## Häufige Varianten und Sonderfälle

| Variation | Wie implementieren | Wann verwenden |
|-----------|--------------------|----------------|
| **„Heute“ hervorheben** | Ersetzen Sie `TimePeriodType.YESTERDAY` durch `TimePeriodType.TODAY` | Echtzeit‑Dashboards |
| **Mehrere Bereiche** | Rufen Sie `add_time_period` für jeden Bereich auf und übergeben Sie unterschiedliche Farben | Komplexe Berichte |
| **Dynamischer Datumsbereich** | Verwenden Sie `TimePeriodType.LAST_7_DAYS` oder `TimePeriodType.NEXT_MONTH` | Rollierende Berichte |
| **Benutzerdefinierte Farbe** | Nutzen Sie `Color.from_argb(255, r, g, b)`, um jede gewünschte Schattierung zu erzeugen | Marken‑konforme Gestaltung |

**Profi‑Tipp:** Setzen Sie immer `condition.style.pattern = BackgroundType.SOLID`, wenn Sie eine einheitliche Füllung wünschen; sonst kann Excel einen Farbverlauf anzeigen, der in verschiedenen Versionen inkonsistent wirkt.

## Fazit

Sie wissen jetzt, wie Sie **excel workbook python**‑Skripte schreiben, die **Zellenhintergrundfarbe setzen**, **excel conditional formatting python** anwenden und **format cells by date** mit Aspose.Cells umsetzen. Das Beispiel behandelt ein **date based conditional formatting**‑Szenario, aber dasselbe Muster funktioniert für jede Zeit‑Perioden‑Regel.

Als Nächstes könnten Sie erkunden:

- Hinzufügen von Datenbalken oder Symbolsets (`FormatConditionType.DATA_BAR`)  
- Kombinieren mehrerer bedingter Regeln für denselben Bereich  
- Export der Arbeitsmappe nach PDF (`SaveFormat.PDF`) für Berichte  

Experimentieren Sie gern mit verschiedenen Farben, Bereichen und Zeit‑Perioden‑Typen, um Ihre Berichtsanforderungen optimal zu erfüllen. Viel Spaß beim Programmieren!

## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren Projekten erkunden können.

- [Excel‑Zellformatierung und Arbeitsmappenverwaltung mit Aspose.Cells für .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Excel‑Automatisierung mit Aspose.Cells .NET: Arbeitsmappe erstellen & externe Links setzen](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Wie man arbeitsmappenbezogene benannte Bereiche in Excel mit Aspose.Cells .NET erstellt](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}