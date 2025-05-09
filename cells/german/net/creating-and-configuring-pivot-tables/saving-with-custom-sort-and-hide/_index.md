---
"description": "Erfahren Sie, wie Sie Pivot-Tabellen mit benutzerdefinierter Sortierung und Zeilenausblendung mithilfe von Aspose.Cells für .NET speichern. Schritt-für-Schritt-Anleitung mit praktischen Beispielen."
"linktitle": "Speichern von Pivot-Tabellen mit benutzerdefiniertem Sortieren und Ausblenden in .NET"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Speichern von Pivot-Tabellen mit benutzerdefiniertem Sortieren und Ausblenden in .NET"
"url": "/de/net/creating-and-configuring-pivot-tables/saving-with-custom-sort-and-hide/"
"weight": 26
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Speichern von Pivot-Tabellen mit benutzerdefiniertem Sortieren und Ausblenden in .NET

## Einführung
In der Welt der Datenanalyse zählen Pivot-Tabellen zu den leistungsstärksten Werkzeugen, um Daten in einem übersichtlichen Format zusammenzufassen, zu analysieren und zu präsentieren. Wenn Sie mit .NET arbeiten und nach einer einfachen Möglichkeit suchen, Pivot-Tabellen zu bearbeiten – insbesondere, um sie mit benutzerdefinierter Sortierung und dem Ausblenden bestimmter Zeilen zu speichern – sind Sie hier genau richtig! Heute erläutern wir die Technik zum Speichern von Pivot-Tabellen mit Aspose.Cells für .NET. Diese Anleitung führt Sie durch alle Schritte – von den Voraussetzungen bis hin zu praktischen Beispielen – und stellt sicher, dass Sie ähnliche Aufgaben selbstständig bewältigen können. Also, los geht‘s!
## Voraussetzungen
Bevor Sie sich in die Details der Codierung stürzen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:
1. Visual Studio: Idealerweise benötigen Sie eine solide IDE für Ihre .NET-Projekte. Visual Studio ist eine hervorragende Wahl.
2. Aspose.Cells für .NET: Sie benötigen Zugriff auf die Aspose-Bibliothek, um Excel-Dateien programmgesteuert verwalten zu können. Sie können [Laden Sie Aspose.Cells für .NET hier herunter](https://releases.aspose.com/cells/net/).
3. Grundkenntnisse in C#: Die Vertrautheit mit den grundlegenden Programmierkonzepten und der Syntax in C# erleichtert den Prozess.
4. Beispiel-Excel-Datei: Wir verwenden eine Beispieldatei mit dem Namen `PivotTableHideAndSortSample.xlsx`. Stellen Sie sicher, dass Sie diese Datei in Ihrem vorgesehenen Dokumentverzeichnis haben.
Sobald Sie Ihre Entwicklungsumgebung eingerichtet und Ihre Beispieldatei bereit haben, sind Sie startklar!
## Pakete importieren
Nachdem wir die Voraussetzungen erfüllt haben, importieren wir die erforderlichen Pakete. Verwenden Sie in Ihrer C#-Datei die folgende Anweisung, um Aspose.Cells einzubinden:
```csharp
using System;
using Aspose.Cells.Pivot;
```
Mit dieser Direktive können Sie auf die Klassen und Methoden der Aspose.Cells-Bibliothek zugreifen. Stellen Sie sicher, dass Sie die Aspose.Cells.dll zu Ihren Projektreferenzen hinzugefügt haben.
## Schritt 1: Einrichten der Arbeitsmappe
Zuerst müssen wir unsere Arbeitsmappe laden. Der folgende Codeausschnitt erledigt das:
```csharp
// Verzeichnisse für Quell- und Ausgabedateien
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
// Laden der Arbeitsmappe
Workbook workbook = new Workbook(sourceDir + "PivotTableHideAndSortSample.xlsx");
```
In diesem Schritt definieren Sie die Verzeichnisse, in denen Ihre Quell- und Ausgabedateien gespeichert werden. Die `Workbook` Der Konstruktor lädt Ihre vorhandene Excel-Datei und macht sie für die Bearbeitung bereit.
## Schritt 2: Zugriff auf das Arbeitsblatt und die Pivot-Tabelle
Greifen wir nun auf das jeweilige Arbeitsblatt in der Arbeitsmappe zu und wählen die Pivot-Tabelle aus, mit der wir arbeiten möchten.
```csharp
// Greifen Sie auf das erste Arbeitsblatt zu
Worksheet worksheet = workbook.Worksheets[0];
// Greifen Sie auf die erste Pivot-Tabelle im Arbeitsblatt zu
var pivotTable = worksheet.PivotTables[0];
```
In diesem Snippet `Worksheets[0]` wählt das erste Blatt in Ihrem Excel-Dokument aus und `PivotTables[0]` Ruft die erste Pivot-Tabelle ab. So können Sie gezielt die Pivot-Tabelle auswählen, die Sie ändern möchten.
## Schritt 3: PivotTable-Zeilen sortieren
Als Nächstes implementieren wir eine benutzerdefinierte Sortierung, um unsere Daten zu organisieren. Konkret sortieren wir die Ergebnisse in absteigender Reihenfolge.
```csharp
// Sortieren des ersten Zeilenfelds in absteigender Reihenfolge
PivotField field = pivotTable.RowFields[0];
field.IsAutoSort = true;
field.IsAscendSort = false;  // false für absteigend
field.AutoSortField = 0;     // Sortieren nach der ersten Spalte
```
Hier verwenden wir die `PivotField` um die Sortierparameter festzulegen. Dadurch wird die Pivot-Tabelle angewiesen, das angegebene Zeilenfeld basierend auf der ersten Spalte in absteigender Reihenfolge zu sortieren. 
## Schritt 4: Daten aktualisieren und berechnen
Nach dem Anwenden der Sortierung ist es wichtig, die Daten der Pivot-Tabelle zu aktualisieren, um sicherzustellen, dass sie unsere Änderungen widerspiegeln.
```csharp
// Aktualisieren und Berechnen der PivotTable-Daten
pivotTable.RefreshData();
pivotTable.CalculateData();
```
Dieser Schritt synchronisiert die Pivot-Tabelle mit Ihren aktuellen Daten und wendet alle bisher vorgenommenen Sortier- und Filteränderungen an. Klicken Sie einfach auf „Aktualisieren“, um die neue Organisation Ihrer Daten anzuzeigen!
## Schritt 5: Bestimmte Zeilen ausblenden
Lassen Sie uns nun die Zeilen ausblenden, deren Werte unter einem bestimmten Schwellenwert liegen, beispielsweise unter 60. Hier können wir die Daten noch weiter filtern.
```csharp
// Geben Sie die Startzeile für die Punkteabfrage an
int currentRow = 3;
int rowsUsed = pivotTable.DataBodyRange.EndRow;
// Zeilen mit einer Punktzahl unter 60 ausblenden
while (currentRow < rowsUsed)
{
    Cell cell = worksheet.Cells[currentRow, 1]; // Vorausgesetzt, die Punktzahl steht in der ersten Spalte
    double score = Convert.ToDouble(cell.Value);
    if (score < 60)
    {
        worksheet.Cells.HideRow(currentRow);  // Zeile ausblenden, wenn die Punktzahl unter 60 liegt
    }
    currentRow++;
}
```
In dieser Schleife prüfen wir jede Zeile im Datenbereich der Pivot-Tabelle. Liegt ein Wert unter 60, wird die Zeile ausgeblendet. Das ist wie das Aufräumen Ihres Arbeitsbereichs – Sie entfernen alles, was Ihnen den Überblick raubt!
## Schritt 6: Abschließendes Aktualisieren und Speichern der Arbeitsmappe
Bevor wir zum Abschluss kommen, aktualisieren wir die Pivot-Tabelle ein letztes Mal, um sicherzustellen, dass das Ausblenden der Zeilen wirksam wird. Anschließend speichern wir die Arbeitsmappe in einer neuen Datei.
```csharp
// Daten ein letztes Mal aktualisieren und berechnen
pivotTable.RefreshData();
pivotTable.CalculateData();
// Speichern der geänderten Arbeitsmappe
workbook.Save(outputDir + "PivotTableHideAndSort_out.xlsx");
```
Durch diese letzte Aktualisierung wird sichergestellt, dass alles auf dem neuesten Stand ist. Durch das Speichern der Arbeitsmappe erstellen Sie eine neue Datei, die alle von uns vorgenommenen Änderungen widerspiegelt.
## Schritt 7: Erfolg bestätigen
Abschließend drucken wir eine Erfolgsmeldung aus, um zu bestätigen, dass unser Vorgang reibungslos abgeschlossen wurde.
```csharp
Console.WriteLine("PivotTableSortAndHide executed successfully.");
```
Diese Zeile dient dem doppelten Zweck, den Erfolg zu bestätigen und Feedback in Ihrer Konsole bereitzustellen, wodurch der Prozess etwas interaktiver und benutzerfreundlicher wird.
## Abschluss
Und fertig! Sie haben erfolgreich gelernt, wie Sie Pivot-Tabellen mit benutzerdefinierten Sortier- und Ausblendfunktionen mit Aspose.Cells für .NET speichern. Vom Laden Ihrer Arbeitsmappe über das Sortieren der Daten bis hin zum Ausblenden unnötiger Details bieten diese Schritte einen strukturierten Ansatz für die programmgesteuerte Verwaltung Ihrer Pivot-Tabellen. Ob Sie Verkaufsdaten analysieren, die Teamleistung verfolgen oder einfach Informationen organisieren – die Beherrschung dieser Fähigkeiten mit Aspose.Cells spart Ihnen wertvolle Zeit und verbessert Ihren Datenanalyse-Workflow.
## Häufig gestellte Fragen
### Was ist Aspose.Cells für .NET?
Aspose.Cells für .NET ist eine .NET-Bibliothek, mit der Entwickler Excel-Tabellen erstellen, bearbeiten und konvertieren können, ohne auf Microsoft Excel angewiesen zu sein. Sie eignet sich perfekt für die Automatisierung von Aufgaben in Excel-Dokumenten.
### Kann ich Aspose.Cells verwenden, ohne dass Microsoft Office installiert ist?
Absolut! Aspose.Cells ist eine eigenständige Bibliothek. Sie müssen Microsoft Office daher nicht auf Ihrem System installiert haben, um mit Excel-Dateien zu arbeiten.
### Wie kann ich eine temporäre Lizenz für Aspose.Cells erhalten?
Sie können eine vorläufige Lizenz beantragen über die [Seite mit temporärer Lizenz](https://purchase.aspose.com/temporary-license/).
### Wo finde ich Unterstützung bei Aspose.Cells-Problemen?
Bei Fragen oder Problemen können Sie die [Aspose-Forum](https://forum.aspose.com/c/cells/9), wo Sie Unterstützung von der Community und dem Aspose-Team finden.
### Gibt es eine kostenlose Testversion für Aspose.Cells?
Ja! Sie können eine kostenlose Testversion von Aspose.Cells herunterladen, um die Funktionen vor dem Kauf zu testen. Besuchen Sie die [Seite zur kostenlosen Testversion](https://releases.aspose.com/) um loszulegen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}