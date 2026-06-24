---
category: general
date: 2026-06-24
description: Naučte se, jak vložit písma při exportu Excelu do HTML pomocí C#. Tento
  krok‑za‑krokem návod také pokrývá převod xlsx do HTML a vytvoření HTML z Excelu.
draft: false
keywords:
- how to embed fonts
- export excel to html
- embed fonts in html
- convert xlsx to html
- create html from excel
language: cs
og_description: Jak vložit písma do HTML při převodu sešitu XLSX pomocí C#. Postupujte
  podle tohoto návodu pro export Excelu do HTML s vloženými písmy.
og_title: Jak vložit fonty při exportu Excelu do HTML – C# tutoriál
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Learn how to embed fonts while exporting Excel to HTML using C#. This
    step‑by‑step tutorial also covers convert xlsx to HTML and create HTML from Excel.
  headline: How to embed fonts when exporting Excel to HTML – Complete C# Guide
  type: TechArticle
- description: Learn how to embed fonts while exporting Excel to HTML using C#. This
    step‑by‑step tutorial also covers convert xlsx to HTML and create HTML from Excel.
  name: How to embed fonts when exporting Excel to HTML – Complete C# Guide
  steps:
  - name: Load the Workbook You Want to Export
    text: First, we need to bring the Excel file into memory. The `Workbook` class
      represents the entire workbook, including worksheets, styles, and embedded resources.
  - name: Create HTML Save Options and Enable Font Embedding
    text: Now we tell the library how to render the HTML. The `HtmlSaveOptions` class
      lets us toggle a bunch of features, but the key property for us is `EmbedAllFonts`.
  - name: Save the Workbook as an HTML File with Embedded Fonts
    text: Finally, we write the HTML file to disk. The `Save` method takes the target
      path and the options we just configured.
  - name: What’s Next?
    text: '- **Styling the output:** Add custom CSS after the generated `<style>`
      block to match your site’s theme. - **Batch processing:** Loop over a folder
      of Excel files and generate a zip of HTML reports. - **Alternative libraries:**
      If you don’t have a commercial license for Aspose.Cells, explore **Close'
  type: HowTo
tags:
- excel
- html
- fonts
- csharp
title: Jak vložit písma při exportu Excelu do HTML – Kompletní C# průvodce
url: /cs/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-exporting-excel-to-html-complete-c-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vložit písma při exportu Excelu do HTML – Kompletní průvodce v C#

Už jste se někdy zamýšleli **jak vložit písma** do HTML, které generujete z Excel sešitu? Možná budujete portál pro reportování a potřebujete, aby exportované tabulky vypadaly přesně jako v původní tabulce – až po vlastní typy písma. V tomto tutoriálu projdeme celý proces, od načtení souboru `.xlsx` až po uložení jako HTML stránky se všemi písmy zabudovanými přímo v ní. Žádné externí CSS triky, žádné chybějící glyfy.

Také se dotkneme souvisejících úkolů jako **export excel to html**, **embed fonts in html**, **convert xlsx to html** a **create html from excel** — abyste měli jednorázovou referenci pro všechny běžné scénáře, na které můžete narazit.

## Co budete potřebovat

- **.NET 6.0** nebo novější (příklad funguje i na .NET Framework, ale .NET 6+ je ideální).
- **Aspose.Cells for .NET** (nebo jakákoli podobná knihovna, která podporuje `HtmlSaveOptions`). Bezplatná zkušební verze funguje pro testování.
- Jednoduchý Excel soubor (`input.xlsx`), který používá vlastní písmo, které chcete zachovat.
- Vaše oblíbené IDE (Visual Studio, Rider nebo VS Code).

To je vše—nic exotického, jen pár NuGet balíčků a tabulka.

