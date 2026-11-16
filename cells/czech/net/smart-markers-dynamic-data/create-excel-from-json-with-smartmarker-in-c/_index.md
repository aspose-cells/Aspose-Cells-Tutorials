---
category: general
date: 2026-11-16
description: Vytvořte Excel z JSON pomocí SmartMarker. Naučte se, jak převést JSON
  do Excelu, vložit JSON do Excelu a během několika minut uložit sešit ve formátu
  xlsx.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json
- convert json to excel
- embed json in excel
- save workbook xlsx
language: cs
lastmod: 2026-11-16
og_description: Rychle vytvořte Excel z JSON. Tento tutoriál ukazuje, jak převést
  JSON do Excelu, vložit JSON do Excelu a uložit sešit xlsx pomocí Aspose.Cells.
og_image_alt: Screenshot of an Excel worksheet showing JSON data inserted into a single
  cell
og_title: Vytvořte Excel z JSON pomocí SmartMarker – krok za krokem průvodce C#
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  headline: Create Excel from JSON with SmartMarker in C#
  type: TechArticle
- description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  name: Create Excel from JSON with SmartMarker in C#
  steps:
  - name: Build and run the console app (`dotnet run`).
    text: Build and run the console app (`dotnet run`).
  - name: Verify the console prints the full path to the generated file.
    text: Verify the console prints the full path to the generated file.
  - name: Open the file in Excel or any spreadsheet viewer.
    text: Open the file in Excel or any spreadsheet viewer.
  - name: Confirm that cell A1 holds the JSON array string exactly as shown above.
    text: Confirm that cell A1 holds the JSON array string exactly as shown above.
  type: HowTo
tags:
- SmartMarker
- Aspose.Cells
- C#
- JSON
title: Vytvořte Excel z JSON pomocí SmartMarker v C#
url: /cs/net/smart-markers-dynamic-data/create-excel-from-json-with-smartmarker-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořte Excel z JSON pomocí SmartMarker v C#

Pokud potřebujete **vytvořit Excel z JSON** v .NET projektu, tento návod ukazuje kompletní, spustitelné řešení. Pomocí procesoru Smart Marker z Aspose.Cells můžete **převést JSON do Excelu**, vložit řetězec JSON přímo do buňky a **uložit sešit xlsx** bez psaní jakéhokoli ručního parsovacího kódu.

Uvidíte, jak zaregistrovat zdroj dat JSON, vložit Smart Marker, který vypíše celé pole jako jediný řetězec JSON, zpracovat list a nakonec zapsat soubor na disk. Na konci tutoriálu budete schopni vygenerovat soubor Excel, který obsahuje původní JSON payload v buňce A1, připravený pro další zpracování nebo reportování.

## Předpoklady

- .NET 6.0 nebo novější (kód funguje také s .NET Framework 4.7+)
- Aspose.Cells pro .NET (NuGet balíček `Aspose.Cells`)
- Základní znalost C# a formátování JSON
- IDE jako Visual Studio nebo VS Code

## Krok 1: Nastavte projekt a importujte jmenné prostory

Vytvořte novou konzolovou aplikaci a přidejte balíček Aspose.Cells:

```bash
dotnet new console -n JsonToExcelDemo
cd JsonToExcelDemo
dotnet add package Aspose.Cells
```

Poté zahrňte požadované jmenné prostory na začátek souboru `Program.cs`:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
```

**Proč?**  
`Aspose.Cells` poskytuje model sešitu, zatímco `Aspose.Cells.SmartMarkers` obsahuje třídu `SmartMarkerProcessor`, která interpretuje značky `&=` v listu.

## Krok 2: Definujte zdroj dat JSON

Umístěte řetězec JSON do proměnné. V tomto příkladu máme pole objednávek:

```csharp
// Step 2: Define the JSON data source
string json = @"{
    ""Orders"": [
        { ""Id"": 1, ""Amount"": 100 },
        { ""Id"": 2, ""Amount"": 150 }
    ]
}";
```

**Proč?**  
Smart Marker funguje s libovolným dobře formovaným JSON. Uložení JSON do řetězce vám umožní jej zaregistrovat přímo, aniž byste potřebovali soubor na disku.

## Krok 3: Zaregistrujte JSON data pomocí SmartMarkerProcessor

Vytvořte instanci `SmartMarkerProcessor` a přiřaďte řetězec JSON ke jménu, na které budete později odkazovat v listu:

```csharp
// Step 3: Register the JSON data with the Smart Marker processor
SmartMarkerProcessor processor = new SmartMarkerProcessor();
processor.RegisterJsonDataSource("OrdersJson", json);
```

**Proč?**  
`RegisterJsonDataSource` analyzuje JSON a zpřístupní jeho hierarchii pro Smart Markery. Název `"OrdersJson"` se stane kořenovým objektem ve výrazech značek.

## Krok 4: Vytvořte sešit a vložte Smart Marker

Instancujte nový sešit, získejte jeho první list a zapište Smart Marker do buňky A1, který vypíše celé pole `Orders` jako jediný řetězec JSON:

```csharp
// Step 4: Create a workbook and get the first worksheet
Worksheet ws = new Workbook().Worksheets[0];

