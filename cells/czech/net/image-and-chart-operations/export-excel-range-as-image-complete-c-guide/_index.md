---
category: general
date: 2026-06-08
description: Exportujte oblast Excelu jako obrázek pomocí C# a Aspose.Cells. Naučte
  se, jak uložit list Excelu jako obrázek během několika jednoduchých kroků.
draft: false
keywords:
- export excel range as image
- save excel worksheet as image
- Aspose.Cells image export
- C# Excel automation
- pivot table to image
language: cs
og_description: Exportujte oblast Excelu jako obrázek pomocí C#. Tento tutoriál vám
  ukáže, jak rychle a spolehlivě uložit list Excelu jako obrázek.
og_title: Exportovat oblast Excelu jako obrázek – Kompletní průvodce C#
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Export Excel range as image using C# and Aspose.Cells. Learn how to
    save Excel worksheet as image in just a few simple steps.
  headline: Export Excel Range as Image – Complete C# Guide
  type: TechArticle
- description: Export Excel range as image using C# and Aspose.Cells. Learn how to
    save Excel worksheet as image in just a few simple steps.
  name: Export Excel Range as Image – Complete C# Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - Aspose.Cells
      for .NET ≥ 23.9 (you can grab a free trial from the Aspose website). - A basic
      understanding of C# and file I/O.'
  - name: What the code does
    text: '- `exportRange.ToImage` captures only the cells inside the range (pivot
      table or custom block). - `worksheet.ToImage` captures the *entire* visible
      area of the worksheet, effectively **save excel worksheet as image**.'
  - name: Multiple Pivot Tables
    text: 'If your workbook contains more than one pivot table, you can loop through
      them:'
  - name: Very Large Ranges
    text: 'Exporting a massive range (e.g., thousands of rows) can consume a lot of
      memory. Mitigate this by:'
  - name: Transparent Backgrounds
    text: 'If you need a transparent background (useful for overlaying on web pages),
      set the background color to `Color.Transparent` before export:'
  - name: File Permissions
    text: Make sure the target directory exists and your process has write permission.
      Otherwise `ToImage` throws an `IOException`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- ImageExport
title: Exportovat oblast Excelu jako obrázek – Kompletní průvodce C#
url: /cs/net/image-and-chart-operations/export-excel-range-as-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Excel Range as Image – Complete C# Guide

Už jste někdy potřebovali **export Excel range as image**, ale nebyli jste si jisti, kterou API volání použít? Nejste v tom sami. Ať už vytváříte řídicí panel pro reportování nebo potřebujete snímek kontingenční tabulky pro snímek PowerPointu, převod bloku buněk na PNG je užitečný trik.

V tomto průvodci projdeme samostatný příklad, který nejen **export excel range as image**, ale také vám ukáže, jak **save excel worksheet as image** pro celý list. Žádné externí skripty, jen čisté C# a Aspose.Cells, takže můžete kód zkopírovat a okamžitě vidět výsledek.

## Co se naučíte

- Načíst existující sešit a najít konkrétní rozsah (kontingenční tabulka nebo libovolný blok buněk).  
- Nastavit možnosti exportu obrázku, jako je formát, rozlišení a škálování.  
- Exportovat jediný rozsah do PNG, JPEG nebo BMP.  
- Rozšířit stejnou logiku na **save excel worksheet as image** v jednom řádku.  
- Tipy pro práci s více kontingenčními tabulkami, velkými rozsahy a běžnými úskalími.

### Požadavky

- .NET 6.0 nebo novější (kód také funguje na .NET Framework 4.7+).  
- Aspose.Cells pro .NET ≥ 23.9 (můžete si stáhnout bezplatnou zkušební verzi z webu Aspose).  
- Základní znalost C# a práce se soubory (I/O).  

Pokud je máte, pojďme na to.

## Krok 1: Nastavte projekt a importujte jmenné prostory

Nejprve vytvořte novou konzolovou aplikaci (nebo integrujte kód do jakéhokoli existujícího projektu). Přidejte NuGet balíček Aspose.Cells:

