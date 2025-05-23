---
"description": "Erfahren Sie, wie Sie Bilder in Excel mit Aspose.Cells für .NET proportional positionieren. Gestalten Sie Ihre Tabellen optisch ansprechender."
"linktitle": "Bild positionieren (proportional) in Excel"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Bild positionieren (proportional) in Excel"
"url": "/de/net/excel-ole-picture-objects/position-picture-proportional-excel/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Bild positionieren (proportional) in Excel

## Einführung
Haben Sie genug von verpixelten Bildern, die nie richtig in Ihre Excel-Tabellen passen? Stellen Sie sich vor: Sie haben ein schönes Logo, das in Ihrer Excel-Tabelle prominent platziert werden soll, aber es wird gequetscht, gestreckt oder ungünstig platziert. Das will niemand! Halten Sie sich fest, denn heute lernen Sie, wie Sie Bilder in Excel mit der Aspose.Cells-Bibliothek für .NET proportional positionieren. Diese leistungsstarke Bibliothek macht die Bearbeitung von Excel-Dateien zum Kinderspiel, sei es für Berichte, Datenanalysen oder einfach zum Aufpeppen Ihrer Präsentationen. Tauchen Sie ein in die Details der perfekten Bildausrichtung!
## Voraussetzungen
Bevor wir mit der eigentlichen Codierung beginnen, müssen Sie einige Dinge auf Ihrem Computer eingerichtet haben:
1. Visual Studio: Stellen Sie sicher, dass Sie Visual Studio installiert haben, da es eine praktische Umgebung für Ihr .NET-Projekt bietet.
2. Aspose.Cells Bibliothek: Sie benötigen die Aspose.Cells Bibliothek. Sie können eine kostenlose Testversion herunterladen oder sie im [Aspose-Website](https://purchase.aspose.com/buy).
3. Grundkenntnisse in C#: Ein wenig Vertrautheit mit der C#-Programmierung trägt wesentlich zum Verständnis der Beispiele bei, die wir besprechen werden.
4. Eine Bilddatei: Halten Sie ein Bild bereit (z. B. Ihr Logo), das Sie in das Excel-Blatt einfügen möchten.
Nachdem Sie nun alles vorbereitet haben, können wir mit der Codierung beginnen!
## Pakete importieren
Um Aspose.Cells in Ihrem Projekt verwenden zu können, müssen Sie die entsprechenden Namespaces importieren. So geht's:
### Neues Projekt erstellen
Erstellen Sie in Visual Studio ein neues Projekt:
- Öffnen Sie Visual Studio.
- Klicken Sie auf „Neues Projekt erstellen“.
- Wählen Sie je nach Wunsch „Klassenbibliothek (.NET Framework)“ oder „Konsolenanwendung“.
### Installieren Sie Aspose.Cells
Sie können das Paket Aspose.Cells über NuGet zu Ihrem Projekt hinzufügen. So geht's:
- Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf Ihr Projekt.
- Wählen Sie „NuGet-Pakete verwalten“ aus.
- Suchen Sie nach „Aspose.Cells“ und klicken Sie auf „Installieren“.
### Using-Direktiven hinzufügen
Fügen Sie oben in Ihrer Codedatei die folgenden Anweisungen ein:
```csharp
using System.IO;
using Aspose.Cells;
```
Diese Anweisungen geben Ihnen Zugriff auf die Klassen, die Sie zum Bearbeiten Ihrer Excel-Dateien benötigen.
Lassen Sie uns dies nun in detaillierte Schritte aufschlüsseln, um ein Bild in Excel erfolgreich proportional zu positionieren.
## Schritt 1: Richten Sie Ihr Verzeichnis ein
Stellen Sie zunächst sicher, dass Sie einen eigenen Ordner für Ihre Dokumente haben. So erstellen Sie ein Verzeichnis, falls es noch nicht existiert:
```csharp
string dataDir = "Your Document Directory";
// Erstellen Sie ein Verzeichnis, falls es noch nicht vorhanden ist.
bool isExists = System.IO.Directory.Exists(dataDir);
if (!isExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Dieser Codeausschnitt erstellt ein neues Verzeichnis (falls es noch nicht existiert), um Ihre Excel-Dateien zu speichern. Ersetzen Sie einfach `"Your Document Directory"` durch den tatsächlichen Pfad, in dem Ihre Dateien gespeichert werden sollen.
## Schritt 2: Instanziieren einer Arbeitsmappe
Als Nächstes erstellen wir eine neue Arbeitsmappe:
```csharp
Workbook workbook = new Workbook();
```
Diese Zeile initialisiert ein neues Arbeitsmappenobjekt und gibt Ihnen eine leere Leinwand zum Arbeiten.
## Schritt 3: Neues Arbeitsblatt hinzufügen
Nachdem wir unsere Arbeitsmappe nun eingerichtet haben, fügen wir ihr ein neues Arbeitsblatt hinzu:
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
Dadurch wird ein neues Arbeitsblatt hinzugefügt und der Index dieses Blattes zurückgegeben, den wir später zur Bearbeitung verwenden können.
## Schritt 4: Zugriff auf das neue Arbeitsblatt
Um das neu hinzugefügte Arbeitsblatt zu bearbeiten, müssen Sie darauf zugreifen:
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
Jetzt, `worksheet` ermöglicht es uns, diesem bestimmten Blatt Inhalte und Bilder hinzuzufügen.
## Schritt 5: Bild einfügen
Jetzt kommt der spannende Teil! Fügen wir Ihr schönes Bild hinzu. Ersetzen `"logo.jpg"` mit dem Namen Ihrer Bilddatei:
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
Diese Zeile fügt das Bild in Zelle F6 ein (da Zeilen und Spalten nullindiziert sind, `5` bezieht sich auf die sechste Zelle).
## Schritt 6: Zugriff auf das hinzugefügte Bild
Sobald das Bild eingefügt ist, können Sie wie folgt darauf zugreifen:
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
Dadurch können Sie die Bildeigenschaften manipulieren.
## Schritt 7: Bild proportional positionieren
Nun positionieren wir das Bild proportional:
```csharp
picture.UpperDeltaX = 200;
picture.UpperDeltaY = 200;
```
Hier, `UpperDeltaX` Und `UpperDeltaY` Passen Sie die Position des Bildes im Verhältnis zu den Abmessungen der Zelle an. Sie können diese Werte optimieren, um Ihr Bild genau richtig zu gestalten.
## Schritt 8: Speichern Sie Ihre Änderungen
Speichern Sie abschließend Ihre Arbeitsmappe, um alle Änderungen beizubehalten:
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
Diese Zeile speichert Ihre Arbeitsmappe als `book1.out.xls` im dafür vorgesehenen Verzeichnis.
## Abschluss
Und da haben Sie es! Sie haben gerade gelernt, wie Sie Bilder in Excel mit Aspose.Cells für .NET proportional positionieren. Es geht nicht nur darum, Bilder einzufügen, sondern sie in Ihren Tabellen perfekt aussehen zu lassen. Denken Sie daran: Ein gut platziertes Bild kann Ihre Datenpräsentation deutlich verbessern.
Viel Spaß beim Experimentieren mit verschiedenen Bildern und Platzierungen und tauchen Sie tiefer in die umfangreichen Funktionen von Aspose.Cells ein. Ihre Excel-Tabellen werden grundlegend überarbeitet!
## Häufig gestellte Fragen
### Was ist Aspose.Cells?
Aspose.Cells ist eine leistungsstarke Bibliothek für .NET, die es Benutzern ermöglicht, Excel-Dateien zu erstellen, zu bearbeiten und zu konvertieren, ohne dass Microsoft Excel installiert sein muss.
### Kann ich Aspose.Cells kostenlos nutzen?
Ja, Aspose.Cells bietet eine kostenlose Testversion an, die Sie herunterladen können [Hier](https://releases.aspose.com/).
### Wo finde ich die Dokumentation?
Sie haben Zugriff auf die umfassende [Dokumentation](https://reference.aspose.com/cells/net/) für Aspose.Cells.
### Unterstützt Aspose.Cells alle Bildformate?
Aspose.Cells unterstützt verschiedene Formate, darunter JPEG, PNG, BMP, GIF und TIFF.
### Wie erhalte ich Support für Aspose.Cells?
Bei Fragen besuchen Sie bitte die [Support-Forum](https://forum.aspose.com/c/cells/9) wo Sie Ihre Fragen stellen können.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}