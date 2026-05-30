---
category: general
date: 2026-05-30
description: Rychle vyplňte šablonu Excelu a naučte se, jak naplnit Excel daty pomocí
  Aspose.Cells SmartMarker. Kompletní průvodce v C# s spustitelným kódem.
draft: false
keywords:
- populate excel template
- fill excel with data
- Aspose.Cells SmartMarker
- automate Excel reporting
- C# Excel automation
language: cs
og_description: Vyplňte šablonu Excel a naplňte Excel daty pomocí Aspose.Cells SmartMarker.
  Postupujte podle tohoto krok‑po‑kroku C# tutoriálu pro okamžité výsledky.
og_title: Naplnit šablonu Excel – Vyplnit data v Excelu pomocí SmartMarkeru
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Populate Excel template quickly and learn how to fill Excel with data
    using Aspose.Cells SmartMarker. Complete C# guide with runnable code.
  headline: Populate Excel Template – Fill Excel Data via SmartMarker
  type: TechArticle
- description: Populate Excel template quickly and learn how to fill Excel with data
    using Aspose.Cells SmartMarker. Complete C# guide with runnable code.
  name: Populate Excel Template – Fill Excel Data via SmartMarker
  steps:
  - name: Empty Collections
    text: 'If `Items` is empty, SmartMarker will leave the table header intact but
      won’t insert any rows. To avoid a blank space, you can add a conditional block:'
  - name: Custom Number Formats
    text: 'Sometimes you need currency symbols or thousands separators. After processing,
      you can apply a style programmatically:'
  - name: Large Data Sets
    text: 'For thousands of rows, enable the `UseFastMode` option to improve performance:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Vyplnit šablonu Excel – Vyplnit data v Excelu pomocí SmartMarkeru
url: /cs/net/smart-markers-dynamic-data/populate-excel-template-fill-excel-data-via-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vyplnění šablony Excel – Naplnění dat v Excelu pomocí SmartMarker

Už jste někdy potřebovali **vyplnit šablonu Excel**, ale nebyli jste si jisti, jak proces automatizovat? V tomto tutoriálu vám ukážeme, jak **naplnit Excel daty** pomocí Aspose.Cells SmartMarker — nástroje, který promění statický sešit na dynamický generátor reportů.

Představte si, že máte předpřipravený fakturační list, prodejní dashboard nebo jakýkoli opakovatelný formulář. Místo ručního zadávání hodnot můžete předat objekt v C# a nechat SmartMarker udělat těžkou práci. Na konci tohoto průvodce budete mít plně funkční projekt, který vezme šablonu, vloží řádky, součty a dokonce podmíněné formátování — bez nutnosti zasahovat do UI.

## Co se naučíte

- Jak připravit zdroj dat, který odpovídá markerům ve vaší šabloně Excel.  
- Jak vytvořit **SmartMarkerProcessor** a povolit podporu rozsahů.  
- Jak **vyplnit šablonu Excel** pomocí vnořených kolekcí, například položek objednávky.  
- Tipy pro řešení okrajových případů, jako jsou prázdné kolekce nebo vlastní formáty čísel.  

Žádné externí služby, žádné VBA makra — pouze čistý C# a Aspose.Cells. Vše, co potřebujete, je .NET 6 (nebo novější) a NuGet balíček Aspose.Cells.

## Požadavky

- Visual Studio 2022 (nebo jakékoli IDE, které preferujete).  
- .NET 6 SDK nainstalovaný.  
- Aspose.Cells pro .NET (můžete si stáhnout bezplatnou zkušební verzi z webu Aspose).  
- Základní šablona Excel s tagy SmartMarker (vytvoříme ji během několika okamžiků).

Pokud některý z těchto bodů není vám známý, nepanikařte; níže uvedené kroky vás provedou každým požadavkem.

## Krok 1: Navrhněte šablonu Excel s tagy SmartMarker

Nejprve otevřete nový sešit a rozvrhněte statické části — logo společnosti, záhlaví atd. Pak vložte placeholdery SmartMarker tam, kde se mají objevit dynamická data.

| Buňka | Obsah |
|------|---------|
| A1   | **Faktura** |
| A3   | `{{CompanyName}}` |
| A5   | **Detaily objednávky** |
| A7   | `{{Orders.Items.Name}}` |
| B7   | `{{Orders.Items.Qty}}` |
| C7   | `{{Orders.Items.Price}}` |
| D7   | `{{Orders.Items.Price * Orders.Items.Qty}}` |

**Proč je to důležité:** SmartMarker čte dvojité složené závorky a mapuje je na vlastnosti objektu, který předáte později. Kolekce `Orders.Items` říká enginu, aby řádek opakoval pro každou položku v seznamu.

> **Tip:** Použijte možnost `RangeSmartMarker` (povolíme ji později), když potřebujete, aby engine automaticky rozšířil rozsah — ideální pro tabulky, které rostou nebo se zmenšují.

Uložte soubor jako `InvoiceTemplate.xlsx` do složky `Resources` ve vašem projektu.

