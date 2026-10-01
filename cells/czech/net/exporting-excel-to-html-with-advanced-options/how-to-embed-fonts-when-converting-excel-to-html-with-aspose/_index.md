---
category: general
date: 2026-10-01
description: Naučte se, jak vložit písma do HTML při převodu Excelu na HTML pomocí
  Aspose.Cells. Exportujte Excel jako HTML s vloženými písmy během několika kroků.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- convert excel to html
- embed fonts in html
- how to export excel
- export excel as html
language: cs
lastmod: 2026-10-01
og_description: Jak vložit písma do HTML při exportu souborů Excel. Postupujte podle
  tohoto krok‑za‑krokem průvodce a převádějte Excel do HTML s vloženými písmy.
og_image_alt: Screenshot of Aspose.Cells code embedding fonts in exported HTML
og_title: Jak vložit písma do HTML z Excelu – průvodce Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  headline: How to embed fonts when converting Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  name: How to embed fonts when converting Excel to HTML with Aspose.Cells
  steps:
  - name: 'Edge case: unsupported fonts'
    text: If the workbook uses a font that is not installed on the server, Aspose.Cells
      falls back to a default system font. To avoid this, install the required fonts
      on the server or embed them manually after export.
  - name: Converting multiple worksheets
    text: If you need to **convert Excel to HTML** for all worksheets, set `ExportActiveWorksheetOnly
      = false` (the default). Aspose.Cells will create a separate HTML file for each
      sheet.
  - name: Controlling CSS output
    text: 'You can reduce the HTML size by disabling inline CSS:'
  - name: Using a stream instead of a file
    text: 'When integrating into a web API, write the HTML to a `MemoryStream` and
      return it directly:'
  type: HowTo
tags:
- Aspose.Cells
- .NET
- Excel conversion
title: Jak vložit písma při převodu Excelu do HTML pomocí Aspose.Cells
url: /cs/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-converting-excel-to-html-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vložit písma při převodu Excelu do HTML pomocí Aspose.Cells

Vkládání písem do HTML při převodu sešitu Excel je nezbytné pro zachování původního vzhledu napříč prohlížeči. Pokud potřebujete převést Excel do HTML a zachovat vlastní písma, tento návod ukazuje kompletní postup. Také se dozvíte, jak exportovat Excel jako HTML a proč má vkládání písem do HTML význam pro konzistentní vykreslování.

Tento tutoriál pokrývá vše, co potřebujete vědět: požadované knihovny, konfiguraci kódu a ověření vygenerovaného HTML souboru. Na konci budete schopni exportovat Excel jako HTML s vloženými písmy během několika řádků C#.

## Co budete potřebovat

* **.NET 6.0 nebo novější** – kód cílí na .NET 6, ale funguje jakákoli verze .NET, která podporuje Aspose.Cells.
* **Aspose.Cells pro .NET** – získejte licenci nebo použijte bezplatnou zkušební verzi z webu Aspose.
* **Vývojové prostředí C#** (Visual Studio, Rider nebo VS Code) – jakékoli IDE, které dokáže kompilovat projekty .NET.
* Excel sešit (`Styled.xlsx`), který používá vlastní písma, jež chcete zachovat.

## Krok 1: Nastavte Aspose.Cells ve vašem .NET projektu

Nejprve přidejte balíček Aspose.Cells NuGet do svého projektu:

```bash
dotnet add package Aspose.Cells
```

Pak zahrňte jmenný prostor na začátku vašeho C# souboru:

```csharp
using Aspose.Cells;
```

Přidání balíčku zpřístupní třídy `Workbook`, `HtmlSaveOptions` a související třídy.

## Krok 2: Načtěte Excel sešit

Načtení sešitu je první konkrétní krok v **jak exportovat Excel** data. Konstruktor `Workbook` načte soubor z disku:

```csharp
// Step 1: Load the Excel workbook
var workbook = new Workbook("YOUR_DIRECTORY/Styled.xlsx");
```

*Proč je to důležité:* Aspose.Cells analyzuje sešit, včetně stylů buněk, vzorců a informací o písmu. Pokud soubor nelze najít, vyvolá se výjimka, proto se ujistěte, že cesta je správná.

## Krok 3: Nakonfigurujte možnosti uložení HTML pro vložení písem

Jádrem **embed fonts in html** je třída `HtmlSaveOptions`. Nastavte `EmbedFonts` na `true`, aby každé písmo použité v sešitu bylo zapsáno do výstupního HTML jako Base64‑kódované pravidlo `@font-face`.

```csharp
// Step 2: Set HTML save options to embed fonts in the output
var htmlOptions = new HtmlSaveOptions
{
    EmbedFonts = true,
    // Optional: keep the original worksheet name as the HTML file name
    ExportActiveWorksheetOnly = true
};
```

*Proč je to důležité:* Ve výchozím nastavení Aspose.Cells odkazuje na externí soubory písem, které nemusí být na klientském počítači dostupné. Povolení `EmbedFonts` zaručuje, že vykreslené HTML bude vypadat identicky jako původní list Excelu, bez ohledu na nainstalovaná písma u uživatele.

### Okrajový případ: nepodporovaná písma

