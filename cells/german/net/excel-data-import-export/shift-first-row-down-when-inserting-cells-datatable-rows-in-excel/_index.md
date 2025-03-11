---
title: Beim Einfügen von DataTable-Zeilen in Excel die erste Zeile nach unten verschieben
linktitle: Beim Einfügen von DataTable-Zeilen in Excel die erste Zeile nach unten verschieben
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie mit Aspose.Cells für .NET DataTable-Zeilen in Excel einfügen, ohne die erste Zeile nach unten zu verschieben. Schritt-für-Schritt-Anleitung für mühelose Automatisierung.
weight: 11
url: /de/net/excel-data-import-export/shift-first-row-down-when-inserting-cells-datatable-rows-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Beim Einfügen von DataTable-Zeilen in Excel die erste Zeile nach unten verschieben

## Einführung

Sind Sie es leid, beim Einfügen neuer Daten in Ihre Excel-Tabellen Zeilen manuell zu verschieben? Dann haben Sie Glück! In diesem Artikel erfahren Sie, wie Sie diesen Prozess mit Aspose.Cells für .NET automatisieren können. Am Ende dieses Tutorials lernen Sie nicht nur, wie Sie mit Datentabellen in Excel arbeiten, sondern auch, wie Sie die Importoptionen an Ihre Bedürfnisse anpassen. Vertrauen Sie mir; das kann Ihnen viel Zeit und Ärger ersparen! Also, holen Sie sich eine Tasse Kaffee und legen Sie los!

## Voraussetzungen

Bevor wir mit der Codierung beginnen, stellen wir sicher, dass Sie alles eingerichtet haben:

