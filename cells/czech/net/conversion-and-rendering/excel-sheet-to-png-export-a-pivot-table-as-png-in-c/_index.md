---
category: general
date: 2026-03-18
description: Návod na převod listu Excel do PNG, ukazující, jak exportovat kontingenční
  tabulku, nastavit tiskovou oblast kontingenční tabulky a exportovat obrázek rozsahu
  v Excelu pomocí Aspose.Cells.
draft: false
keywords:
- excel sheet to png
- how to export pivot
- set print area pivot
- export excel range image
- export worksheet to image
language: cs
og_description: Návod na převod listu Excel do PNG, který vás provede exportem kontingenčních
  tabulek, nastavením tiskové oblasti kontingenční tabulky a exportem obrázku rozsahu
  v Excelu pomocí C#.
og_title: Excelový list do PNG – Kompletní průvodce exportem kontingenčních tabulek
tags:
- Aspose.Cells
- C#
- Excel automation
title: excelový list do png – Exportovat kontingenční tabulku jako PNG v C#
url: /cs/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# excel sheet to png – Exportovat kontingenční tabulku jako PNG v C#

Už jste někdy potřebovali převést **excel sheet to png**, ale nebyli jste si jisti, jak zachytit jen samotnou kontingenční tabulku? Nejste v tom sami. V mnoha reportovacích pipelinech je vizualizace kontingenční tabulky hvězdou a export do PNG vám umožní vložit ji do e‑mailů, dashboardů nebo dokumentace, aniž byste museli přenášet celý sešit.

V tomto průvodci vám ukážeme **jak exportovat pivot**, **nastavit tiskovou oblast pivot**, a nakonec **export excel range image**, takže získáte čistý soubor **export worksheet to image**. Žádné tajemné odkazy na externí dokumentaci – jen kompletní, spustitelný úryvek kódu a vysvětlení každého řádku.

## Co budete potřebovat

- **Aspose.Cells for .NET** (NuGet balíček `Aspose.Cells` – verze 23.12 nebo novější).  
- Vývojové prostředí .NET (Visual Studio, Rider nebo `dotnet` CLI).  
- Excel soubor (`input.xlsx`) obsahující alespoň jednu kontingenční tabulku.

To je vše. Pokud to máte, pojďme se ponořit.

## Krok 1 – Načtení sešitu a získání první listu

Než se můžeme dotknout kontingenční tabulky, potřebujeme mít sešit v paměti.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

namespace PivotToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"C:\Data\input.xlsx");

            // Get the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];
```

*Proč je to důležité:* Načtení souboru nám poskytuje přístup ke všem objektům (tabulky, grafy, pivoty). Použití první listu je jednoduchý výchozí nastavení; pokud potřebujete, můžete `0` nahradit skutečným indexem nebo názvem listu.

## Krok 2 – Získání rozsahu kontingenční tabulky

Kontingenční tabulka žije uvnitř bloku buněk. Potřebujeme tento blok, abychom Excelu řekli, co má tisknout.

```csharp
            // Assume the first pivot table on the sheet
            PivotTable pivot = worksheet.PivotTables[0];

            // The range that the pivot occupies (e.g., A1:D20)
            CellArea pivotRange = pivot.PivotTableRange;
```

*Proč to děláme:* `PivotTableRange` nám udává přesné počáteční a koncové řádky/sloupce. Bez něj by export zahrnoval celý list, což by zmařilo účel **set print area pivot**.

## Krok 3 – Definování tiskové oblasti, aby byl vykreslen jen kontingenční tabulka

Tiskový engine Excelu respektuje vlastnost `PrintArea`. Zúžením na kontingenční tabulku se vyhneme zbytečným datům nebo prázdným buňkám.

```csharp
            // Build the address string: "StartRow,StartColumn:EndRow,EndColumn"
            string printArea = $"{pivotRange.StartRow},{pivotRange.StartColumn}:" +
                               $"{pivotRange.EndRow},{pivotRange.EndColumn}";

            worksheet.PageSetup.PrintArea = printArea;
```

*Tip:* Pokud máte na stejném listu více kontingenčních tabulek, můžete jejich rozsahy sloučit pomocí seznamu odděleného čárkami (`"0,0:10,5,12,0:22,5"`). To je technika **export excel range image** pro několik bloků.

## Krok 4 – Nastavení možností exportu obrázku (formát PNG)

Aspose.Cells vám umožňuje jemně doladit výstup. PNG je bezztrátový, ideální pro ostré vizuály kontingenčních tabulek.

```csharp
            // Configure image export options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: increase resolution for sharper output
                HorizontalResolution = 300,
                VerticalResolution = 300
            };
