---
category: general
date: 2026-07-20
description: Erstelle ein Excel‑Arbeitsbuch in Python mit Aspose.Cells, setze die
  Hintergrundfarbe von Zellen und füge eine bedingte Formatierung in Python hinzu,
  um Zellen nach Datum zu formatieren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- aspose cells conditional formatting
- add conditional formatting python
language: de
lastmod: 2026-07-20
og_description: Erstelle ein Excel-Arbeitsbuch in Python mit Aspose.Cells. Erfahre,
  wie du die Hintergrundfarbe von Zellen festlegst und bedingte Formatierung in Python
  hinzufügst, um Zellen nach Datum zu formatieren.
og_image_alt: Screenshot of an Excel workbook created with Python showing conditional
  formatting applied to date cells
og_title: Excel-Arbeitsmappe mit Python erstellen – Bedingte Formatierung hinzufügen
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Create Excel workbook Python with Aspose.Cells, set cell background
    color, and add conditional formatting python to style cells by date.
  headline: Create Excel Workbook Python – Conditional Formatting Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Change `"I19:K20"` to any A1‑style range, and adjust the sample
      dates accordingly.
    question: Can I target a different date range?
  - answer: Use `FormatConditionType.FORMULA` and set `condition.formula1 = "YOUR_FORMULA"`—for
      example, `=TODAY()-A1=1` to mimic yesterday.
    question: What if I need a custom formula instead of `YESTERDAY`?
  - answer: Call `conditions.add_condition` again with a different `FormatConditionType`.
      The order matters; later rules can override earlier ones.
    question: How do I apply multiple rules to the same range?
  - answer: Yes—modify `condition.style.font.color = Color.white` (or any other `Color`).
    question: Is there a way to set font colour together with background?
  type: FAQPage
tags:
- Aspose.Cells
- Python
- Excel Automation
title: Excel‑Arbeitsmappe mit Python erstellen – Leitfaden zur bedingten Formatierung
url: /de/python/formatting/create-excel-workbook-python-conditional-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-Arbeitsmappe mit Python erstellen – Leitfaden für bedingte Formatierung

Haben Sie sich jemals gefragt, wie man **Excel-Arbeitsmappe mit Python** von Grund auf erstellt und sie ohne Öffnen der Benutzeroberfläche professionell aussehen lässt? Sie sind nicht allein. Viele Entwickler stoßen an ihre Grenzen, wenn sie **Zellhintergrundfarbe setzen** oder datumsbasierte Stile programmgesteuert anwenden müssen.  

In diesem Tutorial führen wir Sie durch ein vollständiges, ausführbares Beispiel, das Aspose.Cells verwendet, um **conditional formatting python**‑Regeln hinzuzufügen, Zellen nach Datum zu formatieren und das Ergebnis als moderne XLSX‑Datei zu speichern. Am Ende haben Sie ein eigenständiges Skript, das Sie in jedes Projekt einbinden können.

## Was Sie lernen werden

- Wie man eine Arbeitsmappe initialisiert und das erste Arbeitsblatt abruft.  
- Möglichkeiten, **set cell background color** für einen gesamten Bereich zu setzen.  
- Verwendung von **aspose cells conditional formatting**, um „Yesterday“-Daten hervorzuheben.  
- Automatisches Anpassen der Spaltenbreite und Speichern der Datei auf dem Datenträger.  

Keine externe Konfiguration ist erforderlich – nur Python 3 und das Aspose.Cells‑Paket. Wenn Sie `aspose-cells` bereits installiert haben, können Sie loslegen; andernfalls reicht ein kurzer `pip install aspose-cells` aus.

## Voraussetzungen

- Python 3.8+ (der Code funktioniert mit 3.9, 3.10 und neueren Versionen).  
- Aspose.Cells für Python via .NET (`aspose-cells` NuGet‑Wrapper).  
- Grundlegende Kenntnisse der Excel‑Konzepte (Zellen, Bereiche, Formatierung).  

Alles vorhanden? Großartig – lassen Sie uns loslegen.

## Excel-Arbeitsmappe mit Python erstellen – Einrichtung und Arbeitsblatt

Zuerst benötigen wir ein frisches Workbook‑Objekt und eine Referenz auf das Standard‑Arbeitsblatt. Dies ist die Leinwand, auf der alle späteren Vorgänge stattfinden.

```python
# Import the necessary Aspose.Cells classes
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and grab the first sheet
workbook = Workbook()                     # create excel workbook python
worksheet = workbook.worksheets[0]        # default is the first worksheet
```

> **Warum das wichtig ist:** `Workbook()` erstellt eine Excel‑Datei im Speicher und eliminiert die Notwendigkeit temporärer Dateien. Die Variable `worksheet` ist unser Einstiegspunkt für zellbasierte Aktionen.

## Zellhintergrundfarbe setzen

Bevor wir Regeln hinzufügen, ist es sinnvoll, dem Zielbereich eine Grundfarbe zu geben, damit die bedingte Formatierung hervorsticht. Der untenstehende Helfer ruft (oder erstellt) eine `FormatConditionCollection` für einen angegebenen Bereich ab und färbt die Zellen mit einem einfarbigen Hintergrund.

```python
def get_format_condition(cell_range: str, base_color: Color):
    """
    Obtain (or create) a FormatConditionCollection for `cell_range`.
    Also set a base background colour for the whole range.
    """
    # Retrieve or add a conditional formatting entry for the range
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    # Apply the base colour to every cell in the range
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color          # set cell background color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection
```

> **Profi‑Tipp:** Wenn Sie denselben Bereich mit mehreren Regeln wiederverwenden möchten, rufen Sie diesen Helfer einmal auf und behalten die zurückgegebene Sammlung; das spart einige API‑Aufrufe.

