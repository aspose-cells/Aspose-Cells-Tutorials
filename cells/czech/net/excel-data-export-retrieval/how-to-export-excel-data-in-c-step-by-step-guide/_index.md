---
category: general
date: 2026-03-21
description: Jak exportovat data z Excelu s názvy sloupců, zachovat formát čísel a
  číst konkrétní řádky pomocí Aspose.Cells v C#. Naučte se efektivně číst list Excelu
  a exportovat specifické řádky.
draft: false
keywords:
- how to export excel
- preserve number format
- export with column names
- read excel worksheet
- export specific rows
language: cs
og_description: Jak exportovat data z Excelu s názvy sloupců, zachovat formát čísel
  a číst konkrétní řádky pomocí Aspose.Cells. Kompletní, spustitelný příklad pro vývojáře
  C#.
og_title: Jak exportovat data z Excelu v C# – Kompletní programovací průvodce
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Jak exportovat data z Excelu v C# – krok za krokem
url: /cs/net/excel-data-export-retrieval/how-to-export-excel-data-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak exportovat data z Excelu v C# – Kompletní programovací průvodce

Už jste se někdy zamysleli nad **jak exportovat excel** data bez ztráty původního formátování? Možná jste zkusili rychlé kopírování‑vkládání a skončili s daty, kde datum vypadá jako „44728“ nebo chybí záhlaví sloupců. To je frustrující, že? V tomto tutoriálu uvidíte čistý, end‑to‑end způsob, jak načíst list Excelu, zachovat formát čísel, exportovat se jmény sloupců a dokonce vybrat jen řádky, které potřebujete.

Budeme používat knihovnu Aspose.Cells, protože poskytuje detailní kontrolu nad možnostmi exportu. Na konci tohoto průvodce budete mít znovupoužitelný úryvek, který můžete vložit do libovolného .NET projektu, a pochopíte, proč každá volba má význam. Žádná externí dokumentace není potřeba – vše, co potřebujete, je zde.

---

## Co se naučíte

- **Read Excel worksheet** do paměti pomocí Aspose.Cells.
- **Export specific rows** (např. řádky 0‑49) při zachování názvů sloupců.
- **Preserve number format** aby měny, data a procenta zůstaly nezměněny.
- Jak **export with column names** a zahrnout komentáře buněk, pokud je potřebujete.
- Kompletní, připravený k spuštění C# příklad plus tipy pro běžné úskalí.

### Předpoklady

- .NET 6.0 nebo novější (kód funguje také s .NET Framework 4.6+).
- Aspose.Cells pro .NET nainstalovaný přes NuGet (`Install-Package Aspose.Cells`).
- Soubor Excel (`input.xlsx`) umístěný ve složce, na kterou můžete odkazovat.

> **Pro tip:** Pokud používáte CI pipeline, zvažte stažení NuGet balíčku z privátního zdroje, abyste se vyhnuli překvapením s licencí.

## Krok 1 – Instalace Aspose.Cells a přidání jmenných prostorů

Nejprve se ujistěte, že balíček Aspose.Cells je ve vašem projektu. Otevřete Package Manager Console a spusťte:

```powershell
Install-Package Aspose.Cells
```

Poté přidejte požadované `using` direktivy na začátek vašeho C# souboru:

```csharp
using Aspose.Cells;
using System.Data;
using System;
```

Tyto importy vám poskytují přístup k `Workbook`, `Worksheet`, `ExportTableOptions` a `DataTable` – základním částem pro **reading an Excel worksheet** a export dat.

## Krok 2 – Načtení sešitu (Read the Excel File)

Nyní skutečně **read the Excel worksheet**. Konstruktor `Workbook` přijímá cestu k souboru a Aspose.Cells zvládne jak formát `.xlsx`, tak starší `.xls`.

```csharp
// Step 2: Load the workbook containing the data
string filePath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(filePath);
```

> **Why this matters:** Načtení sešitu jednou a opětovné použití stejného objektu `Worksheet` je mnohem efektivnější než opakované otevírání souboru, zejména u velkých tabulek.

## Krok 3 – Konfigurace možností exportu (Preserve Number Format & Column Names)

Zde říkáme Aspose.Cells *jak* exportovat. Třída `ExportTableOptions` nám umožňuje jemně doladit výstup. Aktivujeme tři příznaky:

1. `ExportAsString = true` – vynutí, aby se každá buňka stala řetězcem, což zaručuje, že čísla zachovají svůj vizuální vzhled.
2. `IncludeCellComments = true` – kopíruje všechny komentáře připojené k buňkám (užitečné pro dokumentaci).
3. `PreserveNumberFormat = true` – zachová původní formát čísla (symboly měny, vzory dat atd.).

```csharp
// Step 3: Configure export options to control how the table is exported
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export all values as strings
    IncludeCellComments = true,     // Preserve any cell comments
    PreserveNumberFormat = true     // Keep the original number formatting
};
```

> **Edge case:** Pokud nastavíte `ExportAsString` na `false`, ale stále chcete zachovat formáty čísel, můžete skončit s čistými číselnými hodnotami (např. 44728 pro datum). Nechat oba příznaky zapnuté tomuto překvapení předchází.

## Krok 4 – Získání prvního listu (Read Excel Worksheet)

Většina jednoduchých souborů má potřebná data na prvním listu, takže jej získáme podle indexu. Pokud potřebujete jiný list, stačí nahradit `0` odpovídajícím nulovým indexem nebo použít `workbook.Worksheets["SheetName"]`.

