---
category: general
date: 2026-11-22
description: Naplnit šablonu Excel pomocí Aspose.Cells k vytvoření více listů, uložit
  workbook Aspose a vytvořit master‑detail report v C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- populate excel template
- generate multiple sheets
- save aspose workbook
- generate master detail report
language: cs
lastmod: 2026-11-22
og_description: naplnit šablonu Excel pomocí Aspose.Cells, vygenerovat více listů,
  uložit workbook Aspose a vytvořit master‑detail report v jediném C# programu.
og_image_alt: Screenshot showing a populated Excel workbook with multiple detail sheets
og_title: Vyplňte šablonu Excel a vytvořte více listů pomocí Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: populate excel template using Aspose.Cells to generate multiple sheets,
    save aspose workbook, and create a master‑detail report in C#.
  headline: How to populate Excel template and generate multiple sheets with Aspose.Cells
  type: TechArticle
- description: populate excel template using Aspose.Cells to generate multiple sheets,
    save aspose workbook, and create a master‑detail report in C#.
  name: How to populate Excel template and generate multiple sheets with Aspose.Cells
  steps:
  - name: What the resulting workbook looks like
    text: '| Sheet name | Content | |------------|----------| | **Master** | Header
      row with order summary (OrderId, Customer) | | **Details_1** | All `OrderLines`
      where `OrderId = 1` (Pen, Notebook) | | **Details_2** | All `OrderLines` where
      `OrderId = 2` (Pencil) |'
  - name: Expected output
    text: 'Open `MasterDetailResult.xlsx` and you will see:'
  - name: Next steps
    text: '* Explore **SmartMarkerOptions** such as `EnableFormulaCalculation` to
      evaluate formulas after data insertion. * Add charts to the master sheet and
      let the processor update series ranges automatically. * Combine this approach
      with **Aspose.Slides** to export the same data to PowerPoint presentations'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak naplnit šablonu Excel a vytvořit více listů pomocí Aspose.Cells
url: /cs/net/templates-reporting/how-to-populate-excel-template-and-generate-multiple-sheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak naplnit šablonu Excel a vygenerovat více listů pomocí Aspose.Cells

Pokud potřebujete **naplnit šablonu Excel** dynamickými daty, tento průvodce vám ukáže kompletní, připravené řešení. Pomocí Smart Marker enginu Aspose.Cells můžete **vytvořit více listů**, uložit **sešit Aspose**, a vytvořit kompletní **master‑detail report** bez ručního kopírování nebo VBA maker.

Tutoriál vás provede každým krokem – od přípravy master‑detail kolekcí až po uložení finálního souboru – takže můžete kód zkopírovat do svého projektu a okamžitě vidět výsledek.

## Požadavky

* .NET 6.0 nebo novější (kód také funguje s .NET Framework 4.7+)
* Aspose.Cells pro .NET nainstalováno (`dotnet add package Aspose.Cells`)
* Základní vývojové prostředí C# (Visual Studio, VS Code, Rider, atd.)
* Šablona Excel (`MasterDetailTemplate.xlsx`), která obsahuje Smart Marker značky jako `&=Orders.OrderId` a detailní tabulku označenou `&=OrderLines`.

> **Tip:** Uchovávejte šablonu ve stejné složce jako projekt nebo použijte absolutní cestu, aby se předešlo `FileNotFoundException`.

## Přehled řešení

1. **Připravit master‑detail datové kolekce** – zdrojové objekty, které naplňují report.  
2. **Načíst šablonu Excel**, která již obsahuje Smart Marker zástupné značky.  
3. **Vytvořit `SmartMarkerProcessor`** pro interpretaci značek.  
4. **Aplikovat data** a nechat Aspose.Cells **automaticky vygenerovat více listů**.  
5. **Uložit sešit Aspose** na disk.

Každý krok je podrobně vysvětlen níže, s kompletním kódem a očekávaným výstupem.

