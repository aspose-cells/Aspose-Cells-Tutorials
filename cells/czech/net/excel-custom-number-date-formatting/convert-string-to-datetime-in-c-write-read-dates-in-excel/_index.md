---
category: general
date: 2026-02-23
description: Převod řetězce na DateTime v C# a naučte se, jak zapisovat datum do Excelu,
  vynutit výpočet vzorců a číst datum z Excelu pomocí Aspose.Cells.
draft: false
keywords:
- convert string to datetime
- write date to excel
- read date from excel
- force formula calculation
- extract date from excel
language: cs
og_description: Rychle převést řetězec na DateTime v C#. Tento návod ukazuje, jak
  zapsat datum do Excelu, vynutit výpočet vzorce a extrahovat datum z Excelu pomocí
  Aspose.Cells.
og_title: Převod řetězce na DateTime v C# – Průvodce manipulací s daty v Excelu
tags:
- C#
- Excel automation
- Aspose.Cells
title: Převod řetězce na DateTime v C# – zápis a čtení dat v Excelu
url: /cs/net/excel-custom-number-date-formatting/convert-string-to-datetime-in-c-write-read-dates-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod řetězce na DateTime – Zápis a čtení dat v Excelu s C#

Už jste někdy potřebovali **convert string to DateTime** při práci se soubory Excel v C#? Možná jste dostali datum ve formátu `"R3/04/01"` z externího systému a nejste si jisti, jak jej převést na správný objekt `DateTime`. Dobrou zprávou je, že řešení je poměrně jednoduché – jen několik řádků kódu a malý trik „force formula calculation“.

V tomto tutoriálu si projdeme **how to write a date to Excel**, **force formula calculation**, aby Excel rozpoznal hodnotu, a poté **read the date back as a `DateTime`**. Na konci budete mít kompletní, spustitelný příklad, který můžete vložit do libovolného .NET projektu.

> **Co se naučíte**
> - Zapsat řetězec data do buňky (`write date to excel`)
> - Spustit výpočet (`force formula calculation`), aby Excel parsoval řetězec
> - Získat `DateTimeValue` buňky (`extract date from excel`)
> - Běžné úskalí a několik užitečných tipů

## Požadavky

- .NET 6.0 nebo novější (kód funguje také s .NET Framework)
- Aspose.Cells pro .NET (zdarma zkušební verze nebo licencovaná verze). Instalujte přes NuGet:

```bash
dotnet add package Aspose.Cells
```

- Základní znalost syntaxe C# – není potřeba nic složitého.

Teď se ponořme.

![příklad převodu řetězce na datetime](image.png){alt="převod řetězce na datetime v Excelu s C#"}

## Krok 1: Vytvoření nové instance Workbook (Kontext převodu řetězce na DateTime)

Prvním, co potřebujeme, je čerstvý objekt workbook, se kterým budeme pracovat. Představte si ho jako prázdný soubor Excel, který existuje jen v paměti, dokud se nerozhodnete jej uložit.

```csharp
using Aspose.Cells;
using System;

class ExcelDateDemo
{
    static void Main()
    {
        // Step 1 – initialize a workbook (in‑memory Excel file)
        Workbook workbook = new Workbook();
```

> **Proč je to důležité:**  
> Začít s čistým `Workbook` zajišťuje, že žádné skryté formátování nebo existující vzorce nebudou zasahovat do naší logiky převodu dat.

## Krok 2: Zapsat řetězec data do buňky A1 (`write date to excel`)

Dále vložíme surový řetězec `"R3/04/01"` do buňky **A1**. Řetězec má vlastní formát (R3 = rok 2023, měsíc 04, den 01). Excel jej dokáže interpretovat, jakmile ho přinutíme k výpočtu.

```csharp
        // Step 2 – put the raw date string into A1
        // The string "R3/04/01" means 2023‑04‑01 in our custom format
        workbook.Worksheets[0].Cells["A1"].PutValue("R3/04/01");
```

> **Pro tip:** Pokud máte mnoho dat, zvažte iteraci přes rozsah a použití `PutValue` uvnitř smyčky. Metoda automaticky detekuje datový typ, ale s naším vlastním formátem potřebujeme další krok.

## Krok 3: Vynutit výpočet vzorce (`force formula calculation`)

Excel automaticky neparsuje vlastní řetězce dat. Zavoláním `CalculateFormula()` přinutíme engine znovu vyhodnotit list, což spustí jeho interní logiku parsování dat. Tento krok je zásadní; bez něj by `DateTimeValue` vrátil `DateTime.MinValue`.

```csharp
        // Step 3 – force the workbook to evaluate formulas and parse dates
        workbook.CalculateFormula();
```

