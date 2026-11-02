---
category: general
date: 2026-07-03
description: Jak zachovat grafy a zároveň zachovat formátování grafů pomocí Aspose.Slides
  v C#. Postupujte podle tohoto průvodce krok za krokem.
draft: false
keywords:
- how to preserve charts
- preserve chart formatting
language: cs
og_description: Jak zachovat grafy a formátování grafů pomocí Aspose.Slides v C#.
  Kompletní průvodce s kódem.
og_title: Jak zachovat grafy – zachovat formátování grafu v PowerPointu (C#)
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  headline: how to preserve charts – preserve chart formatting in PowerPoint C#
  type: TechArticle
- description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  name: how to preserve charts – preserve chart formatting in PowerPoint C#
  steps:
  - name: Open `EditableCharts.pptx` in PowerPoint.
    text: Open `EditableCharts.pptx` in PowerPoint.
  - name: Click any chart → “Edit Data”.
    text: Click any chart → “Edit Data”.
  - name: The Excel‑like data sheet should appear, letting you modify series values.
    text: The Excel‑like data sheet should appear, letting you modify series values.
  type: HowTo
- questions:
  - answer: Directly no—`ExportEditableObjects` only applies to the PPTX format. Convert
      first, then export.
    question: Does this work with PowerPoint 2003 (PPT) files?
  - answer: Absolutely. The same `ExportEditableObjects` flag keeps SmartArt, tables,
      and diagrams editable.
    question: Can I preserve other objects like SmartArt?
  - answer: 'The slide size is stored in the presentation metadata and isn’t affected
      by these options. No extra code needed. --- ## Next steps – keep the momentum
      Now that you’ve nailed **how to preserve charts**, try exploring: - **preserve
      chart formatting** for specific chart types (e.g., stacked bar vs. rad'
    question: What if I need to keep the original slide size?
  type: FAQPage
tags:
- Aspose.Slides
- C#
- PowerPoint
- chart automation
title: jak zachovat grafy – zachovat formátování grafu v PowerPointu C#
url: /cs/net/setting-chart-appearance/how-to-preserve-charts-preserve-chart-formatting-in-powerpoi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak zachovat grafy – zachování formátování grafu v PowerPoint C#

Už jste se někdy zamysleli **jak zachovat grafy**, když potřebujete programově exportovat nebo upravovat soubor PowerPoint? Možná jste zkusili rychlé uložení a graf se změnil na statický obrázek, čímž se ztratila editovatelnost, na kterou jste počítali.  

V tomto tutoriálu vám ukážeme **jak zachovat grafy** **a** udržet jejich **zachování formátování grafu** pomocí Aspose.Slides pro .NET. Na konci budete mít připravený C# úryvek, který vytvoří PPTX, kde každý graf zůstane editovatelným OOXML objektem – žádné další zploštělé obrázky.

## Co se naučíte

- Přesné kroky, jak načíst prezentaci, nastavit možnosti exportu a uložit ji při **zachování formátování grafu**.  
- Proč je důležitý příznak `ExportEditableObjects` a jak zabraňuje rasterizaci grafů.  
- Běžné úskalí (např. starší PPT formáty, chybějící fonty) a rychlé opravy.  

Předchozí zkušenost s Aspose není vyžadována; stačí základní nastavení C# a soubor PowerPoint, ve kterém chcete zachovat editovatelnost grafů.

## Požadavky

- .NET 6.0 nebo novější (kód funguje také s .NET Framework 4.7+).  
- NuGet balíček Aspose.Slides pro .NET (`Install-Package Aspose.Slides.NET`).  
- Ukázkový soubor `input.pptx`, který obsahuje alespoň jeden graf.  
- Visual Studio, Rider nebo jakýkoli editor, který preferujete.

---

## Krok 1: Nainstalujte Aspose.Slides a vytvořte nový konzolový projekt

Nejprve založte čerstvou konzolovou aplikaci a přidejte knihovnu:

```bash
dotnet new console -n PreserveChartsDemo
cd PreserveChartsDemo
dotnet add package Aspose.Slides.NET
```

> **Pro tip:** Pokud jste za firemním proxy, přidejte příznak `--no-restore` a obnovte později s vašimi proxy nastaveními.

## Krok 2: Načtěte zdrojovou prezentaci – první místo, kde použít **jak zachovat grafy**

Otevřete svůj PPTX soubor pomocí třídy `Presentation`. Zde skutečně začíná cesta k **jak zachovat grafy**.

```csharp
using Aspose.Slides;
using Aspose.Slides.Export;

namespace PreserveChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Load the source presentation
            // Replace the path with the location of your PPTX that contains charts.
            Presentation pres = new Presentation(@"YOUR_DIRECTORY\input.pptx");
```

Všimněte si, že jsme se zatím nedotkli žádných grafových objektů – je to úmyslné. Načtení souboru tak, jak je, zajistí zachování původní XML struktury, což je klíčové pro **zachování formátování grafu** později.

## Krok 3: Nastavte možnosti exportu – jádro **jak zachovat grafy**

Aspose.Slides nabízí třídu `PresentationExportOptions`. Nastavením `ExportEditableObjects` na `true` řeknete enginu, aby ponechal grafy, tabulky a SmartArt jako nativní OOXML části místo jejich zploštění.

```csharp
            // Step 3: Configure export options to keep objects editable
            PresentationExportOptions exportOptions = new PresentationExportOptions
            {
                // This flag is the key to how to preserve charts.
                ExportEditableObjects = true
            };
```

Proč to funguje? Když je `ExportEditableObjects` nastaveno na `false` (výchozí hodnota), knihovna rasterizuje složité objekty pro kompatibilitu, což zničí **zachování formátování grafu**. Zapnutím této volby se zachová původní XML grafu, takže uživatelé mohou otevřít PPTX a stále upravovat data grafu.

## Krok 4: Uložte prezentaci s nastavenými možnostmi

Nyní zapíšeme výstupní soubor. Přetížená metoda `Save`, která přijímá `SaveFormat` a `exportOptions`, zaručuje, že graf zůstane editovatelný.

```csharp
            // Step 4: Save the presentation with the configured options
            pres.Save(@"YOUR_DIRECTORY\EditableCharts.pptx", SaveFormat.Pptx, exportOptions);

            // Optional: Inform the user
            Console.WriteLine("Presentation saved with editable charts at: YOUR_DIRECTORY\\EditableCharts.pptx");
        }
    }
}
```

Po spuštění programu vznikne soubor `EditableCharts.pptx`. Otevřete jej v PowerPointu, klikněte pravým tlačítkem na graf a uvidíte běžnou možnost „Edit Data“ – důkaz, že jsme úspěšně zvládli **jak zachovat grafy** a **zachování formátování grafu**.

## Krok 5: Ověřte výsledek a řešte běžné problémy

### Ověření

1. Otevřete `EditableCharts.pptx` v PowerPointu.  
2. Klikněte na libovolný graf → „Edit Data“.  
3. Měla by se zobrazit Excel‑podobná tabulka, kde můžete měnit hodnoty řad.

Pokud vidíte jen statický obrázek, zkontrolujte:

- Používáte aktuální verzi Aspose.Slides (starší verze měly chyby s `ExportEditableObjects`).  
- Zdrojový PPTX skutečně obsahuje grafové objekty (ne obrázky grafů).  
- Žádné vlastní téma nebo substituce fontů nezpůsobují, že se graf vykreslí jako obrázek.

### Okrajové případy

- **Starší PPT (binární) soubory:** Před aplikací možností exportu je nejprve převedete na PPTX (`pres.Save("temp.pptx", SaveFormat.Pptx)`).  
- **Velké prezentace:** Spotřeba paměti může narůst; zvažte použití vzoru `Dispose` u `Presentation` nebo streamingových API pro masivní soubory.  
- **Vložené fonty:** Pokud cílové prostředí postrádá původní fonty, PowerPoint může přejít na náhradní a vykreslit graf jako obrázek. Vložte fonty do zdrojového souboru nebo je distribuujte spolu s aplikací.

---

## Často kladené otázky (FAQ)

**Q: Funguje to s PowerPoint 2003 (PPT) soubory?**  
A: Přímo ne – `ExportEditableObjects` funguje jen pro formát PPTX. Nejprve soubor převedete, pak exportujete.

**Q: Mohu zachovat i jiné objekty, jako SmartArt?**  
A: Ano. Stejný příznak `ExportEditableObjects` ponechá editovatelné i SmartArt, tabulky a diagramy.

**Q: Co když potřebuji zachovat původní velikost snímku?**  
A: Velikost snímku je uložena v metadatech prezentace a není ovlivněna těmito možnostmi. Žádný další kód není potřeba.

---

## Další kroky – udržte tempo

Nyní, když ovládáte **jak zachovat grafy**, můžete zkusit:

- **zachování formátování grafu** pro konkrétní typy grafů (např. vrstvený sloupcový vs. radar).  
- Použití API `Chart` k programové úpravě dat před uložením.  
- Export do jiných formátů (PDF, HTML) a přitom zachovat editovatelnost grafů ve zdrojovém PPTX.  

Všechny tyto kroky staví na stejném principu: zachovat podkladové OOXML nedotčeno.

---

## Závěr

Prošli jsme **jak zachovat grafy** v souboru PowerPoint pomocí Aspose.Slides pro .NET a ukázali jsme přesné kroky **zachování formátování grafu**, které zajistí, že grafy zůstanou plně editovatelné. Kompletní kód výše můžete vložit do libovolného C# projektu a vysvětlení pokrývají *proč* za každým řádkem – nebudete jen kopírovat, ale skutečně pochopíte.

Vyzkoušejte to, upravte možnosti exportu a brzy budete automatizovat aktualizace prezentací, aniž byste ztratili možnost jemně ladit data grafů. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vašich projektech.

- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [How to Create Charts in Excel Using Aspose.Cells for .NET&#58; A Developer's Guide](/cells/english/net/charts-graphs/create-charts-excel-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}