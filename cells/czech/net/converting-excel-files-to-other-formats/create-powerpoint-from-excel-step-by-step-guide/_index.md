---
category: general
date: 2026-02-09
description: Vytvořte PowerPoint z Excelu během několika minut – naučte se, jak převést
  Excel na PowerPoint a exportovat Excel do PPT pomocí jednoduchého příkladu kódu
  v C#.
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export excel to ppt
- generate ppt from excel
- how to convert excel to pptx
language: cs
og_description: Vytvořte PowerPoint z Excelu rychle. Tento průvodce ukazuje, jak převést
  Excel do PowerPointu, exportovat Excel do PPT a generovat PPT z Excelu pomocí C#.
og_title: Vytvořte PowerPoint z Excelu – kompletní programovací průvodce
tags:
- C#
- Aspose.Cells
- PowerPoint automation
- Office interop
title: Vytvořte PowerPoint z Excelu – průvodce krok za krokem
url: /cs/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření PowerPointu z Excelu – Kompletní programovací průvodce

Už jste někdy potřebovali **vytvořit PowerPoint z Excelu**, ale nebyli jste si jisti, kterou API zavolat? Nejste v tom sami. Mnoho vývojářů narazí na problém, když chtějí převést tabulky na prezentace bez ručního kopírování a vkládání.  

Dobrá zpráva: s několika řádky C# můžete **převést Excel do PowerPointu**, exportovat tvary listu a získat připravený soubor PPTX k prezentaci. V tomto tutoriálu projdeme celý proces, vysvětlíme, proč je každý krok důležitý, a ukážeme vám, jak řešit nejčastější úskalí.

## Co se naučíte

- Jak načíst Excel sešit, který obsahuje grafy, obrázky nebo SmartArt.  
- Přesné volání, které **exportuje Excel do PPT** pomocí knihovny Aspose.Cells.  
- Jak uložit vygenerovanou prezentaci a ověřit výsledek.  
- Tipy pro práci se sešity bez tvarů, úpravu velikosti snímku a řešení nesouladu verzí.

Žádné externí nástroje, žádný COM interop, jen čistý .NET kód, který běží kdekoliv, kde je podporován .NET Core nebo .NET 5+.

---

## Požadavky

Předtím, než se pustíme do práce, ujistěte se, že máte:

1. **Aspose.Cells for .NET** (knihovna, která poskytuje `SaveToPresentation`). Můžete ji získat z NuGet:  

   ```bash
   dotnet add package Aspose.Cells
   ```
2. Aktuální .NET SDK (doporučeno 6.0 nebo novější).  
3. Excel soubor (`shapes.xlsx`), který obsahuje alespoň jeden tvar, graf nebo obrázek, který chcete zobrazit na snímku.

A to je vše — žádná instalace Office, žádné licenční komplikace pro účely tohoto demu (bezplatná zkušební verze funguje bez problémů).

## Krok 1: Načtení Excel sešitu (Vytvoření PowerPointu z Excelu)

Prvním, co potřebujeme, je objekt `Workbook`, který ukazuje na zdrojový soubor. Tento objekt představuje celý Excel dokument, včetně všech listů, grafů a vložených objektů.

```csharp
using Aspose.Cells;
using Aspose.Slides;

// Step 1: Load the Excel workbook containing the shapes
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\shapes.xlsx");

// Why this matters:
// - `Workbook` abstracts the file format, so you don’t have to worry about .xls vs .xlsx.
// - Loading the file early lets you inspect its contents (e.g., count of worksheets) before conversion.
```

> **Pro tip:** Pokud si nejste jisti, zda soubor existuje, zabalte konstruktor do `try/catch` a poskytněte užitečnou chybovou zprávu. Ušetří vás to pozdějšího kryptického `FileNotFoundException`.

## Krok 2: Převod sešitu do PowerPoint prezentace (Export Excel do PPT)

Aspose.Cells obsahuje vestavěný exportér, který převádí celý sešit — nebo jen vybrané listy — do PowerPoint prezentace. Metoda `SaveToPresentation` odlehčuje těžkou práci.

```csharp
// Step 2: Convert the workbook to a PowerPoint presentation (PPTX format)
Presentation presentation = workbook.SaveToPresentation(ExportTo.Pptx);

// How it works:
// - Each worksheet becomes a separate slide.
// - Shapes, charts, and images are rasterized and placed on the slide preserving their layout.
// - You can later tweak the `Presentation` object (e.g., add a title slide) before saving.
```

Pokud potřebujete **generovat ppt z excelu** jen pro podmnožinu listů, můžete použít přetížení, které přijímá kolekci `SheetOptions`. Pro většinu scénářů je výchozí převod dostačující.

## Krok 3: Uložení vygenerované prezentace (Jak převést Excel do PPTX)

Nyní, když máme instanci `Presentation`, její uložení na disk je jednoduché. Výstup bude standardní soubor `.pptx`, který může otevřít jakákoli moderní verze PowerPointu.

