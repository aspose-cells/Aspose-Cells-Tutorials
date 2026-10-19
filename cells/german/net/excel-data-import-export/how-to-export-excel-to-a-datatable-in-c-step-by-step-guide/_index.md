---
category: general
date: 2026-03-18
description: Wie man Excel-Daten in C# in ein DataTable exportiert, mit Code, der
  bestimmte Zellen verarbeitet, Excel in ein DataTable konvertiert und Zahlen formatiert.
  Erfahren Sie, wie Sie bestimmte Zellen exportieren und mehr.
draft: false
keywords:
- how to export excel
- convert excel to datatable
- export specific cells
- excel to datatable c#
- excel range to datatable
language: de
og_description: Wie man Excel‑Daten in ein DataTable in C# exportiert. Dieses Tutorial
  zeigt, wie man bestimmte Zellen exportiert, Excel in ein DataTable konvertiert und
  Zahlen mühelos formatiert.
og_title: Wie man Excel in ein DataTable in C# exportiert – Vollständige Anleitung
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: Wie man Excel in ein DataTable in C# exportiert – Schritt‑für‑Schritt‑Anleitung
url: /de/net/excel-data-import-export/how-to-export-excel-to-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Excel in ein DataTable in C# exportiert – Schritt‑für‑Schritt‑Anleitung

Haben Sie sich jemals gefragt, **wie man Excel**‑Daten in ein `DataTable` exportiert, ohne die Formatierung zu verlieren? Sie sind nicht allein – Entwickler müssen ständig einen Ausschnitt einer Tabelle in den Speicher holen für Berichte, Validierung oder Bulk‑Insert‑Operationen. Die gute Nachricht? Mit ein paar Zeilen C# können Sie einen genauen Bereich (z. B. *A1:F11*) exportieren, jede Zelle als Zeichenkette behandeln und sogar ein benutzerdefiniertes Zahlenformat anwenden.

In diesem Tutorial behandeln wir alles, was Sie wissen müssen: vom Laden der Arbeitsmappe, über die Konfiguration von **export specific cells**, bis hin zur Umwandlung des Bereichs in ein `DataTable` und dem Umgang mit Sonderfällen wie leeren Zeilen oder länderspezifischen Zahlen. Am Ende haben Sie eine wiederverwendbare Methode, die in **excel to datatable c#**‑Szenarien im Produktionscode funktioniert.

> **Voraussetzungen** – Sie benötigen die Aspose.Cells für .NET Bibliothek (oder eine ähnliche API, die `ExportDataTable` bereitstellt). Das Beispiel geht von .NET 6+ aus, aber die Konzepte gelten auch für frühere Versionen.

## Was Sie lernen werden

- Wie man **Excel in DataTable** mit Aspose.Cells konvertiert.
- Exportieren eines benutzerdefinierten Bereichs (`excel range to datatable`), wobei alle Werte als Zeichenketten behandelt werden.
- Anwenden eines Zahlenformats mit zwei Dezimalstellen (`#,#00.00`) beim Export.
- Häufige Stolperfallen (null‑Zeilen, versteckte Spalten) und wie man sie vermeidet.
- Ein sofort kopierbares, vollständig ausführbares Code‑Beispiel.

## Voraussetzungen und Einrichtung

Bevor wir in den Code eintauchen, stellen Sie sicher, dass Sie Folgendes haben:

1. **Aspose.Cells für .NET** über NuGet installiert:

   ```bash
   dotnet add package Aspose.Cells
   ```

2. Eine Excel‑Datei (`input.xlsx`) in einem Ordner, den Sie referenzieren können, z. B. `YOUR_DIRECTORY/input.xlsx`.
3. Ein Projekt, das .NET 6 oder höher anvisiert (die unten gezeigten `using`‑Anweisungen funktionieren sofort).

> **Pro‑Tipp:** Wenn Sie eine andere Bibliothek verwenden (z. B. EPPlus oder ClosedXML), bleibt das Konzept gleich – laden Sie die Arbeitsmappe, wählen Sie einen Bereich aus und rufen Sie eine Methode auf, die ein `DataTable` zurückgibt.

## Schritt 1: Laden der Arbeitsmappe und Abrufen des ersten Arbeitsblatts

