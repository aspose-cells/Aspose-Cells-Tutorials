---
category: general
date: 2026-03-22
description: Jak exportovat Excel s formátováním a zachovat formát čísel. Naučte se
  převést oblast Excel, získat výsledek vzorce a exportovat Excel s formátováním pomocí
  Aspose.Cells.
draft: false
keywords:
- how to export excel
- preserve number format
- convert excel range
- get formula result
- export excel with formatting
language: cs
og_description: Jak exportovat Excel s formátováním a zachovat formát čísel. Krok
  za krokem průvodce převodem oblasti Excel, získáním výsledku vzorce a exportem Excelu
  s formátováním v C#.
og_title: Jak exportovat Excel s formátováním – zachovat formát čísel
tags:
- C#
- Aspose.Cells
- Excel automation
title: Jak exportovat Excel s formátováním – zachovat číselný formát
url: /cs/net/number-and-display-formats-in-excel/how-to-export-excel-with-formatting-preserve-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak exportovat Excel s formátováním – zachovat formát čísel

Už jste se někdy zamysleli nad tím, **jak exportovat Excel** data a přitom zachovat vzhled každé buňky přesně tak, jak jej vidíte v sešitu? Možná potřebujete poslat zprávu klientovi, naplnit grid control, nebo jen uložit hodnoty do databáze. Problémem je často ztráta formátování čísel nebo převod vzorců na surové řetězce.  

V tomto tutoriálu projdeme kompletním, připraveným příkladem v C#, který **zachovává formát čísel**, **převádí oblast Excelu** na `DataTable`, **získává výsledek vzorce** a nakonec **exportuje Excel s formátováním** pomocí Aspose.Cells. Na konci budete mít jedinou metodu, kterou můžete vložit do libovolného projektu a zavolat s odkazem na list.

> **Rychlý náhled:** kód vytvoří sešit, zapíše hodnotu a vzorec, řekne Aspose.Cells, aby exportoval buňky jako formátované řetězce, a vytiskne `123.456 | 246.912` – přesně to, co byste očekávali v Excelu.

---

## Co budete potřebovat

- **Aspose.Cells for .NET** (bezplatná zkušební verze stačí pro učení)
- .NET 6.0 nebo novější (API je stejné i na .NET Framework)
- Základní vývojové prostředí C# (Visual Studio, VS Code, Rider… podle vás)

Žádné další NuGet balíčky kromě Aspose.Cells nejsou potřeba. Pokud jste jej ještě nenainstalovali, spusťte:

```bash
dotnet add package Aspose.Cells
```

---

## Krok 1 – Vytvořte sešit a zapište hodnoty (včetně vzorce)

Nejprve vytvoříme nový sešit a vložíme číselnou hodnotu do **A1**. Pak přidáme jednoduchý vzorec v **B1**, který násobí první buňku dvěma. Tím připravíme podmínky pro ukázku **získání výsledku vzorce** později.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a numeric value and a formula that uses it
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Continue with export options...
        ExportRangeAsDataTable(worksheet);
    }
}
```

**Proč je to důležité:**  
- `PutValue` ukládá surové číslo, zatímco `PutFormula` ukládá výpočet.  
- Aspose.Cells udržuje vzorec **živý**, takže když později požádáme o hodnotu buňky, získáme skutečně `246.912`, ne řetězec `"=A1*2"`.

---

## Krok 2 – Řekněte Aspose.Cells, aby exportoval hodnoty jako formátované řetězce

Pokud jednoduše zavoláte `ExportDataTable` s výchozím nastavením, číselné buňky budou vráceny jako jejich základní hodnoty typu `double`. To odstraní všechny oddělovače tisíců, měnové symboly nebo vlastní desetinná místa, která jste nastavili. Třída `ExportTableOptions` nám umožňuje **zachovat formát čísel** a **exportovat jako řetězec**.

```csharp
static void ExportRangeAsDataTable(Worksheet worksheet)
{
    // Step 2: Set export options to retrieve values as formatted strings
    ExportTableOptions exportOptions = new ExportTableOptions
    {
        ExportAsString = true,          // Return values as strings
        ExportNumberFormat = true      // Preserve the cell's number format
    };

    // Step 3: Export the range A1:B1 to a DataTable
    DataTable dataTable = worksheet.Cells.ExportDataTable(
        firstRow: 0,
        firstColumn: 0,
        totalRows: 1,
        totalColumns: 2,
        includeColumnNames: true,
        options: exportOptions);

    PrintDataTable(dataTable);
}
```

**Klíčový bod:** `ExportNumberFormat = true` je příznak, který umožňuje fungování **zachování formátu čísel**. Bez něj uvidíte `"123.456"` a `"246.912"` jako surová čísla, což může v kódu vypadat v pořádku, ale ne při vložení dat do UI, která očekává stejné formátování jako Excel.

---

## Krok 3 – Vytiskněte exportovaná data (verifikace)

Nyní, když máme `DataTable` plný formátovaných řetězců, vypišme obsah do konzole. To také ukazuje, že úspěšně **získáváme výsledek vzorce** bez nutnosti sami vzorec vyhodnocovat.

```csharp
static void PrintDataTable(DataTable table)
{
    // Step 4: Print the exported values (already formatted)
    foreach (DataRow row in table.Rows)
    {
        // The output will look like: 123.456 | 246.912
        Console.WriteLine($"{row[0]} | {row[1]}");
    }
}
```

Running the program prints:

```
123.456 | 246.912
```

Všimněte si, že druhý sloupec zobrazuje **výsledek vzorce**, nikoli text vzorce. To je přesně to, co potřebujete při **exportu Excelu s formátováním** pro další zpracování.

---

## Krok 4 – Převod větších oblastí Excelu (volitelné)

Příklad výše pracuje s malým úsekem `A1:B1`, ale ve skutečných scénářích často potřebujete exportovat celé tabulky. Stejná metoda funguje pro jakýkoli obdélníkový blok – stačí upravit argumenty `firstRow`, `firstColumn`, `totalRows` a `totalColumns`.

```csharp
// Example: Export a 10‑row by 5‑column block starting at C3
DataTable bigTable = worksheet.Cells.ExportDataTable(
    firstRow: 2,          // Zero‑based index (C3 = row 2, column 2)
    firstColumn: 2,
    totalRows: 10,
    totalColumns: 5,
    includeColumnNames: true,
    options: exportOptions);
