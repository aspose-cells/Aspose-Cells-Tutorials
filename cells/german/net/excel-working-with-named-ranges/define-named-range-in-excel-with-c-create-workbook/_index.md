---
category: general
date: 2026-08-07
description: Definieren Sie einen benannten Bereich in Excel mit C# und lernen Sie,
  wie Sie einer Arbeitsmappe eine Tabelle hinzufügen und die Arbeitsmappe anschließend
  programmgesteuert in einer Datei speichern.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- define named range excel
- save workbook to file
- add named range excel
- add table to worksheet
- create excel workbook programmatically
language: de
lastmod: 2026-08-07
og_description: Definieren Sie einen benannten Bereich in Excel mit C# und sehen Sie,
  wie Sie eine Tabelle hinzufügen, ein Arbeitsbuch programmgesteuert erstellen und
  das Arbeitsbuch in einem einzigen Ablauf in eine Datei speichern.
og_image_alt: Screenshot of C# code that creates an Excel workbook, adds a table,
  defines a named range, and saves the file
og_title: Benannten Bereich in Excel mit C# definieren – vollständiges Arbeitsmappen‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Define named range in Excel with C# and learn how to add a table to
    a worksheet, then save workbook to file programmatically.
  headline: Define named range in Excel with C# – create workbook
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- named range
- programmatic Excel
title: Benannten Bereich in Excel mit C# definieren – Arbeitsmappe erstellen
url: /de/net/excel-working-with-named-ranges/define-named-range-in-excel-with-c-create-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definieren eines benannten Bereichs in Excel mit C# – Arbeitsmappe erstellen

Wenn Sie **einen benannten Bereich in Excel** aus C#‑Code definieren müssen, zeigt Ihnen dieses Tutorial genau, wie das geht. Sie sehen außerdem, wie Sie **eine Tabelle zu einem Arbeitsblatt hinzufügen**, die Arbeitsmappe **programmgesteuert erstellen** und schließlich **die Arbeitsmappe in einer Datei speichern**, ohne die IDE zu verlassen.

Die programmgesteuerte Arbeit mit Excel‑Dateien spart Zeit, eliminiert manuelle Fehler und ermöglicht automatisierte Reporting‑Pipelines. In diesem Leitfaden werden Sie:

* Eine neue Excel‑Arbeitsmappe von Grund auf neu erstellen.  
* Eine Tabelle hinzufügen, die einen bestimmten Zellbereich umfasst.  
* Einen benannten Bereich definieren und Namenskonflikte behandeln.  
* Die Arbeitsmappe auf dem Datenträger persistieren.

Alle Schritte nutzen die **Aspose.Cells for .NET**‑Bibliothek, die mit .NET 6+ und .NET Framework 4.6+ funktioniert. Es ist keine zusätzliche COM‑Interop oder Office‑Installation erforderlich.

## Voraussetzungen

* .NET 6 SDK (oder .NET Framework 4.6+).  
* Visual Studio 2022 oder eine beliebige C#‑kompatible IDE.  
* Aspose.Cells for .NET NuGet‑Paket (`Install-Package Aspose.Cells`).  

> **Pro tip:** Verwenden Sie die kostenlose Evaluierungslizenz während des Testens; ersetzen Sie sie vor dem Deployment durch eine Produktionslizenz.

## Schritt 1: Excel‑Arbeitsmappe programmgesteuert erstellen

Der erste Vorgang besteht darin, ein `Workbook`‑Objekt zu instanziieren. Dieses Objekt repräsentiert die gesamte Excel‑Datei im Speicher.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook in memory
        Workbook workbook = new Workbook();               // create an empty workbook
        Worksheet worksheet = workbook.Worksheets[0];    // get the first (default) worksheet
