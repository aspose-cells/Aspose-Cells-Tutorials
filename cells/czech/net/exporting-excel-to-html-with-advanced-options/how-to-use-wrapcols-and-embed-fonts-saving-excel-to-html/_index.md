---
category: general
date: 2026-10-20
description: Naučte se, jak používat wrapcols v Aspose.Cells, vkládat písma do HTML
  a ukládat Excel jako HTML s kompletním příkladem v C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- embed fonts in html
- save excel as html
- convert workbook to html
- use wrapcols function
language: cs
lastmod: 2026-10-20
og_description: Jak používat wrapcols v Aspose.Cells, vkládat písma do HTML a převádět
  sešit do HTML s jasným průvodcem v C# pro vývojáře.
og_image_alt: Screenshot of an Excel workbook saved as HTML with embedded fonts using
  Aspose.Cells
og_title: Jak používat wrapcols a vkládat písma při exportu Excelu do HTML
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to use wrapcols in Aspose.Cells, embed fonts in HTML, and
    save Excel as HTML with a complete C# example.
  headline: How to use wrapcols and embed fonts saving Excel to HTML
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel to HTML
- Smart Markers
title: Jak použít wrapcols a vložit písma při ukládání Excelu do HTML
url: /cs/net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat wrapcols a vložit písma při ukládání Excelu do HTML

Pokud potřebujete **jak používat wrapcols** ve vzorci Aspose.Cells, tento průvodce vám ukáže přesné kroky. Také se naučíte, jak **vložit písma do HTML** a **uložit Excel jako HTML**, aby výstup vypadal na všech prohlížečích identicky.  

Tutoriál pokrývá tři praktické scénáře: použití funkce `WRAPCOLS`, export sešitu s vloženými písmy a generování reportu master‑detail s pomocí Smart Markers. Na konci budete mít jeden spustitelný program v C#, který demonstruje všechny tyto funkce.

## Požadavky

* .NET 6.0 (nebo novější) nainstalováno.
* Aspose.Cells pro .NET přidáno do vašeho projektu (`dotnet add package Aspose.Cells`).
* Základní znalost C# a Excelových vzorců.

Žádné další knihovny třetích stran nejsou vyžadovány; Aspose.Cells interně zpracovává konverzi do HTML a vkládání písem.

## Krok 1: Ukázka funkce **jak používat wrapcols** ve vzorci

Funkce `WRAPCOLS` rozdělí jednorozměrný rozsah na dvourozměrné pole, přičemž nejprve vyplní sloupce. To je užitečné, když potřebujete přetvořit data pro reportování nebo tvorbu grafů.

```csharp
using Aspose.Cells;
using System;

class WrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Populate a vertical range A1:A3
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // Apply WRAPCOLS(A1:A3, 2) – this creates a 2‑column array {1,2}
        sheet.Cells["B1"].Formula = "=WRAPCOLS(A1:A3, 2)";

        // Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // Output the result to verify the function works
        Console.WriteLine("Result of WRAPCOLS: " + sheet.Cells["B1"].Value);
        // Expected output: Result of WRAPCOLS: 1
    }
}
```

**Proč to funguje:**  
`WRAPCOLS` přijímá dva argumenty – zdrojový rozsah a počet sloupců. Funkce vyplní pole po sloupcích a zahodí přebytečné hodnoty (v příkladu `3`). Výsledek se zobrazí v levém horním buňce cílového rozsahu (`B1`) a můžete rozsah ručně rozšířit, pokud potřebujete celé pole.

> **Tip:** Po nastavení vzorce zavolejte `workbook.CalculateFormula()`, aby byl výsledek aktuální před čtením hodnot buněk.

## Krok 2: **Převést sešit do HTML** a **vložit písma do html**

Při exportu souboru Excel do HTML jsou písma často nahrazována výchozími písmy prohlížeče, což může narušit vizuální rozvržení. Aspose.Cells vám umožní vložit přesná písma použité v sešitu přímo do souboru HTML.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for HtmlSaveOptions
using System;

class HtmlExportDemo
{
    static void Main()
    {
        // Re‑use the workbook from the previous step
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue("Hello");
        sheet.Cells["A2"].PutValue("World");

        // Configure HTML save options
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Embedding fonts ensures the output looks the same on any device
            EmbedFonts = true,
            // Optional: specify a folder for supporting files (images, CSS)
            ExportEmbeddedImages = true
        };

        // Save the workbook as an HTML file with embedded fonts
        string outputPath = @"C:\Temp\WorkbookWithFonts.html";
        workbook.Save(outputPath, htmlOptions);

        Console.WriteLine($"Workbook saved to HTML with embedded fonts at: {outputPath}");
    }
}
```

**Proč je vkládání písem důležité:**  
Když je `EmbedFonts` nastaveno na `true`, Aspose.Cells převádí každé použité TrueType/OpenType písmo na Base64‑kódované pravidlo `@font-face` uvnitř generovaného HTML. Tím se eliminuje potřeba, aby klientský počítač měl stejná písma nainstalována, a zajišťuje pixel‑dokonalé vykreslení.

> **Speciální případ:** Pokud se zdrojový sešit odkazuje na písmo, které není nainstalováno na serveru, Aspose.Cells použije výchozí písmo a zobrazí varování. Ujistěte se, že požadovaná písma jsou k dispozici.

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak používat WRAPCOLS v C# – Vytvořit Excel sešit s funkcemi Wrap](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Jak vložit písma do HTML – Převést Excel do HTML pomocí C#](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/)
- [Jak převést soubory Excel do HTML pomocí Aspose.Cells pro .NET: Skrytí překrytého obsahu](/cells/english/net/workbook-operations/excel-to-html-hide-overlaid-content-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}