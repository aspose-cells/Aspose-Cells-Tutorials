---
category: general
date: 2026-02-14
description: Analyzujte japonské era data v Excelu pomocí vlastního parsování data.
  Naučte se, jak načíst sešit ze souboru pomocí funkce load excel s volbami a vyhnout
  se běžným úskalím.
draft: false
keywords:
- parse japanese era dates
- load excel with options
- load workbook from file
- custom date parsing excel
language: cs
og_description: Zpracovávejte japonské datumy podle éry v Excelu pomocí Aspose.Cells.
  Tento průvodce ukazuje, jak načíst sešit ze souboru s vlastními možnostmi parsování
  dat.
og_title: Rozparsování japonských dat podle éry – krok za krokem C# tutoriál
tags:
- Aspose.Cells
- C#
- Excel automation
title: Zpracování japonských dat era v Excelu – Kompletní průvodce pro vývojáře C#
url: /cs/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Parsování japonských era datumů – kompletní C# tutoriál

Už jste někdy potřebovali **parsovat japonské era datumy** z Excelového listu a přemýšleli, proč se hodnoty mění na podivná čísla? Nejste v tom sami. Mnoho vývojářů narazí na tento problém, když výchozí parser `DateTime` nepozná formát „Reiwa 1/04/01“ používaný v japonských kalendářích.  

Dobrá zpráva: můžete Aspose.Cells říct, aby tyto buňky zacházel jako s japonskými era daty už od okamžiku, kdy **načtete Excel s možnostmi**. V tomto průvodci vás provedeme načítáním sešitu ze souboru, nastavením vlastního parsování dat a ověřením, že data budou přesně tak, jak očekáváte.

Na konci tohoto tutoriálu budete schopni:

* Načíst sešit ze souboru při specifikaci `DateTimeParsing.JapaneseEra`.
* Přistupovat k hodnotám buněk jako k platným objektům `DateTime`.
* Řešit okrajové případy, jako jsou prázdné buňky nebo smíšené kalendáře.
* Rozšířit přístup na jakýkoli scénář **custom date parsing excel**, se kterým se můžete setkat.

> **Požadavek** – Potřebujete knihovnu Aspose.Cells pro .NET (v23.9 nebo novější) a .NET‑kompatibilní IDE (Visual Studio, Rider atd.). Žádné další balíčky nejsou potřeba.

---

## Krok 1: Nastavení Textových Načítacích Možností pro Parsování Japonské Éry  

První věc, kterou uděláme, je říct načítači, jak má interpretovat text, který vypadá jako datum japonské éry. To se provádí pomocí `TxtLoadOptions` a výčtu `DateTimeParsing`.

```csharp
using Aspose.Cells;

// Step 1: Set up load options to understand Japanese era dates
TxtLoadOptions loadOptions = new TxtLoadOptions
{
    // This flag makes the parser treat “R1/04/01” as 2024‑04‑01, etc.
    DateTimeParsing = DateTimeParsing.JapaneseEra
};
```

**Proč je to důležité:** Bez příznaku `JapaneseEra` Aspose.Cells zachází s buňkou jako s obyčejným řetězcem, což vás nutí ručně rozdělit název éry a převést ho. Příznak provádí těžkou práci, udržuje váš kód čistý a méně náchylný k chybám.

---

## Krok 2: Načtení sešitu ze souboru pomocí možností  

Nyní skutečně otevřeme Excel soubor. Všimněte si, jak je objekt `loadOptions` předán konstruktoru `Workbook` — to je krok **load workbook from file**, který respektuje naše vlastní pravidla parsování.

```csharp
// Step 2: Load the workbook with the configured options
string filePath = Path.Combine(Environment.CurrentDirectory, "japan_dates.xlsx");
Workbook workbook = new Workbook(filePath, loadOptions);
```

Pokud se soubor nachází jinde (např. na síťovém disku), stačí upravit `filePath` podle potřeby. Důležité je, aby byla použita stejná instance `loadOptions`; jinak konverze japonské éry neproběhne.

---

## Krok 3: Přístup k parsovaným datumům  

Po načtení sešitu můžete získat hodnoty buněk přesně tak, jako u jakéhokoli běžného data. API automaticky vrací objekt `DateTime`.

```csharp
// Step 3 (optional): Read a date from the first worksheet, cell A1
Worksheet sheet = workbook.Worksheets[0];
Cell dateCell = sheet.Cells["A1"];

// The Value property is already a DateTime because of our parsing option
DateTime parsedDate = dateCell.DateTimeValue;

// Quick sanity check – print to console
Console.WriteLine($"Parsed date from A1: {parsedDate:yyyy-MM-dd}");
```

**Očekávaný výstup** (předpokládáme, že A1 obsahuje „R1/04/01“):

```
Parsed date from A1: 2024-04-01
```

Pokud buňka obsahuje gregoriánské datum, např. „2023‑12‑31“, parser stále funguje — jen vrátí původní datum beze změny.

---

## Krok 4: Ověření všech datumů ve sloupci  

Často potřebujete prohledat celý sloupec japonských era datumů. Níže je kompaktní smyčka, která ukazuje, jak elegantně zacházet s prázdnými buňkami a smíšeným obsahem.

```csharp
// Step 4: Iterate through column B (index 1) and print each parsed date
int firstRow = 0;
int lastRow = sheet.Cells.MaxDataRow; // last row with data

for (int row = firstRow; row <= lastRow; row++)
{
    Cell cell = sheet.Cells[row, 1]; // column B
    if (cell.Type == CellValueType.IsDateTime)
    {
        Console.WriteLine($"Row {row + 1}: {cell.DateTimeValue:yyyy-MM-dd}");
    }
    else if (!cell.IsNull)
    {
        // Fallback: show raw string for non‑date cells
        Console.WriteLine($"Row {row + 1}: (non‑date) {cell.StringValue}");
    }
}
```

