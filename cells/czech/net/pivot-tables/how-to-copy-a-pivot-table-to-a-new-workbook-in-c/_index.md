---
category: general
date: 2026-11-16
description: Jak zkopírovat kontingenční tabulku z jednoho souboru Excel do nového
  sešitu pomocí C#. Naučte se načíst sešit, zkopírovat oblast a zachovat kontingenční
  tabulky.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new workbook
- load excel workbook c#
- Aspose.Cells copy pivot
- preserve pivot table C#
- Excel automation C#
language: cs
lastmod: 2026-11-16
og_description: Jak zkopírovat kontingenční tabulku z existujícího sešitu do nového
  sešitu pomocí C#. Sledujte tento kompletní návod, jak načíst Excel sešit, zkopírovat
  oblast a zachovat kontingenční tabulku beze změny.
og_image_alt: how to copy pivot table example in C#
og_title: Jak zkopírovat kontingenční tabulku do nového sešitu v C# – krok za krokem
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  headline: How to copy a pivot table to a new workbook in C#
  type: TechArticle
- description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  name: How to copy a pivot table to a new workbook in C#
  steps:
  - name: Expected output
    text: 'Running the program produces `CopyWithPivot.xlsx`. Opening the file in
      Excel shows:'
  - name: Copying multiple pivot tables
    text: If your source sheet contains several pivots, expand the `CellArea` to cover
      the union of all ranges, or repeat the copy step for each distinct area.
  - name: Preserving styles and conditional formatting
    text: '`CopyRows` copies cell styles automatically. If you need to preserve workbook‑wide
      named styles or custom number formats, call `destWorkbook.Worksheets[0].CopyStyle`
      before saving.'
  - name: Working with large workbooks
    text: For files larger than 100 MB, consider using `Workbook.LoadOptions` with
      the `MemorySetting` set to `MemorySetting.MemoryPreference` to reduce memory
      pressure.
  - name: Next steps
    text: '* Explore **Aspose.Cells** features such as refreshing pivots programmatically.
      * Combine this approach with **ExcelPackage** (EPPlus) if you need an open‑source
      alternative. * Automate copying across multiple sheets by looping through `srcWorkbook.Worksheets`.'
  type: HowTo
- questions:
  - answer: Aspose.Cells can read macro‑enabled files (`.xlsm`), but the macro code
      isn’t copied. The pivot table itself is preserved because it’s part of the worksheet
      XML.
    question: Does this work with macros or VBA‑enabled workbooks?
  - answer: The copy operation includes the cached data only. If the destination workbook
      needs to refresh from the original source, you’ll have to re‑configure the data
      connection manually.
    question: What if the pivot uses an external data source?
  - answer: 'No. A pivot table needs its cache. The most reliable way is to copy the
      rows that contain the cache, as demonstrated. You can later hide those rows
      if you don’t want them visible. ## Conclusion You now know **how to copy pivot
      table** from one Excel file to another using C#. The tutorial covered **l'
    question: Can I copy the pivot without the underlying data rows?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Jak zkopírovat kontingenční tabulku do nového sešitu v C#
url: /cs/net/pivot-tables/how-to-copy-a-pivot-table-to-a-new-workbook-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zkopírovat kontingenční tabulku do nového sešitu v C#

Pokud potřebujete **how to copy pivot table** z jednoho souboru Excel do nového sešitu, tento průvodce vám ukáže přesné kroky. Naučíte se, jak **load excel workbook c#**, definovat zdrojový rozsah a **copy range to new workbook**, přičemž zachováte kontingenční tabulku nedotčenou.

Kopírování kontingenční tabulky je častý požadavek, když chcete znovu použít šablonu zprávy, migrovat data mezi projekty nebo vytvořit odlehčený soubor pro distribuci. Níže uvedený ukázkový kód používá Aspose.Cells, plně spravovanou .NET knihovnu, která funguje bez nainstalovaného Microsoft Office. Na konci tohoto tutoriálu budete mít spustitelný program, který vytvoří nový sešit obsahující původní kontingenční tabulku, připravený k dalšímu zpracování nebo sdílení.

## Požadavky

