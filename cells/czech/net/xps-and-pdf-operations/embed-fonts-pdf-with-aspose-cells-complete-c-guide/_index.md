---
category: general
date: 2026-06-24
description: Vložte písma do PDF pomocí Aspose.Cells v C#. Naučte se, jak uložit Excel
  jako PDF, exportovat Excel do HTML, převést xlsx na PDF pomocí Aspose a duplikovat
  řádky v kontingenční tabulce.
draft: false
keywords:
- embed fonts pdf
- save excel as pdf
- export excel to html
- xlsx to pdf aspose
- duplicate rows pivot
language: cs
og_description: Vkládání fontů do PDF pomocí Aspose.Cells v C#. Tento tutoriál ukazuje
  krok za krokem, jak uložit Excel jako PDF, exportovat Excel do HTML a další.
og_title: Vložení fontů do PDF pomocí Aspose.Cells – Kompletní průvodce C#
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Embed fonts PDF using Aspose.Cells in C#. Learn how to save Excel as
    PDF, export Excel to HTML, convert xlsx to PDF with Aspose, and duplicate rows
    pivot.
  headline: Embed fonts PDF with Aspose.Cells – Complete C# Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
title: Vložení fontů do PDF pomocí Aspose.Cells – Kompletní C# průvodce
url: /cs/net/xps-and-pdf-operations/embed-fonts-pdf-with-aspose-cells-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vložení fontů do PDF pomocí Aspose.Cells – Kompletní průvodce v C#  

Už jste se někdy zamysleli, jak **embed fonts PDF** při převodu sešitu Excel pomocí Aspose.Cells? Nejste sami — mnoho vývojářů narazí na problém, když vygenerované PDF vypadá špatně na počítačích, které nemají nainstalovány původní fonty.  

V tomto průvodci projdeme reálným příkladem, který nejen **embed fonts PDF**, ale také vám ukáže, jak **save Excel as PDF**, **export Excel to HTML**, převést **xlsx to PDF with Aspose**, a dokonce **duplicate rows pivot** bez poškození kontingenční tabulky. Zní to jako hodně? Žádný problém — rozložíme to krok po kroku.

## Co se naučíte

- Jak zkopírovat řádky, které obsahují kontingenční tabulku, a přitom zachovat kontingenční tabulku neporušenou.  
- Jak vložit smart‑marker, který opakuje detailní list pro každou objednávku.  
- Přesná nastavení, která potřebujete pro **embed fonts PDF**, export grafů jako editovatelný PPTX a zachování zmrazených panelů při **export Excel to HTML**.  
- Tipy pro řešení běžných problémů, jako jsou chybějící fonty nebo poškozené OLE objekty.  

**Požadavky:** .NET 6+ (nebo .NET Framework 4.6+), nainstalovaný Aspose.Cells pro .NET a základní vývojové prostředí C# (Visual Studio, Rider nebo VS Code). Žádné další NuGet balíčky kromě Aspose.Cells nejsou potřeba.

---

## Vložení fontů do PDF – krok za krokem

Níže je kompletní spustitelný kód. Každá sekce je okomentována, aby bylo jasné, proč děláme to, co děláme.

```csharp
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Pivot;
using Aspose.Cells.SmartMarker;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the workbook that contains a pivot table and a shape
        // -------------------------------------------------
        var workbook = new Workbook("YOUR_DIRECTORY/template.xlsx");

        // -------------------------------------------------
        // Step 2: Duplicate the rows that include the pivot table (keeps the pivot intact)
        // -------------------------------------------------
        // The CopyRows method copies rows 0‑29 (30 rows) from the source worksheet
        // to the same worksheet, effectively duplicating the pivot area.
        workbook.Worksheets[0].Cells.CopyRows(0, 0, 30);

        // -------------------------------------------------
        // Step 3: Insert a smart‑marker to repeat a detail sheet for each order
        // -------------------------------------------------
        var orders = new[]
        {
            new { Id = 101, Items = new[] { "Pen", "Paper" } },
            new { Id = 102, Items = new[] { "Book" } }
        };
        var smartMarkerOptions = new SmartMarkerOptions { DetailSheetNewName = "OrderDetail" };
        workbook.Worksheets[0].SmartMarkerProcessing(new { Orders = orders }, smartMarkerOptions);

        // -------------------------------------------------
        // Step 4: Save the workbook as a PPTX file with editable charts, OLE objects, and text boxes
        // -------------------------------------------------
        var pptxOptions = new PptxSaveOptions
        {
            ExportChartsAsEditable = true,
            ExportOleObjects = true,
            ExportTextBoxesAsEditable = true
        };
        workbook.Save("YOUR_DIRECTORY/result.pptx", pptxOptions);

        // -------------------------------------------------
        // Step 5: Save the same workbook as a PDF while embedding standard fonts
        // -------------------------------------------------
        // This is where we actually **embed fonts PDF**.
        var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
        workbook.Save("YOUR_DIRECTORY/result.pdf", pdfOptions);

        // -------------------------------------------------
        // Step 6: Save the workbook as HTML, preserving frozen panes and embedding all fonts
        // -------------------------------------------------
        // The HTML export respects the original layout and keeps the fonts inside the file.
        var htmlOptions = new HtmlSaveOptions
        {
            PreserveFreezePanes = true,
            EmbedAllFonts = true
        };
        workbook.Save("YOUR_DIRECTORY/result.html", htmlOptions);
    }
}
```

### Proč to funguje

