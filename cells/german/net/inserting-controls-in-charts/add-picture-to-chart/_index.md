---
"description": "Erfahren Sie, wie Sie mit Aspose.Cells für .NET ganz einfach Bilder zu Excel-Diagrammen hinzufügen. Optimieren Sie Ihre Diagramme und Präsentationen in nur wenigen Schritten."
"linktitle": "Bild zum Diagramm hinzufügen"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Bild zum Diagramm hinzufügen"
"url": "/de/net/inserting-controls-in-charts/add-picture-to-chart/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Bild zum Diagramm hinzufügen

## Einführung

Haben Sie genug von langweiligen Diagrammen ohne persönliche Note? Möchten Sie lernen, wie Sie Ihre Excel-Grafiken mit Bildern aufpeppen können? Dann haben Sie Glück! In diesem Tutorial tauchen wir in die Welt von Aspose.Cells für .NET ein und lernen, wie Sie Bilder zu Diagrammen in Excel hinzufügen. Also, schnappen Sie sich Ihre Lieblingstasse Kaffee und los geht‘s!

## Voraussetzungen

Bevor wir uns in die Einzelheiten der Codierung stürzen, müssen Sie einige Voraussetzungen erfüllen, damit alles reibungslos verläuft:

- Visual Studio: Hier schreiben und führen Sie Ihren .NET-Code aus. Stellen Sie sicher, dass Visual Studio installiert ist.
- Aspose.Cells für .NET: Sie benötigen diese Bibliothek für die Arbeit mit Excel-Dateien. Sie können [Laden Sie es hier herunter](https://releases.aspose.com/cells/net/).
- Grundlegende Kenntnisse in C#: Ich werde Sie zwar durch den Code führen, aber wenn Sie die Grundlagen von C# beherrschen, wird alles klarer.

### Installationsschritte

1. Installieren Sie Aspose.Cells: Sie können Aspose.Cells über den NuGet-Paketmanager zu Ihrem Visual Studio-Projekt hinzufügen. Navigieren Sie dazu zu „Tools“ > „NuGet-Paketmanager“ > „NuGet-Pakete für Lösung verwalten“ und suchen Sie nach „Aspose.Cells“. Klicken Sie auf „Installieren“.
2. Einrichten Ihres Projekts: Erstellen Sie in Visual Studio ein neues C#-Konsolenanwendungsprojekt.

## Pakete importieren

Sobald Sie alles eingerichtet haben, importieren Sie im nächsten Schritt die erforderlichen Pakete in Ihr Projekt. So geht's:

### Importieren der erforderlichen Namespaces

Oben in Ihrer C#-Codedatei müssen Sie die folgenden Namespaces importieren:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
using System.IO;
```

Dies sagt Ihrem Programm: „Hey! Ich werde diese coolen Funktionen von Aspose.Cells verwenden.“

Nachdem wir nun die Voraussetzungen geschaffen haben, wollen wir den Prozess in mundgerechte Schritte unterteilen. 

## Schritt 1: Definieren Sie Ihre Verzeichnisse

Zuerst müssen wir die Pfade für unsere Ein- und Ausgabedateien einrichten. Dieser Schritt ist entscheidend, da wir wissen müssen, wo sich unsere vorhandene Excel-Datei befindet und wo die geänderte Datei gespeichert werden soll.

```csharp
//Quellverzeichnis
string sourceDir = "Your Document Directory/";

//Ausgabeverzeichnis
string outputDir = "Your Output Directory/";
```

Ersetzen `Your Document Directory` Und `Your Output Directory` mit tatsächlichen Pfaden auf Ihrem Computer. 

## Schritt 2: Laden Sie die vorhandene Arbeitsmappe

Laden wir nun die vorhandene Excel-Datei, in der wir unser Bild zum Diagramm hinzufügen möchten.

```csharp
// Öffnen Sie die vorhandene Datei.
Workbook workbook = new Workbook(sourceDir + "sampleAddingPictureInChart.xls");
```

Dieser Code öffnet die Arbeitsmappe und macht sie zur Bearbeitung bereit.

## Schritt 3: Bereiten Sie den Bildstream vor

Bevor wir das Bild hinzufügen, müssen wir das Bild lesen, das wir in das Diagramm einfügen möchten. 

```csharp
// Holen Sie sich eine Bilddatei zum Stream.
FileStream stream = new FileStream(sourceDir + "sampleAddingPictureInChart.png", FileMode.Open, FileAccess.Read);
```

Stellen Sie sicher, dass Sie das Bild im angegebenen Verzeichnis gespeichert haben.

## Schritt 4: Zielen Sie auf das Diagramm

Geben wir nun an, welchem Diagramm wir unser Bild hinzufügen möchten. In diesem Beispiel wählen wir das erste Diagramm im ersten Arbeitsblatt aus.

```csharp
// Holen Sie sich das Designerdiagramm im zweiten Blatt.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

Sie können auf jedes Arbeitsblatt zugreifen, indem Sie den Index entsprechend ändern.

## Schritt 5: Fügen Sie das Bild zum Diagramm hinzu

Nachdem Sie das Diagramm ausgewählt haben, ist es Zeit, das Bild hinzuzufügen! 

```csharp
// Fügen Sie dem Diagramm ein neues Bild hinzu.
Aspose.Cells.Drawing.Picture pic0 = chart.Shapes.AddPictureInChart(50, 50, stream, 200, 200);
```

Hier, `50` Und `50` sind die X- und Y-Koordinaten, an denen das Bild platziert wird, und `200` ist die Breite und Höhe des Bildes.

## Schritt 6: Passen Sie das Linienformat des Bildes an

Möchten Sie Ihrem Bild etwas Flair verleihen? Sie können den Rahmen anpassen! So geht's:

```csharp
// Holen Sie sich den Linienformattyp des Bildes.
Aspose.Cells.Drawing.LineFormat lineformat = pic0.Line; 

// Legen Sie den Strichstil fest.
lineformat.DashStyle = MsoLineDashStyle.Solid;

// Stellen Sie die Linienstärke ein.
lineformat.Weight = 4;    
```

Mit diesem Snippet können Sie das Aussehen und die Breite des Rahmens festlegen. Wählen Sie einen Stil, der zu Ihrer Präsentation passt!

## Schritt 7: Speichern der geänderten Arbeitsmappe

Nach all der harten Arbeit speichern wir Ihre Änderungen, indem wir die folgende Codezeile ausführen:

```csharp
// Speichern Sie die Excel-Datei.
workbook.Save(outputDir + "outputAddingPictureInChart.xls");
```

Jetzt ist Ihr Bild erfolgreich in das Diagramm integriert und Ihre Ausgabedatei ist zur Anzeige bereit!

## Schritt 8: Erfolg anzeigen

Abschließend können Sie eine einfache Nachricht hinzufügen, um zu bestätigen, dass Ihr Vorgang erfolgreich war:

```csharp
Console.WriteLine("AddingPictureInChart executed successfully.");
```

## Abschluss

In diesem Tutorial haben wir gezeigt, wie Sie Ihren Excel-Diagrammen durch das Hinzufügen von Bildern mit Aspose.Cells für .NET Persönlichkeit verleihen. Mit nur wenigen Schritten können Sie Ihre Präsentationen von banal zu einprägsam machen. Worauf warten Sie noch? Probieren Sie es aus und lassen Sie Ihre Diagramme glänzen!

## Häufig gestellte Fragen

### Kann ich einem einzelnen Diagramm mehrere Bilder hinzufügen?
Ja! Sie können anrufen unter `AddPictureInChart` Methode mehrmals, um so viele Bilder hinzuzufügen, wie Sie möchten.

### Welche Bildformate unterstützt Aspose.Cells?
Aspose.Cells unterstützt eine Vielzahl von Bildformaten, darunter PNG, JPEG, BMP und GIF.

### Kann ich die Position des Bildes anpassen?
Sicher! Die X- und Y-Koordinaten im `AddPictureInChart` Methode ermöglicht eine präzise Positionierung.

### Ist die Nutzung von Aspose.Cells kostenlos?
Aspose.Cells bietet eine kostenlose Testversion an, für den vollen Funktionsumfang ist jedoch eine Lizenz erforderlich. Die Preise finden Sie [Hier](https://purchase.aspose.com/buy).

### Wo finde ich weitere Beispiele?
Schauen Sie sich die [Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/net/) für detailliertere Beispiele und Funktionen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}