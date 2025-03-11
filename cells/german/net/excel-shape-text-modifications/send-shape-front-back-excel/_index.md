---
title: Form in Excel nach vorne oder hinten senden
linktitle: Form in Excel nach vorne oder hinten senden
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Entdecken Sie, wie Sie mit Aspose.Cells für .NET Formen in Excel nach vorne oder hinten verschieben. Diese Anleitung bietet eine Schritt-für-Schritt-Anleitung mit Tipps.
weight: 16
url: /de/net/excel-shape-text-modifications/send-shape-front-back-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Form in Excel nach vorne oder hinten senden

## Einführung
Wenn Sie mit Excel-Dateien arbeiten, benötigen Sie möglicherweise mehr Kontrolle über die visuellen Elemente in Ihrer Tabelle. Formen wie Bilder und Grafiken können die Darstellung Ihrer Daten verbessern. Aber was passiert, wenn sich diese Formen überlappen oder neu angeordnet werden müssen? Hier glänzt Aspose.Cells für .NET. In diesem Tutorial führen wir Sie durch die Schritte zum Bearbeiten von Formen in einem Excel-Arbeitsblatt, insbesondere zum Verschieben von Formen vor oder hinter andere Formen. Wenn Sie bereit sind, Ihr Excel-Spiel zu verbessern, legen wir gleich los!
## Voraussetzungen
Bevor wir beginnen, müssen Sie einige Dinge vorbereitet haben:
1.  Installation der Aspose.Cells-Bibliothek: Stellen Sie sicher, dass Sie die Aspose.Cells-Bibliothek für .NET installiert haben. Sie finden sie[Hier](https://releases.aspose.com/cells/net/).
2. Entwicklungsumgebung: Stellen Sie sicher, dass Sie eine Entwicklungsumgebung mit .NET-Unterstützung eingerichtet haben, beispielsweise Visual Studio.
3. Grundkenntnisse in C#: Wenn Sie mit der C#-Programmierung vertraut sind, verstehen Sie die Codeausschnitte besser.
Okay, Sie haben alle Kästchen auf der Liste der Voraussetzungen angekreuzt? Super! Kommen wir nun zum spaßigen Teil – dem Schreiben von Code!
## Pakete importieren
Bevor wir uns mit der eigentlichen Codierung befassen, importieren wir die erforderlichen Pakete. Fügen Sie einfach die folgende using-Direktive oben in Ihrer C#-Datei hinzu:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
Diese Namespaces sind von entscheidender Bedeutung, da sie die Klassen und Methoden enthalten, die wir zum Bearbeiten von Excel-Dateien und -Formen verwenden.
## Schritt 1: Definieren Sie Ihre Dateipfade
In diesem ersten Schritt müssen wir das Quell- und Ausgabeverzeichnis festlegen. Hier befindet sich Ihre Excel-Datei und hier möchten Sie die geänderte Datei speichern.
```csharp
//Quellverzeichnis
string sourceDir = "Your Document Directory";
//Ausgabeverzeichnis
string outputDir = "Your Document Directory";
```
 Ersetzen`"Your Document Directory"` durch den tatsächlichen Pfad, in dem Ihre Excel-Dateien gespeichert sind.
## Schritt 2: Laden Sie die Arbeitsmappe
Nachdem wir nun unsere Verzeichnisse festgelegt haben, laden wir die Arbeitsmappe (die Excel-Datei), die die Formen enthält, die wir bearbeiten möchten.
```csharp
//Quell-Excel-Datei laden
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
 Diese Codezeile initialisiert eine neue`Workbook` Objekt, das die angegebene Excel-Datei in den Speicher lädt, damit wir damit arbeiten können.
## Schritt 3: Zugriff auf das Arbeitsblatt 
Als Nächstes müssen wir auf das spezifische Arbeitsblatt zugreifen, in dem sich unsere Formen befinden. Für dieses Beispiel verwenden wir das erste Arbeitsblatt.
```csharp
//Greifen Sie auf das erste Arbeitsblatt zu
Worksheet ws = wb.Worksheets[0];
```
 Durch Verweisen`Worksheets[0]`, wir zielen auf das erste Blatt unserer Arbeitsmappe. Wenn sich Ihre Formen auf einem anderen Blatt befinden, passen Sie den Index entsprechend an.
## Schritt 4: Zugriff auf die Formen
Nachdem wir nun auf das Arbeitsblatt zugreifen können, greifen wir auf die Formen zu, die uns interessieren. In diesem Beispiel greifen wir auf die erste und vierte Form zu.
```csharp
//Zugriff auf die erste und vierte Form
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
Diese Linien erhalten basierend auf ihrem Index die spezifischen Formen aus dem Arbeitsblatt.
## Schritt 5: Drucken Sie die Z-Order-Position der Formen
Bevor wir Formen verschieben, drucken wir ihre aktuelle Z-Order-Position aus. So können wir ihre Positionierung verfolgen, bevor wir Änderungen vornehmen.
```csharp
//Drucken Sie die Z-Order-Position der Form
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
 Durch einen Anruf`ZOrderPosition`können wir sehen, wo sich jede Form in der Zeichenreihenfolge befindet.
## Schritt 6: Senden Sie die erste Form nach vorne
Jetzt geht es ans Werk! Schicken wir die erste Form an den Anfang der Z-Reihenfolge.
```csharp
//Schicken Sie diese Form nach vorne
sh1.ToFrontOrBack(2);
```
 Durch das Vorbeigehen`2` Zu`ToFrontOrBack`, weisen wir Aspose.Cells an, diese Form nach vorne zu bringen. 
## Schritt 7: Drucken Sie die Z-Order-Position der zweiten Form
Bevor wir die zweite Form nach hinten schicken, überprüfen wir, wo sie positioniert ist.
```csharp
//Drucken Sie die Z-Order-Position der Form
Console.WriteLine("Z-Order Shape 4: " + sh4.ZOrderPosition);
```
Dies gibt uns Einblick in die Position der vierten Form, bevor wir Änderungen vornehmen.
## Schritt 8: Senden Sie die vierte Form nach hinten
Schließlich senden wir die vierte Form an das Ende des Z-Order-Stapels.
```csharp
//Diese Form nach hinten schicken
sh4.ToFrontOrBack(-2);
```
 Verwenden von`-2` da der Parameter die Form an das hintere Ende des Stapels schickt und so sicherstellt, dass sie andere Formen oder Texte nicht behindert.
## Schritt 9: Speichern der Arbeitsmappe 
Der letzte Schritt besteht darin, Ihre Arbeitsmappe mit den neu positionierten Formen zu speichern.
```csharp
//Speichern der Excel-Ausgabedatei
wb.Save(outputDir + "outputToFrontOrBack.xlsx");
```
Dieser Befehl speichert die geänderte Arbeitsmappe im angegebenen Ausgabeverzeichnis.
## Schritt 10: Bestätigungsnachricht
Lassen Sie uns abschließend eine einfache Bestätigung senden, damit wir wissen, dass unsere Aufgabe erfolgreich abgeschlossen wurde.
```csharp
Console.WriteLine("SendShapeFrontOrBackInWorksheet executed successfully.\r\n");
```
Und damit ist der Code für unser Tutorial abgeschlossen!
## Abschluss
Die Bearbeitung von Formen in Excel mit Aspose.Cells für .NET ist nicht nur unkompliziert, sondern auch leistungsstark. Wenn Sie dieser Anleitung folgen, sollten Sie nun in der Lage sein, Formen problemlos nach vorne oder hinten zu verschieben, was Ihnen eine bessere Kontrolle über Ihre Excel-Präsentationen ermöglicht. Mit diesen Tools sind Sie bereit, die visuelle Attraktivität Ihrer Tabellen zu verbessern.
## Häufig gestellte Fragen
### Welche Programmiersprache benötige ich für Aspose.Cells?  
Sie müssen C# oder eine andere .NET-unterstützte Sprache verwenden, um mit Aspose.Cells zu arbeiten.
### Kann ich Aspose.Cells kostenlos testen?  
 Ja, Sie können mit einer kostenlosen Testversion von Aspose.Cells beginnen[Hier](https://releases.aspose.com/).
### Welche Art von Formen kann ich in Excel bearbeiten?  
Sie können verschiedene Formen wie Rechtecke, Kreise, Linien und Bilder bearbeiten.
### Wie kann ich Support für Aspose.Cells erhalten?  
 Sie können das Community-Forum für Support oder Fragen besuchen[Hier](https://forum.aspose.com/c/cells/9).
### Gibt es eine temporäre Lizenz für Aspose.Cells?  
 Ja, Sie können eine temporäre Lizenz anfordern[Hier](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