```

*Warum das wichtig ist*: Das Erstellen der Arbeitsmappe im Code gibt Ihnen die volle Kontrolle über Tabellen, Stile und Daten, bevor irgendeine Datei die Festplatte berührt.

## Schritt 2: Tabelle zum Arbeitsblatt hinzufügen

Eine Tabelle (auch bekannt als ListObject) bietet integrierte Filter‑, Sortier‑ und Formatierungsfunktionen. Hier erstellen wir eine Tabelle, die die Zellen **A1:B5** abdeckt und ihr den Namen **SalesData** geben.

```csharp
        // Step 2: Define a range and convert it into a table
        Range tableRange = worksheet.Cells.CreateRange("A1:B5", true);
        ListObject table = worksheet.Tables[worksheet.Tables.Add(tableRange, true)];
        table.Name = "SalesData";

        // Populate the table with sample data
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Units");
        worksheet.Cells["A2"].PutValue("Apples");
        worksheet.Cells["B2"].PutValue(120);
        worksheet.Cells["A3"].PutValue("Bananas");
        worksheet.Cells["B3"].PutValue(85);
        worksheet.Cells["A4"].PutValue("Cherries");
        worksheet.Cells["B4"].PutValue(45);
        worksheet.Cells["A5"].PutValue("Dates");
        worksheet.Cells["B5"].PutValue(30);
```

*Warum das wichtig ist*: Das frühe Hinzufügen einer Tabelle ermöglicht es Ihnen, später mit einem **benannten Bereich** auf die Daten zu verweisen, und die strukturierte Referenz der Tabelle kann in Formeln verwendet werden.

## Schritt 3: Benannten Bereich in Excel definieren – Konflikte behandeln

Ein **benannter Bereich** ist ein Bezeichner, der auf eine Zelle oder einen Bereich zeigt und Formeln leichter lesbar macht. Wenn ein Name bereits existiert (z. B. der Tabellenname **SalesData**), wirft Excel einen Konflikt. Der nachfolgende Code zeigt, wie Sie diese Ausnahme abfangen und sicher fortfahren.

```csharp
        // Step 3: Attempt to define a named range with the same identifier as the table
        try
        {
            // This will raise an exception because "SalesData" is already used by the table
            worksheet.Names.Add("SalesData", "A1");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Name conflict prevented: " + ex.Message);
        }

        // Step 4: Add a different named range – this succeeds
        worksheet.Names.Add("SalesTotal", "B6");
        worksheet.Cells["B6"].Formula = "=SUM(SalesData[Units])";
```

*Warum das wichtig ist*: Das Behandeln von Namenskollisionen verhindert Laufzeitabstürze in automatisierten Jobs. Der zweite benannte Bereich **SalesTotal** demonstriert, wie man die Tabellenspalte in einer Formel referenziert.

## Schritt 4: Arbeitsmappe in Datei speichern

Nach allen Änderungen wird die Arbeitsmappe auf dem Datenträger persistiert. Die `Save`‑Methode unterstützt viele Formate; hier verwenden wir das Standard‑`.xlsx`.

```csharp
        // Step 5: Save the workbook to the file system
        string outputPath = @"C:\Temp\NameConflictHandled.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved successfully to {outputPath}");
    }
}
```

*Warum das wichtig ist*: Das programmgesteuerte **Speichern der Arbeitsmappe in einer Datei** ermöglicht Batch‑Verarbeitung, geplante Berichtserstellung und Integration mit Web‑APIs.

## Vollständiger Quellcode auf einen Blick

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Add a table covering A1:B5 and name it "SalesData"
        Range tableRange = worksheet.Cells.CreateRange("A1:B5", true);
        ListObject table = worksheet.Tables[worksheet.Tables.Add(tableRange, true)];
        table.Name = "SalesData";

        // Fill the table with sample data
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Units");
        worksheet.Cells["A2"].PutValue("Apples");   worksheet.Cells["B2"].PutValue(120);
        worksheet.Cells["A3"].PutValue("Bananas");  worksheet.Cells["B3"].PutValue(85);
        worksheet.Cells["A4"].PutValue("Cherries"); worksheet.Cells["B4"].PutValue(45);
        worksheet.Cells["A5"].PutValue("Dates");    worksheet.Cells["B5"].PutValue(30);

        // Try to create a defined name with the same identifier – handle the conflict
        try
        {
            worksheet.Names.Add("SalesData", "A1");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Name conflict prevented: " + ex.Message);
        }

        // Add a different defined name – this succeeds
        worksheet.Names.Add("SalesTotal", "B6");
        worksheet.Cells["B6"].Formula = "=SUM(SalesData[Units])";

        // Save the workbook
        string outputPath = @"C:\Temp\NameConflictHandled.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved successfully to {outputPath}");
    }
}
```

