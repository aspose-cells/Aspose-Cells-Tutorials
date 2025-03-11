---
title: Konvertieren in XPS in .NET
linktitle: Konvertieren in XPS in .NET
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie mit Aspose.Cells für .NET in nur wenigen einfachen Schritten Excel-Dateien in das XPS-Format konvertieren, angeleitet durch praktische Codebeispiele.
weight: 10
url: /de/net/xps-and-pdf-operations/converting-to-xps/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konvertieren in XPS in .NET

## Einführung
Wenn es darum geht, Excel-Dateien in das XPS-Format zu konvertieren, fühlen Sie sich möglicherweise etwas überfordert, insbesondere wenn Sie neu in der Welt der Programmierung sind oder gerade erst in die .NET-Entwicklung einsteigen. Aber keine Angst! In diesem Handbuch werden wir den Prozess mithilfe von Aspose.Cells für .NET wie ein Profi aufschlüsseln. Wenn Sie mit dem Lesen fertig sind, haben Sie nicht nur ein klares Verständnis davon, wie dies geht, sondern auch einige praktische Erkenntnisse gewonnen, die Ihre Programmierkenntnisse verbessern können. Also, legen wir los!
## Voraussetzungen
Bevor Sie sich in die Details der Konvertierung stürzen, stellen wir sicher, dass Sie alles haben, was Sie brauchen. Folgendes benötigen Sie:
1. Visual Studio: Dies ist die IDE, in der Sie Ihren Code schreiben. Stellen Sie sicher, dass Sie sie installiert haben.
2.  Aspose.Cells-Bibliothek: Sie benötigen diese Bibliothek, um Excel-Dateien effizient zu verarbeiten. Sie können sie herunterladen von[Hier](https://releases.aspose.com/cells/net/).
3. Grundkenntnisse in .NET: Kenntnisse in C# oder VB.NET helfen Ihnen, unsere Beispiele besser zu verstehen.
4. Excel-Datei: Halten Sie in Ihrem Arbeitsverzeichnis eine Beispiel-Excel-Datei (für dieses Tutorial verwenden wir „Book1.xls“) bereit.

## Pakete importieren
Nachdem wir nun die Voraussetzungen abgedeckt haben, können wir mit dem Importieren der erforderlichen Pakete fortfahren. Das Importieren der richtigen Namespaces ist entscheidend, da es dem Compiler mitteilt, wo er die Klassen und Methoden finden kann, die wir verwenden werden.
### Richten Sie Ihr Projekt ein
Das Wichtigste zuerst! Öffnen Sie Visual Studio und erstellen Sie ein neues Projekt. Wählen Sie eine Konsolenanwendung, da diese unkompliziert und perfekt für diese Art von Aufgabe geeignet ist.
### Fügen Sie Aspose.Cells zu Ihrem Projekt hinzu
Um mit Aspose.Cells zu beginnen, müssen Sie die Bibliothek hinzufügen. Gehen Sie dazu wie folgt vor:
1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf Ihr Projekt.
2. Klicken Sie auf „NuGet-Pakete verwalten“.
3. Suchen Sie nach „Aspose.Cells“ und klicken Sie auf „Installieren“.
### Importieren der erforderlichen Namespaces
Am Anfang Ihrer C#-Datei müssen Sie Aspose.Cells importieren. Dazu müssen Sie die folgenden using-Direktiven hinzufügen:
```csharp
using System.IO;
using Aspose.Cells;
```
Lassen Sie uns den Prozess der Konvertierung einer Excel-Datei in das XPS-Format in einfache, überschaubare Schritte aufteilen. 
## Schritt 1: Definieren Sie Ihr Dokumentverzeichnis
Hier geben Sie den Pfad an, in dem sich Ihre Excel-Dateien befinden. Dies ist wichtig, da der Code wissen muss, wo die Dateien zu finden sind.
```csharp
string dataDir = "Your Document Directory"; // Stellen Sie sicher, dass Sie durch Ihren tatsächlichen Pfad ersetzen.
```
## Schritt 2: Öffnen Sie eine Excel-Datei
Laden wir nun Ihre Excel-Datei in ein Aspose-Arbeitsmappenobjekt. Durch diese Aktion erhält Ihr Programm Zugriff auf die Daten in dieser Excel-Datei.
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
 Hier erstellen wir eine neue Instanz des`Workbook` Klasse und laden Sie die Datei „Book1.xls“ hinein.
## Schritt 3: Zugriff auf das erste Arbeitsblatt
Als nächstes müssen wir uns das Arbeitsblatt besorgen, an dem wir arbeiten möchten. Da wir das erste Arbeitsblatt verwenden, sieht unser Code folgendermaßen aus:
```csharp
Worksheet sheet = workbook.Worksheets[0]; // Zugriff auf das erste Arbeitsblatt
```
Über diese Codezeile können Sie auf das erste Arbeitsblatt zugreifen und dort weitere Befehle eingeben.
## Schritt 4: Bild- und Druckoptionen konfigurieren
 Nun müssen wir definieren, wie wir unsere Ausgabe rendern möchten. Dazu müssen wir eine Instanz von`ImageOrPrintOptions` und Einstellen des gewünschten Ausgabeformats.
```csharp
Aspose.Cells.Rendering.ImageOrPrintOptions options = new Aspose.Cells.Rendering.ImageOrPrintOptions();
options.SaveFormat = SaveFormat.Xps; // Einstellen des Ausgabeformats auf XPS
```
Dieser Schritt teilt Aspose mit, dass wir den Excel-Inhalt in das XPS-Format konvertieren möchten.
## Schritt 5: Rendern Sie das Blatt
Nachdem die Optionen festgelegt wurden, ist es an der Zeit, das jeweilige Blatt zu rendern:
```csharp
Aspose.Cells.Rendering.SheetRender sr = new Aspose.Cells.Rendering.SheetRender(sheet, options);
sr.ToImage(0, dataDir + "out_printingxps.out.xps");
```
 Hier haben wir ein`SheetRender` Objekt, das sich um den Rendering-Prozess kümmert. Die Methode`ToImage` übernimmt die eigentliche Konvertierung und speichert die gerenderte Ausgabe als „out_printingxps.out.xps“.
## Schritt 6: Exportieren Sie die gesamte Arbeitsmappe nach XPS
Wenn Sie statt nur eines Blattes die gesamte Arbeitsmappe konvertieren möchten, können Sie diesen zusätzlichen Schritt ausführen:
```csharp
WorkbookRender wr = new WorkbookRender(workbook, options);
wr.ToImage(dataDir + "out_whole_printingxps.out.xps");
```
Mit diesem Codeausschnitt können Sie die gesamte Arbeitsmappe auf einmal exportieren. Dies ist effizient, wenn Sie mehrere Arbeitsblätter konvertieren müssen.
## Abschluss
Herzlichen Glückwunsch! Sie haben eine Excel-Datei mithilfe der Aspose.Cells-Bibliothek in .NET erfolgreich in das XPS-Format konvertiert. Das mag nach vielen Schritten aussehen, aber jeder einzelne spielt eine wichtige Rolle im Prozess. Mit diesem Wissen sind Sie gut gerüstet, um Excel-Dateien in Ihren Anwendungen zu verarbeiten und sie für verschiedene Formate zu optimieren. Wenn Sie also das nächste Mal jemand fragt, wie man diese lästigen Tabellen konvertiert, wissen Sie genau, was zu tun ist!
## Häufig gestellte Fragen
### Was ist das XPS-Format?
XPS (XML Paper Specification) ist ein festes Dokumentformat, bei dem das Layout und Erscheinungsbild von Dokumenten beibehält.
### Muss ich Aspose.Cells kaufen, um es zu verwenden?
 Sie können eine kostenlose Testversion von Aspose.Cells ausprobieren[Hier](https://releases.aspose.com/). Anschließend müssen Sie möglicherweise eine Lizenz erwerben, um die volle Funktionalität zu erhalten.
### Kann ich mehrere Excel-Dateien gleichzeitig konvertieren?
Ja, Sie können den Code so anpassen, dass er mehrere Dateien im Verzeichnis durchläuft und für jede Datei die gleiche Konvertierungslogik anwendet.
### Was ist, wenn ich nur bestimmte Blätter konvertieren muss?
 Sie können den Index des gewünschten Blatts im`SheetRender` Objekt, wie in unseren Schritten gezeigt.
### Wo finde ich weitere Informationen zu Aspose.Cells?
 Entdecken Sie die[Dokumentation](https://reference.aspose.com/cells/net/) für erweiterte Funktionen und Optionen, die mit der Bibliothek verfügbar sind.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
