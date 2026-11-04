---
category: general
date: 2026-10-20
description: Erfahren Sie, wie Sie wrapcols in Aspose.Cells verwenden, Schriftarten
  in HTML einbetten und Excel als HTML mit einem vollständigen C#‑Beispiel speichern.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- embed fonts in html
- save excel as html
- convert workbook to html
- use wrapcols function
language: de
lastmod: 2026-10-20
og_description: Wie man wrapcols in Aspose.Cells verwendet, Schriftarten in HTML einbettet
  und ein Arbeitsbuch in HTML konvertiert – ein klarer C#‑Leitfaden für Entwickler.
og_image_alt: Screenshot of an Excel workbook saved as HTML with embedded fonts using
  Aspose.Cells
og_title: Wie man wrapcols verwendet und Schriftarten beim Exportieren von Excel nach
  HTML einbettet
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to use wrapcols in Aspose.Cells, embed fonts in HTML, and
    save Excel as HTML with a complete C# example.
  headline: How to use wrapcols and embed fonts saving Excel to HTML
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel to HTML
- Smart Markers
title: Wie man Wrapcols verwendet und Schriftarten einbettet, wenn man Excel nach
  HTML speichert
url: /de/net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man wrapcols verwendet und Schriftarten beim Speichern von Excel als HTML einbettet

Wenn Sie **how to use wrapcols** in einer Aspose.Cells‑Formel benötigen, zeigt Ihnen dieser Leitfaden die genauen Schritte. Sie lernen außerdem, wie man **Schriftarten in HTML einbettet** und **Excel als HTML speichert**, sodass die Ausgabe in allen Browsern identisch aussieht.  

Das Tutorial behandelt drei praktische Szenarien: die Verwendung der `WRAPCOLS`‑Funktion, das Exportieren einer Arbeitsmappe mit eingebetteten Schriftarten und das Erzeugen eines Master‑Detail‑Berichts mit Smart Markers. Am Ende haben Sie ein einzelnes, ausführbares C#‑Programm, das all diese Funktionen demonstriert.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie:

* .NET 6.0 (oder neuer) installiert.
* Aspose.Cells für .NET zu Ihrem Projekt hinzugefügt (`dotnet add package Aspose.Cells`).
* Grundlegende Kenntnisse in C# und Excel‑Formeln.

Es sind keine zusätzlichen Drittanbieter‑Bibliotheken erforderlich; Aspose.Cells übernimmt die HTML‑Konvertierung und das Einbetten von Schriftarten intern.

## Schritt 1: Demonstration der **how to use wrapcols**‑Funktion in einer Formel

Die `WRAPCOLS`‑Funktion teilt einen eindimensionalen Bereich in ein zweidimensionales Array auf und füllt dabei zuerst die Spalten. Das ist nützlich, wenn Sie Daten für Berichte oder Diagramme umstrukturieren müssen.

```csharp
using Aspose.Cells;
using System;

class WrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Populate a vertical range A1:A3
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // Apply WRAPCOLS(A1:A3, 2) – this creates a 2‑column array {1,2}
        sheet.Cells["B1"].Formula = "=WRAPCOLS(A1:A3, 2)";

        // Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // Output the result to verify the function works
        Console.WriteLine("Result of WRAPCOLS: " + sheet.Cells["B1"].Value);
        // Expected output: Result of WRAPCOLS: 1
    }
}
```

**Warum das funktioniert:**  
`WRAPCOLS` nimmt zwei Argumente – den Quellbereich und die Anzahl der Spalten. Die Funktion füllt das Array spaltenweise und verwirft überschüssige Werte (die `3` im Beispiel). Das Ergebnis erscheint in der oberen linken Zelle des Zielbereichs (`B1`), und Sie können den Bereich manuell erweitern, wenn Sie das gesamte Array benötigen.

> **Pro‑Tipp:** Nachdem Sie die Formel gesetzt haben, rufen Sie `workbook.CalculateFormula()` auf, um sicherzustellen, dass das Ergebnis aktuell ist, bevor Sie Zellwerte auslesen.

## Schritt 2: **Arbeitsmappe in HTML konvertieren** und **Schriftarten in HTML einbetten**

Wenn Sie eine Excel‑Datei nach HTML exportieren, werden Schriftarten häufig durch die Standard‑Schriftarten des Browsers ersetzt, was das visuelle Layout zerstören kann. Aspose.Cells ermöglicht es Ihnen, die tatsächlich in der Arbeitsmappe verwendeten Schriftarten direkt in die HTML‑Datei einzubetten.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for HtmlSaveOptions
using System;

class HtmlExportDemo
{
    static void Main()
    {
        // Re‑use the workbook from the previous step
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue("Hello");
        sheet.Cells["A2"].PutValue("World");

        // Configure HTML save options
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Embedding fonts ensures the output looks the same on any device
            EmbedFonts = true,
            // Optional: specify a folder for supporting files (images, CSS)
            ExportEmbeddedImages = true
        };

        // Save the workbook as an HTML file with embedded fonts
        string outputPath = @"C:\Temp\WorkbookWithFonts.html";
        workbook.Save(outputPath, htmlOptions);

        Console.WriteLine($"Workbook saved to HTML with embedded fonts at: {outputPath}");
    }
}
```

**Warum das Einbetten von Schriftarten wichtig ist:**  
Wenn `EmbedFonts` auf `true` gesetzt ist, konvertiert Aspose.Cells jede verwendete TrueType/OpenType‑Schriftart in eine Base64‑codierte `@font-face`‑Regel innerhalb des erzeugten HTML. Dadurch muss die Client‑Maschine die gleichen Schriftarten nicht installiert haben, was ein pixelgenaues Rendering garantiert.

> **Sonderfall:** Wenn die Quell‑Arbeitsmappe eine Schriftart referenziert, die auf dem Server nicht installiert ist, greift Aspose.Cells auf eine Standardschriftart zurück und gibt eine Warnung aus. Stellen Sie sicher, dass die benötigten Schriftarten verfügbar sind.

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man WRAPCOLS in C# verwendet – Excel‑Arbeitsmappe mit Wrap‑Funktionen erstellen](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Wie man Schriftarten in HTML einbettet – Excel nach HTML mit C# konvertieren](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/)
- [Wie man Excel‑Dateien mit Aspose.Cells für .NET in HTML konvertiert: Überlagerte Inhalte ausblenden](/cells/english/net/workbook-operations/excel-to-html-hide-overlaid-content-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}