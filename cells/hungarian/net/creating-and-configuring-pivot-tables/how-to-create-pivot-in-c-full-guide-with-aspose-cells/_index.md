---
category: general
date: 2026-03-27
description: Hogyan hozhatunk létre pivot táblát C#-ban az Aspose.Cells használatával
  – tanulja meg, hogyan adjon hozzá adatokat, engedélyezze a frissítést, és mentse
  a munkafüzetet xlsx formátumban egyetlen útmutatóban.
draft: false
keywords:
- how to create pivot
- save workbook as xlsx
- how to enable refresh
- how to add data
- generate excel file c#
language: hu
og_description: Hogyan készíts pivot táblát C#-ban az Aspose.Cells segítségével. Ez
  az útmutató megmutatja, hogyan adj hozzá adatokat, engedélyezd a frissítést, és
  mentsd a munkafüzetet xlsx formátumban.
og_title: Hogyan készítsünk pivot táblát C#-ban – Teljes Aspose.Cells útmutató
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hogyan készítsünk pivot táblát C#-ban – Teljes útmutató az Aspose.Cells használatával
url: /hu/net/creating-and-configuring-pivot-tables/how-to-create-pivot-in-c-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan hozzunk létre pivot táblát C#-ban – Teljes Aspose.Cells útmutató

Gondoltad már valaha, **hogyan hozzunk létre pivot táblát** C#-ban anélkül, hogy a COM interopbal küzdenél? Nem vagy egyedül. Sok adat‑vezérelt alkalmazásban gyors megoldásra van szükség, hogy a nyers értékesítési adatokat rendezett összefoglalóvá alakítsuk, és az Aspose.Cells ezt gyerekjátékra változtatja.  

Ebben az útmutatóban minden lépésen végigvezetünk: adat hozzáadása, pivot tábla felépítése, automatikus frissítés bekapcsolása, és végül **save workbook as xlsx**, hogy a felhasználóid azonnal megnyithassák Excelben. A végére egy kész `PivotRefresh.xlsx` fájlod lesz, és alapos megértést kapsz arról, hogy miért fontos minden sor.

## Előkövetelmények

- .NET 6+ (vagy .NET Framework 4.7.2 és újabb) – bármely friss futtatókörnyezet működik.
- Aspose.Cells for .NET – letöltheted a NuGet‑ből (`Install-Package Aspose.Cells`).
- Alapvető ismeretek a C# szintaxisról – mély Excel tudás nem szükséges.

> **Pro tipp:** Ha vállalati gépen dolgozol, győződj meg róla, hogy az Aspose licenc alkalmazva van; ellenkező esetben vízjel jelenik meg a generált fájlon.

## 1. lépés – Hogyan adjunk hozzá adatot egy új munkafüzethez

Mielőtt egy pivot létezhet, szükség van egy forrástáblára. Létrehozunk egy új munkafüzetet, az első munkalapnak *SalesData* nevet adunk, és néhány sort teszünk be, amelyek egy valós értékesítési adathalmazt imitálnak.

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and grab the default sheet
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        // 2️⃣ Write column headers
        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // 3️⃣ Insert a sample row – add more rows as your scenario demands
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);
```

**Miért fontos ez:**  
- `PutValue` használata automatikusan beállítja a cella típusát, így később nem kell aggódnod a szöveg‑ és szám típusú eltérések miatt.  
- Az 1. sorban lévő fejlécek definiálása biztosítja a pivot motor számára a hivatkozási pontot a mezők leképezésekor.

## 2. lépés – Hozz létre egy munkalapot, amely a pivot táblát fogja tartalmazni

A pivot tábla saját munkalapon él, így a forrásadatok tiszták maradnak, és a jelentés rendezett.

```csharp
        // 4️⃣ Add a dedicated sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");
```

> **Mi van, ha már van egy munkalap?** Csak hivatkozz rá index szerint (`workbook.Worksheets["MySheet"]`) egy új hozzáadása helyett.

## 3. lépés – Definiáld a forrás tartományt (Hogyan adj hozzá adatot → Tartomány definiálása)

Az Aspose.Cells-nek szüksége van egy `CellArea`‑ra vagy egy tartomány karakterláncra, amely magában foglalja a fejléceket és az adatokat is. Itt legfeljebb 100 sort feltételezünk; igény szerint módosítsd.

```csharp
        // 5️⃣ Build the source range (A1:D100 covers headers + up to 99 data rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");
```

**Szélsőséges eset:** Ha az adathalmaz dinamikus, kiszámíthatod az utolsó használt sort a `salesDataSheet.Cells.MaxDataRow` segítségével, és ennek megfelelően építheted fel a tartományt.

## 4. lépés – Hogyan hozzunk létre pivot táblát – A pivot tábla beszúrása

Most jön a szórakoztató rész: azt mondjuk az Aspose.Cells-nek, hogy hozzon létre egy pivotot, amely a most beállított tartományra hivatkozik.

```csharp
        // 6️⃣ Insert the pivot table at cell A3 of the pivot sheet
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];
```

Vedd észre a képlet‑stílusú hivatkozást (`=SalesData!A1:D100`). Ez ugyanaz a szintaxis, amit az Excelbe írnál, így az API intuitív.

## 5. lépés – Sor, oszlop és adatmezők konfigurálása (Hogyan adj hozzá adatot → Mezők)

*Region* mezőt sorokra, *Product* mezőt oszlopokra helyezzük, és összegezzük a *Units* és *Revenue* értékeket.

```csharp
        // 7️⃣ Set up row, column, and data fields
        pivotTable.RowFields.Add(0); // 0 = first column => Region
        pivotTable.ColumnFields.Add(1); // 1 = second column => Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);
