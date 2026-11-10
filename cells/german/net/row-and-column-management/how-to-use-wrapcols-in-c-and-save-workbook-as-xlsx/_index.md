---
category: general
date: 2026-10-26
description: Erfahren Sie, wie Sie WRAPCOLS in C# verwenden, um einen Bereich in Spalten
  zu teilen, WRAPROWS für Zeilen anzuwenden und die Arbeitsmappe programmgesteuert
  als XLSX zu speichern.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split range into rows
- excel wrapcols example
- save workbook as xlsx
- create excel workbook programmatically
language: de
lastmod: 2026-10-26
og_description: Wie man WRAPCOLS in C# verwendet, um Daten in Spalten zu splitten,
  WRAPROWS für Zeilen nutzt und die Arbeitsmappe als XLSX speichert. Folgen Sie der
  vollständigen Schritt‑für‑Schritt‑Anleitung.
og_image_alt: Screenshot illustrating how to use WRAPCOLS to split a range into columns
  in Excel
og_title: Wie man WRAPCOLS in C# verwendet – Bereiche aufteilen und als XLSX speichern
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  headline: How to use WRAPCOLS in C# and save workbook as XLSX
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  name: How to use WRAPCOLS in C# and save workbook as XLSX
  steps:
  - name: What the saved file looks like
    text: 'When you open `wrapcols_wraprows_output.xlsx` in Excel you’ll see:'
  - name: Changing the number of columns or rows
    text: '* **More columns:** Increase the second argument of `WRAPCOLS`. Example:
      `=WRAPCOLS(A1:A10,5)` creates five columns, leaving empty cells where data runs
      out. * **Dynamic column count:** Use a cell reference instead of a hard‑coded
      number. `=WRAPCOLS(A1:A10, G1)` where `G1` holds the desired column c'
  - name: Handling empty or non‑numeric cells
    text: WRAPCOLS and WRAPROWS ignore empty cells by default, but they preserve the
      order of non‑empty values. If you need to preserve blanks, wrap the source range
      with `IFERROR` or `TEXT` functions before applying WRAPCOLS.
  - name: Saving to other formats
    text: 'While this tutorial focuses on **save workbook as xlsx**, Aspose.Cells
      supports many formats (`.xls`, `.csv`, `.pdf`, etc.):'
  - name: What’s next?
    text: '* Explore **conditional formatting** to highlight the spilled data. * Combine
      **WRAPCOLS** with **SORT** or **FILTER** for dynamic dashboards. * Use Aspose.Cells’
      **charting API** to visualize the rearranged data directly from code.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Wie man WRAPCOLS in C# verwendet und die Arbeitsmappe als XLSX speichert
url: /de/net/row-and-column-management/how-to-use-wrapcols-in-c-and-save-workbook-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man WRAPCOLS in C# verwendet und die Arbeitsmappe als XLSX speichert

Wenn Sie **how to use WRAPCOLS** benötigen, um Daten in einer Excel‑Datei neu zu organisieren, zeigt Ihnen dieser Leitfaden eine vollständige, ausführbare Lösung. Sie sehen ein **excel wrapcols example**, lernen, wie man **split range into rows** mit WRAPROWS durchführt, und schließen mit **save workbook as XLSX** ab – alles **programmatically** erledigt.

Die Arbeit mit Excel aus C# heraus bedeutet häufig, eine Arbeitsmappe zu erstellen, Formeln anzuwenden und die Datei zu speichern. Der untenstehende Code verwendet die Aspose.Cells‑Bibliothek, mit der Sie Excel‑Dateien manipulieren können, ohne Microsoft Office installiert zu haben. Am Ende dieses Tutorials können Sie **create excel workbook programmatically**, Daten sowohl horizontal als auch vertikal aufteilen und eine saubere `.xlsx`‑Datei erzeugen, die für die Weiterverarbeitung bereit ist.

## Voraussetzungen

