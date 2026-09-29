---
category: general
date: 2026-03-18
description: Extrahujte datum z Excelu a výstupní datum ve formátu yyyy‑mm‑dd v ISO.
  Naučte se číst japonská data podle éry, převádět je a zobrazovat ISO data v C#.
draft: false
keywords:
- extract date from excel
- output date yyyy-mm-dd
- display date iso format
language: cs
og_description: Extrahujte datum z Excelu a vypište ho ve formátu yyyy‑mm‑dd v ISO.
  Krok za krokem C# tutoriál s kompletním kódem a vysvětleními.
og_title: Extrahovat datum z Excelu – Výstup datum ve formátu yyyy‑mm‑dd v C#
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: Extrahujte datum z Excelu a výstup ve formátu yyyy‑mm‑dd – Kompletní průvodce
  C#
url: /cs/net/data-loading-and-parsing/extract-date-from-excel-and-output-date-yyyy-mm-dd-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování data z Excelu – Jak získat datum ve formátu yyyy‑mm‑dd v ISO

Už jste někdy potřebovali **extrahovat datum z Excelu**, ale nebyli jste si jisti, jak zacházet s japonskými érami nebo získat čistý řetězec `yyyy‑mm‑dd`? Nejste v tom sami. V mnoha projektech migrace dat zdrojová sešit ukládá data pomocí japonského kalendáře císaře a následný systém očekává datum ve formátu ISO, například `2024-04-01`.  

V tomto průvodci projdeme kompletním, spustitelným řešením, které načte buňku, interpretuje japonskou éru a **vypíše datum ve formátu yyyy‑mm‑dd**. Na konci přesně vědět, jak **zobrazit datum v ISO formátu** v jakékoli .NET aplikaci, a budete mít znovupoužitelný úryvek kódu, který můžete vložit do svého projektu.

## Co budete potřebovat

- **.NET 6+** (nebo .NET Framework 4.7.2+).  
- **Aspose.Cells for .NET** – knihovna, která nám umožňuje nastavit vlastní kalendář při načítání sešitu.  
- Excel soubor (`japan-date.xlsx`) obsahující datum uložené v buňce s japonskou érou (např. `令和3年4月1日`).  
- Oblíbené IDE – Visual Studio, Rider nebo i VS Code bude stačit.

Žádné další balíčky NuGet nejsou potřeba kromě Aspose.Cells a kód funguje na Windows, Linuxu i macOS.

## Krok 1: Nastavení projektu a instalace Aspose.Cells

```bash
dotnet new console -n ExcelDateDemo
cd ExcelDateDemo
dotnet add package Aspose.Cells
```

> **Tip:** Pokud běžíte na CI serveru, připněte verzi balíčku (`Aspose.Cells 23.12`), aby byly sestavení reprodukovatelné.

## Krok 2: Načtení sešitu s japonským kalendářem císaře

Klíčem k **extrahování data z Excelu**, když zdroj používá ne‑gregoriánský kalendář, je říci Aspose.Cells, který kalendář má při načítání použít. Děláme to pomocí `LoadOptions.Calendar`.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create load options and set the Japanese Emperor calendar
        LoadOptions loadOptions = new LoadOptions
        {
            // This tells Aspose.Cells to interpret era dates correctly
            Calendar = new JapaneseEmperorCalendar()
        };

        // Step 3: Open the workbook that contains Japanese era dates
        // Replace the path with the actual location of your Excel file
        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);
```

**Proč je to důležité:** Bez vlastního kalendáře by Aspose.Cells považoval buňku za obyčejný řetězec a ztratil by informaci o éře. Při přiřazení `JapaneseEmperorCalendar` knihovna automaticky převádí `令和3年4月1日` na `2021‑04‑01` na pozadí.

## Krok 3: Získání data ze specifické buňky

Nyní, když sešit ví, jak interpretovat éru, můžeme buňku načíst jako `DateTime`. Předpokládejme, že datum je v první listu, buňce **A1** (řádek 0, sloupec 0).

```csharp
        // Step 4: Retrieve the date value from the first worksheet, first cell
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0]; // A1

        // GetDateTime() returns a System.DateTime object
        DateTime extractedDate = dateCell.GetDateTime();
```

Pokud je buňka prázdná nebo obsahuje hodnotu, která není datum, `GetDateTime()` vyhodí výjimku. Obranný přístup vypadá takto:

```csharp
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        DateTime extractedDate = dateCell.GetDateTime();
```

**Okrajový případ:** Některé starší Excel soubory ukládají data jako čísla (sériová data). Aspose.Cells je zpracuje automaticky, ale měli byste stále ověřit typ buňky, pokud očekáváte smíšený obsah.

## Krok 4: Výstup data yyyy‑mm‑dd (ISO) a ověření

S `DateTime` v ruce je jeho formátování jako **výstup datum yyyy‑mm‑dd** jedním řádkem:

```csharp
        // Step 5: Output the date in ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

