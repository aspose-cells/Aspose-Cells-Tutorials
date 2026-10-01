---
category: general
date: 2026-10-01
description: Převod japonského data podle éry na gregoriánské DateTime pomocí Aspose.Cells
  v C#. Naučte se rychle převádět japonský kalendář.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert japanese era date
- how to convert japanese calendar
language: cs
lastmod: 2026-10-01
og_description: převést japonské datum éry na gregoriánské DateTime v C#. Tento tutoriál
  vysvětluje, jak přesně převést japonský kalendář pomocí Aspose.Cells.
og_image_alt: Code example converting a Japanese era date string to a Gregorian DateTime
  in a C# console app
og_title: Převod japonského data podle éry na gregoriánské v C# – průvodce krok za
  krokem
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  headline: How to convert Japanese era date to Gregorian in C#
  type: TechArticle
- description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  name: How to convert Japanese era date to Gregorian in C#
  steps:
  - name: Why each step matters
    text: '| Step | Purpose | How it helps the conversion | |------|---------|-----------------------------|
      | **Create workbook** | Provides a container that understands Excel formulas
      and date systems. | The library’s internal date engine is activated only inside
      a workbook. | | **Insert era string** | Suppl'
  - name: Handling invalid or ambiguous strings
    text: '* **Invalid era name** – Aspose.Cells throws a `FormatException`. Wrap
      the conversion in `try/catch` to provide a friendly error message. * **Missing
      year/month/day** – The library expects a full “Era Year/Month/Day” pattern.
      If you receive partial data, prepend missing parts or reject the input ear'
  - name: Next steps
    text: '* Explore **formatting options** to write the Gregorian date back into
      the worksheet with a custom number format. * Combine this conversion with **data
      import pipelines** (e.g., reading CSV files that contain era dates). * Review
      other Aspose.Cells features such as **date arithmetic** and **regional'
  type: HowTo
tags:
- Aspose.Cells
- C#
- date conversion
title: Jak převést japonské datum podle éry na gregoriánské v C#
url: /cs/net/excel-custom-number-date-formatting/how-to-convert-japanese-era-date-to-gregorian-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak převést datum japonské éry na gregoriánské v C#

Pokud potřebujete **převést řetězce s datem japonské éry** na gregoriánská data v C#, tento návod vám ukáže přesně jak na to. Ať už zpracováváte historická data, čtete vstup od uživatele nebo generujete zprávy, knihovna Aspose.Cells usnadňuje konverzi. Navíc se dozvíte nejlepší způsob, **jak převést japonský kalendář** při práci s tabulkami.

Tutoriál pokrývá každý krok – od vytvoření sešitu až po získání hodnoty `DateTime` – takže můžete zkopírovat a spustit kompletní, funkční program. Nepotřebujete žádnou externí dokumentaci; stačí sledovat kód a vysvětlení níže.

## Požadavky

Než začnete, ujistěte se, že máte:

* .NET 6.0 nebo novější (kód funguje také s .NET Framework 4.6+)
* Licenci na **Aspose.Cells** (bezplatná zkušební verze stačí pro testování)
* Vývojové prostředí jako Visual Studio 2022 nebo VS Code
* Základní znalosti C# konzolových aplikací

## Převod japonského data s Aspose.Cells

