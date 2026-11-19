---
category: general
date: 2026-11-19
description: Jak exportovat graf z Excelu jako PNG obrázek pomocí Aspose.Cells. Naučte
  se uložit obrázek grafu z Excelu a nastavit formát PNG během několika kroků.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel chart
- save excel chart image
- set image format png
- save excel picture file
language: cs
lastmod: 2026-11-19
og_description: Jak exportovat graf z Excelu jako PNG obrázek pomocí Aspose.Cells.
  Postupujte podle tohoto krok za krokem průvodce a efektivně uložte obrázek grafu
  z Excelu a nastavte formát PNG.
og_image_alt: How to export Excel chart as a PNG image
og_title: Jak exportovat graf z Excelu jako PNG obrázek – rychlý průvodce C#
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to export Excel chart as a PNG image using Aspose.Cells. Learn
    to save Excel chart image and set image format PNG in just a few steps.
  headline: How to export Excel chart as a PNG image with C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Chart export
title: Jak exportovat graf z Excelu jako PNG obrázek pomocí C#
url: /cs/net/chart-rendering-and-conversion/how-to-export-excel-chart-as-a-png-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak exportovat graf z Excelu jako PNG obrázek v C#

Pokud potřebujete **how to export Excel chart** do přenosného obrázku, tento průvodce ukazuje kompletní, připravené řešení. Pomocí Aspose.Cells můžete **save Excel chart image** ve formátu PNG pomocí pouhých tří řádků kódu a tutoriál také vysvětluje, jak **set image format png** a **save Excel picture file** bezpečně.

Na konci tohoto článku budete mít spustitelný program, který načte sešit, vykreslí první graf a zapíše soubor `pivot.png` na disk. Žádné další nástroje, žádné ruční kopírování – jen čistý C# kód, který můžete vložit do libovolného .NET projektu.

## Požadavky

Před zahájením se ujistěte, že máte:

* .NET 6.0 SDK nebo novější (kód také funguje s .NET Framework 4.6+)
* Visual Studio 2022 nebo jakýkoli C# editor
* Licence Aspose.Cells pro .NET (nebo dočasný evaluační klíč)
* Excel soubor (`pivot.xlsx`), který obsahuje alespoň jeden graf na první listu

Tyto položky jsou jediné externí závislosti; tutoriál nevyžaduje, aby byl na počítači nainstalován Office.

## Krok 1: Instalace Aspose.Cells

Otevřete terminál ve složce projektu a spusťte:

```bash
dotnet add package Aspose.Cells
```

Balíček přidá jmenný prostor `Aspose.Cells`, který poskytuje třídy `Workbook`, `ImageOrPrintOptions` a další potřebné pro **save Excel chart image**.

## Krok 2: Vytvoření minimálního konzolového programu

Vytvořte novou konzolovou aplikaci (`dotnet new console -n ExportChartDemo`) a nahraďte automaticky vygenerovaný soubor `Program.cs` následujícím kódem. Program demonstruje **how to export Excel chart** a obsahuje komentáře, které vysvětlují každé rozhodnutí.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for ImageOrPrintOptions
using System.Drawing.Imaging;  // Provides ImageFormat enum

