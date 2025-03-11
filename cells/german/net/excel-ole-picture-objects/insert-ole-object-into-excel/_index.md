---
title: OLE-Objekt in Excel einfügen
linktitle: OLE-Objekt in Excel einfügen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in diesem umfassenden Handbuch mit Schritt-für-Schritt-Anleitungen, wie Sie mit Aspose.Cells für .NET OLE-Objekte in Excel-Dateien einfügen.
weight: 11
url: /de/net/excel-ole-picture-objects/insert-ole-object-into-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OLE-Objekt in Excel einfügen

## Einführung
Egal, ob Sie Bilder, Diagramme oder andere Dateien einbetten möchten, Aspose.Cells für .NET bietet eine einfache Möglichkeit, dies zu erreichen. In dieser Anleitung werden die Schritte erläutert, die zum Einfügen eines OLE-Objekts in eine Excel-Tabelle erforderlich sind. Am Ende können Sie Ihre Excel-Arbeitsmappen mit personalisierten Einbettungen verbessern, die Ihr Publikum beeindrucken oder verschiedene professionelle Anforderungen erfüllen können. 
## Voraussetzungen
Bevor Sie sich in die Einzelheiten des Codes vertiefen, sollten Sie ein paar Dinge zur Hand haben:
1. Visual Studio: Idealerweise sollten Sie in einer Umgebung arbeiten, die .NET unterstützt, wie etwa Visual Studio. Diese IDE erleichtert das Schreiben, Testen und Debuggen Ihrer Anwendungen.
2. Aspose.Cells-Bibliothek: Sie müssen die Aspose.Cells-Bibliothek installiert haben. Sie können sie über den NuGet-Paketmanager beziehen oder direkt von der[Aspose-Website](https://releases.aspose.com/cells/net/).
3.  Beispieldateien: Stellen Sie zu Demonstrationszwecken sicher, dass Sie ein Bild haben (wie`logo.jpg`) und eine Excel-Datei (`book1.xls`) zum Arbeiten. Auf diese wird im Code verwiesen.
4. Grundlegende Kenntnisse in C#: Wenn Sie mit C# vertraut sind, können Sie die erforderlichen Schritte besser verstehen und bei Bedarf Änderungen vornehmen.
Sobald Sie alles an seinem Platz haben, können Sie die Ärmel hochkrempeln und mit dem Einfügen von OLE-Objekten in Excel beginnen!
## Pakete importieren
Um Excel-Dateien mit Aspose.Cells zu bearbeiten, müssen Sie zunächst die erforderlichen Pakete importieren. Fügen Sie oben in Ihrer C#-Datei die folgenden Namespaces hinzu:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Mit dieser Grundkonfiguration können Sie mit der Arbeitsmappe, den Arbeitsblättern und anderen wichtigen Komponenten interagieren, die Sie für Ihre Aufgabe benötigen.
Lassen Sie uns dies in leicht verständliche Schritte aufteilen.
## Schritt 1: Richten Sie Ihr Dokumentverzeichnis ein
Der erste Schritt besteht darin, festzulegen, wo Ihre Dokumente gespeichert werden sollen. Das ist ganz einfach.
```csharp
// Der Pfad zum Dokumentverzeichnis.
string dataDir = "Your Document Directory";
```
 Ersetzen Sie unbedingt`"Your Document Directory"` durch einen tatsächlichen Verzeichnispfad auf Ihrem System, in dem Sie Ihre Dateien speichern möchten.
## Schritt 2: Erstellen Sie das Verzeichnis, falls es nicht existiert
Als nächstes wollen wir sicherstellen, dass dieses Verzeichnis existiert. Wenn nicht, müssen wir es erstellen.
```csharp
// Erstellen Sie ein Verzeichnis, falls es noch nicht vorhanden ist.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Diese einfache Prüfung verhindert, dass Ihr Programm später unnötige Fehler verursacht.
## Schritt 3: Instanziieren einer neuen Arbeitsmappe
Erstellen wir jetzt eine neue Arbeitsmappe, in der wir mit unseren OLE-Objekten arbeiten.
```csharp
// Instanziieren Sie eine neue Arbeitsmappe.
Workbook workbook = new Workbook();
```
Diese neue Arbeitsmappe dient als Leinwand für das OLE-Objekt, das Sie einfügen möchten.
## Schritt 4: Holen Sie sich das erste Arbeitsblatt
Nachdem wir unsere Arbeitsmappe haben, müssen wir uns das erste Arbeitsblatt holen. Normalerweise arbeiten Sie hier am aktivsten.
```csharp
// Holen Sie sich das erste Arbeitsblatt.
Worksheet sheet = workbook.Worksheets[0];
```
Schön und einfach! Wir können nun damit beginnen, diesem Arbeitsblatt Inhalt hinzuzufügen.
## Schritt 5: Definieren Sie den Pfad für das Bild
Legen wir nun einen Pfad für das Bild fest, das Sie in Ihre Excel-Datei einbetten möchten.
```csharp
//Definieren Sie eine Zeichenfolgevariable zum Speichern des Bildpfads.
string ImageUrl = dataDir + "logo.jpg";
```
 Stellen Sie sicher, dass dieser Pfad den Standort Ihres`logo.jpg` Datei wird gespeichert.
## Schritt 6: Laden Sie das Bild in ein Byte-Array
Wir müssen das Bild in ein Format lesen, mit dem wir arbeiten können. Dazu öffnen wir den Dateistream und lesen seine Daten in ein Byte-Array.
```csharp
// Bringen Sie das Bild in die Streams.
FileStream fs = File.OpenRead(ImageUrl);
// Definieren Sie ein Byte-Array.
byte[] imageData = new Byte[fs.Length];
// Holen Sie sich das Bild aus den Streams in das Byte-Array.
fs.Read(imageData, 0, imageData.Length);
// Schließen Sie den Stream.
fs.Close();
```
Indem wir das Bild in ein Byte-Array einlesen, bereiten wir es für das Einfügen in das Excel-Arbeitsblatt vor.
## Schritt 7: Holen Sie sich den Excel-Dateipfad
Definieren wir nun, wo sich Ihre Excel-Datei befindet.
```csharp
// Holen Sie sich einen Excel-Dateipfad in einer Variablen.
string path = dataDir + "book1.xls";
```
Stellen Sie erneut sicher, dass dieser Pfad korrekt ist und auf die richtige Datei verweist.
## Schritt 8: Laden Sie die Excel-Datei in ein Byte-Array
Genau wie beim Bild müssen wir die Excel-Datei selbst in ein Byte-Array laden.
```csharp
// Bringen Sie die Datei in die Streams.
fs = File.OpenRead(path);
//Definieren Sie ein Byte-Array.
byte[] objectData = new Byte[fs.Length];
// Speichern Sie die Datei aus Streams.
fs.Read(objectData, 0, objectData.Length);
// Schließen Sie den Stream.
fs.Close();
```
Dadurch wird die Excel-Datei für die Einbettung unseres OLE-Objekts vorbereitet.
## Schritt 9: Das OLE-Objekt zum Arbeitsblatt hinzufügen
Nachdem unsere Daten bereit sind, können wir nun das OLE-Objekt in das Arbeitsblatt einfügen.
```csharp
// Fügen Sie dem Arbeitsblatt mit dem Bild ein OLE-Objekt hinzu.
sheet.OleObjects.Add(14, 3, 200, 220, imageData);
// Legen Sie eingebettete OLE-Objektdaten fest.
sheet.OleObjects[0].ObjectData = objectData;
```
 Diese Zeile erstellt ein eingebettetes Objekt im Excel-Dokument. Die Parameter`(14, 3, 200, 220)` Geben Sie den Speicherort und die Größe des eingebetteten Objekts an. Passen Sie diese Werte nach Bedarf für Ihren spezifischen Anwendungsfall an.
## Schritt 10: Speichern Sie die Excel-Datei
Schließlich ist es an der Zeit, Ihre Änderungen an der Excel-Datei zu speichern.
```csharp
// Speichern Sie die Excel-Datei
workbook.Save(dataDir + "output.out.xls");
```
Diese Zeile speichert die Arbeitsmappe mit dem eingefügten OLE-Objekt. Achten Sie darauf, einen sinnvollen Namen zu verwenden!
## Abschluss
Das Einfügen von OLE-Objekten in Excel-Dateien mit Aspose.Cells für .NET ist nicht nur nützlich, sondern auch unkompliziert, wenn Sie es in überschaubare Schritte aufteilen. Mit diesem leistungsstarken Tool können Sie Ihre Excel-Dokumente verbessern und sie interaktiv und optisch ansprechend gestalten. Egal, ob Sie Entwickler sind, der Berichte automatisieren möchte, oder Analyst, der Daten effektiv präsentieren möchte, die Beherrschung der OLE-Einbettung kann ein wichtiger Bestandteil Ihres Toolkits sein.
## Häufig gestellte Fragen
### Was ist ein OLE-Objekt?
Ein OLE-Objekt ist eine Datei, die in ein Dokument eingebettet werden kann, sodass verschiedene Anwendungen miteinander integriert werden können. Beispiele hierfür sind Bilder, Word-Dokumente und Präsentationen.
### Kann ich Aspose.Cells kostenlos nutzen?
 Sie können Aspose.Cells kostenlos testen, indem Sie eine Testversion herunterladen, die auf der Website verfügbar ist.[Webseite](https://releases.aspose.com/).
### Welche Dateiformate kann ich mit OLE-Objekten verwenden?
Sie können je nach Anwendung verschiedene Formate verwenden, darunter Bilder (JPEG, PNG), Word-Dokumente, PDFs und mehr.
### Wird Aspose.Cells auf allen Plattformen unterstützt?
Aspose.Cells für .NET ist in erster Linie für die .NET-Plattform konzipiert. Die Funktionalität kann jedoch in verschiedenen Windows-, Mac- oder Cloud-Umgebungen unterschiedlich sein.
### Wie kann ich Hilfe erhalten, wenn ich auf Probleme stoße?
 Sie erhalten Support über das[Aspose-Forum](https://forum.aspose.com/c/cells/9) wo Entwickler Erkenntnisse und Lösungen austauschen.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
