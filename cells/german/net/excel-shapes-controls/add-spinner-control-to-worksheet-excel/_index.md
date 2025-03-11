---
title: Spinner-Steuerelement zum Arbeitsblatt in Excel hinzufügen
linktitle: Spinner-Steuerelement zum Arbeitsblatt in Excel hinzufügen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in diesem Schritt-für-Schritt-Tutorial, wie Sie mit Aspose.Cells für .NET einem Excel-Arbeitsblatt ein Spinner-Steuerelement hinzufügen.
weight: 23
url: /de/net/excel-shapes-controls/add-spinner-control-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Spinner-Steuerelement zum Arbeitsblatt in Excel hinzufügen

## Einführung
Wenn Sie mit .NET in die Welt der Excel-Automatisierung eintauchen, sind Sie wahrscheinlich auf den Bedarf nach interaktiveren Steuerelementen in Ihren Tabellen gestoßen. Ein solches Steuerelement ist der Spinner, mit dem Benutzer einen Wert einfach erhöhen oder verringern können. In diesem Tutorial erfahren Sie, wie Sie mit Aspose.Cells für .NET einem Excel-Arbeitsblatt ein Spinner-Steuerelement hinzufügen. Wir unterteilen es in leicht verständliche Schritte, damit Sie es nahtlos nachvollziehen können. 
## Voraussetzungen
Bevor wir uns in den Code stürzen, stellen wir sicher, dass Sie alles für ein reibungsloses Erlebnis eingerichtet haben:
1.  Aspose.Cells für .NET: Stellen Sie sicher, dass Sie die Aspose.Cells-Bibliothek haben. Wenn Sie sie noch nicht installiert haben, können Sie die neueste Version von der[Downloadlink](https://releases.aspose.com/cells/net/).
2. Visual Studio: Sie sollten über eine funktionierende Installation von Visual Studio oder einer anderen .NET-IDE Ihrer Wahl verfügen.
3. Grundkenntnisse in C#: Wenn Sie mit der C#-Programmierung vertraut sind, können Sie die Codeausschnitte problemlos verstehen. Wenn Sie gerade erst anfangen, machen Sie sich keine Sorgen! Ich werde Sie durch jeden Teil führen.
## Pakete importieren
Um Aspose.Cells in Ihrem Projekt zu verwenden, müssen Sie die erforderlichen Namespaces importieren. So können Sie Ihre Umgebung einrichten:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Über diese Namespaces können Sie auf die Kernfunktionen von Aspose.Cells zugreifen, einschließlich der Arbeitsmappenbearbeitung und Zeichenfunktionen für Formen wie den Spinner.
Nachdem wir nun die Voraussetzungen erfüllt und die erforderlichen Pakete importiert haben, können wir uns nun der Schritt-für-Schritt-Anleitung widmen. Jeder Schritt ist klar und prägnant gestaltet, sodass Sie ihn problemlos umsetzen können.
## Schritt 1: Richten Sie Ihr Projektverzeichnis ein
Bevor Sie mit dem Codieren beginnen, sollten Sie Ihre Dateien organisieren. Lassen Sie uns ein Verzeichnis für unsere Excel-Dateien erstellen.
```csharp
// Der Pfad zum Dokumentverzeichnis.
string dataDir = "Your Document Directory";
// Erstellen Sie ein Verzeichnis, falls es noch nicht vorhanden ist.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Hier geben wir einen Pfad für unser Dokumentverzeichnis an. Wenn das Verzeichnis nicht existiert, erstellen wir es. Dadurch wird sichergestellt, dass alle von uns generierten Dateien einen bestimmten Speicherort haben.
## Schritt 2: Erstellen Sie eine neue Arbeitsmappe
Jetzt ist es an der Zeit, eine Excel-Arbeitsmappe zu erstellen, in die wir unser Spinner-Steuerelement hinzufügen.
```csharp
// Instanziieren Sie eine neue Arbeitsmappe.
Workbook excelbook = new Workbook();
```
 Der`Workbook` Klasse stellt eine Excel-Datei dar. Indem wir sie instanziieren, erstellen wir eine neue Arbeitsmappe, die für Änderungen bereit ist.
## Schritt 3: Zugriff auf das erste Arbeitsblatt
Wir fügen unseren Spinner zum ersten Arbeitsblatt in der Arbeitsmappe hinzu.
```csharp
// Holen Sie sich das erste Arbeitsblatt.
Worksheet worksheet = excelbook.Worksheets[0];
```
Diese Zeile greift auf das erste Arbeitsblatt (Index 0) unserer Arbeitsmappe zu. Sie können mehrere Arbeitsblätter haben, aber für dieses Beispiel halten wir es einfach.
## Schritt 4: Mit Zellen arbeiten
Als nächstes arbeiten wir mit den Zellen in unserem Arbeitsblatt. Wir werden einige Werte und Stile festlegen.
```csharp
// Holen Sie sich die Arbeitsblattzellen.
Cells cells = worksheet.Cells;
// Geben Sie einen Zeichenfolgenwert in Zelle A1 ein.
cells["A1"].PutValue("Select Value:");
// Legen Sie die Schriftfarbe der Zelle fest.
cells["A1"].GetStyle().Font.Color = Color.Red;
// Stellen Sie den Schrifttext fett ein.
cells["A1"].GetStyle().Font.IsBold = true;
// Geben Sie den Wert in Zelle A2 ein.
cells["A2"].PutValue(0);
```
Hier füllen wir Zelle A1 mit einer Eingabeaufforderung, wenden eine rote Farbe an und machen den Text fett. Wir setzen auch Zelle A2 auf einen Anfangswert von 0, der mit unserem Spinner verknüpft wird.
## Schritt 5: Gestalten Sie die Zelle A2
Als Nächstes wenden wir einige Stile auf die Zelle A2 an, um sie optisch ansprechender zu gestalten.
```csharp
// Stellen Sie die Schattierungsfarbe auf Schwarz mit einfarbigem Hintergrund ein.
cells["A2"].GetStyle().ForegroundColor = Color.Black;
cells["A2"].GetStyle().Pattern = BackgroundType.Solid;
// Legen Sie die Schriftfarbe der Zelle fest.
cells["A2"].GetStyle().Font.Color = Color.White;
// Stellen Sie den Schrifttext fett ein.
cells["A2"].GetStyle().Font.IsBold = true;
```
Wir fügen Zelle A2 einen schwarzen Hintergrund mit einem einfarbigen Muster hinzu und stellen die Schriftfarbe auf Weiß ein. Durch diesen Kontrast fällt sie auf dem Arbeitsblatt auf.
## Schritt 6: Fügen Sie das Spinner-Steuerelement hinzu
Jetzt können wir das Spinner-Steuerelement zu unserem Arbeitsblatt hinzufügen.
```csharp
// Fügen Sie ein Spinner-Steuerelement hinzu.
Aspose.Cells.Drawing.Spinner spinner = excelbook.Worksheets[0].Shapes.AddSpinner(1, 0, 1, 0, 20, 18);
```
Diese Zeile fügt dem Arbeitsblatt ein Spinner-Steuerelement hinzu. Die Parameter geben die Position und Größe des Spinners an (Zeile, Spalte, Breite, Höhe).
## Schritt 7: Konfigurieren Sie die Spinner-Eigenschaften
Passen wir das Verhalten des Spinners unseren Bedürfnissen an.
```csharp
// Legen Sie den Platzierungstyp des Spinners fest.
spinner.Placement = PlacementType.FreeFloating;
// Legen Sie die verknüpfte Zelle für das Steuerelement fest.
spinner.LinkedCell = "A2";
// Stellen Sie den Maximalwert ein.
spinner.Max = 10;
//Legen Sie den Mindestwert fest.
spinner.Min = 0;
// Stellen Sie die Schrittweite der Steuerung ein.
spinner.IncrementalChange = 2;
// Stellen Sie eine 3D-Schattierung ein.
spinner.Shadow = true;
```
Hier legen wir die Eigenschaften des Spinners fest. Wir verknüpfen ihn mit Zelle A2, sodass er den dort angezeigten Wert steuern kann. Die Mindest- und Höchstwerte definieren den Bereich, in dem der Spinner arbeiten kann, während die inkrementelle Änderung festlegt, wie stark sich der Wert mit jedem Klick ändert. Durch das Hinzufügen von 3D-Schattierungen erhält er ein elegantes Aussehen.
## Schritt 8: Speichern Sie die Excel-Datei
Lassen Sie uns abschließend unsere Excel-Arbeitsmappe mit dem integrierten Spinner speichern.
```csharp
// Speichern Sie die Excel-Datei.
excelbook.Save(dataDir + "book1.out.xls");
```
Dieser Befehl speichert die Arbeitsmappe im angegebenen Verzeichnis. Sie können den Dateinamen nach Bedarf ändern.
## Abschluss
Und da haben Sie es! Sie haben erfolgreich ein Spinner-Steuerelement zu einem Excel-Arbeitsblatt hinzugefügt, indem Sie Aspose.Cells für .NET verwenden. Dieses interaktive Element verbessert die Benutzererfahrung, indem es schnelle Anpassungen an Werten ermöglicht. Egal, ob Sie ein dynamisches Berichtstool oder ein Dateneingabeformular erstellen, das Spinner-Steuerelement kann eine wertvolle Ergänzung sein. 
## Häufig gestellte Fragen
### Was ist ein Spinner-Steuerelement in Excel?
Mithilfe eines Spinner-Steuerelements können Benutzer einen numerischen Wert einfach erhöhen oder verringern und so auf intuitive Weise Auswahlen treffen.
### Kann ich das Erscheinungsbild des Spinners anpassen?
Ja, Sie können die Größe, Position und sogar die 3D-Schattierung für ein eleganteres Aussehen ändern.
### Benötige ich eine Lizenz, um Aspose.Cells zu verwenden?
 Aspose.Cells bietet eine kostenlose Testversion an, für den produktiven Einsatz ist jedoch eine kostenpflichtige Lizenz erforderlich. Schauen Sie sich die[Kaufoptionen](https://purchase.aspose.com/buy).
### Wie kann ich Hilfe zu Aspose.Cells erhalten?
 Für Unterstützung besuchen Sie die[Aspose-Forum](https://forum.aspose.com/c/cells/9) wo Sie Fragen stellen und Antworten finden können.
### Ist es möglich, demselben Arbeitsblatt mehrere Spinner hinzuzufügen?
Auf jeden Fall! Sie können so viele Spinner hinzufügen wie nötig, indem Sie für jedes Steuerelement die gleichen Schritte ausführen.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
