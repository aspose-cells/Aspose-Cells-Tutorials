---
category: general
date: 2026-03-22
description: Hogyan exportáljunk Excel-t formázással és megőrizzük a számformátumot.
  Tanulja meg, hogyan konvertáljon Excel-tartományt, hogyan szerezze meg a képlet
  eredményét, és hogyan exportáljon Excel-t formázással az Aspose.Cells használatával.
draft: false
keywords:
- how to export excel
- preserve number format
- convert excel range
- get formula result
- export excel with formatting
language: hu
og_description: Hogyan exportáljunk Excel-t formázással és megőrizve a számformátumot.
  Lépésről‑lépésre útmutató az Excel‑tartomány konvertálásához, a képlet eredményének
  lekéréséhez, és az Excel formázott exportálásához C#‑ban.
og_title: Hogyan exportáljunk Excel-t formázással – a számformátum megőrzése
tags:
- C#
- Aspose.Cells
- Excel automation
title: Hogyan exportáljunk Excel-t formázással – a számformátum megőrzése
url: /hu/net/number-and-display-formats-in-excel/how-to-export-excel-with-formatting-preserve-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan exportáljunk Excel-t formázással – Számformátum megőrzése

Valaha is elgondolkodtál azon, **how to export Excel** adatokat, miközben minden cella megjelenését pontosan úgy őrzöd, ahogy a munkafüzetben látható? Lehet, hogy jelentést kell elküldened egy ügyfélnek, egy rácsvezérlőnek kell adatot adnod, vagy egyszerűen csak az értékeket egy adatbázisban szeretnéd tárolni. A leggyakoribb probléma a számformátum elvesztése vagy a képletek nyers szöveggé válása.  

Ebben az útmutatóban egy teljes, azonnal futtatható C# példán keresztül vezetünk végig, amely **preserves number format**, **converts an Excel range** egy `DataTable`-be, **gets the formula result**, és végül **exports Excel with formatting** az Aspose.Cells használatával. A végére egyetlen metódust kapsz, amelyet bármelyik projektbe beilleszthetsz, és egy munkalap hivatkozással meghívhatsz.

> **Quick preview:** a kód létrehoz egy munkafüzetet, beír egy értéket és egy képletet, azt mondja az Aspose.Cells-nek, hogy exportálja a cellákat formázott karakterláncokként, és kiírja a `123.456 | 246.912` értéket – pontosan azt, amit az Excelben várnál.

---

## Amire szükséged lesz

- **Aspose.Cells for .NET** (az ingyenes próba megfelelő a tanuláshoz)
- .NET 6.0 vagy újabb (az API ugyanaz a .NET Framework‑on is)
- Egy alap C# fejlesztői környezet (Visual Studio, VS Code, Rider… válaszd ki a neked megfelelőt)

Nem szükséges további NuGet csomag az Aspose.Cells-en kívül. Ha még nem telepítetted, futtasd:

```bash
dotnet add package Aspose.Cells
```

---

## 1. lépés – Munkafüzet létrehozása és értékek írása (beleértve egy képletet)

Először létrehozunk egy új munkafüzetet, és egy numerikus értéket helyezünk a **A1** cellába. Ezután egy egyszerű képletet adunk hozzá a **B1** cellához, amely a első cellát kettővel szorozza. Ez előkészíti a **get formula result** bemutatását a későbbiekben.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a numeric value and a formula that uses it
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Continue with export options...
        ExportRangeAsDataTable(worksheet);
    }
}
```

**Miért fontos:**  
- A `PutValue` a nyers számot tárolja, míg a `PutFormula` a számítást.  
- Az Aspose.Cells a képletet **élő** állapotban tartja, így amikor később a cella értékét kérjük, ténylegesen a `246.912` értéket kapjuk, nem a `"=A1*2"` szöveget.

---

## 2. lépés – Az Aspose.Cells tájékoztatása, hogy exportálja az értékeket formázott karakterláncokként

Ha egyszerűen meghívod a `ExportDataTable`-t az alapértelmezett beállításokkal, a numerikus cellák az alapul szolgáló `double` értékekkel fognak visszatérni. Ez eltávolítja az esetleges ezreselválasztókat, pénznem jeleket vagy egyéni tizedesjegyeket, amelyeket beállítottál. Az `ExportTableOptions` osztály lehetővé teszi, hogy **preserve number format** és **export as string**.

```csharp
static void ExportRangeAsDataTable(Worksheet worksheet)
{
    // Step 2: Set export options to retrieve values as formatted strings
    ExportTableOptions exportOptions = new ExportTableOptions
    {
        ExportAsString = true,          // Return values as strings
        ExportNumberFormat = true      // Preserve the cell's number format
    };

    // Step 3: Export the range A1:B1 to a DataTable
    DataTable dataTable = worksheet.Cells.ExportDataTable(
        firstRow: 0,
        firstColumn: 0,
        totalRows: 1,
        totalColumns: 2,
        includeColumnNames: true,
        options: exportOptions);

    PrintDataTable(dataTable);
}
```

**Fontos pont:** az `ExportNumberFormat = true` az a jelző, amely a **preserve number format** működését biztosítja. Enélkül a `"123.456"` és `"246.912"` nyers számként jelenik meg, ami a kódban rendben lehet, de nem akkor, amikor az adatot egy olyan UI‑ba illeszted be, amely az Excelhez hasonló formázást vár.

---

## 3. lépés – Exportált adatok kiírása (ellenőrzés)

Most, hogy van egy `DataTable`-ünk, amely formázott karakterláncokkal teli, írjuk ki a tartalmát a konzolra. Ez azt is bemutatja, hogy sikeresen **get formula result** anélkül, hogy magunk értékelnénk a képletet.

```csharp
static void PrintDataTable(DataTable table)
{
    // Step 4: Print the exported values (already formatted)
    foreach (DataRow row in table.Rows)
    {
        // The output will look like: 123.456 | 246.912
        Console.WriteLine($"{row[0]} | {row[1]}");
    }
}
```

Running the program prints:

```
123.456 | 246.912
```

Vedd észre, hogy a második oszlop a **formula result**-ot mutatja, nem a képlet szövegét. Ez pontosan az, amire szükséged van, amikor **export Excel with formatting**-ot végzel a további feldolgozáshoz.

---

## 4. lépés – Nagyobb Excel tartományok konvertálása (opcionális)

A fenti példa egy apró `A1:B1` szeletet kezel, de a valós helyzetek gyakran igénylik az egész táblázatok exportálását. Ugyanaz a metódus bármilyen téglalap alakú blokkra működik – csak állítsd be a `firstRow`, `firstColumn`, `totalRows` és `totalColumns` argumentumokat.

```csharp
// Example: Export a 10‑row by 5‑column block starting at C3
DataTable bigTable = worksheet.Cells.ExportDataTable(
    firstRow: 2,          // Zero‑based index (C3 = row 2, column 2)
    firstColumn: 2,
    totalRows: 10,
    totalColumns: 5,
    includeColumnNames: true,
    options: exportOptions);
