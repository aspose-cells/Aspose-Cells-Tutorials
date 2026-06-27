---
category: general
date: 2026-06-27
description: Rychle vložte písma do HTML. Naučte se, jak převést DOCX na HTML, jak
  vložit všechna písma a exportovat dokument Word do HTML pomocí jednoduchého příkladu
  v C#.
draft: false
keywords:
- embed fonts in html
- convert docx to html
- how to embed all fonts
- export word document to html
- how to convert docx to html
language: cs
og_description: Vložte písma do HTML pomocí stručného tutoriálu v C#. Naučte se, jak
  převést DOCX na HTML, vložit všechna písma a snadno exportovat Word dokumenty do
  HTML.
og_title: Vložení fontů do HTML – Krok za krokem převod DOCX na HTML
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Embed fonts in HTML quickly. Learn how to convert DOCX to HTML, how
    to embed all fonts, and export Word document to HTML with a simple C# example.
  headline: Embed Fonts in HTML – Complete Guide to Converting DOCX to HTML with Full
    Font Support
  type: TechArticle
- description: Embed fonts in HTML quickly. Learn how to convert DOCX to HTML, how
    to embed all fonts, and export Word document to HTML with a simple C# example.
  name: Embed Fonts in HTML – Complete Guide to Converting DOCX to HTML with Full
    Font Support
  steps:
  - name: 1. Large Documents → Large HTML Files
    text: 'Embedding every font as Base64 can balloon the HTML size, especially with
      multiple heavyweight fonts. If file size is a concern, consider:'
  - name: 2. Font Licensing Restrictions
    text: Some commercial fonts forbid embedding. Aspose.Words respects the font’s
      licensing metadata. If a font can’t be embedded, the exporter will fall back
      to a system font and emit a warning in the console. Always verify your font
      licenses before distribution.
  - name: 3. Missing Glyphs
    text: If the DOCX contains characters from a language not covered by the embedded
      fonts (e.g., Chinese characters in a Latin‑only font), the browser will substitute
      a fallback. To avoid this, ensure the source font supports all required Unicode
      ranges, or embed an additional fallback font.
  - name: 4. Browser Compatibility
    text: All major browsers support Base64‑encoded fonts, but very old versions of
      Internet Explorer (pre‑IE 9) may have issues. If you need legacy support, generate
      external `.woff` files instead of Base64 and reference them via `<link>` tags.
  type: HowTo
