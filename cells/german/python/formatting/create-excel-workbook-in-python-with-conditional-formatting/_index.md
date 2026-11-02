---
category: general
date: 2026-09-05
description: Erstelle eine Excel‑Arbeitsmappe in Python und füge eine bedingte Formatierung
  hinzu, um die Zellen von gestern hervorzuheben. Lerne den vollständigen Code und
  warum jeder Schritt wichtig ist.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- add conditional formatting excel
- highlight cells based on date
- add conditional formatting range
- how to highlight yesterday cells
language: de
lastmod: 2026-09-05
og_description: Erstelle eine Excel‑Arbeitsmappe in Python und füge eine bedingte
  Formatierung hinzu, um die Zellen von gestern hervorzuheben. Befolge diese Schritt‑für‑Schritt‑Anleitung
  für eine vollständige Lösung.
og_image_alt: Screenshot of an Excel sheet where cells are highlighted after creating
  Excel workbook in Python
og_title: Excel‑Arbeitsmappe in Python erstellen – bedingte Formatierung hinzufügen
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
title: Excel‑Arbeitsmappe in Python mit bedingter Formatierung erstellen
url: /de/python/formatting/create-excel-workbook-in-python-with-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Erstellen einer Excel-Arbeitsmappe in Python mit bedingter Formatierung

Wenn Sie **create Excel workbook python** für eine Reporting‑Aufgabe benötigen, zeigt Ihnen dieser Leitfaden, wie Sie eine Arbeitsmappe erzeugen und eine Regel für bedingte Formatierung anwenden, die die Daten von gestern hervorhebt. Sie sehen den genauen Code, warum jede Zeile existiert, und wie Sie die Lösung für andere Datumsbereiche anpassen können.

Bedingte Formatierung ist eine leistungsstarke Methode, um Daten hervorzuheben, die einer bestimmten Bedingung entsprechen. In diesem Tutorial verwenden wir die Aspose.Cells‑Bibliothek für Python via .NET, die vollständige Excel‑Funktionalität bietet, ohne dass Microsoft Office erforderlich ist. Am Ende des Leitfadens haben Sie eine Datei, in der Zellen im Bereich *I19:K20* rosa werden, wenn sie das Datum von gestern enthalten.

## Voraussetzungen

* Python 3.9+ installiert
* `aspose-cells`‑Paket (installieren mit `pip install aspose-cells`)
* Grundlegende Kenntnisse der Python‑Syntax
* Schreibberechtigung für das Verzeichnis, in dem die Arbeitsmappe gespeichert wird

Der Code funktioniert unter Windows, macOS und Linux, solange die .NET‑Runtime verfügbar ist.

## Excel-Arbeitsmappe in Python erstellen

Der erste Schritt besteht darin, ein `Workbook`‑Objekt zu instanziieren und das Standard‑Arbeitsblatt zu holen. Dieses Objekt repräsentiert die gesamte Excel‑Datei im Speicher.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Warum das wichtig ist*: `Workbook()` erstellt eine leere Arbeitsmappe mit einem einzigen Arbeitsblatt. Der Zugriff auf `worksheets[0]` gibt Ihnen einen Handle, um später Daten, Stile und Formatierungen hinzuzufügen.

## Bereich für bedingte Formatierung hinzufügen

Als Nächstes definieren wir den Bereich, der von der bedingten Regel ausgewertet wird. Der Bereich `I19:K20` umfasst sechs Zellen über zwei Zeilen.

```python
# Define the range that will receive the conditional formatting rule
condition_collection = worksheet.conditional_formattings.add("I19:K20")
```

*Warum das wichtig ist*: Das Hinzufügen einer Sammlung für bedingte Formatierung zu einem bestimmten Bereich isoliert die Regel und verhindert, dass sie nicht verwandte Zellen beeinflusst. Dies erfüllt die Anforderung **add conditional formatting range**.

## Regel definieren: Zellen basierend auf Datum hervorheben

Jetzt erstellen wir eine Bedingung vom Typ `TIME_PERIOD`. Dies weist Excel an, den Wert jeder Zelle mit einem vordefinierten Zeitfenster zu vergleichen.

```python
from aspose.cells import FormatConditionType, TimePeriodType

# Add a TIME_PERIOD condition to the collection
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Set the time period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY
```

