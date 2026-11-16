---
category: general
date: 2026-11-16
description: Erfahren Sie, wie Sie ein Array in Excel mit Aspose.Cells, dynamischen
  Array‑Funktionen und einem Lambda‑Reducer erweitern und anschließend die Excel‑Datei
  aus C# schreiben.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- create excel workbook
- how to use lambda
- dynamic array functions
- write excel file
language: de
lastmod: 2026-11-16
og_description: Wie man ein Array in Excel mit Aspose.Cells, dynamischen Array‑Funktionen
  und einem Lambda‑Reducer erweitert. Folgen Sie dem vollständigen C#‑Beispiel, um
  die Excel‑Datei zu schreiben.
og_image_alt: Diagram illustrating how to expand array in an Excel worksheet
og_title: Wie man ein Array in Excel mit Aspose.Cells erweitert – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to expand array in Excel using Aspose.Cells, dynamic array
    functions, and a lambda reducer, then write the Excel file from C#.
  headline: How to expand array in Excel with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. `EXPAND` pads missing columns with blank cells. The same works for
      rows.
    question: Can I expand to more columns than the source provides?
  - answer: '`EXPAND` will treat the source as a single row; you can still specify
      rows and columns to reshape it.'
    question: What if the source array is horizontal (`{1,2,3,4,5}`)?
  - answer: The lambda must return a value compatible with the accumulator type. For
      text concatenation you could use `LAMBDA(acc, val, acc & val)`.
    question: Does `REDUCE` work with non‑numeric data?
  - answer: Only when you need the computed values before saving. Excel will recalculate
      on open if you skip it.
    question: Do I need to call `CalculateFormula` for every change?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: Wie man ein Array in Excel mit Aspose.Cells erweitert
url: /de/net/calculation-engine/how-to-expand-array-in-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ein Array in Excel mit Aspose.Cells erweitert

Wenn Sie **wie man ein Array erweitert** in einem Excel-Arbeitsblatt aus C# benötigen, zeigt dieses Tutorial die genauen Schritte. Sie erstellen eine Excel-Arbeitsmappe, verwenden dynamische Array‑Funktionen wie `EXPAND` und `REDUCE`, wenden einen **Lambda**‑Akkumulator an und schließlich **Excel‑Datei schreiben** auf die Festplatte. Der Ansatz funktioniert mit Aspose.Cells 23.10 oder neuer und erfordert keine manuelle Excel‑Installation.

Am Ende dieses Leitfadens haben Sie eine voll funktionsfähige `ExpandReduceDemo.xlsx`, die die Leistungsfähigkeit dynamischer Array‑Formeln in einem programmatischen Kontext demonstriert.

## Was Sie benötigen

- .NET 6.0 (oder jede von Aspose.Cells unterstützte .NET‑Version)
- Aspose.Cells für .NET‑Paket (`dotnet add package Aspose.Cells`)
- Ein Code‑Editor oder eine IDE (Visual Studio, VS Code, Rider usw.)

Keine zusätzliche COM‑Interop‑ oder Office‑Installation ist erforderlich, da Aspose.Cells das Dateiformat intern verarbeitet.

## Schritt 1: Excel‑Arbeitsmappe erstellen

Die erste Aufgabe besteht darin, **eine Excel‑Arbeitsmappe** im Speicher zu **erstellen**. Aspose.Cells stellt die Klasse `Workbook` bereit, die eine komplette XLSX‑Datei repräsentiert.

```csharp
using System;
using Aspose.Cells;

class ExpandReduceDemo
{
    static void Main()
    {
        // Step 1: instantiate a new workbook and get the default worksheet
        Workbook workbook = new Workbook();              // creates an empty .xlsx structure
        Worksheet sheet = workbook.Worksheets[0];        // the first (and only) sheet by default
```

> **Warum das wichtig ist:** Durch das Instanziieren eines `Workbook` erhalten Sie eine leere Leinwand. Das Standard‑Arbeitsblatt ist bereits vorbereitet, sodass Sie nicht manuell eines hinzufügen müssen, es sei denn, Sie benötigen mehrere Blätter.

## Schritt 2: Vertikale Array‑Konstante einfügen

Die dynamische Array‑Engine von Excel kann mit literalen Array‑Konstanten arbeiten. Wir platzieren das vertikale Array `{1;2;3;4;5}` in die Zelle **A1**.

```csharp
        // Step 2: put a vertical array constant into A1
        sheet.Cells["A1"].PutValue("{1;2;3;4;5}");
```

> **Tipp:** Das Semikolon (`;`) trennt Zeilen in der Konstante, während ein Komma (`,`) Spalten trennen würde. Das entspricht der Syntax von Excel.

## Schritt 3: Das Array in eine Matrix erweitern

Jetzt beantworten wir die Kernfrage – **wie man ein Array erweitert** – mithilfe der `EXPAND`‑Funktion. Die Formel erweitert das einspaltige Array zu einer 5‑Zeilen × 2‑Spalten‑Matrix, beginnend bei **B1**.

```csharp
        // Step 3: use EXPAND to create a 5‑row by 2‑column matrix
        sheet.Cells["B1"].Formula = "EXPAND(A1,5,2)";
```

> **Warum EXPAND?** `EXPAND(source, rows, cols)` zwingt den Quellbereich, die angegebene Größe einzunehmen, und füllt bei Bedarf mit leeren Zellen auf. Es ist die lesbarste Methode, um aus einem einzelnen Array eine größere Matrix zu erzeugen.