```csharp
// Step 3: Save the generated presentation to a file
presentation.Save(@"C:\MyProjects\ExcelToPpt\shapes.pptx");

// Verification:
// Open the file in PowerPoint or use Aspose.Slides to programmatically inspect slide count.
```

> **Co když sešit nemá žádné tvary?**  
> Exportér i tak vytvoří snímky, ale budou prázdné. Před převodem můžete zkontrolovat `workbook.Worksheets[i].Shapes.Count` a rozhodnout, zda daný list přeskočit.

## Volitelné: Doladění výstupu (Pokročilý export Excel do PPT)

Někdy není výchozí velikost snímku (standardní 4:3) ideální pro širokoúhlé prezentace. Před uložením můžete upravit rozměry snímku:

```csharp
// Set slide size to widescreen (16:9)
presentation.SlideSize.SetSize(SlideSizeType.Widescreen, SlideSizeScaleType.DoNotScale);

// Add a custom title slide (optional)
ISlide titleSlide = presentation.Slides.InsertEmptySlide(0, presentation.LayoutSlides[0]);
titleSlide.Shapes.AddAutoShape(ShapeType.Rectangle, 50, 50, 600, 100)
          .TextFrame.Text = "Quarterly Report – Exported from Excel";
```

Tyto úpravy ukazují, **jak převést Excel do PowerPointu** s profesionálním vzhledem, ne jen jako surový výpis dat.

## Kompletní funkční příklad (Všechny kroky dohromady)

Níže je kompletní, připravený program. Zkopírujte jej do konzolové aplikace, upravte cesty k souborům a stiskněte **F5**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string excelPath = @"C:\MyProjects\ExcelToPpt\shapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2️⃣ Convert to PPTX
            Presentation presentation = workbook.SaveToPresentation(ExportTo.Pptx);

            // Optional: set widescreen layout
            presentation.SlideSize.SetSize(SlideSizeType.Widescreen, SlideSizeScaleType.DoNotScale);

            // Optional: add a title slide
            ISlide titleSlide = presentation.Slides.InsertEmptySlide(0, presentation.LayoutSlides[0]);
            titleSlide.Shapes.AddAutoShape(ShapeType.Rectangle, 50, 50, 600, 100)
                      .TextFrame.Text = "Quarterly Report – Exported from Excel";

            // 3️⃣ Save the PPTX file
            string pptxPath = @"C:\MyProjects\ExcelToPpt\shapes.pptx";
            presentation.Save(pptxPath);

            Console.WriteLine($"✅ Successfully created PowerPoint from Excel! File saved at: {pptxPath}");
        }
    }
}
```

**Očekávaný výsledek:** Otevřete `shapes.pptx` v PowerPointu. Uvidíte jeden snímek na každý list, přičemž zachovává původní grafy, obrázky a další tvary. Volitelný titulní snímek se objeví na samém začátku a dodá prezentaci vylepšený úvod.

## Časté otázky a okrajové případy

| Otázka | Odpověď |
|----------|--------|
| *Co když potřebuji jen jeden list?* | Použijte `Workbook.Worksheets[0]` a zavolejte `SaveToPresentation` na tento list pomocí `SheetOptions`. |
| *Mohu zachovat Excelové vzorce?* | Ne — vzorce jsou v snímku vykresleny jako statické hodnoty. Pokud potřebujete živá data, zvažte pozdější propojení PPTX s Excel souborem. |
| *Funguje to na Linuxu/macOS?* | Ano. Aspose.Cells je platformově nezávislý; stačí nainstalovat .NET runtime a vše je připraveno. |
| *Co s sešity chráněnými heslem?* | Načtěte je s `LoadOptions`, které zahrnují heslo, před voláním `SaveToPresentation`. |
| *Proč dostávám prázdné snímky?* | Zkontrolujte, že sešit skutečně obsahuje tvary (`Shapes.Count > 0`). Prázdné snímky jsou vytvořeny pro prázdné listy. |

## Závěr

Nyní máte jasné, end‑to‑end řešení pro **vytvoření PowerPointu z Excelu** pomocí C#. Načtením sešitu, voláním `SaveToPresentation` a uložením výsledku můžete **převést Excel do PowerPointu**, **exportovat Excel do PPT** a **generovat PPT z Excelu** pomocí jen několika řádků kódu.  

Od semene můžete dále zkoumat:

- Přidání animací do vygenerovaných snímků pomocí Aspose.Slides.  
- Automatizaci celého pipeline (např. čtení souborů ze složky, hromadný převod).  
- Integraci kódu do ASP.NET Core API, aby uživatelé mohli nahrát Excel soubor a okamžitě získat PPTX.

Vyzkoušejte to, upravte velikost snímku, přidejte vlastní titul — je spousta prostoru, jak výstup udělat opravdu svým. Máte otázky nebo narazíte na problém? Zanechte komentář níže a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}