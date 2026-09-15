---
category: general
date: 2026-09-15
description: Erfahren Sie, wie Sie die bedingte Formatierung für Zeiträume anwenden
  und die Arbeitsmappe mit Aspose.Cells in Python als XLSX speichern. Enthält Schritt‑für‑Schritt‑Code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- time period conditional formatting
- save workbook as xlsx
- how to create excel workbook python
- how to highlight yesterday in excel
- add conditional formatting python
language: de
lastmod: 2026-09-15
og_description: Wenden Sie die bedingte Formatierung für Zeiträume in Excel mit Python
  an und speichern Sie die Arbeitsmappe als XLSX. Folgen Sie diesem vollständigen
  Leitfaden für Aspose.Cells.
og_image_alt: Screenshot of an Excel sheet where the cells for yesterday are highlighted
  in pink
og_title: Bedingte Formatierung nach Zeiträumen in Excel mit Python anwenden
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  headline: How to apply time period conditional formatting in Excel using Python
  type: TechArticle
- description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  name: How to apply time period conditional formatting in Excel using Python
  steps:
  - name: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
    text: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
  - name: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
    text: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
  - name: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
    text: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
  - name: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
    text: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
  - name: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
    text: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
  - name: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
    text: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
  - name: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
    text: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
  - name: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
    text: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
  - name: The cell `I20` shows the text “Yesterday”.
    text: The cell `I20` shows the text “Yesterday”.
  - name: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
    text: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Wie man in Excel mit Python bedingte Formatierung für Zeiträume anwendet
url: /de/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Zeitperioden‑Bedingte Formatierung in Excel mit Python anwendet

Wenn Sie **time period conditional formatting** in einer Excel‑Datei benötigen, zeigt Ihnen dieses Tutorial genau, wie Sie es mit Python umsetzen. Sie sehen ein vollständiges, ausführbares Beispiel, das eine Arbeitsmappe erstellt, die Daten von gestern hervorhebt und **save workbook as XLSX** in nur wenigen Codezeilen.

Bedingte Formatierung ist eine leistungsstarke Methode, um Daten, die einer bestimmten Regel entsprechen, hervorzuheben. In diesem Leitfaden konzentrieren wir uns auf die Zeitperiode „Yesterday“, aber das gleiche Muster funktioniert für andere integrierte Perioden wie Today, LastWeek und NextMonth. Am Ende des Tutorials werden Sie in der Lage sein, **how to create excel workbook python**‑style‑Skripte zu erstellen, die produktionsreif sind.

## Voraussetzungen

- Python 3.8+ installiert  
- `aspose-cells` und `aspose-pydrawing` Pakete (`pip install aspose-cells aspose-pydrawing`)  
- Grundlegende Vertrautheit mit Python‑Syntax  

Keine zusätzliche Office‑Installation ist erforderlich, da Aspose.Cells die Dateigenerierung intern übernimmt.

## Zeitperioden‑Bedingte Formatierung mit Aspose.Cells in Python

Dieser Abschnitt führt Sie durch jede Codezeile, die für die Hauptaufgabe erforderlich ist. Der untenstehende Codeblock enthält das vollständige Skript; Kommentare erklären den Zweck jedes Schrittes.

