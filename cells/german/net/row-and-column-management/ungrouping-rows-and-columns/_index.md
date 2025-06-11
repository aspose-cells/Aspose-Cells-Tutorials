---
"description": "Erfahren Sie in dieser umfassenden Anleitung, wie Sie mit Aspose.Cells für .NET Zeilen und Spalten in Excel aufheben. Vereinfachen Sie Ihre Excel-Datenmanipulation."
"linktitle": "Gruppieren Sie Zeilen und Spalten in Excel mit Aspose.Cells"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Gruppieren Sie Zeilen und Spalten in Excel mit Aspose.Cells"
"url": "/de/net/row-and-column-management/ungrouping-rows-and-columns/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Gruppieren Sie Zeilen und Spalten in Excel mit Aspose.Cells

## Einführung
Beim Umgang mit Excel-Dateien müssen Sie möglicherweise Zeilen und Spalten aufheben. Ob Sie eine Tabelle bereinigen oder Daten für eine bessere Präsentation neu formatieren – Aspose.Cells für .NET ist ein fantastisches Tool, das den Prozess vereinfacht. In diesem Tutorial führe ich Sie durch die Schritte zum Aufheben der Gruppierung von Zeilen und Spalten in Excel mit Aspose.Cells. Am Ende verfügen Sie über ein solides Verständnis für die programmgesteuerte Arbeit mit Excel-Dateien.
## Voraussetzungen
Bevor wir uns in den Code vertiefen, stellen wir sicher, dass Sie alles eingerichtet haben. Folgendes benötigen Sie:
1. Visual Studio: Sie sollten eine funktionierende Version von Visual Studio auf Ihrem Computer installiert haben. Falls Sie diese noch nicht haben, können Sie sie hier herunterladen: [Visual Studio-Site](https://visualstudio.microsoft.com/).
2. Aspose.Cells für .NET: Sie müssen die Aspose.Cells-Bibliothek herunterladen. Sie finden sie im [Aspose-Releases-Seite](https://releases.aspose.com/cells/net/)Stellen Sie sicher, dass Sie über die erforderlichen Lizenzen verfügen. Diese können Sie erwerben oder über eine [vorläufige Lizenz](https://purchase.aspose.com/temporary-license/).
3. Grundkenntnisse in C#: Ein grundlegendes Verständnis der C#-Programmierung wird Ihnen helfen, den Anweisungen leichter zu folgen.
Sobald Sie alles bereit haben, können wir mit dem lustigen Teil beginnen: dem Code!
## Pakete importieren
Um zu beginnen, müssen Sie die erforderlichen Pakete in Ihr C#-Projekt importieren. So geht's:
1. Öffnen Sie Ihr Projekt in Visual Studio.
2. Fügen Sie einen Verweis auf die Aspose.Cells-Bibliothek hinzu. Klicken Sie dazu mit der rechten Maustaste auf die Verweise in Ihrem Projekt und wählen Sie „Verweis hinzufügen“. Navigieren Sie zum Speicherort der Aspose.Cells-DLL.
3. Fügen Sie oben in Ihrer C#-Datei die folgenden Using-Direktiven hinzu:
```csharp
using System.IO;
using Aspose.Cells;
```
Nachdem nun alles eingerichtet ist, gehen wir die Schritte zum Aufheben der Gruppierung von Zeilen und Spalten in Ihrem Excel-Blatt durch. 
## Schritt 1: Definieren Sie das Dokumentverzeichnis
Zuerst müssen Sie das Verzeichnis angeben, in dem sich Ihre Excel-Datei befindet. Dies können Sie wie folgt einrichten:
```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "Your Document Directory";
```
Ersetzen `"Your Document Directory"` durch den tatsächlichen Pfad auf Ihrem Computer, in dem die Excel-Datei gespeichert ist. 
## Schritt 2: Erstellen eines Dateistreams
Als Nächstes müssen Sie einen Dateistream erstellen, um die Excel-Datei zu öffnen. So geht's:
```csharp
// Erstellen eines Dateistreams, der die zu öffnende Excel-Datei enthält
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
Hier öffnen Sie die Datei mit dem Namen `book1.xls`. Stellen Sie sicher, dass diese Datei in Ihrem angegebenen Verzeichnis vorhanden ist, sonst wird die Fehlermeldung „Datei nicht gefunden“ angezeigt.
## Schritt 3: Instanziieren eines Arbeitsmappenobjekts
Laden wir nun die Excel-Datei in ein Workbook-Objekt. Dadurch können Sie die Arbeitsmappe programmgesteuert bearbeiten:
```csharp
// Instanziieren eines Workbook-Objekts
// Öffnen der Excel-Datei über den Dateistream
Workbook workbook = new Workbook(fstream);
```
Mit dieser Codezeile haben Sie die Excel-Datei erfolgreich in den Speicher geladen und können damit arbeiten.
## Schritt 4: Zugriff auf das Arbeitsblatt
Nachdem Sie die Arbeitsmappe erstellt haben, müssen Sie im nächsten Schritt auf das Arbeitsblatt zugreifen, in dem Sie die Gruppierung von Zeilen und Spalten aufheben möchten. So geht's:
```csharp
// Zugriff auf das erste Arbeitsblatt in der Excel-Datei
Worksheet worksheet = workbook.Worksheets[0];
```
In diesem Fall greifen wir auf das erste Arbeitsblatt zu. Sollten sich Ihre Daten auf einem anderen Blatt befinden, können Sie den Index entsprechend ändern.
## Schritt 5: Gruppierung der Zeilen aufheben
Jetzt kommt der spannende Teil! Wir heben die Gruppierung der ersten sechs Zeilen (von Zeile 0 bis Zeile 5) auf. Verwenden Sie den folgenden Code:
```csharp
// Aufheben der Gruppierung der ersten sechs Zeilen (von 0 bis 5)
worksheet.Cells.UngroupRows(0, 5);
```
Diese Methode entfernt alle Gruppierungen, die auf die angegebenen Zeilen angewendet wurden. So einfach ist das!
## Schritt 6: Spaltengruppierung aufheben
Genau wie Zeilen können Sie auch Spalten aufheben. So heben Sie die Gruppierung der ersten drei Spalten (von Spalte 0 bis Spalte 2) auf:
```csharp
// Aufheben der Gruppierung der ersten drei Spalten (von 0 bis 2)
worksheet.Cells.UngroupColumns(0, 2);
```
## Schritt 7: Speichern Sie die geänderte Excel-Datei
Nachdem Sie die Gruppierung der Zeilen und Spalten aufgehoben haben, speichern Sie die Änderungen im nächsten Schritt wieder in einer Excel-Datei. Dies können Sie mit dem `Save` Verfahren:
```csharp
// Speichern der geänderten Excel-Datei
workbook.Save(dataDir + "output.xls");
```
In diesem Beispiel speichern wir die geänderte Datei als `output.xls`. Sie können den Dateinamen nach Belieben ändern.
## Schritt 8: Schließen Sie den Dateistream
Um Ressourcen freizugeben, sollten Sie abschließend den Dateistream schließen:
```csharp
// Schließen des Dateistreams, um alle Ressourcen freizugeben
fstream.Close();
```
Dies ist eine bewährte Vorgehensweise, um sicherzustellen, dass Ihre Anwendung Dateihandles nicht länger als nötig behält.
## Abschluss
Und da haben Sie es! Sie haben erfolgreich gelernt, wie Sie Zeilen und Spalten in einer Excel-Datei mit Aspose.Cells für .NET aufheben. Mit nur wenigen Codezeilen können Sie Ihre Excel-Dateien programmgesteuert erheblich verändern. Ob Sie Berichte automatisieren oder Daten für Analysen vorbereiten – die Beherrschung dieser Techniken kann Ihnen viel Zeit sparen.
## Häufig gestellte Fragen
### Was ist Aspose.Cells?
Aspose.Cells ist eine leistungsstarke Bibliothek für die Arbeit mit Excel-Dateien in .NET-Anwendungen, die eine einfache Bearbeitung, Konvertierung und Erstellung von Tabellen ermöglicht.
### Kann ich Zeilen und Spalten in Excel mithilfe anderer Bibliotheken aufheben?
Ja, es gibt andere Bibliotheken für die Excel-Bearbeitung in .NET, aber Aspose.Cells bietet umfangreiche Funktionen und Benutzerfreundlichkeit.
### Gibt es eine Möglichkeit, Änderungen nach dem Speichern rückgängig zu machen?
Sobald Sie eine Excel-Datei speichern, kann der vorherige Zustand nicht wiederhergestellt werden, es sei denn, Sie verfügen über eine Sicherungskopie der Originaldatei.
### Wie erhalte ich Support für Aspose.Cells?
Unterstützung erhalten Sie unter [Aspose Support-Forum](https://forum.aspose.com/c/cells/9), wo Sie Fragen stellen und Lösungen finden können.
### Kann ich Aspose.Cells ohne Lizenz verwenden?
Ja, Sie können Aspose.Cells mit bestimmten Einschränkungen kostenlos nutzen und mit einem [vorläufige Lizenz](https://purchase.aspose.com/temporary-license/) für die volle Funktionalität.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}