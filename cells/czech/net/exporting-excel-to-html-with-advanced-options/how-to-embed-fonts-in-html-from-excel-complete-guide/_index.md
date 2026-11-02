---
category: general
date: 2026-03-25
description: Naučte se, jak vložit písma do HTML při exportu Excelu do HTML. Tento
  průvodce krok za krokem vám ukáže, jak vložit písma do HTML a uložit sešit jako
  HTML.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- export excel to html
- how to export excel
- save workbook as html
language: cs
og_description: Jak vložit písma do HTML při exportu Excelu? Postupujte podle tohoto
  návodu, jak vložit písma do HTML, exportovat Excel do HTML a uložit sešit jako HTML
  pomocí Aspose.Cells.
og_title: Jak vložit písma do HTML z Excelu – kompletní průvodce
tags:
- Aspose.Cells
- C#
- HTML export
- Font embedding
title: Jak vložit písma do HTML z Excelu – kompletní průvodce
url: /cs/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-from-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vložit písma do HTML z Excelu – Kompletní průvodce

Už jste se někdy zamýšleli **jak vložit písma** do HTML souboru vygenerovaného z Excel sešitu? Nejste v tom sami. Mnoho vývojářů narazí na problém, kdy exportované HTML vypadá na jejich počítači dobře, ale na jiném zařízení ztratí původní typografii. Dobrá zpráva? Řešení je poměrně jednoduché s Aspose.Cells a můžete mít písma přímo zabudovaná v HTML výstupu.

V tomto tutoriálu projdeme přesně kroky k **vložením písem do html**, ukážeme vám, jak **exportovat Excel do html**, a nakonec demonstrujeme, jak **uložit sešit jako html** se všemi potřebnými nastaveními. Na konci budete mít připravený HTML soubor, který se vykreslí přesně jako váš zdrojový tabulkový list—žádné chybějící glyfy, žádná náhradní písma.

## Požadavky

- .NET 6.0 nebo novější (kód funguje také s .NET Framework)
- Aspose.Cells pro .NET (bezplatná zkušební verze nebo licencovaná verze)
- Ukázkový Excel soubor (`sample.xlsx`), který používá alespoň jedno vlastní písmo
- Visual Studio 2022 nebo jakýkoli C# editor, který preferujete

Žádné další NuGet balíčky nejsou potřeba kromě Aspose.Cells.

## Krok 1: Nastavení projektu a načtení sešitu

Nejprve—vytvořte novou konzolovou aplikaci a přidejte odkaz na Aspose.Cells.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToHtmlWithFonts
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load an existing Excel workbook
            string excelPath = @"C:\Temp\sample.xlsx";
            Workbook workbook = new Workbook(excelPath);
            
            // We'll configure the export options in the next step
        }
    }
}
```

**Proč je to důležité:** Načtení sešitu je základem. Pokud sešit není načten správně, žádné z pozdějších nastavení pro vkládání písem nebude mít žádný efekt. Také si všimněte, že Aspose.Cells automaticky čte informace o písmu uložené v souboru, takže není nutné ručně zadávat názvy písem.

## Krok 2: Vytvoření HtmlSaveOptions a povolení vkládání písem

Nyní vytvoříme instanci `HtmlSaveOptions` a zapneme příznak `EmbedAllFonts`. Tím řekneme Aspose.Cells, aby vložilo každé písmo, na které se sešit odkazuje, přímo do vygenerovaného HTML.

```csharp
// Step 2: Create HTML save options
HtmlSaveOptions htmlSaveOptions = new HtmlSaveOptions();

// Enable embedding of all fonts in the output HTML
htmlSaveOptions.EmbedAllFonts = true;