// Insert a Smart Marker that outputs the whole array as a single JSON string
ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");
```

**Proč?**  
Výraz `OrdersJson.Orders.ArrayAsSingle` říká Smart Markeru, aby vzal pole `Orders` a znovu jej serializoval do JSON, výsledek umístí do cílové buňky. Toto je nejužitečnější způsob, jak **vložit JSON do Excelu**.

## Krok 5: Zpracujte list

Spusťte procesor, aby nahradil značku skutečným řetězcem JSON:

```csharp
// Step 5: Process the worksheet – the marker is replaced with the JSON array string
processor.Process(ws);
```

**Proč?**  
Zpracování prochází každou buňku hledající značky `&=`, vyhodnocuje je vůči registrovaným zdrojům dat a zapisuje získanou hodnotu zpět do listu.

## Krok 6: Uložte sešit jako soubor .xlsx

Nakonec zapište sešit na disk. Upravte cestu na složku, do které máte právo zápisu:

```csharp
// Step 6: Save the workbook
string outputPath = Path.Combine(
    Environment.CurrentDirectory,
    "JsonArraySingleCell.xlsx");

ws.Workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

**Proč?**  
`SaveFormat.Xlsx` zajistí, že soubor bude uložen v moderním formátu Office Open XML, čímž splní požadavek **save workbook xlsx**.

## Kompletní zdrojový kód

Když spojíte všechny části, získáte kompletní, připravený k spuštění program:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // Step 2: Define the JSON data source
        string json = @"{
            ""Orders"": [
                { ""Id"": 1, ""Amount"": 100 },
                { ""Id"": 2, ""Amount"": 150 }
            ]
        }";

        // Step 3: Register the JSON data with the Smart Marker processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.RegisterJsonDataSource("OrdersJson", json);

        // Step 4: Create a workbook and get the first worksheet
        Worksheet ws = new Workbook().Worksheets[0];

        // Insert a Smart Marker that will output the whole array as a single JSON string
        ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");

        // Step 5: Process the worksheet – the marker is replaced with the JSON array string
        processor.Process(ws);

        // Step 6: Save the workbook
        string outputPath = Path.Combine(
            Environment.CurrentDirectory,
            "JsonArraySingleCell.xlsx");
        ws.Workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### Očekávaný výstup v Excelu

Otevřete `JsonArraySingleCell.xlsx`. Buňka A1 bude obsahovat:

```
[{"Id":1,"Amount":100},{"Id":2,"Amount":150}]
```

Řetězec JSON je kompaktní reprezentací původního pole `Orders`, což usnadňuje jeho přenos nebo konzumaci v následných pracovních postupech založených na Excelu.

## Běžné varianty a okrajové případy

| Situace | Úprava |
|-----------|------------|
| **Více JSON objektů** | Zaregistrujte každý objekt pod odlišným jménem (např. `processor.RegisterJsonDataSource("CustomerJson", customerJson);`) a odkazujte na ně pomocí samostatných značek. |
| **Formátovaný JSON v buňce** | Použijte možnost `ArrayAsSinglePretty`: `ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSinglePretty");` |
| **Velké JSON payloady** | Zvažte zápis JSON na skrytý list nebo konverzi do `DataTable` pro lepší výkon. |
| **Vkládání JSON do více buněk** | Umístěte různé značky do dalších buněk, např. `&=OrdersJson.Orders[0].Id` pro získání jednotlivých polí. |

**Tip:** Při práci s velmi velkým JSON zvyšte paměťový buffer sešitu (`WorkbookSettings.MemorySetting`), aby nedošlo k `OutOfMemoryException`.

## Testování řešení

1. Sestavte a spusťte konzolovou aplikaci (`dotnet run`).  
2. Ověřte, že konzole vypíše úplnou cestu k vygenerovanému souboru.  
3. Otevřete soubor v Excelu nebo jiném prohlížeči tabulek.  
4. Potvrďte, že buňka A1 obsahuje řetězec JSON přesně tak, jak je uvedeno výše.

Pokud buňka obsahuje text značky (`&=OrdersJson...`) místo JSON, zkontrolujte, že procesor byl volán **po** umístění značky a že řetězec JSON je platný.

## Závěr

Nyní víte, jak **vytvořit Excel z JSON** pomocí Aspose.Cells Smart Markers, jak **převést JSON do Excelu**, vložit JSON payload přímo do buňky a **uložit sešit xlsx** jedním řádkem kódu. Tento přístup eliminuje ruční parsování, funguje s libovolnou strukturou JSON a vytváří čistý, standardy‑kompatibilní soubor Excel.

### Další kroky

- Prozkoumejte **směrové smyčky Smart Marker** (`&=OrdersJson.Orders`) pro generování řádku pro každou objednávku místo jediného řetězce JSON.  
- Kombinujte tuto techniku s **Excelovými vzorci** pro výpočet součtů z vložených dat.  
- Podívejte se na **čtení JSON zpět z Excelu** pomocí `Workbook.Load` a `SmartMarkerProcessor` v opačném směru.

Neváhejte experimentovat s různými tvary JSON, více listy nebo exportem do jiných formátů, jako je CSV nebo PDF. Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vlastních projektech.

- [Create Excel from JSON with Aspose.Cells Smart Marker](/cells/english/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/)
- [Create Excel Workbook from JSON – Complete Aspose.Cells Guide](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Save Excel Workbook from JSON – Complete Guide](/cells/english/net/templates-reporting/save-excel-workbook-from-json-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}