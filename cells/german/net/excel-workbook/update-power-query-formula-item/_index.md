---
title: Aktualisieren des Power Query-Formelelements
linktitle: Aktualisieren des Power Query-Formelelements
second_title: Aspose.Cells für .NET API-Referenz
description: Aktualisieren Sie Power Query-Formelelemente in Excel ganz einfach mit Aspose.Cells für .NET. Schritt-für-Schritt-Anleitung zur Optimierung Ihrer Datenbearbeitungsprozesse.
weight: 160
url: /de/net/excel-workbook/update-power-query-formula-item/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aktualisieren des Power Query-Formelelements

## Einführung

Wenn Sie schon einmal mit Excel gearbeitet haben, wissen Sie, wie leistungsstark es sein kann – insbesondere, wenn Sie sich mit Power Queries beschäftigen. Diese sind das Geheimrezept, mit dem Sie Ihre Daten mühelos transformieren, bereinigen und analysieren können. Eine raffinierte Möglichkeit, Ihre Power Query-Formeln in Excel zu bearbeiten, ist Aspose.Cells für .NET. Heute führen wir Sie Schritt für Schritt durch die Aktualisierung von Power Query-Formelelementen. Also, schnappen Sie sich Ihren Programmierhut und legen Sie los!

## Voraussetzungen

Bevor Sie sich in den Code vertiefen, sollten Sie einige Dinge eingerichtet haben:

1. Visual Studio: Sie benötigen eine integrierte Entwicklungsumgebung (IDE), um Ihren .NET-Code zu schreiben und auszuführen. Visual Studio ist die erste Wahl.
2.  Aspose.Cells-Bibliothek: Stellen Sie sicher, dass die Aspose.Cells-Bibliothek in Ihrem Projekt verfügbar ist. Sie können sie von der[Website](https://releases.aspose.com/cells/net/).
3. Grundkenntnisse in C#: Wir werden dies gemeinsam durchgehen, aber gewisse Grundkenntnisse in C# sind sicherlich hilfreich, insbesondere bei der Navigation durch die verschiedenen Klassen und Methoden.
4. Beispiel-Excel-Dateien: Sie benötigen die im Codeausschnitt genannten Excel-Dateien. Stellen Sie sicher, dass Sie über Folgendes verfügen:
   - `SamplePowerQueryFormula.xlsx`
   - `SamplePowerQueryFormulaSource.xlsx`

5. .NET Framework: Stellen Sie sicher, dass Ihr Projekt auf eine kompatible Version des .NET Frameworks abzielt.

Nun, da unser Kit bereit ist, können wir mit dem spaßigen Teil fortfahren: dem Schreiben von Code!

## Pakete importieren

Zunächst müssen Sie die erforderlichen Namespaces importieren. So geht's:

```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```

Indem Sie diese Namespaces hinzufügen, teilen Sie dem Compiler mit, dass Sie die Klassen und Methoden aus der Aspose.Cells-Bibliothek verwenden möchten. Dieser Schritt ist entscheidend, da er die Grundlage für den folgenden Code legt.

Lassen Sie uns den von Ihnen bereitgestellten Codeausschnitt aufschlüsseln. Dieses Tutorial führt Sie durch jeden Teil und stellt sicher, dass Sie verstehen, was passiert.

## Schritt 1: Arbeitsverzeichnisse einrichten

In diesem Schritt definieren wir, wo sich unsere Quell- und Ausgabedateien befinden. Dadurch wird sichergestellt, dass Aspose weiß, wo es nach Ihren Excel-Dateien suchen muss.

```csharp
// Arbeitsverzeichnisse
string SourceDir = "Your Document Directory";
string outputDir = "Your Output Directory";
```

## Schritt 2: Laden Sie die Arbeitsmappe

Laden wir jetzt die Excel-Datei, in der sich die Power Query befindet.

```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
 Der`Workbook` Klasse ist Ihr Einstiegspunkt in die Excel-Datei. Indem wir den Pfad unserer Quelldatei übergeben, erstellen wir eine Instanz, die es uns ermöglicht, sie zu bearbeiten. Sie können es sich wie das Öffnen eines Buches vorstellen – Sie bereiten sich darauf vor, seinen Inhalt zu lesen (oder zu bearbeiten).

## Schritt 3: Zugriff auf das Daten-Mashup

Als Nächstes greifen wir auf die Power Query-Formeln zu, die im Data Mashup der Arbeitsmappe gespeichert sind.

```csharp
DataMashup mashupData = workbook.DataMashup;
```
 Der`DataMashup` Die Klasse enthält alle Power Query-Formeln, die mit Ihrer Arbeitsmappe verknüpft sind. Hier erledigen wir die Schwerstarbeit, ähnlich wie wenn Sie einen Werkzeugkasten für Reparaturen öffnen.

## Schritt 4: Durchlaufen der Power Query-Formeln

Jetzt kommt der Teil, in dem wir die Power Query-Formeln durchlaufen, um die spezifische Formel zu finden, die wir aktualisieren möchten.

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

-  Wir durchlaufen jede`PowerQueryFormula` In`mashupData`.
- Innerhalb dieser Schleife tauchen wir in jeden`PowerQueryFormulaItem`.
- Wir prüfen, ob der Name des Elements mit „Quelle“ übereinstimmt. Wenn dies der Fall ist, aktualisieren wir seinen Wert, um eine Verknüpfung zu unserer neuen Quelldatei herzustellen.

Dies ist vergleichbar mit dem Suchen der richtigen Seite in einem Handbuch und dem anschließenden Vornehmen der erforderlichen Aktualisierungen – es ist ein unkomplizierter und sorgfältiger Vorgang.

## Schritt 5: Speichern der aktualisierten Arbeitsmappe

Nachdem wir die Aktualisierungen vorgenommen haben, ist es Zeit, unsere Änderungen zu speichern.

```csharp
// Speichern Sie die Ausgabearbeitsmappe.
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
 Der`Save` Die Methode schreibt die aktualisierte Arbeitsmappe in das angegebene Ausgabeverzeichnis. Das ist, als würden Sie Ihre Änderungen in einer neuen Version des Handbuchs versiegeln, die für andere bereit ist!

## Abschluss

Herzlichen Glückwunsch! Sie haben ein Power Query-Formelelement erfolgreich mit Aspose.Cells für .NET aktualisiert. Mit dieser Methode können Sie die Änderung von Power Query-Formeln in Ihren Excel-Dateien automatisieren und so wertvolle Zeit und Mühe sparen.

## Häufig gestellte Fragen

### Was ist Aspose.Cells?
Aspose.Cells ist eine leistungsstarke Bibliothek zum Bearbeiten von Excel-Dateien in .NET-Anwendungen, ohne dass Microsoft Excel installiert sein muss.

### Benötige ich Microsoft Excel, um Aspose.Cells auszuführen?
Nein, mit Aspose.Cells können Sie Excel-Dateien programmgesteuert erstellen und bearbeiten, ohne dass Excel auf Ihrem Server oder Entwicklungscomputer erforderlich ist.

### Mit welchen Excel-Dateitypen kann ich mit Aspose.Cells arbeiten?
Mit Aspose.Cells können Sie mit .xlsx, .xls, .xlsm und mehreren anderen Excel-Formaten arbeiten.

### Gibt es eine Testversion für Aspose.Cells?
 Ja, Sie können eine kostenlose Testversion herunterladen von der[Aspose Cells-Veröffentlichungsseite](https://releases.aspose.com/).

### Wie kann ich Support für Aspose.Cells erhalten?
 Sie erhalten Support über das[Aspose-Forum](https://forum.aspose.com/c/cells/9), wo Sie Fragen stellen und Antworten von der Community und dem Aspose-Team erhalten können.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