* .NET 6.0 SDK nebo novější (příklad funguje s .NET Core a .NET Framework)
* Visual Studio 2022 nebo jakýkoli C# editor, který preferujete
* Licence Aspose.Cells pro .NET (bezplatná zkušební verze funguje pro hodnocení)
* Zdrojový soubor Excel (`Source.xlsx`), který obsahuje alespoň jednu kontingenční tabulku

> **Tip:** Pokud používáte bezplatnou zkušební verzi, nastavte licenci v kódu, abyste se vyhnuli vodoznakům při hodnocení.

## Krok 1: Načíst zdrojový sešit (load excel workbook c#)

Prvním krokem je otevřít sešit, který obsahuje kontingenční tabulku. Aspose.Cells načte soubor do paměti a poskytne vám plný přístup k listům, buňkám a objektům kontingenčních tabulek.

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Load the source workbook that contains the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");
```

*Proč je to důležité*: Načtení sešitu je základem pro jakoukoli automatizaci Excelu. Bez platného objektu `Workbook` nemůžete prozkoumat kontingenční tabulku ani zkopírovat její data.

## Krok 2: Definovat oblast buněk, která obklopuje kontingenční tabulku (copy range to new workbook)

Kontingenční tabulka se nachází uvnitř obdélníkové bloky buněk. Musíte tuto oblast specifikovat, aby operace kopírování věděla, co přesunout. Konstruktor `CellArea` používá nulové indexy: `StartRow, StartColumn, EndRow, EndColumn`.

```csharp
        // Define the cell range that encloses the pivot table, e.g., A1:K21
        // Row and column indexes start at 0, so A1 = (0,0)
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21
```

*Proč je to důležité*: Explicitním nastavením rozsahu se vyhnete kopírování nesouvisejících dat a zajistíte, že je zahrnutý cache kontingenční tabulky. Rozsah může být vypočítán dynamicky, pokud potřebujete zpracovat různé velikosti kontingenčních tabulek.

## Krok 3: Vytvořit nový sešit a získat jeho první list

Nyní vytvořte cílový sešit, který přijme zkopírované řádky. Aspose.Cells automaticky přidá výchozí list, který použijeme jako cíl.

```csharp
        // Create a new workbook that will receive the copied range
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Proč je to důležité*: Začátek s čistým sešitem zaručuje, že v souboru bude pouze kontingenční tabulka (a její podpůrné řádky), což udržuje výstup odlehčený.

## Krok 4: Zkopírovat řádky ze zdrojového rozsahu do cílového listu (how to copy pivot table)

Metoda `CopyRows` kopíruje celé řádky, zachovává vzorce, formátování a – zásadně – kontingenční tabulky. Parametry metody jsou: počáteční řádek, koncový řádek, kolekce cílových buněk a index řádku v cíli, kde kopírování začíná (zde `0` pro začátek na první řádku).

```csharp
        // Copy the rows that contain the pivot table.
        // Pivot tables inside the range are preserved automatically.
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);
```

*Proč je to důležité*: Použití `CopyRows` místo kopírování jednotlivých buněk zajišťuje, že cache kontingenční tabulky zůstane propojena se zkopírovanými daty. Aspose.Cells se postará o podkladové XML struktury, takže nemusíte kontingenční tabulku ručně znovu vytvářet.

## Krok 5: Uložit výsledný sešit (copy range to new workbook)

Nakonec zapište nový soubor na disk. Cílový sešit nyní obsahuje identickou kontingenční tabulku, která funguje nezávisle na zdrojovém souboru.

```csharp
        // Save the new workbook with the copied pivot table
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        // Optional: inform the user
        System.Console.WriteLine("Pivot table copied successfully!");
    }
}
```

### Očekávaný výstup

Spuštěním programu vznikne `CopyWithPivot.xlsx`. Otevřením souboru v Excelu se zobrazí:

* Stejný rozvrh kontingenční tabulky jako v `Source.xlsx`
* Všechny řádky zdrojových dat, které byly součástí cache kontingenční tabulky
* Žádné odkazy na původní sešit (kontingenční tabulka funguje offline)

## Řešení běžných variant

### Kopírování více kontingenčních tabulek

Pokud váš zdrojový list obsahuje několik kontingenčních tabulek, rozšiřte `CellArea`, aby pokryl sjednocení všech rozsahů, nebo opakujte krok kopírování pro každou samostatnou oblast.

