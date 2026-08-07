---
category: general
date: 2026-08-04
description: Definujte oblast buněk v Aspose.Cells a naučte se, jak efektivně kopírovat
  kontingenční tabulky, kopírovat oblast v Excelu v C# a kopírovat oblast ve stejném
  listu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- define cell area
- how to copy pivot
- copy excel range c#
- copy range same sheet
- aspose.cells copy range
language: cs
lastmod: 2026-08-04
og_description: Definujte oblast buněk v Aspose.Cells a zkopírujte rozsah v Excelu
  v C# při zachování kontingenčních tabulek. Postupujte podle tohoto krok‑za‑krokem
  průvodce pro spolehlivé výsledky.
og_image_alt: Screenshot showing how to define cell area and copy range in Aspose.Cells
og_title: Definovat oblast buněk v Aspose.Cells – kopírovat rozsah Excelu v C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  headline: Define cell area in Aspose.Cells and copy Excel range in C#
  type: TechArticle
- description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  name: Define cell area in Aspose.Cells and copy Excel range in C#
  steps:
  - name: The range A61:J110 contains a copy of the original data.
    text: The range A61:J110 contains a copy of the original data.
  - name: A new pivot table appears at the top of the copied range.
    text: A new pivot table appears at the top of the copied range.
  - name: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
    text: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot tables
title: Definovat oblast buněk v Aspose.Cells a zkopírovat rozsah Excelu v C#
url: /cs/net/range-management/define-cell-area-in-aspose-cells-and-copy-excel-range-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definovat oblast buněk v Aspose.Cells a kopírovat rozsah Excel v C#

Pokud potřebujete **definovat oblast buněk** pro rozsah a poté tento rozsah zkopírovat na stejném listu, tento průvodce vám přesně ukáže, jak to provést pomocí Aspose.Cells pro .NET. Ať už přesouváte zprávu řízenou pivotem nebo duplikujete datový blok, naučíte se celý proces během několika kroků.

Také objevíte **jak kopírovat pivot** tabulky bez ztráty jejich spojení a uvidíte čistý příklad **copy excel range c#**, který funguje ve scénáři **copy range same sheet**. Nepotřebujete žádné externí nástroje – stačí Aspose.Cells a několik řádků C#.

## Co budete potřebovat

- .NET 6.0 nebo novější (kód také funguje s .NET Framework 4.7+)
- Aspose.Cells pro .NET (NuGet balíček `Aspose.Cells`)
- Excel sešitu (`input.xlsx`), který obsahuje pivot tabulku v rozsahu A1:J50
- Vývojové prostředí, např. Visual Studio 2022

## Krok 1: Definovat oblast buněk pro zdrojový rozsah

Prvním úkolem je **definovat oblast buněk**, která představuje blok, který chcete zkopírovat. Aspose.Cells používá strukturu `CellArea`, která ukládá indexy řádků a sloupců začínající od nuly.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Define the source range that contains the pivot table (A1:J50)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 49,       // Row 50
    EndColumn = 9      // Column J
};
```

**Proč je to důležité:** `CellArea` říká Aspose.Cells přesně, na které buňky má působit. Použití indexů začínajících od nuly zabraňuje chybám o jeden řádek/sloupec, které jsou běžné při převodu Excelové notace A1 do kódu.

## Krok 2: Definovat cílovou oblast buněk na stejném listu

Pro **copy range same sheet** musíte také určit, kam mají data dopadnout. Cíl může začínat na libovolném řádku; zde začínáme na řádku 61 (index 60), abychom ponechali prázdný odstup.

```csharp
// Define the destination area on the same sheet (starting at row 61)
CellArea destinationRange = new CellArea
{
    StartRow = 60,     // Row 61
    StartColumn = 0,   // Column A
    EndRow = 109,      // Row 110 (same height as source)
    EndColumn = 9      // Column J (same width as source)
};
```

**Proč je to důležité:** Zrcadlením rozměrů zdroje zajišťujete, že zkopírovaný blok bude přesně pasovat bez oříznutí.

## Krok 3: Kopírovat rozsah při zachování pivot tabulek

Nyní můžete **how to copy pivot** bezpečně. Třída `CopyOptions` obsahuje příznak `CopyPivotTables`, který zachovává definici pivotu, zdroj dat a formátování.

```csharp
// Copy the range while preserving pivot tables
srcWorkbook.Worksheets[0].Cells.CopyRange(
    sourceRange,
    destinationRange,
    new CopyOptions
    {
        CopyPivotTables = true   // Ensure pivot tables are retained
    });
