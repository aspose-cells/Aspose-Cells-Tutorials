---
category: general
date: 2026-05-23
description: Vkládejte písma do HTML při exportu Excelu do HTML pomocí Aspose.Cells.
  Krok za krokem průvodce převodem tabulky do HTML s vloženými písmy.
draft: false
keywords:
- embed fonts in html
- export excel to html
- convert spreadsheet to html
- save workbook as html
- how to embed fonts html
language: cs
og_description: Vkládejte písma do HTML při exportu Excelu do HTML. Naučte se, jak
  převést tabulku do HTML s vloženými písmy během několika jednoduchých kroků.
og_title: Vložit písma do HTML – Export Excelu do HTML pomocí C#
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Embed fonts in HTML when you export Excel to HTML using Aspose.Cells.
    Step‑by‑step guide to convert spreadsheet to HTML with embedded fonts.
  headline: Embed fonts in HTML – Export Excel to HTML with C#
  type: TechArticle
- description: Embed fonts in HTML when you export Excel to HTML using Aspose.Cells.
    Step‑by‑step guide to convert spreadsheet to HTML with embedded fonts.
  name: Embed fonts in HTML – Export Excel to HTML with C#
  steps:
  - name: 1️⃣ **What if my workbook uses a custom font that isn’t installed on the
      server?**
    text: Aspose.Cells can only embed fonts that are available to the runtime. Install
      the `.ttf` or `.otf` file on the machine running the conversion, or copy it
      into the project directory and register it via `System.Drawing.Text.PrivateFontCollection`
      before invoking the save operation.
  - name: 2️⃣ **Will embedding increase the file size dramatically?**
    text: Yes, each embedded font is Base64‑encoded, which adds roughly 33 % overhead.
      If the workbook uses many large fonts, consider enabling `EmbedOnlyUsedFonts
      = true` to limit the payload to fonts actually referenced in the sheet.
  - name: 3️⃣ **Can I still export images separately?**
    text: Setting `ExportImagesAsBase64 = true` (as shown above) inlines images, making
      the HTML truly self‑contained. If you prefer external image files, set this
      property to `false` and specify `ExportImagesFolder` to control the output folder.
  - name: 4️⃣ **Is this approach compatible with older browsers?**
    text: Most modern browsers (Chrome, Edge, Firefox, Safari) support Base64‑encoded
      `@font-face`. Internet Explorer 11 also works, but you might need to ensure
      the MIME type is correct. For legacy support, consider providing a fallback
      font stack in your CSS.
  - name: 5️⃣ **How does this differ from a simple “export excel to html” without
      embedding?**
    text: A plain export writes the text using generic web fonts (`Arial`, `Helvetica`,
      etc.). The visual layout may shift, especially for corporate reports that rely
      on a brand‑specific typeface. Embedding removes that uncertainty.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Vložit písma do HTML – Exportovat Excel do HTML pomocí C#
url: /cs/net/exporting-excel-to-html-with-advanced-options/embed-fonts-in-html-export-excel-to-html-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vkládání fontů do HTML – Export Excel do HTML pomocí C#

Už jste se někdy zamýšleli, jak **vložit fonty do HTML** při exportu sešitu Excel? Nejste v tom jediní. Když sdílíte tabulku jako webovou stránku, chybějící fonty mohou proměnit upravenou zprávu v nečitelný chaos – zejména pokud prohlížeč nemá nainstalovaný původní typ písma.  

V tomto tutoriálu vás provedeme kompletním, připraveným řešením, které vám přesně ukáže **jak vložit fonty do HTML** pomocí Aspose.Cells pro .NET. Na konci budete schopni **exportovat Excel do HTML**, **převést tabulku do HTML** a **uložit sešit jako HTML** s fonty zabudovanými přímo v souboru.

---

## Co se naučíte

- Proč jsou vložené fonty důležité pro webové exporty Excelu.  
- Jak nakonfigurovat `HtmlSaveOptions` pro zapnutí příznaku `EmbedFonts`.  
- Úplný C# program, který načte sešit, použije nastavení a zapíše HTML soubor.  
- Tipy pro práci s vlastními fonty, kompatibilitu verzí a řešení běžných problémů.  

Předchozí zkušenost s Aspose.Cells není vyžadována, ale měli byste mít základní znalosti C# a vývoje v .NET.

## Požadavky

