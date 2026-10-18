---
category: general
date: 2026-06-27
description: Jak exportovat Excel pomocí C# — naučte se převádět Excel do PowerPointu,
  vytvářet PowerPoint z Excelu a načíst sešit Excel v C# během několika minut.
draft: false
keywords:
- how to export excel
- convert excel to powerpoint
- create powerpoint from excel
- load excel workbook c#
- export excel chart powerpoint
language: cs
og_description: Jak exportovat Excel pomocí C# je jednoduché. Postupujte podle tohoto
  krok‑za‑krokem tutoriálu, abyste převáděli Excel do PowerPointu, vytvořili PowerPoint
  z Excelu a načetli Excel sešit v C#.
og_title: Jak exportovat Excel do PowerPointu – Kompletní průvodce C#
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to export Excel using C#—learn to convert Excel to PowerPoint,
    create PowerPoint from Excel, and load Excel workbook C# in minutes.
  headline: How to Export Excel to PowerPoint – Complete C# Guide
  type: TechArticle
- description: How to export Excel using C#—learn to convert Excel to PowerPoint,
    create PowerPoint from Excel, and load Excel workbook C# in minutes.
  name: How to Export Excel to PowerPoint – Complete C# Guide
  steps:
  - name: '**Load Excel workbook** – We read the `.xlsx` file into memory.'
    text: '**Load Excel workbook** – We read the `.xlsx` file into memory.'
  - name: '**Convert workbook to a PowerPoint presentation** – Aspose converts each
      worksheet (or selected chart) into a slide.'
    text: '**Convert workbook to a PowerPoint presentation** – Aspose converts each
      worksheet (or selected chart) into a slide.'
  - name: '**Save the generated presentation** – The final PPTX can be opened in PowerPoint,
      edited, or sent to stakeholders.'
    text: '**Save the generated presentation** – The final PPTX can be opened in PowerPoint,
      edited, or sent to stakeholders.'
  type: HowTo
- questions:
  - answer: Yes. Use `Workbook.Worksheets["Sheet1"]` to isolate a sheet, then call
      `SaveToPresentation` on that worksheet alone.
    question: Can I export only a single worksheet instead of the whole workbook?
  - answer: Macros are not transferred to PowerPoint—only visual objects (charts,
      tables) are exported. If you need macro functionality, consider generating the
      slides first, then adding VBA manually.
    question: What about preserving macros?
  - answer: Absolutely. Aspose.Cells supports legacy formats; just change the file
      extension in `excelPath`.
    question: Does this work with `.xls` files?
  - answer: 'After creating the `Presentation` object, set: ```csharp presentation.SlideSize.Size
      = SlideSizeType.Widescreen; ```'
    question: How do I change the slide size to widescreen (16:9)?
  - answer: 'Open‑source libraries like EPPlus can read Excel, but they don’t provide
      direct Excel‑to‑PowerPoint conversion. You’d need to manually render charts
      to images and insert them, which is far more code. ## Tips & Best Practices
      - **Batch processing:** If you have dozens of workbooks, wrap the conversio'
    question: Is there a free alternative?
  type: FAQPage
tags:
- C#
- Excel
- PowerPoint
- Aspose
title: Jak exportovat Excel do PowerPointu – kompletní průvodce C#
url: /cs/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak exportovat Excel do PowerPointu – Kompletní průvodce v C#

Už jste se někdy zamýšleli **jak exportovat data z Excelu** přímo do prezentace PowerPoint, aniž byste ztratili formátování? Nejste v tom sami. V mnoha reportovacích řetězcích je úzkým místem přesun grafů a tabulek z Excel sešitu do elegantní sady slidů. Dobrá zpráva? Pouhých několik řádků C# vám umožní **převést Excel do PowerPointu**, vygenerovat plně editovatelný PPTX a dokonce zachovat věrnost grafů.

V tomto tutoriálu si projdeme načtení Excel sešitu v C#, převod jeho obsahu na prezentaci PowerPoint a uložení výsledku. Na konci budete schopni **automaticky vytvořit PowerPoint z Excelu** – bez ručního kopírování a vkládání. Žádné těžkopádné UI, jen čistý kód.

> **Co budete potřebovat**  
> * .NET 6+ (nebo .NET Framework 4.7.2+)  
> * NuGet balíčky Aspose.Cells a Aspose.Slides (zvládnou těžkou práci)  
> * Ukázkový Excel soubor s alespoň jedním grafem (pojmenujeme ho `chartOle.xlsx`)  

Pokud máte vše připravené, pojďme na to.

![Diagram ukazující, jak exportovat Excel do PowerPointu pomocí C#](https://example.com/images/export-excel-to-pptx.png "Diagram Jak exportovat Excel do PowerPointu")

## Jak exportovat Excel do PowerPointu pomocí C# – Přehled

Než začneme psát kód, je dobré pochopit trojstupňový tok:

1. **Načíst Excel sešit** – Načteme soubor `.xlsx` do paměti.  
2. **Převést sešit na prezentaci PowerPoint** – Aspose převádí každý list (nebo vybraný graf) na slide.  
3. **Uložit vygenerovanou prezentaci** – Výsledný PPTX lze otevřít v PowerPointu, upravit nebo poslat stakeholderům.

Každý krok je záměrně oddělený, abyste mohli později přidat vlastní logiku (např. vybrat konkrétní listy, aplikovat motivy slidů atd.). Nyní si to rozebráme podrobně.

## Krok 1 – Načtení Excel sešitu v C# stylu

Prvním, co musíte udělat, je načíst Excel soubor do vaší aplikace. S Aspose.Cells je kód přímočarý:

```csharp
using Aspose.Cells;   // Handles Excel files
using Aspose.Slides;  // Handles PowerPoint files
using System;

