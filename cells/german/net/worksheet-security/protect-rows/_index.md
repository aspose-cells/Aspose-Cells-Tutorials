---
"description": "Erfahren Sie, wie Sie Zeilen in einem Excel-Arbeitsblatt mit Aspose.Cells für .NET schützen. Sichern Sie Ihre Daten mit Zeilenschutz und verhindern Sie versehentliche Änderungen."
"linktitle": "Schützen Sie Zeilen im Arbeitsblatt mit Aspose.Cells"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Schützen Sie Zeilen im Arbeitsblatt mit Aspose.Cells"
"url": "/de/net/worksheet-security/protect-rows/"
"weight": 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Schützen Sie Zeilen im Arbeitsblatt mit Aspose.Cells

## Einführung
Die programmgesteuerte Arbeit mit Excel-Dateien erfordert oft nicht nur Datenmanipulation, sondern auch Datenschutz. Ob Sie vertrauliche Daten schützen oder versehentliche Änderungen verhindern möchten – der Schutz von Zeilen in einem Arbeitsblatt kann entscheidend sein. In diesem Tutorial erfahren Sie, wie Sie bestimmte Zeilen in einem Excel-Arbeitsblatt mit Aspose.Cells für .NET schützen. Wir führen Sie durch alle notwendigen Schritte, von der Vorbereitung Ihrer Umgebung bis zur Implementierung der Schutzfunktionen – einfach und verständlich.
## Voraussetzungen
Bevor Sie mit dem Schützen von Zeilen in einem Arbeitsblatt beginnen können, müssen einige Dinge eingerichtet sein:
1. Aspose.Cells für .NET: Stellen Sie sicher, dass Aspose.Cells für .NET auf Ihrem Entwicklungscomputer installiert ist. Falls noch nicht geschehen, können Sie es einfach von der [Aspose Cells-Downloadseite](https://releases.aspose.com/cells/net/).
2. Visual Studio oder eine beliebige .NET-IDE: Zur Implementierung der Lösung benötigen Sie eine Entwicklungsumgebung. Visual Studio ist eine gute Option, aber jede .NET-kompatible IDE funktioniert.
3. Grundlegende C#-Kenntnisse: Wenn Sie die Grundlagen der C#-Programmierung verstehen, können Sie dem Lernprogramm besser folgen und den Beispielcode Ihren Anforderungen entsprechend anpassen.
4. Aspose.Cells API-Dokumentation: Machen Sie sich vertraut mit der [Aspose.Cells für .NET-Dokumentation](https://reference.aspose.com/cells/net/) um einen Überblick über die Klassenstruktur und die in der Bibliothek verwendeten Methoden zu erhalten.
Wenn Sie alle Voraussetzungen erfüllt haben, können wir direkt mit der Implementierung beginnen.
## Pakete importieren
Zunächst müssen Sie die erforderlichen Pakete importieren. Diese Bibliotheken sind für die Interaktion mit Excel-Dateien in Ihrem C#-Projekt unerlässlich.
```csharp
using System.IO;
using Aspose.Cells;
```
Sobald Sie die erforderlichen Pakete importiert haben, können Sie mit der Codierung beginnen. 
Lassen Sie uns den Prozess nun in kleinere Schritte unterteilen, damit Sie ihn ganz einfach nachvollziehen können. Jeder Schritt konzentriert sich auf einen bestimmten Teil der Implementierung, damit Sie ihn schnell verstehen und anwenden können. 
## Schritt 1: Erstellen Sie eine neue Arbeitsmappe und ein neues Arbeitsblatt
Bevor Sie Schutzeinstellungen anwenden können, müssen Sie eine neue Arbeitsmappe erstellen und das gewünschte Arbeitsblatt auswählen. Dies wird Ihr Arbeitsdokument.
```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "Your Document Directory";
// Erstellen Sie ein Verzeichnis, falls es noch nicht vorhanden ist.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Erstellen Sie eine neue Arbeitsmappe.
Workbook wb = new Workbook();
// Erstellen Sie ein Arbeitsblattobjekt und rufen Sie das erste Blatt ab.
Worksheet sheet = wb.Worksheets[0];
```
In diesem Beispiel erstellen wir eine neue Arbeitsmappe mit einem einzelnen Arbeitsblatt (dies ist die Standardeinstellung beim Erstellen einer neuen Arbeitsmappe mit Aspose.Cells). Anschließend greifen wir auf das erste Arbeitsblatt der Arbeitsmappe zu, das als Ziel für unseren Zeilenschutz dient.
## Schritt 2: Definieren von Style- und StyleFlag-Objekten
Im nächsten Schritt definieren Sie die Stil- und Stilflaggenobjekte. Mit diesen Objekten können Sie die Eigenschaften der Zelle ändern, z. B. ob sie gesperrt oder entsperrt ist.
```csharp
// Definieren Sie das Stilobjekt.
Style style;
// Definieren Sie das Styleflag-Objekt.
StyleFlag flag;
```
Sie werden diese Objekte in späteren Schritten verwenden, um die Zelleneigenschaften anzupassen und auf Ihr Arbeitsblatt anzuwenden.
## Schritt 3: Alle Spalten im Arbeitsblatt entsperren
Standardmäßig sind alle Zellen in einem Excel-Arbeitsblatt gesperrt. Wenn Sie ein Arbeitsblatt schützen, bleibt der Sperrstatus jedoch bestehen. Um sicherzustellen, dass nur bestimmte Zeilen oder Zellen geschützt sind, können Sie zunächst alle Spalten entsperren. Dieser Schritt ist unerlässlich, wenn Sie nur bestimmte Zeilen schützen möchten.
```csharp
// Durchlaufen Sie alle Spalten im Arbeitsblatt und entsperren Sie sie.
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    flag = new StyleFlag();
    flag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag);
}
```
In diesem Code durchlaufen wir alle 256 Spalten im Arbeitsblatt (Excel-Arbeitsblätter haben maximal 256 Spalten, indiziert von 0 bis 255) und setzen ihre `IsLocked` Eigentum zu `false`Diese Aktion stellt sicher, dass alle Spalten entsperrt werden. Wir werden später jedoch trotzdem bestimmte Zeilen sperren.
## Schritt 4: Sperren Sie die erste Reihe
Nachdem Sie die Spalten entsperrt haben, sperren Sie im nächsten Schritt die Zeilen, die Sie schützen möchten. In diesem Beispiel sperren wir die erste Zeile. Dadurch wird sichergestellt, dass Benutzer sie nicht ändern können, während andere Zeilen entsperrt bleiben.
```csharp
// Holen Sie sich den Stil der ersten Zeile.
style = sheet.Cells.Rows[0].Style;
// Sperren Sie es.
style.IsLocked = true;
// Instanziieren Sie die Flagge.
flag = new StyleFlag();
// Legen Sie die Sperreinstellung fest.
flag.Locked = true;
// Wenden Sie den Stil auf die erste Zeile an.
sheet.Cells.ApplyRowStyle(0, style, flag);
```
Hier greifen wir auf den Stil der ersten Zeile zu und setzen dessen `IsLocked` Eigentum zu `true`. Danach verwenden wir die `ApplyRowStyle()` Methode, um den Sperrstil auf die gesamte Zeile anzuwenden. Sie können diesen Schritt wiederholen, um weitere Zeilen zu sperren, die Sie schützen möchten.
## Schritt 5: Schützen Sie das Blatt
Nachdem wir die erforderlichen Zeilen entsperrt und gesperrt haben, ist es an der Zeit, das Arbeitsblatt zu schützen. Der Schutz stellt sicher, dass niemand die gesperrten Zeilen oder Zellen ändern kann, es sei denn, er entfernt das Schutzkennwort (falls vorhanden).
```csharp
// Schützen Sie das Blatt.
sheet.Protect(ProtectionType.All);
```
In diesem Schritt schützen wir das gesamte Blatt mit `ProtectionType.All`. Dieser Schutztyp bedeutet, dass alle Aspekte des Blattes, einschließlich gesperrter Zeilen und Zellen, geschützt sind. Sie können diesen Schutz auch anpassen, indem Sie bei Bedarf verschiedene Schutztypen angeben.
## Schritt 6: Speichern der Arbeitsmappe
Abschließend müssen wir die Arbeitsmappe speichern, nachdem wir die erforderlichen Stile und Schutzmaßnahmen angewendet haben. Die Arbeitsmappe kann in verschiedenen Formaten gespeichert werden, z. B. Excel 97-2003, Excel 2010 usw.
```csharp
// Speichern Sie die Excel-Datei.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
Diese Codezeile speichert die Arbeitsmappe im Excel 97-2003-Format mit den vorgenommenen Änderungen. Sie können das Dateiformat nach Ihren Wünschen anpassen, indem Sie aus einer Vielzahl von `SaveFormat` Optionen.
## Abschluss
Und da haben Sie es! Sie haben erfolgreich gelernt, wie Sie Zeilen in einem Arbeitsblatt mit Aspose.Cells für .NET schützen. Mit den obigen Schritten können Sie beliebige Zeilen oder Spalten nach Bedarf entsperren oder sperren und Schutz anwenden, um die Integrität Ihrer Daten zu gewährleisten.
## Häufig gestellte Fragen
### Wie kann ich mehrere Zeilen gleichzeitig schützen?  
Sie können mehrere Zeilen durchlaufen und den Sperrstil auf jede Zeile einzeln anwenden. Ersetzen Sie einfach `0` mit dem Zeilenindex, den Sie sperren möchten.
### Kann ich für den Blattschutz ein Passwort festlegen?  
Ja! Sie können ein Passwort an den `sheet.Protect()` Methode zum Erzwingen des Kennwortschutzes.
### Kann ich Zellen statt ganzer Spalten entsperren?  
Ja! Anstatt Spalten zu entsperren, können Sie einzelne Zellen entsperren, indem Sie deren Stileigenschaften ändern.
### Was passiert, wenn ich versuche, eine geschützte Zeile zu bearbeiten?  
Wenn eine Zeile geschützt ist, verhindert Excel, dass Änderungen an den gesperrten Zellen vorgenommen werden, es sei denn, Sie heben den Schutz des Blatts auf.
### Kann ich bestimmte Bereiche hintereinander schützen?  
Ja! Sie können einzelne Bereiche in einer Reihe sperren, indem Sie die `IsLocked` Eigenschaft für bestimmte Zellen innerhalb des Bereichs.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}