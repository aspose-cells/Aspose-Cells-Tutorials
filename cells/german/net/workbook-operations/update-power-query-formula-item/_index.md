---
"description": "Erfahren Sie in dieser umfassenden Schritt-für-Schritt-Anleitung, wie Sie Power Query-Formeln in Excel mit Aspose.Cells für .NET aktualisieren."
"linktitle": "Aktualisieren des Power Query-Formelelements in der Arbeitsmappe"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Aktualisieren des Power Query-Formelelements in der Arbeitsmappe"
"url": "/de/net/workbook-operations/update-power-query-formula-item/"
"weight": 27
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aktualisieren des Power Query-Formelelements in der Arbeitsmappe

## Einführung
Für jeden Datenanalysten und Excel-Enthusiasten ist es wichtig zu wissen, wie man Daten mit Power Query in Excel effizient verwaltet. Wenn Sie schon einmal die Formelelemente in Ihrer Power Query-Arbeitsmappe aktualisieren mussten, sind Sie hier richtig. Diese Anleitung zeigt Ihnen, wie Sie mit Aspose.Cells für .NET Power Query-Formeln in einer Excel-Arbeitsmappe nahtlos aktualisieren. Mit wenigen Schritten können Sie Ihre Daten bearbeiten und optimieren und so sicherstellen, dass Ihre Arbeitsmappen dynamisch und zentralisiert bleiben.
## Voraussetzungen
Bevor Sie sich in den Beispielcode und die Schritte vertiefen, gehen wir durch, was Sie benötigen:
1. Grundlegende Kenntnisse in C# und .NET: Da wir Code schreiben werden, ist es von Vorteil, mit den Programmierkonzepten in C# vertraut zu sein.
2. Installieren Sie Aspose.Cells für .NET: Sie benötigen die Aspose.Cells-Bibliothek in Ihrem .NET-Projekt. Sie können sie herunterladen [Hier](https://releases.aspose.com/cells/net/).
3. Eine Excel-Datei, die zur Bearbeitung bereit ist: Stellen Sie sicher, dass Sie eine Excel-Datei haben, die eine Power Query enthält, die Sie aktualisieren möchten. Sie benötigen eine Beispielarbeitsmappe wie `SamplePowerQueryFormula.xlsx` zu Ihrer Verfügung.
## Pakete importieren
Stellen Sie zunächst sicher, dass Ihre C#-Datei die folgenden Namespaces enthält:
```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```
Dadurch können Sie auf die von der Aspose.Cells-Bibliothek bereitgestellten Funktionen zugreifen, insbesondere für die Arbeit mit Arbeitsmappen und Power Query-Daten.
## Schritt 1: Richten Sie Ihre Arbeitsverzeichnisse ein
Als Erstes müssen Sie definieren, wo sich Ihre Quell- und Ausgabedateien befinden. 
```csharp
string SourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
```
In diesem Schritt geben Sie die Verzeichnispfade an. Ersetzen Sie `"Your Document Directory"` mit dem tatsächlichen Pfad, in dem Ihre Excel-Dateien gespeichert sind. Dadurch teilt das Programm mit, wo es nach Ihrer Quelldatei suchen und die aktualisierte Datei speichern soll.
## Schritt 2: Laden Sie die Arbeitsmappe
Nachdem Sie Ihre Arbeitsverzeichnisse festgelegt haben, besteht der nächste Schritt darin, Ihre Excel-Datei in das Programm zu laden.
```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
Hier erstellen Sie eine `Workbook` Objekt, das die angegebene Excel-Datei lädt. Das `Workbook` Die Klasse ist Teil der Aspose.Cells-Bibliothek und für alle Vorgänge, die Sie an dieser Excel-Datei durchführen, unerlässlich.
## Schritt 3: Zugriff auf die Power Query-Daten
Sobald die Arbeitsmappe geladen ist, können Sie auf die darin gespeicherten Power Query-Formeln zugreifen.
```csharp
DataMashup mashupData = workbook.DataMashup;
```
In dieser Zeile `DataMashup` Die Eigenschaft erleichtert den Zugriff auf die Power Query-Datenstrukturen in der Arbeitsmappe. Diese Eigenschaft ermöglicht Ihnen die Interaktion mit verschiedenen Aspekten der Power Query-Daten in Ihrer Excel-Datei.
## Schritt 4: Durchlaufen der Power Query-Formeln
Wenn die Power Query-Daten zugänglich sind, besteht der nächste Schritt darin, jede der vorhandenen Formeln zu durchlaufen.
```csharp
foreach (PowerQueryFormula formula in mashupData.PowerQueryFormulas)
{
    foreach (PowerQueryFormulaItem item in formula.PowerQueryFormulaItems)
    {
        if (item.Name == "Source")
        {
            item.Value = "Excel.Workbook(File.Contents(\"" + SourceDir + "SamplePowerQueryFormulaSource.xlsx\"), null, true)";
        }
    }
}
```
Hier geschieht die Magie. Wir durchlaufen jeden `PowerQueryFormula` und dann durch jeden `PowerQueryFormulaItem`. Der `if` Anweisung sucht nach dem Formelelement mit dem Namen „Quelle“ und aktualisiert seinen Wert so, dass er dem Pfad der Quelldatei entspricht, auf die Power Query verweisen soll. Auf diese Weise können Sie dynamisch ändern, aus welcher Datei Power Query Daten abruft.
## Schritt 5: Speichern der aktualisierten Arbeitsmappe
Nachdem Sie die erforderlichen Formelelemente aktualisiert haben, besteht Ihr letzter Schritt darin, die Arbeitsmappe zu speichern.
```csharp
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
```
Diese Zeile speichert die geänderte Arbeitsmappe in einer neuen Datei. Dadurch bleibt das Original erhalten, während Sie mit der aktualisierten Version arbeiten können.
## Schritt 6: Bestätigungsnachricht
Schließlich empfiehlt es sich, zu überprüfen, ob Ihr Code ordnungsgemäß ausgeführt wurde.
```csharp
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
Diese einfache Meldung bestätigt Ihnen in der Konsole, dass Ihr Vorgang erfolgreich war, und sorgt für einen beruhigenden Abschluss des Vorgangs.
## Abschluss
Und fertig! Das Aktualisieren von Power Query-Formelelementen in Excel mit Aspose.Cells für .NET ist in wenigen Schritten erledigt. Mit dieser Anleitung verwalten Sie Ihre Excel-Datenverbindungen effizient und sorgen für einen reibungslosen Ablauf Ihrer Arbeitsmappen. Egal, ob Sie ein erfahrener Profi sind oder gerade erst mit der Datenmanipulation beginnen – Aspose.Cells bietet eine leistungsstarke Möglichkeit zur Automatisierung und Optimierung von Excel-Workflows. 
## Häufig gestellte Fragen
### Kann ich Aspose.Cells mit jeder Version von .NET verwenden?
Aspose.Cells ist mit mehreren Versionen von .NET kompatibel, einschließlich .NET Framework und .NET Core.
### Ist die Nutzung von Aspose.Cells kostenlos?
Aspose.Cells bietet eine kostenlose Testversion an, für die dauerhafte Nutzung ist jedoch eine Lizenz erforderlich. Sie können eine temporäre Lizenz erhalten [Hier](https://purchase.aspose.com/temporary-license/).
### Was ist, wenn meine vorhandene Excel-Datei nicht über Power Query verfügt?
Der beschriebene Prozess konzentriert sich auf die Aktualisierung von Power Query-Elementen. Wenn diese also in Ihrer Datei fehlen, müssen Sie zuerst Power Querys integrieren.
### Wo finde ich weitere Informationen zu Aspose.Cells?
In der Dokumentation finden Sie umfassende Anleitungen und Beispiele. Besuchen Sie die [Dokumentation](https://reference.aspose.com/cells/net/).
### Wie melde ich Fehler oder Probleme mit Aspose.Cells?
Sie können sich an das Support-Forum wenden, um Hilfe bei allen auftretenden Problemen zu erhalten.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}