```bash
dotnet add package Aspose.Cells
```

Poté přidejte požadované jmenné prostory do rozsahu:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;   // For ImageOrPrintOptions
using System.Drawing.Imaging; // For ImageFormat enum
```

> **Pro tip:** Uchovávejte své `using` příkazy na začátku souboru; usnadňuje to čtení kódu – zejména když později přidáváte další funkce Aspose.

## Krok 2: Načtěte sešit obsahující cílový rozsah

Potřebujete sešit na disku. Nahraďte `YOUR_DIRECTORY/input.xlsx` skutečnou cestou k vašemu souboru.

```csharp
// Step 2: Load the workbook containing the data you want to capture
Workbook workbook = new Workbook(@"YOUR_DIRECTORY/input.xlsx");

// Quick sanity check – make sure the file loaded correctly
if (workbook == null)
{
    Console.WriteLine("Failed to load workbook. Check the file path.");
    return;
}
```

Proč je tento krok důležitý: objekt `Workbook` je vstupním bodem pro každou operaci Aspose.Cells. Bez něj nemůžete odkazovat na listy, rozsahy ani kontingenční tabulky.

## Krok 3: Identifikujte rozsah k exportu

Máte dva běžné scénáře:

1. **Specifická kontingenční tabulka** – kód, který jste uvedli, používá `PivotTables[0].PivotTableRange`.  
2. **Libovolný blok buněk** – můžete použít `worksheet.Cells.CreateRange("B2:D10")`.

Níže řešíme oba případy, takže si můžete vybrat ten, který vám vyhovuje.

```csharp
// Step 3a: Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Option A: Export the first pivot table's range
Range exportRange;
if (worksheet.PivotTables.Count > 0)
{
    exportRange = worksheet.PivotTables[0].PivotTableRange;
}
else
{
    // Option B: Fallback to a manual range (e.g., B2:D10)
    exportRange = worksheet.Cells.CreateRange("B2:D10");
}
```

> **Proč nejprve kontrolujeme kontingenční tabulky:** Mnoho souborů s reporty spoléhá na dynamická data kontingenčních tabulek. Pokud žádná neexistuje, záložní řešení zajistí, že tutoriál stále funguje.

## Krok 4: Nakonfigurujte možnosti exportu obrázku

Aspose.Cells vám poskytuje detailní kontrolu nad výstupním obrázkem. Nejčastější nastavení jsou formát, rozlišení (DPI) a zda zahrnout mřížku.

```csharp
// Step 4: Set up image export options
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG works well for lossless quality
    HorizontalResolution = 300,      // 300 DPI for crisp prints
    VerticalResolution = 300,
    // Optional: uncomment to hide gridlines
    // IsGridlinesVisible = false
};
```

Můžete přepnout na `ImageFormat.Jpeg` nebo `ImageFormat.Bmp`, pokud váš downstream systém preferuje tyto typy. Nastavení DPI je důležité, když vkládáte obrázek do vysoce rozlišených PDF nebo prezentací.

## Krok 5: Exportujte rozsah (nebo celý list) jako obrázek

Nyní se děje magie. Metoda `ToImage` zapíše vizuální reprezentaci rozsahu přímo na disk.

```csharp
// Step 5a: Export the selected range to an image file
string rangeImagePath = @"YOUR_DIRECTORY/PivotRange.png";
exportRange.ToImage(rangeImagePath, imgOptions);
Console.WriteLine($"Range exported to: {rangeImagePath}");

