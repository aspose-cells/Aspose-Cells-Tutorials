---
category: general
date: 2026-10-01
description: Rychle vytvořte Excel sešit v C#, naučte se nastavit vzorec, vypočítat
  kotangens a použít funkci PI v Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- how to calculate cot
- set formula in cell
- write formula to cell
- how to use pi function
language: cs
lastmod: 2026-10-01
og_description: Vytvořte Excel sešit v C# pomocí Aspose.Cells. Naučte se nastavit
  vzorec, použít funkci PI a vypočítat kotangens během několika kroků.
og_image_alt: Diagram showing an Excel workbook created in C# with a formula in cell
  A1
og_title: Vytvořte Excel sešit v C# – nastavte vzorce a vypočítejte kotangens
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create Excel workbook in C# quickly, learn how to set a formula, calculate
    cotangent, and use the PI function in Aspose.Cells.
  headline: How to create Excel workbook in C# and set formulas
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak vytvořit Excel sešit v C# a nastavit vzorce
url: /cs/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-in-c-and-set-formulas/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit Excel sešit v C# a nastavit vzorce

Pokud potřebujete **create Excel workbook C#** kód, který zapíše vzorec do buňky, tento návod vám přesně ukáže, jak na to. Uvidíte, jak nastavit vzorec v listu, použít vestavěnou funkci PI a vypočítat kotangens úhlu – vše pomocí Aspose.Cells.

Tutoriál pokrývá vše od inicializace sešitu až po získání vypočítaného výsledku, takže můžete zkopírovat kompletní příklad do svého projektu bez jakýchkoli chybějících částí.

## Požadavky

* .NET 6.0 nebo novější nainstalovaný  
* Platná licence Aspose.Cells (nebo dočasný evaluační klíč)  
* Visual Studio 2022 nebo jakékoli C# IDE, které preferujete  

Kromě `Aspose.Cells` nejsou vyžadovány žádné další balíčky NuGet.

## Vytvoření Excel sešitu v C#

Prvním krokem je vytvořit novou instanci objektu `Workbook`. Tento objekt představuje celý Excel soubor v paměti a poskytuje vám přístup k jeho listům.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                 // creates an empty .xlsx file
        var worksheet = workbook.Worksheets[0];        // the default first sheet

        // Continue with the rest of the steps...
```

Vytvoření sešitu tímto způsobem zajišťuje, že soubor je připraven k dalším úpravám, jako je přidávání dat, formátování buněk nebo zápis vzorců.

## Nastavení vzorce v buňce pomocí funkce PI

Nyní **write formula to cell** A1. Vzorec používá funkci `PI()`, která poskytuje konstantu π, a funkci `COT` k výpočtu jejího kotangensu.

```csharp
        // Step 2: Set a formula in cell A1 (row 0, column 0)
        // The formula calculates the cotangent of π/4, which equals 1
        worksheet.Cells[0, 0].Formula = "=COT(PI()/4)";

        // Continue with calculation...
```

*Proč je to důležité*: `PI()` je vestavěná Excel funkce, která vrací hodnotu π. Pokud ji vydělíte 4, získáte 45°, a `COT` vrací kotangens tohoto úhlu. Toto demonstruje **how to use pi function** uvnitř Excel vzorce z C#.

## Jak vypočítat kotangens pomocí Aspose.Cells

Pokud se ptáte **how to calculate cot** bez ručního převodu úhlů, funkce `COT` udělá těžkou práci. Přijímá úhel v radiánech, takže jej můžete kombinovat s `PI()` pro běžné úhly.

```csharp
        // Step 3: Recalculate the workbook so the formula is evaluated
        workbook.Calculate();

        // Step 4: Retrieve and display the calculated result
        double result = worksheet.Cells[0, 0].DoubleValue;
        Console.WriteLine($"Cotangent of PI/4 = {result}");
    }
}
```

Spuštěním programu se vypíše:

```
Cotangent of PI/4 = 1
```

Protože `COT(π/4)` se rovná 1, výstup potvrzuje, že vzorec byl správně **set formula in cell** a vyhodnocen.

## Zápis vzorce do buňky – další tipy

* **Multiple formulas**: Můžete přiřadit vzorec libovolné buňce pomocí stejné vlastnosti `Formula`, např. `worksheet.Cells["B2"].Formula = "=SIN(PI()/2)";`.  
* **International settings**: Aspose.Cells respektuje jazykové nastavení sešitu, takže názvy funkcí zůstávají v angličtině (`PI`, `COT`) bez ohledu na regionální nastavení uživatele.  
* **Performance**: Pokud potřebujete nastavit tisíce vzorců, seskupte je a na konci zavolejte `workbook.Calculate()` jednou, abyste se vyhnuli opakovaným přepočtům.

## Kompletní spustitelný příklad

Níže je celý program, který můžete zkopírovat a vložit do konzolového projektu. Obsahuje všechny potřebné `using` direktivy a demonstruje kompletní workflow od vytvoření sešitu až po výstup výsledku.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook and obtain the first worksheet
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // Write a formula that uses the PI function and calculates cotangent
        worksheet.Cells[0, 0].Formula = "=COT(PI()/4)";

        // Force calculation so the formula value is materialized
        workbook.Calculate();

        // Read the calculated value and display it
        double cotValue = worksheet.Cells[0, 0].DoubleValue;
        Console.WriteLine($"Cotangent of PI/4 = {cotValue}");

        // Optional: save the workbook to verify the formula visually
        workbook.Save("CotExample.xlsx");
    }
}
```

**Expected output** při spuštění programu:

```
Cotangent of PI/4 = 1
```

Vygenerovaný soubor `CotExample.xlsx` obsahuje vzorec v buňce A1, což vám umožní otevřít jej v Excelu a vidět stejný výsledek.

## Závěr

Nyní víte, jak **create Excel workbook C#** kód, který zapisuje vzorec, používá funkci `PI` a **calculates cot** pomocí Aspose.Cells. Příklad pokrývá celý životní cyklus: vytvoření sešitu, **set formula in cell**, přepočet a získání výsledku.

Další kroky, které můžete prozkoumat:

* Použijte **write formula to cell** pro složitější výpočty, jako jsou finanční modely.  
* Použijte **set formula in cell** spolu s podmíněným formátováním k zvýraznění výsledků.  
* Kombinujte **how to use pi function** s trigonometrickými grafy pro vědecké zprávy.

Neváhejte experimentovat s různými úhly, funkcemi a rozvržením listů. Ovládnutí práce s vzorci v C# otevírá dveře k plně automatizovaným Excel reportingovým pipelineům. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto návodu. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to Calculate Cotangent in Excel with C# – Create Workbook, Use EXPAND](/cells/english/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/)
- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}