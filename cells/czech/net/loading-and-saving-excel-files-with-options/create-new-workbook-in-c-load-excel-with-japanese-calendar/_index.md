---
category: general
date: 2026-02-26
description: Vytvořte nový sešit v C# a naučte se, jak načíst soubory Excel, nastavit
  kalendář na japonský a snadno extrahovat datumy z Excelu.
draft: false
keywords:
- create new workbook
- how to load excel
- how to set calendar
- extract date from excel
- read japanese dates
language: cs
og_description: Vytvořte nový sešit v C# a rychle se naučte, jak načíst Excel, nastavit
  japonský kalendář a extrahovat data z Excel souborů.
og_title: Vytvořit nový sešit v C# – Načíst Excel s japonským kalendářem
tags:
- C#
- Excel
- Aspose.Cells
- DateTime
title: Vytvořit nový sešit v C# – Načíst Excel s japonským kalendářem
url: /cs/net/loading-and-saving-excel-files-with-options/create-new-workbook-in-c-load-excel-with-japanese-calendar/
---

.

Thus final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření nového sešitu v C# – Načtení Excelu s japonským kalendářem

Už jste někdy potřebovali **create new workbook** v C#, ale nebyli jste si jisti, jak přimět Excel respektovat japonský kalendář? Nejste v tom sami. V mnoha podnikovém scénářích obdržíte tabulky, které ukládají data v japonském systému éry, a jejich správné získání může připomínat dešifrování tajného jazyka.

Jde o to, že můžete **create new workbook**, říct načítači, aby interpretoval data pomocí japonského kalendáře, a pak **extract date from excel** pomocí několika řádků kódu. V tomto průvodci projdeme *how to load excel*, *how to set calendar* pro japonská data a nakonec *read Japanese dates* z buňky. Žádné zbytečnosti – jen kompletní, spustitelný příklad, který můžete zkopírovat a vložit do svého projektu.

## Požadavky

- .NET 6.0 nebo novější (kód funguje také na .NET Framework 4.6+)  
- Knihovna **Aspose.Cells** (bezplatná zkušební verze nebo licencovaná verze). Nainstalujte ji přes NuGet:

```bash
dotnet add package Aspose.Cells
```

- Excel soubor (`JapanDates.xlsx`), který obsahuje data v japonské éře v buňce A1.

To je vše. Pokud to máte, můžeme rovnou začít.

---

## Vytvoření nového sešitu a nastavení japonského kalendáře

Prvním krokem je **create new workbook** objekt a nakonfigurovat `LoadOptions`, aby parser věděl, který kalendář použít.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateReader
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // Step 2: Set load options to interpret dates using the Japanese calendar
        workbook.LoadOptions = new LoadOptions { Calendar = CalendarType.Japanese };

        // Step 3: Load the workbook from a file
        workbook.Load("YOUR_DIRECTORY/JapanDates.xlsx");

        // Step 4: Access cell A1 – it now contains a proper DateTime value
        var cellA1 = workbook.Worksheets[0].Cells["A1"];
        DateTime dateValue = cellA1.GetDateTime();

        Console.WriteLine($"The Japanese date in A1 is: {dateValue:yyyy-MM-dd}");
    }
}
```

> **Tip:** Vlastnost `LoadOptions.Calendar` přijímá několik výčtů (`Gregorian`, `Japanese`, `Hijri` atd.). Výběr správného zajistí, že knihovna přeloží text éry (např. “令和3年”) na .NET `DateTime`.

![screenshot příkladu vytvoření nového sešitu](image-url.png "Snímek obrazovky zobrazující novou instanci sešitu s nastavením japonského kalendáře"){: .align-center alt="screenshot příkladu vytvoření nového sešitu"}

### Proč to funguje

- **Workbook creation**: `new Workbook()` vám poskytne čistý start – žádné skryté listy, žádná výchozí data.
- **LoadOptions**: Přiřazením `CalendarType.Japanese` *před* voláním `Load` parser zachází s řetězci založenými na éře jako s daty, nikoli jako s prostým textem.
- **GetDateTime()**: Po načtení `cellA1.GetDateTime()` vrátí skutečný objekt `DateTime`, což vám umožní provádět aritmetiku, formátování nebo vkládání do databáze bez dalších konverzních kroků.

## Jak správně načíst Excel soubor

Možná se ptáte: „Existuje speciální způsob, jak **how to load excel** při práci s ne‑gregoriánskými kalendáři?“ Odpověď je ano – vždy nastavte `LoadOptions` *před* voláním `Load`. Pokud načtete nejprve a pak změníte kalendář, data už byla nesprávně parsována.

```csharp
// Example of a wrong order – will treat Japanese dates as plain strings
Workbook badWorkbook = new Workbook();
badWorkbook.Load("JapanDates.xlsx");          // Loads with default Gregorian calendar
badWorkbook.LoadOptions.Calendar = CalendarType.Japanese; // Too late!
```

Ukázka výše demonstruje běžnou chybu. Správné pořadí (jak je ukázáno v předchozí sekci) zajišťuje, že engine interpretuje buňky *jako data* již od začátku.

## Jak nastavit kalendář pro japonská data

Pokud potřebujete během běhu přepínat kalendáře – například při zpracování dávky souborů, které používají různé systémy éry – můžete znovu použít stejný objekt `Workbook` s novým `LoadOptions` pokaždé.

```csharp
void LoadWithCalendar(string filePath, CalendarType calendar)
{
    Workbook wb = new Workbook
    {
        LoadOptions = new LoadOptions { Calendar = calendar }
    };
    wb.Load(filePath);
    // Now you can read dates according to the chosen calendar
}
```

Volání `LoadWithCalendar("JapanDates.xlsx", CalendarType.Japanese)` přinese stejný výsledek jako náš hlavní příklad, zatímco `CalendarType.Gregorian` by stejnou buňku považovalo za prostý řetězec (nebo vyhodilo výjimku, pokud je formát nepoznatelný).

## Extrahování data z Excelu – čtení japonských dat

Nyní, když je sešit načten se správným kalendářem, získání data je jednoduché. Metoda `Cell.GetDateTime()` vrací `DateTime`, který respektuje konverzi éry.

```csharp
DateTime ExtractJapaneseDate(Workbook wb, string address)
{
    var cell = wb.Worksheets[0].Cells[address];
    return cell.GetDateTime(); // Returns a .NET DateTime
}

