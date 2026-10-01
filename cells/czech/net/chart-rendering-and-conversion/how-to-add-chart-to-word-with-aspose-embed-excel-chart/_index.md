---
category: general
date: 2026-10-01
description: Přidejte graf do Wordu pomocí Aspose během několika minut. Naučte se
  vložit graf z Excelu do Wordu, exportovat graf z Excelu do Wordu, vytvořit Word
  dokument pomocí Aspose a uložit graf ve Word dokumentu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add chart to word
- embed excel chart word
- export chart excel word
- create word document aspose
- save chart word document
language: cs
lastmod: 2026-10-01
og_description: Přidejte graf do Wordu pomocí Aspose během několika minut. Tento návod
  ukazuje, jak vložit graf z Excelu do Wordu, exportovat graf z Excelu do Wordu, vytvořit
  dokument Word pomocí Aspose a uložit graf v dokumentu Word.
og_image_alt: Screenshot illustrating how to add chart to Word using Aspose
og_title: Přidejte graf do Wordu pomocí Aspose – vložte Excel graf
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  headline: How to add chart to Word with Aspose – embed Excel chart
  type: TechArticle
- description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  name: How to add chart to Word with Aspose – embed Excel chart
  steps:
  - name: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
    text: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
  - name: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
    text: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
  - name: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
    text: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
  - name: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
    text: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
  - name: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
    text: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
  type: HowTo
tags:
- Aspose
- C#
- Word automation
title: Jak přidat graf do Wordu pomocí Aspose – vložit graf z Excelu
url: /cs/net/chart-rendering-and-conversion/how-to-add-chart-to-word-with-aspose-embed-excel-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak přidat graf do Wordu pomocí Aspose – vložit graf z Excelu

Pokud potřebujete rychle **přidat graf do Wordu**, tento tutoriál vám poskytne kompletní, připravené řešení. Uvidíte, jak vložit graf z Excelu do souboru Word, exportovat graf z Excelu do Wordu a nakonec **uložit dokument Word s grafem** pomocí několika řádků C#.

Vkládání grafů je běžnou požadavkem při programovém generování zpráv, faktur nebo dashboardů. Na konci tohoto návodu budete schopni **create Word document Aspose** obsahující jakýkoli graf z Excel sešitu, bez ručního kopírování a vkládání.

## Požadavky

- .NET 6.0 nebo novější (kód také funguje s .NET Framework 4.7+)
- NuGet balíčky Aspose.Cells a Aspose.Words (nainstalujte pomocí `dotnet add package Aspose.Cells` a `dotnet add package Aspose.Words`)
- Existující Excel soubor (`Chart.xlsx`), který obsahuje alespoň jeden graf
- Vývojové prostředí, např. Visual Studio 2022 nebo VS Code

## Přidat graf do Wordu pomocí Aspose

Níže je kompletní, samostatný program. Zkopírujte jej do nového konzolového projektu, obnovte balíčky a spusťte jej. Program načte Excel sešit, vytvoří Word dokument, vloží první graf a uloží výsledek.

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

namespace AddChartToWordDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the Excel workbook that contains the chart
            var workbookPath = @"YOUR_DIRECTORY\Chart.xlsx";
            var workbook = new Workbook(workbookPath);

            // Step 2: Create a new Word document that will receive the chart
            var wordDoc = new Document();

            // Step 3: Initialise a DocumentBuilder for the Word document
            var builder = new DocumentBuilder(wordDoc);

            // Step 4: Insert the first chart from the first worksheet into the Word document
            // This uses Aspose.Words' InsertChart overload that accepts an Aspose.Cells chart object
            builder.InsertChart(workbook.Worksheets[0].Charts[0]);

            // Step 5: Save the resulting Word document
            var outputPath = @"YOUR_DIRECTORY\Chart.docx";
            wordDoc.Save(outputPath);

            Console.WriteLine($"Chart successfully added and saved to '{outputPath}'.");
        }
    }
}
```

### Proč je každý řádek důležitý

1. **Loading the workbook** – `Workbook` parsuje Excel soubor a poskytuje programový přístup k jeho listům a grafům.  
2. **Creating the Word document** – `Document` je vstupní bod Aspose.Words pro jakýkoli úkol zpracování Wordu.  
3. **DocumentBuilder** – Tato pomocná třída vám umožňuje vkládat obsah (text, obrázky, grafy) na aktuální pozici kurzoru.  
4. **InsertChart** – Přetížení, které přijímá objekt `Aspose.Cells.Chart`, kopíruje data grafu, formátování a řady přímo do souboru Word. Není vyžadována žádná mezilehlá konverze obrázku, což zachovává vektorovou kvalitu.  
5. **Save** – `Save` zapíše .docx balíček na disk, čímž dokončuje krok **save chart word document**.

#### Očekávaný výstup

Po spuštění programu otevřete `Chart.docx`. Uvidíte přesně ten graf, který byl uložen v `Chart.xlsx`, umístěný tam, kde byl builder umístěn (na začátku dokumentu). Graf zůstává v Wordu plně editovatelný (můžete měnit velikost, barvy nebo upravit zdroj dat).

## Vložit graf z Excelu do Wordu

Pokud potřebujete vložit více než jeden graf, opakujte volání `InsertChart` pro každý objekt grafu. Například pro vložení všech grafů z prvního listu:

```csharp
var sheet = workbook.Worksheets[0];
foreach (Chart chart in sheet.Charts)
{
    builder.InsertChart(chart);
    builder.Writeln(); // add a line break between charts
}
```

**Pro tip:** Použijte `builder.Writeln()` k vložení odstavcové zarážky, aby každý graf začínal na novém řádku.

## Export grafu z Excelu do Wordu – zpracování více listů

Když jsou grafy rozloženy na několika listech, iterujte přes kolekci `Worksheets` sešitu:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    foreach (Chart chart in ws.Charts)
    {
        builder.InsertChart(chart);
        builder.Writeln();
    }
}
```