// Step 1: Load the Excel workbook
string excelPath = @"YOUR_DIRECTORY\chartOle.xlsx";

if (!System.IO.File.Exists(excelPath))
{
    throw new FileNotFoundException($"Excel file not found at {excelPath}");
}

// The Workbook class reads the .xlsx file into memory
Workbook workbook = new Workbook(excelPath);
```

**Proč je to důležité:**  
`Workbook` abstrahuje celý sešit, poskytuje přístup k listům, buňkám a – co je klíčové – vloženým grafům. Pokud vynecháte kontrolu existence souboru, později narazíte na nejasnou `FileNotFoundException`, což může být v produkci noční můra při ladění.

**Tip:** Pokud potřebujete jen konkrétní list, můžete předat objekt `LoadOptions` a omezit tak využití paměti:

```csharp
LoadOptions options = new LoadOptions(LoadFormat.Xlsx) { LoadDataOnly = true };
Workbook workbook = new Workbook(excelPath, options);
```

Tato malá úprava dramaticky zrychlí práci s velkými sešity.

## Krok 2 – Převod Excelu do PowerPointu (Export Excel grafu do PowerPointu)

Nyní přichází magie: převod sešitu na PPTX. Aspose.Slides nabízí jedinou metodu, která udělá těžkou práci:

```csharp
// Step 2: Convert the workbook to a PowerPoint presentation (PPTX format)
Presentation presentation = workbook.SaveToPresentation(ExportToPresentationFormat.Pptx);
```

**Co se děje pod kapotou?**  
`SaveToPresentation` prochází každý list, extrahuje objekty grafů a vytvoří slide pro každý graf. Metoda zachovává původní styl grafu, takže barvy, písma a popisky dat zůstávají nedotčeny. Pokud váš sešit obsahuje jen tabulky, budou na slidu vykresleny jako textová pole.

**Hraniční případ – více grafů:**  
Pokud list obsahuje více než jeden graf, Aspose je na stejném slidu seskupí vertikálně. Chcete-li je mít na oddělených slidech, můžete grafy projít ručně:

```csharp
Presentation presentation = new Presentation();

foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (Chart chart in sheet.Charts)
    {
        // Export each chart as an individual slide
        ISlide slide = presentation.Slides.AddEmptySlide(presentation.SlideSize.Size);
        chart.ExportToSlide(presentation, slide);
    }
}
```

Tento úryvek vám dává jemnou kontrolu – ideální pro profesionální prezentaci.

## Krok 3 – Uložení vygenerované prezentace (Vytvořit PowerPoint z Excelu)

Poslední krok je zapsat PPTX soubor na disk. Je to tak jednoduché:

```csharp
// Step 3: Save the generated presentation to a file
string pptxPath = @"YOUR_DIRECTORY\editable.pptx";
presentation.Save(pptxPath, Aspose.Slides.Export.SaveFormat.Pptx);

