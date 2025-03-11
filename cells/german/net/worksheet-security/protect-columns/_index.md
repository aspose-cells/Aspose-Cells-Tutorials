---
title: Schützen Sie Spalten im Arbeitsblatt mit Aspose.Cells
linktitle: Schützen Sie Spalten im Arbeitsblatt mit Aspose.Cells
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie Spalten in Excel mit Aspose.Cells für .NET schützen. Folgen Sie diesem ausführlichen Tutorial, um Spalten in Excel-Tabellen effektiv zu sperren.
weight: 13
url: /de/net/worksheet-security/protect-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Schützen Sie Spalten im Arbeitsblatt mit Aspose.Cells

## Einführung
Wenn Sie programmgesteuert mit Excel-Dateien arbeiten, müssen Sie möglicherweise bestimmte Bereiche des Arbeitsblatts vor Änderungen schützen. Eine der häufigsten Aufgaben besteht darin, Spalten in einem Arbeitsblatt zu schützen und gleichzeitig andere Teile des Blatts bearbeitbar zu lassen. Hier kommt Aspose.Cells für .NET ins Spiel. In diesem Tutorial führen wir Sie Schritt für Schritt durch den Prozess des Schützens bestimmter Spalten in einem Excel-Arbeitsblatt mit Aspose.Cells für .NET.
## Voraussetzungen
Bevor Sie mit dem Schützen von Spalten beginnen, müssen Sie einige Dinge vorbereitet haben:
- Visual Studio: Auf Ihrem Computer sollte Visual Studio oder eine andere .NET-kompatible IDE installiert sein.
-  Aspose.Cells für .NET: Sie müssen die Bibliothek Aspose.Cells für .NET in Ihr Projekt integriert haben. Sie können sie von der[Webseite](https://releases.aspose.com/cells/net/).
- Grundkenntnisse in C#: Dieses Tutorial setzt grundlegende Kenntnisse der C#-Programmierung voraus.
 Wenn Sie neu bei Aspose.Cells sind, lohnt es sich, einen Blick auf die[Dokumentation](https://reference.aspose.com/cells/net/) um mehr über die Funktionen der Bibliothek und die Arbeit mit ihr zu erfahren.
## Pakete importieren
Um zu beginnen, müssen Sie die erforderlichen Namespaces importieren, die Ihnen die Arbeit mit Aspose.Cells ermöglichen. Nachfolgend finden Sie die Importe, die Sie für dieses Beispiel benötigen:
```csharp
using System.IO;
using Aspose.Cells;
```
- Aspose.Cells: Dieser Namespace ist wichtig, da er Zugriff auf alle Klassen bietet, die für die Arbeit mit Excel-Dateien erforderlich sind.
- System: Dieser Namespace ist für grundlegende Systemfunktionen wie die Dateiverwaltung.
Nachdem Sie nun die erforderlichen Pakete importiert haben, stürzen wir uns in den eigentlichen Prozess des Schützens von Spalten in einem Arbeitsblatt.
## Schritt-für-Schritt-Anleitung zum Schützen von Spalten im Arbeitsblatt
Wir unterteilen diesen Prozess in überschaubare Schritte, damit Sie ihn problemlos nachvollziehen können. So schützen Sie Spalten mit Aspose.Cells für .NET.
## Schritt 1: Einrichten des Dokumentverzeichnisses
Zuerst müssen wir sicherstellen, dass das Verzeichnis, in dem die Datei gespeichert wird, existiert. Wenn nicht, erstellen wir es. Dies ist wichtig, um Fehler beim späteren Speichern der Arbeitsmappe zu vermeiden.
```csharp
string dataDir = "Your Document Directory";
// Erstellen Sie ein Verzeichnis, falls es noch nicht vorhanden ist.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- dataDir: Der Verzeichnispfad, in dem Sie Ihre Ausgabedatei speichern.
- Directory.Exists(): Dies prüft, ob das Verzeichnis bereits existiert.
- Directory.CreateDirectory(): Wenn das Verzeichnis nicht existiert, wird es erstellt.
## Schritt 2: Erstellen Sie eine neue Arbeitsmappe
Nachdem das Verzeichnis festgelegt ist, erstellen wir eine neue Arbeitsmappe. Diese Arbeitsmappe dient als Basisdatei, in der wir Änderungen vornehmen.
```csharp
Workbook wb = new Workbook();
```
- Arbeitsmappe: Dies ist das Hauptobjekt, das eine Excel-Datei darstellt. Sie können es sich als Container für alle Blätter und Daten vorstellen.
## Schritt 3: Zugriff auf das erste Arbeitsblatt
Jede Arbeitsmappe hat mehrere Arbeitsblätter und wir müssen Zugriff auf das erste erhalten, auf dem wir den Spaltenschutz anwenden.
```csharp
Worksheet sheet = wb.Worksheets[0];
```
- Arbeitsblätter[0]: Dadurch wird das erste Arbeitsblatt in der Arbeitsmappe abgerufen (Excel-Arbeitsblätter sind nullindiziert).
## Schritt 4: Definieren Sie die Style- und StyleFlag-Objekte
Als Nächstes definieren wir zwei Objekte, Style und StyleFlag, die zum Anpassen des Erscheinungsbilds und der Schutzeinstellungen der Zellen verwendet werden.
```csharp
Style style;
StyleFlag flag;
```
- Stil: Hiermit können wir Eigenschaften wie Schriftart, Farbe und Schutzeinstellungen von Zellen oder Spalten ändern.
- StyleFlag: Hiermit wird angegeben, welche Eigenschaften bei Verwendung der Methode ApplyStyle angewendet werden sollen.
## Schritt 5: Alle Spalten entsperren
Standardmäßig sperrt Excel alle Zellen in einem Arbeitsblatt, wenn der Schutz angewendet wird. Wir möchten jedoch zunächst alle Spalten entsperren, damit wir später bestimmte Spalten, wie beispielsweise die erste Spalte, sperren können.
```csharp
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    flag = new StyleFlag();
    flag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag);
}
```
- Spalten[(byte)i]: Dadurch wird auf eine bestimmte Spalte im Arbeitsblatt über ihren Index zugegriffen (wir durchlaufen hier die Spalten 0 bis 255).
- style.IsLocked = false: Dadurch werden alle Zellen in der Spalte entsperrt.
- ApplyStyle(): Dies wendet den Stil (entsperrt oder gesperrt) basierend auf der Flagge auf die Spalte an.
## Schritt 6: Sperren Sie die erste Spalte
Nachdem nun alle Spalten entsperrt sind, sperren wir die erste Spalte, um sie zu schützen. Dies ist die Spalte, die Benutzer nicht ändern können.
```csharp
style = sheet.Cells.Columns[0].Style;
style.IsLocked = true;
flag = new StyleFlag();
flag.Locked = true;
sheet.Cells.Columns[0].ApplyStyle(style, flag);
```
- Spalten[0]: Hiermit wird auf die erste Spalte (Index 0) zugegriffen.
- style.IsLocked = true: Dadurch wird die erste Spalte gesperrt, sodass Benutzer keine Änderungen daran vornehmen können.
## Schritt 7: Schützen Sie das Arbeitsblatt
Nachdem wir nun den Schutz für die erste Spalte festgelegt haben, müssen wir den Schutz auf das gesamte Arbeitsblatt anwenden. Dadurch wird sichergestellt, dass gesperrte Zellen (wie die erste Spalte) nicht geändert werden können, sofern der Schutz nicht entfernt wird.
```csharp
sheet.Protect(ProtectionType.All);
```
- sheet.Protect(): Dies wendet den Schutz auf das gesamte Blatt an. Wir geben ProtectionType.All an, um Änderungen zu verhindern, aber Sie können es ändern, wenn Sie möchten, dass Benutzer mit bestimmten Elementen interagieren können.
## Schritt 8: Speichern Sie die Arbeitsmappe
Zum Schluss speichern wir die Arbeitsmappe an einem bestimmten Ort. In diesem Beispiel speichern wir sie in dem Verzeichnis, das wir zuvor erstellt haben.
```csharp
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
- Speichern(): Dadurch wird die Arbeitsmappe im Dateisystem gespeichert.
- SaveFormat.Excel97To2003: Wir speichern die Arbeitsmappe im älteren Excel 97-2003-Format. Sie können dies für ein neueres Format in SaveFormat.Xlsx ändern.
## Abschluss
In diesem Tutorial haben wir Sie durch den gesamten Prozess des Schützens von Spalten in einem Arbeitsblatt mit Aspose.Cells für .NET geführt. Indem Sie diese Schritte befolgen, können Sie ganz einfach anpassen, welche Spalten bearbeitet werden können und welche geschützt sind, und so eine bessere Kontrolle über Ihre Excel-Dokumente haben. Aspose.Cells bietet eine leistungsstarke Möglichkeit, Excel-Dateien programmgesteuert zu verarbeiten, und mit ein wenig Übung können Sie diese Aufgaben meistern, um Ihre Arbeitsabläufe zu automatisieren.
## Häufig gestellte Fragen
### Kann ich mehrere Spalten gleichzeitig schützen?  
Ja, Sie können mehrere Spalten schützen, indem Sie auf jede einzelne Spalte eine Sperre anwenden, so wie wir es für die erste Spalte getan haben.
### Kann ich Benutzern das Bearbeiten bestimmter Spalten erlauben und den Rest gleichzeitig schützen?  
 Auf jeden Fall! Sie können bestimmte Spalten entsperren, indem Sie`style.IsLocked = false` für sie, und wenden Sie dann einen Schutz auf das Arbeitsblatt an.
### Wie entferne ich den Schutz von einem Arbeitsblatt?  
 Um den Schutz aufzuheben, rufen Sie einfach an`sheet.Unprotect()`. Sie können ein Kennwort übergeben, wenn beim Schutz eines festgelegt wurde.
### Kann ich zum Schutz des Arbeitsblattes ein Kennwort festlegen?  
Ja, Sie können ein Passwort als Parameter übergeben an`sheet.Protect("yourPassword")` um sicherzustellen, dass nur autorisierte Benutzer den Blattschutz aufheben können.
### Ist es möglich, einzelne Zellen statt ganzer Spalten zu schützen?  
Ja, Sie können einzelne Zellen sperren, indem Sie auf den Stil der jeweiligen Zelle zugreifen und die Sperreigenschaft auf sie anwenden.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
