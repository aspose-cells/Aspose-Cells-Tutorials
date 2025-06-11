---
"description": "Erfahren Sie, wie Sie mit Aspose.Cells für .NET ein Oval zu einem Excel-Arbeitsblatt hinzufügen. Schritt-für-Schritt-Anleitung mit detaillierten Code-Erklärungen."
"linktitle": "Oval zum Arbeitsblatt in Excel hinzufügen"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Oval zum Arbeitsblatt in Excel hinzufügen"
"url": "/de/net/excel-shapes-controls/add-oval-to-worksheet-excel/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Oval zum Arbeitsblatt in Excel hinzufügen

## Einführung
Das Erstellen ansprechender und interaktiver Excel-Dateien kann mehr als nur Zahlen und Formeln umfassen. Formen wie Ovale können Ihre Arbeitsblätter optisch ansprechender gestalten oder funktionale Elemente hinzufügen. In diesem Tutorial erfahren Sie, wie Sie mit Aspose.Cells für .NET programmgesteuert Ovale in ein Excel-Arbeitsblatt einfügen. Egal, ob Sie etwas Flair oder Funktionalität hinzufügen möchten – wir bieten Ihnen eine Schritt-für-Schritt-Anleitung, die alles detailliert erklärt.
## Voraussetzungen
Bevor Sie sich in den Code vertiefen, müssen Sie einige Dinge vorbereitet haben:
1. Aspose.Cells für .NET-Bibliothek: Sie können es herunterladen von [Hier](https://releases.aspose.com/cells/net/) oder installieren Sie es mit NuGet in Visual Studio.
2. Entwicklungsumgebung: AC# IDE wie Visual Studio.
3. Grundlegende Kenntnisse in C#: Sie sollten mit den grundlegenden Codierungskonzepten in C# vertraut sein.
Denken Sie außerdem daran, Ihr Projekt einzurichten, indem Sie die Aspose.Cells für .NET-Bibliothek installieren. Wenn Sie noch keine Lizenz haben, können Sie eine beantragen. [vorläufige Lizenz](https://purchase.aspose.com/temporary-license/) oder verwenden Sie die [kostenlose Testversion](https://releases.aspose.com/) Version.
## Pakete importieren
Stellen Sie vor dem Schreiben von Code sicher, dass Sie die erforderlichen Namespaces eingefügt haben. Hier ist der C#-Codeausschnitt, um sicherzustellen, dass Sie die richtigen Bibliotheken verwenden:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## Schritt 1: Richten Sie Ihr Verzeichnis ein
Der erste Schritt beim Hinzufügen eines Ovals zu einem Excel-Blatt besteht darin, den Speicherort der Excel-Datei anzugeben. Definieren Sie den Verzeichnispfad und stellen Sie sicher, dass das Verzeichnis existiert, bevor Sie unsere Arbeit speichern.

Wir erstellen einen Verzeichnispfad und prüfen, ob er existiert. Falls der Ordner nicht existiert, wird er erstellt.
```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "Your Document Directory";
// Erstellen Sie ein Verzeichnis, falls es noch nicht vorhanden ist.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Dieser Schritt ist von entscheidender Bedeutung, da er sicherstellt, dass Ihre Datei am richtigen Ort gespeichert wird und Sie später nicht auf Probleme mit dem Dateipfad stoßen.
## Schritt 2: Initialisieren einer neuen Arbeitsmappe
Als Nächstes erstellen wir eine neue Arbeitsmappe, in die wir unsere ovalen Formen einfügen. Die Arbeitsmappe stellt eine Excel-Datei dar, in die wir Inhalte oder Formen einfügen können.

In diesem Schritt instanziieren wir ein neues `Workbook` Objekt, das als Container für unsere Excel-Datei dienen wird.
```csharp
// Instanziieren Sie eine neue Arbeitsmappe.
Workbook excelbook = new Workbook();
```
## Schritt 3: Fügen Sie die erste ovale Form hinzu
Jetzt kommt der spannende Teil: Wir fügen dem Arbeitsblatt eine ovale Form hinzu. Diese ovale Form könnte ein visuelles Element wie eine Schaltfläche oder eine Markierung darstellen. Wir beginnen mit dem Hinzufügen der ersten ovalen Form zum ersten Arbeitsblatt unserer Arbeitsmappe.

Hier verwenden wir die `Shapes.AddOval()` Methode zum Erstellen eines Ovals auf dem Arbeitsblatt in einer bestimmten Zeile und Spalte.
```csharp
// Fügen Sie eine ovale Form hinzu.
Aspose.Cells.Drawing.Oval oval1 = excelbook.Worksheets[0].Shapes.AddOval(2, 0, 2, 0, 130, 160);
```
Die Parameter im Inneren `AddOval()` sind wie folgt:
- Die ersten beiden Zahlen stellen die Zeile und Spalte für die obere linke Ecke des Ovals dar.
- Die nächsten beiden Zahlen stellen die Höhe und Breite des Ovals dar.
## Schritt 4: Legen Sie die Platzierung und den Stil des Ovals fest
Sobald das Oval erstellt ist, können wir seine Position, Linienstärke und Strichart festlegen. Die `Placement` Die Eigenschaft „Oval“ bestimmt, wie sich das Oval verhält, wenn Sie die Größe von Zellen im Arbeitsblatt ändern oder diese verschieben.

Wir lassen das Oval freischweben und passen sein Aussehen an.
```csharp
// Legen Sie die Platzierung des Ovals fest.
oval1.Placement = PlacementType.FreeFloating;
// Stellen Sie die Linienstärke ein.
oval1.Line.Weight = 1;
// Legen Sie den Strichstil des Ovals fest.
oval1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Dadurch kann sich das Oval frei im Arbeitsblatt bewegen und seine Linienstärke und sein Stil werden für visuelle Konsistenz festgelegt.
## Schritt 5: Fügen Sie eine weitere ovale (kreisförmige) Form hinzu
Warum bei einer aufhören? In diesem Schritt fügen wir eine weitere ovale Form hinzu und erstellen dieses Mal einen perfekten Kreis, indem wir Höhe und Breite angleichen.

Wir erstellen ein weiteres Oval, platzieren es an einer anderen Stelle und sorgen durch die Einstellung gleicher Höhe und Breite für eine runde Form.
```csharp
// Fügen Sie eine weitere ovale (kreisförmige) Form hinzu.
Aspose.Cells.Drawing.Oval oval2 = excelbook.Worksheets[0].Shapes.AddOval(9, 0, 2, 15, 130, 130);
```
## Schritt 6: Stylen Sie das zweite Oval
Genau wie zuvor passen wir die Platzierung, Stärke und Strichart dieses zweiten Ovals (oder Kreises) an.

Wir wenden ähnliche Eigenschaften auf das zweite Oval an, um es an den Stil des ersten anzupassen.
```csharp
// Legen Sie die Platzierung des Ovals fest.
oval2.Placement = PlacementType.FreeFloating;
// Stellen Sie die Linienstärke ein.
oval2.Line.Weight = 1;
// Legen Sie den Strichstil des Ovals fest.
oval2.Line.DashStyle = MsoLineDashStyle.Solid;
```
## Schritt 7: Speichern der Arbeitsmappe
Abschließend müssen wir die Arbeitsmappe mit den hinzugefügten Ovalen speichern. Durch das Speichern der Datei werden alle Änderungen gespeichert.

Wir speichern die Arbeitsmappe in dem Verzeichnispfad, den wir zuvor definiert haben.
```csharp
// Speichern Sie die Excel-Datei.
excelbook.Save(dataDir + "book1.out.xls");
```
Und das war’s! Sie haben Ihrem Excel-Arbeitsblatt erfolgreich Ovale hinzugefügt und die Datei gespeichert.
## Abschluss
Das Hinzufügen von Formen wie Ovalen zu einer Excel-Tabelle mit Aspose.Cells für .NET ist nicht nur unkompliziert, sondern auch eine unterhaltsame Möglichkeit, Ihre Tabellen mit zusätzlichen visuellen Elementen zu erweitern. Ob für Designzwecke oder zum Hinzufügen anklickbarer Elemente – Formen können das Aussehen und die Funktion Ihrer Excel-Dateien maßgeblich beeinflussen. Wenn Sie also das nächste Mal an einem Projekt arbeiten, das interaktive oder optisch ansprechende Excel-Tabellen erfordert, wissen Sie genau, wie Sie diese perfekten Ovale hinzufügen!
## Häufig gestellte Fragen
### Kann ich mit Aspose.Cells für .NET andere Formen wie Rechtecke oder Linien hinzufügen?
Ja, Sie können verschiedene Formen wie Rechtecke, Linien und Pfeile hinzufügen, indem Sie `Shapes` Sammlung in Aspose.Cells.
### Ist es möglich, die Größe der Ovale nach dem Hinzufügen zu ändern?
Absolut! Sie können die Höhen- und Breiteneigenschaften der Ovale nach dem Hinzufügen ändern.
### In welchen Dateiformaten außer XLS kann ich die Arbeitsmappe speichern?
Aspose.Cells unterstützt mehrere Formate wie unter anderem XLSX, CSV und PDF.
### Kann ich die Farbe der Ovalkontur ändern?
Ja, Sie können die Linienfarbe des Ovals ändern, indem Sie `Line.Color` Eigentum.
### Ist für Aspose.Cells eine Lizenz erforderlich?
Während Sie Aspose.Cells mit einer kostenlosen Testversion ausprobieren können, benötigen Sie eine [Lizenz](https://purchase.aspose.com/buy) für die langfristige Verwendung oder für den Zugriff auf erweiterte Funktionen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}