---
category: general
date: 2026-02-14
description: Jak exportovat kontingenční tabulku z Excel sešitu do PNG pomocí Aspose.Cells.
  Naučte se, jak načíst Excel sešit, vykreslit kontingenční tabulku do obrázku a snadno
  uložit obrázek kontingenční tabulky.
draft: false
keywords:
- how to export pivot
- export excel pivot
- load excel workbook
- pivot table to png
- save pivot image
language: cs
og_description: jak exportovat kontingenční tabulku z Excelu do PNG v C#. Tento průvodce
  vám ukáže, jak načíst sešit Excel, vykreslit kontingenční tabulku do PNG a uložit
  obrázek kontingenční tabulky.
og_title: Jak exportovat pivot do PNG v C# – kompletní tutoriál
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak exportovat pivot do PNG v C# – krok za krokem
url: /cs/net/rendering-and-export/how-to-export-pivot-to-png-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak exportovat pivot do PNG v C# – kompletní tutoriál

Už jste se někdy zamýšleli **how to export pivot** z listu Excel jako ostrý PNG soubor? Nejste jediní — vývojáři často potřebují rychlou vizuální podobu kontingenční tabulky pro reporty, dashboardy nebo e‑mailové přílohy. Dobrá zpráva? S Aspose.Cells můžete načíst Excel sešit, získat první kontingenční tabulku, převést ji na obrázek a **save pivot image** během několika řádků C#.

V tomto tutoriálu projdeme vše, co potřebujete: od základů **load excel workbook**, přes vykreslení **pivot table to png**, až po uložení souboru na disk. Na konci budete mít samostatný, spustitelný program, který můžete vložit do libovolného .NET projektu.

---

## Co budete potřebovat

- **.NET 6 nebo novější** (kód funguje také na .NET Framework 4.7+)
- **Aspose.Cells for .NET** NuGet balíček (verze 23.12 v době psaní)
- Excel soubor (`input.xlsx`) obsahující alespoň jednu kontingenční tabulku
- Prostředí Visual Studio nebo VS Code, ve kterém se cítíte pohodlně

Žádné další knihovny, žádná COM interop a žádná instalace Excelu — Aspose.Cells vše zvládne v paměti.

---

## Krok 1 – Načtení Excel sešitu

Prvním krokem je načíst sešit do paměti. Zde se hodí klíčové slovo **load excel workbook**.

```csharp
using System.Drawing;
using Aspose.Cells;

class PivotExport
{
    static void Main()
    {
        // Step 1: Load the workbook from disk
        // Adjust the path to where your input.xlsx lives
        var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // Grab the first worksheet (you can also select by name)
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Proč je to důležité:**  
> Načtení sešitu jen jednou udržuje operaci rychlou a zabraňuje zamčení zdrojového souboru. Aspose.Cells načte soubor do řízeného proudu, takže později můžete načíst i z pole bajtů nebo ze síťové lokace.

---

## Krok 2 – Vykreslení kontingenční tabulky na obrázek

Jakmile je sešit v paměti, můžeme přistoupit k jeho kontingenčním tabulkám. API poskytuje praktickou metodu `ToImage()`, která vrací `System.Drawing.Image`.

```csharp
        // Step 2: Find the first pivot table on the worksheet
        if (worksheet.PivotTables.Count == 0)
        {
            System.Console.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }

        // Export the first pivot table as an image
        Image pivotImage = worksheet.PivotTables[0].ToImage();

        // Optional: tweak image quality or size here
        // pivotImage.SetResolution(300, 300);
