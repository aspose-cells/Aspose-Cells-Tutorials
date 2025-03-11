---
title: TextBox-Steuerelemente in Excel bearbeiten
linktitle: TextBox-Steuerelemente in Excel bearbeiten
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in diesem leicht verständlichen Schritt-für-Schritt-Tutorial, wie Sie Textfelder in Excel mit Aspose.Cells für .NET bearbeiten.
weight: 15
url: /de/net/excel-shapes-controls/manipulate-textbox-controls-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TextBox-Steuerelemente in Excel bearbeiten

## Einführung
Wenn Sie schon einmal mit Excel gearbeitet haben, sind Sie wahrscheinlich schon auf diese kleinen Textfelder gestoßen, mit denen Sie schwebenden Text in eine Tabelle einfügen können. Aber was, wenn Sie diese Textfelder programmgesteuert bearbeiten müssen? Hier kommt Aspose.Cells für .NET ins Spiel. Damit können Sie ganz einfach auf Textfelder zugreifen und diese bearbeiten, was es perfekt für die Automatisierung von Aufgaben oder die Anpassung von Berichten macht. In diesem Tutorial führen wir Sie durch den Prozess der Bearbeitung von Textfeldern in Excel mit Aspose.Cells für .NET.
## Voraussetzungen
Bevor wir uns in den eigentlichen Code stürzen, stellen wir sicher, dass Sie alles richtig eingerichtet haben:
1.  Aspose.Cells für .NET: Sie müssen die Bibliothek Aspose.Cells für .NET herunterladen. Den Download-Link finden Sie[Hier](https://releases.aspose.com/cells/net/).
2. .NET-Entwicklungsumgebung: Jede IDE, die .NET unterstützt, wie z. B. Visual Studio, funktioniert.
3. Grundkenntnisse in C#: Dieses Tutorial setzt voraus, dass Sie mit der grundlegenden C#-Syntax und der Struktur von Excel-Arbeitsmappen vertraut sind.
4.  Excel-Datei: Eine vorhandene Excel-Datei mit Textfeldern (wir verwenden`book1.xls`in diesem Beispiel).
5.  Aspose-Lizenz: Wenn Sie die kostenlose Testversion nicht verwenden, müssen Sie[kaufen](https://purchase.aspose.com/buy) eine Lizenz oder einen[vorübergehend](https://purchase.aspose.com/temporary-license/).
Lassen Sie uns nun in die einzelnen Schritte eintauchen!
## Pakete importieren
Bevor Sie Excel-Arbeitsmappen und Textfelder mit Aspose.Cells bearbeiten können, müssen Sie die erforderlichen Namespaces importieren. Hier ist der Codeausschnitt, den Sie oben in Ihrer C#-Datei verwenden:
```csharp
using System.IO;
using Aspose.Cells;
```
Diese Pakete ermöglichen Ihnen den Zugriff auf die Bearbeitung von Arbeitsmappen und Arbeitsblättern sowie das Zeichnen von Objekten (wie etwa Textfeldern).
Nachdem wir nun alles eingerichtet haben, unterteilen wir den Vorgang der Bearbeitung von Textfeldern in leicht verständliche Schritte.
## Schritt 1: Richten Sie Ihr Arbeitsmappenverzeichnis ein
 Der erste Schritt besteht darin, anzugeben, wo sich Ihre Excel-Dateien auf Ihrem System befinden. Sie müssen den Platzhalter`Your Document Directory` durch den tatsächlichen Pfad zu Ihrer Datei. Dieser Pfad wird gespeichert im`dataDir` Variable zur einfachen Referenzierung im gesamten Code.
```csharp
string dataDir = "Your Document Directory";
```
Dadurch weiß Ihr Programm, wo die Excel-Eingabedatei zu finden ist (`book1.xls`) und wo die Ausgabedatei gespeichert werden soll.
## Schritt 2: Öffnen Sie die Excel-Datei
Als Nächstes müssen Sie die vorhandene Excel-Datei in das Aspose.Cells-Arbeitsmappenobjekt laden. Diese Arbeitsmappe fungiert als Container für Ihre Excel-Daten und ermöglicht Ihnen den Zugriff auf die Arbeitsblätter und alle Zeichenobjekte (z. B. Textfelder).
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
 Der`Workbook` Die Klasse von Aspose.Cells lädt die angegebene Excel-Datei aus Ihrem Verzeichnis. Wenn die Datei im angegebenen Verzeichnis nicht vorhanden ist, wird eine Ausnahme ausgelöst. Stellen Sie daher sicher, dass der Pfad korrekt ist.
## Schritt 3: Zugriff auf das erste Arbeitsblatt
Nachdem Sie die Arbeitsmappe geladen haben, können Sie auf ihre Arbeitsblätter zugreifen. In diesem Beispiel greifen wir auf das erste Arbeitsblatt in der Arbeitsmappe zu, das am Index 0 gespeichert ist.
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
 Der`Worksheets` -Eigenschaft gibt Ihnen Zugriff auf alle Blätter in der Arbeitsmappe. Hier interessiert uns nur das erste Blatt, aber Sie können mit jedem Blatt arbeiten, indem Sie den richtigen Index angeben.
## Schritt 4: Holen Sie sich das erste TextBox-Objekt
Textfelder in einem Excel-Blatt werden als Zeichenobjekte betrachtet. Die Klasse Aspose.Cells.Drawing.TextBox bietet Eigenschaften und Methoden, um sie zu bearbeiten. Um auf das erste Textfeld im Arbeitsblatt zuzugreifen, verweisen Sie einfach auf die`TextBoxes` Sammlung nach Index.
```csharp
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[0];
```
 Dies ruft das erste Textfeldobjekt aus dem`TextBoxes` Sammlung. Wenn Ihr Arbeitsblatt an diesem Index kein Textfeld hat, wird eine Ausnahme ausgelöst. Stellen Sie daher immer sicher, dass der Index gültig ist.
## Schritt 5: Text aus dem ersten Textfeld abrufen
 Nachdem Sie auf das Textfeld zugegriffen haben, können Sie den darin enthaltenen Text mit dem`.Text` Eigentum.
```csharp
string text0 = textbox0.Text;
```
 Dadurch wird der Text aus dem ersten Textfeld in das`text0` Zeichenfolge. Sie können es jetzt anzeigen, bearbeiten oder in Ihrer Anwendung verarbeiten.
## Schritt 6: Zugriff auf das zweite TextBox-Objekt
Um mehrere Textfelder zu bearbeiten, können wir weitere aus dem Arbeitsblatt abrufen. Hier greifen wir auf das zweite Textfeld auf ähnliche Weise zu wie auf das erste:
```csharp
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[1];
```
Wieder greifen wir auf das zweite Textfeld zu, indem wir den Index 1 aus dem`TextBoxes`Sammlung.
## Schritt 7: Text aus dem zweiten Textfeld abrufen
Genau wie beim ersten Textfeld können Sie den Text aus dem zweiten Textfeld abrufen und in einer Zeichenfolge speichern:
```csharp
string text1 = textbox1.Text;
```
Dadurch wird der aktuelle Text aus dem zweiten Textfeld erfasst.
## Schritt 8: Ändern Sie den Text im zweiten Textfeld
 Nehmen wir nun an, Sie möchten den Text im zweiten Textfeld ändern. Dies können Sie ganz einfach tun, indem Sie dem`.Text` Eigenschaft des Textfeldobjekts.
```csharp
textbox1.Text = "This is an alternative text";
```
Dadurch wird der Text im zweiten Textfeld auf den neuen Inhalt geändert. Sie können hier je nach Bedarf beliebigen Text einfügen.
## Schritt 9: Speichern Sie die aktualisierte Excel-Datei
 Nachdem Sie die Textfelder geändert haben, ist es an der Zeit, Ihre Änderungen zu speichern. Mit Aspose.Cells können Sie die geänderte Arbeitsmappe mit dem`.Save()` Methode. Sie können einen neuen Dateinamen angeben oder die vorhandene Datei überschreiben.
```csharp
workbook.Save(dataDir + "output.out.xls");
```
Dadurch wird die geänderte Excel-Datei in Ihrem angegebenen Ausgabepfad gespeichert. Wenn Sie die Excel-Datei jetzt öffnen, sehen Sie die Änderungen, die Sie an den Textfeldern vorgenommen haben.
## Abschluss
Und da haben Sie es! Sie haben gerade gelernt, wie Sie Textfelder in Excel mit Aspose.Cells für .NET bearbeiten. Ob Sie die Berichterstellung automatisieren, Excel-Tabellen anpassen oder dynamische Inhalte erstellen, mit Aspose.Cells können Sie jeden Aspekt Ihrer Excel-Dateien ganz einfach programmgesteuert steuern. Vom Extrahieren und Ändern von Text bis zum Speichern der aktualisierten Dateien ist diese Bibliothek ein leistungsstarkes Tool für Entwickler, die mit Excel in .NET-Umgebungen arbeiten.
## Häufig gestellte Fragen
### Kann ich mit Aspose.Cells außer Textfeldern auch andere Zeichenobjekte bearbeiten?
Ja, mit Aspose.Cells können Sie andere Zeichenobjekte wie Formen, Diagramme und Bilder bearbeiten.
### Was passiert, wenn ich versuche, auf ein Textfeld zuzugreifen, das nicht existiert?
 Wenn der Index des Textfelds außerhalb des gültigen Bereichs liegt, wird ein`IndexOutOfRangeException` wird geworfen.
### Kann ich mit Aspose.Cells einem Excel-Arbeitsblatt neue Textfelder hinzufügen?
 Ja, Aspose.Cells ermöglicht das Hinzufügen neuer Textfelder mit dem`AddTextBox` Verfahren.
### Benötige ich eine Lizenz, um Aspose.Cells zu verwenden?
 Ja, Sie müssen eine Lizenz erwerben, aber Aspose bietet auch eine[Kostenlose Testversion](https://releases.aspose.com/).
### Kann ich Aspose.Cells mit anderen Programmiersprachen außer C# verwenden?
Ja, Aspose.Cells kann mit jeder .NET-unterstützten Sprache verwendet werden, beispielsweise VB.NET.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
