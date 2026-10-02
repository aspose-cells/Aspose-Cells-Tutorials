---
category: general
date: 2026-02-09
description: Jak vytvořit sešit v C# s světle modrým pozadím a importovat data s hlavičkami.
  Naučte se přidat světle modré pozadí, použít výchozí styl Excelu a importovat datovou
  tabulku.
draft: false
keywords:
- how to create workbook
- add light blue background
- import data with headers
- excel import datatable c#
- use default style excel
language: cs
og_description: Jak vytvořit sešit v C# s světle modrým pozadím, importovat data s
  hlavičkami a použít výchozí styl Excelu — vše v jedné stručné příručce.
og_title: Jak vytvořit sešit – světle modré pozadí, import dat
tags:
- C#
- Excel
- Aspose.Cells
title: Jak vytvořit sešit – světle modré pozadí, import dat
url: /cs/net/excel-data-import-export/how-to-create-workbook-light-blue-background-data-import/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit sešit – světle modré pozadí, import dat

Už jste se někdy ptali, **jak vytvořit sešit** v C#, který vypadá o něco hezčím hned po vytvoření? Možná jste načetli `DataTable` z databáze a máte dost nudných, výchozích bílých buněk. V tomto tutoriálu vás provedeme vytvořením nového sešitu, přidáním světle modrého pozadí ke sloupci a importem dat s hlavičkami – vše při použití výchozího stylu, který Excel poskytuje.

Také přidáme několik scénářů „co‑když“, jako je zpracování null hodnot nebo přizpůsobení více než jednoho sloupce. Na konci budete mít plně stylovaný Excel soubor, který můžete předat zúčastněným stranám bez jakéhokoli následného zpracování.

## Požadavky

* **.NET 6+** (kód funguje také na .NET Framework 4.6+)  
* **Aspose.Cells for .NET** – knihovna, která poskytuje třídy `Workbook`, `Style` a `ImportDataTable`. Nainstalujte ji přes NuGet:  

  ```bash
  dotnet add package Aspose.Cells
  ```

* Zdroj `DataTable` – ve příkladu vytvoříme falešný, ale můžete jej nahradit libovolným ADO.NET dotazem.

Máte je? Skvělé, pojďme začít.

## Krok 1: Inicializace nového sešitu (Primární klíčové slovo)

První věc, kterou musíte udělat, je **jak vytvořit sešit** – doslova. Třída `Workbook` představuje celý Excel soubor a její konstruktor vám poskytuje čistý začátek.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

namespace ExcelStylingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or obtain an existing one)
            Workbook workbook = new Workbook();   // <-- this is how to create workbook
```

> **Proč je to důležité:** Začít s novým `Workbook` zajišťuje, že máte kontrolu nad všemi styly od samého začátku. Pokud otevřete existující soubor, zdědíte všechny styly, které autor ponechal, což může vést k nekonzistentnímu formátování.

## Krok 2: Připravte DataTable, který budete importovat

Pro ilustraci vytvoříme jednoduchý `DataTable`. Ve skutečných scénářích byste pravděpodobně volali uloženou proceduru nebo metodu ORM.

```csharp
            // Step 2: Retrieve the data you want to import (e.g., from a database)
            DataTable dataTable = GetSampleData(); // replace with your own GetData()
