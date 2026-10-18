---
category: general
date: 2026-03-21
description: Exportujte tabulku dat z Excelu do DataTable s hlavičkami, omezte počet
  desetinných míst a exportujte prvních 100 řádků pomocí Aspose.Cells.
draft: false
keywords:
- export excel data table
- export excel to datatable
- limit decimal places excel
- export first 100 rows
- export excel with headers
language: cs
og_description: Naučte se, jak exportovat tabulku dat z Excelu do DataTable, zachovat
  záhlaví, omezit počet desetinných míst a načíst prvních 100 řádků v C#.
og_title: Export datové tabulky Excel v C# – krok za krokem
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Export datové tabulky Excelu v C# – Kompletní průvodce
url: /cs/net/excel-data-export-retrieval/export-excel-data-table-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export tabulky dat z Excelu – Kompletní průvodce v C#

Potřebujete **export excel data table** z sešitu do .NET `DataTable`? Jste na správném místě—tento průvodce vám přesně ukáže, jak to provést, zachovat záhlaví sloupců, omezit desetinná místa a načíst pouze prvních 100 řádků.  

Pokud jste někdy zírali na tabulku a přemýšleli: „Jak to dostanu do své aplikace, aniž bych přišel o formátování?“, nejste sami. V následujících několika minutách proměníme tuto otázku v konkrétní řešení ke zkopírování a vložení, které funguje s Aspose.Cells, populární knihovnou pro práci s Excelem.

## Co se naučíte

- Jak **export excel to datatable** pomocí metody `ExportDataTable`.  
- Jak zachovat původní názvy sloupců (`export excel with headers`).  
- Jak **limit decimal places excel** hodnoty nastavením `ExportTableOptions`.  
- Jak bezpečně načíst jen prvních 100 řádků (`export first 100 rows`).  

Žádné externí skripty, žádné magické řetězce—jen čistý C#, který můžete vložit do libovolného .NET projektu.

## Požadavky

| Požadavek | Proč je to důležité |
|-------------|----------------|
| .NET 6 nebo novější (nebo .NET Framework 4.7+) | Aspose.Cells podporuje oba, ale novější runtime poskytují asynchronně připravená API. |
| Aspose.Cells for .NET NuGet package | Poskytuje `Workbook`, `ExportTableOptions` a pomocnou metodu `ExportDataTable`. |
| Vzorek souboru Excel (např. `Numbers.xlsx`) | Zdroj dat, která budete exportovat. |
| Základní znalost C# | Budete sledovat ukázky kódu, ale nic složitého není potřeba. |

Pokud vám některý z těchto bodů není známý, stáhněte si NuGet balíček pomocí `dotnet add package Aspose.Cells` a vytvořte malý soubor Excel s několika čísly—vaše testovací data.

![příklad exportu tabulky dat z Excelu](excel-data-table.png "Snímek obrazovky listu Excel, který bude exportován do DataTable")

## Krok 1: Načtení sešitu (export excel data table)

První, co potřebujete, je instance `Workbook`, která ukazuje na váš Excel soubor. Představte si to jako otevření knihy, než začnete číst kapitoly.

```csharp
using Aspose.Cells;

// 1️⃣ Load the workbook that contains the source data
Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");
```

> **Proč je to důležité:** Načtení sešitu vám poskytne přístup k jeho listům, buňkám a stylům. Pokud je cesta k souboru špatná, Aspose vyhodí `FileNotFoundException`, takže zkontrolujte umístění.

## Krok 2: Nastavení možností exportu – limit decimal places excel

Ve výchozím nastavení Aspose exportuje každou číselnou hodnotu s plnou přesností. Často však stačí jen několik významných číslic, zejména když data předáváte do UI gridu nebo API, které očekává zaokrouhlená čísla.

```csharp
using Aspose.Cells;

// 2️⃣ Configure export options – keep only 4 significant digits
ExportTableOptions exportOptions = new ExportTableOptions
{
    // This property trims the number of significant digits.
    SignificantDigits = 4
};
```

> **Tip:** Pokud potřebujete jinou strategii zaokrouhlování (např. vždy nahoru), můžete po exportu `DataTable` doprocesovat. Nastavení `SignificantDigits` je nejrychlejší způsob, jak **limit decimal places excel** bez psaní dalších smyček.

