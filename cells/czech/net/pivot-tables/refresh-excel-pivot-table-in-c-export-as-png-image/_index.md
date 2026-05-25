---
category: general
date: 2026-02-23
description: Obnovte kontingenční tabulku v Excelu v C# a exportujte ji jako PNG obrázek.
  Naučte se načíst Excel sešit v C#, obnovit kontingenční tabulku a uložit výsledek.
draft: false
keywords:
- refresh excel pivot table
- load excel workbook c#
- export pivot as image
- export excel pivot image
language: cs
og_description: Obnovte kontingenční tabulku v Excelu v C# a exportujte ji jako PNG
  obrázek. Průvodce krok za krokem s kompletním kódem a praktickými tipy.
og_title: Obnovit kontingenční tabulku v Excelu v C# – Exportovat jako PNG obrázek
tags:
- C#
- Excel
- Aspose.Cells
- Data Automation
title: Obnovit kontingenční tabulku v Excelu v C# – Exportovat jako PNG obrázek
url: /cs/net/pivot-tables/refresh-excel-pivot-table-in-c-export-as-png-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obnovit kontingenční tabulku Excel v C# – Exportovat jako PNG obrázek

Už jste někdy potřebovali **refresh an Excel pivot table** z aplikace v C# a pak ji převést na obrázek? Nejste jediní, kdo nad tím přemýšlí. V tomto tutoriálu vás provedeme přesně tím, jak **refresh Excel pivot table**, **load Excel workbook C#**, a nakonec **export pivot as image** — vše v čistém, spustitelném úryvku.

Na konci získáte soubor PNG, který vypadá přesně jako kontingenční tabulka v Excelu, připravený k vložení do zpráv, e‑mailů nebo dashboardů. Žádné ruční kopírování, žádné komplikované COM interop, jen přímočarý .NET kód.

## Prerequisites

- .NET 6+ (or .NET Framework 4.7+)
- Aspose.Cells for .NET (free trial or licensed version) – můžete jej získat z NuGet pomocí `Install-Package Aspose.Cells`.
- Existující soubor `input.xlsx`, který obsahuje alespoň jednu kontingenční tabulku.
- Složka, do které máte oprávnění zapisovat výstupní obrázek.

> **Tip:** Pokud používáte Visual Studio, povolte **nullable reference types** (`<Nullable>enable</Nullable>`), abyste včas zachytili chyby související s null.

---

## Krok 1: Načíst sešit Excel v C#

Prvním, co potřebujeme, je objekt `Workbook`, který ukazuje na náš zdrojový soubor. Považujte to za programové otevření souboru Excel.

```csharp
using System;
using Aspose.Cells;

class PivotExportDemo
{
    static void Main()
    {
        // 👉 Step 1: Load the workbook and obtain the first worksheet
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(inputPath);
        Worksheet worksheet = wb.Worksheets[0];

        // The rest of the steps follow…
```

**Proč je to důležité:** Načtení sešitu nám poskytuje přístup k listům, buňkám a – co je nejdůležitější – k vytvořeným kontingenčním tabulkám. Pokud soubor není nalezen, Aspose vyhodí jasnou výjimku `FileNotFoundException`, kterou můžete zachytit a elegantně ošetřit.

---

## Krok 2: Nastavit možnosti exportu obrázku (Export Pivot as Image)

Aspose.Cells vám umožňuje definovat, jak má být kontingenční tabulka vykreslena. Zde požadujeme PNG, protože je bezztrátový a široce podporovaný.

```csharp
        // 👉 Step 2: Configure image export options to use PNG format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            // Optional: set resolution for sharper output
            HorizontalResolution = 300,
            VerticalResolution = 300
        };
```

**Proč PNG?** Na rozdíl od JPEG zachovává PNG ostré čáry mřížky a stínování textu, na které kontingenční tabulky spoléhají. Pokud potřebujete menší soubor, můžete přepnout na `ImageFormat.Jpeg` a upravit kvalitu, ale ztratíte trochu jasnosti.

---

## Krok 3: Refresh the Pivot Table

Než zachytíme vizuál, musíme se ujistit, že kontingenční tabulka odráží nejnovější data. Toto je jádro **refresh excel pivot table**.

```csharp
        // 👉 Step 3: Refresh the first pivot table so it reflects the latest data
        PivotTable pivot = worksheet.PivotTables[0];
        pivot.Refresh();
```

**Co se děje pod kapotou?** `Refresh()` přepočítá kontingenční tabulku na základě zdrojového rozsahu. Pokud jste po uložení sešitu přidali řádky do zdrojových dat, tento volání je načte. Vynechání tohoto kroku vede k zastaralému obrázku, který neodpovídá aktuálním datům.

---

## Krok 4: Vykreslit kontingenční tabulku do PNG (Export Excel Pivot Image)

Nyní, když je vše aktuální, můžeme kontingenční tabulku přímo vykreslit do souboru obrázku.

```csharp
        // 👉 Step 4: Export the refreshed pivot table as a PNG image
        string outputPath = @"YOUR_DIRECTORY\pivot.png";
        pivot.RenderToImage(imgOptions, outputPath);

        Console.WriteLine($"Pivot table exported successfully to: {outputPath}");
    }
}
```

