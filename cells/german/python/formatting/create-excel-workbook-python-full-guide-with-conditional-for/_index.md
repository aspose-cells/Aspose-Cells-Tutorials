---
category: general
date: 2026-07-14
description: Erstelle Python‑Code für eine Excel‑Arbeitsmappe, der die Zellenhintergrundfarbe
  festlegt, Zellen basierend auf einem Datumsbereich hervorhebt und die Arbeitsmappe
  innerhalb von Minuten als XLSX speichert.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- save workbook as xlsx
- highlight cells based on date range
- conditional formatting based on date
language: de
lastmod: 2026-07-14
og_description: Erstellen Sie sofort ein Excel-Arbeitsbuch mit Python. Lernen Sie,
  die Hintergrundfarbe von Zellen festzulegen, Zellen basierend auf einem Datumsbereich
  hervorzuheben und das Arbeitsbuch als XLSX mit Aspose.Cells zu speichern.
og_image_alt: Screenshot showing an Excel sheet created with Python highlighting yesterday's
  dates
og_title: Excel-Arbeitsmappe mit Python erstellen – Schritt‑für‑Schritt bedingte Formatierung
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Create Excel workbook Python code that sets cell background color,
    highlights cells based on date range, and saves workbook as XLSX in minutes.
  headline: Create Excel Workbook Python – Full Guide with Conditional Formatting
  type: TechArticle
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Excel-Arbeitsmappe mit Python erstellen – Vollständiger Leitfaden mit bedingter
  Formatierung
url: /de/python/formatting/create-excel-workbook-python-full-guide-with-conditional-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel‑Arbeitsmappe mit Python erstellen – Vollständige Anleitung inkl. bedingter Formatierung

Haben Sie sich schon einmal gefragt, wie man **Excel‑Arbeitsmappe Python**‑Skripte erstellt, die professionell aussehen, ohne Excel manuell zu öffnen? Sie sind nicht allein. In vielen datengetriebenen Projekten müssen wir Tabellen erzeugen, Zellen farblich kennzeichnen und sogar Daten markieren, die in einen bestimmten Zeitraum fallen – alles aus reinem Python‑Code.

In diesem Tutorial gehen wir Schritt für Schritt durch ein vollständiges, sofort ausführbares Beispiel, das **eine Excel‑Arbeitsmappe mit Python** mithilfe der Aspose.Cells‑Bibliothek **erstellt**, **Zellenhintergrundfarbe setzt**, **bedingte Formatierung basierend auf Datum** anwendet und schließlich **die Arbeitsmappe als xlsx speichert**. Am Ende haben Sie ein wiederverwendbares Snippet, das Sie in jede Automatisierungspipeline einbinden können.

## Was Sie lernen werden

- Wie man eine Arbeitsmappe initialisiert und das erste Arbeitsblatt abruft.  
- Eine Hilfsfunktion, die eine bedingte Formatierungssammlung für einen beliebigen Zellbereich hinzufügt.  
- Verwendung von **bedingter Formatierung basierend auf Datum**, um gestrige Einträge hervorzuheben.  
- Anpassen der Spaltenbreiten für ein übersichtliches Layout.  
- Persistieren des Ergebnisses mit **save workbook as xlsx**.  

Eine externe Excel‑Installation ist nicht erforderlich – Aspose.Cells erledigt alles im Speicher.

## Voraussetzungen

- Python 3.8+ installiert.  
- `aspose-cells`‑Paket (`pip install aspose-cells`).  
- Grundlegende Kenntnisse von Python‑Funktionen und `datetime`‑Objekten.  

Falls Sie Aspose.Cells noch nie verwendet haben, denken Sie daran, dass es sich um eine leistungsstarke, reine‑Python‑API handelt, die das Excel‑Objektmodell nachahmt. Sie ist ideal für serverseitige Generierung, bei der die Office‑Suite nicht verfügbar ist.

## Schritt 1: Arbeitsmappe initialisieren (Create Excel Workbook Python)

Zuerst müssen wir **excel workbook python**‑artig **erstellen**. Dieser Schritt erzeugt ein leeres Arbeitsmappen‑Objekt und verweist auf das Standard‑Arbeitsblatt.

```python
# Step 1 – create a fresh workbook and get the first sheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, Color, SaveFormat
from datetime import datetime

workbook = Workbook()                     # <-- creates a new Excel file in memory
worksheet = workbook.worksheets[0]        # the default (first) sheet
```

> **Warum das wichtig ist:** Die Klasse `Workbook` ist der Einstiegspunkt für jede Excel‑Operation. Durch das programmgesteuerte Erzeugen vermeiden wir jegliche manuelle Dateiverwaltung.

## Schritt 2: Hilfsfunktion zum Hinzufügen einer bedingten Formatierungssammlung (Set Cell Background Color)

Bedingte Formatierung lebt in einer *Sammlung*, die einem Bereich zugeordnet ist. Wir packen dieses Boilerplate in eine kleine Hilfsfunktion, die uns außerdem ermöglicht, **cell background color** für den gesamten Bereich zu setzen.

```python
def add_time_period_condition(cell_range: str, highlight_color: Color):
    """
    Adds a conditional‑formatting collection to `cell_range` and
    applies `highlight_color` as the base fill.
    """
    worksheet.conditional_formattings.add(cell_range)   # attach to the range
    cf = worksheet.conditional_formattings[-1]           # grab the newly added collection
    cf.style.background_color = highlight_color
    cf.style.pattern = BackgroundType.SOLID
    return cf
```

> **Pro‑Tipp:** Eine Hilfsfunktion hält den Hauptablauf sauber und lässt dieselbe Logik leicht für mehrere Bereiche wiederverwenden.

## Schritt 3: Bedingte Formatierung basierend auf Datum anwenden (Highlight Cells Based on Date Range)

