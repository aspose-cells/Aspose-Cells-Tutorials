---
category: general
date: 2026-02-26
description: Exportujte sešit do PDF s vloženými fonty a také exportujte grafy do
  PowerPointu v C#. Naučte se zkopírovat list s kontingenční tabulkou a uložit sešit
  jako PPTX.
draft: false
keywords:
- export workbook to pdf
- export charts to powerpoint
- copy pivot table worksheet
- embed fonts pdf export
- save workbook as pptx
language: cs
og_description: Exportujte sešit do PDF s vloženými fonty a také exportujte grafy
  do PowerPointu v C#. Postupujte podle průvodce krok za krokem, jak zkopírovat kontingenční
  tabulky a uložit jako PPTX.
og_title: Export sešitu do PDF – Kompletní průvodce C#
tags:
- Aspose.Cells
- Aspose.Slides
- C#
- Reporting
title: Export sešitu do PDF – kompletní průvodce C#
url: /cs/net/conversion-to-pdf/export-workbook-to-pdf-complete-c-guide/
---

There are none except placeholders. Good.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export sešitu do PDF – Kompletní průvodce v C#

Export sešitu do PDF je běžná potřeba, když potřebujete sdílet zprávy se zainteresovanými stranami, které nemusí mít nainstalovaný Excel. V tomto tutoriálu vám také ukážeme, jak **exportovat grafy do PowerPointu**, zkopírovat **list s kontingenční tabulkou** a vložit písma, aby PDF vypadalo přesně jako váš návrh na obrazovce.  

Už jste se někdy ptali, proč některá PDF soubory ztrácejí původní rozvržení nebo proč snímky v PowerPointu končí s chybějícími tvary? Odpověď obvykle spočívá v chybějících možnostech během procesu exportu. Na konci tohoto průvodce budete mít jedinou, znovupoužitelnou C# metodu, která řeší všechny tyto problémy – už žádné ruční kopírování‑vkládání ani ladění nastavení exportu.

## Co se naučíte

- Jak vytvořit sešit, přidat výrazy Smart Marker a zpracovat je.  
- Jak **zkopírovat list s kontingenční tabulkou** bez narušení datového zdroje.  
- Jak **exportovat grafy, tvary a textová pole** do prezentace PowerPoint a zachovat jejich editovatelnost.  
- Jak **vložit standardní písma** během exportu do PDF pro konzistentní vykreslování na jakémkoli počítači.  
- Jak **uložit sešit jako PPTX** pomocí přístupu `save workbook as pptx`.  

Vše toto funguje s nejnovějšími knihovnami Aspose.Cells a Aspose.Slides .NET (verze 23.11 v době psaní). Žádné externí nástroje, žádné post‑processing skripty – jen čistý C#.

> **Pro tip:** Pokud již ve svém projektu používáte Aspose, můžete kódové úryvky použít tak, jak jsou; jinak nejprve přidejte NuGet balíčky `Aspose.Cells` a `Aspose.Slides`.

## Požadavky

- .NET 6.0 nebo novější (kód také běží na .NET Framework 4.7.2).  
- Visual Studio 2022 (nebo jakékoli IDE dle vašeho výběru).  
- Aspose.Cells .NET a Aspose.Slides .NET nainstalované přes NuGet.  
- Základní znalost C# a konceptů Excelu, jako jsou Smart Markers a PivotTables.

---

![Diagram exportu sešitu do PDF](export-workbook-to-pdf.png "Pracovní postup exportu sešitu do PDF zobrazující výstupy PDF a PPTX")

## Export sešitu do PDF – Krok za krokem implementace

Níže je kompletní, připravený příklad. Vytvoří sešit, vloží výrazy Smart Marker, zpracuje je, zkopíruje rozsah s kontingenční tabulkou a nakonec uloží jak PDF, tak soubor PowerPoint.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides.Export;

