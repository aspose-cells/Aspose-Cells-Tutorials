---
category: general
date: 2026-03-01
description: Jak rychle a spolehlivě uložit pivot. Naučte se, jak exportovat pivot,
  exportovat obrázek pivotu a převést oblast na obrázek pomocí několika řádků C#.
draft: false
keywords:
- how to save pivot
- how to export pivot
- export pivot image
- convert range to image
language: cs
og_description: Jak uložit pivot v C# během několika sekund. Postupujte podle tohoto
  návodu pro export pivotu, export obrázku pivotu a převod rozsahu na obrázek s čistým
  kódem.
og_title: Jak uložit Pivot jako obrázek – rychlý tutoriál C#
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Jak uložit kontingenční tabulku jako obrázek – krok za krokem průvodce
url: /cs/net/image-and-chart-operations/how-to-save-pivot-as-an-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak uložit kontingenční tabulku jako obrázek – Kompletní tutoriál v C#

Už jste se někdy zamysleli, **jak uložit kontingenční tabulku** přímo z listu Excelu, aniž byste soubor otevírali ručně? Nejste v tom sami. V mnoha reportovacích řetězcích je kontingenční tabulka konečnou vizualizací a další krok – vložení do PDF, poslání e‑mailem nebo umístění na dashboard – vyžaduje statický obrázek. Dobrá zpráva? Pouhými několika voláními API můžete **jak uložit kontingenční tabulku** bez jakékoli UI interakce.

V tomto tutoriálu projdeme přesný kód, který potřebujete k **jak exportovat kontingenční tabulku**, převést tento export na **exportovat obrázek kontingenční tabulky**, a dokonce **převést oblast na obrázek** pro libovolnou vlastní oblast. Na konci budete mít znovupoužitelnou metodu, kterou můžete vložit do jakéhokoli .NET projektu.

> **Rychlá poznámka:** Příklady používají populární knihovnu Aspose.Cells pro .NET, ale koncepty lze přenést na jakoukoli knihovnu, která poskytuje `PivotTable`, `Range` a funkci exportu obrázku.

## Požadavky – Co potřebujete před zahájením

- **.NET 6+** (nebo .NET Framework 4.7.2+) nainstalovaný na vašem počítači.  
- **Aspose.Cells for .NET** (bezplatná zkušební verze nebo licencovaná verze). Můžete ji přidat přes NuGet:  

  ```bash
  dotnet add package Aspose.Cells
  ```
- Základní znalost C# a konceptů Excelu. Není potřeba hluboké vnitřní znalosti.  
- Existující soubor Excel (`sample.xlsx`), který obsahuje alespoň jednu kontingenční tabulku.

Pokud vám některá z těchto věcí není známá, pozastavte se a nejprve nainstalujte balíček – nemá smysl pokračovat, dokud není knihovna připravena.

## Jak uložit kontingenční tabulku jako obrázek – Hlavní metoda

Níže je **kompletní, spustitelný** úryvek, který demonstruje celý proces. Obsahuje importy, zpracování chyb a komentáře, takže jej můžete zkopírovat a vložit přímo do konzolové aplikace.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;   // Needed for Image handling
using System.Drawing;        // System.Drawing.Image

