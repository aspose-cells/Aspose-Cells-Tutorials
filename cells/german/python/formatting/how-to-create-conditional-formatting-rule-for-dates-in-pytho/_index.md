---
category: general
date: 2026-08-24
description: Create conditional formatting rule in Python using Aspose.Cells to highlight
  dates, with auto‑fit column and background color formatting.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting rule
- auto fit column
- conditional formatting by date
- background color conditional format
- date based conditional format
language: de
lastmod: 2026-08-24
og_description: Create conditional formatting rule in Python with Aspose.Cells. Learn
  how to highlight dates, set background colors, and auto‑fit columns in just a few
  lines of code.
og_image_alt: Screenshot of an Excel sheet where yesterday's date cells are highlighted
  in pink
og_title: Create a conditional formatting rule for dates in Python – step‑by‑step
  guide
schemas:
- author: Aspose
  dateModified: '2026-08-24'
  description: Create conditional formatting rule in Python using Aspose.Cells to
    highlight dates, with auto‑fit column and background color formatting.
  headline: How to create conditional formatting rule for dates in Python
  type: TechArticle
tags:
- Aspose.Cells
- Python
- Excel automation
- Conditional formatting
title: How to create conditional formatting rule for dates in Python
url: /de/python/formatting/how-to-create-conditional-formatting-rule-for-dates-in-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man eine bedingte Formatierungsregel für Daten in Python erstellt

Wenn Sie eine **create conditional formatting rule** benötigen, die auf Daten reagiert, zeigt Ihnen dieser Leitfaden genau, wie Sie dies mit Aspose.Cells für Python umsetzen können. Egal, ob Sie ein Reporting‑Dashboard oder eine automatisierte Tabellenkalkulation erstellen, Sie sehen, wie Sie die Daten von gestern hervorheben, eine benutzerdefinierte Hintergrundfarbe anwenden und die **auto fit column**‑Breiten anpassen, sodass das Ergebnis professionell wirkt.

In diesem Tutorial behandeln wir **conditional formatting by date**, demonstrieren ein **background color conditional format** und schließen mit dem Speichern der Arbeitsmappe als XLSX‑Datei ab. Am Ende haben Sie eine wiederverwendbare Hilfsfunktion, die Sie an jede gewünschte **date based conditional format** anpassen können.

## Was Sie lernen werden

* Eine Arbeitsmappe und ein Arbeitsblatt mit Aspose.Cells einrichten.
* Eine Hilfsfunktion schreiben, die ein **date based conditional format** zu einem beliebigen Zellenbereich hinzufügt.
* Zellen mit Beispieldaten füllen, damit die Regel ausgewertet werden kann.
* **auto fit column** anwenden, um den Inhalt lesbar zu machen.
* Die Arbeitsmappe speichern und die hervorgehobenen Zellen überprüfen.

Die einzige Voraussetzung ist eine funktionierende Python‑Umgebung mit dem installierten `aspose-cells`‑Paket.

## Voraussetzungen

| Anforderung | Details |
|-------------|---------|
| Python | 3.8+ |
| Aspose.Cells for Python via Java | `pip install aspose-cells` |
| Grundkenntnisse der Excel‑Konzepte | worksheets, cells, formatting |
| Optional: IDE (VS Code, PyCharm, usw.) | beliebiger Editor, der Python‑Skripte ausführen kann |

## Schritt 1: Eine Arbeitsmappe erstellen und das erste Arbeitsblatt abrufen

Der erste Schritt besteht darin, **create conditional formatting rule**‑bereite Objekte zu erstellen: ein `Workbook` und das zugehörige Standard‑`Worksheet`. Diese Objekte sind der Einstiegspunkt für alle nachfolgenden Vorgänge.