// Optional: Reduce the size of the generated HTML by using base64 encoding
htmlSaveOptions.ExportEmbeddedImages = true;
```

**Proč povolujeme `EmbedAllFonts`:** Když exportujete Excel do HTML bez tohoto příznaku, HTML odkazuje na písma podle názvu. Pokud systém uživatele nemá tato písma nainstalována, prohlížeč přejde na obecnou rodinu, což rozbije rozvržení. Vkládání zaručuje, že přesné glyfy budou součástí HTML souboru.

**Tip:** Pokud potřebujete jen podmnožinu písem (např. víte, že sešit používá jen *Calibri* a *Arial*), můžete nastavit `htmlSaveOptions.FontsList` na vlastní kolekci. To může výrazně zmenšit konečnou velikost souboru.

## Krok 3: Uložení sešitu jako HTML s vloženými písmy

Nakonec zavolejte `Save` na objektu `Workbook`, předáte cestu a možnosti, které jsme právě nakonfigurovali.

```csharp
// Step 3: Save the workbook as an HTML file with embedded fonts
string htmlPath = @"C:\Temp\embedded.html";
workbook.Save(htmlPath, htmlSaveOptions);

Console.WriteLine($"HTML file with embedded fonts saved to: {htmlPath}");
```

A to je vše—váš `embedded.html` nyní obsahuje bloky `<style>` s definicemi `@font-face` a data písem zakódovaná v base64. Otevřete jej v libovolném moderním prohlížeči a měli byste vidět přesně stejnou typografii jako v `sample.xlsx`.

### Očekávaný výsledek

Když otevřete `embedded.html`:

- Vlastní písmo se zobrazí přesně tak, jak je v Excelu.
- Nejsou požadovány žádné externí soubory písem (zkontrolujte záložku Network v dev tools—nemělo by se nic načítat).
- Velikost stránky může být větší než u čistého HTML exportu, ale vizuální věrnost je naprosto přesná.

## Export Excel do HTML – Kompletní příklad

Spojením všeho dohromady, zde je kompletní, spustitelný program:

```csharp
using System;
using Aspose.Cells;