Das erste, was Sie benötigen, ist ein `Workbook`‑Objekt, das Ihre Excel‑Datei repräsentiert. Sobald Sie es haben, können Sie jedes Arbeitsblatt über Index oder Name ansprechen.

```csharp
using Aspose.Cells;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];

            // Continue with export options...
        }
    }
}
```

**Warum das wichtig ist:** Das frühe Laden der Arbeitsmappe ermöglicht es Ihnen, ihre Struktur (versteckte Blätter, Schutz) zu prüfen, bevor Sie entscheiden, welche Zellen exportiert werden sollen. Ist die Datei groß, sollten Sie `LoadOptions` verwenden, um nur die benötigten Teile zu streamen.

## Schritt 2: Exportoptionen konfigurieren – Alle Werte als Zeichenketten behandeln

Wenn Sie Daten für nachgelagerte Verarbeitung exportieren (z. B. Bulk‑Insert in SQL), möchten Sie häufig eine **einheitliche Zeichenketten‑Darstellung**. Das verhindert später Typ‑Mismatches.

```csharp
// Configure export behavior
ExportTableOptions exportOptions = new ExportTableOptions
{
    // Force every cell to be returned as a string, regardless of its original type
    ExportAsString = true,

    // Apply a two‑decimal‑place format to numeric cells
    NumberFormat = "#,##0.00"
};
```

**Erklärung:**  
- `ExportAsString = true` weist Aspose.Cells an, den nativen Zellentyp zu ignorieren und den formatierten Text zurückzugeben.  
- `NumberFormat = "#,##0.00"` sorgt dafür, dass Zahlen wie `1234.5` zu `"1,234.50"` werden – nützlich für Finanzberichte.

Falls Sie die ursprünglichen Datentypen benötigen, setzen Sie einfach `ExportAsString` auf `false` und übernehmen die Konvertierung selbst.

## Schritt 3: Export eines bestimmten Bereichs (A1:F11) in ein DataTable

Jetzt kommt der Kern von **export specific cells**. Die Methode `ExportDataTable` nimmt Start‑/End‑Zeilen‑ und Spaltenindizes (nullbasiert) sowie ein Flag für die Einbeziehung der Kopfzeile.

