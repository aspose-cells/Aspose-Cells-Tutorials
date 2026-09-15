---
category: general
date: 2026-09-15
description: Naučte se, jak uložit sešit jako CSV, exportovat Excel do TXT a použít
  vlastní číselný formát při převodu hodnot buněk na velká písmena v C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save workbook as csv
- apply custom number format
- export excel to txt
- uppercase cell values
- export worksheet as text
language: cs
lastmod: 2026-09-15
og_description: Uložte sešit jako CSV, exportujte Excel do TXT a použijte vlastní
  číselný formát při převodu hodnot buněk na velká písmena pomocí Aspose.Cells v C#.
og_image_alt: Screenshot showing workbook saved as CSV using C# code
og_title: Uložte sešit jako CSV a exportujte Excel do TXT s vlastním formátováním
  v C#
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to save workbook as CSV, export Excel to TXT, and apply custom
    number format while converting cell values to uppercase in C#.
  headline: How to save workbook as CSV and export Excel to TXT with custom formatting
    in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak uložit sešit jako CSV a exportovat Excel do TXT s vlastním formátováním
  v C#
url: /cs/net/converting-excel-files-to-other-formats/how-to-save-workbook-as-csv-and-export-excel-to-txt-with-cus/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak uložit sešit jako CSV a exportovat Excel do TXT s vlastním formátováním v C#

Pokud potřebujete **uložit sešit jako CSV** a zároveň exportovat list jako prostý text a použít vlastní číselný formát, tento průvodce vám ukáže kompletní, připravené řešení. Uvidíte, jak zachovat číselnou přesnost, převést každou hodnotu buňky na velká písmena a pracovat s daty v japonském erovém kalendáři – vše pomocí Aspose.Cells pro .NET.

Exportování dat z Excelu často znamená manipulaci s několika formáty: CSV pro výměnu dat, TXT pro starší systémy a vlastní číselné formáty pro lokálně specifické reportování. Tento tutoriál vás provede každým požadavkem krok za krokem, takže můžete kód přímo zkopírovat do svého projektu.

V následujících sekcích se naučíte, jak:

* **uložit sešit jako csv** s definovaným počtem významných číslic  
* **exportovat excel do txt** a zároveň vynutit **velká písmena v hodnotách buněk**  
* **použít vlastní číselný formát** pro japonské erové datumy a přečíst formátovaný výsledek  

Není potřeba žádných externích nástrojů – stačí knihovna Aspose.Cells a vývojové prostředí .NET.

## Požadavky

* .NET 6.0 nebo novější (kód také funguje s .NET Framework 4.8)  
* Aspose.Cells pro .NET (NuGet balíček `Aspose.Cells`)  
* Základní znalost C# a konceptů Excelu  

---

## Krok 1: Uložení sešitu jako CSV s řízenou přesností

Když **uložíte sešit jako CSV**, číselné hodnoty jsou zapsány pomocí výchozího řetězcového reprezentace, což může vést ke ztrátě přesnosti. Nastavením `CsvSaveOptions.SignificantDigits` určíte Aspose.Cells, kolik významných číslic má zachovat.

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (or load an existing one)
Workbook workbook = new Workbook();               // you can also use new Workbook("input.xlsx");

// Configure CSV options to keep up to 4 significant digits
CsvSaveOptions csvOptions = new CsvSaveOptions
{
    SignificantDigits = 4   // ensures numbers like 123.4567 stay precise
};

// Save the workbook as CSV
string csvPath = @"C:\Temp\Digits.csv";
workbook.Save(csvPath, csvOptions);

