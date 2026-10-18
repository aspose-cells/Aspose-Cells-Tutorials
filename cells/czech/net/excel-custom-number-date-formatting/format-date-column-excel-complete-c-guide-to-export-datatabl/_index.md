---
category: general
date: 2026-07-13
description: Formátovat datumový sloupec v Excelu při exportu DataTable z C#. Naučte
  se exportovat DataTable do Excelu v C# a importovat DataTable do Excelu se stylováním
  během několika minut.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- format date column excel
- excel export datatable c#
- import datatable to excel
language: cs
lastmod: 2026-07-13
og_description: Formátujte sloupec s datem v Excelu snadno. Tento průvodce vám ukáže,
  jak exportovat datatable do Excelu v C# a importovat datatable do Excelu s vlastními
  styly.
og_image_alt: Screenshot showing a formatted date column in an Excel sheet generated
  from C#
og_title: Formátování datového sloupce v Excelu – krok za krokem tutoriál exportu
  v C#
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  headline: Format Date Column Excel – Complete C# Guide to Export DataTable
  type: TechArticle
- description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  name: Format Date Column Excel – Complete C# Guide to Export DataTable
  steps:
  - name: What if My DataTable Has More Than Three Columns?
    text: Just extend the `columnStyles` array. For any column you don’t explicitly
      style, leave the entry `null`; Excel will apply the default General format.
  - name: How to Apply a Custom Date Format (e.g., “dd‑MMM‑yyyy”)?
    text: 'Replace the built‑in number with a custom string:'
  - name: Can I Use This Approach with EPPlus or ClosedXML?
    text: 'Yes, the concept is identical: create a style object, assign it to a column,
      then load the `DataTable`. The API differs, but the **excel export datatable
      c#** pattern remains the same.'
  - name: What About Large DataSets (100k+ rows)?
    text: '`ImportDataTable` is optimized for bulk writes, but you might hit memory
      limits. In that case, consider streaming rows with `Cells.ImportDataTable` in
      chunks, or use `Worksheet.Cells["A1"].PutValue` in a loop while reusing the
      style objects.'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Export
title: Formátování sloupce s datem v Excelu – Kompletní C# průvodce exportem DataTable
url: /cs/net/excel-custom-number-date-formatting/format-date-column-excel-complete-c-guide-to-export-datatabl/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formátování sloupce s datem v Excelu – Kompletní průvodce C# pro export DataTable

Už jste někdy potřebovali **formátovat sloupec s datem v Excelu** při načítání dat z databáze, ale buňky stále ukazovaly surové časové značky? Nejste v tom sami. V mnoha podnikových aplikacích výchozí export vypíše hodnotu `DateTime` jako `2024‑03‑15 00:00:00` a nikdo takový nepořádek nechce.  

Dobrou zprávou je, že můžete řídit přesný vzhled každého sloupce přímo z C#. V tomto tutoriálu projdeme kompletní řešení, které **excel export datatable c#**, aplikuje styl data na první sloupec, styl měny na druhý a nakonec **import datatable to excel** s nulovým úsilím o formátování.

Na konci budete mít znovupoužitelnou metodu, kterou můžete vložit do libovolného .NET projektu, ať už používáte .NET 6, .NET Framework 4.8 nebo novější verzi.

---

## Co budete potřebovat

- **Aspose.Cells for .NET** (nebo libovolná knihovna, která nabízí `CreateStyle` a `ImportDataTable`). Ukázky kódu používají Aspose, protože jeho API je čisté a široce adoptované.
- **DataTable**, který už máte naplněný z SQL, CSV nebo jiného zdroje.
- Visual Studio (nebo vaše oblíbené IDE).  
- .NET runtime 5.0+ (ukázka cílí na .NET 6, ale starší frameworky fungují stejně).

Pokud ještě nemáte Aspose.Cells, stáhněte si bezplatnou zkušební verzi z oficiální stránky – bez nutnosti zadávat platební kartu.

---

## Krok 1: Načtení zdrojových dat jako DataTable

Nejprve potřebujete `DataTable`. V reálných scénářích obvykle pochází z `SqlDataAdapter.Fill`, ale pro přehlednost si vytvoříme jednoduchou tabulku:

