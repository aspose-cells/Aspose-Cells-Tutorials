---
category: general
date: 2026-03-22
description: Egyéni számformátum Excel oktató, amely bemutatja, hogyan importáljunk
  adat táblát Excelbe, állítsuk be az oszlop háttérszínét, formázzuk az oszlopot pénznemként,
  és mentsük a munkafüzetet xlsx formátumban.
draft: false
keywords:
- custom number format excel
- import datatable to excel
- set column background color
- format column as currency
- save workbook as xlsx
language: hu
og_description: Egyedi számformátum Excel oktató, amely végigvezet a DataTable importálásán,
  az oszlop háttérszínének beállításán, az oszlop pénznemkénti formázásán, és a munkafüzet
  xlsx formátumban való mentésén.
og_title: Egyéni számformátum Excelben C#-ban – Lépésről lépésre útmutató
tags:
- C#
- Excel automation
- Aspose.Cells
- Data export
title: Egyéni számformátum Excelben C#-ban – Teljes útmutató
url: /hu/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Egyedi számformátum Excel – Full‑Stack C# Bemutató

Gondolkodtál már azon, hogyan lehet **custom number format excel** stílust alkalmazni közvetlenül C#‑ból? Lehet, hogy már megpróbáltad egy DataTable‑t egy táblázatba exportálni, csak egyszerű számokat láttál, színek nélkül és pénznem formázás nélkül. Ez egy gyakori fájdalompont – különösen, ha egy kifinomult jelentésre van szükséged a döntéshozók számára.

Ebben az útmutatóban együtt megoldjuk ezt a problémát: megtanulod, hogyan **import datatable to excel**, **set column background color**, **format column as currency**, és végül **save workbook as xlsx** egy egyedi számformátummal, amely kiemeli az értékeket. Nincs homályos hivatkozás, csak egy teljes, futtatható megoldás, amelyet egyszerűen beilleszthetsz a projektedbe.

---

## Mit fogsz építeni

A tutorial végére egy önálló C# konzolos alkalmazásod lesz, amely:

1. Lekér egy `DataTable`‑t (a stubot kicserélheted a saját lekérdezésedre).  
2. Létrehoz egy új Excel munkafüzetet az Aspose.Cells (vagy bármely kompatibilis könyvtár) segítségével.  
3. Alkalmaz egy kék, félkövér betűtípust az első oszlopra, egy világos sárga háttérszínt a másodikra, és egy pénznem formátumot (`$#,##0.00`) a harmadikra.  
4. Elmenti a fájlt `DataTableWithStyleArray.xlsx` néven egy általad választott mappába.

Látni fogod, pontosan hogyan járul hozzá minden sor a végső Excel fájlhoz, és megvitatjuk, miért fontosak ezek a választások a karbantarthatóság és a teljesítmény szempontjából.

---

## Előfeltételek

- .NET 6.0 vagy újabb (a kód .NET Framework 4.7+‑vel is működik).  
- Aspose.Cells for .NET (ingyenes próba vagy licencelt verzió). Telepítés NuGet‑en keresztül:

```bash
dotnet add package Aspose.Cells
```

- Alapvető ismeretek a `DataTable`‑ról és a C# konzolos alkalmazásokról.

---

## 1. lépés: A forrásadatok lekérése DataTable‑ként

Először is szükségünk van némi adatra az exporthoz. Valós környezetben valószínűleg egy repository‑t hívnál vagy egy SQL lekérdezést futtatnál. Bemutatásként egy egyszerű táblát hozunk létre memóriában.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetSampleData()
{
    var table = new DataTable("Sales");
    table.Columns.Add("Product", typeof(string));
    table.Columns.Add("Quantity", typeof(int));
    table.Columns.Add("Revenue", typeof(decimal));

    table.Rows.Add("Widget A", 120, 3450.75m);
    table.Rows.Add("Widget B", 85, 2190.00m);
    table.Rows.Add("Widget C", 60, 1580.40m);

    return table;
}
```

> **Miért fontos:** A `DataTable` használata egy táblázatos, séma‑tudatos forrást biztosít, amely tisztán leképezhető az Excel sorokra és oszlopokra. Emellett lehetővé teszi, hogy ugyanazt az export logikát bármely adatkészlethez újrahasználd anélkül, hogy újraírnád a kódot.

---

## 2. lépés: Új munkafüzet létrehozása és az első munkalap lekérése

Most létrehozunk egy Excel munkafüzetet. A `Workbook` osztály képviseli az egész fájlt; a `Worksheets[0]` az alapértelmezett lap, ahová az adatainkat helyezzük.

```csharp
// Initialize a fresh workbook
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet
Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tipp:** Ha több lapra van szükséged, egyszerűen hívd a `workbook.Worksheets.Add("SheetName")`‑t, és ismételd meg a stíluslépéseket minden egyesnél.

