---
title: Fügen Sie dem Arbeitsblatt in Excel ein Gruppenfeld hinzu
linktitle: Fügen Sie dem Arbeitsblatt in Excel ein Gruppenfeld hinzu
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie mit Aspose.Cells für .NET ein Gruppenfeld und Optionsfelder in Excel hinzufügen. Eine Schritt-für-Schritt-Anleitung für Entwickler aller Stufen.
weight: 24
url: /de/net/excel-shapes-controls/add-group-box-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Fügen Sie dem Arbeitsblatt in Excel ein Gruppenfeld hinzu

## Einführung
Wenn es um die Präsentation von Daten geht, ist Excel der König. Durch das Hinzufügen interaktiver Elemente wie Gruppenfelder können Sie Ihre Tabellen ansprechender und benutzerfreundlicher gestalten. Heute tauchen wir in die Welt von Aspose.Cells für .NET ein, einer leistungsstarken Bibliothek, mit der Sie Excel-Tabellen mühelos bearbeiten können. Aber keine Sorge, wenn Sie kein Programmiergenie sind – dieser Leitfaden unterteilt alles in einfache Schritte. Sind Sie bereit, Ihre Excel-Kenntnisse zu verbessern? Dann legen wir los!
## Voraussetzungen
Bevor wir uns in den Code stürzen, benötigen Sie ein paar Dinge:
1. Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem Computer installiert ist. Dort schreiben Sie den .NET-Code.
2.  Aspose.Cells für .NET: Sie müssen diese Bibliothek herunterladen. Sie finden sie[Hier](https://releases.aspose.com/cells/net/). 
3. Grundkenntnisse in C#: Ich werde zwar alles Schritt für Schritt erklären, aber ein wenig Verständnis von C# wird Ihnen helfen, den Anweisungen zu folgen.
## Pakete importieren
Für jedes Projekt müssen Sie zunächst die erforderlichen Pakete importieren. Dabei liegt Ihr Hauptaugenmerk auf Aspose.Cells. So geht's:
## Schritt 1: Öffnen Sie Ihr Projekt in Visual Studio
Starten Sie Visual Studio und öffnen Sie Ihr bestehendes Projekt oder erstellen Sie ein neues. 
## Schritt 2: Verweis auf Aspose.Cells hinzufügen
- Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf Ihr Projekt.
- Wählen Sie „NuGet-Pakete verwalten“ aus.
- Suchen Sie nach „Aspose.Cells“ und installieren Sie es. Dadurch können Sie alle von der Aspose.Cells-Bibliothek bereitgestellten Klassen und Methoden verwenden.
## Schritt 3: Using-Direktive einbinden
Fügen Sie oben in Ihrer C#-Datei den Namespace Aspose.Cells ein:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Dadurch erhalten Sie Zugriff auf die Klassen, die für die Arbeit mit Excel-Dateien erforderlich sind.
Nachdem wir nun alles eingerichtet haben, stürzen wir uns in das Herzstück des Tutorials: das Hinzufügen eines Gruppenfelds mit Optionsfeldern zu einem Excel-Arbeitsblatt. Der Übersichtlichkeit halber unterteilen wir diesen Vorgang in mehrere Schritte.
## Schritt 1: Richten Sie Ihr Dokumentverzeichnis ein
Bevor Sie eine Excel-Datei erstellen, müssen Sie festlegen, wo Sie sie speichern möchten. Erstellen wir ein Verzeichnis, falls es noch nicht vorhanden ist.
```csharp
// Der Pfad zum Dokumentenverzeichnis
string dataDir = "Your Document Directory"; // Geben Sie Ihren gewünschten Pfad an
// Erstellen Sie ein Verzeichnis, falls es noch nicht vorhanden ist.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Dieser Code prüft, ob das Verzeichnis, in dem die Excel-Datei gespeichert wird, existiert. Wenn nicht, wird eines erstellt – das ist, als ob Sie Ihren Arbeitsbereich vorbereiten, bevor Sie sich in das Projekt stürzen!
## Schritt 2: Instanziieren einer neuen Arbeitsmappe
Als Nächstes müssen Sie eine Excel-Arbeitsmappe erstellen, in die Sie Ihr Gruppenfeld hinzufügen.
```csharp
// Instanziieren Sie eine neue Arbeitsmappe.
Workbook excelbook = new Workbook();
```
Diese Zeile initialisiert eine neue Instanz einer Arbeitsmappe. Stellen Sie sich das so vor, als ob Sie eine neue, leere Excel-Datei öffnen würden, die für Änderungen bereit ist.
## Schritt 3: Ein Gruppenfeld hinzufügen
Fügen wir jetzt dieses Gruppenfeld hinzu. 
```csharp
// Fügen Sie dem ersten Arbeitsblatt ein Gruppenfeld hinzu.
GroupBox box = excelbook.Worksheets[0].Shapes.AddGroupBox(1, 0, 1, 0, 300, 250);
```
Hier fügen Sie an den angegebenen Koordinaten im ersten Arbeitsblatt ein Gruppenfeld hinzu. Die Parameter definieren die Position und Größe des Felds, genau wie die Positionierung von Möbeln in einem Raum!
## Schritt 4: Festlegen der Überschrift des Gruppenfelds
Geben wir Ihrem Gruppenfeld jetzt einen Titel!
```csharp
// Legen Sie die Überschrift des Gruppenfelds fest.
box.Text = "Age Groups";
box.Placement = PlacementType.FreeFloating;
```
 Die Zeichenfolge „Altersgruppen“ legt die Bezeichnung fest, die im Gruppenfeld angezeigt wird.`Placement` als`FreeFloating` ermöglicht die Beweglichkeit der Box – Flexibilität ist der Schlüssel!
## Schritt 5: Machen Sie das Gruppenfeld zweidimensional
3D klingt zwar vielleicht extravagant, wir streben hier jedoch einen klassischen Look an.
```csharp
// Machen Sie eine 2D-Box daraus.
box.Shadow = false;
```
Dieser Code entfernt den Schatteneffekt und verleiht der Box ein flaches Aussehen – wie ein einfaches Blatt Papier!
## Schritt 6: Optionsfelder hinzufügen
Lassen Sie uns die Sache etwas spannender gestalten, indem wir einige Optionsfelder für die Benutzereingabe hinzufügen.
## Schritt 6.1: Das erste Optionsfeld hinzufügen
```csharp
// Fügen Sie ein Optionsfeld hinzu.
Aspose.Cells.Drawing.RadioButton radio1 = excelbook.Worksheets[0].Shapes.AddRadioButton(3, 0, 2, 0, 30, 110);
// Legen Sie die Textzeichenfolge fest.
radio1.Text = "20-29";
// Legen Sie Zelle A1 als verknüpfte Zelle für das Optionsfeld fest.
radio1.LinkedCell = "A1";
```
Sie erstellen ein Optionsfeld für die Altersgruppe 20-29 und verknüpfen es mit Zelle A1 im Arbeitsblatt. Das bedeutet, dass Zelle A1 diese Auswahl widerspiegelt, wenn dieses Optionsfeld ausgewählt wird!
## Schritt 6.2: Anpassen des ersten Optionsfelds
Jetzt geben wir ihm etwas Stil.
```csharp
// Machen Sie das Optionsfeld dreidimensional.
radio1.Shadow = true;
// Legen Sie das Gewicht des Optionsfelds fest.
radio1.Line.Weight = 4;
// Legen Sie den Strichstil des Optionsfelds fest.
radio1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Indem wir einen Schatten hinzufügen und den Linienstil anpassen, verbessern wir die Sichtbarkeit der Schaltfläche. Das ist, als würden wir Dekorationen hinzufügen, damit sie von der Seite hervorsticht!
## Schritt 6.3: Wiederholen Sie den Vorgang für weitere Optionsfelder
Wiederholen Sie diesen Vorgang für weitere Altersgruppen:
```csharp
// Zweites Optionsfeld
Aspose.Cells.Drawing.RadioButton radio2 = excelbook.Worksheets[0].Shapes.AddRadioButton(6, 0, 2, 0, 30, 110);
radio2.Text = "30-39";
radio2.LinkedCell = "A1";
radio2.Shadow = true;
radio2.Line.Weight = 4;
radio2.Line.DashStyle = MsoLineDashStyle.Solid;
// Drittes Optionsfeld
Aspose.Cells.Drawing.RadioButton radio3 = excelbook.Worksheets[0].Shapes.AddRadioButton(9, 0, 2, 0, 30, 110);
radio3.Text = "40-49";
radio3.LinkedCell = "A1";
radio3.Shadow = true;
radio3.Line.Weight = 4;
radio3.Line.DashStyle = MsoLineDashStyle.Solid;
```
Jeder Optionsschalter dient zur Auswahl verschiedener Altersgruppen und ist mit derselben Zelle A1 verknüpft. Dies ermöglicht einen einfachen, benutzerfreundlichen Auswahlprozess.
## Schritt 7: Gruppieren Sie die Formen
Nachdem alles an seinem Platz ist, bringen wir Ordnung in die Sache, indem wir unsere Formen gruppieren. 
```csharp
// Holen Sie sich die Formen.
Aspose.Cells.Drawing.Shape[] shapeobjects = new Shape[] { box, radio1, radio2, radio3 };
// Gruppieren Sie die Formen.
Aspose.Cells.Drawing.GroupShape group = excelbook.Worksheets[0].Shapes.Group(shapeobjects);
```
Dieser Schritt verbindet alles zu einer zusammenhängenden Einheit. Es ist, als ob Sie einen Rahmen um Ihre Kunstsammlung legen – er verbindet sie auf wunderbare Weise!
## Schritt 8: Speichern Sie die Excel-Datei
Lassen Sie uns zum Schluss unser Meisterwerk retten!
```csharp
// Speichern Sie die Excel-Datei.
excelbook.Save(dataDir + "book1.out.xls");
```
Diese Codezeile schreibt Ihre Änderungen in eine neue Excel-Datei mit dem Namen „book1.out.xls“ in Ihrem angegebenen Verzeichnis. Wie beim Verschließen eines Umschlags ist Ihre Arbeit jetzt sicher gespeichert!
## Abschluss
Und da haben Sie es – eine vollständige Anleitung zum Hinzufügen eines Gruppenfelds und von Optionsfeldern zu einem Excel-Arbeitsblatt mit Aspose.Cells für .NET! Mit jedem Schritt haben Sie gelernt, wie Sie Excel programmgesteuert bearbeiten können, was Ihnen endlose Möglichkeiten zur Anpassung von Berichten, Datenvisualisierungen und mehr eröffnet. Das Schöne am Programmieren ist, dass Sie Aufgaben automatisieren und relativ einfach benutzerfreundliche Schnittstellen erstellen können – stellen Sie sich das Potenzial vor!
## Häufig gestellte Fragen
### Was ist Aspose.Cells?
Aspose.Cells ist eine .NET-Bibliothek zum Verwalten von Excel-Dateien, die Aufgaben wie das programmgesteuerte Lesen, Schreiben und Bearbeiten von Tabellen ermöglicht.
### Benötige ich Programmiererfahrung, um Aspose.Cells zu verwenden?
Einige Programmierkenntnisse sind zwar hilfreich, dieses Tutorial führt Sie jedoch durch die Grundlagen und ist somit auch für Anfänger zugänglich!
### Kann ich das Erscheinungsbild von Gruppenfeldern und Schaltflächen anpassen?
Auf jeden Fall! Aspose.Cells bietet umfangreiche Optionen zum Gestalten von Formen, einschließlich Farben, Größen und 3D-Effekten.
### Gibt es eine kostenlose Testversion für Aspose.Cells?
 Ja! Sie können es kostenlos testen, indem Sie[Kostenlose Aspose-Testversion](https://releases.aspose.com/).
### Wo finde ich weitere Ressourcen oder Support für Aspose.Cells?
 Der[Aspose Support Forum](https://forum.aspose.com/c/cells/9) ist ein hervorragender Ort, um Hilfe zu suchen und Wissen mit der Community zu teilen.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