```

> **Tip:** Pokud váš sešit obsahuje více kontingenčních tabulek, jednoduše projděte `worksheet.PivotTables` a exportujte každou. Volání `ToImage()` respektuje aktuální zobrazení (filtry, řezače atd.), takže získáte přesně to, co uživatel vidí.

---

## Krok 3 – Uložení vygenerovaného PNG souboru

Nakonec bitmapu uložíme na disk. Přetížení `Save` automaticky vybere formát podle přípony souboru.

```csharp
        // Step 3: Save the image as PNG
        var outputPath = @"YOUR_DIRECTORY\pivot.png";
        pivotImage.Save(outputPath, System.Drawing.Imaging.ImageFormat.Png);

        System.Console.WriteLine($"Pivot table exported successfully to {outputPath}");
    }
}
```

Spuštěním programu vznikne soubor `pivot.png`, který vypadá přesně jako kontingenční tabulka v Excelu. Otevřete jej v libovolném prohlížeči obrázků a uvidíte řádky, sloupce i součty vykreslené pixel‑perfektně.

---

## Řešení běžných okrajových případů

### Více listů nebo kontingenčních tabulek

Pokud se vaše kontingenční tabulka nachází na jiném listu, změňte index listu nebo použijte název listu:

```csharp
Worksheet ws = workbook.Worksheets["SalesData"];
```

Pak cyklus:

```csharp
foreach (PivotTable pt in ws.PivotTables)
{
    Image img = pt.ToImage();
    img.Save($"pivot_{pt.Name}.png", ImageFormat.Png);
}
```

### Velké kontingenční tabulky

U velmi velkých pivotů může být výchozí velikost obrázku obrovská. Velikost vykreslení můžete ovlivnit úpravou zoom faktoru listu před voláním `ToImage()`:

```csharp
worksheet.PageSetup.Zoom = 75; // renders at 75 % of original size
```

### Správa paměti

`System.Drawing.Image` implementuje `IDisposable`. V produkčním kódu obalte obrázek do bloku `using`, aby se nativní zdroje uvolnily okamžitě:

```csharp
using (Image pivotImage = worksheet.PivotTables[0].ToImage())
{
    pivotImage.Save(outputPath, ImageFormat.Png);
}
```

---

## Kompletní funkční příklad

Níže je kompletní, připravený k běhu program. Vložte jej do nového konzolového projektu, upravte cesty k souborům a stiskněte **F5**.

```csharp
using System;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;

namespace PivotExportDemo
{
    class Program
    {
        static void Main()
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook (load excel workbook)
            // -----------------------------------------------------------------
            string inputFile = @"YOUR_DIRECTORY\input.xlsx";
            Workbook wb = new Workbook(inputFile);
            Worksheet ws = wb.Worksheets[0]; // first worksheet

            // -----------------------------------------------------------------
            // 2️⃣ Ensure a pivot table exists and export it (how to export pivot)
            // -----------------------------------------------------------------
            if (ws.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found. Exiting.");
                return;
            }

            // Export the first pivot table as a PNG image (pivot table to png)
            using (Image img = ws.PivotTables[0].ToImage())
            {
                // -----------------------------------------------------------------
                // 3️⃣ Save the pivot image to disk (save pivot image)
                // -----------------------------------------------------------------
                string outputFile = @"YOUR_DIRECTORY\pivot.png";
                img.Save(outputFile, ImageFormat.Png);
                Console.WriteLine($"Pivot exported successfully → {outputFile}");
            }
        }
    }
}
```

**Očekávaný výstup:**  
```
Pivot exported successfully → YOUR_DIRECTORY\pivot.png
```

A soubor `pivot.png` bude obsahovat vizuální repliku původní kontingenční tabulky.

---

## Často kladené otázky

- **Funguje to s .xlsx soubory, které obsahují grafy?**  
  Ano. Metoda `ToImage()` se stará jen o rozvržení kontingenční tabulky; grafy nejsou ovlivněny.

- **Mohu exportovat do JPEG nebo BMP místo PNG?**  
  Rozhodně — stačí změnit argument `ImageFormat` v metodě `Save`. PNG je bezztrátový, proto jej doporučujeme pro ostrá data.

- **Co když je sešit chráněn heslem?**  
  Načtěte jej pomocí přetížení s heslem:  
  `Workbook wb = new Workbook(inputFile, new LoadOptions { Password = "mySecret" });`

---

## Závěr

Právě jsme si ukázali **how to export pivot** z Excel souboru do PNG obrázku pomocí Aspose.Cells. Kroky — **load excel workbook**, najít **pivot table to png** a **save pivot image** — jsou jednoduché, ale dostatečně silné pro reálné reportingové pipeline.

Dále můžete zkusit:

- Automatizovat export všech kontingenčních tabulek ve složce (export excel pivot in bulk)  
- Vložit PNG do PDF nebo HTML e‑mailu (kombinace s iTextSharp nebo Razor)  
- Přidat vodoznaky nebo vlastní stylování k exportovanému obrázku  

Vyzkoušejte to a nechte obrázky mluvit ve vašem dalším dashboardu.

---

![příklad výstupu exportu pivot](assets/pivot-export-example.png "příklad výstupu exportu pivot")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}