// Step 5b: If you need to **save excel worksheet as image**, use the worksheet's ToImage overload
string sheetImagePath = @"YOUR_DIRECTORY/FullSheet.png";
worksheet.ToImage(sheetImagePath, imgOptions);
Console.WriteLine($"Worksheet exported to: {sheetImagePath}");
```

### Co kód dělá

- `exportRange.ToImage` zachytí pouze buňky uvnitř rozsahu (kontingenční tabulka nebo vlastní blok).  
- `worksheet.ToImage` zachytí *celou* viditelnou oblast listu, efektivně **save excel worksheet as image**.  

Oba volání respektují nastavení, která jste nastavili dříve – takže získáte PNG soubory s rozlišením 300 DPI.

## Řešení okrajových případů a časté otázky

### Více kontingenčních tabulek

Pokud váš sešit obsahuje více než jednu kontingenční tabulku, můžete je projít v cyklu:

```csharp
for (int i = 0; i < worksheet.PivotTables.Count; i++)
{
    Range ptRange = worksheet.PivotTables[i].PivotTableRange;
    string outPath = $@"YOUR_DIRECTORY/Pivot_{i}.png";
    ptRange.ToImage(outPath, imgOptions);
    Console.WriteLine($"Pivot {i} saved to {outPath}");
}
```

### Velmi velké rozsahy

Exportování masivního rozsahu (např. tisíce řádků) může spotřebovat hodně paměti. Omezte to tím, že:

- Snížíte `HorizontalResolution` / `VerticalResolution`.  
- Exportujete po částech (rozdělením rozsahu na menší bloky).  

### Průhledná pozadí

Pokud potřebujete průhledné pozadí (užitečné pro překrytí na webových stránkách), nastavte barvu pozadí na `Color.Transparent` před exportem:

```csharp
imgOptions.BackgroundColor = System.Drawing.Color.Transparent;
```

### Oprávnění souborů

Ujistěte se, že cílový adresář existuje a váš proces má oprávnění k zápisu. Jinak `ToImage` vyhodí `IOException`.

## Kompletní funkční příklad

Spojením všeho dohromady zde máte připravený konzolový program ke spuštění:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing.Imaging;

namespace ExcelImageExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths for your environment
            string inputPath = @"YOUR_DIRECTORY/input.xlsx";
            string rangeImagePath = @"YOUR_DIRECTORY/PivotRange.png";
            string sheetImagePath = @"YOUR_DIRECTORY/FullSheet.png";

            // Load workbook
            Workbook workbook = new Workbook(inputPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // Determine which range to export
            Range exportRange;
            if (worksheet.PivotTables.Count > 0)
            {
                exportRange = worksheet.PivotTables[0].PivotTableRange;
            }
            else
            {
                exportRange = worksheet.Cells.CreateRange("B2:D10");
            }

            // Configure image options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // Export range as image
            exportRange.ToImage(rangeImagePath, imgOptions);
            Console.WriteLine($"Range exported to: {rangeImagePath}");

            // Export entire worksheet as image
            worksheet.ToImage(sheetImagePath, imgOptions);
            Console.WriteLine($"Worksheet exported to: {sheetImagePath}");
        }
    }
}
```

**Očekávaný výstup** (konzole):

```
Range exported to: YOUR_DIRECTORY/PivotRange.png
Worksheet exported to: YOUR_DIRECTORY/FullSheet.png
```

Otevřete vygenerované PNG soubory a uvidíte pixel‑dokonalý snímek vybraného rozsahu a celého listu.

## Závěr

Právě jsme probrali vše, co potřebujete k **export excel range as image** a také jak **save excel worksheet as image** pomocí Aspose.Cells a C#. Od načtení sešitu po jemné ladění možností obrázku a práci s více kontingenčními tabulkami, kroky jsou jednoduché a plně reprodukovatelné.

Dále můžete:

- Experimentovat s různými hodnotami `ImageFormat` (JPEG, BMP).  
- Kombinovat obrázek s PDF pomocí třídy `Document` pro generování reportů.  
- Automatizovat proces pro dávku souborů ve složce.  

Neváhejte upravit úryvek podle svého pracovního postupu – ať už posíláte obrázky do webového API, vkládáte je do e‑mailů nebo generujete tiskové reporty. Šťastné programování a ať obrázky mluví za vaše data v Excelu!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Export Excel Cells to Image Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Export Excel Workbook As Image Using Aspose Cells For Java](/cells/german/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}