// Usage
DateTime japaneseDate = ExtractJapaneseDate(workbook, "A1");
Console.WriteLine($"Extracted date: {japaneseDate:d}");
```

### Okrajové případy a co‑když scénáře

| Situace                              | Co dělat                                                                                               |
|--------------------------------------|--------------------------------------------------------------------------------------------------------|
| Buňka obsahuje **text** místo data   | Nejdříve zavolejte `cell.GetString()`, ověřte pomocí `DateTime.TryParse` nebo v Excelu vynutíte validaci dat. |
| Je potřeba zpracovat více listů      | Procházejte `workbook.Worksheets` a aplikujte stejnou logiku extrakce na každý list.                   |
| Data jsou uložena jako **čísla** (Excel sériové) | `cell.GetDateTime()` stále funguje, protože Aspose.Cells automaticky převádí sériová čísla.            |
| Soubor je **chráněn heslem**         | Použijte `LoadOptions.Password = "yourPwd"` před voláním `Load`.                                      |

## Kompletní funkční příklad (připravený ke zkopírování a vložení)

Níže je kompletní program, který můžete vložit do konzolové aplikace. Obsahuje ošetření chyb a demonstruje všechna čtyři sekundární klíčová slova v kontextu.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateReader
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // 1️⃣  Create new workbook and configure calendar (primary keyword)
        // --------------------------------------------------------------------
        Workbook workbook = new Workbook
        {
            LoadOptions = new LoadOptions { Calendar = CalendarType.Japanese }
        };

        // --------------------------------------------------------------------
        // 2️⃣  How to load excel – correct order matters (secondary keyword)
        // --------------------------------------------------------------------
        try
        {
            workbook.Load("YOUR_DIRECTORY/JapanDates.xlsx");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load Excel file: {ex.Message}");
            return;
        }

        // --------------------------------------------------------------------
        // 3️⃣  How to set calendar – already done before loading (secondary)
        // --------------------------------------------------------------------
        // (If you need to change it later, see the LoadWithCalendar method above.)

        // --------------------------------------------------------------------
        // 4️⃣  Extract date from excel – read Japanese dates (secondary keywords)
        // --------------------------------------------------------------------
        try
        {
            var cell = workbook.Worksheets[0].Cells["A1"];
            DateTime japaneseDate = cell.GetDateTime(); // Proper DateTime thanks to the calendar setting
            Console.WriteLine($"Japanese date in A1 → {japaneseDate:yyyy-MM-dd}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error extracting date: {ex.Message}");
        }
    }
}
```

**Očekávaný výstup** (při předpokladu, že A1 obsahuje “令和3年5月12日”):

```
Japanese date in A1 → 2021-05-12
```

Pokud buňka obsahuje gregoriánské datum, např. “2021‑05‑12”, stejný kód stále funguje, protože knihovna se elegantně vrátí k gregoriánské interpretaci.

## Závěr

Nyní víte, jak **create new workbook**, správně **how to load excel**, nastavit vhodný **how to set calendar**, a nakonec **extract date from excel** při **read Japanese dates** bez jakéhokoli ručního parsování. Hlavní ponaučení je, že kalendář musí být definován *před* načtením; jakmile je sešit v paměti, data jsou již materializována jako správné objekty `DateTime`.

### Co dál?

- **Batch processing**: Procházejte složku souborů a pro každý zavolejte `LoadWithCalendar`.
- **Export to other formats**: Použijte `workbook.Save("output.csv")` po konverzi.
- **Localization**: Kombinujte `CultureInfo` s `DateTime.ToString` pro zobrazení dat v preferovaném jazyce uživatele.

Neváhejte experimentovat – vyměňte `CalendarType.Japanese` za `CalendarType.Hijri` nebo `CalendarType.Gregorian` a sledujte, jak se stejný kód automaticky přizpůsobí. Pokud narazíte na problémy, zanechte komentář níže nebo si prohlédněte dokumentaci Aspose.Cells pro podrobnější informace o API.

Šťastné programování a užívejte si převod těch tajemných japonských dat v éře na čisté .NET `DateTime` hodnoty!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}