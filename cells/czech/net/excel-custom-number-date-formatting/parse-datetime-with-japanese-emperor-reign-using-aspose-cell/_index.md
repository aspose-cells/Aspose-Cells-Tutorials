---
category: general
date: 2026-09-24
description: Rozparsujte DateTime s japonským obdobím vlády císaře pomocí Aspose.Cells
  v C#. Povolte japonský kalendář éry, zapisujte řetězce éry a získejte přesné hodnoty
  DateTime.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Parse DateTime with Japanese Emperor Reign
- Aspose.Cells
- C# date parsing
- Japanese era calendar
- Workbook Settings
- DateTimeValue
language: cs
lastmod: 2026-09-24
og_description: Zpracujte DateTime s japonským obdobím vlády císaře pomocí Aspose.Cells
  v C#. Tento tutoriál ukazuje, jak povolit japonský kalendář era, zapisovat řetězce
  era a načíst zpět správný DateTime.
og_image_alt: Screenshot of C# code parsing a Japanese era date with Aspose.Cells
og_title: Rozparsování DateTime s japonským císařským obdobím pomocí Aspose.Cells
  – průvodce pro C#
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  headline: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  type: TechArticle
- description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  name: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  steps:
  - name: Multiple era formats
    text: 'Aspose.Cells recognises several era representations:'
  - name: Invalid strings
    text: 'When the string cannot be parsed (e.g., `"令和99年13月40日"`), `DateTimeValue`
      returns `DateTime.MinValue`. You can check for this condition:'
  - name: Disabling the feature
    text: 'If you later need to store raw era strings without conversion, set the
      flag back to `false`:'
  - name: Performance tip
    text: Enabling the era calendar adds a small overhead to every `PutValue` call
      that involves strings. If you only parse a handful of cells, enable the flag
      right before the operation and disable it afterward to minimise impact.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DateTime
- Japanese era
- .NET
title: Rozebrat datum a čas s japonským obdobím vlády císaře pomocí Aspose.Cells
url: /cs/net/excel-custom-number-date-formatting/parse-datetime-with-japanese-emperor-reign-using-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rozparsování DateTime s japonským císařským obdobím pomocí Aspose.Cells

Pokud potřebujete **parsovat DateTime s japonským císařským obdobím** v .NET aplikaci, tento průvodce vám přesně ukáže, jak to provést pomocí Aspose.Cells. Povolením japonského kalendáře era, zápisem řetězce založeného na éře a načtením výsledné hodnoty `DateTime` získáte spolehlivé, kulturně citlivé datumy bez ruční manipulace s řetězci.

Práce s japonskými daty podle éry je běžná ve financích, vládě a starších systémech, které stále ukládají data jako “令和3年5月10日”. Tento tutoriál pokrývá kompletní workflow, od nastavení projektu po získání objektu `DateTime`, který můžete použít v výpočtech, logování nebo zobrazení v UI.

## Co se naučíte

- Jak přidat balíček Aspose.Cells NuGet do projektu C#.
- Jak zapnout **japonský kalendář era** pomocí `Workbook.Settings`.
- Jak zapsat řetězec japonského data podle éry do buňky a nechat Aspose.Cells jej automaticky parsovat.
- Jak načíst parsovaný `DateTime` pomocí vlastnosti `DateTimeValue`.

**Požadavky**  
- .NET 6.0 nebo novější (kód také funguje s .NET Framework 4.7+).  
- Základní znalost C# a Visual Studio (nebo jakéhokoli IDE).  
- Přístup k internetu pro stažení balíčku Aspose.Cells.

---

## Krok 1: Instalace Aspose.Cells

Otevřete složku projektu v terminálu nebo v konzoli NuGet Package Manager a spusťte:

```bash
dotnet add package Aspose.Cells
```

Nebo ve Visual Studiu klikněte pravým tlačítkem na projekt → **Manage NuGet Packages** → vyhledejte **Aspose.Cells** a klikněte na **Install**.  
To přidá sestavení `Aspose.Cells`, které poskytuje `Workbook`, `Worksheet` a funkce parsování, které potřebujeme.

## Krok 2: Povolení japonského kalendáře era

Aspose.Cells ve výchozím nastavení zakazuje parsování japonské éry. Musíte jej zapnout pomocí příznaku `Workbook.Settings.UseJapaneseEraCalendar`.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Enable parsing of Japanese era dates (e.g., 令和, 平成)
        workbook.Settings.UseJapaneseEraCalendar = true;
```

Nastavení `UseJapaneseEraCalendar` na `true` říká knihovně, aby interpretovala řetězce obsahující názvy éry (`令和`, `平成`, `昭和` atd.) podle oficiálních pravidel japonského kalendáře.

## Krok 3: Zapsání řetězce japonského data podle éry do buňky

Poté získejte první list a vložte řetězec japonského data podle éry do buňky **A1**.

```csharp
        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Write the era‑based date string into cell A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");
