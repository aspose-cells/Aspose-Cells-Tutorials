---
category: general
date: 2026-03-21
description: Exportálja az Excel adat táblázatot DataTable‑be fejlécekkel, korlátozza
  a tizedesjegyek számát, és exportálja az első 100 sort az Aspose.Cells használatával.
draft: false
keywords:
- export excel data table
- export excel to datatable
- limit decimal places excel
- export first 100 rows
- export excel with headers
language: hu
og_description: Tanulja meg, hogyan exportálja az Excel adat táblázatot DataTable-be,
  megtartva a fejléceket, korlátozva a tizedesjegyek számát, és lekérve az első 100
  sort C#-ban.
og_title: Excel adat táblázat exportálása C#-ban – Lépésről lépésre útmutató
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Excel adat táblázat exportálása C#-ban – Teljes útmutató
url: /hu/net/excel-data-export-retrieval/export-excel-data-table-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel Adattábla Exportálása – Teljes C# Bemutató

Szükséged van **excel adat tábla exportálására** egy munkafüzetből egy .NET `DataTable`-be? Jó helyen vagy—ez az útmutató pontosan megmutatja, hogyan teheted meg, hogyan tartsd meg az oszlopfejléceket, hogyan korlátozd a tizedesjegyek számát, és hogyan olvasd be csak az első 100 sort.  

Ha már valaha is a táblázatot bámultad, és azon tűnődtél, hogy „Hogyan juttassam be ezt az alkalmazásomba anélkül, hogy elveszíteném a formázást?”, nem vagy egyedül. A következő néhány percben ezt a „mi lenne, ha” gondolatot konkrét, másol‑beilleszthető megoldássá alakítjuk, amely az Aspose.Cells könyvtárral működik, egy népszerű Excel‑kezelő könyvtárral.

## Mit fogsz megtanulni

- Hogyan **exportálj excel-t datatable-be** a `ExportDataTable` metódus használatával.  
- Hogyan tartsd meg az eredeti oszlopneveket (`export excel with headers`).  
- Hogyan **korlátozd a tizedesjegyek számát excel** értékeknél az `ExportTableOptions` konfigurálásával.  
- Hogyan szerezd meg biztonságosan csak az első 100 sort (`export first 100 rows`).  

Nincsenek külső szkriptek, nincsenek varázslatos karakterláncok—csak egyszerű C#, amelyet bármely .NET projektbe beilleszthetsz.

## Előfeltételek

| Követelmény | Miért fontos |
|-------------|---------------|
| .NET 6 vagy újabb (vagy .NET Framework 4.7+) | Az Aspose.Cells mindkettőt támogatja, de az újabb futtatókörnyezetek aszinkron API-kat biztosítanak. |
| Aspose.Cells for .NET NuGet csomag | Biztosítja a `Workbook`, `ExportTableOptions` és a `ExportDataTable` segédfüggvényt. |
| Egy minta Excel fájl (pl. `Numbers.xlsx`) | Az exportálandó adatok forrása. |
| Alap C# ismeretek | Követni fogod a kódrészleteket, de semmi különleges tudás nem szükséges. |

Ha ezek bármelyike ismeretlennek tűnik, szerezd be a NuGet csomagot a `dotnet add package Aspose.Cells` paranccsal, és hozz létre egy kis Excel fájlt néhány számmal—ez lesz a tesztadatod.

![excel adat tábla exportálás példa](excel-data-table.png "Képernyőkép egy Excel munkalapról, amely DataTable-be lesz exportálva")

## 1. lépés: A munkafüzet betöltése (export excel data table)

Az első dolog, amire szükséged van, egy `Workbook` példány, amely a te Excel fájlodra mutat. Olyan, mintha egy könyvet nyitnál meg, mielőtt bármely fejezetet olvasnál.

```csharp
using Aspose.Cells;

// 1️⃣ Load the workbook that contains the source data
Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");
```

> **Miért fontos:** A munkafüzet betöltése hozzáférést biztosít a munkalapokhoz, cellákhoz és stílusokhoz. Ha a fájl útvonala hibás, az Aspose `FileNotFoundException`-t dob, ezért ellenőrizd a helyet.

## 2. lépés: Exportálási beállítások konfigurálása – limit decimal places excel

Alapértelmezés szerint az Aspose minden numerikus értéket teljes pontossággal exportál. Gyakran csak néhány jelentős számjegyre van szükség, különösen, ha az adatot UI‑rácsba vagy egy kerekített számokat elváró API‑ba szeretnéd betáplálni.

```csharp
using Aspose.Cells;

// 2️⃣ Configure export options – keep only 4 significant digits
ExportTableOptions exportOptions = new ExportTableOptions
{
    // This property trims the number of significant digits.
    SignificantDigits = 4
};
```

