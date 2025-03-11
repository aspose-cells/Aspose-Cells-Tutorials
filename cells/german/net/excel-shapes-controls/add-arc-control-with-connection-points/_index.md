---
title: Arc Control mit Verbindungspunkten hinzufügen
linktitle: Arc Control mit Verbindungspunkten hinzufügen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Entdecken Sie in dieser ausführlichen Anleitung, wie Sie mit Aspose.Cells für .NET Bogensteuerelemente mit Verbindungspunkten hinzufügen.
weight: 27
url: /de/net/excel-shapes-controls/add-arc-control-with-connection-points/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Arc Control mit Verbindungspunkten hinzufügen

## Einführung
Wenn es darum geht, visuell ansprechende Excel-Berichte zu erstellen, spielen Illustrationen eine wichtige Rolle. Egal, ob Sie einen Finanzbericht oder eine Projektübersicht erstellen, die Verwendung von Formen wie Bögen kann Ihrer Datenpräsentation Tiefe und Klarheit verleihen. Heute tauchen wir tief in die Verwendung von Aspose.Cells für .NET ein, um Bogensteuerelemente mit Verbindungspunkten in Ihre Excel-Arbeitsblätter einzufügen. Wenn Sie sich also schon einmal gefragt haben, wie Sie Ihre Tabellen aufpeppen oder Ihre Daten zum Singen bringen können, lesen Sie weiter!
## Voraussetzungen
Bevor wir uns in die aufregende Programmierung stürzen, stellen wir sicher, dass Sie alles eingerichtet haben. Folgendes benötigen Sie:
1. .NET Framework: Stellen Sie sicher, dass Sie eine kompatible Version installiert haben. Aspose.Cells funktioniert mit mehreren Versionen, einschließlich .NET Core.
2.  Aspose.Cells für .NET: Sie müssen die Aspose.Cells-Bibliothek herunterladen und installieren. Sie können sie ganz einfach von der[Downloadlink](https://releases.aspose.com/cells/net/).
3. Eine gute IDE: Visual Studio, der treue Begleiter jedes .NET-Entwicklers, wird Ihnen dabei helfen, Ihre Programmiererfahrung zu optimieren.
4. Grundkenntnisse in C#: Wenn Sie sich mit C# auskennen, wird Ihnen dieses Tutorial leicht fallen.
5. Zugriff auf Ihr Dokumentverzeichnis: Wissen Sie, wo Sie Ihre Excel-Dateien speichern. Das ist wichtig, um Ihre Ausgabe effizient zu organisieren.
## Pakete importieren
Der nächste Schritt besteht darin, sicherzustellen, dass Sie die richtigen Pakete in Ihr Projekt importiert haben. Aspose.Cells für .NET hat verschiedene Funktionen, daher halten wir es einfach. Folgendes müssen Sie einbinden:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Über diese Namespaces haben Sie Zugriff auf alle Zeichenfunktionen und Zellenverwaltungsfunktionen, die Sie in diesem Handbuch verwenden werden.
## Schritt 1: Richten Sie Ihr Dokumentverzeichnis ein
Das Wichtigste zuerst: Richten wir ein Verzeichnis ein, in dem Sie diese tollen neuen Excel-Dateien speichern. Und so gehen wir vor:
```csharp
string dataDir = "Your Document Directory";
// Erstellen Sie ein Verzeichnis, falls es noch nicht vorhanden ist.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Dieser Code überprüft, ob der von Ihnen angegebene Ordner existiert. Wenn nicht, wird einer erstellt. Einfach, oder? Es ist immer gut, einen bestimmten Ort für Ihre Dateien zu haben, um Unordnung zu vermeiden.
## Schritt 2: Instanziieren einer Arbeitsmappe
Nachdem unser Verzeichnis nun bereit ist, erstellen wir eine neue Excel-Arbeitsmappe.
```csharp
Workbook excelbook = new Workbook();
```
 Durch einen Anruf bei`Workbook` Konstruktor sagen Sie im Wesentlichen: „Hey, lass uns eine neue Excel-Datei beginnen!“ Dies wird die Leinwand für alle Ihre Formen und Daten sein.
## Schritt 3: Hinzufügen der ersten Bogenform
Hier beginnt der Spaß! Fügen wir unsere erste Bogenform hinzu.
```csharp
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
Diese Codezeile fügt dem ersten Arbeitsblatt eine Bogenform hinzu. Die Parameter geben die Koordinaten des Bogens und die Winkel an, die seine Krümmung definieren. 
## Schritt 4: Passen Sie das Erscheinungsbild des Bogens an
Eine leere Bogenform ist wie eine Leinwand ohne Farbe – sie braucht ein wenig Gespür!
### Bogenfüllfarbe festlegen
```csharp
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
```
Dadurch wird der Bogen durchgehend blau. Sie können die Farbe in jeden beliebigen Farbton ändern, indem Sie`Color.Blue` für eine andere Farbe.
### Bogenplatzierung festlegen
```csharp
arc1.Placement = PlacementType.FreeFloating;
```
Wenn Sie die Platzierung auf „FreeFloating“ einstellen, kann sich der Bogen unabhängig von Zellgrenzen bewegen, was Ihnen Flexibilität bei der Positionierung gibt.
### Linienstärke und -stil anpassen
```csharp
arc1.Line.Weight = 1;      
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Hier definieren Sie Stärke und Stil der Linie und machen sie markanter und optisch ansprechender.
## Schritt 5: Hinzufügen einer weiteren Bogenform
Warum bei einer aufhören? Fügen wir eine weitere Bogenform hinzu, um unsere Excel-Grafik zu bereichern.
```csharp
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Wie der erste Bogen wird dieser an einer anderen Position hinzugefügt – hier kommt die Magie des Designs zum Tragen!
## Schritt 6: Passen Sie den zweiten Bogen an
Verleihen wir auch unserem zweiten Bogen etwas Persönlichkeit!
### Bogenlinienfarbe ändern
```csharp
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
```
Wir bleiben bei der einheitlichen Farbe Blau, Sie können aber jederzeit mischen und kombinieren, um zu sehen, was am besten zu Ihrem Design passt!
### Legen Sie ähnliche Eigenschaften wie beim ersten Bogen fest
Stellen Sie sicher, dass Sie diese ästhetischen Entscheidungen nachbilden:
```csharp
arc2.Placement = PlacementType.FreeFloating;
arc2.Line.Weight = 1;           
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Hier stellen Sie einfach sicher, dass der zweite Bogen mit dem ersten übereinstimmt, und sorgen so für ein einheitliches Erscheinungsbild auf Ihrem gesamten Arbeitsblatt.
## Schritt 7: Speichern Sie Ihre Arbeitsmappe
Kein Meisterwerk ist vollständig, ohne gespeichert zu werden, oder? Es ist an der Zeit, Ihre Bögen in eine Excel-Datei zu schreiben.
```csharp
excelbook.Save(dataDir + "book1.out.xls");
```
Diese Zeile speichert Ihre neu erstellten Bögen in einer Excel-Datei mit dem Namen „book1.out.xls“ in Ihrem angegebenen Verzeichnis.
## Abschluss
Herzlichen Glückwunsch! Sie haben gerade die Grundlagen des Hinzufügens von Bogensteuerelementen mit Verbindungspunkten in Ihren Excel-Tabellen mithilfe von Aspose.Cells für .NET gemeistert. Diese Funktion verschönert nicht nur Ihre Tabellen, sondern kann auch komplexe Daten leichter verständlich machen. Egal, ob Sie ein erfahrener Entwickler sind oder gerade erst anfangen, diese visuellen Elemente können Ihre Berichte von langweilig in großartig verwandeln.
## Häufig gestellte Fragen
### Was ist Aspose.Cells?
Aspose.Cells ist eine leistungsstarke .NET-Bibliothek, mit der Entwickler Excel-Dateien programmgesteuert erstellen und bearbeiten können.
### Kann ich Aspose.Cells kostenlos nutzen?
 Ja! Sie können eine kostenlose Testversion ausprobieren. Besuchen Sie[dieser Link](https://releases.aspose.com/) um zu beginnen.
### Wie füge ich außer Bögen andere Formen hinzu?
Sie können verschiedene im Aspose.Cells.Drawing-Namespace verfügbare Klassen verwenden, um verschiedene Formen wie Rechtecke, Kreise und mehr hinzuzufügen.
### Welche Dateitypen kann ich mit Aspose.Cells erstellen?
Sie können verschiedene Excel-Formate erstellen und bearbeiten, darunter XLS, XLSX, CSV und mehr.
### Gibt es technischen Support für Aspose.Cells?
 Auf jeden Fall! Sie können auf die[Aspose-Supportforum](https://forum.aspose.com/c/cells/9) um Hilfe.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
