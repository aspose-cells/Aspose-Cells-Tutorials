---
title: Hinzufügen eines Textfelds zum Arbeitsblatt in Excel
linktitle: Hinzufügen eines Textfelds zum Arbeitsblatt in Excel
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in diesem Schritt-für-Schritt-Tutorial, wie Sie mit Aspose.Cells für .NET anpassbare Textfelder zu Excel hinzufügen.
weight: 14
url: /de/net/excel-shapes-controls/add-textbox-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hinzufügen eines Textfelds zum Arbeitsblatt in Excel

## Einführung
Möchten Sie Ihre Excel-Tabellen mit einzigartigen visuellen Elementen aufwerten, die Ihr Publikum fesseln? Das Hinzufügen von Textfeldern ist eine großartige Möglichkeit, dies zu erreichen! Mit Aspose.Cells für .NET können Sie Textfelder ganz einfach in Ihre Excel-Arbeitsblätter integrieren und Ihre Dokumente informativer und optisch ansprechender gestalten. Diese Schritt-für-Schritt-Anleitung führt Sie durch den einfachen Prozess des Hinzufügens von Textfeldern mit Aspose.Cells und zeigt, wie Sie sie mit Text, Farben, Hyperlinks und mehr personalisieren können!
## Voraussetzungen
Bevor wir uns in das Codierungswunder stürzen, hier die wesentlichen Voraussetzungen für einen reibungslosen Ablauf:
1. .NET-Entwicklungsumgebung: Sie benötigen ein funktionierendes .NET-Framework sowie eine IDE wie Visual Studio. Stellen Sie sicher, dass es auf die neueste Version aktualisiert ist!
2.  Aspose.Cells für .NET: Stellen Sie sicher, dass Sie die Aspose.Cells-Bibliothek heruntergeladen haben. Sie können die neueste Version herunterladen unter[Hier](https://releases.aspose.com/cells/net/).
3. Grundlegende Programmierkenntnisse: Kenntnisse in C# und einige allgemeine Konzepte zur Handhabung von Excel-Dateien erleichtern dieses Tutorial!
## Pakete importieren
Stellen Sie sicher, dass Sie die erforderlichen Pakete am Anfang Ihrer C#-Datei importieren. So können Sie das tun:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## Installieren Sie Aspose.Cells
Falls Sie dies noch nicht getan haben, können Sie Aspose.Cells über den NuGet-Paket-Manager in Visual Studio hinzufügen:
1. Öffnen Sie Visual Studio.
2.  Gehe zu`Tools` ->`NuGet Package Manager` ->`Manage NuGet Packages for Solution`.
3. Suchen Sie nach „Aspose.Cells“ und installieren Sie es für Ihr Projekt.
Nachdem wir nun die Grundlagen gelegt haben, können wir uns dem spaßigen Teil widmen!
## Schritt 1: Einrichten Ihres Dokumentverzeichnisses
Richten wir zunächst das Verzeichnis ein, in dem alle Ihre Excel-Dokumente gespeichert werden. Es ist wichtig, sicherzustellen, dass dieses Verzeichnis vorhanden ist, bevor wir mit der Erstellung unserer Arbeitsmappe beginnen.
```csharp
// Der Pfad zum Dokumentverzeichnis.
string dataDir = "Your Document Directory"; 
// Erstellen Sie ein Verzeichnis, falls es noch nicht vorhanden ist.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists) 
    System.IO.Directory.CreateDirectory(dataDir);
```
Dieser Codeausschnitt erstellt ein Verzeichnis namens`Your Document Directory` (ersetzen Sie dies bitte durch Ihren tatsächlichen Pfad), falls dieser noch nicht vorhanden ist. Kinderleicht, oder?
## Schritt 2: Instanziieren einer neuen Arbeitsmappe
Als Nächstes müssen wir eine neue Arbeitsmappe erstellen, in die wir unsere Textfelder einfügen. Dies lässt sich ganz einfach mit ein paar Codezeilen erledigen:
```csharp
// Instanziieren Sie eine neue Arbeitsmappe.
Workbook workbook = new Workbook();
```
Diese Codezeile erstellt eine neue Excel-Arbeitsmappe. Einfach und unkompliziert!
## Schritt 3: Zugriff auf das erste Arbeitsblatt
Nachdem wir nun unsere Arbeitsmappe fertig haben, holen wir uns das erste Arbeitsblatt, in das wir unser Textfeld einfügen:
```csharp
// Holen Sie sich das erste Arbeitsblatt im Buch.
Worksheet worksheet = workbook.Worksheets[0];
```
 So haben Sie nun Zugriff auf das erste Arbeitsblatt mit dem Namen`worksheet`. Es ist Zeit, es zum Glänzen zu bringen!
## Schritt 4: Hinzufügen eines Textfelds
Okay, es ist Zeit, unser erstes Textfeld hinzuzufügen! So geht's:
```csharp
// Fügen Sie der Sammlung ein neues Textfeld hinzu.
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
In dieser Zeile geben wir die Zeile und Spalte an, in der das Textfeld platziert wird, und legen seine Breite und Höhe fest (160 bzw. 200). Sie können diese Zahlen gerne an Ihr Layout anpassen!
## Schritt 5: Abrufen des TextBox-Objekts
Nachdem wir das Textfeld hinzugefügt haben, benötigen wir eine Referenz darauf, damit wir seinen Inhalt anpassen können:
```csharp
// Holen Sie sich das Textfeldobjekt.
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[textboxIndex];
```
 Jetzt,`textbox0` ist Ihre Eintrittskarte zum Ändern dieses Textfelds!
## Schritt 6: Füllen der TextBox mit Inhalt
Als Nächstes geben wir etwas Text für das Textfeld ein:
```csharp
// Füllen Sie den Text aus.
textbox0.Text = "ASPOSE______The .NET & JAVA Component Publisher!";
```
So einfach ist das Einfügen von Text in Ihr Textfeld! 
## Schritt 7: TextBox-Erscheinungsbild anpassen
Wie wäre es, wenn wir es ein wenig aufpeppen? Sie können Schriftfarben, Stile und mehr anpassen!
```csharp
// Legen Sie die Schriftfarbe fest.
textbox0.Font.Color = Color.Blue;
// Stellen Sie die Schriftart auf fett ein.
textbox0.Font.IsBold = true;
// Stellen Sie die Schriftgröße ein.
textbox0.Font.Size = 14;
// Schriftattribut auf Kursiv setzen.
textbox0.Font.IsItalic = true;
```
Probieren Sie ruhig verschiedene Farben und Stile aus, um zu sehen, was optisch am besten wirkt!
## Schritt 8: Hinzufügen eines Hyperlinks
Möchten Sie Ihr Textfeld in einen anklickbaren Link verwandeln? Dann tun wir das:
```csharp
// Fügen Sie dem Textfeld einen Hyperlink hinzu.
textbox0.AddHyperlink("http://www.aspose.com/");
```
Jetzt wird jeder, der auf Ihr Textfeld klickt, zur Aspose-Website weitergeleitet. Es ist wie Magie!
## Schritt 9: Festlegen des TextBox-Platzierungstyps
Sie haben verschiedene Möglichkeiten, wie sich das Textfeld im Verhältnis zu Ihrem Arbeitsblatt verhalten soll. Hier ist ein Beispiel, wie Sie es frei schwebend einstellen können:
```csharp
// Legen Sie die Platzierung fest.
textbox0.Placement = PlacementType.FreeFloating;
```
Wenn Sie alternativ die Größe ändern und sich mit den Zellen verschieben möchten, können Sie es folgendermaßen einstellen:
```csharp
// Legen Sie den Platzierungstyp fest, da das Textfeld mit den Zellen verschoben und seine Größe geändert wird.
textbox1.Placement = PlacementType.MoveAndSize;
```
## Schritt 10: Linien- und Füllformate anpassen
So können Sie das Aussehen des Rahmens und der Füllung des Textfelds ändern:
```csharp
// Holen Sie sich das Füllformat des Textfelds.
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;            
// Ruft den Zeilenformattyp des Textfelds ab.
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;           
// Stellen Sie die Linienstärke ein.
lineformat.Weight = 6;
// Stellen Sie den Strichstil auf Squaredot ein.
lineformat.DashStyle = MsoLineDashStyle.SquareDot;
```
Damit können Sie Ihr Textfeld weiter anpassen und Bilder hinzufügen, die zu Ihrem Stil passen.
## Schritt 11: Hinzufügen eines weiteren Textfelds
Niemand hat gesagt, dass wir nur ein Textfeld hinzufügen können! Fügen wir ein weiteres mit einem anderen Text ein:
```csharp
// Fügen Sie ein weiteres Textfeld hinzu.
textboxIndex = worksheet.TextBoxes.Add(15, 4, 85, 120);
// Holen Sie sich das zweite Textfeld.
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[textboxIndex];
// Geben Sie einen Text ein.
textbox1.Text = "This is another simple text box";
```
Jetzt peppen Sie Ihre Excel-Tabelle mit mehreren Textfeldern richtig auf!
## Schritt 12: Speichern Ihrer Arbeitsmappe
Endlich ist es Zeit, unser Meisterwerk zu speichern! Hier ist die letzte Codezeile für heute:
```csharp
// Speichern Sie die Excel-Datei.
workbook.Save(dataDir + "book1.out.xls");
```
Mit nur dieser einen Codezeile haben Sie eine Excel-Datei mit anpassbaren Textfeldern erstellt und geändert!
## Abschluss
Herzlichen Glückwunsch! Sie haben sich mithilfe von Aspose.Cells für .NET erfolgreich durch die Welt der Textfelder in Excel navigiert. Sie haben nicht nur gelernt, wie Sie ein Textfeld hinzufügen, sondern auch, wie Sie es anpassen, um Ihre Tabellen ansprechender zu gestalten. Von der Änderung von Farben und Stilen bis hin zum Hinzufügen von Hyperlinks sind die Möglichkeiten praktisch unbegrenzt! 
Sind Sie bereit, mit der Transformation Ihrer Excel-Dokumente zu beginnen? Lassen Sie Ihrer Kreativität freien Lauf und experimentieren Sie mit verschiedenen Layouts!
## Häufig gestellte Fragen
### Was ist Aspose.Cells für .NET?
Aspose.Cells für .NET ist eine leistungsstarke Bibliothek, mit der Entwickler mühelos Excel-Dateien erstellen, bearbeiten und konvertieren können.
### Kann ich Aspose.Cells vor dem Kauf ausprobieren?
 Ja! Sie können eine kostenlose Testversion herunterladen und verwenden[Hier](https://releases.aspose.com/).
### Wo finde ich die Dokumentation für Aspose.Cells?
 Eine ausführliche Dokumentation finden Sie unter[Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/net/).
### Gibt es Support, wenn ich auf Probleme stoße?
 Auf jeden Fall! Wenn Sie Hilfe benötigen, besuchen Sie die[Aspose Forum](https://forum.aspose.com/c/cells/9) um Hilfe.
### Kann ich Aspose.Cells ohne Lizenz verwenden?
 Sie können zwar eine kostenlose Testversion verwenden, für den Zugriff auf die volle Funktionalität müssen Sie jedoch eine Lizenz erwerben. Sehen Sie sich die Preise an[Hier](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
