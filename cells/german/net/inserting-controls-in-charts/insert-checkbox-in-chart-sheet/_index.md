---
title: Kontrollkästchen in Diagrammblatt einfügen
linktitle: Kontrollkästchen in Diagrammblatt einfügen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in diesem Schritt-für-Schritt-Tutorial, wie Sie mit Aspose.Cells für .NET ganz einfach ein Kontrollkästchen in ein Excel-Diagrammblatt einfügen.
weight: 13
url: /de/net/inserting-controls-in-charts/insert-checkbox-in-chart-sheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kontrollkästchen in Diagrammblatt einfügen

## Einführung

Wenn Sie schon einmal ein Diagramm in Excel erstellt haben, wissen Sie, dass diese unglaublich leistungsfähig zur Visualisierung von Daten sein können. Aber was wäre, wenn Sie diese Interaktivität noch weiter steigern könnten, indem Sie direkt im Diagramm ein Kontrollkästchen hinzufügen? Das mag zwar ein wenig kompliziert klingen, ist aber mit der Aspose.Cells-Bibliothek für .NET eigentlich ganz unkompliziert. In diesem Tutorial führe ich Sie Schritt für Schritt durch den Prozess und mache ihn einfach und leicht nachvollziehbar.

## Voraussetzungen

Bevor wir mit dem Tutorial beginnen, stellen wir sicher, dass Sie alles eingerichtet haben. Folgendes benötigen Sie:

### Visual Studio installiert
- Zuallererst benötigen Sie Visual Studio. Wenn Sie es noch nicht installiert haben, können Sie es von der Microsoft-Site herunterladen.

