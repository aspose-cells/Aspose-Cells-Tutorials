---
category: general
date: 2026-03-30
description: Naučte se formátovat datum ve formátu ISO při čtení hodnot data a času
  v Excelu a extrahovat data a čas z Excelu pomocí Aspose.Cells v C#.
draft: false
keywords:
- format date iso
- read excel datetime
- extract datetime excel
- Aspose.Cells date parsing
- Japanese era dates
language: cs
og_description: formátovat datum ISO z dat Excel pomocí Aspose.Cells. Tento průvodce
  ukazuje, jak číst datum a čas v Excelu, extrahovat hodnoty data a času z Excelu
  a výstupní ISO data.
og_title: Formát ISO data z Excelu – krok po kroku C# tutoriál
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: Formát ISO data z Excelu – Kompletní C# průvodce
url: /cs/net/excel-custom-number-date-formatting/format-date-iso-from-excel-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# formátování data iso z Excelu – Kompletní průvodce C#

Už jste někdy potřebovali **format date iso** při získávání dat z listu Excel? Možná pracujete s japonskými daty er, nebo jen chcete čistý řetězec `yyyy‑MM‑dd` pro API payload. V tomto tutoriálu uvidíte přesně, jak **read Excel datetime** buňky, **extract datetime Excel** hodnoty, a převést je do formátu ISO‑8601 – bez hádání.

Provedeme vás reálným příkladem, který používá Aspose.Cells, vysvětlí, proč je každý řádek důležitý, a ukáže vám konečný výstup, který můžete zkopírovat a vložit do svého projektu. Na konci budete schopni zpracovat podivné řetězce er, jako je “令和3年5月1日”, a vytvořit standardní ISO datum, připravené pro databáze, JSON nebo kamkoli jej potřebujete.

## Požadavky

- .NET 6.0 nebo novější (kód funguje i s .NET Framework)
- Aspose.Cells pro .NET (bezplatná zkušební verze nebo licencovaná verze)
- Základní znalost C# a konceptů Excelu
- Visual Studio nebo jakýkoli C# editor, který máte rádi

Kromě Aspose.Cells nejsou vyžadovány žádné další NuGet balíčky, takže nastavení je poměrně jednoduché.

---

## Krok 1: Vytvořte Workbook a zaměřte se na první list

Prvním krokem je vytvořit nový objekt `Workbook`. Ten vám poskytne v‑paměti reprezentaci souboru Excel, kterou můžete následně upravovat nebo číst.

```csharp
using Aspose.Cells;
using System.Globalization;

// Step 1: Initialize a new workbook and grab the first worksheet
Workbook workbook = new Workbook();                 // creates an empty .xlsx
Worksheet worksheet = workbook.Worksheets[0];      // the default sheet is "Sheet1"
```

*Proč je to důležité:*  
Vytvoření workbooku programově vám umožní vyhnout se práci s fyzickými soubory během testování. Také zajišťuje, že odkaz na list je vždy platný – žádná neočekávaná null‑reference později, když se pokusíte **read Excel datetime** hodnoty.

## Krok 2: Zapište řetězec japonského data er do buňky

Naším cílem je ukázat parsování ne‑gregoriánského data. Řetězec er vložíme přímo do buňky **A1**.

```csharp
// Step 2: Insert a Japanese era date string into cell A1
worksheet.Cells["A1"].PutValue("令和3年5月1日");
```

*Tip:* Pokud získáváte data z existujícího workbooku, přeskočíte volání `PutValue` a jen odkážete na buňku, která již datum obsahuje. Klíčové je, že buňka obsahuje **string**, který představuje datum v japonském lunisolárním kalendáři.

## Krok 3: Nastavte kulturu, která rozumí japonskému lunisolárnímu kalendáři

Třída .NET `CultureInfo` vám umožňuje určit, jak mají být data interpretována. Výměnou výchozího gregoriánského kalendáře za `JapaneseLunisolarCalendar` poskytnete parseru potřebný kontext.

```csharp
// Step 3: Set up a culture using the Japanese lunisolar calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();
```

*Proč to děláme:*  
Pokud byste se pokusili parsovat “令和3年5月1日” s výchozí kulturou, .NET by vyhodil `FormatException`. Výměna za lunisolární kalendář řekne runtime přesně, jak mapovat “令和3年” (3. rok éry Reiwa) na gregoriánský rok 2021.

## Krok 4: Parsujte hodnotu buňky jako `DateTime` pomocí nastavené kultury

Nyní přichází jádro operace – převod řetězce er na správný objekt `DateTime`. Aspose.Cells poskytuje pohodlný přetížený `GetDateTime`, který přijímá `CultureInfo`.

```csharp
// Step 4: Retrieve the cell value as a DateTime, respecting the Japanese culture
DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);
```