namespace ExportChartDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook that contains the pivot chart
            // -----------------------------------------------------------------
            // Replace the path with the actual location of your Excel file.
            string workbookPath = @"YOUR_DIRECTORY\pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -----------------------------------------------------------------
            // 2️⃣ Set up image export options (PNG format)
            // -----------------------------------------------------------------
            // This is where we **set image format png** for the exported picture.
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: control the resolution (DPI) of the output image.
                // Higher DPI yields larger files but sharper charts.
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 3️⃣ Render the first picture (the chart) on the first worksheet
            // -----------------------------------------------------------------
            // Aspose.Cells stores charts as Picture objects inside the worksheet.
            // The index [0] refers to the first chart; adjust if you have multiple.
            Worksheet sheet = workbook.Worksheets[0];
            if (sheet.Pictures.Count == 0)
            {
                Console.WriteLine("No pictures found on the first worksheet.");
                return;
            }

            // Render the picture to a PNG file.
            string outputPath = @"YOUR_DIRECTORY\pivot.png";
            sheet.Pictures[0].RenderToImage(imageOptions, outputPath);

            Console.WriteLine($"Chart exported successfully to: {outputPath}");
        }
    }
}
```

### Proč je každá část důležitá

* **Loading the workbook** – `Workbook` parsuje soubor `.xlsx` bez potřeby nainstalovaného Microsoft Excel.
* **ImageOrPrintOptions** – Tento objekt řídí výstupní formát. Nastavením `ImageFormat = ImageFormat.Png` **sets image format png**, což je bezztrátový a široce podporovaný formát.
* **RenderToImage** – Metoda `RenderToImage` převádí graf (objekt `Picture`) na soubor obrázku. Metoda také automaticky zpracovává škálování, DPI a průhlednost.
* **Error handling** – Kontrola `sheet.Pictures.Count == 0` zabraňuje výjimce za běhu, pokud list neobsahuje žádné grafy, což je častý okrajový případ, když uživatelé ukazují na špatný list.

## Krok 3: Spuštění programu a ověření výsledku

1. Sestavte projekt: `dotnet build`.
2. Spusťte jej: `dotnet run --project ExportChartDemo`.

Pokud je vše správně nakonfigurováno, uvidíte:

```
Chart exported successfully to: YOUR_DIRECTORY\pivot.png
```

Otevřete `pivot.png` v libovolném prohlížeči obrázků. Měli byste vidět přesnou vizuální reprezentaci grafu z Excelu, což potvrzuje, že jste úspěšně **saved Excel picture file**.

### Očekávaný výstup

Níže je ukázka toho, jak může vypadat exportovaný PNG (skutečný graf závisí na vašem zdrojovém souboru).

![Exported Excel chart saved as PNG image](images/exported-chart.png){: .center alt="Jak exportovat graf z Excelu jako PNG obrázek"}

## Krok 4: Pokročilé možnosti – export více grafů

Pokud váš sešit obsahuje více než jeden graf, můžete projít kolekci `Pictures` pomocí smyčky:

```csharp
for (int i = 0; i < sheet.Pictures.Count; i++)
{
    string chartPath = $@"YOUR_DIRECTORY\chart_{i + 1}.png";
    sheet.Pictures[i].RenderToImage(imageOptions, chartPath);
    Console.WriteLine($"Chart {i + 1} saved to {chartPath}");
}
```

Tento vzor vám umožní **save Excel chart image** pro každý graf na listu, což je užitečné pro reportingové pipeline.

## Časté problémy a jak se jim vyhnout

| Příznak | Pravděpodobná příčina | Řešení |
|---------|-----------------------|--------|
| `ArgumentOutOfRangeException` on `Pictures[0]` | List nemá žádný graf nebo je graf na jiném listu. | Ověřte index listu (`Worksheets[0]`) a ujistěte se, že graf existuje. Použijte `Worksheets["SheetName"]`, pokud je potřeba. |
| Exported image is blurry | DPI nastavené příliš nízko (výchozí 96). | Zvyšte `HorizontalResolution` a `VerticalResolution` v `ImageOrPrintOptions`. |
| PNG file is empty or corrupted | Chybějící licence způsobující omezení evaluační verze. | Aplikujte platnou licenci Aspose.Cells před načtením sešitu (`License license = new License(); license.SetLicense("Aspose.Total.lic");`). |
| File path errors (`FileNotFoundException`) | Nesprávný zástupný text `YOUR_DIRECTORY`. | Použijte absolutní cesty nebo `Path.Combine(Environment.CurrentDirectory, "pivot.xlsx")`. |

Řešením těchto problémů zajistíte plynulý zážitek při **save excel picture file**.

## Pro tip: Export přímo do paměťového proudu

Někdy potřebujete obrázek v paměti (např. pro nahrání do webového API) místo zápisu na disk:

```csharp
using (var ms = new MemoryStream())
{
    sheet.Pictures[0].RenderToImage(imageOptions, ms);
    // ms now contains the PNG bytes – you can send them over HTTP, store in DB, etc.
}
```

Stejná logika **set image format png** se použije; pouze nahradíte cestu k souboru proudem.

## Závěr

Nyní víte, **how to export Excel chart** jako PNG soubor pomocí Aspose.Cells pro .NET. Tutoriál pokryl:

* Instalaci knihovny
* Načtení sešitu
* **Setting image format png**
* **Saving Excel chart image** na disk
* Zpracování více grafů a běžných chyb

S tímto základem můžete integrovat export grafů do automatizovaného reportingu, webových služeb nebo desktopových nástrojů. Dále prozkoumejte související témata, jako je **save excel picture file** jako JPEG (`ImageFormat.Jpeg`) nebo převod grafů do PDF pro tisknutelné zprávy.

Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Převod koláčového grafu z Excelu na obrázek pomocí Aspose.Cells .NET: Průvodce krok za krokem](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)
- [Export grafu jako PNG – Kompletní průvodce převodem Excelu do HTML s Aspose.Cells](/cells/english/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/)
- [Export buněk Excelu na obrázek pomocí Aspose.Cells .NET: Průvodce krok za krokem](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}