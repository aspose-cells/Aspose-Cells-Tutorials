---
category: general
date: 2026-01-14
description: Jak vložit písma do HTML a vynutit výpočet vzorců při převodu Excelu
  do HTML. Naučte se nastavit oblast tisku a exportovat grafy.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- force formula calculation
- convert excel to html
- how to set print area
language: cs
og_description: Jak vložit písma do HTML, vynutit výpočet vzorců a převést Excel do
  HTML s nastavením tiskové oblasti – vše v C#.
og_title: Jak vložit písma do HTML – Kompletní C# průvodce
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Jak vložit fonty do HTML – Kompletní průvodce C#
url: /cs/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vložit písma do HTML – Kompletní průvodce v C#  

Už jste se někdy zamysleli **jak vložit písma do HTML** při exportu sešitu Excel? Nejste v tom jediní. Mnoho vývojářů narazí na problém, když vygenerované HTML vypadá na jejich počítači dobře, ale na jiném zařízení ztratí typografii. Dobrá zpráva? S Aspose.Cells pro .NET můžete vložit přesné soubory písem přímo do výstupu HTML – žádné chybějící glyfy.  

V tomto tutoriálu projdeme kompletní příklad, který nejen ukazuje **jak vložit písma do HTML**, ale také demonstruje **vynucení výpočtu vzorců**, **konverzi Excelu do HTML** a dokonce **jak nastavit tiskovou oblast** před exportem grafu do editovatelného PPTX. Na konci budete mít jeden spustitelný C# program, který můžete vložit do libovolného .NET projektu.  

---  

## Co vytvoříte  

- Vytvořte nový sešit, zapište několik maticových vzorců a **vynutí výpočet vzorců**, aby byly výsledky zapsány do souboru.  
- Uložte sešit jako HTML při **vkládání písem** a jejich selektorů variant.  
- Načtěte druhý sešit, který obsahuje graf, definujte **tiskovou oblast** a exportujte tento list do editovatelné prezentace PowerPoint.  
- Vše toto pomocí jen několika řádků čistého, dobře komentovaného C# kódu.  

Žádné externí nástroje, žádné ruční kopírování souborů písem – Aspose.Cells udělá těžkou práci za vás.  

## Požadavky  

| Požadavek | Důvod |
|-------------|--------|
| .NET 6.0 nebo novější | Moderní jazykové funkce a lepší výkon |
| Aspose.Cells pro .NET (NuGet balíček `Aspose.Cells`) | Poskytuje `Workbook`, `HtmlSaveOptions`, `ImageOrPrintOptions` atd. |
| Několik souborů písem TrueType/OpenType (např. `Arial.ttf`) umístěných ve složce projektu | Potřebné pro vkládání; Aspose je automaticky načte, pokud jsou nainstalovány v hostitelském OS |
| Základní znalost C# | Pro sledování kódu a jeho přizpůsobení vašim scénářům |

## Krok 1 – Vytvořte sešit a zapište maticové vzorce  

Nejprve vytvoříme novou instanci `Workbook` a vložíme dva maticové vzorce do buněk **A1** a **A3**. Tyto vzorce (`WRAPCOLS` a `WRAPROWS`) vytvoří malou matici 2‑sloupce/2‑řádky, kterou později uvidíme vygenerovanou v HTML výstupu.  

```csharp
using Aspose.Cells;

namespace FontEmbeddingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Write WRAPCOLS formula – returns a 2‑column array
            worksheet.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4},2)";

            // Write WRAPROWS formula – returns a 2‑row array
            worksheet.Cells[2, 0].Formula = "=WRAPROWS({1;2;3;4},2)";
```

> **Proč je to důležité:** Vložení vzorců vám poskytne dynamický obsah, který bude vyhodnocen, když později vynutíme výpočet. Také to ukazuje, že export do HTML dokáže správně zpracovat výsledky matic.  

## Krok 2 – Vynutit výpočet vzorců  