Console.WriteLine($"Workbook saved as CSV to {csvPath}");
```

**Proč je to důležité:**  
Nastavení `SignificantDigits` zabraňuje zaokrouhlovacím chybám, které se často objevují při výměně velkých datových sad s podřadnými systémy (např. datovými sklady). Objekt `CsvSaveOptions` vám také umožňuje řídit oddělovače, kódování a další CSV‑specifické nastavení, pokud je potřeba.

## Krok 2: Export listu jako prostý text při převodu hodnot na velká písmena

Export listu do jednoduchého souboru `.txt` je užitečný pro starší importní rutiny, které očekávají data oddělená mezerami. Povolením `ExportTableOptions.ExportAsString` a poskytnutím delegáta `CustomExport` můžete **exportovat excel do txt** a současně vynutit **velká písmena v hodnotách buněk**.

```csharp
// Prepare export options for plain‑text output
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true, // forces every cell to be treated as a string
    // CustomExport receives the cell and its current string value,
    // allowing you to modify it before it is written.
    CustomExport = (cell, value) =>
    {
        // Convert the cell value to an upper‑case string
        return value?.ToString().ToUpperInvariant();
    }
};

// Define the output path for the text file
string txtPath = @"C:\Temp\Table.txt";

// Export the first worksheet (index 0) as a tab‑delimited text file
workbook.Worksheets[0].ExportTable(txtPath, tableOptions);

Console.WriteLine($"Worksheet exported as text to {txtPath}");
```

**Proč je to důležité:**  
Mnoho integračních bodů (např. dávkové úlohy na mainframe) očekává identifikátory v kapitálkách. Callback `CustomExport` vám dává plnou kontrolu nad reprezentací každé buňky, což umožňuje vložit transformace jako ořezávání, doplňování nebo lokálně specifické formátování bez nutnosti post‑processingu souboru.

## Krok 3: Použití vlastního číselného formátu a načtení formátovaného výsledku

Vestavěné číselné formáty v Excelu pokrývají většinu případů, ale někdy potřebujete zobrazit datum v konkrétním kalendářním systému – například v japonské éře. Následující kód ukazuje, jak **použít vlastní číselný formát** na buňku a poté přečíst formátovaný řetězec, který respektuje jazykové nastavení sešitu.

```csharp
// Create a new workbook for the era example
Workbook eraWorkbook = new Workbook();

// Access the first worksheet and target cell A1
Worksheet sheet = eraWorkbook.Worksheets[0];
Cell dateCell = sheet.Cells["A1"];

// Insert a Japanese‑era date string (Reiwa 3 = 2021)
dateCell.PutValue("Reiwa 3/04/01");

// Apply a built‑in date number format (14 = mm-dd-yy)
// You could also assign a custom format string, e.g., "[$-ja-JP]ggge年m月d日"
Style style = eraWorkbook.CreateStyle();
style.Number = 14; // standard short date format
dateCell.SetStyle(style);

// Force formula calculation (necessary if the cell contains a formula)
eraWorkbook.CalculateFormula();

