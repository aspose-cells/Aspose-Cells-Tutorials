---
category: general
date: 2026-11-16
description: Erstelle bedingte Formatierung in Excel mit Python. Lerne, einen Bereich
  für bedingte Formatierung hinzuzufügen, Daten hervorzuheben und ein Arbeitsbuch
  programmgesteuert zu erstellen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting
- create excel workbook python
- how to highlight dates
- add conditional formatting range
- add conditional formatting python
language: de
lastmod: 2026-11-16
og_description: Erstelle bedingte Formatierung in Excel mit Python. Dieses Tutorial
  zeigt, wie man einen Bereich für bedingte Formatierung hinzufügt, Daten hervorhebt
  und eine Arbeitsmappe erstellt.
og_image_alt: Screenshot of Excel sheet with conditional formatting applied using
  Python
og_title: Bedingte Formatierung in Excel mit Python erstellen – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create conditional formatting in Excel using Python. Learn to add a
    conditional formatting range, highlight dates, and build a workbook programmatically.
  headline: How to create conditional formatting in Excel with Python
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Wie man in Excel mit Python bedingte Formatierung erstellt
url: /de/python/formatting/how-to-create-conditional-formatting-in-excel-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man bedingte Formatierung in Excel mit Python erstellt

Wenn Sie **bedingte Formatierung** in einer Excel‑Datei erstellen müssen, während Sie in Python arbeiten, zeigt Ihnen dieser Leitfaden genau, wie das geht. Sie lernen, **excel workbook python**‑artig zu erstellen, einen Formatierungsbereich zu definieren und Daten hervorzuheben, ohne die IDE zu verlassen.

Bedingte Formatierung ermöglicht es Ihnen, Zellen, die bestimmte Kriterien erfüllen, visuell zu kennzeichnen – perfekt für Dashboards, Berichte oder Daten‑Validierungs‑Sheets. Am Ende dieses Tutorials besitzen Sie eine voll funktionsfähige Arbeitsmappe, die Zellen mit dem Datum „Gestern“ rosa färbt, während der Rest des Bereichs grün bleibt.

## Was Sie erreichen werden

* Eine neue Arbeitsmappe von Grund auf erstellen.  
* Eine Sammlung von bedingten Formatierungen für einen bestimmten Zellblock hinzufügen.  
* Eine **TIME_PERIOD**‑Regel anwenden, die Daten hervorhebt (das Szenario „wie man Daten hervorhebt“).  
* Die Datei als XLSX‑Arbeitsmappe speichern, bereit für die Weiterverarbeitung.

**Voraussetzungen**  
* Python 3.8+  
* `aspose-cells` Python‑Paket (`pip install aspose-cells`)  
* Grundlegende Kenntnisse des Python‑Moduls `datetime`  

---

## Wie man bedingte Formatierung in Python erstellt

Der erste Schritt besteht darin, die Arbeitsmappe und das Arbeitsblatt einzurichten, das die Formatierungsregeln hosten wird.

```python
# Step 1: Import required classes and create a new workbook
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Instantiate a blank workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Optional: auto‑fit column 12 (L) to make the output readable
worksheet.auto_fit_column(12)
```

**Warum das wichtig ist** – `Workbook` ist der Einstiegspunkt für alle Excel‑Operationen. Das programmatische Erstellen der Arbeitsmappe ersetzt den manuellen Schritt „Datei → Neu“ und ermöglicht automatisierte Berichtspipelines.

---

## Vorbereitung der bedingten Formatierungssammlung – Bereich für bedingte Formatierung hinzufügen

Als Nächstes definieren wir den Zellblock, der die Regel erhalten soll. In diesem Beispiel ist der Bereich **I19:K20**.

```python
# Step 2: Create a conditional‑format collection for the target range
conds = worksheet.conditional_formattings.add("I19:K20")

# Apply a base style (green background) that will show when no rule matches
conds[0].style.background_color = Color.medium_sea_green
conds[0].style.pattern = BackgroundType.SOLID
```

**Erklärung** – `conditional_formattings.add` registriert eine neue Sammlung, die an die Adresszeichenfolge gebunden ist. Die erste Bedingung (`conds[0]`) fungiert als „Standard“‑Stil; die spätere Regel überschreibt sie, wenn ihre Kriterien erfüllt sind.

---

## Hinzufügen einer TIME_PERIOD‑Bedingung – wie man Daten hervorhebt

Jetzt fügen wir die eigentliche Logik hinzu, die „Gestern“-Daten erkennt und sie rosa färbt.