Aspose.Cells vyhodnocuje vzorce líně. Abychom zajistili, že naše HTML obsahuje vypočtené hodnoty (namísto surových vzorců), zavoláme `CalculateFormula()`.  

```csharp
            // Step 2: Force calculation so the formulas are evaluated
            worksheet.CalculateFormula();
```

> **Tip:** Pokud tento krok přeskočíte, HTML zobrazí text vzorce (`=WRAPCOLS...`) místo čísel, což podkopává smysl upraveného exportu.  

## Krok 3 – Nakonfigurujte možnosti uložení HTML pro vložení písem  

Nyní přichází hvězda představení: vkládání písem. Nastavením `EmbedFonts` na `true` řeknete Aspose, aby zahrnulo data písem jako Base64‑kódované proudy uvnitř vygenerovaného HTML souboru. Povolení `EmbedFontVariationSelectors` zajistí, že jakékoli selektory variant OpenType (používané pro pokročilou typografii) jsou také zachovány.  

```csharp
            // Step 3: Prepare HTML save options that embed fonts and their variation selectors
            HtmlSaveOptions htmlSaveOptions = new HtmlSaveOptions
            {
                EmbedFonts = true,
                EmbedFontVariationSelectors = true
            };
```

> **Jak to funguje:** Když je HTML zapisováno, Aspose vloží blok `<style>` s pravidly `@font-face`, které odkazují na vložené data URI. Prohlížeče vykreslí přesně stejné písmo bez ohledu na písma nainstalovaná u klienta.  

## Krok 4 – Uložte sešit jako HTML  

Nejprve uložíme sešit do souboru `.xlsx` (pro případ, že budete potřebovat zdroj) a poté jej exportujeme do HTML pomocí právě definovaných možností.  

```csharp
            // Step 4: Save the workbook as HTML using the configured options
            string outputDir = @"C:\Demo\Output\"; // adjust to your environment
            workbook.Save(Path.Combine(outputDir, "fontDemo.xlsx"));
            workbook.Save(Path.Combine(outputDir, "fontDemo.html"), htmlSaveOptions);
```

> **Výsledek:** Otevřete `fontDemo.html` v libovolném moderním prohlížeči a uvidíte, že hodnoty matice jsou vykresleny s vloženým písmem, i když písmo není nainstalováno ve vašem počítači.  

## Krok 5 – Načtěte sešit s grafem a nastavte tiskovou oblast  

Následně ukážeme **jak nastavit tiskovou oblast** před exportem listu, který obsahuje graf. Tisková oblast omezuje, co se vykreslí, což je užitečné, když chcete v konečném PPTX jen konkrétní oblast.  

```csharp
            // Step 5: Load a workbook that contains a chart and configure PPTX export options
            Workbook chartWorkbook = new Workbook(Path.Combine(outputDir, "chartEditable.xlsx"));

            // Define the print area (e.g., A1:G20) – this is the SECONDARY keyword in action
            chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:G20";
```

> **Proč nastavit tiskovou oblast?** Bez ní by Aspose exportovalo celý list, což by mohlo zahrnout prázdné řádky/sloupce a nafouknout soubor PPTX.  

## Krok 6 – Exportujte list do editovatelného PPTX  

Na závěr exportujeme list do editovatelného souboru PowerPoint. Nastavením `ExportChartAsEditable = true` se graf uloží jako nativní tvary PowerPointu, což umožní koncovým uživatelům jej přímo v PowerPointu upravovat.  

```csharp
            // Step 6: Configure PPTX export options
            ImageOrPrintOptions pptSaveOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportChartAsEditable = true
            };

            // Step 7: Save as editable PPTX
            chartWorkbook.Save(Path.Combine(outputDir, "editableChart.pptx"), pptSaveOptions);
        }
    }
}
```

> **Co získáte:** `editableChart.pptx` obsahuje graf ze souboru `chartEditable.xlsx` jako editovatelné objekty PowerPointu, omezené na oblast `A1:G20`.  

## Přehled očekávaného výstupu  

