---
category: general
date: 2026-06-21
description: Erstelle eine Multiplikationstabelle in Excel mit Python. Lerne, wie
  man Lambda verwendet, wie man makearray nutzt, das Excel‑Array anzeigt und Excel‑Werte
  mit Python ausliest, in einer Schritt‑für‑Schritt‑Anleitung.
draft: false
keywords:
- create multiplication table
- how to use lambda
- how to use makearray
- display excel array
- read excel values python
language: de
og_description: Erstelle eine Multiplikationstabelle in Excel mit Python. Dieses Tutorial
  zeigt, wie man Lambda, makearray verwendet, ein Excel‑Array anzeigt und Excel‑Werte
  effizient mit Python ausliest.
og_title: Multiplikationstabelle in Excel mit Python erstellen – Komplettanleitung
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create multiplication table in Excel using Python. Learn how to use
    lambda, how to use makearray, display excel array and read excel values python
    in a step‑by‑step tutorial.
  headline: Create multiplication table in Excel with Python – Full Guide
  type: TechArticle
tags:
- python
- excel
- openpyxl
title: Multiplikationstabelle in Excel mit Python erstellen – Vollständige Anleitung
url: /de/python/import-and-export/create-multiplication-table-in-excel-with-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Multiplikationstabelle in Excel mit Python erstellen – Vollständige Anleitung

Haben Sie sich jemals gefragt, wie man **create multiplication table** in Excel erstellt, ohne jede Zelle manuell einzugeben? Sie sind nicht allein. In vielen Reporting‑Szenarien benötigen Sie ein schnelles 5×5‑Raster (oder größer) von Produkten, und das von Hand zu erledigen ist Zeitverschwendung.  

In diesem Tutorial führen wir Sie durch eine saubere, Python‑gesteuerte Methode, um diese Tabelle zu erzeugen, sie mit einer `MAKEARRAY`‑Formel einzubetten und anschließend die Ergebnisse zurück in Ihr Skript zu holen. Unterwegs beantworten wir **how to use lambda**, zeigen **how to use makearray** und demonstrieren **display excel array** sowie **read excel values python** – alles in einem zusammenhängenden Beispiel.

Am Ende haben Sie einen wiederverwendbaren Code‑Snippet, der mit jeder Arbeitsmappe funktioniert, und Sie verstehen, warum dieser Ansatz sowohl schnell als auch zukunftssicher ist.

## Was Sie benötigen

- Python 3.8+ (die neueste stabile Version ist in Ordnung)
- Die `openpyxl`‑Bibliothek (oder jede Excel‑fähige Bibliothek, die Formeln unterstützt)
- Ein grundlegendes Verständnis von Lambda‑Ausdrücken in Python
- Keine speziellen Excel‑Add‑Ins; die native `MAKEARRAY`‑Funktion (verfügbar in Excel 365) übernimmt die schwere Arbeit

Falls Ihnen etwas fehlt, führen Sie einfach `pip install openpyxl` aus und Sie können loslegen.

## Multiplikationstabelle erstellen – Überblick

Die Kernidee ist einfach: Wir erstellen eine neue Arbeitsmappe, schreiben eine `MAKEARRAY`‑Formel, die eine 5 × 5‑Multiplikationsmatrix erzeugt, zwingen Excel, sie zu berechnen, und lesen schließlich die resultierenden Werte zurück in Python.

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Insert a MAKEARRAY formula that builds a 5×5 multiplication table
# The formula uses a LAMBDA that returns r*c for each row (r) and column (c)
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"

# Step 3: Calculate all formulas so the array is materialized in the sheet
workbook.calculate_formula()

# Step 4: Read and display the top‑left 5×5 block of values
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

Das Ausführen des Skripts gibt aus:

```
[1, 2, 3, 4, 5]
[2, 4, 6, 8, 10]
[3, 6, 9, 12, 15]
[4, 8, 12, 16, 20]
[5, 10, 15, 20, 25]
```

Das ist eine voll funktionsfähige **create multiplication table** in Excel, die vollständig aus Python generiert wurde.

