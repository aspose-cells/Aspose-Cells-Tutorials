---
category: general
date: 2026-06-08
description: Rozparsujte japonské datum podle éry v C# pomocí Aspose.Cells. Naučte
  se, jak CultureInfo ja‑JP a formát japonské éry umožňují přesnou konverzi dat v
  Excelu.
draft: false
keywords:
- parse japanese era date
- Aspose.Cells
- CultureInfo ja-JP
- Japanese era format
- Excel date conversion
- C# DateTime parsing
language: cs
og_description: Rychle parsujte japonské datum podle éry v C#. Tento tutoriál ukazuje,
  jak CultureInfo ja‑JP a Aspose.Cells převádějí řetězce s érou na správné objekty
  DateTime.
og_title: Parsování japonského data éry v C# – Průvodce Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Parse Japanese era date in C# using Aspose.Cells. Learn how CultureInfo
    ja-JP and Japanese era format enable accurate Excel date conversion.
  headline: Parse Japanese Era Date in C# with Aspose.Cells – Full Guide
  type: TechArticle
- description: Parse Japanese era date in C# using Aspose.Cells. Learn how CultureInfo
    ja-JP and Japanese era format enable accurate Excel date conversion.
  name: Parse Japanese Era Date in C# with Aspose.Cells – Full Guide
  steps:
  - name: 5.1 Invalid or Empty Strings
    text: '```csharp string maybeDate = workbook.Worksheets[0].Cells["B1"].GetString();
      // could be empty if (string.IsNullOrWhiteSpace(maybeDate)) { Console.WriteLine("Cell
      B1 is empty – skipping."); } else { // Attempt to parse; catch format exceptions
      try { DateTime dt = DateTime.Parse(maybeDate, new Cultur'
  - name: 5.2 Older Eras (Showa, Taisho)
    text: 'The same `CultureInfo ja-JP` works for older eras automatically:'
  - name: 5.3 Using `DateTime.ParseExact` for Strict Validation
    text: 'If you want to enforce the exact Japanese era pattern, use a custom format
      string:'
  type: HowTo
- questions:
  - answer: Yes. As long as the workbook’s `Settings.CultureInfo` is set to `ja-JP`
      *before* you call `GetDateTime()`, Aspose.Cells will interpret the existing
      strings correctly.
    question: Does this work with .xlsx files that already contain era dates?
  - answer: The parsing returns a `DateTime` with `Kind = Unspecified`. If you need
      UTC or local time, apply `DateTime.SpecifyKind` or convert after parsing.
    question: What about time zones?
  - answer: Absolutely. Loop through the desired range and call `GetDateTime()` on
      each cell—just remember to handle exceptions for malformed entries.
    question: Can I parse multiple cells at once?
  type: FAQPage
tags:
- C#
- Excel
- DateTime
- Localization
title: Rozparsování japonského data podle éry v C# s Aspose.Cells – Kompletní průvodce
url: /cs/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Parsování japonského data éry v C# s Aspose.Cells – Kompletní průvodce

Už jste někdy potřebovali **parse japanese era date** řetězce přímo z Excelu? Možná načítáte data ze starého systému, který stále používá „令和3年5月12日“ a chcete získat čistý `DateTime` pro tvorbu reportů. V tomto tutoriálu projdeme kompletní, připravený příklad, který převádí tyto řetězce ve stylu éry na správná data v C# – žádné hádání.

Budeme používat **Aspose.Cells**, výkonnou .NET knihovnu pro práci s Excelem, spolu s nastavením **CultureInfo ja-JP**, které umí číst japonské éry. Na konci budete mít znovupoužitelný úryvek, který zvládne „令和“, „平成“ a dokonce i starší éry bez potíží.

## Požadavky

- .NET 6.0 nebo novější (kód funguje také na .NET Framework 4.6+)  
- Aspose.Cells pro .NET (můžete si stáhnout bezplatnou zkušební verzi z NuGet: `Install-Package Aspose.Cells`)  
- Základní znalost C# – nic složitého, stačí konzolová aplikace  
- IDE dle vašeho výběru (Visual Studio, Rider, VS Code, atd.)

To je vše. Žádné další služby, žádné neznámé třetí strany.

## Krok 1: Nastavení projektu a přidání Aspose.Cells

Nejprve vytvořte novou konzolovou aplikaci:

```bash
dotnet new console -n JapaneseEraParser
cd JapaneseEraParser
dotnet add package Aspose.Cells
```

Nyní otevřete **Program.cs** a přidejte požadované jmenné prostory:

```csharp
using System;
using System.Globalization;
using Aspose.Cells;
```

> **Tip:** Pokud používáte Visual Studio, IDE vám automaticky navrhne přidání `using` direktiv po napsání názvů tříd.

## Krok 2: Vytvoření sešitu a nastavení japonské kultury

Klíč k **parse japanese era date** je nastavit Aspose.Cells, aby používalo správnou kulturu. Nastavení `CultureInfo` na `ja-JP` aktivuje parsování s ohledem na éry.

```csharp
// Step 2: Initialize a new workbook and set Japanese culture
Workbook workbook = new Workbook();
workbook.Settings.CultureInfo = new CultureInfo("ja-JP");
```

Proč je to důležité? Japonský kalendář má několik epoch (např. *Reiwa* (令和), *Heisei* (平成)). Objekt `CultureInfo` obsahuje `JapaneseCalendar`, který zná počáteční data jednotlivých epoch, takže jakýkoli řetězec ve formátu japonské éry může být správně interpretován.

## Krok 3: Zapsání řetězce japonského data éry do buňky

Vložme ukázkové datum do buňky **A1**. Klidně změňte řetězec a vyzkoušejte různé epochy.

```csharp
// Step 3: Put a Japanese era date string into A1
string japaneseDate = "令和3年5月12日"; // Reiwa 3, May 12, 2021
workbook.Worksheets[0].Cells["A1"].PutValue(japaneseDate);
```

Pokud raději pracujete s existujícím sešitem, můžete jej načíst pomocí `new Workbook("path/to/file.xlsx")` a krok tvorby přeskočit.

## Krok 4: Získání hodnoty jako objektu C# DateTime

Nyní se děje magie. Voláním `GetDateTime()` Aspose.Cells přečte buňku s předem nastaveným `CultureInfo` a vrátí správný `DateTime`.

```csharp
// Step 4: Parse the cell value into a DateTime
DateTime parsedDate = workbook.Worksheets[0].Cells["A1"].GetDateTime();
Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

**Očekávaný výstup**

```
Parsed DateTime: 2021-05-12
```

To je celý **parse japanese era date** proces – čtyři stručné řádky kódu.

## Krok 5: Řešení okrajových případů a alternativních epoch

Reálná data nejsou vždy čistá. Zde je několik scénářů, na které můžete narazit, a jak je řešit.

### 5.1 Neplatné nebo prázdné řetězce

```csharp
string maybeDate = workbook.Worksheets[0].Cells["B1"].GetString(); // could be empty
if (string.IsNullOrWhiteSpace(maybeDate))
{
    Console.WriteLine("Cell B1 is empty – skipping.");
}
else
{
    // Attempt to parse; catch format exceptions
    try
    {
        DateTime dt = DateTime.Parse(maybeDate, new CultureInfo("ja-JP"));
        Console.WriteLine($"B1 parsed as {dt:yyyy-MM-dd}");
    }
    catch (FormatException)
    {
        Console.WriteLine($"Unable to parse '{maybeDate}' as a Japanese era date.");
    }
}
```

### 5.2 Starší epochy (Showa, Taisho)

Stejné `CultureInfo ja-JP` automaticky funguje i pro starší epochy:

```csharp
string showaDate = "昭和45年12月31日"; // Showa 45 = 1970-12-31
DateTime showaParsed = DateTime.Parse(showaDate, new CultureInfo("ja-JP"));
Console.WriteLine(showaParsed.ToString("yyyy-MM-dd")); // 1970-12-31
```

### 5.3 Použití `DateTime.ParseExact` pro přísnou validaci

Pokud chcete vynutit přesný vzor japonské epochy, použijte vlastní formátovací řetězec:

```csharp
string pattern = "ggggy年M月d日"; // gggg = era name, y = year in era
DateTime strictDate = DateTime.ParseExact(japaneseDate, pattern, new CultureInfo("ja-JP"));
Console.WriteLine(strictDate); // 2021-05-12 00:00:00
```

Tento přístup vyhodí `FormatException`, pokud řetězec neodpovídá, což může být užitečné pro kontrolu kvality dat.

## Kompletní funkční příklad

Níže je kompletní program, který můžete zkopírovat do **Program.cs** a spustit.

```csharp
using System;
using System.Globalization;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and set Japanese culture
        Workbook workbook = new Workbook();
        workbook.Settings.CultureInfo = new CultureInfo("ja-JP");

        // 2️⃣ Insert a Japanese era date string
        string japaneseDate = "令和3年5月12日";
        workbook.Worksheets[0].Cells["A1"].PutValue(japaneseDate);

        // 3️⃣ Parse the cell value into DateTime
        DateTime parsedDate = workbook.Worksheets[0].Cells["A1"].GetDateTime();
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");

        // 4️⃣ Demonstrate handling an older era
        string showaDate = "昭和45年12月31日";
        DateTime showaParsed = DateTime.Parse(showaDate, new CultureInfo("ja-JP"));
        Console.WriteLine($"Showa parsed: {showaParsed:yyyy-MM-dd}");

        // 5️⃣ Strict parsing with ParseExact
        string pattern = "gggy年M月d日";
        try
        {
            DateTime strict = DateTime.ParseExact(japaneseDate, pattern, new CultureInfo("ja-JP"));
            Console.WriteLine($"Strict parse: {strict:yyyy-MM-dd}");
        }
        catch (FormatException ex)
        {
            Console.WriteLine($"Strict parse failed: {ex.Message}");
        }
    }
}
```

Spusťte jej pomocí `dotnet run` a měli byste vidět:

```
Parsed DateTime: 2021-05-12
Showa parsed: 1970-12-31
Strict parse: 2021-05-12
```

Boom – **parse japanese era date** hotovo, a máte šablonu pro jakoukoli epochu, na kterou narazíte.

![Diagram postupu parsování japonského data éry – ukazuje vytvoření sešitu, nastavení kultury, zápis do buňky a volání GetDateTime](parse-japanese-era-date.png "Diagram ilustrující, jak parsovat japonské datum éry pomocí Aspose.Cells a CultureInfo ja-JP")

## Často kladené otázky

- **Funguje to s .xlsx soubory, které již obsahují data v epochách?**  
  Ano. Dokud je `Settings.CultureInfo` sešitu nastaveno na `ja-JP` *před* voláním `GetDateTime()`, Aspose.Cells správně interpretuje existující řetězce.

- **Co s časovými pásmy?**  
  Parsování vrací `DateTime` s `Kind = Unspecified`. Pokud potřebujete UTC nebo lokální čas, použijte `DateTime.SpecifyKind` nebo po parsování konverzi.

- **Mohu parsovat více buněk najednou?**  
  Rozhodně. Projděte požadovaný rozsah a zavolejte `GetDateTime()` pro každou buňku – jen nezapomeňte ošetřit výjimky u špatně formátovaných položek.

## Závěr

Probrali jsme vše, co potřebujete k **parse japanese era date** řetězcům v C# s pomocí Aspose.Cells a vestavěného `CultureInfo ja-JP`. Od nastavení sešitu, zápisu řetězců ve formátu epoch, získání čistého `DateTime` až po řešení okrajových případů jako starší epochy a přísná validace – tento průvodce vám poskytuje řešení připravené do produkce.

Dále můžete zkoumat **Excel konverzi dat** pro číselné sériové datumy, nebo se ponořit do **C# DateTime parsování** s vlastním kalendářem pro jiné lokály. Stejný vzor funguje pro thajský buddhistický kalendář, hebrejský kalendář a další – stačí vyměnit `CultureInfo`.

Máte nějaký specifický problém? Zanechte komentář a pojďme to společně vyřešit. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Jak implementovat validaci dat v .NET pomocí Aspose.Cells: Komplexní průvodce](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Změna systému dat v Excelu na 1904 pomocí Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [Efektivní konverze Excelu do PDF s vlastními formáty dat pomocí Aspose.Cells pro Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}