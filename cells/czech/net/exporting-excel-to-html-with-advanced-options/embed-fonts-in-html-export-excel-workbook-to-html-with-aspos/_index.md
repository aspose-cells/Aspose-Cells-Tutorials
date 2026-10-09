---
category: general
date: 2026-06-17
description: Vkládejte písma do HTML při ukládání sešitu jako HTML. Naučte se, jak
  převést sešit do HTML a exportovat Excel HTML s vloženými písmy během několika kroků.
draft: false
keywords:
- embed fonts in html
- save workbook as html
- convert workbook to html
- how to export excel html
language: cs
og_description: Vkládejte písma do HTML při ukládání sešitu jako HTML. Postupujte
  podle tohoto návodu, jak převést sešit do HTML, a zjistěte, jak exportovat Excel
  HTML s úplnou podporou písem.
og_title: Vložit písma do HTML – Exportovat sešit Excelu do HTML
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Embed fonts in HTML while you save workbook as HTML. Learn how to convert
    workbook to HTML and export Excel HTML with embedded fonts in a few steps.
  headline: Embed Fonts in HTML – Export Excel Workbook to HTML with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Excel
- HTML export
title: Vložit písma do HTML – Exportovat sešit Excel do HTML pomocí Aspose.Cells
url: /cs/net/exporting-excel-to-html-with-advanced-options/embed-fonts-in-html-export-excel-workbook-to-html-with-aspos/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vložit písma do HTML – Export sešitu Excel do HTML pomocí Aspose.Cells

Už jste se někdy zamýšleli, jak **vložit písma do HTML** při exportu listu Excel? Nejste v tom jediní. Mnoho vývojářů narazí na problém, když vygenerované HTML zobrazuje obecné sans‑serif místo původního stylu v Excelu. Dobrá zpráva? Pár řádků kódu vám umožní **uložit sešit jako HTML** a zachovat všechna písma beze změny.

V tomto tutoriálu projdeme celý proces **převodu sešitu do HTML** pomocí Aspose.Cells pro .NET, vysvětlíme, proč je vkládání písem důležité, a ukážeme vám přesně **jak exportovat Excel do HTML**, aby výsledek vypadal přesně jako zdrojová tabulka. Žádné externí nástroje, žádné ruční post‑processing—pouze čistý, spustitelný C# kód.

## Požadavky

- .NET 6.0 nebo novější (příklad funguje na .NET Core, .NET Framework a .NET 5+)
- NuGet balíček Aspose.Cells pro .NET (`Install-Package Aspose.Cells`)
- Základní znalost C# a práce se soubory Excel
- Volitelné: vlastní soubor TrueType fontu, který chcete vložit (např. `MyFont.ttf`)

Máte vše připravené? Skvělé—ponořme se.

## Krok 1: Nastavení projektu a načtení sešitu Excel

Nejprve potřebujeme objekt sešitu. Můžete jej vytvořit od nuly nebo načíst existující `.xlsx`. Zde je minimální nastavení, které také přidá vlastní font do kolekce stylů sešitu.

```csharp
using Aspose.Cells;
using System.IO;

// Load an existing workbook (replace with your own path)
Workbook wb = new Workbook("SampleData.xlsx");

// OPTIONAL: Register a custom font if your sheet uses one that isn’t standard
string fontPath = Path.Combine(Directory.GetCurrentDirectory(), "MyFont.ttf");
if (File.Exists(fontPath))
{
    // Register the font with the font manager – this ensures Aspose knows about it
    FontConfigs.AddFontFile(fontPath);
}
```

*Proč tento krok?* Načtením sešitu nejprve dáváme Aspose.Cells možnost prozkoumat všechny styly buněk. Registrace vlastního fontu zajišťuje, že font bude nalezen, když jej později vložíme do HTML souboru.

## Krok 2: Konfigurace HTML Save Options pro **vložení písem do HTML**

Magie spočívá v `HtmlSaveOptions`. Nastavením `EmbedFonts = true` říkáte knihovně, aby vložila každé použité písmo jako Base64‑kódované pravidlo `@font-face` uvnitř vygenerovaného HTML souboru.

```csharp
// Configure HTML save options – this is where we embed fonts in HTML
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // Embed all referenced fonts directly into the HTML output
    EmbedFonts = true,

    // Optional: keep the original layout (useful for complex sheets)
    ExportActiveWorksheetOnly = true,

    // Optional: produce a single HTML file (no external CSS or images)
    ExportImagesAsBase64 = true
};
```

*Proč povolit `EmbedFonts`?* Bez toho odkazuje výstupní HTML na systémová písma a kdokoli, kdo otevře soubor na počítači, kde tato písma nejsou nainstalována, uvidí náhradní písmo. Vkládání zaručuje vizuální věrnost napříč prohlížeči a zařízeními.

## Krok 3: **Uložit sešit jako HTML** s nakonfigurovanými možnostmi

Nyní soubor konečně zapíšeme. Metoda `Save` přijímá tři argumenty: cílovou cestu, formát (`SaveFormat.Html`) a možnosti, které jsme právě nakonfigurovali.