Jádro konverze spočívá v několika jednoduchých voláních API. Aspose.Cells automaticky interpretuje řetězce japonské éry (např. „Reiwa 2/04/01“) a výsledek poskytuje jako objekt `DateTime` po přepočítání listu.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                // creates an empty Excel file in memory
        var worksheet = workbook.Worksheets[0];       // the default sheet is at index 0

        // Step 2: Insert a Japanese era date string into cell A1
        // The string follows the Japanese calendar format: Era Year/Month/Day
        worksheet.Cells[0, 0].PutValue("Reiwa 2/04/01");

        // Step 3: Apply a default style to the cell (required for proper calculation)
        // Without a style, Aspose.Cells may treat the content as plain text and skip conversion.
        worksheet.Cells[0, 0].SetStyle(workbook.CreateStyle());

        // Step 4: Recalculate the worksheet so the date string is converted to a Gregorian date
        // The Calculate method parses the era string and updates the cell's internal value.
        worksheet.Calculate();

        // Step 5: Retrieve and display the converted DateTime value (2020‑04‑01)
        DateTime gregorian = worksheet.Cells[0, 0].DateTimeValue;
        Console.WriteLine($"Gregorian date: {gregorian:yyyy-MM-dd}");
    }
}
```

### Proč je každý krok důležitý

| Krok | Účel | Jak pomáhá při konverzi |
|------|------|------------------------|
| **Create workbook** | Poskytuje kontejner, který rozumí Excelovým vzorcům a datovým systémům. | Interní datumový engine knihovny je aktivován pouze uvnitř sešitu. |
| **Insert era string** | Dodává surový text japonského kalendáře, který chcete převést. | Aspose.Cells rozpozná názvy epoch jako *Reiwa*, *Heisei*, *Showa* atd. |
| **Set style** | Vynutí, aby buňka byla považována za hodnotovou, nikoli za doslovný řetězec. | Bez nastavení stylu může metoda `Calculate` buňku ignorovat a text zůstane nezměněn. |
| **Calculate** | Spustí parsování řetězce éry a konverzi na interní sériové číslo data. | Knihovna převádí „Reiwa 2/04/01“ → sériové číslo → gregoriánské `DateTime`. |
| **Read `DateTimeValue`** | Vrací převedený .NET objekt `DateTime`. | Nyní máte standardní `DateTime`, který můžete použít v jakémkoli .NET API. |

## Jak převést japonský kalendář v jiných scénářích

Stejný přístup funguje pro jakýkoli název japonské éry podporovaný Aspose.Cells:

```csharp
// Example: converting a Heisei era date
worksheet.Cells[0, 0].PutValue("Heisei 30/12/31"); // corresponds to 2018‑12‑31
worksheet.Calculate();
Console.WriteLine(worksheet.Cells[0, 0].DateTimeValue); // 2018-12-31
```

### Zpracování neplatných nebo nejednoznačných řetězců

* **Neplatný název éry** – Aspose.Cells vyhodí `FormatException`. Zabalte konverzi do `try/catch`, abyste poskytli uživatelsky přívětivou chybovou zprávu.
* **Chybějící rok/měsíc/den** – Knihovna očekává úplný vzor „Era Year/Month/Day“. Pokud obdržíte neúplná data, doplňte chybějící části nebo vstup odmítněte již na začátku.
* **Různá nastavení locale** – Konverze **nezávisí** na aktuální kultuře vlákna; vždy používá mapu japonských epoch zabudovanou v Aspose.Cells. To činí metodu bezpečnou pro server‑side zpracování.

```csharp
try
{
    worksheet.Cells[0, 0].PutValue(userInput);
    worksheet.Calculate();
    DateTime result = worksheet.Cells[0, 0].DateTimeValue;
    // Use result...
}
catch (FormatException ex)
{
    Console.WriteLine($"Unable to parse Japanese era date: {ex.Message}");
}
```

## Praktické tipy a časté úskalí

* **Vždy zavolejte `SetStyle`** před `Calculate`. Vynechání tohoto kroku je častým zdrojem chyb, protože buňka zůstane obyčejným textovým kontejnerem.
* **Znovu použijte stejný sešit**, pokud potřebujete převést mnoho dat. Vytváření nového sešitu pro každou konverzi přináší zbytečnou režii.
* **Dávková konverze** – Naplňte sloupec řetězci éry, zavolejte jednou `worksheet.Calculate()` a pak přečtěte celý sloupec `DateTimeValue`. Je to podstatně efektivnější než přepočítávat buňku po buňce.
* **Kompatibilita verzí** – Logika konverze éry byla zavedena v Aspose.Cells 22.9. Ujistěte se, že používáte tuto verzi nebo novější; starší verze řetězec zacházejí jako čistý text.

## Kompletní funkční příklad (konzolová aplikace)

Níže najdete samostatný program, který můžete okamžitě zkompilovat a spustit. Ukazuje konverzi jak pro Reiwa, tak pro Heisei a elegantně ošetřuje chyby.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConverter
{
    static void Main()
    {
        // Initialize workbook once
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        var style = workbook.CreateStyle();
        sheet.Cells[0, 0].SetStyle(style);
        sheet.Cells[1, 0].SetStyle(style);

        // Sample inputs
        string[] eraDates = { "Reiwa 2/04/01", "Heisei 30/12/31", "InvalidEra 1/01/01" };

        for (int i = 0; i < eraDates.Length; i++)
        {
            sheet.Cells[i, 0].PutValue(eraDates[i]);
        }

        // Perform conversion for all populated cells
        sheet.Calculate();

        // Output results
        for (int i = 0; i < eraDates.Length; i++)
        {
            try
            {
                DateTime dt = sheet.Cells[i, 0].DateTimeValue;
                Console.WriteLine($"{eraDates[i]} → {dt:yyyy-MM-dd}");
            }
            catch (Exception)
            {
                Console.WriteLine($"{eraDates[i]} → conversion failed");
            }
        }
    }
}
```

**Očekávaný výstup v konzoli**

```
Reiwa 2/04/01 → 2020-04-01
Heisei 30/12/31 → 2018-12-31
InvalidEra 1/01/01 → conversion failed
```

Spuštěním tohoto programu ověříte, že knihovna správně **převádí datum japonské éry** a elegantně hlásí nepodporované hodnoty.

## Závěr

Nyní víte, jak **převést řetězce s datem japonské éry** na standardní gregoriánské objekty `DateTime` pomocí Aspose.Cells v C#. Proces se zjednodušuje na vložení textu éry, nastavení stylu, přepočítání listu a načtení `DateTimeValue`. Dodržením výše uvedených kroků můžete také odpovědět na širší otázku **jak převést japonský kalendář** hromadně, ošetřit chyby a optimalizovat výkon.

### Další kroky

* Prozkoumejte **možnosti formátování**, jak zapsat gregoriánské datum zpět do listu s vlastním číselným formátem.
* Spojte tuto konverzi s **datovými importními pipeline** (např. čtení CSV souborů obsahujících data v éře).
* Prohlédněte si další funkce Aspose.Cells, jako **aritmetiku s daty** a **regionální nastavení** pro složitější kalendářní scénáře.

Šťastné programování a klidně upravte ukázku podle vlastních pracovních postupů!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vlastních projektech.

- [Parse Japanese Era Date in C# with Aspose.Cells – Full Guide](/cells/english/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/)
- [Enable Japanese Era Parsing in C# with Aspose.Cells](/cells/english/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/)
- [How to create workbook and convert string to date in C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-workbook-and-convert-string-to-date-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}