---
category: general
date: 2026-05-04
description: Jak aktualizovat kontingenční tabulku v C# a exportovat ji jako PNG,
  poté vložit obrázek do listu. Postupujte podle tohoto průvodce krok za krokem s
  kompletním kódem.
draft: false
keywords:
- how to refresh pivot
- how to export pivot
- insert image into worksheet
- refresh pivot table code
- load excel workbook c#
language: cs
og_description: Jak aktualizovat kontingenční tabulku v C#? Naučte se exportovat kontingenční
  tabulku jako obrázek a vložit ji do listu s kompletními příklady kódu.
og_title: Jak obnovit Pivot v C# – Exportovat a vložit jako obrázek
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Jak obnovit Pivot v C# – Exportovat a vložit jako obrázek
url: /cs/net/pivot-tables/how-to-refresh-pivot-in-c-export-and-insert-as-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak obnovit kontingenční tabulku v C# – Export a vložení jako obrázek

Obnovení kontingenční tabulky v C# je častou překážkou při automatizaci Excelových reportů. V tomto průvodci uvidíte přesně **jak obnovit kontingenční tabulku**, exportovat ji jako PNG a vložit tento obrázek do zástupce listu – vše v jediném spustitelném programu.

Pokud se také ptáte, *jak exportovat kontingenční tabulku*, nebo potřebujete **vložit obrázek do listu**, jste na správném místě. Projdeme každý řádek, vysvětlíme, proč je důležitý, a dokonce se podíváme na několik okrajových případů, na které můžete narazit v reálných projektech.

---

## Co budete potřebovat

- **Aspose.Cells for .NET** (knihovna, která poskytuje `Workbook`, `Worksheet`, `ImageOrPrintOptions` atd.). Můžete ji získat z NuGet: `Install-Package Aspose.Cells`.
- .NET 6 nebo novější (kód níže cílí na .NET 6, ale funguje s jakoukoliv novější verzí).
- Základní znalost C# a práce se soubory – nic složitého.

To je vše. Žádné další DLL, žádné COM interop, jen čistá C# konzolová aplikace.

## Krok 1 – Načtení Excel sešitu v C# stylu

Nejprve musíme otevřít zdrojový soubor. Zde se nachází část **load excel workbook c#**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from disk
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Grab the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Proč?**  
> Načtení sešitu nám poskytuje přístup k jeho listům, kontingenčním tabulkám a zástupcům obrázků. Pokud soubor není nalezen, Aspose vyhodí jasnou `FileNotFoundException`, kterou můžete zachytit pro uživatelsky přívětivější rozhraní.

## Krok 2 – Připravit možnosti obrázku pro export kontingenční tabulky

Nyní říkáme Aspose, jak má exportovaný obrázek vypadat. Toto je jádro **how to export pivot**.

```csharp
        // Step 2: Set up image export options – PNG is lossless and widely supported
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Png,
            // Optional: tweak resolution for sharper images
            HorizontalResolution = 300,
            VerticalResolution = 300
        };
```

> **Tip:**  
> Pokud potřebujete JPEG pro menší velikost souboru, změňte `SaveFormat.Png` na `SaveFormat.Jpeg` a podle toho upravte `Quality`.

## Krok 3 – Kód pro obnovení kontingenční tabulky

Zastaralá kontingenční tabulka zobrazuje stará data. Její obnovení zajišťuje, že obrázek odráží nejnovější čísla.

```csharp
        // Step 3: Refresh the first pivot table in the worksheet
        if (worksheet.PivotTables.Count > 0)
        {
            worksheet.PivotTables[0].Refresh();
        }
        else
        {
            Console.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }
```

> **Proč obnovit?**  
> Kontingenční tabulky ukládají do mezipaměti zdrojová data při jejich vytvoření. Pokud se podkladový list změní (např. přidají se nové řádky), mezipaměť se zastará. Volání `Refresh()` donutí Aspose znovu dotázat se na zdrojový rozsah, což zajišťuje, že exportovaný obrázek není uvízlý se zastaralými součty.

## Krok 4 – Převést obnovenou kontingenční tabulku na obrázek

Zde je kouzelný řádek, který skutečně **export pivot** do pole bajtů.

```csharp
        // Step 4: Export the refreshed pivot table as an image
        byte[] pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);
```

> **Co získáte:**  
> `pivotImage` nyní obsahuje PNG‑kódovaný obrázek kontingenční tabulky, připravený k zápisu na disk nebo vložení jinam.

## Krok 5 – Vložit obrázek do listu

Zde **vložíme obrázek do listu**. Umístíme obrázek do prvního zástupce obrázku (pokud existuje).

