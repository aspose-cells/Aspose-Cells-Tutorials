---
category: general
date: 2026-10-01
description: Fügen Sie ein Diagramm in Word mit Aspose in nur wenigen Minuten hinzu.
  Lernen Sie, ein Excel‑Diagramm in Word einzubetten, Diagramme von Excel nach Word
  zu exportieren, ein Word‑Dokument mit Aspose zu erstellen und das Diagramm im Word‑Dokument
  zu speichern.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add chart to word
- embed excel chart word
- export chart excel word
- create word document aspose
- save chart word document
language: de
lastmod: 2026-10-01
og_description: Fügen Sie in wenigen Minuten ein Diagramm zu Word mit Aspose hinzu.
  Dieser Leitfaden zeigt, wie man ein Excel‑Diagramm in Word einbettet, ein Diagramm
  von Excel nach Word exportiert, ein Word‑Dokument mit Aspose erstellt und das Diagramm
  im Word‑Dokument speichert.
og_image_alt: Screenshot illustrating how to add chart to Word using Aspose
og_title: Diagramm in Word einfügen mit Aspose – Excel-Diagramm einbetten
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  headline: How to add chart to Word with Aspose – embed Excel chart
  type: TechArticle
- description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  name: How to add chart to Word with Aspose – embed Excel chart
  steps:
  - name: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
    text: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
  - name: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
    text: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
  - name: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
    text: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
  - name: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
    text: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
  - name: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
    text: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
  type: HowTo
tags:
- Aspose
- C#
- Word automation
title: Wie man ein Diagramm in Word mit Aspose hinzufügt – Excel‑Diagramm einbetten
url: /de/net/chart-rendering-and-conversion/how-to-add-chart-to-word-with-aspose-embed-excel-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ein Diagramm mit Aspose in Word einfügt – Excel‑Diagramm einbetten

Wenn Sie **ein Diagramm schnell zu Word hinzufügen** möchten, bietet dieses Tutorial eine komplette, sofort ausführbare Lösung. Sie sehen, wie Sie ein Excel‑Diagramm in eine Word‑Datei einbetten, das Diagramm von Excel nach Word exportieren und schließlich **das Word‑Dokument mit dem Diagramm speichern** – mit nur wenigen Zeilen C#.

Das Einbetten von Diagrammen ist ein häufiges Bedürfnis, wenn Sie Berichte, Rechnungen oder Dashboards programmgesteuert erzeugen. Am Ende dieses Leitfadens können Sie **ein Word‑Dokument mit Aspose** erstellen, das jedes Diagramm aus einer Excel‑Arbeitsmappe enthält, ohne manuelles Kopieren‑Einfügen.

## Voraussetzungen

- .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.7+)
- Aspose.Cells und Aspose.Words NuGet‑Pakete (Installation via `dotnet add package Aspose.Cells` und `dotnet add package Aspose.Words`)
- Eine vorhandene Excel‑Datei (`Chart.xlsx`), die mindestens ein Diagramm enthält
- Eine Entwicklungsumgebung wie Visual Studio 2022 oder VS Code

## Diagramm mit Aspose zu Word hinzufügen

Unten finden Sie das vollständige, eigenständige Programm. Kopieren Sie es in ein neues Konsolenprojekt, stellen Sie die Pakete wieder her und führen Sie es aus. Das Programm lädt die Excel‑Arbeitsmappe, erstellt ein Word‑Dokument, fügt das erste Diagramm ein und speichert das Ergebnis.

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