### Aspose.Cells-Bibliothek
-  Das nächste wichtige Tool ist die Aspose.Cells-Bibliothek für .NET. Sie können sie ganz einfach über die[Aspose-Website](https://releases.aspose.com/cells/net/) zum Download. Wenn Sie lieber testen möchten, bevor Sie kaufen, gibt es auch eine[kostenlose Testversion verfügbar](https://releases.aspose.com/).

### Grundlegende Kenntnisse in C#
- Da wir Code schreiben werden, sind Grundkenntnisse in C# von Vorteil. Keine Sorge, ich erkläre Ihnen alles im Laufe der Zeit!

### Ausgabeverzeichnis
- Sie benötigen ein Verzeichnis, in dem Ihre Excel-Ausgabedateien gespeichert werden. Stellen Sie sicher, dass Sie dieses zur Hand haben.

Nachdem Sie diese Voraussetzungen von Ihrer Liste abgehakt haben, können wir loslegen!

## Pakete importieren

Richten wir zunächst unser Projekt in Visual Studio ein und importieren die erforderlichen Pakete. Hier ist eine einfache Schritt-für-Schritt-Anleitung:

### Neues Projekt erstellen

Öffnen Sie Visual Studio und erstellen Sie ein neues Konsolenanwendungsprojekt. Befolgen Sie einfach diese einfachen Schritte:
- Klicken Sie auf „Neues Projekt erstellen“.
- Wählen Sie aus den Optionen „Konsolen-App (.NET Framework)“ aus.
- Geben Sie Ihrem Projekt einen Namen wie beispielsweise „CheckboxInChart“.

### Installieren Sie Aspose.Cells über NuGet

Sobald Ihr Projekt eingerichtet ist, ist es an der Zeit, die Aspose.Cells-Bibliothek hinzuzufügen. Sie können dies über den NuGet-Paket-Manager tun:
- Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf Ihr Projekt und wählen Sie „NuGet-Pakete verwalten“ aus.
- Suchen Sie nach „Aspose.Cells“ und klicken Sie auf „Installieren“.
- Dadurch werden alle benötigten Abhängigkeiten einbezogen, sodass Sie problemlos mit der Verwendung der Bibliothek beginnen können.

### Erforderliche Using-Direktiven hinzufügen

 Ganz oben auf Ihrer`Program.cs` Fügen Sie die folgenden Using-Direktiven hinzu, um die Aspose.Cells-Funktionen verfügbar zu machen:
```csharp
using Aspose.Cells.Charts;
using System;
using Aspose.Cells.Drawing;
```

Jetzt haben Sie die Einrichtung abgeschlossen! Es ist, als würde man vor dem Bau eines Hauses ein solides Fundament legen – entscheidend für eine stabile Struktur.

Jetzt, da wir alles eingerichtet haben, können wir uns mit dem Codierungsteil befassen! Hier finden Sie eine detaillierte Anleitung zum Einfügen eines Kontrollkästchens in ein Diagrammblatt mit Aspose.Cells.

## Schritt 1: Definieren Sie Ihr Ausgabeverzeichnis

Bevor wir zum spannenden Teil kommen, müssen wir definieren, wo unsere Datei gespeichert werden soll. Sie sollten einen Ausgabeverzeichnispfad angeben.
```csharp
string outputDir = "C:\\YourOutputDirectory\\"; // Wechseln Sie in das angegebene Verzeichnis
```
 Ersetzen Sie unbedingt`"C:\\YourOutputDirectory\\"`mit dem Pfad, in dem Sie Ihre Datei speichern möchten. Betrachten Sie dies als das Einrichten Ihres Arbeitsbereichs; Sie müssen wissen, wo Sie Ihre Werkzeuge (oder in diesem Fall Ihre Excel-Datei) ablegen.

## Schritt 2: Instanziieren eines Arbeitsmappenobjekts

 Als nächstes erstellen wir eine Instanz des`Workbook` Klasse. Hier findet unsere gesamte Arbeit statt.
```csharp
Workbook workbook = new Workbook();
```
Diese Codezeile ist wie das Öffnen einer leeren Leinwand. Sie können mit dem Malen (oder in unserem Fall mit dem Programmieren) beginnen!

## Schritt 3: Hinzufügen eines Diagramms zum Arbeitsblatt

Jetzt ist es an der Zeit, Ihrer Arbeitsmappe ein Diagramm hinzuzufügen. So geht's:
```csharp
int index = workbook.Worksheets.Add(SheetType.Chart);
Worksheet sheet = workbook.Worksheets[index];
sheet.Charts.AddFloatingChart(ChartType.Column, 0, 0, 1024, 960);
```
In diesem Code sind Sie:
- Hinzufügen eines neuen Diagrammblatts zur Arbeitsmappe.
- Diagrammtyp auswählen. Hier wählen wir ein einfaches Säulendiagramm.
- Geben Sie die Abmessungen Ihres Diagramms an.

Betrachten Sie diesen Schritt als Auswahl des gewünschten Bilderrahmentyps, bevor Sie Ihr Kunstwerk hineinlegen.

## Schritt 4: Datenreihen zu Ihrem Diagramm hinzufügen

Füllen wir nun das Diagramm mit einigen Datenreihen. So fügen Sie Beispieldaten hinzu:
```csharp
sheet.Charts[0].NSeries.Add("{1,2,3}", false);
```
Diese Zeile ist entscheidend! Sie ist, als würden Sie Farbe auf Ihre Leinwand auftragen. Die Zahlen stellen einige Beispieldatenpunkte für Ihr Diagramm dar.

## Schritt 5: Hinzufügen eines Kontrollkästchens zum Diagramm

Jetzt kommen wir zum spaßigen Teil – dem Hinzufügen eines Kontrollkästchens zu unserem Diagramm. So geht's:
```csharp
sheet.Charts[0].Shapes.AddShapeInChart(MsoDrawingType.CheckBox, PlacementType.Move, 400, 400, 1000, 600);
sheet.Charts[0].Shapes[0].Text = "CheckBox 1";
```
In diesem Code:
- Wir geben den Typ der Form an, die wir hinzufügen möchten – in diesem Fall ein Kontrollkästchen.
- `PlacementType.Move` bedeutet, dass sich das Kontrollkästchen verschiebt, wenn sich das Diagramm verschiebt.
- Wir legen außerdem die Position und Größe des Kontrollkästchens innerhalb des Diagrammbereichs fest und legen abschließend die Textbeschriftung des Kontrollkästchens fest.

Das Hinzufügen eines Kontrollkästchens ist wie das Sahnehäubchen auf Ihrem Eisbecher: Es verbessert die gesamte Präsentation!

## Schritt 6: Speichern der Excel-Datei

Zum Schluss speichern wir unsere Arbeit. Hier ist das letzte Puzzleteil:
```csharp
workbook.Save(outputDir + "InsertCheckboxInChartSheet_out.xlsx");
```
Diese Zeile speichert Ihre neu erstellte Excel-Datei mit dem Kontrollkästchen im angegebenen Ausgabeverzeichnis. Das ist so, als ob Sie Ihr Kunstwerk in eine Schutzhülle einschließen würden!

## Abschluss

Und da haben Sie es! Sie haben erfolgreich ein Kontrollkästchen zu einem Diagrammblatt in einer Excel-Datei hinzugefügt, indem Sie Aspose.Cells für .NET verwenden. Indem Sie diese Schritte befolgen, können Sie interaktive und dynamische Excel-Tabellen erstellen, die großartige Funktionalität bieten und Ihre Datenvisualisierungen noch ansprechender machen.

## Häufig gestellte Fragen

### Was ist Aspose.Cells?  
Aspose.Cells ist eine leistungsstarke Bibliothek zum Erstellen und Bearbeiten von Excel-Dateien in .NET-Anwendungen.

### Kann ich Aspose.Cells kostenlos nutzen?  
 Ja, Aspose bietet eine kostenlose Testversion an. Sie können mit der verfügbaren Testversion beginnen[Hier](https://releases.aspose.com/).

### Ist das Hinzufügen eines Kontrollkästchens zu einem Diagrammblatt kompliziert?  
Überhaupt nicht! Wie in diesem Tutorial gezeigt, ist dies mit nur wenigen einfachen Codezeilen möglich.

### Wo kann ich Aspose.Cells kaufen?  
 Sie können Aspose.Cells von ihrem[Kauflink](https://purchase.aspose.com/buy).

### Wie kann ich Unterstützung erhalten, wenn Probleme auftreten?  
 Aspose bietet ein Support-Forum, in dem Sie Fragen stellen und Lösungen finden können. Schauen Sie sich deren[Support-Seite](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
