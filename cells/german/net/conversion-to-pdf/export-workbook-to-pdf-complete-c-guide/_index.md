---
category: general
date: 2026-02-26
description: Exportiere die Arbeitsmappe als PDF mit eingebetteten Schriftarten und
  exportiere zudem Diagramme nach PowerPoint in C#. Lerne, ein Pivot‑Tabellen‑Arbeitsblatt
  zu kopieren und die Arbeitsmappe als PPTX zu speichern.
draft: false
keywords:
- export workbook to pdf
- export charts to powerpoint
- copy pivot table worksheet
- embed fonts pdf export
- save workbook as pptx
language: de
og_description: Exportiere die Arbeitsmappe als PDF mit eingebetteten Schriftarten
  und exportiere außerdem Diagramme nach PowerPoint in C#. Befolge die Schritt‑für‑Schritt‑Anleitung,
  um Pivot‑Tabellen zu kopieren und als PPTX zu speichern.
og_title: Arbeitsmappe als PDF exportieren – Vollständiger C#‑Leitfaden
tags:
- Aspose.Cells
- Aspose.Slides
- C#
- Reporting
title: Arbeitsmappe nach PDF exportieren – Vollständiger C#‑Leitfaden
url: /de/net/conversion-to-pdf/export-workbook-to-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Arbeitsmappe nach PDF exportieren – Vollständiger C# Leitfaden

Das Exportieren einer Arbeitsmappe nach PDF ist ein häufiges Anliegen, wenn Sie Berichte mit Stakeholdern teilen müssen, die möglicherweise kein Excel installiert haben. In diesem Tutorial zeigen wir Ihnen außerdem, wie Sie **Diagramme nach PowerPoint exportieren**, ein **Pivot‑Tabellen‑Arbeitsblatt kopieren** und Schriftarten einbetten, sodass das PDF genau wie Ihr Bildschirm‑Design aussieht.  

Haben Sie sich schon einmal gefragt, warum manche PDFs das ursprüngliche Layout verlieren oder warum PowerPoint‑Folien fehlende Formen aufweisen? Die Antwort liegt meist in fehlenden Optionen während des Exportvorgangs. Am Ende dieses Leitfadens besitzen Sie eine einzelne, wiederverwendbare C#‑Methode, die all diese Schmerzpunkte abdeckt – kein manuelles Kopieren‑Einfügen mehr und kein Herumfummeln an Export‑Einstellungen.

## Was Sie lernen werden

- Wie man eine Arbeitsmappe erstellt, Smart Marker‑Ausdrücke hinzufügt und verarbeitet.  
- Wie man ein **Pivot‑Tabellen‑Arbeitsblatt kopiert**, ohne die Datenquelle zu beschädigen.  
- Wie man **Diagramme, Formen und Textfelder** in eine PowerPoint‑Präsentation exportiert und dabei editierbar lässt.  
- Wie man **Standard‑Schriftarten** beim PDF‑Export einbettet, um eine konsistente Darstellung auf jedem Rechner zu gewährleisten.  
- Wie man die Arbeitsmappe **als PPTX speichert** mit dem Ansatz `save workbook as pptx`.  

All das funktioniert mit den neuesten Aspose.Cells‑ und Aspose.Slides .NET‑Bibliotheken (Version 23.11 zum Zeitpunkt des Schreibens). Keine externen Tools, keine Nachbearbeitungsskripte – nur reines C#.

> **Pro tip:** Wenn Sie Aspose bereits in Ihrem Projekt verwenden, können Sie die Code‑Snippets unverändert übernehmen; andernfalls fügen Sie zuerst die NuGet‑Pakete `Aspose.Cells` und `Aspose.Slides` hinzu.

## Voraussetzungen

- .NET 6.0 oder höher (der Code läuft auch unter .NET Framework 4.7.2).  
- Visual Studio 2022 (oder jede andere IDE Ihrer Wahl).  
- Aspose.Cells .NET und Aspose.Slides .NET über NuGet installiert.  
- Grundlegende Kenntnisse in C# und Excel‑Konzepten wie Smart Markers und PivotTables.

---

![Diagramm zum Exportieren einer Arbeitsmappe nach PDF](export-workbook-to-pdf.png "Workflow zum Exportieren einer Arbeitsmappe nach PDF, der PDF- und PPTX-Ausgaben zeigt")

## Arbeitsmappe nach PDF exportieren – Schritt‑für‑Schritt‑Implementierung

Im Folgenden finden Sie das vollständige, sofort ausführbare Beispiel. Es erstellt eine Arbeitsmappe, fügt Smart Marker‑Ausdrücke ein, verarbeitet sie, kopiert einen Pivot‑Tabellen‑Bereich und speichert schließlich sowohl eine PDF‑ als auch eine PowerPoint‑Datei.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides.Export;