```

**Proč je to důležité:** Bez nastavení `CopyPivotTables = true` by se pivot stal statickým snímkem a ztratil interaktivitu. Tato volba kopíruje podkladovou cache a spojení, takže nový pivot se chová přesně jako originál.

## Krok 4: Uložit sešit

Nakonec zapíšete změny zpět na disk. Výstupní soubor ukazuje, že pivot tabulka byla duplikována na stejném listu.

```csharp
// Save the modified workbook
srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

**Pro tip:** Použijte `srcWorkbook.Save("CopyWithPivot.xlsx", SaveFormat.Xlsx)`, pokud potřebujete vynutit konkrétní formát, zejména při práci se staršími verzemi Excelu.

## Krok 5: Ověřit zkopírovanou pivot tabulku

Otevřete `CopyWithPivot.xlsx` v Excelu a zkontrolujte následující:

1. Rozsah A61:J110 obsahuje kopii původních dat.
2. Nová pivot tabulka se objeví na začátku zkopírovaného rozsahu.
3. Aktualizace pivotu odráží změny ve zdrojových datech, což potvrzuje, že **how to copy pivot** byl úspěšný.

Pokud se pivot neaktualizuje, ujistěte se, že rozsah zdrojových dat v definici pivotu stále ukazuje na původní oblast sešitu. Aspose.Cells automaticky aktualizuje odkaz na zdroj, když je `CopyPivotTables` nastaven na true.

## Okrajové případy a varianty

| Situace | Co změnit |
|-----------|----------------|
| **Kopírovat do jiného listu** | Nahraďte `srcWorkbook.Worksheets[0]` indexem nebo názvem cílového listu a podle toho upravte `destinationRange`. |
| **Kopírovat sloučený blok buněk** | Nastavte `CopyOptions.PasteType = PasteType.All`, aby se zachovaly sloučené buňky a formátování. |
| **Kopírovat pouze hodnoty, ne vzorce** | Použijte `CopyOptions.PasteType = PasteType.Values`, abyste se vyhnuli přenosu vzorců odkazujících na původní list. |
| **Velké rozsahy ( > 10 000 řádků )** | Zvažte použití `Workbook.Copy` pro celé listy ke zlepšení výkonu a poté odstraňte nežádoucí řádky. |

Tyto varianty ukazují, že stejná logika **aspose.cells copy range** může být přizpůsobena mnoha reálným scénářům.

## Kompletní funkční příklad

Níže je kompletní, připravený k spuštění program. Nahraďte `YOUR_DIRECTORY` skutečnou cestou ke složce na vašem počítači.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 1: Define the source cell area (A1:J50)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 49,
            EndColumn = 9
        };

        // Step 2: Define the destination cell area on the same sheet (A61:J110)
        CellArea destinationRange = new CellArea
        {
            StartRow = 60,
            StartColumn = 0,
            EndRow = 109,
            EndColumn = 9
        };

        // Step 3: Copy the range while preserving pivot tables
        srcWorkbook.Worksheets[0].Cells.CopyRange(
            sourceRange,
            destinationRange,
            new CopyOptions { CopyPivotTables = true });

        // Step 4: Save the modified workbook
        srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

**Očekávaný výstup:** Po spuštění programu `CopyWithPivot.xlsx` obsahuje původní data plus identický blok začínající na řádku 61, včetně funkční pivot tabulky.

## Závěr

Nyní víte, jak **define cell area** v Aspose.Cells, **copy excel range c#** a **copy range same sheet** při zachování veškeré funkčnosti pivotu. Tato technika eliminuje chyby při ručním kopírování a škáluje na velké sešity.

Dále prozkoumejte související témata, jako je **how to copy pivot** napříč více listy, nebo použijte **aspose.cells copy range** k duplikaci celých listů s formátováním. Experimentujte s různými nastaveními `CopyOptions`, abyste přizpůsobili chování kopírování potřebám vašeho projektu.

Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}