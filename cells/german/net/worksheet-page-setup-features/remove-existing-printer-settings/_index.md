---
title: Vorhandene Druckereinstellungen aus Arbeitsblättern entfernen
linktitle: Vorhandene Druckereinstellungen aus Arbeitsblättern entfernen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in dieser ausführlichen Schritt-für-Schritt-Anleitung, wie Sie mit Aspose.Cells für .NET vorhandene Druckereinstellungen aus Excel-Arbeitsblättern entfernen.
weight: 19
url: /de/net/worksheet-page-setup-features/remove-existing-printer-settings/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vorhandene Druckereinstellungen aus Arbeitsblättern entfernen

## Einführung
Wenn Sie schon einmal mit Excel-Dateien gearbeitet haben, wissen Sie, wie wichtig es ist, dass Ihre Dokumente richtig eingerichtet sind – insbesondere beim Drucken. Wussten Sie, dass Druckereinstellungen manchmal von einem Arbeitsblatt auf ein anderes übertragen werden können, was möglicherweise Ihr Drucklayout stört? In diesem Tutorial erfahren Sie, wie Sie mithilfe der leistungsstarken Aspose.Cells-Bibliothek für .NET vorhandene Druckereinstellungen ganz einfach aus Arbeitsblättern entfernen können. Egal, ob Sie ein erfahrener Entwickler sind oder gerade erst anfangen, dieser Artikel soll Sie durch jeden Schritt führen. Lassen Sie uns anfangen!
## Voraussetzungen
Bevor wir uns in die Programmiermagie stürzen, müssen Sie einige Dinge einrichten:
1. Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem Computer installiert ist.
2. Aspose.Cells für .NET-Bibliothek: Sie können die Aspose.Cells-Bibliothek herunterladen von[Hier](https://releases.aspose.com/cells/net/).
3. Grundlegende Kenntnisse in C#: Da es in diesem Tutorial um die Codierung in C# geht, sind grundlegende Kenntnisse der Sprache hilfreich.
4. Beispiel-Excel-Datei: Sie benötigen eine vorhandene Excel-Datei mit den Druckereinstellungen, die Sie entfernen möchten. Sie können gerne ein Beispiel erstellen oder ein vorhandenes Dokument verwenden.
Sobald Sie Ihre Umgebung eingerichtet haben, können wir mit der Entschlüsselung des Codes beginnen.
## Pakete importieren
Bevor wir uns in den eigentlichen Code zum Entfernen der Druckereinstellungen stürzen, müssen wir sicherstellen, dass wir die richtigen Pakete in unser C#-Projekt importiert haben. Folgendes benötigen Sie am Anfang Ihrer Codedatei:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Nachdem wir nun alles haben, was wir brauchen, können wir uns mit den Einzelheiten des Codes befassen.
## Schritt 1: Definieren Sie Ihr Quell- und Ausgabeverzeichnis
Im ersten Schritt geben Sie an, wo sich Ihr ursprüngliches Excel-Dokument befindet und wo Sie die geänderte Version speichern möchten.
```csharp
// Quellverzeichnis
string sourceDir = "Your Document Directory\\";
// Ausgabeverzeichnis
string outputDir = "Your Document Directory\\";
```
 Ersetzen Sie unbedingt`"Your Document Directory\\"` durch den tatsächlichen Pfad zu Ihren Dokumenten.
## Schritt 2: Laden Sie die Excel-Quelldatei
Als Nächstes laden wir die Arbeitsmappe (Excel-Datei), die die Druckereinstellungen enthält. Sie sollten sicherstellen, dass der Dateipfad korrekt ist.
```csharp
// Quell-Excel-Datei laden
Workbook wb = new Workbook(sourceDir + "sampleRemoveExistingPrinterSettingsOfWorksheets.xlsx");
```
 Hier laden wir die angegebene Excel-Datei in eine`Workbook` Objekt mit dem Namen`wb`.
## Schritt 3: Ermitteln Sie die Anzahl der Arbeitsblätter
Wir müssen wissen, wie viele Arbeitsblätter sich in der Arbeitsmappe befinden, damit wir sie durchlaufen und etwaige Druckereinstellungen überprüfen können.
```csharp
// Abrufen der Blattanzahl der Arbeitsmappe
int sheetCount = wb.Worksheets.Count;
```
Diese Codezeile ruft die Anzahl der in der Arbeitsmappe vorhandenen Arbeitsblätter ab.
## Schritt 4: Alle Arbeitsblätter durchlaufen
Lassen Sie uns nun die Bühne so einrichten, dass jedes Arbeitsblatt in der Arbeitsmappe durchlaufen wird. Wir werden prüfen, ob für jedes Arbeitsblatt vorhandene Druckereinstellungen vorhanden sind.
```csharp
// Alle Blätter iterieren
for (int i = 0; i < sheetCount; i++)
{
    // Zugriff auf das i-te Arbeitsblatt
    Worksheet ws = wb.Worksheets[i];
```
## Schritt 5: Seiteneinrichtung für Zugriffsarbeitsblätter
Jedes Arbeitsblatt verfügt über Seiteneinrichtungseigenschaften, die die Druckereinstellungen enthalten, die wir überprüfen und möglicherweise entfernen möchten.
```csharp
    // Einrichten der Access-Arbeitsblattseite
    PageSetup ps = ws.PageSetup;
```
## Schritt 6: Überprüfen Sie, ob vorhandene Druckereinstellungen vorhanden sind
Es ist an der Zeit zu prüfen, ob Druckereinstellungen für das aktuelle Arbeitsblatt vorhanden sind. Wenn dies der Fall ist, drucken wir eine Meldung und entfernen sie.
```csharp
    // Prüfen Sie, ob Druckereinstellungen für dieses Arbeitsblatt vorhanden sind
    if (ps.PrinterSettings != null)
    {
        Console.WriteLine("PrinterSettings of this worksheet exist.");
```
## Schritt 7: Drucken Sie die Arbeitsblattdetails
Wenn Druckereinstellungen gefunden werden, zeigen wir einige nützliche Informationen über das Arbeitsblatt und seine Druckereinstellungen an.
```csharp
        Console.WriteLine("Sheet Name: " + ws.Name);
        Console.WriteLine("Paper Size: " + ps.PaperSize);
```
Dadurch können wir überprüfen, für welche Blätter die Druckereinstellungen definiert sind.
## Schritt 8: Entfernen Sie die Druckereinstellungen
 Jetzt kommt der Hauptakt! Wir entfernen die bestehenden Druckereinstellungen, indem wir`null` zur`PrinterSettings` Eigentum.
```csharp
        // Entfernen Sie die Druckereinstellungen, indem Sie sie auf null setzen
        ps.PrinterSettings = null;
        Console.WriteLine("Printer settings of this worksheet are now removed by setting it null.");
        Console.WriteLine("");
    }
}
```
## Schritt 9: Speichern der geänderten Arbeitsmappe
Lassen Sie uns abschließend die Arbeitsmappe speichern, nachdem Sie alle erforderlichen Änderungen vorgenommen haben.
```csharp
// Speichern der Arbeitsmappe
wb.Save(outputDir + "outputRemoveExistingPrinterSettingsOfWorksheets.xlsx");
```
## Abschluss
Und da haben Sie es! Sie haben gerade gelernt, wie Sie mit Aspose.Cells für .NET vorhandene Druckereinstellungen aus Excel-Arbeitsblättern entfernen. Mit diesem einfachen Vorgang können Sie sicherstellen, dass Ihre Dokumente genau so gedruckt werden, wie Sie es möchten – ohne dass lästige alte Einstellungen übrig bleiben. Wenn Sie also das nächste Mal Probleme mit den Druckereinstellungen haben, wissen Sie genau, was zu tun ist!
## Häufig gestellte Fragen
### Was ist Aspose.Cells?
Aspose.Cells ist eine .NET-Bibliothek, die es Entwicklern ermöglicht, nahtlos mit Excel-Dateien zu arbeiten, ohne dass Microsoft Excel installiert sein muss.
### Muss ich Aspose.Cells kaufen, um es zu verwenden?
 Sie können mit einer kostenlosen Testversion beginnen, für die langfristige Nutzung müssen Sie jedoch eine Lizenz erwerben. Überprüfen Sie[Hier](https://purchase.aspose.com/buy) für Optionen.
### Kann ich die Druckereinstellungen für alle Arbeitsblätter auf einmal entfernen?
Ja! Wie wir im Tutorial gezeigt haben, können Sie jedes Arbeitsblatt durchlaufen, um die Einstellungen zu entfernen.
### Besteht bei der Änderung der Druckereinstellungen die Gefahr eines Datenverlusts?
Nein, das Entfernen der Druckereinstellungen wirkt sich nicht auf die eigentlichen Daten in Ihren Arbeitsblättern aus.
### Wo finde ich Hilfe zu Aspose.Cells?
 Community-Unterstützung und Ressourcen finden Sie unter[Aspose-Forum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
