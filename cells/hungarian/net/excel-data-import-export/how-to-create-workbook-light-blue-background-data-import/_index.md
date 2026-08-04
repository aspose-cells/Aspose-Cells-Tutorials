---
category: general
date: 2026-02-09
description: Hogyan hozzunk létre munkafüzetet C#-ban világoskék háttérrel, és importáljunk
  adatokat fejlécekkel. Tanulja meg, hogyan adjon hozzá világoskék hátteret, használja
  az alapértelmezett Excel-stílust, és importálja a DataTable-t.
draft: false
keywords:
- how to create workbook
- add light blue background
- import data with headers
- excel import datatable c#
- use default style excel
language: hu
og_description: Hogyan hozzunk létre C#-ban egy munkafüzetet világoskék háttérrel,
  importáljunk adatokat fejlécekkel, és alkalmazzuk az alapértelmezett Excel-stílust
  – mindezt egy tömör útmutatóban.
og_title: Hogyan készítsünk munkafüzetet – Világoskék háttér, adatimport
tags:
- C#
- Excel
- Aspose.Cells
title: Munkafüzet létrehozása – Világoskék háttér, adatimport
url: /hu/net/excel-data-import-export/how-to-create-workbook-light-blue-background-data-import/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan hozzunk létre munkafüzetet – Világoskék háttér, adatimportálás

Gondoltad már, **hogyan hozzunk létre munkafüzetet** C#‑ban, ami egy kicsit szebben néz ki már a dobozból? Talán egy `DataTable`‑t húztál ki egy adatbázisból, és eleged van a unalmas, alap‑fehér cellákból. Ebben az útmutatóban végigvezetünk egy új munkafüzet létrehozásán, egy világoskék háttér hozzáadásán egy oszlophoz, és az adatok importálásán fejlécekkel – mindezt az Excel alapértelmezett stílusának használatával.

Be fogunk szórni néhány “mi‑ha” forgatókönyvet is, például null értékek kezelése vagy több oszlop testreszabása. A végére egy teljesen formázott Excel‑fájlod lesz, amelyet közvetlenül szállíthatsz a stakeholder‑eknek utófeldolgozás nélkül.

## Előfeltételek

Mielőtt belevágnánk, győződj meg róla, hogy rendelkezel:

* **.NET 6+** (a kód .NET Framework 4.6+‑on is működik)  
* **Aspose.Cells for .NET** – a könyvtár, amely a `Workbook`, `Style` és `ImportDataTable` hívásokat biztosítja. Telepítsd NuGet‑en keresztül:  

  ```bash
  dotnet add package Aspose.Cells
  ```

* Egy `DataTable` forrás – a példában egyet szimulálunk, de helyettesítheted bármely ADO.NET lekérdezéssel.

Megvan minden? Remek, kezdjünk bele.

## 1. lépés: Új munkafüzet inicializálása (Primary Keyword)

Az első dolog, amit meg kell tenned, **hogyan hozzunk létre munkafüzetet** – szó szerint. A `Workbook` osztály képviseli az egész Excel‑fájlt, és a konstruktorja egy tiszta lapot ad.

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

> **Miért fontos:** Egy friss `Workbook`‑kel kezdve minden stílust a kezdetektől irányíthatsz. Ha egy meglévő fájlt nyitsz meg, akkor örökölöd az eredeti szerző által hagyott stílusokat, ami következetlen formázáshoz vezethet.

## 2. lépés: Készítsd elő a importálandó DataTable‑t

Az illusztráció kedvéért hozzunk létre egy egyszerű `DataTable`‑t. Valós környezetben valószínűleg egy tárolt eljárást vagy ORM metódust hívnál meg.

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

> **Tipp:** Ha pontosan úgy akarod megőrizni az oszlopsorrendet, ahogy az adatbázisban szerepel, állítsd az `ImportDataTable` `importColumnNames` paraméterét `true`‑ra. Ez azt mondja az Aspose.Cells‑nek, hogy írja ki helyetted az oszlopfejléceket.

## 3. lépés: Oszlopstílusok definiálása – Alap + Világoskék háttér

