---
title: Festlegen der PDF-Erstellungszeit in .NET
linktitle: Festlegen der PDF-Erstellungszeit in .NET
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie mit Aspose.Cells die PDF-Erstellungszeit in .NET festlegen. Folgen Sie unserer Schritt-für-Schritt-Anleitung für die nahtlose Konvertierung von Excel in PDF.
weight: 11
url: /de/net/xps-and-pdf-operations/setting-pdf-creation-time/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Festlegen der PDF-Erstellungszeit in .NET

## Einführung
Im heutigen digitalen Zeitalter ist die Fähigkeit, Dokumente in verschiedene Formate zu konvertieren, für viele Anwendungen von entscheidender Bedeutung. Ein häufiges Bedürfnis ist die Konvertierung von Excel-Tabellen in PDF-Dateien. Dadurch bleibt nicht nur die Formatierung erhalten, sondern auch das Teilen und Drucken wird erheblich vereinfacht. Wenn Sie Entwickler sind und mit .NET arbeiten, ist Aspose.Cells eine fantastische Bibliothek, die diesen Prozess vereinfacht. In diesem Tutorial erfahren Sie, wie Sie die PDF-Erstellungszeit festlegen, wenn Sie eine Excel-Datei mit Aspose.Cells für .NET in PDF konvertieren.
## Voraussetzungen
Bevor wir uns in die Einzelheiten des Codes stürzen, stellen wir sicher, dass Sie alles haben, was Sie für den Einstieg brauchen.
### Was du brauchst
1. Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem Computer installiert ist. Dies wird Ihre Entwicklungsumgebung sein.
2.  Aspose.Cells für .NET: Laden Sie die Aspose.Cells-Bibliothek herunter von[Webseite](https://releases.aspose.com/cells/net/)Sie können auch mit einer kostenlosen Testversion beginnen, um die Funktionen zu testen.
3. Grundkenntnisse in C#: Wenn Sie mit der C#-Programmierung vertraut sind, verstehen Sie die Codeausschnitte besser.
4.  Excel-Datei: Halten Sie eine Excel-Datei zur Konvertierung bereit. Für dieses Beispiel verwenden wir eine Datei namens`Book1.xlsx`.
Nachdem Sie nun die Voraussetzungen erfüllt haben, kommen wir zum spaßigen Teil: dem Importieren der erforderlichen Pakete und dem Schreiben des Codes!
## Pakete importieren
Zu Beginn müssen Sie die erforderlichen Namespaces in Ihre C#-Datei importieren. Dies ist wichtig, da Sie dadurch auf die von der Aspose.Cells-Bibliothek bereitgestellten Klassen und Methoden zugreifen können.
### Öffnen Sie Ihr C#-Projekt
Öffnen Sie Visual Studio und erstellen Sie entweder ein neues Projekt oder öffnen Sie ein vorhandenes, in dem Sie die PDF-Konvertierungsfunktion implementieren möchten.
### Aspose.Cells-Referenz hinzufügen
Sie können die Aspose.Cells-Bibliothek zu Ihrem Projekt hinzufügen, indem Sie im Solution Explorer mit der rechten Maustaste auf Ihr Projekt klicken, „NuGet-Pakete verwalten“ auswählen und nach „Aspose.Cells“ suchen. Installieren Sie das Paket.
### Namespaces importieren
Fügen Sie oben in Ihrer C#-Datei die folgenden Namespaces ein:
```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Charts;
```
Über diese Namespaces erhalten Sie Zugriff auf die Workbook-Klasse und andere wichtige Funktionen.

Nachdem wir nun unsere Pakete importiert haben, wollen wir den Prozess der Konvertierung einer Excel-Datei in eine PDF-Datei unter Festlegen der Erstellungszeit aufschlüsseln.
## Schritt 1: Definieren Sie das Dokumentverzeichnis
Zunächst müssen Sie das Verzeichnis angeben, in dem Ihre Dokumente gespeichert sind. Hier befindet sich Ihre Excel-Datei und hier wird auch das Ausgabe-PDF gespeichert.
```csharp
string dataDir = "Your Document Directory"; // Geben Sie Ihr Dokumentverzeichnis an
```
 Ersetzen`"Your Document Directory"` mit dem tatsächlichen Pfad, auf dem Ihr`Book1.xlsx` Datei befindet. Dieser Pfad hilft der Anwendung, die Datei zur Verarbeitung zu finden.
## Schritt 2: Laden Sie die Excel-Datei
 Als nächstes laden Sie die Excel-Datei in ein`Workbook` Objekt. Hier glänzt Aspose.Cells, da es Ihnen die mühelose Arbeit mit Excel-Dateien ermöglicht.
```csharp
string inputPath = dataDir + "Book1.xlsx"; // Pfad zu Ihrer Excel-Datei
Workbook workbook = new Workbook(inputPath); // Laden Sie die Excel-Datei
```
 Der`Workbook` Die Klasse wird zum Laden und Bearbeiten von Excel-Dateien verwendet. Indem Sie den Eingabepfad übergeben, teilen Sie der Anwendung mit, mit welcher Datei gearbeitet werden soll.
## Schritt 3: PdfSaveOptions erstellen
 Jetzt ist es Zeit, eine Instanz von`PdfSaveOptions`. Mit dieser Klasse können Sie verschiedene Optionen zum Speichern Ihrer Arbeitsmappe als PDF angeben, einschließlich der Erstellungszeit.
```csharp
PdfSaveOptions options = new PdfSaveOptions(); // PdfSaveOptions-Instanz erstellen
options.CreatedTime = DateTime.Now; // Stellen Sie die Erstellungszeit auf jetzt ein
```
 Durch die Einstellung`options.CreatedTime` Zu`DateTime.Now`stellen Sie sicher, dass die PDF-Datei das aktuelle Datum und die aktuelle Uhrzeit ihrer Erstellung wiedergibt.
## Schritt 4: Speichern Sie die Arbeitsmappe als PDF
Abschließend speichern Sie die Arbeitsmappe mit den soeben definierten Optionen als PDF-Datei.
```csharp
workbook.Save(dataDir + "output.pdf", options); //Als PDF speichern
```
 Diese Codezeile speichert die Arbeitsmappe im PDF-Format am angegebenen Speicherort.`options` Der Parameter wird übergeben, um die Erstellungszeit in die PDF-Metadaten aufzunehmen.

## Abschluss
Und da haben Sie es! Sie haben eine Excel-Datei erfolgreich mit Aspose.Cells für .NET in eine PDF-Datei konvertiert, komplett mit einem Erstellungszeitstempel. Diese Funktion kann unglaublich nützlich sein, wenn Sie den Überblick über Dokumentversionen behalten müssen oder wenn Sie den Empfängern Informationen darüber geben möchten, wann das Dokument erstellt wurde.
 Wenn Sie weitere Funktionen von Aspose.Cells entdecken möchten, schauen Sie sich unbedingt die[Dokumentation](https://reference.aspose.com/cells/net/).
## Häufig gestellte Fragen
### Was ist Aspose.Cells?
Aspose.Cells ist eine leistungsstarke Bibliothek für .NET, mit der Entwickler Excel-Dateien erstellen, bearbeiten und konvertieren können.
### Kann ich Aspose.Cells kostenlos nutzen?
 Ja, Sie können mit einer kostenlosen Testversion beginnen, die auf der[Aspose-Website](https://releases.aspose.com/).
### Wie lege ich andere PDF-Eigenschaften fest?
 Sie können verschiedene PDF-Eigenschaften festlegen mit dem`PdfSaveOptions` Klasse, wie Seitengröße, Komprimierung und mehr.
### Ist es möglich, mehrere Excel-Dateien gleichzeitig zu konvertieren?
Ja, Sie können eine Liste von Dateien durchlaufen und auf jede Datei denselben Konvertierungsprozess anwenden.
### Wo erhalte ich Support für Aspose.Cells?
 Sie können Unterstützung von der Aspose-Community erhalten über deren[Support-Forum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
