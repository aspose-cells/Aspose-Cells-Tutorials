---
category: general
date: 2026-08-08
description: Erstelle ein Excel‑Arbeitsbuch mit Python und füge eine bedingte Formatierung
  basierend auf dem Datum hinzu. Schritt‑für‑Schritt‑Anleitung mit Aspose.Cells, um
  die Zellen von gestern hervorzuheben.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- conditional formatting based on date
- Aspose.Cells Python example
- Excel date formatting Python
- Python Excel automation
language: de
lastmod: 2026-08-08
og_description: Erstellen Sie eine Excel-Arbeitsmappe in Python mit Aspose.Cells und
  wenden Sie eine datumsbasierte bedingte Formatierung für dynamische Tabellenkalkulationen
  an.
og_image_alt: Screenshot of an Excel sheet created with Python showing cells highlighted
  by date conditional formatting
og_title: Excel-Arbeitsmappe mit Python erstellen – bedingte Formatierung für Datum
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Create Excel workbook Python and add conditional formatting based on
    date. Step‑by‑step guide using Aspose.Cells to highlight yesterday’s cells.
  headline: Create Excel workbook Python date conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: 'Excel-Arbeitsmappe mit Python erstellen: Bedingte Formatierung für Datum'
url: /de/python/formatting/create-excel-workbook-python-date-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-Arbeitsmappe mit Python erstellen – Datumsbasierte bedingte Formatierung

Wenn Sie **Excel-Arbeitsmappe mit Python erstellen** und automatisch Zellen hervorheben möchten, die einem bestimmten Datum entsprechen, zeigt Ihnen dieses Tutorial genau, wie es geht. Sie lernen, **bedingte Formatierung basierend auf Datum** anzuwenden, sodass die Daten von gestern in Rosa leuchten, mit der Aspose.Cells-Bibliothek.

Der Leitfaden führt Sie durch jeden Schritt – von der Installation des SDK bis zum Speichern der finalen .xlsx‑Datei – sodass Sie ein funktionierendes Beispiel in Ihr eigenes Projekt kopieren‑und‑einfügen können. Keine externe Dokumentation ist erforderlich; sämtlicher Code und alle Erklärungen sind in sich abgeschlossen.

## Voraussetzungen

* Python 3.8 oder neuer installiert.
* `aspose-cells`‑Paket (der Python‑Wrapper für Aspose.Cells). Installieren Sie es mit:
  ```bash
  pip install aspose-cells
  ```
* Grundlegende Kenntnisse in Python und Excel‑Konzepten wie Arbeitsblättern und Zellformaten.

> **Pro Tipp:** Aspose.Cells funktioniert, ohne dass Microsoft Excel installiert sein muss, und ist damit ideal für serverseitige Automatisierung.

## Schritt 1: Excel-Arbeitsmappe in Python erstellen

Die erste Aufgabe besteht darin, ein neues Workbook zu instanziieren und das Standard‑Arbeitsblatt zu holen. Dieses Objekt repräsentiert die gesamte Excel‑Datei und bietet Zugriff auf Zeilen, Spalten und Formatierungs‑APIs.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook – this automatically adds one worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]   # reference to the first (default) sheet
```

Das Erstellen des Workbooks ist die Grundlage für jede weitere Manipulation, egal ob Sie Daten, Formeln oder Formatierungsregeln hinzufügen.

## Schritt 2: Datumsbasierte bedingte Formatierung definieren

Jetzt fügen wir **bedingte Formatierung basierend auf Datum** hinzu. Das Enum `FormatConditionType.TIME_PERIOD` ermöglicht es, vordefinierte Zeiträume wie Yesterday, Today oder LastWeek anzugeben.

```python
from aspose.cells import FormatConditionType, BackgroundType, TimePeriodType
from aspose.pydrawing import Color

# Target range I19:K20 – three columns by two rows
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions

# Add a new time‑period condition (e.g., Yesterday)
condition_index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[condition_index]

# Set the visual style: pink solid background
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Specify that the condition should trigger for "Yesterday"
condition.time_period = TimePeriodType.YESTERDAY
```

Warum dieser Schritt wichtig ist: Excel bewertet die Bedingung für jede Zelle im Bereich. Wenn der Wert einer Zelle innerhalb des definierten Zeitraums (gestern) liegt, wird der zugewiesene Stil automatisch angewendet.

## Schritt 3: Bereich mit Beispieldaten füllen

Um die Regel in Aktion zu sehen, schreiben wir ein paar `datetime`‑Objekte in die Zielzellen. Einer davon ist bewusst auf das gestrige Datum relativ zum internen Datumsystem des Workbooks gesetzt.

```python
from datetime import datetime

# Cell I19 – yesterday’s date (will be highlighted)
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # This date matches the "Yesterday" rule
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel’s built‑in date format
cell_i19.set_style(style_i19)

# Cell K20 – a random later date (no highlight)
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Not yesterday, so no formatting
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

Die Zeile `number = 30` weist Excel an, den Wert im standardmäßigen Kurzdatumsformat anzuzeigen. Sie können diesen Index zu jedem integrierten Zahlenformat ändern, wenn Sie eine andere Darstellung bevorzugen.