```

*Proč PNG?* Na rozdíl od JPEG zachovává PNG ostrost textu a průhledná pozadí, což ho činí preferovaným pro scénáře **excel sheet to png**.

## Krok 5 – Export listu (oblast kontingenční tabulky) do souboru PNG

Nyní se děje magie – vykreslíme definovanou tiskovou oblast do obrázku.

```csharp
            // Export the first page (index 0) of the worksheet to an image
            // The page corresponds to the print area we set earlier
            worksheet.ToImage(0, imgOptions).Save(@"C:\Data\pivot.png");

            // Inform the user
            System.Console.WriteLine("Pivot exported to PNG successfully!");
        }
    }
}
```

*Co uvidíte:* Soubor `pivot.png`, který obsahuje jen kontingenční tabulku, bez dalších řádků nebo sloupců. Otevřete jej v libovolném prohlížeči obrázků a získáte připravený vizuál ke sdílení.

---

## Často kladené otázky a okrajové případy

### Co když sešit obsahuje **více kontingenčních tabulek**?

Získejte `PivotTableRange` každé kontingenční tabulky, sloučte rozsahy a přiřaďte spojený řetězec k `PrintArea`. Příklad:

```csharp
string combinedArea = "";
foreach (PivotTable pt in worksheet.PivotTables)
{
    CellArea ca = pt.PivotTableRange;
    combinedArea += $"{ca.StartRow},{ca.StartColumn}:{ca.EndRow},{ca.EndColumn},";
}
combinedArea = combinedArea.TrimEnd(','); // Remove trailing comma
worksheet.PageSetup.PrintArea = combinedArea;
```

### Můžu exportovat do **jiných formátů obrázků**?

Určitě. Změňte `imgOptions.ImageFormat = ImageFormat.Jpeg;` (nebo `Bmp`, `Gif`, `Tiff`). Jen pamatujte, že JPEG zavádí kompresní artefakty – obvykle není ideální pro textově náročné pivoty.

### Jak zacházet s **velkými kontingenčními tabulkami**, které se rozprostírají na více stránkách?

Nastavte `imgOptions.OnePagePerSheet = false;`, aby se povolilo vícestránkové vykreslování, a poté projděte stránky ve smyčce:

```csharp
int pageCount = worksheet.PageCount;
for (int i = 0; i < pageCount; i++)
{
    worksheet.ToImage(i, imgOptions).Save($@"C:\Data\pivot_page{i + 1}.png");
}
```

### Co s **skrytými řádky/sloupci**?

Aspose respektuje nastavení viditelnosti listu. Pokud potřebujete ignorovat skryté prvky, dočasně je odhalte před exportem nebo ručně upravte `PrintArea`.

---

## Kompletní funkční příklad (připravený ke kopírování a vložení)

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

namespace PivotToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook & select sheet
            Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Get the first pivot table's range
            PivotTable pivot = worksheet.PivotTables[0];
            CellArea pivotRange = pivot.PivotTableRange;

            // 3️⃣ Set print area to the pivot only
            string printArea = $"{pivotRange.StartRow},{pivotRange.StartColumn}:" +
                               $"{pivotRange.EndRow},{pivotRange.EndColumn}";
            worksheet.PageSetup.PrintArea = printArea;

            // 4️⃣ Prepare PNG export options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // 5️⃣ Export to PNG
            worksheet.ToImage(0, imgOptions).Save(@"C:\Data\pivot.png");

            System.Console.WriteLine("✅ Pivot exported to PNG at C:\\Data\\pivot.png");
        }
    }
}
```

Spusťte program a najdete `pivot.png` přesně tam, kam jste ukázali. Otevřete soubor – měli byste vidět ostrý výstup jen kontingenční tabulky, nic jiného.

---

## Závěr

Nyní máte **kompletní, end‑to‑end řešení** pro převod **excel sheet to png**, které se zaměřuje výhradně na kontingenční tabulku. Nastavením **print area pivot**, konfigurací **image export options** a použitím metody `ToImage` z Aspose.Cells můžete automatizovat generování reportů, vkládat vizuály na webové stránky nebo jednoduše archivovat snímky analytiky.

Co dál? Vyzkoušejte výměnu PNG za vysoké rozlišení PDF (`ImageFormat.Pdf`), experimentujte s více pivoty na jednom listu nebo zkombinujte tento přístup s exportem grafů pro plnohodnotný exportní pipeline dashboardu.

Máte vlastní tip, který byste chtěli sdílet? Zanechte komentář, nebo se pusťte do dalšího tutoriálu, kde prozkoumáme **export worksheet to image** pro snímky celých listů, včetně grafů a podmíněného formátování. Šťastné kódování!  

<img src="pivot.png" alt="excel sheet to png example of pivot table export">

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}