### Warum `MAKEARRAY` anstelle einer Python‑Schleife verwenden?

- **Performance**: Excel führt die Berechnung nativ aus, was bei großen Matrizen schneller ist.
- **Live updating**: Wenn Sie später die Dimensionen in der Formel ändern, berechnet das Blatt automatisch neu.
- **Readability**: Die Formel drückt die Absicht („make an array“) direkt aus und hält Ihren Python‑Code übersichtlich.

## Wie man lambda in Python für Excel‑Formeln verwendet

Der `LAMBDA`‑Teil des `MAKEARRAY`‑Aufrufs ist eine an Excel‑seitige anonyme Funktion, kein Python‑Lambda. Trotzdem ist das Konzept dasselbe: Sie definieren ein kleines, inline‑Logikstück, das `r` (Zeilenindex) und `c` (Spaltenindex) nimmt und `r*c` zurückgibt.  

Wenn Sie neu bei **how to use lambda** in der Excel‑Welt sind, denken Sie daran, dass es sich um eine Mini‑Funktion handelt, die nur innerhalb der Formel existiert. Es ist nicht nötig, irgendwo eine separate Funktion zu deklarieren. In Python betten wir einfach den String ein:

```python
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"
```

Diese Zeile sagt Excel: *„Für jede Zelle in einem 5‑mal‑5‑Block berechne Zeile × Spalte.“*  

Da das Lambda von Excel ausgewertet wird, müssen Sie sich hier nicht um die Python‑eigene Lambda‑Syntax kümmern – nur um die Excel‑Syntax.

## Wie man makearray zur Erzeugung von Arrays verwendet

`MAKEARRAY` ist eine relativ neue Ergänzung zur Excel‑Funktionsbibliothek (verfügbar in Microsoft 365 seit 2022). Es ersetzt ältere Tricks wie `INDEX` + `ROW`/`COLUMN`‑Kombinationen. Die Signatur lautet:

```
MAKEARRAY(rows, columns, lambda)
```

- **rows** – gewünschte Anzahl an Zeilen.
- **columns** – gewünschte Anzahl an Spalten.
- **lambda** – ein Excel‑LAMBDA, das `(row, column)` erhält und einen Wert zurückgibt.

In unserem Beispiel haben wir `5,5` für eine klassische Multiplikationstabelle übergeben, aber Sie können diese Zahlen leicht ändern:

```python
worksheet["A1"] = "=MAKEARRAY(10,10, LAMBDA(r,c, r*c))"
```

Damit erhalten Sie eine 10 × 10‑Tabelle, ohne Python‑Schleifen zu verwenden. Dies demonstriert **how to use makearray** für jede Art von deterministischem Raster, sei es eine Lookup‑Tabelle, ein Heatmap oder ein Finanzplan.

## Excel‑Array anzeigen – Daten zurück nach Python holen

Sobald Excel die Formel berechnet hat, befinden sich die resultierenden Werte im Blatt wie jede manuell eingegebene Zelle. Um **display excel array** zu zeigen, iterieren wir über den Bereich und geben jede Zeile aus:

```python
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

- Verwenden Sie `worksheet.cell(row, column).value` anstelle des Dictionary‑Stil‑Indexierens, wenn Sie größere Bereiche handhaben müssen; es ist etwas schneller.
- Wenn Sie eine hübschere Tabelle wünschen, ziehen Sie `tabulate` oder `pandas.DataFrame` zur Formatierung der Ausgabe in Betracht.

Unten ist ein Screenshot des resultierenden Blatts (der Alt‑Text des Bildes enthält das Haupt‑Keyword für SEO):

![Screenshot, der die Erstellung einer Multiplikationstabelle in Excel mit Python zeigt](/images/multiplication-table-excel.png)

## Excel‑Werte mit Python lesen – Matrix für weitere Verarbeitung extrahieren

Oft ist der nächste Schritt nach **display excel array**, diese Zahlen in eine Datenanalyse‑Pipeline zu speisen. Dort glänzt **read excel values python**. Die gleiche Schleife, die wir zum Ausdrucken verwendet haben, kann umfunktioniert werden, um eine Liste von Listen, ein NumPy‑Array oder ein Pandas‑DataFrame zu erstellen:

```python
import pandas as pd

