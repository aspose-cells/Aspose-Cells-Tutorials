---
category: general
date: 2026-09-15
description: Naučte se, jak vložit písma do SVG a exportovat graf z Excelu do PowerPointu,
  včetně převodu XLSX na SVG a převodu XLSX na PPTX s kompletními ukázkami kódu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in SVG
- export excel chart to powerpoint
- convert xlsx to svg
- convert xlsx to pptx
- save workbook as svg
language: cs
lastmod: 2026-09-15
og_description: Vložte písma do SVG a exportujte graf z Excelu do PowerPointu pomocí
  krok‑za‑krokem C# kódu. Převádějte XLSX na SVG a XLSX na PPTX rychle a spolehlivě.
og_image_alt: Screenshot showing an Excel chart exported to PowerPoint with embedded
  fonts in the resulting SVG file
og_title: Vložení fontů do SVG a export grafu z Excelu do PowerPointu – kompletní
  průvodce
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  headline: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  type: TechArticle
- description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  name: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  steps:
  - name: Open `EditableChart.pptx` in PowerPoint.
    text: Open `EditableChart.pptx` in PowerPoint.
  - name: Locate the slide containing the chart.
    text: Locate the slide containing the chart.
  - name: Choose **Chart Tools → Design → Edit Data**.
    text: Choose **Chart Tools → Design → Edit Data**.
  - name: Confirm that the Excel‑style data grid appears and that you can change values.
    text: Confirm that the Excel‑style data grid appears and that you can change values.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak vložit písma do SVG při převodu souborů Excel do SVG a PowerPointu
url: /cs/net/converting-excel-files-to-other-formats/how-to-embed-fonts-in-svg-when-converting-excel-files-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vložit písma do SVG při převodu souborů Excel do SVG a PowerPoint

Pokud potřebujete **vložit písma do SVG** při převodu sešitu Excel, tento průvodce vám přesně ukáže, jak na to. Také se naučíte, jak **exportovat graf z Excelu do PowerPointu**, a jak **převést XLSX na SVG** a **převést XLSX na PPTX** s editovatelnými grafy.

Práce s daty Excel programově často znamená, že musíte stejný vizuální obsah přesouvat mezi různými formáty souborů. Ruční přetvoření grafu v PowerPointu nebo opětovné aplikování písem v SVG je náchylné k chybám a časově náročné. Na konci tohoto tutoriálu budete mít jeden, znovupoužitelný úryvek C#, který:

* Uloží sešit jako SVG soubor s vloženými písmy a selektory variací písma.  
* Exportuje stejný sešit do souboru PPTX, kde graf zůstane editovatelný.  

Jedinou podmínkou je aktuální verze **Aspose.Cells for .NET** (2024‑x nebo novější) a vývojové prostředí .NET, například Visual Studio 2022.

---

## Co budete potřebovat  

* .NET 6.0 nebo novější (kód také funguje na .NET Framework 4.8).  
* NuGet balíček Aspose.Cells for .NET (`Install-Package Aspose.Cells`).  
* Soubor Excel (`input.xlsx`) obsahující alespoň jeden graf.  
* Oprávnění k zápisu do výstupního adresáře.  

---

## Vložení písem do SVG při převodu XLSX na SVG  

Vložení písem zajišťuje, že SVG se vykreslí správně na jakémkoli zařízení, i když cílový systém postrádá původní typy písma. Třída `SvgSaveOptions` poskytuje dva příznaky, které to umožňují: `EmbedFonts` a `FontVariationSelectors`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// OPTIONAL: Use WRAPCOLS to reshape data before export (demonstrates a formula)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)"; // 2 columns per wrap
sheet.Calculate(); // Force calculation so the formula result appears

// Configure SVG options to embed fonts
SvgSaveOptions svgOptions = new SvgSaveOptions
{
    EmbedFonts = true,                // embed fonts in the SVG
    FontVariationSelectors = true    // include variation selectors for better Unicode handling
};

// Save the workbook as an SVG file
string svgPath = @"YOUR_DIRECTORY\WithFonts.svg";
workbook.Save(svgPath, svgOptions);
```

**Proč to funguje:**  
* `EmbedFonts = true` zkopíruje soubory písem do sekce `<defs>` SVG, čímž eliminuje externí závislosti.  
* `FontVariationSelectors = true` přidá potřebné selektory pro písma podporující funkce OpenType, zachovávající varianty glyfů jako ligatury.  

**Očekávaný výsledek:** Otevřete `WithFonts.svg` v libovolném moderním prohlížeči; text v grafu nebo buňkách se zobrazí se stejným typem písma, jaký byl použit v Excelu, i na počítačích, kde toto písmo není nainstalováno.

---

## Export grafu z Excelu do PowerPointu s editovatelnými grafy  

Když potřebujete vložit graf do snímku PowerPointu, ale zároveň umožnit příjemci upravit data grafu, `PptxSaveOptions` od Aspose.Cells nabízí příznak `ExportEditableChart`.

```csharp
// Configure PPTX options to keep charts editable after export
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableChart = true   // allow chart editing in PowerPoint
};