```csharp
using System;
using System.Data;

DataTable GetSampleData()
{
    var dt = new DataTable();
    dt.Columns.Add("OrderDate", typeof(DateTime));
    dt.Columns.Add("TotalAmount", typeof(decimal));
    dt.Columns.Add("Customer", typeof(string));

    dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
    dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
    dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");

    return dt;
}
```

> **Tip:** Když načítáte data přímo ze stored procedure, ujistěte se, že typy sloupců odpovídají zamýšleným formátům v Excelu. Sloupec typu `datetime` bude později cílem našeho **format date column excel** stylu.

---

## Krok 2: Vytvoření Excel sešitu a definice stylů sloupců

Nyní vytvoříme nový sešit. Trik pro **format date column excel** spočívá ve vytvoření objektu `Style`, nastavení jeho vlastnosti `Number` na vestavěný formát data v Excelu (kód 14) a přiřazení tohoto stylu ke správnému indexu sloupce.

```csharp
using Aspose.Cells;

Workbook wb = new Workbook();               // creates a blank workbook
Worksheet sheet = wb.Worksheets[0];        // we’ll work with the first sheet

// Prepare a style array – one entry per DataTable column
Style[] columnStyles = new Style[dt.Columns.Count];

// Column 0 – format as a short date (e.g., 03/15/2024)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Excel built‑in date format

// Column 1 – format as currency (e.g., $1,245.67)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].Number = 2;                // Built‑in currency format

// Column 2 – no special formatting; leave null or default
columnStyles[2] = null;
```

Proč `Number = 14`? Excel ukládá data jako sériová čísla; formát 14 říká programu, aby tato čísla zobrazil podle lokálního krátkého formátu data. Pokud potřebujete vlastní vzor (např. `dd‑MMM‑yyyy`), můžete místo toho nastavit `columnStyles[0].Custom = "dd-MMM-yyyy"`.

---

## Krok 3: Import DataTable do listu s aplikovanými styly

Jakmile je pole stylů připravené, import je jediný řádek kódu. To je jádro **excel export datatable c#** a zároveň místo, kde **import datatable to excel** zachovává naše formátování.

```csharp
// Import the DataTable, include column headers, start at cell A1 (row 0, column 0)
sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
```

Přetížení `ImportDataTable`, které používáme, přijímá pole stylů a aplikuje každý styl na odpovídající sloupec během zápisu dat. Není potřeba žádná následná smyčka – váš sloupec s datem je už hezky naformátovaný.

---

## Krok 4: Uložení sešitu (nebo přímé streamování do prohlížeče)

Podle scénáře můžete soubor uložit na disk, do paměťového proudu nebo jej vrátit jako HTTP odpověď. Zde jsou tři běžné vzory:

```csharp
// 1️⃣ Save to a physical file
wb.Save("ExportedReport.xlsx");

// 2️⃣ Save to a MemoryStream (useful for ASP.NET Core)
using var ms = new MemoryStream();
wb.Save(ms, SaveFormat.Xlsx);
ms.Position = 0; // rewind for downstream consumers

// 3️⃣ Return as a file download in ASP.NET MVC
public IActionResult DownloadReport()
{
    var dt = GetSampleData();
    var wb = BuildWorkbook(dt); // encapsulate steps 2‑3 in a method
    using var ms = new MemoryStream();
    wb.Save(ms, SaveFormat.Xlsx);
    return File(ms.ToArray(), 
                "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
                "Report.xlsx");
}
```

> **Pozor:** Pokud používáte `FileResult` v ASP.NET Core, nezapomeňte nastavit `Response.Headers["Cache-Control"] = "no-cache"` při generování souboru za běhu. Zabrání to prohlížeči, aby podával zastaralou verzi.

---

## Krok 5: Ověření výsledku – Jak vypadá Excel list

Po spuštění kódu otevřete `ExportedReport.xlsx`. Měli byste vidět:

| OrderDate (formatted) | TotalAmount (currency) | Customer |
|-----------------------|------------------------|----------|
| 03/13/2024            | $1,245.67              | Acme Corp|
| 03/14/2024            | $980.00                | Beta Ltd |
| 03/15/2024            | $1,500.25              | Gamma Inc|

