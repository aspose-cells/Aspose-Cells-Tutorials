---
category: general
date: 2026-10-26
description: Naučte se exportovat grafy z Excelu do PowerPointu pomocí C#. Zachovejte
  editovatelnost tvarů a uložte jako PPTX pomocí několika řádků kódu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel charts to powerpoint
- Aspose.Cells export
- C# Excel to PowerPoint conversion
- preserve shape editability
- SaveFormat.Pptx
- Workbook.Save method
language: cs
lastmod: 2026-10-26
og_description: Exportujte grafy z Excelu do PowerPointu pomocí C#. Tento průvodce
  ukazuje, jak zachovat editovatelnost tvarů a uložit jako PPTX pomocí Aspose.Cells.
og_image_alt: Export Excel charts to PowerPoint example showing a chart transferred
  from Excel to a slide
og_title: Export grafů z Excelu do PowerPointu pomocí C# – krok za krokem průvodce
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  headline: How to export Excel charts to PowerPoint using C#
  type: TechArticle
- description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  name: How to export Excel charts to PowerPoint using C#
  steps:
  - name: Load the Excel workbook
    text: '```csharp using Aspose.Cells;'
  - name: (Optional) Adjust workbook settings
    text: In most cases the default settings are sufficient for a clean export. However,
      if you need to change the calculation mode, page setup, or hide certain sheets,
      you can do it here.
  - name: Save the workbook as a PowerPoint file
    text: '```csharp // Export the workbook to PPTX while keeping chart shapes editable
      workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx); ```'
  - name: Verify the result
    text: 'Open `Shapes.pptx` in PowerPoint and:'
  - name: 'Edge case: Exporting multiple worksheets with separate charts'
    text: If your Excel file contains several worksheets, each with its own chart,
      Aspose.Cells creates a separate slide for each chart automatically. You can
      control slide order by rearranging worksheets before the save operation.
  - name: 'Performance tip: Stream the output instead of writing to disk'
    text: When generating PowerPoint files in a web API, avoid temporary files by
      writing to a `MemoryStream`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- PowerPoint
title: Jak exportovat grafy z Excelu do PowerPointu pomocí C#
url: /cs/net/chart-rendering-and-conversion/how-to-export-excel-charts-to-powerpoint-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak exportovat grafy z Excelu do PowerPointu pomocí C#

Pokud potřebujete **exportovat grafy z Excelu do PowerPointu**, tento průvodce vás provede kompletním, připraveným řešením. Ať už vytváříte reportingový dashboard nebo automatizujete prezentace, uvidíte, jak několik řádků C# kódu udrží tvary vašich grafů plně editovatelné po konverzi.

V tomto tutoriálu se naučíte:

* Načíst existující Excel sešit, který obsahuje grafy.  
* (Volitelně) upravit nastavení sešitu před konverzí.  
* Uložit sešit jako PowerPoint soubor při zachování editovatelnosti tvarů.  

Vše je provedeno pomocí **Aspose.Cells for .NET**, knihovny, která provádí konverzi z Excelu do PowerPointu bez nutnosti Microsoft Office na serveru.

## Co budete potřebovat

| Požadavek | Důvod |
|-------------|--------|
| .NET 6.0 nebo novější | Moderní runtime s plnými jazykovými funkcemi |
| Visual Studio 2022 (nebo jakékoli IDE) | Pohodlný editor a debugger |
| **Aspose.Cells for .NET** NuGet balíček | Poskytuje třídu `Workbook` a podporu `SaveFormat.Pptx` |
| Excel soubor (`ChartAndShapes.xlsx`) obsahující alespoň jeden graf | Zdroj grafů, které chcete exportovat |

> **Pro tip:** Použijte bezplatnou verzi **Aspose.Cells Evaluation** k otestování kódu; licenční klíč odstraní vodoznak hodnocení.

```bash
dotnet add package Aspose.Cells
```

## Export grafů z Excelu do PowerPointu – kompletní workflow

Níže je kompletní kód, který provádí export při **zachování editovatelnosti tvarů**. Každý krok je podrobně vysvětlen.

### Krok 1: Načíst Excel sešit

```csharp
using Aspose.Cells;

// Load the workbook that holds the charts you want to export
Workbook workbook = new Workbook(@"C:\Projects\ChartAndShapes.xlsx");
```

*Třída `Workbook` představuje celý Excel soubor. Načtení souboru načte všechny listy, grafy a tvary do paměti, což je nutné pro další manipulaci.*

### Krok 2: (Volitelně) Upravit nastavení sešitu

Ve většině případů jsou výchozí nastavení dostatečná pro čistý export. Pokud však potřebujete změnit režim výpočtu, nastavení stránky nebo skrýt určité listy, můžete to provést zde.

```csharp
// Example: ensure all formulas are calculated before export
workbook.CalculateFormula();