```csharp
// Export cells A1:F11 (rows 0‑10, columns 0‑5) including the header row
DataTable table = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    endRow: 10,
    endColumn: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

**Was Sie erhalten:** Ein `DataTable` mit 11 Zeilen (einschließlich der Kopfzeile) und 6 Spalten (`A`‑`F`). Alle Werte sind Zeichenketten, formatiert gemäß `exportOptions`.

## Schritt 4: Ergebnis überprüfen – Ausgabe in die Konsole

Es ist immer ratsam, die Ausgabe zu prüfen, bevor Sie die Tabelle an eine andere Komponente übergeben.

```csharp
// Simple console dump
foreach (DataRow row in table.Rows)
{
    foreach (var item in row.ItemArray)
    {
        Console.Write($"{item}\t");
    }
    Console.WriteLine();
}
```

Sie sollten etwa Folgendes sehen:

```
Id      Name        Qty     Price   Total   Date
1       Widget A    10      2.50    25.00   2026-01-01
2       Widget B    5       3.75    18.75   2026-01-02
...
```

Beachten Sie, dass die numerischen Spalten zwei Dezimalstellen anzeigen, genau wie wir es angegeben haben.

## Vollständiges funktionierendes Beispiel (kopier‑bereit)

Unten finden Sie das vollständige Programm, das alles zusammenführt. Fügen Sie es in ein neues Konsolenprojekt ein, passen Sie den Dateipfad an und führen Sie es aus – keine zusätzliche Konfiguration nötig.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load workbook and select worksheet
            // -------------------------------------------------
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -------------------------------------------------
            // 2️⃣ Set export options – strings + number format
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                NumberFormat = "#,##0.00"
            };

            // -------------------------------------------------
            // 3️⃣ Export range A1:F11 (rows 0‑10, cols 0‑5)
            // -------------------------------------------------
            DataTable table = worksheet.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                endRow: 10,
                endColumn: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // -------------------------------------------------
            // 4️⃣ Output to console for verification
            // -------------------------------------------------
            Console.WriteLine("=== Exported DataTable ===");
            foreach (DataRow row in table.Rows)
            {
                foreach (var cell in row.ItemArray)
                {
                    Console.Write($"{cell}\t");
                }
                Console.WriteLine();
            }

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Wichtige Erkenntnisse aus dem Code:**

- Das Objekt `ExportTableOptions` ist wiederverwendbar; Sie können es an mehrere `ExportDataTable`‑Aufrufe übergeben, wenn Sie mehrere Bereiche exportieren müssen.
- Die Indizierung beginnt bei **0**, sodass `A1` auf `(0,0)` abgebildet wird.
- Durch Setzen von `includeColumnNames` auf `true` werden automatisch die Werte der ersten Zeile als Spaltenüberschriften verwendet – ideal für nachgelagerte `DataTable`‑Operationen.

## Umgang mit Sonderfällen & häufigen Fragen

### Was ist, wenn das Arbeitsblatt versteckte Zeilen oder Spalten hat?

Aspose.Cells berücksichtigt die Sichtbarkeit standardmäßig. Wenn Sie versteckte Daten exportieren müssen, setzen Sie `exportOptions.ExportHiddenRows = true` und `ExportHiddenColumns = true`.

### Meine Excel‑Datei enthält Formeln – erhalte ich die berechneten Werte?

Ja. Standardmäßig gibt `ExportDataTable` den **angezeigten Wert** (das Ergebnis der Formel) zurück. Wenn Sie den rohen Formeltext benötigen, setzen Sie `exportOptions.ExportFormulas = true`.

### Wie überspringe ich komplett leere Zeilen?

Nach dem Export können Sie das `DataTable` bereinigen:

```csharp
foreach (DataRow row in table.Rows.Cast<DataRow>()
                                   .Where(r => r.ItemArray.All(c => c == DBNull.Value || string.IsNullOrWhiteSpace(c.ToString()))).ToList())
{
    table.Rows.Remove(row);
}
```

### Kann ich einen nicht zusammenhängenden Bereich exportieren (z. B. A1:B5 und D1:E5)?

Aspose.Cells unterstützt keine disjunkten Bereiche in einem einzigen Aufruf. Stattdessen exportieren Sie jeden Block separat und fügen die resultierenden `DataTable`s anschließend manuell zusammen.

## Leistungstipps

- **`ExportTableOptions` wiederverwenden** für mehrere Exporte; jedes Mal eine neue Instanz zu erstellen verursacht nur geringen Aufwand, macht den Code aber unübersichtlich.
- **Große Dateien streamen** mit `LoadOptions`, um zu vermeiden, dass die gesamte Arbeitsmappe in den Speicher geladen wird.
- **`DataTable` vermeiden**, wenn Sie nur einen schnellen CSV‑Export benötigen – `ExportDataTable` ist praktisch, aber nicht die speichereffizienteste Lösung für riesige Tabellen.

## Fazit

Wir haben gezeigt, **wie man Excel**‑Daten in ein `DataTable` exportiert, dabei die Formatierung steuert, bestimmte Zellbereiche behandelt und sicherstellt, dass jeder Wert als Zeichenkette ankommt. Das vollständige Beispiel demonstriert einen sauberen, produktionsbereiten Ansatz, den Sie für **convert excel to datatable**, **export specific cells** oder jedes **excel range to datatable**‑Szenario anpassen können.

Fühlen Sie sich frei zu experimentieren: ändern Sie den Bereich, schalten Sie `ExportAsString` um, oder leiten Sie das `DataTable` direkt in Entity Framework für Bulk‑Inserts. Der Himmel ist die Grenze, sobald Sie diese solide Grundlage haben.

### Nächste Schritte & verwandte Themen

- **Importieren eines DataTable zurück nach Excel** – lernen Sie die Gegenoperation mit `ImportDataTable`.
- **Bulk‑Insert eines DataTable in SQL Server** – verwenden Sie `SqlBulkCopy` für superschnelle Ladungen.
- **Arbeiten mit EPPlus oder ClosedXML** – sehen Sie, wie dieselbe Aufgabe mit alternativen Bibliotheken aussieht.
- **Zellen beim Export formatieren** – erkunden Sie `ExportTableOptions` weiter für Datumsformate, benutzerdefinierte Kultur‑Einstellungen und mehr.

Haben Sie Fragen oder einen anderen Anwendungsfall? Hinterlassen Sie einen Kommentar, und wir halten die Diskussion am Laufen. Viel Spaß beim Coden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}