```

**Proč to funguje:**  
Když je `UseJapaneseEraCalendar` aktivní, `PutValue` prozkoumá řetězec, detekuje předponu éry (`令和`) a interně jej převede na odpovídající gregoriánský rok (2021). Knihovna pak uloží hodnotu jako skutečný objekt `DateTime`, nikoli jen text.

## Krok 4: Načtení parsované hodnoty `DateTime`

Nyní přečtěte `DateTimeValue` buňky. Aspose.Cells automaticky vrátí gregoriánské datum.

```csharp
        // Retrieve the parsed DateTime from cell A1
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Output the result to the console
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
    }
}
```

Spuštění programu vypíše:

```
Parsed Gregorian date: 2021-05-10
```

Výstup potvrzuje, že **Parse DateTime with Japanese Emperor Reign** správně převedl “令和3年5月10日” na 10. května 2021.

## Krok 5: Zpracování okrajových případů a běžných variant

### Více formátů éry
Aspose.Cells rozpoznává několik reprezentací éry:

| Éra (japonština) | Rozsah gregoriánských let |
|------------------|---------------------------|
| 明治 (Meiji)   | 1868‑1912            |
| 大正 (Taishō)  | 1912‑1926            |
| 昭和 (Shōwa)   | 1926‑1989            |
| 平成 (Heisei)  | 1989‑2019            |
| 令和 (Reiwa)   | 2019‑present         |

Pokud vaše zdrojová data kombinují znaky s plnou šířkou, mezery nebo používají kanji „年“, „月“, „日“, parser stále úspěšně funguje. Například, `"平成31年4月30日"` se převede na `2019-04-30`.

### Neplatné řetězce
Když řetězec nelze parsovat (např. `"令和99年13月40日"`), `DateTimeValue` vrátí `DateTime.MinValue`. Můžete tuto podmínku zkontrolovat:

```csharp
if (parsedDate == DateTime.MinValue)
{
    Console.WriteLine("The cell does not contain a valid Japanese era date.");
}
```

### Zakázání funkce
Pokud později potřebujete uložit surové řetězce éry bez konverze, nastavte příznak zpět na `false`:

```csharp
workbook.Settings.UseJapaneseEraCalendar = false;
```

### Tip pro výkon
Povolení kalendáře éry přidává malou režii ke každému volání `PutValue`, které zahrnuje řetězce. Pokud parsujete jen několik buněk, zapněte příznak těsně před operací a po ní jej vypněte, aby se dopad minimalizoval.

## Kompletní, spustitelný příklad

Níže je celý program, který můžete zkopírovat, vložit a okamžitě spustit.

```csharp
using Aspose.Cells;
using System;

class ParseJapaneseEraDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Turn on Japanese era parsing
        workbook.Settings.UseJapaneseEraCalendar = true;

        // 3️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 4️⃣ Write an era date string into A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");

        // 5️⃣ Retrieve the parsed DateTime
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
        // Expected output: Parsed Gregorian date: 2021-05-10
    }
}
```

**Očekávaný výstup**

```
Parsed Gregorian date: 2021-05-10
```

Program demonstruje kompletní tok pro **Parse DateTime with Japanese Emperor Reign** pomocí Aspose.Cells, od vytvoření sešitu až po získání použitelného objektu `DateTime`.

---

## Závěr

Nyní víte, jak **parsovat DateTime s japonským císařským obdobím** v C# pomocí:

1. Instalace **Aspose.Cells**.  
2. Povolení **japonského kalendáře era** pomocí `Workbook.Settings`.  
3. Zápis řetězců založených na éře do buněk.  
4. Čtení výsledné `DateTimeValue`.  

Tento přístup eliminuje ruční logiku parsování, respektuje oficiální hranice éry a bezproblémově se integruje s existujícím .NET kódem pro práci s daty.  

**Další kroky**  
- Prozkoumejte další funkce specifické pro kulturu v Aspose.Cells, jako je **parsování dat v C#** pro hidžra nebo thajské buddhistické kalendáře.  
- Kombinujte tuto techniku s **Workbook Settings**, jako je `CalcEngine`, pro vyhodnocování vzorců odkazujících na data podle éry.  
- Použijte parsovaný `DateTime` v reportingu, ukládání do databáze nebo UI komponentách, které vyžadují gregoriánská data.  

Klidně experimentujte s různými řetězci éry, zpracovávejte neplatný vstup a integrujte řešení do větších datových importních pipeline. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Parsování japonských dat podle éry v Excelu – Kompletní průvodce pro vývojáře C#](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [Jak parsovat japonská data v C# – Kompletní průvodce](/cells/english/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/)
- [Jak implementovat validaci data v .NET pomocí Aspose.Cells: Komplexní průvodce](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}