```csharp
// Define the output HTML file path
string outputPath = Path.Combine(Directory.GetCurrentDirectory(), "with-fonts.html");

// Save the workbook as HTML with embedded fonts
wb.Save(outputPath, SaveFormat.Html, saveOptions);
```

Pokud vše proběhne hladce, získáte jediný soubor `with-fonts.html`, který obsahuje kompletní rozvržení tabulky *a* data fontu zakódovaná přímo v markupu.

## Očekávaný výstup

Otevřete `with-fonts.html` v libovolném moderním prohlížeči (Chrome, Edge, Firefox). Měli byste vidět:

- Stejné hodnoty buněk, barvy a ohraničení jako v původním souboru Excel.
- Text vykreslený ve stejném fontu, který jste použili v Excelu, i když tento font není nainstalován na vašem počítači.
- Žádné externí `.css` nebo souborové obrázky—vše je uvnitř HTML souboru.

Níže je malý úryvek toho, jak může vygenerovaný blok `<style>` vypadat (řetězec Base64 je zkrácen pro stručnost):

```html
<style type="text/css">
@font-face{
    font-family:'MyCustomFont';
    src:url(data:font/truetype;charset=utf-8;base64,AAEAAAALAIAAAwAwT1Mv... ) format('truetype');
}
...
</style>
```

## Krok 4: Časté úskalí a jak je opravit

| Problém | Proč k tomu dochází | Oprava |
|------|----------------|-----|
| **Missing font in the HTML** | The font file wasn’t registered with `FontConfigs` before saving. | Call `FontConfigs.AddFontFile` *before* creating `HtmlSaveOptions`. |
| **Huge HTML file size** | Embedding many large fonts can inflate the file. | Only embed the fonts you actually need; use `saveOptions.FontEmbeddingMode = FontEmbeddingMode.Subset` to embed only used glyphs (available in newer Aspose versions). |
| **Incorrect characters (e.g., Asian glyphs)** | Font doesn’t contain required Unicode ranges. | Ensure the source font supports the characters, or embed an additional fallback font. |
| **Performance slowdown on large workbooks** | Embedding fonts adds processing overhead. | Export only the active worksheet (`ExportActiveWorksheetOnly = true`) or split the workbook into smaller parts. |

## Krok 5: Rozšíření řešení – Export více listů

Pokud potřebujete **převést sešit do HTML** pro všechny listy, jednoduše vypněte `ExportActiveWorksheetOnly`:

```csharp
saveOptions.ExportActiveWorksheetOnly = false; // Export every sheet
wb.Save("all-sheets.html", SaveFormat.Html, saveOptions);
```

Každý list se objeví jako samostatný `<div>` ve stejném HTML souboru, stále s vloženými fonty.

## Tip: Kombinace s úpravou CSS

Někdy chcete mít přísnější kontrolu nad vygenerovaným markupem. `HtmlSaveOptions` nabízí vlastnost `CssClassPrefix`, která zabraňuje kolizím názvů tříd při slučování více HTML exportů:

```csharp
saveOptions.CssClassPrefix = "myExcel_";
```

Nyní každá vygenerovaná CSS třída začne `myExcel_`, což usnadní pozdější použití vlastního stylesheetu.

## Shrnutí

- **Vložit písma do HTML** nastavením `HtmlSaveOptions.EmbedFonts = true`.
- Použijte **uložit sešit jako HTML** (`wb.Save(..., SaveFormat.Html, ...)`) k vytvoření jediného, samostatného souboru.
- Tato metoda **převádí sešit do HTML** při zachování každého vizuálního detailu, odpovídá na klasickou otázku **jak exportovat Excel do HTML** s plnou věrností.
- Zaregistrujte vlastní fonty pomocí `FontConfigs.AddFontFile`, aby byly k dispozici pro vložení.
- Upravit možnosti jako `ExportImagesAsBase64` a `ExportActiveWorksheetOnly`, aby vyhovovaly potřebám vašeho projektu.

## Co dál?

- Zkuste exportovat do **MHTML** (`SaveFormat.Mhtml`) pro ještě přenosnější balíček.
- Prozkoumejte **konverzi do PDF** (`SaveFormat.Pdf`), pokud potřebujete formát připravený k tisku.
- Integrovat export HTML do webového API, aby si uživatelé mohli okamžitě stáhnout stylizované tabulky.

Neváhejte experimentovat—měňte fonty, výběr listů nebo kombinujte více exportních formátů. Flexibilita Aspose.Cells vám umožní přizpůsobit výstup jakémukoli scénáři, od automatizovaných reportovacích dashboardů po HTML úryvky připravené k odeslání e-mailem.

Šťastné programování a ať váš HTML vždy vypadá přesně jako původní list Excel!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která navazují na techniky předvedené v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak vytvořit a exportovat Excel do HTML pomocí Aspose.Cells Java \| Průvodce operacemi sešitu](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Nastavení výchozího písma při konverzi Excel do HTML s Aspose.Cells pro .NET \| Průvodce operacemi sešitu](/cells/english/net/workbook-operations/excel-html-conversion-default-font-aspose-cells-net/)
- [Jak exportovat Excel do HTML s mřížkovými čarami pomocí Aspose.Cells pro .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}