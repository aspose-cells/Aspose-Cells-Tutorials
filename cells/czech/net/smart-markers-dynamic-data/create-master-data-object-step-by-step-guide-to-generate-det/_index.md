---
category: general
date: 2026-02-14
description: Vytvořte hlavní datový objekt v C# a bez námahy generujte detailní list.
  Naučte se celý workflow SmartMarkeru s praktickými příklady kódu.
draft: false
keywords:
- create master data object
- generate detail sheet
- smartmarker processing
- worksheet automation
- c# data binding
language: cs
og_description: Vytvořte hlavní datový objekt v C# a vygenerujte detailní list pomocí
  SmartMarkeru. Postupujte podle našeho podrobného tutoriálu pro připravené řešení.
og_title: Vytvoření objektu hlavních dat – kompletní průvodce
tags:
- C#
- SmartMarker
- Excel Automation
title: Vytvoření objektu hlavních dat – průvodce krok za krokem pro vytvoření detailního
  listu
url: /cs/net/smart-markers-dynamic-data/create-master-data-object-step-by-step-guide-to-generate-det/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření objektu hlavních dat – Kompletní tutoriál

Už jste někdy potřebovali **create master data object** pro list Excel, ale nebyli jste si jisti, jak ho propojit s detailním listem SmartMarker? Nejste v tom sami. V mnoha scénářích reportování hlavní objekt řídí dynamický detailní list a správné propojení může připomínat skládání puzzle bez obrázku.  

V tomto průvodci projdeme celý proces — vytvoření objektu hlavních dat, nastavení možností SmartMarker pro **generate detail sheet** a nakonec spuštění procesoru. Na konci budete mít spustitelný úryvek, který můžete vložit do libovolného .NET projektu používajícího knihovnu GrapeCity Documents for Excel (GcExcel) library.

## Co budete potřebovat

- .NET 6+ (nebo .NET Framework 4.7.2) s odkazem na `GcExcel.dll`
- Základní znalost C# (proměnné, anonymní typy, inicializátory objektů)
- Excel sešit, který již obsahuje SmartMarker značky jako `{{OrderId}}` a tabulku pro řádky položek
- Visual Studio, Rider nebo jakýkoli editor, který preferujete

To je vše — žádné další NuGet balíčky kromě základní distribuce GcExcel.

## Krok 1: Vytvoření objektu hlavních dat

Prvním krokem je **create master data object**, který odráží strukturu očekávanou značkami SmartMarker. Považujte ho za malý model reportu v paměti.

```csharp
// Step 1: Build the master data object that feeds the SmartMarkers.
// It contains an OrderId and a collection of line items.
var orderData = new
{
    OrderId = 1,
    Items = new[]
    {
        new { Product = "A", Quantity = 2 },
        new { Product = "B", Quantity = 5 }
    }
};
```

Proč zde použít anonymní typ? Protože vám umožňuje definovat lehký kontejner bez deklarace plnohodnotné třídy — ideální pro rychlé ukázky nebo když se struktura pravděpodobně nezmění. Pokud později potřebujete znovupoužitelný model, stačí nahradit `var` správným POCO.

> **Tip:** Udržujte názvy vlastností (`OrderId`, `Product`, `Quantity`) identické s placeholdery ve vašem listu; SmartMarker je porovnává bez ohledu na velikost písmen.

## Krok 2: Nastavení možností SmartMarker pro vytvoření detailního listu

Nyní řekneme SmartMarkeru, že chceme samostatný list pro tabulku řádkových položek. Zde vstupuje do hry klíčové slovo **generate detail sheet**.

```csharp
// Step 2: Set up SmartMarker options.
// Enabling DetailSheet creates a new sheet for each master record.
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheet = true,
    // The new sheet will be named using the OrderId value.
    DetailSheetNewName = "Order_{OrderId}"
};
```

Vzor `DetailSheetNewName` používá placeholdery v složených závorkách, které jsou nahrazeny za běhu. V našem příkladu se list nazve `Order_1`. Pokud později projdete více objednávek, každá získá vlastní záložku — přesně to, co většina účetních očekává.

## Krok 3: Spuštění procesoru SmartMarker

S připravenými daty a možnostmi je posledním krokem zavolat procesor na cílový list.

```csharp
// Step 3: Execute SmartMarker processing on the worksheet.
// 'worksheet' is an IWorksheet instance that points to the template sheet.
worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);
```

