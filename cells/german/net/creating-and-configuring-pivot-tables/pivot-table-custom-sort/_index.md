---
"description": "Erfahren Sie, wie Sie Pivot-Tabellen in .NET mit Aspose.Cells programmgesteuert sortieren. Eine Schritt-für-Schritt-Anleitung zur Einrichtung, Konfiguration, Sortierung und Speicherung der Ergebnisse als Excel- und PDF-Dateien."
"linktitle": "PivotTable benutzerdefinierte Sortierung programmgesteuert in .NET"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "PivotTable benutzerdefinierte Sortierung programmgesteuert in .NET"
"url": "/de/net/creating-and-configuring-pivot-tables/pivot-table-custom-sort/"
"weight": 29
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PivotTable benutzerdefinierte Sortierung programmgesteuert in .NET

## Einführung
Wenn es um die Arbeit mit Excel in einer .NET-Umgebung geht, sticht eine Bibliothek besonders hervor: Aspose.Cells. Ist es nicht toll, wenn ein Tool die programmgesteuerte Bearbeitung von Tabellen ermöglicht? Genau das macht Aspose.Cells! Im heutigen Tutorial tauchen wir tief in die Welt der Pivot-Tabellen ein und zeigen Ihnen, wie Sie mit dieser vielseitigen Bibliothek benutzerdefinierte Sortierungen programmgesteuert implementieren.
## Voraussetzungen
Bevor wir die Ärmel hochkrempeln und uns in den Code stürzen, stellen Sie sicher, dass Sie ein paar Dinge vorbereitet haben:
1. Visual Studio: Sie benötigen eine funktionierende Version von Visual Studio. Hier passiert die ganze Magie.
2. .NET Framework: Kenntnisse in der .NET-Programmierung sind unerlässlich. Egal, ob Sie .NET Core oder .NET Framework lieben – Sie sind bestens vorbereitet.
3. Aspose.Cells Bibliothek: Sie müssen die Aspose.Cells Bibliothek installieren. Sie erhalten sie von der [Download-Link](https://releases.aspose.com/cells/net/) und fügen Sie es Ihrem Projekt hinzu.
4. Grundlegendes Verständnis von Pivot-Tabellen: Sie müssen zwar kein Experte sein, aber ein wenig Wissen über die Funktionsweise von Pivot-Tabellen ist im Verlauf dieses Lernprogramms hilfreich.
5. Beispiel-Excel-Datei: Lassen Sie eine Beispiel-Excel-Datei mit dem Namen `SamplePivotSort.xlsx` bereit in Ihrem Arbeitsverzeichnis zum Testen.
## Pakete importieren
Sobald alle Voraussetzungen erfüllt sind, importieren Sie zunächst die erforderlichen Pakete. Fügen Sie dazu die folgenden Zeilen am Anfang Ihres Codes ein:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Pivot;
```
Dieses Paket bietet alle Funktionen, die Sie zum Bearbeiten von Excel-Dateien mit Aspose.Cells benötigen.

Okay, kommen wir zum spannenden Teil! Wir unterteilen den Prozess der Erstellung einer Pivot-Tabelle und der benutzerdefinierten Sortierung in überschaubare Schritte.
## Schritt 1: Einrichten der Arbeitsmappe
Um loszulegen, müssen wir unsere Arbeitsmappe einrichten. So geht's:
```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
Workbook wb = new Workbook(sourceDir + "SamplePivotSort.xlsx");
```
In diesem Schritt initialisieren wir ein neues `Workbook` Instanz mit dem Pfad zu unserer Excel-Datei. Diese dient als Leinwand, auf der unsere Pivot-Tabelle zum Leben erweckt wird.
## Schritt 2: Zugriff auf das Arbeitsblatt
Als Nächstes müssen wir auf das Arbeitsblatt zugreifen, in dem wir unsere Pivot-Tabelle hinzufügen.
```csharp
Worksheet sheet = wb.Worksheets[0];
PivotTableCollection pivotTables = sheet.PivotTables;
```
Hier nehmen wir das erste Arbeitsblatt in unserer Arbeitsmappe und rufen die `PivotTableCollection`. Diese Sammlung ermöglicht uns die Verwaltung aller Pivot-Tabellen in diesem Arbeitsblatt.
## Schritt 3: Erstellen Sie Ihre erste Pivot-Tabelle
Jetzt ist es an der Zeit, unsere Pivot-Tabelle zu erstellen.
```csharp
int index = pivotTables.Add("=Sheet1!A1:C10", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables[index];
```
Wir fügen unserem Arbeitsblatt eine neue Pivot-Tabelle hinzu und geben den Datenbereich und dessen Position an. „E3“ gibt an, wo unsere Pivot-Tabelle beginnen soll. Anschließend verweisen wir über ihren Index auf diese neue Pivot-Tabelle.
## Schritt 4: PivotTable-Einstellungen konfigurieren
Konfigurieren wir nun unsere Pivot-Tabelle! Dabei steuern wir Aspekte wie Gesamtsummen und Feldanordnungen.
```csharp
pivotTable.RowGrand = false;
pivotTable.ColumnGrand = false;
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
PivotField rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
Wir stellen sicher, dass keine Gesamtsummen für Zeilen und Spalten angezeigt werden, was die Daten übersichtlicher macht. Anschließend fügen wir dem Zeilenbereich das erste Feld hinzu und ermöglichen so die automatische und aufsteigende Sortierung.
## Schritt 5: Spalten und Datenfelder hinzufügen
Sobald die Zeilen festgelegt sind, fügen wir die Spalten- und Datenfelder hinzu.
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Column,0);
PivotField colField = pivotTable.ColumnFields[0];
colField.NumberFormat = "dd/mm/yyyy";
colField.IsAutoSort = true;
colField.IsAscendSort = true;
```
Wir fügen das zweite Feld als Spalte hinzu und formatieren es als Datum. Auch hier aktivieren wir die automatische Sortierung und aufsteigende Reihenfolge, um die Übersicht zu behalten. Abschließend fügen wir unserem Datenbereich noch das dritte Feld hinzu:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Data,2);
```
## Schritt 6: Aktualisieren und Berechnen der Pivot-Tabelle
Nachdem wir alle erforderlichen Felder hinzugefügt haben, stellen wir sicher, dass unsere Pivot-Tabelle aktuell und bereit ist.
```csharp
pivotTable.RefreshData();
pivotTable.CalculateData();
```
Diese Methoden aktualisieren und berechnen die Daten neu und stellen sicher, dass alles auf dem neuesten Stand ist und in unserer Pivot-Tabelle korrekt angezeigt wird.
## Schritt 7: Benutzerdefinierte Sortierung basierend auf Zeilenfeldwerten
Lassen Sie uns etwas Flair hinzufügen, indem wir die Pivot-Tabelle nach bestimmten Werten wie „Meeresfrüchte“ sortieren.
```csharp
index = pivotTables.Add("=Sheet1!A1:C10", "E10", "PivotTable2");
pivotTable = pivotTables[index];
```
Wir wiederholen den Vorgang, indem wir eine weitere Pivot-Tabelle erstellen und sie ähnlich wie die erste einrichten. Wir können sie nun weiter anpassen:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
## Schritt 8: Zusätzliche Sortieranpassungen. Versuchen wir eine andere Sortiermethode basierend auf einem bestimmten Datum:
```csharp
// Hinzufügen einer weiteren Pivot-Tabelle zum Sortieren nach einem Datum
index = pivotTables.Add("=Sheet1!A1:C10", "E18", "PivotTable3");
pivotTable = pivotTables[index];
// Wiederholen Sie die Zeilen- und Spalteneinstellungen ähnlich wie in den vorherigen Schritten
```
Sie wiederholen einfach denselben Vorgang und erstellen eine dritte Pivot-Tabelle mit auf Ihre Anforderungen zugeschnittenen Sortierkriterien.
## Schritt 9: Speichern Sie die Arbeitsmappe. Es ist Zeit, all die harte Arbeit zu speichern, die wir hineingesteckt haben!
```csharp
wb.Save(outputDir + "out.xlsx");
PdfSaveOptions options = new PdfSaveOptions();
options.OnePagePerSheet = true;
wb.Save(outputDir + "out.pdf", options);
```
Hier speichern Sie die Arbeitsmappe als Excel-Datei und als PDF. Die `PdfSaveOptions` ermöglicht eine bessere Formatierung und stellt sicher, dass jedes Blatt nach der Konvertierung auf einer separaten Seite angezeigt wird.
## Schritt 10: Abschließen. Fassen Sie alles zusammen, indem Sie dem Benutzer mitteilen, dass alles in Ordnung ist.
```csharp
Console.WriteLine("PivotTableCustomSort executed successfully.");
```
## Abschluss
Sie haben nun gelernt, wie Sie die Leistungsfähigkeit von Aspose.Cells nutzen, um Pivot-Tabellen in Ihren .NET-Anwendungen zu erstellen und anzupassen. Von der Ersteinrichtung bis zur benutzerdefinierten Sortierung sorgt jeder Schritt für ein nahtloses Erlebnis. Ob Sie jährliche Verkaufsdaten präsentieren oder Bestandsstatistiken verfolgen müssen – diese Kenntnisse werden Ihnen von Nutzen sein!
## Häufig gestellte Fragen
### Was ist eine Pivot-Tabelle?
Eine Pivot-Tabelle ist ein Datenverarbeitungstool in Excel, mit dem Sie Daten zusammenfassen und analysieren können und das Ihnen eine flexible Möglichkeit bietet, auf einfache Weise Erkenntnisse zu gewinnen.
### Wie installiere ich Aspose.Cells?
Sie können es über NuGet in Visual Studio installieren oder direkt von der [Download-Link](https://releases.aspose.com/cells/net/).
### Gibt es eine Testversion von Aspose.Cells?
Ja! Sie können es kostenlos testen, indem Sie die [Link zur kostenlosen Testversion](https://releases.aspose.com/).
### Kann ich mehrere Felder in einer Pivot-Tabelle sortieren?
Absolut! Sie können je nach Bedarf mehrere Felder hinzufügen und sortieren.
### Wo finde ich Unterstützung für Aspose.Cells?
Die Community ist sehr aktiv und Sie können Fragen in ihrem Forum stellen [Hier](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}