## Krok 3: Export požadovaného rozsahu (export first 100 rows)

Nyní řekneme Aspose, který blok buněk chceme přenést do `DataTable`. V tomto tutoriálu načteme prvních 100 řádků a prvních 10 sloupců, ale můžete tyto hodnoty upravit podle svých potřeb.

```csharp
using System.Data;
using Aspose.Cells;

// 3️⃣ Export a block of cells (first 100 rows × 10 columns) to a DataTable
DataTable dataTable = workbook.Worksheets[0].Cells.ExportDataTable(
    startRow: 0,          // zero‑based index, first row
    startColumn: 0,       // first column (A)
    totalRows: 100,       // export only the first 100 rows
    totalColumns: 10,     // and the first 10 columns
    exportColumnNames: true, // keep column headers (export excel with headers)
    options: exportOptions);
```

> **Hraniční případ:** Pokud list obsahuje méně než 100 řádků, Aspose jednoduše exportuje to, co je k dispozici, aniž by vyhodil chybu. Přesto můžete chtít chránit před nečekaně malým rozsahem:

```csharp
int rowsToExport = Math.Min(100, workbook.Worksheets[0].Cells.MaxDataRow + 1);
```

## Krok 4: Ověření výsledku – rychlý výpis do konzole

Zobrazit data v debuggeru je fajn, ale vypsání několika řádků do konzole potvrdí, že **export excel to datatable** skutečně fungoval a že desetinná místa jsou oříznuta.

```csharp
static void PrintDataTable(DataTable table)
{
    foreach (DataRow row in table.Rows)
    {
        foreach (var item in row.ItemArray)
            Console.Write($"{item}\t");
        Console.WriteLine();
    }
}

// Call the helper
PrintDataTable(dataTable);
```

### Očekávaný výstup

```
ID      Name    Score   Ratio   Date        ...
1       Alice   95.12   0.8234  2023-01-15  ...
2       Bob     88.5    0.7612  2023-01-16  ...
3       Carol   73.33   0.6721  2023-01-17  ...
...
```

Všimněte si, že číselné sloupce nyní ukazují jen čtyři významné číslice, což odpovídá nastavení `SignificantDigits = 4`, které jsme použili dříve.

## Krok 5: Zabalit vše dohromady – kompletní spustitelný příklad

Níže je celý program, který můžete zkopírovat a vložit do konzolové aplikace. Obsahuje ošetření chyb, volitelnou kontrolu počtu řádků a pomocnou metodu pro výpis.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class ExportExcelDemo
{
    static void Main()
    {
        try
        {
            // 👉 Load the workbook
            Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");

            // 👉 Set up export options (limit decimal places excel)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                SignificantDigits = 4
            };

            // 👉 Determine safe row count (export first 100 rows)
            int maxRows = workbook.Worksheets[0].Cells.MaxDataRow + 1;
            int rowsToExport = Math.Min(100, maxRows);

            // 👉 Export to DataTable (export excel to datatable, export excel with headers)
            DataTable dt = workbook.Worksheets[0].Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: rowsToExport,
                totalColumns: 10,
                exportColumnNames: true,
                options: exportOptions);

            // 👉 Show a glimpse of the data
            PrintDataTable(dt);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }

    static void PrintDataTable(DataTable table)
    {
        foreach (DataRow row in table.Rows)
        {
            foreach (var item in row.ItemArray)
                Console.Write($"{item}\t");
            Console.WriteLine();
        }
    }
}
```

Spusťte program a uvidíte prvních 100 řádků vašeho listu, pěkně zaokrouhlených, s neporušenými názvy sloupců.

## Často kladené otázky a úskalí

| Otázka | Odpověď |
|----------|--------|
| **Co když má můj list sloučené buňky?** | `ExportDataTable` rozplývá sloučené buňky tak, že vezme hodnotu z levé horní buňky. Pokud potřebujete vlastní zpracování, nejprve buňky rozlučte nebo čtěte surové objekty `Cell`. |
| **Mohu exportovat místo toho do `DataSet`?** | Ano — použijte `ExportDataTable` |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}