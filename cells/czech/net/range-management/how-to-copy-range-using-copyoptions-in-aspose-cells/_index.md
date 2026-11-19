---
category: general
date: 2026-11-19
description: Naučte se, jak pomocí CopyOptions v Aspose.Cells kopírovat oblast a zachovat
  formátování i kontingenční tabulky při kopírování oblasti Excelu s formátováním.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range using copyoptions
- copy excel range with formatting
- Aspose.Cells copy range
- preserve pivot tables Aspose
- Excel automation C#
language: cs
lastmod: 2026-11-19
og_description: Kopírování rozsahu pomocí CopyOptions v Aspose.Cells vám umožňuje
  duplikovat data Excelu s úplným zachováním formátování a kontingenčních tabulek,
  což umožňuje spolehlivou manipulaci s sešitem.
og_image_alt: Screenshot of C# code that copies an Excel range using Aspose.Cells
  CopyOptions
og_title: Kopírování rozsahu pomocí CopyOptions v Aspose.Cells – krok za krokem
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  headline: How to copy range using CopyOptions in Aspose.Cells
  type: TechArticle
- description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  name: How to copy range using CopyOptions in Aspose.Cells
  steps:
  - name: Why `CopyOptions` matters
    text: '* **Performance** – The library performs a single internal operation rather
      than copying cells one‑by‑one. * **Accuracy** – All visual aspects (fonts, colors,
      borders) survive the move, which eliminates visual drift in generated reports.
      * **Reliability** – Pivot tables remain functional because the'
  - name: What if the destination area overlaps the source?
    text: 'Aspose.Cells throws an `ArgumentException`. To avoid this, calculate a
      destination that does not intersect the source, or copy to a different worksheet:'
  - name: How to copy between different workbooks?
    text: 'Create a second `Workbook` instance for the target file and use the same
      `CopyOptions` object:'
  - name: Does `CopyOptions` also copy merged cells?
    text: Yes. The `CopyStyle` flag includes merged‑cell information. If you need
      finer control, set `options.CopyMergedCells = true` (available in newer versions).
  - name: What about large ranges (thousands of rows)?
    text: The operation is memory‑efficient, but you may want to increase the `WorkbookSettings`
      `MemorySetting` to `MemorySetting.MemoryPreference` for very large files.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak kopírovat oblast pomocí CopyOptions v Aspose.Cells
url: /cs/net/range-management/how-to-copy-range-using-copyoptions-in-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak kopírovat oblast pomocí CopyOptions v Aspose.Cells

Pokud potřebujete **copy range using CopyOptions** v Aspose.Cells, tento průvodce vám přesně ukáže, jak duplikovat blok buněk při zachování veškerého formátování a vložených kontingenčních tabulek. Mnoho vývojářů má potíže se zachováním stylu při přesunu dat mezi listy a třída `CopyOptions` tento problém řeší bez dalších ručních kroků.

V tomto tutoriálu se naučíte:

* Definovat zdrojové a cílové oblasti v Excel sešitu.  
* Použít `CopyOptions` k zachování formátování buněk, šířek sloupců a kontingenčních tabulek.  
* Uložit výsledek do nového souboru připraveného pro další zpracování.

Příklad funguje s libovolným souborem `.xlsx` a vyžaduje pouze knihovnu Aspose.Cells pro .NET.

## Požadavky

Než začnete, ujistěte se, že máte:

* .NET 6.0 nebo novější nainstalovaný.  
* Platnou licenci Aspose.Cells pro .NET (nebo bezplatný evaluační klíč).  
* Visual Studio 2022 nebo libovolné C# IDE podle vašeho výběru.  

Žádné další NuGet balíčky nejsou potřeba nad rámec `Aspose.Cells`.

## Krok 1: Nastavení projektu a import jmenných prostorů

Vytvořte novou konzolovou aplikaci a přidejte odkaz na Aspose.Cells:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Your code will go here
        }
    }
}
```

Direktiva `using Aspose.Cells;` vám poskytne přístup k `Workbook`, `CellArea` a `CopyOptions`.

## Krok 2: Načtení sešitu, který chcete upravit

```csharp
// Step 2: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

`Workbook` představuje celý Excel soubor. Nahraďte `YOUR_DIRECTORY` složkou, která obsahuje váš zdrojový soubor.

## Krok 3: Definování zdrojových a cílových oblastí

```csharp
// Step 3: Define the source range (A1:H30)
CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");

// Step 3b: Define the destination range (A35:H64)
CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");
```

`CellArea.CreateCellArea` vytvoří obdélníkovou oblast na základě adresy levého horního a pravého dolního rohu. Souřadnice můžete upravit tak, aby odpovídaly velikosti bloku, který chcete kopírovat.

## Krok 4: Kopírování oblasti při zachování formátování a kontingenčních tabulek

