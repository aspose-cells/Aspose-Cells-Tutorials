---
category: general
date: 2026-06-05
description: Jak exportovat grafy z PowerPointu pomocí C#. Zahrnuje export OLE objektů
  a umožňuje upravovat grafy v výsledném PPTX – krok za krokem.
draft: false
keywords:
- how to export charts
- export ole objects
- how to export ole
- make charts editable
language: cs
og_description: Jak exportovat grafy z PowerPointu pomocí C#. Naučte se exportovat
  OLE objekty a udělat grafy editovatelnými v uloženém PPTX – krok za krokem.
og_title: Jak exportovat grafy – Kompletní průvodce PowerPoint C#
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  headline: How to Export Charts – Complete PowerPoint C# Guide
  type: TechArticle
- description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  name: How to Export Charts – Complete PowerPoint C# Guide
  steps:
  - name: Full Working Example
    text: Below is the complete, self‑contained program you can compile and run. It
      includes `using` statements, proper disposal, and comments that explain each
      line.
  - name: What if the source file has no charts?
    text: The code will still run; `ExportEditableCharts` simply has no effect because
      there’s nothing to convert. No error is thrown.
  - name: Can I export only specific charts?
    text: Yes. Instead of using the global `ExportEditableCharts` flag, you can iterate
      through `presentation.Slides` and set `Chart.IsEditable = true` on individual
      chart objects before saving. This gives you granular control.
  - name: Does enabling OLE export increase file size?
    text: A little. The binary OLE streams are stored verbatim, so the resulting PPTX
      can be a few kilobytes larger. In most business scenarios the trade‑off is worth
      it because you retain full editability.
  - name: Which PowerPoint versions can open the resulting file?
    text: Any version that supports the OOXML standard (PowerPoint 2007 and later).
      The editable chart feature relies on the native chart editor introduced in Office
      2007, so older binaries like `.ppt` won’t benefit.
  type: HowTo
tags:
- PowerPoint
- C#
- Aspose.Slides
- OLE
- Charts
title: Jak exportovat grafy – kompletní průvodce PowerPoint C#
url: /cs/net/chart-rendering-and-conversion/how-to-export-charts-complete-powerpoint-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak exportovat grafy – Kompletní průvodce PowerPoint C# 

Už jste se někdy zamýšleli **jak exportovat grafy** z PowerPoint prezentace, aniž byste přišli o možnost je později upravovat? Nejste v tom sami. V mnoha reportovacích řetězcích jsou data grafu uložena přímo v souboru PPTX a jakmile soubor předáte dál, příjemce často potřebuje upravit hodnotu nebo změnit popisek. Dobrou zprávou je, že s několika řádky C# můžete zachovat editovatelnost a zároveň exportovat vložené OLE objekty.

V tomto tutoriálu projdeme praktickým, připraveným k okamžitému spuštění příkladem, který ukazuje **jak exportovat grafy**, jak **exportovat OLE objekty** a jak **udělat grafy editovatelné** v výstupním souboru. Na konci budete mít znovupoužitelný úryvek, který můžete vložit do libovolného .NET projektu používajícího knihovnu Aspose.Slides.

> **Pro tip:** Pokud jste v Aspose.Slides noví, ujistěte se, že jste do projektu přidali NuGet balíček `Aspose.Slides.NET` – jinak se kód nepřeloží.

## Co budete potřebovat

| Požadavek | Proč je důležité |
|-------------|----------------|
| .NET 6+ (nebo .NET Framework 4.7+) | Moderní runtime poskytují lepší výkon a snadnější správu balíčků. |
| Aspose.Slides for .NET (nejnovější verze) | Tato knihovna poskytuje třídy `Presentation` a `PptxSaveOptions`, které použijeme. |
| Ukázkový PowerPoint soubor s alespoň jedním grafem | Demo funguje na libovolném `.pptx`, který obsahuje graf; po exportu uvidíte editovatelnost. |
| IDE (Visual Studio, Rider nebo VS Code) | Užitečné pro rychlé ladění a prohlížení vygenerovaného souboru. |

Žádné další nástroje třetích stran nejsou potřeba – vše zajišťuje Aspose API.

