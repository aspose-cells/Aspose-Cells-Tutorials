---
"description": "Entdecken Sie mit unserer leicht verständlichen Anleitung, wie Sie externe Ressourcen bei der Konvertierung von Excel in PDF mit Aspose.Cells für .NET steuern."
"linktitle": "Steuern Sie externe Ressourcen in Excel zu PDF in Aspose.Cells"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Steuern Sie externe Ressourcen in Excel zu PDF in Aspose.Cells"
"url": "/de/net/rendering-and-export/control-loading-of-external-resources/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Steuern Sie externe Ressourcen in Excel zu PDF in Aspose.Cells

## Einführung
Im heutigen digitalen Zeitalter ist die Konvertierung von Excel-Tabellen in PDF-Dokumente eine alltägliche Aufgabe. Ob Berichte, Finanzdaten oder Präsentationsmaterialien – Sie möchten sicherstellen, dass Ihre PDFs genau Ihren Vorstellungen entsprechen. Aspose.Cells für .NET ist eine robuste Bibliothek, mit der Sie diesen Konvertierungsprozess bis ins kleinste Detail steuern können, insbesondere bei der Verarbeitung externer Ressourcen wie Bilder, die Ihre Excel-Dateien begleiten. In dieser Anleitung erfahren Sie, wie Sie externe Ressourcen während der Konvertierung von Excel in PDF mit Aspose.Cells steuern. Also, schnappen Sie sich Ihr Lieblingsgetränk und los geht‘s!
## Voraussetzungen
Bevor wir ins Detail gehen, stellen wir sicher, dass Sie alles haben, was Sie für den Start benötigen. Hier ist eine kurze Checkliste:
1. Visual Studio oder eine beliebige .NET-kompatible IDE: Sie benötigen eine Umgebung zum Schreiben und Testen Ihres Codes.
2. Aspose.Cells für .NET: Wenn Sie es noch nicht installiert haben, gehen Sie zu [Aspose Downloads](https://releases.aspose.com/cells/net/) Seite und holen Sie sich die neueste Version.
3. Grundkenntnisse in C#: Kenntnisse der Programmiersprache C# sind hilfreich. Sollten Sie sich bei bestimmten Konzepten unsicher sein, können Sie diese gerne nachschlagen.
4. Beispiel einer Excel-Datei: Bereiten Sie eine Excel-Datei mit allen externen Ressourcen vor, die Sie konvertieren möchten. Sie können die bereitgestellte Beispieldatei „samplePdfSaveOptions_StreamProvider.xlsx“ verwenden.
5. Eine Bilddatei zum Testen: Diese wird während der Konvertierung als externe Ressource verwendet. Die Bilddatei "newPdfSaveOptions_StreamProvider.png" eignet sich gut als Platzhalter.
## Pakete importieren
Um loszulegen, müssen Sie die erforderlichen Namespaces aus der Aspose.Cells-Bibliothek importieren. Dies ist für den Zugriff auf deren Funktionen unerlässlich. Fügen Sie am Anfang Ihrer Datei unbedingt die folgenden using-Direktiven hinzu:
```csharp
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Rendering;
using System;
```
Diese Pakete stellen alle wichtigen Klassen und Methoden bereit, die Sie zur Ausführung Ihrer Aufgaben benötigen.
## Schritt 1: Erstellen Sie Ihre Stream-Provider-Klasse
Der erste Schritt besteht darin, eine Stream-Provider-Klasse zu erstellen, die Folgendes implementiert: `IStreamProvider` Schnittstelle. Mit dieser Klasse können Sie steuern, wie externe Ressourcen geladen werden.
```csharp
class MyStreamProvider : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        Debug.WriteLine("-----Close Stream-----");
    }
    public void InitStream(StreamProviderOptions options)
    {
        string sourceDir = "Your Document Directory";
        Debug.WriteLine("-----Init Stream-----");
        // Lesen Sie das neue Bild in einem Speicherstream und weisen Sie es der Stream-Eigenschaft zu
        byte[] bts = File.ReadAllBytes(sourceDir + "newPdfSaveOptions_StreamProvider.png");
        MemoryStream ms = new MemoryStream(bts);
        options.Stream = ms;
    }
}
```
In dieser Klasse:
- CloseStream: Diese Methode wird aufgerufen, wenn der Stream geschlossen wird. Im Moment schreiben wir nur eine Debug-Meldung zur Nachverfolgung.
- InitStream: Hier beginnt die Magie. Hier lesen Sie Ihr externes Bild als Byte-Array, konvertieren es in einen Speicherstrom und weisen es dem `options.Stream` Eigentum.
## Schritt 2: Quell- und Ausgabeverzeichnisse einrichten
Nachdem Ihr Stream-Anbieter nun bereit ist, müssen Sie festlegen, wo sich Ihre Excel-Datei befindet und wo Sie Ihre PDF-Datei speichern möchten.
```csharp
// Quellverzeichnis
string sourceDir = "Your Document Directory";
// Ausgabeverzeichnis
string outputDir = "Your Document Directory";
```
Einfach ersetzen `"Your Document Directory"` mit dem tatsächlichen Pfad auf Ihrem Computer, in dem sich Ihre Dateien befinden. Die Organisation Ihrer Dateien ist entscheidend!
## Schritt 3: Laden Sie Ihre Excel-Datei
Als nächstes laden Sie die Excel-Datei, aus der Sie das PDF erstellen möchten.
```csharp
// Laden Sie die Quell-Excel-Datei mit externen Bildern
Workbook wb = new Workbook(sourceDir + "samplePdfSaveOptions_StreamProvider.xlsx");
```
Wir verwenden die `Workbook` Klasse von Aspose.Cells, die Ihre Excel-Datei darstellt. Die Datei kann verschiedene externe Ressourcen wie Bilder enthalten, die Sie während der Konvertierung steuern möchten.
## Schritt 4: PDF-Speicheroptionen festlegen
Bevor Sie die Arbeitsmappe als PDF speichern, legen Sie fest, wie sie gespeichert werden soll. Sie können diese Optionen Ihren Anforderungen entsprechend anpassen.
```csharp
// PDF-Speicheroptionen angeben – Stream-Anbieter
PdfSaveOptions opts = new PdfSaveOptions();
opts.OnePagePerSheet = true; // Jedes Blatt auf einer neuen Seite speichern
```
Hier erstellen wir eine neue Instanz von `PdfSaveOptions`mit dem Sie die Formatierung Ihrer PDF-Datei anpassen können. Die `OnePagePerSheet` Die Option ist praktisch, um sicherzustellen, dass jedes Excel-Blatt im endgültigen PDF eine eigene Seite erhält.
## Schritt 5: Weisen Sie Ihren Stream-Anbieter zu
Wenn Ihre PDF-Optionen festgelegt sind, müssen Sie Aspose anweisen, Ihren benutzerdefinierten Stream-Anbieter für externe Ressourcen zu verwenden.
```csharp
wb.Settings.StreamProvider = new MyStreamProvider();
```
Diese Linie verbindet Ihre `Workbook` Instanz mit dem `MyStreamProvider` Klasse, die Sie zuvor erstellt haben. Das bedeutet, dass Ihr Anbieter externe Ressourcen, die während der Konvertierung gefunden werden, wie angegeben behandelt.
## Schritt 6: Speichern Sie die Arbeitsmappe als PDF
Wenn alles eingestellt ist, ist es endlich an der Zeit, Ihre Excel-Arbeitsmappe als PDF zu speichern.
```csharp
// Speichern Sie die Arbeitsmappe als PDF
wb.Save(outputDir + "outputPdfSaveOptions_StreamProvider.pdf", opts);
```
Durch einen Anruf bei der `Save` Methode auf dem Arbeitsmappenobjekt und Übergeben Ihres Ausgabeverzeichnisses zusammen mit den PDF-Optionen konvertieren Sie die Excel-Datei in eine schön formatierte PDF-Datei.
## Schritt 7: Erfolgreiche Ausführung bestätigen
Abschließend ist es immer schön, bestätigen zu können, dass Ihr Vorgang erfolgreich war!
```csharp
Console.WriteLine("ControlLoadingOfExternalResourcesInExcelToPDF executed successfully.\r\n");
```
Durch die Ausgabe einer Erfolgsmeldung auf der Konsole bleiben Sie über den Status Ihres Vorgangs informiert. Es empfiehlt sich, diese kleinen Bestätigungen in Ihren Code einzubinden.
## Abschluss
Fertig! Mit diesen einfachen Schritten können Sie den Umgang mit externen Ressourcen bei der Konvertierung von Excel in PDF mit Aspose.Cells präzise steuern. Das bedeutet, dass Ihre Dokumente nun Bilder und andere externe Elemente präzise einbinden können und so stets ein hochwertiges Endprodukt gewährleisten.
## Häufig gestellte Fragen
### Was ist Aspose.Cells?  
Aspose.Cells ist eine leistungsstarke Bibliothek für .NET-Entwickler, mit der Sie Excel-Dateien in verschiedenen Formaten erstellen, bearbeiten, konvertieren und rendern können.
### Wie lade ich Aspose.Cells herunter?  
Sie können die neueste Version von Aspose.Cells herunterladen von der [Download-Link](https://releases.aspose.com/cells/net/).
### Kann ich Aspose.Cells kostenlos testen?  
Ja! Sie können eine kostenlose Testversion erhalten, indem Sie die [Seite „Kostenlose Testversion“](https://releases.aspose.com/).
### Wo finde ich Unterstützung für Aspose.Cells?  
Bei Supportanfragen können Sie die [Aspose Support-Forum](https://forum.aspose.com/c/cells/9).
### Wie kann ich eine temporäre Lizenz für Aspose.Cells erhalten?  
Sie können eine vorläufige Lizenz beantragen [Hier](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}