// Save the same workbook as a PPTX file
string pptxPath = @"YOUR_DIRECTORY\EditableChart.pptx";
workbook.Save(pptxPath, pptxOptions);
```

**Proč je to důležité:**  
Nastavení `ExportEditableChart` na `true` uloží graf jako objekt Office Open XML grafu místo statického obrázku. Když otevřete `EditableChart.pptx` v PowerPointu, můžete pravým tlačítkem kliknout na graf → **Edit Data** a upravit řady stejně jako nativní graf v PowerPointu.

**Kroky ověření:**  

1. Otevřete `EditableChart.pptx` v PowerPointu.  
2. Najděte snímek obsahující graf.  
3. Vyberte **Chart Tools → Design → Edit Data**.  
4. Potvrďte, že se zobrazí datová mřížka ve stylu Excelu a že můžete měnit hodnoty.

---

## Převod XLSX na SVG – kompletní přehled pracovního postupu  

Níže je kompaktní verze, která kombinuje načítání, volitelné manipulace s daty a ukládání jako SVG. Použijte ji, když potřebujete jen výstup SVG.

```csharp
public void ConvertXlsxToSvg(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Example: apply a formula to demonstrate cell calculations
    Worksheet ws = wb.Worksheets[0];
    ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
    ws.Calculate();

    SvgSaveOptions opts = new SvgSaveOptions
    {
        EmbedFonts = true,
        FontVariationSelectors = true
    };

    wb.Save(outputPath, opts);
}
```

Zavolejte metodu takto:

```csharp
ConvertXlsxToSvg(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.svg");
```

**Tip pro okrajové případy:** Pokud váš sešit obsahuje vlastní písma, která nejsou nainstalována na serveru, vložte je ručně před voláním `Save`. Použijte `FontInfoCollection` k přidání souborů písem do `SvgSaveOptions` pomocí vlastnosti `CustomFonts` (k dispozici v novějších verzích Aspose.Cells).

---

## Převod XLSX na PPTX – zachování editovatelnosti grafu  

Následující pomocná metoda demonstruje cestu **convert XLSX to PPTX**, přičemž zajišťuje, že graf zůstane editovatelný.

```csharp
public void ConvertXlsxToPptx(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Ensure any chart you want to keep editable is on the first worksheet
    // (Aspose.Cells exports only the first worksheet by default for PPTX)
    PptxSaveOptions opts = new PptxSaveOptions
    {
        ExportEditableChart = true
    };

    wb.Save(outputPath, opts);
}
```

Použití:

```csharp
ConvertXlsxToPptx(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.pptx");
```

**Často kladená otázka:** *Co když má můj sešit více listů s grafy?*  
**Odpověď:** Aspose.Cells exportuje ve výchozím nastavení první list. Pro zahrnutí dalších listů iterujte přes `workbook.Worksheets`, zkopírujte každý graf na nový snímek a uložte každý snímek samostatně pomocí objektů `Presentation` z Aspose.Slides. Tento pokročilý scénář přesahuje základní tok „uložit sešit jako SVG“ a „exportovat graf z Excelu do PowerPointu“, ale základní příznaky zůstávají stejné.

---

## Praktické tipy a úskalí  

* **Výkon:** Vkládání písem zvyšuje velikost souboru SVG. Pokud je velikost problém, nastavte `EmbedFonts = false` a spoléhejte se na web‑safe písma.  
* **Licencování písem:** Ujistěte se, že máte právo vložit písma, která používáte; některá komerční písma omezuje vkládání.  
* **Kompatibilita grafů:** Editovatelné grafy jsou uloženy jako části `chart.xml` uvnitř PPTX. Velmi složité grafy (např. 3‑D nebo kombinované grafy) mohou při úpravě v PowerPointu ztratit část stylování. Otestujte nejčastěji potřebné typy grafů.  
* **Neshody verzí:** Příznak `ExportEditableChart` vyžaduje Aspose.Cells 20.10 nebo novější. Použití starší verze tiše přejde na rastrový obrázek.  
* **Bezpečnost vláken:** Objekt Workbook není bezpečný pro více vláken. Vytvořte novou instanci `Workbook` pro každý požadavek ve scénáři webové služby.  

---

## Kompletní příklad od začátku do konce  

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class ExcelExportDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputFile = @"YOUR_DIRECTORY\input.xlsx";
        string svgFile   = @"YOUR_DIRECTORY\WithFonts.svg";
        string pptxFile  = @"YOUR_DIRECTORY\EditableChart.pptx";

        // 1. Load workbook
        Workbook workbook = new Workbook(inputFile);

        // 2. Optional: reshape data using WRAPCOLS
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
        sheet.Calculate();

        // 3. Save as SVG with embedded fonts
        SvgSaveOptions svgOpts = new SvgSaveOptions
        {
            EmbedFonts = true,
            FontVariationSelectors = true
        };
        workbook.Save(svgFile, svgOpts);
        Console.WriteLine($"SVG saved with embedded fonts to: {svgFile}");

        // 4. Save as PPTX with editable chart
        PptxSaveOptions pptxOpts = new PptxSaveOptions
        {
            ExportEditableChart = true
        };
        workbook.Save(pptxFile, pptxOpts);
        Console.WriteLine($"PPTX saved with editable chart to: {pptxFile}");
    }
}
```

Spuštěním tohoto programu vzniknou dva soubory:

* **WithFonts.svg** – SVG, který se vykreslí přesně jako pohled v Excelu, včetně písem.  
* **EditableChart.pptx** – prezentace PowerPoint, kde lze graf upravovat přímo.

---

## Závěr  

Nyní víte, jak **vložit písma do SVG** při **převodu XLSX na SVG**, a jak **exportovat graf z Excelu do PowerPointu**, přičemž graf zůstane editovatelný. Stejný kód také ukazuje čistý způsob, jak **uložit sešit jako SVG** a **převést XLSX na PPTX** s minimálním úsilím.

Odtud můžete dále zkoumat témata jako:

* Přidání vlastních písem programově (`svgOptions.CustomFonts`).  
* Hromadné zpracování více sešitů ve službě na pozadí.  
* Použití Aspose.Slides k vytvoření více‑snímkových PPTX souborů, které kombinují několik grafů z Excelu.  

Experimentujte s možnostmi, přizpůsobte úryvky svému projektu a užívejte si spolehlivé převody Excel‑na‑SVG/PPTX bez ručního post‑zpracování. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/german/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/french/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}