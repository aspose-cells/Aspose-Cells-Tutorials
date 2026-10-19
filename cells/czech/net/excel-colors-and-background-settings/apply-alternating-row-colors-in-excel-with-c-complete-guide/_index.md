---
category: general
date: 2026-07-03
description: Použijte střídavé barvy řádků při importu datové tabulky do Excelu pomocí
  C#. Naučte se, jak exportovat datovou tabulku C# do Excelu, uložit stylovanou tabulku
  v Excelu a zachovat formátování sešitu.
draft: false
keywords:
- apply alternating row colors
- import datatable to excel
- export c# datatable to excel
- save styled table excel
- save workbook with formatting
language: cs
og_description: Použijte střídavé barvy řádků v Excelu pomocí C#. Tento tutoriál ukazuje,
  jak importovat datovou tabulku do Excelu, exportovat datovou tabulku C# do Excelu
  a uložit sešit s formátováním.
og_title: Použijte střídavé barvy řádků v Excelu s C# – Kompletní průvodce
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  headline: Apply Alternating Row Colors in Excel with C# – Complete Guide
  type: TechArticle
- description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  name: Apply Alternating Row Colors in Excel with C# – Complete Guide
  steps:
  - name: Expected Output
    text: '| ID | Name | Department | HireDate | |----|---------|------------|------------|
      | 1 | Alice | Finance | 15‑01‑2020 | | 2 | Bob | HR | 23‑06‑2019 | | 3 | Charlie
      | IT | 10‑03‑2021 | | 4 | Diana | Marketing | 05‑11‑2018 |'
  - name: What if my DataTable has thousands of rows?
    text: The `ImportDataTable` method streams data efficiently, but you might hit
      memory limits on very large tables. In such cases, consider splitting the export
      into multiple worksheets or using the `ImportDataTable` overload that lets you
      specify a start row and column.
  - name: Can I use custom colors instead of the built‑in ones?
    text: Absolutely. Just replace the `ForegroundColor` assignments in `styleWhite`
      and `styleGray` with any `System.Drawing.Color` you prefer—think pastel blues
      or corporate brand colors.
  - name: How do I ensure the alternating style works when the user adds rows later?
    text: If users edit the file manually, the original style array won’t automatically
      extend. A quick workaround is to convert the range into an Excel Table (`ListObject`)
      after import; Excel then repeats the pattern for new rows.
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataExport
title: Aplikujte střídavé barvy řádků v Excelu pomocí C# – Kompletní průvodce
url: /cs/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Použít střídavé barvy řádků v Excelu s C# – Kompletní průvodce

Už jste někdy potřebovali **aplikovat střídavé barvy řádků** při exportu C# `DataTable` do Excelu? Nejste jediní – vývojáři se neustále ptají, jak udělat tyto tabulky vypadat profesionálně, aniž by po exportu ručně upravovali Excel. Dobrá zpráva? Můžete to provést programově během několika řádků kódu.

V tomto tutoriálu projdeme **import datatable to excel**, ukážeme vám, jak **export c# datatable to excel** s formátovanou tabulkou, a nakonec **save styled table excel** při zachování formátování. Na konci budete schopni **save workbook with formatting**, která vypadá připravená na schůzku s klientem.

## Požadavky

- .NET 6.0 nebo novější (ukázka používá .NET 6, ale funguje jakákoli recentní verze)
- Aspose.Cells pro .NET (bezplatná zkušební verze nebo licencovaná) – tato knihovna usnadňuje stylování
- Zdroj `DataTable` (může pocházet z databáze, CSV nebo kolekce v paměti)

> **Tip:** Pokud ještě nemáte Aspose.Cells, můžete jej získat z NuGet pomocí `dotnet add package Aspose.Cells`.

## Krok 1: Nastavte projekt a načtěte svá data

