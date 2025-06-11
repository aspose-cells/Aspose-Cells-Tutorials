---
"description": "Erfahren Sie, wie Sie mit Aspose.Cells für .NET interaktive PDFs mit Lesezeichen erstellen. Diese Schritt-für-Schritt-Anleitung macht es Ihnen leicht."
"linktitle": "Fügen Sie PDF-Lesezeichen mit benannten Zielen in Aspose.Cells hinzu"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Fügen Sie PDF-Lesezeichen mit benannten Zielen in Aspose.Cells hinzu"
"url": "/de/net/rendering-and-export/add-pdf-bookmarks/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Fügen Sie PDF-Lesezeichen mit benannten Zielen in Aspose.Cells hinzu

## Einführung
Wenn Sie schon einmal mit umfangreichen PDF-Dokumenten gearbeitet haben, wissen Sie, wie schwierig es sein kann, durch seitenlange Informationen zu navigieren. Lesezeichen tragen entscheidend zur Verbesserung der Benutzerfreundlichkeit bei, da sie schnelle Navigationspunkte bieten. In diesem Tutorial erfahren Sie, wie Sie mit Aspose.Cells für .NET Lesezeichen mit benannten Zielen in ein aus einer Excel-Datei generiertes PDF einfügen.
## Voraussetzungen
Bevor wir ins Detail gehen, stellen wir sicher, dass alles bereit ist. Um diesem Tutorial folgen zu können, benötigen Sie:
1. Visual Studio: Die ideale IDE für die .NET-Entwicklung. Stellen Sie sicher, dass Visual Studio auf Ihrem Computer installiert ist.
2. Aspose.Cells für .NET: Sie benötigen Aspose.Cells-Bibliotheken. Sie können [Laden Sie es hier herunter](https://releases.aspose.com/cells/net/)Wenn Sie es erst einmal ausprobieren möchten, schnappen Sie sich Ihre [kostenlose Testversion hier](https://releases.aspose.com/).
3. .NET Framework: Stellen Sie sicher, dass Sie eine kompatible Version installiert haben. Aspose.Cells unterstützt mehrere Versionen von .NET.
4. Grundkenntnisse in C#: Wenn Sie die C#-Syntax beherrschen, können Sie die Codeausschnitte besser verstehen.
Mit diesen Elementen in Ihrem Toolkit sind wir bereit, ein PDF-Dokument mit Lesezeichen zu erstellen!
## Pakete importieren
Zunächst müssen wir sicherstellen, dass unser Projekt die Funktionen von Aspose.Cells nutzen kann. Erstellen Sie zunächst ein neues C#-Projekt in Visual Studio. Anschließend importieren Sie die benötigten Pakete. Dies geschieht normalerweise am Anfang Ihrer Codedatei:
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
Sehen Sie, wie einfach das ist? Mit nur wenigen Zeilen erhalten Sie ein leistungsstarkes Toolkit für die Bearbeitung von Excel-Dateien.
## Schritt 1: Einrichten der Verzeichnisse
Zunächst müssen Sie das Quell- und das Ausgabeverzeichnis angeben. Hier befindet sich Ihre ursprüngliche Excel-Datei und hier wird Ihre PDF-Datei gespeichert.
```csharp
string sourceDir = "Your Document Directory"; // zB "C:\\MeineDateien\\"
string outputDir = "Your Document Directory"; // zB "C:\\MyOutput\\"
```
Betrachten Sie diesen Schritt als Vorbereitung Ihres Arbeitsbereichs. So wie ein Maler nicht ohne Staffelei oder Leinwand anfangen würde, sollten Sie nicht mit dem Programmieren beginnen, ohne Ihre Dateispeicherorte festzulegen.
## Schritt 2: Laden Sie die Excel-Quelldatei
Als Nächstes müssen wir Ihre Excel-Datei mithilfe der Arbeitsmappenklasse in den Speicher laden.
```csharp
Workbook wb = new Workbook(sourceDir + "samplePdfBookmarkEntry_DestinationName.xlsx");
```
Das Laden der Arbeitsmappe ist wie das Öffnen eines Dokuments voller Potenzial. Es bietet Zugriff auf alle Arbeitsblätter, Zellen und Formatierungsfunktionen Ihrer ursprünglichen Excel-Datei.
## Schritt 3: Zugriff auf das Arbeitsblatt
Nachdem wir unsere Arbeitsmappe geladen haben, greifen wir auf das erste Arbeitsblatt zu. Hier befinden sich die Zellen, auf die wir für unsere Lesezeichen verweisen.
```csharp
Worksheet ws = wb.Worksheets[0];
```
Jeder Künstler braucht eine Leinwand! In diesem Szenario dient das Arbeitsblatt als Leinwand, auf der Sie bestimmen, welche Zellen die Lesezeichen enthalten sollen.
## Schritt 4: Lesezeichen erstellen
### Zugriff auf bestimmte Zellen
Wir erstellen ein Lesezeichen für eine bestimmte Zelle, beispielsweise Zelle C5. Wir erstellen einen Lesezeicheneintrag, verknüpfen ihn mit dieser Zelle und vergeben einen Namen. 
```csharp
Cell cell = ws.Cells["C5"];
PdfBookmarkEntry bookmarkEntry = new PdfBookmarkEntry();
bookmarkEntry.Text = "Text"; // Ändern Sie den Namen Ihres bevorzugten Lesezeichens
bookmarkEntry.Destination = cell;
bookmarkEntry.DestinationName = "AsposeCells--" + cell.Name;
```
Stellen Sie sich das so vor, als würden Sie eine Haftnotiz in Ihrem Dokument anbringen. Der Titel gibt an, wohin Ihr Lesezeichen führt, während das Ziel (Zelle C5) angibt, wohin es Sie in der PDF-Datei führt.
### Hinzufügen von Unterlesezeichen
Wir können die Benutzerfreundlichkeit durch das Hinzufügen von Unterlesezeichen verbessern. Wir greifen nun auf zwei zusätzliche Zellen (G56 und L4) zu und richten sie als Unterlesezeichen ein.
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
Diese Organisation erstellt eine hierarchische Struktur, die die Navigation vereinfacht – halten Sie sich für ein optimales Benutzererlebnis an die „Lesezeichen-Grundlagen“!
## Schritt 5: Speichern der PDF-Datei mit Lesezeichen
### PdfSaveOptions erstellen
Es ist Zeit, die PDF-Speicheroptionen zu erstellen und das von uns erstellte Lesezeichen einzufügen.
```csharp
PdfSaveOptions opts = new PdfSaveOptions();
opts.Bookmark = bookmarkEntry;
```
In diesem Schritt kommen alle Ihre bisherigen Vorbereitungen zusammen. Sie sagen im Wesentlichen: „Ich möchte, dass mein PDF nicht nur ein einfaches Dokument, sondern ein interaktiver Leitfaden ist!“
### Speichern des Dokuments
Abschließend speichern wir die Arbeitsmappe im PDF-Format und integrieren dabei unsere Lesezeichen.
```csharp
wb.Save(outputDir + "outputPdfBookmarkEntry_DestinationName.pdf", opts);
```
Und schon zahlt sich Ihre ganze harte Arbeit mit einem gut strukturierten PDF-Dokument voller praktischer Lesezeichen aus!
## Abschluss
Herzlichen Glückwunsch! Sie haben mit Aspose.Cells für .NET erfolgreich ein PDF mit Lesezeichen und benannten Zielen erstellt. Sie haben gelernt, wie Sie durch Excel-Dateien navigieren, auf bestimmte Zellen zugreifen und Lesezeichen erstellen, die die Benutzerinteraktion verbessern. Stellen Sie sich vor, wie viel einfacher die Navigation in Ihren PDF-Dokumenten mit diesen praktischen Lesezeichen sein wird.
## Häufig gestellte Fragen
### Was ist Aspose.Cells für .NET?
Aspose.Cells ist eine leistungsstarke Bibliothek für die Arbeit mit Excel-Dateien, mit der Sie Tabellen programmgesteuert erstellen, ändern und konvertieren können.
### Kann ich Aspose.Cells in einem kostenlosen Projekt verwenden?
Ja! Aspose bietet eine kostenlose Testversion an, wenn Sie die Funktionen vor dem Kauf einer Lizenz erkunden möchten.
### Wie erhalte ich eine Lizenz für Aspose.Cells?
Sie können eine Lizenz direkt bei deren [Kaufseite](https://purchase.aspose.com/buy).
### Mit welchen Dokumenttypen kann Aspose.Cells arbeiten?
Es kann mit verschiedenen Formaten arbeiten, darunter XLSX, XLS, CSV, PDF und viele andere.
### Wo bekomme ich Hilfe, wenn ich auf Probleme stoße?
Unterstützung finden Sie im [Aspose-Foren](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}