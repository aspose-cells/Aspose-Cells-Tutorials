---
title: Diagramm rendern
linktitle: Diagramm rendern
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Entdecken Sie, wie Sie mit Aspose.Cells Diagramme in .NET rendern. Folgen Sie unserem Schritt-für-Schritt-Tutorial, um mühelos beeindruckende Visualisierungen zu erstellen.
weight: 10
url: /de/net/chart-rendering-and-conversion/render-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Diagramm rendern

## Einführung

Diagramme sind ein wesentliches Element bei der Datenpräsentation und -analyse, da sie komplexe Informationen leicht verständlich machen. Wenn Sie mit .NET arbeiten und Diagramme programmgesteuert erstellen müssen, ist Aspose.Cells eine leistungsstarke Bibliothek, die intuitive und erweiterte Funktionen für die Handhabung von Excel-Dateien und -Diagrammen bietet. In dieser Anleitung gehen wir den Prozess der Diagrammdarstellung mit Aspose.Cells für .NET durch. Machen Sie sich bereit für dieses ausführliche Tutorial, das spannend und leicht verständlich ist!

## Voraussetzungen

Bevor wir uns in den Code stürzen, stellen wir sicher, dass Sie alles bereit haben. Folgendes benötigen Sie:

1. .NET-Umgebung: Stellen Sie sicher, dass Sie eine .NET-Entwicklungsumgebung eingerichtet haben. Sie können Visual Studio oder jede andere IDE verwenden, die .NET unterstützt.
2.  Aspose.Cells für .NET: Sie müssen die Aspose.Cells-Bibliothek installiert haben. Sie können sie herunterladen von[Asposes Release-Seite](https://releases.aspose.com/cells/net/).
3. Grundlegende C#-Kenntnisse: Wenn Sie mit der C#-Programmierung vertraut sind, können Sie die Beispiele besser verstehen. Aber keine Sorge, wenn Sie noch neu sind – in diesem Handbuch wird alles Schritt für Schritt erklärt!

## Pakete importieren

Der erste Schritt auf Ihrer Programmierreise ist das Importieren der erforderlichen Pakete. Öffnen Sie Ihr Projekt in Ihrer IDE und fügen Sie den folgenden Namespace hinzu:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
```

Diese Namespaces bieten Ihnen Zugriff auf die von der Aspose.Cells-Bibliothek angebotenen Funktionen und ermöglichen Ihnen die nahtlose Erstellung und Bearbeitung Ihrer Diagramme.


Nachdem wir nun die Voraussetzungen und Importe behandelt haben, stürzen wir uns nun in die Einzelheiten der Diagrammdarstellung! Wir unterteilen es in klare, überschaubare Schritte.

## Schritt 1: Richten Sie Ihr Ausgabeverzeichnis ein

Bevor wir unsere Arbeitsmappe und unser Diagramm erstellen, müssen wir festlegen, wo unsere Ausgaben gespeichert werden. Auf diese Weise wissen Sie genau, wo Sie unser Diagramm finden, wenn es erstellt wird.

```csharp
string outputDir = "Your Output Directory"; // Geben Sie hier das Ausgabeverzeichnis an.
```

Ersetzen Sie „Ihr Ausgabeverzeichnis“ durch den Pfad, in dem Sie Ihre Diagrammbilder speichern möchten.

## Schritt 2: Erstellen Sie eine Arbeitsmappe

Als Nächstes richten wir eine neue Arbeitsmappe ein. Hier geschieht die ganze Magie!

```csharp
Workbook workbook = new Workbook();
```

 Diese Zeile erstellt eine neue Instanz des`Workbook` Klasse, die es uns ermöglicht, mit Blättern und Diagrammen zu arbeiten.

## Schritt 3: Neues Arbeitsblatt hinzufügen

Jetzt, da wir unsere Arbeitsmappe haben, ist es Zeit, ein neues Arbeitsblatt hinzuzufügen. Stellen Sie sich Arbeitsblätter als verschiedene Seiten in einem Notizbuch vor, auf denen Sie Ihre Daten organisieren können.

```csharp
int sheetIndex = workbook.Worksheets.Add();
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```

Hier fügen wir ein neues Arbeitsblatt hinzu und erhalten einen Verweis darauf. Sie werden mit diesem Arbeitsblatt arbeiten, um Ihre Daten und Diagramme einzugeben.

## Schritt 4: Beispielwerte eingeben

Nachdem wir unser Arbeitsblatt erstellt haben, fügen wir den Zellen einige Beispieldaten hinzu. Auf diesen Daten basiert Ihr Diagramm. Wählen Sie also Werte, die für Ihren Diagrammtyp sinnvoll sind!

```csharp
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```

In diesem Snippet füllen wir die Zellen „A1“ bis „A3“ mit einigen numerischen Werten und die Zellen „B1“ bis „B3“ mit einem anderen Wertesatz. Sie können diese Zahlen gerne an Ihre Bedürfnisse anpassen!

## Schritt 5: Erstellen Sie ein Diagramm

Jetzt ist es an der Zeit, Ihr Diagramm zu erstellen. Wir werden einen Säulendiagrammtyp hinzufügen, der sich hervorragend zum Vergleichen von Werten eignet.

```csharp
int chartIndex = worksheet.Charts.Add(ChartType.Column, 5, 0, 15, 5);
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

Hier fügen wir an der angegebenen Stelle ein Diagramm hinzu, indem wir sein Layout definieren: Die erste Zahlengruppe stellt die Position des Diagramms im Raster dar.

## Schritt 6: Datenreihen zum Diagramm hinzufügen

Nachdem das Diagramm erstellt wurde, müssen wir es nun an die Daten binden, die wir in den vorherigen Schritten eingegeben haben.

```csharp
chart.NSeries.Add("A1:B3", true);
```

Diese Linie verbindet die Datenreihe des Diagramms mit den Werten in den Zellen „A1“ bis „B3“. Das bedeutet, dass Ihr Diagramm die Daten wie vorgesehen visuell darstellt.

## Schritt 7: Speichern Sie das Diagramm als Bild

Konvertieren wir nun unser Diagramm in ein Bildformat, damit es problemlos geteilt und angezeigt werden kann.

```csharp
chart.ToImage(outputDir + "outputChartRendering.emf", System.Drawing.Imaging.ImageFormat.Emf);
```

In diesem Schritt speichern wir das Diagramm als EMF-Bild (Enhanced Metafile) im angegebenen Ausgabeverzeichnis. Sie können es auch in anderen Formaten wie BMP oder PNG speichern.

## Schritt 8: Diagramm in Bitmap konvertieren

Wenn Sie lieber mit Bitmaps arbeiten, erfahren Sie hier, wie Sie Ihr Diagramm in ein Bitmap-Format konvertieren.

```csharp
System.Drawing.Bitmap bitmap = chart.ToImage();
bitmap.Save(outputDir + "outputChartRendering.bmp", System.Drawing.Imaging.ImageFormat.Bmp);
```

Dadurch wird Ihr Diagramm als BMP-Bild gespeichert. Denken Sie daran, dass BMP-Dateien in der Regel größer sind, aber eine unglaublich hohe Qualität aufweisen!

## Schritt 9: Rendern mit erweiterten Optionen

Wir können das Diagramm auch mit einigen erweiterten Bildoptionen für eine bessere Qualität und Auflösung rendern. Lassen Sie uns ein paar Optionen einrichten:

```csharp
ImageOrPrintOptions options = new ImageOrPrintOptions()
{
    VerticalResolution = 300,
    HorizontalResolution = 300,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.AntiAlias
};
```

Diese Optionen tragen dazu bei, die visuelle Qualität des von Ihnen generierten Bildes zu verbessern, was besonders für Präsentationen oder Veröffentlichungen nützlich ist.

## Schritt 10: Diagramm mit erweiterten Optionen in Bild konvertieren

Lassen Sie uns nun das Diagramm mit den erweiterten Optionen konvertieren, die wir gerade festgelegt haben.

```csharp
chart.ToImage(outputDir + "outputChartRendering.png", options);
```

Dadurch wird Ihr Diagramm als PNG-Datei mit erweiterten Qualitätseinstellungen gespeichert.

## Schritt 11: Exportieren des Diagramms als PDF

Wenn Sie ein ansprechendes und leicht weiterzugebendes Dokument wünschen, können Sie Ihr Diagramm auch direkt in das PDF-Format exportieren.

```csharp
chart.ToPdf(outputDir + "outputChartRendering.pdf");
```

Mit diesem Schritt wird eine PDF-Datei erstellt, die Ihr Diagramm enthält. Sie eignet sich perfekt für digitale Berichte oder zum Teilen mit Kollegen.

## Abschluss 

Herzlichen Glückwunsch! Sie haben erfolgreich ein Diagramm mit Aspose.Cells für .NET gerendert. Diese leistungsstarke Bibliothek vereinfacht die Erstellung und Bearbeitung von Excel-Dateien und -Diagrammen und macht Ihre Daten viel zugänglicher und optisch ansprechender. Ob Sie Berichte, Analysen oder Präsentationen erstellen, Diagramme haben eine erhebliche Wirkung und mit Aspose können Sie sie problemlos programmgesteuert erstellen.

## Häufig gestellte Fragen

### Welche Diagrammtypen kann ich mit Aspose.Cells für .NET erstellen?
Sie können verschiedene Diagramme erstellen, darunter unter anderem Säulen-, Linien-, Kreis- und Balkendiagramme.

### Kann ich das Erscheinungsbild der Diagramme anpassen?
Ja, Aspose.Cells ermöglicht umfassende Anpassungen, einschließlich Farben, Stilen und Diagrammelementen.

### Gibt es eine kostenlose Testversion?
Auf jeden Fall! Sie können eine kostenlose Testversion herunterladen unter[Hier](https://releases.aspose.com/).

### Wo erhalte ich Support für Aspose.Cells?
 Community-Unterstützung und Ressourcen finden Sie unter[Aspose Support Forum](https://forum.aspose.com/c/cells/9).

### Benötige ich eine Lizenz, um Aspose.Cells zu verwenden?
 Ja, für die weitere Nutzung nach Ablauf der Testphase ist eine Lizenz erforderlich. Sie können jedoch eine temporäre Lizenz beantragen.[Hier](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