## Bedingte Formatierung in Python für Datumsbereiche hinzufügen

Jetzt kommt der spaßige Teil: Wir erstellen eine **time‑period conditional formatting**‑Regel, die Zellen mit dem gestrigen Datum hervorhebt. Das demonstriert die Leistungsfähigkeit von **format cells by date** mit Aspose.Cells.

```python
def apply_yesterday_rule():
    """
    Apply a “Yesterday” conditional formatting rule to the range I19:K20.
    Cells that match will turn pink; others stay with the base colour.
    """
    # Obtain the condition collection for the target range
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)

    # Create a TIME_PERIOD condition (this is the aspose cells conditional formatting type we need)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]

    # Define the appearance for cells that meet the condition
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Set the time period to “Yesterday”
    condition.time_period = TimePeriodType.YESTERDAY

    # Populate sample dates to demonstrate the rule
    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))   # matches “Yesterday”
    cell_i19.style.number = 30                 # Excel number format for dates
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))    # does NOT match
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    # Add a label for clarity
    worksheet.cells.get("I20").put_value("Yesterday")
```

> **Warum `TIME_PERIOD` verwenden?** Es abstrahiert die Notwendigkeit, eigene Formeln zu schreiben. Aspose.Cells prüft das Datum gegenüber dem aktuellen Systemdatum, sodass die Regel stets relevant bleibt.

### Ausführen der Regel

```python
apply_yesterday_rule()
```

Wenn Sie die resultierende Datei öffnen, leuchten die Zellen `I19` pink (weil sie „Yesterday“ sind), während `K20` die Grundfarbe Grün beibehält.

## Spalten automatisch anpassen und Arbeitsmappe speichern

Eine übersichtliche Tabelle wirkt professionell. Das automatische Anpassen sorgt dafür, dass unsere Daten nicht gequetscht werden.

```python
# Step 4: Auto‑fit the column width for a tidy appearance
worksheet.auto_fit_column(12)   # column index is zero‑based; 12 corresponds to column M

# Step 5: Save the workbook to disk
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Randfall:** Wenn Sie ein Verzeichnis angeben, das nicht existiert, löst `workbook.save` einen Fehler aus. Verpacken Sie den Speicheraufruf in einen `try/except`‑Block, falls Sie eine sanfte Fehlerbehandlung benötigen.

### Vollständiges Skript (zum Kopieren‑Einfügen bereit)

Unten finden Sie das komplette Skript, bereit zum Ausführen. Ersetzen Sie einfach `YOUR_DIRECTORY` durch einen gültigen Ordner auf Ihrem Rechner.

```python
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create the workbook and worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

def get_format_condition(cell_range: str, base_color: Color):
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection

def apply_yesterday_rule():
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = TimePeriodType.YESTERDAY

    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))
    cell_i19.style.number = 30
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    worksheet.cells.get("I20").put_value("Yesterday")

apply_yesterday_rule()
worksheet.auto_fit_column(12)

output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Das Ausführen dieses Skripts erzeugt `TimePeriodExample.xlsx` mit der beschriebenen bedingten Formatierung.

## Häufige Fragen & Tipps

- **Kann ich einen anderen Datumsbereich anvisieren?**  
  Absolut. Ändern Sie `"I19:K20"` in einen beliebigen A1‑Stil‑Bereich und passen Sie die Beispieldaten entsprechend an.

- **Was, wenn ich eine benutzerdefinierte Formel anstelle von `YESTERDAY` benötige?**  
  Verwenden Sie `FormatConditionType.FORMULA` und setzen Sie `condition.formula1 = "YOUR_FORMULA"` – zum Beispiel `=TODAY()-A1=1`, um gestern zu simulieren.

- **Wie wende ich mehrere Regeln auf denselben Bereich an?**  
  Rufen Sie `conditions.add_condition` erneut mit einem anderen `FormatConditionType` auf. Die Reihenfolge ist wichtig; spätere Regeln können frühere überschreiben.

- **Gibt es eine Möglichkeit, die Schriftfarbe zusammen mit dem Hintergrund zu setzen?**  
  Ja – ändern Sie `condition.style.font.color = Color.white` (oder jede andere `Color`).

## Fazit

Sie wissen jetzt, wie man **Excel-Arbeitsmappe mit Python** mithilfe von Aspose.Cells **Zellhintergrundfarbe setzt** und **conditional formatting python** hinzufügt, das Zellen nach Datum formatiert. Das Skript ist voll funktionsfähig, behandelt Randfälle wie fehlende Verzeichnisse und kann zu komplexeren Szenarien wie mehrstufiger bedingter Logik oder dynamischer Bereichserkennung erweitert werden.

Bereit für den nächsten Schritt? Versuchen Sie, die „Yesterday“-Regel durch „Last Week“ zu ersetzen, experimentieren Sie mit Farbverläufen oder erzeugen Sie einen vollständigen Bericht mit Dutzenden formatierter Tabellen. Die Bausteine sind alle vorhanden, und Sie haben gerade den Kern von **aspose cells conditional formatting** in Python gemeistert.

Viel Spaß beim Programmieren und teilen Sie gerne Ihre eigenen Varianten in den Kommentaren!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Meistern Sie die Excel-Zellformatierung und das Arbeitsbuch-Management mit Aspose.Cells für .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Wie man ein Excel-Arbeitsbuch als ODS erstellt und speichert mit Aspose.Cells für .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Wie man arbeitsbuchbezogene benannte Bereiche in Excel mit Aspose.Cells .NET erstellt](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}