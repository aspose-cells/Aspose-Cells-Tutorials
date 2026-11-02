---
category: general
date: 2026-09-18
description: Naučte se, jak rozšířit pole v Excelu pomocí funkce EXPAND, naplnit šablonu
  Excelu a vytvořit dynamický rozsah listu v Excelu pomocí C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- populate excel template
- dynamic range excel
- use expand function
- expand array formula
language: cs
lastmod: 2026-09-18
og_description: Jak rozšířit pole v Excelu pomocí funkce EXPAND, naplnit šablonu Excelu
  a vytvořit dynamické řešení rozsahu v Excelu pomocí kódu C#.
og_image_alt: Excel worksheet showing expanded 5x5 array and Smart Markers result
og_title: Jak rozšířit pole v Excelu a vyplnit šablonu
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to expand array in Excel using the EXPAND function, populate
    an Excel template, and create a dynamic range Excel worksheet with C#.
  headline: How to expand array in Excel and populate a template
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Jak rozšířit pole v Excelu a naplnit šablonu
url: /cs/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak rozšířit pole v Excelu a naplnit šablonu

Pokud potřebujete **jak rozšířit pole** v Excelu při vyplňování předem navržené šablony, tento průvodce vám ukáže kompletní řešení od začátku do konce. Pomocí funkce `EXPAND` spolu s Smart Markery z Aspose.Cells můžete převést odkaz na jedinou buňku na oblast 5 × 5 a automaticky nahradit značky jako `{IsActive}` živými daty.

Ukážeme si, jak **populate excel template**, vytvořit **dynamic range excel** a správně **use expand function** v projektu C#. Na konci tutoriálu budete mít spustitelný program, který načte soubor `.xlsx`, rozšíří pole pomocí vzorce, použije Smart Markery a uloží výsledek.

## Požadavky

* .NET 6.0 nebo novější (kód také funguje s .NET Core 3.1+)
* Aspose.Cells pro .NET (NuGet balíček `Aspose.Cells`)
* Excel sešit, který obsahuje buňku s placeholderovým vzorcem (např. `B2`) a Smart Marker jako `{IsActive}`
* Základní znalost C# a Excelových vzorců

> **Tip:** Funkce `EXPAND` je k dispozici pouze v Excelu pro Microsoft 365 a Excel 2021+. Starší verze vrátí chybu `#NAME?`.

## Krok 1: Jak rozšířit pole pomocí funkce EXPAND

Prvním krokem je načíst sešit a zapsat vzorec `EXPAND`, který převádí jedinou zdrojovou buňku na větší matici.  

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook that contains the template layout
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Apply the EXPAND function to cell B2.
        // =EXPAND(A2,5,5) expands the array that starts at A2 into a 5‑row by 5‑column range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";
```

Proč je to důležité: `EXPAND` odstraňuje potřebu ručně kopírovat vzorce přes řádky a sloupce. Když se změní zdrojová buňka (`A2`), celý blok 5 × 5 se automaticky aktualizuje, což vám poskytne **dynamic range excel**, který reaguje na změny dat.

## Krok 2: Naplnění Excel šablony pomocí Smart Markerů

Smart Markery vám umožňují vložit placeholdery do šablony, které jsou nahrazeny hodnotami z objektu C#. Toto je nejpohodlnější způsob, jak **populate excel template** bez psaní kódu buňka po buňce.

```csharp
        // Prepare an anonymous object that matches the marker names in the template.
        var data = new { IsActive = true };

        // Apply Smart Markers. The marker {IsActive} inside a formula like
        // =IF({IsActive}, "Active", "Inactive") will be replaced with the value from the object.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);
```

Volání `SmartMarkersProcessor().Apply` prohledá celý list, najde `{IsActive}` a vloží boolean hodnotu. Vzorec pak automaticky vyhodnotí na `"Active"` nebo `"Inactive"`.

## Krok 3: Ověření rozšířené oblasti a naplněného výsledku

Po aplikaci jak vzorce `EXPAND`, tak Smart Markerů můžete programově přečíst několik buněk a ověřit, že vše funguje podle očekávání.

```csharp
        // Optional: read a cell from the expanded block to confirm the value.
        var sampleValue = ws.Cells["B2"].Value; // top‑left cell of the expanded range
        Console.WriteLine($"Top‑left of expanded range: {sampleValue}");

        // Read the marker result cell (assume it is C2)
        var status = ws.Cells["C2"].StringValue;
        Console.WriteLine($"Status from Smart Marker: {status}");
