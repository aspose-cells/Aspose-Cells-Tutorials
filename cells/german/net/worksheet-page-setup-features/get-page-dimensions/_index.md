---
"description": "Erfahren Sie, wie Sie mit Aspose.Cells für .NET Seitenabmessungen in einem Excel-Arbeitsblatt erhalten. Eine Schritt-für-Schritt-Anleitung zum Anpassen der Papierformate A2, A3, A4 und Letter."
"linktitle": "Seitenabmessungen des Arbeitsblatts abrufen"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Seitenabmessungen des Arbeitsblatts abrufen"
"url": "/de/net/worksheet-page-setup-features/get-page-dimensions/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Seitenabmessungen des Arbeitsblatts abrufen

## Einführung
Wenn Sie programmgesteuert mit Aspose.Cells für .NET mit Excel-Dateien arbeiten, müssen Sie möglicherweise auf die Seitenabmessungen eines Arbeitsblatts zugreifen und diese festlegen. Die Kenntnis der Abmessungen kann beim Layout, Drucken und Anpassen von Excel-Tabellen für bestimmte Zwecke hilfreich sein. In diesem Artikel erfahren Sie, wie Sie mit Aspose.Cells für .NET verschiedene Seitenabmessungen in Excel abrufen und anzeigen. Wir führen Sie Schritt für Schritt durch, damit Sie alle Details kennen und sicher loslegen können.
## Voraussetzungen
Bevor wir loslegen, stellen wir sicher, dass Sie alles haben, was Sie brauchen, um diesem Tutorial zu folgen.
1. Aspose.Cells für .NET: Stellen Sie sicher, dass Sie Aspose.Cells für .NET installiert haben. Sie können [Laden Sie die Bibliothek hier herunter](https://releases.aspose.com/cells/net/) oder installieren Sie es über NuGet in Ihrem .NET-Projekt.
2. .NET-Umgebung: Eine kompatible .NET-Entwicklungsumgebung (z. B. Visual Studio).
3. Lizenz-Setup: Für die volle Funktionalität von Aspose.Cells benötigen Sie eine Lizenz. Sie können [Fordern Sie eine kostenlose temporäre Lizenz an](https://purchase.aspose.com/temporary-license/) zu Auswertungszwecken.
Beginnen Sie mit der kostenlosen Testversion von Aspose.Cells, wenn Sie es zum ersten Mal testen.
## Pakete importieren
Bevor wir uns in den Code stürzen, müssen Sie den Aspose.Cells-Namespace in Ihr Projekt importieren, um auf alle erforderlichen Klassen und Methoden zuzugreifen.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Lassen Sie uns den Vorgang in einfache Schritte unterteilen. Hier greifen wir auf verschiedene Papierformate zu, wenden sie auf ein Arbeitsblatt an und drucken die Abmessungen für jedes Format aus.
## Schritt 1: Erstellen einer Arbeitsmappeninstanz
Der erste Schritt besteht darin, eine Instanz des `Workbook` Klasse. Dieses Objekt fungiert als unsere Hauptarbeitsmappe mit Arbeitsblättern, die wir bearbeiten können.
```csharp
Workbook book = new Workbook();
```
Denken Sie an `Workbook` als Hauptcontainer für Ihre Excel-Datei. Wir benötigen ihn für den Zugriff und die Steuerung einzelner Arbeitsblätter.
## Schritt 2: Zugriff auf das erste Arbeitsblatt
Als Nächstes greifen wir auf das erste Arbeitsblatt in der Arbeitsmappe zu. Standardmäßig enthält eine neue Arbeitsmappe ein Blatt, sodass wir direkt über einen Index von `0`.
```csharp
Worksheet sheet = book.Worksheets[0];
```
Der `Worksheets` Sammlung in `Workbook` ermöglicht uns den Zugriff auf jedes Arbeitsblatt über den Index. Hier greifen wir auf das erste Blatt zu, um mit der Festlegung der Seitenabmessungen zu beginnen.
## Schritt 3: Papiergröße auf A2 einstellen und Abmessungen anzeigen
Nachdem wir nun Zugriff auf unser Arbeitsblatt haben, stellen wir das Papierformat auf A2 ein. Das Einstellen des Papierformats ist nützlich, um die Seite vor dem Drucken oder Exportieren zu formatieren. Sobald wir das Papierformat eingestellt haben, drucken wir die Seitenabmessungen in Zoll.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Hier ändern wir die `PaperSize` Eigentum zu `PaperA2`. Nachdem Sie die Größe eingestellt haben, `PageSetup.PaperWidth` Und `PageSetup.PaperHeight` Breite und Höhe des Blattes in Zoll abrufen. So erhalten wir einen schnellen Überblick über die Seitenmaße.
## Schritt 4: Papiergröße auf A3 und Anzeigeabmessungen einstellen
Passen Sie die Seitenabmessungen mit den gleichen Schritten wie oben auf A3 an. Diese Änderung ist nützlich für etwas größere Ausdrucke oder um mehr Inhalt auf eine Seite zu bringen.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Das Format A3 ist doppelt so groß wie A4 und eignet sich daher gut für große Tabellen oder detaillierte Diagramme. Durch Ändern der Papiergröße lässt sich das Arbeitsblattlayout entsprechend anpassen.
## Schritt 5: Papiergröße auf A4 und Anzeigeabmessungen einstellen
Stellen wir nun das Papierformat auf A4 ein. Dies ist das am häufigsten verwendete Seitenformat für den Druck von Dokumenten. Die aktualisierten Abmessungen werden anschließend angezeigt.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Wenn Ihr Zieldokument ein Standarddokumentformat ist, ist A4 in der Regel die beste Größe. Die Kenntnis der Abmessungen kann beim Anpassen des Inhaltslayouts helfen, um Druckprobleme zu vermeiden.
## Schritt 6: Papierformat auf Letter und Anzeigeabmessungen einstellen
Zum Schluss stellen wir das Papierformat auf das in Nordamerika übliche Letter-Format ein. Drucken wir die Abmessungen noch einmal aus.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
In Nordamerika wird für Dokumente häufig das Letter-Format verwendet. Daher ist die Einstellung dieser Größe bei der Zusammenarbeit mit dort ansässigen Teams oder Kunden hilfreich.
## Abschluss
In diesem Tutorial haben wir gezeigt, wie Sie mit Aspose.Cells für .NET Seitenmaße für verschiedene Papierformate festlegen und abrufen. Durch die Konfiguration von Seitengrößen wie A2, A3, A4 und Letter können Sie Excel-Arbeitsblätter an spezifische Druck- und Layoutanforderungen anpassen. Diese Kontrolle über die Seitenmaße ist besonders wertvoll für professionelle Berichte und Präsentationen, da sie sicherstellt, dass Ihre Inhalte perfekt auf jede Seitengröße passen.
## Häufig gestellte Fragen
### Wie kann ich die Ausrichtung der Seite in Aspose.Cells ändern?  
Sie können die Ausrichtung ändern, indem Sie `PageSetup.Orientation` und setzen Sie sie auf `PageOrientationType.Podertrait` or `PageOrientationType.Landscape`.
### Kann ich in Aspose.Cells benutzerdefinierte Seitenabmessungen festlegen?  
Ja, Sie können benutzerdefinierte Seitenabmessungen festlegen, indem Sie die Ränder und Skalierungsoptionen unter `PageSetup` für mehr Kontrolle.
### Was ist die Standardpapiergröße in Aspose.Cells?  
Das Standardpapierformat ist in der Regel A4. Dies kann jedoch von regionalen Einstellungen abhängen und kann bei Bedarf angepasst werden.
### Ist es möglich, Seitenlayouts in Aspose.Cells in der Vorschau anzuzeigen?  
Während Aspose.Cells keine grafische Vorschau bietet, können Sie Layouts programmgesteuert einrichten und Druckvorschauen in Excel verwenden.
### Wie installiere ich Aspose.Cells für .NET?  
Sie können Aspose.Cells mit dem NuGet Package Manager in Visual Studio installieren oder die DLL von der [Aspose.Cells-Downloadseite](https://releases.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}