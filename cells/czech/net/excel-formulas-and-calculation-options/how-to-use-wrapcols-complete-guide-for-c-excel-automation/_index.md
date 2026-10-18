---
category: general
date: 2026-07-13
description: Jak použít WRAPCOLS v C# k převodu pole na sloupce, aplikaci pole vzorce
  v Excelu a programovému vytvoření sešitu Excel – vše s jasnými kroky.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- convert array to columns
- apply array formula excel
- create excel workbook programmatically
- evaluate excel formula c#
language: cs
lastmod: 2026-07-13
og_description: Jak používat WRAPCOLS v C# vám umožní rychle převést pole na sloupce,
  aplikovat pole vzorce ve stylu Excelu a programově vyhodnotit výsledek.
og_image_alt: Screenshot showing how to use WRAPCOLS formula in a C# generated Excel
  sheet
og_title: Jak používat WRAPCOLS v C# – Rychlé vytváření Excel sešitu
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: How to use WRAPCOLS in C# to convert array to columns, apply array
    formula Excel, and create Excel workbook programmatically—all with clear steps.
  headline: How to Use WRAPCOLS – Complete Guide for C# Excel Automation
  type: TechArticle
- description: How to use WRAPCOLS in C# to convert array to columns, apply array
    formula Excel, and create Excel workbook programmatically—all with clear steps.
  name: How to Use WRAPCOLS – Complete Guide for C# Excel Automation
  steps:
  - name: What if I need more than two columns?
    text: 'Just change the second argument of WRAPCOLS. For example, `=WRAPCOLS({1,2,3,4,5,6},3)`
      would produce three columns:'
  - name: Can I feed a dynamic range instead of a hard‑coded array?
    text: 'Absolutely. You can build the array string programmatically:'
  - name: What about error handling?
    text: 'If the formula is malformed, `Calculate()` will throw a `CellsException`.
      Wrap the calculation in a try/catch block and log the error:'
  - name: Does this work with older Excel versions?
    text: WRAPCOLS was introduced in Excel 365/2021. When you save the file as an
      older `.xls` format, the formula may be lost. Stick to `.xlsx` if you need the
      function to survive outside the C# engine.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Jak používat WRAPCOLS – Kompletní průvodce pro automatizaci Excelu v C#
url: /cs/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat WRAPCOLS – Kompletní průvodce pro automatizaci Excelu v C#

Už jste se někdy zamysleli **jak používat WRAPCOLS**, když potřebujete převést plochý seznam na úhlednou tabulku v souboru Excel generovaném z C#? Nejste v tom sami. Ať už vytváříte reportingový engine, exportujete výsledky průzkumu, nebo si jen hrajete s daty, funkce WRAPCOLS může okamžitě přetvořit pole na požadovaný počet sloupců.  

V tomto tutoriálu vás provedeme celým procesem: od **programatického vytvoření sešitu Excel** po **aplikaci poleové formule ve stylu Excel** a nakonec **vyhodnocení formule v C#**. Na konci budete schopni **převést pole na sloupce** jedním řádkem kódu, bez nutnosti ručního cvičení buňka‑po‑buňce.

> **Co získáte:** spustitelný ukázkový kód, vysvětlení každého kroku, tipy na běžné úskalí a návrhy na rozšíření řešení.

## Požadavky

- .NET 6.0+ (nebo jakékoli aktuální .NET runtime)
- IDE pro C# (Visual Studio, Rider nebo VS Code)
- Knihovna **Aspose.Cells for .NET** (bezplatná zkušební verze funguje dobře) – je to nejjednodušší způsob, jak manipulovat se soubory Excel bez nutnosti mít nainstalovaný Excel.
- Základní znalost syntaxe C# a Excelových vzorců.

Pokud dáváte přednost jiné knihovně (např. EPPlus nebo ClosedXML), základní myšlenky zůstávají stejné – stačí vyměnit volání API.

## Krok 1: Nastavte svůj projekt a přidejte knihovnu pro Excel

Nejprve vytvořte novou konzolovou aplikaci a přidejte Aspose.Cells přes NuGet:

```bash
dotnet new console -n WrapColsDemo
cd WrapColsDemo
dotnet add package Aspose.Cells
```

