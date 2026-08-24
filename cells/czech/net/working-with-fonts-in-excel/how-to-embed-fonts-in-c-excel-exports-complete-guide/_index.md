---
category: general
date: 2026-02-15
description: Zjistěte, jak vložit písma při exportu Excelu do SVG a XPS, správně zapisovat
  Unicode znaky a vkládat písma do SVG pomocí Aspose.Cells.
draft: false
keywords:
- how to embed fonts
- export excel to svg
- how to write unicode
- embed fonts in svg
- how to export xps
language: cs
og_description: Jak vložit písma při exportu Excelu do SVG a XPS, zapisovat Unicode
  znaky a vložit písma do SVG pomocí Aspose.Cells.
og_title: Jak vložit písma do exportů Excel v C# – krok po kroku
tags:
- Aspose.Cells
- C#
- Excel Export
- Font Embedding
title: Jak vložit písma do exportů Excel v C# – Kompletní průvodce
url: /cs/net/working-with-fonts-in-excel/how-to-embed-fonts-in-c-excel-exports-complete-guide/
---

to keep all shortcodes exactly.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vložit písma v C# Excel exportech – Kompletní průvodce

Už jste se někdy zamýšleli **jak vložit písma** do Excel exportu, aby výstup vypadal naprosto stejně na každém počítači? Nejste v tom sami. Když pošlete list klientovi, který nemá nainstalované stejné typy písma, dokument může vypadat poškozeně, zejména pokud obsahuje speciální Unicode symboly. V tomto tutoriálu projdeme praktické řešení, které nejen ukazuje **jak vložit písma**, ale také se zabývá **export excel to svg**, **how to write unicode** a **how to export xps** pomocí Aspose.Cells.

Na konci průvodce budete mít připravený C# úryvek, který zapíše Unicode znak s výběrovým selektorem, vloží požadovaná písma a vytvoří jak XPS, tak SVG soubory, které se vykreslí perfektně všude. Žádné externí nástroje, žádné hacky po zpracování – jen čistý, samostatný kód.

## Požadavky

- .NET 6.0 nebo novější (API funguje stejně na .NET Framework 4.8)
- Aspose.Cells for .NET (NuGet package `Aspose.Cells`)
- Složka na disku, kam lze uložit vygenerované soubory
- Základní znalost syntaxe C# (pokud jste úplný začátečník, kód je bohatě okomentován)

Pokud už máte tyto součásti připravené, skvělé – pojďme rovnou k implementaci.

## Krok 1: Nastavení sešitu a listu (How to Embed Fonts – Výchozí bod)

Prvním, co potřebujeme, je čerstvý objekt `Workbook`. Představte si sešit jako kontejner pro všechny listy, styly a zdroje. Vytvořit jej je jednoduché, ale je to základ pro jakoukoli operaci **embed fonts in svg**, protože informace o písmu žijí na úrovni sešitu.

```csharp
using Aspose.Cells;

namespace FontEmbeddingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and grab the first worksheet
            Workbook workbook = new Workbook();               // fresh workbook
            Worksheet ws = workbook.Worksheets[0];            // default sheet
```

> **Proč je to důležité:** Když později exportujete do SVG nebo XPS, Aspose.Cells se dívá na kolekci stylů sešitu, aby rozhodl, která písma vložit. Začátek s čistým sešitem zajišťuje, že žádné cizí odkazy na písma nezkazí výstup.

## Krok 2: Zapsání Unicode znaku s výběrovým selektorem (How to Write Unicode)

Unicode znaky mohou být záludné, zejména když potřebujete konkrétní variantu glifu. Znak `𝟘` (MATHEMATICAL DOUBLE‑STRUCK ZERO) spojený s Variation Selector‑1 (`\uFE00`) nutí vykreslovací engine zvolit „plain“ prezentaci. Toto je dokonalá ukázka **how to write unicode**, protože ukazuje přesný řetězec, který musíte vložit do buňky.

```csharp
            // Step 2: Write the character '𝟘' followed by Variation Selector-1 into cell A1
            // The literal "\uFE00" is the Variation Selector; it tells the font to use the base glyph.
            ws.Cells["A1"].PutValue("𝟘\uFE00");
```

> **Tip:** Pokud v výstupu někdy uvidíte chybějící glif (�), dvakrát zkontrolujte, že cílové písmo skutečně podporuje základní znak *a* výběrový selektor. Ne všechna písma to umí.

## Krok 3: Export listu do XPS (How to Export XPS)

XPS je formát s pevnou rozložením podobný PDF, ale nativní pro Windows. Export do XPS při **embedding fonts** zaručuje, že dokument bude vypadat identicky na jakémkoli Windows počítači, i když písmo není lokálně nainstalováno.

```csharp
            // Step 3: Export the worksheet to XPS – fonts are embedded automatically
            string xpsPath = @"C:\Exports\VarSel.xps";
            ws.Cells.ExportToXps(xpsPath);
```

> **Co uvidíte:** Otevřete vzniklý `VarSel.xps` ve Windows Reader; dvojitě přeškrtnutá nula se zobrazí přesně jako v Excelu, se zachovaným správným stylem.

## Krok 4: Export listu do SVG s vloženými písmy (Embed Fonts in SVG)

