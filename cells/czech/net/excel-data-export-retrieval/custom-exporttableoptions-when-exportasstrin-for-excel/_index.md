---
category: general
date: 2026-10-26
description: Vlastní ExportTableOptions při ExportAsStrin vám umožňuje exportovat
  data z Excelu jako řetězce v C#. Postupujte podle průvodce krok za krokem pro nastavení
  a spuštění exportu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Custom ExportTableOptions when ExportAsStrin
- how to export excel as string
- ExportTableOptions C#
- Excel to DataTable string conversion
- Aspose.Cells export as string
language: cs
lastmod: 2026-10-26
og_description: Vlastní ExportTableOptions, když ExportAsStrin umožňuje export do
  Excelu pouze jako řetězec. Naučte se přesné kroky, jak nakonfigurovat a spustit
  export v C#.
og_image_alt: Code snippet showing ExportTableOptions configuration for string export
og_title: Vlastní ExportTableOptions při ExportAsString – export Excelu jako řetězec
  v C#
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
title: Vlastní ExportTableOptions při ExportAsStrin pro Excel
url: /cs/net/excel-data-export-retrieval/custom-exporttableoptions-when-exportasstrin-for-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vlastní ExportTableOptions při ExportAsStrin – export Excelu jako řetězec v C#

Pokud potřebujete **Custom ExportTableOptions when ExportAsStrin**, abyste získali každou hodnotu buňky jako prostý řetězec, tento návod vám ukáže přesně, jak na to. Ať už budujete pipeline pro import dat nebo potřebujete čistý výstup připravený pro CSV, uvidíte, proč konfigurace možností tímto způsobem zabraňuje neočekávaným konverzím typů.

V tomto tutoriálu se naučíte **jak exportovat excel jako řetězec** pomocí knihovny Aspose.Cells, uvidíte kompletní spustitelný kód a pochopíte důvody za každým nastavením. Není potřeba žádná externí dokumentace – vše, co potřebujete, je zde.

## Prerequisites

Než začnete, ujistěte se, že máte:

* .NET 6.0 SDK nebo novější nainstalovaný  
* Visual Studio 2022 (nebo jakékoli IDE podporující .NET)  
* Aspose.Cells for .NET balíček (nainstalujte přes NuGet: `Install-Package Aspose.Cells`)  
* Excel sešit (`sample.xlsx`) umístěný v kořenovém adresáři projektu  

Tyto položky jsou jedinými závislostmi; kód běží na Windows, Linuxu i macOS bez dalších knihoven.

## Step 1: Load the workbook you want to export

Prvním krokem při použití **Custom ExportTableOptions when ExportAsStrin** je získat objekt `Worksheet` z načteného sešitu. Tento objekt vám poskytuje přístup k řádkům, sloupcům a exportovacímu API.

```csharp
using Aspose.Cells;
using System.Data;

// Load the workbook from disk
Workbook workbook = new Workbook("sample.xlsx");

// Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*Proč je to důležité:*  
`Workbook` načte soubor jednou a udržuje veškeré informace o formátování v paměti. Výběrem konkrétního `Worksheet` omezíte rozsah exportu a vyhnete se zbytečnému zpracování skrytých listů.

## Step 2: Configure ExportTableOptions with ExportAsString = true

Jádrem **Custom ExportTableOptions when ExportAsStrin** je objekt `ExportTableOptions`. Nastavení `ExportAsString` přinutí exportér zacházet s každou buňkou jako s řetězcem, bez ohledu na její původní datový typ (datum, číslo, boolean atd.). Povolení `PreserveFormatting` zachová vizuální styl (např. měnové symboly) ve výsledném řetězci.

```csharp
// Create and configure the export options
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export every cell value as a string
    PreserveFormatting = true      // Keep the original cell formatting
};
```

*Proč je to důležité:*  
Když později zavoláte `ExportDataTable`, knihovna normálně zkouší odhadnout .NET typ každého sloupce. S `ExportAsString = true` je tento odhad přeskočen, čímž se zabrání neočekávaným konverzím `DateTime` nebo `double`, které mohou rozbít následné CSV parsery.

## Step 3: Export a range to a DataTable using the custom options

Nyní můžete exportovat obdélníkový rozsah (řádky 0‑9, sloupce 0‑4) z listu. Metoda vrátí `DataTable`, kde je každé pole typu `string`.

```csharp
// Export rows 0‑9 and columns 0‑4 (5 columns total) as a DataTable
DataTable dataTable = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 10,
    totalColumns: 5,
    options: exportOptions);
```

*Proč je to důležité:*  
`ExportDataTable` je nejpohodlnější způsob, jak přenést data z Excelu do relační struktury, kterou mnoho .NET API již rozumí (např. Entity Framework, Dapper). Předáním **Custom ExportTableOptions when ExportAsStrin** zajistíte, že `DataColumn.DataType` bude `typeof(string)`.

## Step 4: Verify the result – all values are strings

Je dobré ověřit, že export proběhl podle očekávání. Následující smyčka vypíše každou buňku a její runtime typ.

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

**Expected output**

```
123 (String)    2023‑01‑15 (String)    $45.67 (String)    TRUE (String)    Sample text (String)
...
```

Každá buňka ukazuje `String` jako svůj typ, což potvrzuje, že **Custom ExportTableOptions when ExportAsStrin** fungovalo správně.

## Step 5: Optional – write the DataTable to CSV

Pokud je vaším konečným cílem soubor prostého textu, můžete snadno serializovat `DataTable` do CSV:



## What Should You Learn Next?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Export HTML Strings from Excel to DataTable using Aspose.Cells for .NET: A Step‑by‑Step Guide](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)
- [Export Custom Properties Excel Pdf Aspose Cells Net](/cells/hongkong/net/workbook-operations/export-custom-properties-excel-pdf-aspose-cells-net/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hongkong/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}