```csharp
        // Step 5: Insert the image into the first picture placeholder
        if (worksheet.Pictures.Count > 0)
        {
            worksheet.Pictures[0].ImageBytes = pivotImage;
        }
        else
        {
            // If no placeholder exists, add a new picture at cell A1
            int pictureIndex = worksheet.Pictures.Add(0, 0, pivotImage).Index;
            Console.WriteLine($"Added new picture at index {pictureIndex}.");
        }
```

> **Proč použít zástupce?**  
> Mnoho Excel šablon obsahuje předem naformátovaný tvar obrázku (velikost, okraj, pozice). Cílením na `Pictures[0]` zachováme rozvržení. Pokud šablona nemá zástupce, fallback vytvoří nový obrázek ukotvený v buňce A1.

## Krok 6 – Uložit sešit (volitelné)

Nakonec změny uložíme. Můžete přepsat originál nebo zapsat do nového souboru.

```csharp
        // Step 6: Save the updated workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

> **Očekávaný výsledek:**  
> Otevřete `output.xlsx` a uvidíte, že kontingenční tabulka je obnovena, exportována jako ostrý PNG a zobrazena v prvním slotu obrázku. Zbytek sešitu zůstane nedotčen.

## Kompletní funkční příklad (připravený ke kopírování a vložení)

Níže je kompletní blok kódu, který můžete vložit do nového konzolového projektu. Nechybí žádná část.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);
        Worksheet worksheet = workbook.Worksheets[0];

        // Configure image export options (PNG, 300 DPI)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // Refresh the first pivot table
        if (worksheet.PivotTables.Count == 0)
        {
            Console.WriteLine("No pivot tables found.");
            return;
        }
        worksheet.PivotTables[0].Refresh();

        // Export pivot to PNG byte array
        byte[] pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);

        // Insert the image into a picture placeholder or add a new picture
        if (worksheet.Pictures.Count > 0)
        {
            worksheet.Pictures[0].ImageBytes = pivotImage;
        }
        else
        {
            worksheet.Pictures.Add(0, 0, pivotImage);
        }

        // Save the workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Spusťte program, otevřete vzniklý soubor a ověřte, že kontingenční tabulka odráží nejnovější data a zobrazuje se jako vysoce rozlišený obrázek.

## Často kladené otázky a okrajové případy

| Question | Answer |
|----------|--------|
| **Co když má sešit více listů?** | Upravte `workbook.Worksheets[0]` na odpovídající index nebo název (`workbook.Worksheets["Sheet2"]`). |
| **Mohu exportovat více kontingenčních tabulek?** | Projděte `worksheet.PivotTables` v cyklu a opakujte kroky 3‑4 pro každou. Uložte každý obrázek do samostatného zástupce nebo je spojte do jednoho listu. |
| **Co s velkými kontingenčními tabulkami, které zatěžují paměť?** | Použijte `ImageOrPrintOptions` s nižším DPI nebo exportujte do JPEG, aby se snížila velikost pole bajtů. |
| **Musím něco uvolnit?** | Objekty Aspose jsou spravované; `using` blok není povinný, ale můžete obalit `Workbook` do `using` bloku, pokud preferujete deterministické čištění. |
| **Je to kompatibilní s .NET Core?** | Ano. Aspose.Cells podporuje .NET Core, .NET 5/6 a .NET Framework. Stačí odkazovat na příslušný NuGet balíček. |

## Tipy a osvědčené postupy

- **Ověřujte cesty**: Používejte `Path.Combine` a `Environment.GetFolderPath`, abyste se vyhnuli pevně zakódovaným oddělovačům.
- **Zpracování chyb**: Zabalte celé tělo `Main` do `try/catch` a logujte `Exception.Message` pro produkční skripty.
- **Návrh šablony**: Umístěte průhledný tvar obrázku tam, kde chcete mít obrázek kontingenční tabulky; tím zachováte šířky sloupců a výšky řádků.
- **Výkon**: Pokud potřebujete jen obrázek, můžete úplně vynechat ukládání sešitu a zapsat `pivotImage` do samostatného PNG souboru.

## Závěr

Nyní víte, **jak obnovit kontingenční tabulku** v C#, exportovat tento obnovený pohled jako obrázek a **vložit obrázek do listu** bez problémů. Kompletní řešení – načtení sešitu, nastavení možností exportu, obnovení kontingenční tabulky, převod na PNG a uložení souboru – pokrývá celý workflow, který jste požadovali.

Jste připraveni na další výzvu? Zkuste zkombinovat **how to export pivot** s dávkovým zpracováním více souborů, nebo prozkoumejte **refresh pivot table code** pro dynamické zdroje dat jako databáze nebo CSV kanály. Stejný vzor platí: načíst, obnovit, exportovat, vložit, uložit.

Šťastné programování a ať vaše Excel automatizace zůstane čerstvá a dokonalá jako obrázek!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}