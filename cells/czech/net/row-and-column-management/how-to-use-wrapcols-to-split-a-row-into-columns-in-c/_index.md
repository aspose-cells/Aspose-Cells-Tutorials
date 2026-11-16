---
category: general
date: 2026-11-16
description: Naučte se, jak v C# použít WRAPCOLS k rozdělení řádku na sloupce, automatizaci
  sešitu Excel, výpočtu vzorců a uložení souboru Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split row into columns
- automate excel workbook
- excel formula calculation
- save excel file c#
language: cs
lastmod: 2026-11-16
og_description: Jak použít WRAPCOLS v C# k rozdělení řádku na sloupce, automatizaci
  sešitu Excel, spuštění výpočtu vzorce a uložení souboru Excel.
og_image_alt: Screenshot showing WRAPCOLS function splitting a row into columns in
  an Excel workbook
og_title: Jak použít WRAPCOLS v C# – rozdělit řádky, vypočítat vzorce a uložit soubory
  Excel
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to use WRAPCOLS in C# to split a row into columns, automate
    an Excel workbook, calculate formulas, and save the Excel file.
  headline: How to use WRAPCOLS to split a row into columns in C#
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a row into columns, automate
    an Excel workbook, calculate formulas, and save the Excel file.
  name: How to use WRAPCOLS to split a row into columns in C#
  steps:
  - name: How WRAPCOLS works
    text: '* **Source range** – `A1:T1` contains the original 20 values. * **Column
      count** – `5` tells Excel to create five columns per row. * **Result** – Excel
      fills cells `A2:E5` with the wrapped data automatically.'
  - name: Expected output
    text: 'Open `WrapColsDemo.xlsx` and you’ll see:'
  - name: Next steps
    text: '* Explore other dynamic array functions such as `SEQUENCE`, `FILTER`, and
      `UNIQUE` to enrich your Excel automation toolkit. * Combine `WRAPCOLS` with
      chart generation APIs to produce ready‑to‑publish reports. * Integrate the code
      into a background service that processes CSV uploads and outputs resha'
  type: HowTo
tags:
- Excel automation
- C#
- Aspose.Cells
title: Jak použít WRAPCOLS k rozdělení řádku do sloupců v C#
url: /cs/net/row-and-column-management/how-to-use-wrapcols-to-split-a-row-into-columns-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak použít WRAPCOLS k rozdělení řádku na sloupce v C#

Pokud potřebujete **how to use WRAPCOLS** v projektu C#, tento průvodce vám ukáže kompletní, spustitelné řešení. Uvidíte, jak rozdělit řádek na sloupce, automatizovat sešit Excel, spustit výpočet Excelových vzorců a nakonec uložit soubor Excel ve stylu C#.

Práce s Excelem programově často znamená zpracování velkých datových sad a funkce `WRAPCOLS` vám umožní přetvořit jeden řádek na matici bez ručního cyklování. Níže uvedené kroky pokrývají vše, co potřebujete – od vytvoření sešitu až po finální výstup souboru – takže můžete tuto techniku začlenit do jakékoli aplikace .NET.

## Co tento tutoriál pokrývá

* Vytvoření nového sešitu a přístup k jeho prvnímu listu.  
* Naplnění řádku sekvenčními hodnotami (1‑20).  
* Použití Excelového vzorce `WRAPCOLS` k rozdělení řádku na bloky po 5 sloupcích.  
* Spuštění **excel formula calculation**, aby se výsledek stal součástí listu.  
* Použití **save excel file c#** k zápisu sešitu na disk.  

Žádná externí konfigurace není vyžadována kromě knihovny Aspose.Cells pro .NET (nebo jakéhokoli kompatibilního API podporujícího `WRAPCOLS`). Na konci průvodce budete mít soubor pojmenovaný `WrapColsDemo.xlsx`, který obsahuje čtyři řádky po pěti sloupcích, odvozené z původních jednorázových dat.

## Požadavky

* .NET 6.0 nebo novější (kód také funguje s .NET Core 3.1 a .NET Framework 4.7+).  
* Odkaz na **Aspose.Cells** (k dispozici přes NuGet: `Install-Package Aspose.Cells`).  
* Základní znalost syntaxe C# a Excelových vzorců.  