Pokud sešit používá písmo, které není nainstalováno na serveru, Aspose.Cells přejde na výchozí systémové písmo. Abyste tomu předešli, nainstalujte požadovaná písma na server nebo je po exportu vložte ručně.

## Krok 4: Uložte sešit jako HTML pomocí nakonfigurovaných možností

Nyní můžete zapsat HTML soubor. Metoda `Save` přijímá výstupní cestu a instanci `HtmlSaveOptions`:

```csharp
// Step 3: Save the workbook as an HTML file using the configured options
workbook.Save("YOUR_DIRECTORY/Styled.html", htmlOptions);
```

Po provedení obsahuje `Styled.html` data tabulky a blok `<style>` s Base64‑kódovanými definicemi `@font-face` pro každé vlastní písmo.

## Krok 5: Ověřte vložená písma

Otevřete `Styled.html` v prohlížeči. Prozkoumejte sekci `<head>`; měli byste vidět něco jako:

```html
<style>
@font-face {
    font-family: 'Calibri';
    src: url(data:font/ttf;base64,AAEAAAARAQAABAA...);
}
...
</style>
```

Pokud se písma zobrazí správně v vykreslené tabulce, vložení bylo úspěšné. Pokud zaznamenáte chybějící glyfy, zkontrolujte, že zdrojové soubory písem jsou nainstalovány na stroji provádějícím konverzi.

## Běžné varianty a další možnosti

### Převod více listů

Pokud potřebujete **convert Excel to HTML** pro všechny listy, nastavte `ExportActiveWorksheetOnly = false` (výchozí). Aspose.Cells vytvoří samostatný HTML soubor pro každý list.

```csharp
htmlOptions.ExportActiveWorksheetOnly = false;
workbook.Save("YOUR_DIRECTORY/AllSheets.html", htmlOptions);
```

### Řízení výstupu CSS

Můžete zmenšit velikost HTML vypnutím inline CSS:

```csharp
htmlOptions.ExportCssSeparately = true; // Generates a .css file alongside the .html
```

### Použití proudu místo souboru

Při integraci do webového API zapisujte HTML do `MemoryStream` a vraťte jej přímo:

```csharp
using var stream = new MemoryStream();
workbook.Save(stream, htmlOptions);
stream.Position = 0; // Reset for reading
// Return stream as a file download in ASP.NET Core
```

## Profesionální tip: Licencujte produkt, aby se odstranily vodotisky z hodnocení

Pokud používáte zkušební verzi, vygenerované HTML může obsahovat komentář s vodotiskem. Aplikujte svou licenci Aspose.Cells před načtením sešitu, aby výstup byl čistý:

```csharp
var license = new License();
license.SetLicense("Aspose.Total.lic");
```

## Kompletní funkční příklad

Níže je kompletní, spustitelný program, který demonstruje **jak vložit písma**, **convert excel to html** a **export excel as html** najednou:

```csharp
using System;
using Aspose.Cells;

class ExcelToHtmlWithEmbeddedFonts
{
    static void Main()
    {
        // Apply license if you have one (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Total.lic");

        // 1️⃣ Load the Excel workbook
        var workbookPath = @"YOUR_DIRECTORY/Styled.xlsx";
        var workbook = new Workbook(workbookPath);

        // 2️⃣ Configure HTML save options to embed fonts
        var htmlOptions = new HtmlSaveOptions
        {
            EmbedFonts = true,
            ExportActiveWorksheetOnly = true, // Export only the first sheet
            ExportCssSeparately = false        // Keep CSS inline for a single file
        };

        // 3️⃣ Save as HTML
        var htmlPath = @"YOUR_DIRECTORY/Styled.html";
        workbook.Save(htmlPath, htmlOptions);

        Console.WriteLine($"Excel workbook '{workbookPath}' has been exported to HTML with embedded fonts at '{htmlPath}'.");
    }
}
```

**Očekávaný výstup:** Po spuštění programu se v `YOUR_DIRECTORY` objeví `Styled.html`. Otevření souboru v libovolném moderním prohlížeči zobrazí tabulku se stejnými písmy jako v původním Excel souboru, i na počítačích, kde tato písma chybí.

## Závěr

Nyní víte, **jak vložit písma**, když **převádíte Excel do HTML** pomocí Aspose.Cells, a viděli jste celý tok od načtení sešitu po ověření vložených písem. Tento přístup zajišťuje, že vizuální věrnost vašich Excel souborů zůstane zachována v generovaném HTML, což je ideální pro webové reportování, e‑mailové newslettery nebo jakýkoli scénář, kde musíte **exportovat Excel jako HTML** s vlastní typografií.

Dále prozkoumejte související témata, jako **export Excel as PDF**, **styling HTML output with custom CSS** nebo **batch‑processing multiple workbooks**. Každé z nich staví na stejném vzoru `HtmlSaveOptions`, takže můžete kód přizpůsobit s minimálními změnami.

Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Jak exportovat Excel do HTML – Průvodce krok za krokem](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-step-by-step-guide/)
- [Jak vložit písma do HTML – Kompletní C# průvodce](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-complete-c-guide/)
- [Jak vložit písma při převodu Excelu do PDF – Průvodce krok za krokem](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}