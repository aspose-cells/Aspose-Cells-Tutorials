---
category: general
date: 2026-09-27
description: Tanulja meg, hogyan lehet sorokat törölni egy Excel táblázatból C#‑ban
  egy lépésről‑lépésre útmutatóval, amely bemutatja, hogyan lehet gyorsan betölteni
  egy Excel munkafüzetet C#‑ban.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from Excel table
- load Excel workbook C#
language: hu
lastmod: 2026-09-27
og_description: Sorok törlése Excel táblázatból C#‑ban egyértelmű példával. Ez az
  útmutató bemutatja, hogyan töltsünk be Excel munkafüzetet C#‑ban, és hogyan kezeljünk
  gyakori speciális eseteket.
og_image_alt: Screenshot illustrating delete rows from Excel table using C# code
og_title: Sorok törlése Excel táblázatból C#-ban – teljes kód útmutató
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  headline: How to delete rows from Excel table using C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  name: How to delete rows from Excel table using C#
  steps:
  - name: What if the table has a different name or position?
    text: '* **Named table:** Use `ws.ListObjects["MyTableName"]` instead of the index.
      * **Multiple tables:** Loop through `ws.ListObjects` and pick the one that matches
      a condition (e.g., column header names). * **Dynamic row count:** You can compute
      `rowCount` at runtime by inspecting `ws.ListObjects[0].Dat'
  - name: Edge‑case handling
    text: '| Situation | Recommended code change | |----------------------------------------|--------------------------------------------------------------|
      | Table is empty or has fewer rows | Check `ws.ListObjects[0].DataRange.RowCount`
      before deleting. | | Rows to delete exceed table size | Clamp `rowCount`'
  - name: How do I delete rows from **all** tables in a workbook?
    text: '```csharp foreach (Worksheet sheet in workbook.Worksheets) { foreach (ListObject
      tbl in sheet.ListObjects) { // Example: delete the first data row of each table
      if (tbl.DataRange.RowCount > 1) tbl.DeleteRows(1, 1); } } ```'
  - name: Can I delete rows based on a **cell value**?
    text: 'Yes. Scan the `DataRange` for matching cells, collect their zero‑based
      indices, then delete in descending order:'
  - name: What if I need to **preserve formatting**?
    text: '`DeleteRows` removes the entire row from the table but retains the table’s
      style for remaining rows. If you need to keep specific formatting on a row you’re
      deleting, copy the style to another row before deletion.'
  - name: Does this work with **.xls** (Excel 97‑2003) files?
    text: Yes. Aspose.Cells automatically detects the file format, so the same code
      works with `.xls`. Just change the file extension in the `Workbook` constructor.
  - name: Next steps
    text: '* Explore **ClosedXML** or **EPPlus** if you prefer a fully open‑source
      stack. * Combine row deletion with **data validation** to clean spreadsheets
      before importing into a database. * Automate the process for a folder of workbooks
      using `Directory.GetFiles` and a loop.'
  type: HowTo
tags:
- Excel
- C#
- .NET
title: Hogyan töröljünk sorokat egy Excel táblából C#-val
url: /hu/net/row-and-column-management/how-to-delete-rows-from-excel-table-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel táblázat sorainak törlése C#‑ban – teljes programozási útmutató

Ha **sorokat kell törölni egy Excel táblázatból** egy .xlsx fájlban, ez a tutorial pontosan megmutatja, hogyan teheted ezt C#‑ban. Egy tömör, futtatható példát láthatsz, amely betölti az Excel munkafüzetet, eltávolítja a megadott sorokat az első táblázatból, és elmenti az eredményt. A megközelítés a népszerű Aspose.Cells könyvtárral működik, és más .NET Excel API‑kra is adaptálható.

Sorok törlése egy táblázatból gyakori feladat importált adatok tisztításakor, jelentésrészletek rövidítésénél vagy a táblázatok frissítésének automatizálásakor. A útmutató végére képes leszel **Excel munkafüzet betöltésére C#‑ban**, egy táblázat (ListObject) megtalálására, tetszőleges sorok törlésére, és a módosított fájl visszaírására a lemezre.

## Előfeltételek

* .NET 6.0 vagy újabb telepítve (a kód .NET Framework 4.7+‑vel is működik).
* Hivatkozás a **Aspose.Cells** NuGet csomagra (vagy bármely kompatibilis könyvtárra, amely elérhetővé teszi a `Workbook`, `Worksheet` és `ListObject` típusokat).
* Egy `input.xlsx` nevű bemeneti fájl, amely a projektedből elérhető mappában van elhelyezve.
* Alapvető ismeretek a C# szintaxisról és a Visual Studio‑ról (vagy a kedvenc IDE‑dról).

> **Pro tipp:** Ha nyílt forráskódú alternatívát részesítesz előnyben, ugyanaz a logika alkalmazható a **ClosedXML**‑lel – csak cseréld le az Aspose‑specifikus osztályokat `XLWorkbook`, `IXLWorksheet` és `IXLTable`‑re.

## 1. lépés: Excel munkafüzet betöltése C#‑ban

Az első művelet a forrásfájl beolvasása a memóriába. A munkafüzet betöltése általában kevés erőforrást igényel a tipikus táblázatméretek esetén, és teljes hozzáférést biztosít a munkalapokhoz, táblázatokhoz és cellaértékekhez.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook
// Replace YOUR_DIRECTORY with the actual folder path, e.g. @"C:\Data"
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

*Miért fontos:* A `Workbook` feldolgozza a .xlsx fájl Open XML struktúráját, és `Worksheet` objektumok gyűjteményét teszi elérhetővé. Ha a fájl nem található, az Aspose `FileNotFoundException`‑t dob, ezért győződj meg arról, hogy az útvonal helyes.

## 2. lépés: Cél munkalap elérése

A legtöbb táblázat több munkalapot tartalmaz; ki kell választanod azt, amelyik a módosítani kívánt táblázatot tartalmazza. Itt az első munkalapot (`Worksheets[0]`) használjuk, ami egyszerű fájlok esetén biztonságos alapértelmezett.

```csharp
// Step 2: Access the first worksheet
Worksheet ws = workbook.Worksheets[0];
```

*Miért fontos:* A `Worksheet` a táblázatok (`ListObjects`) tárolója. A megfelelő munkalap elérése megakadályozza a véletlen módosításokat a nem kapcsolódó adatokon.

## 3. lépés: Sorok törlése egy Excel táblázatból

Az Excel táblázatokat `ListObject` objektumok képviselik. A munkalapon az első táblázat a `ListObjects[0]`. A `DeleteRows(startIndex, rowCount)` metódus a sorokat **a táblázat adatmezőjéhez viszonyítva** távolítja el, nem a munkalap abszolút sor számait.  

Ebben a példában a táblázat második és harmadik sorát töröljük (a fejléc a 0‑s sor, ezért az 1‑es indexnél kezdünk).

```csharp
// Step 3: Delete rows 1 and 2 from the first table (ListObject)
// The first row (index 0) is the header, so we start at index 1
ws.ListObjects[0].DeleteRows(1, 2);
```

### Mi a teendő, ha a táblázat más névvel vagy pozícióval rendelkezik?

* **Névtelt táblázat:** Használd a `ws.ListObjects["MyTableName"]`‑t az index helyett.
* **Több táblázat:** Iterálj a `ws.ListObjects`‑en, és válaszd ki azt, amelyik megfelel egy feltételnek (pl. oszlopfejléc nevek).
* **Dinamikus sor szám:** A `rowCount`‑t futásidőben kiszámíthatod a `ws.ListObjects[0].DataRange.RowCount` vizsgálatával.

### Szélsőséges esetek kezelése

| Helyzet                              | Ajánlott kómmódosítás                                      |
|--------------------------------------|------------------------------------------------------------|
| A táblázat üres vagy kevesebb sorral rendelkezik | Ellenőrizd a `ws.ListObjects[0].DataRange.RowCount` értékét a törlés előtt. |
| A törlendő sorok száma meghaladja a táblázat méretét | Korlátozd a `rowCount`‑t a `DataRange.RowCount - startIndex` értékre. |
| Sorok törlése feltétel alapján (pl. C oszlop értéke) | Iteráld a `DataRange.Rows`‑t, gyűjtsd össze a megfelelő indexeket, majd fordított sorrendben töröld őket, hogy az indexek stabilak maradjanak. |

## 4. lépés: Módosított munkafüzet mentése

A törlés után írd vissza a munkafüzetet egy új fájlba (vagy felülírhatod az eredetit, ha így szeretnéd). A mentés egy friss .xlsx‑et hoz létre, amely tükrözi a módosított táblázatot.

```csharp
// Step 4: Save the modified workbook
workbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

