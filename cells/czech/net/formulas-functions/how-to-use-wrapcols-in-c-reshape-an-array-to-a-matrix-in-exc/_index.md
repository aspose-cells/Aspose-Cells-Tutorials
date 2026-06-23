---
category: general
date: 2026-06-17
description: Jak použít WRAPCOLS v C# k přeformování pole na matici, zapsat maticový
  vzorec do buňky a načíst existující soubory Excel pomocí Aspose.Cells.
draft: false
keywords:
- how to use wrapcols
- reshape array to matrix
- write array formula
- write formula to cell
- load existing excel
language: cs
og_description: Jak použít WRAPCOLS v C# k rychlému převedení pole na matici, zápisu
  maticového vzorce do buňky a práci s existujícími soubory Excel.
og_title: Jak použít WRAPCOLS v C# – Převést pole na matici
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: How to use WRAPCOLS in C# to reshape an array to a matrix, write array
    formula to a cell, and load existing Excel files with Aspose.Cells.
  headline: How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel
  type: TechArticle
- description: How to use WRAPCOLS in C# to reshape an array to a matrix, write array
    formula to a cell, and load existing Excel files with Aspose.Cells.
  name: How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel
  steps:
  - name: 'Optional: Write a Dynamic Array Reference'
    text: 'If you prefer to reference a range instead of a hard‑coded list, you can
      use:'
  - name: 1. What if I need a different number of rows?
    text: '`WRAPCOLS` only takes the column count; the row count is inferred. To force
      a specific row count, you can combine it with `WRAPROWS` or pad the source array
      with empty strings.'
  - name: 2. Does WRAPCOLS work with text values?
    text: 'Absolutely. Replace the numbers with quoted strings:'
  - name: 3. Can I apply formatting to the generated matrix?
    text: 'After calculation, you can style the range programmatically:'
  - name: 4. How do I handle very large arrays?
    text: Aspose.Cells can process tens of thousands of elements, but keep an eye
      on memory. If you hit limits, consider writing the data in chunks or using `Workbook.Settings.MemorySetting
      = MemorySetting.MemoryPreference;`.
  type: HowTo
tags:
- excel
- csharp
- aspose.cells
title: Jak použít WRAPCOLS v C# – Přetvořit pole na matici v Excelu
url: /cs/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat WRAPCOLS v C# – Přetvořit pole na matici v Excelu

Už jste se někdy zamýšleli **jak používat WRAPCOLS** k převodu plochého seznamu čísel na přehlednou tabulku v Excelu? Nejste v tom sami. Ať už vytváříte nástroj pro reportování nebo si jen hrajete s daty, přetvoření pole na matici vám může ušetřit spoustu ručního kopírování‑vkládání.

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který vám ukáže, jak **zapsat pole jako vzorec do buňky**, vypočítat výsledek a dokonce **načíst existující Excel** sešit, pokud je potřeba. Na konci budete mít stabilní úryvek kódu připravený ke kopírování‑vkládání, který funguje s nejnovější verzí Aspose.Cells pro .NET.

## Co se naučíte

- Účel funkce `WRAPCOLS` a kdy se hodí.  
- Jak **přetvořit pole na matici** pomocí jediného vzorce.  
- Krok‑za‑krokem kód k **zapsání vzorce do buňky** a vynucení výpočtu.  
- Volitelné techniky pro **načtení existujícího Excel** souboru před aplikací vzorce.  
- Běžné úskalí a tipy pro rozšíření přístupu na větší datové sady.

Žádná externí dokumentace není potřeba — vše, co potřebujete, je zde.

## Požadavky

- .NET 6.0 nebo novější (kód také funguje na .NET Framework 4.7+).  
- Aspose.Cells pro .NET nainstalováno (`dotnet add package Aspose.Cells`).  
- Základní znalost syntaxe C#; pokud vám nevadí vytvořit konzolovou aplikaci, můžete začít.

