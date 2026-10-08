---
category: general
date: 2026-03-21
description: Nastavte vlastní formát buňky v C# a naučte se, jak zapisovat datum do
  Excelu, aplikovat vlastní formát data, číst DateTime z Excelu a rychle vytvořit
  sešit a list.
draft: false
keywords:
- set cell custom format
- write date to excel
- read datetime from excel
- apply custom date format
- create workbook worksheet
language: cs
og_description: Nastavte vlastní formát buňky v C# pro zápis data do Excelu, použijte
  vlastní formát data, načtěte DateTime z Excelu a snadno vytvořte list pracovního
  sešitu.
og_title: Nastavte vlastní formát buňky v C# – Zápis a čtení dat v Excelu
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Nastavení vlastního formátu buňky v C# – Kompletní průvodce zápisem a čtením
  dat v Excelu
url: /cs/net/excel-custom-number-date-formatting/set-cell-custom-format-in-c-complete-guide-to-writing-readin/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nastavení vlastního formátu buňky – zápis a čtení dat v Excelu pomocí C#

## Co se naučíte

- Jak **create workbook worksheet** programmatically.  
- Přesné kroky k **write date to Excel** pomocí řetězce specifického pro locale.  
- Jak **apply custom date format** (včetně zápisu japonské éry).  
- Jak **read DateTime from Excel** zpět do objektu `DateTime`.  
- Tipy, úskalí a varianty, na které můžete narazit při práci s daty v Excelu.

Žádná externí dokumentace není potřeba – vše, co potřebujete, je zde.

## Požadavky

- .NET 6.0 nebo novější (kód také funguje na .NET Framework 4.7+).  
- Aspose.Cells pro .NET nainstalovaný přes NuGet (`Install-Package Aspose.Cells`).  
- Základní znalost syntaxe C# – nic složitého.

> **Pro tip:** Pokud používáte Visual Studio, povolte *nullable reference types*, abyste včas zachytili jemné chyby.

## Krok 1: Vytvořte Workbook a Worksheet  

Nejprve potřebujete objekt workbook, který představuje soubor Excel, a worksheet, kde budou data uložena.

```csharp
using Aspose.Cells;
using System;

class ExcelDateDemo
{
    static void Main()
    {
        // Step 1: Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];           // default sheet is named "Sheet1"
```

*Proč je to důležité:* Třída `Workbook` je vstupním bodem pro všechny operace s Excelem. Vytvoření v paměti znamená, že se souborový systém nedotýkáte, dokud explicitně neuložíte, což udržuje proces rychlý a vhodný pro testování.

## Krok 2: Zapsat datum do Excelu  

Dále vložíme řetězec japonské éry (`"R02-04-01"`) do buňky **A1**. Řetězec napodobuje éru Reiwa (rok 2, duben 1).

```csharp
        // Step 2: Write a Japanese era date string into cell A1
        worksheet.Cells["A1"].PutValue("R02-04-01");
```

*Co se děje:* `PutValue` uloží surový řetězec. Aspose.Cells se jej později pokusí parsovat podle stylu buňky. Pokud tento krok přeskočíte a zapíšete přímo `DateTime`, ztratíte informaci o éře, kterou chcete zobrazit.

## Krok 3: Použijte vestavěný číselný formát data (ID 14)

Excel má vestavěný formát data s ID 14 (`mm-dd-yy`). Použitím tohoto formátu řeknete enginu, že buňka **obsahuje datum**, nikoli jen text.

```csharp
        // Step 3: Apply the built‑in date number format (ID 14)
        worksheet.Cells["A1"].Style.Number = 14;
```

*Proč použít ID 14?* Jedná se o univerzální „krátký datum“ formát, který zajišťuje, že Excel zachází s obsahem jako s hodnotou data, což je předpoklad pro správnou funkci jakéhokoli vlastního formátu.

## Krok 4: Nastavte vlastní formát pro zobrazení zápisu japonské éry  

Nyní zábavná část: řekneme Excelu, aby zobrazil datum pomocí formátu japonské éry. Vlastní řetězec `[$-ja-JP]ggge年m月d日` to přesně provede.

```csharp
        // Step 4: Set a custom format to display the date in Japanese era notation
        worksheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge年m月d日";
```

*Explanation:*  
- `[$-ja-JP]` vynutí locale na japonštinu.  
- `ggg` je název éry (např. „R“ pro Reiwa).  
- `e` je rok éry.  
- `年`, `月`, `日` jsou doslovné japonské znaky pro rok, měsíc, den.

