---
category: general
date: 2026-02-09
description: Zjistěte, jak vložit písma do HTML při exportu Excelu do HTML pomocí
  Aspose.Cells. Tento návod krok za krokem také zahrnuje převod Excelu do HTML a jak
  exportovat Excel s vloženými písmy.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- export excel to html
- convert excel to html
- how to export excel
language: cs
og_description: Jak vložit písma do HTML při exportu Excelu. Postupujte podle tohoto
  kompletního návodu, jak převést Excel do HTML s vloženými písmy pomocí Aspose.Cells.
og_title: Jak vložit písma do HTML – Průvodce exportem Excelu do HTML
tags:
- Aspose.Cells
- C#
- Excel
- HTML
title: Jak vložit písma do HTML při exportu z Excelu – kompletní průvodce
url: /cs/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-when-exporting-excel-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vložit písma do HTML při exportu Excelu – Kompletní průvodce

Už jste se někdy zamýšleli **jak vložit písma do HTML** při převodu sešitu Excel na webovou stránku? Nejste jediní. Mnoho vývojářů narazí na problém, když vygenerované HTML vypadá na jejich počítači dobře, ale v prohlížeči se zobrazí s generickými náhradními písmy. Dobrá zpráva? S několika řádky C# a správnými možnostmi ukládání můžete doručit přesně tu typografii, kterou jste navrhli v Excelu.

V tomto tutoriálu vás provedeme exportem souboru Excel do HTML **s vloženými písmy**, pomocí Aspose.Cells pro .NET. Po cestě se také dotkneme základů *export excel to html*, ukážeme vám, jak *convert excel to html* v různých scénářích, a odpovíme na nevyhnutelné otázky „**how to export excel**“, které se objevují na fórech.

## Co si odnesete

- Plně funkční C# konzolová aplikace, která uloží sešit `.xlsx` jako `embedded.html`.
- Vysvětlení, proč má vložení písem význam pro věrnost napříč prohlížeči.
- Tipy pro práci s licencováním písem, velkými sešity a výkonem.
- Rychlé tipy na alternativní způsoby *export excel to html*, pokud nepoužíváte Aspose.Cells.

### Požadavky

- .NET 6.0 nebo novější (kód také funguje na .NET Framework 4.7+).
- Aspose.Cells pro .NET nainstalovaný přes NuGet (`Install-Package Aspose.Cells`).
- Základní znalost C# a objektového modelu Excelu.
- Písmo TrueType (`.ttf`) nebo OpenType (`.otf`), ke kterému máte právo vložit.

Žádné těžké nastavení, žádný COM interop, jen pár NuGet balíčků a textový editor.

---

## Jak vložit písma do HTML – Krok 1: Připravte svůj sešit

Než můžeme Aspose.Cells říct, aby vložil písma, potřebujeme sešit, který skutečně používá vlastní písmo. Vytvořme malý sešit v paměti, aplikujme na buňku ne‑systémové písmo a uložíme jej.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Saving;   // Needed for HtmlSaveOptions

// Step 1: Create a new workbook and access the first worksheet
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];

// Step 2: Insert some text and apply a custom font (e.g., "Comic Sans MS")
Style style = workbook.CreateStyle();
style.Font.Name = "Comic Sans MS";   // This font is usually not available on all browsers
style.Font.Size = 14;
style.Font.IsBold = true;

// Apply the style to cell A1
Cell cell = sheet.Cells["A1"];
cell.PutValue("Hello, embedded fonts!");
cell.SetStyle(style);

// Save the workbook as an intermediate .xlsx (optional, just for inspection)
workbook.Save("sample.xlsx");
```

**Proč je to důležité:** Pokud sešit nikdy neodkazuje na vlastní písmo, není pro Aspose.Cells co vložit. Explicitním nastavením `style.Font.Name` vynutíme, aby exportér hledal soubor písma v systému a zahrnul jej do výstupu HTML.

> **Tip:** Vždy testujte s písmem, které není zaručeno, že bude na cílových počítačích přítomno. Systémová písma jako Arial neukážou funkci vkládání.

## Jak vložit písma do HTML – Krok 2: Nakonfigurujte možnosti uložení HTML

Nyní přichází magický řádek, který odpovídá na hlavní otázku: *how to embed fonts in HTML*.

```csharp
// Step 3: Create HtmlSaveOptions and enable font embedding
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // Setting this flag tells Aspose.Cells to embed all referenced fonts as base‑64 data URIs
    EmbedFonts = true,

    // Optional: Reduce file size by embedding only the characters actually used
    EmbedFontSubset = true,

    // Optional: Choose a folder for external resources (images, CSS)
    ExportImagesAsBase64 = true
};
```

- `EmbedFonts = true` provádí těžkou práci; prohledá sešit na všechny odkazy na písma, najde odpovídající soubory `.ttf`/`.otf` a vloží je přímo do vygenerovaného HTML `<style>` bloku.
- `EmbedFontSubset = true` je optimalizace výkonu – do výstupu se zahrnou jen glyfy, které skutečně používáte, což udržuje konečné HTML úzké.
- `ExportImagesAsBase64` je užitečné, když máte také grafy nebo obrázky; vše končí v jednom souboru, což je ideální pro e‑mail nebo rychlé ukázky.

## Jak vložit písma do HTML – Krok 3: Uložte sešit

Nakonec zavoláme `Save` s možnostmi, které jsme právě nakonfigurovali.

```csharp
// Step 4: Export the workbook to HTML with embedded fonts
string outputPath = "embedded.html";
workbook.Save(outputPath, htmlOptions);

