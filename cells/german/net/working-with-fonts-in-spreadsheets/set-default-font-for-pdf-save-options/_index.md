---
title: Standardschriftart für PDF-Speicheroptionen festlegen
linktitle: Standardschriftart für PDF-Speicheroptionen festlegen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie mit Aspose.Cells für .NET Standardschriftarten für PDF-Speicheroptionen festlegen, damit Ihre Dokumente jedes Mal perfekt aussehen.
weight: 11
url: /de/net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Standardschriftart für PDF-Speicheroptionen festlegen

## Einführung
Wenn Sie Berichte, Rechnungen oder andere Dokumente im PDF-Format erstellen, ist es von größter Bedeutung, dass Ihr Inhalt genau richtig aussieht. Schriftarten spielen eine wichtige Rolle bei der Aufrechterhaltung der visuellen Attraktivität und Lesbarkeit Ihrer Dokumente. Was passiert jedoch, wenn die Schriftart, die Sie in Ihrer Excel-Datei verwendet haben, auf dem System, auf dem Sie Ihr PDF erstellen, nicht verfügbar ist? Hier kommt Aspose.Cells für .NET ins Spiel. Mit dieser leistungsstarken Bibliothek können Sie Standardschriftarten für Ihre PDF-Speicheroptionen festlegen und so sicherstellen, dass Ihre Dokumente professionell und konsistent aussehen, unabhängig davon, wo sie geöffnet werden.
## Voraussetzungen
Bevor wir beginnen, stellen Sie sicher, dass Sie Folgendes haben:
1. Visual Studio: Sie benötigen eine Entwicklungsumgebung wie Visual Studio, um Ihren Code zu schreiben und auszuführen.
2.  Aspose.Cells für .NET: Sie können die neueste Version herunterladen von[dieser Link](https://releases.aspose.com/cells/net/)Alternativ können Sie es über den NuGet-Paket-Manager in Visual Studio installieren.
3. Grundkenntnisse in C#: Das Verständnis der Grundlagen von C# hilft Ihnen, den Codebeispielen zu folgen.
4. Beispiel-Excel-Datei: Halten Sie eine Beispiel-Excel-Datei zum Testen bereit. Sie können eine mit verschiedenen Schriftarten und Stilen erstellen, um zu sehen, wie Aspose.Cells mit fehlenden Schriftarten umgeht.
## Pakete importieren
Bevor Sie Aspose.Cells in Ihrem Projekt verwenden können, müssen Sie die erforderlichen Pakete importieren. So geht's:
1. Öffnen Sie Ihr Projekt: Starten Sie Visual Studio und öffnen Sie Ihr vorhandenes Projekt oder erstellen Sie ein neues.
2. Referenzen hinzufügen: Klicken Sie im Solution Explorer mit der rechten Maustaste auf Ihr Projekt und wählen Sie „NuGet-Pakete verwalten“ aus.
3. Installieren Sie Aspose.Cells: Suchen Sie nach „Aspose.Cells“ und klicken Sie auf die Schaltfläche „Installieren“.
4. Using-Direktiven hinzufügen: Fügen Sie oben in Ihrer C#-Datei die folgenden Namespaces ein:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## Schritt 1: Richten Sie Ihre Verzeichnisse ein
Bevor Sie mit Dateien arbeiten, müssen Sie die Quell- und Ausgabeverzeichnisse definieren. So können Sie Ihre Excel-Eingabedatei leichter finden und die generierten Ausgabedateien einfacher speichern.
```csharp
// Quellverzeichnis
string sourceDir = "Your Document Directory";
// Ausgabeverzeichnis
string outputDir = "Your Document Directory";
```
 Ersetzen`"Your Document Directory"` durch den tatsächlichen Pfad zu Ihren Verzeichnissen.
## Schritt 2: Öffnen Sie die Excel-Datei
 Nachdem wir nun unsere Verzeichnisse eingerichtet haben, öffnen wir die Excel-Datei, mit der Sie arbeiten möchten. Die`Workbook` Die Klasse in Aspose.Cells wird zum Laden des Excel-Dokuments verwendet.
```csharp
// Öffnen einer Excel-Datei
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
Stellen Sie sicher, dass Sie den Dateinamen durch Ihren tatsächlichen Dateinamen ersetzen.
## Schritt 3: Bild-Rendering-Optionen einrichten
Als nächstes müssen wir die Rendering-Optionen für die Konvertierung unserer Excel-Tabelle in ein Bildformat konfigurieren. Wir erstellen eine Instanz von`ImageOrPrintOptions`, und geben Sie den Bildtyp und die Standardschriftart an.
```csharp
// Rendern im PNG-Dateiformat
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
 In diesem Codeausschnitt setzen wir die`CheckWorkbookDefaultFont` Eigentum an`false`, d. h. wenn eine Schriftart fehlt, wird stattdessen die angegebene Standardschriftart („Times New Roman“) verwendet.
## Schritt 4: Das Blatt als Bild rendern
 Lassen Sie uns nun das erste Blatt der Arbeitsmappe als PNG-Bild rendern. Wir verwenden die`SheetRender` Klasse, um dies zu erreichen.
```csharp
// Rendern Sie das erste Arbeitsblatt in ein Bild
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## Schritt 5: Bildtyp ändern und in TIFF rendern
 Wenn Sie dasselbe Blatt in ein anderes Bildformat, wie z. B. TIFF, rendern möchten, können Sie einfach die`ImageType` Eigenschaft und wiederholen Sie den Rendervorgang.
```csharp
// Auf TIFF-Format einstellen
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## Schritt 6: PDF-Speicheroptionen konfigurieren
 Als nächstes richten wir die PDF-Speicheroptionen ein. Wir erstellen eine Instanz von`PdfSaveOptions`legen Sie die Standardschriftart fest und geben Sie an, dass nach fehlenden Schriftarten gesucht werden soll.
```csharp
// Konfigurieren von PDF-Speicheroptionen
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false;
```
## Schritt 7: Speichern Sie die Arbeitsmappe als PDF
Nachdem die Speicheroptionen konfiguriert sind, ist es an der Zeit, unsere Excel-Arbeitsmappe als PDF-Datei zu speichern. 
```csharp
// Speichern Sie die Arbeitsmappe als PDF
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```
## Schritt 8: Ausführung bestätigen
Abschließend empfiehlt es sich, den Benutzer darüber zu informieren, dass der Vorgang erfolgreich abgeschlossen wurde. Dies können Sie mithilfe einer einfachen Konsolenmeldung erreichen.
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## Abschluss
Aspose.Cells bietet eine flexible und robuste Möglichkeit, Excel-Dateimanipulationen zu handhaben, und erleichtert Entwicklern die Erstellung optisch ansprechender Dokumente, deren Formatierung erhalten bleibt. Ganz gleich, ob Sie an Berichten, Finanzdokumenten oder einer anderen Form der Datenpräsentation arbeiten, die Kontrolle über die Schriftartdarstellung kann Ihre Ausgabequalität erheblich verbessern.
## Häufig gestellte Fragen
### Was ist Aspose.Cells?
Aspose.Cells ist eine leistungsstarke .NET-Bibliothek, mit der Entwickler Excel-Dateien bearbeiten können, ohne dass Microsoft Excel installiert sein muss. Sie unterstützt verschiedene Dateiformate und bietet umfangreiche Funktionen für die Arbeit mit Tabellenkalkulationen.
### Wie kann ich eine Standardschriftart für meine Excel-Dateien festlegen?
 Sie können eine Standardschriftart festlegen mit dem`PdfSaveOptions` Klasse und geben Sie den gewünschten Schriftartnamen an. Dadurch wird sichergestellt, dass Ihr Dokument auch dann die von Ihnen angegebene Standardschriftart verwendet, wenn eine Schriftart fehlt.
### Kann ich Excel-Dateien in andere Formate als PDF konvertieren?
Auf jeden Fall! Mit Aspose.Cells können Sie Excel-Dateien in verschiedene Formate konvertieren, darunter Bilder (PNG, TIFF), HTML, CSV und mehr.
### Ist die Nutzung von Aspose.Cells kostenlos?
Aspose.Cells ist ein kommerzielles Produkt, aber Sie können es mit einer eingeschränkten Testversion kostenlos ausprobieren. Für die volle Funktionalität müssen Sie eine Lizenz erwerben.
### Wo finde ich Unterstützung für Aspose.Cells?
 Sie finden Unterstützung für Aspose.Cells unter[Aspose-Forum](https://forum.aspose.com/c/cells/9), wo Sie Fragen stellen und Erkenntnisse mit anderen Benutzern und Entwicklern austauschen können.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