Spuštěním programu proti souboru, který obsahuje `令和3年4月1日`, se vytiskne:

```
Extracted date (ISO): 2021-04-01
```

To je přesný **zobrazovaný datum v iso formátu**, který vyžaduje mnoho API.

## Kompletní funkční příklad

Sestavením všech částí dohromady získáte kompletní, připravený program ke kopírování a vložení:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook with Japanese era support
        LoadOptions loadOptions = new LoadOptions
        {
            Calendar = new JapaneseEmperorCalendar()
        };

        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);

        // Access the cell that holds the date (A1)
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0];

        // Validate the cell contains a date
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        // Extract the DateTime value
        DateTime extractedDate = dateCell.GetDateTime();

        // Convert to ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

> **Poznámka:** Nahraďte `YOUR_DIRECTORY` skutečnou složkou obsahující `japan-date.xlsx`. Kód funguje s libovolným listem a libovolnou buňkou – stačí upravit indexy.

## Práce s dalšími kalendáři (volitelné)

Pokud někdy potřebujete **extrahovat datum z Excelu**, který používá thajský buddhistický kalendář nebo hebrejský kalendář, jednoduše vyměňte instanci kalendáře:

```csharp
loadOptions.Calendar = new ThaiBuddhistCalendar();   // for Thai dates
// or
loadOptions.Calendar = new HebrewCalendar();         // for Hebrew dates
```

Zbytek logiky zůstává nezměněn, což ukazuje flexibilitu tohoto přístupu.

## Časté úskalí a jak se jim vyhnout

| Problém | Proč se to děje | Řešení |
|-------|----------------|-----|
| `GetDateTime()` vyhodí `InvalidCastException` | Buňka není datum (možná řetězec) | Zkontrolujte `Cell.Type` před voláním, nebo použijte `DateTime.TryParse` na `Cell.StringValue`. |
| Špatný rok po konverzi | Načtený sešit bez nastavení `Calendar` | Vždy vytvořte `LoadOptions` s příslušným kalendářem **před** otevřením souboru. |
| ISO výstup zobrazuje časovou část (`2021-04-01 00:00:00`) | Použito `ToString()` bez formátovacího řetězce | Použijte formátovací řetězec `"yyyy-MM-dd"` k vynucení **výstupu datum yyyy‑mm‑dd**. |
| Soubor nenalezen | Relativní cesta ukazuje na špatnou složku | Použijte `Path.Combine(Environment.CurrentDirectory, "japan-date.xlsx")` nebo zadejte absolutní cestu. |

## Profesionální tipy pro produkční kód

1. **Ukládejte sešit do cache** pokud potřebujete načíst mnoho dat ze stejného souboru – otevření sešitu je relativně náročné.  
2. **Zabalte logiku extrakce** do znovupoužitelné metody:

   ```csharp
   static string ExtractIsoDate(string file, int sheetIdx, int row, int col)
   {
       var opts = new LoadOptions { Calendar = new JapaneseEmperorCalendar() };
       var wb = new Workbook(file, opts);
       var cell = wb.Worksheets[sheetIdx].Cells[row, col];
       if (cell.Type != CellValueType.IsDateTime) return null;
       return cell.GetDateTime().ToString("yyyy-MM-dd");
   }
   ```

3. **Zaznamenejte původní řetězec éry** (`cell.StringValue`) vedle ISO výstupu pro auditní záznamy.  
4. **Jednotkové testy** metody s několika pevně zakódovanými Excel soubory pokrývajícími různé éry (Heisei, Reiwa) pro zajištění správnosti.

## Vizualizace

Níže je rychlý diagram ilustrující tok dat – od buňky v Excelu po ISO řetězec.  

![Příklad extrahování data z Excelu zobrazující Excel → LoadOptions → DateTime → ISO řetězec]  

*Alt text: “extrahování data z excelu” diagram zobrazující konverzní pipeline.*

## Závěr

Probrali jsme vše, co potřebujete k **extrahování data z Excelu**, zpracování japonských hodnot éry a **výstupu data yyyy‑mm‑dd**, aby odpovídalo **zobrazovanému datu v iso formátu**, který moderní API milují. Řešení je samostatné, funguje s libovolnou verzí .NET podporující Aspose.Cells a lze jej rozšířit na další kalendáře jedinou změnou řádku.

Máte na mysli jiný kalendář? Nebo možná získáváte data z více sloupců? Klidně upravte pomocnou funkci `ExtractIsoDate` nebo zanechte komentář níže. Šťastné programování a ať jsou vaše data vždy v dokonalé ISO synchronizaci!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}