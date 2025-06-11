---
"date": "2025-04-05"
"description": "Erfahren Sie, wie Sie mit Aspose.Cells für .NET HTML-formatierte Daten aus DataTables nahtlos in Excel-Tabellen importieren, alle Textstile beibehalten und Ihre Produktivität steigern."
"title": "So importieren Sie HTML-formatierte Datentabellen mit Aspose.Cells für .NET in Excel"
"url": "/de/net/import-export/aspose-cells-net-data-table-import-html-formatting/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# So importieren Sie HTML-formatierte Datentabellen mit Aspose.Cells für .NET in Excel

## Einführung

Haben Sie Probleme mit der manuellen Formatierung importierter Webseiten- oder Datenbankdaten in Excel? Damit sind Sie nicht allein! Entwickler müssen oft Textstile wie Fettdruck und Kursivschrift beibehalten, die für die Lesbarkeit entscheidend sind. Mit Aspose.Cells für .NET wird das Importieren einer DataTable mit HTML-formatierten Zeichenfolgen in eine Excel-Arbeitsmappe unter Beibehaltung des Stils zum Kinderspiel.

In diesem Lernprogramm erfahren Sie, wie Sie mit Aspose.Cells HTML-formatierte Daten aus einer DataTable in Excel importieren und so sicherstellen, dass Ihre Daten in Tabellenkalkulationen genau wie vorgesehen angezeigt werden.

**Was Sie lernen werden:**
- Einrichten und Konfigurieren von Aspose.Cells für .NET
- Importieren von DataTables mit HTML-Formatierung mithilfe von Aspose.Cells
- Automatisches Anpassen der Zeilen- und Spaltengröße an den Inhalt
- Speichern von Arbeitsmappen in mehreren Formaten, wie XLSX und ODS

Stellen wir zunächst sicher, dass Sie die notwendigen Voraussetzungen erfüllen!

## Voraussetzungen

Bevor Sie loslegen, stellen Sie sicher, dass Sie Folgendes haben:
- **Erforderliche Bibliotheken:** Aspose.Cells für .NET (Version 21.9 oder höher)
- **Anforderungen für die Umgebungseinrichtung:** Visual Studio mit installiertem .NET Core SDK
- **Erforderliche Kenntnisse:** Grundlegende Kenntnisse in C# und Vertrautheit mit DataTables in .NET

## Einrichten von Aspose.Cells für .NET

Installieren Sie zunächst die Aspose.Cells-Bibliothek in Ihrem Projekt über:

**Verwenden der .NET-CLI:**
```bash
dotnet add package Aspose.Cells
```

**Verwenden der Paketmanager-Konsole:**
```plaintext
PM> NuGet\Install-Package Aspose.Cells
```

