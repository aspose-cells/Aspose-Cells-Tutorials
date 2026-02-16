---
category: general
date: 2026-02-15
description: Vytvořte sešit v C# a exportujte DataTable do Excelu s formátováním řádků,
  nastavte pozadí řádku a automatizujte úkoly v Excelu během několika minut.
draft: false
keywords:
- create workbook c#
- excel export formatting
- export datatable excel
- set row background
- excel automation c#
language: cs
og_description: Rychle vytvořte sešit v C#, aplikujte styly řádků a automatizujte
  export do Excelu s kompletními příklady kódu a tipy na osvědčené postupy.
og_title: Vytvořit sešit v C# – Exportovat DataTable do Excelu s formátováním
tags:
- C#
- Excel
- DataExport
title: Vytvořit sešit C# – Export DataTable do Excelu s formátováním
url: /cs/net/excel-data-export-retrieval/create-workbook-c-export-datatable-to-excel-with-formatting/
---

step by step.

I'll write final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření sešitu C# – Export DataTable do Excelu s formátováním

Už jste někdy potřebovali **vytvořit sešit C#** a uložit `DataTable` do Excelu s vlastním stylováním? Nejste v tom sami. V mnoha podnikových aplikacích je požadavek vyprodukovat hezky naformátovaný tabulkový soubor, který ne‑technický uživatel otevře a okamžitě pochopí.

V tomto průvodci projdeme kompletním, připraveným řešením, které vám ukáže **jak vytvořit sešit C#**, použít **excel export formatting**, nastavit **row background** a využít **excel automation c#** k vytvoření vylepšeného souboru. Žádné vágní odkazy typu „viz dokumentace“ – jen celý kód, vysvětlení, proč je každá řádka důležitá, a tipy, které můžete použít už zítra.

---

## Požadavky

- .NET 6 (nebo .NET Framework 4.6+).  
- Visual Studio 2022 nebo jakékoli IDE podporující C#.  
- NuGet balíček **Aspose.Cells for .NET** (nebo libovolná knihovna poskytující `Workbook`, `Worksheet`, `Style`).  
- Základní znalost `DataTable`.  

Pokud ještě nemáte Aspose.Cells, spusťte:

```bash
dotnet add package Aspose.Cells
```

> **Tip:** Bezplatná zkušební verze funguje pro většinu vývojových scénářů; jen nezapomeňte před nasazením nahradit licenční klíč.

---

![Create workbook C# example showing styled rows in Excel]( "Create workbook C# example with row background colors")

---

## Krok 1: Inicializace sešitu a listu (Create Workbook C#)

První, co musíte udělat, je vytvořit instanci `Workbook`. Představte si to jako otevření zcela nového Excel souboru v paměti.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // Create a new workbook – this is the core of create workbook C#
        var workbook = new Workbook();

        // Grab the first worksheet (index 0) – it's already there by default
        var worksheet = workbook.Worksheets[0];

        // The rest of the steps will fill this worksheet with data and styling
        ExportDataTableWithStyling(workbook, worksheet);
    }
}
```

**Proč?**  
`Workbook` obsahuje celý Excel dokument, zatímco `Worksheet` představuje jeden list. Začátek s čistým sešitem vám dává plnou kontrolu nad výstupem – žádné skryté výchozí styly, které by se mohly nechtěně objevit.

---

## Krok 2: Příprava ukázkového DataTable (Export DataTable Excel)

Ve skutečném projektu byste data načítali z databáze, ale pro ilustraci vytvoříme malý `DataTable` za běhu.

```csharp
private static DataTable GetSampleData()
{
    var dt = new DataTable("Employees");
    dt.Columns.Add("Id", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Department", typeof(string));
    dt.Columns.Add("Salary", typeof(decimal));

    dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
    dt.Rows.Add(2, "Bob Smith", "IT", 68000);
    dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
    dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);

    return dt;
}
```

**Proč je to důležité:**  
Export `DataTable` je nejčastější způsob, jak přenést tabulková data z aplikace do Excelu. Výše uvedená metoda je zcela samostatná, takže ji můžete zkopírovat do libovolného projektu a bude fungovat.

---

## Krok 3: Vytvoření stylu pro každý řádek (Excel Export Formatting)

Aby každý řádek měl vlastní barvu pozadí, vytvoříme objekt `Style` pro každý řádek v `DataTable`. Zde se ukazuje síla **excel export formatting**.

```csharp
private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
{
    var styles = new Style[rowCount];

    // Define a palette of background colors – feel free to extend
    var colors = new[] { System.Drawing.Color.LightYellow,
                         System.Drawing.Color.LightCyan,
                         System.Drawing.Color.LightGreen,
                         System.Drawing.Color.LightPink };

    for (int i = 0; i < rowCount; i++)
    {
        // Create a fresh style instance
        var style = workbook.CreateStyle();

        // Cycle through our color array so rows get alternating shades
        style.ForegroundColor = colors[i % colors.Length];
        style.Pattern = BackgroundType.Solid;

        // Optional: make the font a little bolder for readability
        style.Font.IsBold = true;

        styles[i] = style;
    }

    return styles;
}
```

**Proč stylovat řádek po řádku?**  
Pokud potřebujete zvýraznit konkrétní záznamy (např. prodlené faktury), můžete místo jednoduchého cyklu barev použít podmíněnou logiku – stačí nastavit `style.ForegroundColor` podle dat v řádku.

---

## Krok 4: Import DataTable s řádkovými styly (Set Row Background)

Nyní spojíme vše dohromady: data, sešit a styly.

```csharp
private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
{
    // 1️⃣ Get the data
    DataTable dt = GetSampleData();

    // 2️⃣ Build a style for each row
    Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

    // 3️⃣ Import the DataTable starting at cell A1.
    //    The `true` flag tells Aspose.Cells to include column headers.
    worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

    // 4️⃣ Save the workbook to disk
    string outputPath = "EmployeesReport.xlsx";
    workbook.Save(outputPath);
    Console.WriteLine($"Workbook saved to {outputPath}");
}
```

**Co uvidíte:**  
Po otevření `EmployeesReport.xlsx` uvidíte hlavičkový řádek v výchozím formátování a čtyři datové řádky, z nichž každý má lehkou barvu pozadí. Výsledek vypadá jako ručně vytvořená zpráva, ne jako nudný výpis.

---

## Krok 5: Pokročilé tipy pro Excel Automation C# (Excel Automation C#)

Níže najdete několik rychlých triků, které můžete přidat k základnímu příkladu:

| Tip | Ukázka kódu | Kdy použít |
|-----|--------------|------------|
| **Auto‑Fit Columns** | `worksheet.AutoFitColumns();` | Po importu dat, aby nedošlo ke zkrácení textu. |
| **Freeze Header Row** | `worksheet.WindowPane.SplitRows = 1;` | Když tabulka může přesáhnout výšku obrazovky. |
| **Conditional Formatting** | <details><summary>Show</summary>```csharp\nvar cf = worksheet.ConditionalFormattings[0];\ncf.AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");\ncf.Style.ForegroundColor = System.Drawing.Color.LightSalmon;\ncf.Style.Pattern = BackgroundType.Solid;\n```</details> | Zvýraznit platy nad určitým prahem. |
| **Protect Sheet** | `worksheet.Protect(ProtectionType.All, "myPassword");` | Když potřebujete zprávy jen pro čtení. |