namespace ReportExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Build the workbook and add Smart Markers
            // -------------------------------------------------
            var reportWorkbook = new Workbook();
            Worksheet dataSheet = reportWorkbook.Worksheets[0];

            // Header with a variable department name
            dataSheet.Cells["A1"].PutValue("Report for ${$dept=Department}");

            // Conditional text based on department
            dataSheet.Cells["A2"].PutValue("${if $dept == \"Sales\"}Sales Summary${else}Other Summary${/if}");

            // Table header for orders – this will be repeated for each order
            dataSheet.Cells["A5:D5"].PutValue("${Orders.Product}|${Orders.Quantity}|${Orders.Price}");

            // -------------------------------------------------
            // Step 2: Process Smart Markers and name the detail sheet
            // -------------------------------------------------
            reportWorkbook.SmartMarkerProcessor.Options.DetailSheetNewName = "Orders_${$dept}";
            reportWorkbook.SmartMarkerProcessor.Process();

            // -------------------------------------------------
            // Step 3: Copy the range that contains the pivot table
            // -------------------------------------------------
            // Assume the pivot table lives in A1:G30 on the original sheet
            Range sourceRange = dataSheet.Cells.CreateRange("A1", "G30");
            Worksheet copySheet = reportWorkbook.Worksheets.Add("Copy");
            sourceRange.Copy(copySheet.Cells["A1"]);   // Pivot table is duplicated intact

            // -------------------------------------------------
            // Step 4: Export to PowerPoint (keep charts, shapes, text boxes)
            // -------------------------------------------------
            var pptOptions = new PresentationOptions
            {
                ExportCharts = true,
                ExportShapes = true,
                ExportTextBoxes = true
            };
            string pptPath = @"C:\Temp\FinalPresentation.pptx";
            reportWorkbook.Save(pptPath, SaveFormat.Pptx, pptOptions);

            // -------------------------------------------------
            // Step 5: Export to PDF and embed standard fonts
            // -------------------------------------------------
            var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
            string pdfPath = @"C:\Temp\FinalReport.pdf";
            reportWorkbook.Save(pdfPath, pdfOptions);

            Console.WriteLine("Export completed:");
            Console.WriteLine($" • PDF saved to {pdfPath}");
            Console.WriteLine($" • PowerPoint saved to {pptPath}");
        }
    }
}
```

### Warum das funktioniert

1. **Smart‑Marker‑Verarbeitung** ermöglicht es, die Arbeitsmappe aus jeder Datenquelle (JSON, DataTables usw.) zu füllen, ohne Schleifen zu schreiben.  
2. **DetailSheetNewName** erstellt ein separates Blatt für jede Abteilung und liefert Ihnen einen sauberen, abteilungsspezifischen Tab.  
3. **Kopieren des Bereichs** (`sourceRange.Copy`) dupliziert die Pivot‑Tabelle *einschließlich* ihres Caches, sodass das kopierte Blatt sich exakt wie das Original verhält.  
4. **PresentationOptions** mit `ExportCharts`, `ExportShapes` und `ExportTextBoxes` weist Aspose an, diese Objekte als native PowerPoint‑Elemente zu rendern und die Editierbarkeit zu erhalten.  
5. **PdfSaveOptions.EmbedStandardFonts** sorgt dafür, dass das PDF auf Rechnern ohne die Original‑Schriftarten identisch aussieht.

Das Ergebnis sind zwei Dateien—`FinalReport.pdf` und `FinalPresentation.pptx`—die per E‑Mail, Archivierung oder in jedem Viewer angezeigt werden können, ohne an Qualität zu verlieren.

## Diagramme nach PowerPoint exportieren (Arbeitsmappe als PPTX speichern)

Wenn Ihr Bericht Diagramme enthält, möchten Sie diese wahrscheinlich editierbar in PowerPoint haben. Die Klasse `PresentationOptions` ist dabei der Schlüssel. Hier ein fokussierter Ausschnitt, der nur den Diagramm‑Export‑Teil zeigt:

```csharp
// Assuming reportWorkbook already contains charts
var pptExportOptions = new PresentationOptions
{
    ExportCharts = true,      // Convert Excel charts to PowerPoint chart objects
    ExportShapes = false,    // Skip shapes if you don’t need them
    ExportTextBoxes = true   // Keep any text boxes editable
};