![příklad naplnění šablony Excel](https://example.com/images/populate-excel-template.png "příklad naplnění šablony Excel")

## Krok 1: Připravit master‑detail datové kolekce

Master‑detail reporty se opírají o dvě související kolekce: seznam objednávek (master) a seznam řádků objednávek (detail). Smart Marker engine přiřazuje řádky podle pole `OrderId`.

```csharp
using System.Collections.Generic;

// Master collection – one record per order
var orders = new List<object>
{
    new { OrderId = 1, Customer = "Alice" },
    new { OrderId = 2, Customer = "Bob" }
};

// Detail collection – multiple rows per order
var orderLines = new List<object>
{
    new { OrderId = 1, Item = "Pen",      Qty = 10 },
    new { OrderId = 1, Item = "Notebook", Qty = 5  },
    new { OrderId = 2, Item = "Pencil",   Qty = 20 }
};
```

**Proč je to důležité:**  
`SmartMarkerProcessor` prohledává šablonu na značky jako `&=Orders.OrderId` a `&=OrderLines.Item`. Poskytnutím dvou samostatných kolekcí Aspose.Cells automaticky vytvoří nový list pro každý master záznam a vyplní detailní řádky odpovídajícím způsobem.

## Krok 2: Načíst šablonu Excel, která obsahuje Smart Markery

Šablona obsahuje rozvržení, formátování a zástupné značky. Ujistěte se, že název souboru a cesta jsou správné.

```csharp
using Aspose.Cells;

// Adjust the path to where you stored the template
string templatePath = @"YOUR_DIRECTORY\MasterDetailTemplate.xlsx";
Workbook workbook = new Workbook(templatePath);
```

**Proč je to důležité:**  
Načtením šablony získá procesor objekt sešitu, který již ví, kam data vložit. Veškeré formátování (písma, okraje, vzorce) zůstává zachováno, takže vygenerovaný report vypadá profesionálně bez dalšího kódu pro stylování.

## Krok 3: Vytvořit SmartMarkerProcessor

Procesor je engine, který nahrazuje značky skutečnými hodnotami.

```csharp
// Initialise the processor with the loaded workbook
var processor = new SmartMarkerProcessor(workbook);
```

**Proč je to důležité:**  
`SmartMarkerProcessor` odděluje logiku Smart Marker od zbytku sešitu, což vám umožní znovu použít stejný sešit pro další operace (např. grafy) po aplikaci dat.

## Krok 4: Aplikovat master‑detail data a vygenerovat více listů

Zde svázeme dvě kolekce s procesorem a řekneme Aspose.Cells, jak pojmenovat každý vygenerovaný list.

```csharp
using Aspose.Cells.SmartMarkers;

// Combine the collections into an anonymous object matching the marker names
var data = new { Orders = orders, OrderLines = orderLines };

// Options let you control sheet naming and other behaviours
var options = new SmartMarkerOptions
{
    // {0} will be replaced by the master record index (1‑based)
    DetailSheetNewName = "Details_{0}"
};

// Apply the data – this step creates a new sheet for each order
processor.ApplyTemplate(data, options);
```

**Proč je to důležité:**  
Vzor `DetailSheetNewName` vytváří listy pojmenované `Details_1`, `Details_2` atd., odpovídající každé objednávce v master kolekci. Toto automatické generování listů je jádrem **vytváření více listů** bez ručního procházení sešitu.

### Jak vypadá výsledný sešit

| Název listu | Obsah |
|------------|----------|
| **Master** | Řádek hlavičky s přehledem objednávek (OrderId, Customer) |
| **Details_1** | Všechny `OrderLines`, kde `OrderId = 1` (Pen, Notebook) |
| **Details_2** | Všechny `OrderLines`, kde `OrderId = 2` (Pencil) |

Master list může být také naplněn přidáním Smart Marker tabulky, která iteruje přes `Orders`. Detailní listy jsou vytvořeny automaticky procesorem.

## Krok 5: Uložit sešit Aspose

Nakonec zapíšete naplněný sešit do nového souboru.

```csharp
// Choose the output path – ensure the folder exists
string resultPath = @"YOUR_DIRECTORY\MasterDetailResult.xlsx";
workbook.Save(resultPath);
```

**Proč je to důležité:**  
Volání `Save` zapíše sešit v paměti do fyzického souboru `.xlsx`, čímž dokončuje krok **uložit sešit Aspose**. Soubor lze otevřít v Excelu, Google Sheets nebo jakémkoli prohlížeči podporujícím formát OpenXML.

### Očekávaný výstup

Otevřete `MasterDetailResult.xlsx` a uvidíte:

* **List “Master”** – tabulka uvádějící Order 1 (Alice) a Order 2 (Bob).  
* **List “Details_1”** – dva řádky: Pen (10) a Notebook (5).  
* **List “Details_2”** – jeden řádek: Pencil (20).

Veškeré formátování z původní šablony (barvy hlavičky, šířky sloupců, formáty čísel) je zachováno.

## Řešení běžných okrajových případů

| Situace | Doporučený přístup |
|-----------|----------------------|
| **Šablona nenalezena** | Zabalte volání `new Workbook(...)` do `try/catch` a zaznamenejte `FileNotFoundException`. |
| **Velké datové sady (10 000+ řádků)** | Zvyšte `SmartMarkerOptions.MaxRowsPerSheet`, pokud potřebujete více řádků na list, nebo stránkujte ručně. |
| **Vlastní pojmenování listů** | Použijte formátovací řetězec jako `DetailSheetNewName = "Order_{0}_{1}"`, kde `{1}` může být vlastnost z master záznamu (např. `Customer`). |
| **Podmíněné formátování podle objednávky** | Přidejte pravidlo podmíněného formátování do šablony, které odkazuje na značku (např. `&=Orders.Status`) a nechte procesor ji vyhodnotit. |

## Kompletní spustitelný program

Níže je kompletní C# konzolová aplikace, která spojuje všechny části. Nahraďte `YOUR_DIRECTORY` skutečnou cestou ke složce na vašem počítači.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class SmartMarkerDetailSheetDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Prepare master‑detail data collections
        // -------------------------------------------------
        var orders = new List<object>
        {
            new { OrderId = 1, Customer = "Alice" },
            new { OrderId = 2, Customer = "Bob" }
        };

        var orderLines = new List<object>
        {
            new { OrderId = 1, Item = "Pen",      Qty = 10 },
            new { OrderId = 1, Item = "Notebook", Qty = 5  },
            new { OrderId = 2, Item = "Pencil",   Qty = 20 }
        };

        // -------------------------------------------------
        // Step 2: Load the template workbook that contains smart markers
        // -------------------------------------------------
        string templatePath = @"YOUR_DIRECTORY\MasterDetailTemplate.xlsx";
        Workbook workbook = new Workbook(templatePath);

        // -------------------------------------------------
        // Step 3: Create a SmartMarkerProcessor to handle the template
        // -------------------------------------------------
        var processor = new SmartMarkerProcessor(workbook);

        // -------------------------------------------------
        // Step 4: Apply the master‑detail data and generate multiple sheets
        // -------------------------------------------------
        var data = new { Orders = orders, OrderLines = orderLines };
        var options = new SmartMarkerOptions
        {
            DetailSheetNewName = "Details_{0}"
        };

        processor.ApplyTemplate(data, options);

        // -------------------------------------------------
        // Step 5: Save the populated Aspose workbook
        // -------------------------------------------------
        string resultPath = @"YOUR_DIRECTORY\MasterDetailResult.xlsx";
        workbook.Save(resultPath);

        Console.WriteLine($"Report generated successfully: {resultPath}");
    }
}
```

Spusťte program (`dotnet run` nebo `Ctrl+F5` ve Visual Studiu). Po dokončení otevřete `MasterDetailResult.xlsx` a ověřte, že **naplnění šablony Excel** vytvořilo očekávaný master‑detail report s **více listy**.

## Závěr

Nyní víte, jak **naplnit šablonu Excel** pomocí Aspose.Cells, **vytvořit více listů**, **uložit sešit Aspose** a vytvořit robustní **master‑detail report** během několika řádků C#. Smart Marker engine odstraňuje potřebu ručních smyček, zachovává vaše formátování a snadno škáluje na větší datové sady.

### Další kroky

* Prozkoumejte **SmartMarkerOptions**, například `EnableFormulaCalculation`, pro vyhodnocení vzorců po vložení dat.  
* Přidejte grafy do master listu a nechte procesor automaticky aktualizovat rozsahy sérií.  
* Kombinujte tento přístup s **Aspose.Slides** pro export stejných dat do PowerPoint prezentací.

Neváhejte experimentovat s různými rozvrženími šablon, vlastními vzory pojmenování listů nebo dalšími detailními kolekcemi. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Vytvořit master detail report v C# – Naplnit šablonu Excel pomocí SmartMarker](/cells/english/net/smart-markers-dynamic-data/create-master-detail-report-in-c-populate-excel-template-wit/)
- [Jak generovat Excel ze šablony pomocí C# a Aspose.Cells](/cells/english/net/templates-reporting/how-to-generate-excel-from-template-with-c-and-aspose-cells/)
- [Aspose Cells Smart Markers – Naplnit šablonu Excel](/cells/english/java/templates-reporting/aspose-cells-smart-markers-populate-excel-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}