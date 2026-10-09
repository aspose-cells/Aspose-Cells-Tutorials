---
category: general
date: 2026-03-01
description: Návod na čtení a zápis Excelu v C# ukazuje, jak přečíst hodnotu buňky
  v Excelu a zapsat datum a čas do Excelu pomocí C# a Aspose.Cells v několika jednoduchých
  krocích.
draft: false
keywords:
- read write excel c#
- read excel cell value
- write datetime to excel
- c# excel interop
- aspnet excel automation
language: cs
og_description: Návod na čtení a zápis Excelu v C# vysvětluje, jak číst hodnotu buňky
  v Excelu a zapisovat datum a čas do Excelu s jasnými příklady kódu a osvědčenými
  postupy.
og_title: Čtení a zápis Excel v C# – krok za krokem
tags:
- C#
- Excel
- Aspose.Cells
title: Čtení a zápis Excelu v C# – Kompletní průvodce čtením a zápisem buněk v Excelu
url: /cs/net/cell-operations/read-write-excel-c-complete-guide-to-reading-and-writing-exc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Čtení a zápis Excel C# – Kompletní průvodce čtením a zápisem buněk v Excelu

Už jste někdy zkusili **read write Excel C#** a skončili s kryptickou výjimkou nebo nesprávným datem? Nejste v tom sami. Mnoho vývojářů narazí, když potřebují vytáhnout japonské datum éry z listu a poté uložit správný `DateTime` zpět do stejné buňky.  

V tomto průvodci si ukážeme, jak přesně **read excel cell value** a **write datetime to excel** pomocí C# a výkonné knihovny Aspose.Cells. Na konci budete mít samostatný, spustitelný příklad, který můžete vložit do libovolného .NET projektu.

## Co se naučíte

- Jak nainstalovat a odkazovat na Aspose.Cells v projektu .NET 6+.
- Přesný kód potřebný k získání buňky, která obsahuje řetězec japonské éry jako `"R3/5/12"`.
- Jak převést tento řetězec na `DateTime` pomocí kultury `"ja-JP"`.
- Kroky k vložení výsledného `DateTime` zpět do stejné buňky listu.
- Tipy pro zpracování okrajových případů, jako jsou prázdné buňky nebo neočekávané formáty éry.

Předchozí zkušenost s Excel interop není vyžadována – stačí základní znalost C# a .NET. Pojďme na to.

![Screenshot of read write Excel C# operation showing cell B2 before and after conversion](read-write-excel-csharp.png "read write excel c# example")

## Krok 1: Nastavení projektu – Základy čtení a zápisu Excel C#  

Než se ponoříme do kódu, potřebujeme pevný základ.

1. **Vytvořte novou konzolovou aplikaci** (nebo jakýkoli .NET projekt) cílící na .NET 6 nebo novější:

   ```bash
   dotnet new console -n ExcelEraDemo
   cd ExcelEraDemo
   ```

2. **Přidejte NuGet balíček Aspose.Cells**. Jedná se o plně spravovanou knihovnu, která funguje bez COM interopu:

   ```bash
   dotnet add package Aspose.Cells
   ```

3. **Zkopírujte soubor Excel** (`EraDates.xlsx`) do kořenového adresáře projektu. Tento sešit by měl obsahovat list pojmenovaný `"Sheet1"` s buňkou **B2**, která obsahuje hodnotu jako `"R3/5/12"` (Reiwa 3, květen 12).

To je vše, co potřebujete k nastavení. Zbytek tutoriálu se zaměřuje na samotnou logiku **read excel cell value** a **write datetime to excel**.

## Krok 2: Čtení hodnoty buňky Excel pomocí C#  

Nyní, když je projekt připraven, načteme řetězec z listu. Následující úryvek ukazuje přesný řetězec volání:

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Load the workbook (adjust the path as needed)
        Workbook wb = new Workbook("EraDates.xlsx");
        Worksheet ws = wb.Worksheets["Sheet1"];   // assumes the sheet is named Sheet1

        // Step 2: Get the cell that holds the Japanese era date string
        // B2 contains something like "R3/5/12"
        Cell dateCell = ws.Cells["B2"];  

        // Step 3: Read the string representation from the cell
        string eraDateString = dateCell.StringValue;  

        Console.WriteLine($"Original cell value: {eraDateString}");
        // -------------------------------------------------
        // From here we’ll convert the era string to a DateTime.
        // -------------------------------------------------
    }
}
```

**Proč to funguje:** `Cell.StringValue` vždy vrací zobrazený text, bez ohledu na podkladový číselný formát. To zaručuje, že pracujeme s přesným řetězcem "R3/5/12", který uživatel vidí.

### Časté úskalí

- **Prázdné buňky** – `StringValue` vrací prázdný řetězec. Ošetřete to před parsováním.  
- **Neočekávané formáty** – Pokud buňka obsahuje "2023/05/12", parser éry vyhodí výjimku; může být potřeba záložní řešení.

## Krok 3: Zápis DateTime do Excelu pomocí C#  

S řetězcem éry v ruce jej nyní parsujeme pomocí `DateTime.ParseExact`. Formát "ggyy/MM/dd" říká .NETu, aby očekával japonskou éru (`gg`), dvouciferný rok (`yy`) a komponenty měsíce/den.

```csharp
        // Step 4: Convert the era date string to a DateTime using the Japanese culture
        DateTime parsedDate;
        try
        {
            parsedDate = DateTime.ParseExact(
                eraDateString,
                "ggyy/MM/dd",
                new CultureInfo("ja-JP"));
        }
        catch (FormatException)
        {
            Console.WriteLine("The cell value does not match the expected Japanese era format.");
            return;
        }

        Console.WriteLine($"Parsed DateTime (UTC): {parsedDate:u}");

        // Step 5: Store the resulting DateTime back into the same cell
        dateCell.PutValue(parsedDate);

        // Optional: Apply a standard date format so Excel shows it nicely
        dateCell.SetStyle(new Style { Number = 14 }); // 14 = "m/d/yyyy"

        // Save the workbook to a new file so we don’t overwrite the original
        wb.Save("EraDates_Converted.xlsx");
        Console.WriteLine("Workbook saved as EraDates_Converted.xlsx");