Tyto úryvky ukazují šíři možností **excel automation c#** – můžete sešit rozšiřovat, aniž byste přepisovali základní logiku importu.

---

## Často kladené otázky a okrajové případy

**Co když má DataTable tisíce řádků?**  
Aspose.Cells data streamuje efektivně, ale můžete chtít zakázat vytváření stylu pro každý řádek, abyste ušetřili paměť. Místo toho použijte jeden styl pro celý rozsah:

```csharp
var range = worksheet.Cells.CreateRange(1, dt.Rows.Count, 0, dt.Columns.Count);
range.SetStyle(rowStyles[0]); // reuse one style for the whole block
```

**Mohu exportovat do .csv místo .xlsx?**  
Jistě – stačí změnit formát uložení:

```csharp
workbook.Save("EmployeesReport.csv", SaveFormat.Csv);
```

Styling se ztratí (CSV nemá žádné formátování), ale export dat zůstane stejný.

**Funguje to na .NET Core?**  
Ano. Aspose.Cells podporuje .NET Standard 2.0 a novější, takže stejný kód běží na .NET 6, .NET 7 i .NET Framework.

---

## Kompletní funkční příklad (Copy‑Paste Ready)

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // 1️⃣ Create a new workbook – core of create workbook C#
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // 2️⃣ Export DataTable with styling
        ExportDataTableWithStyling(workbook, worksheet);
    }

    private static DataTable GetSampleData()
    {
        var dt = new DataTable("Employees");
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Department", typeof(string));
        dt.Columns.Add("Salary", typeof(decimal));

        dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
        dt.Rows.Add(2, "Bob Smith", "IT", 68000);
        dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
        dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);
        return dt;
    }

    private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
    {
        var styles = new Style[rowCount];
        var colors = new[]
        {
            System.Drawing.Color.LightYellow,
            System.Drawing.Color.LightCyan,
            System.Drawing.Color.LightGreen,
            System.Drawing.Color.LightPink
        };

        for (int i = 0; i < rowCount; i++)
        {
            var style = workbook.CreateStyle();
            style.ForegroundColor = colors[i % colors.Length];
            style.Pattern = BackgroundType.Solid;
            style.Font.IsBold = true;
            styles[i] = style;
        }

        return styles;
    }

    private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
    {
        DataTable dt = GetSampleData();
        Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

        // Import with row styles – sets row background (set row background)
        worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

        // Optional polish
        worksheet.AutoFitColumns();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}