**Výsledek:** Otevřete `pivot.png` a uvidíte pixel‑dokonalý snímek obnovené kontingenční tabulky. Tento soubor lze připojit k e‑mailu, vložit do webové stránky nebo použít v reportovacím enginu.

### Očekávaný výstup

```
Pivot table exported successfully to: YOUR_DIRECTORY\pivot.png
```

Pokud přejdete do složky, PNG by mělo zobrazovat stejné řádky, sloupce a filtry, jaké vidíte v Excelu.

---

## Řešení běžných okrajových případů

| Situace | Co dělat |
|-----------|------------|
| **Multiple pivot tables** | Procházejte `worksheet.PivotTables` a pro každou zavolejte `Refresh()` / `RenderToImage()`. |
| **Dynamic sheet names** | Použijte `wb.Worksheets[wb.Worksheets.IndexOf("SheetName")]` nebo vyhledejte podle `worksheet.Name`. |
| **Large datasets** | Zvyšte `imgOptions.OnePagePerSheet = false` a nastavte `imgOptions.PageWidth`/`PageHeight` pro řízení stránkování. |
| **Missing Aspose.Cells license** | Zkušební verze přidává vodoznak. Získejte licenci a před načtením sešitu zavolejte `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");`. |
| **File‑path issues** | Použijte `Path.Combine(Environment.CurrentDirectory, "input.xlsx")`, abyste se vyhnuli pevně zakódovaným oddělovačům. |

---

## Tipy a osvědčené postupy

- **Správně uvolňovat** – Zabalte `Workbook` do bloku `using` nebo po dokončení zavolejte `wb.Dispose()`, aby se uvolnily nativní zdroje.
- **Ukládat vykreslené obrázky do cache** – Pokud potřebujete stejný obrázek kontingenční tabulky opakovaně, uložte PNG na disk a znovu jej použijte místo opětovného vykreslování.
- **Bezpečnost vláken** – Každé vlákno by mělo pracovat s vlastní instancí `Workbook`; objekty Aspose.Cells nejsou vláknově bezpečné.
- **Výkon** – Vykreslování velkých kontingenčních tabulek může být náročné na paměť. Nastavte `imgOptions.ImageFormat` na `Bmp` pro rychlejší, ale větší soubory, nebo snižte DPI pro rychlejší vykreslení.

---

## Úplný funkční příklad (připravený ke kopírování)

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class PivotExportDemo
{
    static void Main()
    {
        // 👉 Step 1: Load the workbook and obtain the first worksheet
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.xlsx");
        if (!File.Exists(inputPath))
        {
            Console.Error.WriteLine($"File not found: {inputPath}");
            return;
        }

        Workbook wb = new Workbook(inputPath);
        Worksheet worksheet = wb.Worksheets[0];

        // 👉 Step 2: Configure image export options to use PNG format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 👉 Step 3: Refresh the first pivot table so it reflects the latest data
        if (worksheet.PivotTables.Count == 0)
        {
            Console.Error.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }

        PivotTable pivot = worksheet.PivotTables[0];
        pivot.Refresh();

        // 👉 Step 4: Export the refreshed pivot table as a PNG image
        string outputPath = Path.Combine(Environment.CurrentDirectory, "pivot.png");
        pivot.RenderToImage(imgOptions, outputPath);

        Console.WriteLine($"Pivot table exported successfully to: {outputPath}");

        // Clean up
        wb.Dispose();
    }
}
```

Spusťte program, otevřete `pivot.png` a uvidíte obnovenou kontingenční tabulku přesně tak, jak se zobrazuje v Excelu.

---

## Často kladené otázky

**Q: Funguje to s .xlsx soubory vytvořenými v LibreOffice?**  
A: Ano. Aspose.Cells čte formát Open XML bez ohledu na původní aplikaci, takže můžete **load excel workbook c#** z LibreOffice, exportu Google Sheets nebo jakéhokoli jiného zdroje.

**Q: Můžu exportovat více listů najednou?**  
A: Rozhodně. Procházejte `wb.Worksheets` a použijte stejnou logiku `RenderToImage` pro každý list. Jen nezapomeňte každému výstupu dát jedinečný název souboru.

**Q: Co když kontingenční tabulka používá externí datový zdroj?**  
A: Aspose.Cells může obnovit externí připojení, pokud jsou vložena v souboru, ale budete muset programově poskytnout řetězec připojení a přihlašovací údaje. Viz dokumentace Aspose k `DataSourceOptions`.

---

## Závěr

Nyní máte robustní řešení od začátku do konce pro **refresh excel pivot table** z C# a **export excel pivot image** jako PNG. Kód ukazuje, jak **load excel workbook c#**, nastavit možnosti obrázku, zajistit, že kontingenční tabulka odráží nejnovější data, a nakonec ji vykreslit do souboru.

Dále můžete prozkoumat **export pivot as image** v jiných formátech (PDF, SVG) nebo automatizovat proces pro více sešitů v dávce. Chcete vložit PNG do Wordového reportu? Stejná třída `ImageOrPrintOptions` funguje s Aspose.Words.

Neváhejte experimentovat, zkoušet nové věci a klást otázky v komentářích — šťastné programování! 

![Snímek obrazovky obnovení kontingenční tabulky Excel](image.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}