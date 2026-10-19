---
category: general
date: 2026-09-21
description: Exportujte Excel do PowerPointu s editovatelnými grafy pomocí Aspose.Cells.
  Postupujte podle tohoto krok‑za‑krokem návodu k převodu listu do formátu PPTX a
  zachování editovatelnosti grafů.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- worksheet to powerpoint
- export excel chart pptx
- editable charts pptx
language: cs
lastmod: 2026-09-21
og_description: Exportujte Excel do PowerPointu s editovatelnými grafy pomocí Aspose.Cells.
  Naučte se, jak převést list do PPTX a zachovat plnou editovatelnost grafů.
og_image_alt: Screenshot of a PowerPoint slide showing an editable Excel chart after
  export
og_title: Export Excel do PowerPointu s editovatelnými grafy – C# tutoriál
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  headline: Export Excel to PowerPoint with editable charts in C#
  type: TechArticle
- description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  name: Export Excel to PowerPoint with editable charts in C#
  steps:
  - name: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
    text: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
  - name: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
    text: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
  - name: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
    text: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
  - name: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
    text: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel‑to‑PowerPoint
- PPTX export
title: Exportovat Excel do PowerPointu s editovatelnými grafy v C#
url: /cs/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-editable-charts-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Excel do PowerPointu s editovatelnými grafy v C#

Export Excel do PowerPointu s editovatelnými grafy je běžná požadavek, když potřebujete znovu použít vizuály z tabulek v prezentacích. Tento průvodce vám ukáže, jak **exportovat Excel do PowerPointu**, přičemž zachová editovatelnost grafů, pomocí Aspose.Cells pro .NET.

Naučíte se, jak:

* Načíst existující sešit, který obsahuje grafy a textová pole.  
* Nastavit možnosti exportu PPTX tak, aby grafy a tvary zůstaly editovatelné.  
* Převést konkrétní list do souboru PowerPoint, který lze otevřít a upravit v Microsoft PowerPoint.

Předpokládá se, že máte základní znalosti C# a aktuální verzi .NET (≥ .NET 6). Předchozí zkušenost s Aspose.Cells není vyžadována.

---

## Export Excel do PowerPointu – přehled

Základní myšlenkou **exportu Excel do PowerPointu** je považovat každý list za zdroj obrázku, který lze vykreslit na PPTX snímek. Přepnutím příznaků `ExportChartAsEditableText` a `ExportShapeAsEditableText` Aspose.Cells zapisuje podkladová data grafu jako objekty kreslení PowerPointu místo plochého bitmapového obrazu. To způsobí, že výsledný snímek je plně editovatelný – stejně jako graf vytvořený přímo v PowerPointu.

> **Proč používat editovatelné grafy?**  
> Editovatelné grafy umožňují prezentujícím upravovat data, barvy nebo popisky bez nutnosti vracet se k původnímu souboru Excel, což urychluje poslední úpravy a udržuje plynulý průběh prezentace.

---

## Převod listu do PowerPointu (worksheet to PowerPoint)

