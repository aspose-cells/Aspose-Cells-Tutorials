---
category: general
date: 2026-10-26
description: Zakázat automatický filtr v Excelu pomocí C#. Tento tutoriál ukazuje,
  jak programově odstranit automatický filtr z tabulky v Excelu a obsahuje kompletní
  funkční příklad.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- disable autofilter in excel
- remove autofilter from excel table
- Excel automation C#
- Aspose.Cells filter handling
- programmatic Excel editing
language: cs
lastmod: 2026-10-26
og_description: Rychle vypněte automatický filtr v Excelu. Postupujte podle tohoto
  návodu, jak odstranit automatický filtr z tabulky v Excelu pomocí C# a Aspose.Cells.
og_image_alt: Screenshot of an Excel worksheet where the autofilter has been disabled
og_title: Zakázat automatický filtr v Excelu pomocí C# – krok za krokem průvodce
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  headline: How to disable autofilter in Excel with C# – complete guide
  type: TechArticle
- description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  name: How to disable autofilter in Excel with C# – complete guide
  steps:
  - name: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
    text: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
  - name: Click any column header – you should **not** see the drop‑down filter arrow.
    text: Click any column header – you should **not** see the drop‑down filter arrow.
  - name: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
    text: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Jak zakázat automatický filtr v Excelu pomocí C# – kompletní průvodce
url: /cs/net/excel-autofilter-validation/how-to-disable-autofilter-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zakázat automatický filtr v Excelu pomocí C# – kompletní průvodce

Pokud potřebujete **zakázat automatický filtr v Excelu**, tento průvodce vám přesně ukáže, jak to provést z C#. Ať už čistíte zprávu před publikací nebo automatizujete pipeline pro export dat, odstranění filtru zajistí, že list zobrazí každý řádek. Také se naučíte, jak **odstranit automatický filtr z Excel tabulky** jedním spolehlivým voláním.

Použijeme populární knihovnu **Aspose.Cells for .NET**, protože funguje bez nutnosti mít nainstalovaný Excel na serveru. Na konci tohoto tutoriálu budete mít samostatnou konzolovou aplikaci, která načte sešit, najde první tabulku a zakáže její automatický filtr. Řešení funguje s .xlsx soubory vytvořenými v Excelu 2007 nebo novějším.

## Co budete potřebovat