| Požadavek | Proč je důležité |
|-------------|----------------|
| **.NET 6.0 nebo novější** | Moderní runtime; starší frameworky mohou postrádat nejnovější funkce Aspose.Cells. |
| **Aspose.Cells pro .NET** (NuGet balíček `Aspose.Cells`) | Poskytuje třídu `HtmlSaveOptions`, kterou potřebujeme. |
| **TrueType nebo OpenType font** který chcete vložit (např. `Arial.ttf`) | Pouze tyto formáty fontů lze vložit do HTML souboru. |
| **IDE** (Visual Studio, Rider, VS Code) | Umožňuje snadné spuštění a ladění ukázky. |

Pokud jste ještě nenainstalovali NuGet balíček, spusťte:

```bash
dotnet add package Aspose.Cells
```

## Krok 1: Načtěte sešit, který chcete převést

Nejprve potřebujeme instanci `Workbook`. Můžete načíst existující soubor `.xlsx`, vytvořit nový od nuly nebo dokonce načíst data z databáze. Zde je minimální příklad, který otevře soubor `Sample.xlsx` ze složky projektu:

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source Excel file
        var workbook = new Workbook("Sample.xlsx");
        // Continue with HTML conversion...
```

> **Proč tento krok?**  
> `Workbook` objekt je vstupním bodem pro všechny operace Aspose.Cells. Bez něj nemůžete přistupovat k listům, stylům ani datům, která se nakonec převedou do HTML.

## Krok 2: Nakonfigurujte HTML možnosti uložení pro **vložení fontů do HTML**

Nyní přichází magický řádek, který odpovídá na otázku „jak vložit fonty do html“. Vytvoříme instanci `HtmlSaveOptions` a nastavíme `EmbedFonts` na `true`. Tím řekneme knihovně, aby vložila data fontu jako Base64‑kódovaná CSS pravidla `@font-face`.

```csharp
        // Step 2: Set up HTML save options with embedded fonts
        var htmlOptions = new HtmlSaveOptions
        {
            // This flag ensures fonts are written directly into the HTML file
            EmbedFonts = true,

            // Optional: you can control whether to embed only used fonts
            // EmbedOnlyUsedFonts = true,

            // Optional: control the output folder for external resources
            ExportImagesAsBase64 = true
        };
```

> **Proč povolit `EmbedFonts`?**  
> Když je výsledné HTML otevřeno na počítači, který nemá původní font, prohlížeč přejde na generické písmo. Vložení zaručuje vizuální věrnost napříč všemi platformami.

## Krok 3: Uložte sešit jako HTML

S připravenými možnostmi zavoláme `Workbook.Save`, předáme požadovaný název souboru a objekt `HtmlSaveOptions`. Knihovna provede těžkou práci – převod buněk, vzorců a stylů do HTML značek a následné vložení dat fontu do `<style>` tagů.

```csharp
        // Step 3: Export the workbook to HTML with embedded fonts
        workbook.Save("output.html", htmlOptions);

        // Inform the user
        Console.WriteLine("Workbook successfully saved as HTML with embedded fonts.");
    }
}
```

> **Co uvidíte:**  
> Otevřete `output.html` v libovolném moderním prohlížeči a všimnete si stejné typografie jako v původním souboru Excel, i když uživatel nemá font nainstalovaný lokálně.

## Kompletní funkční příklad

Spojením všech částí získáte kompletní program, který můžete zkopírovat a vložit do konzolového projektu:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook
        var workbook = new Workbook("Sample.xlsx");

        // 2️⃣ Configure HTML save options to embed fonts
        var htmlOptions = new HtmlSaveOptions
        {
            EmbedFonts = true,
            ExportImagesAsBase64 = true,
            // You can also set ExportActiveWorksheetOnly = true if you only need one sheet
        };

        // 3️⃣ Save the workbook as HTML
        workbook.Save("output.html", htmlOptions);

        Console.WriteLine("✅ Workbook saved as HTML with embedded fonts.");
    }
}
```

Spusťte program (`dotnet run`) a poté otevřete `output.html`. Měli byste vidět věrnou repliku původní tabulky, včetně přesně použitých fontů.

![Příklad výstupu HTML s vloženými fonty](embed-fonts-html.png "Snímek obrazovky zobrazující HTML soubor s vloženými fonty")

*Text obrázku: vložení fontů do html – snímek vygenerované HTML stránky zachovávající původní fonty tabulky.*

## Časté otázky a okrajové případy