```python
# -*- coding: utf-8 -*-
"""
Apply time period conditional formatting to highlight yesterday's dates
and save the workbook as XLSX using Aspose.Cells for Python.
"""

from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the range that will receive the conditional formatting rule
cell_range = "I19:K20"
cond_format = worksheet.conditional_formattings.add(cell_range)

# Step 3: Add a TIME_PERIOD condition for “Yesterday” and style it
condition_index = cond_format.add_condition(FormatConditionType.TIME_PERIOD)
condition = cond_format[condition_index]
condition.style.background_color = Color.pink          # Highlight colour
condition.style.pattern = BackgroundType.SOLID        # Solid fill
condition.time_period = TimePeriodType.YESTERDAY      # Built‑in “Yesterday” period

# Step 4: Populate the range with sample dates (Excel number format 30 = short date)
date_cells = ["I19", "K20"]                           # Cells that will contain dates
sample_dates = [datetime(2008, 7, 30), datetime(2008, 8, 3)]
for cell_ref, date_val in zip(date_cells, sample_dates):
    cell = worksheet.cells.get(cell_ref)
    cell.put_value(date_val)                         # Write the Python datetime
    style = cell.get_style()
    style.number = 30                                 # Excel short date format
    cell.set_style(style)

# Step 5: Add a label so the user knows what the rule represents
worksheet.cells.get("I20").put_value("Yesterday")

# Step 6: Auto‑fit the column for better readability (column L is index 12)
worksheet.auto_fit_column(12)

# Step 7: Save the workbook – this demonstrates “save workbook as xlsx”
output_path = "TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

### Warum jeder Schritt wichtig ist

1. **Creating the workbook** liefert Ihnen eine Excel‑Datei im Speicher, die Sie manipulieren können, ohne Excel zu öffnen.  
2. **Defining the range** (`I19:K20`) teilt Aspose.Cells mit, wo die Regel gilt, und hält die Logik isoliert.  
3. **Adding a TIME_PERIOD condition** verwendet Asposes integrierte Aufzählung `TimePeriodType.YESTERDAY`. Dadurch entfallen manuelle Datumsberechnungen und die Regel wird automatisch aktualisiert, wenn die Datei an einem anderen Tag geöffnet wird.  
4. **Setting the style** (`background_color` und `pattern`) bestimmt, wie die hervorgehobenen Zellen aussehen. Die Verwendung von `Color.pink` macht die Regel leicht erkennbar.  
5. **Writing sample dates** mit Zahlenformat 30 stellt sicher, dass Excel sie als Kurzdatumsformat und nicht als Seriennummer anzeigt.  
6. **Auto‑fitting the column** verbessert die Lesbarkeit für jeden, der die Datei später öffnet.  
7. **Saving as XLSX** erzeugt eine weit verbreitete kompatible Datei, die in Excel, Google Sheets oder jedem modernen Tabellenkalkulationsprogramm geöffnet werden kann.

## Wie man Excel‑Arbeitsmappe Python‑style mit Aspose.Cells erstellt

Das obige Skript demonstriert bereits die minimalen Schritte, um **how to create excel workbook python**. In der Praxis möchten Sie vielleicht:

- Mehrere Arbeitsblätter hinzufügen (`workbook.worksheets.add("Report")`).  
- Große Datentabellen mit Schleifen oder pandas DataFrames füllen (`worksheet.cells.import_data_table`).  
- Zusätzliche Formatierungen (Schriftarten, Rahmen) mit `cell.get_style()` anwenden.

All diese Aktionen folgen demselben Muster: Das Objekt abrufen, seine Eigenschaften ändern und `set_style` oder `save` aufrufen.

## Bedingte Formatierung mit Python hinzufügen – weitere nützliche Muster

Über das „Yesterday“-Beispiel hinaus unterstützt Aspose.Cells mehrere Arten von bedingter Formatierung:

| FormatConditionType | Typischer Anwendungsfall |
|---------------------|--------------------------|
| `FORMAT_CONDITION_TYPE_EXPRESSION` | Benutzerdefinierte Formeln (`=A1>100`) |
| `FORMAT_CONDITION_TYPE_CELL_VALUE` | Einfache Vergleiche (`>`, `<`, `=`) |
| `FORMAT_CONDITION_TYPE_COLOR_SCALE` | Verlaufende Farbschalen |
| `FORMAT_CONDITION_TYPE_DATA_BAR`   | Balkenvisualisierung in Zelle |

Um **add conditional formatting python** für einen numerischen Schwellenwert hinzuzufügen, würden Sie `FormatConditionType.TIME_PERIOD` durch `FormatConditionType.CELL_VALUE` ersetzen und `condition.operator_type` sowie `condition.formula1` setzen.

```python
# Example: highlight values greater than 500
idx = cond_format.add_condition(FormatConditionType.CELL_VALUE)
cond = cond_format[idx]
cond.operator_type = ConditionOperatorType.GREATER_THAN
cond.formula1 = "500"
cond.style.background_color = Color.light_green
```

## Arbeitsmappe als XLSX speichern – bewährte Methoden

Wenn Sie **save workbook as xlsx** ausführen, sollten Sie Folgendes beachten:

- **Specifying the correct `SaveFormat`** (`SaveFormat.XLSX`) um veraltete Formate zu vermeiden.  
- **Using a deterministic file name** falls das Skript in einer Schleife läuft (`f"report_{datetime.now():%Y%m%d}.xlsx"`).  
- **Closing resources** (`workbook.dispose()`) in langlaufenden Diensten, um nativen Speicher freizugeben.  

Das Beispiel verwendet bereits `SaveFormat.XLSX`, das eine moderne, zip‑basierte Arbeitsmappe erzeugt, die alle Regeln der bedingten Formatierung beibehält.

## Gestern in Excel hervorheben – Verifizierungsschritte

Nach dem Ausführen des Skripts öffnen Sie `TimePeriodExample.xlsx`:

1. Die Zellen `I19` und `K20` enthalten die Daten `30‑07‑2008` und `03‑08‑2008`.  
2. Die Zelle `I20` zeigt den Text „Yesterday“.  
3. Wenn Sie Ihr Systemdatum auf **July 30 2008** ändern und die Datei erneut öffnen, werden die Zellen mit passenden Daten automatisch rosa gefüllt.  
4. Ändern Sie das Systemdatum auf einen anderen Tag, wird die rosa Füllung entfernt, was bestätigt, dass die Regel auf die **time period conditional formatting**‑Logik reagiert.

## Häufige Fallstricke und wie man sie vermeidet

- **Missing `aspose-pydrawing`** – die `Color`‑Klasse befindet sich in diesem Paket; das Vergessen der Installation führt zu einem `ImportError`.  
- **Incorrect number format** – die Verwendung des Standard‑General‑Formats zeigt Seriennummern (z. B. 39822). Setzen Sie immer `style.number = 30` für Kurzdatumsformate.  
- **Range mismatch** – der Bereich der bedingten Formatierung muss die Zellen, die Sie hervorheben möchten, einschließen; andernfalls hat die Regel keine Wirkung.

## Profi‑Tipp: Wiederverwendung der Formatierungsroutine

Wenn Sie dieselbe „Yesterday“-Regel in mehreren Arbeitsmappen benötigen, verpacken Sie die Logik in eine Hilfsfunktion:

```python
def apply_yesterday_highlight(worksheet, address):
    cf = worksheet.conditional_formattings.add(address)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    cond = cf[idx]
    cond.style.background_color = Color.pink
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