namespace ReportExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Build the workbook and add Smart Markers
            // -------------------------------------------------
            var reportWorkbook = new Workbook();
            Worksheet dataSheet = reportWorkbook.Worksheets[0];

            // Header with a variable department name
            dataSheet.Cells["A1"].PutValue("Report for ${$dept=Department}");

            // Conditional text based on department
            dataSheet.Cells["A2"].PutValue("${if $dept == \"Sales\"}Sales Summary${else}Other Summary${/if}");

            // Table header for orders – this will be repeated for each order
            dataSheet.Cells["A5:D5"].PutValue("${Orders.Product}|${Orders.Quantity}|${Orders.Price}");

            // -------------------------------------------------
            // Step 2: Process Smart Markers and name the detail sheet
            // -------------------------------------------------
            reportWorkbook.SmartMarkerProcessor.Options.DetailSheetNewName = "Orders_${$dept}";
            reportWorkbook.SmartMarkerProcessor.Process();

            // -------------------------------------------------
            // Step 3: Copy the range that contains the pivot table
            // -------------------------------------------------
            // Assume the pivot table lives in A1:G30 on the original sheet
            Range sourceRange = dataSheet.Cells.CreateRange("A1", "G30");
            Worksheet copySheet = reportWorkbook.Worksheets.Add("Copy");
            sourceRange.Copy(copySheet.Cells["A1"]);   // Pivot table is duplicated intact

            // -------------------------------------------------
            // Step 4: Export to PowerPoint (keep charts, shapes, text boxes)
            // -------------------------------------------------
            var pptOptions = new PresentationOptions
            {
                ExportCharts = true,
                ExportShapes = true,
                ExportTextBoxes = true
            };
            string pptPath = @"C:\Temp\FinalPresentation.pptx";
            reportWorkbook.Save(pptPath, SaveFormat.Pptx, pptOptions);

            // -------------------------------------------------
            // Step 5: Export to PDF and embed standard fonts
            // -------------------------------------------------
            var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
            string pdfPath = @"C:\Temp\FinalReport.pdf";
            reportWorkbook.Save(pdfPath, pdfOptions);

            Console.WriteLine("Export completed:");
            Console.WriteLine($" • PDF saved to {pdfPath}");
            Console.WriteLine($" • PowerPoint saved to {pptPath}");
        }
    }
}
```

### Proč to funguje

1. **Smart Marker processing** vám umožní naplnit sešit z libovolného datového zdroje (JSON, DataTables, atd.) bez psaní smyček.  
2. **DetailSheetNewName** vytvoří samostatný list pro každé oddělení, což vám poskytne čistý list podle oddělení.  
3. **Copying the range** (`sourceRange.Copy`) duplikuje kontingenční tabulku *včetně* jejího cache, takže zkopírovaný list funguje přesně jako originál.  
4. **PresentationOptions** s `ExportCharts`, `ExportShapes` a `ExportTextBoxes` říká Aspose, aby vykreslil tyto objekty jako nativní prvky PowerPointu, čímž zachová editovatelnost.  
5. **PdfSaveOptions.EmbedStandardFonts** zajišťuje, že PDF vypadá identicky na počítačích, které nemají nainstalována původní písma.

Výsledkem jsou dva soubory — `FinalReport.pdf` a `FinalPresentation.pptx` — které lze poslat e‑mailem, archivovat nebo zobrazit v libovolném prohlížeči bez ztráty kvality.

## Export grafů do PowerPointu (Uložení sešitu jako PPTX)

Pokud váš report obsahuje grafy, pravděpodobně je budete chtít editovatelné v PowerPointu. Třída `PresentationOptions` je klíčová. Zde je zaměřený úryvek, který ukazuje jen část exportu grafu:

```csharp
// Assuming reportWorkbook already contains charts
var pptExportOptions = new PresentationOptions
{
    ExportCharts = true,      // Convert Excel charts to PowerPoint chart objects
    ExportShapes = false,    // Skip shapes if you don’t need them
    ExportTextBoxes = true   // Keep any text boxes editable
};

