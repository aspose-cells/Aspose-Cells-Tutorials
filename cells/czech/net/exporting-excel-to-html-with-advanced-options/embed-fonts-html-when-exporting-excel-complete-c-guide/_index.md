---
category: general
date: 2026-02-28
description: Naučte se, jak vložit písma do HTML při exportu Excelu do HTML pomocí
  Aspose.Cells. Obsahuje tipy na uložení jako HTML, export Excelu do HTML a převod
  tabulky do HTML.
draft: false
keywords:
- embed fonts html
- export excel html
- save as html
- save excel html
- convert spreadsheet html
language: cs
og_description: Vkládání fontů do HTML je nezbytné pro dokonalou konverzi Excel‑na‑HTML.
  Tento průvodce vám ukáže, jak exportovat Excel HTML s vloženými fonty pomocí Aspose.Cells.
og_title: Vkládání fontů do HTML při exportu z Excelu – Kompletní průvodce C#
tags:
- Aspose.Cells
- C#
- HTML export
- Excel automation
title: Vkládání fontů do HTML při exportu z Excelu – Kompletní C# průvodce
url: /cs/net/exporting-excel-to-html-with-advanced-options/embed-fonts-html-when-exporting-excel-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# embed fonts html při exportu Excel – Kompletní průvodce C#

Už jste někdy potřebovali **embed fonts html** při převodu sešitu Excel na webovou stránku? Nejste v tom sami — mnoho vývojářů narazí na problém, kdy vygenerované HTML vypadá na jejich počítači dobře, ale na jiném prohlížeči ztrácí přesnou typografii. Dobrá zpráva? S několika řádky C# a Aspose.Cells můžete **export excel html**, který nese původní písma přímo v souboru.

V tomto tutoriálu projdeme každý krok k **save as html** s vloženými písmy, probereme, proč byste možná chtěli **save excel html** bez písem, a dokonce ukážeme rychlý způsob, jak **convert spreadsheet html** pro e‑mailové newslettery. Žádné externí nástroje, jen čistý kód, který můžete vložit do libovolného .NET projektu.

## Co budete potřebovat

- **Aspose.Cells for .NET** (nejnovější verze, 2025‑R2 v době psaní).  
- Vývojové prostředí .NET (Visual Studio 2022 nebo VS Code).  
- Excelový sešit, který chcete exportovat (libovolný soubor *.xlsx*).

To je vše — žádné další balíčky, žádné složité JavaScriptové triky. Jakmile máte knihovnu přidánu, zbytek je jednoduchý.

## Krok 1: Nastavení projektu a přidání Aspose.Cells

Nejprve vytvořte novou konzolovou aplikaci (nebo ji integrujte do existující služby). Přidejte NuGet balíček:

```bash
dotnet add package Aspose.Cells
```

> **Tip:** Pokud používáte firemní zdroj, ujistěte se, že je nastavený; jinak příkaz selže tiše.

Nyní zahrňte jmenný prostor na začátku vašeho C# souboru:

```csharp
using Aspose.Cells;
using Aspose.Cells.Saving;
```

Tato using vám poskytne přístup ke třídě `Workbook` a `HtmlSaveOptions`, které budeme později potřebovat.

## Krok 2: Načtení Excelového sešitu

Můžete načíst sešit z disku, proudu nebo dokonce z pole bajtů. Zde je nejjednodušší verze, která čte ze souboru:

```csharp
// Load the source Excel file
Workbook wb = new Workbook(@"C:\Files\SampleData.xlsx");

// Optional: adjust settings like calculation mode if needed
wb.CalculateFormula();
```

Proč volat `CalculateFormula()`? Pokud list obsahuje vzorce, knihovna vypočítá jejich hodnoty před exportem, což zajistí, že HTML zobrazí stejné čísla jako v Excelu.

## Krok 3: Nastavení HTML Save Options pro vložení písem

Toto je jádro tutoriálu. Ve výchozím nastavení Aspose.Cells vytváří HTML soubor, který odkazuje na externí CSS a soubory písem. Pro **embed fonts html** přepněte příznak `EmbedFonts`:

```csharp
// Step 3: Configure HTML save options to embed fonts in the output
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // Embeds all used fonts directly into the HTML as Base64‑encoded data URIs
    EmbedFonts = true,

    // Optional: keep the original cell formatting
    ExportActiveWorksheetOnly = true,

    // Optional: generate a single HTML file (no separate CSS folder)
    ExportToSingleFile = true
};
```

Nastavení `EmbedFonts = true` říká Aspose.Cells, aby vzalo každé písmo použité v sešitu, převedlo jej na řetězec Base64 a vložilo do bloku `<style>`. To zaručuje, že kdokoli otevře `Result.html`, uvidí přesně stejnou typografii, bez ohledu na to, zda je písmo nainstalováno v jejich systému.