* .NET 6.0 oder neuer (der Code funktioniert auch mit .NET Framework 4.7+)
* Ein Verweis auf das **Aspose.Cells** NuGet‑Paket  
  ```bash
  dotnet add package Aspose.Cells
  ```
* Grundlegende Kenntnisse in C# und Excel‑Formeln

## Schritt 1: Wie man WRAPCOLS verwendet, um einen Bereich in Spalten aufzuteilen

Die **WRAPCOLS**‑Funktion nimmt einen eindimensionalen Bereich und verteilt seine Werte über die angegebene Anzahl von Spalten. In diesem Beispiel beginnen wir mit Werten in `A1:A10` und lassen WRAPCOLS drei Spalten erzeugen.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is the “create excel workbook programmatically” step
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Populate source data for demonstration
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 0].PutValue($"Item {i + 1}");
        }

        // Apply WRAPCOLS: split A1:A10 into 3 columns starting at C1
        // The formula is entered in cell C1 (row 0, column 2)
        ws.Cells[0, 2].Formula = "=WRAPCOLS(A1:A10,3)";

        // -------------------------------------------------
        // Why this works:
        // -------------------------------------------------
        // * WRAPCOLS reads the source range (A1:A10) vertically.
        // * The second argument (3) tells Excel to create three columns.
        // * The function returns a 2‑dimensional array that Excel spills into the
        //   surrounding cells automatically.
        // -------------------------------------------------
```

> **Result:** Zellen `C1:E4` enthalten jetzt die ursprünglichen zehn Elemente, verteilt auf drei Spalten (die letzte Spalte enthält die verbleibenden Elemente).

![Screenshot, der zeigt, wie man WRAPCOLS verwendet, um einen Bereich in Spalten in Excel aufzuteilen](image-url.png)

## Schritt 2: Bereich mit WRAPROWS in Zeilen aufteilen

Während **WRAPCOLS** horizontal arbeitet, führt **WRAPROWS** das Gegenteil aus: Es verteilt einen Bereich über eine angegebene Anzahl von Zeilen. Hier nehmen wir Werte aus `B1:B10` und ordnen sie in zwei Zeilen ab `F1` an.

```csharp
        // Populate a second source column for WRAPROWS
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 1].PutValue($"Value {i + 1}");
        }

        // Apply WRAPROWS: split B1:B10 into 2 rows starting at F1
        ws.Cells[0, 5].Formula = "=WRAPROWS(B1:B10,2)";

        // -------------------------------------------------
        // Why WRAPROWS is useful:
        // -------------------------------------------------
        // * It converts a vertical list into a matrix with the specified row count.
        // * Handy when you need to prepare data for pivot tables, charts, or
        //   reporting layouts that expect a horizontal orientation.
        // -------------------------------------------------
```

> **Result:** Die Formel füllt die Zellen `F1:K2` mit den zehn Werten, verteilt über zwei Zeilen.

## Schritt 3: Arbeitsmappe als XLSX speichern

Nach dem Anwenden der Formeln ist der letzte Schritt, die Datei zu speichern. Der Vorgang **save workbook as xlsx** schreibt die im Speicher befindliche Arbeitsmappe auf die Festplatte im modernen OpenXML‑Format.

```csharp
        // Save the workbook – this completes the “save workbook as xlsx” step
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "wrapcols_wraprows_output.xlsx");

        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### Wie die gespeicherte Datei aussieht

Wenn Sie `wrapcols_wraprows_output.xlsx` in Excel öffnen, sehen Sie:

| C | D | E |
|---|---|---|
| Element 1 | Element 4 | Element 7 |
| Element 2 | Element 5 | Element 8 |
| Element 3 | Element 6 | Element 9 |
|        |        | Element 10 |

und

| F | G | H | I | J | K |
|---|---|---|---|---|---|
| Wert 1 | Wert 3 | Wert 5 | Wert 7 | Wert 9 | |
| Wert 2 | Wert 4 | Wert 6 | Wert 8 | Wert 10 | |

