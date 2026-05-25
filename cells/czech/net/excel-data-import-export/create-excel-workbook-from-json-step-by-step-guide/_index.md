---
category: general
date: 2026-03-25
description: Vytvořte Excel sešit z JSON a uložte jej jako xlsx. Naučte se, jak exportovat
  JSON do xlsx, generovat Excel z JSON a naplnit Excel z JSON během několika minut.
draft: false
keywords:
- create excel workbook
- export json to xlsx
- generate excel from json
- populate excel from json
- save workbook as xlsx
language: cs
og_description: Vytvořte sešit Excelu z JSON okamžitě. Tento průvodce ukazuje, jak
  exportovat JSON do XLSX, generovat Excel z JSON a naplnit Excel z JSON pomocí Aspose.Cells.
og_title: Vytvořte Excel sešit z JSON – kompletní C# tutoriál
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Vytvořte Excel sešit z JSON – krok za krokem
url: /cs/net/excel-data-import-export/create-excel-workbook-from-json-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření Excel sešitu z JSON – Kompletní C# tutoriál

Už jste někdy potřebovali **create excel workbook** z JSON payloadu, ale nevedeli jste, kde začít? Nejste v tom sami; mnoho vývojářů narazí na tuto překážku, když se snaží převést data z API do přehledné tabulky. Dobrá zpráva? S několika řádky C# a Aspose.Cells můžete **export json to xlsx**, **generate excel from json** a **populate excel from json** bez používání třetích konvertorů.

V tomto průvodci projdeme celý proces – od surového JSON řetězce, přes vložení do SmartMarkeru, až po **save workbook as xlsx** na disku. Na konci budete mít připravený Excel soubor, který vypadá takto:

| Name | Score |
|------|-------|
| John | 90    |
| Anna | 85    |

> **Pro tip:** Pokud již v projektu používáte Aspose.Cells, můžete znovu použít stejnou instanci `Workbook` pro více JSON importů – skvělé pro dávkové zpracování.

## Co budete potřebovat

- **.NET 6+** (nebo jakýkoli recent .NET Framework podporující C# 10)
- **Aspose.Cells for .NET** – nainstalujte přes NuGet: `dotnet add package Aspose.Cells`
- Základní znalost syntaxe C# (není potřeba hluboké znalosti Excelu)

To je vše. Žádné externí služby, žádný COM interop, jen čistý spravovaný kód.

## Krok 1: Inicializace nového Excel sešitu

Prvním krokem je vytvořit nový objekt workbook. Představte si to jako otevření prázdného Excel souboru, do kterého později vložíme data.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and grab the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];
```

Proč začínat s novým workbookem? Zajišťuje čistý stav, zabraňuje zbytkům stylů z předchozích běhů a udržuje velikost souboru minimální – ideální pro automatizované pipeline.

## Krok 2: Připravte JSON data, která chcete importovat

Pro demonstraci použijeme malý JSON pole, ale můžete jej nahradit libovolným platným JSON, který získáte z webové služby, souboru nebo databázového dotazu.

```csharp
// Step 2: JSON string representing a simple collection of records
string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";
```

Všimněte si dvojitě escapovaných uvozovek (`\"`) – to je jen syntaxe řetězce v C#. Ve skutečném scénáři byste pravděpodobně četli tento řetězec ze souboru:

```csharp
// string jsonData = File.ReadAllText("data.json");
```

## Krok 3: Nastavte SmartMarker, aby zpracoval celé pole jako jeden záznam

Engine SmartMarker v Aspose.Cells dokáže automaticky iterovat přes kolekce. Povolením **ArrayAsSingle** zacházíme s celým JSON polem jako s jedním záznamem, což je přesně to, co potřebujeme pro plochou tabulku.

```csharp
// Step 3: Configure SmartMarker options – array‑as‑single mode
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // This makes the whole JSON array behave like one record
};
```

Pokud tento příznak zapomenete, SmartMarker se pokusí vytvořit samostatný list pro každý prvek – rozhodně ne to, co chcete při generování jednoduché tabulky.

## Krok 4: Umístěte SmartMarker token do listu

SmartMarker tokeny vypadají jako `${jsonArray}`. Když se procesor spustí, nahradí token daty ze zdroje JSON. Token umístíme do buňky **A1**, aby výstup začal v levém horním rohu.

```csharp
// Step 4: Insert the SmartMarker token into cell A1
worksheet.Cells["A1"].PutValue("${jsonArray}");
```

Můžete také předzpracovat formátování řádku s hlavičkou. Například nastavit tučný font na první řádek:

```csharp
Cell headerCell = worksheet.Cells["A1"];
headerCell.Style.Font.IsBold = true;
```

## Krok 5: Spusťte SmartMarker procesor

Nyní se děje magie. Procesor načte JSON, přiřadí každou vlastnost ke sloupci a zapíše řádky pod token.