*Miért fontos:* A `Save` sorosítja a memóriában lévő reprezentációt a lemezre. Ha meg kell őrizned az eredeti fájlt, mindig egy másik útvonalra írd.

## Teljes, futtatható példa

Az összes lépés egyesítése egy önálló programot eredményez, amelyet másolhatsz, beilleszthetsz és futtathatsz.

```csharp
using System;
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Adjust the folder path as needed
        const string folder = @"YOUR_DIRECTORY";

        // Load the workbook (load Excel workbook C#)
        Workbook workbook = new Workbook($"{folder}\\input.xlsx");

        // Access the first worksheet
        Worksheet ws = workbook.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (ws.ListObjects.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Delete rows 1 and 2 from the first table (skip header)
        ListObject table = ws.ListObjects[0];
        int rowsToDelete = Math.Min(2, table.DataRange.RowCount - 1); // guard against short tables
        if (rowsToDelete > 0)
        {
            table.DeleteRows(1, rowsToDelete);
            Console.WriteLine($"Deleted {rowsToDelete} row(s) from table \"{table.Name}\".");
        }
        else
        {
            Console.WriteLine("Table does not have enough rows to delete.");
        }

        // Save the result
        workbook.Save($"{folder}\\output.xlsx");
        Console.WriteLine("Workbook saved as output.xlsx");
    }
}
```