Die Formeln bleiben in den Zellen, sodass spätere Änderungen an den Quellbereichen automatisch übernommen werden.

## Schritt 4: Häufige Variationen und Sonderfälle

### Ändern der Anzahl von Spalten oder Zeilen

* **Mehr Spalten:** Erhöhen Sie das zweite Argument von `WRAPCOLS`.  
  Beispiel: `=WRAPCOLS(A1:A10,5)` erzeugt fünf Spalten und lässt leere Zellen, wenn die Daten ausgehen.
* **Dynamische Spaltenanzahl:** Verwenden Sie einen Zellbezug anstelle einer fest codierten Zahl.  
  `=WRAPCOLS(A1:A10, G1)`, wobei `G1` die gewünschte Spaltenanzahl enthält.

### Umgang mit leeren oder nicht‑numerischen Zellen

WRAPCOLS und WRAPROWS ignorieren standardmäßig leere Zellen, bewahren jedoch die Reihenfolge nicht‑leerer Werte. Wenn Sie Leerstellen erhalten möchten, umschließen Sie den Quellbereich mit den Funktionen `IFERROR` oder `TEXT`, bevor Sie WRAPCOLS anwenden.

### Speichern in anderen Formaten

Obwohl sich dieses Tutorial auf **save workbook as xlsx** konzentriert, unterstützt Aspose.Cells viele Formate (`.xls`, `.csv`, `.pdf`, usw.):

```csharp
workbook.Save("output.pdf", SaveFormat.Pdf);   // Export to PDF
workbook.Save("output.csv", SaveFormat.Csv);   // Export to CSV
```

## Profi‑Tipps und Fallstricke

* **Pro‑Tipp:** Setzen Sie `Workbook.Settings.CalcEngineEnabled = true`, wenn Sie die Formeln unmittelbar nach dem Speichern auswerten möchten.
* **Achtung:** Große Quellbereiche können sehr große Spill‑Bereiche erzeugen, was die Leistung beeinträchtigen kann. Begrenzen Sie die Bereichsgröße oder teilen Sie den Vorgang auf mehrere Arbeitsblätter auf.
* **Thread‑Sicherheit:** Aspose.Cells‑Objekte sind **nicht** thread‑sicher. Erstellen Sie für jeden Thread eine separate `Workbook`‑Instanz, wenn Sie Dateien parallel verarbeiten.

## Fazit

Sie wissen jetzt, **how to use WRAPCOLS** zu verwenden, um einen vertikalen Bereich in mehrere Spalten aufzuteilen, wie man **split range into rows** mit WRAPROWS durchführt und wie man **save workbook as XLSX** nach diesen Transformationen ausführt. Wenn Sie die obigen Schritte befolgen, können Sie **create excel workbook programmatically**, leistungsstarke Spill‑Formeln anwenden und sofort nutzbare Excel‑Dateien ohne manuelle Eingriffe erzeugen.

### Was kommt als Nächstes?

* Erkunden Sie **conditional formatting**, um die gespalteten Daten hervorzuheben.
* Kombinieren Sie **WRAPCOLS** mit **SORT** oder **FILTER** für dynamische Dashboards.
* Verwenden Sie Aspose.Cells’ **charting API**, um die umgeordneten Daten direkt aus dem Code zu visualisieren.

Viel Spaß beim Programmieren und beim Automatisieren Ihrer Excel‑Arbeitsabläufe!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man wrapcols in C# verwendet – Vollständiger Leitfaden mit Excel WRAPROWS & Formeln neu berechnen](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [Wie man WRAPCOLS in C# verwendet – Ein Array in eine Matrix in Excel umformen](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)
- [Wie man WRAPCOLS verwendet – Vollständiger Leitfaden für C# Excel‑Automatisierung](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}