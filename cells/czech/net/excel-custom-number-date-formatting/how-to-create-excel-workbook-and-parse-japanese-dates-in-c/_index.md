---
category: general
date: 2026-10-10
description: Vytvořte Excel sešit v C# a nastavte hodnotu buňky na japonské datum
  éry, poté použijte vlastní formát a přečtěte datum buňky pomocí Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set cell value
- apply custom format
- read date cell
- excel date parsing
language: cs
lastmod: 2026-10-10
og_description: Vytvořte Excel sešit v C# a zpracujte japonské datumy v érách. Naučte
  se nastavit hodnotu buňky, použít vlastní formát a načíst datumovou buňku pomocí
  Aspose.Cells.
og_image_alt: Screenshot showing a C# program that creates an Excel workbook and parses
  a Japanese era date
og_title: Vytvořte sešit Excelu v C# – kompletní průvodce parsováním data
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and set cell value with a Japanese era
    date, then apply custom format and read date cell using Aspose.Cells.
  headline: How to create Excel workbook and parse Japanese dates in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: Jak vytvořit sešit Excelu a parsovat japonské datumy v C#
url: /cs/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit Excel sešit a parsovat japonské datumy v C#

Pokud potřebujete **vytvořit Excel sešit** od nuly, tento návod vám ukáže přesně jak. Naučíte se **nastavit hodnotu buňky** pomocí řetězce s japonským era datem, **aplikovat vlastní formát**, který rozumí éře, a nakonec **přečíst buňku s datem** a získat .NET `DateTime`. Kompletní příklad funguje s nejnovější verzí Aspose.Cells pro .NET, takže můžete kód zkopírovat‑vložit do libovolného C# projektu.

Práce s daty, která obsahují japonské éry, může být obtížná, protože výchozí parser Excelu nerozpoznává symboly éry. Použitím vlastního číselného formátu (`[ja-JP-Era]`) řeknete Excelu, jak řetězec interpretovat, což umožňuje spolehlivé **excel date parsing**. Níže uvedené kroky pokrývají celý workflow, od vytvoření sešitu až po extrakci data.

## Požadavky

- .NET 6.0 nebo novější (kód také běží na .NET Framework 4.7+)
- Aspose.Cells pro .NET (NuGet balíček `Aspose.Cells`)
- Základní znalost C# a Visual Studio nebo libovolného IDE dle vašeho výběru

## Krok 1: Vytvořit Excel sešit a přidat list

Prvním krokem je **vytvořit Excel sešit** v paměti. Aspose.Cells automaticky vytvoří výchozí list, ale můžete přidat další podle potřeby.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateExample
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // Optional: rename the default worksheet for clarity
        workbook.Worksheets[0].Name = "Dates";
```

Vytvoření sešitu alokuje interní struktury, které později obsahují buňky, styly a vzorce. V tomto okamžiku se žádný soubor neukládá, což zajišťuje rychlou a testovatelnou operaci.

## Krok 2: Nastavit hodnotu buňky s řetězcem japonské éry

Dále **nastavte hodnotu buňky** na japonskou era reprezentaci `"R5-04-01"` (Reiwa 5, 1. duben). Řetězec následuje vzor `EraYear-MM-DD`.

```csharp
        // Step 2: Reference cell A1 on the first worksheet
        Cell dateCell = workbook.Worksheets[0].Cells["A1"];

        // Put the Japanese era date string into the cell
        dateCell.PutValue("R5-04-01");
```

Použití `PutValue` uloží surový text. Excel s ním bude zacházet jako s řetězcem, dokud ho neovlivní číselný formát. Tento přístup funguje pro jakoukoliv vlastní kalendářní reprezentaci, nejen pro japonské éry.

## Krok 3: Aplikovat vlastní číselný formát, který rozumí japonské éře

Nyní **aplikujte vlastní formát**, aby Excel mohl převést řetězec éry na skutečné sériové datum. Formát `[ja-JP-Era]yyyy/MM/dd` říká enginu, aby interpretoval úvodní znak éry (`R` pro Reiwa) a vypočítal gregoriánské datum.

```csharp
        // Step 3: Apply a custom number format for Japanese era parsing
        dateCell.Style.Custom = "[ja-JP-Era]yyyy/MM/dd";