namespace AddChartToWordDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the Excel workbook that contains the chart
            var workbookPath = @"YOUR_DIRECTORY\Chart.xlsx";
            var workbook = new Workbook(workbookPath);

            // Step 2: Create a new Word document that will receive the chart
            var wordDoc = new Document();

            // Step 3: Initialise a DocumentBuilder for the Word document
            var builder = new DocumentBuilder(wordDoc);

            // Step 4: Insert the first chart from the first worksheet into the Word document
            // This uses Aspose.Words' InsertChart overload that accepts an Aspose.Cells chart object
            builder.InsertChart(workbook.Worksheets[0].Charts[0]);

            // Step 5: Save the resulting Word document
            var outputPath = @"YOUR_DIRECTORY\Chart.docx";
            wordDoc.Save(outputPath);

            Console.WriteLine($"Chart successfully added and saved to '{outputPath}'.");
        }
    }
}
```

### Warum jede Zeile wichtig ist

1. **Laden der Arbeitsmappe** – `Workbook` analysiert die Excel‑Datei und gibt Ihnen programmatischen Zugriff auf deren Arbeitsblätter und Diagramme.  
2. **Erstellen des Word‑Dokuments** – `Document` ist der Einstiegspunkt von Aspose.Words für jede Word‑Verarbeitungs‑Aufgabe.  
3. **DocumentBuilder** – Diese Hilfsklasse ermöglicht das Einfügen von Inhalten (Text, Bilder, Diagramme) an der aktuellen Cursor‑Position.  
4. **InsertChart** – Die Überladung, die ein `Aspose.Cells.Chart`‑Objekt akzeptiert, kopiert die Daten, Formatierung und Serien des Diagramms direkt in die Word‑Datei. Es ist keine Zwischenschritt‑Bildkonvertierung nötig, wodurch die Vektor‑Qualität erhalten bleibt.  
5. **Save** – `Save` schreibt das .docx‑Paket auf die Festplatte und schließt den Schritt **save chart word document** ab.

#### Erwartete Ausgabe

Nach dem Ausführen des Programms öffnen Sie `Chart.docx`. Sie sehen exakt das Diagramm, das in `Chart.xlsx` gespeichert war, an der Stelle, an der der Builder platziert wurde (der Anfang des Dokuments). Das Diagramm bleibt vollständig editierbar in Word (Sie können die Größe ändern, Farben anpassen oder die Datenquelle modifizieren).

## Excel‑Diagramm in Word einbetten

Wenn Sie mehr als ein Diagramm einbetten müssen, wiederholen Sie den Aufruf von `InsertChart` für jedes Diagramm‑Objekt. Beispiel: Alle Diagramme des ersten Arbeitsblatts einbetten:

```csharp
var sheet = workbook.Worksheets[0];
foreach (Chart chart in sheet.Charts)
{
    builder.InsertChart(chart);
    builder.Writeln(); // add a line break between charts
}
```

**Pro‑Tipp:** Verwenden Sie `builder.Writeln()`, um einen Absatzumbruch einzufügen, sodass jedes Diagramm in einer neuen Zeile beginnt.

## Diagramm Excel Word exportieren – mehrere Arbeitsblätter verarbeiten

Wenn Diagramme über mehrere Arbeitsblätter verteilt sind, iterieren Sie über die `Worksheets`‑Sammlung der Arbeitsmappe:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    foreach (Chart chart in ws.Charts)
    {
        builder.InsertChart(chart);
        builder.Writeln();
    }
}
```

Dieser Ansatz **export chart Excel Word** für jede Arbeitsmappen‑Struktur und macht die Lösung robust für komplexe Berichte.

## Word‑Dokument mit Aspose erstellen – Aussehen anpassen

Sie können Größe und Position jedes eingefügten Diagramms steuern, indem Sie das von `InsertChart` zurückgegebene `Shape` anpassen:

```csharp
Shape chartShape = builder.InsertChart(chart);
chartShape.Width = 500;   // width in points
chartShape.Height = 300;  // height in points
chartShape.WrapType = WrapType.Inline; // make the chart flow with text
```

Das Setzen von `WrapType` auf `Inline` sorgt dafür, dass sich das Diagramm wie ein normaler Absatz verhält – oft wünschenswert bei automatischer Dokumentenerstellung.

## Word‑Dokument mit Diagramm speichern – bewährte Methoden

- **Verwenden Sie einen aussagekräftigen Dateinamen** (`Report_Q1_2026.docx`), um die Versionsverwaltung zu erleichtern.
- **Objekte freigeben**, wenn Sie fertig sind, besonders bei großen Batch‑Prozessen:

```csharp
wordDoc.Dispose();
workbook.Dispose();
```

- **Ergebnis programmatisch validieren**, wenn Sie viele Dateien erzeugen:

```csharp
if (System.IO.File.Exists(outputPath))
{
    Console.WriteLine("File saved successfully.");
}
else
{
    Console.Error.WriteLine("Failed to save the document.");
}
```

## Häufige Fragen & Sonderfälle

| Frage | Antwort |
|----------|--------|
| *Kann ich ein Diagramm einfügen, das nicht das erste im Blatt ist?* | Ja. Greifen Sie über den Index zu: `sheet.Charts[2]` für das dritte Diagramm. |
| *Was, wenn das Excel‑Diagramm eine Datenquelle nutzt, die nicht in der Arbeitsmappe enthalten ist?* | Aspose.Cells bettet die Daten direkt in das Diagramm‑Objekt ein, sodass das Diagramm funktionsfähig bleibt, selbst wenn der Quellbereich entfernt wird. |
| *Benötige ich eine Lizenz für Aspose?* | Eine kostenlose Evaluation funktioniert, aber eine lizensierte Version entfernt das Evaluations‑Wasserzeichen und schaltet alle Funktionen frei. |
| *Ist das Diagramm nach dem Einfügen in Word editierbar?* | Das Diagramm wird als natives Word‑Diagramm eingefügt, sodass Benutzer Serien, Titel und Stile über die Word‑Benutzeroberfläche bearbeiten können. |
| *Wie füge ich ein Diagramm als Bild statt als natives Diagramm ein?* | Verwenden Sie `builder.InsertImage(chart.ToImage())`, um ein Raster‑Bild einzubetten. Das ist nützlich, wenn Sie die exakte visuelle Darstellung ohne Word‑seitige Editierbarkeit bewahren wollen. |

## Vollständiges funktionierendes Beispiel (copy‑paste)

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

class AddChartToWord
{
    static void Main()
    {
        // Load Excel workbook
        var wb = new Workbook(@"C:\Data\Chart.xlsx");

        // Create Word document
        var doc = new Document();
        var builder = new DocumentBuilder(doc);

        // Insert every chart from every worksheet
        foreach (Worksheet ws in wb.Worksheets)
        {
            foreach (Chart ch in ws.Charts)
            {
                Shape shape = builder.InsertChart(ch);
                shape.Width = 500;
                shape.Height = 300;
                builder.Writeln(); // separate charts
            }
        }

        // Save the document
        var outPath = @"C:\Data\ReportWithCharts.docx";
        doc.Save(outPath);
        Console.WriteLine($"Document saved to {outPath}");
    }
}
```

Das Ausführen des Codes erzeugt eine Word‑Datei (`ReportWithCharts.docx`), die **add chart to word** Ergebnisse für jedes Diagramm der Quell‑Arbeitsmappe enthält.

## Fazit

Sie wissen jetzt, wie Sie **ein Diagramm zu Word hinzufügen** mit Aspose.Cells und Aspose.Words, wie Sie **Excel‑Diagramm in Word einbetten**, **Diagramm Excel Word exportieren**, **Word‑Dokument mit Aspose erstellen** und schließlich **das Word‑Dokument mit Diagramm speichern**. Der Ansatz funktioniert sowohl für Ein‑Diagramm‑Szenarien als auch für komplexe Arbeitsmappen mit vielen Diagrammen über mehrere Arbeitsblätter hinweg.

Nächste Schritte, die Sie erkunden könnten:

- Anwenden benutzerdefinierter Stile auf die eingefügten Diagramme (Farben, Schriftarten) über die `Chart`‑API.
- Kombination des Diagrammeinfügens mit Textgenerierung, um vollständig automatisierte Berichte zu erzeugen.
- Verwendung von Aspose.Slides, falls Sie ...

## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [How to Save DOCX from Excel – Complete Guide to Export Charts to Word](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-docx-from-excel-complete-guide-to-export-charts/)
- [Create Excel Workbook with Pie Chart Using Aspose.Cells .NET - Comprehensive Guide](/cells/english/net/charts-graphs/create-excel-workbook-pie-chart-aspose-cells-net/)
- [Create a Bubble Chart in Excel Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/charts-graphs/create-bubble-chart-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}