---
"description": "Erfahren Sie in unserer Schritt-für-Schritt-Anleitung, wie Sie mit Aspose.Cells programmgesteuert eine Pivot-Tabelle in .NET erstellen. Analysieren Sie Ihre Daten effizient."
"linktitle": "Erstellen Sie programmgesteuert eine neue Pivot-Tabelle in .NET"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Erstellen Sie programmgesteuert eine neue Pivot-Tabelle in .NET"
"url": "/de/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Erstellen Sie programmgesteuert eine neue Pivot-Tabelle in .NET

## Einführung
Das Erstellen einer Pivot-Tabelle kann eine anspruchsvolle Aufgabe sein, insbesondere wenn Sie es programmgesteuert tun. Aber keine Angst! Mit Aspose.Cells für .NET ist das Erstellen einer Pivot-Tabelle nicht nur unkompliziert, sondern auch äußerst leistungsstark für die Datenanalyse. In diesem Tutorial führen wir Sie Schritt für Schritt durch die Erstellung einer neuen Pivot-Tabelle in einer .NET-Anwendung. Egal, ob Sie Daten für Verkäufe, Sport oder andere Geschäftskennzahlen hinzufügen – mit dieser Anleitung sind Ihre Pivot-Tabellen im Handumdrehen einsatzbereit.

## Voraussetzungen
Bevor wir loslegen, stellen wir sicher, dass alles bereit ist. Folgendes müssen Sie tun:

