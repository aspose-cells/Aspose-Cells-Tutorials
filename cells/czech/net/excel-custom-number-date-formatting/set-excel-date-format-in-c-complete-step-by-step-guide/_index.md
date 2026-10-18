---
category: general
date: 2026-02-28
description: Naučte se, jak nastavit formát data v Excelu, číst datum a čas v Excelu,
  extrahovat datum z Excelu a vypočítat vzorce sešitu pomocí Aspose.Cells v C#. Kompletní
  spustitelný příklad.
draft: false
keywords:
- set excel date format
- read excel datetime
- extract date from excel
- calculate workbook formulas
- get datetime cell
language: cs
og_description: Ovládněte nastavení formátu data v Excelu, čtení data a času, extrakci
  dat a výpočet vzorců v sešitu s kompletním příkladem v C#.
og_title: Nastavení formátu data v Excelu v C# – Kompletní průvodce krok za krokem
tags:
- Aspose.Cells
- C#
- Excel automation
title: Nastavte formát data v Excelu v C# – Kompletní průvodce krok za krokem
url: /cs/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# set excel date format – Complete C# Guide

Už jste někdy narazili na problém **nastavit formát data v Excelu**, když generujete tabulky za běhu? Nejste v tom sami. Mnoho vývojářů narazí na situaci, kdy buňka ukazuje surový řetězec místo správného data, zejména u japonských era dat nebo vlastních řetězců locale.

V tomto tutoriálu projdeme reálný příklad, který **nastaví formát data v Excelu**, poté **načte datum a čas z Excelu**, **extrahuje datum z Excelu** a dokonce **vypočítá vzorce sešitu**, abyste konečně **získali hodnoty buňky s datem a časem** jako nativní .NET `DateTime` objekty. Žádné externí odkazy, jen samostatný, spustitelný úryvek, který můžete vložit do Visual Studia a okamžitě vidět výsledek.

## Co budete potřebovat

- **Aspose.Cells for .NET** (jakákoli recentní verze; použité API funguje s 23.x a novějšími)  
- .NET 6 nebo novější (kód také kompiluje s .NET Framework 4.6+)  
- Základní znalost syntaxe C# – pokud umíte napsat `Console.WriteLine`, jste připraveni.

To je vše. Žádné další NuGet balíčky kromě Aspose.Cells, není potřeba instalace Excelu.

## Jak nastavit formát data v Excelu v C#

Prvním krokem je říct Excelu, že buňka obsahuje datum, ne jen text. Aspose.Cells poskytuje vestavěné ID číselného formátu (`14`), které odpovídá krátkému datovému vzoru aktuálního locale.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Step 2: Write a Japanese era date string into cell A1
        sheet.Cells["A1"].PutValue("Reiwa 2-04-01");

        // Step 3: Apply the standard date number format (ID 14) to A1
        // This tells Excel to treat the cell as a date.
        sheet.Cells["A1"].Style.Number = 14;

        // Step 4: Force Excel to recalculate formulas so the value is parsed
        workbook.CalculateFormula();

        // Step 5: Retrieve the parsed value as a .NET DateTime
        DateTime parsedDate = sheet.Cells["A1"].GetDateTime();

        // Step 6: Show the result – should be 2020‑04‑01
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
    }
}
```

> **Tip:** Volání `CalculateFormula()` je klíčové. Bez něj buňka stále obsahuje surový řetězec a `GetDateTime()` by vyhodilo výjimku. Tento řádek přinutí Aspose.Cells spustit svůj interní parser a efektivně **vypočítat vzorce sešitu** za nás.

Výstup, který uvidíte po spuštění programu, je:

```
Parsed DateTime: 2020-04-01
```

To potvrzuje, že jsme úspěšně **nastavili formát data v Excelu**, a že jsme dokázali **získat buňku s datem a časem** jako správný `DateTime`.

## Čtení hodnot datum‑čas z Excelu  

Nyní, když je datum uloženo správně, můžete se ptát, jak ho později načíst, třeba z existujícího souboru. Stejná metoda `GetDateTime()` funguje na každé buňce, která již má nastavený formát data.

```csharp
// Assuming 'sheet' is already loaded from an existing workbook
DateTime existingDate = sheet.Cells["B5"].GetDateTime();
Console.WriteLine($"Cell B5 contains: {existingDate:d}");
```

Pokud buňka není formátována jako datum, `GetDateTime()` vrátí `DateTime.MinValue`. Proto vždy **nejprve nastavte formát data v Excelu**.

## Extrahování data z buněk Excelu  

Někdy buňka obsahuje kompletní časové razítko (datum + čas), ale vy potřebujete jen část data. Časovou složku můžete oříznout pomocí `.Date` na vráceném `DateTime`.

```csharp
DateTime fullStamp = sheet.Cells["C3"].GetDateTime(); // e.g., 2023-07-15 14:30:00
DateTime onlyDate = fullStamp.Date;                  // 2023-07-15 00:00:00
Console.WriteLine($"Date only: {onlyDate:yyyy-MM-dd}");
```

Tento přístup funguje bez ohledu na podkladový číselný formát v Excelu, pokud je buňka rozpoznána jako datum.

## Výpočet vzorců sešitu  

Co když je datum výsledkem vzorce, např. `=TODAY()` nebo `=DATE(2022,5,10)`? Aspose.Cells vyhodnotí vzorec, když zavoláte `CalculateFormula()`. Poté se buňka chová přesně jako ručně zadané datum.

```csharp
sheet.Cells["D2"].Formula = "=TODAY()";
workbook.CalculateFormula(); // Re‑evaluate the sheet
DateTime today = sheet.Cells["D2"].GetDateTime();
Console.WriteLine($"Today is: {today:yyyy-MM-dd}");
```

Všimněte si, že nebylo nutné měnit styl buňky; Excel už považuje výsledek vzorce za datum, pokud vzorec vrátí sériové číslo, které odpovídá datu.

## Získání buňky s datum‑časem z existujícího sešitu  

Spojením všech částí získáte kompaktní rutinu, kterou můžete vložit do libovolného projektu, otevřít Excel soubor, zajistit, že všechny datumové buňky jsou správně interpretovány, a vrátit seznam objektů `DateTime`.

```csharp
using System.Collections.Generic;
using Aspose.Cells;

