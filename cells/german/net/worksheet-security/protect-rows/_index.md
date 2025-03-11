---
title: Schützen Sie Zeilen im Arbeitsblatt mit Aspose.Cells
linktitle: Schützen Sie Zeilen im Arbeitsblatt mit Aspose.Cells
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie Zeilen in einem Excel-Arbeitsblatt mit Aspose.Cells für .NET schützen. Sichern Sie Ihre Daten mit Zeilenschutz und verhindern Sie versehentliche Änderungen.
weight: 18
url: /de/net/worksheet-security/protect-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Schützen Sie Zeilen im Arbeitsblatt mit Aspose.Cells

## Einführung
Das programmgesteuerte Arbeiten mit Excel-Dateien ist oft eine Aufgabe, die nicht nur Datenmanipulation, sondern auch Datenschutz erfordert. Ob Sie vertrauliche Daten schützen oder versehentliche Änderungen verhindern müssen, der Schutz von Zeilen in einem Arbeitsblatt kann ein entscheidender Schritt sein. In diesem Tutorial erfahren Sie, wie Sie mit Aspose.Cells für .NET bestimmte Zeilen in einem Excel-Arbeitsblatt schützen. Wir führen Sie durch alle erforderlichen Schritte, von der Vorbereitung Ihrer Umgebung bis zur Implementierung der Schutzfunktionen auf einfache, leicht verständliche Weise.
## Voraussetzungen
Bevor Sie mit dem Schützen von Zeilen in einem Arbeitsblatt beginnen können, müssen einige Dinge eingerichtet sein:
1.  Aspose.Cells für .NET: Stellen Sie sicher, dass Sie Aspose.Cells für .NET auf Ihrem Entwicklungscomputer installiert haben. Wenn Sie dies noch nicht getan haben, können Sie es einfach von der[Aspose Cells-Downloadseite](https://releases.aspose.com/cells/net/).
2. Visual Studio oder eine beliebige .NET-IDE: Um die Lösung zu implementieren, müssen Sie eine Entwicklungsumgebung eingerichtet haben. Visual Studio ist eine großartige Option, aber jede .NET-kompatible IDE funktioniert.
3. Grundlegende C#-Kenntnisse: Das Verständnis der Grundlagen der C#-Programmierung wird Ihnen dabei helfen, dem Lernprogramm zu folgen und den Beispielcode Ihren Anforderungen entsprechend zu ändern.
4.  Aspose.Cells API-Dokumentation: Machen Sie sich vertraut mit der[Aspose.Cells für .NET-Dokumentation](https://reference.aspose.com/cells/net/) um einen Überblick über die Klassenstruktur und die in der Bibliothek verwendeten Methoden zu erhalten.
Wenn alle Voraussetzungen erfüllt sind, können wir direkt mit der Implementierung beginnen.
## Pakete importieren
Zu Beginn müssen Sie die erforderlichen Pakete importieren. Diese Bibliotheken sind für die Interaktion mit Excel-Dateien in Ihrem C#-Projekt von entscheidender Bedeutung.
```csharp
using System.IO;
using Aspose.Cells;
```
Sobald Sie die erforderlichen Pakete importiert haben, können Sie mit der Codierung beginnen. 
Lassen Sie uns den Prozess nun in kleinere Schritte unterteilen, damit Sie ihn ganz einfach nachvollziehen können. Jeder Schritt konzentriert sich auf einen bestimmten Teil der Implementierung, damit Sie ihn schnell verstehen und anwenden können. 
## Schritt 1: Erstellen Sie eine neue Arbeitsmappe und ein neues Arbeitsblatt
Bevor Sie Schutzeinstellungen anwenden können, müssen Sie eine neue Arbeitsmappe erstellen und das Arbeitsblatt auswählen, mit dem Sie arbeiten möchten. Dies wird Ihr Arbeitsdokument sein.
```csharp
// Der Pfad zum Dokumentverzeichnis.
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
In diesem Beispiel erstellen wir eine neue Arbeitsmappe mit einem einzelnen Arbeitsblatt (das ist die Standardeinstellung, wenn Sie eine neue Arbeitsmappe mit Aspose.Cells erstellen). Wir greifen dann auf das erste Arbeitsblatt in der Arbeitsmappe zu, das das Ziel für unseren Zeilenschutz sein wird.
## Schritt 2: Style- und StyleFlag-Objekte definieren
Der nächste Schritt besteht darin, die Stil- und Stilflaggenobjekte zu definieren. Mit diesen Objekten können Sie die Eigenschaften der Zelle ändern, z. B. ob sie gesperrt oder entsperrt ist.
```csharp
// Definieren Sie das Stilobjekt.
Style style;
// Definieren Sie das Styleflag-Objekt.
StyleFlag flag;
```
Sie verwenden diese Objekte in späteren Schritten, um die Zelleneigenschaften anzupassen und auf Ihr Arbeitsblatt anzuwenden.
## Schritt 3: Alle Spalten im Arbeitsblatt entsperren
Standardmäßig sind alle Zellen in einem Excel-Arbeitsblatt gesperrt. Wenn Sie jedoch ein Arbeitsblatt schützen, wird der Sperrstatus erzwungen. Um sicherzustellen, dass nur bestimmte Zeilen oder Zellen geschützt sind, können Sie zunächst alle Spalten entsperren. Dieser Schritt ist wichtig, wenn Sie nur bestimmte Zeilen schützen möchten.
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
 In diesem Code durchlaufen wir alle 256 Spalten im Arbeitsblatt (Excel-Arbeitsblätter haben maximal 256 Spalten, indiziert von 0 bis 255) und setzen deren`IsLocked` Eigentum an`false`. Diese Aktion stellt sicher, dass alle Spalten entsperrt werden. Wir werden später aber trotzdem noch bestimmte Zeilen sperren.
## Schritt 4: Sperren Sie die erste Reihe
Nachdem Sie die Spalten entsperrt haben, besteht der nächste Schritt darin, bestimmte Zeilen zu sperren, die Sie schützen möchten. In diesem Beispiel sperren wir die erste Zeile. Dadurch wird sichergestellt, dass Benutzer sie nicht ändern können, während andere Zeilen entsperrt bleiben.
```csharp
//Holen Sie sich den Stil der ersten Zeile.
style = sheet.Cells.Rows[0].Style;
// Sperren Sie es.
style.IsLocked = true;
//Instanziieren Sie die Flagge.
flag = new StyleFlag();
// Legen Sie die Sperreinstellung fest.
flag.Locked = true;
// Wenden Sie den Stil auf die erste Zeile an.
sheet.Cells.ApplyRowStyle(0, style, flag);
```
Hier greifen wir auf den Stil der ersten Zeile zu und setzen dessen`IsLocked` Eigentum an`true` . Danach verwenden wir die`ApplyRowStyle()` Methode, um den Sperrstil auf die gesamte Zeile anzuwenden. Sie können diesen Schritt wiederholen, um alle anderen Zeilen zu sperren, die Sie schützen möchten.
## Schritt 5: Schützen Sie das Blatt
Nachdem wir nun die erforderlichen Zeilen entsperrt und gesperrt haben, ist es an der Zeit, das Arbeitsblatt zu schützen. Der Schutz stellt sicher, dass niemand die gesperrten Zeilen oder Zellen ändern kann, es sei denn, er entfernt das Schutzkennwort (sofern angegeben).
```csharp
// Schützen Sie das Blatt.
sheet.Protect(ProtectionType.All);
```
 In diesem Schritt schützen wir das gesamte Blatt mit`ProtectionType.All`. Diese Art von Schutz bedeutet, dass alle Aspekte des Blatts, einschließlich gesperrter Zeilen und Zellen, geschützt sind. Sie können diesen Schutz auch anpassen, indem Sie bei Bedarf verschiedene Schutztypen angeben.
## Schritt 6: Speichern der Arbeitsmappe
Abschließend müssen wir die Arbeitsmappe speichern, nachdem wir die erforderlichen Stile und Schutzmaßnahmen angewendet haben. Die Arbeitsmappe kann in verschiedenen Formaten gespeichert werden, z. B. Excel 97-2003, Excel 2010 usw.
```csharp
// Speichern Sie die Excel-Datei.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
Diese Codezeile speichert die Arbeitsmappe im Excel 97-2003-Format mit den angewendeten Änderungen. Sie können das Dateiformat nach Ihren Wünschen ändern, indem Sie aus einer Vielzahl von`SaveFormat` Optionen.
## Abschluss
Und da haben Sie es! Sie haben erfolgreich gelernt, wie Sie Zeilen in einem Arbeitsblatt mit Aspose.Cells für .NET schützen. Indem Sie die obigen Schritte befolgen, können Sie beliebige Zeilen oder Spalten nach Bedarf entsperren oder sperren und Schutz anwenden, um die Integrität Ihrer Daten sicherzustellen.
## Häufig gestellte Fragen
### Wie kann ich mehrere Zeilen gleichzeitig schützen?  
 Sie können mehrere Zeilen durchlaufen und den Sperrstil auf jede Zeile einzeln anwenden. Ersetzen Sie einfach`0` mit dem Zeilenindex, den Sie sperren möchten.
### Kann ich für den Blattschutz ein Passwort festlegen?  
 Ja! Sie können ein Passwort an den`sheet.Protect()` Methode zum Erzwingen des Kennwortschutzes.
### Kann ich Zellen statt ganzer Spalten entsperren?  
Ja! Anstatt Spalten zu entsperren, können Sie einzelne Zellen entsperren, indem Sie deren Stileigenschaften ändern.
### Was passiert, wenn ich versuche, eine geschützte Zeile zu bearbeiten?  
Wenn eine Zeile geschützt ist, verhindert Excel, dass an den gesperrten Zellen Änderungen vorgenommen werden, sofern Sie den Schutz des Blattes nicht aufheben.
### Kann ich bestimmte Bereiche hintereinander schützen?  
 Ja! Sie können einzelne Bereiche in einer Reihe sperren, indem Sie die`IsLocked` Eigenschaft für bestimmte Zellen innerhalb des Bereichs.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
