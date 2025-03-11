---
title: Drehen und Ändern der Textrichtung in Excel
linktitle: Drehen und Ändern der Textrichtung in Excel
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Transformieren Sie die Textrichtung in Excel mit Aspose.Cells für .NET. Folgen Sie unserer Schritt-für-Schritt-Anleitung, um Text einfach zu drehen und anzupassen.
weight: 22
url: /de/net/excel-formatting-and-styling/rotating-and-changing-text-direction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Drehen und Ändern der Textrichtung in Excel

## Einführung
Wenn wir programmgesteuert mit Excel-Dateien arbeiten, stehen wir oft vor der Herausforderung, Daten in einem gewünschten Format anzuzeigen. Wollten Sie schon einmal die Textrichtung in einer Excel-Zelle ändern? Vielleicht muss der Text von rechts nach links gelesen werden, insbesondere wenn Sie mit Sprachen wie Arabisch oder Hebräisch arbeiten. Oder vielleicht suchen Sie einfach nach einer Möglichkeit, die visuelle Attraktivität Ihrer Tabellen zu verbessern. Was auch immer Ihr Grund ist, Aspose.Cells für .NET bietet eine unkomplizierte Lösung zum Bearbeiten der Textrichtung in Excel-Dateien. In diesem Tutorial erklären wir die Schritte, die zum Drehen und Ändern der Textrichtung in Excel mit Aspose.Cells erforderlich sind.
## Voraussetzungen
Bevor wir uns in den Codierungsteil stürzen, stellen Sie sicher, dass Sie ein paar Dinge bereit haben:
1. Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem Computer installiert ist. Die Aspose.Cells-Bibliothek funktioniert gut damit.
2.  Aspose.Cells-Bibliothek: Sie benötigen die Aspose.Cells-Bibliothek für .NET. Sie können sie von der[Website](https://releases.aspose.com/cells/net/).
3. Grundkenntnisse in C#: Wenn Sie mit der C#-Programmierung vertraut sind, können Sie dem Lernprogramm leichter folgen.
4. .NET Framework: Stellen Sie sicher, dass Ihr Projekt auf das .NET Framework abzielt, da Aspose.Cells für die Arbeit in dieser Umgebung konzipiert ist.
Wenn alle Voraussetzungen erfüllt sind, kann es losgehen!
## Pakete importieren
Bereiten wir nun unser Projekt vor, indem wir die erforderlichen Pakete importieren. So können Sie es tun:
### Neues Projekt erstellen
- Öffnen Sie Visual Studio und erstellen Sie ein neues Projekt.
- Wählen Sie aus den Vorlagen die Konsolenanwendung aus und geben Sie ihr einen geeigneten Namen wie „ExcelTextDirectionDemo“.
### Aspose.Cells-Bibliothek hinzufügen
- Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Projekt und wählen Sie „NuGet-Pakete verwalten“.
- Suchen Sie nach Aspose.Cells und installieren Sie es.
### Erforderliche Namespaces importieren
 Jetzt ist es an der Zeit, die notwendigen Namespaces einzubringen. Oben in Ihrem`Program.cs` Fügen Sie die Datei Folgendes ein:
```csharp
using System.IO;
using Aspose.Cells;
```
Damit sind Sie bereit, Excel-Dateien zu ändern! Nun können wir mit der eigentlichen Codierung beginnen.
## Schritt 1: Richten Sie Ihr Dokumentverzeichnis ein
Um sicherzustellen, dass wir unsere Excel-Datei am richtigen Ort speichern, müssen wir ein Verzeichnis definieren. So geht's:
```csharp
// Der Pfad zum Dokumentverzeichnis.
string dataDir = "Your Document Directory"; // Passen Sie Ihren Verzeichnispfad an
// Erstellen Sie ein Verzeichnis, falls es noch nicht vorhanden ist.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

Dieser Code legt ein Verzeichnis zum Speichern der Excel-Datei fest. Er prüft, ob das Verzeichnis existiert und erstellt es, wenn nicht. Ersetzen Sie unbedingt`"Your Document Directory"` mit einem gültigen Pfad.
## Schritt 2: Instanziieren eines Arbeitsmappenobjekts
Als Nächstes erstellen wir eine neue Excel-Arbeitsmappe. Hier bearbeiten wir unsere Zellen.
```csharp
// Instanziieren eines Workbook-Objekts
Workbook workbook = new Workbook();
```

 Durch die Schaffung einer`Workbook` -Objekt beginnen Sie im Wesentlichen mit einer neuen, leeren Excel-Datei, die Sie ändern können.
## Schritt 3: Abrufen der Referenz des Arbeitsblatts
Greifen Sie jetzt auf das Arbeitsblatt zu, in dem Sie Änderungen vornehmen möchten.
```csharp
// Abrufen der Referenz des Arbeitsblatts
Worksheet worksheet = workbook.Worksheets[0];
```

 Der`Worksheet` Objekt bezieht sich auf das erste Arbeitsblatt in Ihrer Arbeitsmappe. Sie können auf andere Blätter zugreifen, indem Sie den Index ändern.
## Schritt 4: Zugriff auf eine bestimmte Zelle
Konzentrieren wir uns auf eine bestimmte Zelle, in diesem Fall „A1“. 
```csharp
// Zugriff auf die Zelle „A1“ aus dem Arbeitsblatt
Aspose.Cells.Cell cell = worksheet.Cells["A1"];
```

Diese Codezeile erhält Zugriff auf die Zelle „A1“, die wir gleich ändern werden.
## Schritt 5: Wert zur Zelle hinzufügen
Es ist Zeit, einige Daten in unsere Zelle einzugeben.
```csharp
// Einen Wert zur Zelle „A1“ hinzufügen
cell.PutValue("Visit Aspose!");
```

Hier fügen wir einfach den Text „Besuchen Sie Aspose!“ in die Zelle „A1“ ein. Sie können dies beliebig ändern.
## Schritt 6: Einrichten des Textstils
Jetzt kommt der Teil, wo wir die Textrichtung ändern. 
```csharp
// Festlegen der horizontalen Ausrichtung des Textes in der Zelle "A1"
Style style = cell.GetStyle();
```

Dadurch wird der vorhandene Stil der Zelle abgerufen und der Weg für Änderungen geebnet.
## Schritt 7: Ändern der Textrichtung 
Und hier geschieht die Magie! Sie können die Textrichtung wie folgt ändern:
```csharp
// Festlegen der Textrichtung von rechts nach links
style.TextDirection = TextDirectionType.RightToLeft;
```

Diese Zeile legt die Textrichtung von rechts nach links fest, was für Sprachen wie Arabisch oder Hebräisch wichtig ist. 
## Schritt 8: Anwenden des Stils auf die Zelle
Nachdem Sie den Textrichtungsstil geändert haben, wenden Sie diese Änderungen wieder auf die Zelle an:
```csharp
cell.SetStyle(style);
```

Sie wenden den geänderten Stil wieder auf die Zelle an und stellen sicher, dass er die neue Textrichtung widerspiegelt.
## Schritt 9: Speichern der Excel-Datei
Abschließend speichern wir unsere Änderungen in einer neuen Excel-Datei.
```csharp
// Speichern der Excel-Datei
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```

Dieser Code speichert die Arbeitsmappe unter dem angegebenen Dateinamen im angegebenen Verzeichnis. Das angegebene Format ist Excel 97-2003.
## Abschluss
Und los geht‘s! Sie haben erfolgreich gelernt, wie Sie mit Aspose.Cells für .NET die Textrichtung in einer Excel-Zelle drehen und ändern. Ist es nicht erstaunlich, wie ein paar Codezeilen das Layout und die Sprachzugänglichkeit Ihrer Tabelle komplett verändern können? Die Möglichkeit, Excel-Dateien programmgesteuert zu bearbeiten, eröffnet eine Welt voller Möglichkeiten, von der Automatisierung von Berichten bis zur Verbesserung der Datenpräsentation.
## Häufig gestellte Fragen
### Kann ich die Textrichtung für mehrere Zellen ändern?  
Ja, Sie können einen Zellbereich durchlaufen und dieselben Änderungen anwenden.
### Ist die Nutzung von Aspose.Cells kostenlos?  
Aspose.Cells bietet eine kostenlose Testversion an, für die weitere Nutzung ist jedoch eine Lizenz erforderlich.
### In welchen anderen Formaten kann ich speichern?  
Aspose.Cells unterstützt verschiedene Formate wie XLSX, CSV und PDF.
### Muss ich außer Visual Studio noch etwas anderes installieren?  
Nur die Aspose.Cells-Bibliothek muss zu Ihrem Projekt hinzugefügt werden.
### Wo finde ich weitere Informationen zu Aspose.Cells?  
 Sie können die[Dokumentation](https://reference.aspose.com/cells/net/) für umfassende Anleitungen und API-Referenzen.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