static List<DateTime> ExtractAllDates(string filePath)
{
    Workbook wb = new Workbook(filePath);
    Worksheet ws = wb.Worksheets[0];
    wb.CalculateFormula(); // Make sure formulas are evaluated

    var dates = new List<DateTime>();
    foreach (Cell cell in ws.Cells)
    {
        // Check if the cell has a date number format (ID 14‑22 are common date formats)
        if (cell.GetStyle().Number >= 14 && cell.GetStyle().Number <= 22)
        {
            dates.Add(cell.GetDateTime());
        }
    }
    return dates;
}
```

Volání `ExtractAllDates("Sample.xlsx")` vám vrátí každé datum, které bylo **správně nastaveno jako formát data v Excelu** v první listu.

## Časté úskalí a jak se jim vyhnout  

| Problém | Proč k tomu dochází | Řešení |
|---------|----------------------|--------|
| `GetDateTime()` vyhazuje `ArgumentException` | Buňka není rozpoznána jako datum (chybí číselný formát) | Použijte `Style.Number = 14` **před** voláním `CalculateFormula()` |
| Datum se zobrazuje jako `1900‑01‑00` | Sériové číslo 0 v Excelu je interpretováno jako epoch | Ujistěte se, že buňka skutečně obsahuje platné sériové číslo (>0) |
| Japonské era řetězce se neparsují | Aspose.Cells parsuje era řetězce až po `CalculateFormula()` | Nechte surový řetězec, nastavte formát data, pak zavolejte `CalculateFormula()` |
| Posuny časových pásem | `DateTime` je uložen bez informací o pásmu, ale aplikace může zobrazovat v jiném locale | Použijte `DateTimeKind.Utc` nebo provádějte explicitní konverzi podle potřeby |

## Obrázek – vizuální souhrn  

![příklad nastavení formátu data v Excelu](excel-date-format.png "příklad nastavení formátu data v Excelu")

Diagram ilustruje tok: **zapsat řetězec → aplikovat číselný formát → přepočítat → získat DateTime**.

## Závěr  

Probrali jsme vše, co potřebujete k **nastavení formátu data v Excelu**, **čtení datum‑časových hodnot z Excelu**, **extrahování data z Excelu**, **výpočtu vzorců sešitu** a nakonec **získání hodnot buňky s datum‑časem** jako nativních .NET objektů. Kompletní, spustitelný kód je připravený ke zkopírování a vložení a vysvětlení vám poskytují „proč“ za každým krokem, takže můžete vzor přizpůsobit složitějším scénářům.

### Co dál?

- **Hromadný import/export:** Použijte pomocnou metodu `ExtractAllDates` k dávkovému zpracování velkých reportů.  
- **Vlastní formáty data:** Nahraďte `Style.Number = 14` za `Style.Custom = "yyyy/mm/dd"` pro locale‑nezávislé formátování.  
- **Datumy s časovým pásmem:** Kombinujte `DateTimeOffset` se sériovými čísly Excelu pro globální aplikace.

Klidně experimentujte, přidejte podmíněné formátování nebo uložte data do databáze. Pokud narazíte na problémy, zanechte komentář – šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}