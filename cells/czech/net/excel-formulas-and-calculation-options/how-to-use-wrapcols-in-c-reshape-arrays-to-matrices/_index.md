---
category: general
date: 2026-05-23
description: Jak použít WRAPCOLS v C# k přeformování 1D pole na 2D matici. Naučte
  se funkci wrap columns, napište vzorec do buňky a snadno převádějte 1D na 2D.
draft: false
keywords:
- how to use wrapcols
- reshape array to matrix
- convert 1d to 2d
- write formula to cell
- wrap columns function
language: cs
og_description: Jak použít WRAPCOLS v C# vám umožní přetvořit jednorozměrné pole na
  dvourozměrnou matici jedním vzorcem. Postupujte podle tohoto průvodce, abyste napsali
  vzorec do buňky a ovládli funkci WRAPCOLS.
og_title: Jak použít WRAPCOLS v C# – Přetvořit pole na matice
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to use WRAPCOLS in C# to reshape a 1D array into a 2D matrix. Learn
    the wrap columns function, write formula to cell, and convert 1d to 2d easily.
  headline: How to Use WRAPCOLS in C# – Reshape Arrays to Matrices
  type: TechArticle
- description: How to use WRAPCOLS in C# to reshape a 1D array into a 2D matrix. Learn
    the wrap columns function, write formula to cell, and convert 1d to 2d easily.
  name: How to Use WRAPCOLS in C# – Reshape Arrays to Matrices
  steps:
  - name: Why this matters
    text: You could try to roll your own matrix logic, but the **wrap columns function**
      already handles edge cases like uneven division and empty inputs. Adding the
      Aspose.Cells NuGet package gives us a clean API to interact with Excel formulas
      directly from C#.
  - name: The core of “how to use WRAPCOLS”
    text: 'The **WRAPCOLS** function takes two arguments: an array (or range) and
      the number of columns you want per row. In our case we’ll reshape the literal
      array `{1,2,3,4,5,6}` into **2 rows × 3 columns**.'
  - name: Expected output
    text: '``` 1 2 3 4 5 6 ```'
  type: HowTo
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Jak použít WRAPCOLS v C# – Přetvořit pole na matice
url: /cs/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-in-c-reshape-arrays-to-matrices/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat WRAPCOLS v C# – Přetvoření polí na matice

Už jste se někdy zamysleli **jak používat WRAPCOLS**, když potřebujete převést plochý seznam čísel na přehlednou tabulku? Nejste sami—mnoho vývojářů narazí na problém, když se snaží převést jednorozměrný seznam na dvourozměrnou mřížku, aniž by psali spoustu smyčkového kódu. Dobrá zpráva? Funkce WRAPCOLS (někdy nazývaná wrap columns function) udělá těžkou práci v jediném řádku a můžete ji vložit přímo do sešitu Excelu z C#.

V tomto tutoriálu projdeme celý proces: od vytvoření sešitu, přes **write formula to cell**, až po **reshape array to matrix**, a nakonec **convert 1d to 2d** pomocí vzorce WRAPCOLS. Na konci budete mít znovupoužitelný úryvek, který funguje s libovolným číselným polem, a pochopíte, proč je funkce wrap columns často čistší alternativou k ručnímu přetváření polí.

## Požadavky

Before we dive in, make sure you have:

* .NET 6.0 nebo novější (kód funguje také na .NET Framework 4.6+)  
* Knihovna **Aspose.Cells for .NET** (zdarma zkušební verze nebo licencovaná kopie) – je to komponenta, která nám poskytuje objekty `Workbook`, `Worksheet` a `Cell` použité níže.  
* Základní znalost syntaxe C#—není vyžadována pokročilá znalost Excelu.

Máte to? Skvělé—ponořme se do toho.

