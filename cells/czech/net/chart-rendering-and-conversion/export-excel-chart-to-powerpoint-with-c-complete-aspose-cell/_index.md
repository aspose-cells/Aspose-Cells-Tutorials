---
category: general
date: 2026-08-04
description: Exportujte graf z Excelu do PowerPointu pomocí Aspose.Cells v C#. Postupujte
  podle tohoto podrobného průvodce konverzí z Excelu do PowerPointu a zachovejte editovatelnost
  tvarů.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel chart to powerpoint
- Aspose.Cells PPTX export
- editable shapes in PowerPoint
- Excel to PowerPoint conversion
- C# chart export
language: cs
lastmod: 2026-08-04
og_description: Exportujte graf z Excelu do PowerPointu pomocí Aspose.Cells v C#.
  Naučte se vytvořit editovatelný PPTX, zachovat data grafu a automatizovat konverzi
  z Excelu do PowerPointu.
og_image_alt: Screenshot of an Excel chart rendered as an editable PowerPoint slide
og_title: Exportujte graf z Excelu do PowerPointu pomocí C# – kompletní tutoriál Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  headline: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  type: TechArticle
- description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  name: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  steps:
  - name: Expected output
    text: '| File name | Content on slide | |--------------------------|------------------------------------------|
      | `ShapesExport.pptx` | The chart from `Shapes.xlsx` rendered as an editable
      PowerPoint chart, with axis labels, legends, and data series intact. |'
  - name: Exporting multiple worksheets
    text: If you need a slide for each worksheet, loop through `workbook.Worksheets`
      and call `Save` with a unique file name for each iteration.
  - name: Controlling slide layout
    text: Aspose.Slides lets you add a custom slide layout after the export. Create
      a new presentation, import the generated slide, and then apply a master theme.
  - name: Handling charts with external data sources
    text: If a chart references a data range outside the defined print area, extend
      the `PrintArea` to include those cells. Otherwise the chart may lose data series
      during export.
  - name: Licensing considerations
    text: 'Aspose libraries work in evaluation mode with a watermark. To remove the
      watermark, set the license before any API call:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- PowerPoint
title: Export grafu z Excelu do PowerPointu pomocí C# – kompletní průvodce Aspose.Cells
url: /cs/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Excel chart to PowerPoint s C# – kompletní průvodce Aspose.Cells

Pokud potřebujete **exportovat graf z Excelu do PowerPointu**, tento tutoriál vám ukáže, jak to provést pomocí Aspose.Cells a Aspose.Slides v C#. Získáte plně editovatelný PPTX, který zachovává data grafu i tvary, takže konverze je připravena na další úpravy designu.

Export grafů z Excelu do PowerPointu je běžná potřeba při tvorbě automatizovaných reportovacích pipeline, prodejních prezentací nebo výukových materiálů. V tomto průvodci se naučíte přesné kroky pro **konverzi Excel → PowerPoint**, která ponechává všechny prvky grafu editovatelné. Není potřeba ruční kopírování‑vkládání a kód funguje jak s .NET 6+, tak s klasickým .NET Framework.

## Požadavky

Než začnete, ujistěte se, že máte:

- Platnou licenci Aspose.Cells (nebo bezplatný evaluační klíč)  
- Aspose.Slides pro .NET přidaný do projektu (knihovna zajišťuje výstup PPTX)  
- Nainstalovaný .NET 6 SDK nebo novější  
- Excel sešit, který obsahuje alespoň jeden graf (pro tento příklad používáme `Shapes.xlsx`)  

NuGet balíčky můžete nainstalovat pomocí následujících příkazů:

```bash
dotnet add package Aspose.Cells
dotnet add package Aspose.Slides
```

## Krok 1: Načtení Excel sešitu

Prvním krokem je otevřít sešit, který obsahuje graf, jenž chcete exportovat. Třída `Workbook` představuje celý Excel soubor.

