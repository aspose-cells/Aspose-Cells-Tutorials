---
category: general
date: 2026-03-01
description: Importujte data s formátováním do Excelu pomocí C#. Naučte se, jak importovat
  DataTable do Excelu a přidat buňkám barvu pozadí během několika kroků.
draft: false
keywords:
- import data with formatting
- how to import datatable into excel
- add background color to excel cells
language: cs
og_description: Importujte data s formátováním do Excelu pomocí C#. Podrobný návod,
  který ukazuje, jak importovat DataTable a přidat buňkám barvu pozadí.
og_title: Import dat s formátováním do Excelu – průvodce C#
tags:
- C#
- Excel
- DataTable
- Formatting
title: Import dat s formátováním do Excelu pomocí C#
url: /cs/net/excel-data-import-export/import-data-with-formatting-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Importovat data s formátováním do Excelu pomocí C#

Už jste někdy potřebovali **importovat data s formátováním** do sešitu Excel, ale stále jste dostávali obyčejný, nudný list? Nejste v tom sami. Většina vývojářů narazí na tento problém, když zjistí, že výchozí import odstraní všechny barvy a styly, které jste tak pečlivě nastavili ve svých zdrojových datech.

V tomto tutoriálu projdeme kompletním, připraveným k okamžitému spuštění řešením, které **importuje DataTable do Excelu** a **přidá barvu pozadí buňkám v Excelu** současně. Žádné další zpracování po importu není potřeba — váš sešit bude vypadat přesně tak, jak chcete, hned po vytvoření.

## Co se naučíte

- Jak načíst data do `DataTable`.
- Jak definovat pole objektů `Style`, které nesou barvy pozadí.
- Jak zavolat `ImportDataTable` s těmito styly, aby import zachoval formátování.
- Kompletní, spustitelný příklad, který můžete vložit do konzolové aplikace a okamžitě vidět výsledek.
- Tipy, úskalí a varianty pro reálné projekty.

### Požadavky

- .NET 6.0 nebo novější (kód funguje také s .NET Framework 4.6+).
- Knihovna **GemBox.Spreadsheet** (bezplatná verze stačí pro ukázku).
- Základní znalost C# a konceptů Excelu.

Pokud se ptáte *proč GemBox?*, je to proto, že nabízí jednorázovou metodu `ImportDataTable`, která přijímá pole stylů — právě to, co potřebujeme k **importu dat s formátováním** bez psaní smyčky.

---

## Krok 1: Nastavení projektu a přidání GemBox.Spreadsheet

Pro zahájení vytvořte novou konzolovou aplikaci:

```bash
dotnet new console -n ExcelImportDemo
cd ExcelImportDemo
dotnet add package GemBox.Spreadsheet
```

> **Tip:** Bezplatná verze omezuje listy na 150 000 buněk, což je pro ukázky dostatek. Pokud limit překročíte, upgradujte nebo přejděte na EPPlus, ale API bude vypadat mírně odlišně.

## Krok 2: Načtení zdrojových dat jako `DataTable`

První, co potřebujeme, je `DataTable`, který napodobuje data, jež byste normálně načetli z databáze. Zde je malý pomocník, který vytvoří takovou tabulku v paměti:

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register the free license (remove for paid version).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve the source data as a DataTable.
        DataTable dataTable = GetSampleData();

        // Remaining steps will follow...
    }

    /// <summary>
    /// Generates a sample DataTable with three columns and five rows.
    /// In a real app you’d replace this with a DB call.
    /// </summary>
    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

**Proč je to důležité:** Oddělením načítání dat do vlastní metody můžete libovolně zaměnit zdroj — SQL, CSV, webová služba — bez zásahu do logiky importu. To udržuje kód čistý a dělá tutoriál **jak importovat datatable do excel** znovupoužitelným.

## Krok 3: Definování stylů, které chcete použít

Nyní přichází zábavná část: vytvoříme pole objektů `Style`, z nichž každý má odlišnou `ForegroundColor`. GemBox vám umožní nastavit `BackgroundPatternColor` (vyplnění buňky) a `ForegroundColor` (barvu textu). Pro tuto ukázku obarvíme první dva sloupce odlišně.

```csharp
        // 2️⃣ Define the styles to apply to the imported cells.
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // Column 0 – Light blue fill
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Column 1 – Light green fill
            // No style for column 2 – it will keep the default look.
        };
```