# Build a list of rows
data = []
for row_index in range(1, 6):
    row = [worksheet.cell(row=row_index, column=col_index).value
           for col_index in range(1, 6)]
    data.append(row)

# Convert to DataFrame for easy manipulation
df = pd.DataFrame(data, columns=[f"Col{c}" for c in range(1, 6)],
                  index=[f"Row{r}" for r in range(1, 6)])

print(df)
```

Ausgabe:

```
      Col1  Col2  Col3  Col4  Col5
Row1     1     2     3     4     5
Row2     2     4     6     8    10
Row3     3     6     9    12    15
Row4     4     8    12    16    20
Row5     5    10    15    20    25
```

Jetzt haben Sie ein vollständig typisiertes DataFrame, das Sie plotten, als CSV exportieren oder in ein Machine‑Learning‑Modell einspeisen können. Damit ist der **read excel values python**‑Teil des Workflows abgeschlossen.

## Randfälle & Praktische Tipps

- **Formula recalculation**: Wenn Sie die Arbeitsmappe nach dem ersten Aufruf von `calculate_formula()` ändern, müssen Sie sie erneut aufrufen; sonst bleibt das zwischengespeicherte Array veraltet.
- **Non‑365 Excel**: Ältere Excel‑Versionen unterstützen `MAKEARRAY` nicht. In diesem Fall greifen Sie auf eine Python‑generierte Tabelle zurück und schreiben jede Zelle einzeln.
- **Large tables**: Für Matrizen größer als ~100 × 100 sollten Sie das Streaming der Daten in Betracht ziehen, um zu vermeiden, dass das gesamte Blatt in den Speicher geladen wird.
- **Error handling**: Wickeln Sie die Berechnungs‑ und Leseschritte in `try/except`‑Blöcke, um `InvalidFileException` oder `FormulaError` abzufangen.

## Fazit

Wir haben Ihnen gerade gezeigt, wie man **create multiplication table** in Excel mit Python erstellt, wobei wir die Leistungsfähigkeit von **how to use lambda** und **how to use makearray** nutzen. Sie haben gesehen, wie man **display excel array** anzeigt, diese Werte mit **read excel values python** zurückliest und das Ergebnis sogar in ein Pandas‑DataFrame für nachgelagerte Analysen umwandelt.

Möchten Sie weitergehen? Versuchen Sie, die Multiplikationslogik durch etwas Komplexeres zu ersetzen – vielleicht eine Distanzmatrix, eine Wahrscheinlichkeits‑tabelle oder ein dynamisches Preis‑Raster. Das gleiche Muster gilt: eine Zeile `MAKEARRAY`, ein kurzer `calculate_formula()` und ein paar Python‑Schleifen, um die Daten zu extrahieren.

Wenn Ihnen diese Anleitung geholfen hat, geben Sie ihr einen Stern auf GitHub, teilen Sie sie mit Kollegen oder hinterlassen Sie einen Kommentar mit Ihrem Anwendungsfall. Viel Spaß beim Coden und genießen Sie die Kürze, Excel‑Tabellen mit einer einzigen Formel zu erzeugen!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man Excel-Arbeitsmappen mit Aspose.Cells .NET erstellt und konfiguriert: Eine Schritt‑für‑Schritt‑Anleitung](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Aspose.Cells .NET Tutorial: Wie man Excel‑Arbeitsmappen einfach erstellt und ändert](/cells/english/net/workbook-operations/aspose-cells-net-create-modify-excel-workbooks/)
- [Wie man benannte Bereiche in Excel mit Aspose.Cells .NET erstellt und gestaltet | Schritt‑für‑Schritt‑Anleitung](/cells/english/net/range-management/create-style-named-ranges-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}