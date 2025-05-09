---
"description": "Erfahren Sie, wie Sie mit Aspose.Cells für .NET Text mit Formen in Excel drehen. Folgen Sie dieser Schritt-für-Schritt-Anleitung für eine perfekte Excel-Präsentation."
"linktitle": "Drehen Sie Text mit Form in Excel"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Drehen Sie Text mit Form in Excel"
"url": "/de/net/excel-shape-text-modifications/rotate-text-shape-excel/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Drehen Sie Text mit Form in Excel

## Einführung
In der Excel-Welt ist die visuelle Darstellung genauso wichtig wie die Daten selbst. Ob beim Erstellen eines Berichts oder beim Entwerfen eines dynamischen Dashboards – die Anordnung der Informationen kann deren Lesbarkeit und Gesamterscheinungsbild erheblich beeinflussen. Wollten Sie schon immer Text drehen, um ihn stilvoll an Formen auszurichten? Dann haben Sie Glück! In diesem Tutorial erfahren Sie, wie Sie mit Aspose.Cells für .NET Text mit Formen drehen, damit Ihre Tabellen nicht nur informativ, sondern auch beeindruckend sind.
## Voraussetzungen
Bevor wir beginnen, stellen wir sicher, dass Sie alles haben, was Sie brauchen:
1. Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem Computer installiert ist, da wir unseren Code dort schreiben werden.
2. Aspose.Cells für .NET: Sie benötigen die Aspose.Cells-Bibliothek. Sie können [Laden Sie hier die neueste Version herunter](https://releases.aspose.com/cells/net/) oder testen Sie es kostenlos mit einem [kostenlose Testversion](https://releases.aspose.com/).
3. Grundkenntnisse in C#: Kenntnisse in C# und der .NET-Umgebung sind hilfreich, wir begleiten Sie jedoch bei jedem Schritt.
4. Excel-Datei: Eine Beispiel-Excel-Datei, nennen wir sie `sampleRotateTextWithShapeInsideWorksheet.xlsx`, wird zum Testen unseres Codes benötigt. Sie sollten diese Datei in einem Verzeichnis ablegen, auf das Sie leicht zugreifen können.
Alles bereit? Super! Dann lasst uns zum spaßigen Teil übergehen.
## Pakete importieren
Um loszulegen, müssen wir die erforderlichen Pakete in unser Projekt importieren. So geht's:
### Neues Projekt erstellen
1. Öffnen Sie Visual Studio.
2. Wählen Sie „Neues Projekt erstellen“.
3. Wählen Sie „Konsolen-App“ und wählen Sie C# als Ihre bevorzugte Programmiersprache.
### Installieren Sie Aspose.Cells
Fügen wir nun Aspose.Cells zu Ihrem Projekt hinzu. Sie können dies mit dem NuGet-Paket-Manager tun:
1. Öffnen Sie „Extras“ im oberen Menü.
2. Wählen Sie „NuGet-Paket-Manager“ und dann „NuGet-Pakete für Lösung verwalten“.
3. Suchen Sie nach „Aspose.Cells“.
4. Klicken Sie auf „Installieren“, um es Ihrem Projekt hinzuzufügen.
### Using-Direktive hinzufügen
Oben in Ihrer C#-Hauptdatei müssen Sie die folgende Anweisung hinzufügen:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
Jetzt können wir mit dem Programmieren beginnen!
Lassen Sie uns den Vorgang in leicht verständliche Schritte unterteilen. So drehen Sie Text mit Formen in einer Excel-Datei:
## Schritt 1: Richten Sie Ihre Verzeichnispfade ein
Zunächst müssen Sie die Quell- und Ausgabeverzeichnisse für Ihre Excel-Dateien einrichten. So geht's:
```csharp
//Quellverzeichnis
string sourceDir = "Your Document Directory"; // Legen Sie Ihr Dokumentverzeichnis fest
//Ausgabeverzeichnis
string outputDir = "Your Document Directory"; // Legen Sie Ihr Ausgabeverzeichnis fest
```
Ersetzen `"Your Document Directory"` mit dem tatsächlichen Pfad, wo Ihr `sampleRotateTextWithShapeInsideWorksheet.xlsx` Datei befindet.
## Schritt 2: Laden Sie die Excel-Beispieldatei
Laden wir nun die Excel-Beispieldatei. Dies ist wichtig, da wir die vorhandenen Daten bearbeiten möchten.
```csharp
//Beispiel-Excel-Datei laden.
Workbook wb = new Workbook(sourceDir + "sampleRotateTextWithShapeInsideWorksheet.xlsx");
```
## Schritt 3: Zugriff auf das Arbeitsblatt
Sobald die Datei geladen ist, müssen wir auf das Arbeitsblatt zugreifen, das wir ändern möchten. In unserem Fall ist es das erste Arbeitsblatt.
```csharp
//Greifen Sie auf das erste Arbeitsblatt zu.
Worksheet ws = wb.Worksheets[0];
```
## Schritt 4: Ändern einer Zelle
Als Nächstes ändern wir eine bestimmte Zelle, um eine Nachricht anzuzeigen. In unserem Beispiel verwenden wir Zelle B4.
```csharp
//Greifen Sie auf Zelle B4 zu und fügen Sie dort eine Nachricht hinzu.
Cell b4 = ws.Cells["B4"];
b4.PutValue("Text is not rotating with shape because RotateTextWithShape is false.");
```
Bei diesem Schritt dreht sich alles um Kommunikation – wir müssen sicherstellen, dass jeder, der dieses Blatt öffnet, versteht, was wir optimieren.
## Schritt 5: Zugriff auf die erste Form
Um Text zu drehen, benötigen wir eine Form. Hier greifen wir auf die erste Form im Arbeitsblatt zu.
```csharp
//Greifen Sie auf die erste Form zu.
Shape sh = ws.Shapes[0];
```
## Schritt 6: Formtextausrichtung anpassen
Und hier geschieht die Magie. Wir passen die Textausrichtungseigenschaften der Form an.
```csharp
//Greifen Sie auf die Textausrichtung der Form zu.
Aspose.Cells.Drawing.Texts.ShapeTextAlignment shapeTextAlignment = sh.TextBody.TextAlignment;
//Drehen Sie Text nicht mit der Form, indem Sie RotateTextWithShape auf „false“ setzen.
shapeTextAlignment.RotateTextWithShape = false;
```
Durch die Einstellung `RotateTextWithShape` auf „false“ stellen wir sicher, dass der Text aufrecht bleibt und sich nicht mit der Form dreht, sodass alles ordentlich und übersichtlich bleibt.
## Schritt 7: Speichern Sie die Excel-Ausgabedatei
Abschließend speichern wir unsere Änderungen in einer neuen Excel-Datei. So stellen wir sicher, dass unsere Änderungen nicht verloren gehen und wir eine übersichtliche Ausgabe erhalten.
```csharp
//Speichern Sie die Excel-Ausgabedatei.
wb.Save(outputDir + "outputRotateTextWithShapeInsideWorksheet.xlsx");
```
Und das war’s! Ihre Ausgabedatei ist nun gespeichert, einschließlich des Textes in Zelle B4 und der an der Form vorgenommenen Anpassungen.
## Schritt 8: Führen Sie den Code aus
In Ihrem `Main` Methode, umschließen Sie alle oben genannten Codefragmente und führen Sie Ihr Projekt aus. Die Änderungen werden in Ihrer Ausgabedatei angezeigt!
```csharp
Console.WriteLine("RotateTextWithShapeInsideWorksheet executed successfully.");
```
## Abschluss
Das Drehen von Text mit Formen in Excel mit Aspose.Cells für .NET mag zunächst aufwendig erscheinen, ist aber im Detail ganz einfach. Mit diesen einfachen Schritten können Sie Ihre Tabellen professioneller und optisch ansprechender gestalten. Egal, ob Sie dies für einen Kunden oder für Ihre persönlichen Projekte tun, alle werden von der Qualität Ihrer Arbeit begeistert sein!
## Häufig gestellte Fragen
### Kann ich Aspose.Cells kostenlos nutzen?
Ja! Sie können die [kostenlose Testversion](https://releases.aspose.com/) um die Bibliothek auszuprobieren.
### Welche Excel-Versionen unterstützt Aspose.Cells?
Aspose.Cells unterstützt eine Vielzahl von Excel-Formaten, darunter XLS, XLSX, CSV und mehr.
### Ist es in älteren Excel-Versionen möglich, Text mit Formen zu drehen?
Ja, die Funktionalität kann auf ältere, von Aspose.Cells unterstützte Formate angewendet werden.
### Wo finde ich weitere Dokumentation zu Aspose.Cells?
Entdecken Sie die umfassende [Dokumentation](https://reference.aspose.com/cells/net/) für weitere Einblicke.
### Wie erhalte ich Support für Aspose.Cells?
Sie können Unterstützung anfordern, indem Sie die [Aspose-Forum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}