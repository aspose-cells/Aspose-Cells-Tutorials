---
category: general
date: 2026-03-01
description: Naučte se, jak vložit písma do HTML při převodu Excelu na HTML pomocí
  Aspose.Cells. Tento podrobný návod také ukazuje, jak uložit Excel jako HTML.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- convert excel to html
- create html from excel
- save excel as html
language: cs
og_description: Jak vložit písma do HTML při exportu Excelu do HTML. Sledujte tento
  kompletní tutoriál, abyste zachovali typografii napříč prohlížeči.
og_title: Jak vložit fonty do HTML – Rychlý průvodce C#
tags:
- Aspose.Cells
- C#
- HTML export
title: Jak vložit písma do HTML – Převést Excel do HTML pomocí C#
url: /cs/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vložit fonty do HTML – převod Excel do HTML pomocí C#

Už jste se někdy zamysleli **nad tím, jak vložit fonty do HTML**, aby váš převod Excel‑to‑HTML vypadal pixel‑perfect? Nejste v tom sami. Když exportujete sešit do HTML, výchozí chování je odkazovat na systémové fonty, což může rozbít rozvržení na počítačích, které tyto fonty nemají nainstalované.  

Zapnutím vkládání fontů zaručíte, že výstup zachová původní typografii, ať už je zobrazen kdekoliv. V tomto tutoriálu projdeme přesně kroky k **embed fonts in html** pomocí Aspose.Cells pro .NET a také se dotkneme souvisejících úkolů, jako je **convert Excel to HTML**, **create HTML from Excel**, a **save Excel as HTML**.

## Co se naučíte

- Proč je vkládání fontů důležité pro konzistenci napříč prohlížeči.  
- Přesný C# kód potřebný k povolení **embed fonts in html** při ukládání sešitu.  
- Jak řešit běžné okrajové případy, jako jsou velké soubory fontů nebo licenční omezení.  
- Rychlé ověřovací kroky, aby bylo jisté, že jsou fonty skutečně vloženy.

### Požadavky

- .NET 6.0 nebo novější (kód funguje také s .NET Framework 4.6+).  
- NuGet balíček Aspose.Cells pro .NET nainstalován (`Install-Package Aspose.Cells`).  
- Základní znalost C# a práce se soubory Excel.  
- Alespoň jeden vlastní TrueType/OpenType font použitý ve vašem sešitu.

> **Pro tip:** Pokud používáte Visual Studio, povolte „Nullable reference types“, abyste včas zachytili možné problémy s null.

---

## Krok 1: Nastavení projektu a načtení sešitu

Nejprve vytvořte novou konzolovou aplikaci (nebo ji integrujte do existujícího řešení). Pak přidejte jmenný prostor Aspose.Cells.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load an existing Excel file that uses custom fonts
        string sourcePath = @"C:\Temp\Report.xlsx";
        Workbook wb = new Workbook(sourcePath);
```

*Proč je to důležité:* Načtení sešitu poskytuje knihovně přístup k stylům buněk, které obsahují informace o fontu, které později chceme vložit.

---

## Krok 2: Vytvořte **HtmlSaveOptions** a zapněte vkládání fontů

Třída `HtmlSaveOptions` řídí každý aspekt exportu do HTML. Nastavení `EmbedFonts = true` říká Aspose.Cells, aby vložil požadované soubory fontů přímo do HTML (jako Base64‑kódované data URL).

```csharp
        // Step 2: Create HTML save options
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();

        // Enable embedding of fonts in the saved HTML
        htmlOptions.EmbedFonts = true;

        // Optional: Reduce the size of embedded fonts by subsetting
        htmlOptions.SubsetEmbeddedFonts = true;