namespace PivotExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the workbook that holds the pivot table
            string workbookPath = @"C:\Temp\sample.xlsx";

            // Destination folder for the exported image
            string outputFolder = @"C:\Temp\Images";

            try
            {
                // Ensure output directory exists
                System.IO.Directory.CreateDirectory(outputFolder);

                // Call the helper that does the actual work
                SavePivotAsImage(workbookPath, outputFolder, "pivot.png");
                Console.WriteLine("Pivot saved successfully!");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }

        /// <summary>
        /// Saves the first pivot table in the given workbook as an image file.
        /// This method shows exactly **how to export pivot** and **convert range to image**.
        /// </summary>
        /// <param name="workbookPath">Full path to the source .xlsx file.</param>
        /// <param name="outputFolder">Folder where the image will be written.</param>
        /// <param name="fileName">Desired image file name (e.g., pivot.png).</param>
        public static void SavePivotAsImage(string workbookPath, string outputFolder, string fileName)
        {
            // Load the workbook
            Workbook wb = new Workbook(workbookPath);

            // --------------------------------------------------------------
            // Step 1: Get the first pivot table from the first worksheet
            // --------------------------------------------------------------
            Worksheet ws = wb.Worksheets[0];
            if (ws.PivotTables.Count == 0)
                throw new InvalidOperationException("No pivot tables found in the worksheet.");

            // This is the object we will eventually export.
            PivotTable pivot = ws.PivotTables[0];

            // --------------------------------------------------------------
            // Step 2: Create a range that covers the entire pivot table
            // --------------------------------------------------------------
            // The CreateRange method returns a Range object that precisely
            // matches the pivot's visual bounds.
            Range pivotRange = pivot.CreateRange();

            // --------------------------------------------------------------
            // Step 3: Convert the range to an image (the **export pivot image** step)
            // --------------------------------------------------------------
            // ToImage returns a System.Drawing.Image instance.
            Image pivotImg = pivotRange.ToImage();

            // --------------------------------------------------------------
            // Step 4: Save the image to a file
            // --------------------------------------------------------------
            string fullPath = System.IO.Path.Combine(outputFolder, fileName);
            pivotImg.Save(fullPath, System.Drawing.Imaging.ImageFormat.Png);
        }
    }
}
```

### Proč to funguje

- **Přístup k kontingenční tabulce:** `ws.PivotTables[0]` získá první kontingenční tabulku, která je často tou, kterou chcete exportovat. Pokud máte více kontingenčních tabulek, stačí změnit index nebo projít kolekci.
- **Vytvoření oblasti:** `pivot.CreateRange()` vám poskytne objekt `Range`, který odpovídá přesným buňkám zobrazeným na obrazovce. Toto je klíčový krok, který vám umožní **převést oblast na obrázek** bez ručního počítání adres.
- **Převod oblasti na obrázek:** `pivotRange.ToImage()` interně rasterizuje buňky, zachovává formátování, barvy a okraje – přesně to, co vidíte v Excelu.
- **Uložení PNG:** Poslední volání `Save` zapíše přenosný PNG soubor, čímž je **export obrázku kontingenční tabulky** připravený pro jakýkoli následný proces (PDF, e‑mail, web).

## Jak exportovat kontingenční tabulku – Varianty, které můžete potřebovat

### Export více kontingenčních tabulek ze stejného listu

Pokud váš sešit obsahuje několik kontingenčních tabulek, můžete je projít v cyklu:

```csharp
foreach (PivotTable pt in ws.PivotTables)
{
    Range r = pt.CreateRange();
    Image img = r.ToImage();
    string name = $"pivot_{pt.Index}.png";
    img.Save(System.IO.Path.Combine(outputFolder, name), ImageFormat.Png);
}
```

### Export do jiných formátů (JPEG, BMP, GIF)

Metoda `Image.Save` přijímá libovolný `ImageFormat`. Stačí vyměnit `ImageFormat.Png` za `ImageFormat.Jpeg` nebo `ImageFormat.Bmp`:

```csharp
pivotImg.Save(fullPath, System.Drawing.Imaging.ImageFormat.Jpeg);
```

### Úprava rozlišení obrázku

Někdy potřebujete snímek vyššího rozlišení pro tisk. Použijte přetížení, které přijímá `ImageOrPrintOptions`:

```csharp
ImageOrPrintOptions opts = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    Resolution = 300   // DPI
};
Image highRes = pivotRange.ToImage(opts);
highRes.Save(fullPath, ImageFormat.Png);
```

## Převést oblast na obrázek – Mimo kontingenční tabulky

Metoda `ToImage` není omezena jen na kontingenční tabulky. Chcete zachytit graf, datovou tabulku nebo vlastní blok buněk? Stačí předat libovolný `Range`:

```csharp
// Capture cells B2:E20 as an image
Range customRange = ws.Cells.CreateRange("B2", "E20");
Image rangeImg = customRange.ToImage();
rangeImg.Save(@"C:\Temp\custom_range.png", ImageFormat.Png);
```

To je podstata **převodu oblasti na obrázek** – stejná API, kterou jste použili pro kontingenční tabulku, funguje pro jakýkoli obdélníkový blok.

## Časté úskalí a profesionální tipy

- **Obnovení kontingenční tabulky:** Pokud se změní zdrojová data, zavolejte `pivot.RefreshData()` před vytvořením oblasti. Vynechání tohoto kroku může vést k zastaralému obrázku.
- **Skryté řádky/sloupce:** Ve výchozím nastavení jsou skryté řádky/sloupce ignorovány. Pokud je potřebujete viditelné, nastavte `pivot.ShowHiddenData = true` před `CreateRange()`.
- **Správa paměti:** `Image` implementuje `IDisposable`. V produkčním kódu zabalte obrázek do bloku `using` nebo po uložení zavolejte `Dispose()`, aby nedošlo k únikům paměti.
- **Bezpečnost vláken:** Objekt Aspose.Cells není bezpečný pro více vláken. Pokud exportujete kontingenční tabulky z více vláken, vytvořte pro každé vlákno samostatnou instanci `Workbook`.

## Kompletní funkční příklad – Řešení v jednom souboru

Pro ty, kteří milují kopírování a vkládání, zde je celý program zkomprimovaný do jediného souboru. Vložte jej do nového konzolového projektu, aktualizujte cesty a spusťte.

```csharp
using System;
using System.Drawing;
using System.Drawing.Imaging;
using System.IO;
using Aspose.Cells;

