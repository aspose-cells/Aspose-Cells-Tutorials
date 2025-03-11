---
title: Programmgesteuertes Verwenden der Kopiermethode in Excel
linktitle: Programmgesteuertes Verwenden der Kopiermethode in Excel
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie die Kopiermethode in Aspose.Cells für .NET verwenden, um Excel-Dateien effizient zu bearbeiten. Schritt-für-Schritt-Anleitung enthalten.
weight: 10
url: /de/net/excel-formatting-methods-and-options/using-copy-method/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Programmgesteuertes Verwenden der Kopiermethode in Excel

## Einführung
Wenn es um die programmgesteuerte Verwaltung und Bearbeitung von Tabellen geht, ist Aspose.Cells für .NET ein Kraftpaket, das Ihnen Zeit sparen und Ihren Arbeitsablauf optimieren kann. Eine der häufigsten Aufgaben, mit denen Entwickler konfrontiert werden, ist das Kopieren von Bereichen von einem Arbeitsblatt in ein anderes innerhalb einer Excel-Arbeitsmappe. In diesem Tutorial führen wir Sie durch die Verwendung der Copy-Methode in Aspose.Cells und führen Sie mit klaren Erklärungen und Codebeispielen durch jeden Schritt.
## Voraussetzungen
Bevor wir uns mit den Schritten zur Verwendung der Kopiermethode befassen, müssen Sie sicherstellen, dass die folgenden Voraussetzungen erfüllt sind:
1. .NET Framework: Stellen Sie sicher, dass das .NET Framework auf Ihrem Computer installiert ist. Aspose.Cells ist mit verschiedenen Versionen kompatibel. Überprüfen Sie daher deren[Dokumentation](https://reference.aspose.com/cells/net/) für Einzelheiten.
2. Visual Studio: Es ist wichtig, dass Visual Studio oder eine kompatible IDE für die .NET-Entwicklung eingerichtet ist. So können Sie Ihre Projekte bequem erstellen und verwalten.
3.  Aspose.Cells Bibliothek: Laden Sie die Aspose.Cells Bibliothek herunter von der[Veröffentlichungsseite](https://releases.aspose.com/cells/net/) und fügen Sie in Ihrem Projekt einen Verweis darauf hinzu.
4.  Beispiel einer Excel-Datei: Erstellen Sie eine Excel-Datei oder halten Sie eine bereit (z. B.`Book1.xlsx`), mit denen Sie in diesem Tutorial arbeiten werden.
5. Grundlegende C#-Kenntnisse: Vertrautheit mit den Konzepten und der Syntax der C#-Sprache.
Sobald diese Voraussetzungen erfüllt sind, können Sie mit dem Programmieren beginnen!
## Pakete importieren
Um die von Aspose.Cells bereitgestellten Funktionen nutzen zu können, müssen Sie die erforderlichen Pakete importieren. Stellen Sie in Ihrem C#-Projekt sicher, dass Sie am Anfang Ihrer Codedatei die folgende using-Direktive einfügen:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Dadurch haben Sie Zugriff auf die Klassen und Methoden, die für die einfache Bearbeitung von Excel-Dateien erforderlich sind.
Nachdem Sie nun alles vorbereitet haben, unterteilen wir den Vorgang der Verwendung der Kopiermethode in überschaubare Schritte. Wir beginnen mit dem Laden der Excel-Datei und kopieren dann den gewünschten Bereich.
## Schritt 1: Einrichten des Dateistreams
Der erste Schritt besteht darin, einen Dateistream zu erstellen, der es uns ermöglicht, unsere Excel-Datei zu öffnen und damit zu arbeiten. So geht's:
```csharp
// Der Pfad zum Dokumentverzeichnis.
string dataDir = "Your Document Directory";
// Erstellen eines Dateistreams, der die zu öffnende Excel-Datei enthält
FileStream fstream = new FileStream(dataDir + "Book1.xlsx", FileMode.Open);
```
 In diesem Code müssen Sie den Pfad angeben, in dem Ihr`Book1.xlsx` Datei befindet. Die`FileMode.Open` Der Parameter gibt an, dass wir eine vorhandene Datei öffnen möchten.
## Schritt 2: Öffnen der Arbeitsmappe
Als Nächstes erstellen wir mithilfe des gerade eingerichteten Dateistreams ein Workbook-Objekt. Dadurch erhalten wir Zugriff auf den Inhalt der Excel-Datei.
```csharp
// Öffnen der Excel-Datei über den Dateistream
Workbook workbook = new Workbook(fstream);
```
An diesem Punkt haben wir die Arbeitsmappe geöffnet und können mit der Arbeit mit ihrem Inhalt beginnen.
## Schritt 3: Zugriff auf das Arbeitsblatt
Sobald die Arbeitsmappe geladen ist, müssen wir auf das spezifische Arbeitsblatt zugreifen, mit dem wir arbeiten möchten. Normalerweise ist dies das erste Arbeitsblatt in der Arbeitsmappe.
```csharp
// Zugriff auf das erste Arbeitsblatt in der Excel-Datei
Worksheet worksheet = workbook.Worksheets[0];
```
 Hier,`Worksheets[0]` greift auf das erste Blatt zu. Wenn Sie auf ein anderes Arbeitsblatt zugreifen möchten, ändern Sie einfach den Index.
## Schritt 4: Den Bereich kopieren
Jetzt kommt der Hauptteil – das Kopieren des Zellbereichs. In diesem Tutorial zeigen wir, wie Sie bedingte Formatierungseinstellungen von einer Zelle in eine andere kopieren und wie Sie den gesamten Bereich eines Excel-Blatts kopieren.
### Bedingte Formatierung kopieren (Beispiel)
```csharp
// Bedingte Formatierungseinstellungen von Zelle „A1“ in Zelle „B1“ kopieren
// Arbeitsblatt.BedingteFormatierung kopieren(0, 0, 0, 1);
```
Diese Zeile ist im Originalcode auskommentiert, zeigt Ihnen aber, wie Sie bedingte Formatierung von Zelle A1 in Zelle B1 im selben Arbeitsblatt kopieren. Die Parameter stellen Zeilen- und Spaltenindizes der Quell- und Zielzellen dar. Sie können die Auskommentierung aufheben, wenn diese Funktion benötigt wird.
### Gesamten Bereich kopieren (Beispiel)
Wir können unsere Kopierfunktionalität noch erweitern, indem wir auch das Kopieren eines gesamten Bereichs ermöglichen. Dazu verwenden wir eine Schleife, die alle Arbeitsblätter durchläuft.
```csharp
int TotalRowCount = 0;
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    // Zugriff auf jedes Arbeitsblatt
    Worksheet sourceSheet = workbook.Worksheets[i];
    // Abrufen des Anzeigebereichs im Arbeitsblatt
    Range sourceRange = sourceSheet.Cells.MaxDisplayRange;
    // Erstellen eines Bereichs im Zielarbeitsblatt
    Range destRange = worksheet.Cells.CreateRange(
        sourceRange.FirstRow + TotalRowCount,
        sourceRange.FirstColumn,
        sourceRange.RowCount,
        sourceRange.ColumnCount);
    // Kopieren des Quellbereichs in den Zielbereich
    destRange.Copy(sourceRange);
    // Aktualisieren der Gesamtzeilenanzahl für die nächste Schleifeniteration
    TotalRowCount += sourceRange.RowCount; 
}
```
## Schritt 5: Speichern der geänderten Arbeitsmappe
Nachdem Sie die erforderlichen Bereiche kopiert haben, sollten Sie die geänderte Arbeitsmappe speichern, um Ihre Änderungen beizubehalten. So gehen Sie vor:
```csharp
// Speichern der geänderten Excel-Datei
workbook.Save(dataDir + "output.xls");
```
 Dieser Code speichert Ihre geänderte Arbeitsmappe als`output.xls` in Ihrem angegebenen Verzeichnis. Achten Sie darauf, ein geeignetes Format auszuwählen, das Ihren Anforderungen entspricht. 
## Schritt 6: Schließen des Dateistreams
Um sicherzustellen, dass wir Systemressourcen freigeben, müssen wir schließlich den ursprünglich geöffneten Dateistrom schließen.
```csharp
// Schließen des Dateistreams, um alle Ressourcen freizugeben
fstream.Close();
```
Und schon haben Sie den Vorgang des Kopierens der Bereiche und Speicherns der aktualisierten Excel-Datei erfolgreich abgeschlossen!
## Abschluss
Die Verwendung der Kopiermethode in Aspose.Cells für .NET bietet Ihnen leistungsstarke Funktionen zum einfachen Bearbeiten von Excel-Dateien. Wenn Sie dieser Schritt-für-Schritt-Anleitung folgen, können Sie Zellbereiche und bedingte Formatierungen effektiv von einem Arbeitsblatt in ein anderes kopieren und so Ihre Datenverwaltungsaufgaben optimieren. 
## Häufig gestellte Fragen
### Was ist Aspose.Cells für .NET?
Aspose.Cells für .NET ist eine Bibliothek, die es Entwicklern ermöglicht, Excel-Dateien programmgesteuert in .NET-Anwendungen zu erstellen, zu bearbeiten und zu verwalten.
### Kann ich mit Aspose.Cells Formate, Formeln und Werte kopieren?
Ja, mit Aspose.Cells können Sie nicht nur Werte, sondern auch Formate und Formeln zwischen Bereichen kopieren.
### Ist die Nutzung von Aspose.Cells kostenlos?
 Aspose.Cells bietet eine kostenlose Testversion an, für die weitere Nutzung muss jedoch eine Lizenz erworben werden. Weitere Informationen finden Sie[Hier](https://purchase.aspose.com/buy).
### Wie erhalte ich Unterstützung, wenn Probleme auftreten?
 Sie können Hilfe über das Aspose-Supportforum erhalten.[Hier](https://forum.aspose.com/c/cells/9).
### Wo kann ich die Aspose.Cells-Bibliothek herunterladen?
 Sie können die Bibliothek von der Release-Seite herunterladen[Hier](https://releases.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