- questions:
  - answer: Yes. Set `saveOptions.FontSubset = FontSubset.None` and manually add the
      fonts you need via `FontInfoCollection`. This gives you fine‑grained control
      but adds a few extra lines of code.
    question: Can I embed only specific fonts instead of every font?
  - answer: Absolutely. Aspose.Words can load `.doc` files the same way; just point
      `new Document("file.doc")` at your legacy file.
    question: Does this work with DOC files (older Word format)?
  - answer: 'You can write the HTML to a `MemoryStream` instead of a file: ```csharp
      using (MemoryStream htmlStream = new MemoryStream()) { doc.Save(htmlStream,
      saveOptions); string htmlContent = Encoding.UTF8.GetString(htmlStream.ToArray());
      // Return htmlContent from your API } ``` --- ## Conclusion We’ve cove'
    question: What if I need to generate HTML for a web service?
  type: FAQPage
tags:
- Aspose.Words
- C#
- HTML export
title: Vkládání fontů do HTML – Kompletní průvodce převodem DOCX do HTML s plnou podporou
  fontů
url: /cs/net/conversion-and-rendering/embed-fonts-in-html-complete-guide-to-converting-docx-to-htm/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vkládání fontů do HTML – Kompletní průvodce konverzí DOCX do HTML s plnou podporou fontů

Už jste se někdy zamýšleli, jak vložit fonty do HTML při převodu dokumentu Word? Nejste v tom sami. Mnoho vývojářů narazí na problém, kdy exportované HTML vypadá na jejich počítači dobře, ale na jiném selže, protože chybí fonty. Dobrá zpráva? Vkládání fontů do HTML je hračka, jakmile znáte správné možnosti.

V tomto tutoriálu si projdeme **jak převést DOCX do HTML** pomocí Aspose.Words pro .NET, ukážeme **jak vložit všechny fonty** a nakonec **exportovat Word dokument do HTML** se všemi glyfy zachovanými. Na konci budete mít jediný spustitelný úryvek, který můžete vložit do libovolného C# projektu.

## Požadavky

Než se pustíme do práce, ujistěte se, že máte:

- .NET 6.0 nebo novější (kód funguje také na .NET Framework 4.6+)
- Platnou licenci Aspose.Words pro .NET (nebo dočasný evaluační klíč)
- DOCX soubor, který chcete převést (budeme ho nazývat `input.docx`)
- Visual Studio 2022 nebo libovolné IDE, které preferujete

To je vše — žádné další balíčky, žádné složité příkazy v terminálu. Připravení? Pojďme na to.

---

## Krok 1: Načtení zdrojového dokumentu

Prvním, co potřebujete, je objekt `Document`, který představuje váš Word soubor. Představte si to jako načtení plátna před tím, než začnete malovat.

```csharp
using Aspose.Words;
using Aspose.Words.Saving;

// Step 1: Load the source document
Document doc = new Document("YOUR_DIRECTORY/input.docx");
```

> **Proč je to důležité:** Načtení dokumentu poskytuje Aspose.Words přístup k podkladovým informacím o fontu. Pokud DOCX odkazuje na vlastní fonty, jsou nyní součástí objektu `Document` a mohou být později zabaleny do HTML.

## Krok 2: Vytvoření HTML Save Options a povolení vkládání fontů

Nyní přichází magický řádek, který odpovídá na otázku **jak vložit všechny fonty**. Třída `HtmlSaveOptions` vám umožní doladit chování exportu a příznak `EmbedAllFonts` dělá přesně to, co napovídá jeho název — zabaluje každý font použitý v DOCX do výsledného HTML souboru.

```csharp
// Step 2: Create HTML save options and enable embedding all fonts
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // Embeds every font used in the document into the HTML as base‑64 data URIs
    EmbedAllFonts = true,

    // Optional: control the output folder for external resources (images, CSS)
    ExportImagesAsBase64 = true,

    // Optional: keep the original CSS class names for easier styling later
    CssStyleSheetType = CssStyleSheetType.Inline
};
```

> **Tip:** Nastavením `ExportImagesAsBase64` na `true` zajistíte, že HTML bude skutečně samostatné — žádné samostatné soubory s obrázky k odeslání. Pokud dáváte přednost externím obrázkům, nastavte ho na `false` a určete `ResourcesFolder`.

## Krok 3: Uložení dokumentu jako HTML s vloženými fonty

Nakonec zapíšeme HTML soubor na disk. Metoda `Save` respektuje právě nastavené možnosti a vytvoří soubor `.html`, který obsahuje *všechny* fonty zakódované jako pravidla `@font-face`.

```csharp
// Step 3: Save the document as HTML with embedded fonts
doc.Save("YOUR_DIRECTORY/embedded.html", saveOptions);
```

To je celý pracovní postup. Když otevřete `embedded.html` v libovolném moderním prohlížeči, uvidíte původní rozložení Wordu, včetně přesně stejné typografie — žádné chybějící znaky, žádné náhradní fonty.

## Očekávaný výstup a ověření

Otevřete vygenerovaný `embedded.html` v Chrome, Edge nebo Firefoxu. Měli byste vidět:

- Text vykreslený ve stejném typu písma jako v originálním DOCX (např. *Calibri*, *Cambria* nebo jakýkoli vlastní font, který jste zabalení)
- Žádné externí soubory `.ttf` nebo `.woff` v adresáři — fonty jsou vloženy jako Base64 řetězce uvnitř `<style>` tagů
- Obrázky zobrazené správně, pokud jste ponechali `ExportImagesAsBase64 = true`

Pokud si prohlédnete zdrojový kód stránky, hledejte blok jako tento:

```html
<style type="text/css">
@font-face {
    font-family: 'MyCustomFont';
    src: url('data:font/ttf;base64,AAEAAAARAQAABAA...') format('truetype');
}
...
</style>
```

Vidět `data:font/ttf;base64` payload potvrzuje, že **vložení fontů do HTML** bylo úspěšné.

## Časté problémy a okrajové případy

### 1. Velké dokumenty → velké HTML soubory
Vložení každého fontu jako Base64 může výrazně zvětšit velikost HTML, zejména při více těžkých fontech. Pokud je velikost souboru problém, zvažte:

- Použití `EmbedSystemFonts = false` k vynechání běžných systémových fontů, které prohlížeče už mají.
- Rozdělení dokumentu na sekce a export každé zvlášť.

### 2. Omezení licencí fontů
Některé komerční fonty zakazují vkládání. Aspose.Words respektuje licenční metadata fontu. Pokud font nelze vložit, exportér přejde na systémový font a vypíše varování do konzole. Vždy si před distribucí ověřte licence vašich fontů.

### 3. Chybějící glyfy
Pokud DOCX obsahuje znaky z jazyka, který není pokryt vloženými fonty (např. čínské znaky v latinském fontu), prohlížeč použije náhradní font. Aby se tomu předešlo, ujistěte se, že zdrojový font podporuje všechny požadované Unicode rozsahy, nebo vložte další náhradní font.

### 4. Kompatibilita prohlížečů
Všechny hlavní prohlížeče podporují Base64‑zakódované fonty, ale velmi staré verze Internet Explorer (před IE 9) mohou mít problémy. Pokud potřebujete podporu starších verzí, generujte externí soubory `.woff` místo Base64 a odkazujte na ně pomocí `<link>` tagů.

## Pokročilá přizpůsobení (volitelné)

#### Export do samostatného CSS souboru
Pokud dáváte přednost čistšímu HTML souboru, nastavte `CssStyleSheetType = CssStyleSheetType.External` a určete `CssStyleSheetFileName`. Vygenerovaný `.css` bude obsahovat pravidla `@font-face`, zatímco HTML na něj odkazuje.

```csharp
saveOptions.CssStyleSheetType = CssStyleSheetType.External;
saveOptions.CssStyleSheetFileName = "styles.css";
```

#### Řízení formátů fontů
Můžete omezit formáty vložených fontů (např. jen `woff2`) úpravou vlastnosti `FontFormat`:

```csharp
saveOptions.FontFormat = FontFormat.Woff2;
```

Tím se sníží velikost, přičemž stále pokrýváte většinu moderních prohlížečů.

## Kompletní funkční příklad

Níže je kompletní program, který můžete zkopírovat a vložit do konzolové aplikace. Obsahuje ošetření chyb a komentáře pro přehlednost.

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Saving;

namespace DocxToHtmlWithFonts
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths to your environment
            string inputPath = @"YOUR_DIRECTORY\input.docx";
            string outputPath = @"YOUR_DIRECTORY\embedded.html";

            try
            {
                // Load the DOCX file
                Document doc = new Document(inputPath);

                // Configure HTML export options
                HtmlSaveOptions saveOptions = new HtmlSaveOptions
                {
                    EmbedAllFonts = true,               // <-- key to embed fonts in html
                    ExportImagesAsBase64 = true,        // keep everything in one file
                    CssStyleSheetType = CssStyleSheetType.Inline,
                    // Optional: reduce font payload size
                    // FontFormat = FontFormat.Woff2
                };

                // Save as HTML
                doc.Save(outputPath, saveOptions);

                Console.WriteLine($"Successfully exported '{inputPath}' to HTML with embedded fonts.");
                Console.WriteLine($"Open '{outputPath}' in a browser to verify the result.");
            }
            catch (Exception ex)
            {
                Console.WriteLine("An error occurred during conversion:");
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

Spusťte program, otevřete vygenerovaný `embedded.html` a uvidíte zachovanou původní Word stylizaci — přesně to, co jste chtěli, když jste se ptali na **jak vložit všechny fonty**.

## Často kladené otázky

**Q: Můžu vložit jen konkrétní fonty místo všech fontů?**  
A: Ano. Nastavte `saveOptions.FontSubset = FontSubset.None` a ručně přidejte potřebné fonty pomocí `FontInfoCollection`. Tím získáte jemnou kontrolu, ale přidáte několik dalších řádků kódu.

**Q: Funguje to i s DOC soubory (starší formát Wordu)?**  
A: Rozhodně. Aspose.Words dokáže načíst soubory `.doc` stejným způsobem; stačí použít `new Document("file.doc")` na váš starší soubor.

**Q: Co když potřebuji generovat HTML pro webovou službu?**  
A: Můžete zapisovat HTML do `MemoryStream` místo souboru:

```csharp
using (MemoryStream htmlStream = new MemoryStream())
{
    doc.Save(htmlStream, saveOptions);
    string htmlContent = Encoding.UTF8.GetString(htmlStream.ToArray());
    // Return htmlContent from your API
}
```

## Závěr

Probrali jsme vše, co potřebujete k **vložení fontů do HTML** při **konverzi DOCX do HTML** pomocí Aspose.Words pro .NET. Načtením zdrojového dokumentu, povolením `EmbedAllFonts` a uložením s `HtmlSaveOptions` získáte samostatný HTML soubor, který vypadá přesně jako originální Word soubor — žádné chybějící glyfy, žádné extra assety.

Nyní můžete:

- Nasadit HTML na libovolný statický web
- Poslat ho e‑mailem bez obav o dostupnost fontů
- Integrovat převod do automatizovaných pipeline (CI/CD, dávkové zpracování atd.)

Pokud vás zajímají další kroky, podívejte se na **jak převést DOCX do HTML** s vlastními CSS tématy, nebo experimentujte s **exportem Word dokumentu do HTML** při zachování tabulek a složitých rozvržení. Možnosti jsou neomezené a jádro techniky — vkládání všech fontů — zůstává stejné.

Šťastné kódování a ať se vám HTML vždy vykresluje s dokonalou typografií!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Jak nakonfigurovat nastavení HTML Cross-Type v Aspose.Cells .NET pro konverzi Excelu do HTML](/cells/english/net/workbook-operations/configure-html-cross-type-aspose-cells-net/)
- [Jak řídit komentáře při exportu HTML v .NET pomocí Aspose.Cells](/cells/english/net/comments-annotations/net-html-export-comment-control-aspose-cells/)
- [Jak implementovat vlastní Stream Provider pro export HTML v Aspose.Cells .NET](/cells/english/net/import-export/custom-stream-provider-html-export-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}