// Example: hide a sheet that you don’t want in the PowerPoint
workbook.Worksheets["SecretData"].IsVisible = false;
```

> **Proč je to důležité:** Úprava nastavení před konverzí zajišťuje, že vygenerované snímky odrážejí přesně požadovaný stav, zejména když vzorce nebo skryté listy mohou ovlivnit data grafu.

### Krok 3: Uložit sešit jako PowerPoint soubor

```csharp
// Export the workbook to PPTX while keeping chart shapes editable
workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx);
```

*Konstanta `SaveFormat.Pptx` říká Aspose.Cells, aby vytvořil PowerPoint prezentaci. Interně knihovna převádí každý Excel graf na PowerPoint tvar, který zůstává plně editovatelný v Microsoft PowerPoint.*

### Krok 4: Ověřit výsledek

Otevřete `Shapes.pptx` v PowerPointu a:

1. Vyberte graf na libovolném snímku.  
2. Klikněte pravým tlačítkem → **Edit Data**.  
3. Potvrďte, že se zobrazí tabulka dat grafu a můžete měnit hodnoty.

Pokud se graf otevře v panelu **Edit Data**, konverze byla úspěšná a **editovatelnost tvarů** je zachována.

![Export Excel charts to PowerPoint example](export-excel-charts-to-powerpoint.png){.img-fluid alt="Příklad exportu grafů z Excelu do PowerPointu"}

## Časté problémy a jak se jim vyhnout

| Problém | Příčina | Řešení |
|-------|-------|-----|
| Grafy se zobrazují jako statické obrázky | Použití starší verze Aspose.Cells, která nepodporuje export do PPTX | Aktualizujte na nejnovější Aspose.Cells 23.x nebo novější |
| Chybějící data v PowerPoint grafu | Sešit nebyl před exportem plně vypočítán | Zavolejte `workbook.CalculateFormula()` před `Save` |
| Tvary nejsou editovatelné | Ukládání pomocí `SaveFormat.Xlsx` místo `SaveFormat.Pptx` | Ujistěte se, že předáváte `SaveFormat.Pptx` metodě `Workbook.Save` |
| Výjimka licence za běhu | Evaluační verze bez registrované licence | Zaregistrujte licenci pomocí `License license = new License(); license.SetLicense("Aspose.Cells.lic");` |

### Okrajový případ: Export více listů s oddělenými grafy

Pokud váš Excel soubor obsahuje několik listů, každý s vlastním grafem, Aspose.Cells automaticky vytvoří samostatný snímek pro každý graf. Pořadí snímků můžete ovládat přeuspořádáním listů před operací uložení.

```csharp
// Move the worksheet that should appear first in the slide deck
workbook.Worksheets.MoveTo(2, 0); // move sheet index 2 to position 0
```

### Tip pro výkon: Streamovat výstup místo zápisu na disk

Při generování PowerPoint souborů ve webovém API se vyhněte dočasným souborům tím, že zapíšete do `MemoryStream`.

```csharp
using (MemoryStream pptStream = new MemoryStream())
{
    workbook.Save(pptStream, SaveFormat.Pptx);
    // Return the stream as a file download
    FileContentResult result = new FileContentResult(pptStream.ToArray(),
        "application/vnd.openxmlformats-officedocument.presentationml.presentation")
    {
        FileDownloadName = "Charts.pptx"
    };
    return result;
}
```

## Kompletní, spustitelný příklad

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1. Load the workbook containing charts
            string excelPath = @"C:\Projects\ChartAndShapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2. (Optional) Ensure formulas are up‑to‑date
            workbook.CalculateFormula();

            // 3. Export to PowerPoint while preserving shape editability
            string pptxPath = @"C:\Projects\Shapes.pptx";
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export complete. PowerPoint saved to: {pptxPath}");
        }
    }
}
```

**Očekávaný výstup:** Konzole vypíše potvrzovací zprávu a `Shapes.pptx` se otevře v PowerPointu, přičemž každý Excel graf se zobrazí na samostatném snímku. Výběrem grafu můžete upravit jeho data, což potvrzuje, že **editovatelnost tvarů** je zachována.

## Shrnutí a další kroky

Nyní víte, jak **exportovat grafy z Excelu do PowerPointu** pomocí C# a přitom zachovat grafy plně editovatelné. Jádrem řešení je metoda `Workbook.Save` s `SaveFormat.Pptx`, funkce **Aspose.Cells export**, která abstrahuje složité zpracování Open XML.

Odtud můžete dále zkoumat:

* Přidání vlastních názvů snímků nebo poznámek pomocí API **Aspose.Slides**.  
* Konverze dalších objektů Excelu (tabulky, obrázky) spolu s grafy.  
* Automatizace hromadného zpracování více sešitů v background službě.

Neváhejte experimentovat s volitelnými nastaveními uvedenými výše a začlenit tento vzor do vašich reportingových pipeline pro rychlé a spolehlivé generování PowerPointu.

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Export grafu z Excelu do PowerPointu s C# – kompletní průvodce Aspose.Cells](/cells/english/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/)
- [Jak exportovat Excel do PowerPointu s C# – kompletní průvodce](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)
- [Jak exportovat tvary z Excelu do PowerPointu – kompletní průvodce](/cells/english/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}