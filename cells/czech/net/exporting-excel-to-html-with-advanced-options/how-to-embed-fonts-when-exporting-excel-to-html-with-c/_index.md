---
category: general
date: 2026-10-10
description: Naučte se, jak vložit písma při exportu Excelu do HTML v C#. Tento průvodce
  zahrnuje export Excel do HTML, konverzi Excel do HTML a jak uložit Excel s vloženými
  písmy.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- export excel html
- convert excel html
- how to save excel
- embed fonts html
language: cs
lastmod: 2026-10-10
og_description: Jak vložit písma při exportu Excelu do HTML v C#. Sledujte tento kompletní
  návod, jak exportovat Excel do HTML, převést Excel HTML a naučte se, jak uložit
  Excel s vloženými písmy.
og_image_alt: Screenshot showing exported HTML file that demonstrates how to embed
  fonts from Excel
og_title: Jak vložit písma při exportu Excelu do HTML – krok za krokem průvodce v
  C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to embed fonts while exporting Excel to HTML in C#. This
    guide covers export excel html, convert excel html, and how to save Excel with
    embedded fonts.
  headline: How to embed fonts when exporting Excel to HTML with C#
  type: TechArticle
tags:
- Excel
- HTML export
- Font embedding
- C#
title: Jak vložit písma při exportu Excelu do HTML pomocí C#
url: /cs/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-exporting-excel-to-html-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vložit písma při exportu Excelu do HTML pomocí C#

Pokud potřebujete **jak vložit písma** do HTML souboru vygenerovaného z Excel sešitu, tento tutoriál ukazuje přesné kroky. Exportování Excelu do HTML často odstraňuje vlastní písma, což narušuje vizuální věrnost původní tabulky. Správným nastavením možností můžete zachovat každé písmo přímo v HTML výstupu.

V tomto průvodci se naučíte, jak **exportovat excel html**, **převést excel html** a **jak uložit Excel** s vloženými písmy pomocí knihovny Aspose.Cells pro .NET. Řešení funguje s .NET 6+ a vyžaduje jen několik řádků C# kódu.

## Co dosáhnete

- Kompletní, spustitelný C# program, který načte existující soubor `.xlsx`.
- HTML výstup, kde jsou všechna použitá písma vložena jako Base64‑kódované `@font-face` pravidla.
- Jistota, že exportované HTML vypadá identicky jako zdrojový sešit v jakémkoli prohlížeči.

## Požadavky

| Požadavek | Důvod |
|-------------|--------|
| .NET 6 SDK or later | Poskytuje runtime pro C# projekt. |
| Visual Studio 2022 (or any IDE) | Umožňuje snadno vytvořit a spustit konzolovou aplikaci. |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | Poskytuje třídu `HtmlSaveOptions` a funkci `EmbedFonts`. |
| An Excel file (`sample.xlsx`) that uses a custom font (e.g., *Calibri* or a downloaded TrueType font) | Excel soubor (`sample.xlsx`), který používá vlastní písmo (např. *Calibri* nebo stažené TrueType písmo). Demonstruje efekt vložení písma. |

> **Tip:** Pokud pracujete za firemním proxy, nakonfigurujte NuGet tak, aby používal proxy před instalací balíčku.

## Krok 1: Instalace Aspose.Cells

Otevřete terminál ve složce projektu a spusťte:

```bash
dotnet add package Aspose.Cells
```

Příkaz přidá nejnovější stabilní verzi Aspose.Cells do vašeho projektu, čímž zpřístupní třídy `Workbook` a `HtmlSaveOptions`.

## Krok 2: Načtení Excel sešitu