```csharp
// Step 5: Process the SmartMarker with our JSON data and options
worksheet.SmartMarkerProcessor.Process(jsonData, options);
```

Behind the scenes, Aspose.Cells:

1. Analyzuje JSON do .NET objektu.
2. Přiřadí názvy vlastností (`Name`, `Score`) k záhlavím sloupců.
3. Zapíše každý prvek pole jako nový řádek.

Pokud váš JSON obsahuje vnořené objekty, můžete na ně odkazovat pomocí notace s tečkou (`${parent.child}`) – užitečná funkce pro složitější reporty.

## Krok 6: Uložte sešit jako soubor XLSX

Nakonec uložte workbook na disk. Přípona souboru `.xlsx` říká Excelu (a většině ostatních tabulkových aplikací), že se jedná o OpenXML sešit.

```csharp
// Step 6: Save the workbook to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Samozřejmě můžete streamovat workbook přímo do HTTP odpovědi, pokud vytváříte webové API:

```csharp
// Example for ASP.NET Core
using (var stream = new MemoryStream())
{
    workbook.Save(stream, SaveFormat.Xlsx);
    stream.Position = 0;
    return File(stream, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "data.xlsx");
}
```

## Kompletní funkční příklad

Níže je kompletní, připravený program, který zahrnuje všechny výše uvedené kroky. Zkopírujte jej do nového konzolového projektu a stiskněte **F5**.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ JSON data to be merged into the sheet
        string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";

        // 3️⃣ Enable array‑as‑single mode so the whole array is one record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Put a SmartMarker token in A1 that points to the JSON array
        worksheet.Cells["A1"].PutValue("${jsonArray}");

        // Optional: make the header bold for better readability
        worksheet.Cells["A1"].Style.Font.IsBold = true;

        // 5️⃣ Process the SmartMarker with the JSON payload
        worksheet.SmartMarkerProcessor.Process(jsonData, options);

        // 6️⃣ Save the result as an XLSX file
        string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"✅ Workbook created and saved to: {outputPath}");
    }
}
```

**Očekávaný výsledek:** Otevření `json-single.xlsx` zobrazí dva řádky pod tučnou hlavičkou – `John` se skóre `90` a `Anna` s `85`. Názvy sloupců jsou automaticky odvozeny z názvů vlastností JSON.

## Časté otázky a okrajové případy

### Co když moje JSON klíče obsahují mezery nebo speciální znaky?

SmartMarker očekává platná jména identifikátorů. Nahraďte mezery podtržítky nebo použijte vlastní mapování:

```csharp
// Example JSON: {"First Name":"John"}
string jsonData = "[{\"First_Name\":\"John\",\"Score\":90}]";
// Token stays the same – Aspose.Cells will map "First_Name" to column header "First_Name"
```

### Jak exportovat velké JSON pole (tisíce řádků)?

Procesor interně streamuje data, takže využití paměti zůstává skromné. Nicméně můžete chtít:

- Zvýšit limit `MaxRows` listu (`worksheet.Cells.MaxRow = 1_048_576;` – maximální počet řádků v Excelu).
- Vypnout mřížku pro lepší výkon (`worksheet.IsGridlinesVisible = false;`).

### Můžu přidat více JSON tabulek do stejného sešitu?

Ano. Stačí umístit různé SmartMarker tokeny do samostatných oblastí (např. `${orders}` v `A10`, `${customers}` v `D1`) a zavolat `Process` jednou pro každý token nebo jednou s kompozitním JSON objektem obsahujícím oba pole.

## Bonus: Přidání jednoduchého grafu (volitelné)

Pokud chcete vizualizovat skóre, přidejte rychlý sloupcový graf po naplnění dat:

```csharp
// Insert a column chart starting at cell E1
int chartIndex = worksheet.Charts.Add(ChartType.Column, 0, 4, 15, 10);
Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("B2:B3", true);
chart.NSeries[0].Name = "Score";
chart.Title.Text = "Scores by Name";
```

## Závěr

Nyní víte, **how to create excel workbook** z JSON řetězce, **export json to xlsx**, **generate excel from json** a **populate excel from json** pomocí funkce SmartMarker v Aspose.Cells. Kompletní řešení – inicializace sešitu, konfigurace SmartMarkeru, zpracování JSON a uložení souboru – se vejde do několika řádků, ale dokáže pracovat s obrovskými datovými sadami.

Další kroky? Zkuste nahradit statický JSON voláním API, přidejte podmíněné formátování na základě skóre nebo generujte více listů pro různé datové domény. Stejný vzor funguje pro CSV, XML nebo i výstupy z databáze – stačí změnit zdrojový řetězec a upravit SmartMarker token.

Šťastné programování a ať jsou vaše tabulky vždy přehledné!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}