Všimněte si, že **format date column excel** zobrazuje čistý krátký datum, zatímco sloupec měny se automaticky přizpůsobí vašim regionálním nastavením. Není potřeba ručně formátovat buňky po jedné.

![format date column excel example](/images/format-date-column-excel.png)

*Alt text obrázku: format date column excel – screenshot Excel listu s řádně naformátovaným sloupcem data.*

---

## Často kladené otázky a okrajové případy

### Co když má můj DataTable více než tři sloupce?

Jednoduše rozšiřte pole `columnStyles`. Pro sloupce, které nechcete explicitně stylovat, ponechte položku `null`; Excel použije výchozí formát General.

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 10; // Percent format, for example
```

### Jak použít vlastní formát data (např. „dd‑MMM‑yyyy”)?

Nahraďte vestavěné číslo vlastním řetězcem:

```csharp
columnStyles[0].Custom = "dd-MMM-yyyy";
```

### Lze tento přístup použít s EPPlus nebo ClosedXML?

Ano, koncept je stejný: vytvoříte objekt stylu, přiřadíte jej sloupci a načtete `DataTable`. API se liší, ale pattern **excel export datatable c#** zůstává stejný.

### Co s velkými datovými sadami (100 k+ řádků)?

`ImportDataTable` je optimalizováno pro hromadné zápisy, ale můžete narazit na limity paměti. V takovém případě zvažte streamování řádků pomocí `Cells.ImportDataTable` po částech, nebo použijte `Worksheet.Cells["A1"].PutValue` ve smyčce při opakovaném použití objektů stylů.

---

## Kompletní funkční příklad (všechny kroky v jedné metodě)

Níže je samostatná metoda, kterou můžete zkopírovat a vložit do libovolné konzolové aplikace nebo ASP.NET kontroleru. Ukazuje celý tok – od načtení dat po export Excelu se stylováním.

```csharp
using System;
using System.Data;
using System.IO;
using Aspose.Cells;

public class ExcelExporter
{
    // Entry point for demonstration
    public static void Main()
    {
        DataTable dt = GetSampleData();
        Workbook wb = BuildWorkbook(dt);
        wb.Save("StyledExport.xlsx");
        Console.WriteLine("Excel file created – check StyledExport.xlsx");
    }

    // Generates the sample DataTable (Step 1)
    private static DataTable GetSampleData()
    {
        var dt = new DataTable();
        dt.Columns.Add("OrderDate", typeof(DateTime));
        dt.Columns.Add("TotalAmount", typeof(decimal));
        dt.Columns.Add("Customer", typeof(string));

        dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
        dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
        dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");
        return dt;
    }

    // Builds the workbook with styled columns (Steps 2‑3)
    private static Workbook BuildWorkbook(DataTable dt)
    {
        var wb = new Workbook();
        var sheet = wb.Worksheets[0];

        // Allocate style array
        Style[] columnStyles = new Style[dt.Columns.Count];

        // Format column 0 as short date
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].Number = 14; // short date

        // Format column 1 as currency
        columnStyles[1] = wb.CreateStyle();
        columnStyles[1].Number = 2; // currency

        // No style for column 2 (Customer name)
        columnStyles[2] = null;

        // Import with headers, start at A1
        sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
        return wb;
    }
}
```

Spusťte program, otevřete `StyledExport.xlsx` a uvidíte, že **format date column excel** byl aplikován perfektně.

---

## Shrnutí a další kroky

Právě jsme si ukázali, jak **format date column excel** při **excel export datatable c#**, a jak **import datatable to excel** s formátováním po sloupcích v jediném volání. Hlavní body:

1. Vytvořte `Style` pro každý sloupec, který chcete formátovat.  
2. Použijte `Number = 14` pro data, `Number = 2` pro měnu nebo libovolný vlastní formát.  
3. Předávejte pole stylů metodě `ImportDataTable` – knihovna udělá těžkou práci.

Co můžete zkusit dál?

- **Podmíněné formátování** pro zvýraznění prodlevých dat.  
- **


## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným krok‑za‑krokem vysvětlením, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vlastních projektech.

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Export Excel Data to DataTable Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/import-export/export-excel-data-datatatable-aspose-cells-net/)
- [Export HTML Strings from Excel to DataTable using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}