```csharp
using Aspose.Cells;
using Aspose.Slides;   // required for PPTX output

// Load the Excel workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

**Proč je to důležité:** Načtením sešitu získáte přístup k jeho listům, grafům a formátování. Aspose.Cells čte soubor bez nutnosti mít nainstalovaný Microsoft Office, což řešení udržuje lehkým a server‑friendly.

## Krok 2: Výběr listu a definování tiskové oblasti

List může obsahovat mnoho grafů, ale obvykle exportujete konkrétní oblast. Nastavením `PrintArea` řeknete Aspose.Cells, které buňky (včetně grafů) mají být vykresleny.

```csharp
// Choose the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Define the area that contains the chart and any supporting data
worksheet.PageSetup.PrintArea = "A1:G30";
```

**Proč je to důležité:** Omezením exportu na definovanou tiskovou oblast se vyhnete zbytečným prázdným snímkům a udržíte velikost PPTX souboru malou. Oblast lze upravit tak, aby přesně odpovídala rozsahu vašeho grafu.

## Krok 3: Konfigurace exportních možností pro editovatelný PPTX

Aspose.Cells používá třídu `ImageOrPrintOptions` k řízení výstupního formátu a editovatelnosti. Nastavením `ImageFormat` na `ImageFormat.Pptx` vytvoříte PowerPoint soubor, zatímco `ExportEditableShapes = true` zachová grafické objekty jako editovatelné tvary.

```csharp
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Pptx,   // Target format
    ExportEditableShapes = true       // Keep shapes/textboxes editable
};

// Attach the options to the worksheet's print settings
worksheet.PageSetup.PrintOptions = exportOptions;
```

**Proč je to důležité:** Příznak `ExportEditableShapes` je klíčem k výsledku **editovatelných tvarů v PowerPointu**. Bez něj by byl graf rasterizován jako obrázek a ztratil by možnost později měnit datové body nebo stylování.

## Krok 4: Uložení listu jako PowerPoint prezentace

Nakonec zavolejte metodu `Save` na objektu `Workbook`. Výčtový typ `SaveFormat.Pptx` říká Aspose.Cells, aby vytvořil PowerPoint soubor.

```csharp
// Export the selected worksheet to a PPTX file
workbook.Save("YOUR_DIRECTORY/ShapesExport.pptx", SaveFormat.Pptx);
```

Po dokončení kódu otevřete `ShapesExport.pptx` v PowerPointu. Uvidíte snímek, který obsahuje původní Excel graf jako nativní PowerPoint grafický objekt. Dvojklikem na graf můžete upravit data, změnit barvy nebo přidat animace – stejně jako kdybyste graf vytvořili přímo v PowerPointu.

### Očekávaný výstup

| Název souboru            | Obsah na snímku                         |
|--------------------------|------------------------------------------|
| `ShapesExport.pptx`      | Graf z `Shapes.xlsx` vykreslený jako editovatelný PowerPoint graf, se zachovanými popisky os, legendami a datovými sériemi. |

## Kompletní, spustitelný příklad

Níže je celý program, který můžete zkopírovat, vložit a spustit. Obsahuje všechny potřebné `using` direktivy, ošetření chyb a komentáře.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;   // Required for PPTX output

class ExcelToPowerPoint
{
    static void Main()
    {
        // Path to the source Excel file – adjust as needed
        const string excelPath = "YOUR_DIRECTORY/Shapes.xlsx";
        // Path for the generated PowerPoint file
        const string pptxPath = "YOUR_DIRECTORY/ShapesExport.pptx";

        try
        {
            // Load the workbook
            Workbook workbook = new Workbook(excelPath);

            // Use the first worksheet (you can change the index or name)
            Worksheet worksheet = workbook.Worksheets[0];

            // Define the area that contains the chart
            worksheet.PageSetup.PrintArea = "A1:G30";

            // Set export options for PPTX with editable shapes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Pptx,
                ExportEditableShapes = true
            };
            worksheet.PageSetup.PrintOptions = exportOptions;

            // Save as PPTX
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export successful. PPTX saved to: {pptxPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**Vysvětlení jednotlivých bloků**

| Blok | Účel |
|------|------|
| `using` directives | Načte jmenné prostory Aspose.Cells a Aspose.Slides. |
| `Workbook workbook = new Workbook(excelPath);` | Načte Excel soubor bez nutnosti mít nainstalovaný Office. |
| `worksheet.PageSetup.PrintArea = "A1:G30";` | Omezí export na oblast, která obsahuje graf. |
| `ImageOrPrintOptions` | Konfiguruje výstup PPTX a povoluje **Aspose.Cells PPTX export** s editovatelnými tvary. |
| `workbook.Save(pptxPath, SaveFormat.Pptx);` | Zapíše PowerPoint soubor na disk. |
| `try / catch` | Poskytuje základní ošetření chyb pro chybějící soubory nebo licenční problémy. |

Spuštěním tohoto programu získáte PowerPoint snímek, který můžete otevřít v Microsoft PowerPoint, Google Slides (po konverzi) nebo v jakémkoli kompatibilním prohlížeči.

## Běžné varianty a okrajové případy

### Export více listů

Pokud potřebujete snímek pro každý list, projděte `workbook.Worksheets` a zavolejte `Save` s unikátním názvem souboru pro každou iteraci.

```csharp
int index = 1;
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.PageSetup.PrintOptions = exportOptions;
    string fileName = $"Slide{index++}.pptx";
    workbook.Save(fileName, SaveFormat.Pptx);
}
```

### Řízení rozvržení snímku

Aspose.Slides vám umožní po exportu přidat vlastní rozvržení snímku. Vytvořte novou prezentaci, importujte vygenerovaný snímek a poté aplikujte hlavní téma.

```csharp
using Aspose.Slides.Export;