```csharp
// Step 4: Copy the range using CopyOptions
CopyOptions options = new CopyOptions
{
    // Preserve all cell styles, number formats, and column widths
    CopyStyle = true,
    // Keep formulas unchanged (they will still reference the original sheet)
    CopyFormula = true,
    // Preserve any pivot tables that intersect the copied area
    CopyPivotTables = true,
    // Retain data validation and conditional formatting
    CopyDataValidation = true,
    CopyConditionalFormatting = true
};

workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
```

Objekt `CopyOptions` říká Aspose.Cells, co má zachovat. Nastavení `CopyPivotTables = true` je klíčové pro **copy range using CopyOptions**, když váš zdroj obsahuje kontingenční tabulky. Ostatní příznaky zajišťují, že **copy excel range with formatting** je dosaženo automaticky – není potřeba žádný další kód pro opětovné aplikování stylů po kopírování.

### Proč je `CopyOptions` důležitý

* **Výkon** – Knihovna provádí jedinou interní operaci místo kopírování buněk po jedné.  
* **Přesnost** – Všechny vizuální aspekty (písma, barvy, ohraničení) přežijí přesun, což eliminuje vizuální odchylky v generovaných zprávách.  
* **Spolehlivost** – Kontingenční tabulky zůstávají funkční, protože jejich cache a zdrojové odkazy jsou duplikovány.

## Krok 5: Uložení upraveného sešitu

```csharp
// Step 5: Save the workbook with the copied range
workbook.Save("YOUR_DIRECTORY/output.xlsx");
Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
```

Po zavolání `Save` soubor `output.xlsx` obsahuje původní data plus duplikovaný blok na cílovém místě, kompletně s formátováním a kontingenčními tabulkami.

## Kompletní zdrojový kód pro referenci

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // Define source and destination ranges
            CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");
            CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");

            // Configure copy options to preserve everything
            CopyOptions options = new CopyOptions
            {
                CopyStyle = true,
                CopyFormula = true,
                CopyPivotTables = true,
                CopyDataValidation = true,
                CopyConditionalFormatting = true
            };

            // Perform the copy operation
            workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);

            // Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");
            Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
        }
    }
}
```

Spuštěním tohoto programu se vypíše:

```
Range copied successfully. Output saved to output.xlsx
```

Otevřete `output.xlsx` v Excelu – uvidíte blok A1:H30 duplikovaný v A35:H64, se všemi barvami buněk, ohraničením, číselnými formáty a případnými kontingenčními tabulkami zachovanými.

## Často kladené otázky a řešení okrajových případů

### Co když se cílová oblast překrývá se zdrojovou?

Aspose.Cells vyhodí `ArgumentException`. Abyste tomu předešli, vypočítejte cílovou oblast, která se se zdrojovou nekříží, nebo kopírujte do jiného listu:

```csharp
Worksheet destSheet = workbook.Worksheets.Add("CopySheet");
destSheet.Cells.CopyRange(sourceRange, CellArea.CreateCellArea("A1", "H30"), options);
```

### Jak kopírovat mezi různými sešity?

Vytvořte druhou instanci `Workbook` pro cílový soubor a použijte stejný objekt `CopyOptions`:

```csharp
Workbook target = new Workbook();
target.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
target.Save("target.xlsx");
```

### Kopíruje `CopyOptions` také sloučené buňky?

Ano. Příznak `CopyStyle` zahrnuje informace o sloučených buňkách. Pokud potřebujete jemnější kontrolu, nastavte `options.CopyMergedCells = true` (k dispozici v novějších verzích).

### Co s velkými oblastmi (tisíce řádků)?

Operace je paměťově úsporná, ale můžete zvýšit nastavení `WorkbookSettings` `MemorySetting` na `MemorySetting.MemoryPreference` pro velmi velké soubory.

## Profesionální tipy

* **Znovu použijte stejnou instanci `CopyOptions`** pro více kopií – snižuje to režii alokace objektů.  
* **Validujte oblasti** před kopírováním: `if (!CellArea.IsValid(sourceRange) || !CellArea.IsValid(destinationRange))` pomáhá zachytit chyby způsobené překlepy již včas.  
* **Vypněte výpočty** (`workbook.Settings.CalcMode = CalculationMode.Manual`) během kopírování velkých datových sad pro zrychlení procesu, poté po kopírování zavolejte `workbook.CalculateFormula()`, pokud potřebujete aktualizované výsledky.

## Závěr

Nyní víte, jak **copy range using CopyOptions** v Aspose.Cells, čímž dosáhnete plného **copy excel range with formatting** při zachování kontingenčních tabulek a dalších pokročilých funkcí. Tento přístup eliminuje ruční opětovné aplikování stylů a zajišťuje, že vaše Excel automatizace zůstane robustní a udržovatelná.

Další kroky, které můžete prozkoumat:

* Použít `CopyOptions` k duplikaci celých listů.  
* Kombinovat operaci kopírování s `WorksheetCollection.AddCopy` pro generování reportů na základě šablon.  
* Integrovat kód do ASP.NET Core API pro poskytování Excel transformací za běhu.

Neváhejte experimentovat s různými souřadnicemi zdroje/cíle a sdílet své výsledky v komentářích!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, která vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Excel Aspose Cells Dotnet Copy Range Data](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/french/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}