---
category: general
date: 2026-10-26
description: Benutzerdefinierte ExportTableOptions, wenn ExportAsStrin verwendet wird,
  ermöglichen das Exportieren von Excel-Daten als Zeichenketten in C#. Folgen Sie
  der Schritt‑für‑Schritt‑Anleitung, um den Export zu konfigurieren und auszuführen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Custom ExportTableOptions when ExportAsStrin
- how to export excel as string
- ExportTableOptions C#
- Excel to DataTable string conversion
- Aspose.Cells export as string
language: de
lastmod: 2026-10-26
og_description: Benutzerdefinierte ExportTableOptions, wenn ExportAsStrin aktiviert
  ist, ermöglichen den reinen String‑Excel‑Export. Erfahren Sie die genauen Schritte
  zur Konfiguration und Ausführung des Exports in C#.
og_image_alt: Code snippet showing ExportTableOptions configuration for string export
og_title: Benutzerdefinierte ExportTableOptions bei ExportAsString – Excel als Zeichenkette
  in C# exportieren
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Custom ExportTableOptions when ExportAsStrin lets you export Excel
    data as strings in C#. Follow the step‑by‑step guide to configure and run the
    export.
  headline: Custom ExportTableOptions when ExportAsStrin for Excel
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Benutzerdefinierte ExportTableOptions beim ExportAsStrin für Excel
url: /de/net/excel-data-export-retrieval/custom-exporttableoptions-when-exportasstrin-for-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Benutzerdefinierte ExportTableOptions bei ExportAsStrin – Excel als Zeichenkette exportieren in C#

Wenn Sie **Custom ExportTableOptions when ExportAsStrin** benötigen, um jeden Zellenwert als einfache Zeichenkette zu erhalten, zeigt Ihnen dieser Leitfaden genau, wie Sie das tun. Egal, ob Sie eine Daten‑Import‑Pipeline erstellen oder einen sauberen CSV‑bereiten Dump benötigen, Sie werden sehen, warum die Konfiguration der Optionen auf diese Weise Typkonvertierungs‑Überraschungen vermeidet.

In diesem Tutorial lernen Sie **how to export excel as string** mit der Aspose.Cells-Bibliothek, sehen den vollständigen, ausführbaren Code und verstehen die Begründung hinter jeder Einstellung. Keine externe Dokumentation ist erforderlich – alles, was Sie benötigen, finden Sie hier.

## Voraussetzungen

* .NET 6.0 SDK oder später installiert  
* Visual Studio 2022 (oder jede IDE, die .NET unterstützt)  
* Aspose.Cells for .NET-Paket (Installation über NuGet: `Install-Package Aspose.Cells`)  
* Eine Excel-Arbeitsmappe (`sample.xlsx`) im Stammordner des Projekts abgelegt  

Diese Elemente sind die einzigen Abhängigkeiten; der Code läuft unter Windows, Linux oder macOS ohne zusätzliche Bibliotheken.

## Schritt 1: Laden Sie die Arbeitsmappe, die Sie exportieren möchten

Das Erste, was Sie tun, wenn Sie **Custom ExportTableOptions when ExportAsStrin** verwenden, ist, ein `Worksheet`‑Objekt aus einer geladenen Arbeitsmappe zu erhalten. Dieses Objekt gibt Ihnen Zugriff auf Zeilen, Spalten und die Export‑API.

```csharp
using Aspose.Cells;
using System.Data;

// Load the workbook from disk
Workbook workbook = new Workbook("sample.xlsx");

// Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*Warum das wichtig ist:*  
`Workbook` liest die Datei einmal ein und behält alle Formatierungsinformationen im Speicher. Durch die Auswahl eines bestimmten `Worksheet` begrenzen Sie den Exportumfang und vermeiden unnötige Verarbeitung versteckter Tabellen.

## Schritt 2: ExportTableOptions mit ExportAsString = true konfigurieren

Der Kern von **Custom ExportTableOptions when ExportAsStrin** ist das `ExportTableOptions`‑Objekt. Das Setzen von `ExportAsString` zwingt den Exporter, jede Zelle als Zeichenkette zu behandeln, unabhängig von ihrem ursprünglichen Datentyp (Datum, Zahl, Boolesch usw.). Das Aktivieren von `PreserveFormatting` bewahrt den visuellen Stil (z. B. Währungssymbole) in der resultierenden Zeichenkette.

```csharp
// Create and configure the export options
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export every cell value as a string
    PreserveFormatting = true      // Keep the original cell formatting
};
```

*Warum das wichtig ist:*  
Wenn Sie später `ExportDataTable` aufrufen, versucht die Bibliothek normalerweise, den .NET‑Typ jeder Spalte zu ermitteln. Mit `ExportAsString = true` wird dieser Ermittlungsschritt übersprungen, wodurch unerwartete `DateTime`‑ oder `double`‑Konvertierungen verhindert werden, die nachgelagerte CSV‑Parser beschädigen könnten.

## Schritt 3: Exportieren Sie einen Bereich in ein DataTable‑Objekt mit den benutzerdefinierten Optionen

Jetzt können Sie einen rechteckigen Bereich (Zeilen 0‑9, Spalten 0‑4) aus dem Arbeitsblatt exportieren. Die Methode gibt ein `DataTable` zurück, bei dem jedes Feld ein `string` ist.

```csharp
// Export rows 0‑9 and columns 0‑4 (5 columns total) as a DataTable
DataTable dataTable = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 10,
    totalColumns: 5,
    options: exportOptions);
```

*Warum das wichtig ist:*  
`ExportDataTable` ist der bequemste Weg, Excel‑Daten in eine relationale Struktur zu überführen, die viele .NET‑APIs bereits verstehen (z. B. Entity Framework, Dapper). Durch das Übergeben der **Custom ExportTableOptions when ExportAsStrin** stellen Sie sicher, dass jeder `DataColumn.DataType` `typeof(string)` ist.

## Schritt 4: Ergebnis überprüfen – alle Werte sind Zeichenketten

Es ist gute Praxis, zu bestätigen, dass der Export wie erwartet funktioniert hat. Die folgende Schleife gibt jede Zelle und ihren Laufzeittyp aus.

```csharp
Console.WriteLine("Exported DataTable (all values as strings):");
foreach (DataRow row in dataTable.Rows)
{
    for (int i = 0; i < dataTable.Columns.Count; i++)
    {
        object value = row[i];
        Console.Write($"{value} ({value.GetType().Name})\t");
    }
    Console.WriteLine();
}
```

**Erwartete Ausgabe**

```
123 (String)    2023‑01‑15 (String)    $45.67 (String)    TRUE (String)    Sample text (String)
...
```

Jede Zelle zeigt `String` als Typ an, was bestätigt, dass **Custom ExportTableOptions when ExportAsStrin** korrekt funktioniert hat.

## Schritt 5: Optional – DataTable in CSV schreiben

Wenn Ihr endgültiges Ziel eine reine Textdatei ist, können Sie das `DataTable` ganz einfach in CSV serialisieren:



## Was Sie als Nächstes lernen sollten

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [HTML‑Strings aus Excel in DataTable exportieren mit Aspose.Cells für .NET: Eine Schritt‑für‑Schritt‑Anleitung](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)
- [Benutzerdefinierte Eigenschaften aus Excel/PDF mit Aspose Cells .NET exportieren](/cells/hongkong/net/workbook-operations/export-custom-properties-excel-pdf-aspose-cells-net/)
- [Aspose Cells Java: Benutzerdefinierte Ladefilter für den Excel‑Export](/cells/hongkong/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}