> **Tip:** Pokud používáte Visual Studio, povolte *nullable reference types* (`<Nullable>enable</Nullable>`), abyste včas zachytili možné chyby s null.

## Krok 1: Nastavte projekt a importujte jmenné prostory

Nejprve vytvořte nový konzolový projekt (nebo vložte kód do existujícího). Poté přidejte potřebné `using` direktivy, aby kompilátor věděl, kde se nachází `Workbook` a `Worksheet`.

```csharp
using System;
using Aspose.Cells;   // Main library for Excel manipulation

namespace WrapColsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill in the logic in the next steps
        }
    }
}
```

> **Proč je to důležité:** Importování `Aspose.Cells` vám poskytuje přístup k vysoce výkonnému Excel enginu, který vyhodnocuje `WRAPCOLS` bez nutnosti mít nainstalovaný Excel na počítači.

## Krok 2: Vytvořte nebo načtěte sešit

Můžete začít od nuly nebo otevřít existující soubor. Následující úryvek ukazuje obě možnosti; stačí zakomentovat tu, kterou nepotřebujete.

```csharp
// Option A – Create a brand‑new workbook
Workbook workbook = new Workbook();   // starts with a single empty worksheet

// Option B – Load an existing Excel file (useful when you have templates)
// string inputPath = @"C:\Data\input.xlsx";
// Workbook workbook = new Workbook(inputPath);
```

> **Hraniční případ:** Pokud je načítaný soubor chráněn heslem, předávejte heslo jako druhý argument: `new Workbook(path, "password")`.

## Krok 3: Získejte cílový list

Většinou je první list (`Worksheets[0]`) tím, co potřebujete, ale můžete také odkazovat na list podle názvu.

```csharp
Worksheet sheet = workbook.Worksheets[0];               // by index
// Worksheet sheet = workbook.Worksheets["DataSheet"]; // by name (if it exists)
```

## Krok 4: Zapište vzorec WRAPCOLS do buňky

Zde je jádro tutoriálu. `WRAPCOLS` přijímá pole a počet sloupců a poté rozprostře hodnoty po řádcích. Vzorec umístíme do **A1**, aby matice začínala v levém horním rohu.

```csharp
// Write the WRAPCOLS formula that turns {1,2,3,4,5,6} into 2 rows × 3 columns
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

> **Co se děje?**  
> - Syntaxe s kulatými závorkami `{1,2,3,4,5,6}` vytváří inline konstantu pole.  
> - Druhý argument (`3`) říká Excelu, aby vytvořil tři sloupce a automaticky zabalil zbývající položky do nových řádků.  
> - Protože používáme Aspose.Cells, vzorec je uložen přesně tak, jak byste jej napsali v Excelu, a engine jej vyhodnotí na požádání.

### Volitelné: Zapsat dynamický odkaz na pole

Pokud dáváte přednost odkazovat na oblast místo pevně zakódovaného seznamu, můžete použít:

```csharp
// Assume B1:B6 already contains numbers you want to reshape
sheet.Cells["A1"].Formula = "=WRAPCOLS(B1:B6,3)";
```

Tímto způsobem se matice automaticky aktualizuje, kdykoli se změní zdrojová oblast.

## Krok 5: Vynutit výpočet a uložit výsledek

Aspose.Cells nevyhodnocuje vzorce, dokud mu to neřeknete. Voláním `Calculate()` se výsledek materializuje a výstup vzorce se změní na skutečné hodnoty v buňkách.

```csharp
// Force calculation so the WRAPCOLS output appears in the sheet
workbook.Calculate();

// Save the workbook – adjust the path as needed
string outputPath = @"C:\Data\output.xlsx";
workbook.Save(outputPath);
```

Když otevřete `output.xlsx` v Excelu, uvidíte:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

To je efekt **přetvoření pole na matici**, který jste chtěli.

## Kompletní funkční příklad

Spojením všech částí dohromady získáte připravený program ke spuštění:

```csharp
using System;
using Aspose.Cells;

