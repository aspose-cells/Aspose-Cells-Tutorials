---
category: general
date: 2026-10-04
description: Naučte se, jak pomocí C# zkopírovat kontingenční tabulku z jednoho sešitu
  do druhého. Tento průvodce také popisuje, jak kopírovat řádky, duplikovat kontingenční
  tabulku a efektivně kopírovat oblast v Excelu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- how to copy rows
- duplicate pivot table
language: cs
lastmod: 2026-10-04
og_description: Kopírování kontingenční tabulky v Excelu pomocí C#. Sledujte tento
  kompletní průvodce, jak duplikovat kontingenční tabulky, kopírovat řádky a kopírovat
  oblast v Excelu pomocí Aspose.Cells.
og_image_alt: Screenshot showing a duplicated pivot table in an Excel worksheet after
  using C# code
og_title: Kopírování kontingenční tabulky v Excelu pomocí C# – krok za krokem průvodce
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to copy pivot table from one workbook to another using C#.
    This guide also covers how to copy rows, duplicate pivot table, and copy Excel
    range efficiently.
  headline: How to copy pivot table in Excel with C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak zkopírovat kontingenční tabulku v Excelu pomocí C# a Aspose.Cells
url: /cs/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zkopírovat kontingenční tabulku v Excelu pomocí C# a Aspose.Cells

Pokud potřebujete **copy pivot table** z jednoho sešitu do druhého, tento tutoriál vám ukáže kompletní, spustitelný řešení. Uvidíte přesně, jak načíst zdrojový soubor, definovat oblast, která obsahuje kontingenční tabulku, zkopírovat řádky (včetně definice kontingenční tabulky) a výsledek uložit. Ať už automatizujete reportingovou pipeline nebo vytváříte migrační nástroj, níže uvedené kroky vám umožní duplikovat kontingenční tabulku pomocí několika řádků C#.

Kopírování kontingenční tabulky je víc než kopírování hodnot buněk; podkladová cache a nastavení polí musí být přeneseny společně. Příklad používá knihovnu **Aspose.Cells**, protože automaticky zpracovává metadata kontingenční tabulky, takže nemusíte ručně obnovovat cache. Na konci tohoto průvodce budete schopni **how to copy pivot**, **copy excel range** a **how to copy rows** bezpečně.

## Požadavky

- .NET 6.0 nebo novější nainstalováno (kód také funguje s .NET Framework 4.7+).
- Platná licence Aspose.Cells pro .NET nebo dočasná evaluační licence.
- Dva soubory Excel: `Source.xlsx` obsahující kontingenční tabulku, kterou chcete duplikovat, a prázdná složka, kam bude zapsán `CopyWithPivot.xlsx`.
- Visual Studio 2022 (nebo jakékoli IDE podporující C#).

## Krok 1: Nastavte projekt a přidejte Aspose.Cells

Vytvořte nový konzolový projekt a přidejte NuGet balíček Aspose.Cells:

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
dotnet add package Aspose.Cells
```

Balíček poskytuje třídy `Workbook`, `Worksheet` a `CellArea`, které jsou použity v níže uvedeném kódu.

## Krok 2: Načtěte zdrojový sešit, který obsahuje kontingenční tabulku

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the source workbook that holds the pivot you want to duplicate
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");
```

> **Proč je to důležité:** Načtení sešitu vytvoří v‑paměti reprezentaci všech listů, včetně skrytých cache kontingenčních tabulek. Bez načtení souboru nemůžete odkazovat na oblast kontingenční tabulky.

## Krok 3: Definujte oblast buněk, která zahrnuje kontingenční tabulku

Musíte Aspose.Cells sdělit, které řádky a sloupce patří k kontingenční tabulce. Struktura `CellArea` vám umožňuje specifikovat obdélníkový blok.

```csharp
        // Define the rectangle that encloses the pivot table (adjust as needed)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,      // first row (zero‑based)
            StartColumn = 0,   // first column
            EndRow = 30,       // last row of the pivot
            EndColumn = 10     // last column of the pivot
        };
```

> **Tip:** Pokud si nejste jisti přesnou velikostí, otevřete zdrojový soubor v Excelu, vyberte kontingenční tabulku a poznamenejte oblast zobrazenou v Name Boxu (např. `A1:K31`). Převěďte souřadnice Excelu na indexy začínající od nuly pro kód.

## Krok 4: Vytvořte nový cílový sešit a získejte jeho první list

```csharp
        // Create an empty workbook that will receive the copied pivot
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

> **Proč je tento krok nutný:** Cílový sešit musí existovat, než můžete kopírovat řádky. Aspose.Cells automaticky vytvoří výchozí list, který použijeme jako cíl.

## Krok 5: Zkopírujte řádky (včetně kontingenční tabulky) ze zdroje do cíle

Metoda `CopyRows` kopíruje jak hodnoty buněk, tak podkladovou cache kontingenční tabulky.

```csharp
        // Copy rows from source to destination, preserving the pivot definition
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,      // source cells
            sourceRange.StartRow,                 // first row to copy
            sourceRange.EndRow - sourceRange.StartRow + 1, // number of rows
            destWorksheet.Cells,                  // target cells
            sourceRange.StartRow);                // target start row
```

> **Jak to funguje:**  
> - `CopyRows` přijímá zdrojový list, počáteční řádek a počet řádků ke kopírování.  
> - Také přijímá cílový list a řádek, kde má kopírování začít.  
> - Protože zdrojová oblast zahrnuje kontingenční tabulku, metoda přenáší cache kontingenční tabulky, seznam polí a rozvržení beze změny. Toto je jádro **how to copy pivot** bez ztráty funkčnosti.

### Okrajový případ: kopírování kontingenční tabulky, která se rozprostírá na více listech

Pokud zdrojová data kontingenční tabulky jsou na jiném listu než samotná tabulka, cache se stále kopíruje, protože Aspose.Cells ukládá cache v sešitu, nikoli v listu. Přesto musíte zajistit, aby cílový sešit obsahoval stejnou oblast zdrojových dat; jinak se v kontingenční tabulce zobrazí chyby `#REF!`. V takových případech nejprve zkopírujte oblast zdrojových dat a poté řádky kontingenční tabulky.