## Krok 2: Připravte zdroj dat, který odpovídá markerům šablony

Nyní vytvoříme anonymní objekt v C# (nebo silně typovanou třídu), jehož názvy vlastností se shodují s markery. Klíčové je přesně zrcadlit hierarchii.

```csharp
// Step 2: Prepare the data source that matches the template markers
var data = new
{
    CompanyName = "Acme Corp.",
    Orders = new[]
    {
        new
        {
            Items = new[]
            {
                new { Name = "Pen",   Qty = 2, Price = 1.5m },
                new { Name = "Notebook", Qty = 1, Price = 3.75m },
                new { Name = "Stapler",  Qty = 1, Price = 5.0m }
            }
        }
    }
};
```

**Proč je to důležité:** Pole `Orders` obsahuje jedinou objednávku a každá objednávka má pole `Items`. SmartMarker bude iterovat přes `Items` a klonovat řádek pro každý prvek. Pokud později budete potřebovat více objednávek, stačí přidat další objekty do pole `Orders` — žádné změny kódu nejsou potřeba.

## Krok 3: Načtěte šablonu a vytvořte instanci SmartMarkerProcessor

S připravenými daty načteme sešit, vytvoříme procesor a řekneme mu, aby respektoval značky rozsahů.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Load the template workbook
Workbook workbook = new Workbook("Resources/InvoiceTemplate.xlsx");

// Get the first worksheet (where our markers live)
Worksheet ws = workbook.Worksheets[0];

// Step 3: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

**Proč je to důležité:** `SmartMarkerProcessor` je engine, který parsuje markery, rozšiřuje rozsahy a zapisuje hodnoty. Oddělením procesoru od sešitu udržujete kód čistý a znovupoužitelný.

## Krok 4: Zpracujte list s povoleným RangeSmartMarker

Magie nastává, když zavoláme `Process`. Nastavením `RangeSmartMarker = true` řekneme SmartMarkeru, aby považoval celý řádkový rozsah za opakovatelný blok a automaticky vkládal nebo mazal řádky podle potřeby.

```csharp
// Step 4: Process the worksheet using SmartMarker with range support enabled
processor.Process(ws, data, new SmartMarkerOptions { RangeSmartMarker = true });
```

V tomto okamžiku engine:

1. Prohledal list pro značky `{{...}}`.  
2. Namapoval každou značku na vlastnost v `data`.  
3. Detekoval rozsah tabulky (A7:D7) a duplikoval jej třikrát — jednou pro každou položku.  
4. Vypočítal výraz `Price * Qty` pro sloupec s celkem.

## Krok 5: Uložte výsledný sešit

Nakonec zapíšeme vyplněný sešit na disk (nebo jej pošleme jako stream zpět webovému klientovi).

```csharp
// Step 5: Save the populated workbook
workbook.Save("Output/InvoicePopulated.xlsx");
```

Otevřete `InvoicePopulated.xlsx` a uvidíte upravenou tabulku:

| Název      | Množství | Cena | Celkem |
|-----------|----------|------|--------|
| Pen       | 2        | 1.5  | 3.00   |
| Notebook  | 1        | 3.75 | 3.75   |
| Stapler   | 1        | 5.00 | 5.00   |

Krok **vyplnění šablony Excel** je nyní dokončen a úspěšně jste **naplnili Excel daty** pro libovolný počet řádků.

## Řešení běžných okrajových případů

### Prázdné kolekce

Pokud je `Items` prázdná, SmartMarker ponechá záhlaví tabulky, ale nevloží žádné řádky. Aby se předešlo prázdnému prostoru, můžete přidat podmíněný blok:

```csharp
{{#if Orders.Items.Length > 0}}
    ... table rows ...
{{else}}
    No items were ordered.
{{/if}}
```

### Vlastní formáty čísel

Někdy potřebujete měnové symboly nebo oddělovače tisíců. Po zpracování můžete styl aplikovat programově:

```csharp
Style style = workbook.CreateStyle();
style.Number = 164; // Built‑in currency format
StyleFlag flag = new StyleFlag { NumberFormat = true };

foreach (Cell cell in ws.Cells["C8:D12"])
{
    cell.SetStyle(style, flag);
}
```

### Velké datové sady

Pro tisíce řádků povolte možnost `UseFastMode`, která zlepší výkon:

```csharp
processor.Process(ws, data, new SmartMarkerOptions { 
    RangeSmartMarker = true,
    UseFastMode = true
});
```

## Kompletní funkční příklad

Níže je kompletní, samostatný program, který můžete zkopírovat a vložit do konzolové aplikace. Obsahuje všechny `using` direktivy, přípravu dat, zpracování i uložení.



## Co byste se měli naučit dál?

- [Populate Excel with Data Using Aspose.Cells and Smart Markers](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)
- [How to Populate Excel Cells with Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/cell-operations/aspose-cells-dotnet-populate-excel-data/)
- [Automate Excel Data Export Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}