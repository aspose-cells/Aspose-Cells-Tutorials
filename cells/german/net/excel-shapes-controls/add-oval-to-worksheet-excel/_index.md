---
title: Oval zum Arbeitsblatt in Excel hinzufügen
linktitle: Oval zum Arbeitsblatt in Excel hinzufügen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie mit Aspose.Cells für .NET einem Excel-Arbeitsblatt ein Oval hinzufügen. Schritt-für-Schritt-Anleitung mit ausführlichen Codeerklärungen.
weight: 17
url: /de/net/excel-shapes-controls/add-oval-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Oval zum Arbeitsblatt in Excel hinzufügen

## Einführung
Das Erstellen beeindruckender und interaktiver Excel-Dateien kann mehr als nur Zahlen und Formeln umfassen. Formen wie Ovale können optisch ansprechend sein oder funktionale Elemente in Ihren Arbeitsblättern bereitstellen. In diesem Tutorial erfahren Sie, wie Sie mit Aspose.Cells für .NET programmgesteuert Ovale zu einem Excel-Arbeitsblatt hinzufügen. Egal, ob Sie etwas Flair oder Funktionalität hinzufügen möchten, wir haben eine Schritt-für-Schritt-Anleitung für Sie, in der alles erklärt wird.
## Voraussetzungen
Bevor Sie sich in den Code vertiefen, müssen einige Dinge bereit sein:
1.  Aspose.Cells für .NET-Bibliothek: Sie können es herunterladen von[Hier](https://releases.aspose.com/cells/net/) oder installieren Sie es mit NuGet in Visual Studio.
2. Entwicklungsumgebung: AC# IDE wie Visual Studio.
3. Grundlegende Kenntnisse in C#: Sie sollten mit den grundlegenden Codierungskonzepten in C# vertraut sein.
 Denken Sie auch daran, Ihr Projekt einzurichten, indem Sie die Aspose.Cells für .NET-Bibliothek installieren. Wenn Sie noch keine Lizenz haben, können Sie eine[vorläufige Lizenz](https://purchase.aspose.com/temporary-license/) oder verwenden Sie die[Kostenlose Testversion](https://releases.aspose.com/) Version.
## Pakete importieren
Stellen Sie vor dem Schreiben von Code sicher, dass Sie die erforderlichen Namespaces eingefügt haben. Hier ist der C#-Codeausschnitt, um sicherzustellen, dass Sie die richtigen Bibliotheken verwenden:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## Schritt 1: Richten Sie Ihr Verzeichnis ein
Der erste Schritt beim Hinzufügen eines Ovals zu einem Excel-Blatt besteht darin, anzugeben, wo Ihre Excel-Datei gespeichert werden soll. Lassen Sie uns den Verzeichnispfad definieren und sicherstellen, dass das Verzeichnis existiert, bevor wir unsere Arbeit speichern.

Wir erstellen einen Verzeichnispfad und überprüfen, ob er existiert. Wenn der Ordner nicht existiert, wird er erstellt.
```csharp
// Der Pfad zum Dokumentverzeichnis.
string dataDir = "Your Document Directory";
// Erstellen Sie ein Verzeichnis, falls es noch nicht vorhanden ist.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Dieser Schritt ist wichtig, da er gewährleistet, dass Ihre Datei am richtigen Ort gespeichert wird und Sie später nicht auf Probleme mit dem Dateipfad stoßen.
## Schritt 2: Initialisieren einer neuen Arbeitsmappe
Als Nächstes müssen wir eine neue Arbeitsmappe erstellen, in die wir unsere ovalen Formen einfügen. Die Arbeitsmappe stellt eine Excel-Datei dar, und wir können Inhalte oder Formen hinzufügen.

 In diesem Schritt instanziieren wir ein neues`Workbook` Objekt, das als Container für unsere Excel-Datei dienen wird.
```csharp
// Instanziieren Sie eine neue Arbeitsmappe.
Workbook excelbook = new Workbook();
```
## Schritt 3: Fügen Sie die erste ovale Form hinzu
Jetzt kommt der spaßige Teil – das Hinzufügen einer ovalen Form zum Arbeitsblatt. Dieses Oval könnte ein visuelles Element wie eine Schaltfläche oder eine Hervorhebung darstellen. Wir beginnen, indem wir die erste ovale Form zum ersten Arbeitsblatt unserer Arbeitsmappe hinzufügen.

 Hier verwenden wir die`Shapes.AddOval()` Methode zum Erstellen eines Ovals auf dem Arbeitsblatt in einer bestimmten Zeile und Spalte.
```csharp
// Fügen Sie eine ovale Form hinzu.
Aspose.Cells.Drawing.Oval oval1 = excelbook.Worksheets[0].Shapes.AddOval(2, 0, 2, 0, 130, 160);
```
 Die Parameter im Inneren`AddOval()` sind wie folgt:
- Die ersten beiden Zahlen stellen die Zeile und Spalte für die obere linke Ecke des Ovals dar.
- Die nächsten beiden Zahlen stellen die Höhe und Breite des Ovals dar.
## Schritt 4: Legen Sie die Platzierung und den Stil des Ovals fest
 Sobald das Oval erstellt ist, können wir seine Position, Linienstärke und Strichart festlegen.`Placement` bestimmt, wie sich das Oval verhält, wenn Sie die Größe ändern oder Zellen im Arbeitsblatt verschieben.

Wir lassen das Oval freischwebend erscheinen und passen sein Erscheinungsbild an.
```csharp
// Legen Sie die Platzierung des Ovals fest.
oval1.Placement = PlacementType.FreeFloating;
// Stellen Sie die Linienstärke ein.
oval1.Line.Weight = 1;
// Legen Sie den Strichstil des Ovals fest.
oval1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Dadurch kann sich das Oval frei im Arbeitsblatt bewegen und seine Linienstärke und sein Stil werden für visuelle Konsistenz festgelegt.
## Schritt 5: Fügen Sie eine weitere ovale (Kreis-)Form hinzu
Warum bei einer aufhören? In diesem Schritt fügen wir eine weitere ovale Form hinzu und erstellen dieses Mal einen perfekten Kreis, indem wir Höhe und Breite gleich machen.

Wir erstellen ein weiteres Oval, platzieren es an einer anderen Stelle und sorgen durch gleiche Höhe und Breite für eine kreisrunde Form.
```csharp
// Fügen Sie eine weitere ovale (kreisförmige) Form hinzu.
Aspose.Cells.Drawing.Oval oval2 = excelbook.Worksheets[0].Shapes.AddOval(9, 0, 2, 15, 130, 130);
```
## Schritt 6: Stylen Sie das zweite Oval
Genau wie zuvor passen wir die Platzierung, Stärke und den Strichstil dieses zweiten Ovals (oder Kreises) an.

Wir wenden ähnliche Eigenschaften auf das zweite Oval an, um es dem Stil des ersten anzupassen.
```csharp
// Legen Sie die Platzierung des Ovals fest.
oval2.Placement = PlacementType.FreeFloating;
// Stellen Sie die Linienstärke ein.
oval2.Line.Weight = 1;
// Legen Sie den Strichstil des Ovals fest.
oval2.Line.DashStyle = MsoLineDashStyle.Solid;
```
## Schritt 7: Speichern Sie die Arbeitsmappe
Zum Schluss müssen wir die Arbeitsmappe mit den gerade hinzugefügten Ovalen speichern. Durch das Speichern der Datei wird sichergestellt, dass alle unsere Änderungen gespeichert werden.

Wir speichern die Arbeitsmappe in dem Verzeichnispfad, den wir zuvor definiert haben.
```csharp
// Speichern Sie die Excel-Datei.
excelbook.Save(dataDir + "book1.out.xls");
```
Und das war’s! Sie haben Ihrem Excel-Arbeitsblatt erfolgreich Ovale hinzugefügt und die Datei gespeichert.
## Abschluss
Das Hinzufügen von Formen wie Ovalen zu einem Excel-Blatt mit Aspose.Cells für .NET ist nicht nur unkompliziert, sondern auch eine unterhaltsame Möglichkeit, Ihre Tabellen mit zusätzlichen visuellen Elementen zu verbessern. Ob für Designzwecke oder zum Hinzufügen anklickbarer Elemente, Formen können eine wichtige Rolle dabei spielen, wie Ihre Excel-Dateien aussehen und funktionieren. Wenn Sie also das nächste Mal an einem Projekt arbeiten, das interaktive oder optisch ansprechende Excel-Blätter erfordert, wissen Sie genau, wie Sie diese perfekten Ovale hinzufügen!
## Häufig gestellte Fragen
### Kann ich mit Aspose.Cells für .NET andere Formen wie Rechtecke oder Linien hinzufügen?
 Ja, Sie können verschiedene Formen wie Rechtecke, Linien und Pfeile hinzufügen mit dem`Shapes` Sammlung in Aspose.Cells.
### Ist es möglich, die Größe der Ovale nach dem Hinzufügen zu ändern?
Auf jeden Fall! Sie können die Höhen- und Breiteneigenschaften der Ovale nach dem Hinzufügen ändern.
### In welchen Dateiformaten außer XLS kann ich die Arbeitsmappe speichern?
Aspose.Cells unterstützt mehrere Formate wie unter anderem XLSX, CSV und PDF.
### Kann ich die Farbe der Umrandung des Ovals ändern?
 Ja, Sie können die Linienfarbe des Ovals ändern mit dem`Line.Color` Eigentum.
### Ist für Aspose.Cells eine Lizenz erforderlich?
 Während Sie Aspose.Cells mit einer kostenlosen Testversion ausprobieren können, benötigen Sie eine[Lizenz](https://purchase.aspose.com/buy) für den langfristigen Gebrauch oder für den Zugriff auf erweiterte Funktionen.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
