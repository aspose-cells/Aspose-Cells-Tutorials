---
category: general
date: 2026-05-30
description: Povolte parsování japonských epoch v C# pomocí Aspose.Cells. Naučte se
  nastavit kulturu sešitu, parsovat data epoch a pracovat s japonským kalendářem v
  Excelových listech.
draft: false
keywords:
- enable japanese era parsing
- Aspose.Cells Japanese era
- set workbook culture
- parse era dates
- c# excel date parsing
language: cs
og_description: Povolte parsování japonských epoch v C# s Aspose.Cells. Tento průvodce
  ukazuje, jak nastavit kulturu sešitu, povolit podporu epoch a pracovat s japonskými
  daty.
og_title: Povolit parsování japonské éry v C# – Kompletní průvodce
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Enable Japanese era parsing in C# using Aspose.Cells. Learn to set
    workbook culture, parse era dates, and handle Japanese calendar in Excel worksheets.
  headline: Enable Japanese Era Parsing in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Povolit parsování japonských epoch v C# s Aspose.Cells
url: /cs/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Povolení parsování japonských érá v C# s Aspose.Cells

Už jste někdy potřebovali **enable japanese era parsing** při generování Excel souborů pro japonského klienta? Nejste jediní—mnoho vývojářů narazí na problém, když se v datech objeví starý japonský kalendář (令和, 平成, atd.). Dobrou zprávou je, že Aspose.Cells to udělá hračkou rozpoznat tyto datumy éry a převést je na standardní gregoriánské hodnoty.

V tomto tutoriálu projdeme přesně kroky k **enable japanese era parsing** pomocí Aspose.Cells, nastavíme kulturu sešitu na japonskou a vložíme datum formátované jako éra do buňky. Na konci budete mít spustitelný úryvek C#, který parsuje „令和3年5月1日“ na správný datumový objekt `2021‑05‑01`. Není potřeba žádná externí dokumentace—stačí zkopírovat, vložit a spustit.

## Požadavky

- .NET 6.0 nebo novější (kód funguje s .NET Core, .NET Framework a .NET 5+)
- Aspose.Cells pro .NET (NuGet balíček `Aspose.Cells`)
- Základní znalost C# — pokud umíte napsat `Console.WriteLine`, jste v pohodě
- IDE dle vašeho výběru (Visual Studio, VS Code, Rider…)

> **Tip:** Udržujte verzi Aspose.Cells aktuální; verze 24.10+ obsahuje nejnovější definice japonských érá.

## Proč povolit parsování japonských érá?

Japonské kalendáře používají éry spojené s imperiálními vládami. Ve většině moderních aplikací budete chtít ukládat data ve známém gregoriánském formátu, ale zdrojová data mohou stále přicházet jako „令和3年5月1日“. Pokud vynecháte **enable japanese era parsing**, řetězec bude považován za prostý text, což rozbije výpočty, řazení a tvorbu grafů. Zapnutím podpory éry Aspose.Cells automaticky převádí tyto řetězce na správné hodnoty `DateTime`, zachovává čitelnost pro japonské uživatele i číselnou správnost pro následné zpracování.

## Krok 1: Nastavte kulturu sešitu na japonskou

První věc, kterou musíte udělat, je říct Aspose.Cells, že výchozí locale sešitu je japonský (`ja-JP`). Tím zajistíte, že jakékoli kulturu specifické parsování (včetně názvů éry) bude podle japonských pravidel.

```csharp
using Aspose.Cells;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Set the workbook culture to Japanese (ja-JP)
        workbook.Settings.Culture = new CultureInfo("ja-JP");
```

> **Why this matters:** Objekt `CultureInfo` řídí formáty čísel, oddělovače dat a co je pro nás nejdůležitější, kalendářní systém používaný při parsování řetězců.

## Krok 2: Povolit parsování japonských érá

Nyní, když je kultura nastavena, musíte přepnout přepínač, který řekne Aspose.Cells, aby rozpoznával datumy éry. To je jádro **enable japanese era parsing**.

```csharp
        // Enable parsing of Japanese era dates (令和, 平成, 昭和, etc.)
        workbook.Settings.UseJapaneseEra = true;
```

> **Common pitfall:** Zapomenutí tohoto příznaku způsobí, že „令和3年5月1日“ zůstane jako doslovný řetězec. Když je zapnutý, Aspose.Cells automaticky mapuje éru na správný gregoriánský rok.

## Krok 3: Vložit datum formátované jako éra do buňky

S kulturou a podporou éry připravenou je vkládání japonského řetězce s érou jednoduché. Knihovna jej parsuje a uloží jako skutečnou hodnotu `DateTime`.

```csharp
        // Grab the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Insert a Japanese era date string into cell A1
        // The string "令和3年5月1日" becomes 2021‑05‑01 internally
        sheet.Cells["A1"].PutValue("令和3年5月1日");

        // Save the workbook to verify the result
        workbook.Save("JapaneseEraDemo.xlsx");
    }
}
```