```

**Proč používáme `PutValue`**: Aspose.Cells automaticky detekuje .NET typ a zapíše odpovídající typ buňky v Excelu. Předání `DateTime` vede k pravému Excel datu, které lze formátovat nebo použít ve vzorcích.

### Okrajové případy a tipy

- **Časová pásma** – objekty `DateTime` jsou uloženy bez informací o pásmu. Pokud potřebujete UTC, zavolejte `DateTime.SpecifyKind`.  
- **Záložní kultura** – pokud očekáváte jiné kultury, zabalte parsování do pomocné funkce, která zkouší více objektů `CultureInfo`.  
- **Výkon** – při zpracování tisíců řádků opakovaně používejte jedinou instanci `CultureInfo` místo vytváření nové v každé iteraci.

## Krok 4: Kompletní funkční příklad – Spojení všeho dohromady  

Níže je kompletní, připravený k spuštění program. Zkopírujte a vložte jej do `Program.cs`, ujistěte se, že `EraDates.xlsx` leží vedle zkompilovaného binárního souboru, a spusťte `dotnet run`.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Load workbook
        Workbook wb = new Workbook("EraDates.xlsx");
        Worksheet ws = wb.Worksheets["Sheet1"];   // Change if your sheet has a different name

        // -------------------------------------------------
        // 1️⃣ Read the Japanese era string from B2
        // -------------------------------------------------
        Cell dateCell = ws.Cells["B2"];
        string eraDateString = dateCell.StringValue?.Trim();

        if (string.IsNullOrEmpty(eraDateString))
        {
            Console.WriteLine("Cell B2 is empty. Nothing to convert.");
            return;
        }

        Console.WriteLine($"Original cell value: {eraDateString}");

        // -------------------------------------------------
        // 2️⃣ Parse the era string into a DateTime
        // -------------------------------------------------
        DateTime parsedDate;
        try
        {
            parsedDate = DateTime.ParseExact(
                eraDateString,
                "ggyy/MM/dd",
                new CultureInfo("ja-JP"));
        }
        catch (FormatException)
        {
            Console.WriteLine("The value does not match the expected Japanese era format (ggyy/MM/dd).");
            return;
        }

        Console.WriteLine($"Parsed DateTime: {parsedDate:u}");

        // -------------------------------------------------
        // 3️⃣ Write the DateTime back into the same cell
        // -------------------------------------------------
        dateCell.PutValue(parsedDate);

        // Apply a friendly date format (e.g., 2023/05/12)
        Style style = wb.CreateStyle();
        style.Number = 14; // Built‑in date format
        dateCell.SetStyle(style);

        // Save the updated workbook
        wb.Save("EraDates_Converted.xlsx");
        Console.WriteLine("Conversion complete – saved as EraDates_Converted.xlsx");
    }
}
```

**Očekávaný výstup**

```
Original cell value: R3/5/12
Parsed DateTime: 2021-05-12 00:00:00Z
Conversion complete – saved as EraDates_Converted.xlsx
```

Když otevřete `EraDates_Converted.xlsx`, buňka **B2** nyní zobrazuje běžné datum (např. `5/12/2021`) a může být použita v Excelových výpočtech stejně jako jakákoli jiná hodnota data.

## Profesionální tipy pro robustní kód čtení a zápisu Excel C#  

- **Ověřte před zápisem** – použijte `Cell.IsFormula` nebo `Cell.Type`, abyste nechtěně nepřepsali vzorce.  
- **Dávkové zpracování** – pokud potřebujete převést celý sloupec, projděte `ws.Cells.Columns[1]` (sloupec B) a aplikujte stejnou logiku.  
- **Bezpečnost vláken** – objekty Aspose.Cells nejsou thread‑safe; při paralelizaci vytvořte samostatné instance `Workbook` pro každé vlákno.  
- **Logování** – pro produkční skripty nahraďte `Console.WriteLine` vhodným loggerem (např. Serilog), aby zachytil selhání parsování.  
- **Testování** – napište jednotkové testy, které předají známé řetězce éry do pomocné metody a ověří výsledné hodnoty `DateTime`.

## Závěr  

Právě jste si osvojili **read write Excel C#** tím, že jste se naučili **read excel cell value**, parsovat japonský řetězec éry a **write datetime to excel** s jistotou. Kompletní příklad ukazuje čistý, end‑to‑end workflow, který můžete přizpůsobit hromadným operacím, různým kulturám nebo dokonce pipelineům Excel‑na‑databázi.  

Co dál? Zkuste rozšířit skript tak, aby zpracovával celý sloupec dat éry, nebo prozkoumejte bohaté možnosti formátování v Aspose.Cells pro stylizaci výstupních buněk. Můžete také experimentovat s dalšími knihovnami jako EPPlus nebo ClosedXML – většina logiky zůstává stejná, liší se jen volání API.  

Máte otázky nebo obtížnou Excel situaci? Zanechte komentář níže a šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}