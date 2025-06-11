---
"description": "Erfahren Sie in dieser Schritt-für-Schritt-Anleitung, wie Sie den Komprimierungsgrad von Excel-Arbeitsmappen mit Aspose.Cells für .NET anpassen. Optimieren Sie Ihre Dateiverwaltung."
"linktitle": "Komprimierungsstufe in der Arbeitsmappe anpassen"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Komprimierungsstufe in der Arbeitsmappe anpassen"
"url": "/de/net/workbook-operations/adjust-compression-level/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Komprimierungsstufe in der Arbeitsmappe anpassen

## Einführung
Bei der Verwaltung großer Excel-Dateien ist Komprimierung entscheidend. Sie spart nicht nur Speicherplatz, sondern macht auch Dateiübertragungen schneller und effizienter. Wenn Sie mit Aspose.Cells für .NET arbeiten, können Sie die Komprimierungsstufe Ihrer Arbeitsmappen ganz einfach anpassen. In dieser Anleitung führen wir Sie Schritt für Schritt durch den Prozess und stellen sicher, dass Sie jeden Teil des Codes und seine Funktionsweise verstehen.
## Voraussetzungen
Bevor Sie sich in den Code vertiefen, müssen einige Voraussetzungen erfüllt sein:
1. Grundkenntnisse in C#: Wenn Sie mit der C#-Programmierung vertraut sind, können Sie die Codeausschnitte besser verstehen.
2. Aspose.Cells Bibliothek: Sie müssen die Aspose.Cells Bibliothek installiert haben. Sie können sie herunterladen von [Hier](https://releases.aspose.com/cells/net/).
3. Visual Studio: Zum Ausführen des Codes ist eine Entwicklungsumgebung wie Visual Studio erforderlich.
4. .NET Framework: Stellen Sie sicher, dass Ihr Projekt mit einer kompatiblen Version des .NET Frameworks eingerichtet ist.
## Pakete importieren
Um zu beginnen, müssen Sie die erforderlichen Pakete in Ihr C#-Projekt importieren. So geht's:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```
Diese Pakete sind für die Arbeit mit Excel-Dateien mit der Aspose.Cells-Bibliothek unerlässlich. Die `Aspose.Cells` Namespace enthält alle Klassen, die Sie zum Bearbeiten von Excel-Dateien benötigen, während `Aspose.Cells.Xlsb` bietet die Möglichkeit, Dateien im XLSB-Format zu speichern.
Lassen Sie uns nun den Vorgang zum Anpassen der Komprimierungsstufe in einer Arbeitsmappe in überschaubare Schritte unterteilen.
## Schritt 1: Quell- und Ausgabeverzeichnisse definieren
Zunächst müssen Sie angeben, wo sich Ihre Quelldateien befinden und wo Sie die Ausgabedateien speichern möchten. Dies ist wichtig, damit Ihr Programm weiß, wo es die benötigten Dateien findet.
```csharp
// Quellverzeichnis
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```
Ersetzen `"Your Document Directory"` mit dem tatsächlichen Pfad zu Ihren Verzeichnissen. Dies hilft dem Programm, die zu komprimierenden Dateien zu finden.
## Schritt 2: Laden Sie die Arbeitsmappe
Als Nächstes laden Sie die Arbeitsmappe, die Sie komprimieren möchten. Und hier beginnt die Magie!
```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```
In dieser Zeile erstellen wir eine neue Instanz des `Workbook` Klasse und laden Sie eine vorhandene Excel-Datei. Stellen Sie sicher, dass der Dateiname mit dem Namen in Ihrem Quellverzeichnis übereinstimmt.
## Schritt 3: Speicheroptionen einrichten
Jetzt ist es an der Zeit, die Speicheroptionen zu konfigurieren. Wir legen den Komprimierungstyp für die Ausgabedatei fest. 
```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```
Der `XlsbSaveOptions` Mit der Klasse können Sie beim Speichern Ihrer Arbeitsmappe im XLSB-Format verschiedene Optionen angeben, einschließlich der Komprimierungsstufen.
## Schritt 4: Messen Sie die Komprimierungszeit für Stufe 1
Beginnen wir mit der ersten Komprimierungsstufe. Wir messen, wie lange es dauert, die Arbeitsmappe mit dieser Komprimierungsstufe zu speichern.
```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```
Hier setzen wir den Komprimierungstyp auf Stufe 1, speichern die Arbeitsmappe und messen anschließend die verstrichene Zeit. So erhalten wir eine Vorstellung davon, wie lange der Vorgang dauert.
## Schritt 5: Komprimierungszeit für Stufe 6 messen
Als nächstes sehen wir uns an, wie die Komprimierung der Stufe 6 funktioniert.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level6;
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```
Dieser Schritt ähnelt dem vorherigen, wir ändern jedoch die Komprimierungsstufe auf Stufe 6. Sie werden feststellen, dass die benötigte Zeit je nach Komplexität der Arbeitsmappe variieren kann.
## Schritt 6: Komprimierungszeit für Stufe 9 messen
Schauen wir uns abschließend die Leistung mit der höchsten Komprimierungsstufe an.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level9;
workbook.Save(outDir + "LargeSampleFile_level_9_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 9 Elapsed Time: " + elapsedMs);
```
In diesem Schritt stellen wir die Komprimierungsstufe auf Stufe 9 ein. Hier sehen Sie normalerweise die deutlichste Reduzierung der Dateigröße, die Verarbeitung kann jedoch länger dauern.
## Schritt 7: Endgültige Ausgabe
Nach dem Durchlaufen aller Komprimierungsstufen können Sie eine Meldung ausgeben, dass der Vorgang erfolgreich abgeschlossen wurde.
```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```
Diese einfache Codezeile bestätigt, dass die Ausführung Ihres Programms ohne Probleme abgeschlossen wurde.
## Abschluss
Das Anpassen des Komprimierungsgrads Ihrer Arbeitsmappen mit Aspose.Cells für .NET ist ein unkomplizierter Vorgang, der zu erheblichen Vorteilen hinsichtlich Dateigröße und Leistung führen kann. Mit den in dieser Anleitung beschriebenen Schritten können Sie die Komprimierung problemlos in Ihre Anwendungen implementieren und die Effizienz Ihrer Excel-Dateiverwaltung verbessern.
## Häufig gestellte Fragen
### Was ist Aspose.Cells?  
Aspose.Cells ist eine leistungsstarke Bibliothek für .NET, mit der Entwickler Excel-Dateien erstellen, bearbeiten und konvertieren können, ohne Microsoft Excel zu benötigen.
### Wie installiere ich Aspose.Cells?  
Sie können Aspose.Cells herunterladen und installieren von der [Aspose-Website](https://releases.aspose.com/cells/net/).
### Welche Komprimierungsstufen sind verfügbar?  
Aspose.Cells unterstützt mehrere Komprimierungsstufen von Stufe 1 (niedrigste Komprimierung) bis Stufe 9 (höchste Komprimierung).
### Kann ich Aspose.Cells kostenlos testen?  
Ja! Sie können eine kostenlose Testversion von Aspose.Cells erhalten [Hier](https://releases.aspose.com/).
### Wo finde ich Unterstützung für Aspose.Cells?  
Bei Fragen oder Support können Sie das Aspose-Supportforum besuchen [Hier](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}