*Warum das wichtig ist*: `TIME_PERIOD` ist der einzige integrierte Typ, der direkt „Yesterday“, „Today“, „Last Week“ usw. unterstützt. Durch das Setzen von `condition.time_period` auf `YESTERDAY` bewertet die Regel automatisch den Datumswert jeder Zelle im Vergleich zum Tag vor dem aktuellen Datum.

## Stil für Zellen, die die Bedingung erfüllen, festlegen

Bedingte Formatierung benötigt zudem einen visuellen Stil. Hier wählen wir eine durchgehend rosa Füllung, um die passenden Zellen hervorzuheben.

```python
from aspose.pydrawing import Color as DrawingColor
from aspose.cells import BackgroundType

# Apply a pink solid background to cells that satisfy the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID
```

*Warum das wichtig ist*: Das Stil‑Objekt definiert, wie Excel Zellen rendert, die die Bedingung erfüllen. Die Verwendung einer durchgehend rosa Füllung erfüllt die Anforderung **highlight cells based on date** und macht das Ergebnis leicht überprüfbar.

## Beispiel-Daten zum Auswerten einfügen

Um die Regel in Aktion zu sehen, fügen wir zwei Datumswerte ein – einen, der dem gestrigen Datum entspricht, und einen, der das nicht tut. Das `number`‑Format `30` entspricht dem integrierten Datumsformat `mm-dd-yy`.

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

*Warum das wichtig ist*: Das Bereitstellen sowohl eines passenden als auch eines nicht passenden Datums ermöglicht es Ihnen zu überprüfen, dass die bedingte Formatierung korrekt funktioniert. Passen Sie die Daten beim Ausführen des Skripts an den aktuellen Monat an oder ersetzen Sie sie durch dynamische Werte.

## Arbeitsmappe speichern

Abschließend schreiben wir die Datei auf die Festplatte. Die Konstante `SaveFormat.XLSX` stellt sicher, dass die Ausgabe eine moderne Excel‑Datei ist.

```python
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

*Warum das wichtig ist*: Das Persistieren der Arbeitsmappe ermöglicht es Ihnen, sie in Excel, LibreOffice oder einem anderen Viewer, der XLSX unterstützt, zu öffnen. Der ausgegebene Pfad bestätigt, wo die Datei geschrieben wurde.

## Vollständiges Skript

Wenn man alle Teile zusammenfügt, sieht das vollständige, ausführbare Skript folgendermaßen aus:

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

### Erwartete Ausgabe

Wenn Sie `TimePeriodExample.xlsx` öffnen:

* Zelle **I19** erscheint mit einem rosa Hintergrund, weil ihr Wert gestern entspricht.
* Zelle **K20** behält den Standard‑Hintergrund bei, weil ihr Datum außerhalb des Zeitraums liegt.
* Das Label **„Yesterday“** steht in Zelle I20 zur Klarstellung.

## Häufige Variationen und Randfälle

| Situation | Anpassung |
|-----------|------------|
| **Heute statt gestern hervorheben** | Ändern Sie `condition.time_period = TimePeriodType.TODAY`. |
| **Regel auf einen größeren Bereich anwenden** | Aktualisieren Sie den Bereichs‑String in `add(\"I19:K20\")` zu etwas wie `\"A1:Z100\"`. |
| **Andere Füllfarbe verwenden** | Ersetzen Sie `DrawingColor.pink` durch ein anderes `DrawingColor` (z. B. `DrawingColor.light_green`). |
| **Mit dynamischen Daten arbeiten** | Berechnen Sie `datetime.now() - timedelta(days=1)` für gestern und schreiben Sie diesen Wert in die Zellen, bevor Sie die Regel anwenden. |

**Pro‑Tipp:** Wenn Sie die Arbeitsmappe programmgesteuert für viele Benutzer erzeugen, halten Sie die Definition der bedingten Formatierung getrennt von der Dateneinfügung. So können Sie denselben Stil über mehrere Tabellen hinweg wiederverwenden, ohne Code zu duplizieren.

## Ergebnis programmgesteuert überprüfen (optional)

Wenn Sie die Formatierung bestätigen möchten, ohne Excel zu öffnen, können Sie nach dem Speichern den Stil einer Zelle inspizieren:



## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Excel Automation&#58; Arbeitsmappe erstellen und ListBox mit Aspose.Cells für .NET hinzufügen](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Excel‑Arbeitsmappe erstellen und Beschriftungen mit Aspose.Cells für Java hinzufügen](/cells/english/java/advanced-excel-charts/data-labeling/)
- [Excel Automation Arbeitsmappe erstellen und ListBox Aspose Cells hinzufügen](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}