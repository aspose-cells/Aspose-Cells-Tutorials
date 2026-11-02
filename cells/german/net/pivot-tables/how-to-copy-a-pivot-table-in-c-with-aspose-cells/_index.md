---
category: general
date: 2026-09-27
description: Erfahren Sie, wie Sie eine Pivot‑Tabelle in C# mit Aspose.Cells kopieren.
  Enthält das Kopieren von Zeilen mit Formatierung, das Kopieren der Pivot‑Tabelle
  in ein anderes Blatt und das Exportieren der Pivot‑Tabelle in eine neue Arbeitsmappe.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy rows with formatting
- copy pivot table to another sheet
- how to copy excel rows
- export pivot table to new workbook
language: de
lastmod: 2026-09-27
og_description: Wie man eine Pivot‑Tabelle in C# mit Aspose.Cells kopiert. Folgen
  Sie der Schritt‑für‑Schritt‑Anleitung, um Zeilen mit Formatierung zu kopieren, eine
  Pivot‑Tabelle in ein anderes Blatt zu verschieben und sie in eine neue Arbeitsmappe
  zu exportieren.
og_image_alt: Excel sheet showing a copied pivot table after using Aspose.Cells
og_title: Wie man eine Pivot‑Tabelle in C# kopiert – vollständige Aspose.Cells‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to copy a pivot table in C# using Aspose.Cells. Includes
    copy rows with formatting, copy pivot table to another sheet, and export pivot
    table to a new workbook.
  headline: How to copy a pivot table in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot table
title: Wie man eine Pivot‑Tabelle in C# mit Aspose.Cells kopiert
url: /de/net/pivot-tables/how-to-copy-a-pivot-table-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man eine Pivot‑Tabelle in C# mit Aspose.Cells kopiert

Wenn Sie eine **Pivot‑Tabelle** von einem Arbeitsblatt zu einem anderen **kopieren** müssen, kann das Erlernen, **wie man Pivot‑Tabellen** in C# mit Aspose.Cells **kopiert**, Ihnen Stunden manueller Arbeit ersparen. Der Ansatz ermöglicht es Ihnen außerdem, **Zeilen mit Formatierung zu kopieren**, den Pivot‑Cache intakt zu halten und sogar **Pivot‑Tabelle in eine neue Arbeitsmappe zu exportieren**, wenn Sie eine eigenständige Datei benötigen.

Dieses Tutorial führt Sie durch den kompletten Workflow:

* ein Workbook erstellen,
* den Pivot‑Tabellen‑Bereich kopieren und dabei die Formatierung beibehalten,
* die kopierten Daten auf ein neues Blatt legen und
* das Ergebnis als separate Datei speichern.