Nejprve vytvořte konzolovou aplikaci (nebo jakýkoli C# projekt) a přidejte potřebné `using` direktivy. Pak načtěte data do `DataTable`. Pro ilustraci vygenerujeme jednoduchou tabulku za běhu.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Retrieve the source data as a DataTable
        DataTable sourceTable = GetSampleData();

        // The rest of the steps follow...
    }

    // Helper that creates a dummy DataTable
    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

**Proč je to důležité:** Mít připravený `DataTable` znamená, že můžete **import datatable to excel** jedním voláním, čímž se eliminuje potřeba ručního vkládání buněk po jedné.

## Krok 2: Vytvořte sešit a definujte střídavé styly řádků

Nyní vytvoříme novou instanci `Workbook`. Trik pro **apply alternating row colors** spočívá v `ImportTableOptions.StyleArray`. Použijeme první dva vestavěné styly (obvykle bílý a světle šedý), ale později je můžete přizpůsobit.

```csharp
// Step 2: Create a new workbook
Workbook workbook = new Workbook();

// Define two simple styles: white (default) and light gray
Style styleWhite = workbook.Styles[workbook.Styles.Add()];
styleWhite.ForegroundColor = System.Drawing.Color.White;
styleWhite.Pattern = BackgroundType.Solid;

Style styleGray = workbook.Styles[workbook.Styles.Add()];
styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242); // light gray
styleGray.Pattern = BackgroundType.Solid;

// Step 3: Set up ImportTableOptions with the alternating styles
ImportTableOptions importOptions = new ImportTableOptions
{
    // The array alternates between the two styles for each row
    StyleArray = new Style[] { styleWhite, styleGray }
};
```

**Vysvětlení:** `ImportTableOptions` říká Aspose.Cells, jak má během importu zacházet s každým řádkem. Poskytnutím `StyleArray` se dvěma položkami knihovna automaticky obarví každý lichý řádek prvním stylem a každý sudý řádek druhým – přesně to, co potřebujete pro **apply alternating row colors**.

## Krok 3: Načtěte DataTable do listu (včetně hlaviček)

S připraveným sešitem a styly nyní **import datatable to excel**. Metoda `ImportDataTable` udělá těžkou práci: zapíše názvy sloupců, respektuje pole stylů a umístí data počínaje buňkou A1.

```csharp
// Step 4: Import the DataTable into the first worksheet (include column headers)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells.ImportDataTable(sourceTable, true, importOptions);
```

**Proč zahrnujeme `true` jako druhý argument:** Říká metodě, aby zapsala názvy sloupců jako první řádek, což je nezbytné pro profesionálně vypadající report.

## Krok 4: Doladění tabulky (volitelné, ale užitečné)

Pokud chcete, aby se sloupce automaticky přizpůsobily nebo přidat řádek filtru, pár dalších řádků to vylepší.

```csharp
// Auto‑fit all columns for readability
sheet.AutoFitColumns();

// Add a filter to the header row
sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";
```

Tyto úpravy neovlivňují střídavé barvy, ale zlepšují celkový uživatelský zážitek souboru **save styled table excel**.

## Krok 5: Uložte sešit a zachovejte veškeré formátování

Nakonec zapíšeme soubor na disk. Metoda `Save` zachová každý nastavený styl, čímž zajistí, že střídavé řádky zůstanou nedotčeny.