```

**Tip:** Pokud má váš list již řádek s hlavičkou, nastavte `includeColumnNames` na `true`. Aspose.Cells použije první řádek oblasti jako názvy sloupců, což je užitečné, když později svázete `DataTable` s UI gridem.

---

## Krok 5 – Časté úskalí a jak se jim vyhnout

| Problém | Proč se to děje | Řešení |
|-------|----------------|-----|
| **Čísla ztrácejí čárky nebo měnové symboly** | `ExportAsString` je `false` nebo `ExportNumberFormat` chybí | Nastavte oba `ExportAsString = true` **a** `ExportNumberFormat = true`. |
| **Buňky s vzorcem vrací text vzorce** | Nezavolali jste `CalculateFormula` před exportem (potřebné jen pokud sešit není nastaven na automatické výpočty) | Buď povolte automatické výpočty (`workbook.CalculateFormula()`) nebo se spolehněte na `ExportAsString`, který vynutí vyhodnocení. |
| **Hlavičky se zobrazují jako datové řádky** | `includeColumnNames` je nastaveno na `false`, přičemž oblast obsahuje řádek s hlavičkou | Nastavte `includeColumnNames = true`, aby se první řádek považoval za názvy sloupců. |
| **Velké oblasti způsobují tlak na paměť** | Export celého listu najednou načte vše do paměti | Exportujte po částech (např. 500 řádků najednou) a v případě potřeby sloučte `DataTable`. |

---

## Krok 6 – Kompletní funkční příklad (připravený ke kopírování a vložení)

Níže je celý program, od `using` direktiv po `Main`. Vložte jej do konzolové aplikace a stiskněte **F5** – okamžitě uvidíte formátovaný výstup.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate cells
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Export options: keep formatting and return strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            ExportNumberFormat = true
        };

        // Export A1:B1 as a DataTable
        DataTable dataTable = worksheet.Cells.ExportDataTable(
            firstRow: 0,
            firstColumn: 0,
            totalRows: 1,
            totalColumns: 2,
            includeColumnNames: true,
            options: exportOptions);

        // Print results
        foreach (DataRow row in dataTable.Rows)
        {
            Console.WriteLine($"{row[0]} | {row[1]}"); // Expected: "123.456 | 246.912"
        }

        // Keep console window open
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**Očekávaný výstup**

```
123.456 | 246.912

Press any key to exit...
```

Toto je celý **postup, jak exportovat Excel**, s zachovaným formátováním, vyhodnocenými výsledky vzorců a čistým `DataTable` připraveným pro libovolného .NET spotřebitele.

---

## Závěr

Probrali jsme vše, co potřebujete vědět o **exportu Excel** dat při **zachování formátu čísel**, **převodu oblasti Excelu** na `DataTable` a **získávání výsledků vzorců** bez dalšího parsování. Klíčová je konfigurace `ExportTableOptions` – jakmile nastavíte `ExportAsString` a `ExportNumberFormat` na `true`, Aspose.Cells udělá těžkou práci za vás.

Odtud můžete:

- Připojit `DataTable` k WPF `DataGrid` nebo ASP.NET MVC pohledu.
- Zapsat tabulku do CSV souboru a zachovat přesnou vizuální reprezentaci.
- Rozšířit přístup na více listů nebo dynamické oblasti.

Neváhejte experimentovat s různými formáty (měna, procenta) a většími bloky dat. Pokud narazíte na nějaké potíže, vraťte se k tabulce **častých úskalí** – pokrývá nejčastější problémy při **exportu Excelu s formátováním**.

Šťastné programování a ať jsou vaše exportované tabulky vždy tak upravené jako originály!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}