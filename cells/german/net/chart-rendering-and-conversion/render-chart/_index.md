---
"description": "Entdecken Sie, wie Sie mit Aspose.Cells Diagramme in .NET rendern. Folgen Sie unserer Schritt-für-Schritt-Anleitung, um mühelos beeindruckende Visualisierungen zu erstellen."
"linktitle": "Diagramm rendern"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Diagramm rendern"
"url": "/de/net/chart-rendering-and-conversion/render-chart/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Diagramm rendern

## Einführung

Diagramme sind ein wesentliches Element der Datenpräsentation und -analyse und machen komplexe Informationen leicht verständlich. Wenn Sie mit .NET arbeiten und Diagramme programmgesteuert erstellen müssen, ist Aspose.Cells eine leistungsstarke Bibliothek mit intuitiven und erweiterten Funktionen für die Verarbeitung von Excel-Dateien und -Diagrammen. In dieser Anleitung führen wir Sie durch die Diagrammdarstellung mit Aspose.Cells für .NET. Tauchen Sie ein in dieses ausführliche Tutorial, das spannend und leicht verständlich ist!

## Voraussetzungen

Bevor wir mit dem Code beginnen, stellen wir sicher, dass Sie alles bereit haben. Folgendes benötigen Sie:

1. .NET-Umgebung: Stellen Sie sicher, dass Sie eine .NET-Entwicklungsumgebung eingerichtet haben. Sie können Visual Studio oder eine andere IDE verwenden, die .NET unterstützt.
2. Aspose.Cells für .NET: Sie benötigen die Aspose.Cells-Bibliothek. Sie können sie hier herunterladen: [Asposes Release-Seite](https://releases.aspose.com/cells/net/).
3. Grundlegende C#-Kenntnisse: Wenn Sie mit der C#-Programmierung vertraut sind, können Sie die Beispiele besser verstehen. Aber keine Sorge, wenn Sie noch neu sind – in diesem Handbuch wird alles Schritt für Schritt erklärt!

## Pakete importieren

Der erste Schritt beim Programmieren ist das Importieren der benötigten Pakete. Öffnen Sie Ihr Projekt in Ihrer IDE und fügen Sie den folgenden Namespace hinzu:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
```

Diese Namespaces bieten Ihnen Zugriff auf die von der Aspose.Cells-Bibliothek angebotenen Funktionen und ermöglichen Ihnen die nahtlose Erstellung und Bearbeitung Ihrer Diagramme.


Nachdem wir die Voraussetzungen und Importe besprochen haben, können wir uns nun mit den Details der Diagrammdarstellung befassen! Wir unterteilen dies in klare, überschaubare Schritte.

## Schritt 1: Richten Sie Ihr Ausgabeverzeichnis ein

Bevor wir unsere Arbeitsmappe und unser Diagramm erstellen, müssen wir festlegen, wo unsere Ausgaben gespeichert werden. So wissen Sie genau, wo sich das Diagramm befindet, wenn es erstellt wird.

```csharp
string outputDir = "Your Output Directory"; // Geben Sie hier das Ausgabeverzeichnis an.
```

Ersetzen Sie „Ihr Ausgabeverzeichnis“ durch den Pfad, in dem Sie Ihre Diagrammbilder speichern möchten.

## Schritt 2: Erstellen einer Arbeitsmappe

Als Nächstes erstellen wir eine neue Arbeitsmappe. Hier geschieht die ganze Magie!

```csharp
Workbook workbook = new Workbook();
```

Diese Zeile erstellt eine neue Instanz des `Workbook` Klasse, die es uns ermöglicht, mit Blättern und Diagrammen zu arbeiten.

## Schritt 3: Neues Arbeitsblatt hinzufügen

Nachdem wir nun unsere Arbeitsmappe erstellt haben, ist es an der Zeit, ein neues Arbeitsblatt hinzuzufügen. Stellen Sie sich Arbeitsblätter als verschiedene Seiten in einem Notizbuch vor, auf denen Sie Ihre Daten organisieren können.

```csharp
int sheetIndex = workbook.Worksheets.Add();
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```

Hier fügen wir ein neues Arbeitsblatt hinzu und erhalten einen Verweis darauf. Sie werden dieses Arbeitsblatt verwenden, um Ihre Daten und Diagramme einzugeben.

## Schritt 4: Beispielwerte eingeben

Nachdem wir unser Arbeitsblatt erstellt haben, fügen wir den Zellen einige Beispieldaten hinzu. Diese Daten bilden die Grundlage für Ihr Diagramm. Wählen Sie daher Werte, die für Ihren Diagrammtyp sinnvoll sind!

```csharp
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```

In diesem Snippet füllen wir die Zellen „A1“ bis „A3“ mit numerischen Werten und die Zellen „B1“ bis „B3“ mit anderen Werten. Sie können diese Zahlen gerne an Ihre Bedürfnisse anpassen!

## Schritt 5: Erstellen Sie ein Diagramm

Jetzt ist es an der Zeit, Ihr Diagramm zu erstellen. Wir werden ein Säulendiagramm hinzufügen, das sich hervorragend zum Vergleichen von Werten eignet.

```csharp
int chartIndex = worksheet.Charts.Add(ChartType.Column, 5, 0, 15, 5);
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

Hier fügen wir ein Diagramm an der angegebenen Stelle hinzu, indem wir sein Layout definieren: Die erste Zahlengruppe stellt die Position des Diagramms im Raster dar.

## Schritt 6: Datenreihen zum Diagramm hinzufügen

Nachdem das Diagramm erstellt wurde, müssen wir es nun an die Daten binden, die wir in den vorherigen Schritten eingegeben haben.

```csharp
chart.NSeries.Add("A1:B3", true);
```

Diese Linie verbindet die Datenreihe des Diagramms mit den Werten in den Zellen „A1“ bis „B3“. Dadurch werden die Daten in Ihrem Diagramm wie vorgesehen visuell dargestellt.

## Schritt 7: Speichern Sie das Diagramm als Bild

Konvertieren wir nun unser Diagramm in ein Bildformat, damit es einfach geteilt und angezeigt werden kann.

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

Dadurch wird Ihr Diagramm als BMP-Bild gespeichert. BMP-Dateien sind zwar in der Regel größer, bieten aber eine unglaublich hohe Qualität!

## Schritt 9: Rendern mit erweiterten Optionen

Wir können das Diagramm auch mit erweiterten Bildoptionen für eine bessere Qualität und Auflösung rendern. Lassen Sie uns einige Optionen einrichten:

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

Dadurch wird Ihr Diagramm als PNG-Datei mit verbesserten Qualitätseinstellungen gespeichert.

## Schritt 11: Exportieren des Diagramms als PDF

Wenn Sie ein ansprechendes und leicht weiterzugebendes Dokument wünschen, können Sie Ihr Diagramm direkt in das PDF-Format exportieren.

```csharp
chart.ToPdf(outputDir + "outputChartRendering.pdf");
```

In diesem Schritt wird eine PDF-Datei erstellt, die Ihr Diagramm enthält. Sie eignet sich daher ideal für digitale Berichte oder zum Teilen mit Kollegen.

## Abschluss 

Herzlichen Glückwunsch! Sie haben erfolgreich ein Diagramm mit Aspose.Cells für .NET erstellt. Diese leistungsstarke Bibliothek vereinfacht die Erstellung und Bearbeitung von Excel-Dateien und -Diagrammen und macht Ihre Daten deutlich zugänglicher und optisch ansprechender. Ob Berichte, Analysen oder Präsentationen – Diagramme haben eine große Wirkung. Mit Aspose können Sie sie ganz einfach programmgesteuert erstellen.

## Häufig gestellte Fragen

### Welche Diagrammtypen kann ich mit Aspose.Cells für .NET erstellen?
Sie können eine Vielzahl von Diagrammen erstellen, darunter unter anderem Säulen-, Linien-, Kreis- und Balkendiagramme.

### Kann ich das Erscheinungsbild der Diagramme anpassen?
Ja, Aspose.Cells ermöglicht umfassende Anpassungen, einschließlich Farben, Stilen und Diagrammelementen.

### Gibt es eine kostenlose Testversion?
Absolut! Sie können eine kostenlose Testversion herunterladen von [Hier](https://releases.aspose.com/).

### Wo erhalte ich Support für Aspose.Cells?
Community-Support und Ressourcen finden Sie unter [Aspose Support Forum](https://forum.aspose.com/c/cells/9).

### Benötige ich eine Lizenz, um Aspose.Cells zu verwenden?
Ja, für die weitere Nutzung nach der Testphase ist eine Lizenz erforderlich. Sie können jedoch eine temporäre Lizenz beantragen. [Hier](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}