```

```csharp
        // Helper method that returns a dummy DataTable
        static DataTable GetSampleData()
        {
            DataTable table = new DataTable("Employees");
            table.Columns.Add("ID", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("HireDate", typeof(DateTime));
            table.Columns.Add("Salary", typeof(decimal));

            table.Rows.Add(1, "Alice Johnson", new DateTime(2020, 5, 12), 72000);
            table.Rows.Add(2, "Bob Smith", new DateTime(2019, 3, 4), 68000);
            table.Rows.Add(3, "Carol White", DBNull.Value, 75000); // demonstrates a null value
            return table;
        }
```

> **Tip:** Pokud potřebujete zachovat přesné pořadí sloupců tak, jak je v databázi, nastavte parametr `importColumnNames` metody `ImportDataTable` na `true`. Tím řeknete Aspose.Cells, aby pro vás zapsal hlavičky sloupců.

## Krok 3: Definujte styly sloupců – výchozí + světle modré pozadí

Nyní odpovídáme na část hádanky **přidat světle modré pozadí**. Aspose.Cells vám umožňuje předat pole objektů `Style`, které odpovídají každému importovanému sloupci. První položka je styl pro sloupec 0, druhá pro sloupec 1 a tak dále. Pokud máte méně stylů než sloupců, zbývající sloupce použijí výchozí styl.

```csharp
            // Step 3: Define column styles – the default style and a custom style with a light‑blue foreground
            Style defaultStyle = workbook.DefaultStyle; // this is the use default style excel
            Style lightBlueStyle = workbook.CreateStyle();
            lightBlueStyle.ForegroundColor = Color.LightBlue;
            lightBlueStyle.Pattern = BackgroundType.Solid; // make sure the color shows

            // Apply default style to the first column, light blue to the second column
            Style[] columnStyles = { defaultStyle, lightBlueStyle };
```

> **Proč jen dva styly?** V našem příkladu máme čtyři sloupce, ale chceme, aby vynikl pouze druhý sloupec (Name). Délka pole nemusí odpovídat počtu sloupců; chybějící položky automaticky zdědí výchozí styl sešitu.

## Krok 4: Importujte DataTable s hlavičkami a styly

Zde spojujeme **excel import datatable c#** a **import data with headers**. Metoda `ImportDataTable` provádí těžkou práci: zapíše názvy sloupců, řádky a aplikuje pole stylů, které jsme právě vytvořili.

```csharp
            // Step 4: Import the DataTable into the first worksheet starting at cell A1, applying the styles
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells.ImportDataTable(dataTable, // the source DataTable
                                        true,       // import column names as headers
                                        0,          // start row (0‑based)
                                        0,          // start column (0‑based)
                                        columnStyles);
```

### Očekávaný výsledek

Po spuštění programu bude `workbook` obsahovat jediný list, který vypadá takto:

| **ID** | **Jméno** (světle modré) | **Datum nástupu** | **Plat** |
|-------|------------------------|--------------|------------|
| 1     | Alice Johnson          | 5/12/2020    | 72000      |
| 2     | Bob Smith              | 3/4/2019     | 68000      |
| 3     | Carol White            | *(blank)*    | 75000      |

* Sloupec **Jméno** má světle modré pozadí, což dokazuje, že pole stylů funguje.
* Hlavičky sloupců jsou generovány automaticky, protože jsme předali `true` pro `importColumnNames`.
* Null hodnoty se zobrazují jako prázdné buňky, což je výchozí chování Aspose.Cells.

## Krok 5: Uložení sešitu (Volitelné, ale užitečné)

Pravděpodobně budete chtít soubor zapsat na disk nebo jej streamovat zpět webovému klientovi. Uložení je jednoduché:

```csharp
            // Step 5: Save the workbook to a file
            string outputPath = "StyledEmployees.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

> **Pro tip:** Pokud cílíte na starší verze Excelu, změňte `SaveFormat.Xlsx` na `SaveFormat.Xls`. API provede konverzi za vás.

## Okrajové případy a varianty

### Více stylovaných sloupců

Pokud potřebujete více než jeden stylovaný sloupec, jednoduše rozšiřte pole `columnStyles`:

```csharp
Style[] columnStyles = { defaultStyle, lightBlueStyle, defaultStyle, lightBlueStyle };
```

Nyní budou jak **Jméno**, tak **Plat** světle modré.

### Podmíněné formátování místo pevných stylů

Někdy chcete, aby se sloupec zbarvil červeně, když hodnota překročí práh. To je místo, kde **use default style excel** potkává podmíněné formátování:

```csharp
int salaryColIdx = 3; // zero‑based index for Salary column
FormatCondition condition = sheet.ConditionalFormattings[0]
    .AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");
condition.Style.ForegroundColor = Color.LightCoral;
condition.Style.Pattern = BackgroundType.Solid;
```

### Import bez hlaviček

Pokud váš následný systém již poskytuje vlastní hlavičky, stačí předat `false` pro argument `importColumnNames`. Data začnou v `A1` a můžete po té napsat vlastní hlavičky.

```csharp
sheet.Cells.ImportDataTable(dataTable, false, 1, 0); // start at row 2 (index 1)
```

## Úplný funkční příklad (Vše

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}