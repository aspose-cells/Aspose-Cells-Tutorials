---
category: general
date: 2026-03-30
description: Vytvořte Excel sešit v C# s formátováním měny. Naučte se, jak importovat
  DataTable, přidat číselný formát v Excelu a během několika minut použít formát měny
  na sloupec.
draft: false
keywords:
- create excel workbook c#
- format cells currency
- import datatable to excel
- add number format excel
- apply currency format column
language: cs
og_description: Vytvořte Excel sešit v C# a okamžitě formátujte buňky jako měnu. Tento
  krok‑za‑krokem návod ukazuje, jak importovat DataTable do Excelu a přidat číselný
  formát pro sloupec.
og_title: Vytvoření Excel sešitu v C# – Průvodce formátováním měny
tags:
- Aspose.Cells
- C#
- Excel automation
title: Vytvořit Excel sešit v C# – použít formát měny a importovat DataTable
url: /cs/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření Excel sešitu C# – Použití formátu měny a import DataTable

Už jste někdy potřebovali **vytvořit Excel sešit C#**, který už vypadá jako profesionální zpráva? Možná taháte prodejní čísla z databáze a chcete, aby sloupec s cenou zobrazoval dolary, aniž byste museli ručně upravovat Excel. Zní to povědomě? Nejste v tom sami – většina vývojářů narazí na tento problém, když poprvé automatizují export do Excelu.

V tomto průvodci projdeme kompletním, připraveným řešením, které **vytvoří Excel sešit C#**, importuje `DataTable` a **naformátuje sloupec Price jako měnu**. Na konci budete mít soubor nazvaný `StyledTable.xlsx`, který můžete otevřít a uvidíte hezky naformátovaná čísla. Žádné další zpracování není potřeba.

> **Co se naučíte**
> - Jak nastavit Aspose.Cells v .NET projektu  
> - Jak **importovat datatable do excelu** pomocí pole stylů  
> - Jak **přidat číselný formát excel** pro konkrétní sloupec  
> - Tipy pro práci s více sloupci nebo různými locale  

> **Požadavky**
> - .NET 6+ (nebo .NET Framework 4.6+) nainstalovaný  
> - NuGet balíček Aspose.Cells pro .NET (`Install-Package Aspose.Cells`)  
> - Základní znalost C# a DataTables  

---

## Krok 1: Připravte DataTable (import datatable to excel)

Nejprve potřebujeme nějaká ukázková data. Ve skutečné aplikaci byste pravděpodobně tuto tabulku naplnili dotazem do databáze, ale pevně zakódovaný příklad udržuje věci jednoduché.

```csharp
using System.Data;

// Create a DataTable with two columns: Product (string) and Price (double)
DataTable dataTable = new DataTable();
dataTable.Columns.Add("Product", typeof(string));
dataTable.Columns.Add("Price", typeof(double));

// Add a few rows – you can add as many as you like
dataTable.Rows.Add("Apple", 1.23);
dataTable.Rows.Add("Banana", 0.78);
dataTable.Rows.Add("Cherry", 2.50);
```

*Proč je to důležité*: `DataTable` je most mezi vašimi obchodními daty a souborem Excel. Aspose.Cells jej může importovat přímo a zachovat názvy sloupců i datové typy.

---

## Krok 2: Vytvořte nový sešit (create excel workbook c#)

Nyní vytvoříme samotný objekt Excel souboru. Představte si ho jako prázdné plátno, na které budete malovat.

```csharp
using Aspose.Cells;

// Instantiate a fresh workbook – this is the core of create excel workbook c#
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0). You could also add more sheets later.
Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** Pokud potřebujete více listů, zavolejte `workbook.Worksheets.Add()` a každému dejte smysluplný název.

---

## Krok 3: Definujte styl měny (format cells currency)

Aspose.Cells vám umožní vytvořit objekt `Style`, který popisuje, jak mají buňky vypadat. Pro měnu použijeme vestavěný číselný formát ID 164 (`"$#,##0.00"`).

```csharp
// Create a new style object for the price column
Style priceStyle = workbook.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format "$#,##0.00"
```

*Proč ne nastavit jen řetězec formátu?* Použití vestavěného ID zajišťuje kompatibilitu napříč verzemi Excelu a vyhýbá se locale‑specifickým potížím.

---

## Krok 4: Sestavte pole stylů (apply currency format column)

Při importu `DataTable` můžete předat pole objektů `Style` – jeden pro každý sloupec. `null` znamená „použít výchozí styl“. Zde aplikujeme `priceStyle` pouze na druhý sloupec.

```csharp
// Column 0 (Product) gets the default style, Column 1 (Price) gets the currency style
Style[] columnStyles = { null, priceStyle };
```

Pokud později přidáte další sloupce, stačí pole rozšířit. Délka `columnStyles` musí odpovídat počtu sloupců, které importujete, jinak Aspose vyhodí výjimku.

---

## Krok 5: Importujte DataTable se styly (import datatable to excel)

Teď se stane kouzlo – náš `DataTable` se objeví v listu a sloupec s cenou okamžitě zobrazí měnu.

```csharp
// Parameters:
//  - dataTable: source data
//  - true: include column headers
//  - startRow: 0 (top of sheet)
//  - startColumn: 0 (first column)
//  - columnStyles: style array defined above
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

*Co když máte více než dva sloupce?* Stačí rozšířit `columnStyles`, aby každý sloupec dostal odpovídající styl (nebo `null` pro výchozí). Toto je nejčistší způsob, jak **přidat číselný formát excel** selektivně.