Console.WriteLine($"Presentation saved successfully to {pptxPath}");
```

**Proč je dobré výstup ověřit:**  
Po uložení otevřete `editable.pptx` v PowerPointu. Měli byste vidět jeden slide na graf, každý plně editovatelný (můžete měnit barvy, přesouvat objekty atd.). Pokud graf vypadá špatně, zkontrolujte, že původní Excel graf používá standardní písma – některá vlastní písma se nemusí správně vložit.

**Častý úskalí:**  
Ukládání na síťový sdílený adresář bez odpovídajících oprávnění vyvolá `UnauthorizedAccessException`. Ujistěte se, že běžící účet má právo zápisu do `YOUR_DIRECTORY`.

## Kompletní funkční příklad – Všechny kroky dohromady

Níže je kompletní, připravený program. Vložte jej do nového projektu Console App, obnovte NuGet balíčky a stiskněte **F5**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Paths – adjust to your environment
            string excelPath = @"YOUR_DIRECTORY\chartOle.xlsx";
            string pptxPath = @"YOUR_DIRECTORY\editable.pptx";

            // -------------------------------------------------
            // Step 1: Load the Excel workbook (load excel workbook c#)
            // -------------------------------------------------
            if (!System.IO.File.Exists(excelPath))
            {
                Console.WriteLine($"Error: File not found -> {excelPath}");
                return;
            }

            Workbook workbook = new Workbook(excelPath);
            Console.WriteLine("Excel workbook loaded successfully.");

            // -------------------------------------------------
            // Step 2: Convert Excel to PowerPoint (export excel chart powerpoint)
            // -------------------------------------------------
            Presentation presentation = workbook.SaveToPresentation(ExportToPresentationFormat.Pptx);
            Console.WriteLine("Workbook converted to PowerPoint.");

            // -------------------------------------------------
            // Step 3: Save the generated presentation (create powerpoint from excel)
            // -------------------------------------------------
            presentation.Save(pptxPath, Aspose.Slides.Export.SaveFormat.Pptx);
            Console.WriteLine($"Presentation saved at: {pptxPath}");
        }
    }
}
```

**Očekávaný výstup (konzole):**

```
Excel workbook loaded successfully.
Workbook converted to PowerPoint.
Presentation saved at: YOUR_DIRECTORY\editable.pptx
```

Otevřete `editable.pptx` a uvidíte slide pro každý graf, připravený k dalším úpravám.

## Často kladené otázky (FAQ)

**Q: Můžu exportovat jen jeden list místo celého sešitu?**  
A: Ano. Použijte `Workbook.Worksheets["Sheet1"]` k izolaci listu a poté zavolejte `SaveToPresentation` jen na tomto listu.

**Q: Co s makry?**  
A: Makra nejsou přenášena do PowerPointu – exportují se jen vizuální objekty (grafy, tabulky). Pokud potřebujete makra, vytvořte slidy nejprve a poté přidejte VBA ručně.

**Q: Funguje to i s `.xls` soubory?**  
A: Rozhodně. Aspose.Cells podporuje starší formáty; stačí změnit příponu v `excelPath`.

**Q: Jak změnit velikost slidu na widescreen (16:9)?**  
A: Po vytvoření objektu `Presentation` nastavte:

```csharp
presentation.SlideSize.Size = SlideSizeType.Widescreen;
```

**Q: Existuje zdarma alternativa?**  
A: Open‑source knihovny jako EPPlus umí číst Excel, ale neposkytují přímý převod Excel → PowerPoint. Museli byste grafy nejprve vykreslit jako obrázky a pak je vložit, což vyžaduje podstatně více kódu.

## Tipy a osvědčené postupy

- **Dávkové zpracování:** Pokud máte desítky sešitů, zabalte převod do smyčky `Parallel.ForEach` – dejte však pozor na thread‑unsafe objekty Aspose.  
- **Správa paměti:** Zavolejte `presentation.Dispose()` a `workbook.Dispose()` při práci s velkými soubory, aby se rychle uvolnily nativní zdroje.  
- **Styling slidů:** Po převodu můžete aplikovat motiv hlavního slidu pomocí `presentation.SlideMaster` a zajistit tak jednotný vzhled všech slidů.  
- **Testování:** Automatizujte jednoduchý unit test, který načte známý sešit, spustí převod a ověří, že výsledný PPTX obsahuje očekávaný počet slidů.

## Závěr

Ukázali jsme vám **jak exportovat data z Excelu** do prezentace PowerPoint pomocí C#. Načtením sešitu, převodem pomocí Aspose a uložením PPTX máte nyní opakovatelný, programovatelný způsob, jak **převést Excel do PowerPointu**, **vytvořit PowerPoint z Excelu** a **načíst Excel sešit v C# stylu** bez ručního úsilí. Kód je samostatný, funguje na jakémkoli moderním .NET runtime a lze jej rozšířit pro složité reportovací řetězce.

Připravení na další výzvu? Zkuste vložit více grafů na jeden slide, aplikovat vlastní rozvržení slidů nebo automaticky generovat poznámky k řečníkovi. Možnosti jsou neomezené, když spojíte automatizaci Excelu s generováním PowerPointu.

Máte otázky nebo zajímavý případ použití? Napište komentář níže a šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vlastních projektech.

- [Jak převést Excel do PowerPointu pomocí Aspose.Cells pro .NET: Kompletní průvodce](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Jak exportovat grafy z Excelu do PDF pomocí Aspose.Cells pro .NET: Krok za krokem](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Jak exportovat Excel do HTML s mřížkami pomocí Aspose.Cells pro .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}