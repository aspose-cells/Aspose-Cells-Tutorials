---
category: general
date: 2026-10-10
description: Převod Excelu do PowerPointu a nastavení tiskové oblasti v C# s Aspose.Cells
  – naučte se, jak exportovat Excel, nastavit tiskovou oblast a vytvořit soubor PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- set print area excel
- how to export excel
- how to set print area
- convert excel to pptx
language: cs
lastmod: 2026-10-10
og_description: Převod Excelu do PowerPointu pomocí Aspose.Cells. Tento tutoriál ukazuje,
  jak nastavit oblast tisku, exportovat Excel a vytvořit soubor PPTX v C#.
og_image_alt: Screenshot of code that converts Excel to PowerPoint while setting the
  print area
og_title: Převod Excelu do PowerPointu – kompletní průvodce pro vývojáře C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert Excel to PowerPoint and set print area in C# with Aspose.Cells
    – learn how to export Excel, set print area, and generate a PPTX file.
  headline: Convert Excel to PowerPoint and set print area
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Převést Excel do PowerPointu a nastavit oblast tisku
url: /cs/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod Excelu do PowerPointu a nastavení tiskové oblasti

Pokud potřebujete **convert Excel to PowerPoint**, tento průvodce vám přesně ukáže, jak to provést v C#. Definováním tiskové oblasti nejprve, řídíte, které buňky se zobrazí na každém snímku, a výsledný soubor PPTX odpovídá vašim očekáváním rozvržení. Řešení také odpovídá na otázky „how to export Excel“ a „how to set print area“ pomocí stejné základny kódu.

V tomto tutoriálu budete:

* Načíst existující sešit.
* Nastavit tiskovou oblast pro list (krok **set print area excel**).
* Konfigurovat možnosti převodu pro výstup PowerPoint.
* Vygenerovat soubor **convert excel to pptx** jedním voláním metody.

Veškerý potřebný kód je zahrnut, takže jej můžete okamžitě zkopírovat, vložit a spustit.

## Požadavky

Než začnete, ujistěte se, že máte:

| Requirement | Why it matters |
|-------------|----------------|
| **.NET 6.0 or later** | Ukázkový projekt cílí na .NET 6+, ale jakákoli verze .NET, která podporuje C# 10, funguje. |
| **Aspose.Cells for .NET** | Tato knihovna poskytuje `Workbook`, `ImageOrPrintOptions` a metodu `ConvertToPdf` (používanou pro PPTX). Nainstalujte ji přes NuGet: `dotnet add package Aspose.Cells` |
| **An input Excel file** | Tutoriál používá `input.xlsx`. Umístěte jej do složky, na kterou můžete odkazovat z kódu. |
| **Write permission to the output folder** | Program zapisuje `output.pptx`. Ujistěte se, že adresář existuje a je zapisovatelný. |

> **Pro tip:** Pokud pracujete s více listy, opakujte krok nastavení tiskové oblasti pro každý list před převodem.

## Krok 1: Vytvořte nový C# konzolový projekt

Otevřete terminál nebo okno PowerShell a spusťte:

```bash
dotnet new console -n ExcelToPowerPointDemo
cd ExcelToPowerPointDemo
dotnet add package Aspose.Cells
```

Tím se vytvoří nový projekt s názvem **ExcelToPowerPointDemo** a přidá se balíček Aspose.Cells, který je hlavní závislostí pro **how to export Excel** do dalších formátů.

## Krok 2: Napište kód pro převod