```csharp
// Step 4: Get the first worksheet from the workbook
Worksheet firstWorksheet = workbook.Worksheets[0];
```

> **Why it’s useful:** Přímý přístup k objektu listu vám dává plnou kontrolu nad jeho kolekcí `Cells`, což je nezbytné pro **export specific rows** později.

## Krok 5 – Export rozsahu buněk (Export Specific Rows)

Nyní jádro tutoriálu: export řádků 0‑49 a sloupců 0‑4 (tj. prvních 50 řádků a prvních pěti sloupců) do `DataTable`. Také požádáme Aspose.Cells, aby zahrnul názvy sloupců jako první řádek `DataTable`.

```csharp
// Step 5: Export a range of cells (rows 0‑49, columns 0‑4) to a DataTable using the options
DataTable exportedTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 50,
    totalColumns: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

### Co to dělá

- **`startRow: 0`** – začíná na úplně vrcholu listu.
- **`totalRows: 50`** – získá prvních 50 řádků (tj. **export specific rows**).
- **`totalColumns: 5`** – omezuje export na prvních pět sloupců.
- **`includeColumnNames: true`** – zajišťuje, že záhlaví sloupců `DataTable` odpovídá řádku s hlavičkou v Excelu, což splňuje požadavek **export with column names**.
- **`exportOptions`** – použije nastavení z Kroku 3, takže vaše číselné hodnoty zůstanou ve formátu jako “$1,234.56” místo “1234.56”.

## Krok 6 – Ověření exportu (Jak výsledek vypadá)

Vytiskněme několik prvních řádků do konzole, abyste viděli, že formátování přežilo.

```csharp
// Step 6: Display a few rows to verify the export
Console.WriteLine("=== Exported DataTable Preview ===");
foreach (DataRow row in exportedTable.Rows)
{
    // Join each column with a tab for readability
    Console.WriteLine(string.Join("\t", row.ItemArray));
}
```

**Očekávaný výstup (příklad):**

```
=== Exported DataTable Preview ===
Date        Description    Amount   Tax   Total
01/02/2024  Widget A       $120.00  $12  $132.00
01/03/2024  Widget B       $200.00  $20  $220.00
...
```

Všimněte si, že data se zobrazují ve formátu `MM/dd/yyyy` a měna si zachovává symbol `$` – díky **preserve number format**.

## Běžné úskalí a jak se jim vyhnout

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| Data se změní na velká čísla | `ExportAsString` zůstalo `false` | Nechte `ExportAsString = true` nebo buňky převádějte ručně |
| Chybí záhlaví sloupců | `includeColumnNames` nastaveno na `false` | Nastavte na `true`, když potřebujete **export with column names** |
| Komentáře zmizí | `IncludeCellComments` není povoleno | Zapněte `IncludeCellComments` v `ExportTableOptions` |
| Export špatného listu | Použití `Worksheets[0]` u souboru s více listy | Zadejte název listu: `workbook.Worksheets["Data"]` |
| Výjimka mimo rozsah | `totalRows` překračuje skutečný počet řádků | Použijte `Math.Min(totalRows, worksheet.Cells.MaxDataRow + 1)` |

## Bonus: Export celého listu při zachování formátů

Pokud později rozhodnete, že potřebujete celý list, stačí nahradit `totalRows` a `totalColumns` maximálními rozměry listu:

```csharp
int maxRows = firstWorksheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int maxCols = firstWorksheet.Cells.MaxDataColumn + 1;

DataTable fullTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: maxRows,
    totalColumns: maxCols,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

Nyní máte rutinu **read excel worksheet**, která funguje pro jakoukoli velikost, přičemž stále **preserving number format** a **exporting with column names**.

## Kompletní funkční příklad (připravený ke kopírování‑vkládání)

Níže je kompletní program, který můžete vložit do konzolové aplikace. Obsahuje všechny kroky, importy a jednoduchý výpis pro ověření.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);

            // 2️⃣ Set export options (preserve number format, include comments, export as strings)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                IncludeCellComments = true,
                PreserveNumberFormat = true
            };

            // 3️⃣ Grab the first worksheet (read excel worksheet)
            Worksheet sheet = workbook.Worksheets[0];

            // 4️⃣ Export rows 0‑49, columns 0‑4 (export specific rows) with column headers
            DataTable table = sheet.Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: 50,
                totalColumns: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // 5️⃣ Show a preview
            Console.WriteLine("=== Exported DataTable Preview ===");
            foreach (DataRow row in table.Rows)
            {
                Console.WriteLine(string.Join("\t", row.ItemArray));
            }

            // Keep console open
            Console.WriteLine("\nExport complete. Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

Uložte to jako `Program.cs`, spusťte `dotnet run` a měli byste vidět formátovaný náhled ve vašem terminálu.

## Závěr

Právě jsme prošli **how to export excel** data pomocí Aspose.Cells, pokrývající vše od načtení sešitu po zachování formátu čísel, export se jmény sloupců a omezení exportu na konkrétní řádky. Kód je samostatný, plně spustitelný a obsahuje praktické ochrany proti nejčastějším úskalím.

Jste připraveni na další výzvu? Zkuste exportovat přímo do CSV při zachování původního formátování čísel, nebo vložte `DataTable` do kontextu Entity Framework Core pro hromadné vkládání do databáze. Obě situace staví na stejných základech, které jsme zde probírali.

Pokud vám tento průvodce přišel užitečný

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}