Na pozadí SmartMarker prohledá list po značkách, vloží hodnoty `orderData` a protože `DetailSheet` je `true`, zkopíruje šablonu do nového listu pojmenovaného `Order_1`. Všechny řádky položek se objeví v detailní oblasti a zachová se jakékoli formátování, které jste v šabloně použili.

### Kompletní funkční příklad

Níže je samostatný konzolový program, který otevře šablonový sešit (`Template.xlsx`), provede tři kroky a uloží výsledek jako `Result.xlsx`. Můžete jej zkopírovat a vložit do nového konzolového projektu a stisknout **F5**.

```csharp
using System;
using GrapeCity.Documents.Excel;

class Program
{
    static void Main()
    {
        // Load the Excel template that contains SmartMarker tags.
        var workbook = new Workbook();
        workbook.Open("Template.xlsx");

        // -------------------------------------------------
        // Step 1: Create the master data object.
        // -------------------------------------------------
        var orderData = new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Product = "A", Quantity = 2 },
                new { Product = "B", Quantity = 5 }
            }
        };

        // -------------------------------------------------
        // Step 2: Configure SmartMarker options to generate detail sheet.
        // -------------------------------------------------
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheet = true,
            DetailSheetNewName = "Order_{OrderId}"
        };

        // -------------------------------------------------
        // Step 3: Process the worksheet.
        // -------------------------------------------------
        // Assume the first sheet holds the master template.
        var worksheet = workbook.Worksheets[0];
        worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);

        // Save the populated workbook.
        workbook.Save("Result.xlsx");
        Console.WriteLine("Done! Check Result.xlsx – a new sheet named Order_1 should exist.");
    }
}
```

#### Očekávaný výstup

- **Result.xlsx** obsahuje list s názvem `Order_1`.
- Buňka `A1` (nebo kdekoliv jste umístili `{{OrderId}}`) nyní zobrazuje `1`.
- Tabulka začínající v bloku SmartMarker obsahuje dva řádky:

  | Product | Quantity |
  |---------|----------|
  | A       | 2        |
  | B       | 5        |

Pokud soubor otevřete, uvidíte, že formátování ze šablony je zachováno — okraje, písma, podmíněné formátování — vše nedotčeno.

## Časté otázky a okrajové případy

### Co když mám více objednávek?

Zabalte objekt hlavních dat do kolekce a nechte SmartMarker iterovat automaticky:

```csharp
var orders = new[]
{
    new {
        OrderId = 1,
        Items = new[] { new { Product = "A", Quantity = 2 } }
    },
    new {
        OrderId = 2,
        Items = new[] { new { Product = "C", Quantity = 3 } }
    }
};

worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);
```

Každá objednávka vytvoří vlastní list (`Order_1`, `Order_2`, …). Procesor zachází s vnějším polem jako s hlavní kolekcí.

### Jak ovlivním pozici listu?

Nastavte `smartMarkerOptions.DetailSheetInsertIndex = 2;` pro umístění nového listu za druhou záložku, nebo použijte `DetailSheetInsertAfter = "Summary"` pro vložení za pojmenovaný list.

### Mohu detailní list pro konkrétní běh zakázat?

Jednoduše přepněte `DetailSheet = false;`. SmartMarker pak zapíše řádky položek do stejného listu, kde jsou umístěny hlavní značky.

### Co s velkými datovými sadami?

SmartMarker data streamuje efektivně, ale pokud překročíte několik stovek tisíc řádků, můžete narazit na limit Excelu 1 048 576 řádků. V takovém případě rozdělte data do více hlavních záznamů nebo zvažte export do CSV.

## Vizualizace

![Diagram ukazující, jak vytvořit objekt hlavních dat a vygenerovat detailní list pomocí SmartMarker](/images/smartmarker-flow.png)

*Ilustrace ukazuje tok od C# objektu hlavních dat → možnosti SmartMarker → zpracování listu → nový detailní list.*

## Závěr

Nyní víte, jak **create master data object** v C# a nastavit SmartMarker tak, aby **generate detail sheet** automaticky. Tříkrokový vzor — data, možnosti, procesor — pokrývá většinu scénářů automatizace Excelu s GcExcel.  

Odtud můžete zkoumat:

- Přidání dat hlavičky/patky na každý detailní list
- Použití podmíněného formátování na základě stavu objednávky
- Export vygenerovaného sešitu do PDF pomocí `workbook.SaveAsPdf(...)`

Neváhejte experimentovat, rozbít věci a pak je znovu spojit. To je nejrychlejší cesta, jak zvládnout automatizaci listů. Šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}