Sie werden sehen, warum die eingebaute `CopyRows`‑Methode die zuverlässigste Methode ist, um **Pivot‑Tabellen in ein anderes Blatt zu kopieren**, und Sie erhalten Tipps zum Umgang mit Sonderfällen wie ausgeblendeten Zeilen oder externen Datenquellen.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| .NET 6.0 oder höher | Aspose.Cells unterstützt .NET 6+ und bietet die beste Leistung. |
| Visual Studio 2022 (oder jede C#‑IDE) | Sie benötigen einen Editor, der NuGet‑Pakete wiederherstellen kann. |
| Aspose.Cells für .NET (NuGet‑Paket `Aspose.Cells`) | Diese Bibliothek stellt die im Beispiel verwendete `CopyRows`‑API bereit. |
| Eine Quell‑Excel‑Datei (`source.xlsx`), die eine Pivot‑Tabelle im Bereich `A1:G20` enthält | Der Code kopiert diesen spezifischen Bereich; passen Sie den Bereich an, falls Ihre Pivot‑Tabelle größer ist. |

Installieren Sie die Bibliothek mit der NuGet‑CLI oder der Package Manager Console:

```bash
dotnet add package Aspose.Cells
```

## Schritt 1: Laden des Workbooks, das die Pivot‑Tabelle enthält

Die erste Zeile erstellt ein `Workbook`‑Objekt, das die gesamte Excel‑Datei repräsentiert. Das Laden der Datei einmal gibt Ihnen Lese‑/Schreibzugriff auf jedes Arbeitsblatt.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Warum dieser Schritt wichtig ist** – Ohne das Laden des Workbooks können keine der nachfolgenden `CopyRows`‑Aufrufe auf die Quelldaten oder den Pivot‑Cache zugreifen.

## Schritt 2: Quell‑ und Ziel‑Arbeitsblätter vorbereiten

Sie benötigen ein Ziel‑Blatt, in dem die kopierte Pivot‑Tabelle abgelegt wird. Der untenstehende Code holt das erste Arbeitsblatt (auf dem die ursprüngliche Pivot‑Tabelle liegt) und fügt ein neues Blatt mit dem Namen **Copy** hinzu.

```csharp
// Get the source worksheet (index 0 = first sheet)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a new worksheet that will receive the copied rows
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
```

> **Pro‑Tipp:** Wenn das Ziel‑Blatt bereits existiert, rufen Sie zuerst `Worksheets.RemoveAt(index)` auf, um doppelte Namen zu vermeiden.

## Schritt 3: Definieren des Zellbereichs, der die Pivot‑Tabelle umschließt

Ein `CellArea`‑Objekt beschreibt die Zelle oben‑links und unten‑rechts des Bereichs, den Sie verschieben möchten. In diesem Beispiel belegt die Pivot‑Tabelle `A1:G20`. Passen Sie die Koordinaten für größere Tabellen an.

```csharp
// Define the range that includes the pivot table (A1:G20)
CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");
```

## Schritt 4: Zeilen mit Formatierung kopieren und den Pivot‑Cache erhalten

Die `CopyRows`‑Methode kopiert **Zeilen** vom Quell‑Blatt zum Ziel‑Blatt. Durch das Übergeben von `CopyOptions.CopyAll` stellen Sie sicher, dass Werte, Formatierungen, Diagramme und eingebettete Objekte – all das, was zu einer Pivot‑Tabelle gehört – übertragen werden.

```csharp
// Copy the rows from the source area to the destination sheet
sourceSheet.CopyRows(
    sourceArea.StartRow,          // start row in the source sheet
    destinationSheet,            // target worksheet
    0,                            // start row in the destination sheet
    sourceArea.RowCount,          // number of rows to copy
    CopyOptions.CopyAll);        // copy everything (values, formats, objects, etc.)
```

### Warum `CopyRows` für Pivot‑Tabellen besser funktioniert als `Copy`

* `CopyRows` berücksichtigt den internen Pivot‑Cache, sodass die kopierte Pivot‑Tabelle funktionsfähig bleibt.
* Es bewahrt **Zeilen mit Formatierung** exakt so, wie sie im Originalblatt erscheinen.
* Im Gegensatz zu einem einfachen `Copy` eines Bereichs verschiebt es auch ausgeblendete Zeilen und zugehörige Slicer.

## Schritt 5: Das Workbook mit der kopierten Pivot‑Tabelle speichern

Schließlich schreiben Sie das modifizierte Workbook auf die Festplatte. Die neue Datei enthält das Originalblatt plus ein **Copy**‑Blatt, das ein voll funktionsfähiges Duplikat der ursprünglichen Pivot‑Tabelle enthält.

```csharp
// Save the workbook to a new file
workbook.Save(@"YOUR_DIRECTORY\pivot_copied.xlsx");
```

### Erwartetes Ergebnis

Wenn Sie `pivot_copied.xlsx` öffnen:

* Blatt **Sheet1** enthält weiterhin die Originaldaten und die Pivot‑Tabelle.
* Blatt **Copy** zeigt eine identische Pivot‑Tabelle mit demselben Layout, denselben Filtern und derselben Formatierung.
* Alle Formeln und Datenverbindungen bleiben erhalten, weil der Pivot‑Cache zusammen mit den Zeilen kopiert wurde.

## Wie man eine Pivot‑Tabelle in ein anderes Blatt derselben Arbeitsmappe kopiert

Wenn Sie die Pivot‑Tabelle nur in einem anderen vorhandenen Blatt benötigen (z. B. „Report“), ersetzen Sie den Schritt zur Erstellung des Zielblatts durch einen Verweis auf das Zielblatt:

```csharp
Worksheet destinationSheet = workbook.Worksheets["Report"]; // existing sheet
sourceSheet.CopyRows(sourceArea.StartRow, destinationSheet, 0,
                     sourceArea.RowCount, CopyOptions.CopyAll);
```

Dieses Snippet demonstriert **Pivot‑Tabelle in ein anderes Blatt kopieren** ohne ein neues Arbeitsblatt zu erstellen.

## Pivot‑Tabelle in neue Arbeitsmappe exportieren

Manchmal möchten Sie die Pivot‑Tabelle in einer völlig separaten Datei haben. Nach dem Kopiervorgang können Sie alle Arbeitsblätter außer demjenigen, das die kopierte Pivot‑Tabelle enthält, entfernen und dann speichern:

```csharp
// Keep only the copied sheet
for (int i = workbook.Worksheets.Count - 1; i >= 0; i--)
{
    if (workbook.Worksheets[i].Name != "Copy")
        workbook.Worksheets.RemoveAt(i);
}

// Save as a new workbook containing only the pivot table
workbook.Save(@"YOUR_DIRECTORY\pivot_only.xlsx");
```

Jetzt enthält `pivot_only.xlsx` ein einzelnes Blatt mit der duplizierten Pivot‑Tabelle und erfüllt die Anforderung **Pivot‑Tabelle in neue Arbeitsmappe exportieren**.

## Wie man Excel‑Zeilen kopiert, ohne die Formatierung zu verlieren

Der gleiche `CopyRows`‑Aufruf funktioniert für jeden Bereich, nicht nur für Pivot‑Tabellen. Wenn Sie **Excel‑Zeilen kopieren** müssen, die bedingte Formatierung, Datenvalidierung oder zusammengeführte Zellen enthalten, verwenden Sie dieselbe Methode:

```csharp
// Example: copy rows 30‑40 from Sheet1 to Sheet2
sourceSheet.CopyRows(29, // zero‑based index for row 30
                     workbook.Worksheets["Sheet2"],
                     0,
                     11, // rows 30‑40 = 11 rows
                     CopyOptions.CopyAll);
```

Da `CopyOptions.CopyAll` alles überträgt, sehen die Ziel‑Zeilen exakt wie die Quell‑Zeilen aus.

## Häufige Fallstricke und wie man sie vermeidet

| Fallstrick | Symptom | Lösung |
|------------|---------|--------|
| Quellbereich umfasst nicht die gesamte Pivot‑Tabelle | Die kopierte Pivot‑Tabelle erscheint abgeschnitten. | Stellen Sie sicher, dass `CellArea` alle Zeilen/Spalten der Pivot‑Tabelle abdeckt. |
| Zielblatt enthält bereits Daten | Überschriebene Zeilen führen zu Datenverlust. | Wählen Sie ein frisches Blatt oder beginnen Sie das Kopieren bei einem höheren Zeilenindex. |
| Pivot‑Tabelle verwendet eine externe Datenquelle | Die Kopie verliert ihre Verbindung. | Rufen Sie nach dem Kopieren `pivotTable.RefreshData()` auf, um die Verbindung wiederherzustellen. |
| Ausgeblendete Zeilen werden weggelassen | Einige Zeilen verschwinden in der Kopie. | `CopyRows` kopiert automatisch ausgeblendete Zeilen; stellen Sie sicher, dass Sie nicht `CopyOptions.CopyValuesOnly` verwenden. |

## Vollständiges, ausführbares Beispiel

Unten finden Sie ein eigenständiges Programm, das Sie in ein neues Konsolenprojekt einfügen können. Es demonstriert jeden der oben besprochenen Schritte.

```csharp
using System;
using Aspose.Cells;

namespace PivotTableCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains the pivot table
            string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2️⃣ Get source and destination worksheets
            Worksheet sourceSheet = workbook.Worksheets[0]; // first sheet
            Worksheet destinationSheet = workbook.Worksheets.Add("Copy");

            // 3️⃣ Define the cell area that holds the pivot table (A1:G20)
            CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");

            // 4️⃣ Copy rows with formatting and keep the pivot cache
            sourceSheet.CopyRows(
                sourceArea.StartRow,      // start row index (0‑based)
                destinationSheet,        // target sheet
                0,                        // start row in destination
                sourceArea.RowCount,      // number of rows to copy
                CopyOptions.CopyAll);    // copy everything

            // 5️⃣ Save the workbook with the copied pivot table
            string destPath = @"YOUR_DIRECTORY\pivot_copied.xlsx";
            workbook.Save(destPath);

            Console.WriteLine("Pivot table copied successfully to " + destPath);
        }
    }
}
```

**Ausführen des Programms** erstellt `pivot_copied.xlsx` mit einem Duplikat der ursprünglichen Pivot‑Tabelle auf einem neuen Blatt namens **Copy**.

## Fazit

Sie wissen jetzt, **wie man eine Pivot‑Tabelle** in C# kopiert, indem man

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Neues Workbook erstellen – Wie man ein Arbeitsblatt mit einer Pivot‑Tabelle kopiert](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Pivot‑Tabelle in C# kopieren – Vollständige Schritt‑für‑Schritt‑Anleitung](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [Wie man einen Bereich mit Pivot‑Tabellen in C# kopiert – Vollständiger Leitfaden](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}