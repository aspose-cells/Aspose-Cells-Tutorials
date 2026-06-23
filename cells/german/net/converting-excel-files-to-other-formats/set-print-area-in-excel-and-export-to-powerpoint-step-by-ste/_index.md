---
category: general
date: 2026-03-22
description: Druckbereich in Excel festlegen und Excel in PowerPoint mit editierbaren
  Formen konvertieren. Erfahren Sie, wie Sie die Titelzeile wiederholen, PowerPoint
  aus Excel erstellen und Excel nach PPTX exportieren.
draft: false
keywords:
- set print area
- convert excel to powerpoint
- repeat title row
- create powerpoint from excel
- export excel to pptx
language: de
og_description: Druckbereich in Excel festlegen und in eine PowerPoint‑Folie mit editierbaren
  Formen konvertieren. Folgen Sie dieser vollständigen Anleitung, um die Titelzeile
  zu wiederholen und Excel nach PPTX zu exportieren.
og_title: Druckbereich in Excel festlegen – Export nach PowerPoint Tutorial
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint generation
title: Druckbereich in Excel festlegen und nach PowerPoint exportieren – Schritt‑für‑Schritt‑Anleitung
url: /de/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Druckbereich in Excel festlegen und nach PowerPoint exportieren – Vollständiges Programmier‑Tutorial

Haben Sie schon einmal **den Druckbereich** in einem Excel‑Arbeitsblatt festlegen und diesen Ausschnitt dann in eine PowerPoint‑Folie umwandeln müssen? Sie sind nicht allein. In vielen Reporting‑Pipelines sollen dieselben Daten, die sich schön drucken lassen, auch in einer Präsentation erscheinen, oft mit der ersten Zeile als Titel wiederholt. Die gute Nachricht? Mit ein paar Zeilen C# können Sie **excel to powerpoint konvertieren**, alle Textfelder editierbar halten und sogar **die Titelzeile automatisch wiederholen**.

In diesem Leitfaden gehen wir Schritt für Schritt durch alles, was Sie wissen müssen: von der Konfiguration des Druckbereichs bis zur Erstellung einer PPTX‑Datei, die Sie direkt in PowerPoint bearbeiten können. Am Ende können Sie **powerpoint from excel erstellen**, das Ergebnis als **export excel to pptx** ausgeben und denselben Code in jedem .NET‑Projekt wiederverwenden. Kein Zauber, nur klare Schritte und ein vollständiges, ausführbares Beispiel.

## Was Sie benötigen

Bevor wir starten, stellen Sie sicher, dass Sie folgendes haben:

- **.NET 6.0** oder höher (die API funktioniert auch mit .NET Framework)
- **Aspose.Cells for .NET** (die Bibliothek, die `Workbook`, `ImageOrPrintOptions` usw. bereitstellt)
- Eine grundlegende C#‑IDE (Visual Studio, Rider oder VS Code mit der C#‑Erweiterung)
- Eine Excel‑Datei (`input.xlsx`), die die zu exportierenden Daten enthält

Das war’s – keine zusätzlichen NuGet‑Pakete außer Aspose.Cells. Falls Sie die Bibliothek noch nicht hinzugefügt haben, führen Sie aus:

```bash
dotnet add package Aspose.Cells
```

Jetzt können wir loslegen.

## Schritt 1: Arbeitsmappe laden – Ausgangspunkt für den Export

Das Erste, was Sie tun müssen, ist die Arbeitsmappe zu laden, die das Blatt enthält, das Sie in eine Folie umwandeln wollen. Denken Sie an die Arbeitsmappe als das Quelldokument; ohne sie ist nichts weiter von Bedeutung.

```csharp
using Aspose.Cells;

// Load the workbook that contains the shapes and data
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\input.xlsx");
```

**Warum das wichtig ist:** Das Laden der Arbeitsmappe gibt Ihnen Zugriff auf die Arbeitsblatt‑Sammlung, die Seiten‑Einrichtungs‑Optionen und die Export‑Engine. Wenn Sie diesen Schritt überspringen, können Sie weder den **Druckbereich** festlegen noch Zeilen wiederholen.