Nahraďte obsah souboru `Program.cs` kompletním příkladem níže. Kód demonstruje **convert excel to powerpoint**, ukazuje **how to set print area** a vytváří soubor **convert excel to pptx**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook (how to export Excel)
            // -----------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);
            Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} worksheet(s).");

            // -----------------------------------------------------------------
            // 2️⃣ Define the print area for the first worksheet (set print area excel)
            // -----------------------------------------------------------------
            // The range "A1:G30" will be the only part visible on the slide.
            // Adjust the range to match the data you want to show.
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";
            Console.WriteLine($"Print area set to {sheet.PageSetup.PrintArea} on sheet \"{sheet.Name}\".");

            // -----------------------------------------------------------------
            // 3️⃣ Configure conversion options for PowerPoint output
            // -----------------------------------------------------------------
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                // SaveFormat.Pptx tells Aspose.Cells to generate a PowerPoint file.
                SaveFormat = SaveFormat.Pptx,
                // Optional: set the slide size or DPI if needed.
                // HorizontalResolution = 300,
                // VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 4️⃣ Convert the worksheet to a PowerPoint presentation (convert excel to powerpoint)
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);
            Console.WriteLine($"Successfully created PowerPoint file at: {outputPath}");
        }
    }
}
```

### Proč je každá část důležitá

* **Loading the workbook** – Toto je první krok v jakémkoli scénáři **how to export Excel**. `Workbook` načte soubor do paměti a poskytne vám plný přístup k listům, buňkám a formátování.
* **Setting the print area** – Při přiřazení `PageSetup.PrintArea` říkáte Aspose.Cells, které buňky mají být vykresleny. To je jádro **set print area excel**; bez toho by byl exportován celý list, což by mohlo vytvořit obrovské, nečitelné snímky.
* **Choosing `SaveFormat.Pptx`** – Objekt `ImageOrPrintOptions` vám umožňuje přepínat výstupní formáty. Nastavením `SaveFormat` na `Pptx` spustíte pipeline **convert excel to pptx**.
* **Calling `ConvertToPdf`** – Navzdory názvu metody, když je `SaveFormat` nastaven na `Pptx`, knihovna vytvoří soubor PowerPoint. Toto je doporučený způsob, jak **convert excel to powerpoint** jedním voláním.

## Krok 3: Spusťte program

Z adresáře projektu spusťte:

```bash
dotnet run
```

Pokud je vše správně nakonfigurováno, měli byste vidět výstup v konzoli podobný:

```
Loaded workbook with 1 worksheet(s).
Print area set to A1:G30 on sheet "Sheet1".
Successfully created PowerPoint file at: YOUR_DIRECTORY\output.pptx
```

Otevřete `output.pptx` v Microsoft PowerPoint nebo v jakémkoli kompatibilním prohlížeči. Každý snímek odpovídá tištěné stránce listu, omezené na rozsah, který jste definovali.

## Práce s více listy

Pokud váš sešit obsahuje více než jeden list a chcete, aby každý list byl ve vlastní sadě snímků, projděte kolekci:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    Worksheet ws = workbook.Worksheets[i];
    ws.PageSetup.PrintArea = "A1:G30"; // adjust per sheet if needed
    string slidePath = $@"YOUR_DIRECTORY\output_sheet{i + 1}.pptx";
    ws.ConvertToPdf(conversionOptions, slidePath);
    Console.WriteLine($"Created {slidePath}");
}
```

Tento vzor ukazuje **how to export Excel** data list po listu, přičemž stále **setting print area** individuálně.

## Okrajové případy a tipy pro nejlepší praxi

| Situation | Recommended approach |
|-----------|----------------------|
| **Very large worksheets** | Snižte tiskovou oblast nebo zvyšte `HorizontalResolution`/`VerticalResolution`, aby velikost PPTX zůstala zvládnutelná. |
| **Different page orientations** | Nastavte `sheet.PageSetup.Orientation = PageOrientationType.Landscape;` před převodem. |
| **Custom slide size** | Použijte `conversionOptions.OnePagePerSheet = false;` a upravte `conversionOptions.Width` / `conversionOptions.Height`. |
| **Missing input file** | Zabalte kód načítání do `try { … } catch (FileNotFoundException)` bloku, aby poskytl jasnou chybovou zprávu. |
| **Non‑ASCII characters** | Ujistěte se, že sešit je uložen s kódováním UTF‑8; Aspose.Cells automaticky zpracovává Unicode. |

## Kompletní zdrojový kód pro referenci

Níže je celý program, včetně `using` direktiv a komentářů. Uložte jej jako `Program.cs` uvnitř projektu vytvořeného v **Krok 1**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the Excel file you want to convert.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";

            // 1️⃣ Load the workbook (how to export Excel)
            Workbook workbook = new Workbook(inputPath);

            // Select the first worksheet – you can loop for multiple sheets.
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Set the print area (set print area excel)
            sheet.PageSetup.PrintArea = "A1:G30";

            // 3️⃣ Prepare conversion options for PowerPoint output.
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx   // This triggers convert excel to pptx
            };

            // 4️⃣ Convert the worksheet to PowerPoint (convert excel to powerpoint)
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);

            Console.WriteLine("Conversion complete.");
        }
    }
}
```

## Očekávaný výstup

Spuštěním programu se vytvoří soubor PowerPoint (`output.pptx`), který obsahuje:

* Jeden snímek na každou tištěnou stránku listu.
* Pouze buňky v rozsahu **A1:G30** jsou viditelné na každém snímku.
* Zachované formátování (písma, barvy, ohraničení) tak, jak se objevuje v Excelu.

Otevřete soubor v PowerPointu a ověřte, že rozvržení odpovídá definované tiskové oblasti.

## Závěr

Nyní víte, jak **convert Excel to PowerPoint** a zároveň přesně **set print area excel** pomocí Aspose.Cells v C#. Tutoriál pokryl **how to export Excel**, demonstroval **how to set print area** a ukázal kompletní **convert excel to pptx**.

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area in Excel and Export to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}