**Vysvětlení:**  
- Objekt `Style` je lehký kontejner; nemusíte vytvářet nový pro každou buňku.  
- Zarovnáním pořadí pole se pořadím sloupců GemBox automaticky použije odpovídající styl během importu.  
- To je klíč k **importu dat s formátováním** — formátování cestuje spolu s daty, ne až po importu.

## Krok 4: Import `DataTable` do listu s použitím stylů

S připravenými daty a styly můžeme nyní vytvořit sešit, vybrat první list a zavolat `ImportDataTable`. Signatura metody vypadá takto:

```csharp
public void ImportDataTable(
    DataTable dataTable,
    bool includeColumnNames,
    int startRow,
    int startColumn,
    Style[] columnStyles = null);
```

Zde je, jak ji používáme:

```csharp
        // 3️⃣ Create a new workbook and import the DataTable.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        // Import, include column headers, start at A1 (0,0), apply our styles.
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the file to disk.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Excel file 'Report.xlsx' created with formatted data.");
```

**Co se děje pod kapotou?**  
- `true` říká GemBoxu, aby zapsal názvy sloupců jako první řádek.  
- `0, 0` umisťuje import do buňky A1.  
- `importStyles` spojuje každý sloupec s barvami, které jsme dříve definovali.  

Když otevřete *Report.xlsx*, uvidíte sloupec **ID** světle modrý, sloupec **Name** světle zelený a sloupec **Score** nezměněný. To je **import dat s formátováním** v jediném volání.

## Krok 5: Ověření výsledku (očekávaný výstup)

Otevřete vygenerovaný `Report.xlsx`. Měli byste vidět něco jako:

| ID (světle modrá) | Name (světle zelená) | Skóre |
|-------------------|----------------------|-------|
| 1                 | Alice                | 93.5 |
| 2                 | Bob                  | 78.0 |
| 3                 | Charlie              | 85.2 |
| 4                 | Diana                | 91.3 |
| 5                 | Ethan                | 67.8 |

- Buňky ve sloupci **ID** mají světle modré pozadí.  
- Buňky ve sloupci **Name** mají světle zelené pozadí.  
- Sloupec **Score** zůstává s výchozím bílým pozadím.

![Excel list ukazující import dat s formátováním – sloupec ID světle modrý, sloupec Name světle zelený](excel-screenshot.png "příklad importu dat s formátováním")

*Alt text obrázku obsahuje hlavní klíčové slovo pro SEO.*

## Časté otázky a okrajové případy

### Můžu použít více než jen barvy pozadí?

Ano. `Style` vám umožní nastavit písma, ohraničení, číselné formáty a dokonce podmíněné formátování. Například, aby byly skóre nad 90 tučná a červená:

```csharp
Style highScoreStyle = new Style()
{
    FontColor = Color.Red,
    FontBold = true
};
worksheet.Cells["C2:C6"].ConditionalFormatting.Add(
    ConditionalFormattingCondition.GreaterThan, "90", highScoreStyle);
```

### Co když má můj DataTable více sloupců než stylů?

GemBox použije styly jen na sloupce, pro které existuje odpovídající položka v poli. Přebytečné sloupce použijí výchozí styl — žádná chyba se nevyhodí.

### Funguje to s velkými datovými sadami?

Ano, ale dejte pozor na limit bezplatné verze (150 000 buněk). Pro obrovské reporty zvažte placenou licenci nebo streamování dat řádek po řádku pomocí `worksheet.Cells[row, col].Value = …` — přijdete však o pohodlí jednorázového volání.

### Jak importovat data s formátováním z existující šablony Excel?

Nejprve načtěte šablonu sešitu:

```csharp
var template = ExcelFile.Load("Template.xlsx");
var targetSheet = template.Worksheets[0];
targetSheet.Cells.ImportDataTable(dataTable, true, 5, 2, importStyles);
template.Save("FilledReport.xlsx");
```

Tím si zachováte loga v hlavičkách, patičky a jakékoli předdefinované styly, zatímco **importujete data s formátováním** pro dynamickou část.

## Kompletní funkční příklad (připravený ke kopírování a vložení)

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register free license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Get the source data.
        DataTable dataTable = GetSampleData();

        // 2️⃣ Define column styles (background colors).
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // ID column
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Name column
            // Score column gets default style.
        };

        // 3️⃣ Create workbook and import with styles.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the result.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Report.xlsx created – import data with formatting complete.");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

Spusťte program (`dotnet run`) a otevřete vygenerovaný *Report.xlsx*, abyste okamžitě viděli aplikované barvy.

## Závěr

Nyní máte pevný, konec

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}