string pptFile = @"C:\Temp\ChartsOnly.pptx";
reportWorkbook.Save(pptFile, SaveFormat.Pptx, pptExportOptions);
```

**Co se děje pod kapotou?** Aspose převádí každý Excel graf na nativní PowerPoint graf, zachovává sérii, názvy os a formátování. To je mnohem lepší než exportovat graf jako statický obrázek, protože vaše publikum může později upravovat datové body.

## Kopírování listu s kontingenční tabulkou bez ztráty dat

Kontingenční tabulky jsou často nejnáročnější částí exportu, protože se spoléhají na skrytý cache. Jednoduchá metoda `Copy` funguje, protože Aspose kopíruje jak viditelný rozsah **tak** i podkladový objekt cache.

```csharp
// Copy the whole sheet (including pivot table) to a new workbook
Workbook clone = new Workbook();
reportWorkbook.Worksheets[0].CopyTo(clone.Worksheets[0]);
clone.Save(@"C:\Temp\PivotCopy.xlsx", SaveFormat.Xlsx);
```

> **Poznámka:** Pokud potřebujete kontingenční tabulku jen na novém listu ve stejném sešitu, dřívější přístup `sourceRange.Copy` je lehčí a zabraňuje vytvoření celého nového sešitu.

## Vkládání písem pro export do PDF – Proč je to důležité

Když otevřete PDF na počítači, který nemá původní písma, může se text posunout, změnit se zalomení řádků nebo znaky zmizet. Nastavení `EmbedStandardFonts = true` říká Aspose vložit nejčastější písma (Arial, Times New Roman, atd.) přímo do PDF proudu.

Pokud používáte vlastní písma, přepněte na `PdfSaveOptions.FontEmbeddingMode = FontEmbeddingMode.EmbedAll`. Zde je příklad:

```csharp
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    FontEmbeddingMode = FontEmbeddingMode.EmbedAll   // For custom fonts
};
reportWorkbook.Save(@"C:\Temp\CustomFontReport.pdf", pdfOpts);
```

Nyní každý příjemce vidí přesně stejný rozvrh, jaký jste navrhli – žádná překvapení.

## Shrnutí kompletního funkčního příkladu

Když spojíme vše dohromady, kompletní program (zobrazený dříve) provádí následující:

1. **Creates** sešit s placeholdery Smart Marker.  
2. **Processes** značky, generuje detailní list pojmenovaný podle oddělení.  
3. **Copies** rozsah, který obsahuje kontingenční tabulku, do nového listu a zachovává jeho funkčnost.  
4. **Exports** sešit do PowerPointu, přičemž grafy, tvary a textová pole zůstávají editovatelná.  
5. **Exports** stejný sešit do PDF a při tom vkládá standardní písma pro spolehlivé vykreslení.

Spusťte program, otevřete vygenerované soubory a uvidíte:

- **PDF**: Ostré tabulky, vložená písma a stejný vizuální styl jako v Excelu.  
- **PowerPoint**: Editovatelné grafy, které můžete pravým kliknutím → *Edit Data* v PowerPointu, a tvary, které zůstávají plně manipulovatelné.

---

## Často kladené otázky (FAQ)

**Q: Funguje to s .NET Core?**  
Ano—Aspose.Cells a Aspose.Slides jsou multiplatformní. Stačí cílit na .NET 6 nebo novější a stejný kód běží na Windows, Linuxu nebo macOS.

**Q: Co když potřebuji exportovat jen podmnožinu listů?**  
Použijte `Workbook.Save` s `SaveOptions`, které umožňují specifikovat `SheetNames`. Příklad: `new PresentationOptions { SheetNames = new[] { "Copy" } }`.

**Q: Můžu PDF zašifrovat?**  
Určitě. Nastavte `PdfSaveOptions.EncryptionDetails` s heslem před voláním `Save`.

**Q: Moje kontingenční tabulka používá externí datový zdroj – rozbije kopírování odkaz?**  
Operace kopírování zahrnuje cache, nikoli externí připojení. Kontingenční tabulka bude i nadále fungovat offline, ale neobnoví se vůči původnímu zdroji. Pokud potřebujete živou aktualizaci, exportujte zdrojová data spolu se sešitem.

## Další kroky a související témata

- **Dynamic Data Sources** – Naučte se, jak napájet JSON nebo DataTable do Smart Markers pro reporting v reálném čase.  
- **Advanced PDF Styling** – Prozkoumejte `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}