## Krok 4: Uložení sešitu jako HTML

Nyní spojíme sešit a možnosti a vytvoříme finální soubor:

```csharp
// Step 4: Save the document as an HTML file using the configured options
string outputPath = @"C:\Files\Result.html";
wb.Save(outputPath, SaveFormat.Html, htmlOptions);
```

Po provedení tohoto řádku bude `Result.html` umístěn vedle všech podpůrných zdrojů (pokud jste neaktivovali `ExportToSingleFile`). Otevřete jej v Chrome, Edge nebo Firefoxu — uvidíte, že písma vypadají identicky jako v původním Excelu.

### Rychlé ověření

Aby jste se ujistili, že jsou písma skutečně vložena, otevřete HTML soubor v textovém editoru a vyhledejte `@font-face`. Měli byste vidět blok podobný tomuto:

```css
@font-face {
    font-family: 'Calibri';
    src: url(data:font/ttf;base64,AAEAAA...);
}
```

Pokud atribut `src` obsahuje dlouhý `data:` URL, úspěšně jste to dokončili.

## Krok 5: Co když nechcete vložená písma?

Někdy dáváte přednost lehčímu HTML souboru a nevadí vám, že prohlížeč použije systémová písma. Stačí přepnout příznak:

```csharp
htmlOptions.EmbedFonts = false; // This will generate a normal CSS reference
```

Tento přístup je užitečný, když generujete **export excel html** pro interní dashboardy, kde řídíte prostředí, nebo když potřebujete **convert spreadsheet html** pro e‑mail s nízkou šířkou pásma, kde velikost hraje roli.

## Krok 6: Řešení okrajových případů a běžných úskalí

| Situace | Doporučené řešení |
|-----------|-----------------|
| **Velké sešity** ( > 50 MB ) | Použijte `ExportToSingleFile = false`, aby HTML a data písem zůstaly oddělené; prohlížeče špatně zvládají velké řetězce Base64. |
| **Vlastní písma nejsou vložena** | Ujistěte se, že písmo je nainstalováno na počítači, kde probíhá konverze; Aspose.Cells může vložit jen písma, která najde. |
| **Chybějící glyfy** | Některé funkce OpenType mohou být ztraceny; zvažte konverzi listu na obrázek (`SaveFormat.Png`) jako záložní řešení. |
| **Problémy s výkonem** | Ukládejte objekt `HtmlSaveOptions` do cache, pokud konvertujete mnoho souborů ve smyčce; vyhněte se jeho opakovanému vytváření v každé iteraci. |

## Krok 7: Kompletní funkční příklad

Spojením všeho dohromady, zde je samostatný program, který můžete zkopírovat a spustit:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Saving;

namespace ExcelToHtmlWithEmbeddedFonts
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string sourcePath = @"C:\Files\SampleData.xlsx";
            Workbook wb = new Workbook(sourcePath);
            wb.CalculateFormula(); // Ensure formulas are up‑to‑date

            // 2️⃣ Configure HTML options (embed fonts)
            HtmlSaveOptions htmlOptions = new HtmlSaveOptions
            {
                EmbedFonts = true,
                ExportActiveWorksheetOnly = true,
                ExportToSingleFile = true,
                // Optional: set a custom CSS class prefix to avoid clashes
                CssClassPrefix = "aspose_"
            };

            // 3️⃣ Save as HTML
            string outputPath = @"C:\Files\Result.html";
            wb.Save(outputPath, SaveFormat.Html, htmlOptions);

            Console.WriteLine($"✅ HTML file with embedded fonts created at: {outputPath}");
        }
    }
}
```

Spusťte program a poté otevřete `Result.html`. Měli byste vidět list vykreslený se stejnými písmy jako v Excelu — žádné chybějící znaky, žádná náhradní písma.

![embed fonts html example](/images/embed-fonts-html.png){alt="výsledek embed fonts html ukazující přesnou typografii"}

## Závěr

Nyní máte kompletní end‑to‑end řešení pro **embed fonts html** při provádění operace **export excel html** pomocí Aspose.Cells. Přepnutím jediné vlastnosti můžete přepnout mezi těžkým, plně samostatným HTML souborem a lehčí verzí, která spoléhá na externí písma. Tato flexibilita usnadňuje **save as html**, **save excel html**, nebo dokonce **convert spreadsheet html** pro různé scénáře — od interních reportovacích dashboardů po e‑mailové newslettery připravené k odeslání.  

Co dál? Zkuste exportovat více listů do jedné HTML stránky, experimentujte s různými možnostmi zpracování obrázků (`HtmlSaveOptions.ImageFormat`) nebo zkombinujte toto s konverzí do PDF, abyste nabídli jak webové, tak tiskové formáty. Možnosti jsou neomezené a nyní máte pod rukama základní techniku.  

Šťastné programování a neváhejte zanechat komentář, pokud narazíte na potíže!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}