> **Tip:** Použijte přepínač `--version` pro zamknutí na známou stabilní verzi, např. `Aspose.Cells 24.9`.

Nyní otevřete `Program.cs`. Začneme přidáním požadovaných jmenných prostorů:

```csharp
using System;
using Aspose.Cells;   // Main API for workbook manipulation
```

## Krok 2: Vytvořte nový sešit a cílovou buňku

Dále vytvořte novou instanci sešitu a vyberte buňku, kde bude umístěna formule WRAPCOLS. V Excelu je buňka **A1** řádek 0, sloupec 0.

```csharp
// Step 2.1: Create a new workbook (blank Excel file)
Workbook workbook = new Workbook();

// Step 2.2: Grab the first worksheet (default)
Worksheet sheet = workbook.Worksheets[0];

// Step 2.3: Define the target cell (A1)
Cell targetCell = sheet.Cells[0, 0];
```

Proč to děláme? Objekt `Workbook` je kontejner pro všechny listy, styly a výpočty. Explicitním odkazem na buňku udržujeme kód přehledný a vyhneme se později „magickým číslům“.

## Krok 3: Vložte poleovou formuli WRAPCOLS

Nyní přichází jádro tutoriálu—**jak používat WRAPCOLS**. Funkce přijímá pole a počet sloupců a vrací dvourozměrný rozsah. V syntaxi Excelu to vypadá takto:

```
=WRAPCOLS({1,2,3,4}, 2)
```

To říká Excelu, aby uspořádal čísla 1‑4 do **2 sloupců**, což vede k:

| A | B |
|---|---|
| 1 | 3 |
| 2 | 4 |

Pro vložení této formule z C#:

```csharp
// Step 3: Apply the WRAPCOLS array formula to A1
targetCell.Formula = "=WRAPCOLS({1,2,3,4},2)";
```

Všimněte si, že používáme **řetězec**, který napodobuje to, co byste zadali do řádku s formulí v Excelu. Toto je krok **aplikace poleové formule v Excelu**, a Aspose.Cells ji automaticky považuje za poleovou formuli, protože WRAPCOLS vrací rozsah.

## Krok 4: Vynutí výpočet, aby byla formule vyhodnocena

Excel obvykle přepočítává líně – jen při otevření souboru. Protože chceme výsledek přečíst okamžitě, musíme spustit výpočet:

```csharp
// Step 4: Calculate the workbook so the WRAPCOLS formula resolves
workbook.Calculate();
```

Volání `Calculate()` je akce **vyhodnocení excelové formule v C#**, která nutí engine spočítat každou formuli, včetně našeho pole WRAPCOLS. Bez tohoto volání by `targetCell.Value` bylo stále `null`.

## Krok 5: Získání a ověření výsledku

Po výpočtu sešitu můžeme získat hodnotu(y) z buněk, které pole obsadilo. Levá horní buňka (A1) obsahuje první prvek, sousední buňky zbytek. Přečtěme celý blok 2 × 2:

```csharp
// Step 5: Read the evaluated values from the resulting range
object[,] result = targetCell.GetArrayValue() as object[,];

// Simple sanity check: print the 2x2 matrix to console
if (result != null)
{
    for (int r = 0; r < result.GetLength(0); r++)
    {
        for (int c = 0; c < result.GetLength(1); c++)
        {
            Console.Write($"{result[r, c]}\t");
        }
        Console.WriteLine();
    }
}
else
{
    Console.WriteLine("No array result was returned.");
}
```

Po spuštění programu by konzole měla zobrazit:

```
1   3
2   4
```

Tento výstup potvrzuje, že jsme úspěšně **převáděli pole na sloupce** pomocí WRAPCOLS.

## Krok 6: Uložení sešitu (volitelné, ale užitečné)

Pokud chcete soubor otevřít v Excelu a vidět formuli v reálném čase, stačí jej uložit:

```csharp
// Step 6: Persist the workbook to disk (optional)
workbook.Save("WrapColsDemo.xlsx");
Console.WriteLine("Workbook saved as WrapColsDemo.xlsx");
```

Po otevření souboru se v buňce A1 zobrazí formule WRAPCOLS a pod ní vyplněný dvousloupcový rozsah. Tento krok je užitečný pro ladění nebo pro předání souboru koncovým uživatelům.

## Časté otázky a okrajové případy