## Krok 1 – Načtení zdrojové prezentace

Nejprve musíme načíst původní PPTX do paměti. Představte si to jako otevření dokumentu ve Wordu před zahájením úprav.

```csharp
using Aspose.Slides;

// Step 1: Load the source presentation
Presentation presentation = new Presentation(@"C:\MyProjects\input.pptx");
```

> **Proč je to důležité:** Objekt `Presentation` je vstupním bodem pro všechny další operace. Rozebere soubor, vytvoří objektový model snímků, tvarů, grafů a OLE objektů a udržuje vše v měnitelném stavu.

## Krok 2 – Vytvoření možností uložení a povolení editovatelných grafů

Ve výchozím nastavení, když zavoláte `Save`, knihovna převádí grafy na statické obrázky. Aby zůstaly editovatelné, musíte přepnout příznak `ExportEditableCharts`.

```csharp
// Step 2: Create PPTX save options and enable editable charts
PptxSaveOptions saveOptions = new PptxSaveOptions
{
    // This tells Aspose to keep chart data in a format PowerPoint can edit.
    ExportEditableCharts = true
};
```

> **Jak to funguje:** Když je `ExportEditableCharts` nastaven na `true`, knihovna zapíše XML definici grafu (`chart.xml`) do PPTX místo rasterizace. PowerPoint pak načte toto XML a umožní uživateli otevřít editor grafu.

## Krok 3 – Povolení exportu vložených OLE objektů

Mnoho prezentací vkládá listy Excelu, diagramy Visia nebo dokonce PDF soubory jako OLE objekty. Pokud chcete, aby přežily celý proces, povolte `ExportOLEObjects`.

```csharp
// Step 3: Enable export of embedded OLE objects
saveOptions.ExportOLEObjects = true;
```

> **Co “export OLE objects” skutečně znamená:** OLE balíček je uložen jako binární blob uvnitř PPTX. Nastavením tohoto příznaku zachováte původní binární data, což příjemci umožní dvojklikem otevřít objekt v jeho nativní aplikaci (např. Excel). Bez toho by byl OLE objekt odstraněn, což by přerušilo odkazy a ztratila se data.

## Krok 4 – Uložení prezentace s nastavenými možnostmi

Nyní, když máme možnosti připravené, jednoduše řekneme Aspose, aby soubor zapsal.

```csharp
// Step 4: Save the presentation with the configured options
presentation.Save(@"C:\MyProjects\editable.pptx", saveOptions);
```

> **Výsledek:** `editable.pptx` obsahuje stejné snímky jako `input.pptx`, ale jakýkoli graf lze upravit přímo v PowerPointu a všechny vložené OLE objekty zůstávají nedotčeny.

### Kompletní funkční příklad

Níže je kompletní, samostatný program, který můžete zkompilovat a spustit. Obsahuje `using` direktivy, správné uvolnění prostředků a komentáře vysvětlující každý řádek.

```csharp
using System;
using Aspose.Slides;

namespace ExportChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the source PPTX
            string sourcePath = @"C:\MyProjects\input.pptx";
            // Path where the edited PPTX will be saved
            string destPath = @"C:\MyProjects\editable.pptx";

            // Load the presentation
            using (Presentation presentation = new Presentation(sourcePath))
            {
                // Configure save options
                PptxSaveOptions options = new PptxSaveOptions
                {
                    ExportEditableCharts = true,   // make charts editable
                    ExportOLEObjects = true        // export OLE objects such as embedded Excel sheets
                };

                // Save the new file
                presentation.Save(destPath, options);
            }

            Console.WriteLine("Presentation saved with editable charts and OLE objects.");
        }
    }
}
```

**Očekávaný výstup:** Po spuštění programu otevřete `editable.pptx` v PowerPointu. Klikněte pravým tlačítkem na libovolný graf → *Edit Data* → otevře se editor grafu, což potvrzuje, že **make charts editable** uspěl. Dvojklikem na vložený list Excelu se otevře v Excelu, což dokazuje, že **export OLE objects** fungoval.

