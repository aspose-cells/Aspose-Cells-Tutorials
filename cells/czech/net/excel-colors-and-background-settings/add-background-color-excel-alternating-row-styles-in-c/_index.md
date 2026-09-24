---
category: general
date: 2026-04-07
description: Přidejte barvu pozadí řádkům v Excelu pomocí C#. Naučte se, jak aplikovat
  střídavé barvy řádků, nastavit jednotné styly pozadí a importovat datovou tabulku
  do Excelu v jednom workflow.
draft: false
keywords:
- add background color excel
- apply alternating row colors
- style excel rows
- set solid background
- import datatable to excel
language: cs
og_description: Přidejte barvu pozadí řádkům v Excelu pomocí C#. Tento průvodce ukazuje,
  jak aplikovat střídavé barvy řádků, nastavit jednotné pozadí a efektivně importovat
  datovou tabulku do Excelu.
og_title: Přidat barvu pozadí v Excelu – Střídavé styly řádků v C#
tags:
- C#
- Excel
- DataTable
- Styling
title: Přidat barvu pozadí v Excelu – střídavé styly řádků v C#
url: /cs/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidání barvy pozadí v Excelu – střídavé styly řádků v C#

Už jste někdy potřebovali **add background color excel** řádky, ale nebyli jste si jisti, jak to udělat bez tisíce řádků komplikovaného kódu? Nejste v tom sami — většina vývojářů narazí na tuto překážku, když se poprvé snaží, aby jejich tabulky vypadaly víc než jen surový výpis dat.  

Dobrá zpráva? Za pár minut můžete **apply alternating row colors**, nastavit **solid background** a dokonce **import datatable to excel** pomocí čistého, znovupoužitelného vzoru v C#.  

V tomto tutoriálu projdeme celý proces, od načtení dat do `DataTable` až po stylování každého řádku pomocí světle žluto‑bílého pruhovaného vzoru. Nejsou potřeba žádné externí knihovny kromě solid Excel‑handling balíčku (např. **ClosedXML** nebo **GemBox.Spreadsheet**), a uvidíte, proč je tento přístup výkonný a snadno udržovatelný.

## Co se naučíte

- Jak načíst data a vložit je do listu Excel.
- Jak **style excel rows** pomocí střídavých barev pozadí.
- Mechanika **set solid background** pomocí objektu `Style`.
- Jak **import datatable to excel** při zachování stylů řádků.
- Tipy pro řešení okrajových případů, jako jsou prázdné tabulky nebo vlastní barevná schémata.

> **Pro tip:** Pokud už používáte objekt sešitu (`wb`) z knihovny, která podporuje vytváření stylů, můžete znovu použít stejné instance `Style` napříč více listy — šetříte paměť a udržujete kód přehledný.

---

## Krok 1: Načtení dat – Příprava DataTable

Než můžeme provést jakékoli stylování, potřebujeme zdroj řádků. Ve většině reálných scénářů pochází z databáze, API nebo CSV souboru. Pro ilustraci vytvoříme jednoduchý `DataTable` v paměti.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using GemBox.Spreadsheet;      // Or ClosedXML, whichever you prefer

// Simulated data fetch – replace with your own data access logic
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with sample rows
    for (int i = 1; i <= 10; i++)
        table.Rows.Add(i, $"Student {i}", Math.Round(new Random().NextDouble() * 100, 2));

    return table;
}
```

**Proč je to důležité:** Použití `DataTable` vám poskytuje tabulární, schématem‑vědomý kontejner, který Excel knihovna může importovat přímo, čímž se eliminuje potřeba psát smyčky po jednotlivých buňkách.

---

## Krok 2: Vytvoření stylů řádků – **Apply alternating row colors**

Nyní vytvoříme pole objektů `Style` — jeden pro každý řádek — aby každý řádek mohl mít vlastní pozadí. Vzor, který použijeme, je klasický světle žlutý pro sudé řádky a bílý pro liché řádky.

```csharp
// Assume 'wb' is an existing Workbook instance
Workbook wb = new Workbook();

// Retrieve data
DataTable dataTable = GetData();

// Allocate a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style instance
    rowStyles[i] = wb.CreateStyle();

    // Choose background colour based on row index
    rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;

    // Ensure the colour is actually applied
    rowStyles[i].Pattern = BackgroundType.Solid;   // <-- **set solid background**
}
```

**Vysvětlení:**  
- `wb.CreateStyle()` vám poskytne čistý objekt stylu, který můžete upravit, aniž byste ovlivnili ostatní.  
- Ternární operátor `(i % 2 == 0)` rozhoduje, zda je řádek sudý (světle žlutý) nebo lichý (bílý).  
- Nastavení `Pattern = BackgroundType.Solid` je klíčový krok, který **set solid background**; bez něj by barva byla ignorována.

---

## Krok 3: Získání cílového listu

Většina knihoven poskytuje kolekci listů. Budeme pracovat s prvním, ale můžete cílit na libovolný index nebo název, který preferujete.

```csharp
Worksheet worksheet = wb.Worksheets[0];   // First worksheet in the workbook
```

Pokud je sešit zcela nový, knihovna obvykle vytvoří výchozí list. Jinak můžete přidat list explicitně:

```csharp
// Alternative: create a new sheet named "Report"
Worksheet worksheet = wb.Worksheets.Add("Report");
```

---

## Krok 4: Import DataTable s řádkovými styly – **Import datatable to excel**

S připravenými styly je posledním krokem vložit `DataTable` do listu a aplikovat odpovídající styl na každý řádek.

```csharp
// Parameters: (DataTable, includeHeaders, startRow, startColumn, stylesArray)
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

