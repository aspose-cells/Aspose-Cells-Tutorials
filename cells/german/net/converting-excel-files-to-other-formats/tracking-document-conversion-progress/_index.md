---
title: Programmgesteuertes Verfolgen des Dokumentkonvertierungsfortschritts in .NET
linktitle: Programmgesteuertes Verfolgen des Dokumentkonvertierungsfortschritts in .NET
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in diesem ausführlichen Tutorial, wie Sie den Fortschritt der Dokumentkonvertierung programmgesteuert mit Aspose.Cells für .NET verfolgen.
weight: 20
url: /de/net/converting-excel-files-to-other-formats/tracking-document-conversion-progress/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Programmgesteuertes Verfolgen des Dokumentkonvertierungsfortschritts in .NET

## Einführung
Möchten Sie Ihren Dokumentkonvertierungsprozess mit Aspose.Cells für .NET verbessern? Dann sind Sie hier richtig! In diesem Tutorial werden wir uns eingehend mit der Verfolgung des Konvertierungsfortschritts von Excel-Dokumenten befassen, während diese in das PDF-Format umgewandelt werden. Wir führen Sie nicht nur durch die wesentlichen Schritte, um dies zu erreichen, sondern geben Ihnen dabei auch einige hilfreiche Einblicke. Also, legen wir los!
## Voraussetzungen
Bevor wir uns in die Einzelheiten der Verfolgung der Dokumentkonvertierung stürzen, sollten einige Voraussetzungen erfüllt sein:
1. Grundkenntnisse in C#: Da wir zum Codieren C# verwenden, sind grundlegende Kenntnisse dieser Programmiersprache hilfreich.
2. Visual Studio installiert: Dies dient als unsere Entwicklungsumgebung. Sie können jede beliebige Version verwenden, aber die neueste ist immer eine gute Wahl.
3.  Aspose.Cells für .NET: Stellen Sie sicher, dass Sie Aspose.Cells installiert haben. Sie können es herunterladen von der[Aspose-Website](https://releases.aspose.com/cells/net/).
4.  Eine Excel-Datei: Halten Sie eine Beispiel-Excel-Datei zur Konvertierung bereit. Sie können eine einfache`.xlsx` Datei, um mitzumachen.
## Pakete importieren
Nachdem wir nun unsere Voraussetzungen erfüllt haben, ist es an der Zeit, die erforderlichen Pakete in Ihr C#-Projekt zu importieren. So geht's:
### Neues Projekt erstellen
1. Öffnen Sie Visual Studio und erstellen Sie ein neues Projekt. Wählen Sie der Einfachheit halber eine Konsolen-App-Vorlage.
### Verweis auf Aspose.Cells hinzufügen
2. Klicken Sie mit der rechten Maustaste auf die Verweise im Projektmappen-Explorer, wählen Sie Verweis hinzufügen aus und navigieren Sie zur Aspose.Cells-Assembly, falls diese nicht automatisch hinzugefügt wird. Sie können den NuGet-Paket-Manager auch verwenden, indem Sie den folgenden Befehl in der Paket-Manager-Konsole ausführen:
```bash
Install-Package Aspose.Cells
```
### Namespaces importieren
3.  Ganz oben auf Ihrer`Program.cs` Fügen Sie die folgende Using-Direktive hinzu:
```csharp
using Aspose.Cells.Rendering;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Jetzt ist unser Projekt-Setup fertig!

Nachdem wir diese Grundlagen gelegt haben, können wir nun den eigentlichen Prozess der Verfolgung der Dokumentkonvertierung in überschaubare Schritte unterteilen. 
## Schritt 1: Definieren Sie Ihre Verzeichnisse
Geben Sie zunächst die Verzeichnisse an, in denen Ihre Quell- und Ausgabedateien gespeichert werden. So geht's:
```csharp
// Quellverzeichnis
string sourceDir = "Your Document Directory";
// Ausgabeverzeichnis
string outputDir = "Your Document Directory";
```
 Ersetzen Sie unbedingt`"Your Document Directory"` durch den tatsächlichen Pfad auf Ihrem System. So können Sie Ihre Dateien leichter finden.
## Schritt 2: Laden Sie die Arbeitsmappe
 Als nächstes müssen Sie Ihre Excel-Arbeitsmappe laden mit dem`Workbook` Klasse. So geht's:
```csharp
Workbook workbook = new Workbook(sourceDir + "PagesBook1.xlsx");
```
 Diese Codezeile erzeugt eine`Workbook` Objekt, das uns die Interaktion mit der angegebenen Excel-Datei ermöglicht.
## Schritt 3: PDF-Speicheroptionen einrichten
Nun richten wir die PDF-Speicheroptionen ein. Hier beginnt die Magie der Fortschrittsverfolgung. Sie erstellen eine Instanz von`PdfSaveOptions` und weisen Sie ihm einen Rückruf zu.
```csharp
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.PageSavingCallback = new TestPageSavingCallback();
```
Durch die Zuweisung eines benutzerdefinierten Rückrufs (`TestPageSavingCallback`) können wir unsere eigene Logik zur Verfolgung des Seitenkonvertierungsfortschritts implementieren.
## Schritt 4: Speichern Sie die Arbeitsmappe als PDF
 Wenn alles eingerichtet ist, ist es an der Zeit, Ihre Arbeitsmappe als PDF zu speichern. Verwenden Sie die`Save` Methode der`Workbook` Klasse wie folgt:
```csharp
workbook.Save(outputDir + "DocumentConversionProgress.pdf", pdfSaveOptions);
```
Diese Zeile löst den Konvertierungsprozess aus und ruft unsere Rückrufmethoden auf, während die Seiten verarbeitet werden.
## Schritt 5: Implementieren der Callback-Klasse
 Erstellen wir nun die`TestPageSavingCallback` Klasse. Hier definieren Sie, was zu Beginn und am Ende des Speicherns jeder Seite geschieht.
```csharp
public class TestPageSavingCallback : IPageSavingCallback
{
    public void PageStartSaving(PageStartSavingArgs args)
    {
        Console.WriteLine("Start saving page index {0} of pages {1}", args.PageIndex, args.PageCount);
        // Keine Seiten vor Seitenindex 2 ausgeben.
        if (args.PageIndex < 2)
        {
            args.IsToOutput = false;
        }
    }
    public void PageEndSaving(PageEndSavingArgs args)
    {
        Console.WriteLine("End saving page index {0} of pages {1}", args.PageIndex, args.PageCount);
        // Keine Seiten nach Seitenindex 8 ausgeben.
        if (args.PageIndex >= 8)
        {
            args.HasMorePages = false;
        }
    }
}
```
- `PageStartSaving`Diese Methode wird aufgerufen, kurz bevor eine Seite gespeichert wird. Hier protokollieren wir für jede Seite den Beginn des Speichervorgangs. Zusätzlich können wir steuern, ob die Seite ausgegeben werden soll oder nicht. In diesem Fall werden Seiten vor Index 2 übersprungen.
- `PageEndSaving`: Diese Methode wird aufgerufen, nachdem eine Seite gespeichert wurde. Sie ermöglicht es Ihnen, das Ende des Speicherns für jede Seite zu protokollieren und zu steuern, ob weitere Seiten verarbeitet werden sollen. In diesem Beispiel stoppen wir nach Seitenindex 8.
## Abschluss
Herzlichen Glückwunsch! Sie haben erfolgreich ein System zur Verfolgung des Fortschritts der Dokumentkonvertierung mit Aspose.Cells für .NET implementiert. Mit diesem Ansatz können Sie nicht nur den Konvertierungsprozess überwachen, sondern auch steuern, welche Seiten ein- oder ausgeschlossen werden sollen, wodurch Ihr Dokumentenmanagement wesentlich effizienter wird.
## Häufig gestellte Fragen
### Was ist Aspose.Cells?
Aspose.Cells ist eine leistungsstarke .NET-Bibliothek, mit der Entwickler Excel-Dateien programmgesteuert erstellen, bearbeiten und konvertieren können.
### Wie kann ich eine kostenlose Testversion von Aspose.Cells erhalten?
 Sie können eine kostenlose Testversion herunterladen von der[Aspose-Website](https://releases.aspose.com/).
### Ist es möglich, den Konvertierungsprozess anzupassen?
Ja, mithilfe von Rückrufen können Sie anpassen, wie Seiten während der Konvertierung verarbeitet werden.
### Kann ich den Namen der Ausgabedatei steuern?
Auf jeden Fall! Sie können beim Speichern der Arbeitsmappe einen beliebigen Namen für Ihre Ausgabedatei angeben.
### Wo finde ich Unterstützung für Aspose.Cells?
 Sie erhalten Unterstützung durch den Besuch der[Aspose-Forum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