1. Visual Studio: Stellen Sie sicher, dass Sie Visual Studio installiert haben (2017 oder höher sollte problemlos funktionieren).
2.  Aspose.Cells für .NET: Sie benötigen die Aspose.Cells-Bibliothek. Wenn Sie dies noch nicht getan haben, können Sie es herunterladen[Hier](https://releases.aspose.com/cells/net/).
3. Grundlegende Kenntnisse in C# und Excel: Grundkenntnisse in der C#-Programmierung und der Funktionsweise von Excel helfen Ihnen sicherlich dabei, den Schritten besser zu folgen.

 Sie sollten auch eine Excel-Beispieldatei zur Hand haben. In dieser Anleitung verwenden wir ein Beispiel namens`sampleImportTableOptionsShiftFirstRowDown.xlsx`. Sie können diese Datei erstellen oder eine Vorlage finden, die Ihren Anforderungen entspricht.

## Pakete importieren

Bevor wir mit dem Programmieren beginnen, müssen wir sicherstellen, dass wir die erforderlichen Pakete importieren. Schließen Sie in Ihr C#-Projekt die folgenden Namespaces ein:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Diese Pakete sind für die Arbeit mit Arbeitsmappen, Arbeitsblättern und Tabellen unverzichtbar.

## Schritt 1: Richten Sie Ihr Projekt ein

### Erstellen eines neuen C#-Projekts

Beginnen Sie mit der Erstellung einer neuen C#-Konsolenanwendung in Visual Studio. Geben Sie Ihrem Projekt einen passenden Namen, beispielsweise „ExcelDataImport“.

### Aspose.Cells NuGet-Paket hinzufügen

Um das Aspose.Cells-Paket hinzuzufügen, klicken Sie im Solution Explorer mit der rechten Maustaste auf Ihr Projekt, wählen Sie „NuGet-Pakete verwalten“ und suchen Sie nach „Aspose.Cells“. Installieren Sie das Paket, um sicherzustellen, dass Sie auf alle benötigten Funktionen zugreifen können.

## Schritt 2: Definieren Sie die Datentabelle

 Als nächstes implementieren wir die`ICellsDataTable` Schnittstelle, um eine Klasse zu erstellen, die die zu importierenden Daten bereitstellt. So können Sie die`CellsDataTable` Klasse:

```csharp
class CellsDataTable : ICellsDataTable
{
    int m_index = -1;
    static String[] colsNames = new String[] { "Pet", "Fruit", "Country", "Color" };
    static String[] col0data = new String[] { "Dog", "Cat", "Duck" };
    static String[] col1data = new String[] { "Apple", "Pear", "Banana" };
    static String[] col2data = new String[] { "UK", "USA", "China" };
    static String[] col3data = new String[] { "Red", "Green", "Blue" };
    static String[][] colsData = new String[][] { col0data, col1data, col2data, col3data };
    
    // ... andere Mitglieder implementieren ...
}
```

Hier definieren wir die Spaltennamen und die Daten für jede Spalte, was die Struktur unserer importierten Tabelle erleichtert.

## Schritt 3: Implementieren von ICellsDataTable-Schnittstellenmitgliedern

 Innerhalb der`CellsDataTable` Klasse müssen Sie die Mitglieder der`ICellsDataTable` Schnittstelle. Hier ist die erforderliche Implementierung:

```csharp
public object this[string columnName]
{
    get
    {
        throw new NotImplementedException();
    }
}

object ICellsDataTable.this[int columnIndex]
{
    get
    {
        return colsData[columnIndex][m_index];
    }
}

string[] ICellsDataTable.Columns
{
    get { return colsNames; }
}

int ICellsDataTable.Count
{
    get { return col0data.Length; }
}

void ICellsDataTable.BeforeFirst()
{
    m_index = -1;
}

bool ICellsDataTable.Next()
{
    m_index++;
    return (m_index < Count);
}
```

Dieser Teil der Klasse kümmert sich um den Datenabruf, definiert, wie viele Zeilen und Spalten vorhanden sind, und verwaltet den aktuellen Indexstatus.

## Schritt 4: Schreiben Sie die Hauptfunktion

 Erstellen wir nun die`Run`Methode zum Orchestrieren des gesamten Tabellenimportprozesses:

```csharp
public static void Run()
{
    string sourceDir = "Your Document Directory\\";
    string outputDir = "Your Document Directory\\";
    
    CellsDataTable cellsDataTable = new CellsDataTable();
    Workbook wb = new Workbook(sourceDir + "sampleImportTableOptionsShiftFirstRowDown.xlsx");
    Worksheet ws = wb.Worksheets[0];
```

## Schritt 5: Importoptionen festlegen

 Um das Importverhalten zu steuern, sollten Sie eine Instanz von`ImportTableOptions` und legen Sie die Eigenschaften entsprechend fest. Konkret möchten wir festlegen`ShiftFirstRowDown` Zu`false`.

```csharp
    ImportTableOptions opts = new ImportTableOptions();
    opts.ShiftFirstRowDown = false; // Wir wollen die erste Reihe nicht nach unten verschieben
```

## Schritt 6: Importieren der DataTable

 Nun können wir die Daten aus unserem`CellsDataTable` in das Arbeitsblatt.

```csharp
    ws.Cells.ImportData(cellsDataTable, 2, 2, opts);
}
```

Dieser Befehl fügt Ihre Datentabelle direkt ab der angegebenen Zeile und Spalte ein.

## Schritt 7: Speichern Sie die Arbeitsmappe

Abschließend speichern wir die geänderte Arbeitsmappe wieder in einer Datei:

```csharp
    wb.Save(outputDir + "outputImportTableOptionsShiftFirstRowDown-False.xlsx");
}
```

## Abschluss

Und da haben Sie es! Sie haben gelernt, wie Sie mit Aspose.Cells für .NET DataTable-Zeilen in ein Excel-Blatt einfügen, ohne die erste Zeile zu verschieben. Dieser Prozess rationalisiert nicht nur die Datenmanipulation in Excel, sondern verbessert auch die Leistung Ihrer Anwendung, indem er eine normalerweise mühsame Aufgabe automatisiert. Mit diesem Wissen in Ihrem Toolkit sind Sie besser für die Bewältigung von Excel-Automatisierungsaufgaben gerüstet und sparen Zeit und Mühe.

## Häufig gestellte Fragen

### Was ist Aspose.Cells für .NET?
Aspose.Cells für .NET ist eine Programmierbibliothek, mit der Entwickler Excel-Dateien in .NET-Anwendungen erstellen, bearbeiten und konvertieren können.

### Benötige ich eine Lizenz, um Aspose.Cells zu verwenden?
Ja, für den vollen Funktionsumfang benötigen Sie eine gültige Lizenz. Für erste Tests steht jedoch eine kostenlose Testversion zur Verfügung.

### Kann ich Aspose.Cells in Webanwendungen verwenden?
Absolut! Aspose.Cells ist perfekt für Desktop-, Web- und Cloud-basierte Anwendungen, die in .NET entwickelt wurden.

### Welche Arten von Excel-Dateien kann ich mit Aspose.Cells erstellen?
Sie können eine Vielzahl von Excel-Dateiformaten erstellen, darunter XLSX, XLS, CSV und mehr.

### Wo erhalte ich Support für Aspose.Cells?
 Sie können Fragen stellen oder Hilfe finden im[Aspose-Foren](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
