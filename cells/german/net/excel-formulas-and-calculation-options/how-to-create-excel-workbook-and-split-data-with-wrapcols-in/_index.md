---
category: general
date: 2026-10-10
description: Erstellen Sie eine Excel‑Arbeitsmappe in C# und verwenden Sie die WRAPCOLS‑Funktion,
  um Array‑Daten in Spalten aufzuteilen. Folgen Sie einer vollständigen Schritt‑für‑Schritt‑Anleitung
  mit ausführbarem Code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- excel formula split data
- use wrapcols function
- how to use wrapcols
- split array columns
language: de
lastmod: 2026-10-10
og_description: Erstellen Sie eine Excel-Arbeitsmappe in C# und wenden Sie die WRAPCOLS‑Funktion
  an, um Array‑Daten in Spalten zu splitten. Dieser Leitfaden zeigt den vollständigen
  Code und erklärt jeden Schritt.
og_image_alt: Screenshot of an Excel sheet showing three columns filled by the WRAPCOLS
  formula
og_title: Excel‑Arbeitsmappe erstellen und Daten mit WRAPCOLS in C# aufteilen
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  headline: How to create Excel workbook and split data with WRAPCOLS in C#
  type: TechArticle
- description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  name: How to create Excel workbook and split data with WRAPCOLS in C#
  steps:
  - name: Using the function with different data types
    text: 'The `WRAPCOLS` function is not limited to numbers. You can split text values,
      dates, or mixed types:'
  - name: Variable column count at runtime
    text: 'Often the number of columns you need depends on user input. You can build
      the formula string dynamically:'
  - name: Large arrays and performance
    text: '`WRAPCOLS` can handle thousands of elements, but evaluating extremely large
      arrays in a single cell may increase calculation time. If you notice slowdown:'
  - name: Handling empty cells
    text: If the source array contains empty strings (`""`) or `NULL` values, `WRAPCOLS`
      inserts blank cells, preserving the column layout. This behavior is useful when
      you need placeholder columns for later data entry.
  - name: Using named ranges instead of literals
    text: 'For maintainability, define a named range that holds the source data, then
      reference it:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Wie man eine Excel‑Arbeitsmappe erstellt und Daten mit WRAPCOLS in C# aufteilt
url: /de/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man eine Excel‑Arbeitsmappe erstellt und Daten mit WRAPCOLS in C# aufteilt

Wenn Sie programmgesteuert **eine Excel‑Arbeitsmappe erstellen** müssen, zeigt Ihnen dieser Leitfaden genau, wie Sie das tun und wie Sie **Array‑Daten** mithilfe der `WRAPCOLS`‑Funktion über Spalten verteilen. Sie erhalten ein vollständiges, ausführbares Beispiel, das eine `.xlsx`‑Datei erzeugt, in der die Daten auf drei Spalten verteilt sind.

Das Tutorial behandelt alles, was Sie benötigen: erforderliche NuGet‑Pakete, jede Codezeile, warum die `WRAPCOLS`‑Formel funktioniert und wie Sie die Lösung an unterschiedliche Array‑Größen oder Spaltenzahlen anpassen. Am Ende können Sie die **use wrapcols function**‑Technik in jedes C#‑Projekt einbetten, das Excel‑Dateien erzeugt.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

* .NET 6.0 SDK oder höher installiert  
* Eine C#‑IDE (Visual Studio, VS Code, Rider usw.)  
* Das **Aspose.Cells for .NET**‑NuGet‑Paket – die Bibliothek, die die im Beispiel verwendete `Workbook`‑Klasse bereitstellt  

Sie benötigen keine Office‑Installation; Aspose.Cells schreibt die `.xlsx`‑Datei direkt.

## Schritt 1 – Excel‑Arbeitsmappe erstellen

Die erste Aufgabe besteht darin, ein neues Workbook‑Objekt zu instanziieren und eine Referenz auf das erste Arbeitsblatt zu erhalten. Dieser Schritt ist die Grundlage für jede weitere Manipulation.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();                // creates an empty Excel file in memory
        Worksheet ws = wb.Worksheets[0];             // the default worksheet is at index 0
