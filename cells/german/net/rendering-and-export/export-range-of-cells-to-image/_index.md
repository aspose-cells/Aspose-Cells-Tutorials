---
"description": "Exportieren Sie Excel-Zellbereiche mit Aspose.Cells für .NET ganz einfach in Bilder. Optimieren Sie Ihre Berichte und Präsentationen."
"linktitle": "Exportieren Sie Zellbereiche mit Aspose.Cells in ein Bild"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Exportieren Sie Zellbereiche mit Aspose.Cells in ein Bild"
"url": "/de/net/rendering-and-export/export-range-of-cells-to-image/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Exportieren Sie Zellbereiche mit Aspose.Cells in ein Bild

## Einführung
Bei der Arbeit mit Excel-Dateien ist die Möglichkeit, bestimmte Zellbereiche in Bilder umzuwandeln, äußerst nützlich. Stellen Sie sich vor, Sie müssen einen wichtigen Teil Ihrer Tabelle freigeben, ohne das gesamte Dokument zu senden – hier kommt Aspose.Cells für .NET ins Spiel! In dieser Anleitung führen wir Sie Schritt für Schritt durch den Export eines Zellbereichs in ein Bild und stellen sicher, dass Sie jeden Teil des Prozesses ohne technische Hürden meistern.
## Voraussetzungen
Bevor Sie mit dem Lernprogramm beginnen, müssen Sie einige Voraussetzungen erfüllen, um sicherzustellen, dass Sie alles richtig eingerichtet haben:
1. Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem System installiert ist.
2. Aspose.Cells für .NET: Laden Sie diese Bibliothek herunter von der [Aspose-Site](https://releases.aspose.com/cells/net/)Sie können auch eine kostenlose Testversion starten, wenn Sie die Funktionen vor der Verpflichtung erkunden möchten.
3. Grundlegende C#-Kenntnisse: Wenn Sie mit C# und dem .NET-Framework vertraut sind, verstehen Sie den Code besser.
4. Eine Beispiel-Excel-Datei: Für dieses Tutorial verwenden wir eine Datei namens `sampleExportRangeOfCellsInWorksheetToImage.xlsx`Sie können zu Testzwecken eine einfache Excel-Datei erstellen.
Nachdem wir nun die Voraussetzungen abgedeckt haben, können wir direkt mit dem Code beginnen!
## Pakete importieren
Zunächst müssen wir die erforderlichen Namespaces importieren. So geht's:
```csharp
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Rendering;
using System;
```
Mit diesen Paketen können wir mit Arbeitsmappen und Arbeitsblättern arbeiten und die Darstellung unserer Zellbereiche verwalten.
## Schritt 1: Richten Sie Ihre Verzeichnispfade ein
Das Einrichten von Verzeichnissen mag banal erscheinen, ist aber äußerst wichtig. Dieser Schritt stellt sicher, dass Ihr Programm weiß, wo die Dateien zu finden sind und wo die exportierten Bilder gespeichert werden sollen.
```csharp
// Quellverzeichnis
string sourceDir = "Your Document Directory";
// Ausgabeverzeichnis
string outputDir = "Your Document Directory";
```
Ersetzen `"Your Document Directory"` mit dem tatsächlichen Pfad, in dem sich Ihre Dateien befinden. Dies kann ein Pfad auf Ihrem lokalen Laufwerk oder einem Netzwerkverzeichnis sein.
## Schritt 2: Erstellen einer Arbeitsmappe aus der Quelldatei
Der nächste Schritt besteht darin, eine `Workbook` Objekt, das als Einstiegspunkt in die Excel-Datei dient.
```csharp
// Arbeitsmappe aus Quelldatei erstellen.
Workbook workbook = new Workbook(sourceDir + "sampleExportRangeOfCellsInWorksheetToImage.xlsx");
```
Hier erstellen wir ein neues `Workbook` Geben Sie beispielsweise den vollständigen Pfad der Excel-Datei an, mit der Sie arbeiten möchten. In diesem Schritt wird die Datei geöffnet und für die Bearbeitung vorbereitet.
## Schritt 3: Zugriff auf das erste Arbeitsblatt
Sobald wir unsere Arbeitsmappe haben, müssen wir auf das Arbeitsblatt zugreifen, das die Daten enthält, die wir exportieren möchten.
```csharp
// Greifen Sie auf das erste Arbeitsblatt zu
Worksheet worksheet = workbook.Worksheets[0];
```
Der `Worksheets` Sammlung ist 0-indiziert, was bedeutet, dass `Worksheets[0]` gibt uns das erste Blatt. Sie können den Index anpassen, wenn Sie ein anderes Blatt wünschen.
## Schritt 4: Druckbereich festlegen
Als nächstes müssen wir den Bereich definieren, den wir als Bild exportieren möchten. Dies geschieht durch Festlegen des Druckbereichs auf dem Arbeitsblatt.
```csharp
// Stellen Sie den Druckbereich auf den gewünschten Bereich ein
worksheet.PageSetup.PrintArea = "D8:G16";
```
In diesem Fall geben wir an, dass die Zellen von D8 bis G16 exportiert werden sollen. Passen Sie diese Zellreferenzen entsprechend den zu erfassenden Daten an.
## Schritt 5: Ränder konfigurieren
Stellen wir sicher, dass unser exportiertes Bild keine unnötigen Leerzeichen enthält. Wir setzen alle Ränder auf Null.
```csharp
// Alle Ränder auf 0 setzen
worksheet.PageSetup.LeftMargin = 0;
worksheet.PageSetup.RightMargin = 0;
worksheet.PageSetup.TopMargin = 0;
worksheet.PageSetup.BottomMargin = 0;
```
Dieser Schritt ist entscheidend, um sicherzustellen, dass das resultierende Bild perfekt passt und keine Unordnung darum herum herrscht.
## Schritt 6: Bildoptionen festlegen
Als Nächstes legen wir die Optionen für die Bilddarstellung fest. Dazu gehört die Angabe der Auflösung und des Bildtyps.
```csharp
// Setzen Sie die Option „OnePagePerSheet“ auf „true“.
ImageOrPrintOptions options = new ImageOrPrintOptions();
options.OnePagePerSheet = true;
options.ImageType = ImageType.Jpeg;
options.HorizontalResolution = 200;
options.VerticalResolution = 200;
```
Hier geben wir an, dass das Bild im JPEG-Format mit einer Auflösung von 200 DPI vorliegen soll. Sie können die DPI-Werte gerne Ihren Anforderungen entsprechend anpassen.
## Schritt 7: Rendern Sie das Arbeitsblatt in ein Bild
Jetzt kommt der spannende Teil: das eigentliche Rendern des Arbeitsblatts in ein Bild!
```csharp
// Nehmen Sie das Bild Ihres Arbeitsblatts
SheetRender sr = new SheetRender(worksheet, options);
sr.ToImage(0, outputDir + "outputExportRangeOfCellsInWorksheetToImage.jpg");
```
Wir schaffen eine `SheetRender` Instanz und Aufruf `ToImage` , um das Bild von der ersten Seite des angegebenen Arbeitsblatts zu generieren. Das Bild wird im Ausgabeverzeichnis unter dem angegebenen Dateinamen gespeichert.
## Schritt 8: Ausführung bestätigen
Schließlich ist es immer gut, nach Abschluss des Vorgangs Feedback zu geben, daher drucken wir eine Nachricht auf der Konsole.
```csharp
Console.WriteLine("ExportRangeOfCellsInWorksheetToImage executed successfully.\r\n");
```
Dieser Schritt ist entscheidend, um den Erfolg des Vorgangs zu bestätigen, insbesondere wenn der Code in einer Konsolenanwendung ausgeführt wird.
## Abschluss
Und da haben Sie sie – Ihre Schritt-für-Schritt-Anleitung zum Exportieren eines Zellbereichs in ein Bild mit Aspose.Cells für .NET! Diese leistungsstarke Bibliothek ermöglicht Ihnen die nahtlose Bearbeitung und Bearbeitung von Excel-Dateien. Jetzt wissen Sie, wie Sie wichtige Zellen als Bilder erfassen. Ob für Berichte, Präsentationen oder einfach zum Teilen bestimmter Daten – diese Methode ist unglaublich praktisch und effizient. 
## Häufig gestellte Fragen
### Kann ich das Bildformat ändern?
Ja! Sie können die `ImageType` Eigenschaft zur Unterstützung anderer Formate wie PNG oder BMP.
### Was ist, wenn ich mehrere Bereiche exportieren möchte?
Sie müssen die Rendering-Schritte für jeden Bereich wiederholen, den Sie exportieren möchten.
### Gibt es eine Größenbeschränkung für den Bereich, den ich exportieren kann?
Obwohl Aspose.Cells recht robust ist, können extrem große Bereiche die Leistung beeinträchtigen. Es empfiehlt sich, innerhalb angemessener Grenzen zu testen.
### Kann ich diesen Prozess automatisieren?
Absolut! Sie können diesen Code in größere Anwendungen oder Skripte integrieren, um Ihre Excel-Aufgaben zu automatisieren.
### Wo bekomme ich zusätzliche Unterstützung?
Weitere Hilfe erhalten Sie auf der [Aspose Support Forum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}