Rufen Sie `apply_yesterday_highlight(worksheet, "A1:A10")` überall dort auf, wo es benötigt wird.

## Fazit

Dieser Leitfaden zeigte Ihnen, wie Sie **time period conditional formatting** in Excel mit Python implementieren, wie Sie **save workbook as XLSX** ausführen und wie Sie **highlight yesterday in Excel** mit einem einzigen, wiederverwendbaren Skript hervorheben. Sie haben nun eine solide Grundlage, um **add conditional formatting python**‑Code zu jedem Automatisierungsprojekt hinzuzufügen, egal ob Sie tägliche Berichte erstellen, Dashboards bauen oder Datenexporte vorbereiten.

**Nächste Schritte**

- Weitere `TimePeriodType`‑Werte wie `TODAY` oder `LAST_WEEK` erkunden.  
- Mehrere bedingte Regeln im selben Bereich kombinieren, um reichhaltigere visuelle Hinweise zu erhalten.  
- Die Generierung der Arbeitsmappe in einen Webservice oder einen geplanten Job integrieren.

Viel Spaß beim Programmieren und genießen Sie die visuelle Klarheit, die bedingte Formatierung Ihrer Excel‑Automatisierung verleiht!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Meistern der bedingten Formatierung in Excel mit Aspose.Cells .NET : Ein umfassender Leitfaden](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Meistern von Aspose.Cells .NET : Bedingte Formatierung auf alternierende Zeilen in Excel anwenden](/cells/english/net/formatting/aspose-cells-net-conditional-formatting-alternate-rows/)
- [Meistern der bedingten Formatierung mit benutzerdefinierten Schriftarten in Excel mithilfe von Aspose.Cells für .NET und C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}