Tento přístup **export chart Excel Word** pro jakékoli rozložení sešitu, což činí řešení robustním pro složité zprávy.

## Vytvořit Word dokument Aspose – přizpůsobení vzhledu

Můžete řídit velikost a pozici každého vloženého grafu úpravou objektu `Shape`, který vrací `InsertChart`:

```csharp
Shape chartShape = builder.InsertChart(chart);
chartShape.Width = 500;   // width in points
chartShape.Height = 300;  // height in points
chartShape.WrapType = WrapType.Inline; // make the chart flow with text
```

Nastavení `WrapType` na `Inline` zajistí, že se graf chová jako běžný odstavec, což je často žádoucí pro automatizovanou generaci dokumentů.

## Uložit dokument Word s grafem – osvědčené postupy

- **Použijte popisný název souboru** (`Report_Q1_2026.docx`) pro usnadnění verzování.
- **Uvolněte objekty** po dokončení, zejména ve velkých dávkových procesech:

```csharp
wordDoc.Dispose();
workbook.Dispose();
```

- **Ověřte výsledek** programově, pokud generujete mnoho souborů:

```csharp
if (System.IO.File.Exists(outputPath))
{
    Console.WriteLine("File saved successfully.");
}
else
{
    Console.Error.WriteLine("Failed to save the document.");
}
```

## Časté otázky a okrajové případy

| Question | Answer |
|----------|--------|
| *Mohu vložit graf, který není první na listu?* | Ano. Přistupujte k němu pomocí indexu: `sheet.Charts[2]` pro třetí graf. |
| *Co když Excel graf používá zdroj dat, který není v sešitu?* | Aspose.Cells vloží data přímo do objektu grafu, takže graf zůstane funkční i po odstranění zdrojového rozsahu. |
| *Potřebuji licenci pro Aspose?* | Bezplatná zkušební verze funguje, ale licencovaná verze odstraňuje vodoznak hodnocení a odemyká všechny funkce. |
| *Bude graf po vložení v Wordu editovatelný?* | Graf je vložen jako nativní Word graf, takže uživatelé mohou upravovat řady, názvy a styly pomocí rozhraní Wordu. |
| *Jak vložit graf jako obrázek místo nativního grafu?* | Použijte `builder.InsertImage(chart.ToImage())` pro vložení rastrového obrázku. To je užitečné, pokud chcete zachovat přesné vizuální zobrazení bez editovatelnosti na úrovni Wordu. |

## Kompletní funkční příklad (kopíruj‑vložit)

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

class AddChartToWord
{
    static void Main()
    {
        // Load Excel workbook
        var wb = new Workbook(@"C:\Data\Chart.xlsx");

        // Create Word document
        var doc = new Document();
        var builder = new DocumentBuilder(doc);

        // Insert every chart from every worksheet
        foreach (Worksheet ws in wb.Worksheets)
        {
            foreach (Chart ch in ws.Charts)
            {
                Shape shape = builder.InsertChart(ch);
                shape.Width = 500;
                shape.Height = 300;
                builder.Writeln(); // separate charts
            }
        }

        // Save the document
        var outPath = @"C:\Data\ReportWithCharts.docx";
        doc.Save(outPath);
        Console.WriteLine($"Document saved to {outPath}");
    }
}
```

Spuštěním kódu vznikne Word soubor (`ReportWithCharts.docx`), který obsahuje výsledky **add chart to word** pro každý graf ve zdrojovém sešitu.

## Závěr

Nyní víte, jak **add chart to Word** pomocí Aspose.Cells a Aspose.Words, jak **embed Excel chart word**, **export chart Excel Word**, **create Word document Aspose**, a nakonec **save chart word document**. Tento přístup funguje pro scénáře s jedním grafem i pro složité sešity s mnoha grafy napříč více listy.

Další kroky, které můžete prozkoumat:

- [Jak uložit DOCX z Excelu – Kompletní průvodce exportem grafů do Wordu](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-docx-from-excel-complete-guide-to-export-charts/)
- [Vytvořit Excel sešit s koláčovým grafem pomocí Aspose.Cells .NET – komplexní průvodce](/cells/english/net/charts-graphs/create-excel-workbook-pie-chart-aspose-cells-net/)
- [Vytvořit bublinový graf v Excelu pomocí Aspose.Cells .NET&#58; krok za krokem průvodce](/cells/english/net/charts-graphs/create-bubble-chart-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}