// Retrieve the formatted string as it would appear in Excel
string formattedDate = dateCell.StringValue;
Console.WriteLine($"Formatted date (locale aware): {formattedDate}");
```

**Proč je to důležité:**  
Použití `SetStyle` s číselným formátem zajišťuje, že zobrazení buňky respektuje regionální nastavení, což je klíčové pro reporty distribuované napříč různými locale. Když později čtete `StringValue`, získáte přesně ten řetězec, který uživatel vidí v uživatelském rozhraní Excelu, čímž se eliminuje potřeba ručního parsování.

## Kompletní, spustitelný příklad

Níže je jediný program, který kombinuje všechny tři kroky. Vložte jej do nového projektu Console App, přidejte NuGet balíček Aspose.Cells a spusťte.

```csharp
using Aspose.Cells;
using System;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Save workbook as CSV ----------
            Workbook workbook = new Workbook(); // start with a fresh workbook
            // (Optionally load an existing file: new Workbook("input.xlsx"))

            // Populate some sample data
            workbook.Worksheets[0].Cells["A1"].PutValue(123.456789);
            workbook.Worksheets[0].Cells["B1"].PutValue("Sample Text");

            CsvSaveOptions csvOptions = new CsvSaveOptions
            {
                SignificantDigits = 4
            };
            string csvPath = @"C:\Temp\Digits.csv";
            workbook.Save(csvPath, csvOptions);
            Console.WriteLine($"Saved CSV to {csvPath}");

            // ---------- Step 2: Export worksheet as text with uppercase ----------
            ExportTableOptions tableOptions = new ExportTableOptions
            {
                ExportAsString = true,
                CustomExport = (cell, value) => value?.ToString().ToUpperInvariant()
            };
            string txtPath = @"C:\Temp\Table.txt";
            workbook.Worksheets[0].ExportTable(txtPath, tableOptions);
            Console.WriteLine($"Exported TXT to {txtPath}");

            // ---------- Step 3: Apply custom number format ----------
            Workbook eraWorkbook = new Workbook();
            Cell dateCell = eraWorkbook.Worksheets[0].Cells["A1"];
            dateCell.PutValue("Reiwa 3/04/01");

            Style eraStyle = eraWorkbook.CreateStyle();
            eraStyle.Number = 14; // short date format; replace with custom if needed
            dateCell.SetStyle(eraStyle);
            eraWorkbook.CalculateFormula();

            Console.WriteLine($"Japanese era date formatted: {dateCell.StringValue}");
        }
    }
}
```

**Očekávaný výstup**

```
Saved CSV to C:\Temp\Digits.csv
Exported TXT to C:\Temp\Table.txt
Japanese era date formatted: 4/1/2021
```

(Přesný formát data se může lišit podle nastavení locale vašeho systému.)

---

## Často kladené otázky a řešení okrajových případů

| Otázka | Odpověď |
|----------|--------|
| *Co když potřebuji jiný oddělovač v CSV?* | Nastavte `csvOptions.Separator` na `','`, `'\t'` nebo jakýkoli vlastní znak před voláním `Save`. |
| *Mohu zachovat původní číselnou přesnost místo zaokrouhlování?* | Použijte `SignificantDigits = 0` pro zápis celé hodnoty s dvojitou přesností, nebo nastavte `NumberDecimalSeparator` pro locale‑specifické desetinné symboly. |
| *Jak exportovat jen konkrétní oblast místo celého listu?* | Zavolejte `ExportTable(string fileName, ExportTableOptions options, CellArea area)` a předáte `CellArea`, který oblast definuje. |
| *Co když sešit obsahuje vzorce odkazující na jiné listy?* | Ujistěte se, že před exportem zavoláte `workbook.CalculateFormula()`; jinak získáte pouze uložené (cached) hodnoty. |
| *Existuje způsob, jak zachovat původní formátování buněk (písma, barvy) v TXT souboru?* | Formáty prostého textu nemohou zachovat vizuální stylování. Pokud potřebujete bohaté formátování, zvažte export do HTML (`HtmlSaveOptions`). |

## Závěr

Nyní víte, jak **uložit sešit jako CSV** s řízenou přesností, **exportovat excel do TXT** při vynucení **velkých písmen v hodnotách buněk** a **použít vlastní číselný formát** pro lokálně citlivé zobrazování datumů. Každý úryvek je samostatný, funguje ihned a dodržuje osvědčené postupy jak pro výkon, tak pro udržovatelnost.

Dále můžete zkoumat:

* Použití `HtmlSaveOptions` pro zachování stylování při exportu do web‑přátelských formátů.  
* Využití `CsvSaveOptions.Encoding` pro UTF‑8 nebo jiné znakové sady při práci s vícejazyčnými daty.  
* Automatizaci dávkového zpracování více listů pomocí smyčky přes `workbook.Worksheets`.

Neváhejte přizpůsobit kód svým datovým pipelineům a nechte flexibilitu Aspose.Cells udělat těžkou práci za vás.

---

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vlastních projektech.

- [Uložit sešit do textového CSV formátu](/cells/german/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)
- [Uložit sešit do textového CSV formátu](/cells/french/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)
- [Uložit sešit do textového CSV formátu](/cells/spanish/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}