```python
# Step 1 – initialize workbook and worksheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create a new, empty workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Warum das wichtig ist:* Das `Workbook` enthält die gesamte Excel‑Datei, während das `Worksheet` der Ort ist, an dem Sie Zellen, Stile und **conditional formatting by date** anwenden. Ohne diese Objekte hat der restliche Code keinen Ansatzpunkt.

## Schritt 2: Eine Hilfsfunktion erstellen, um ein TIME_PERIOD‑bedingtes Format hinzuzufügen

Anstatt denselben Boiler‑Plate‑Code für jeden Bereich zu wiederholen, kapseln wir die Logik in einer Hilfsfunktion. Diese Funktion fügt ein **background color conditional format** hinzu, das Zellen basierend auf einem `TimePeriodType` (z. B. Yesterday, Today, LastWeek) färbt.

```python
def add_time_period_condition(cell_range: str, bg_color: Color, period: TimePeriodType):
    """
    Attach a TIME_PERIOD conditional format to `cell_range`.
    The rule highlights cells that fall within `period` using `bg_color`.

    Args:
        cell_range: A1‑style range string, e.g., "I19:K20".
        bg_color:   Desired background color for matching cells.
        period:     Aspose.Cells TimePeriodType enum value.
    Returns:
        The FormatConditionCollection for further customization if needed.
    """
    # 1️⃣ Attach a new ConditionalFormatting block to the specified range
    worksheet.conditional_formattings.add(cell_range)

    # 2️⃣ Grab the collection of conditions for that block
    conditions = worksheet.conditional_formattings[-1].format_conditions

    # 3️⃣ (Optional) Set a default background for the whole range
    conditions.back_color = bg_color

    # 4️⃣ Add a TIME_PERIOD condition and configure its appearance
    idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[idx]

    # Apply the visual style – pink background in this example
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Define which period triggers the formatting
    condition.time_period = period

    return conditions
```

*Warum wir eine Hilfsfunktion verwenden:* Sie isoliert die Logik des **date based conditional format**, wodurch der Code leichter zu lesen, zu testen und in mehreren Tabellen oder Projekten wiederzuverwenden ist.

## Schritt 3: Die bedingte Formatierungsregel auf einen bestimmten Bereich anwenden

Jetzt verwenden wir die Hilfsfunktion, um Zellen hervorzuheben, die „Yesterday“ enthalten. Dies ist der Kern unserer **create conditional formatting rule**‑Operation.

```python
# Step 3 – highlight cells I19:K20 that contain “Yesterday”
add_time_period_condition(
    cell_range="I19:K20",
    bg_color=Color.medium_sea_green,   # optional default background for the whole range
    period=TimePeriodType.YESTERDAY   # the date‑based trigger
)
```

Wenn die Arbeitsmappe geöffnet wird, erscheint jede Zelle in `I19:K20`, deren Datum dem gestrigen Datum entspricht, mit einer rosa Füllung (der Stil, den wir in der Hilfsfunktion festgelegt haben). Das Argument `bg_color` zeigt, wie Sie bei Bedarf einen Standard‑Hintergrund hinter der bedingten Farbe schichten können.

## Schritt 4: Den Bereich mit Beispieldaten füllen

Eine bedingte Regel wird erst sichtbar, wenn das Arbeitsblatt Daten enthält, die die Bedingung erfüllen. Wir fügen zwei Daten ein: eines, das „Yesterday“ entspricht, und ein weiteres, das außerhalb des Zeitraums liegt.

```python
# Step 4 – insert sample dates for demonstration

# Cell I19 will match the YESTERDAY period
yesterday_cell = worksheet.cells.get("I19")
yesterday_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008 is “yesterday” relative to 31‑Jul‑2008
yesterday_cell.get_style().number = 30          # 30 = built‑in date format
yesterday_cell.set_style(yesterday_cell.get_style())

# Cell K20 will NOT match the period (it’s a later date)
outside_cell = worksheet.cells.get("K20")
outside_cell.put_value(datetime(2008, 8, 3))     # 03‑Aug‑2008 is outside “Yesterday”
outside_cell.get_style().number = 30
outside_cell.set_style(outside_cell.get_style())

