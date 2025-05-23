---
"description": "Erfahren Sie in dieser Schritt-für-Schritt-Anleitung, wie Sie mit Aspose.Cells für .NET Zeilen und Spalten in Excel gruppieren."
"linktitle": "Gruppieren Sie Zeilen und Spalten in Excel mit Aspose.Cells"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Gruppieren Sie Zeilen und Spalten in Excel mit Aspose.Cells"
"url": "/de/net/row-and-column-management/grouping-rows-and-columns/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Gruppieren Sie Zeilen und Spalten in Excel mit Aspose.Cells

## Einführung
Wenn Sie mit großen Excel-Tabellen arbeiten, wissen Sie, wie wichtig eine übersichtliche und benutzerfreundliche Struktur ist. Das Gruppieren von Zeilen und Spalten erleichtert Ihnen die Erstellung von Abschnitten und vereinfacht die Datennavigation erheblich. Mit Aspose.Cells für .NET können Sie Zeilen und Spalten in Excel einfach programmgesteuert gruppieren und erhalten so die volle Kontrolle über das Layout Ihrer Dateien.
In diesem Tutorial erfahren Sie alles, was Sie zum Einrichten, Gruppieren und Ausblenden von Zeilen und Spalten in einer Excel-Tabelle mit Aspose.Cells für .NET wissen müssen. Am Ende können Sie Excel-Dateien wie ein Profi bearbeiten, ohne Excel selbst öffnen zu müssen. Bereit zum Einstieg?
## Voraussetzungen
Bevor wir uns in den Code stürzen, stellen wir sicher, dass Sie alles eingerichtet und bereit haben:
1. Aspose.Cells für .NET-Bibliothek: Sie benötigen diese Bibliothek für die Arbeit mit Excel-Dateien. Sie können sie herunterladen [Hier](https://releases.aspose.com/cells/net/).
2. Visual Studio: Dieses Tutorial verwendet Visual Studio für Codebeispiele.
3. Grundlegende C#-Kenntnisse: Vertrautheit mit C# und .NET ist hilfreich.
4. Aspose-Lizenz: Um Evaluierungsbeschränkungen zu vermeiden, ist eine kostenpflichtige oder temporäre Lizenz erforderlich. Erwerben Sie eine temporäre Lizenz [Hier](https://purchase.aspose.com/temporary-license/).
## Pakete importieren
Importieren Sie zunächst den erforderlichen Aspose.Cells-Namespace zusammen mit den erforderlichen .NET-Bibliotheken für die Dateiverwaltung. 
```csharp
using System.IO;
using Aspose.Cells;
```
Lassen Sie uns jeden Teil des Codes aufschlüsseln, damit Sie ihm leichter folgen und ihn verstehen können.
## Schritt 1: Richten Sie Ihr Datenverzeichnis ein
Zunächst müssen wir den Pfad zur Excel-Datei definieren, mit der wir arbeiten werden. Dies ist normalerweise ein lokaler Pfad, es kann aber auch ein Pfad im Netzwerk sein.
```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "Your Document Directory";
```
Ersetzen Sie hier `"Your Document Directory"` mit dem tatsächlichen Pfad zu Ihren Excel-Dateien. Diese Einstellung hilft Ihrem Code, die benötigten Dateien zu finden.
## Schritt 2: Erstellen Sie einen Dateistream für den Zugriff auf die Excel-Datei
Aspose.Cells erfordert, dass Sie die Datei über einen Dateistream öffnen. Dieser Stream liest und lädt den Dateiinhalt zur Verarbeitung.
```csharp
// Erstellen eines Dateistreams, der die zu öffnende Excel-Datei enthält
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
Der obige Code öffnet `book1.xls` aus dem angegebenen Verzeichnis. Falls die Datei nicht existiert, erstellen Sie sie oder ändern Sie den Dateinamen.
## Schritt 3: Laden Sie die Arbeitsmappe mit Aspose.Cells
Nun initialisieren wir die Arbeitsmappe über Aspose.Cells. Dieser Schritt ermöglicht uns den Zugriff auf die Excel-Datei und ermöglicht eine einfache Bearbeitung.
```csharp
// Öffnen der Excel-Datei über den Dateistream
Workbook workbook = new Workbook(fstream);
```
Nach dieser Zeile wird `workbook` Das Objekt enthält alle Daten und die Struktur Ihrer Excel-Datei. Stellen Sie sich das so vor, als ob die gesamte Tabelle in den Speicher geladen wäre.
## Schritt 4: Zugriff auf das Arbeitsblatt, das Sie ändern möchten
Aspose.Cells speichert jedes Arbeitsblatt in der Arbeitsmappe als separates Objekt. Hier wählen wir das erste Arbeitsblatt aus.
```csharp
// Zugriff auf das erste Arbeitsblatt in der Excel-Datei
Worksheet worksheet = workbook.Worksheets[0];
```
Wenn Sie ein bestimmtes Arbeitsblatt benötigen, können Sie diese Zeile ändern, um über den Namen oder Index darauf zuzugreifen.
## Schritt 5: Zeilen im Arbeitsblatt gruppieren
Jetzt kommt der spaßige Teil: das Gruppieren der Zeilen! Wir gruppieren die ersten sechs Zeilen und blenden sie aus.
```csharp
// Gruppieren der ersten sechs Zeilen (von 0 bis 5) und Ausblenden durch Übergeben von „true“
worksheet.Cells.GroupRows(0, 5, true);
```
Die einzelnen Parameter bewirken Folgendes:
- 0, 5: Die Start- und Endindizes für die zu gruppierenden Zeilen. In Excel beginnt die Zeilenindizierung bei 0.
- true: Wenn Sie dies auf „true“ setzen, werden die gruppierten Zeilen ausgeblendet.
Nach der Ausführung werden die Zeilen von 0 bis 5 gruppiert und ausgeblendet.
## Schritt 6: Spalten im Arbeitsblatt gruppieren
Genau wie Zeilen können Sie Spalten gruppieren, um ein übersichtlicheres Layout zu erstellen. So gruppieren Sie die ersten drei Spalten.
```csharp
// Gruppieren der ersten drei Spalten (von 0 bis 2) und Ausblenden durch Übergeben von „true“
worksheet.Cells.GroupColumns(0, 2, true);
```
Parameter für diese Funktion sind:
- 0, 2: Der zu gruppierende Spaltenbereich, wobei die Indizierung bei 0 beginnt.
- true: Dieser Parameter blendet die gruppierten Spalten aus.
Ihre ausgewählten Spalten (0 bis 2) werden jetzt gruppiert und ausgeblendet in der Excel-Datei angezeigt.
## Schritt 7: Speichern Sie die geänderte Excel-Datei
Nachdem wir Änderungen vorgenommen haben, speichern wir die Datei unter einem neuen Namen, um ein Überschreiben des Originals zu vermeiden.
```csharp
// Speichern der geänderten Excel-Datei
workbook.Save(dataDir + "output.xls");
```
Sie haben nun Ihre gruppierten Zeilen und Spalten erfolgreich gespeichert in `output.xls`. Sie können den Dateinamen nach Bedarf anpassen.
## Schritt 8: Schließen Sie den Dateistream, um Ressourcen freizugeben
Schließen Sie abschließend den Dateistream, um alle Ressourcen freizugeben. Andernfalls kann es zu Problemen kommen, wenn Sie erneut auf die Datei zugreifen oder sie ändern müssen.
```csharp
// Schließen des Dateistreams, um alle Ressourcen freizugeben
fstream.Close();
```
Und das war's! Sie haben jetzt Zeilen und Spalten in einer Excel-Datei mit Aspose.Cells für .NET gruppiert.
## Abschluss
Das Gruppieren von Zeilen und Spalten in Excel mit Aspose.Cells für .NET ist ein unkomplizierter Prozess, der Ihre Tabellen deutlich benutzerfreundlicher und übersichtlicher macht. Mit nur wenigen Codezeilen beherrschen Sie eine leistungsstarke Funktion, die manuell in Excel mehr Schritte erfordern würde. Außerdem können Sie diesen Prozess für viele Dateien automatisieren, was Zeit spart und Fehler reduziert. Diese Anleitung zeigt Ihnen alle Schritte, die Sie benötigen, um Ihre Excel-Dateien programmgesteuert zu verwalten.
## Häufig gestellte Fragen
### Kann ich Zeilen und Spalten gruppieren, ohne sie auszublenden?  
Ja! Einfach weitergeben `false` als dritter Parameter in der `GroupRows` oder `GroupColumns` Verfahren.
### Was ist, wenn ich die Gruppierung von Zeilen oder Spalten aufheben möchte?  
Verwenden `woderksheet.Cells.UngroupRows(startRow, endRow)` or `worksheet.Cells.UngroupColumns(startColumn, endColumn)` , um die Gruppierung aufzuheben.
### Kann ich mehrere Bereiche innerhalb desselben Arbeitsblatts gruppieren?  
Absolut. Rufen Sie die `GroupRows` oder `GroupColumns` -Methode für jeden Bereich, den Sie gruppieren möchten.
### Benötige ich eine Lizenz, um Aspose.Cells für .NET zu verwenden?  
Ja, obwohl eine Testversion verfügbar ist, benötigen Sie eine Lizenz, um den vollen Funktionsumfang freizuschalten. Sie können eine temporäre Lizenz erhalten [Hier](https://purchase.aspose.com/temporary-license/).
### Kann ich Zeilen und Spalten mit bedingter Logik gruppieren?  
Ja! Sie können eine bedingte Gruppierung erstellen, indem Sie vor der Gruppierung eine Logik in Ihren Code integrieren, die von den Daten in jeder Zeile oder Spalte abhängt.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}