## Schritt 4: Die Matrix mit einem Lambda‑Akkumulator reduzieren

Die `REDUCE`‑Funktion iteriert über einen Bereich und aggregiert Werte mithilfe eines **Lambda**‑Ausdrucks. Hier summieren wir jeden Spaltenwert in einer einzelnen Spalte und platzieren das Ergebnis in **D1**.

```csharp
        // Step 4: REDUCE the expanded matrix using a lambda accumulator
        sheet.Cells["D1"].Formula = "REDUCE(A1, B1:E5, LAMBDA(acc, val, acc+val))";
```

> **Wie man Lambda verwendet:** Der `LAMBDA(acc, val, acc+val)` erhält den aktuellen Akkumulator (`acc`) und den nächsten Zellenwert (`val`). Er gibt den neuen Akkumulator zurück und führt damit eine laufende Summe aus. Dies demonstriert **wie man Lambda** in Excel‑Formeln aus dem Code verwendet.

## Schritt 5: Formeln berechnen, damit Ergebnisse erscheinen

Aspose.Cells wertet Formeln nicht automatisch aus, wenn Sie sie setzen. Der Aufruf von `CalculateFormula` zwingt die Engine, jede Formel in der Arbeitsmappe zu berechnen.

```csharp
        // Step 5: recalculate all formulas so the results are materialized
        workbook.CalculateFormula();
```

> **Hinweis:** Wenn Sie die erzeugte Datei in Excel öffnen, sind die Werte bereits sichtbar, da sie vorher berechnet wurden.

## Schritt 6: Excel‑Datei auf die Festplatte schreiben

Abschließend **schreiben Sie die Excel‑Datei** mit der `Save`‑Methode. Wählen Sie einen Ordner, für den Sie Schreibrechte besitzen.

```csharp
        // Step 6: save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\ExpandReduceDemo.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Erwartetes Ergebnis

| A | B | C | D |
|---|---|---|---|
| {1;2;3;4;5} | 1 |  | 15 |
|            | 2 |  |    |
|            | 3 |  |    |
|            | 4 |  |    |
|            | 5 |  |    |

- **Spalte B** und **C** enthalten die von `EXPAND` erzeugte 5 × 2‑Matrix.
- **Zelle D1** zeigt `15`, die Summe aller Zahlen, berechnet mit der `REDUCE` + **Lambda**‑Formel.

## Häufige Fragen und Sonderfälle

- **Kann ich auf mehr Spalten erweitern, als die Quelle bereitstellt?**  
  Ja. `EXPAND` füllt fehlende Spalten mit leeren Zellen auf. Das Gleiche gilt für Zeilen.

- **Was ist, wenn das Quell‑Array horizontal ist (`{1,2,3,4,5}`)?**  
  `EXPAND` behandelt die Quelle als einzelne Zeile; Sie können dennoch Zeilen und Spalten angeben, um sie umzuformen.

- **Funktioniert `REDUCE` mit nicht‑numerischen Daten?**  
  Das Lambda muss einen Wert zurückgeben, der mit dem Typ des Akkumulators kompatibel ist. Für die Textverkettung könnten Sie `LAMBDA(acc, val, acc & val)` verwenden.

- **Muss ich `CalculateFormula` bei jeder Änderung aufrufen?**  
  Nur wenn Sie die berechneten Werte vor dem Speichern benötigen. Excel wird beim Öffnen neu berechnen, wenn Sie es überspringen.

## Pro‑Tipps

- **Leistung:** Bei großen Arbeitsmappen rufen Sie `workbook.CalculateFormula` einmal nach dem Setzen aller Formeln auf, anstatt nach jeder Zelle.
- **Versionssicherheit:** `EXPAND` und `REDUCE` sind in Excel 365 und neueren Versionen verfügbar. Aspose.Cells implementiert sie unabhängig von der Ziel‑Excel‑Version, da die Berechnungs‑Engine integriert ist.
- **Formeln debuggen:** Verwenden Sie `sheet.Cells["B1"].Formula`, um die exakt gesetzte Zeichenkette auszulesen; das hilft beim dynamischen Aufbau von Formeln.

## Fazit

Sie wissen jetzt **wie man ein Array erweitert** in Excel mit Aspose.Cells, nutzen **dynamische Array‑Funktionen**, wenden ein **Lambda** mit `REDUCE` an und **schreiben eine Excel‑Datei** aus C#. Dieses End‑zu‑End‑Beispiel lässt sich an komplexere Daten­transformationen anpassen, wie Matrix‑Transposition, kumulative Summen oder benutzerdefinierte Aggregationen.

---

*Nächste Schritte:*  
- Erkunden Sie weitere dynamische Funktionen wie `FILTER`, `SORT` und `UNIQUE`.  
- Kombinieren Sie mehrere `LAMBDA`‑Ausdrücke, um wiederverwendbare benutzerdefinierte Funktionen zu erstellen.  
- Integrieren Sie die Arbeitsmappenerstellung in ASP.NET Core‑APIs für die sofortige Berichtserstellung.

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man eine Excel‑Arbeitsmappe in C# mit einer dynamischen Array‑Formel erstellt](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/)
- [Wie man ein Array in Excel erweitert und eine Vorlage füllt](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)
- [Wie man ein Array in C# mit Aspose.Cells erweitert – Schritt‑für‑Schritt‑Anleitung](/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}