> **Tip:** Pokud dáváte přednost bezplatné alternativě, open‑source knihovna EPPlus také podporuje vlastní vzorce, ale `WRAPCOLS` je vestavěná pouze v knihovnách, které implementují kompletní výpočetní engine Excelu, jako je Aspose.Cells.

## Krok 1: Vytvořte nový sešit a získejte první list

Prvním krokem je vytvořit objekt `Workbook` a získat jeho výchozí list. Tento objekt představuje celý soubor Excel v paměti.

```csharp
using Aspose.Cells;

...

// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                 // creates an empty workbook
Worksheet sheet = workbook.Worksheets[0];           // the first worksheet (named "Sheet1")
```

Programatické vytvoření sešitu je základem úkolů **automate excel workbook**. Reference `Worksheet` vám umožňuje přímo manipulovat s buňkami.

## Krok 2: Naplňte první řádek hodnotami 1‑20

Dále naplňte buňky `A1` až `T1` čísly od 1 do 20. Jednoduchý `for` cyklus zapíše každou hodnotu do odpovídajícího sloupce.

```csharp
// Step 2: Fill the first row with values 1‑20
for (int col = 0; col < 20; col++)
{
    sheet.Cells[0, col].PutValue(col + 1);   // Row 0 = first row, column index starts at 0
}
```

Proč zapisovat hodnoty programově? Zajišťuje to, že demo funguje na jakémkoli počítači bez ručního zadávání dat, což je nezbytné při **automate excel workbook** generování ve dávkových procesech.

## Krok 3: Použijte funkci WRAPCOLS k rozdělení řádku na bloky po 5 sloupcích

Nyní použijeme Excelový vzorec `WRAPCOLS`. Přijímá zdrojový rozsah a počet sloupců a vrací dvourozměrné pole, které „zabalí“ zdrojová data do zadaného počtu sloupců.

```csharp
// Step 3: Use the WRAPCOLS function to split the row into 5‑column blocks
sheet.Cells["A2"].Formula = "WRAPCOLS(A1:T1,5)";
```

Umístěním vzorce do buňky `A2` řeknete Excelu, aby výstup začal ve druhém řádku. Výsledkem bude matice 4 × 5, protože 20 položek děleno 5 sloupci dává čtyři řádky.

### Jak WRAPCOLS funguje

* **Zdrojový rozsah** – `A1:T1` obsahuje původních 20 hodnot.  
* **Počet sloupců** – `5` říká Excelu, aby vytvořil pět sloupců na řádek.  
* **Výsledek** – Excel automaticky vyplní buňky `A2:E5` zabalenými daty.  

Pokud budete potřebovat **split row into columns** s jinou velikostí bloku, stačí změnit druhý argument. Například `WRAPCOLS(A1:T1,4)` vytvoří pět řádků po čtyřech sloupcích.

## Krok 4: Vypočítejte vzorce, aby byl výsledek WRAPCOLS materializován

Nově přidaný vzorec zůstává nevyhodnocený, dokud se nespustí výpočetní engine. Voláním `CalculateFormula()` zajistíte, že krok **excel formula calculation** zapíše skutečné hodnoty do listu.

```csharp
// Step 4: Calculate formulas so the WRAPCOLS result is materialised
workbook.CalculateFormula();
```

Spuštění výpočtu je klíčové, když později **save excel file c#**, protože uložený soubor musí obsahovat vypočtené hodnoty, ne jen text vzorce. Bez tohoto kroku by výstupní sešit ukazoval `#N/A` nebo surový vzorec místo očekávaných čísel.

## Krok 5: Uložte sešit na disk

Nakonec uložte sešit pomocí metody `Save`. Můžete zadat libovolnou platnou cestu k souboru; příklad používá zástupný adresář, který byste měli nahradit svým vlastním.