```csharp
// Step 5: Save the workbook with the styled table
string outputPath = @"C:\Temp\StyledEmployees.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Když otevřete `StyledEmployees.xlsx`, uvidíte čistou tabulku, kde řádky střídavě mají bílou a světle šedou barvu – přesně takový vizuální prvek, na který se mnoho uživatelů spoléhá pro čitelnost.

### Očekávaný výstup

| ID | Name    | Department | HireDate   |
|----|---------|------------|------------|
| 1  | Alice   | Finance    | 15‑01‑2020 |
| 2  | Bob     | HR         | 23‑06‑2019 |
| 3  | Charlie | IT         | 10‑03‑2021 |
| 4  | Diana   | Marketing  | 05‑11‑2018 |

- Řádek 1, 3 … → bílý podklad  
- Řádek 2, 4 … → světle šedý podklad  

To je celý proces **save workbook with formatting**.

## Časté otázky a okrajové případy

### Co když má můj DataTable tisíce řádků?

`ImportDataTable` metoda streamuje data efektivně, ale u velmi velkých tabulek můžete narazit na limity paměti. V takových případech zvažte rozdělení exportu do více listů nebo použití přetížení `ImportDataTable`, které umožňuje zadat počáteční řádek a sloupec.

### Mohu použít vlastní barvy místo vestavěných?

Určitě. Stačí nahradit přiřazení `ForegroundColor` v `styleWhite` a `styleGray` libovolnou `System.Drawing.Color`, kterou preferujete – například pastelové modré nebo firemní barvy.

```csharp
styleWhite.ForegroundColor = System.Drawing.Color.LightBlue;
styleGray.ForegroundColor = System.Drawing.Color.LightCyan;
```

### Jak zajistit, aby střídavý styl fungoval, když uživatel později přidá řádky?

Pokud uživatelé soubor upravují ručně, původní pole stylů se automaticky neprodlouží. Rychlé řešení je po importu převést oblast na Excelovou tabulku (`ListObject`); Excel pak opakuje vzor pro nové řádky.

```csharp
int lastRow = sheet.Cells.MaxDataRow;
int lastCol = sheet.Cells.MaxDataColumn;
string tableRange = $"A1:{CellsHelper.ColumnIndexToName(lastCol)}{lastRow + 1}";
ListObject table = sheet.ListObjects[sheet.ListObjects.Add(tableRange, true)];
```

Nyní každý nový řádek zdědí střídavé barvy.

## Kompletní funkční příklad (všechny kroky na jednom místě)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve source data
        DataTable sourceTable = GetSampleData();

        // 2️⃣ Create workbook and define alternating styles
        Workbook workbook = new Workbook();

        Style styleWhite = workbook.Styles[workbook.Styles.Add()];
        styleWhite.ForegroundColor = System.Drawing.Color.White;
        styleWhite.Pattern = BackgroundType.Solid;

        Style styleGray = workbook.Styles[workbook.Styles.Add()];
        styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242);
        styleGray.Pattern = BackgroundType.Solid;

        ImportTableOptions importOptions = new ImportTableOptions
        {
            StyleArray = new Style[] { styleWhite, styleGray }
        };

        // 3️⃣ Import DataTable (including headers)
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(sourceTable, true, importOptions);

        // 4️⃣ Optional polish
        sheet.AutoFitColumns();
        sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";

        // 5️⃣ Save the styled workbook
        string outputPath = @"C:\Temp\StyledEmployees.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

Spusťte program, otevřete vygenerovaný soubor a okamžitě uvidíte aplikované střídavé barvy – žádné ruční formátování není potřeba.

## Závěr

Právě jsme ukázali, jak **apply alternating row colors**, když **import datatable to excel** pomocí C#. Proces zahrnuje vše, co potřebujete k **export c# datatable to excel**, **save styled table excel** a **save workbook with formatting**, která vypadá profesionálně hned po vytvoření.

Další kroky? Zkuste vyměnit dva styly za vlastní motiv, nebo převést oblast na Excelovou tabulku, aby uživatelé mohli řadit a filtrovat a zároveň zachovat barevný vzor. Můžete také prozkoumat podmíněné formátování pomocí `ConditionalFormattingCollection` pro dynamičtější vizuální nápovědy.

Got a twist

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vlastních projektech.

- [Jak importovat DataTable do Excelu pomocí Aspose.Cells pro .NET (průvodce krok za krokem)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Použití barev a pozadí v Excelu pomocí Aspose.Cells pro .NET](/cells/english/net/formatting/colors-and-background/)
- [Automatizace tématických barev v Excelu pomocí Aspose.Cells .NET pro efektivní formátování](/cells/english/net/formatting/automate-excel-theme-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}