```

Spuštění programu by mělo vypsat původní hodnotu z `A2` (nebo výsledek pole) a buď **Active**, nebo **Inactive** v závislosti na příznaku `IsActive`.

## Krok 4: Uložení sešitu – finální výstup

Nakonec zapíšete upravený sešit na disk. Tento krok demonstruje kompletní tok od načtení, rozšíření, naplnění až po uložení souboru.

```csharp
        // Save the workbook with the expanded array and populated markers.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Uložený soubor `output.xlsx` nyní obsahuje matici 5 × 5 vytvořenou vzorcem `EXPAND` a buňku, která odráží hodnotu `{IsActive}`. Otevřete soubor v Excelu a uvidíte dynamickou oblast v akci.

## Okrajové případy a osvědčené postupy

| Situace                                 | Doporučení                                                                                           |
|-----------------------------------------|------------------------------------------------------------------------------------------------------|
| Verze Excelu nepodporuje `EXPAND`      | Použijte klasické vzorce `=OFFSET` nebo `=INDEX`, nebo upgradujte na Office 365.                     |
| Potřeba rozšířit na proměnnou velikost   | Použijte `ROWS(source)` a `COLUMNS(source)` uvnitř `EXPAND` pro skutečnou dynamiku.                  |
| Více Smart Markerů ve stejném listu      | Zavolejte `SmartMarkersProcessor().Apply` jednou s kompozitním datovým objektem.                     |
| Velké sešity (> 10 000 řádků)           | Vypněte výpočty během zápisu vzorců (`workbook.Settings.CheckFormula = false`).                     |

## Kompletní funkční příklad

Níže je kompletní, samostatný program, který můžete zkopírovat a vložit do nového konzolového projektu.

```csharp
using System;
using Aspose.Cells;

class ExpandArrayDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook that serves as the template.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Write the EXPAND formula to create a 5x5 dynamic range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";

        // 3️⃣ Prepare data for Smart Markers.
        var data = new { IsActive = true };

        // 4️⃣ Apply Smart Markers – replaces {IsActive} in any formula or text.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);

        // 5️⃣ (Optional) Verify a couple of cells.
        Console.WriteLine($"Expanded top‑left: {ws.Cells["B2"].Value}");
        Console.WriteLine($"Marker result: {ws.Cells["C2"].StringValue}");

        // 6️⃣ Save the final workbook.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
        Console.WriteLine("Workbook saved successfully.");
    }
}
```

**Očekávaný výstup při spuštění programu** (předpokládáme, že `A2` obsahuje číslo `42`):

```
Expanded top‑left: 42
Marker result: Active
Workbook saved successfully.
```

Otevření `output.xlsx` ukazuje blok 5 × 5 vyplněný hodnotami odvozenými z `A2` a buňku, která obsahuje **Active**.

## Závěr

Nyní víte, **how to expand array** v Excelu pomocí funkce `EXPAND`, jak **populate excel template** pomocí Smart Markerů a jak vytvořit **dynamic range excel**, který se automaticky přizpůsobuje zdrojovým datům. Příklad také ukazuje správný způsob **use expand function** a **expand array formula** v reálném scénáři automatizace v C#.

Dále zvažte rozšíření řešení:

* Nahraďte pevné rozměry `5,5` rozměry `ROWS(A2:A10), COLUMNS(A2:E2)` pro skutečně proměnné oblasti.
* Kombinujte více Smart Markerů pro generování kompletních reportů (např. seznamy zaměstnanců, tabulky prodeje).
* Prozkoumejte styling API Aspose.Cells pro automatické formátování rozšířeného bloku.

Neváhejte experimentovat s různými zdrojovými poli, názvy markerů a rozvržením sešitu. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Export Data to Excel: Populate a Template from an Array in C#](/cells/english/net/smart-markers-dynamic-data/export-data-to-excel-populate-a-template-from-an-array-in-c/)
- [How to create array in Excel with C# – Step-by-Step Guide](/cells/english/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/)
- [Processing Data Using Array Function in Excel](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}