---

## 3. lépés: Oszlopstílusok meghatározása – betűtípus, háttér és számformátum

Az Aspose.Cells‑ben a stílusok `Style` objektumokkal történnek. Egy tömböt hozunk létre, ahol minden elem a DataTable egy oszlopának felel meg.

```csharp
// Prepare an array to hold three distinct styles
Style[] columnStyles = new Style[3];

// 1️⃣ First column – blue, bold font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = System.Drawing.Color.Blue;
columnStyles[0].Font.IsBold = true;

// 2️⃣ Second column – light‑yellow background
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
columnStyles[1].Pattern = BackgroundType.Solid;

// 3️⃣ Third column – custom currency format (custom number format excel)
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Custom = "$#,##0.00";
```

> **Miért stílustömb?** Egy tömb átadása az `ImportDataTable`‑nek lehetővé teszi, hogy egyetlen hívásban különböző stílust alkalmazz minden oszlopra, ami egyszerű és teljesítményorientált. Emellett garantálja, hogy a formázás szinkronban marad az adat sorrendjével.

---

## 4. lépés: DataTable importálása a stílusok alkalmazásával

Itt van a művelet szíve: betápláljuk a `DataTable`‑t a munkalapba, megmondjuk az Aspose‑nak, hogy vegye fel a fejléc sort, és átadjuk a `columnStyles` tömböt.

```csharp
// Import data starting at cell A1 (row 0, column 0)
worksheet.Cells.ImportDataTable(
    GetSampleData(),   // source DataTable
    true,              // include column names as header
    0, 0,              // start row, start column
    columnStyles);     // apply the style array
```

> **Mi történik a háttérben?** Az Aspose végigiterál minden oszlopon, kiírja a fejlécet, majd minden sor értékét. Ezzel egyidejűleg alkalmazza a tömbből a megfelelő `Style`‑t, így egy kék „Product” fejlécet, egy sárgás árnyalatú „Quantity” oszlopot és egy szépen formázott „Revenue” oszlopot kapsz.

---

## 5. lépés: Munkafüzet mentése XLSX fájlként

Végül a munkafüzetet lemezre mentjük. A `Save` metódus automatikusan az XLSX formátumot választja a fájl kiterjesztése alapján.

```csharp
// Choose a folder that exists on your machine
string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";

// Ensure the directory exists (optional safety check)
System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);

// Save the workbook
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

> **Tipp:** Ha a fájlt stream‑ként kell továbbadni (pl. egy web API‑hoz), használd a `workbook.Save(stream, SaveFormat.Xlsx)`‑t a fájlútvonal helyett.

---

## Teljes működő példa

Az alábbiakban a teljes program látható, amelyet beilleszthetsz egy új konzolos projektbe. Fordítható és futtatható változatban egy stílusos Excel fájlt hoz létre.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Get data
            DataTable dataTable = GetSampleData();

            // Step 2 – Create workbook & worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 3 – Prepare column styles
            Style[] columnStyles = new Style[3];

            // Font style for first column (blue, bold)
            columnStyles[0] = workbook.CreateStyle();
            columnStyles[0].Font.Color = System.Drawing.Color.Blue;
            columnStyles[0].Font.IsBold = true;

            // Background style for second column (light yellow)
            columnStyles[1] = workbook.CreateStyle();
            columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
            columnStyles[1].Pattern = BackgroundType.Solid;

            // Currency format for third column (custom number format excel)
            columnStyles[2] = workbook.CreateStyle();
            columnStyles[2].Custom = "$#,##0.00";

            // Step 4 – Import data with styles
            worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

            // Step 5 – Save as XLSX
            string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";
            System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }

        // Helper method to build a demo DataTable
        static DataTable GetSampleData()
        {
            var table = new DataTable("Sales");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Revenue", typeof(decimal));

            table.Rows.Add("Widget A", 120, 3450.75m);
            table.Rows.Add("Widget B", 85, 2190.00m);
            table.Rows.Add("Widget C", 60, 1580.40m);

            return table;
        }
    }
}
```