> **Proč vynucujeme výpočet:**  
> Volání `CalculateFormula` říká Aspose.Cells, aby prošel všechny buňky, jako by uživatel v Excelu stiskl **F9**. Tato konverze převádí text na skutečné sériové datum, které .NET dokáže pochopit.

## Krok 4: Získat hodnotu buňky jako objekt DateTime (`read date from excel` & `extract date from excel`)

Nyní můžeme bezpečně přečíst `DateTimeValue` buňky. Aspose.Cells jej vystavuje jako strukturu `DateTime`, již převedenou ze sériového čísla Excelu.

```csharp
        // Step 4 – read the parsed date back as a DateTime
        DateTime dateFromCell = workbook.Worksheets[0].Cells["A1"].DateTimeValue;

        // Display the result
        Console.WriteLine($"Parsed date: {dateFromCell:yyyy-MM-dd}");
    }
}
```

**Očekávaný výstup v konzoli**

```
Parsed date: 2023-04-01
```

Pokud spustíte program a uvidíte výše uvedený řádek, úspěšně jste **converted string to datetime**, zapsali datum do Excelu, vynutili výpočet vzorce a získali datum zpět.

## Kompletní funkční příklad (Všechny kroky dohromady)

Níže je kompletní program, který můžete zkopírovat a vložit do nového konzolového projektu. Žádné části nechybí a kód se kompiluje tak, jak je.

```csharp
using Aspose.Cells;
using System;

class ExcelDateDemo
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Write the raw date string to cell A1
        workbook.Worksheets[0].Cells["A1"].PutValue("R3/04/01");

        // 3️⃣ Force Excel to evaluate formulas (parses the date)
        workbook.CalculateFormula();

        // 4️⃣ Retrieve the parsed date as a DateTime object
        DateTime dateFromCell = workbook.Worksheets[0].Cells["A1"].DateTimeValue;

        // Verify the conversion
        Console.WriteLine($"Parsed date: {dateFromCell:yyyy-MM-dd}");
    }
}
```

### Rychlý kontrolní seznam

| ✅ | Úkol |
|---|------|
| ✅ | **Write date to excel** – `PutValue("R3/04/01")` |
| ✅ | **Force formula calculation** – `CalculateFormula()` |
| ✅ | **Read date from excel** – `DateTimeValue` |
| ✅ | **Extract date from excel** – convert to `yyyy‑MM‑dd` format |
| ✅ | Kompletní, spustitelný kód |

## Běžné okrajové případy a jak je řešit

| Situace | Na co si dát pozor | Navrhované řešení |
|-----------|-------------------|---------------|
| **Různé vlastní formáty** (např. `"R4/12/31"` pro 2024‑12‑31) | Excel nemusí automaticky rozpoznat předponu “R”. | Předzpracujte řetězec: nahraďte `R` za `20` před `PutValue`. |
| **Prázdné nebo null buňky** | `DateTimeValue` vrátí `DateTime.MinValue`. | Zkontrolujte vlastnost `IsDate` před čtením: `if (cell.IsDate) …` |
| **Velké datové sady** | Přepočítávání celého sešitu pokaždé může být pomalé. | Zavolejte `CalculateFormula()` jednou po hromadném zápisu všech dat. |
| **Nastavení specifická pro locale** | Některé locale očekávají pořadí den‑měsíc‑rok. | Nastavte `WorkbookSettings.CultureInfo` na `CultureInfo.InvariantCulture`, pokud je potřeba. |

## Profesionální tipy pro reálné projekty

1. **Batch processing** – Když máte tisíce řádků, nejprve zapište všechny řetězce a pak jednorázově zavolejte `CalculateFormula()`. Tím výrazně snížíte režii.
2. **Error handling** – Zabalte převod do try/catch a zaznamenejte buňky, kde je `IsDate` false. Pomůže vám to včas odhalit špatně formátované vstupy.
3. **Saving the workbook** – Pokud potřebujete uchovat kopii, jednoduše po kroku 4 přidejte `workbook.Save("output.xlsx");`.
4. **Performance** – Pro scénáře jen pro čtení zvažte použití `LoadOptions` s `LoadFormat.Xlsx`, aby se urychlilo načítání velkých souborů.

## Závěr

Nyní máte robustní, kompletní postup pro **convert string to datetime** při práci s Excelem v C#. **Zapsáním data do Excelu**, **vynucením výpočtu vzorce** a následným **čtením `DateTimeValue`** můžete spolehlivě převést jakýkoli podporovaný formát řetězce na .NET `DateTime`.  

Neváhejte experimentovat: změňte vstupní řetězec, vyzkoušejte různé locale nebo rozšiřte logiku na celý sloupec. Když zvládnete tyto základy, práce s daty v Excelu bude hračka.

**Další kroky** – prozkoumejte související témata jako **formátování buněk jako datum**, **používání vlastních číselných formátů** nebo **export sešitu zpět do streamu pro webová API**. Šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}