| Soubor | Popis |
|------|-------------|
| `fontDemo.xlsx` | Původní sešit s vypočtenými maticovými vzorci. |
| `fontDemo.html` | HTML soubor, který **vkládá písma**, zobrazuje výsledky matice a funguje offline. |
| `editableChart.pptx` | Prezentace PowerPoint s editovatelným grafem, respektující **tiskovou oblast**, kterou jste nastavili. |

Otevřete `fontDemo.html` v Chrome nebo Edge; všimnete si, že text používá přesně to písmo, které jste vložili (např. Arial), i když jej váš systém nemá. Graf v `editableChart.pptx` lze dvojklikem otevřít a upravit stejně jako jakýkoli nativní graf v PowerPointu.  

## Časté otázky a okrajové případy  

### Co když mé písmo není nainstalováno na serveru?  
Aspose.Cells vloží jen písma, která jsou *k dispozici* běhovému prostředí. Pokud konkrétní soubor písma chybí, HTML se vrátí k výchozímu písmu prohlížeče. Pro zajištění vložení zkopírujte požadované soubory `.ttf`/`.otf` do složky aplikace a odkažte na ně pomocí `FontInfo` (pokročilý scénář).  

### Mohu vložit jen podmnožinu znaků pro zmenšení velikosti souboru?  
Ano. Použijte `HtmlSaveOptions.FontEmbeddingMode = FontEmbeddingMode.Subset`. To řekne Aspose, aby zahrnulo jen glyfy skutečně použité v sešitu, čímž výrazně zmenší HTML payload.  

### Funguje **vynucení výpočtu vzorců** také pro volatilní funkce jako `NOW()`?  
Rozhodně. `CalculateFormula()` vyhodnocuje všechny vzorce, včetně volatilních, v okamžiku, kdy jej zavoláte. Pokud potřebujete, aby výpočet odrážel konkrétní datum/čas, nastavte předem `CalculationOptions` sešitu.  

### Co s velkými sešity – způsobí vkládání písem nafouknutí HTML?  
Vkládání písem přidá přibližně 100‑200 KB na písmo (v závislosti na velikosti). Pro masivní reporty zvažte odkazování na webová písma místo vložení, nebo použijte zmíněný režim podmnožiny.  

## Profesionální tipy a osvědčené postupy  

- **Dávkové ukládání:** Pokud generujete desítky HTML souborů, znovu použijte jedinou instanci `HtmlSaveOptions`, abyste se vyhnuli zbytečným alokacím.  
- **Ukládání tiskových oblastí do cache:** Při exportu mnoha listů uložte požadovanou tiskovou oblast do konfiguračního souboru, aby byl kód DRY.  
- **Validace výstupu:** Po uložení HTML spusťte rychlou kontrolu v headless prohlížeči (např. Puppeteer), abyste se ujistili, že písma se správně vykreslují před odesláním uživatelům.  
- **Uzamčení verze:** Výše uvedený kód cílí na Aspose.Cells 23.12+. Novější verze mohou přidat další možnosti jako `FontEmbeddingMode`. Vždy kontrolujte poznámky k vydání.  

## Závěr  

Probrali jsme **jak vložit písma do HTML** pomocí Aspose.Cells, ukázali důležitost **vynucení výpočtu vzorců**, předvedli čistý workflow **konverze Excelu do HTML** a vysvětlili **jak nastavit tiskovou oblast** před exportem grafu do editovatelného PPTX. Kompletní, spustitelný příklad je v jediném souboru `Program.cs`, takže jej můžete zkopírovat, upravit cesty a spustit ještě dnes.  

Připraveni na další krok? Zkuste vyměnit vložené písmo za vlastní firemní typografii, nebo experimentujte s režimem vložení `Subset`, abyste udrželi HTML lehké. Stejný vzor funguje pro PDF, obrázky a dokonce i CSV exporty – stačí změnit třídu `SaveOptions`.  

Máte další otázky ohledně vkládání písem, práce s vzorci nebo triků s tiskovou oblastí? Zanechte komentář níže nebo mě kontaktujte na fórech komunity Aspose. Šťastné programování!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}