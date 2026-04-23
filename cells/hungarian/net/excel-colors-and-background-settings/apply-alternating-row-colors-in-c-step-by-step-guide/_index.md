---
category: general
date: 2026-03-18
description: Tanulja meg, hogyan alkalmazzon váltakozó sor színeket egy munkalapon
  C#-ban. Tartalmazza a sor háttérszínének beállítását, a világos sárga háttér hozzáadását
  és a sorok váltakozó színezését.
draft: false
keywords:
- apply alternating row colors
- set row background color
- add light yellow background
- set alternating row shading
- color rows alternately
language: hu
og_description: Alkalmazzon váltakozó sor színeket C#-ban az olvashatóság javítása
  érdekében. Ez az útmutató bemutatja, hogyan állítsa be a sor háttérszínét, hogyan
  adjon hozzá világos sárga háttérszínt, és hogyan színezze a sorokat váltakozva.
og_title: Váltakozó sorok színének alkalmazása C#-ban – Teljes útmutató
tags:
- C#
- DataTable
- Spreadsheet styling
- UI design
title: Váltakozó sorok színének alkalmazása C#-ban – Lépésről lépésre útmutató
url: /hu/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Alkalmazzon váltakozó sor színeket C#‑ban – Teljes útmutató

Valaha is szüksége volt **váltakozó sor színek** alkalmazására egy adat‑vezérelt munkalapon, de nem tudta, hol kezdje? Nem egyedül van ezzel – a legtöbb fejlesztő ugyanebbe a helyzetbe kerül, amikor először próbálja barátságosabbá tenni a táblázatokat. A jó hír? Néhány C#‑sorral **beállíthatja a sor háttérszínét**, hozzáadhat egy **light yellow background**‑ot, és egy kifinomult rácsot kap, amely azonnal javítja az olvashatóságot.

Ebben az útmutatóban végigvezetjük a teljes folyamatot, a `DataTable` memóriába töltésétől a sorok finom sárga‑fehér csíkos stílusáig. A végére magabiztosan **color rows alternately** tud majd, és néhány hasznos variációt is megmutatunk, ha más árnyalatokra vagy dinamikus témára van szüksége.

## What You’ll Need

Mielőtt belevágunk, győződjön meg róla, hogy a következőkkel rendelkezik:

- Egy .NET projekt, amely .NET 6 vagy újabb célkeretrendszert használ (a kód .NET Framework 4.7+‑on is működik).  
- Egy táblázatkezelő könyvtár, amely támogatja a stílusobjektumokat – a példában egy általános `Workbook`/`Worksheet` API‑t használunk, amely hasonló a **Aspose.Cells**, **GemBox.Spreadsheet** vagy **ClosedXML** könyvtárakhoz.  
- Egy `DataTable` forrás – lehet adatbázis‑lekérdezés, CSV‑import vagy bármilyen memóriában lévő gyűjtemény.  

Nem szükséges extra NuGet csomag a táblázatkezelő könyvtáron kívül. Ha Aspose.Cells‑t használ, a névtér `Aspose.Cells`; ClosedXML‑nél `ClosedXML.Excel`. Cserélje ki a `CreateStyle` és `ImportDataTable` hívásokat ennek megfelelően.

## Step 1: Retrieve the Source Data as a DataTable

First thing’s first—grab the data you want to display. In real‑world apps this usually means hitting a database, but for clarity we’ll stub a helper method called `GetData()` that returns a populated `DataTable`.

```csharp
// Step 1: Retrieve the source data as a DataTable
DataTable dataTable = GetData();   // Replace with your actual data retrieval logic
```

> **Why this matters:** The `DataTable` defines the rows and columns that later receive the alternating shading. If the table is empty, there’s nothing to style, so always verify that `Rows.Count` > 0 before proceeding.

### Pro tip
If you’re pulling data from Entity Framework, you can use `DataTable.Load(reader)` after executing a `SqlCommand`. That keeps the code tidy and avoids manual column definitions.

## Step 2: Allocate an Array to Hold a Style for Each Row

Next, we need a container that matches the number of rows. Most spreadsheet APIs let you pass a style array to the import method, so we’ll create a `Style[]` sized exactly to the row count.

```csharp
// Step 2: Allocate an array to hold a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];
```

> **Explanation:** By pre‑allocating the array, we avoid reallocating a new style object on every iteration, which can be a performance win when dealing with thousands of rows.

## Step 3: Apply Alternating Row Colors (Light Yellow / White)

Now comes the heart of the matter: **apply alternating row colors**. We’ll loop through each row, create a fresh style instance from the workbook, and set its background based on the row index. Even rows get a light yellow fill, odd rows stay white.

```csharp
// Step 3: Create alternating background colors (light yellow / white) for the rows
for (int rowIndex = 0; rowIndex < dataTable.Rows.Count; rowIndex++)
{
    // Create a new style instance from the workbook
    rowStyles[rowIndex] = wb.CreateStyle();

    // Apply a light yellow background to even rows, white to odd rows
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow   // add light yellow background
        : Color.White;        // set row background color to white

    rowStyles[rowIndex].Pattern = BackgroundType.Solid; // set alternating row shading
}
```

### Why this works
- **`rowIndex % 2 == 0`** checks whether the row is even.  
- **`Color.LightYellow`** gives a gentle, non‑intrusive hue that’s perfect for data tables.  
- **`BackgroundType.Solid`** ensures the fill covers the whole cell, achieving the **set row background color** effect.  