```

Vlastní formát je uložen v objektu stylu buňky. Aspose.Cells respektuje tento formát během renderování i konverze hodnot, což umožňuje spolehlivé **excel date parsing** později v pipeline.

## Krok 4: Získat parsovanou hodnotu DateTime z buňky

Nakonec **přečtěte buňku s datem**, abyste získali .NET `DateTime`. Vlastnost `DateTimeValue` vrací převedenou hodnotu na základě dříve aplikovaného vlastního formátu.

```csharp
        // Step 4: Retrieve the parsed DateTime value
        DateTime parsedDate = dateCell.DateTimeValue;

        // Output the result to the console for verification
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
```

Po spuštění programu se v konzoli vypíše:

```
Parsed Gregorian date: 2023-04-01
```

Výstup potvrzuje, že řetězec japonské éry `"R5-04-01"` byl správně interpretován jako 1. duben 2023.

## Kompletní, spustitelný příklad

Sestavením všech částí získáte samostatný program, který můžete okamžitě zkompilovat a spustit.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateExample
{
    static void Main()
    {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Reference cell A1
        Cell dateCell = workbook.Worksheets[0].Cells["A1"];

        // Insert Japanese era date string
        dateCell.PutValue("R5-04-01");

        // Apply custom format for Japanese era parsing
        dateCell.Style.Custom = "[ja-JP-Era]yyyy/MM/dd";

        // Retrieve the parsed DateTime
        DateTime parsedDate = dateCell.DateTimeValue;

        // Show the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");

        // (Optional) Save the workbook to verify the visual format
        workbook.Save("JapaneseEraDate.xlsx");
    }
}
```

Po spuštění programu se vytvoří soubor `JapaneseEraDate.xlsx` s buňkou A1 zobrazující `2023/04/01`, zatímco konzole ukáže stejný gregoriánský datum. Soubor lze otevřít v Excelu a vidět formátovanou hodnotu.

## Proč tento přístup funguje

- **create excel workbook** – Instancování `Workbook` vytvoří kompletní strukturu Excel souboru v paměti, aniž by se dotklo disku.
- **set cell value** – `PutValue` uloží surový text, což je nutné před aplikací kulturně specifického formátu.
- **apply custom format** – Token `[ja-JP-Era]` propojuje notaci éry s interním sériovým datovým systémem Excelu.
- **read date cell** – `DateTimeValue` automaticky použije styl buňky k provedení konverze a vrátí nativní `DateTime`.
- **excel date parsing** – Delegováním parsování na styl buňky se vyhnete ruční manipulaci s řetězci, snižujete počet chyb a zlepšujete podporu locale.

## Okrajové případy a praktické tipy

- **Různé éry** – Použijte `S` pro Showa, `H` pro Heisei, `R` pro Reiwa. Stejný formátovací řetězec funguje pro všechny éry.
- **Neplatné řetězce** – Pokud buňka obsahuje špatně formátované datum éry, `DateTimeValue` vrátí `DateTime.MinValue`. Před čtením zkontrolujte `dateCell.IsDate`.
- **Více buněk** – Aplikujte vlastní formát na celý rozsah (`range.ApplyStyle(style)`) když potřebujete parsovat mnoho datumů.
- **Výkon** – Nastavení stylu jednou na sloupec je rychlejší než na každou buňku u velkých listů.
- **Možnosti ukládání** – Aspose.Cells může exportovat do XLSX, XLS, CSV nebo PDF. Vyberte formát, který odpovídá dalšímu zpracování.

## Často kladené otázky

**Mohu použít vestavěnou .NET kulturu místo vlastního formátu?**  
Třída .NET `CultureInfo` nerozumí japonským symbolům éry stejným způsobem jako Excel. Použití vlastního číselného formátu je nejspolehlivější metoda pro **excel date parsing** řetězců s érou.

**Co když potřebuji zapsat datum zpět do Excelu ve formátu éry?**  
Nastavte hodnotu buňky na `DateTime` a aplikujte stejný vlastní formát. Excel automaticky zobrazí éru.

**Funguje to i ve starších verzích Excelu?**  
Token `[ja-JP-Era]` je podporován v Excelu 2010 a novějším. Aspose.Cells tuto funkci emuluje, takže se sešit zobrazuje správně i v starších verzích Excelu, které nemají nativní podporu éry.

## Závěr

Nyní víte, jak **vytvořit Excel sešit**, **nastavit hodnotu buňky** s řetězcem japonské éry, **aplikovat vlastní formát** a **přečíst buňku s datem**, abyste získali `DateTime`. Tento vzor poskytuje robustní **excel date parsing** bez ruční manipulace s řetězci, což činí váš C# automatizační kód stručný a spolehlivý.

Dále prozkoumejte související témata jako **formátování více sloupců s daty**, **práce s jinými kulturními kalendáři** nebo **export sešitu do PDF**. Každé rozšíření staví na stejných principech, takže můžete řešení přizpůsobit široké škále lokalizačních scénářů. Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, která vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Create Excel Workbook in C# – Apply Custom Number Format](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/)
- [Create Excel Workbook with Custom Format – C# Guide](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-custom-format-c-guide/)
- [Excel Automation with Aspose.Cells .NET: Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}