SVG je vektorový formát obrázku, který prohlížeče vykreslují za běhu. Ve výchozím nastavení Aspose.Cells odkazuje na písmo podle názvu, což může vést k problémům s chybějícími glify, pokud prohlížeč nemá písmo nainstalováno. Třída `SvgSaveOptions` nám umožňuje **embed fonts in SVG**, čímž se soubor změní na samostatný balíček.

```csharp
            // Step 4: Export to SVG with fonts embedded
            string svgPath = @"C:\Exports\VarSel.svg";
            SvgSaveOptions svgOptions = new SvgSaveOptions
            {
                EmbedFonts = true          // crucial flag – forces font embedding
            };
            ws.Cells.ExportToSvg(svgPath, svgOptions);
```

> **Výsledek:** Otevřete `VarSel.svg` v libovolném moderním prohlížeči (Chrome, Edge, Firefox). Unicode znak se vykreslí správně bez jakýchkoli externích souborů písem. Pokud prozkoumáte zdroj SVG, uvidíte blok `<style>` obsahující Base64‑kódovanou definici písma.

## Kompletní funkční příklad (Všechny kroky dohromady)

Níže je kompletní program, který můžete zkopírovat a vložit do konzolové aplikace. Obsahuje všechny výše uvedené kroky plus závěrečnou zprávu do konzole, abyste věděli, kdy proces skončí.

```csharp
using Aspose.Cells;
using System;

namespace FontEmbeddingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create workbook and worksheet
            Workbook workbook = new Workbook();
            Worksheet ws = workbook.Worksheets[0];

            // Write Unicode character with variation selector
            ws.Cells["A1"].PutValue("𝟘\uFE00");

            // Export to XPS (fonts embedded automatically)
            string xpsPath = @"C:\Exports\VarSel.xps";
            ws.Cells.ExportToXps(xpsPath);
            Console.WriteLine($"XPS exported to: {xpsPath}");

            // Export to SVG with embedded fonts
            string svgPath = @"C:\Exports\VarSel.svg";
            SvgSaveOptions svgOptions = new SvgSaveOptions
            {
                EmbedFonts = true
            };
            ws.Cells.ExportToSvg(svgPath, svgOptions);
            Console.WriteLine($"SVG exported to: {svgPath}");

            Console.WriteLine("All files generated successfully.");
        }
    }
}
```

### Očekávaný výstup

- **`VarSel.xps`** – jednosloupcový XPS dokument zobrazující dvojitě přeškrtnutou nulu ve stejném písmu, jaké používá Excel.
- **`VarSel.svg`** – SVG soubor, který obsahuje vložený proud písma; otevřete jej v prohlížeči a uvidíte stejný glif, bez chybějících znakových polí.

## Časté úskalí & Pro tipy (How to Embed Fonts Effectively)

| Problém | Proč se to děje | Oprava |
|---------|----------------|--------|
| Glif se zobrazuje jako čtvereček v SVG | Písmo nebylo vloženo (`EmbedFonts = false`) | Nastavte `EmbedFonts = true` v `SvgSaveOptions`. |
| Výběrový selektor je ignorován | Písmo nemá variantní glif | Vyberte písmo, které explicitně podporuje výběrový selektor, např. **Cambria Math** nebo **Arial Unicode MS**. |
| Export selže s “Access denied” | Cílová složka je jen pro čtení nebo neexistuje | Ujistěte se, že složka (`C:\Exports\`) existuje a proces má oprávnění k zápisu. |
| Velikost XPS souboru je obrovská | Vkládání velkých souborů písma zbytečně | Použijte lehké písmo (např. **Calibri**), pokud potřebujete jen základní latinské znaky. |

> **Pro tip:** Pokud exportujete mnoho listů, znovu použijte jedinou instanci `SvgSaveOptions`, abyste se vyhnuli vytváření duplicitních proudů písma, což může nafouknout velikost SVG.

## Rozšíření řešení (Co když potřebujete více?)

- **Batch Export:** Procházejte `workbook.Worksheets` a pro každý list zavolejte `ExportToSvg`, přičemž předáte jedinečný název souboru.
- **Custom Font Substitution:** Použijte `Style.Font.Name` k vynucení konkrétního písma před exportem. To je užitečné, když zdrojový sešit používá písmo, které není licenčně přátelské.
- **Higher‑Resolution Images:** Pro rastrové formáty (PNG, JPEG) můžete nastavit `Resolution` v `ImageOrPrintOptions` – není to potřeba pro SVG, ale je dobré vědět, pokud se později rozhodnete generovat PNG náhledy.

## Závěr

Probrali jsme **how to embed fonts** v exportech do XPS i SVG, ukázali **how to write unicode** znaky s výběrovými selektory a ukázali vám, jak **export excel to svg** při zachování písem uvnitř souboru. Dodržením výše uvedených kroků odstraníte otrávený problém „chybějící písmo“ a zajistíte, že kdokoli – bez ohledu na nainstalovaná písma – uvidí přesně to, co jste zamýšleli.

Jste připraveni na další výzvu? Zkuste vložit vlastní TrueType písmo, které není nainstalováno na serveru, nebo experimentujte s exportem do PDF při zachování vložených písem. Oba přístupy staví na stejných principech, které jsme zde prozkoumali.

Šťastné programování a ať vaše exportované dokumenty vždy vypadají pixel‑perfektně!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}