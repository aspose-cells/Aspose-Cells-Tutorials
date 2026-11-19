---
category: general
date: 2026-11-19
description: Nastavte formát čísla buňky v C# a naučte se, jak použít formát data
  v Excelu pro japonské éry, což umožní spolehlivou konverzi dat v Excelu v C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set cell number format
- apply excel date format
- c# excel date conversion
- japanese era date excel
- aspose.cells date handling
language: cs
lastmod: 2026-11-19
og_description: Nastavte formát čísel buňky v C# a použijte formát data Excel pro
  japonské éry. Postupujte podle tohoto kompletního průvodce pro přesnou konverzi
  dat v C# a Excelu.
og_image_alt: Screenshot showing a C# code editor with set cell number format applied
  to an Excel cell
og_title: Nastavte formát čísel v buňce a převádějte japonské datumy v C# – průvodce
  krok za krokem
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  headline: Set cell number format and convert Japanese dates in C#
  type: TechArticle
- description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  name: Set cell number format and convert Japanese dates in C#
  steps:
  - name: Why this works
    text: '* `Style.Number = 14` maps to Excel’s *Short Date* format (`mm/dd/yyyy`
      by default). * When the cell contains a Japanese era string like `R3/04/01`,
      Aspose.Cells’ internal parser recognises the era and converts it to the corresponding
      Gregorian serial number during `CalculateFormula()`. * After the '
  - name: When to use a custom format
    text: '* Reports intended for Japanese audiences. * When you need to preserve
      the original era information for legal documents. * In dashboards where both
      Gregorian and era dates are shown side‑by‑side.'
  - name: Full end‑to‑end example
    text: Below is a self‑contained program that demonstrates both the Gregorian and
      era outputs in one run.
  - name: Edge cases & common pitfalls
    text: '| Situation | What to watch for | Fix / Recommendation | |----------------------------------------|------------------------------------------------------|----------------------------------------------------------|
      | Empty or malformed era string | `PutValue` stores the literal text; conversion
      fails'
  - name: Automation tip
    text: 'If you need to process a large range of era dates (e.g., column A contains
      many Japanese dates), wrap the conversion logic in a loop:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Date conversion
title: Nastavte formát čísla buňky a převádějte japonské datumy v C#
url: /cs/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nastavte formát čísla buňky a převádějte japonské datumy v C#

Pokud potřebujete **nastavit formát čísla buňky** v projektu automatizace Excelu v C#, tento průvodce vám ukáže, jak **použít formát data v Excelu** a provést **C# Excel převod data** pro japonské éry. Získáte kompletní, spustitelný příklad, který převádí řetězec z éry Reiwa (např. `R3/04/01`) na gregoriánské datum `2021‑04‑01`.

## Co se naučíte

* Jak vytvořit sešit a získat přístup k jeho prvnímu listu.  
* Jak **nastavit formát čísla buňky**, aby Excel považoval hodnotu za datum.  
* Jak **použít formát data v Excelu**, který rozpozná řetězce japonských epoch.  
* Jak spustit **C# Excel převod data** přepočítáním vzorců.  
* Očekávaný výstup a tipy na řešení problémů pro okrajové případy.

**Požadavky**

* .NET 6 nebo novější (kód také funguje s .NET Framework 4.6+).  
* Aspose.Cells pro .NET 2024 nebo novější – nainstalujte přes NuGet: `dotnet add package Aspose.Cells`.  
* Základní znalost C# a práce s daty v Excelu.

> **Tip:** Aspose.Cells funguje bez nainstalovaného Microsoft Office, což je ideální pro server‑side automatizaci.

## Nastavení formátu čísla buňky pomocí Aspose.Cells v C#

Prvním krokem je říci Excelu, že buňka obsahuje datum. Excel ukládá data jako sériová čísla, takže musíme na cílovou buňku použít vestavěný formát data (ID 14).

```csharp
using System;
using Aspose.Cells;

class JapaneseEraDateDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Insert a Japanese era date string (Reiwa 3) into cell A1
        sheet.Cells["A1"].PutValue("R3/04/01");

        // 3️⃣ **Set cell number format** – use built‑in date format ID 14
        //    This tells Excel to treat the string as a date value.
        sheet.Cells["A1"].Style.Number = 14;

        // 4️⃣ Recalculate formulas so the internal date engine converts the era.
        workbook.CalculateFormula();

        // 5️⃣ Output the converted Gregorian date.
        Console.WriteLine(sheet.Cells["A1"].StringValue); // → 2021-04-01
    }
}
```

### Proč to funguje

* `Style.Number = 14` odpovídá formátu *Short Date* v Excelu (`mm/dd/yyyy` ve výchozím nastavení).  
* Když buňka obsahuje řetězec japonské éry, např. `R3/04/01`, interní parser Aspose.Cells rozpozná éru a během `CalculateFormula()` ji převede na odpovídající gregoriánské sériové číslo.  
* Po výpočtu `StringValue` vrací naformátované gregoriánské datum.

## Použití formátu data v Excelu pro japonské datumy v éře

Pokud chcete, aby buňka zobrazovala japonskou éru místo gregoriánského data, můžete použít vlastní číselný formát, který zahrnuje kód éry. Toto demonstruje schopnost **apply excel date format**.

