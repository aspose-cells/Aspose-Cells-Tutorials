---
category: general
date: 2026-11-19
description: Jak použít wrapcols v C# k zalamování dat v Excelu a rychlému výpočtu
  Excelových vzorců.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- calculate excel formulas
- wrap data in excel
- save excel file c#
- load excel workbook c#
language: cs
lastmod: 2026-11-19
og_description: Jak použít wrapcols v C# k zalamování dat v Excelu. Naučte se počítat
  Excelové vzorce a programově ukládat sešit.
og_image_alt: Screenshot showing wrapped data in an Excel worksheet after applying
  WRAPCOLS
og_title: Jak použít wrapcols v C# – zabalit data v Excelu
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to use wrapcols in C# to wrap data in Excel and calculate Excel
    formulas quickly.
  headline: How to use wrapcols in C# to wrap data in Excel
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Data Wrapping
title: Jak použít wrapcols v C# k zalamování dat v Excelu
url: /cs/net/formatting-rows-and-columns-in-excel/how-to-use-wrapcols-in-c-to-wrap-data-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak použít wrapcols v C# k zalomení dat v Excelu

Pokud potřebujete **how to use wrapcols** přeuspořádat vertikální seznam do více sloupců, tento průvodce vám ukáže přesné kroky. Také se naučíte, jak **calculate Excel formulas**, aby byl výsledek uložen v souboru, který uložíte.

Práce s Excelem z C# často začíná načtením sešitu, aplikací vzorců a nakonec uložením změn. Tento tutoriál pokrývá všechny tyto fáze a zároveň zachovává kód snadno kopírovatelný do vašeho vlastního projektu.

## Co dosáhnete

