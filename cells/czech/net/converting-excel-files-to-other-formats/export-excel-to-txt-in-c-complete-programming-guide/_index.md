---
category: general
date: 2026-08-11
description: Exportujte Excel do txt v C# s podrobným návodem. Naučte se, jak převést
  xlsx na prostý text pomocí Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- convert xlsx to plain text
- how to export excel worksheet as text
- export worksheet as text file
language: cs
lastmod: 2026-08-11
og_description: Exportovat Excel do txt v C# rychle. Tento tutoriál ukazuje, jak převést
  xlsx na prostý text, nastavit formáty a pracovat s velkými listy.
og_image_alt: Code snippet that exports an Excel worksheet to a plain text file using
  C#
og_title: Export Excel do txt v C# – krok za krokem průvodce pro vývojáře
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  headline: Export excel to txt in C# – complete programming guide
  type: TechArticle
- description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  name: Export excel to txt in C# – complete programming guide
  steps:
  - name: – load the workbook
    text: '```csharp using Aspose.Cells;'
  - name: – get the first worksheet
    text: '```csharp Worksheet sheet = workbook.Worksheets[0]; ```'
  - name: – define export options for text conversion
    text: '```csharp ExportTableOptions exportOptions = new ExportTableOptions { ExportAsString
      = true, // Export all values as text DateTimeFormat = "yyyy-MM-dd", // Desired
      date format NumberFormat = "#,##0.00" // Desired numeric format }; ```'
  - name: – export worksheet as text file
    text: '```csharp // Apply the options to the worksheet sheet.ExportTableOptions
      = exportOptions;'
  type: HowTo
tags:
- excel
- csharp
- text export
- aspose.cells
title: Export Excel do TXT v C# – kompletní programovací průvodce
url: /cs/net/converting-excel-files-to-other-formats/export-excel-to-txt-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Excel do txt v C# – kompletní programovací průvodce

Pokud potřebujete **exportovat excel do txt**, můžete dosáhnout výsledku pomocí několika řádků C# kódu. Tento průvodce ukazuje, jak převést sešit `.xlsx` do souboru prostého textu při zachování definovaného formátu dat.

Exportování listů jako textových souborů je běžná požadavek, když podřadné systémy přijímají pouze oddělená data nebo když potřebujete auditovat surové hodnoty buněk. V následujících sekcích se naučíte, jak nastavit formáty data a čísel, pracovat s velkými listy a vyhnout se typickým úskalím.

## Požadavky pro převod xlsx na prostý text

Před zahájením se ujistěte, že máte:

* .NET 6.0 (nebo novější) nainstalovaný – kód cílí na .NET Standard 2.0, takže funguje také s .NET Framework 4.6+.
* Licenci pro **Aspose.Cells** (bezplatná zkušební verze funguje pro testování).
* IDE, například Visual Studio 2022 nebo Visual Studio Code.
* Soubor Excel pojmenovaný `input.xlsx` umístěný ve složce, na kterou můžete odkazovat z vašeho projektu.

Tyto položky jsou jedinými externími požadavky; tutoriál nezávisí na dalších balíčcích NuGet.

## Jak exportovat excel do txt pomocí Aspose.Cells

Aspose.Cells poskytuje třídu `ExportTableOptions`, která vám umožňuje řídit, jak jsou hodnoty buněk vykresleny jako řetězce. Nastavením `ExportAsString` na `true` vynutíte, aby každá buňka byla zapsána jako text, což je nezbytné, když chcete deterministický výstup prostého textu.

### Krok 1 – načtení sešitu

```csharp
using Aspose.Cells;

string inputPath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(inputPath);
```

*Konstruktor `Workbook` načte soubor Excel do paměti. Pokud soubor neexistuje, je vyvolána výjimka, takže můžete chtít tento volání zabalit do bloku try‑catch pro produkční kód.*

### Krok 2 – získání prvního listu

```csharp
Worksheet sheet = workbook.Worksheets[0];
```

*Listy jsou indexovány od nuly, takže index 0 odkazuje na první kartu. Můžete nahradit index názvem listu (`workbook.Worksheets["Sheet1"]`), pokud potřebujete cílit na konkrétní kartu.*

### Krok 3 – definování možností exportu pro převod textu

```csharp
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,               // Export all values as text
    DateTimeFormat = "yyyy-MM-dd",       // Desired date format
    NumberFormat   = "#,##0.00"          // Desired numeric format
};
```

*`ExportAsString` zajišťuje, že každá buňka, bez ohledu na svůj původní typ, se v výstupním souboru stane řetězcem. Vlastnosti `DateTimeFormat` a `NumberFormat` vám umožňují řídit, jak se zobrazují data a čísla, což je klíčové, když **převádíte xlsx na prostý text** pro systémy, které očekávají konkrétní vzor.*

### Krok 4 – export listu jako textový soubor

```csharp
// Apply the options to the worksheet
sheet.ExportTableOptions = exportOptions;

// Export the data to a tab‑delimited text file
string outputPath = @"YOUR_DIRECTORY\Exported.txt";
sheet.ExportDataTable(outputPath);
```

