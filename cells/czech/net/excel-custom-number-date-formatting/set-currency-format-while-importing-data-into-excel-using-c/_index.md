---
category: general
date: 2026-11-19
description: Nastavte formát měny v Excelu pomocí C# – naučte se, jak nastavit číselný
  formát a styl sloupců v Excelu během importu listu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set currency format
- how to set number format
- assign number format
- excel worksheet import
- style excel columns
language: cs
lastmod: 2026-11-19
og_description: Nastavte formát měny v Excelu pomocí C# a objevte, jak nastavit formát
  čísel, přiřadit formát čísel a stylovat sloupce v Excelu během importu listu.
og_image_alt: Screenshot showing Excel cells formatted as currency after import
og_title: Nastavte formát měny v Excelu pomocí C# – kompletní průvodce krok za krokem
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  headline: Set currency format while importing data into Excel using C#
  type: TechArticle
- description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  name: Set currency format while importing data into Excel using C#
  steps:
  - name: Expected result
    text: 'When you open **FinancialReport.xlsx**, you’ll see:'
  - name: Assign number format to date columns
    text: '```csharp // Suppose column 2 contains dates and you want "dd-MMM-yyyy"
      columnStyles[2].Number = 14; // 14 = built‑in short date ```'
  - name: Use custom number formats for percentages
    text: '```csharp columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00% ```'
  - name: Styling beyond number formats
    text: 'You can also set font, background color, or alignment on the same `Style`
      object:'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
- Formatting
title: Nastavit formát měny při importu dat do Excelu pomocí C#
url: /cs/net/excel-custom-number-date-formatting/set-currency-format-while-importing-data-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nastavení formátu měny při importu dat do Excelu pomocí C#

Pokud potřebujete **nastavit formát měny** v listu Excelu, tento návod vám ukáže, jak **nastavit formát čísel** a stylovat sloupce během **importu listu Excel**. Uvidíte kompletní, spustitelný příklad, který přiřadí správný formát čísel každému sloupci `DataTable` a importuje data s požadovaným stylem.

Práce s Excelem z C# často vyžaduje víc než jen vypsání surových hodnot — musíte také řídit, jak se čísla zobrazují. Ať už generujete faktury, finanční zprávy nebo dashboardy, správné formátování měny, procent nebo dat okamžitě zpřehlední výstup.

## Požadavky

* .NET 6.0 (nebo novější) nainstalováno.
* Odkaz na **Aspose.Cells for .NET** (nebo libovolnou knihovnu, která poskytuje třídu `Style` s vlastností `Number`).  
  *NuGet*: `Install-Package Aspose.Cells`.
* Základní znalost `DataTable` a kolekcí v C#.
* IDE, např. Visual Studio 2022 nebo VS Code.

## Krok 1: Získání dat, která budou zapsána do listu

Nejprve získejte `DataTable`, který obsahuje surová data, jež chcete exportovat. V reálných projektech může pocházet z databázového dotazu, volání API nebo CSV parseru.

```csharp
using System.Data;

/// <summary>
/// Returns a sample DataTable with three columns:
/// Id (int), Amount (decimal), and Description (string).
/// </summary>
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Amount", typeof(decimal));
    table.Columns.Add("Description", typeof(string));

    // Sample rows
    table.Rows.Add(1, 1234.56m, "Office supplies");
    table.Rows.Add(2, 98765.43m, "Consulting fees");
    table.Rows.Add(3, 0.99m, "Miscellaneous");

    return table;
}

// Retrieve the data
DataTable dataTable = GetData();
```

> **Proč je to důležité:** Importování plně naplněného `DataTable` vám umožní oddělit logiku získávání dat od logiky generování Excelu, což zlepšuje testovatelnost a udržovatelnost.

## Krok 2: Vytvoření pole stylů — jedna položka na sloupec v DataTable

Aspose.Cells očekává `Style[]`, jehož délka odpovídá počtu sloupců, které chcete importovat. Každý prvek může obsahovat konkrétní formát čísla.

```csharp
// Allocate a Style object for each column
Style[] columnStyles = new Style[dataTable.Columns.Count];

// Initialize each Style instance (required before assigning properties)
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = ws.Workbook.CreateStyle();
}
```

> **Tip:** I když potřebujete formátování jen pro podmnožinu sloupců, musíte vytvořit instanci `Style` pro každý sloupec; jinak během importu získáte `NullReferenceException`.