**Várt kimenet** (konzol):

```
Deleted 2 row(s) from table "Table1".
Workbook saved as output.xlsx
```

Nyisd meg az `output.xlsx`‑t – az első táblázat már nem tartalmazza a törölt sorokat, míg a fejléc sor változatlan marad.

## Gyakori kérdések és változatok

### Hogyan törölhetek sorokat **minden** táblázatból egy munkafüzetben?

```csharp
foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (ListObject tbl in sheet.ListObjects)
    {
        // Example: delete the first data row of each table
        if (tbl.DataRange.RowCount > 1)
            tbl.DeleteRows(1, 1);
    }
}
```

### Törölhetek sorokat egy **cellaérték** alapján?

Igen. Vizsgáld át a `DataRange`‑t a megfelelő cellákért, gyűjtsd össze a nullához viszonyított indexeket, majd csökkenő sorrendben töröld őket:

```csharp
var rowsToRemove = new List<int>();
for (int i = 0; i < table.DataRange.RowCount; i++)
{
    var cell = table.DataRange[i, 2]; // column C (zero‑based)
    if (cell.StringValue == "Obsolete")
        rowsToRemove.Add(i);
}

// Delete rows from bottom to top to keep indices valid
rowsToRemove.Sort((a, b) => b.CompareTo(a));
foreach (int rowIdx in rowsToRemove)
    table.DeleteRows(rowIdx, 1);
```

### Mi a teendő, ha **formázást kell megőrizni**?

A `DeleteRows` eltávolítja a teljes sort a táblázatból, de a táblázat stílusát megtartja a maradék soroknál. Ha egy törölt sorra vonatkozó konkrét formázást meg kell őrizned, másold a stílust egy másik sorra a törlés előtt.

### Működik ez **.xls** (Excel 97‑2003) fájlokkal is?

Igen. Az Aspose.Cells automatikusan felismeri a fájlformátumot, így ugyanaz a kód működik `.xls` esetén is. Csak módosítsd a fájl kiterjesztését a `Workbook` konstruktorban.

## Teljesítmény tippek

* **Csoportos törlések:** Sok sor egyesével történő törlése lassabb lehet. Amikor csak lehetséges, használj egyetlen `DeleteRows(start, count)` hívást.
* **Kerüld a UI szál blokkolását:** Ha asztali alkalmazásba integrálod, futtasd a munkafüzet manipulációt egy háttérszálon, hogy a felhasználói felület reagálók maradjon.
* **Megfelelő erőforrás-felszabadítás:** Bár az Aspose.Cells kezelt memóriát használ, nagy fájlok esetén tedd a `Workbook`‑ot egy `using` blokkba, hogy a források gyorsan felszabaduljanak.

## Következtetés

Most már egy teljes, éles környezetben is használható példával rendelkezel, amely **sorokat töröl egy Excel táblázatból** C#‑ban. Az útmutató bemutatta, hogyan **tölts be egy Excel munkafüzetet C#‑ban**, hogyan találj meg egy `ListObject`‑et, hogyan távolíts el biztonságosan sorokat, és hogyan mentsd el a frissített fájlt. A szélsőséges esetek kezelése és a teljesítmény‑tanácsok segítségével ezt a mintát bonyolultabb szituációkra is adaptálhatod, például feltételes törlésekre, több táblázatra vagy alternatív .NET Excel könyvtárakra.

### Következő lépések

* Fedezd fel a **ClosedXML**‑t vagy az **EPPlus**‑t, ha teljesen nyílt forráskódú stacket szeretnél.
* Kombináld a sorok törlését **adatvalidációval**, hogy a táblázatokat tisztítsd adatbázisba importálás előtt.
* Automatizáld a folyamatot egy munkafüzetek mappájára a `Directory.GetFiles` és egy ciklus használatával.

Nyugodtan kísérletezz különböző sorintervallumokkal, táblázatnevekkel és feltételes logikával. Boldog kódolást!

## Mit érdemes legközelebb megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Excel fájl betöltése C# – Hogyan töröljünk sorokat és távolítsunk el konkrét sorokat](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)
- [Hogyan szúrjunk be és töröljünk sorokat Excelben az Aspose.Cells for .NET‑vel: Átfogó útmutató](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Hogyan töröljünk üres sorokat Excelben az Aspose.Cells .NET‑vel az adat tisztításához](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}