1. Installieren Sie .NET Framework: Stellen Sie sicher, dass das .NET Framework auf Ihrem Computer installiert ist. Aspose.Cells unterstützt verschiedene Versionen, es ist jedoch ratsam, die neueste Version zu verwenden.
2. Aspose.Cells Bibliothek: Sie benötigen die Aspose.Cells Bibliothek. Sie können [Laden Sie es hier herunter](https://releases.aspose.com/cells/net/) oder erhalten Sie eine [vorläufige Lizenz](https://purchase.aspose.com/temporary-license/) zur Auswertung.
3. IDE-Setup: Halten Sie eine C#-kompatible IDE wie Visual Studio bereit, in der Sie ein neues Projekt starten können.
4. Grundkenntnisse in C#: Wenn Sie mit der C#-Programmierung vertraut sind, können Sie den Anweisungen folgen, ohne zu sehr ins Stocken zu geraten.

Sind Sie bereit? Super! Jetzt können wir mit dem Importieren der erforderlichen Pakete beginnen.

## Pakete importieren
Als Erstes müssen Sie die benötigten Namespaces in Ihr C#-Projekt importieren. Öffnen Sie Ihre C#-Datei und fügen Sie die folgenden using-Direktiven hinzu:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Diese Namespaces bieten Ihnen Zugriff auf die Arbeitsmappen-, Arbeitsblatt- und Pivot-Tabellenfunktionen, die wir in diesem Lernprogramm verwenden werden.

## Schritt 1: Erstellen Sie ein Arbeitsmappenobjekt
Das Erstellen einer Arbeitsmappe ist der Anfang Ihrer Reise. Beginnen wir mit der Instanziierung einer neuen Arbeitsmappe und dem Zugriff auf das erste Arbeitsblatt.

```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "Your Document Directory";
// Instanziieren eines Workbook-Objekts
Workbook workbook = new Workbook();

// Abrufen der Referenz des neu hinzugefügten Arbeitsblatts
Worksheet sheet = workbook.Worksheets[0];
```

In diesem Schritt erstellen wir eine `Workbook` Instanz, die unsere Excel-Datei darstellt, und greifen Sie auf das allererste Arbeitsblatt zu, das unser Spielplatz für die Pivot-Tabelle sein wird.

## Schritt 2: Daten in Zellen einfügen
Als Nächstes füllen wir unser Arbeitsblatt mit Beispieldaten. Wir fügen Zeilen für verschiedene Sportarten, Quartale und Umsatzzahlen ein, um unserer Pivot-Tabelle eine Zusammenfassung zu geben.

```csharp
Cells cells = sheet.Cells;

// Festlegen des Wertes für die Zellen
Cell cell = cells["A1"];
cell.PutValue("Sport");
cell = cells["B1"];
cell.PutValue("Quarter");
cell = cells["C1"];
cell.PutValue("Sales");

// Datenzelle füllen = Zellen["A2"];
cell.PutValue("Golf");
// ... Weitere Dateneinträge
```

Hier definieren wir unsere Spaltenüberschriften und fügen unter jeder Überschrift Werte ein. Diese Daten dienen als Quelle für unsere Pivot-Tabelle. Achten Sie daher auf eine gute Organisation! Folgen Sie diesem Block, um einen umfassenden Datensatz zu erstellen.

## Schritt 3: Hinzufügen einer Pivot-Tabelle
Nachdem unsere Daten bereit sind, können wir die Pivot-Tabelle erstellen. Wir verwenden die Pivot-Tabellensammlung aus dem Arbeitsblatt, um unsere neue Pivot-Tabelle hinzuzufügen.

```csharp
Aspose.Cells.Pivot.PivotTableCollection pivotTables = sheet.PivotTables;

// Hinzufügen einer PivotTable zum Arbeitsblatt
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```

In diesem Codeausschnitt fügen wir dem Arbeitsblatt eine Pivot-Tabelle hinzu, die auf unseren Datenbereich (in diesem Fall die Zellen A1 bis C8) verweist. Wir platzieren die Pivot-Tabelle beginnend bei Zelle E3 und nennen sie „PivotTable2“. Ziemlich einfach, oder?

## Schritt 4: Anpassen der Pivot-Tabelle
Nachdem wir unsere Pivot-Tabelle erstellt haben, können wir sie anpassen, um aussagekräftige Zusammenfassungen anzuzeigen. Wir können steuern, was in den Zeilen, Spalten und Datenbereichen der Pivot-Tabelle angezeigt wird.

```csharp
// Zugriff auf die Instanz der neu hinzugefügten PivotTable
Aspose.Cells.Pivot.PivotTable pivotTable = pivotTables[index];

// Gesamtsummen für Zeilen werden nicht angezeigt.
pivotTable.RowGrand = false;

// Ziehen Sie das erste Feld in den Zeilenbereich.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Row, 0);

// Ziehen Sie das zweite Feld in den Spaltenbereich.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Column, 1);

// Ziehen Sie das dritte Feld in den Datenbereich.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Data, 2);
```

In diesem Schritt weisen wir die Pivot-Tabelle an, Gesamtsummen für Zeilen auszublenden. Anschließend legen wir fest, welche Felder in die Zeilen-, Spalten- und Datenbereiche aufgenommen werden sollen. Die Sportnamen füllen die Zeilen, die Quartale die Spalten und die Verkaufszahlen die Zusammenfassungen.

## Schritt 5: Speichern der Arbeitsmappe
Abschließend möchten wir unsere neu erstellte Arbeitsmappe speichern, um die Früchte unserer Arbeit zu sehen.

```csharp
// Speichern der Excel-Datei
workbook.Save(dataDir + "pivotTable_test_out.xls");
```

Geben Sie einfach einen entsprechenden Pfad an, und die Ausgabe Ihrer Pivot-Tabelle wird in einer Excel-Datei gespeichert, die Sie öffnen und überprüfen können.

## Abschluss
Das programmgesteuerte Erstellen von Pivot-Tabellen mit Aspose.Cells für .NET kann Ihnen erheblich Zeit sparen, insbesondere bei großen Datensätzen. Sie haben gelernt, wie Sie Ihr Projekt einrichten, notwendige Pakete importieren, Daten einpflegen und eine anpassbare Pivot-Tabelle von Grund auf neu erstellen. Wenn Sie also das nächste Mal in Zahlen ertrinken, denken Sie an dieses Tutorial und überlassen Sie Aspose.Cells die Arbeit.

## Häufig gestellte Fragen
### Was ist Aspose.Cells?
Aspose.Cells ist eine leistungsstarke .NET-Bibliothek zum programmgesteuerten Erstellen und Verwalten von Excel-Tabellen.

### Gibt es eine kostenlose Testversion für Aspose.Cells?
Ja, Sie können eine kostenlose Testversion erhalten [Hier](https://releases.aspose.com/).

### Kann ich das Erscheinungsbild der Pivot-Tabelle anpassen?
Absolut! Sie können Formatierung, Layout und sogar Stile der Pivot-Tabelle nach Ihren Wünschen anpassen.

### Wo finde ich weitere Beispiele und Dokumentation zu Aspose.Cells?
Sie können die [Dokumentation](https://reference.aspose.com/cells/net/) für umfassende Anleitungen und Beispiele.

### Wie erhalte ich Support für Aspose.Cells?
Unterstützung erhalten Sie durch die [Aspose-Forum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}