## Krok 3: Přiřazení formátu čísel požadovaným sloupcům

Vestavěná čísla stylů se liší podle knihovny. V Aspose.Cells:

* `0` → Obecný (celé číslo)  
* `2` → Měna (např. `$#,##0.00`)  
* `3` → Datum, atd.

Zde **přiřazujeme formát čísel** dvěma sloupcům: první sloupec (Id) zůstává jako celé číslo, zatímco druhý sloupec (Amount) získá formát měny.

```csharp
// Column 0 → integer format (style number 0)
columnStyles[0].Number = 0;

// Column 1 → currency format (style number 2)
columnStyles[1].Number = 2;

// If you need a custom format, you can also use a format string:
// columnStyles[1].Custom = "$#,##0.00";
```

> **Jak nastavit formát čísel**: Použití vlastnosti `Number` je nejrychlejší způsob, jak vybrat vestavěný formát. Pro měny specifické pro locale zvažte použití vlastního formátovacího řetězce, který obsahuje odpovídající symbol měny.

## Krok 4: Import DataTable do listu s aplikací stylů sloupců

Jakmile je pole stylů připravené, importujte data. Metoda `ImportDataTable` respektuje předané styly.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];

// Import the DataTable, starting at cell A1 (row 0, column 0)
// The third argument (true) tells the method to write column headers.
ws.Cells.ImportDataTable(
    dataTable,
    /* includeColumnNames */ true,
    /* startRow */ 0,
    /* startColumn */ 0,
    columnStyles);

// Save the workbook
workbook.Save("FinancialReport.xlsx", SaveFormat.Xlsx);
```

### Očekávaný výsledek

Když otevřete **FinancialReport.xlsx**, uvidíte:

| Id | Částka      | Popis            |
|----|------------|------------------|
| 1  | $1,234.56  | Kancelářské potřeby |
| 2  | $98,765.43 | Poradenské služby |
| 3  | $0.99      | Různé            |

*Sloupec **Částka** je zobrazen pomocí nastaveného formátu měny, zatímco **Id** zůstává jako celé číslo.*

## Jak nastavit formát čísel pro další scénáře

### Přiřazení formátu čísel ke sloupcům s daty

```csharp
// Suppose column 2 contains dates and you want "dd-MMM-yyyy"
columnStyles[2].Number = 14; // 14 = built‑in short date
```

### Použití vlastních formátů čísel pro procenta

```csharp
columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00%
```

### Stylování nad rámec formátů čísel

Na stejném objektu `Style` můžete také nastavit písmo, barvu pozadí nebo zarovnání:

```csharp
columnStyles[1].Font.IsBold = true;
columnStyles[1].ForegroundColor = Color.LightYellow;
columnStyles[1].HorizontalAlignment = TextAlignmentType.Center;
```

> **Proč to funguje:** Objekt `Style` shromažďuje všechny vizuální vlastnosti buňky. Když předáte pole metodě `ImportDataTable`, každá buňka automaticky zdědí definovaný styl.

## Časté úskalí a jak se jim vyhnout

| Úskalí | Příznak | Řešení |
|--------|---------|--------|
| Zapomenutí vytvořit každou instanci `Style` | `NullReferenceException` při importu | Projděte pole v cyklu a zavolejte `CreateStyle()` před nastavením vlastností. |
| Použití nesprávného vestavěného číselného indexu | Špatný formát (např. data se zobrazují jako celá čísla) | Podívejte se do dokumentace knihovny na správné konstanty `Number`. |
| Neuložení sešitu | Žádný výstupní soubor nebo prázdný soubor | Po dokončení importu zavolejte `workbook.Save(...)`. |
| Neshoda locale pro symbol měny | `$` se zobrazuje i v locale, které nejsou US | Použijte vlastní formátovací řetězec s odpovídajícím symbolem (např. `"€#,##0.00"`). |

## Kompletní, spustitelný příklad



## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto návodu. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Vytvořit Excel soubor C# – stylovat buňky a nastavit formát měny](/cells/english/net/excel-formatting-and-styling/create-excel-file-c-style-cells-and-set-currency-format/)
- [Jak formátovat sloupce v Excelu v C# – kompletní průvodce](/cells/english/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/)
- [Vytvořit Excel sešit C# – aplikovat formát měny a importovat DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}