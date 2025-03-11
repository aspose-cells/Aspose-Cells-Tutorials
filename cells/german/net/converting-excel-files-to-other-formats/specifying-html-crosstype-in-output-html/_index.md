---
title: Programmgesteuertes Angeben von HTML-CrossType in der HTML-Ausgabe in .NET
linktitle: Programmgesteuertes Angeben von HTML-CrossType in der HTML-Ausgabe in .NET
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie HTML CrossType in Aspose.Cells für .NET angeben. Folgen Sie unserem Schritt-für-Schritt-Tutorial, um Excel-Dateien präzise in HTML zu konvertieren.
weight: 17
url: /de/net/converting-excel-files-to-other-formats/specifying-html-crosstype-in-output-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Programmgesteuertes Angeben von HTML-CrossType in der HTML-Ausgabe in .NET

## Einführung
Wenn Sie Excel-Dateien in .NET-Anwendungen in HTML konvertieren, müssen Sie möglicherweise angeben, wie Querverweise in der Ausgabe behandelt werden. Die Klasse HtmlSaveOptions in Aspose.Cells für .NET bietet verschiedene Einstellungen zur Steuerung des Konvertierungsprozesses, und eine dieser Optionen ist HtmlCrossType. In diesem Tutorial erfahren Sie, wie Sie den HTML-Quertyp beim Exportieren von Excel-Dateien in das HTML-Format programmgesteuert angeben. 
## Voraussetzungen
Bevor Sie sich in den Code vertiefen, stellen Sie sicher, dass Sie über Folgendes verfügen:
-  Aspose.Cells für .NET: Stellen Sie sicher, dass die Aspose.Cells-Bibliothek in Ihrem Projekt installiert ist. Sie können sie von der[Aspose-Website](https://releases.aspose.com/cells/net/).
- Visual Studio: Eine funktionierende Installation von Visual Studio oder einer anderen .NET-Entwicklungsumgebung.
- Grundkenntnisse in C#: Wenn Sie mit der C#-Programmierung vertraut sind, verstehen Sie die Beispiele besser.
-  Beispiel-Excel-Datei: Halten Sie eine Beispiel-Excel-Datei bereit, mit der Sie arbeiten können. Für dieses Beispiel verwenden wir`sampleHtmlCrossStringType.xlsx`.
## Pakete importieren
Um zu beginnen, müssen Sie die erforderlichen Aspose.Cells-Namespaces importieren. So können Sie das tun:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Wir wollen dies Schritt für Schritt aufschlüsseln, damit Sie es leicht nachvollziehen und diese Funktionalität in Ihren eigenen Projekten implementieren können.
## Schritt 1: Definieren Sie Ihre Quell- und Ausgabeverzeichnisse
Zuerst müssen Sie die Verzeichnisse für Ihre Excel-Quelldatei festlegen und den Speicherort für die HTML-Ausgabedatei festlegen.
```csharp
// Quellverzeichnis
string sourceDir = "Your Document Directory";
// Ausgabeverzeichnis
string outputDir = "Your Document Directory";
```
## Schritt 2: Laden Sie die Excel-Beispieldatei
 Laden Sie als nächstes Ihre Excel-Beispieldatei in ein`Workbook` Objekt. Hier beginnt die ganze Magie.
```csharp
// Laden Sie die Excel-Beispieldatei
Workbook wb = new Workbook(sourceDir + "sampleHtmlCrossStringType.xlsx");
```
 Ersetzen Sie hier`"Your Document Directory"` durch den tatsächlichen Pfad, in dem sich Ihre Excel-Datei befindet. Diese Zeile liest die Excel-Datei in den Speicher, damit Sie sie bearbeiten können.
## Schritt 3: HTML-Speicheroptionen festlegen
 Jetzt erstellen wir eine Instanz von`HtmlSaveOptions`, womit Sie konfigurieren können, wie die Excel-Datei in HTML konvertiert wird.
```csharp
// HTML-Cross-Type angeben
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.HtmlCrossStringType = HtmlCrossType.Default;
```
 In diesem Schritt haben wir die`HtmlCrossStringType` Zu`HtmlCrossType.Default`, eine der verfügbaren Optionen zum Umgang mit Querverweisen im Ausgabe-HTML.
## Schritt 4: Ändern Sie den Kreuztyp nach Bedarf
 Sie können verschiedene Typen angeben für`HtmlCrossStringType` basierend auf Ihren Anforderungen. Hier sind die verschiedenen Optionen, die Sie verwenden können:
- `HtmlCrossType.Default`: Der Standardkreuztyp.
- `HtmlCrossType.MSExport`: Exportiert das HTML mit MS Excel-ähnlichem Verhalten.
- `HtmlCrossType.Cross`: Erstellt Querverweise.
- `HtmlCrossType.FitToCell`: Passt die Querverweise an die Zellabmessungen an.
 Sie können die`HtmlCrossStringType` so was:
```csharp
opts.HtmlCrossStringType = HtmlCrossType.MSExport;
// oder
opts.HtmlCrossStringType = HtmlCrossType.Cross;
// oder
opts.HtmlCrossStringType = HtmlCrossType.FitToCell;
```
## Schritt 5: Speichern Sie die Ausgabe-HTML-Datei
 Nachdem Sie Ihre Optionen konfiguriert haben, können Sie die konvertierte HTML-Datei speichern. Verwenden Sie dazu die`Save` Methode auf Ihrem`Workbook` Objekt:
```csharp
// Ausgabe-HTML
wb.Save(outputDir + "out" + opts.HtmlCrossStringType + ".htm", opts);
```
 Hier benennen wir die Ausgabedatei basierend auf dem`HtmlCrossStringType` wir eingestellt haben. So können Sie leicht erkennen, welcher Kreuztyp bei der Konvertierung verwendet wurde.
## Schritt 6: Erfolgreiche Ausführung bestätigen
Abschließend ist es immer sinnvoll, zu bestätigen, dass Ihr Vorgang erfolgreich war. Sie können eine Meldung auf der Konsole ausgeben:
```csharp
Console.WriteLine("SpecifyHtmlCrossTypeInOutputHTML executed successfully.\r\n");
```
Dadurch erfahren Sie, dass der Vorgang fehlerfrei abgeschlossen wurde.
## Abschluss
Und da haben Sie es! Sie haben den HTML-Cross-Type für Ihren Excel-Export in .NET mithilfe von Aspose.Cells erfolgreich angegeben. Diese Funktion ist besonders nützlich, wenn Sie bestimmte Formatierungen oder Referenzen in Ihrer HTML-Ausgabe beibehalten müssen, um sicherzustellen, dass Ihre konvertierten Dokumente Ihren Anforderungen entsprechen.
## Häufig gestellte Fragen
### Was ist HtmlCrossType in Aspose.Cells?  
HtmlCrossType definiert, wie Querverweise in der Excel-Datei während der HTML-Konvertierung behandelt werden. Sie können Optionen wie Standard, MSExport, Cross und FitToCell auswählen.
### Kann ich Aspose.Cells kostenlos nutzen?  
 Aspose.Cells bietet eine kostenlose Testversion an. Sie können diese von ihrem[Webseite](https://releases.aspose.com/).
### Wie installiere ich Aspose.Cells in meinem .NET-Projekt?  
 Sie können Aspose.Cells über den NuGet-Paket-Manager in Visual Studio installieren, indem Sie den folgenden Befehl ausführen:`Install-Package Aspose.Cells`.
### Wo finde ich die Dokumentation für Aspose.Cells?  
 Eine ausführliche Dokumentation finden Sie auf Aspose.Cells[Hier](https://reference.aspose.com/cells/net/).
### Was soll ich tun, wenn beim Speichern der HTML-Datei ein Fehler auftritt?  
Stellen Sie sicher, dass die Verzeichnispfade korrekt sind und dass Sie über Schreibberechtigungen für das Ausgabeverzeichnis verfügen. Wenn das Problem weiterhin besteht, suchen Sie im Aspose-Supportforum nach Hilfe.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
