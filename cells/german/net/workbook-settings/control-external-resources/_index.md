---
"description": "Erfahren Sie in unserem umfassenden Schritt-für-Schritt-Tutorial, wie Sie externe Ressourcen in Excel mit Aspose.Cells für .NET steuern."
"linktitle": "Steuern externer Ressourcen mithilfe der Arbeitsmappeneinstellungen"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Steuern externer Ressourcen mithilfe der Arbeitsmappeneinstellungen"
"url": "/de/net/workbook-settings/control-external-resources/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Steuern externer Ressourcen mithilfe der Arbeitsmappeneinstellungen

## Einführung
Im Bereich der Datenmanipulation und -präsentation kann der effiziente Umgang mit externen Ressourcen entscheidend sein. Wenn Sie mit Excel-Dateien arbeiten und externe Ressourcen mit Aspose.Cells für .NET nahtlos verwalten möchten, sind Sie hier genau richtig! In diesem Artikel befassen wir uns eingehend mit der Steuerung externer Ressourcen bei der Arbeit mit Excel-Arbeitsmappen. Am Ende dieses Leitfadens können Sie mühelos eine maßgeschneiderte Lösung zum Laden von Bildern und Daten aus externen Quellen implementieren.
## Voraussetzungen
Bevor wir uns in die Details der Programmierung stürzen, müssen einige Voraussetzungen erfüllt sein. Stellen Sie sicher, dass Sie:
1. Visual Studio: Sie benötigen eine IDE zum Schreiben und Testen Ihrer .NET-Anwendungen. Visual Studio ist aufgrund seiner umfassenden Unterstützung und Benutzerfreundlichkeit die empfohlene Option.
2. Laden Sie Aspose.Cells für .NET herunter: Falls Sie es noch nicht getan haben, holen Sie sich die Aspose.Cells-Bibliothek von der [Download-Link](https://releases.aspose.com/cells/net/). 
3. Grundlegende Kenntnisse in C#: Wenn Sie mit den Konzepten von C# und .NET Framework vertraut sind, wird Ihnen der Prozess leichter fallen.
4. Richten Sie Ihre Umgebung ein: Stellen Sie sicher, dass Ihr Projekt auf die Aspose.Cells-Bibliothek verweist. Dies können Sie über den NuGet-Paket-Manager in Visual Studio tun.
5. Beispieldateien: Halten Sie eine Excel-Beispieldatei bereit, die eine externe Ressource, beispielsweise ein verknüpftes Bild, enthält. Diese Datei dient der Veranschaulichung der besprochenen Funktionen.
Sobald Sie diese eingerichtet haben, können Sie sich mit der Steuerung externer Ressourcen mit Aspose.Cells befassen.
## Pakete importieren
Um mit dem Programmieren zu beginnen, müssen Sie die erforderlichen Pakete in Ihre C#-Datei importieren. Folgendes benötigen Sie:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
Diese Namespaces bieten Zugriff auf die Funktionen, die zum Bearbeiten von Excel-Dateien und zur Verarbeitung von Bildern erforderlich sind.
Lassen Sie uns das Ganze in überschaubare Schritte unterteilen, um Ihnen bei der Kontrolle externer Ressourcen zu helfen, indem Sie `Workbook Settings`Wir zeigen Ihnen Schritt für Schritt, wie Sie einen benutzerdefinierten Stream-Provider erstellen, eine Excel-Datei laden und ein Arbeitsblatt in ein Bild rendern. Machen Sie mit!
## Schritt 1: Quell- und Ausgabeverzeichnisse definieren
Zu Beginn müssen wir die Verzeichnisse angeben, aus denen wir unsere Dateien lesen und in denen wir unsere Ausgabe speichern. Es ist wichtig, die richtigen Pfade anzugeben, um Fehler beim Suchen von Dateien zu vermeiden.
```csharp
// Quellverzeichnis
static string sourceDir = "Your Document Directory";
// Ausgabeverzeichnis
static string outputDir = "Your Document Directory";
```
Ersetzen `"Your Document Directory"` durch den tatsächlichen Pfad, in dem sich Ihre Dateien befinden.
## Schritt 2: Implementieren der IStreamProvider-Schnittstelle
Als nächstes erstellen wir eine benutzerdefinierte Klasse, die Folgendes implementiert: `IStreamProvider` Schnittstelle. Diese Klasse verwaltet den Zugriff auf externe Ressourcen (wie Bilder).
```csharp
class SP : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        // Bereinigen Sie bei Bedarf alle Ressourcen
    }
    public void InitStream(StreamProviderOptions options)
    {
        // Öffnen Sie den Dateistream der externen Ressource
        FileStream fi = new FileStream(sourceDir + "sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.png", FileMode.OpenOrCreate, FileAccess.Read);
        options.Stream = fi;
    }
}
```
Im `InitStream` Methode öffnen wir die Datei, die als unsere externe Ressource fungiert, und weisen sie dem `Stream` -Eigenschaft. Dadurch kann die Arbeitsmappe beim Rendern auf die Ressource zugreifen.
## Schritt 3: Laden Sie die Excel-Datei
Nachdem unser Stream-Provider nun bereit ist, laden wir die Excel-Arbeitsmappe, die die externe Ressource enthält.
```csharp
public static void Run()
{
    // Beispiel-Excel-Datei laden
    Workbook wb = new Workbook(sourceDir + "sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.xlsx");
    
    // Stellen Sie Ihre Implementierung von IStreamProvider bereit
    wb.Settings.StreamProvider = new SP();
```
In diesem Snippet laden wir unsere Excel-Datei und weisen unsere benutzerdefinierte `StreamProvider` Implementierung zur Handhabung externer Ressourcen.
## Schritt 4: Zugriff auf das Arbeitsblatt
Nach dem Laden der Arbeitsmappe können wir problemlos auf das gewünschte Arbeitsblatt zugreifen. Nehmen wir das erste.
```csharp
    // Greifen Sie auf das erste Arbeitsblatt zu
    Worksheet ws = wb.Worksheets[0];
```
Ganz einfach, oder? Sie können auf jedes Arbeitsblatt zugreifen, indem Sie seinen Index angeben.
## Schritt 5: Bild- oder Druckoptionen konfigurieren
Nun definieren wir, wie das Ausgabebild aussehen soll. Wir konfigurieren Optionen wie die Sicherstellung, dass pro Blatt eine Seite vorhanden ist, und legen den Ausgabebildtyp fest.
```csharp
    // Bild- oder Druckoptionen festlegen
    ImageOrPrintOptions opts = new ImageOrPrintOptions();
    opts.OnePagePerSheet = true;
    opts.ImageType = Drawing.ImageType.Png;
```
Wenn Sie PNG als Ausgabeformat wählen, stellen Sie sicher, dass die Qualität scharf und klar bleibt!
## Schritt 6: Rendern Sie das Arbeitsblatt in ein Bild
Nachdem alles eingerichtet ist, rendern wir das ausgewählte Arbeitsblatt in eine Bilddatei! Das ist der spannende Teil: Sie sehen, wie Ihr Excel-Blatt in ein wunderschönes Bild umgewandelt wird.
```csharp
    // Erstellen Sie ein Blatt-Rendering, indem Sie die erforderlichen Parameter übergeben
    SheetRender sr = new SheetRender(ws, opts);
    // Konvertieren Sie Ihr gesamtes Arbeitsblatt in ein PNG-Bild
    sr.ToImage(0, outputDir + "outputControlExternalResourcesUsingWorkbookSetting_StreamProvider.png");
    
    Console.WriteLine("ControlExternalResourcesUsingWorkbookSetting_StreamProvider executed successfully.");
}
```
Der `ToImage` Die Funktion übernimmt die gesamte Arbeit und konvertiert das Blatt in ein Bild. Sobald dieser Schritt abgeschlossen ist, finden Sie das Bild in Ihrem Ausgabeverzeichnis gespeichert.
## Abschluss
Und fertig! Sie verfügen nun über das Know-how zur Steuerung externer Ressourcen bei der Arbeit mit Excel-Dateien mit Aspose.Cells in .NET. Dies erweitert nicht nur die Möglichkeiten Ihrer Anwendung, sondern macht auch die Handhabung von Datensätzen und Präsentationen zum Kinderspiel. Mit den angegebenen Schritten können Sie diese Funktionalität problemlos replizieren und an die spezifischen Anforderungen Ihres Projekts anpassen.
## Häufig gestellte Fragen
### Was ist Aspose.Cells?
Aspose.Cells ist eine leistungsstarke Bibliothek für C#- und .NET-Entwickler zum Erstellen, Bearbeiten und Verwalten von Excel-Dateien, ohne dass Microsoft Excel installiert sein muss.
### Wie kann ich Aspose.Cells für .NET herunterladen?
Sie können es herunterladen von der [Aspose-Website](https://releases.aspose.com/cells/net/).
### Gibt es eine kostenlose Testversion?
Ja! Sie können eine kostenlose Testversion von Aspose.Cells über deren [Veröffentlichungsseite](https://releases.aspose.com/).
### Welche Dateitypen unterstützt Aspose.Cells?
Aspose.Cells unterstützt verschiedene Excel-Formate, darunter XLS, XLSX, CSV und mehr.
### Wo finde ich Unterstützung für Aspose.Cells?
Sie können das Aspose-Supportforum unter besuchen [Aspose Forum](https://forum.aspose.com/c/cells/9) um Hilfe.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}