---
category: general
date: 2026-02-09
description: Vytvořte referenční oblast kontingenční tabulky v C# a exportujte obrázek
  kontingenční tabulky. Naučte se, jak uložit oblast Excelu jako PNG pomocí Aspose.Cells
  – rychlý, kompletní návod.
draft: false
keywords:
- create pivot reference range
- export pivot table image
- save excel range as png
- Aspose.Cells C#
- Excel automation C#
language: cs
og_description: Vytvořte referenční oblast kontingenční tabulky v C# a exportujte
  obrázek kontingenční tabulky do PNG. Kompletní krok‑za‑krokem průvodce pro uložení
  oblasti v Excelu jako PNG.
og_title: Vytvořit referenční oblast kontingenční tabulky – Exportovat obrázek kontingenční
  tabulky jako PNG
tags:
- Aspose.Cells
- C#
- Excel
title: Vytvořit referenční oblast kontingenční tabulky – Exportovat obrázek kontingenční
  tabulky jako PNG
url: /cs/net/rendering-and-export/create-pivot-reference-range-export-pivot-table-image-as-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření referenčního rozsahu kontingenční tabulky – Export obrázku kontingenční tabulky jako PNG

Potřebujete **vytvořit referenční rozsah kontingenční tabulky** v sešitu Excel pomocí C#? Můžete také **exportovat obrázek kontingenční tabulky** a **uložit rozsah Excelu jako png** pomocí jen několika řádků kódu. Podle mé zkušenosti je převod živé kontingenční tabulky na statický obrázek praktický způsob, jak vložit analytiku do zpráv, e‑mailů nebo dashboardů, aniž byste museli přenášet celý sešit.

V tomto tutoriálu projdeme vše, co potřebujete vědět: požadované knihovny, přesný kód, proč je každé volání důležité, a několik úskalí, na která můžete narazit. Na konci budete schopni s jistotou vygenerovat soubor PNG libovolné kontingenční tabulky a pochopíte, jak přizpůsobit tento vzor pro více listů nebo vlastní formáty obrázků.

## Požadavky

- **Aspose.Cells for .NET** (bezplatná zkušební verze funguje dobře pro testování).  
- **.NET 6.0** nebo novější – API, které používáme, je plně kompatibilní s .NET Standard 2.0+, takže starší frameworky také zkompilují.  
- Základní projekt v C# (Console App, WinForms nebo ASP.NET – cokoliv, co může odkazovat na NuGet balíček).  

Pokud jste ještě nenainstalovali Aspose.Cells, spusťte:

```bash
dotnet add package Aspose.Cells
```

A to je vše – žádná COM interop, žádný Excel nainstalovaný na serveru.

## Krok 1: Otevření sešitu a přístup k prvnímu listu

Prvním krokem je načíst soubor sešitu a získat list, který obsahuje kontingenční tabulku. Záměrně vybíráme **první list** (`Worksheets[0]`), protože většina ukázkových souborů umisťuje kontingenční tabulku právě tam, ale můžete index nahradit názvem, pokud chcete.

```csharp
using Aspose.Cells;
using System;

// Load an existing Excel file (replace with your own path)
Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Access the first worksheet – this is where our pivot lives
Worksheet worksheet = wb.Worksheets[0];
```

*Proč je to důležité:* `Worksheet` je vstupní bod pro jakoukoli operaci založenou na rozsahu. Pokud ukážete na špatný list, následné volání `PivotTables[0]` vyvolá `IndexOutOfRangeException`.

## Krok 2: Vytvoření referenčního rozsahu kontingenční tabulky

Nyní požádáme samotnou kontingenční tabulku, aby nám poskytla **referenční rozsah**. Tento rozsah představuje přesné buňky, které tvoří kontingenční tabulku – záhlaví, datové řádky a součty. Metoda `CreateReferenceRange()` provádí těžkou práci interně, zpracovává sloučené buňky a skryté řádky.

```csharp
// Grab the first pivot table on the worksheet
PivotTable pivot = worksheet.PivotTables[0];

// Build a reference range that covers the whole pivot
Range pivotReferenceRange = pivot.CreateReferenceRange();
```

> **Tip:** Pokud váš sešit obsahuje více kontingenčních tabulek, iterujte přes `worksheet.PivotTables` a vyberte tu, kterou potřebujete, podle její vlastnosti `Name`.

## Krok 3: Vykreslení referenčního rozsahu jako obrázku

Aspose.Cells dokáže vykreslit libovolný `Range` do obrázku. Vrácený objekt podporuje jak rastrové (PNG, JPEG), tak vektorové (SVG) formáty. Zde požadujeme výchozí rastrový obrázek, což je objekt kompatibilní s `System.Drawing.Image`.

```csharp
// Convert the pivot reference range into an image object
ImageOrVector pivotImage = pivotReferenceRange.ToImage();
```

*Co se děje pod kapotou?* API zachytí vizuální rozvržení rozsahu, respektuje styly buněk, písma a podmíněné formátování. Je to v podstatě to samé jako pořízení snímku obrazovky, ale programově a bez uživatelského rozhraní.

## Krok 4: Uložení vygenerovaného obrázku do souboru

Nakonec obrázek uložíme. Metoda `Save` automaticky zvolí PNG, pokud jí předáte příponu „.png“. Můžete také předat objekt `SaveOptions`, pokud potřebujete řídit DPI nebo použít jiný formát.

```csharp
// Save the image as PNG – the extension drives the format
pivotImage.Save("YOUR_DIRECTORY/pivot.png");
```

Po provedení tohoto řádku otevřete `pivot.png` a uvidíte pixel‑dokonalý snímek kontingenční tabulky, připravený k vložení kamkoli.

## Kompletní funkční příklad

