---
title: Arbeitsmappe im Text-CSV-Format speichern
linktitle: Arbeitsmappe im Text-CSV-Format speichern
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in diesem umfassenden Schritt-für-Schritt-Tutorial für .NET-Entwickler, wie Sie mit Aspose.Cells Excel-Arbeitsmappen mühelos in das CSV-Format konvertieren.
weight: 17
url: /de/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Arbeitsmappe im Text-CSV-Format speichern

## Einführung
Beim Umgang mit Daten kann das von Ihnen gewählte Format entscheidend dafür sein, wie einfach Sie damit arbeiten können. Zu den gängigsten Formaten für die Verarbeitung tabellarischer Daten gehört CSV (Comma-Separated Values). Wenn Sie als Entwickler mit Excel-Dateien arbeiten und Arbeitsmappen in das CSV-Format konvertieren müssen, ist Aspose.Cells für .NET eine fantastische Bibliothek, die diese Aufgabe vereinfacht. In diesem Tutorial werden wir die Schritte zum nahtlosen Konvertieren einer Excel-Arbeitsmappe in ein CSV-Textformat aufschlüsseln.
## Voraussetzungen
Bevor wir loslegen, stellen wir sicher, dass Sie alles für den Start bereit haben:
1. Grundkenntnisse in C# und .NET: Da wir Code in C# schreiben werden, ist die Vertrautheit mit der Sprache und dem .NET-Framework unerlässlich.
2. Aspose.Cells-Bibliothek: Stellen Sie sicher, dass die Aspose.Cells-Bibliothek für .NET in Ihrer Entwicklungsumgebung installiert ist. Sie können sie herunterladen[Hier](https://releases.aspose.com/cells/net/).
3. Visual Studio oder eine beliebige C#-IDE: Sie benötigen eine integrierte Entwicklungsumgebung (IDE), um Ihren Code zu schreiben und auszuführen. Visual Studio ist eine beliebte Wahl.
4. Excel-Arbeitsmappe: Bereiten Sie eine Beispiel-Excel-Arbeitsmappe (z. B. „book1.xls“) vor, die einige Daten enthält, um die Konvertierung zu testen.
## Pakete importieren
Nachdem wir nun unsere Voraussetzungen erfüllt haben, besteht der erste Schritt des Prozesses darin, die erforderlichen Pakete zu importieren. In Ihrem C#-Projekt müssen Sie den folgenden Namespace oben in Ihrer Codedatei einfügen:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Über diese Namespaces erhalten Sie Zugriff auf die Klassen und Methoden, die Sie zum Arbeiten mit Excel-Dateien und Verwalten von Speicherströmen benötigen.
## Schritt 1: Pfad zum Dokumentenverzeichnis festlegen
Der erste Schritt in unserem Prozess besteht darin, zu definieren, wo unsere Dokumente (Excel-Arbeitsmappen) gespeichert sind. Dies ist wichtig, da unser Programm dadurch weiß, wo sich die zu verarbeitenden Dateien befinden. 
```csharp
// Der Pfad zum Dokumentverzeichnis.
string dataDir = "Your Document Directory";
```
 Ersetzen Sie unbedingt`"Your Document Directory"` durch den tatsächlichen Pfad, in dem sich Ihre Datei „book1.xls“ befindet. Dies kann ein Verzeichnis auf Ihrem Computer oder ein Pfad zu einem Server sein.
## Schritt 2: Laden Sie Ihre Quellarbeitsmappe
Als Nächstes müssen wir die Excel-Arbeitsmappe laden, die in das CSV-Format konvertiert wird.
```csharp
// Laden Sie Ihre Quellarbeitsmappe
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
 Der`Workbook` Die Klasse aus der Aspose.Cells-Bibliothek ermöglicht die Bearbeitung und den Zugriff auf Excel-Arbeitsmappen. Durch Übergabe des Dateipfads laden wir die angegebene Arbeitsmappe zur Verarbeitung.
## Schritt 3: Initialisieren eines Byte-Arrays für Arbeitsmappendaten
Bevor wir mit der Konvertierung der Arbeitsmappe in CSV beginnen, müssen wir ein leeres Byte-Array initialisieren, das schließlich alle Arbeitsblattdaten enthalten wird.
```csharp
// 0-Byte-Array
byte[] workbookData = new byte[0];
```
Dieses Byte-Array kombiniert die Daten aus jedem Arbeitsblatt zu einer einzigen Struktur, die wir später in eine Datei schreiben können.
## Schritt 4: Optionen zum Speichern von Text einrichten
Legen wir nun die Optionen für das Speichern des Textformats fest. Sie können benutzerdefinierte Trennzeichen wählen oder bei Tabulatoren bleiben.
```csharp
// Optionen zum Speichern von Text. Sie können jede Art von Trennzeichen verwenden
TxtSaveOptions opts = new TxtSaveOptions();
opts.Separator = '\t'; // Tabulator als Trennzeichen festlegen
```
 In diesem Beispiel verwenden wir ein Tabulatorzeichen als Trennzeichen. Sie können ersetzen`'\t'` durch ein beliebiges Zeichen, beispielsweise ein Komma (`,`), je nachdem, wie Sie Ihre CSV-Datei formatieren möchten.
## Schritt 5: Durch jedes Arbeitsblatt iterieren
 Als nächstes durchlaufen wir alle Arbeitsblätter in der Arbeitsmappe und speichern jedes in unserem`workbookData` Array, aber Sie müssen zuerst auswählen, an welchem Arbeitsblatt gearbeitet werden soll.
```csharp
// Kopieren Sie alle Arbeitsblattdaten im Textformat in das Arbeitsmappendatenarray
for (int idx = 0; idx < workbook.Worksheets.Count; idx++)
{
    // Das aktive Arbeitsblatt im Textformat speichern
    MemoryStream ms = new MemoryStream();
    workbook.Worksheets.ActiveSheetIndex = idx;
    workbook.Save(ms, opts);
```
 Die Schleife durchläuft jedes Arbeitsblatt in der Arbeitsmappe.`ActiveSheetIndex` ist so eingestellt, dass bei jedem Durchlauf der Schleife das aktuelle Arbeitsblatt gespeichert wird. Die Ergebnisse werden mit einem`MemoryStream`.
## Schritt 6: Arbeitsblattdaten abrufen
 Nach dem Speichern eines Arbeitsblatts im Speicherstrom besteht der nächste Schritt darin, diese Daten abzurufen und an unsere anzuhängen`workbookData` -Array.
```csharp
    // Speichern Sie die Arbeitsblattdaten im Blattdaten-Array
    ms.Position = 0; // Position des Speicherstroms zurücksetzen
    byte[] sheetData = ms.ToArray(); // Holen Sie sich das Byte-Array
```
`ms.Position = 0;` setzt die Position zum Lesen nach dem Schreiben zurück. Dann verwenden wir`ToArray()` um den Speicherstrom in ein Byte-Array zu konvertieren, das die Arbeitsblattdaten enthält.
## Schritt 7: Arbeitsblattdaten kombinieren
 Nun werden wir die Daten aus jedem Arbeitsblatt in einem einzigen zusammenfassen.`workbookData` Array, das zuvor initialisiert wurde.
```csharp
    // Kombinieren Sie diese Arbeitsblattdaten zu einem Arbeitsmappendatenarray
    byte[] combinedArray = new byte[workbookData.Length + sheetData.Length];
    Array.Copy(workbookData, 0, combinedArray, 0, workbookData.Length);
    Array.Copy(sheetData, 0, combinedArray, workbookData.Length, sheetData.Length);
    workbookData = combinedArray;
}
```
Wir erstellen ein neues Array, das groß genug ist, um sowohl vorhandene Arbeitsmappendaten als auch neue Arbeitsblattdaten aufzunehmen. Anschließend kopieren wir die vorhandenen und neuen Daten zur späteren Verwendung in dieses kombinierte Array.
## Schritt 8: Gesamte Arbeitsmappendaten in Datei speichern
 Schließlich, mit all den Daten kombiniert in unserem`workbookData` Array, wir können dieses Array in einem angegebenen Dateipfad speichern.
```csharp
//Gesamte Arbeitsmappendaten in einer Datei speichern
File.WriteAllBytes(dataDir + "out.txt", workbookData);
```
`WriteAllBytes` nimmt das kombinierte Byte-Array und schreibt es in eine Textdatei mit dem Namen „out.txt“ im angegebenen Verzeichnis.
## Abschluss
Und da haben Sie es! Sie haben eine Excel-Arbeitsmappe erfolgreich mit Aspose.Cells für .NET in ein CSV-Format konvertiert. Dieser Prozess ist nicht nur effizient, sondern ermöglicht auch die einfache Bearbeitung von Excel-Daten für weitere Analysen oder Berichte. Jetzt können Sie Ihre Datenverarbeitungsaufgaben automatisieren oder diese Funktionalität sogar in größere Anwendungen integrieren.
## Häufig gestellte Fragen
### Kann ich für die CSV-Datei andere Trennzeichen verwenden?
 Ja, Sie können die`opts.Separator` durch jedes beliebige Zeichen, beispielsweise Kommas oder Pipe-Zeichen.
### Ist die Nutzung von Aspose.Cells kostenlos?
 Aspose.Cells ist nicht kostenlos, aber Sie können eine kostenlose Testversion erhalten[Hier](https://releases.aspose.com/).
### In welchen Formaten außer CSV kann ich speichern?
Aspose.Cells ermöglicht das Speichern in mehreren Formaten, darunter XLSX, PDF und mehr.
### Kann ich mit Aspose.Cells große Excel-Dateien verarbeiten?
Ja, Aspose.Cells ist für die effiziente Verarbeitung großer Dateien ausgelegt, die Leistung kann jedoch von den Systemressourcen abhängen.
### Wo finde ich ausführlichere Dokumentation?
Ausführliche Dokumentationen und Beispiele finden Sie auf der[Referenzseite](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