You can swap `Color.LightYellow` with any other shade (e.g., `Color.LightCyan`) if you prefer a different look. The same logic also lets you **color rows alternately** based on other criteria, such as status flags.

## Step 4: Import the DataTable into the Worksheet with the Prepared Styles

Finally, we push everything into the worksheet. Most libraries expose an `ImportDataTable` overload that accepts a style array. The `true` flag tells the API to write column headers, and the `0, 0` coordinates start at the top‑left cell.

```csharp
// Step 4: Import the DataTable into the worksheet, applying the prepared row styles
ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

> **Result:** The worksheet now displays your data with a clean **alternating row shading** pattern—light yellow on even rows, white on odd rows. Users can scan the grid without their eyes hopping back and forth.

### Expected Output
If you opened the resulting spreadsheet, you’d see something like this:

| ID | Name      | Quantity |
|----|-----------|----------|
| **1** | Apple      | 50       |
| **2** | Banana     | 30       |
| **3** | Cherry     | 20       |
| **4** | Date       | 15       |

Rows 1, 3, 5… have a **light yellow background**, while rows 2, 4, 6… remain **white**. The header row (row 0) inherits the default style unless you customize it separately.

## Optional Variations & Edge Cases

### 1. Using a Different Color Palette
If light yellow clashes with your branding, simply replace `Color.LightYellow` with another `System.Drawing.Color`. For a blue‑gray theme you might use:

```csharp
rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
    ? Color.FromArgb(220, 235, 247) // soft blue
    : Color.White;
```

### 2. Dynamic Shading Based on Data
Sometimes you want to highlight rows that meet a condition (e.g., low inventory). Combine the modulo check with a custom test:

```csharp
int quantity = Convert.ToInt32(dataTable.Rows[rowIndex]["Quantity"]);
if (quantity < 20)
{
    rowStyles[rowIndex].ForegroundColor = Color.Salmon; // urgent low‑stock color
}
else
{
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow
        : Color.White;
}
```

### 3. Applying Styles to Specific Columns Only
If you only need the **set row background color** on certain columns, create a separate style for each column and assign it after the import using the worksheet’s cell range API.

```csharp
// Example for column B only
var colBStyle = wb.CreateStyle();
colBStyle.ForegroundColor = Color.LightYellow;
colBStyle.Pattern = BackgroundType.Solid;

// Apply after import
ws.Cells[$"B2:B{dataTable.Rows.Count + 1}"].SetStyle(colBStyle);
```

### 4. Performance Tip for Large Tables
When dealing with > 10,000 rows, consider reusing a single style object for each color instead of creating a new one per row. The array then holds references to the two shared styles, dramatically cutting memory usage.

```csharp
Style yellowStyle = wb.CreateStyle();
yellowStyle.ForegroundColor = Color.LightYellow;
yellowStyle.Pattern = BackgroundType.Solid;

Style whiteStyle = wb.CreateStyle();
whiteStyle.ForegroundColor = Color.White;
whiteStyle.Pattern = BackgroundType.Solid;

for (int i = 0; i < dataTable.Rows.Count; i++)
    rowStyles[i] = (i % 2 == 0) ? yellowStyle : whiteStyle;
```

## Full Working Example

Below is a self‑contained program you can paste into a console app. It uses a fictitious `Workbook`/`Worksheet` API; replace the types with those from your chosen library.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using YourSpreadsheetLib;     // Replace with actual namespace

class Program
{
    static void Main()
    {
        // Initialize workbook & worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Step 1: Retrieve data
        DataTable dataTable = GetData();

        // Step 2: Allocate style array
        Style[] rowStyles = new Style[dataTable.Rows.Count];

        // Step 3: Apply alternating row colors
        for (int i = 0; i < dataTable.Rows.Count; i++)
        {
            rowStyles[i] = wb.CreateStyle();
            rowStyles[i].ForegroundColor = (i % 2 == 0)
                ? Color.LightYellow   // add light yellow background
                : Color.White;        // set row background color
            rowStyles[i].Pattern = BackgroundType.Solid; // set alternating row shading
        }

        // Step 4: Import with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // Save to file
        wb.Save("AlternatingRows.xlsx");
        Console.WriteLine("Workbook saved with alternating row colors.");
    }

    // Sample data generator
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(1, "Apple", 50);
        dt.Rows.Add(2, "Banana", 30);
        dt.Rows.Add(3, "Cherry", 20);
        dt.Rows.Add(4, "Date", 15);
        dt.Rows.Add(5, "Elderberry", 5);
        return dt;
    }
}
```

**Output:** A file named `AlternatingRows.xlsx` where each row alternates between a light yellow fill and white, making the table easier on the eyes.

## Frequently Asked Questions

**Q: Does this approach work with Excel‑style conditional formatting?**  
A: Yes. If your library supports conditional rules, you can translate the same logic into a rule that checks `MOD(ROW(),2)=0`. The code‑based method shown here is more portable across libraries that lack built‑in conditional formatting.

**Q: What if I need to **color rows alternately** in a PDF table instead of an Excel sheet?**  
A: Most PDF table generators (e.g., iTextSharp, PdfSharp) let you set a `BackgroundColor` per row. The same modulo calculation applies—

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}