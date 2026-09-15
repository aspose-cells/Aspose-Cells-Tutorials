---
category: general
date: 2026-02-15
description: Hozzon létre munkafüzetet C#-ban, és exportálja a DataTable-t Excelbe
  sorformázással, állítsa be a sor háttérszínét, és automatizálja az Excel feladatokat
  percek alatt.
draft: false
keywords:
- create workbook c#
- excel export formatting
- export datatable excel
- set row background
- excel automation c#
language: hu
og_description: Készíts gyorsan C#-os munkafüzetet, alkalmazz sorstílusokat, és automatizáld
  az Excel exportálást teljes kódrészletekkel és legjobb gyakorlat tippekkel.
og_title: Munkafüzet létrehozása C#‑ban – DataTable exportálása Excelbe formázással
tags:
- C#
- Excel
- DataExport
title: Munkafüzet létrehozása C# – DataTable exportálása Excelbe formázással
url: /hu/net/excel-data-export-retrieval/create-workbook-c-export-datatable-to-excel-with-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Munkafüzet létrehozása C#‑ban – DataTable exportálása Excelbe formázással

Volt már szükséged **create workbook C#**‑ra, és egy `DataTable`‑t Excelbe exportálni egyedi stílussal? Nem vagy egyedül. Sok üzleti alkalmazásban az a követelmény, hogy egy szépen formázott táblázatot generáljunk, amelyet egy nem technikai felhasználó azonnal megnyithat és megérthet.  

Ebben az útmutatóban egy teljes, azonnal futtatható megoldáson keresztül vezetünk végig, amely megmutatja, hogyan **create workbook C#**, hogyan alkalmazz **excel export formatting**, hogyan állíts be **row background**, és hogyan használd a **excel automation c#**‑t egy kifinomult fájl létrehozásához. Nincsenek homályos „lásd a dokumentációt” rövidítések – csak a teljes kód, magyarázatok arra, hogy miért fontos minden sor, és olyan tippek, amelyeket már holnap is használni fogsz.

---

## Előfeltételek

- .NET 6 (vagy .NET Framework 4.6+).  
- Visual Studio 2022 vagy bármely C#‑kompatibilis IDE.  
- A **Aspose.Cells for .NET** NuGet csomag (vagy bármely könyvtár, amely `Workbook`, `Worksheet`, `Style` osztályokat biztosít).  
- Alapvető ismeretek a `DataTable`‑ról.  

Ha még nincs Aspose.Cells, futtasd:

```bash
dotnet add package Aspose.Cells
```

> **Pro tipp:** Az ingyenes próba a legtöbb fejlesztési szcenárióban működik; csak ne felejtsd el a licenckulcsot cserélni a kiadás előtt.

![Create workbook C# példa, amely stílusos sorokat mutat Excelben]( "Create workbook C# példa sor háttérszínekkel")

---

## 1. lépés: A munkafüzet és munkalap inicializálása (Create Workbook C#)

Az első dolog, amit meg kell tenned, egy `Workbook` példányosítása. Gondolj rá úgy, mintha egy vadonatúj Excel fájlt nyitnál meg a memóriában.

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

**Miért?**  
`Workbook` az egész Excel dokumentumot tartalmazza, míg `Worksheet` egyetlen fület képvisel. Egy tiszta munkafüzetből indulva biztosítod, hogy minden kimeneti aspektust irányíthass – nem kerülnek be rejtett alapértelmezett stílusok.

---

## 2. lépés: Minta DataTable előkészítése (Export DataTable Excel)

Egy valódi projektben adatbázisból húznád az adatokat, de a szemléltetés kedvéért egy apró `DataTable`‑t hozunk létre helyben.

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

**Miért fontos ez:**  
A `DataTable` exportálása a leggyakoribb módja a táblázatos adatok egy alkalmazásból Excelbe való átvitelének. A fenti metódus teljesen önálló, így bármely projektbe be tudod másolni, és működni fog.

---

## 3. lépés: Stílus létrehozása soronként (Excel Export Formatting)

Ahhoz, hogy minden sor saját háttérszínt kapjon, egy `Style` objektumot generálunk a `DataTable` minden egyes sorához. Itt jön képbe a **excel export formatting**.

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

**Miért soronkénti stílus?**  
Ha ki szeretnél emelni bizonyos rekordokat (pl. lejárt számlák), egyszerű színciklust helyettesíthetsz feltételes logikával – csak állítsd be a `style.ForegroundColor`‑t a sor adatai alapján.

---

## 4. lépés: DataTable importálása sorstílusokkal (Set Row Background)

Most mindent összehozunk: az adatot, a munkafüzetet és a stílusokat.

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

**Mit fogsz látni:**  
Az `EmployeesReport.xlsx` megnyitása egy alapértelmezett formázású fejlécsort mutat, majd négy adat sort, mindegyik enyhe háttérszínnel festve. Az eredmény egy kézzel készített jelentéshez hasonlít, nem egy unalmas adatkiíráshoz.

---

## 5. lépés: Haladó Excel Automation C# tippek (Excel Automation C#)

Az alábbiakban néhány gyors trükköt találsz, amelyeket az alap példára építhetsz:

| Tipp | Kódrészlet | Mikor használjuk |
|-----|--------------|-------------|
| **Oszlopok automatikus méretezése** | `worksheet.AutoFitColumns();` | Adatok importálása után, hogy elkerüld a levágott szöveget. |
| **Fejléc sor rögzítése** | `worksheet.WindowPane.SplitRows = 1;` | Ha a táblázat a képernyőn túlra görgethető. |
| **Feltételes formázás** | <details><summary>Megjelenítés</summary>```csharp\nvar cf = worksheet.ConditionalFormattings[0];\ncf.AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");\ncf.Style.ForegroundColor = System.Drawing.Color.LightSalmon;\ncf.Style.Pattern = BackgroundType.Solid;\n```</details> | A küszöbérték feletti fizetések kiemelése. |
| **Munkalap védelme** | `worksheet.Protect(ProtectionType.All, "myPassword");` | Ha csak olvasható jelentéseket kell készíteni. |

---

## Gyakori kérdések és széljegyek

**Mi van, ha a DataTable több ezer sort tartalmaz?**  
Az Aspose.Cells hatékonyan streameli az adatokat, de a memória megtakarítása érdekében érdemes lehet letiltani a stílusok létrehozását minden sorra. Ehelyett alkalmazz egyetlen stílust egy tartományra:

```csharp
var range = worksheet.Cells.CreateRange(1, dt.Rows.Count, 0, dt.Columns.Count);
range.SetStyle(rowStyles[0]); // reuse one style for the whole block
```

**Exportálhatok .csv‑be az .xlsx helyett?**  
Persze – csak változtasd meg a mentési formátumot:

```csharp
workbook.Save("EmployeesReport.csv", SaveFormat.Csv);
```

A formázás elveszik (a CSV nem támogat stílusokat), de az adatexportálás ugyanaz marad.

**Működik ez .NET Core‑on?**  
Igen. Az Aspose.Cells támogatja a .NET Standard 2.0‑t és újabbakat, így ugyanaz a kód fut .NET 6, .NET 7 vagy .NET Framework környezetben.

---

## Teljes működő példa (másolás‑beillesztés kész)

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