---
"description": "Erfahren Sie in unserem umfassenden Schritt-für-Schritt-Tutorial, wie Sie die Quelldaten einer Pivot-Tabelle programmgesteuert mit Aspose.Cells für .NET ändern."
"linktitle": "Quelldaten der Pivot-Tabelle programmgesteuert in .NET ändern"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Quelldaten der Pivot-Tabelle programmgesteuert in .NET ändern"
"url": "/de/net/creating-and-configuring-pivot-tables/changing-source-data/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Quelldaten der Pivot-Tabelle programmgesteuert in .NET ändern

## Einführung
In der Welt der Datenanalyse gibt es kaum ein so herausragendes Tool wie Microsoft Excel. Täglich nutzen unzählige Nutzer Excel zur Verwaltung und Analyse ihrer Daten. Doch hinter den Kulissen geht es viel komplexer zu als nur Klicken und Ziehen. Wenn Sie schon immer Excel-Dateien programmgesteuert bearbeiten wollten – insbesondere die Quelldaten einer Pivot-Tabelle ändern – sind Sie hier genau richtig! In diesem Leitfaden erfahren Sie, wie Sie dies mit Aspose.Cells für .NET erreichen. Egal, ob Sie bereits erfahrener Entwickler sind oder gerade erst in die Welt der Programmierung eintauchen, dieses Tutorial bietet Ihnen wertvolle und leicht verständliche Informationen.
## Voraussetzungen
Bevor wir mit der Änderung der Quelldaten einer Pivot-Tabelle beginnen, stellen wir sicher, dass Sie alles eingerichtet und startklar haben:
1. Visual Studio: Stellen Sie sicher, dass Sie eine Kopie von Microsoft Visual Studio installiert haben, da wir unseren Code hier schreiben werden.
2. Aspose.Cells Bibliothek: Sie müssen die Aspose.Cells Bibliothek heruntergeladen und in Ihrem Projekt referenziert haben. Sie können sie herunterladen [Hier](https://releases.aspose.com/cells/net/).
3. Grundkenntnisse in C#: Obwohl dieses Tutorial vereinfacht ist, hilft Ihnen das Verständnis von C# dabei, den Code besser zu verstehen.
4. Excel-Datei: Sie sollten über eine Beispiel-Excel-Datei (z. B. „Book1.xlsx“) verfügen, die eine Pivot-Tabelle enthält, die wir bearbeiten können.
Gut, nachdem diese Voraussetzungen erfüllt sind, können wir mit dem Importieren der erforderlichen Pakete fortfahren und mit dem Codieren beginnen!
## Pakete importieren
Das Wichtigste zuerst: Importieren wir die benötigten Pakete. Öffnen Sie Ihr C#-Projekt in Visual Studio und fügen Sie oben in Ihrer Codedatei die folgenden using-Direktiven hinzu:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Über diese Namespaces erhalten Sie Zugriff auf die wesentlichen Klassen, die Sie zum Arbeiten mit Excel-Dateien und zum Bearbeiten ihres Inhalts mithilfe von Aspose.Cells benötigen.

Lassen Sie uns den Prozess nun in überschaubare Schritte unterteilen. Wir gehen durch das Öffnen einer Excel-Datei, das Bearbeiten des Arbeitsblatts, das Ändern der Datenquelle der Pivot-Tabelle und das Speichern der Ergebnisse.
## Schritt 1: Definieren Sie Ihr Dokumentverzeichnis
Zuerst müssen Sie angeben, wo sich Ihre Excel-Datei befindet. Ändern Sie die `dataDir` Variable, die auf den Ordner verweist, der Ihr „Book1.xlsx“ enthält.
```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "Your Document Directory";
```
Diese Zeile richtet das Verzeichnis ein, in dem Ihre Excel-Datei gespeichert ist, sodass Sie später leichter darauf zugreifen können.
## Schritt 2: Geben Sie den Eingabepfad an
Als Nächstes erstellen wir eine Zeichenfolge, um den vollständigen Pfad zu Ihrer Excel-Eingabedatei anzugeben:
```csharp
string InputPath = dataDir + "Book1.xlsx";
```
Dies trägt zur Optimierung Ihres Dateizugriffs bei, da Sie im gesamten Code nicht immer wieder denselben Pfad eingeben müssen.
## Schritt 3: Erstellen eines Dateistreams
Nun öffnen wir die Excel-Datei. Wir erstellen eine `FileStream` mit dem Sie den Inhalt der Excel-Datei lesen können:
```csharp
// Erstellen eines Dateistreams, der die zu öffnende Excel-Datei enthält
FileStream fstream = new FileStream(InputPath, FileMode.Open);
```
Diese Zeile öffnet die Datei im Lesemodus und ermöglicht uns den Zugriff auf ihre Daten.
## Schritt 4: Laden Sie die Arbeitsmappe
Wenn der Dateistream vorhanden ist, besteht der nächste Schritt darin, die Arbeitsmappe zu laden:
```csharp
// Öffnen der Excel-Datei über den Dateistream
Workbook workbook = new Workbook(fstream);
```
Dieser Befehl nimmt Ihre Excel-Datei und lädt sie in eine `Workbook` Objekt. Nach dem Laden können Sie die Datei nach Bedarf bearbeiten.
## Schritt 5: Zugriff auf das Arbeitsblatt
Zeit, in die Einzelheiten einzutauchen. Wir greifen auf das erste Arbeitsblatt in der Arbeitsmappe zu:
```csharp
// Zugriff auf das erste Arbeitsblatt in der Excel-Datei
Worksheet worksheet = workbook.Worksheets[0];
```
Dadurch haben Sie direkten Zugriff auf die Daten im ersten Arbeitsblatt und können diese problemlos ändern.
## Schritt 6: Neue Daten eintragen
Als Nächstes möchten wir neue Daten in die Zellen einfügen. In diesem Beispiel fügen wir einige Beispieldaten hinzu:
```csharp
// Füllen der Arbeitsblattzellen mit neuen Daten
worksheet.Cells["A9"].PutValue("Golf");
worksheet.Cells["B9"].PutValue("Qtr4");
worksheet.Cells["C9"].PutValue(7000);
```
Hier setzen wir die Werte "Golf", "Qtr4" und `7000` in bestimmte Zellen. Sie können diese Werte nach Bedarf ändern.
## Schritt 7: Ändern Sie den benannten Bereich
Nun ändern wir den benannten Bereich, auf den sich die Pivot-Tabelle bezieht. Dazu erstellen oder aktualisieren wir einen Bereich:
```csharp
// Ändern des benannten Bereichs „DataSource“
Range range = worksheet.Cells.CreateRange(0,0,9,3);
range.Name = "DataSource";
```
Durch die Definition eines neuen Bereichs stellen wir sicher, dass die Pivot-Tabelle beim Aktualisieren diese neuen Daten verwendet.
## Schritt 8: Speichern Sie die geänderte Excel-Datei
Nach all den Änderungen ist es wichtig, Ihre Arbeit zu speichern! Speichern wir die geänderte Arbeitsmappe:
```csharp
// Speichern der geänderten Excel-Datei
workbook.Save(dataDir + "output.xls");
```
Dieser Befehl speichert die Arbeitsmappe in einer neuen Datei, sodass Sie Ihre Originaldatei nicht überschreiben, es sei denn, Sie möchten dies!
## Schritt 9: Schließen Sie den Dateistream
Abschließend ist es wichtig, den Dateistream zu schließen, um alle verwendeten Ressourcen freizugeben:
```csharp
// Schließen des Dateistreams, um alle Ressourcen freizugeben
fstream.Close();
```
Dieser Schritt stellt sicher, dass Ihre Anwendung keinen Speicher verliert und effizient bleibt.
## Abschluss
Herzlichen Glückwunsch! Sie haben die Quelldaten einer Pivot-Tabelle erfolgreich programmgesteuert in .NET mit Aspose.Cells geändert. Diese Funktionalität eröffnet Ihnen vielfältige Möglichkeiten zur Automatisierung von Excel-Aufgaben und zur Verbesserung Ihres Workflows. Ob Sie Finanzberichte aktualisieren, Verkaufsdaten verfolgen oder einfach nur mit Datensätzen experimentieren – die Möglichkeit, dies programmgesteuert zu tun, spart Ihnen viel Zeit und reduziert das Fehlerrisiko.

## Häufig gestellte Fragen
### Was ist Aspose.Cells?
Aspose.Cells ist eine leistungsstarke .NET-Bibliothek für die Arbeit mit Excel-Dateien, die es Benutzern ermöglicht, Excel-Dokumente programmgesteuert zu erstellen, zu ändern und zu bearbeiten.
### Kann ich mit dieser Methode die Quelldaten bestehender Pivot-Tabellen ändern?
Absolut! Mit dieser Methode können Sie die Datenquelle für vorhandene Pivot-Tabellen in Ihrer Excel-Arbeitsmappe aktualisieren.
### Muss Office installiert sein, um Aspose.Cells zu verwenden?
Nein! Aspose.Cells ist eine eigenständige Bibliothek. Das bedeutet, dass Sie Microsoft Office nicht installieren müssen, um mit Excel-Dateien zu arbeiten.
### Ist die Nutzung von Aspose.Cells kostenlos?
Aspose.Cells bietet eine kostenlose Testversion an, für den vollen Funktionsumfang ist jedoch eine Lizenz erforderlich. Details finden Sie hier. [Hier](https://purchase.aspose.com/buy).
### Wo finde ich weitere Beispiele und Unterstützung?
Weitere Beispiele und Unterstützung finden Sie im [Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/net/) und ihr Community-Forum [Hier](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}