## Schritt 4: Spaltenbreite für bessere Lesbarkeit anpassen

Das automatische Anpassen der Spalte, die die Daten enthält, macht die Ausgabe leichter lesbar, besonders wenn das Workbook in Excel oder einem Viewer geöffnet wird.

```python
# Column 12 corresponds to column L (zero‑based indexing)
worksheet.auto_fit_column(12)
```

## Schritt 5: Workbook auf Festplatte speichern

Speichern Sie schließlich das Workbook als .xlsx‑Datei. Ersetzen Sie `"YOUR_DIRECTORY"` durch einen echten Pfad auf Ihrem Rechner.

```python
import os

output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Wenn Sie `TimePeriodDemo.out.xlsx` in Excel öffnen, wird die Zelle **I19** mit einem rosa Hintergrund angezeigt, weil ihr Wert der „Yesterday“-Regel entspricht, während **K20** unverändert bleibt.

### Erwartete Ausgabe

| I19 (Datum) | I20 (Bezeichnung) | J19 | J20 | K19 | K20 (Datum) |
|------------|-------------------|-----|-----|-----|------------|
| *2008‑07‑30* (rosa Hintergrund) | Gestern | – | – | – | *2008‑08‑03* (keine Formatierung) |

Die rosa Schattierung bestätigt, dass **bedingte Formatierung basierend auf Datum** wie beabsichtigt funktioniert.

## Häufige Variationen und Sonderfälle

| Situation | How to adapt the code |
|-----------|-----------------------|
| **Highlight “Today” instead of “Yesterday”** | Change `condition.time_period = TimePeriodType.TODAY` |
| **Apply the rule to an entire column** | Use `worksheet.get_range("A:A").format_conditions` |
| **Use a custom date range (e.g., last 7 days)** | Replace the time‑period condition with a formula condition: <br>```python<br>condition = conditions.add_condition(FormatConditionType.FORMULA)<br>condition.formula1 = 'AND(A1>=TODAY()-7, A1<=TODAY())'<br>``` |
| **Different background colors** | Set `condition.style.background_color = Color.light_green` (or any `Color` you prefer) |
| **Running on Linux without a display** | Aspose.Cells is fully headless; no extra configuration required. |

## Vollständiges, ausführbares Beispiel

Unten finden Sie das vollständige Skript, das Sie unverändert ausführen können (nachdem Sie das Ausgabeverzeichnis aktualisiert haben). Alle Importe, Kommentare und grundlegenden Fehlerbehandlungen sind enthalten.

```python
# -*- coding: utf-8 -*-
"""
Create Excel workbook Python with date conditional formatting.
Demonstrates how to highlight yesterday’s dates using Aspose.Cells.
"""

import os
from datetime import datetime
from aspose.cells import (
    Workbook, SaveFormat,
    FormatConditionType, BackgroundType,
    TimePeriodType
)
from aspose.pydrawing import Color

# ----------------------------------------------------------------------
# 1️⃣ Initialize workbook
# ----------------------------------------------------------------------
workbook = Workbook()
worksheet = workbook.worksheets[0]

# ----------------------------------------------------------------------
# 2️⃣ Add conditional formatting for "Yesterday"
# ----------------------------------------------------------------------
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions
cond_idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[cond_idx]

# Visual style: pink solid fill
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
condition.time_period = TimePeriodType.YESTERDAY

# ----------------------------------------------------------------------
# 3️⃣ Populate sample dates
# ----------------------------------------------------------------------
# Cell that should match the condition
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Yesterday relative to demo data
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel short‑date format
cell_i19.set_style(style_i19)

# Cell that does NOT match
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label
worksheet.cells.get("I20").put_value("Yesterday")

# ----------------------------------------------------------------------
# 4️⃣ Auto‑fit column for better visibility
# ----------------------------------------------------------------------
worksheet.auto_fit_column(12)   # Column L (0‑based index)

# ----------------------------------------------------------------------
# 5️⃣ Save workbook
# ----------------------------------------------------------------------
output_dir = "YOUR_DIRECTORY"   # <-- replace with a real folder
os.makedirs(output_dir, exist_ok=True)
output_path = os.path.join(output_dir, "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Das Ausführen des Skripts erzeugt eine Excel‑Datei, in der die „Gestern“-Zelle automatisch hervorgehoben wird, was **Excel-Arbeitsmappe mit Python erstellen** kombiniert mit **bedingter Formatierung basierend auf Datum** demonstriert.

## Fazit

Sie wissen jetzt, wie man **Excel-Arbeitsmappe mit Python erstellen** Objekte erzeugt, eine **datumsbasierte bedingte Formatierung** definiert

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Excel-Arbeitsmappe mit Aspose.Cells in Java erstellen: Eine Schritt‑für‑Schritt‑Anleitung](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Excel-Arbeitsmappe mit Diagrammen mithilfe von Aspose.Cells .NET \| Schritt‑für‑Schritt‑Anleitung](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)
- [Excel‑Automatisierung: Arbeitsmappe erstellen und ListBox hinzufügen mit Aspose.Cells für .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}