## Krok 6: Uložte sešit, který nyní obsahuje zkopírovanou kontingenční tabulku

```csharp
        // Persist the destination workbook to disk
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

Spuštěním programu vznikne `CopyWithPivot.xlsx` s přesnou kopií původní kontingenční tabulky, včetně všech slicerů, filtrů a vypočtených polí.

### Očekávaný výstup

Když otevřete `CopyWithPivot.xlsx`:

- Kontingenční tabulka se zobrazí na stejné pozici (např. A1:K31) jako v `Source.xlsx`.
- Všechny štítky řádků a sloupců, součty a formátování jsou zachovány.
- Obnovení (refresh) kontingenční tabulky ukazuje stejná data jako zdroj, což potvrzuje, že cache byla zkopírována správně.

## Jak kopírovat řádky bez kontingenční tabulky (copy excel range)

Pokud potřebujete pouze **copy excel range** bez jakýchkoli dat kontingenční tabulky, můžete použít stejnou metodu `CopyRows`, ale nasměrovat ji na oblast, která neobsahuje kontingenční tabulku. Například:

```csharp
// Copy a simple data table from rows 5‑15, columns A‑D
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    4,            // start at row 5 (zero‑based)
    11,           // copy 11 rows (5‑15 inclusive)
    destWorksheet.Cells,
    0);           // paste at the top of the destination sheet
```

Toto ukazuje **how to copy rows** pro obecná data, což potvrzuje všestrannost stejného API.

## Duplikovat kontingenční tabulku ve stejném sešitu (alternativní přístup)

Někdy chcete **duplicate pivot table** v rámci stejného sešitu místo vytváření nového souboru. To můžete dosáhnout kopírováním řádků na jiné místo:

```csharp
// Duplicate pivot table to start at row 40 in the same worksheet
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    sourceRange.StartRow,
    sourceRange.EndRow - sourceRange.StartRow + 1,
    destWorksheet.Cells,
    40); // destination start row (zero‑based)
```

Po uložení bude sešit obsahovat dvě identické kontingenční tabulky – užitečné pro srovnání vedle sebe nebo vytvoření záložních kopií.

## Časté úskalí a jak se jim vyhnout

| Úskalí | Proč k tomu dochází | Řešení |
|---------|----------------|-----|
| Kontingenční tabulka zobrazuje `#REF!` po kopírování | Oblast zdrojových dat není v cílovém sešitu přítomna | Nejprve zkopírujte oblast zdrojových dat, nebo použijte `CopyRows` na list se zdrojovými daty před kopírováním kontingenční tabulky |
| Ztráta formátování | Kopírovány byly pouze hodnoty (např. použitím `Copy` místo `CopyRows`) | Vždy používejte `CopyRows`, který zachovává styl, formátování a metadata kontingenční tabulky |
| Neočekávaný posun řádku | Počáteční řádek v cíli neodpovídá počátečnímu řádku ve zdroji | Ověřte, že počáteční řádek `destWorksheet.Cells` odpovídá zamýšlenému umístění |
| Velké sešity způsobují tlak na paměť | `CopyRows` načítá celé listy do paměti | Zpracovávejte kopírování po částech nebo použijte streamingové API při práci s více než 100 000 řádky |

## Kompletní, spustitelný příklad

Níže je kompletní program, který můžete vložit do `Program.cs` a okamžitě spustit (nahraďte `YOUR_DIRECTORY` skutečnou cestou na vašem počítači).

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook containing the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");

        // 2️⃣ Define the area that encloses the pivot (adjust to your sheet)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 30,
            EndColumn = 10
        };

        // 3️⃣ Create the destination workbook (empty) and get its first sheet
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // 4️⃣ Copy rows—including the pivot cache—into the destination
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,
            sourceRange.StartRow,
            sourceRange.EndRow - sourceRange.StartRow + 1,
            destWorksheet.Cells,
            sourceRange.StartRow);

        // 5️⃣ Save the result
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

Spusťte program pomocí `dotnet run`. Po dokončení otevřete `CopyWithPivot.xlsx` a ověřte, že kontingenční tabulka se zobrazí přesně jako ve zdrojovém souboru.

## Závěr

Nyní víte, jak **copy pivot table** z jednoho Excel sešitu do druhého pomocí C# a Aspose.Cells. Průvodce pokryl kompletní workflow – od načtení zdrojového souboru, definování oblasti buněk kontingenční tabulky, kopírování řádků až po uložení cílového sešitu. Také jste se naučili **how to copy rows**, **copy excel range** a **duplicate pivot table** v rámci stejného souboru, plus častá úskalí a tipy na osvědčené postupy.

Jste připraveni na další krok? Zkuste přidat kód, který programově obnoví zkopírovanou kontingenční tabulku, nebo prozkoumejte export kontingenční tabulky do PDF pomocí Aspose.Cells. Experimentujte s různými zdrojovými oblastmi a rychle si osvojíte automatizaci Excelu v .NET.

---

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vlastních projektech.

- [Kopírovat kontingenční tabulku v C# – Kompletní průvodce krok za krokem](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [Vytvořit nový Excel sešit – Kopírovat a duplikovat kontingenční tabulku](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [kopírovat řádky excel – Zachovat kontingenční tabulku při duplikaci řádků](/cells/english/net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}