### Várt eredmény

Amikor megnyitod a `DataTableWithStyleArray.xlsx` fájlt, a következőt fogod látni:

| **Product** (blue, bold) | **Quantity** (light‑yellow) | **Revenue** (currency) |
|--------------------------|-----------------------------|------------------------|
| Widget A                 | 120                         | $3,450.75              |
| Widget B                 | 85                          | $2,190.00              |
| Widget C                 | 60                          | $1,580.40              |

A megadott **custom number format excel** (`$#,##0.00`) biztosítja, hogy minden bevétel cella dollárjelet, ezres elválasztót és két tizedesjegyet jelenítsen meg – pontosan azt, amit a pénzügyi csapatok elvárnak.

---

## Gyakran Ismételt Kérdések és Különleges Esetek

### Használhatom ezt másik Excel könyvtárral?

Természetesen. A koncepció – oszloponként stílus létrehozása és importálás közbeni alkalmazása – átültethető EPPlus, ClosedXML vagy NPOI esetén is. Az API hívások különböznek, de a minta ugyanaz marad.

### Mi van, ha a DataTable‑m több oszlopot tartalmaz, mint a stílusok?

Az Aspose az alapértelmezett stílust alkalmazza minden olyan oszlopra, amelynek nincs megfelelő bejegyzése a `columnStyles` tömbben. A meglepetések elkerülése érdekében vagy állítsd be a tömb méretét a `dataTable.Columns.Count` értékére, vagy generálj stílusokat dinamikusan egy ciklusban.

### Hogyan állíthatok be egyedi számformátumot dátumokhoz?

Csak állítsd be a `style.Custom = "dd‑mm‑yyyy"`‑t (vagy bármely érvényes Excel formátum stringet). Ugyanez a tömb‑alapú megközelítés működik dátumok, százalékok vagy tudományos jelölés esetén is.

### Van mód a oszlopok automatikus méretezésére importálás után?

Igen – hívd a `worksheet.AutoFitColumns();`‑t az importálás után. Gyors szélességszámítást végez a cellák tartalma alapján.

### Mi a helyzet nagy adatkészletekkel (100 000+ sor)?

Az `ImportDataTable` tömeges műveletekre van optimalizálva, de előfordulhat memóriakorlát. Ebben az esetben fontold meg a sorok manuális streamelését a `Cells[i, j].PutValue(...)`‑val, és egyetlen `Style` objektum újrahasználatát a terhelés csökkentése érdekében.

---

## Pro tippek és gyakori buktatók

- **Kerüld a keménykódolt útvonalak** használatát a produkciós kódban; használd az `Environment.GetFolderPath`‑t vagy a konfigurációs beállításokat.  
- **A munkafüzetet zárd le** (dispose), ha hosszú‑távú szolgáltatásban vagy – tedd `using` blokkba a natív erőforrások felszabadításához.  
- **Figyelj a kultúraspecifikus elválasztókra**. A `custom` formátum `$#,##0.00` kényszeríti a pontot tizedeselválasztóként az operációs rendszer helyi beállításaitól függetlenül, ami általában a pénzügyi jelentésekhez szükséges.  
- **Ne felejtsd el hivatkozni a System.Drawing** (vagy a `.NET Core`‑on a `System.Drawing.Common`‑ra) a stílusban használt színstruktúrákhoz.  
- **Teszteld a kimenetet különböző Excel verziókon**; a régebbi verziók esetleg kissé eltérően értelmezhetik egyes egyedi formátumokat.

---

## Összegzés

Mindezt lefedtük, ami szükséges a **custom number format excel** fájlokhoz C#‑ból: adatlekérés `DataTable`‑ból, **import datatable to excel**, **set column background color** alkalmazása, **format column as currency** használata, és végül **save workbook as x

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}