```

**Miért ezek az indexek?**  
Az Aspose.Cells a oszlopokat 0‑tól indexeli, így a `0` a *Region* mezőre mutat. A `DataFields.Add` metódus lehetővé teszi a mező átnevezését (pl. „Sum of Units”) és egy aggregációs típus kiválasztását – a `Sum` a leggyakoribb numerikus adatoknál.

## 6. lépés – Hogyan engedélyezzük a frissítést – A pivot automatikus frissítése megnyitáskor

Ha a forrásadat később megváltozik, valószínűleg szeretnéd, hogy a pivot automatikusan tükrözze ezeket a változásokat. Itt jön képbe a `RefreshDataOnOpen`.

```csharp
        // 8️⃣ Turn on automatic refresh when the file is opened
        pivotTable.RefreshDataOnOpen = true;
```

**Megjegyzés:** Ez a jelző csak akkor működik, ha a munkafüzetet Excelben nyitják meg; Aspose.Cells‑ben nem számolja újra automatikusan, hacsak manuálisan nem hívod a `pivotTable.RefreshData()`‑t.

## 7. lépés – Munkafüzet mentése XLSX formátumban (Hogyan mentsük a munkafüzetet XLSX‑ként)

Végül a fájlt lemezre mentjük. A `.xlsx` formátum a modern, zip‑alapú Excel fájltípus, amely mindenhol működik.

```csharp
        // 9️⃣ Save the workbook – this also satisfies the “save workbook as xlsx” requirement
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

A program futtatása egy **PivotRefresh.xlsx** nevű fájlt hoz létre a végrehajtási mappában. Nyisd meg Excelben, és egy rendezett pivotot látsz *Region* sorokkal, *Product* oszlopokkal, valamint összegezett *Units* és *Revenue* értékekkel. Mivel engedélyeztük a frissítést, a *SalesData* munkalapon végzett bármilyen módosítás automatikusan frissíti a pivotot a következő megnyitáskor.

### Várt kimenet

| Region | Widget | Gadget | … |
|--------|--------|--------|---|
| East   | 120    | 0      |   |
| West   | 0      | 85     |   |
| **Grand Total** | **120** | **85** |   |

*​A számok a hozzáadott soroktól függően változhatnak.*

---

## Gyakori kérdések és variációk

### Mi van, ha több pivot táblára van szükségem?

Ismételheted a **4. lépést** más névvel és helyszínnel. A `PivotTables.Add` minden hívása egy új indexet ad vissza, amelyet a táblaobjektum lekérésére használhatsz.

### Hogyan változtassam az aggregációt *Átlag*‑ra a *Összeg* helyett?

Cseréld le a `PivotTableDataAggregationType.Sum`-t `PivotTableDataAggregationType.Average`-ra a `DataFields.Add` hívásokban.

### Stílusozhatom a pivotot (betűtípusok, színek)?

Igen. A pivot létrehozása után hozzáférhetsz a `Style` tulajdonságához, vagy cellaformázást alkalmazhatsz a pivotot tartalmazó tartományra. Például:

```csharp
pivotTable.Style = workbook.Styles[workbook.Styles.Add()];
pivotTable.Style.Font.Color = System.Drawing.Color.DarkBlue;
```

### Lehetőség van további sorok hozzáadására a munkafüzet mentése után?

Természetesen. Töltsd be a fájlt a `new Workbook("PivotRefresh.xlsx")` segítségével, adj hozzá sorokat a *SalesData* munkalaphoz, és a mentés előtt hívd meg a `pivotTable.RefreshData()`‑t.

---

## Teljes működő példa (másolás‑beillesztés kész)

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // Step 1: Create workbook & add sample data
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // Sample rows – extend as needed
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);

        salesDataSheet.Cells["A3"].PutValue("West");
        salesDataSheet.Cells["B3"].PutValue("Gadget");
        salesDataSheet.Cells["C3"].PutValue(85);
        salesDataSheet.Cells["D3"].PutValue(4250);

        // Step 2: Add sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");

        // Step 3: Define source range (covers up to 100 rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");

        // Step 4: Insert pivot table
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];

        // Step 5: Configure fields
        pivotTable.RowFields.Add(0); // Region
        pivotTable.ColumnFields.Add(1); // Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);

        // Step 6: Enable automatic refresh
        pivotTable.RefreshDataOnOpen = true;

        // Step 7: Save as .xlsx
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

Mentsd a fájlt, futtasd, és nyisd meg a generált **PivotRefresh.xlsx**‑t – most már elsajátítottad, **hogyan hozzunk létre pivot táblát** C#‑ban.

---

## Összegzés

Áttekintettük, hogyan lehet programozottan **pivot táblákat létrehozni**, hogyan **adatot hozzáadni**, hogyan **engedélyezni a frissítést**, és végül hogyan **menteni a munkafüzetet xlsx‑ként** az Aspose.Cells használatával. A kód

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}