> **Pro‑Tipp:** Verwenden Sie während des Testens einen absoluten Pfad und wechseln Sie anschließend zu einem relativen Pfad oder einem konfigurationsbasierten Pfad für die Produktion.

## Schritt 2: Export‑Optionen konfigurieren – Textfelder und Formen editierbar halten

Beim Export nach PowerPoint möchten Sie wahrscheinlich, dass die resultierende Folie editierbar ist. Aspose.Cells lässt das mit `ImageOrPrintOptions` steuern. Wenn Sie `ExportTextBoxes` und `ExportShapeObjects` auf `true` setzen, bewahrt die Bibliothek diese Objekte als native PowerPoint‑Elemente, anstatt sie zu einem Bild zu flatten.

```csharp
// Configure export options for a PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // The target format – crucial for PowerPoint
    ExportTextBoxes = true,            // Keep text boxes editable
    ExportShapeObjects = true          // Keep shape objects editable
};
```

**Warum das wichtig ist:** Wenn Sie jemals **excel to powerpoint konvertieren** und dann die Folie manuell anpassen wollen, spart Ihnen diese Einstellung das mühsame Neuerstellen von Textfeldern. Außerdem bleiben alle Formen (wie Pfeile oder Diagramme) als Vektorobjekte erhalten, die Sie skalieren können.

## Schritt 3: Druckbereich festlegen und Titelzeile wiederholen

Jetzt kommen wir zum Kern des Tutorials: **Druckbereich festlegen** und die erste Zeile auf jeder gedruckten Seite (bzw. auf jeder exportierten Folie) wiederholen. Der Druckbereich sagt Excel, welche Zellen für den Druck – bzw. in unserem Fall für den Export – berücksichtigt werden sollen.

```csharp
// Define the area of the sheet to export (A1:G20)
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G20";

// Repeat the first row as a title on each printed page
sheet.PageSetup.PrintTitleRows = "$1:$1";
```

**Warum das wichtig ist:** Durch die Begrenzung des Exports auf `A1:G20` vermeiden Sie das Einbeziehen riesiger leerer Bereiche, was die Konvertierung beschleunigt und die Folie übersichtlich hält. Die Zeile `PrintTitleRows` lässt die erste Zeile wie eine Kopfzeile wirken – genau das, was Sie benötigen, wenn Sie **Titelzeile wiederholen** in einer Präsentation.

> **Randfall:** Beginnt Ihr Datenbereich in Zeile 2, passen Sie den Bereich entsprechend an (z. B. `PrintTitleRows = "$2:$2"`).

## Schritt 4: Arbeitsblatt als PowerPoint‑Datei speichern

Zum Schluss schreiben wir die Folie auf die Festplatte. Die `Save`‑Methode erhält den Ziel‑Dateinamen und die zuvor konfigurierten Optionen. Das Ergebnis ist eine PPTX‑Datei mit editierbaren Textfeldern und Formen, bereit zum Öffnen in PowerPoint.

```csharp
// Save the selected sheet as a PPTX file using the configured options
string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
workbook.Save(outputPath, exportOptions);
```

**Was Sie sehen werden:** Öffnen Sie `SheetWithEditableShapes.pptx` in PowerPoint. Die erste Zeile erscheint als Titel, alle Zellen von `A1:G20` werden gerendert, und alle Formen, die Sie in Excel hinzugefügt haben, bleiben verschieb‑ und editierbar. Keine gerasterten Bilder – nur native PowerPoint‑Objekte.

## Vollständiges funktionierendes Beispiel – Alle Schritte kombiniert