* Načíst existující soubor `.xlsx` z disku (**load excel workbook c#**).
* Použít funkci `WRAPCOLS` na oblast, čímž efektivně **wrap data in Excel**.
* Vynutit výpočet vzorce (**calculate Excel formulas**).
* Uložit upravený sešit (**save Excel file c#**).

Jedinou podmínkou je odkaz na **Aspose.Cells for .NET** (nebo jakoukoli knihovnu, která podporuje funkci `WRAPCOLS`). Kód funguje s .NET 6+ a Visual Studio 2022, ale jakékoli C# IDE postačí.

## Jak použít wrapcols s Aspose.Cells

Funkce listu `WRAPCOLS` přijímá jednorozměrnou oblast a vrací dvourozměrné pole, které vyplní zadaný počet sloupců. Aspose.Cells vyhodnocuje funkci stejně jako Excel, takže ji můžete použít přímo ve vzorci buňky.

```csharp
using System;
using Aspose.Cells;          // Install-Package Aspose.Cells via NuGet

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook and get the first worksheet
        var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(workbookPath);
        Worksheet ws = wb.Worksheets[0];

        // Step 2: Write the WRAPCOLS formula into a cell
        // This wraps the values from A2:A10 into 3 columns, starting at A1
        ws.Cells["A1"].Formula = "=WRAPCOLS(A2:A10,3)";

        // Step 3: Force calculation so the result becomes a static range
        wb.CalculateFormula();

        // Step 4: Save the workbook so you can open it in Excel
        var outputPath = @"YOUR_DIRECTORY\output.xlsx";
        wb.Save(outputPath);

        Console.WriteLine("Workbook saved to " + outputPath);
    }
}
```

### Proč je každý řádek důležitý

* **Loading the workbook** vám poskytuje živý objektový model, který odráží soubor Excel na disku.  
* **Assigning the formula** do `A1` říká Excelu (nebo Aspose.Cells), aby oblast považoval za dynamické pole.  
* **`CalculateFormula()`** spouští výpočetní engine; bez něj by vzorec zůstal nevyhodnocený, dokud nebude soubor otevřen v Excelu.  
* **Saving** zapíše vypočtené hodnoty zpět do nového souboru, takže zalomená data jsou viditelná pro každého, kdo otevře sešit.

## Programatické výpočty Excel vzorců

Volání `Workbook.CalculateFormula()` je doporučený způsob, jak **calculate Excel formulas**, když potřebujete výsledky okamžitě. Metoda respektuje všechny vestavěné funkce, uživatelem definované funkce a jakékoli externí odkazy, které jsou již vyřešeny.

Pokud máte více listů, které na sobě závisí, můžete také předat objekt `CalculationOptions`, který řídí limity iterací nebo povolí vícevláknové výpočty:

```csharp
var options = new CalculationOptions
{
    // Enable iterative calculation for circular references
    IterativeCalculation = true,
    MaxIterations = 100,
    // Use all available CPU cores
    EnableMultiThreadedCalculation = true
};

wb.CalculateFormula(options);
```

Tento extra krok je volitelný pro jednoduchý příklad `WRAPCOLS`, ale v rozsáhlejších sešitech, kde záleží na výkonu, se stává nezbytným.

## Uložení Excel souboru v C# po zalomení dat

Volání `Workbook.Save()` zapíše celý sešit, včetně nově vytvořeného pole vytvořeného funkcí `WRAPCOLS`. Můžete zvolit kterýkoli z podporovaných formátů (`.xlsx`, `.xls`, `.csv`, atd.):

```csharp
// Save as a standard XLSX file (default)
wb.Save(@"YOUR_DIRECTORY\wrapped.xlsx");

// Save as CSV – only the active sheet is exported
wb.Save(@"YOUR_DIRECTORY\wrapped.csv", SaveFormat.Csv);
```

Krok **save Excel file c#** zajišťuje, že zalomená data přetrvávají, takže při dalším otevření souboru uživatel vidí statickou tabulku místo vzorce.

## Načtení Excel sešitu v C# a příprava listu

Pokud váš zdrojový soubor ještě neobsahuje data, která chcete zalomit, můžete je vytvořit za běhu:

```csharp
// Create a new workbook with a single worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Populate column A with sample values
for (int i = 0; i < 9; i++)
{
    ws.Cells[i + 2, 0].PutValue($"Item {i + 1}");
}
```

Tento úryvek demonstruje **load excel workbook c#** v tom smyslu, že můžete začít s prázdným sešitem, naplnit jej a poté použít `WRAPCOLS`. Stejný vzor funguje, když potřebujete před zalomením importovat data z databáze nebo CSV souboru.

## Profesionální tip: ověření výsledku bez otevření Excelu

Po uložení můžete programově načíst zpět zalomenou oblast a potvrdit, že operace byla úspěšná:

```csharp
// Reload the saved file
Workbook checkWb = new Workbook(@"YOUR_DIRECTORY\output.xlsx");
Worksheet checkWs = checkWb.Worksheets[0];

// Print the first three rows of the wrapped area
for (int row = 0; row < 3; row++)
{
    for (int col = 0; col < 3; col++)
    {
        Console.Write($"{checkWs.Cells[row, col].StringValue}\t");
    }
    Console.WriteLine();
}
```

Konzole by měla zobrazit původní seznam rozdělený do tří sloupců, což potvrzuje, že **wrap data in excel** fungovalo podle očekávání.

## Časté otázky a okrajové případy

| Question | Answer |
|----------|--------|
| *Co když má zdrojová oblast více řádků, než může `WRAPCOLS` vyplnit?* | Funkce pokračuje ve vytváření nových řádků podle potřeby. Počet sloupců zůstává pevný. |
| *Mohu zalomit do jiného počtu sloupců?* | Ano—změňte druhý argument, např. `=WRAPCOLS(A2:A10,5)` pro pět sloupců. |
| *Musím po výpočtu vymazat vzorec?* | Ne, pokud zavoláte `CalculateFormula()`. Funkce vrací statické pole, ale vzorec zůstává v buňce. Pokud chcete čistou hodnotu, zkopírujte oblast a vložte‑hodnoty přes ni. |
| *Bude to fungovat se staršími soubory `.xls`?* | `WRAPCOLS` je funkce dynamického pole zavedena v Excel 365. Starší formáty souborů, které nepodporují dynamická pole, uloží vzorec, ale nemusí správně zobrazit zalomený výsledek. Pro spolehlivé chování použijte `.xlsx`. |

## Závěr

Nyní víte, **how to use wrapcols** v C# k **wrap data in Excel**, jak **calculate Excel formulas** za běhu a jak **save Excel file C#** po transformaci. Kompletní příklad ukazuje načtení sešitu, aplikaci funkce `WRAPCOLS`, vynucení výpočtu a uložení výsledku.

### Další kroky

* Prozkoumejte další funkce dynamických polí, jako jsou `UNWRAPCOLS` nebo `SEQUENCE`.  
* Použijte **Aspose.Cells** k importu dat z databáze a následnému automatickému zalomení.  
* Kombinujte `WRAPCOLS` s podmíněným formátováním pro zvýraznění konkrétních řádků po zalomení.

Neváhejte experimentovat s různými zdrojovými oblastmi, počty sloupců a výstupními formáty. Pokud narazíte na problémy, obvykle pomůže návrat ke kroku **calculate Excel formulas** nebo kontrola nastavení výpočtu sešitu.

--- 

*Obrázek: ![Snímek zalomených dat v Excelu](/images/wrapcols-example.png){.align-center alt="Snímek obrazovky zobrazující zalomená data v listu Excel po aplikaci WRAPCOLS"}*

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak použít WRAPCOLS v C# pro Excel pole a ukládání sešitu](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-in-c-for-excel-arrays-and-workbook-savin/)
- [Jak vytvořit Excel sešit a rozdělit data pomocí WRAPCOLS v C#](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}