![Výsledná 2x3 matice po použití funkce WRAPCOLS v C# – jak používat WRAPCOLS](https://example.com/images/wrapcols-result.png "Jak používat WRAPCOLS – výsledná 2x3 matice")

## Krok 1: Nastavení projektu a přidání Aspose.Cells

### Proč je to důležité

Můžete se pokusit vytvořit vlastní logiku matic, ale **wrap columns function** již řeší okrajové případy, jako je nerovnoměrné dělení a prázdné vstupy. Přidání NuGet balíčku Aspose.Cells nám poskytuje čisté API pro přímou interakci s Excelovými vzorci z C#.

```bash
dotnet add package Aspose.Cells
```

*Pro tip:* Pokud používáte Visual Studio, klikněte pravým tlačítkem na projekt → **Manage NuGet Packages** → vyhledejte **Aspose.Cells** a nainstalujte nejnovější stabilní verzi.

## Krok 2: Vytvoření nového sešitu (nebo načtení existujícího)

Nyní, když je knihovna na místě, můžeme vytvořit objekt sešitu. Zde se provede krok **write formula to cell**.

```csharp
using Aspose.Cells;

class WrapColsDemo
{
    static void Main()
    {
        // Step 2: Initialize a fresh workbook
        Workbook workbook = new Workbook();          // creates an empty .xls/.xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0]; // grab the first sheet
```

Zde jsme vytvořili zcela nový sešit; můžete také načíst existující soubor pomocí `new Workbook("path/to/file.xlsx")`, pokud potřebujete vložit matici do předem formátované šablony.

## Krok 3: Vložení vzorce WRAPCOLS do buňky

### Jádro „jak používat WRAPCOLS“

Funkce **WRAPCOLS** přijímá dva argumenty: pole (nebo oblast) a počet sloupců, které chcete mít v řádku. V našem případě přetvoříme doslovné pole `{1,2,3,4,5,6}` na **2 řádky × 3 sloupce**.

```csharp
        // Step 3: Write the WRAPCOLS formula into cell A1
        // The formula =WRAPCOLS({1,2,3,4,5,6},3) tells Excel to wrap every 3 items into a new row.
        worksheet.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

Všimněte si, že vzorec odráží to, co byste zadali přímo v Excelu. Umístěním do `Cells[0,0]` (buňka **A1**) **zapíšeme vzorec do buňky** bez jakéhokoli dalšího kódu.

## Krok 4: Vynucení výpočtu, aby se vzorec vyhodnotil

Aspose.Cells nevyhodnocuje vzorce automaticky, pokud mu to neřeknete. Tento krok zajistí, že sešit skutečně obsahuje přetvořenou matici.

```csharp
        // Step 4: Recalculate the workbook so the WRAPCOLS formula runs
        workbook.CalculateFormula();
```

Pokud tento řádek přeskočíte, buňky budou stále zobrazovat text vzorce místo vypočtených hodnot.

## Krok 5: Načtení výsledku zpět (volitelné, ale užitečné pro ověření)

Možná budete chtít potvrdit, že operace **reshape array to matrix** byla úspěšná. Zde je rychlá smyčka, která vypíše výslednou mřížku 2‑by‑3 do konzole.

```csharp
        // Step 5: Output the matrix to the console for verification
        for (int row = 0; row < 2; row++)          // we expect 2 rows
        {
            for (int col = 0; col < 3; col++)      // and 3 columns per row
            {
                var value = worksheet.Cells[row, col].StringValue;
                Console.Write(value + "\t");
            }
            Console.WriteLine();
        }

        // Optional: Save the workbook to disk to see the Excel view
        workbook.Save("WrapColsResult.xlsx");
    }
}
```

### Očekávaný výstup

```
1   2   3
4   5   6
```

Konzole zobrazuje přesně stejný rozvrh, jaký byste viděli v Excelu po spuštění vzorce WRAPCOLS. To je transformace **convert 1d to 2d** v akci.

## Krok 6: Zpracování okrajových případů – Co když délka pole není násobkem počtu sloupců?

Pokud má zdrojové pole například 7 prvků a požádáte o 3 sloupce, WRAPCOLS vytvoří poslední řádek s zbývajícími prvky a zbytek buněk nechá prázdný. Zde je rychlá úprava pro demonstraci:

```csharp
worksheet.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6,7},3)";
workbook.CalculateFormula();
```

Výsledek:

```
1   2   3
4   5   6
7       
```

**wrap columns function** elegantně doplní poslední řádek prázdnými buňkami, takže nebudete potřebovat další kód pro zpracování nesouladu velikostí.

## Krok 7: Použití WRAPCOLS s dynamickými daty

V reálných projektech budete zřídka pole hard‑codovat. Místo toho vytvoříte řetězcovou reprezentaci z kolekce C#:

```csharp
int[] numbers = Enumerable.Range(1, 12).ToArray(); // 1..12
string arrayLiteral = "{" + string.Join(",", numbers) + "}";
int columns = 4; // desired columns per row

worksheet.Cells[0, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
workbook.CalculateFormula();
```

Nyní jste **converted 1d to 2d** pro libovolnou délku a stále získáte stejný čistý výstup matice. Vzorec je vytvořen za běhu, ale podkladová **wrap columns function** zůstává stejná.

## Časté úskalí a profesionální tipy

| Pitfall | Why it Happens | Fix |
|---------|----------------|-----|
| Zapomenutí `workbook.CalculateFormula()` | Aspose.Cells nechává vzorce nevyhodnocené | Vždy zavolejte tuto metodu po nastavení jakéhokoli vzorce |
| Použití ne‑číselného literálu pole | WRAPCOLS očekává čísla nebo řetězce, které lze převést | Ujistěte se, že literál obsahuje pouze čísla (nebo řetězce v uvozovkách) |
| Neúmyslné přepsání existujících dat | Umístění vzorce do buňky, která již obsahuje data | Vyberte prázdnou buňku (např. A1) nebo nejprve vymažte oblast |
| Nesprávné odkazování na index listu | `Worksheets[0]` je první list, ale můžete mít přidané další | Ověřte `worksheet = workbook.Worksheets["SheetName"];` pokud je potřeba |

## Proč WRAPCOLS překonává ruční smyčky

* **Readability** – Jeden řádek vzorce nahrazuje desítky `for` smyček.  
* **Performance** – Nativní engine Excelu je vysoce optimalizovaný pro pole vzorců.  
* **Maintainability** – Budoucí vývojáři okamžitě pochopí záměr: “wrap these values into columns”.  
* **Portability** – Stejný vzorec funguje, pokud exportujete sešit do Google Sheets nebo LibreOffice—nepotřebujete logiku specifickou pro C#.

## Kompletní funkční příklad (připravený ke kopírování a vložení)



## Související tutoriály

- [Jak používat Aspose.Cells pro .NET k zobrazení rozsahů buněk jako popisky dat v grafech](/cells/english/net/charts-graphs/aspose-cells-net-chart-customization-cell-ranges-data-labels/)
- [Jak používat Aspose.Cells pro .NET k seskupování řádků a sloupců v Excelu](/cells/english/net/data-analysis/excel-grouping-aspose-cells-net/)
- [Jak používat funkci Excel IF](/cells/english/java/basic-excel-functions/how-to-use-excel-if-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}