![jak exportovat grafy diagram](https://example.com/images/export-charts.png "jak exportovat grafy – PowerPoint po exportu")

*(Alt text: jak exportovat grafy – snímek PowerPoint s editovatelným grafem a OLE objektem)*

## Časté otázky a okrajové případy

### Co když zdrojový soubor neobsahuje žádné grafy?

Kód bude i tak fungovat; `ExportEditableCharts` jednoduše nemá žádný efekt, protože není co převádět. Žádná chyba není vyhozena.

### Můžu exportovat jen konkrétní grafy?

Ano. Místo globálního příznaku `ExportEditableCharts` můžete projít `presentation.Slides` a nastavit `Chart.IsEditable = true` u jednotlivých grafů před uložením. To vám dává jemnější kontrolu.

```csharp
foreach (ISlide slide in presentation.Slides)
{
    foreach (IChart chart in slide.Shapes.OfType<IChart>())
    {
        chart.IsEditable = true; // enable editability only for this chart
    }
}
```

### Zvyšuje povolení OLE exportu velikost souboru?

Trochu. Binární OLE streamy jsou uloženy beze změny, takže výsledný PPTX může být o několik kilobajtů větší. Ve většině obchodních scénářů je tento kompromis výhodný, protože zachovává plnou editovatelnost.

### Které verze PowerPointu mohou otevřít výsledný soubor?

Jakákoli verze podporující standard OOXML (PowerPoint 2007 a novější). Funkce editovatelných grafů spoléhá na nativní editor grafů zavedený v Office 2007, takže starší binární formáty jako `.ppt` nebudou mít výhodu.

## Tipy pro produkčně připravený kód

| Tip | Důvod |
|-----|--------|
| Používejte bloky `using` (jak je ukázáno) k uvolnění objektů `Presentation`. | Zabraňuje únikům paměti, zejména při zpracování mnoha souborů najednou. |
| Ověřte cesty k souborům před načtením. | Zabraňuje `FileNotFoundException`, která by zhavarovala službu běžící na pozadí. |
| Zaznamenávejte nastavení `ExportEditableCharts` a `ExportOLEObjects`. | Užitečné při řešení problémů, když uživatel hlásí needitovatelné grafy. |
| Zachyťte `Aspose.Slides.Exception` samostatně. | Poskytuje srozumitelnější chybové zprávy z knihovny (např. nepodporované typy grafů). |
| Zvažte `PptxCompressionLevel`, pokud záleží na velikosti souboru. | Můžete komprimovat výstup a přitom zachovat editovatelnost. |

## Shrnutí – Co jsme dosáhli

Začali jsme s jasnou otázkou: **jak exportovat grafy** z PowerPoint souboru a přitom je zachovat editovatelné a uchovat vložené OLE objekty. Načtením prezentace, nastavením `PptxSaveOptions` (`ExportEditableCharts = true` a `ExportOLEObjects = true`) a uložením souboru nyní máme PPTX, který splňuje oba požadavky. Stejný vzor lze znovu použít pro hromadné konverze, CI pipeline nebo jakýkoli automatizovaný nástroj pro reportování.

## Co zkusit dál?

- **Exportovat grafy jako obrázky** pro statické reporty (`saveOptions.ExportEditableCharts = false`).  
- **Převést PPTX na PDF** při zachování vektorové grafiky (`PdfSaveOptions`).  
- **Manipulovat s daty grafu programově** (např. aktualizovat hodnoty řad před exportem).  
- **Integrovat s Azure Functions** pro poskytování API na vyžádání exportu grafů.  

Klidně experimentujte a dejte nám vědět, jaké okrajové případy jste narazili. Šťastné kódování a ať jsou všechny vaše grafy editovatelné!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, která vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy ve vašich projektech.

- [Jak exportovat Excel grafy do PDF pomocí Aspose.Cells pro .NET: krok za krokem](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Jak převést Excel grafy do SVG pomocí Aspose.Cells pro .NET (průvodce krok za krokem)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Jak použít motivy na Excel grafy pomocí Aspose.Cells .NET: průvodce krok za krokem](/cells/english/net/charts-graphs/apply-themes-charts-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}