**Tip:** `CellValueType.IsDateTime` je nejbezpečnější způsob, jak zkontrolovat, zda parser uspěl. Chrání vás před `InvalidCastException`, když buňka obsahuje neočekávaný text.

---

## Krok 5: Časté úskalí a jak je řešit  

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Prázdné buňky vrací `DateTime.MinValue`** | Parser zachází s prázdnými řetězci jako s minimálním datem. | Zkontrolujte `cell.IsNull` před přístupem k `DateTimeValue`. |
| **Smíšené kalendáře (japonský + gregoriánský) ve stejném sloupci** | Parser zvládá oba, ale můžete potřebovat je rozlišit pro reportování. | Použijte `cell.StringValue` k prozkoumání původního textu, když je `cell.Type` `IsString`. |
| **Nesprávná éra (např. „H30“ pro Heisei) po roce 2019** | Heisei skončil v roce 2019; pozdější data by měla používat „R“. | Ověřte předponu éry před tím, než budete důvěřovat parsovanému výsledku. |
| **Snížení výkonu u velkých souborů** | Načítání s vlastními možnostmi přidává malé zatížení. | Načtěte jen požadované listy (`Workbook.LoadOptions.LoadAllWorksheets = false`). |

---

## Krok 6: Kompletní funkční příklad  

Spojením všeho dohromady zde máte samostatnou konzolovou aplikaci, kterou můžete zkopírovat a spustit. Ukazuje **custom date parsing excel** od začátku až do konce.

```csharp
// FullExample.cs
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure load options for Japanese era dates
        TxtLoadOptions loadOptions = new TxtLoadOptions
        {
            DateTimeParsing = DateTimeParsing.JapaneseEra
        };

        // 2️⃣ Load the workbook from file with those options
        string filePath = Path.Combine(Environment.CurrentDirectory, "japan_dates.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        Workbook workbook = new Workbook(filePath, loadOptions);
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Read a single cell (A1) – demonstrates automatic parsing
        Cell a1 = sheet.Cells["A1"];
        Console.WriteLine($"A1 raw value: {a1.StringValue}");
        Console.WriteLine($"A1 parsed date: {a1.DateTimeValue:yyyy-MM-dd}");

        // 4️⃣ Loop through column B to show batch parsing
        Console.WriteLine("\n--- Column B Dates ---");
        int lastRow = sheet.Cells.MaxDataRow;
        for (int row = 0; row <= lastRow; row++)
        {
            Cell cell = sheet.Cells[row, 1]; // B column
            if (cell.Type == CellValueType.IsDateTime)
                Console.WriteLine($"Row {row + 1}: {cell.DateTimeValue:yyyy-MM-dd}");
            else if (!cell.IsNull)
                Console.WriteLine($"Row {row + 1}: (non‑date) {cell.StringValue}");
        }

        // 5️⃣ Optional: Save a copy with dates converted to ISO format
        // This shows that the workbook now holds proper DateTime objects.
        workbook.Save("japan_dates_converted.xlsx");
        Console.WriteLine("\nWorkbook saved as japan_dates_converted.xlsx");
    }
}
```

**Co byste měli vidět** když `japan_dates.xlsx` obsahuje:

| A | B |
|---|---|
| R1/04/01 | 2023‑12‑31 |
| H30/12/31 | R2/01/01 |
| (blank) | R2/02/15 |

Console output:

```
A1 raw value: R1/04/01
A1 parsed date: 2024-04-01

--- Column B Dates ---
Row 1: 2023-12-31
Row 2: 2025-01-01
Row 3: (non-date) 
Row 4: 2025-02-15
Workbook saved as japan_dates_converted.xlsx
```

Uložený soubor nyní obsahuje správné datumové buňky, které můžete otevřít v Excelu a vidět běžné formátování data.

---

## Závěr  

Právě jsme ukázali, jak **parsovat japonské era datumy** v Excelu nastavením `TxtLoadOptions`, **load workbook from file** s těmito možnostmi a pracovat s výslednými hodnotami `DateTime`. Stejný vzor — nastavení vlastních příznaků parsování a následné načtení sešitu — platí pro jakýkoli požadavek **custom date parsing excel**, ať už jde o fiskální období, ISO čísla týdnů nebo proprietární formáty.

Máte jinou éru nebo smíšený kalendář v tabulce? Stačí vyměnit `DateTimeParsing.JapaneseEra` za jinou hodnotu výčtu (např. `DateTimeParsing.Custom`) a poskytnout řetězec formátu. Flexibilita Aspose.Cells znamená, že téměř nikdy nebudete muset psát ruční konverzní kód.

**Další kroky**, které můžete prozkoumat:

* **Načíst Excel s možnostmi** pro CSV soubory (`CsvLoadOptions`) pro zpracování lokálně specifických oddělovačů.
* Použijte `Workbook.Save` s `SaveFormat.Xlsx` k exportu vyčištěných dat.
* Kombinujte tento přístup s **Aspose.Slides** nebo **Aspose.Words** pro reportingové pipeline.

Vyzkoušejte to, upravte možnosti a nechte knihovnu udělat těžkou práci. Šťastné programování!  

![Snímek obrazovky parsovaných japonských era datumů v konzolovém okně – příklad parsování japonských era datumů](/images/parse-japanese-era-dates.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}