string pptFile = @"C:\Temp\ChartsOnly.pptx";
reportWorkbook.Save(pptFile, SaveFormat.Pptx, pptExportOptions);
```

**Was passiert im Hintergrund?** Aspose übersetzt jedes Excel‑Diagramm in ein natives PowerPoint‑Diagramm, wobei Serien, Achsentitel und Formatierung erhalten bleiben. Das ist weitaus besser, als das Diagramm als statisches Bild zu exportieren, weil Ihr Publikum später Datenpunkte anpassen kann.

## Pivot‑Tabellen‑Arbeitsblatt kopieren, ohne Daten zu verlieren

Pivot‑Tabellen sind oft der kniffligste Teil eines Exports, weil sie auf einen versteckten Cache angewiesen sind. Die einfache `Copy`‑Methode funktioniert, weil Aspose sowohl den sichtbaren Bereich **als auch** das zugrunde liegende Cache‑Objekt kopiert.

```csharp
// Copy the whole sheet (including pivot table) to a new workbook
Workbook clone = new Workbook();
reportWorkbook.Worksheets[0].CopyTo(clone.Worksheets[0]);
clone.Save(@"C:\Temp\PivotCopy.xlsx", SaveFormat.Xlsx);
```

> **Hinweis:** Wenn Sie die Pivot‑Tabelle nur auf einem neuen Blatt innerhalb derselben Arbeitsmappe benötigen, ist der frühere Ansatz `sourceRange.Copy` leichter und vermeidet das Erstellen einer komplett neuen Arbeitsmappe.

## Schriftarten für den PDF‑Export einbetten – Warum das wichtig ist

Wenn Sie ein PDF auf einem Rechner öffnen, dem die Original‑Schriftarten fehlen, kann der Text verschoben werden, Zeilenumbrüche ändern sich oder Zeichen verschwinden. Das Setzen von `EmbedStandardFonts = true` weist Aspose an, die gängigsten Schriftarten (Arial, Times New Roman usw.) direkt in den PDF‑Stream einzubetten.

Verwenden Sie benutzerdefinierte Schriftarten, wechseln Sie zu `PdfSaveOptions.FontEmbeddingMode = FontEmbeddingMode.EmbedAll`. Hier ein Beispiel:

```csharp
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    FontEmbeddingMode = FontEmbeddingMode.EmbedAll   // For custom fonts
};
reportWorkbook.Save(@"C:\Temp\CustomFontReport.pdf", pdfOpts);
```

Jetzt sieht jeder Empfänger exakt das gleiche Layout, das Sie entworfen haben – keine Überraschungen.

## Zusammenfassung des vollständigen Beispielprogramms

Wenn man alles zusammenfügt, erledigt das komplette Programm (wie oben gezeigt) Folgendes:

1. **Erstellt** eine Arbeitsmappe mit Smart‑Marker‑Platzhaltern.  
2. **Verarbeitet** die Marker und erzeugt ein Detailblatt, das nach der Abteilung benannt ist.  
3. **Kopiert** einen Bereich, der eine Pivot‑Tabelle enthält, in ein neues Arbeitsblatt und bewahrt dessen Funktionalität.  
4. **Exportiert** die Arbeitsmappe nach PowerPoint und lässt Diagramme, Formen und Textfelder editierbar.  
5. **Exportiert** dieselbe Arbeitsmappe nach PDF und bettet Standard‑Schriftarten ein, um eine zuverlässige Darstellung zu gewährleisten.

Führen Sie das Programm aus, öffnen Sie die erzeugten Dateien, und Sie sehen:

- **PDF**: Scharfe Tabellen, eingebettete Schriftarten und derselbe visuelle Stil wie die Excel‑Quelle.  
- **PowerPoint**: Editierbare Diagramme, die Sie mit Rechtsklick → *Daten bearbeiten* in PowerPoint anpassen können, sowie Formen, die vollständig manipulierbar bleiben.

---

## Häufig gestellte Fragen (FAQ)

**F: Funktioniert das mit .NET Core?**  
Ja – Aspose.Cells und Aspose.Slides sind plattformübergreifend. Ziel‑Framework .NET 6 oder höher und derselbe Code läuft unter Windows, Linux oder macOS.

**F: Was, wenn ich nur einen Teil der Arbeitsblätter exportieren muss?**  
Verwenden Sie `Workbook.Save` mit `SaveOptions`, die Ihnen erlauben, `SheetNames` anzugeben. Beispiel: `new PresentationOptions { SheetNames = new[] { "Copy" } }`.

**F: Kann ich das PDF verschlüsseln?**  
Absolut. Setzen Sie `PdfSaveOptions.EncryptionDetails` mit einem Passwort, bevor Sie `Save` aufrufen.

**F: Meine Pivot‑Tabelle verwendet eine externe Datenquelle – wird das Kopieren die Verknüpfung brechen?**  
Der Kopiervorgang beinhaltet den Cache, nicht die externe Verbindung. Die Pivot‑Tabelle funktioniert offline weiter, wird jedoch nicht gegen die Original‑Quelle aktualisiert. Wenn Sie eine Live‑Aktualisierung benötigen, exportieren Sie die Quelldaten zusammen mit der Arbeitsmappe.

## Nächste Schritte & verwandte Themen

- **Dynamische Datenquellen** – Erfahren Sie, wie Sie JSON oder eine DataTable in Smart Markers für Echtzeit‑Berichte einspeisen.  
- **Erweiterte PDF‑Gestaltung** – Erkunden Sie `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}