Console.WriteLine($"Workbook exported with embedded fonts to: {outputPath}");
```

Po dokončení běhu otevřete `embedded.html` v libovolném moderním prohlížeči. Měli byste vidět text vykreslený ve *Comic Sans MS*, i když písmo není nainstalováno lokálně. Prohlížeč načte `<style>` blok, který obsahuje pravidlo `@font-face` s `data:font/ttf;base64,...` payloadem – přesně to, co jsme chtěli.

![Výstup HTML s vloženými písmy](embed-fonts-html.png "Snímek obrazovky ukazující, jak vložit písma do HTML")

*Text alternativy obrázku:* **how to embed fonts in HTML** – snímek vygenerované stránky s aplikovaným vlastním písmem.

---

## Export Excel do HTML – Alternativní přístupy

Pokud nejste vázáni na Aspose.Cells, existují i jiné způsoby *export excel to html*:

| Knihovna / Nástroj | Podpora vkládání písem | Rychlá poznámka |
|--------------------|------------------------|-----------------|
| **ClosedXML** | Žádná vestavěná podpora vkládání písem | Generuje prostý HTML; musíte ručně přidat `@font-face`. |
| **EPPlus** | Žádné vkládání písem | Vhodné pro datové tabulky, ale ztrácí stylování. |
| **Office Interop** | Může vložit písma pomocí `SaveAs` s `xlHtmlStatic` | Vyžaduje nainstalovaný Excel na serveru – obecně nedoporučeno. |
| **LibreOffice CLI** | Může vložit písma pomocí příznaku `--embed-fonts` | Funguje napříč platformami, ale přidává těžkou závislost. |

Když potřebujete spolehlivé řešení na straně serveru bez nainstalovaného Office, Aspose.Cells zůstává nejjednodušší cestou k *convert excel to html* s vloženými písmy.

## Jak exportovat Excel – Běžné úskalí a jak je opravit

1. **Chybějící soubory písem** – Pokud cílové písmo není na stroji, na kterém kód běží, Aspose.Cells tiše přeskočí vložení a HTML se vrátí k generickému písmu.  
   *Řešení:* Nainstalujte písmo na server nebo zkopírujte soubory `.ttf`/`.otf` vedle spustitelného souboru a nastavte `FontSources` ručně:

   ```csharp
   FontSources.AddFolder(@"C:\MyFonts");
   ```

2. **Licenční omezení** – Některá komerční písma zakazují vkládání.  
   *Řešení:* Zkontrolujte EULA písma. Pokud je vkládání zakázáno, vyberte jiné písmo nebo hostujte soubor písma sami s odpovídající licencí.

3. **Velké sešity** – Vkládání mnoha písem může nafouknout velikost HTML.  
   *Řešení:* Použijte `EmbedFontSubset = true` (jak bylo ukázáno dříve) nebo omezte sešit jen na listy, které potřebujete, před exportem.

4. **Kompatibilita prohlížečů** – Starší prohlížeče (IE 8 a starší) nerozumí base‑64 `@font-face`.  
   *Řešení:* Poskytněte náhradní CSS pravidlo, které odkazuje na webově přístupnou verzi písma `.woff`.

---

## Převod Excel do HTML – Ověření výsledku

Po spuštění ukázky otevřete `embedded.html` a hledejte `<style>` blok, který začíná takto:

```html
<style type="text/css">
@font-face {
    font-family: 'Comic Sans MS';
    src: url('data:font/ttf;base64,AAEAAAALAIAAAwAwT1MvMg8S...') format('truetype');
}
...
</style>
```

Pokud vidíte URL `data:`, vložení bylo úspěšné. Tělo stránky bude obsahovat něco podobného:

```html
<div class="c0">Hello, embedded fonts!</div>
```

---

## Často kladené otázky (FAQ)

**Q: Funguje to s Excelovými vzorci?**  
A: Rozhodně. Vzorce jsou vyhodnoceny před generováním HTML, takže zobrazené hodnoty jsou statické řetězce – stejně jako běžný export.

**Q: Mohu vložit písma při exportu do ZIP balíčku místo jediného HTML souboru?**  
A: Ano. Nastavte `htmlOptions.ExportToSingleFile = false` a Aspose.Cells vytvoří složku s oddělenými CSS a soubory písem, což některé týmy preferují pro správu verzí.

**Q: Co když potřebuji vložit

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}