- **CopyRows** duplikuje řádky, které obsahují kontingenční tabulku, takže původní kontingenční tabulka zůstane propojena se svými zdrojovými daty. To splňuje požadavek **duplicate rows pivot**.  
- **SmartMarkerProcessing** vytvoří nový list pro každou objednávku, automatizuje generování detailního listu.  
- **PdfSaveOptions.EmbedStandardFonts = true** říká Aspose.Cells, aby vložil fonty přímo do PDF souboru, což je klíč k **embed fonts pdf**. Bez tohoto nastavení by PDF použilo systémové fonty, což by rozbilo rozvržení na jiných počítačích.  
- **HtmlSaveOptions** s `EmbedAllFonts` a `PreserveFreezePanes` zajišťuje, že při **export Excel to HTML** vizuální věrnost odpovídá originálnímu sešitu.  

#### Očekávaný výstup

- `result.pdf` – PDF, ve kterém jsou vloženy všechny použité fonty; otevřete jej na jakémkoli počítači a text bude vypadat identicky jako ve zdroji.  
- `result.pptx` – soubor PowerPoint s editovatelnými grafy a OLE objekty.  
- `result.html` – HTML složka (`result.html` + `result_files`), která zobrazuje sešit v prohlížeči se zachovanými zmrazenými panely.  

---

## Uložení Excelu jako PDF pomocí Aspose.Cells

Pokud je vaším jediným cílem **save Excel as PDF**, můžete vynechat další kroky a soustředit se na nastavení PDF:

```csharp
var workbook = new Workbook("template.xlsx");

// Minimal PDF conversion – embed fonts for portability
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,   // crucial for embed fonts pdf
    Compliance = PdfCompliance.PdfA1b // optional: make the PDF archival‑friendly
};

workbook.Save("output.pdf", pdfOpts);
```

**Tip:** Když cílíte na shodu s PDF/A, Aspose automaticky vloží všechny fonty, takže získáte další úroveň bezpečnosti pro dlouhodobé ukládání.

---

## Export Excelu do HTML při zachování rozvržení

Export do HTML často ztrácí vzhled původního listu, zejména když jsou použity zmrazené panely. Následující úryvek ukazuje přesná nastavení, která potřebujete:

```csharp
var wb = new Workbook("template.xlsx");

var htmlOpts = new HtmlSaveOptions
{
    PreserveFreezePanes = true, // keeps the top rows/columns locked
    EmbedAllFonts = true,       // embeds fonts so the page looks the same everywhere
    ExportActiveWorksheetOnly = true,
    ExportCellValueAsString = true
};

wb.Save("output.html", htmlOpts);
```

Protože jsme nastavili `EmbedAllFonts`, generované HTML obsahuje data fontů zakódovaná v base‑64, což splňuje požadavek **export excel to html** bez jakýchkoli externích CSS souborů.

---

## Převod Xlsx na PDF pomocí Aspose.Cells

Někdy se ve vyhledávání objevuje termín “**xlsx to pdf aspose**”. Níže uvedený kód demonstruje přesný převodní proces, včetně několika dalších vylepšení:

```csharp
var wb = new Workbook("template.xlsx");

// Optional: set page layout before conversion
wb.Worksheets[0].PageSetup.Orientation = PageOrientation.Landscape;
wb.Worksheets[0].PageSetup.FitToPagesWide = 1;
wb.Worksheets[0].PageSetup.FitToPagesTall = 0;

// PDF options – embed fonts and keep hyperlinks intact
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    ExportHyperlinks = true,
    OnePagePerSheet = false
};

wb.Save("converted.pdf", pdfOpts);
```

**Proč se zabývat nastavením stránky?** Pokud to přeskočíte, výchozí PDF může oříznout sloupce nebo řádky. Úprava rozvržení nejprve zajistí, že finální PDF bude odpovídat tomu, co vidíte v Excelu.

---

## Duplikování řádků v kontingenční tabulce – zachování kontingenční tabulky

Častým problémem je pokus o kopírování řádků, které obsahují kontingenční tabulku; kontingenční tabulka často ztratí spojení se zdrojem dat. Metoda `CopyRows`, kterou jsme použili dříve, to za vás udělá:

```csharp
// Duplicate the first 30 rows (adjust as needed)
workbook.Worksheets[0].Cells.CopyRows(sourceRow: 0, destinationRow: 0, totalRows: 30);
```

- **sourceRow** – první řádek rozsahu, který chcete zkopírovat.  
- **destinationRow** – kam má být kopie umístěna (stejný list, stejný počáteční index pro efektivní duplikaci).  
- **totalRows** – kolik řádků má být zkopírováno.  

Protože mezipaměť kontingenční tabulky žije v listu, kopírování řádků **nepoškodí** kontingenční tabulku. To splňuje klíčové slovo **duplicate rows pivot** a zároveň udržuje sešit přehledný.

---

## Kompletní funkční příklad – shrnutí

Spojením všeho dohromady je zde kompletní program, který můžete vložit do konzolové aplikace a spustit okamžitě:



## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vlastních projektech.

- [Uložit sešit Excel jako PDF s vlastními fonty pomocí Aspose.Cells pro .NET](/cells/english/net/workbook-operations/save-excel-workbook-pdf-custom-fonts-aspose-cells-net/)
- [Jak exportovat grafy z Excelu do PDF pomocí Aspose.Cells pro .NET: krok za krokem](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Jak exportovat řezače (slicers) z Excelu do PDF pomocí Aspose.Cells pro .NET](/cells/english/net/workbook-operations/export-excel-slicers-to-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}