# Optional label for clarity – not part of the rule
worksheet.cells.get("I20").put_value("Yesterday")
```

*Warum das wichtig ist:* Durch die Verwendung von `datetime`‑Objekten stellen wir sicher, dass Excel die Werte als echte Daten behandelt, was für das korrekte Funktionieren von **conditional formatting by date** erforderlich ist. Das numerische Format (`30`) garantiert, dass die Zellen als erkennbare Daten angezeigt werden.

## Schritt 5: Spalte automatisch anpassen und die Arbeitsmappe speichern

Nachdem Daten und Formatierung vorhanden sind, ist der letzte Schliff, die Breiten mit **auto fit column** anzupassen, damit die Daten vollständig sichtbar sind. Anschließend schreiben wir die Datei auf die Festplatte.

```python
# Step 5 – adjust column width and save the file

# Auto‑fit column 12 (the column that contains our sample data)
worksheet.auto_fit_column(12)

# Save the workbook as an XLSX file
output_path = "YOUR_DIRECTORY/TimePeriodDemo.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

Der Aufruf `auto_fit_column` prüft den längsten Inhalt in Spalte 12 (entspricht Spalte **L** in Excel) und erweitert die Breite entsprechend. Dieser kleine Schritt verhindert abgeschnittene Daten und lässt das **background color conditional format** deutlich sichtbar werden.

### Erwartetes Ergebnis

Wenn Sie `TimePeriodDemo.out.xlsx` öffnen:

| I19 (date) | I20 (label) | K20 (date) |
|------------|------------|------------|
| 30‑Jul‑2008 (highlighted pink) | Yesterday | 03‑Aug‑2008 (no highlight) |

* Die Zelle mit dem gestrigen Datum zeigt einen rosa Hintergrund, weil die **create conditional formatting rule** den Zeitraum `YESTERDAY` getroffen hat.
* Alle anderen Zellen behalten den Standard‑Hintergrund (oder das optionale `medium_sea_green`, das Sie angegeben haben).
* Spalte L wird automatisch verbreitert, sodass die Daten vollständig lesbar sind.

## Häufige Variationen und Randfälle

| Situation | Wie der Code anzupassen ist |
|-----------|-----------------------------|
| **„Today“ statt „Yesterday“ hervorheben** | Replace `TimePeriodType.YESTERDAY` with `TimePeriodType.TODAY`. |
| **Eine andere Hintergrundfarbe verwenden** | Change `condition.style.background_color = Color.pink` to any other `Color` (e.g., `Color.light_sky_blue`). |
| **Die Regel auf einen nicht zusammenhängenden Bereich anwenden** | Call `add_time_period_condition` multiple times with different `cell_range` strings (e.g., `"A1:A10", "C1:C10"`). |
| **Mit einer bereits vorhandenen Arbeitsmappe arbeiten** | Load the file with `Workbook("myfile.xlsx")` instead of creating a new one. |
| **Mehrere datumbasierte Bedingungen im selben Bereich** | After the first `add_time_period_condition` call, add another condition with `conditions.add_condition(FormatConditionType.TIME_PERIOD)` and set a different `time_period`. |

## Fazit

Sie wissen jetzt, wie Sie mit Aspose.Cells für Python eine **create conditional formatting rule** erstellen, die auf Daten reagiert, ein **background color conditional format** anwenden und die Breiten mit **auto fit column** anpassen. Die Hilfsfunktion abstrahiert die Logik, sodass Sie dasselbe Muster für jedes **conditional formatting by date**‑Szenario wiederverwenden können – sei es „Yesterday“, „LastWeek“ oder ein benutzerdefinierter Bereich.

Als Nächstes könnten Sie erkunden:

* Hinzufügen von **icon sets** oder **data bars** neben Datumsregeln.
* Generieren dynamischer Berichte, die Daten aus einer Datenbank ziehen.
* Kombinieren mehrerer **date based conditional format**‑Regeln in einem einzigen Blatt.

Fühlen Sie sich frei, mit verschiedenen Farben, Zeiträumen und Bereichen zu experimentieren, um den Anforderungen Ihres Projekts gerecht zu werden. Viel Spaß beim Programmieren!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Master Conditional Formatting in Excel Using Aspose.Cells .NET: A Comprehensive Guide](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [How to Extract Conditional Formatting Colors Using Aspose.Cells for .NET](/cells/english/net/formatting/extract-conditional-formatting-colors-aspose-cells-net/)
- [Master Conditional Formatting with Custom Fonts in Excel using Aspose.Cells for .NET and C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}