Unten finden Sie das komplette, copy‑paste‑bereite Programm. Führen Sie es als Konsolen‑App aus oder betten Sie es in eine größere Lösung ein.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the workbook
            string inputPath = @"C:\MyProjects\ExcelToPpt\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Set export options for editable PPTX
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportTextBoxes = true,
                ExportShapeObjects = true
            };

            // Step 3: Define print area and repeat title row
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G20";
            sheet.PageSetup.PrintTitleRows = "$1:$1";

            // Step 4: Save as PowerPoint
            string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
            workbook.Save(outputPath, exportOptions);

            Console.WriteLine($"Successfully exported to {outputPath}");
        }
    }
}
```

**Erwartete Ausgabe:** Nach dem Ausführen des Programms gibt die Konsole die Erfolgsmeldung aus und die PPTX‑Datei erscheint am angegebenen Ort. Beim Öffnen der Datei sehen Sie eine einzelne Folie mit dem ausgewählten Bereich, editierbaren Textfeldern und allen ursprünglichen Formen.

## Häufige Fragen & Stolperfallen

| Frage | Antwort |
|----------|--------|
| **Funktioniert das mit mehreren Arbeitsblättern?** | Ja. Durchlaufen Sie `workbook.Worksheets` und wiederholen Sie die gleichen Schritte für jedes Blatt, wobei Sie den Ausgabedateinamen jeweils anpassen. |
| **Was, wenn ich mehr als eine Folie exportieren muss?** | Rufen Sie `workbook.Save` mehrfach mit unterschiedlichen `ImageOrPrintOptions`‑Objekten auf, die ggf. unterschiedliche `PageSetup`‑Einstellungen haben. |
| **Kann ich die Foliengröße ändern?** | Verwenden Sie `exportOptions.ImageFormat`, um die DPI zu setzen, oder passen Sie `sheet.PageSetup.PaperSize` vor dem Speichern an. |
| **Ist Aspose.Cells kostenlos?** | Es gibt eine kostenlose Evaluierung mit Wasserzeichen. Für den Produktionseinsatz ist eine Lizenz erforderlich. |
| **Was ist mit Excel‑Formeln?** | Exportiert werden die **berechneten Ergebnisse** zum Zeitpunkt des Exports. Wenn Sie Live‑Formeln in PowerPoint benötigen, müssen Sie einen anderen Ansatz wählen. |

## Tipps für einen reibungslosen Workflow

- **Pro‑Tipp:** Setzen Sie `Workbook.Settings.CalcMode = CalculationModeType.Automatic` vor dem Export, um sicherzustellen, dass alle Formeln aktuell sind.
- **Achten Sie auf:** Sehr große Bereiche können zu Speicherbelastungen führen. Beschränken Sie den Druckbereich auf das kleinste notwendige Gebiet.
- **Performance‑Tipp:** Wiederverwenden Sie ein einzelnes `ImageOrPrintOptions`‑Objekt, wenn Sie viele Blätter exportieren; das Erzeugen eines neuen Objekts bei jedem Durchlauf verursacht zusätzlichen Overhead.
- **Versionshinweis:** Der obige Code zielt auf Aspose.Cells 23.10 (veröffentlicht November 2023). Neuere Versionen behalten dieselbe API bei, prüfen Sie jedoch immer die Release‑Notes auf mögliche Breaking Changes.

## Fazit

Wir haben gezeigt, wie man **den Druckbereich** in einem Excel‑Arbeitsblatt festlegt, die erste Zeile als Titel wiederholt und dann **excel to pptx exportiert**, wobei editierbare Textfelder und Formen erhalten bleiben. Kurz gesagt, Sie kennen jetzt einen zuverlässigen Weg, **excel to powerpoint zu konvertieren**, **Titelzeile zu wiederholen** und **powerpoint from excel zu erstellen** – mit nur wenigen Zeilen C#.

Bereit für den nächsten Schritt? Automatisieren Sie die Stapelkonvertierung Dutzender Berichte oder fügen Sie nach dem Export benutzerdefinierte Folien‑Layouts mit dem PowerPoint‑SDK hinzu. Der Himmel ist das Limit – experimentieren Sie, brechen Sie Dinge und genießen Sie die Macht der programmatischen Dokumentengenerierung.

Wenn Ihnen dieses Tutorial gefallen hat, teilen Sie es, hinterlassen Sie einen Kommentar mit Ihren eigenen Anpassungen oder entdecken Sie unsere anderen Anleitungen zu **export excel to pptx** und verwandten Automatisierungsthemen. Viel Spaß beim Coden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}