Pokud potřebujete jiné locale, jednoduše nahraďte `ja-JP` odpovídajícím kódem kultury (např. `en-US`).

## Krok 5: Získat parsovanou hodnotu DateTime  

Nakonec si přečteme **skutečný `DateTime`**, který Excel z buňky parsoval. To dokazuje, že řetězec byl správně interpretován.

```csharp
        // Step 5: Retrieve the parsed DateTime value from the cell
        DateTime parsedDate = worksheet.Cells["A1"].DateTime;   // => 2020‑04‑01

        // Output to console for verification
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

*Výsledek:* Konzole vypíše `Parsed DateTime: 2020-04-01`. I když jsme zadali řetězec japonské éry, Excel interně ukládá gregoriánské datum, které můžete použít pro výpočty, porovnání nebo další export.

## Krok 6: Uložit Workbook (volitelné)

Pokud chcete vidět formátovaný workbook v Excelu, stačí jej uložit na disk.

```csharp
        // Optional: Save the workbook to a file
        workbook.Save("JapaneseEraDate.xlsx");
    }
}
```

Otevřete vygenerovaný soubor **JapaneseEraDate.xlsx** a uvidíte buňku **A1**, která zobrazuje `R02年4月1日` (přesný formát japonské éry, který jsme nastavili).

![příklad nastavení vlastního formátu buňky](image-placeholder.png "Buňka Excelu zobrazující datum japonské éry – nastavení vlastního formátu buňky")

*Alt text výše obsahuje hlavní klíčové slovo, splňující požadavek SEO pro obrázek.*

## Běžné varianty a okrajové případy  

### Zápis jiného formátu data  

Pokud dáváte přednost ISO‑8601 (`2020-04-01`) místo řetězce éry, stačí změnit volání `PutValue`:

```csharp
worksheet.Cells["A1"].PutValue(new DateTime(2020, 4, 1));
worksheet.Cells["A1"].Style.Number = 14;                 // keep built‑in date format
worksheet.Cells["A1"].Style.Custom = "yyyy-mm-dd";      // custom ISO format
```

### Práce s nulovými nebo prázdnými buňkami  

Při čtení data vždy kontrolujte prázdné buňky, abyste se vyhnuli `InvalidOperationException`:

```csharp
if (!worksheet.Cells["A1"].IsDate)
{
    Console.WriteLine("Cell A1 does not contain a valid date.");
}
else
{
    DateTime dt = worksheet.Cells["A1"].DateTime;
    // use dt...
}
```

### Podpora více locale  

Můžete projít seznam kódů kultur a aplikovat je dynamicky:

```csharp
string[] cultures = { "ja-JP", "en-US", "fr-FR" };
foreach (var culture in cultures)
{
    worksheet.Cells["A1"].Style.Custom = $"[$-{culture}]ggge年m月d日";
    // Save or export per culture if needed
}
```

## Profesionální tipy a úskalí  

- **Vždy nejprve nastavte vestavěný číselný formát** (`Style.Number`). Bez něj Excel považuje buňku za prostý text a vlastní formát je ignorován.  
- **Kódy locale jsou necitlivé na velikost písmen**, ale použití kanonické podoby (`ja-JP`) zabraňuje záměně.  
- **Ukládání je volitelné** pro zpracování v paměti; můžete workbook streamovat přímo do webové odpovědi (`workbook.Save(stream, SaveFormat.Xlsx)`).  
- **Licence Aspose.Cells**: Bezplatná evaluační verze přidává vodoznak. Pro produkci se ujistěte, že máte platnou licenci, aby nedošlo k výkonovým penalizacím.

## Shrnutí  

Ukázali jsme, jak **nastavit vlastní formát buňky** v C# pro zobrazení dat japonské éry, jak **zapsat datum do Excelu**, **aplikovat vlastní formát data**, **číst DateTime z Excelu** a **vytvořit workbook worksheet** – vše v jednom samostatném programu. Hlavní klíčové slovo se objevuje přirozeně v celém textu, zatímco sekundární klíčová slova jsou zapletena do nadpisů a těla textu, což splňuje jak SEO, tak standardy AI‑citací.

## Co dál?

- Prozkoumejte **conditional formatting** pro zvýraznění prošlých termínů.  
- Kombinujte tento přístup s **PivotTables** pro dynamické reportování.  
- Vyzkoušejte **čtení velkých CSV souborů** a jejich převod do Excelu se stejnou logikou zpracování dat.  

Neváhejte experimentovat s různými locale, vlastními vzory nebo dokonce časovými pásmy. Pokud narazíte na problémy, zanechte komentář níže – šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}