### Co když potřebuji více než dva sloupce?

Stačí změnit druhý argument WRAPCOLS. Například `=WRAPCOLS({1,2,3,4,5,6},3)` vytvoří tři sloupce:

| A | B | C |
|---|---|---|
| 1 | 3 | 5 |
| 2 | 4 | 6 |

Aktualizujte řádek v C# odpovídajícím způsobem:

```csharp
targetCell.Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

### Můžu použít dynamický rozsah místo pevně zakódovaného pole?

Určitě. Můžete sestavit řetězec pole programově:

```csharp
int[] numbers = Enumerable.Range(1, 10).ToArray();
string arrayLiteral = "{" + string.Join(",", numbers) + "}";
targetCell.Formula = $"=WRAPCOLS({arrayLiteral},2)";
```

Tímto způsobem můžete **aplikovat poleovou formuli v Excelu** za běhu, což je ideální pro reporty s proměnnou velikostí dat.

### Jak řešit chyby?

Pokud je formule špatně vytvořena, `Calculate()` vyhodí `CellsException`. Zabalte výpočet do bloku try/catch a zaznamenejte chybu:

```csharp
try
{
    workbook.Calculate();
}
catch (CellsException ex)
{
    Console.Error.WriteLine($"Formula evaluation failed: {ex.Message}");
}
```

### Funguje to se staršími verzemi Excelu?

WRAPCOLS byl zaveden v Excel 365/2021. Když soubor uložíte ve starším formátu `.xls`, může se formule ztratit. Používejte `.xlsx`, pokud potřebujete, aby funkce přežila mimo C# engine.

## Kompletní funkční příklad

Spojením všeho dohromady získáte kompletní, připravený program ke zkopírování:

```csharp
using System;
using System.Linq;
using Aspose.Cells;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.Worksheets[0];
            Cell targetCell = sheet.Cells[0, 0];

            // 2️⃣ Build a dynamic array (optional)
            int[] numbers = Enumerable.Range(1, 8).ToArray(); // {1,2,3,4,5,6,7,8}
            string arrayLiteral = "{" + string.Join(",", numbers) + "}";

            // 3️⃣ Apply WRAPCOLS – convert array to columns (2 columns in this case)
            targetCell.Formula = $"=WRAPCOLS({arrayLiteral},2)";

            // 4️⃣ Force calculation – evaluate excel formula c#
            try
            {
                workbook.Calculate();
            }
            catch (CellsException ex)
            {
                Console.Error.WriteLine($"Failed to evaluate formula: {ex.Message}");
                return;
            }

            // 5️⃣ Retrieve the 2‑column result
            object[,] result = targetCell.GetArrayValue() as object[,];
            if (result != null)
            {
                Console.WriteLine("WRAPCOLS result:");
                for (int r = 0; r < result.GetLength(0); r++)
                {
                    for (int c = 0; c < result.GetLength(1); c++)
                    {
                        Console.Write($"{result[r, c]}\t");
                    }
                    Console.WriteLine();
                }
            }

            // 6️⃣ Save the file for visual inspection (optional)
            workbook.Save("WrapColsDemo.xlsx");
            Console.WriteLine("\nWorkbook saved as WrapColsDemo.xlsx");
        }
    }
}
```

Spusťte `dotnet run` a měli byste vidět vytištěnou matici, následovanou potvrzením, že soubor `.xlsx` existuje.

## Shrnutí a další kroky

Probrali jsme **jak používat WRAPCOLS** k **převodu pole na sloupce**, ukázali techniku **aplikace poleové formule v Excelu** z C#, vynutili výpočet pro **vyhodnocení excelové formule v C#** a uložili výsledek pro další zpracování.  

Pokud chcete další informace:

- **Dynamické počty sloupců:** nechte počet sloupců být proměnnou zadanou uživatelem.
- **Styling výstupu:** aplikujte písma, ohraničení nebo podmíněné formátování pomocí Aspose.Cells po výpočtu.
- **Kombinování s dalšími funkcemi:** vnořte WRAPCOLS do `LET` nebo `FILTER`

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Aspose.Cells .NET&#58; How to Create & Style Excel Workbooks Programmatically](/cells/english/net/formatting/aspose-cells-net-create-style-excel-workbooks/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}