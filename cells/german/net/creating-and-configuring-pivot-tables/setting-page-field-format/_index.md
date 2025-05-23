---
"description": "Erfahren Sie, wie Sie Seitenfeldformate in PivotTables programmgesteuert mit Aspose.Cells für .NET festlegen. Folgen Sie unserem Schritt-für-Schritt-Tutorial für nahtloses Datenmanagement."
"linktitle": "Programmgesteuertes Festlegen des Seitenfeldformats in .NET"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Programmgesteuertes Festlegen des Seitenfeldformats in .NET"
"url": "/de/net/creating-and-configuring-pivot-tables/setting-page-field-format/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Programmgesteuertes Festlegen des Seitenfeldformats in .NET

## Einführung
Das Erstellen und Bearbeiten von Excel-Dateien mithilfe von Code kann besonders hilfreich sein, insbesondere bei der Analyse großer Datensätze. Eines der besten Tools in Ihrem Arsenal ist Aspose.Cells für .NET. Damit können Sie programmgesteuert mit Excel-Dateien interagieren und komplexe Berichtsstrukturen erstellen. In diesem Tutorial erfahren Sie, wie Sie mit dieser leistungsstarken Bibliothek Seitenfeldformate in einer PivotTable einrichten. Egal, ob Sie erfahrener Entwickler oder Anfänger sind – am Ende dieses Leitfadens haben Sie ein gutes Verständnis für die Arbeit mit PivotTables und ihren verschiedenen Einstellungen in .NET.
## Voraussetzungen
Bevor wir uns kopfüber in die Programmierung stürzen, stellen wir sicher, dass alles richtig eingerichtet ist. Folgendes benötigen Sie:
- Visual Studio: Eine Arbeitsumgebung, in der Sie Ihren .NET-Code schreiben und ausführen können.
- Aspose.Cells: Sie können die Bibliothek herunterladen [Hier](https://releases.aspose.com/cells/net/).
- Grundkenntnisse in C#: Wenn Sie mit der C#-Programmierung vertraut sind, können Sie die Codeausschnitte besser verstehen.
- Excel-Datei: Halten Sie eine Excel-Datei bereit (z. B. `Book1.xls`) mit Daten, die für die Erstellung einer PivotTable geeignet sind. 
Falls Sie es noch nicht getan haben, holen Sie sich Ihre kostenlose Testversion von Aspose.Cells [Hier](https://releases.aspose.com/).
## Pakete importieren
Um loszulegen, müssen Sie die richtigen Pakete in Ihr Projekt importieren. Fügen Sie zunächst Verweise auf die Aspose.Cells-Bibliothek in Ihrem C#-Projekt hinzu. So geht's:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Dadurch werden alle erforderlichen Klassen und Methoden einbezogen, die zum Bearbeiten von Excel-Dateien mit Aspose.Cells erforderlich sind.
## Schritt 1: Richten Sie Ihren Arbeitsbereich ein
Definieren Sie zunächst Ihr Arbeitsverzeichnis, in dem Ihre Excel-Dateien gespeichert werden. Sie können beispielsweise eine Variable wie folgt deklarieren:
```csharp
string dataDir = "Your Document Directory";
```
## Laden der Arbeitsmappe
Als Nächstes müssen wir unsere Excel-Vorlage laden. Dies ist ein wichtiger Schritt, da er den Kontext für unsere Operationen festlegt:
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Diese Zeile lädt die vorhandene Arbeitsmappe aus dem angegebenen Verzeichnis.
## Schritt 2: Zugriff auf das Arbeitsblatt
Sobald Ihre Arbeitsmappe geladen ist, können Sie auf das Arbeitsblatt mit der PivotTable oder den zu analysierenden Daten zugreifen. So geht's:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Dadurch wird das erste Arbeitsblatt der geladenen Arbeitsmappe abgerufen. Sie können den Index problemlos ändern, wenn Sie mit mehreren Blättern arbeiten.
## Schritt 3: Zugriff auf die PivotTable
Im Folgenden greifen wir auf die PivotTable im ausgewählten Arbeitsblatt zu. Wenn Sie eine einzelne PivotTable verwenden, können Sie deren Index auf `0`:
```csharp
int pivotindex = 0;
// Zugriff auf die PivotTable
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
Dieser Codeausschnitt wählt die erste PivotTable im Arbeitsblatt aus. 
## Schritt 4: Konfigurieren der PivotTable
Jetzt kommt der spannende Teil! Richten wir die PivotTable so ein, dass die Gesamtsummen für die Zeilen angezeigt werden:
```csharp
pivotTable.RowGrand = true;
```
Diese Zeile stellt sicher, dass Ihr Bericht Gesamtsummen anzeigt, die eine nützliche Zusammenfassung für die Datenanalyse sein können.
## Schritt 5: Auf Zeilenfelder zugreifen und diese konfigurieren
Als nächstes müssen wir auf die Zeilenfelder der PivotTable zugreifen:
```csharp
Aspose.Cells.Pivot.PivotFieldCollection pivotFields = pivotTable.RowFields;
```
Diese Sammlung ermöglicht es uns, die Felder nach Bedarf zu bearbeiten.
## Konfigurieren des Felds „Erste Zeile“
Möchten Sie bestimmte Zwischensummentypen festlegen? Greifen wir auf das erste Feld in unserer Sammlung zu und konfigurieren es:
```csharp
Aspose.Cells.Pivot.PivotField pivotField = pivotFields[0];
// Festlegen von Zwischensummen.
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Sum, true);
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Count, true);
```
Durch die Aktivierung `Sum` Und `Count` Zwischensummen können wir Daten schnell in unserem Bericht zusammenfassen.
## Schritt 6: Festlegen der Autosort-Optionen
Als Nächstes wenden wir eine intelligente Sortierung an. Auf diese Weise ordnet Ihre PivotTable die Daten in einer sinnvollen Reihenfolge an:
```csharp
// Festlegen von Autosortieroptionen.
pivotField.IsAutoSort = true;
pivotField.IsAscendSort = true;
pivotField.AutoSortField = -5; // Verwenden eines vordefinierten Sortierfelds.
```
Dieser Codeausschnitt ermöglicht die automatische Sortierung und gibt die aufsteigende Reihenfolge vor. 
## Schritt 7: AutoShow-Optionen festlegen
Möchten Sie Ihre Daten weiter filtern? Die AutoShow-Option ist hilfreich, um bestimmte Datenpunkte unter definierten Bedingungen anzuzeigen:
```csharp
// Festlegen der AutoShow-Optionen.
pivotField.IsAutoShow = true;
pivotField.IsAscendShow = false;
pivotField.AutoShowField = 0; // Geben Sie das Feld an, das automatisch angezeigt werden soll.
```
Dadurch wird sichergestellt, dass in Ihrer PivotTable nur relevante Daten angezeigt werden, was für mehr Übersichtlichkeit und Fokus sorgt.
## Schritt 8: Speichern Ihrer Arbeit
Nach all diesen Konfigurationen möchten Sie Ihre Arbeit nicht verlieren! Speichern Sie die geänderte Arbeitsmappe wie folgt:
```csharp
workbook.Save(dataDir + "output.xls");
```
Jetzt finden Sie die neu erstellte Excel-Datei in Ihrem Dokumentverzeichnis.
## Abschluss
Und da haben Sie es! Wir haben einen umfassenden und praktischen Ansatz zum programmgesteuerten Festlegen von Seitenfeldformaten in einer PivotTable mit Aspose.Cells für .NET vorgestellt. Mit den einfachen Schritten können Sie Ihre Excel-Daten sicher an Ihre Berichtsanforderungen anpassen. Es ist unglaublich, was Sie erreichen können, wenn Sie die Leistung von C# mit Aspose.Cells kombinieren.
## Häufig gestellte Fragen
### Was ist Aspose.Cells?
Aspose.Cells ist eine .NET-Bibliothek, mit der Entwickler Excel-Dateien programmgesteuert erstellen, bearbeiten und konvertieren können.
### Wie installiere ich Aspose.Cells?
Sie können es direkt herunterladen von der [Aspose-Website](https://releases.aspose.com/cells/net/).
### Kann ich Aspose.Cells ohne eine Excel-Installation verwenden?
Ja, Aspose.Cells ist eine eigenständige Bibliothek, für die keine Installation von Microsoft Excel erforderlich ist.
### Wo finde ich detaillierte Unterstützung?
Detaillierten Support und Foren finden Sie unter [Aspose-Unterstützung](https://forum.aspose.com/c/cells/9).
### Wie kann ich eine vorläufige Lizenz erhalten?
Eine temporäre Lizenz erhalten Sie bei [Hier](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}