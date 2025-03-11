---
title: Steuern externer Ressourcen mithilfe der Arbeitsmappeneinstellungen
linktitle: Steuern externer Ressourcen mithilfe der Arbeitsmappeneinstellungen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in unserem umfassenden Schritt-für-Schritt-Tutorial, wie Sie mit Aspose.Cells für .NET externe Ressourcen in Excel steuern.
weight: 10
url: /de/net/workbook-settings/control-external-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Steuern externer Ressourcen mithilfe der Arbeitsmappeneinstellungen

## Einführung
Im Bereich der Datenmanipulation und -präsentation kann der effiziente Umgang mit externen Ressourcen entscheidend sein. Wenn Sie mit Excel-Dateien arbeiten und externe Ressourcen nahtlos mit Aspose.Cells für .NET verwalten möchten, sind Sie hier genau richtig! In diesem Artikel werden wir uns eingehend mit der Steuerung externer Ressourcen bei der Arbeit mit Excel-Arbeitsmappen befassen. Am Ende dieses Handbuchs können Sie mühelos eine benutzerdefinierte Lösung zum Laden von Bildern und Daten aus externen Quellen implementieren.
## Voraussetzungen
Bevor wir uns in die Details der Programmierung stürzen, müssen einige Voraussetzungen erfüllt sein. Stellen Sie sicher, dass Sie:
1. Verwenden Sie Visual Studio: Sie benötigen eine IDE zum Schreiben und Testen Ihrer .NET-Anwendungen. Aufgrund seiner umfassenden Unterstützung und Benutzerfreundlichkeit ist Visual Studio die am meisten empfohlene Option.
2.  Laden Sie Aspose.Cells für .NET herunter: Falls Sie dies noch nicht getan haben, laden Sie die Aspose.Cells-Bibliothek von der[Downloadlink](https://releases.aspose.com/cells/net/). 
3. Grundlegende Kenntnisse in C#: Wenn Sie mit den Konzepten von C# und dem .NET-Framework vertraut sind, wird der Prozess für Sie reibungsloser ablaufen.
4. Richten Sie Ihre Umgebung ein: Stellen Sie sicher, dass Ihr Projekt auf die Aspose.Cells-Bibliothek verweist. Sie können dies über den NuGet Package Manager in Visual Studio tun.
5. Beispieldateien: Halten Sie eine Excel-Beispieldatei bereit, die eine externe Ressource enthält, z. B. ein verknüpftes Bild. Diese Datei hilft dabei, die besprochenen Funktionen zu demonstrieren.
Sobald Sie diese eingerichtet haben, können Sie mit der Steuerung externer Ressourcen mit Aspose.Cells beginnen.
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
 Lassen Sie uns das Ganze in überschaubare Schritte unterteilen, um Ihnen bei der Kontrolle externer Ressourcen zu helfen, indem Sie`Workbook Settings`. Wir werden durch die Erstellung eines benutzerdefinierten Stream-Providers, das Laden einer Excel-Datei und das Rendern eines Arbeitsblatts in ein Bild gehen. Machen Sie mit!
## Schritt 1: Quell- und Ausgabeverzeichnisse definieren
Zu Beginn müssen wir die Verzeichnisse angeben, aus denen wir unsere Dateien lesen und in denen wir unsere Ausgabe speichern. Es ist wichtig, die richtigen Pfade anzugeben, um Fehler zu vermeiden, bei denen die Datei nicht gefunden wurde.
```csharp
// Quellverzeichnis
static string sourceDir = "Your Document Directory";
// Ausgabeverzeichnis
static string outputDir = "Your Document Directory";
```
 Ersetzen`"Your Document Directory"` durch den tatsächlichen Pfad, in dem sich Ihre Dateien befinden.
## Schritt 2: Implementieren der IStreamProvider-Schnittstelle
 Als nächstes erstellen wir eine benutzerdefinierte Klasse, die Folgendes implementiert:`IStreamProvider` Schnittstelle. Diese Klasse verwaltet, wie auf externe Ressourcen (wie Bilder) zugegriffen wird.
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
 Im`InitStream` Methode öffnen wir die Datei, die als externe Ressource fungiert, und weisen sie der`Stream`-Eigenschaft. Dadurch kann die Arbeitsmappe beim Rendern auf die Ressource zugreifen.
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
 In diesem Snippet laden wir unsere Excel-Datei und weisen unsere benutzerdefinierte`StreamProvider` Implementierung zur Handhabung externer Ressourcen.
## Schritt 4: Zugriff auf das Arbeitsblatt
Nachdem wir die Arbeitsmappe geladen haben, können wir problemlos auf das gewünschte Arbeitsblatt zugreifen. Nehmen wir das erste.
```csharp
    // Greifen Sie auf das erste Arbeitsblatt zu
    Worksheet ws = wb.Worksheets[0];
```
Es ist ganz einfach, nicht wahr? Sie können auf jedes Arbeitsblatt zugreifen, indem Sie seinen Index angeben.
## Schritt 5: Bild- oder Druckoptionen konfigurieren
Jetzt definieren wir, wie das Ausgabebild aussehen soll. Wir konfigurieren Optionen wie die Sicherstellung, dass für jedes Blatt eine Seite vorhanden ist, und geben den Ausgabebildtyp an.
```csharp
    // Bild- oder Druckoptionen festlegen
    ImageOrPrintOptions opts = new ImageOrPrintOptions();
    opts.OnePagePerSheet = true;
    opts.ImageType = Drawing.ImageType.Png;
```
Wenn Sie PNG als Ausgabeformat wählen, ist sichergestellt, dass die Qualität klar und deutlich bleibt.
## Schritt 6: Rendern Sie das Arbeitsblatt in ein Bild
Nachdem alles eingerichtet ist, rendern wir das ausgewählte Arbeitsblatt in eine Bilddatei! Jetzt kommt der spannende Teil: Sie sehen, wie Ihr Excel-Blatt in ein schönes Bild umgewandelt wird.
```csharp
    // Erstellen Sie ein Blatt-Rendering, indem Sie die erforderlichen Parameter übergeben
    SheetRender sr = new SheetRender(ws, opts);
    // Konvertieren Sie Ihr gesamtes Arbeitsblatt in ein PNG-Bild
    sr.ToImage(0, outputDir + "outputControlExternalResourcesUsingWorkbookSetting_StreamProvider.png");
    
    Console.WriteLine("ControlExternalResourcesUsingWorkbookSetting_StreamProvider executed successfully.");
}
```
 Der`ToImage` Die Funktion übernimmt die ganze Arbeit und wandelt das Blatt in ein Bild um. Sobald dieser Schritt abgeschlossen ist, finden Sie das Bild in Ihrem Ausgabeverzeichnis gespeichert.
## Abschluss
Und da haben Sie es! Sie verfügen jetzt über das Know-how zur Steuerung externer Ressourcen bei der Arbeit mit Excel-Dateien unter Verwendung von Aspose.Cells in .NET. Dies erweitert nicht nur die Fähigkeiten Ihrer Anwendung, sondern macht auch die Handhabung von Datensätzen und Präsentationen zum Kinderspiel. Indem Sie die angegebenen Schritte befolgen, können Sie diese Funktionalität problemlos replizieren und an die spezifischen Anforderungen Ihres Projekts anpassen.
## Häufig gestellte Fragen
### Was ist Aspose.Cells?
Aspose.Cells ist eine leistungsstarke Bibliothek für C#- und .NET-Entwickler zum Erstellen, Bearbeiten und Verwalten von Excel-Dateien, ohne dass Microsoft Excel installiert sein muss.
### Wie kann ich Aspose.Cells für .NET herunterladen?
 Sie können es herunterladen von der[Aspose-Website](https://releases.aspose.com/cells/net/).
### Gibt es eine kostenlose Testversion?
 Ja! Sie können eine kostenlose Testversion von Aspose.Cells über deren[Veröffentlichungsseite](https://releases.aspose.com/).
### Welche Dateitypen unterstützt Aspose.Cells?
Aspose.Cells unterstützt verschiedene Excel-Formate, darunter XLS, XLSX, CSV und mehr.
### Wo finde ich Unterstützung für Aspose.Cells?
 Sie können das Aspose-Supportforum unter besuchen:[Aspose Forum](https://forum.aspose.com/c/cells/9) um Hilfe.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