> **Pro tipp:** Ha más kerekítési stratégiára van szükséged (pl. mindig felfelé kerekítés), az export után post‑processzálhatod a `DataTable`‑t. A `SignificantDigits` beállítás a leggyorsabb módja a **limit decimal places excel** elérésének anélkül, hogy extra ciklusokat írnál.

## 3. lépés: A kívánt tartomány exportálása (export first 100 rows)

Most megmondjuk az Aspose‑nak, mely cellatartományt szeretnénk egy `DataTable`‑be átemelni. Ebben a bemutatóban az első 100 sort és az első 10 oszlopot vesszük, de a számokat a saját szituációdhoz igazíthatod.

```csharp
using System.Data;
using Aspose.Cells;

// 3️⃣ Export a block of cells (first 100 rows × 10 columns) to a DataTable
DataTable dataTable = workbook.Worksheets[0].Cells.ExportDataTable(
    startRow: 0,          // zero‑based index, first row
    startColumn: 0,       // first column (A)
    totalRows: 100,       // export only the first 100 rows
    totalColumns: 10,     // and the first 10 columns
    exportColumnNames: true, // keep column headers (export excel with headers)
    options: exportOptions);
```

> **Edge case:** Ha a munkalap kevesebb, mint 100 sort tartalmaz, az Aspose egyszerűen exportálja, ami létezik, hibát nem dobva. Azonban érdemes lehet védekezni egy váratlanul kis tartomány ellen:

```csharp
int rowsToExport = Math.Min(100, workbook.Worksheets[0].Cells.MaxDataRow + 1);
```

## 4. lépés: Az eredmény ellenőrzése – Gyors konzol kiíratás

Jó látni az adatokat a hibakeresőben, de néhány sor kiírása a konzolra megerősíti, hogy a **export excel to datatable** valóban működött, és a tizedesjegyek levágásra kerültek.

```csharp
static void PrintDataTable(DataTable table)
{
    foreach (DataRow row in table.Rows)
    {
        foreach (var item in row.ItemArray)
            Console.Write($"{item}\t");
        Console.WriteLine();
    }
}

// Call the helper
PrintDataTable(dataTable);
```

### Várható kimenet

```
ID      Name    Score   Ratio   Date        ...
1       Alice   95.12   0.8234  2023-01-15  ...
2       Bob     88.5    0.7612  2023-01-16  ...
3       Carol   73.33   0.6721  2023-01-17  ...
...
```

Vedd észre, hogy a numerikus oszlopok most már csak négy jelentős számjegyet mutatnak, ami megfelel a korábban alkalmazott `SignificantDigits = 4` beállításnak.

## 5. lépés: Összefoglalás – Teljes, futtatható példa

Az alábbi teljes programot másol‑beillesztheted egy konzolalkalmazásba. Tartalmaz hibakezelést, a opcionális sor‑szám védelmet, valamint egy segédmetódust a kiíratáshoz.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class ExportExcelDemo
{
    static void Main()
    {
        try
        {
            // 👉 Load the workbook
            Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");

            // 👉 Set up export options (limit decimal places excel)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                SignificantDigits = 4
            };

            // 👉 Determine safe row count (export first 100 rows)
            int maxRows = workbook.Worksheets[0].Cells.MaxDataRow + 1;
            int rowsToExport = Math.Min(100, maxRows);

            // 👉 Export to DataTable (export excel to datatable, export excel with headers)
            DataTable dt = workbook.Worksheets[0].Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: rowsToExport,
                totalColumns: 10,
                exportColumnNames: true,
                options: exportOptions);

            // 👉 Show a glimpse of the data
            PrintDataTable(dt);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }

    static void PrintDataTable(DataTable table)
    {
        foreach (DataRow row in table.Rows)
        {
            foreach (var item in row.ItemArray)
                Console.Write($"{item}\t");
            Console.WriteLine();
        }
    }
}
```

Futtasd a programot, és látni fogod a munkalap első 100 sorát, szépen kerekítve, az oszlopnevekkel változatlanul.

## Gyakori kérdések és buktatók

| Kérdés | Válasz |
|----------|--------|
| **Mi van, ha a munkalap egyesített cellákat tartalmaz?** | `ExportDataTable` egyesített cellákat laposít, a bal‑felső cella értékét veszi. Ha egyedi kezelést igényelsz, először bontsd fel az egyesítést, vagy olvasd a nyers `Cell` objektumokat. |
| **Exportálhatok egy `DataSet`‑be helyette?** | Igen—használd a `ExportDataTable`-t |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}