```csharp
// Example: copy two separate ranges
CellArea firstPivot = new CellArea(0, 0, 20, 10);
CellArea secondPivot = new CellArea(25, 0, 45, 10);

destWorksheet.Cells.CopyRows(firstPivot.StartRow, firstPivot.EndRow, destWorksheet.Cells, 0);
destWorksheet.Cells.CopyRows(secondPivot.StartRow, secondPivot.EndRow, destWorksheet.Cells, 21); // start after first block
```

### Zachování stylů a podmíněného formátování

`CopyRows` automaticky kopíruje styly buněk. Pokud potřebujete zachovat pojmenované styly na úrovni celého sešitu nebo vlastní formáty čísel, zavolejte `destWorkbook.Worksheets[0].CopyStyle` před uložením.

### Práce s velkými sešity

U souborů větších než 100 MB zvažte použití `Workbook.LoadOptions` s nastavením `MemorySetting` na `MemorySetting.MemoryPreference`, aby se snížilo zatížení paměti.

```csharp
LoadOptions loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeSrc = new Workbook(@"bigfile.xlsx", loadOptions);
```

## Kompletní zdrojový kód (připravený ke spuštění)

Níže je kompletní program, včetně `using` direktiv a komentářů. Zkopírujte jej do nového konzolového projektu a nahraďte `YOUR_DIRECTORY` skutečnou cestou ke složce.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source workbook (load excel workbook c#)
        // -------------------------------------------------
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");

        // -------------------------------------------------
        // Step 2: Define the area that contains the pivot table
        // -------------------------------------------------
        // Adjust the indices if your pivot occupies a different range.
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21

        // -------------------------------------------------
        // Step 3: Create the destination workbook
        // -------------------------------------------------
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // -------------------------------------------------
        // Step 4: Copy rows (how to copy pivot table)
        // -------------------------------------------------
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);

        // -------------------------------------------------
        // Step 5: Save the new file (copy range to new workbook)
        // -------------------------------------------------
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        Console.WriteLine("Pivot table copied successfully!");
    }
}
```

Spusťte program (`dotnet run` nebo `Ctrl+F5` ve Visual Studiu). Po dokončení otevřete `CopyWithPivot.xlsx` a ověřte, že kontingenční tabulka se chová přesně jako originál.

## Často kladené otázky

**Q: Funguje to s makry nebo sešity povolenými pro VBA?**  
A: Aspose.Cells dokáže číst soubory s makry (`.xlsm`), ale kód makra není zkopírován. Samotná kontingenční tabulka je zachována, protože je součástí XML listu.

**Q: Co když kontingenční tabulka používá externí zdroj dat?**  
A: Operace kopírování zahrnuje pouze data v cache. Pokud cílový sešit potřebuje obnovit data z původního zdroje, budete muset ručně znovu nastavit datové připojení.

**Q: Můžu zkopírovat kontingenční tabulku bez podkladových řádků s daty?**  
A: Ne. Kontingenční tabulka potřebuje svůj cache. Nejspolehlivější způsob je zkopírovat řádky, které cache obsahují, jak je ukázáno. Později můžete tyto řádky skrýt, pokud je nechcete zobrazovat.

## Závěr

Nyní víte, **how to copy pivot table** z jednoho souboru Excel do druhého pomocí C#. Tutoriál pokryl **load excel workbook c#**, definoval **copy range to new workbook** a použil metodu `CopyRows` z Aspose.Cells k zachování kontingenční tabulky nedotčené. S kompletním, spustitelným příkladem můžete tento vzor začlenit do reportingových pipeline, automatizovaných exportních nástrojů nebo jakéhokoli scénáře, kde kontingenční tabulka musí přecházet mezi sešity.

### Další kroky

* Prozkoumejte funkce **Aspose.Cells**, například programové obnovování kontingenčních tabulek.  
* Kombinujte tento přístup s **ExcelPackage** (EPPlus), pokud potřebujete open‑source alternativu.  
* Automatizujte kopírování napříč více listy pomocí smyčky přes `srcWorkbook.Worksheets`.

Klidně experimentujte s různými rozsahy, přidejte vlastní stylování nebo vložte logiku do větší služby pro zpracování dat. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Create New Workbook in C# – Copy Pivot Table](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)
- [How to copy pivot table in Excel with C# and Aspose.Cells](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/)
- [Copy pivot table to new workbook, export shape to PowerPoint](/cells/english/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}