```csharp
// Apply a custom format that forces the Japanese era display
sheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";

// Recalculate to apply the custom format
workbook.CalculateFormula();

// Output the era‑styled string
Console.WriteLine(sheet.Cells["A1"].StringValue); // → R3年04月01日
```

* `[$-ja-JP]` vynutí japonské národní prostředí.  
* `ggg` představuje název éry (např. `R` pro Reiwa).  
* Přidání doslovných znaků (`年`, `月`, `日`) vytvoří známé japonské rozložení data.

### Kdy použít vlastní formát

* Zprávy určené pro japonské publikum.  
* Když potřebujete zachovat původní informaci o éře pro právní dokumenty.  
* V dashboardech, kde jsou vedle sebe zobrazena jak gregoriánská, tak érová data.

## C# Excel převod data – práce s japonskými érami

Proces **c# excel date conversion** lze rozdělit na tři logické části:

1. **Rozparsovat řetězec éry** – Aspose.Cells automaticky rozpozná `R` (Reiwa), `H` (Heisei), `S` (Showa) atd.  
2. **Převést na sériové číslo** – Excel ukládá data jako dny od 30.12.1899.  
3. **Naformátovat sériové číslo** – buď vestavěným formátem (ID 14), nebo vlastním japonským formátem.

### Kompletní end‑to‑end příklad

Níže je samostatný program, který v jednom běhu ukazuje jak výstup v gregoriánském formátu, tak v érovém.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConversion
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Input: Reiwa 3 (2021) – can be any era string
        ws.Cells["A1"].PutValue("R3/04/01");

        // ---- Part 1: Gregorian output ----
        ws.Cells["A1"].Style.Number = 14;      // built‑in short date
        wb.CalculateFormula();                // forces conversion
        string gregorian = ws.Cells["A1"].StringValue;
        Console.WriteLine($"Gregorian: {gregorian}"); // 2021-04-01

        // ---- Part 2: Japanese era output ----
        ws.Cells["B1"].PutValue("R3/04/01");   // repeat input for clarity
        ws.Cells["B1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";
        wb.CalculateFormula();
        string era = ws.Cells["B1"].StringValue;
        Console.WriteLine($"Japanese era: {era}"); // R3年04月01日
    }
}
```

**Očekávaný výstup v konzoli**

```
Gregorian: 2021-04-01
Japanese era: R3年04月01日
```

### Okrajové případy a časté úskalí

| Situace                                 | Na co si dát pozor                                   | Oprava / Doporučení                                      |
|-----------------------------------------|------------------------------------------------------|----------------------------------------------------------|
| Prázdný nebo špatně formátovaný řetězec éry | `PutValue` ukládá doslovný text; převod selže       | Ověřte vstup pomocí regulárního výrazu před zápisem do buňky. |
| Neshoda národního prostředí             | Vlastní formát zobrazuje západní číslice místo japonských znaků | Zajistěte, aby vlastní formát (`Custom`) obsahoval `[$-ja-JP]` nebo nastavte `Workbook.Settings.CultureInfo` na `ja-JP`. |
| Sešit obsahuje vzorce odkazující na buňku s datem | Přepočet může přepsat výsledky vzorců               | Zavolejte `CalculateFormula` **po** všech krocích formátování, nebo použijte `Workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)`, pokud potřebujete přeskočit chyby. |
| Použití starších verzí Aspose.Cells      | Podpora japonských epoch byla přidána ve 3. čtvrtletí 2022 | Aktualizujte na nejnovější NuGet balíček.               |

## Testování řešení

1. **Spusťte program** z Visual Studio nebo `dotnet run`.  
2. Ověřte, že konzole vypíše gregoriánské datum `2021‑04‑01` a řetězec éry `R3年04月01日`.  
3. Otevřete vygenerovaný sešit (pokud přidáte `wb.Save("Demo.xlsx");`) v Microsoft Excel a uvidíte stejný formát aplikovaný na buňky.

### Tip pro automatizaci

Pokud potřebujete zpracovat velký rozsah datumů v éře (např. sloupec A obsahuje mnoho japonských datumů), zabalte logiku převodu do smyčky:

```csharp
for (int row = 0; row < ws.Cells.MaxDataRow + 1; row++)
{
    var cell = ws.Cells[row, 0]; // column A
    cell.Style.Number = 14;
}
wb.CalculateFormula();
```

Tento přístup udržuje operaci **set cell number format** rychlou a paměťově úspornou.

## Závěr

Nyní víte, jak **nastavit formát čísla buňky** v C# pomocí Aspose.Cells, jak **použít formát data v Excelu** pro řetězce japonských epoch, a jak provést spolehlivý **C# Excel převod data** z éry na gregoriánská data. Kompletní, spustitelný kód ukazuje oba výstupy a zdůrazňuje běžné okrajové případy.

**Další kroky**

* Prozkoumejte další vestavěné ID formátů

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [nastavit formát data v Excelu v C# – Kompletní krok‑za‑krokem průvodce](/cells/english/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/)
- [Jak použít číselný formát v Excelu s Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)
- [Jak použít vlastní číselný formát v Excelu v C#](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}