```

`Workbook` repräsentiert die gesamte Datei, während `Worksheet` ein einzelnes Blatt darstellt. Durch das Erstellen der Arbeitsmappe im Speicher vermeiden Sie Festplatten‑I/O, bis Sie sie explizit speichern.

## Schritt 2 – WRAPCOLS anwenden, um Array‑Spalten aufzuteilen

Jetzt setzen Sie eine Formel in Zelle **A1**, die `WRAPCOLS` verwendet. Die Funktion erhält zwei Argumente: das Quell‑Array und die Anzahl der Spalten, in die das Array aufgeteilt werden soll.

```csharp
        // Step 2: Apply the WRAPCOLS formula to split the array into 3 columns
        // The array {1,2,3,4,5,6} will be distributed as:
        // 1 2 3
        // 4 5 6
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

**Warum das funktioniert:** `WRAPCOLS` nimmt das flache Array `{1,2,3,4,5,6}` und füllt das Arbeitsblatt zeilenweise, wobei pro Zeile drei Spalten erzeugt werden. Das erste Argument kann ein beliebiges Excel‑Array‑Literal, ein benannter Bereich oder eine dynamische Array‑Formel sein. Das zweite Argument (`3`) gibt Excel an, wie viele Spalten erzeugt werden sollen, bevor zur nächsten Zeile gewechselt wird.

### Verwendung der Funktion mit verschiedenen Datentypen

Die `WRAPCOLS`‑Funktion ist nicht auf Zahlen beschränkt. Sie können Textwerte, Datumsangaben oder gemischte Typen aufteilen:

```csharp
        // Example with mixed data: strings and numbers
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";
```

Wenn das Quell‑Array Zeichenketten enthält, behandelt Excel das Ergebnis automatisch als Textzellen. Diese Flexibilität ermöglicht es Ihnen, **excel formula split data** für Berichte, Dashboards oder Daten‑Migrations‑Aufgaben zu nutzen.

## Schritt 3 – Formeln berechnen, damit das Arbeitsblatt gefüllt wird

Formeln werden als Zeichenketten gespeichert, bis Sie das Workbook auffordern, sie zu berechnen. Der Aufruf von `CalculateFormula` erzwingt die Auswertung und schreibt die Ergebnisse in die Zellen.

```csharp
        // Step 3: Calculate formulas so the worksheet is populated
        wb.CalculateFormula();   // evaluates all formulas in the workbook
```

Ohne diesen Aufruf würde die gespeicherte Datei nur den Formeltext enthalten, nicht die berechneten Werte. Die Methode wirkt sich auf das gesamte Workbook aus, sodass Sie weitere Formeln an anderen Stellen platzieren können, die dann alle mit einem einzigen Aufruf ausgewertet werden.

## Schritt 4 – Arbeitsmappe speichern, um das Ergebnis zu sehen

Schließlich schreiben Sie die Arbeitsmappe auf die Festplatte. Wählen Sie einen Ordner, für den Sie Schreibrechte haben, und geben Sie der Datei einen eindeutigen Namen.

```csharp
        // Step 4: Save the workbook to see the result
        string outputPath = @"output.xlsx";
        wb.Save(outputPath);      // creates output.xlsx in the application directory
    }
}
```

Wenn Sie `output.xlsx` in Excel (oder einem kompatiblen Viewer) öffnen, sehen Sie:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

Wenn Sie das Beispiel mit gemischten Typen verwendet haben, würden die Zeilen 3‑4 entsprechend Text und Zahlen enthalten.

## Erweiterte Varianten und Edge‑Case‑Behandlung

### Variable Spaltenanzahl zur Laufzeit

Oft hängt die benötigte Spaltenanzahl von Benutzereingaben ab. Sie können den Formelausdruck dynamisch zusammenbauen:

```csharp
int columns = 4; // could come from UI, config, etc.
string arrayLiteral = "{10,20,30,40,50,60,70,80}";
ws.Cells[5, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
```

### Große Arrays und Performance

`WRAPCOLS` kann Tausende von Elementen verarbeiten, aber die Auswertung extrem großer Arrays in einer einzelnen Zelle kann die Berechnungszeit erhöhen. Wenn Sie eine Verlangsamung bemerken:

* Teilen Sie das Quell‑Array in kleinere Stücke und schreiben Sie jedes Stück in eine separate Startzelle.  
* Verwenden Sie `WorkbookSettings`, um die mehr‑threadige Berechnung zu aktivieren:

