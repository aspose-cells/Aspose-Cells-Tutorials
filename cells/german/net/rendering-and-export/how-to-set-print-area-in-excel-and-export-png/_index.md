---
category: general
date: 2026-09-27
description: Druckbereich in Excel festlegen und lernen, wie man PNG‑Bilder ausgewählter
  Zellen exportiert. Dieser Leitfaden behandelt außerdem das Speichern eines Bereichs
  als Bild und das Hinzufügen eines Bildes zum Arbeitsblatt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- how to export png
- save range as image
- add picture to worksheet
- export selected cells image
language: de
lastmod: 2026-09-27
og_description: Druckbereich in Excel festlegen und PNG mit Aspose.Cells exportieren.
  Folgen Sie dieser Schritt‑für‑Schritt‑Anleitung, um einen Bereich als Bild zu speichern
  und ein Bild in das Arbeitsblatt einzufügen.
og_image_alt: Screenshot showing set print area excel and exported PNG file
og_title: Druckbereich in Excel festlegen – PNG in C# exportieren
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Set print area in Excel and learn how to export PNG images of selected
    cells. This guide also covers saving range as image and adding picture to worksheet.
  headline: How to set print area in Excel and export PNG
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Wie man den Druckbereich in Excel festlegt und PNG exportiert
url: /de/net/rendering-and-export/how-to-set-print-area-in-excel-and-export-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man den Druckbereich in Excel festlegt und PNG exportiert

Wenn Sie **set print area excel** vor dem Erstellen eines Bildes festlegen müssen, zeigt Ihnen diese Anleitung genau, wie Sie das tun. Sie lernen außerdem, **how to export png**‑Dateien aus einem bestimmten Bereich zu exportieren, **save range as image** und **add picture to worksheet** in einem einzigen, wiederholbaren Workflow.

Die programmgesteuerte Arbeit mit Excel bedeutet oft, dass Sie nur einen Teil der Zellen – zum Beispiel eine Pivot‑Tabelle oder ein Diagramm – in ein Bild umwandeln möchten. Durch das vorherige Definieren eines Druckbereichs stellen Sie sicher, dass das exportierte PNG exakt die gewünschten Zellen enthält, nicht mehr und nicht weniger. Dieses Tutorial führt Sie Schritt für Schritt vom Laden der Arbeitsmappe bis zum Speichern der finalen PNG‑Datei und erklärt, warum jede Einstellung wichtig ist.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

