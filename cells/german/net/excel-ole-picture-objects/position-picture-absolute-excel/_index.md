---
"description": "Erfahren Sie in diesem umfassenden Schritt-für-Schritt-Tutorial, wie Sie Bilder in Excel mit Aspose.Cells für .NET absolut positionieren."
"linktitle": "Bildposition (absolut) in Excel"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Bildposition (absolut) in Excel"
"url": "/de/net/excel-ole-picture-objects/position-picture-absolute-excel/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Bildposition (absolut) in Excel

## Einführung
Haben Sie schon einmal Probleme gehabt, Bilder in einer Excel-Tabelle korrekt zu positionieren? Sie sind nicht allein! Viele Anwender stehen vor dieser Herausforderung, insbesondere wenn ihre Datenvisualisierung eine absolute Positionierung für eine bessere Ästhetik oder Übersichtlichkeit erfordert. Suchen Sie nicht weiter; diese Anleitung führt Sie durch den einfachen Prozess der absoluten Positionierung von Bildern in einem Excel-Arbeitsblatt mit Aspose.Cells für .NET. Egal, ob Sie Entwickler sind und Excel-Manipulationen durchführen oder Datenanalyst Ihre Berichte verbessern möchten – unser Schritt-für-Schritt-Tutorial vereinfacht Ihre Excel-Erfahrung mit Bildern!
## Voraussetzungen
Bevor Sie sich in den Code und die Einzelheiten vertiefen, müssen Sie ein paar Dinge bereithalten:
1. Aspose.Cells-Bibliothek: Stellen Sie sicher, dass Sie die neueste Version der Aspose.Cells für .NET-Bibliothek haben. Sie können sie von der [Veröffentlichungsseite](https://releases.aspose.com/cells/net/).
2. Entwicklungsumgebung: Stellen Sie sicher, dass Sie eine funktionierende .NET-Entwicklungsumgebung eingerichtet haben. Sie können Visual Studio oder eine andere IDE Ihrer Wahl verwenden.
3. Grundkenntnisse in C#: Um die Codeausschnitte zu verstehen, sind Kenntnisse der Programmiersprache C# von Vorteil.
4. Bilddatei: Speichern Sie eine Bilddatei (z. B. „logo.jpg“) in Ihrem angegebenen Dokumentverzeichnis, die Sie in Ihr Excel-Blatt einfügen möchten.

## Pakete importieren
Stellen wir zunächst sicher, dass wir die erforderlichen Pakete für unser Projekt importieren. Ihre Projektdatei sollte die folgenden Namespaces enthalten:
```csharp
using System.IO;
using Aspose.Cells;
```
Durch den Import dieser Namespaces stellen wir sicher, dass unser Programm die von Aspose.Cells bereitgestellten Funktionen nutzen kann.
Lassen Sie uns dies der Übersichtlichkeit halber in überschaubare Schritte unterteilen.
## Schritt 1: Richten Sie Ihr Dokumentverzeichnis ein
In diesem ersten Schritt müssen Sie das Verzeichnis definieren, in dem sich Ihre Dokumente befinden. Dies ist wichtig, damit das Programm weiß, wo Dateien gespeichert oder abgerufen werden sollen. So richten Sie es ein:
```csharp
string dataDir = "Your Document Directory";
```
Einfach ersetzen `"Your Document Directory"` mit dem tatsächlichen Pfad, in dem sich Ihre Bilddatei befindet. Dies könnte so etwas sein wie `"C:\\Users\\YourUsername\\Documents\\"`.
## Schritt 2: Instanziieren eines Arbeitsmappenobjekts
Als nächstes müssen Sie eine neue Instanz des `Workbook` Klasse. Dieses Objekt stellt Ihre Excel-Datei dar:
```csharp
Workbook workbook = new Workbook();
```
An diesem Punkt verfügen Sie über eine Arbeitsmappe, die mit Daten und Bildern gefüllt werden kann.
## Schritt 3: Hinzufügen eines neuen Arbeitsblatts
Nachdem Sie die Arbeitsmappe erstellt haben, müssen Sie ihr ein Arbeitsblatt hinzufügen. Hier wird die Magie des Hinzufügens und Positionierens von Bildern sichtbar:
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
Diese Zeile erstellt ein neues Arbeitsblatt in Ihrer Arbeitsmappe und gibt dessen Index zurück, den wir in der Variable speichern `sheetIndex`.
## Schritt 4: Abrufen des neuen Arbeitsblatts
Referenzieren wir das neu erstellte Arbeitsblatt. Mithilfe des Index, den wir gerade erhalten haben, können wir auf das Arbeitsblatt zugreifen und es bearbeiten:
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
Jetzt können Sie mit dem `worksheet` Objekt, um Inhalte hinzuzufügen, einschließlich Bilder.
## Schritt 5: Hinzufügen eines Bildes
Jetzt kommt der spannende Teil! Hier fügen wir das Bild unserem Arbeitsblatt hinzu. Wir geben die Zeilen- und Spaltenindizes an, an denen das Bild verankert werden soll (in diesem Fall in Zelle „F6“, also Zeile 5 und Spalte 5):
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
Diese Zeile fixiert das Bild effektiv an der angegebenen Position relativ zum gesamten Arbeitsblatt. Derzeit unterliegt es jedoch noch der Größenänderung zusammen mit den Zellen.
## Schritt 6: Zugriff auf das neu hinzugefügte Bild
Um das Bild weiter zu bearbeiten, müssen Sie auf seine Eigenschaften zugreifen:
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
Damit erhalten Sie Zugriff auf die Eigenschaften des Bildes, das wir gerade hinzugefügt haben!
## Schritt 7: Absolute Positionierung für das Bild festlegen
Um das Bild absolut (in Pixeln) zu positionieren, müssen Sie seine Position mit dem `Left` Und `Top` Eigenschaften. Hier können Sie steuern, wo das Bild angezeigt wird:
```csharp
picture.Left = 60;
picture.Top = 10;
```
Beide Werte können Sie nach Bedarf anpassen, sie stellen die horizontale bzw. vertikale Positionierung des Bildes dar.
## Schritt 8: Speichern der Excel-Datei
Nachdem Sie alle Änderungen vorgenommen haben, können Sie die Arbeitsmappe speichern:
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
Dadurch wird eine Excel-Datei mit dem Namen erstellt `book1.out.xls` in Ihrem zuvor definierten Dokumentverzeichnis, das Ihr Arbeitsblatt mit dem absolut platzierten Bild enthält.

## Abschluss
Und fertig! Sie haben ein Bild erfolgreich in einem Excel-Blatt mit absoluter Positionierung mithilfe von Aspose.Cells für .NET positioniert. Dieser unkomplizierte Vorgang verbessert nicht nur die visuelle Darstellung Ihrer Excel-Dokumente, sondern stellt auch sicher, dass die Bilder genau dort bleiben, wo Sie sie haben möchten – unabhängig von Änderungen an Zellengröße und Zeilenhöhe. Ob Sie nun einen Bericht erstellen oder ein Dashboard erstellen, Sie können sicherstellen, dass Ihre Bilder jedes Mal perfekt platziert sind.
## Häufig gestellte Fragen
### Was ist Aspose.Cells für .NET?
Aspose.Cells für .NET ist eine .NET-Bibliothek, die es Entwicklern ermöglicht, Excel-Tabellen programmgesteuert zu erstellen, zu bearbeiten und zu konvertieren, ohne dass Microsoft Excel erforderlich ist.
### Kann ich mit Aspose.Cells andere Bildmanipulationen durchführen?
Ja, neben der Positionierung können Sie mithilfe der Aspose.Cells-Bibliothek auch die Größe von Bildern in Excel-Tabellen ändern, sie drehen und bearbeiten.
### Ist die Nutzung von Aspose.Cells kostenlos?
Aspose.Cells ist ein kommerzielles Produkt, aber Sie können mit einer kostenlosen Testversion beginnen, die auf deren [Seite zur kostenlosen Testversion](https://releases.aspose.com/).
### Wie erhalte ich eine temporäre Lizenz für Aspose.Cells?
Sie können eine vorläufige Fahrerlaubnis beantragen über das [Seite mit temporärer Lizenz](https://purchase.aspose.com/temporary-license/) bereitgestellt von Aspose.
### Wo finde ich weitere Beispiele und Dokumentation?
Der [Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/net/) enthält umfangreiche Ressourcen, einschließlich Codebeispielen und detaillierteren Funktionen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}