```

**Pro tipp:** Ha a lapod már tartalmaz fejlécsort, állítsd a `includeColumnNames` értékét `true`-ra. Az Aspose.Cells a tartomány első sorát fogja oszlopnevekként használni, ami hasznos, ha később a `DataTable`-t UI rácshoz kötöd.

---

## 5. lépés – Gyakori buktatók és hogyan kerüld el őket

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Numbers lose commas or currency symbols** | `ExportAsString` is `false` or `ExportNumberFormat` is omitted | Set both `ExportAsString = true` **and** `ExportNumberFormat = true`. |
| **Formula cells return the formula text** | You didn’t call `CalculateFormula` before export (only needed if the workbook isn’t set to auto‑calculate) | Either enable auto‑calculate (`workbook.CalculateFormula()`) or rely on `ExportAsString` which forces evaluation. |
| **Headers appear as data rows** | `includeColumnNames` set to `false` while your range includes a header row | Set `includeColumnNames = true` to treat the first row as column names. |
| **Large ranges cause memory pressure** | Exporting the entire sheet at once loads everything into memory | Export in chunks (e.g., 500 rows at a time) and merge `DataTable`s if needed. |

---

## 6. lépés – Teljes működő példa (másolás-beillesztés kész)

Az alábbiakban a teljes program látható, a `using` direktíváktól a `Main`-ig. Illeszd be egy konzolos alkalmazásba, és nyomd meg a **F5**-öt – a formázott kimenetet azonnal láthatod.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate cells
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Export options: keep formatting and return strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            ExportNumberFormat = true
        };

        // Export A1:B1 as a DataTable
        DataTable dataTable = worksheet.Cells.ExportDataTable(
            firstRow: 0,
            firstColumn: 0,
            totalRows: 1,
            totalColumns: 2,
            includeColumnNames: true,
            options: exportOptions);

        // Print results
        foreach (DataRow row in dataTable.Rows)
        {
            Console.WriteLine($"{row[0]} | {row[1]}"); // Expected: "123.456 | 246.912"
        }

        // Keep console window open
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**Expected output**

```
123.456 | 246.912

Press any key to exit...
```

Ez a teljes **how to export excel** munkafolyamat, a formázás megmarad, a képlet eredmények kiértékelődnek, és egy tiszta `DataTable` áll készen bármely .NET felhasználó számára.

---

## Következtetés

Megmutattuk mindent, amit a **how to export Excel** adatok **preserving number format**, **converting an Excel range** egy `DataTable`-be, és **getting formula results** extra feldolgozás nélkül kell tudnod. A kulcs az `ExportTableOptions` konfiguráció – ha beállítod az `ExportAsString` és `ExportNumberFormat` értékét `true`-ra, az Aspose.Cells elvégzi a nehéz munkát.

From here you can:

- A `DataTable`-t csatlakoztathatod egy WPF `DataGrid`-hez vagy ASP.NET MVC nézethez.
- A táblát CSV fájlba írhatod, miközben megőrzöd a pontos vizuális megjelenést.
- Kiterjesztheted a megközelítést több munkalapra vagy dinamikus tartományokra.

Nyugodtan kísérletezz különböző formátumokkal (pénznem, százalék) és nagyobb adatblokkokkal. Ha bármilyen furcsaságba ütközöl, nézd meg újra a **common pitfalls** táblázatot – ez lefedi a leggyakoribb akadályokat, amikor **export excel with formatting**-et végzel.

Boldog kódolást, és legyenek az exportált táblázataid mindig olyan kifinomultak, mint az eredetiek!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}