Vytvořte novou konzolovou aplikaci (`dotnet new console`) a přidejte následující kód do souboru `Program.cs`:

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load an existing workbook. Replace the path with your actual file location.
        Workbook wb = new Workbook("sample.xlsx");
        // Continue with HTML export...
    }
}
```

**Proč je tento krok důležitý:**  
Načtení sešitu vám poskytuje přístup k jeho listům, stylům a vlastním písmům odkazovaným v souboru. Bez načtené instance `Workbook` nemůžete konfigurovat možnosti exportu.

## Krok 3: Nastavení možností uložení HTML pro vložení písem

Třída `HtmlSaveOptions` řídí každý aspekt exportu do HTML. Nastavením `EmbedFonts = true` řeknete Aspose.Cells, aby vložil každé písmo použité v sešitu přímo do vygenerovaného HTML souboru.

```csharp
// Configure HTML save options to embed fonts
HtmlSaveOptions opts = new HtmlSaveOptions
{
    // When true, the exporter creates @font-face rules with Base64 data.
    EmbedFonts = true,

    // Optional: keep the original folder structure for images.
    ExportImagesAsBase64 = true,

    // Optional: generate a single HTML file (no external CSS folder).
    ExportActiveWorksheetOnly = false
};
```

**Vysvětlení:**  
- `EmbedFonts` je klíčový příznak, který splňuje požadavek **jak vložit písma**.  
- `ExportImagesAsBase64` zajišťuje, že všechny obrázky se také stanou součástí jediného HTML souboru, což usnadňuje nasazení.  
- `ExportActiveWorksheetOnly` nastavený na `false` zaručuje, že jsou zahrnuty všechny listy, což je užitečné, když sešit obsahuje více listů.

## Krok 4: Uložení sešitu jako HTML s vloženými písmy

Nyní zavolejte metodu `Save`, předáte požadovanou cestu výstupu a možnosti, které jste právě nakonfigurovali:

```csharp
// Save the workbook as an HTML file with embedded fonts
wb.Save("Embedded.html", opts);
```

Výsledný soubor `Embedded.html` obsahuje:

- Standardní HTML značky pro data tabulky.
- Jeden nebo více bloků `<style>` s pravidly `@font-face`, které vkládají vlastní písma jako Base64 řetězce.
- Všechny obrázky zakódované přímo v HTML (pokud jsou).

## Krok 5: Ověření, že jsou písma skutečně vložena

Otevřete `Embedded.html` v prohlížeči (Chrome, Edge, Firefox). Stránka by měla vypadat přesně jako originální Excel sešit, i když cílový počítač nemá vlastní písma nainstalována.

Pro dvojitou kontrolu vložení:

1. Otevřete zdrojový kód stránky (`Ctrl+U` ve většině prohlížečů).  
2. Vyhledejte `@font-face`. Uvidíte blok podobný:

```css
@font-face {
    font-family: 'Calibri';
    src: url('data:font/ttf;base64,AAEAAAALAIAAAwAwT1Mv...') format('truetype');
    font-weight: normal;
    font-style: normal;
}
```

Pokud atribut `src` obsahuje URL typu `data:`, písmo bylo úspěšně vloženo.

## Běžné varianty a okrajové případy

| Situace | Navrhovaná úprava |
|-----------|----------------------|
| **Velký sešit s mnoha vlastními písmy** | Zvyšte `MaxFontEmbeddingSize` (pokud je k dispozici) nebo rozdělte export do více HTML souborů, aby nedošlo k překročení limitů velikosti prohlížeče. |
| **Potřebujete jen jeden list** | Nastavte `opts.ExportActiveWorksheetOnly = true` a aktivujte požadovaný list před uložením (`wb.Worksheets[0].Activate();`). |
| **Vkládání písem není povoleno firemní politikou** | Nastavte `opts.EmbedFonts = false` a spoléhejte se na web‑bezpečná písma nebo poskytněte soubory písem vedle HTML. |
| **Cílení na starší prohlížeče, které nepodporují Base64 písma** | Použijte `opts.FontEmbeddingMode = FontEmbeddingMode.FontFile;` (pokud verze knihovny podporuje) k vytvoření samostatných `.ttf` souborů a odkazujte na ně běžnými URL. |

## Kompletní, spustitelný příklad

Níže je kompletní program, který můžete zkopírovat a vložit do `Program.cs`. Obsahuje všechny potřebné `using` direktivy a ošetření chyb pro produkčně připravený skript.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load the workbook (replace with your file path)
            Workbook wb = new Workbook("sample.xlsx");

            // 2️⃣ Configure HTML export options to embed fonts
            HtmlSaveOptions opts = new HtmlSaveOptions
            {
                EmbedFonts = true,               // ✅ Core requirement: how to embed fonts
                ExportImagesAsBase64 = true,     // Keep everything in one file
                ExportActiveWorksheetOnly = false
            };

            // 3️⃣ Save as HTML with embedded fonts
            string outputPath = "Embedded.html";
            wb.Save(outputPath, opts);

            Console.WriteLine($"HTML file with embedded fonts saved to: {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**Očekávaný výstup:**  
Spuštěním programu se vypíše potvrzovací řádek a vytvoří se `Embedded.html`. Otevřením souboru v libovolném moderním prohlížeči se zobrazí tabulka se všemi původními písmy zachovanými, čímž splníte cíl **jak vložit písma**.

## Závěr

Nyní víte, **jak vložit písma** při provádění operace **export excel html**, jak **převést excel html** bez ztráty typů písma, a přesné kroky **jak uložit excel** jako HTML soubor s vloženými písmy. Použitím `HtmlSaveOptions.EmbedFonts = true` se vygenerované HTML stane samostatným, přenosným a vizuálně identickým se zdrojovým sešitem.

### Co dál?

- Prozkoumejte vlastnosti `HtmlSaveOptions` pro řízení CSS, zpracování obrázků a výběr listů.  
- Kombinujte tuto techniku se server‑side automatizací pro generování HTML reportů za běhu.  
- Podívejte se na **embed fonts html** pro jiné formáty dokumentů (např. PDF) pomocí podobných Aspose API.

Neváhejte experimentovat s různými písmy, velikostmi sešitu a prostředími prohlížečů. Pokud narazíte na problémy, podívejte se znovu na tabulku okrajových případů výše nebo konzultujte dokumentaci Aspose.Cells pro pokročilé scénáře vkládání písem. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak exportovat Excel do HTML – Kompletní programovací průvodce](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-complete-programming-guide/)
- [Jak exportovat Excel do HTML – Průvodce krok za krokem](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-step-by-step-guide/)
- [Jak vložit písma při konverzi Excelu do PDF – Kompletní průvodce](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-complete-gui/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}