```

*Proč povolujeme `SubsetEmbeddedFonts`*: Odstraňuje nepoužité glyfy, čímž zmenšuje výsledný HTML soubor – což je zvláště užitečné při práci s velkými rodinami fontů.

---

## Krok 3: Vyberte výstupní složku a uložte HTML

Nyní rozhodněte, kam má být HTML soubor uložen. Aspose.Cells také vygeneruje složku pro podpůrné soubory (obrázky, CSS atd.).  

```csharp
        // Define output location
        string outputFolder = @"C:\Temp\ExportedHtml";
        string outputFile = System.IO.Path.Combine(outputFolder, "Report.html");

        // Ensure the folder exists
        System.IO.Directory.CreateDirectory(outputFolder);

        // Step 3: Save the workbook as HTML with the configured options
        wb.Save(outputFile, htmlOptions);

        Console.WriteLine($"HTML file with embedded fonts saved to: {outputFile}");
    }
}
```

*Co uvidíte:* Otevřete výsledný `Report.html` v libovolném prohlížeči. Vlastní fonty by se měly vykreslovat správně i v případě, že font není nainstalován na počítači.

---

## Krok 4: Ověřte, že jsou fonty skutečně vloženy

Rychlý způsob, jak potvrdit vložení, je prozkoumat vygenerovaný HTML soubor. Hledejte bloky `<style>`, které obsahují pravidla `@font-face` s `src: url(data:font/ttf;base64,…)`.  

```html
/* Example snippet from the output */
@font-face {
    font-family: 'MyCustomFont';
    src: url(data:font/ttf;base64,AAEAAAARAQAABAA...);
    font-weight: normal;
    font-style: normal;
}
```

Pokud vidíte URI `data:`, font je vložen. Neměly by být odkazovány žádné externí soubory `.ttf` nebo `.woff`.

---

## Časté otázky a okrajové případy

| Otázka | Odpověď |
|----------|--------|
| **Co když můj sešit používá mnoho různých fontů?** | Vložení všech může zvětšit velikost HTML. Použijte `htmlOptions.SubsetEmbeddedFonts = true`, aby se zachovaly jen potřebné glyfy, nebo ručně omezte, které fonty vložit pomocí `htmlOptions.FontsToEmbed`. |
| **Musím se starat o licencování fontů?** | Rozhodně. Vložení fontu do HTML souboru vytvoří kopii, která je distribuována s vaším obsahem. Ujistěte se, že máte právo font redistribuovat (např. open‑source fonty jako Google Fonts jsou v pořádku). |
| **Bude to fungovat ve starších prohlížečích jako IE9?** | Přístup pomocí Base64 data‑URI je podporován až do IE8, ale existuje limit velikosti (~32 KB). Pro velmi velké fonty zvažte přechod na externí soubory fontů a jejich servírování přes HTTP. |
| **Mohu vložit fonty při převodu Excel do PDF místo HTML?** | Ano—Aspose.Cells také podporuje `PdfSaveOptions.EmbedStandardFonts` a `PdfSaveOptions.FontEmbeddingMode`. Koncept je stejný, jen jiná API. |
| **Co když potřebuji **create HTML from Excel** na serveru bez UI?** | Stejný kód funguje v ASP.NET Core, Azure Functions nebo jakémkoli headless prostředí—stačí zajistit, aby proces měl přístup ke čtení souborů fontů. |

## Tipy pro výkon

1. **Cache the HTML** pokud exportujete stejný sešit opakovaně; krok vkládání může být náročný na CPU.  
2. **Compress the output folder** (zabalte do zipu) před odesláním po síti; vložené fonty jsou již Base64‑kódované, takže zip stále ušetří několik kilobajtů.  
3. **Avoid embedding system fonts** (Arial, Times New Roman), pokud nepotřebujete konkrétní verzi; prohlížeče je už mají.

## Kompletní funkční příklad (připravený ke zkopírování)

```csharp
using System;
using Aspose.Cells;

class EmbedFontsDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook (your Excel file must contain custom fonts)
        string excelPath = @"C:\Temp\Sample.xlsx";
        Workbook workbook = new Workbook(excelPath);

        // 2️⃣ Prepare HTML options with font embedding enabled
        HtmlSaveOptions options = new HtmlSaveOptions
        {
            EmbedFonts = true,               // ✅ This is the key line for embedding fonts
            SubsetEmbeddedFonts = true,      // ✅ Reduces file size by keeping only used glyphs
            ExportActiveWorksheetOnly = true // Optional: export just the active sheet
        };

        // 3️⃣ Define where the HTML will be saved
        string outputDir = @"C:\Temp\HtmlExport";
        System.IO.Directory.CreateDirectory(outputDir);
        string htmlPath = System.IO.Path.Combine(outputDir, "Sample.html");

        // 4️⃣ Save the workbook as HTML
        workbook.Save(htmlPath, options);

        Console.WriteLine($"✅ HTML with embedded fonts saved at: {htmlPath}");
    }
}
```

Spuštěním tohoto programu se vytvoří soubor `Sample.html`, který **embed fonts in html** a lze jej otevřít na jakémkoli zařízení bez ztráty původního vzhledu.

## Závěr

Probrali jsme **how to embed fonts in HTML** při **convert Excel to HTML**, čímž zajistíme, že vizuální věrnost vašeho sešitu přežije cestu na web. Přepnutím `HtmlSaveOptions.EmbedFonts` (a volitelně `SubsetEmbeddedFonts`) získáte samostatný HTML soubor, který funguje napříč prohlížeči, i na počítačích, kde chybí původní fonty.  

Dále můžete zkoumat **create HTML from Excel** pro více listů, nebo se ponořit do **save Excel as HTML** s vlastními CSS tématy. Obě situace používají stejný objekt `HtmlSaveOptions`—stačí upravit vlastnosti jako `ExportActiveWorksheetOnly` nebo `CssStyleSheetType`.  

Vyzkoušejte to, upravte možnosti a nechte vložené fonty udělat těžkou práci. Pokud narazíte na problémy, zanechte komentář—šťastné programování!  

![Příklad vložení fontů do HTML](https://example.com/images/embed-fonts.png "Jak vložit fonty do HTML")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}