Erwerben Sie eine Lizenz für die volle Funktionalität von der [Aspose-Website](https://purchase.aspose.com/temporary-license/) um alle Funktionen ohne Einschränkungen zu erkunden.

### Grundlegende Initialisierung

So können Sie Ihr Projekt mit Aspose.Cells initialisieren:
```csharp
using Aspose.Cells;

// Initialisieren eines neuen Workbook-Objekts
Workbook workbook = new Workbook();
```

Dies legt die Grundlage für die Arbeit mit Excel-Dateien in .NET unter Verwendung von Aspose.Cells.

## Implementierungshandbuch

Lassen Sie uns den Import von DataTables mit HTML-Formatierung in klare Schritte aufteilen.

### Vorbereiten Ihrer Datenquelle

**Überblick:**
Beginnen Sie mit dem Einrichten einer DataTable mit Beispieldaten, die HTML-formatierte Zeichenfolgen enthält, um die Styling-Funktionen von Aspose.Cells zu demonstrieren.
```csharp
using System.Data;

// Legen Sie hier Ihre Quell- und Ausgabeverzeichnisse fest
string SourceDir = "YOUR_SOURCE_DIRECTORY";
string OutputDir = "YOUR_OUTPUT_DIRECTORY";

// Bereiten Sie eine DataTable mit einigen HTML-formatierten Werten vor
dataTable = new DataTable("Products");
dataTable.Columns.Add("Product ID", typeof(Int32));
dataTable.Columns.Add("Product Name", typeof(string));
dataTable.Columns.Add("Units In Stock", typeof(Int32));

// Hinzufügen von Zeilen mit HTML-Formatierung
DataRow dr = dataTable.NewRow();
dr[0] = 1;
dr[1] = "<i>Aniseed</i> Syrup"; // HTML-Kursivschrift für Produktnamen
dr[2] = 15;
dataTable.Rows.Add(dr);

dr = dataTable.NewRow();
dr[0] = 2;
dr[1] = "<b>Boston Crab Meat</b>"; // HTML-Fettdruck für Produktnamen
dr[2] = 123;
dataTable.Rows.Add(dr);
```

### Festlegen der Importoptionen

**Konfigurieren Sie die Importtabellenoptionen:**
Verwenden `ImportTableOptions` um anzugeben, dass Zellenwerte als HTML-Zeichenfolgen interpretiert werden sollen.
```csharp
// Erstellen Sie Importoptionen zum Verarbeiten von HTML-formatierten Zeichenfolgen
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.IsFieldNameShown = true; // Spaltenüberschriften in den Import einbeziehen
importOptions.IsHtmlString = true; // Interpretieren von Zellenwerten als HTML-Strings
```

### Daten in Excel importieren

**Überblick:**
Erstellen Sie eine Arbeitsmappe und ein Arbeitsblatt und verwenden Sie dann `ImportData` um Ihre DataTable mit der gesamten Formatierung in Excel zu importieren.
```csharp
// Erstellen Sie eine Arbeitsmappe und holen Sie sich das erste Arbeitsblatt
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Importieren Sie die DataTable beginnend bei Zeile 0, Spalte 0
worksheet.Cells.ImportData(dataTable, 0, 0, importOptions);

// Passen Sie die Zeilen- und Spaltengröße für eine bessere Lesbarkeit an
worksheet.AutoFitRows();
worksheet.AutoFitColumns();
```

### Speichern Ihrer Arbeitsmappe

Speichern Sie Ihre Arbeitsmappe abschließend sowohl im XLSX- als auch im ODS-Format, um die Kompatibilität zwischen verschiedenen Tabellenkalkulationsanwendungen sicherzustellen.
```csharp
string output1Path = OutputDir + "Output.out.xlsx";
string output2Path = OutputDir + "Output.out.ods";

// Speichern Sie die Arbeitsmappe in zwei Formaten
workbook.Save(output1Path);
workbook.Save(output2Path);
```

## Praktische Anwendungen

Diese Funktion ist von unschätzbarem Wert für Szenarien, in denen die Datenpräsentation wichtig ist, wie zum Beispiel:
- **Berichterstattung:** Automatisches Anwenden von Stilen auf Finanzberichte.
- **Datenmigration:** Verschieben von aus dem Web Scraping gewonnenen Daten in Excel unter Beibehaltung der HTML-Formatierung.
- **Bestandsverwaltung:** Anzeige von Produktdetails mit Schwerpunkt auf kritischen Attributen.

Durch die Integration dieser Funktionalität können Prozesse bei Geschäftsanalysen und Berichtsaufgaben erheblich optimiert werden.

## Überlegungen zur Leistung

Beachten Sie beim Arbeiten mit großen Datensätzen Folgendes:
- **DataTable-Größe optimieren:** Um den Speicherverbrauch zu reduzieren, schließen Sie nur die erforderlichen Spalten ein.
- **Arbeitsmappenressourcen verwalten:** Entsorgen Sie Arbeitsmappen umgehend, nachdem Sie sie in freie Ressourcen gespeichert haben.
- **Verwenden Sie die Aspose.Cells-Funktionen:** Nutzen Sie integrierte Optimierungen für die effiziente Handhabung komplexer Datenstrukturen.

## Abschluss

Sie beherrschen den Import von HTML-formatierten DataTables in Excel mit Aspose.Cells für .NET. Diese Fähigkeit spart Zeit und verbessert die Präsentationsqualität Ihrer Berichte und Dokumente.

Um die Möglichkeiten weiter zu erkunden, experimentieren Sie mit anderen Aspose.Cells-Funktionen wie Diagrammintegration oder bedingter Formatierung. Sind Sie bereit für einen Schritt weiter? Setzen Sie diese Lösung in Ihrem nächsten Projekt ein!

## FAQ-Bereich

**F: Wie gehe ich mit großen Datensätzen mit HTML-Inhalten um?**
A: Optimieren Sie die DataTable-Größe und stellen Sie mithilfe der Best Practices von Aspose.Cells eine effiziente Speicherverwaltung innerhalb von .NET sicher.

**F: Kann ich Daten aus anderen Quellen als DataTables importieren?**
A: Ja, Aspose.Cells unterstützt verschiedene Datenquellen. Weitere Informationen finden Sie in der Dokumentation.

**F: Was ist, wenn meine HTML-Tags in Excel nicht richtig dargestellt werden?**
A: Stellen Sie sicher, dass Ihre `ImportTableOptions` ist konfiguriert mit `IsHtmlString = true`.

**F: Gibt es eine kostenlose Version von Aspose.Cells?**
A: Mit einer Testlizenz können Sie vorübergehend alle Funktionen nutzen. Besuchen Sie die [Aspose-Site](https://purchase.aspose.com/temporary-license/) für weitere Informationen.

**F: Kann ich Arbeitsmappen in anderen Formaten als XLSX und ODS speichern?**
A: Ja, Aspose.Cells unterstützt zahlreiche Dateiformate, darunter PDF, CSV und mehr.

## Ressourcen

Weitere Informationen und Ressourcen finden Sie unter:
- [Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/net/)
- [Aktuelle Veröffentlichungen herunterladen](https://releases.aspose.com/cells/net/)
- [Lizenzen erwerben](https://purchase.aspose.com/buy)
- [Kostenloser Testdownload](https://releases.aspose.com/cells/net/)
- [Erwerb einer temporären Lizenz](https://purchase.aspose.com/temporary-license/)
- [Aspose Support Forum](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}