---
title: Fügen Sie PDF-Lesezeichen mit benannten Zielen in Aspose.Cells hinzu
linktitle: Fügen Sie PDF-Lesezeichen mit benannten Zielen in Aspose.Cells hinzu
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie mit Aspose.Cells für .NET interaktive PDFs mit Lesezeichen erstellen. Diese Schritt-für-Schritt-Anleitung macht es ganz einfach.
weight: 10
url: /de/net/rendering-and-export/add-pdf-bookmarks/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Fügen Sie PDF-Lesezeichen mit benannten Zielen in Aspose.Cells hinzu

## Einführung
Wenn Sie schon einmal mit langen PDF-Dokumenten gearbeitet haben, wissen Sie, wie schwierig es sein kann, durch seitenlange Informationen zu navigieren. Lesezeichen spielen eine wichtige Rolle bei der Verbesserung des Benutzererlebnisses, da sie schnelle Navigationspunkte bieten. In diesem Tutorial erfahren Sie, wie Sie Lesezeichen mit benannten Zielen in ein PDF einfügen, das mit Aspose.Cells für .NET aus einer Excel-Datei generiert wurde.
## Voraussetzungen
Bevor wir uns ins Detail stürzen, stellen wir sicher, dass Sie alles vorbereitet haben. Um diesem Tutorial folgen zu können, benötigen Sie:
1. Visual Studio: Dies ist die IDE für die .NET-Entwicklung. Stellen Sie sicher, dass es auf Ihrem Computer installiert ist.
2.  Aspose.Cells für .NET: Sie benötigen Aspose.Cells-Bibliotheken. Sie können[Laden Sie es hier herunter](https://releases.aspose.com/cells/net/) . Wenn Sie es erst einmal ausprobieren möchten, schnappen Sie sich Ihre[kostenlose Testversion hier](https://releases.aspose.com/).
3. .NET Framework: Stellen Sie sicher, dass Sie eine kompatible Version installiert haben. Aspose.Cells unterstützt mehrere Versionen von .NET.
4. Grundkenntnisse in C#: Wenn Sie die C#-Syntax beherrschen, können Sie die Codeausschnitte besser verstehen.
Mit diesen Elementen in Ihrem Toolkit sind wir bereit, ein PDF-Dokument mit Lesezeichen zu erstellen!
## Pakete importieren
Zunächst müssen wir sicherstellen, dass unser Projekt die Funktionen von Aspose.Cells nutzen kann. Beginnen Sie mit der Erstellung eines neuen C#-Projekts in Visual Studio. Danach möchten Sie die erforderlichen Pakete importieren. Normalerweise tun Sie dies oben in Ihrer Codedatei:
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
Sehen Sie, wie einfach das ist? Durch das Hinzufügen einiger Zeilen wird ein leistungsstarkes Toolkit für die Handhabung von Excel-Dateien freigeschaltet.
## Schritt 1: Einrichten der Verzeichnisse
Zu Beginn müssen Sie die Quell- und Ausgabeverzeichnisse angeben. Hier befindet sich Ihre ursprüngliche Excel-Datei und hier wird Ihre PDF-Datei gespeichert.
```csharp
string sourceDir = "Your Document Directory"; // zB "C:\\MeineDateien\\"
string outputDir = "Your Document Directory"; // zB "C:\\MyOutput\\"
```
Betrachten Sie diesen Schritt als Vorbereitung Ihres Arbeitsbereichs. So wie ein Maler nicht ohne Staffelei oder Leinwand anfangen würde, sollten Sie nicht mit dem Programmieren beginnen, ohne Ihre Dateispeicherorte anzugeben.
## Schritt 2: Laden Sie die Excel-Quelldatei
Als Nächstes müssen wir Ihre Excel-Datei mithilfe der Arbeitsmappenklasse in den Speicher laden.
```csharp
Workbook wb = new Workbook(sourceDir + "samplePdfBookmarkEntry_DestinationName.xlsx");
```
Das Laden der Arbeitsmappe ist wie das Öffnen eines Dokuments voller Potenzial. Es bietet Zugriff auf alle Arbeitsblätter, Zellen und Formatierungsfunktionen Ihrer ursprünglichen Excel-Datei.
## Schritt 3: Zugriff auf das Arbeitsblatt
Nachdem wir unsere Arbeitsmappe geladen haben, greifen wir auf das erste Arbeitsblatt zu. Die Zellen, auf die wir für unsere Lesezeichen verweisen, befinden sich hier.
```csharp
Worksheet ws = wb.Worksheets[0];
```
Jeder Künstler braucht eine Leinwand! In diesem Szenario fungiert das Arbeitsblatt als Leinwand, auf der Sie bestimmen, welche Zellen die Lesezeichen enthalten sollen.
## Schritt 4: Lesezeichen erstellen
### Auf bestimmte Zellen zugreifen
Lassen Sie uns ein Lesezeichen für eine bestimmte Zelle erstellen, beispielsweise Zelle C5. Wir erstellen einen Lesezeicheneintrag, verknüpfen ihn mit dieser Zelle und geben ihm einen Namen. 
```csharp
Cell cell = ws.Cells["C5"];
PdfBookmarkEntry bookmarkEntry = new PdfBookmarkEntry();
bookmarkEntry.Text = "Text"; // Wechseln Sie zu Ihrem bevorzugten Lesezeichennamen
bookmarkEntry.Destination = cell;
bookmarkEntry.DestinationName = "AsposeCells--" + cell.Name;
```
Sie können sich das so vorstellen, als würden Sie eine Haftnotiz auf Ihrem Dokument anbringen. Der Titel gibt an, wohin Ihr Lesezeichen führt, während das Ziel (Zelle C5) angibt, wohin es Sie in der PDF-Datei führt.
### Untergeordnete Lesezeichen hinzufügen
Wir können das Benutzererlebnis verbessern, indem wir Unterlesezeichen hinzufügen. Wir greifen jetzt auf zwei zusätzliche Zellen (G56 und L4) zu und richten sie als Unterlesezeichen ein.
```csharp
cell = ws.Cells["G56"];
PdfBookmarkEntry subbookmarkEntry1 = new PdfBookmarkEntry();
subbookmarkEntry1.Text = "Text1"; // Erstes Unterlesezeichen
subbookmarkEntry1.Destination = cell;
subbookmarkEntry1.DestinationName = "AsposeCells--" + cell.Name;
cell = ws.Cells["L4"];
PdfBookmarkEntry subbookmarkEntry2 = new PdfBookmarkEntry();
subbookmarkEntry2.Text = "Text2"; // Zweites Unterlesezeichen
subbookmarkEntry2.Destination = cell;
subbookmarkEntry2.DestinationName = "AsposeCells--" + cell.Name;
```
Diese Unterlesezeichen funktionieren wie die Kapitel eines Buches und führen den Benutzer zu spezifischeren Inhalten innerhalb des Dokuments.
### Untergeordnete Lesezeichen zur Liste hinzufügen
Als Nächstes gruppieren wir unsere Unterlesezeichen unter dem Hauptlesezeichen, das wir zuvor erstellt haben.
```csharp
ArrayList list = new ArrayList();
list.Add(subbookmarkEntry1);
list.Add(subbookmarkEntry2);
bookmarkEntry.SubEntry = list;
```
Durch diese Organisation entsteht eine hierarchische Struktur, die die Navigation vereinfacht – halten Sie sich für ein optimales Benutzererlebnis an die „Grundlagen des Lesezeichensetzens“!
## Schritt 5: PDF mit Lesezeichen speichern
### PdfSaveOptions erstellen
Es ist Zeit, die PDF-Speicheroptionen zu erstellen und das von uns erstellte Lesezeichen einzubinden.
```csharp
PdfSaveOptions opts = new PdfSaveOptions();
opts.Bookmark = bookmarkEntry;
```
In diesem Schritt kommen alle Ihre vorherigen Vorbereitungen zusammen. Im Grunde sagen Sie damit: „Ich möchte, dass mein PDF nicht nur ein einfaches Dokument ist, sondern ein interaktiver Leitfaden!“
### Speichern des Dokuments
Abschließend speichern wir die Arbeitsmappe im PDF-Format und integrieren dabei unsere Lesezeichen.
```csharp
wb.Save(outputDir + "outputPdfBookmarkEntry_DestinationName.pdf", opts);
```
Und schon zahlt sich all Ihre harte Arbeit in Form eines gut strukturierten PDF-Dokuments mit praktischen Lesezeichen aus!
## Abschluss
Herzlichen Glückwunsch! Sie haben mit Aspose.Cells für .NET erfolgreich ein PDF mit Lesezeichen und benannten Zielen erstellt. Sie haben gelernt, wie Sie durch Excel-Dateien navigieren, auf bestimmte Zellen zugreifen und Lesezeichen erstellen, die die Benutzerinteraktion verbessern. Stellen Sie sich vor, wie viel einfacher es sein wird, mit diesen praktischen Lesezeichen in Ihren PDF-Dokumenten zu navigieren.
## Häufig gestellte Fragen
### Was ist Aspose.Cells für .NET?
Aspose.Cells ist eine leistungsstarke Bibliothek für die Arbeit mit Excel-Dateien, mit der Sie Tabellen programmgesteuert erstellen, ändern und konvertieren können.
### Kann ich Aspose.Cells in einem kostenlosen Projekt verwenden?
Ja! Aspose bietet eine kostenlose Testversion an, wenn Sie die Funktionen vor dem Kauf einer Lizenz erkunden möchten.
### Wie erhalte ich eine Lizenz für Aspose.Cells?
 Sie können eine Lizenz direkt bei deren[Kaufseite](https://purchase.aspose.com/buy).
### Mit welchen Dokumenttypen kann Aspose.Cells arbeiten?
Es kann mit verschiedenen Formaten arbeiten, darunter XLSX, XLS, CSV, PDF und viele andere.
### Wo bekomme ich Hilfe, wenn ich auf Probleme stoße?
 Unterstützung finden Sie im[Aspose-Foren](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