Spojením všech částí získáte samostatný konzolový program, který můžete zkopírovat a spustit:

```csharp
using Aspose.Cells;
using System;

namespace PivotExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

            // 2️⃣ Access first worksheet
            Worksheet worksheet = wb.Worksheets[0];

            // 3️⃣ Get first pivot table
            if (worksheet.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found on the first sheet.");
                return;
            }
            PivotTable pivot = worksheet.PivotTables[0];

            // 4️⃣ Create a reference range that covers the whole pivot
            Range pivotReferenceRange = pivot.CreateReferenceRange();

            // 5️⃣ Render the range to an image
            ImageOrVector pivotImage = pivotReferenceRange.ToImage();

            // 6️⃣ Save as PNG
            string outputPath = "YOUR_DIRECTORY/pivot.png";
            pivotImage.Save(outputPath);

            Console.WriteLine($"Pivot table image saved to {outputPath}");
        }
    }
}
```

**Očekávaný výstup:** soubor pojmenovaný `pivot.png` umístěný v `YOUR_DIRECTORY`. Otevřete jej v libovolném prohlížeči obrázků – měli byste vidět přesné rozvržení původní kontingenční tabulky, včetně záhlaví sloupců, datových řádků a celkových součtů.

## Export obrázku kontingenční tabulky – Přizpůsobení velikosti a DPI

Někdy je výchozí obrázek příliš malý pro snímek prezentace. Rozlišení můžete ovládat předáním objektu `ImageOrVectorSaveOptions`:

```csharp
using Aspose.Cells.Drawing;

// Define PNG options – 300 DPI for high‑quality print
ImageOrVectorSaveOptions options = new ImageOrVectorSaveOptions
{
    ImageFormat = ImageFormat.Png,
    Resolution = 300 // DPI
};

pivotImage.Save("YOUR_DIRECTORY/pivot_highres.png", options);
```

*Proč upravovat DPI?* Vyšší DPI poskytuje ostřejší hrany, zejména když je PNG zvětšováno v PowerPointu nebo PDF.

## Uložení rozsahu Excelu jako PNG – Práce s více listy

Pokud potřebujete exportovat kontingenční tabulky z několika listů, projděte `Workbook.Worksheets` a opakujte kroky. Zde je stručný úryvek:

```csharp
foreach (Worksheet ws in wb.Worksheets)
{
    foreach (PivotTable pt in ws.PivotTables)
    {
        Range refRange = pt.CreateReferenceRange();
        ImageOrVector img = refRange.ToImage();
        string fileName = $"pivot_{ws.Name}_{pt.Name}.png";
        img.Save($"YOUR_DIRECTORY/{fileName}");
        Console.WriteLine($"Saved {fileName}");
    }
}
```

Tento vzor **exportuje obrázek kontingenční tabulky** pro každou kontingenční tabulku v sešitu a každý soubor je pojmenován podle svého listu a kontingenční tabulky – ideální pro hromadné zpracování.

## Časté úskalí a jak se jim vyhnout

| Problém | Proč k tomu dochází | Řešení |
|-------|----------------|-----|
| `IndexOutOfRangeException` on `PivotTables[0]` | List neobsahuje žádné kontingenční tabulky. | Zkontrolujte `worksheet.PivotTables.Count` před přístupem. |
| Výstup prázdného obrázku | Kontingenční tabulka je filtrována tak, že skrývá všechny řádky. | Zajistěte, aby kontingenční tabulka měla viditelná data, nebo zavolejte `pivot.RefreshData();` před vytvořením rozsahu. |
| PNG s nízkým rozlišením | Výchozí DPI je 96. | Použijte `ImageOrVectorSaveOptions.Resolution` jak je uvedeno výše. |
| Chyby cesty k souboru | Neplatné znaky v `YOUR_DIRECTORY`. | Použijte `Path.Combine` a `Path.GetInvalidPathChars()` pro sanitaci. |

## Ověření – Rychlý test

Po spuštění kompletního příkladu:

1. Otevřete `pivot.png` ve Windows Photo Viewer.  
2. Ověřte, že záhlaví sloupců, datové řádky a součty odpovídají zobrazení v Excelu.  
3. Pokud zjistíte chybějící řádky, dvojitě zkontrolujte, že metoda **RefreshData** kontingenční tabulky byla zavolána před `CreateReferenceRange()`.

## Bonus: Vložení PNG do dokumentu Word

Protože je obrázek již ve formátu PNG, můžete jej přímo předat do Aspose.Words:

```csharp
using Aspose.Words;
Document doc = new Document();
DocumentBuilder builder = new DocumentBuilder(doc);
builder.InsertImage("YOUR_DIRECTORY/pivot.png");
doc.Save("YOUR_DIRECTORY/report.docx");
```

Nyní máte Word report, který obsahuje přesný snímek vaší kontingenční tabulky – bez nutnosti ručního kopírování a vkládání.

## Závěr

Nyní jste se naučili, jak **vytvořit referenční rozsah kontingenční tabulky**, **exportovat obrázek kontingenční tabulky** a **uložit rozsah Excelu jako png** pomocí Aspose.Cells v C#. Hlavní body jsou:

- Použijte `PivotTable.CreateReferenceRange()` k izolaci vizuální oblasti kontingenční tabulky.  
- Převěďte tento rozsah na obrázek pomocí `Range.ToImage()`.  
- Uložte obrázek jako PNG, případně upravte DPI pro tiskovou kvalitu.

Odtud můžete zkoumat hromadný export, různé formáty obrázků (SVG, JPEG) nebo dokonce vložení PNG do PDF či Word dokumentů. Možnosti jsou neomezené, jakmile máte kontingenční tabulku zachycenou jako statický grafický prvek.

Máte otázky nebo složitý scénář? Zanechte komentář níže a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}