---

## Krok 6: Uložte sešit (create excel workbook c#)

Nakonec zapíšeme soubor na disk. Vyberte libovolnou složku, do které máte právo zapisovat.

```csharp
// Save the workbook as an XLSX file
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

Otevřete `StyledTable.xlsx` v Excelu a měli byste vidět:

| Product | Price |
|---------|-------|
| Apple   | $1.23 |
| Banana  | $0.78 |
| Cherry  | $2.50 |

Sloupec **Price** je již naformátován jako měna – žádné další kroky nejsou potřeba.

---

## Okrajové případy a varianty

### Více sloupců, různé formáty

Pokud potřebujete **formátovat buňky měnou** pro několik sloupců (např. Cost, Tax, Total), vytvořte pro každý samostatný `Style` a naplňte `columnStyles` odpovídajícím způsobem:

```csharp
Style costStyle = workbook.CreateStyle();
costStyle.Number = 164; // currency

Style taxStyle = workbook.CreateStyle();
taxStyle.Number = 164;

// Assuming columns: Product, Cost, Tax, Total
Style[] styles = { null, costStyle, taxStyle, priceStyle };
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, styles);
```

### Měna specifická pro locale

Pro euro nebo britskou libru použijte jiné vestavěné ID (např. 165 pro `€#,##0.00`). Alternativně nastavte vlastní řetězec formátu:

```csharp
priceStyle.Custom = "€#,##0.00";
```

### Velké datové sady

Aspose.Cells zvládne miliony řádků, ale spotřeba paměti roste s počtem objektů stylů. Pro všechny sloupce s měnou použijte jedinou instanci `Style`, abyste udrželi paměťovou stopu nízkou.

### Chybějící styly

Pokud je `columnStyles` kratší než počet sloupců, Aspose použije výchozí styl pro zbývající sloupce. To je užitečné, když vás zajímají jen některé sloupce.

---

## Kompletní funkční příklad (všechny kroky dohromady)

Níže je kompletní program, který můžete zkopírovat a vložit do konzolové aplikace. Obsahuje všechny části, o kterých jsme mluvili, a několik užitečných komentářů.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Build sample DataTable (import datatable to excel)
        // -------------------------------------------------
        DataTable dataTable = new DataTable();
        dataTable.Columns.Add("Product", typeof(string));
        dataTable.Columns.Add("Price", typeof(double));
        dataTable.Rows.Add("Apple", 1.23);
        dataTable.Rows.Add("Banana", 0.78);
        dataTable.Rows.Add("Cherry", 2.50);
        // You can add as many rows as you like here.

        // -------------------------------------------------
        // Step 2: Create a new workbook (create excel workbook c#)
        // -------------------------------------------------
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // -------------------------------------------------
        // Step 3: Define a currency style (format cells currency)
        // -------------------------------------------------
        Style priceStyle = workbook.CreateStyle();
        priceStyle.Number = 164; // "$#,##0.00" – built‑in currency format

        // -------------------------------------------------
        // Step 4: Build the style array (apply currency format column)
        // -------------------------------------------------
        // First column gets default style (null), second column uses priceStyle.
        Style[] columnStyles = { null, priceStyle };

        // -------------------------------------------------
        // Step 5: Import the DataTable with the style array
        // -------------------------------------------------
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // -------------------------------------------------
        // Step 6: Save the workbook to disk
        // -------------------------------------------------
        string outputPath = @"YOUR_DIRECTORY\StyledTable.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Očekávaný výsledek:** Po otevření `StyledTable.xlsx` uvidíte sloupec `Price` s dolarovým znakem a dvěma desetinnými místy, přesně tak, jak požadoval návod **format cells currency**.

---

## Často kladené otázky

**Q: Funguje to s .NET Core?**  
A: Naprosto. Aspose.Cells je kompatibilní s .NET standard, takže můžete cílit na .NET 5, .NET 6 nebo novější verze bez změn.

**Q: Co když má můj DataTable 10 sloupců, ale chci formátovat jen sloupec 5?**  
A: Vytvořte `Style[]` o délce 10, vyplňte pozice 0‑4 a 6‑9 hodnotou `null` a na index 4 (nulová báze) vložte svůj vlastní styl. Aspose respektuje každou položku.

**Q: Můžu skrýt řádek s hlavičkou?**  
A: Po importu nastavte `worksheet.Cells.Rows[0].Hidden = true;` nebo jednoduše předávejte `false` pro parametr `includeColumnNames` v metodě `ImportDataTable`.

---

## Závěr

Právě jsme **vytvořili Excel sešit C#**, importovali `DataTable` a **aplikovali formát měny** pomocí Aspose.Cells. Hlavní kroky – příprava dat, definice stylu, sestavení pole stylů, import pomocí `ImportDataTable` a uložení – pokrývají jádro většiny úloh automatizace Excelu.

Odtud můžete dál zkoumat:

- **přidat číselný formát excel** pro data nebo procenta  
- Export více listů v jednom souboru  
- Použití **format cells currency** s locale‑specifickými symboly  
- Automatizaci tvorby grafů na základě stejných dat  

Vyzkoušejte to a rychle se stanete osobou, na kterou se tým obrací s Excel reporty. Máte vlastní tip nebo trik? Napište komentář níže – šťastné kódování!  

![create excel workbook c# screenshot](image.png "create excel workbook c#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}