* .NET 6.0 oder höher installiert  
* Visual Studio 2022 (oder jede C#‑IDE)  
* Das **Aspose.Cells for .NET** NuGet‑Paket (`Install-Package Aspose.Cells`)  
* Eine Excel‑Datei (`input.xlsx`) in einem bekannten Verzeichnis  

Diese Voraussetzungen stellen sicher, dass der Code ohne zusätzliche Konfiguration läuft.

## Schritt 1: Laden Sie die Arbeitsmappe, mit der Sie arbeiten möchten

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Load the workbook from disk
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

Die Klasse `Workbook` repräsentiert die gesamte Excel‑Datei. Das Laden zu Beginn gibt Ihnen Zugriff auf Arbeitsblätter, Zellen und Seiten‑Setup‑Optionen.

## Schritt 2: **Set print area excel** für den Zielbereich

```csharp
// Define the range you want to capture
string printArea = "A1:G20";

// Apply the range as the print area on the first worksheet
workbook.Worksheets[0].PageSetup.PrintArea = printArea;
```

Das Festlegen des **print area** teilt Excel (und Aspose.Cells) mit, welche Zellen zur druckbaren Seite gehören. Wenn Sie das Blatt später als Bild exportieren, wird nur dieser Bereich gerendert, was für ein sauberes **export selected cells image** entscheidend ist.

## Schritt 3: Bildexportoptionen konfigurieren – **how to export png**

```csharp
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG ensures lossless quality
    OnePagePerSheet = true           // Export the defined print area as a single page
};
```

`ImageOrPrintOptions` steuert das Ausgabeformat. Durch die Wahl von `ImageFormat.Png` erhalten Sie ein hochauflösendes Bild mit transparentem Hintergrund, das sowohl im Web als auch auf dem Desktop gut funktioniert.

## Schritt 4: Erstellen Sie ein Bild aus dem definierten Bereich und **add picture to worksheet**

```csharp
// Create a picture object from the selected range
Picture picture = workbook.Worksheets[0].Pictures.Add(
    0,                                     // top‑left row index where the picture will be placed
    0,                                     // top‑left column index where the picture will be placed
    workbook.Worksheets[0].Cells.CreateRange(printArea));
```

Die Methode `Pictures.Add` fügt ein neues Bild in das Arbeitsblatt ein. Indem Sie den in Schritt 2 erstellten Bereich übergeben, **save range as image** Sie direkt auf dem Blatt, was nützlich ist, wenn Sie das Bild später an anderer Stelle in der Arbeitsmappe referenzieren müssen.

## Schritt 5: **Save the picture as an image file** – Abschluss des **export selected cells image**‑Workflows

```csharp
// Save the picture to disk as a PNG file
picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);
```

Ein Aufruf von `Save` schreibt das Bild mit den in Schritt 3 definierten Optionen in das Dateisystem. Die resultierende Datei `selected_range.png` enthält exakt die Zellen, die durch den Befehl **set print area excel** festgelegt wurden.

## Vollständiges, ausführbares Beispiel

Wenn Sie alle Bausteine zusammenfügen, erhalten Sie ein kompaktes Programm, das Sie in jede Konsolenanwendung einbinden können:

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

class ExportExcelRangeAsPng
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Set print area excel
        string printArea = "A1:G20";
        workbook.Worksheets[0].PageSetup.PrintArea = printArea;

        // 3️⃣ Configure how to export png
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            OnePagePerSheet = true
        };

        // 4️⃣ Add picture to worksheet (save range as image)
        Picture picture = workbook.Worksheets[0].Pictures.Add(
            0,
            0,
            workbook.Worksheets[0].Cells.CreateRange(printArea));

        // 5️⃣ Export selected cells image
        picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);

        Console.WriteLine("PNG exported successfully to YOUR_DIRECTORY\\selected_range.png");
    }
}
```

### Erwartete Ausgabe

Beim Ausführen des Programms wird Folgendes ausgegeben:

```
PNG exported successfully to YOUR_DIRECTORY\selected_range.png
```

Und Sie finden eine Datei `selected_range.png`, die nur die Zellen A1 bis G20 aus `input.xlsx` zeigt.

## Häufige Fallstricke und wie man sie vermeidet

| Problem | Warum es passiert | Lösung |
|---------|-------------------|--------|
| Das exportierte Bild enthält das gesamte Blatt | Kein Druckbereich wurde definiert | Stellen Sie sicher, dass Sie **set print area excel** festlegen, bevor Sie das Bild erstellen |
| PNG ist unscharf | Standard‑DPI ist niedrig | Setzen Sie `imageOptions.DpiX` und `imageOptions.DpiY` auf einen höheren Wert (z. B. 300) |
| Datei‑nicht‑gefunden‑Fehler | Falscher Verzeichnispfad | Verwenden Sie `Path.Combine` oder prüfen Sie doppelt, ob der Ordner existiert |
| Bild erscheint versetzt | Falsche Zeilen‑/Spaltenindizes | Die ersten beiden Parameter von `Pictures.Add` sind die Zelle oben‑links, an der das Bild platziert wird; lassen Sie sie bei `0,0` für einen sauberen Export |

## Profi‑Tipp: Mehrere Bereiche in einem Durchlauf exportieren

Wenn Sie **export selected cells image** für mehrere Bereiche benötigen, wiederholen Sie die Schritte 2‑5 innerhalb einer Schleife und ändern Sie `printArea` bei jedem Durchlauf. Denken Sie daran, jedem Bild einen eindeutigen Dateinamen zu geben, sonst überschreibt ein späterer Save die vorherige Datei.

## Fazit

Sie wissen jetzt, wie Sie **set print area excel**, **how to export png**, **save range as image** und **add picture to worksheet** mit Aspose.Cells verwenden. Diese End‑zu‑End‑Lösung ermöglicht es Ihnen, jeden Zellblock mit nur wenigen Zeilen C#‑Code in ein hochwertiges PNG zu verwandeln.

Als Nächstes könnten Sie:

* Rahmen oder Wasserzeichen zum exportierten PNG hinzufügen (nach *add picture to worksheet* mit Styling suchen)  
* Direkt nach PDF exportieren für druckbare Berichte (*export selected cells image* → PDF‑Workflow)  
* Den Prozess für mehrere Arbeitsmappen in einem Batch‑Job automatisieren  

Experimentieren Sie gern mit unterschiedlichen Bereichen, DPI‑Einstellungen oder Bildformaten, um die Anforderungen Ihres Projekts zu erfüllen. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [Druckbereich in Excel festlegen und nach PowerPoint exportieren – Schritt‑für‑Schritt‑Anleitung](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Excel‑Druckbereich nach HTML exportieren mit Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-print-area-html-aspose-cells-java/)
- [Wie man einen Druckbereich in Excel mit Aspose.Cells für .NET festlegt](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}