namespace WrapColsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a new workbook (or load an existing one)
            Workbook workbook = new Workbook(); // new Workbook(@"C:\Data\input.xlsx");

            // 2️⃣ Get the first worksheet
            Worksheet sheet = workbook.Worksheets[0];

            // 3️⃣ Write the WRAPCOLS formula – reshape {1..6} into 2×3
            sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

            // 4️⃣ Force calculation so the matrix is materialized
            workbook.Calculate();

            // 5️⃣ Save the result
            string outputPath = @"C:\Data\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Spusťte program, otevřete `output.xlsx` a uvidíte matici přesně tak, jak je zobrazena výše.

## Časté otázky a úskalí

### 1. Co když potřebuji jiný počet řádků?

`WRAPCOLS` přijímá pouze počet sloupců; počet řádků je odvozen. Pro vynucení konkrétního počtu řádků můžete kombinovat s `WRAPROWS` nebo doplnit zdrojové pole prázdnými řetězci.

```csharp
// Example: Force 3 rows, 2 columns (will add blanks if needed)
sheet.Cells["A1"].Formula = "=WRAPROWS({1,2,3,4,5,6},3)";
```

### 2. Funguje WRAPCOLS s textovými hodnotami?

Ano. Nahraďte čísla řetězci v uvozovkách:

```csharp
sheet.Cells["A1"].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",\"Apr\",\"May\",\"Jun\"},3)";
```

### 3. Můžu aplikovat formátování na vygenerovanou matici?

Po výpočtu můžete oblast programově naformátovat:

```csharp
Range matrix = sheet.Cells.CreateRange("A1:C2");
Style style = workbook.CreateStyle();
style.Font.Color = System.Drawing.Color.Blue;
style.Font.IsBold = true;
matrix.ApplyStyle(style, new StyleFlag() { Font = true });
```

### 4. Jak zacházet s velmi velkými poli?

Aspose.Cells dokáže zpracovat desítky tisíc prvků, ale sledujte využití paměti. Pokud narazíte na limity, zvažte zápis dat po částech nebo použití `Workbook.Settings.MemorySetting = MemorySetting.MemoryPreference;`.

## Tipy pro produkční kód

- **Ukládejte referenci na list** pokud zapisujete mnoho vzorců ve smyčce; snižuje to režii vyhledávání.  
- **Vypněte automatický výpočet** (`workbook.Settings.CalculateFormulaOnOpen = false;`), když plánujete hromadně zapisovat desítky vzorců, a na konci zavolejte `Calculate()` jednou.  
- **Zabalte operace se soubory do try/catch** pro včasné odhalení chyb oprávnění:

```csharp
try
{
    workbook.Save(outputPath);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
}
```

- **Validujte vstup** před sestavením řetězce vzorce — zejména pokud spojujete hodnoty poskytnuté uživatelem, abyste předešli špatně vytvořeným vzorcům.

## Vizualizace

![Jak použít výsledek WRAPCOLS matice v Excelu](wrapcols-output.png "How to use WRAPCOLS in C# to reshape an array to a matrix")

*Snímek obrazovky ukazuje matici 2 × 3 vytvořenou vzorcem WRAPCOLS.*

## Závěr

Probrali jsme **jak používat WRAPCOLS** v C# od začátku do konce: vytvoření nebo načtení sešitu, zápis pole jako vzorce do buňky, vynucení výpočtu a uložení výsledku. Nyní víte, jak **přetvořit pole na matici**, **zapsat pole jako vzorec** a **načíst existující Excel** soubory — vše pomocí několika řádků čistého, udržovatelného kódu.

Dále můžete zkoumat:

## Co byste se měli naučit dál?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Load Excel Files Efficiently Using Aspose.Cells in .NET](/cells/english/net/workbook-operations/efficient-excel-load-aspose-cells-net/)
- [How to Load and Modify Excel Files Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/workbook-operations/load-modify-excel-aspose-cells-net/)
- [How to Set Language in Excel Files Using Aspose.Cells .NET for Multilingual Support](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}