### Erwartetes Ergebnis

* Eine Excel‑Datei namens **NameConflictHandled.xlsx** erscheint in `C:\Temp`.  
* Blatt 1 enthält eine formatierte Tabelle **SalesData** mit Produkt‑Einheiten‑Zeilen.  
* Zelle **B6** zeigt die Summe der Spalte **Units**, berechnet über den benannten Bereich **SalesTotal**.  
* Die Konsole gibt eine Meldung zum Namenskonflikt (falls vorhanden) aus und bestätigt den Dateipfad.

## Häufige Fragen & Sonderfälle

| Frage | Antwort |
|----------|--------|
| **Kann ich einen benannten Bereich definieren, der mehrere Arbeitsblätter umfasst?** | Ja. Verwenden Sie `worksheet.Names.Add("GlobalRange", "'Sheet1'!A1:B5")` und referenzieren Sie ihn von jedem Blatt aus. |
| **Was ist, wenn ich eine vorhandene Datei überschreiben muss?** | Rufen Sie `workbook.Save(path, SaveFormat.Xlsx, new SaveOptions { Overwrite = true })` auf. |
| **Wie füge ich einen benannten Bereich ohne Konflikt hinzu, wenn der Name bereits existiert?** | Entfernen Sie den bestehenden Namen mit `worksheet.Names.Remove("ExistingName")`, bevor Sie den neuen hinzufügen, oder erzeugen Sie einen eindeutigen Bezeichner (z. B. `Guid.NewGuid().ToString("N")`). |
| **Gibt es eine Möglichkeit, automatisch einen Stil auf die Tabelle anzuwenden?** | Setzen Sie nach der Tabellenerstellung `table.Style = workbook.Styles[BuiltInStyleId.TableStyleMedium9];`. |
| **Funktioniert das unter .NET Core?** | Aspose.Cells unterstützt .NET Core, .NET 5/6/7 und .NET Framework. Binden Sie einfach dasselbe NuGet‑Paket ein. |

## Fazit

Sie wissen jetzt, wie Sie **einen benannten Bereich in Excel** mit C# definieren, **eine Tabelle zu einem Arbeitsblatt hinzufügen** und **die Arbeitsmappe programmgesteuert in einer Datei speichern**. Das vollständige Beispiel demonstriert das Erstellen einer Excel‑Arbeitsmappe von Grund auf, das Behandeln von Namenskonflikten und das Generieren einer nutzbaren Berichtdatei in einem einzigen, wiederholbaren Ablauf.

Als Nächstes können Sie verwandte Themen wie **Diagramme zu einem Arbeitsblatt hinzufügen**, **Export nach PDF** oder **Einlesen vorhandener Arbeitsmappen** erkunden. All diese bauen auf den hier behandelten Grundlagen auf, sodass Sie bereit sind, die Lösung auf komplexere Automatisierungsszenarien auszudehnen. Viel Spaß beim Coden!


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Create Named Range of Cells in Excel](/cells/english/net/excel-creating-formatting-named-ranges/create-named-range-of-cells/)
- [How to Implement Named Range Formulas in .NET using Aspose.Cells for Excel Automation](/cells/english/net/formulas-functions/implement-named-range-formulas-net-aspose-cells/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}