namespace PivotExportDemo
{
    class Program
    {
        static void Main()
        {
            string src = @"C:\Temp\sample.xlsx";
            string outDir = @"C:\Temp\Images";

            Directory.CreateDirectory(outDir);
            SaveFirstPivotAsPng(src, outDir, "pivot.png");
        }

        static void SaveFirstPivotAsPng(string workbookPath, string folder, string fileName)
        {
            Workbook wb = new Workbook(workbookPath);
            Worksheet ws = wb.Worksheets[0];

            if (ws.PivotTables.Count == 0)
                throw new Exception("Worksheet contains no pivots.");

            PivotTable pt = ws.PivotTables[0];
            Range r = pt.CreateRange();

            using (Image img = r.ToImage())
            {
                string full = Path.Combine(folder, fileName);
                img.Save(full, ImageFormat.Png);
            }
        }
    }
}
```

Po spuštění se vypíše „Pivot saved successfully!“ a vytvoří se soubor `pivot.png` právě tam, kam jste ukázali.

## Závěr

Probrali jsme **jak uložit kontingenční tabulku** v C# od začátku až do konce, ukázali vám **jak exportovat kontingenční tabulku** pro různé scénáře, demonstrovali **export obrázku kontingenční tabulky** v různých formátech a vysvětlili podkladové mechaniky **převodu oblasti na obrázek**. S těmito úryvky můžete automatizovat generování reportů, vkládat obrázky do PDF nebo jednoduše archivovat své analytické dashboardy, aniž byste kdykoliv ručně otevírali Excel.

Další kroky? Zkuste vložit vygenerovaný PNG do PDF pomocí Aspose.PDF, nebo jej nahrát do Azure Blob pro webové využití. Můžete také zkusit exportovat grafy stejným způsobem – stačí nahradit `PivotTable` objektem `Chart` a zavolat `ToImage()`.

Máte otázky ohledně okrajových případů, licencování nebo výkonu? Zanechte komentář níže a šťastné programování! 

![jak uložit kontingenční tabulku](/images/pivot-save-example.png "jak uložit kontingenční tabulku")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}