### 1️⃣ **Co když můj sešit používá vlastní font, který není nainstalován na serveru?**  
Aspose.Cells může vložit pouze fonty, které jsou dostupné během běhu. Nainstalujte soubor `.ttf` nebo `.otf` na stroj, který provádí konverzi, nebo jej zkopírujte do adresáře projektu a zaregistrujte pomocí `System.Drawing.Text.PrivateFontCollection` před voláním operace uložení.

### 2️⃣ **Zvýší vložení velikost souboru výrazně?**  
Ano, každý vložený font je Base64‑kódovaný, což přidává přibližně 33 % režii. Pokud sešit používá mnoho velkých fontů, zvažte povolení `EmbedOnlyUsedFonts = true`, aby se omezeno množství na fonty skutečně použité v listu.

### 3️⃣ **Mohu stále exportovat obrázky samostatně?**  
Nastavení `ExportImagesAsBase64 = true` (jak je ukázáno výše) vloží obrázky do HTML, čímž se stane skutečně samostatným souborem. Pokud dáváte přednost externím souborům obrázků, nastavte tuto vlastnost na `false` a určete `ExportImagesFolder` pro kontrolu výstupní složky.

### 4️⃣ **Je tento přístup kompatibilní se staršími prohlížeči?**  
Většina moderních prohlížečů (Chrome, Edge, Firefox, Safari) podporuje Base64‑kódované `@font-face`. Internet Explorer 11 také funguje, ale může být nutné zajistit správný MIME typ. Pro starší podporu zvažte poskytnutí záložního fontového zásobníku ve vašem CSS.

### 5️⃣ **Jak se to liší od jednoduchého „exportu Excel do HTML“ bez vložení?**  
Jednoduchý export zapisuje text pomocí generických webových fontů (`Arial`, `Helvetica` atd.). Vizuální rozvržení se může posunout, zejména u firemních zpráv, které spoléhají na specifické firemní písmo. Vložení tuto nejistotu odstraňuje.

## Profesionální tipy a osvědčené postupy

- **Ukládejte HTML do cache**, pokud opakovaně generujete stejnou zprávu. Proces konverze, ač rychlý, stále spotřebovává CPU cykly.
- **Ověřte výstup** pomocí HTML validátoru (např. W3C validator), abyste zachytili případné chyby značkování, které by mohly rozbít e‑mailové klienty.
- **Kombinujte s minifikací CSS**, pokud plánujete poskytovat HTML přes web. Vložená data fontu jsou již komprimována, ale okolní CSS lze zkrátit.
- **Dávejte pozor na licencování**: Aspose.Cells vyžaduje platnou licenci pro produkční použití; jinak se v HTML výstupu objeví vodoznak.
- **Testujte na více zařízeních** – zejména na mobilních prohlížečích – aby vložené fonty byly správně vykresleny na různých hustotách obrazovky.

## Závěr

Nyní máte kompletní řešení připravené ke zkopírování pro **vložení fontů do HTML**, když **exportujete Excel do HTML**, **převádíte tabulku do HTML**, nebo jednoduše **ukládáte sešit jako HTML** s plnou typografickou věrností. Přepnutím příznaku `EmbedFonts` v `HtmlSaveOptions` odstraníte problém „chybějícího fontu“ a poskytnete vyladěnou, samostatnou webovou stránku jakémukoli publiku.

Jste připraveni na další výzvu? Zkuste přidat **interaktivní grafy** do HTML exportu, nebo experimentujte s **konverzí do PDF**, abyste viděli, jak se vložené fonty chovají v jiném formátu. Stejný vzor `HtmlSaveOptions` platí – stačí změnit typ výstupu.

Šťastné programování a ať vaše tabulky vždy vypadají přesně tak, jak jste zamýšleli – bez ohledu na to, kde jsou zobrazeny!

## Související tutoriály

- [Převod Excel do HTML v Javě pomocí Aspose.Cells: Průvodce krok za krokem](/cells/english/java/workbook-operations/convert-excel-html-aspose-cells-java/)
- [Export Excel do HTML pomocí Aspose.Cells Java: Průvodce krok za krokem](/cells/english/java/workbook-operations/export-excel-html-aspose-cells-java/)
- [Převod Excel do HTML s tooltipy pomocí Aspose.Cells Java: Komplexní průvodce](/cells/english/java/workbook-operations/excel-to-html-conversion-with-tooltips-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}