---
"description": "Erfahren Sie in diesem ausführlichen Schritt-für-Schritt-Tutorial, wie Sie mit Aspose.Cells für .NET einen Durchstreicheffekt auf Text in Excel anwenden."
"linktitle": "Erstellen eines Durchstreicheffekts für Text in Excel"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Erstellen eines Durchstreicheffekts für Text in Excel"
"url": "/de/net/working-with-fonts-in-excel/creating-strike-out-effect/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Erstellen eines Durchstreicheffekts für Text in Excel

## Einführung
In Excel sind visuelle Elemente genauso wichtig wie die Daten selbst. Ob Sie wichtige Änderungen hervorheben oder nicht mehr relevante Elemente markieren – der Durchstreicheffekt ist eine klassische Methode zur visuellen Darstellung in Tabellenkalkulationen. In dieser Anleitung führen wir Sie durch die Implementierung eines Durchstreicheffekts in Excel mit Aspose.Cells für .NET. Dieses Tutorial behandelt nicht nur die notwendigen Voraussetzungen, sondern bietet auch eine Schritt-für-Schritt-Anleitung, damit Sie diesen Effekt problemlos reproduzieren können.
## Voraussetzungen
Bevor Sie mit dem Lernprogramm beginnen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:
1. Entwicklungsumgebung: Sie sollten eine .NET-Entwicklungsumgebung eingerichtet haben. Dies kann Visual Studio oder eine andere IDE Ihrer Wahl sein, die die .NET-Entwicklung unterstützt.
2. Aspose.Cells für .NET: Stellen Sie sicher, dass Aspose.Cells in Ihrem Projekt installiert ist. Sie können es unter folgendem Link herunterladen: [Laden Sie Aspose.Cells herunter](https://releases.aspose.com/cells/net/).
3. Grundkenntnisse in C#: Ein grundlegendes Verständnis der C#-Programmierung ist hilfreich, da die Beispiele in C# codiert werden.
4. .NET Framework: Stellen Sie sicher, dass Ihr Projekt auf eine kompatible Version des .NET Frameworks abzielt, normalerweise .NET Core oder .NET Framework 4.5 und höher.
## Pakete importieren
Bevor Sie Code schreiben, müssen Sie die erforderlichen Namespaces aus Aspose.Cells importieren. Dies ist entscheidend für den Zugriff auf verschiedene Funktionen der Bibliothek. So importieren Sie die erforderlichen Namespaces:
```csharp
using System.IO;
using Aspose.Cells;
```
Mit diesen Importen haben Sie Zugriff auf die Arbeitsmappen-, Arbeitsblatt- und Stilklassen, die in diesem Lernprogramm verwendet werden.
Nachdem wir nun die Grundlagen gelegt haben, unterteilen wir den Prozess in überschaubare Schritte. Jeder Schritt wird von klaren Anweisungen begleitet, die Sie durch die Erstellung eines Durchstreicheffekts für Text in Excel führen.
## Schritt 1: Definieren Sie das Dokumentverzeichnis
Definieren Sie zunächst den Pfad, in dem Ihre Excel-Dokumente gespeichert werden. Dies ist der Speicherort für Ihre Ausgabedateien.
```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "Your Document Directory";
```
Ersetzen `"Your Document Directory"` mit dem tatsächlichen Verzeichnispfad, in dem Sie Ihre Excel-Datei speichern möchten. Dadurch wird das Verzeichnis für Ihre Ausgabe eingerichtet.
## Schritt 2: Erstellen Sie das Verzeichnis
Als Nächstes müssen Sie sicherstellen, dass das im vorherigen Schritt angegebene Verzeichnis vorhanden ist. Falls nicht, können Sie es programmgesteuert erstellen.
```csharp
// Erstellen Sie ein Verzeichnis, falls es noch nicht vorhanden ist.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Dieser Code prüft, ob das Verzeichnis existiert und erstellt es, falls nicht. Dies hilft, Fehler beim späteren Speichern der Datei zu vermeiden.
## Schritt 3: Instanziieren eines Arbeitsmappenobjekts
Jetzt erstellen Sie ein neues Arbeitsmappenobjekt. Dies bildet die Grundlage Ihrer Excel-Datei, in der Sie Daten hinzufügen und Formate anwenden.
```csharp
// Instanziieren eines Workbook-Objekts
Workbook workbook = new Workbook();
```
Der `Workbook` Die Klasse stellt eine Excel-Datei dar. Indem Sie eine Instanz dieser Klasse erstellen, erstellen Sie im Wesentlichen ein neues Excel-Dokument.
## Schritt 4: Neues Arbeitsblatt hinzufügen
Jede Arbeitsmappe kann mehrere Arbeitsblätter enthalten. Erstellen wir nun ein neues Arbeitsblatt in Ihrer Arbeitsmappe.
```csharp
// Hinzufügen eines neuen Arbeitsblatts zum Excel-Objekt
int i = workbook.Worksheets.Add();
```
Der `Add` Methode der `Worksheets` Die Sammlung fügt der Arbeitsmappe ein neues Arbeitsblatt hinzu und gibt dessen Index zurück. 
## Schritt 5: Referenz des neuen Arbeitsblatts abrufen
Nachdem Sie das Arbeitsblatt erstellt haben, müssen Sie für zukünftige Vorgänge darauf verweisen.
```csharp
// Abrufen der Referenz des neu hinzugefügten Arbeitsblatts durch Übergeben seines Blattindex
Worksheet worksheet = workbook.Worksheets[i];
```
Hier holen Sie das neu erstellte Arbeitsblatt anhand seines Index (`i`). Dadurch erhalten Sie Zugriff auf die Bearbeitung des Arbeitsblatts.
## Schritt 6: Zugriff auf eine Zelle
Sie möchten auf eine bestimmte Zelle in Ihrem Arbeitsblatt zugreifen, in der Sie das Durchstreichformat anwenden möchten. In diesem Beispiel verwenden wir die Zelle `A1`.
```csharp
// Zugriff auf die Zelle „A1“ aus dem Arbeitsblatt
Aspose.Cells.Cell cell = worksheet.Cells["A1"];
```
In Excel werden Zellen durch ihre Spalten- und Zeilenkennungen (z. B. "A1") referenziert. Wir erhalten einen Verweis auf die Zelle `A1` zur weiteren Manipulation.
## Schritt 7: Wert zur Zelle hinzufügen
Als nächstes fügen wir einen Text in die Zelle ein. Wir schreiben „Hallo Aspose!“ in die Zelle `A1`.
```csharp
// Hinzufügen eines Wertes zur Zelle „A1“
cell.PutValue("Hello Aspose!");
```
Der `PutValue` Mit dieser Methode wird der Zelle ein Zeichenfolgenwert zugewiesen. Sie können diese Zeichenfolge beliebig ändern.
## Schritt 8: Den Stil der Zelle abrufen
Da wir nun Text in unserer Zelle haben, ist es an der Zeit, auf den Stil der Zelle zuzugreifen, um die gewünschte Formatierung anzuwenden, einschließlich des Durchstreicheffekts.
```csharp
// Den Stil der Zelle erhalten
Style style = cell.GetStyle();
```
Der `GetStyle` Die Methode ruft den aktuellen Stil der Zelle ab und ermöglicht Ihnen, Eigenschaften wie Schriftart, -größe und Effekte zu ändern.
## Schritt 9: Legen Sie den Durchstreicheffekt fest
Wenden wir den Durchstreicheffekt auf den Text in der Zelle an. Wir ändern den Schriftstil der Zelle.
```csharp
// ExStart:SetStrikeout
// Festlegen des Durchstreicheffekts für die Schriftart
style.Font.IsStrikeout = true;
// ExEnd:SetStrikeout
```
Durch die Einstellung `IsStrikeout` auf „true“ setzen, weisen Sie Excel an, den Text in der ausgewählten Zelle optisch durchzustreichen – ähnlich wie wenn Sie etwas optisch von einer Liste streichen.
## Schritt 10: Den Stil auf die Zelle anwenden
Nachdem Sie den Stil geändert haben, müssen Sie ihn wieder auf die Zelle anwenden, um die Änderungen widerzuspiegeln.
```csharp
// Anwenden des Stils auf die Zelle
cell.SetStyle(style);
```
Der `SetStyle` Die Methode aktualisiert die Zelle mit dem neuen Stil, der jetzt die Durchstreichformatierung enthält.
## Schritt 11: Speichern Sie die Excel-Datei
Abschließend speichern wir die Arbeitsmappe im angegebenen Verzeichnis. In diesem Beispiel speichern wir die Datei unter dem Namen `book1.out.xls`.
```csharp
// Speichern der Excel-Datei
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
Der `Save` Die Methode schreibt die Arbeitsmappe im Excel-Format 97-2003 auf die Festplatte. Sie können bei Bedarf andere Formate angeben.
## Abschluss
Das Erstellen eines Durchstreicheffekts für Text in Excel mit Aspose.Cells für .NET ist ein einfacher Prozess, wenn Sie ihn Schritt für Schritt durchgehen. Mit dieser Anleitung können Sie Ihre Tabellenkalkulationen nun mit visuellen Hinweisen aufwerten und Ihre Daten nicht nur informativ, sondern auch optisch ansprechend gestalten.
## Häufig gestellte Fragen
### Was ist Aspose.Cells?
Aspose.Cells ist eine leistungsstarke Bibliothek zum Verwalten von Excel-Dateien in .NET-Anwendungen, mit der Sie Excel-Dokumente programmgesteuert erstellen, bearbeiten und konvertieren können.
### Kann ich Aspose.Cells kostenlos nutzen?
Ja, Sie können es während einer Testphase kostenlos nutzen. Eine kostenlose Testversion ist verfügbar unter [Kostenlose Testversion von Aspose.Cells](https://releases.aspose.com/).
### Wie kaufe ich Aspose.Cells?
Sie können eine Lizenz für Aspose.Cells über deren Website erwerben [Aspose.Cells kaufen](https://purchase.aspose.com/buy).
### Gibt es Beispiele für die Verwendung von Aspose.Cells?
Ja, Sie finden zahlreiche Beispiele und Codeausschnitte im [Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/net/).
### Wo erhalte ich Support für Aspose.Cells?
Sie erhalten Community-Support und Hilfe von der [Aspose Forum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}