### Očekávaný výstup

- **Buňka A1** v generovaném souboru `JapaneseEraDemo.xlsx` zobrazí **2021‑05‑01** (nebo lokalizovaný japonský formát data, pokud jej otevřete v Excelu s japonským locale).
- Základní hodnota je skutečný `DateTime`, takže ji můžete bezpečně použít ve vzorcích, kontingenčních tabulkách nebo dalších výpočtech v C#.

## Krok 4: Ověřit parsované datum programově (volitelné)

Pokud chcete dvojitě ověřit, že parsování uspělo před uložením, můžete buňku přečíst zpět:

```csharp
        // Retrieve the value as a DateTime
        DateTime parsedDate = sheet.Cells["A1"].GetDateTime();

        Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
        // Output: Parsed date: 2021-05-01
```

Tento malý ověřovací krok je užitečný v unit testech nebo při zpracování uživatelem poskytnutých Excel souborů.

## Okrajové případy a varianty

| Scénář | Co dělat |
|----------|------------|
| **Více érá v jednom sešitu** | Nechte `UseJapaneseEra = true`; Aspose.Cells rozpozná všechny podporované éry (令和, 平成, 昭和, 大正, 明治). |
| **Smíšené gregoriánské a érové řetězce** | Parser automaticky rozlišuje; gregoriánské řetězce zůstávají beze změny. |
| **Požadavky na vlastní kalendář** | Stále můžete nastavit `Workbook.Settings.Calendar` na konkrétní instanci `Calendar`, pokud potřebujete větší kontrolu. |
| **Starší verze .NET** | Stejný kód funguje na .NET Framework 4.6+; jen se ujistěte, že je k dispozici konstruktor `System.Globalization.CultureInfo`. |

## Praktické tipy pro reálné projekty

- **Ukládejte CultureInfo do cache**, pokud vytváříte mnoho sešitů v cyklu; opakované vytváření přidává režii.
- **Validujte vstup** před voláním `PutValue`; špatně formátované řetězce éry vyhodí výjimku.
- **Vypněte parsování éry** (`UseJapaneseEra = false`), když jste si jisti, že data nikdy neobsahují datumy v éře—může to mírně zlepšit výkon.
- **Použijte `Workbook.SaveOptions`** k řízení výstupního formátu (XLSX, XLS, CSV) při zachování parsovaného data.

## Kompletní funkční příklad (připravený ke kopírování a vložení)

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class EnableJapaneseEraParsingDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Set workbook culture to Japanese (ja-JP)
        workbook.Settings.Culture = new CultureInfo("ja-JP");

        // 3️⃣ Enable Japanese era parsing
        workbook.Settings.UseJapaneseEra = true;

        // 4️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 5️⃣ Insert an era‑formatted date
        sheet.Cells["A1"].PutValue("令和3年5月1日");

        // Optional: read back the parsed value
        DateTime dt = sheet.Cells["A1"].GetDateTime();
        Console.WriteLine($"Parsed date: {dt:yyyy-MM-dd}");

        // Save the workbook
        workbook.Save("EnableJapaneseEraParsing.xlsx");
    }
}
```

Spusťte program, otevřete vygenerovaný soubor a uvidíte **2021‑05‑01** v buňce A1—důkaz, že jsme úspěšně **enable japanese era parsing**.

## Závěr

Právě jsme ukázali, jak **enable japanese era parsing** v C# pomocí Aspose.Cells, nastavit kulturu sešitu a bez problémů převést datumy éry jako „令和3年5月1日“ na standardní gregoriánské hodnoty. Kroky jsou minimální, kód je samostatný a výsledek funguje v Excelu bezchybně.

Jste připraveni na další výzvu? Zkuste zkombinovat **set workbook culture** s formátováním čísel pro japonský jen, nebo vygenerujte vícelistový report, který kombinuje gregoriánská a érová data. Nyní máte základ pro zvládnutí jakýchkoli zvláštností japonského kalendáře ve vašich .NET Excel automatizačních projektech.

---

*Pokud vám tento průvodce pomohl, zvažte dát hvězdičku repozitáři Aspose.Cells na GitHubu nebo sdílet své tipy v komentářích. Šťastné kódování!*

## Co byste se měli naučit dál?

- [Načíst Excel sešity s kulturou‑specifickými daty pomocí Aspose.Cells pro .NET](/cells/english/net/formatting/load-workbook-culture-specific-dates-aspose-cells-net/)
- [Jak nastavit jazyk v Excel souborech pomocí Aspose.Cells .NET pro vícejazyčnou podporu](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [Načíst sešit s kulturou‑specifickými daty Aspose Cells .NET](/cells/chinese/net/formatting/load-workbook-culture-specific-dates-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}