![Snímek obrazovky ukazující, jak vložit písma do HTML generovaného z Excelu pomocí C#](how-to-embed-fonts-in-html-from-excel.png)

*Text obrázku: jak vložit písma do HTML z Excelu pomocí Aspose.Cells*

## Implementace krok za krokem

Níže rozdělíme řešení do tří jasných kroků. Každý krok obsahuje **co**, **proč** a **jak**, plus celý kód, který můžete zkopírovat a vložit do konzolové aplikace.

### Krok 1: Načtěte sešit, který chcete exportovat

Nejprve musíme načíst Excel soubor do paměti. Třída `Workbook` představuje celý sešit, včetně listů, stylů a vložených zdrojů.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook you want to export
var workbook = new Workbook(@"C:\Projects\ExcelExport\input.xlsx");

// Why this matters:
// - The Workbook object parses all cell data, formulas, and style definitions.
// - If the source file uses a custom font, Aspose.Cells keeps a reference to that font.
// - Loading the file early ensures the later HTML conversion has everything it needs.
```

> **Tip:** Pokud pracujete s velkými soubory, zvažte použití `LoadOptions` pro streamování sešitu a snížení zatížení paměti.

### Krok 2: Vytvořte HTML Save Options a povolte vkládání písem

Nyní řekneme knihovně, jak má HTML vykreslovat. Třída `HtmlSaveOptions` nám umožňuje přepínat řadu funkcí, ale klíčová vlastnost pro nás je `EmbedAllFonts`.

```csharp
// Step 2: Create HTML save options and enable font embedding
var htmlOptions = new HtmlSaveOptions
{
    // When true, all fonts used in the workbook are embedded as Base64‑encoded @font‑face rules.
    EmbedAllFonts = true,

    // Optional niceties:
    ExportActiveWorksheetOnly = false, // Export the whole workbook, not just the active sheet.
    ExportImagesAsBase64 = true         // Keeps the HTML self‑contained (no external image files).
};

// Why this matters:
// - `EmbedAllFonts = true` converts each font into a data URI and injects it into a <style> block.
// - This guarantees that the HTML will look identical on any browser, even if the user doesn’t have the font installed.
// - Embedding images as Base64 further isolates the output, making it perfect for email bodies or offline reports.
```

### Krok 3: Uložte sešit jako HTML soubor s vloženými písmy

Nakonec zapíšeme HTML soubor na disk. Metoda `Save` přijímá cílovou cestu a možnosti, které jsme právě nastavili.

```csharp
// Step 3: Save the workbook as an HTML file with embedded fonts
string outputPath = @"C:\Projects\ExcelExport\embedded.html";
workbook.Save(outputPath, htmlOptions);

// Why this matters:
// - The generated `embedded.html` contains a <style> block with @font-face rules for every custom font.
// - No external `.ttf` or `.woff` files are required; everything lives inside the HTML file.
// - This is the most portable way to share Excel‑styled content on the web.
```

#### Očekávaný výstup

Otevřete `embedded.html` v libovolném moderním prohlížeči (Chrome, Edge, Firefox, Safari). Měli byste vidět:

- Veškerý text buněk vykreslený přesně stejným písmem, jaké bylo použito v původním Excel souboru.
- Žádné chybějící znaky ani náhradní písma.
- Čistý, samostatný HTML dokument (klikněte pravým → Zobrazit zdroj stránky a prohlédněte vložený blok `<style>`).

## Ověření, že jsou písma skutečně vložena

Někdy můžete mít podezření, že písma nebyla skutečně vložena — zejména pokud používáte firemní písmo s licenčními omezeními. Zde je rychlá kontrola:

1. Otevřete HTML soubor v Chrome.
2. Stiskněte `Ctrl+U` (nebo klikněte pravým → Zobrazit zdroj stránky).
3. Vyhledejte `@font-face`. Měli byste vidět záznam `src: url(data:font/ttf;base64,...)` pro každé vlastní písmo.

Pokud atribut `src` ukazuje na místní cestu k souboru místo datového URI, příznak `EmbedAllFonts` neúčinkoval — možná protože písmo není nainstalováno na stroji, který provádí konverzi. Ujistěte se, že soubor s písmem je přístupný procesu.

## Časté problémy a okrajové případy

| Problém | Proč se to děje | Oprava |
|-------|----------------|-----|
| **Chybějící vlastní písmo** | Písmo není nainstalováno na serveru pro konverzi. | Nainstalujte písmo na stroj nebo zkopírujte soubory `.ttf/.otf` do známé složky a nastavte `FontEmbeddingMode = FontEmbeddingMode.EmbedAll` (pokud knihovna podporuje). |
| **Obrovská velikost HTML souboru** | Vkládání mnoha velkých písem zvětšuje soubor (každé písmo může být >200 KB). | Vkládejte pouze písma, která skutečně používáte: nastavte `htmlOptions.FontEmbeddingMode = FontEmbeddingMode.EmbedSubset` (pokud je k dispozici), aby se vložily jen potřebné glyfy. |
| **Nesprávné vykreslení znaků** | Zdrojový Excel používá složité skripty (např. arabštinu) a knihovna ve výchozím nastavení používá ne‑RTL rozložení. | Povolte `htmlOptions.EnableRtl = true` a ujistěte se, že je na sešitu nastavena správná lokalizace. |
| **Externí obrázky se stále zobrazují** | `ExportImagesAsBase64` zůstalo ve výchozím nastavení (`false`). | Nastavte `ExportImagesAsBase64 = true` jak je uvedeno výše, nebo ručně nahraďte URL obrázků po exportu. |

## Pokročilejší: Automatizace procesu ve Web API

Pokud potřebujete tuto funkci zpřístupnit koncovým uživatelům, zabalte kód do ASP.NET Core kontroleru:

```csharp
[ApiController]
[Route("api/[controller]")]
public class ExcelExportController : ControllerBase
{
    [HttpPost("to-html")]
    public IActionResult ConvertToHtml(IFormFile file)
    {
        if (file == null || file.Length == 0)
            return BadRequest("No file uploaded.");

        using var stream = file.OpenReadStream();
        var workbook = new Workbook(stream);
        var options = new HtmlSaveOptions
        {
            EmbedAllFonts = true,
            ExportImagesAsBase64 = true
        };

        using var ms = new MemoryStream();
        workbook.Save(ms, options);
        ms.Position = 0;
        return File(ms, "text/html", $"{Path.GetFileNameWithoutExtension(file.FileName)}.html");
    }
}
```

- **Proč to pomáhá:** Uživatelé nahrávají soubor `.xlsx` a API vrací připravený HTML dokument se všemi vloženými písmy — žádné dočasné soubory na disku.
- **Bezpečnostní poznámka:** Ověřte velikost a typ souboru; zvažte sandboxování konverze, pokud přijímáte nahrávky od nedůvěryhodných uživatelů.

## Shrnutí

Probrali jsme **jak vložit písma** při **exportu Excelu do HTML** pomocí C#. Klíčové kroky jsou:

1. Načtěte sešit (`Workbook`).
2. Nastavte `HtmlSaveOptions` s `EmbedAllFonts = true`.
3. Uložte do `.html` a ověřte vložený blok `<style>`.

Nyní také víte, jak **convert xlsx to html**, **create html from excel**, a jak řešit nejčastější okrajové případy. Klidně experimentujte s dalšími možnostmi — jako `ExportHiddenSheets` nebo `CssClassPrefix` — pro doladění výstupu podle vašeho konkrétního projektu.

### Co dál?

- **Styling the output:** Přidejte vlastní CSS po vygenerovaném bloku `<style>`, aby odpovídalo motivu vašeho webu.
- **Batch processing:** Procházejte složku s Excel soubory a generujte zip s HTML reporty.
- **Alternative libraries:** Pokud nemáte komerční licenci pro Aspose.Cells, prozkoumejte kombinaci **ClosedXML** + **HtmlAgilityPack** (i když vkládání písem bude vyžadovat ruční zpracování).

Máte otázky ohledně konkrétní funkce Excelu nebo jiného scénáře nasazení? Zanechte komentář níže a rád vám pomohu. Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným vysvětlením, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak exportovat Excel do HTML s mřížkovými čarami pomocí Aspose.Cells pro .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)
- [Jak exportovat podobné styly ohraničení z Excelu do HTML pomocí Aspose.Cells pro .NET](/cells/english/net/workbook-operations/export-similar-border-styles-excel-html-aspose-cells/)
- [Převod Excelu do HTML s tooltipy pomocí Aspose.Cells pro .NET: Průvodce krok za krokem](/cells/english/net/workbook-operations/convert-excel-html-tooltips-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}