*`ExportDataTable` zapisuje obsah listu do prostého textového souboru pomocí vámi zadaných možností. Výchozí oddělovač je znak tabulátoru (`\t`). Pokud potřebujete jiný oddělovač, můžete použít přetížení, které přijímá instanci `ExportTableOptions`, a specifikovat `ExportTableOptions.Separator`. Výsledný soubor lze otevřít v libovolném textovém editoru nebo importovat do databáze.*

#### Očekávaný výstup

Assume `input.xlsx` contains:

| A            | B       | C          |
|--------------|---------|------------|
| 2023‑05‑01   | 1234.5  | Ukázkový text|

S výše uvedenými možnostmi bude soubor `Exported.txt` obsahovat:

```
2023-05-01	1,234.50	Sample text
```

Každý sloupec je oddělen tabulátorem, data mají formát `yyyy‑MM‑dd` a čísla používají čárku jako oddělovač tisíců a dvě desetinná místa.

## Časté úskalí při exportu listu jako textového souboru

| Problém | Proč k tomu dochází | Jak tomu předejít |
|-------|----------------|-----------------|
| Formátování čísel závislé na místním nastavení | Výchozí formát respektuje nastavení OS, což může způsobit nekonzistentní použití čárek nebo teček. | Explicitně nastavte `NumberFormat` v `ExportTableOptions`. |
| Skryté řádky nebo sloupce se objevují ve výstupu | Aspose.Cells exportuje celý použitý rozsah, včetně skrytých řádků. | Nastavte `ExportTableOptions.ExportHiddenRows = false` a `ExportHiddenColumns = false`, pokud je chcete přeskočit. |
| Velké listy způsobují tlak na paměť | Celý sešit je načten do paměti před exportem. | Použijte `Workbook.LoadOptions` s `LoadDataOnly = true` ke snížení využití paměti, nebo zpracovávejte soubor po částech. |
| Buňky s daty uložené jako text ve zdrojovém souboru | Pokud buňka již obsahuje formátovaný řetězec, exportér ji považuje za text a ignoruje `DateTimeFormat`. | Ujistěte se, že zdrojový sešit ukládá data jako správné typy Excel data. |

Řešení těchto problémů činí proces **jak exportovat excel list jako text** spolehlivým napříč různými prostředími.

## Rozšíření řešení – vlastní oddělovače a streamovací export

Pokud potřebujete soubor s hodnotami oddělenými čárkou (CSV) místo souboru odděleného tabulátorem, upravte možnosti:

```csharp
exportOptions.Separator = ',';
exportOptions.ExportHiddenRows = false;   // optional
exportOptions.ExportHiddenColumns = false; // optional
sheet.ExportTableOptions = exportOptions;
sheet.ExportDataTable(@"YOUR_DIRECTORY\Exported.csv");
```

Pro soubory větší než 500 MB zabraňuje streamování výstupu aplikaci v vyčerpání RAM:

```csharp
using (FileStream stream = new FileStream(@"YOUR_DIRECTORY\LargeExport.txt",
                                          FileMode.Create,
                                          FileAccess.Write,
                                          FileShare.None,
                                          bufferSize: 81920,
                                          useAsync: true))
{
    sheet.ExportDataTable(stream, exportOptions);
}
```

Přetížení, které přijímá `Stream`, zapisuje řádky postupně, což je ideální pro dávkové úlohy nebo webové služby, které vracejí textový soubor přímo klientovi.

## Ověření výsledku programově

Po dokončení exportu můžete načíst první řádek zpět do paměti a potvrdit formát:

```csharp
string firstLine = File.ReadLines(outputPath).First();
Console.WriteLine($"First line: {firstLine}");
```

Spuštěním tohoto úryvku by se měla vytisknout stejná řádka, jaká je uvedena v sekci *Očekávaný výstup*, což vám poskytne jistotu, že převod byl úspěšný.

## Shrnutí kompletního kódu

Složení všech částí dohromady poskytne samostatný program, který můžete zkopírovat do konzolové aplikace:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputPath  = @"YOUR_DIRECTORY\input.xlsx";
        string outputPath = @"YOUR_DIRECTORY\Exported.txt";

        // Load workbook
        Workbook workbook = new Workbook(inputPath);
        Worksheet sheet = workbook.Worksheets[0];

        // Configure export options
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            DateTimeFormat = "yyyy-MM-dd",
            NumberFormat   = "#,##0.00",
            Separator      = '\t' // tab delimiter
        };

        // Apply options and export
        sheet.ExportTableOptions = exportOptions;
        sheet.ExportDataTable(outputPath);

        // Simple verification
        string firstLine = File.ReadLines(outputPath).First();
        Console.WriteLine($"Export completed. First line: {firstLine}");
    }
}
```

Zkompilujte a spusťte program; soubor `Exported.txt` se objeví ve stejném adresáři jako zdrojový sešit.

## Další kroky a související témata

* **Export worksheet as text file** – experimentujte s různými oddělovači, kódováními (UTF‑8 vs. ASCII) a styly konců řádků pro multiplatformní kompatibilitu.
* **Bulk conversion** – projděte `workbook.Worksheets` a vygenerujte samostatný textový soubor pro každou kartu.
* **Integration with databases** – přesměrujte vygenerovaný text přímo do operace hromadného vkládání pro SQL Server nebo PostgreSQL.
* **

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to Export Excel Files in .NET Using Aspose.Cells&#58; A Comprehensive Guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [How to Export Visible Excel Rows Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}