Most válaszolunk a **add light blue background** feladványra. Az Aspose.Cells lehetővé teszi, hogy egy `Style` objektumokból álló tömböt adj meg, amely minden importált oszlophoz tartozik. Az első elem a 0‑s oszlop stílusa, a második az 1‑es, stb. Ha kevesebb stílus van, mint oszlop, a hiányzó oszlopok az alapstílust öröklik.

```csharp
            // Step 3: Define column styles – the default style and a custom style with a light‑blue foreground
            Style defaultStyle = workbook.DefaultStyle; // this is the use default style excel
            Style lightBlueStyle = workbook.CreateStyle();
            lightBlueStyle.ForegroundColor = Color.LightBlue;
            lightBlueStyle.Pattern = BackgroundType.Solid; // make sure the color shows

            // Apply default style to the first column, light blue to the second column
            Style[] columnStyles = { defaultStyle, lightBlueStyle };
```

> **Miért csak két stílus?** A példánk négy oszlopot tartalmaz, de csak a második oszlopot (Name) akarjuk kiemelni. A tömb hossza nem kell, hogy megegyezzen az oszlopszámmal; a hiányzó bejegyzések automatikusan az alapstílust veszik át.

## 4. lépés: DataTable importálása fejlécekkel és stílusokkal

Itt egyesítjük a **excel import datatable c#** és a **import data with headers** elemeket. Az `ImportDataTable` metódus végzi a nehéz munkát: kiírja az oszlopneveket, a sorokat, és alkalmazza a korábban épített stílustömböt.

```csharp
            // Step 4: Import the DataTable into the first worksheet starting at cell A1, applying the styles
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells.ImportDataTable(dataTable, // the source DataTable
                                        true,       // import column names as headers
                                        0,          // start row (0‑based)
                                        0,          // start column (0‑based)
                                        columnStyles);
```

### Várt eredmény

A program futtatása után a `workbook` egyetlen munkalapot tartalmaz, amely így néz ki:

| **ID** | **Name** (világoskék) | **HireDate** | **Salary** |
|-------|------------------------|--------------|------------|
| 1     | Alice Johnson          | 5/12/2020    | 72000      |
| 2     | Bob Smith              | 3/4/2019     | 68000      |
| 3     | Carol White            | *(blank)*    | 75000      |

* A **Name** oszlop világoskék háttérrel rendelkezik, bizonyítva, hogy a stílustömb működik.
* Az oszlopfejlécek automatikusan generálódnak, mivel a `importColumnNames` paramétert `true`‑ra állítottuk.
* A null értékek üres cellaként jelennek meg, ami az Aspose.Cells alapértelmezett viselkedése.

## 5. lépés: Munkafüzet mentése (Opcionális, de hasznos)

Valószínűleg a fájlt le akarod menteni a lemezre vagy vissza akarod streamelni egy webkliensnek. A mentés egyszerű:

```csharp
            // Step 5: Save the workbook to a file
            string outputPath = "StyledEmployees.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

> **Pro tipp:** Ha régebbi Excel verziókat célozol, változtasd a `SaveFormat.Xlsx`‑et `SaveFormat.Xls`‑re. Az API elvégzi a konverziót helyetted.

## Szélső esetek és variációk

### Több stílusú oszlop

Ha egynél több oszlopot szeretnél stílusozni, egyszerűen bővítsd a `columnStyles` tömböt:

```csharp
Style[] columnStyles = { defaultStyle, lightBlueStyle, defaultStyle, lightBlueStyle };
```

Most a **Name** és a **Salary** is világoskék lesz.

### Feltételes formázás rögzített stílus helyett

Néha egy oszlopnak pirosra kell váltania, ha az érték egy küszöböt meghalad. Itt jön a **use default style excel** a feltételes formázással együtt:

```csharp
int salaryColIdx = 3; // zero‑based index for Salary column
FormatCondition condition = sheet.ConditionalFormattings[0]
    .AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");
condition.Style.ForegroundColor = Color.LightCoral;
condition.Style.Pattern = BackgroundType.Solid;
```

### Importálás fejlécek nélkül

Ha a downstream rendszer már saját fejléceket biztosít, csak add át `false`‑t az `importColumnNames` argumentumnak. Az adatok az `A1`‑től kezdődnek, és később saját fejléceket írhatsz.

```csharp
sheet.Cells.ImportDataTable(dataTable, false, 1, 0); // start at row 2 (index 1)
```

## Teljes működő példa (All

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}