| Prerequisite | Why it matters |
|--------------|----------------|
| .NET 6.0 or later | Poskytuje runtime pro C# kód. |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | Umožňuje programový přístup k listům, tabulkám a automatickým filtrům. |
| A sample Excel file (`Sample.xlsx`) that contains at least one table with an autofilter applied | Ukázkový Excel soubor (`Sample.xlsx`), který obsahuje alespoň jednu tabulku s aplikovaným automatickým filtrem. Kód pracuje s první tabulkou; existence tabulky nám umožňuje demonstrovat zakázání filtru. |
| Visual Studio 2022 (or any C# IDE) | Umožňuje snadné sestavení a ladění konzolové aplikace. |

> **Tip:** Pokud dáváte přednost bezplatné alternativě, můžete kód upravit tak, aby používal **ClosedXML** nebo **EPPlus**; základní myšlenka—nastavení vlastnosti `AutoFilter` tabulky na `null`—zůstává stejná.

## Krok 1: Vytvořte nový konzolový projekt

Otevřete terminál nebo příkazový řádek Visual Studio a spusťte:

```bash
dotnet new console -n ExcelFilterDemo
cd ExcelFilterDemo
dotnet add package Aspose.Cells
```

## Krok 2: Načtěte sešit a najděte první list

Prvním logickým krokem je otevřít soubor sešitu. Aspose.Cells načte soubor do objektu `Workbook`, který vám poskytuje přímý přístup k listům a tabulkám.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the Excel file you want to modify
        const string inputPath = "Sample.xlsx";

        // Load the workbook into memory
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **Proč tento krok?** Načtení sešitu je nutné, než můžete manipulovat s jakýmikoli Excel objekty. Použití prvního listu (`Worksheets[0]`) odráží typický scénář, kdy hlavní data jsou na prvním listu.

## Krok 3: Získejte první tabulku definovanou na listu

Excel tabulky (také nazývané ListObjects) jsou kontejnery, které obsahují strukturovaná data. Každá tabulka může mít svůj vlastní automatický filtr. Pro odstranění filtru nejprve potřebujeme odkaz na objekt tabulky.

```csharp
        // Get the first table on the worksheet.
        // If the worksheet has no tables, this will throw an IndexOutOfRangeException.
        Table table = worksheet.Tables[0];
```

> **Hraniční případ:** Pokud sešit může obsahovat listy bez tabulek, zabalte přístup do podmínky `if (worksheet.Tables.Count > 0)`. Tím se zabrání chybám za běhu a řešení bude robustnější.

## Krok 4: Zakázat automatický filtr pro tabulku

Skutečné zakázání je jediný řádek: přiřaďte `null` vlastnosti `AutoFilter` objektu `Table`. Tím se vymaže jakékoli kritérium filtru a odstraní se rozbalovací šipky z řádku záhlaví.

```csharp
        // Disable the autofilter – this clears any applied filter.
        table.AutoFilter = null;
```

Po spuštění tohoto řádku se tabulka chová jako běžný rozsah bez uživatelského rozhraní filtru.

## Krok 5: Uložte upravený sešit

Nakonec zapište změny zpět na disk. Můžete přepsat původní soubor nebo vytvořit nový, aby byl zdroj zachován.

```csharp
        // Save the workbook. Use a new file name to avoid overwriting the original.
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

### Kompletní zdrojový kód

Když spojíme všechny části, kompletní program vypadá takto:

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the original Excel file
        const string inputPath = "Sample.xlsx";

        // Load the workbook
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (worksheet.Tables.Count == 0)
        {
            System.Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Get the first table
        Table table = worksheet.Tables[0];

        // Disable the autofilter – clears any applied filter
        table.AutoFilter = null;

        // Save the modified workbook
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

Spusťte program pomocí `dotnet run`. Po provedení otevřete `Sample_NoFilter.xlsx` v Excelu; uvidíte, že šipky filtrů zmizely a všechny řádky jsou viditelné.

## Ověřte, že automatický filtr skutečně zmizel

1. Otevřete uložený soubor (`Sample_NoFilter.xlsx`) v Microsoft Excel.  
2. Klikněte na libovolné záhlaví sloupce – neměli byste **vidět** rozbalovací šipku filtru.  
3. Pokud stále vidíte šipky, zkontrolujte, že tabulka, kterou jste cílovali, je skutečně ta s filtrem. Všechny tabulky můžete vypsat pomocí:

```csharp
foreach (var tbl in worksheet.Tables)
{
    System.Console.WriteLine($"Table name: {tbl.Name}, Has AutoFilter: {tbl.AutoFilter != null}");
}
```

Výstup v konzoli by měl uvádět `Has AutoFilter: False` pro tabulku, kterou jste upravili.

## Časté úskalí a jak se jim vyhnout

| Příznak | Pravděpodobná příčina | Řešení |
|---------|-----------------------|--------|
| `IndexOutOfRangeException` at `worksheet.Tables[0]` | List nemá žádné tabulky. | Přidejte kontrolu `if (worksheet.Tables.Count == 0)` před přístupem. |
| Saved file still shows filters | Upravili jste špatný list nebo tabulku. | Použijte `wb.Worksheets["SheetName"]` nebo iterujte přes `wb.Worksheets` k nalezení správné tabulky. |
| The program crashes on older .NET versions | Program selhává na starších verzích .NET. | Aktualizujte cílový framework v souboru `.csproj`. |
| NullReferenceException when `table.AutoFilter` is already null | Došlo k NullReferenceException, protože `table.AutoFilter` je již null. | Znovu načtěte sešit nebo před přiřazením zkontrolujte `if (table.AutoFilter != null)`. |

## Rozšíření řešení

Nyní, když víte, jak **zakázat automatický filtr v Excelu**, můžete chtít:

* **Odstranit automatický filtr z Excel tabulky** pouze když je splněna konkrétní podmínka (např. když je nastaven uživatelský příznak). Přidejte `if` podmínku kolem `table.AutoFilter = null;`.
* **Použít nový filtr** programově po vymazání starého, pomocí `table.AutoFilter.Range` a `table.AutoFilter.AddFilterColumn(...)`.
* **Zpracovat více tabulek** ve stejném sešitu pomocí smyčky přes `worksheet.Tables` a zakázat každý filtr.

Tato rozšíření následují stejný vzor ukázaný výše a udržují kód čistý.

## Závěr

Nyní máte stručnou, připravenou pro produkci metodu, jak **zakázat automatický filtr v Excelu** pomocí C#. Načtením sešitu, přístupem k první tabulce a nastavením `table.AutoFilter = null` efektivně **odstraníte automatický filtr z Excel tabulky** bez manuální interakce. Kompletní příklad se zkompiluje, spustí a vytvoří čistý soubor připravený pro další automatizaci nebo distribuci.

Neváhejte experimentovat s dalšími tabulkami, podmíněnou logikou nebo alternativními knihovnami. Pokud narazíte na nějaké hraniční případy, vraťte se k sekci řešení problémů nebo prozkoumejte rozsáhlou dokumentaci Aspose.Cells pro pokročilé zpracování filtrů. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to remove autofilter from Excel tables using C#](/cells/english/net/excel-autofilter-validation/how-to-remove-autofilter-from-excel-tables-using-c/)
- [Clear filter UI in Excel with C# – Remove AutoFilter Button](/cells/english/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/)
- [How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide](/cells/english/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}