```python
# Step 3: Add a TIME_PERIOD condition that highlights cells dated “Yesterday”
idx = conds.add_condition(FormatConditionType.TIME_PERIOD)   # returns the new index
condition = conds[idx]

# Define the visual style for cells that satisfy the condition
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Set the rule to the built‑in YESTERDAY period
condition.time_period = TimePeriodType.YESTERDAY
```

**Warum TIME_PERIOD verwenden?** – Aspose.Cells stellt eingebaute Aufzählungen wie `YESTERDAY`, `TODAY` und `LAST_WEEK` bereit. Sie vergleichen den Datumswert der Zelle mit dem aktuellen Systemdatum und machen benutzerdefinierte Formeln überflüssig.

---

## Beispiel‑Daten einfügen – Regel demonstrieren

Um die Formatierung in Aktion zu sehen, fügen wir ein Datum ein, das zur Regel passt, und ein weiteres, das nicht passt.

```python
# Step 4: Populate sample dates so the rule can be seen

# Cell I19 gets a date that is “yesterday” relative to 2008‑07‑31
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))  # yesterday for the example
style = cell_i19.get_style()
style.number = 30                         # full date format (e.g., 7/30/2008)
cell_i19.set_style(style)

# Cell K20 gets a later date – it should stay green
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))   # a future date
style = cell_k20.get_style()
style.number = 30
cell_k20.set_style(style)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

**Hinweis zum Randfall** – Die `TIME_PERIOD`‑Regel funktioniert nur mit *echten* Datumswerten. Enthält eine Zelle Text (z. B. „N/A“), wird die Regel ignoriert, sodass unerwartete Farbwechsel vermieden werden.

---

## Arbeitsmappe speichern – add conditional formatting python

Abschließend schreiben wir die Arbeitsmappe auf die Festplatte. Die Datei kann in jedem Tabellenkalkulationsprogramm geöffnet werden, um die Farben zu überprüfen.

```python
# Step 5: Save the workbook
output_path = "TimePeriodExample.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

**Erwartetes Ergebnis**  

| I19 (grün → rosa) | J19 (grün) | K19 (grün) |
|--------------------|------------|------------|
| 7/30/2008 (gestern) | – | – |
| **I20**: „Gestern“-Label | – | – |
| I21‑K21 (grün)    | – | – |

Die Zelle **I19** erscheint mit einem rosa Hintergrund, weil ihr Datum dem Zeitraum „Gestern“ entspricht, während **K20** grün bleibt.

---

## Häufige Fragen und praktische Tipps

* **Kann ich einen benutzerdefinierten Datumsbereich anstelle eines integrierten Zeitraums verwenden?**  
  Ja. Ersetzen Sie `condition.time_period` durch `condition.formula1 = "TODAY()-1"` und setzen Sie `condition.type = FormatConditionType.FORMULA`.

* **Was, wenn meine Arbeitsmappe bereits Daten enthält?**  
  Verwenden Sie `worksheet.cells.import_data`, um Daten in großen Mengen zu laden, bevor Sie die Sammlung der bedingten Formatierung hinzufügen.

* **Leistung bei großen Tabellen?**  
  Das Hinzufügen vieler Bedingungen kann die Darstellung verlangsamen. Gruppieren Sie Zellen mit derselben Regel in einen einzigen Bereich (z. B. „A1:C1000“), um die Anzahl der Bedingungen gering zu halten.

* **Plattformübergreifende Kompatibilität?**  
  Die erzeugte XLSX‑Datei folgt dem Office Open XML‑Standard und funktioniert daher in Windows‑, macOS‑ und Linux‑Tabellenkalkulationsanwendungen.

---

## Fazit

Sie wissen jetzt, wie man **bedingte Formatierung** in einer Excel‑Arbeitsmappe mit Python erstellt. Das Tutorial behandelte das Erstellen der Arbeitsmappe, das Definieren eines **add conditional formatting range**, das Anwenden einer **how to highlight dates**‑Regel und das Speichern der Datei – alles mit dem **add conditional formatting python**‑Ansatz von Aspose.Cells.

Ab hier können Sie:

* Das Regelset mit anderen `TimePeriodType`‑Werten erweitern (z. B. `TODAY`, `LAST_MONTH`).  
* Mehrere Bedingungen für denselben Bereich kombinieren, um reichhaltigere visuelle Hinweise zu erhalten.  
* Dieses Vorgehen in automatisierte Berichtspipelines oder Web‑Services integrieren.

Viel Spaß beim Coden, und experimentieren Sie gern mit verschiedenen Farben, Bereichen und Datumslogiken, um Ihre Berichtsanforderungen zu erfüllen!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Create Excel workbook Python date conditional formatting](/cells/english/python/formatting/create-excel-workbook-python-date-conditional-formatting/)
- [How to apply time period conditional formatting in Excel using Python](/cells/english/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/)
- [Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting](/cells/english/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}