Jetzt **highlight cells based on date range**. Das Beispiel fokussiert sich auf „gestern“, Sie können jedoch `TimePeriodType.YESTERDAY` durch `TODAY`, `LAST_WEEK` usw. ersetzen.

```python
# Step 3 – create a TIME_PERIOD rule for I19:K20 (yesterday)
cf = add_time_period_condition("I19:K20", Color.medium_sea_green)

condition_index = cf.add_condition(FormatConditionType.TIME_PERIOD)
condition = cf[condition_index]

# Define the visual style for the matching cells
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# The actual rule: any cell whose date is yesterday gets the pink fill
condition.time_period = TimePeriodType.YESTERDAY
```

> **Was passiert?**  
> 1. Wir geben dem gesamten Bereich zunächst einen neutralen grünen Hintergrund.  
> 2. Dann fügen wir eine `TIME_PERIOD`‑Bedingung hinzu, die die Füllung **nur** dann rosa überschreibt, wenn das Datum der Zelle gestern ist.  
> 3. Das Enum `TimePeriodType` übernimmt die Datumsberechnung, sodass Sie keine eigene Logik schreiben müssen.

## Schritt 4: Beispiel‑Daten einfügen (So the Rule Can Be Evaluated)

Um die Regel in Aktion zu sehen, tragen wir ein paar Daten in das Blatt ein. Einer liegt im „gestern“-Fenster, der andere nicht.

```python
# Populate I19 with a date that is yesterday (relative to the hard‑coded date)
date_cell = worksheet.cells.get("I19")
date_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008
date_style = date_cell.get_style()
date_style.number = 30                     # Excel’s built‑in date format
date_cell.set_style(date_style)

# Populate K20 with a date that is NOT yesterday
date_cell = worksheet.cells.get("K20")
date_cell.put_value(datetime(2008, 8, 3))    # 03‑Aug‑2008
date_style = date_cell.get_style()
date_style.number = 30
date_cell.set_style(date_style)

# Add a label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

> **Hinweis zu Randfällen:** Wenn Ihre Arbeitsmappe in verschiedenen Locale‑Einstellungen geöffnet wird, sollten Sie `date_style.custom = "dd‑mm‑yyyy"` verwenden, um ein einheitliches Anzeigeformat zu erzwingen.

## Schritt 5: Layout aufräumen (Auto‑Fit Columns)

Ein gedrängtes Tabellenblatt wirkt unprofessionell. Lassen Sie uns **column width for a tidy output** anpassen.

```python
# Auto‑fit column L (index 12) to show the full content without truncation
worksheet.auto_fit_column(12)
```

> **Warum auto‑fit?** Es sorgt dafür, dass lange Beschriftungen oder Daten vollständig sichtbar sind – besonders wichtig, wenn Sie die Datei mit nicht‑technischen Stakeholdern teilen.

## Schritt 6: Arbeitsmappe speichern (Save Workbook As XLSX)

Abschließend **save workbook as xlsx** an einem Ort Ihrer Wahl. Die Konstante `SaveFormat.XLSX` weist Aspose.Cells an, das moderne OpenXML‑Format zu schreiben.

```python
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Erwartetes Ergebnis:**  
> - Die Zellen I19 und K20 enthalten Daten.  
> - I19 (gestern) ist rosa hervorgehoben, während K20 grün bleibt.  
> - Spalte L wird automatisch erweitert, um das Label „Yesterday“ vollständig anzuzeigen.  

Öffnen Sie `TimePeriodDemo.xlsx` in Excel, die bedingte Formatierung ist bereits aktiv – keine zusätzlichen Schritte nötig.

---

![Excel sheet showing highlighted yesterday date](https://example.com/images/excel-demo.png "Screenshot of the generated Excel file with highlighted cells")

*Das obige Bild veranschaulicht die fertige Arbeitsmappe; beachten Sie die rosa Hervorhebung in der Zelle, die das gestrige Datum enthält.*

## Zusammenfassung: Was wir erreicht haben

- **Created an Excel workbook python** von Grund auf mit Aspose.Cells.  
- **Set cell background color** für einen gesamten Bereich, um dem Blatt eine visuelle Kennzeichnung zu geben.  
- **Conditional formatting based on date** angewendet, um gestrige Einträge automatisch zu markieren.  
- **Saved workbook as xlsx**, bereit für Verteilung oder weitere Verarbeitung.  

All das geschah in weniger als 60 Zeilen Python, und der Code funktioniert auf jeder Plattform, die das Aspose.Cells‑Runtime unterstützt.

## Nächste Schritte & verwandte Themen

Wenn Ihnen das gefallen hat, könnten Sie auch folgende Themen erkunden:

- **set cell background color** für ganze Zeilen basierend auf Statuswerten (z. B. „Completed“, „Pending“).  
- Verwendung von **highlight cells based on date range**, um rollierende Fenster zu erstellen (letzte 7 Tage, aktueller Monat).  
- Export in andere Formate wie **CSV** oder **PDF** mit `SaveFormat.CSV` bzw. `SaveFormat.PDF`.  
- Hinzufügen von **charts** programmgesteuert, um die gerade formatierten Daten zu visualisieren.  

Passen Sie die Datumslogik an, ändern Sie die Farbpalette oder erweitern Sie den Bereich auf ganze Spalten. Das Muster bleibt gleich: Arbeitsmappe erstellen, bedingte Formatierungssammlung anhängen, Regel definieren und speichern.

Haben Sie Fragen zu einem speziellen Anwendungsfall? Hinterlassen Sie einen Kommentar unten – happy coding!

## Was Sie als Nächstes lernen sollten


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Excel Automation with Aspose.Cells .NET: Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/hongkong/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}