namespace ExcelToHtmlWithFonts
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string excelPath = @"C:\Temp\sample.xlsx";
            Workbook workbook = new Workbook(excelPath);
            
            // 2️⃣ Configure HTML export options
            HtmlSaveOptions htmlOptions = new HtmlSaveOptions
            {
                EmbedAllFonts = true,          // ✅ Embed every used font
                ExportEmbeddedImages = true,   // ✅ Include images as base64
                ExportChartImageFormat = ImageFormat.Png,
                ExportImagesAsBase64 = true    // ✅ Keep everything in one file
            };
            
            // 3️⃣ Save as HTML
            string htmlPath = @"C:\Temp\embedded.html";
            workbook.Save(htmlPath, htmlOptions);
            
            Console.WriteLine($"✅ HTML with embedded fonts saved at: {htmlPath}");
        }
    }
}
```

**Proč to funguje:** Objekt `HtmlSaveOptions` je výkonný kontejner. Přepnutím `EmbedAllFonts` řeknete Aspose.Cells, aby prohledal kolekci stylů sešitu, načetl soubory písem z OS a vložil je. Příznaky `ExportEmbeddedImages` a `ExportImagesAsBase64` udržují HTML samostatné, což je užitečné, když potřebujete soubor poslat e-mailem nebo uložit do databáze.

## Časté úskalí při vkládání písem do HTML

I když máte správný kód, několik drobných problémů vás může zaskočit. Pojďme je řešit dříve, než se stanou bolestí hlavy.

| Issue | Why it Happens | How to Fix |
|-------|----------------|------------|
| **Missing font on the server** | The server where the code runs may not have the custom font installed. | Install the required fonts on the server or copy the `.ttf/.otf` files to a known folder and set `htmlSaveOptions.FontsLocation` to that path. |
| **Chybějící písmo na serveru** | Server, na kterém kód běží, možná nemá nainstalováno vlastní písmo. | Nainstalujte požadovaná písma na server nebo zkopírujte soubory `.ttf/.otf` do známé složky a nastavte `htmlSaveOptions.FontsLocation` na tuto cestu. |
| **Large HTML file** | Embedding many heavy fonts can bloat the HTML (sometimes >5 MB). | Use `htmlSaveOptions.FontsList` to embed only the necessary fonts, or consider sub‑setting the fonts with a tool like FontForge before embedding. |
| **Velký HTML soubor** | Vkládání mnoha těžkých písem může HTML nafouknout (někdy >5 MB). | Použijte `htmlSaveOptions.FontsList` k vložení jen potřebných písem, nebo zvažte podmnožení písem pomocí nástroje jako FontForge před vložením. |
| **Licensing restrictions** | Some commercial fonts forbid embedding. | Verify the font’s EULA. If embedding is disallowed, fall back to a web‑safe alternative or convert the sheet to PDF instead. |
| **Licenční omezení** | Některá komerční písma zakazují vkládání. | Ověřte EULA písma. Pokud je vkládání zakázáno, použijte web‑safe alternativu nebo místo toho převěďte list do PDF. |
| **Browser compatibility** | Very old browsers (IE 8) may ignore `@font-face` with base64 data. | Provide a fallback CSS rule or serve a separate CSS file for legacy browsers. |
| **Kompatibilita prohlížečů** | Velmi staré prohlížeče (IE 8) mohou ignorovat `@font-face` s base64 daty. | Poskytněte náhradní CSS pravidlo nebo servírujte samostatný CSS soubor pro starší prohlížeče. |
| **Incorrect Unicode range** | The embedded font may not contain all characters used (e.g., Asian glyphs). | Ensure the source font supports the required Unicode blocks, or embed a secondary font that covers the missing range. |
| **Nesprávný Unicode rozsah** | Vložené písmo nemusí obsahovat všechny použité znaky (např. asijské glyfy). | Ujistěte se, že zdrojové písmo podporuje požadované Unicode bloky, nebo vložte sekundární písmo, které pokrývá chybějící rozsah. |

## Pokročilé: Vkládání pouze vybraných písem

Pokud víte, že váš sešit používá jen *Calibri* a *Times New Roman*, můžete omezit vkládání takto:

```csharp
htmlSaveOptions.FontsList = new string[] { "Calibri", "Times New Roman" };
```

Tím se dramaticky zmenší velikost HTML, přičemž se zachová vzhled a pocit.

## Testování výstupu

Po vygenerování `embedded.html` proveďte tyto rychlé kontroly:

1. Otevřete soubor v Chrome/Edge/Firefox.
2. Otevřete Developer Tools → Network → filtrujte podle **font**. Neměli byste vidět žádné externí požadavky.
3. Prohlédněte blok `<style>`; najdete pravidla `@font-face` s `src: url(data:font/ttf;base64,…)`.
4. Porovnejte vykreslený text s původním zobrazením v Excelu—pixel‑perfektní zarovnání znamená úspěch.

## Shrnutí

V tomto průvodci jsme probrali **jak vložit písma** do HTML při **exportu Excelu do HTML** pomocí Aspose.Cells. Vytvořením instance `HtmlSaveOptions`, nastavením `EmbedAllFonts = true` a voláním `Workbook.Save` získáte samostatný HTML soubor, který věrně reprodukuje typografii původního tabulkového listu. Také jsme se podívali na časté úskalí, tipy na výkon a rychlý způsob, jak vložit jen ta písma, která skutečně potřebujete.

---

### Co dál?

- **Export Excel do PDF s vloženými písmy** – ideální pro tiskové dokumenty.
- **Převod více listů do jednoho HTML souboru** – naučte se o `HtmlSaveOptions.OnePagePerSheet`.
- **Dynamické generování HTML v ASP.NET Core** – streamujte HTML přímo do prohlížeče bez dotyku souborového systému.

Neváhejte experimentovat s možnostmi, zanechte komentář, pokud narazíte na problém, a šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}