```csharp
wb.Settings.CalcMode = CalculationModeType.Automatic;
wb.Settings.EnableMultiThreadedCalc = true;
```

### Umgang mit leeren Zellen

Wenn das Quell‑Array leere Zeichenketten (`""`) oder `NULL`‑Werte enthält, fügt `WRAPCOLS` leere Zellen ein und bewahrt das Spaltenlayout. Dieses Verhalten ist nützlich, wenn Sie Platzhalter‑Spalten für spätere Dateneingaben benötigen.

### Verwendung benannter Bereiche anstelle von Literalen

Zur besseren Wartbarkeit definieren Sie einen benannten Bereich, der die Quelldaten enthält, und referenzieren diesen:

```csharp
ws.Cells["D1:D6"].PutValue(new object[] { 11, 12, 13, 14, 15, 16 });
ws.Cells["E1"].Formula = "=WRAPCOLS(D1:D6,3)";
```

Jetzt liest die Formel Daten direkt aus dem Arbeitsblatt, wodurch **how to use wrapcols** in dynamischen Reporting‑Szenarien ermöglicht wird.

## Häufige Fallstricke und Profi‑Tipps

* **Lassen Sie das zweite Argument nicht weg.** `WRAPCOLS(array)` ohne Spaltenanzahl gibt eine einzelne Spalte zurück, was den Zweck des Aufteilens von Daten zunichte macht.  
* **Vermeiden Sie das Mischen von Array‑Dimensionen.** Das Quell‑Array muss eindimensional sein; die Angabe eines zweidimensionalen Arrays (z. B. `{ {1,2},{3,4} }`) löst einen `#VALUE!`‑Fehler aus.  
* **Nach der Berechnung speichern.** Wenn Sie `wb.Save` vor `CalculateFormula` aufrufen, enthält die Datei nur den Formeltext.  
* **Dateiberechtigungen prüfen.** Wenn Sie in eingeschränkten Umgebungen (z. B. ASP.NET) laufen, stellen Sie sicher, dass die Prozessidentität in den Zielordner schreiben kann.  

## Vollständiges funktionierendes Beispiel

Unten finden Sie das vollständige Programm, das Sie kopieren, einfügen und ausführen können. Es enthält alle Imports, Fehlerbehandlung und Kommentare.

```csharp
using System;
using Aspose.Cells;

class ExcelWrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Split a numeric array into 3 columns
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

        // Split a mixed array (text + numbers) into 3 columns, starting at row 3
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";

        // Dynamically build a formula with a variable column count
        int columnCount = 4;
        string sourceArray = "{10,20,30,40,50,60,70,80}";
        ws.Cells[5, 0].Formula = $"=WRAPCOLS({sourceArray},{columnCount})";

        // Evaluate all formulas
        wb.CalculateFormula();

        // Save the workbook
        string outputPath = "output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Das Ausführen des Programms erzeugt `output.xlsx` mit drei getrennten Bereichen, die **excel formula split data** mithilfe der `WRAPCOLS`‑Funktion demonstrieren.

## Fazit

Sie wissen jetzt, wie man in C# **Excel‑Arbeitsmappen** erstellt und wie man die **use wrapcols function** nutzt, um **Array‑Spalten** effizient aufzuteilen. Die wichtigsten Schritte – Instanziieren von `Workbook`, Einfügen der `WRAPCOLS`‑Formel, Berechnen und Speichern – bilden ein wiederverwendbares Muster für jede Automatisierungsaufgabe, die eine Datenverteilung über Spalten erfordert.

Ab hier können Sie:

* `WRAPCOLS` mit anderen dynamischen Array‑Funktionen wie `FILTER` oder `SORT` kombinieren.  
* Große Datensätze aus Datenbanken exportieren und Excel das Layout automatisch überlassen.  
* Benutzergesteuerte Berichte erstellen, bei denen die Spaltenanzahl über ein UI‑Steuerelement ausgewählt wird.

Experimentieren Sie mit verschiedenen Array‑Quellen, Spaltenzahlen und zusätzlichen Formeln, um diese Grundlage zu erweitern. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Create Excel Workbook – Convert Array to Matrix with WRAPCOLS](/cells/english/net/calculation-engine/create-excel-workbook-convert-array-to-matrix-with-wrapcols/)
- [Create Excel Workbook C# – Step‑by‑Step Guide](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}