**Co se děje pod kapotou?**  
- `true` říká metodě, aby zapsala názvy sloupců jako první řádek.  
- `0, 0` označuje levý horní roh (A1) jako vkládací bod.  
- `rowStyles` přiřadí každý `Style` odpovídajícímu datovému řádku, čímž získáme střídavé barvy, které jsme připravili dříve.

---

## Krok 5: Uložení sešitu

Poslední část skládačky je uložení sešitu do souboru, abyste jej mohli otevřít v Excelu a vidět výsledek.

```csharp
// Choose a format – XLSX is the modern default
wb.Save("StudentScores.xlsx");

// Optional: open automatically (Windows only)
System.Diagnostics.Process.Start("StudentScores.xlsx");
```

Otevřete soubor a měli byste vidět přehledně naformátovaný list:

- Řádek hlavičky tučně (výchozí styl knihovny).  
- Řádky 1, 3, 5… s čistým bílým pozadím.  
- Řádky 2, 4, 6… s jemným světle žlutým výplní, což usnadňuje čtení.

### Očekávaný výstup – náhled

| Id | Name      | Score |
|----|-----------|-------|
| 1  | Student 1 | 78.45 |
| 2  | Student 2 | 62.13 |
| 3  | Student 3 | 91.27 |
| …  | …         | …     |

Rows 2, 4, 6, … appear with a light‑yellow background—exactly the **apply alternating row colors** effect we aimed for.

![Add background color excel example](https://example.com/excel-background.png "Add background color excel example")

*(Alt text obsahuje primární klíčové slovo pro SEO.)*

---

## Řešení okrajových případů a variant

### Prázdný DataTable

Pokud je `dataTable.Rows.Count` nula, pole `rowStyles` bude prázdné a `ImportDataTable` stále zapíše řádek hlavičky (pokud je `includeHeaders` nastaveno na `true`). Výjimka není vyvolána, ale možná budete chtít zabránit vytvoření téměř prázdného souboru:

```csharp
if (dataTable.Rows.Count == 0)
{
    Console.WriteLine("No data to export – workbook will contain only headers.");
}
```

### Vlastní barevná schémata

Chcete místo žluté/bílé pruhy modro‑šedou? Stačí nahradit hodnoty `Color`:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightBlue : Color.LightGray;
```

Klidně načtěte barvy z konfiguračního souboru, aby ne‑vývojáři mohli ladit paletu bez úpravy kódu.

### Znovupoužití stylů napříč více listy

Pokud exportujete několik tabulek do stejného sešitu, můžete pole stylů vygenerovat jednou a znovu jej použít:

```csharp
Style[] sharedStyles = CreateAlternatingStyles(dataTable.Rows.Count);
worksheet1.Cells.ImportDataTable(dt1, true, 0, 0, sharedStyles);
worksheet2.Cells.ImportDataTable(dt2, true, 0, 0, sharedStyles);
```

Jen dejte pozor, aby obě tabulky měly stejný počet řádků, nebo vygenerujte nové pole pro každý list.

---

## Kompletní funkční příklad

Spojením všeho dohromady získáte samostatný program, který můžete zkopírovat a vložit do konzolové aplikace.

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;   // Install-Package GemBox.Spreadsheet

class Program
{
    static void Main()
    {
        // License free for small projects – remove for commercial use
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Initialise workbook
        Workbook wb = new Workbook();

        // 3️⃣ Create alternating row styles
        Style[] rowStyles = CreateAlternatingStyles(dataTable.Rows.Count);

        // 4️⃣ Get (or create) the target worksheet
        Worksheet ws = wb.Worksheets.Add("Report");

        // 5️⃣ Import data with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // 6️⃣ Save the file
        wb.Save("Report.xlsx");
        Console.WriteLine("Excel file created – check Report.xlsx");
    }

    // Helper: generate a DataTable with sample data
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        var rnd = new Random();
        for (int i = 1; i <= 12; i++)
            dt.Rows.Add(i, $"Student {i}", Math.Round(rnd.NextDouble() * 100, 2));

        return dt;
    }

    // Helper: create style array for alternating colors
    static Style[] CreateAlternatingStyles(int rowCount)
    {
        var wb = new Workbook();               // Temporary workbook for style creation
        var styles = new Style[rowCount];
        for (int i = 0; i < rowCount; i++)
        {
            styles[i] = wb.CreateStyle();
            styles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;
            styles[i].Pattern = BackgroundType.Solid;   // **set solid background**
        }
        return styles;
    }
}
```

Spusťte program, otevřete `Report.xlsx` a uvidíte střídavé pozadí přesně tak, jak je popsáno.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}