*Co se děje pod kapotou:*  
`GetDateTime` načte surový řetězec, použije pravidla kalendáře poskytnuté kulturou a vrátí `DateTime`, který představuje stejný okamžik v gregoriánském kalendáři. To je okamžik, kdy **extract datetime Excel** data ve formě, se kterou můžete v .NET pracovat.

## Krok 5: Vypište parsované datum ve formátu ISO 8601

Nakonec formátujeme `DateTime` jako ISO řetězec – `yyyy‑MM‑dd` – který je univerzálně akceptován API, databázemi a front‑end frameworky.

```csharp
// Step 5: Print the date in ISO format (e.g., 2021-05-01)
Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // Output: 2021-05-01
```

*Proč ISO?*  
ISO 8601 odstraňuje nejednoznačnost. “05/01/2021” může být 1. května nebo 5. ledna v závislosti na locale. `2021-05-01` je naprosto jasné, proto **format date iso** používáme téměř ve všech integračních scénářích.

## Kompletní funkční příklad

Níže je kompletní, připravený k spuštění program. Zkopírujte jej do projektu konzolové aplikace, přidejte odkaz na Aspose.Cells a stiskněte **F5**.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and select the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date string into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // 3️⃣ Set up Japanese lunisolar culture
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();

        // 4️⃣ Parse the cell value as DateTime using the culture
        DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);

        // 5️⃣ Output the date in ISO format
        Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // 2021-05-01
    }
}
```

**Očekávaný výstup**

```
2021-05-01
```

Spusťte jej jednou a uvidíte ISO‑formátované datum vytištěné do konzole. To je celý proces od **read Excel datetime** po **format date iso**.

## Řešení běžných okrajových případů

### 1. Buňky obsahující skutečná Excel data jako čísla

Někdy Excel ukládá data jako sériová čísla (např. `44204`). V takovém případě nepotřebujete kulturu; stačí zavolat `GetDateTime()` bez parametrů:

```csharp
DateTime serialDate = worksheet.Cells["B2"].GetDateTime(); // B2 holds a numeric date
Console.WriteLine(serialDate.ToString("yyyy-MM-dd"));
```

### 2. Prázdné nebo neplatné buňky

Pokud je buňka prázdná nebo obsahuje neparsovatelný řetězec, `GetDateTime` vyhodí výjimku. Zabalte volání do `try/catch` nebo nejprve zkontrolujte `IsDateTime`:

```csharp
if (worksheet.Cells["C3"].Type == CellValueType.IsDateTime)
{
    DateTime safeDate = worksheet.Cells["C3"].GetDateTime();
    Console.WriteLine(safeDate.ToString("yyyy-MM-dd"));
}
else
{
    Console.WriteLine("Cell C3 does not contain a valid date.");
}
```

### 3. Různé formáty era

Další japonské éry (Heisei, Showa) následují stejný vzor. Stejný `JapaneseLunisolarCalendar` je automaticky zvládne, takže nepotřebujete další logiku – stačí předat řetězec.

## Pro tipy a úskalí

- **Performance:** Při zpracování velkých tabulek znovu použijte jedinou instanci `CultureInfo` místo vytváření nové uvnitř smyčky.
- **Thread Safety:** Objekt `CultureInfo` je po nastavení kalendáře jen pro čtení, takže je bezpečné jej sdílet mezi vlákny.
- **Aspose.Cells Licensing:** Pokud používáte bezplatnou zkušební verzi, pamatujte, že některé funkce mohou být omezené po vypršení zkušebního období. Parsování data zde funguje jak ve zkušební, tak licencované verzi.
- **Time Zones:** `DateTime`, který získáte, je **unspecified** (žádná časová zóna). Pokud potřebujete UTC, zavolejte `DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc)` nebo převést pomocí `TimeZoneInfo`.

## Závěr

Probrali jsme vše, co potřebujete k **format date iso** z Excelového sešitu pomocí C#. Začínáme s čistým japonským řetězcem er, **read Excel datetime**, nastavíme správnou kulturu, **extract datetime excel** data a nakonec vypíšeme čistý ISO‑8601 řetězec. Přístup funguje pro jakoukoli reprezentaci data, kterou Excel může nabídnout, ať už jde o sériové číslo, locale‑specifický řetězec nebo tradiční formát er.

Další kroky? Zkuste projít celou sloupec dat, zapsat ISO výsledky zpět do nového listu, nebo je přímo vložit do JSON payloadu pro webovou službu. Pokud vás zajímají jiné kalendářní systémy (hebrejský, islámský), Aspose.Cells a .NET `CultureInfo` usnadní i tyto experimenty.

Máte otázky nebo obtížný formát data, který se vám nedaří rozluštit? Zanechte komentář níže a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}