Níže je kompletní, spustitelný příklad, který demonstruje konverzi **worksheet to PowerPoint**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the chart and textbox
            // Replace YOUR_DIRECTORY with the actual folder path on your machine.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Configure PPTX export options to keep charts and shapes editable
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,               // Target format: PPTX
                ExportChartAsEditableText = true,           // Enable editable charts
                ExportShapeAsEditableText = true            // Enable editable shapes/textboxes
            };

            // Step 3: Export the first worksheet (index 0) to a PowerPoint file
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";
            workbook.Worksheets[0].ConvertToImage(exportOptions, outputPath);

            Console.WriteLine($"Worksheet successfully exported to {outputPath}");
        }
    }
}
```

### Vysvětlení každého kroku

| Krok | Co kód dělá | Proč je to důležité pro **export excel chart pptx** |
|------|-------------------|----------------------------------------------|
| 1️⃣   | Načte `input.xlsx` do objektu `Aspose.Cells.Workbook`. | Sešit poskytuje přístup k grafům, které chcete exportovat. |
| 2️⃣   | Nastaví `ExportType` na `Pptx` a povolí `ExportChartAsEditableText` a `ExportShapeAsEditableText`. | Tyto příznaky jsou klíčem k **editable charts pptx** – říkají knihovně, aby zapisovala geometrii grafu jako objekty kreslení PowerPointu místo rastrových obrázků. |
| 3️⃣   | Volá `ConvertToImage` na první list, čímž vytvoří `Worksheet.pptx`. | Metoda provádí operaci **export excel to powerpoint** a zapíše soubor PPTX, který lze otevřít přímo v PowerPointu. |

> **Tip:** Pokud potřebujete exportovat *více* listů, projděte `workbook.Worksheets` v cyklu a pro každý zavolejte `ConvertToImage`, případně pojmenujte výstupní soubory `Sheet1.pptx`, `Sheet2.pptx` atd.

---

## Povolení editovatelných grafů v PPTX (export excel chart pptx)

Když je `ExportChartAsEditableText` nastaven na `true`, Aspose.Cells zapisuje každý graf jako kolekci elementů `<a:graphic>` uvnitř PPTX XML. PowerPoint pak tyto elementy považuje za nativní objekty grafu, na které můžete dvojklikem otevřít editor grafu.

**Časté úskalí**

* **Chybějící licence Aspose.Cells** – Bez licence knihovna přidá vodoznak do výstupu. Zaregistrujte licenci brzy ve vašem programu (`License license = new License(); license.SetLicense("Aspose.Cells.lic");`).  
* **Ne podporované typy grafů** – Zatímco většina 2‑D grafů (sloupcové, čárové, koláčové) je plně editovatelná, některé složité 3‑D nebo kombinované grafy mohou být převedeny na obrázky. Otestujte konkrétní typy grafů, pokud spoléháte na plnou editovatelnost.  
* **Velké listy** – Export velmi velkých listů může spotřebovat značnou paměť. Zvažte použití `ExportMaxRows` nebo `ExportMaxColumns` v `ImageOrPrintOptions` k omezení oblasti, která se převádí.

---

## Tipy pro zachování editovatelných grafů (editable charts pptx)

1. **Zachovat rozsahy dat grafu** – Ujistěte se, že zdroj dat grafu se nachází ve stejném listu, který exportujete. Odkazy napříč listy jsou v PPTX převedeny na statické hodnoty.  
2. **Používejte nejnovější verzi Aspose.Cells** – Nové vydání zlepšuje podporu dalších funkcí grafů a opravuje okrajové chyby související s exportem PPTX.  
3. **Ověřte výstup** – Po konverzi otevřete vygenerovaný PPTX v PowerPointu a ověřte, že můžete upravovat název grafu, řady a popisky os. Pokud se některý prvek zobrazuje jako obrázek, zkontrolujte, že je povolen `ExportChartAsEditableText` a že typ grafu je podporován.  
4. **Dávkové zpracování** – Pro automatizační scénáře (např. generování sady snímků z mnoha Excel reportů) zabalte logiku konverze do metody, která přijímá `Workbook`, `int worksheetIndex` a `string outputPath`. Tím se izoluje workflow **export excel to powerpoint** a učiní jej znovupoužitelným.

---

## Shrnutí kompletního funkčního příkladu

Spojením všeho dohromady zde máte minimální program, který můžete zkopírovat a vložit do nového .NET konzolového projektu:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Register license (optional but removes evaluation watermark)
            // var license = new License();
            // license.SetLicense("Aspose.Cells.lic");

            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";

            Workbook workbook = new Workbook(inputPath);

            ImageOrPrintOptions options = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,
                ExportChartAsEditableText = true,
                ExportShapeAsEditableText = true
            };

            workbook.Worksheets[0].ConvertToImage(options, outputPath);

            Console.WriteLine($"Export complete: {outputPath}");
        }
    }
}
```

**Očekávaný výsledek**

* Soubor pojmenovaný `Worksheet.pptx` se objeví v `YOUR_DIRECTORY`.  
* Otevření souboru v Microsoft PowerPoint zobrazí snímek obsahující původní graf a případná textová pole.  
* Dvojklik na graf otevře editor grafu v PowerPointu, což vám umožní změnit hodnoty řad, barvy nebo názvy os – čímž se ověří, že funkce **editable charts pptx** funguje podle očekávání.

---

## Závěr

Nyní máte kompletní řešení pro **export Excel do PowerPointu**, které zachovává editovatelnost grafů. Nastavením `ImageOrPrintOptions` s `ExportChartAsEditableText` a `ExportShapeAsEditableText` proces konverze vytvoří nativní soubor PPTX, kde se grafy chovají stejně jako ty vytvořené přímo v PowerPointu.  

Od zde můžete:

* Rozšířit kód tak, aby zvládal více listů (**worksheet to PowerPoint** pro každý).  
* Kombinovat export s dalšími funkcemi Aspose.Cells, jako je přidání názvů snímků nebo vkládání obrázků.  
* Prozkoumat související témata, jako je **export Excel chart PPTX** s vlastními motivy nebo automatizace celého procesu generování sady snímků.

Klidně experimentujte s různými typy grafů, přidávejte popisky dat nebo integrujte tento workflow do většího reportovacího systému. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s krok‑za‑krokem vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak převést Excel do PowerPointu pomocí Aspose.Cells pro .NET: Kompletní průvodce](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}