```csharp
// Step 5: Save the workbook
string outputPath = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "WrapColsDemo.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Volání `Save` ukazuje **save excel file c#** v nejjednodušší podobě. Aspose.Cells automaticky zvolí formát XLSX podle přípony souboru. Pokud potřebujete starší soubor `.xls`, změňte příslušně příponu.

### Očekávaný výstup

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 2 | 3 | 4 | 5 |
| 6 | 7 | 8 | 9 |10 |
|11 |12 |13 |14 |15 |
|16 |17 |18 |19 |20 |

Původní jediný řádek byl **split row into columns** do čtyř řádků, z nichž každý obsahuje pět sloupců.

## Kompletní zdrojový kód

Spojením všech kroků dohromady získáte kompaktní, samostatný program:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class WrapColsDemo
{
    static void Main()
    {
        // Step 1: Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Step 2: Fill first row with values 1‑20
        for (int col = 0; col < 20; col++)
        {
            sheet.Cells[0, col].PutValue(col + 1);
        }

        // Step 3: Apply WRAPCOLS to split into 5‑column blocks
        sheet.Cells["A2"].Formula = "WRAPCOLS(A1:T1,5)";

        // Step 4: Force calculation so values are materialised
        workbook.CalculateFormula();

        // Step 5: Save the workbook (change the path as needed)
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "WrapColsDemo.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Zkopírujte kód do nového konzolového projektu, obnovte NuGet balíček Aspose.Cells a spusťte. Program vytvoří soubor Excel na vaší ploše během několika sekund.

## Běžné varianty a okrajové případy

| Situation | Adjustment |
|-----------|------------|
| **Různá velikost bloku** | Změňte `WRAPCOLS(A1:T1,5)` na `WRAPCOLS(A1:T1, n)`, kde `n` je požadovaný počet sloupců. |
| **Více zdrojových řádků** | Použijte `WRAPCOLS(A1:A10,5)` k zabalení vertikálního rozsahu do matice s 5 sloupci. |
| **Dynamický zdrojový rozsah** | Sestavte řetězec adresy v C# (`$"A1:{CellIndexToName(0, lastCol)}1"`) před přiřazením vzorce. |
| **Velké listy** | Zavolejte `workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)`, aby se přeskočily buňky způsobující chyby a zlepšil se výkon. |
| **Ukládání jako CSV** | Nahraďte `workbook.Save(outputPath)` za `workbook.Save(outputPath, SaveFormat.Csv)`. |

## Tipy pro řešení problémů

* **Formula not evaluated** – Ujistěte se, že voláte `workbook.CalculateFormula()` *po* nastavení vzorce. Vynechání tohoto kroku ponechá buňku s nevyhodnoceným textem `WRAPCOLS`.  
* **File access denied** – Ověřte, že cílový adresář existuje a že váš proces má oprávnění k zápisu. Použití `Environment.SpecialFolder.Desktop` eliminuje většinu problémů s oprávněními.  
* **Incorrect number of rows** – Dvakrát zkontrolujte druhý argument funkce `WRAPCOLS`. Definuje počet sloupců, ne počet řádků; řádky jsou odvozeny z celkového počtu zdrojových buněk dělených tímto počtem sloupců.

## Závěr

Nyní víte, **how to use WRAPCOLS** v C# k **split row into columns**, plně **automate excel workbook** tvorbu, spustit **excel formula calculation** a **save excel file c#** pomocí jediné čisté kódové základny. Tato technika eliminuje ruční operace kopírování‑vkládání a snadno škáluje pro velké datové transformační pipeline.

### Další kroky

* Prozkoumejte další dynamické pole funkce jako `SEQUENCE`, `FILTER` a `UNIQUE`, abyste rozšířili svůj toolbox pro automatizaci Excelu.  
* Kombinujte `WRAPCOLS` s API pro generování grafů, abyste vytvořili připravené zprávy k publikaci.  
* Integrajte kód do background služby, která zpracovává nahrané CSV soubory a vytváří přetvořené Excel soubory pro následnou analytiku.  

Neváhejte experimentovat s různými zdrojovými rozsahy a počty sloupců – upravte vzorec, znovu spusťte výpočet a sledujte okamžitou aktualizaci sešitu. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [jak použít wrapcols v C# – Kompletní průvodce s Excel WRAPROWS a přepočtem vzorců](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [Jak použít WRAPCOLS – Kompletní průvodce pro C# Excel automatizaci](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)
- [Jak použít WRAPCOLS v C# – Přetvořit pole na matici v Excelu](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}