// Load the PPTX created by Aspose.Cells
Presentation pres = new Presentation(pptxPath);

// Apply a built‑in layout (e.g., Title and Content)
pres.Slides[0].LayoutSlide = pres.LayoutSlides[(int)SlideLayoutType.TitleAndContent];

// Save the final presentation
pres.Save("FinalPresentation.pptx", SaveFormat.Pptx);
```

### Práce s grafy, které používají externí zdroje dat

Pokud graf odkazuje na datový rozsah mimo definovanou tiskovou oblast, rozšiřte `PrintArea`, aby zahrnovala i tyto buňky. Jinak může graf při exportu ztratit datové série.

### Licenční úvahy

Knihovny Aspose fungují v evaluačním režimu s vodoznakem. Pro odstranění vodoznaku nastavte licenci před jakýmkoli voláním API:

```csharp
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

Totéž udělejte pro Aspose.Slides, pokud používáte jeho pokročilé funkce.

## Pro tipy

- **Znovupoužití exportních možností:** Vytvořte jedinou instanci `ImageOrPrintOptions` a přiřaďte ji každému listu, aby byl kód DRY.  
- **Dávkové zpracování:** Pro rozsáhlé reportování kombinujte tuto logiku exportu s background workerem nebo Azure Function, abyste generovali PPTX soubory na vyžádání.  
- **Výkon:** Pokud potřebujete jen obrázek grafu (ne editovatelný), nastavte `ExportEditableShapes = false`. Tím snížíte využití paměti a urychlíte konverzi.  
- **Testování:** Ověřte vygenerovaný PPTX jak na Windows, tak na macOS instalacích PowerPointu, protože některé renderovací odchylky se liší mezi platformami.

## Závěr

Nyní máte kompletní end‑to‑end řešení pro **export grafu z Excelu do PowerPointu** pomocí C#. Tutoriál pokryl načtení sešitu, výběr tiskové oblasti, konfiguraci **Aspose.Cells PPTX exportu** s **editovatelnými tvary v PowerPointu** a uložení výsledku jako plně editovatelného PPTX souboru.  

Odtud můžete zkoumat další scénáře **Excel → PowerPoint konverze**, jako je dávkový export, vlastní rozvržení snímků nebo integrace procesu do webového API. Experimentujte s různými typy grafů, přidávejte obrázky nebo kombinujte více listů do jedné prezentace, aby výstup odpovídal vašim obchodním potřebám.

Jste připraveni automatizovat svůj reportingový workflow? Vyzkoušejte výměnu zdrojového souboru, úpravu tiskové oblasti a integraci kódu do vašich existujících .NET služeb. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Jak převést Excel do PowerPointu pomocí Aspose.Cells pro .NET: Kompletní průvodce](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Jak exportovat grafy z Excelu do PDF pomocí Aspose.Cells pro .NET: Krok za krokem](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Export buněk z Excelu do obrázku pomocí Aspose.Cells .NET: Krok za krokem](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}