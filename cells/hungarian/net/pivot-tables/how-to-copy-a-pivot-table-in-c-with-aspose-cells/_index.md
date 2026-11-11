---
category: general
date: 2026-09-27
description: Tanulja meg, hogyan másolhat pivot táblát C#-ban az Aspose.Cells használatával.
  Tartalmazza a sorok formázással való másolását, a pivot tábla másik lapra való másolását,
  valamint a pivot tábla új munkafüzetbe való exportálását.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy rows with formatting
- copy pivot table to another sheet
- how to copy excel rows
- export pivot table to new workbook
language: hu
lastmod: 2026-09-27
og_description: Hogyan másoljon pivot táblát C#-ban az Aspose.Cells használatával.
  Kövesse a lépésről‑lépésre útmutatót a formázott sorok másolásához, a pivot tábla
  egy másik munkalapra történő áthelyezéséhez, és az új munkafüzetbe való exportáláshoz.
og_image_alt: Excel sheet showing a copied pivot table after using Aspose.Cells
og_title: Hogyan másoljunk pivot táblát C#-ban – teljes Aspose.Cells útmutató
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to copy a pivot table in C# using Aspose.Cells. Includes
    copy rows with formatting, copy pivot table to another sheet, and export pivot
    table to a new workbook.
  headline: How to copy a pivot table in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot table
title: Hogyan másolhatunk pivot táblát C#-ban az Aspose.Cells segítségével
url: /hu/net/pivot-tables/how-to-copy-a-pivot-table-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan másoljon pivot táblát C#-ban az Aspose.Cells segítségével

Ha **pivot táblát kell másolnia** egy munkalapról a másikra, a **pivot tábla másolása** C#-ban az Aspose.Cells használatával órákat takaríthat meg a kézi munkával szemben. A megközelítés lehetővé teszi a **sorok formázással való másolását**, a pivot gyorsítótár érintetlenül hagyását, és akár a **pivot tábla exportálását egy új munkafüzetbe**, ha önálló fájlra van szüksége.

Ez a bemutató végigvezeti a teljes munkafolyamatot:

* munkafüzet létrehozása,  
* a pivot‑tábla tartomány másolása a formázás megőrzésével,  
* a másolt adatok elhelyezése egy új lapon, és  
* az eredmény mentése külön fájlként.

Meg fogja látni, miért a beépített `CopyRows` metódus a legmegbízhatóbb mód a **pivot tábla másolására egy másik lapra**, és tippeket kap a speciális esetek kezelésére, például rejtett sorok vagy külső adatforrások esetén.

## Előfeltételek

Mielőtt elkezdené, győződjön meg róla, hogy rendelkezik a következőkkel:

| Követelmény | Miért fontos |
|-------------|----------------|
| .NET 6.0 vagy újabb | Az Aspose.Cells a .NET 6+ verziókat támogatja, és a legjobb teljesítményt nyújtja. |
| Visual Studio 2022 (vagy bármely C# IDE) | Szüksége van egy szerkesztőre, amely képes visszaállítani a NuGet csomagokat. |
| Aspose.Cells for .NET (NuGet csomag `Aspose.Cells`) | Ez a könyvtár biztosítja a példában használt `CopyRows` API-t. |
| Egy forrás Excel fájl (`source.xlsx`), amely pivot táblát tartalmaz a `A1:G20` tartományban | A kód ezt a konkrét tartományt másolja; ha a pivot táblája nagyobb, módosítsa a tartományt. |

Telepítse a könyvtárat a NuGet CLI vagy a Package Manager Console segítségével:

```bash
dotnet add package Aspose.Cells
```

## 1. lépés: Töltsük be a pivot táblát tartalmazó munkafüzetet

Az első sor egy `Workbook` objektumot hoz létre, amely az egész Excel fájlt képviseli. A fájl egyszeri betöltése olvasási/írási hozzáférést biztosít minden munkalaphoz.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Miért fontos ez a lépés** – A munkafüzet betöltése nélkül a későbbi `CopyRows` hívások nem tudnak hivatkozni a forrás adatokra vagy a pivot gyorsítótárra.

## 2. lépés: Készítsük elő a forrás és a cél munkalapokat

Szüksége lesz egy cél lapra, ahol a másolt pivot tábla megjelenik. Az alábbi kód lekéri az első munkalapot (ahol az eredeti pivot tábla található) és hozzáad egy új lapot **Copy** néven.

```csharp
// Get the source worksheet (index 0 = first sheet)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a new worksheet that will receive the copied rows
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
```

> **Pro tipp:** Ha a cél lap már létezik, először hívja meg a `Worksheets.RemoveAt(index)` metódust, hogy elkerülje a duplikált neveket.

## 3. lépés: Határozzuk meg a pivot táblát körülvevő cellatartományt

Egy `CellArea` objektum leírja a mozgatni kívánt tartomány bal‑felső és jobb‑alsó celláit. Ebben a példában a pivot tábla a `A1:G20` tartományt foglalja el. Nagyobb táblák esetén állítsa be a koordinátákat.

```csharp
// Define the range that includes the pivot table (A1:G20)
CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");
```

## 4. lépés: Sorok másolása formázással és a pivot gyorsítótár megőrzése

A `CopyRows` metódus **sorokat** másol a forrás lapról a cél lapra. A `CopyOptions.CopyAll` megadásával biztosítja, hogy az értékek, formázás, diagramok és beágyazott objektumok – amelyek mind a pivot tábla részei – átkerülnek.

```csharp
// Copy the rows from the source area to the destination sheet
sourceSheet.CopyRows(
    sourceArea.StartRow,          // start row in the source sheet
    destinationSheet,            // target worksheet
    0,                            // start row in the destination sheet
    sourceArea.RowCount,          // number of rows to copy
    CopyOptions.CopyAll);        // copy everything (values, formats, objects, etc.)
```

### Miért működik a `CopyRows` jobban, mint a `Copy` pivot tábláknál

* A `CopyRows` tiszteletben tartja a belső pivot gyorsítótárat, így a másolt pivot tábla továbbra is működőképes marad.
* Pontosan úgy **másolja a sorokat formázással**, ahogy azok az eredeti lapon szerepelnek.
* Egy egyszerű `Copy` tartomány helyett a rejtett sorokat és a hozzájuk tartozó szeletelőket is áthelyezi.

## 5. lépés: A munkafüzet mentése a másolt pivot táblával

Végül írjuk a módosított munkafüzetet a lemezre. Az új fájl az eredeti lapot és egy **Copy** lapot tartalmaz, amely a teljesen működőképes másolatot hordozza az eredeti pivot tábláról.

```csharp
// Save the workbook to a new file
workbook.Save(@"YOUR_DIRECTORY\pivot_copied.xlsx");
```

### Várt eredmény

Amikor megnyitja a `pivot_copied.xlsx` fájlt:

* A **Sheet1** lapon továbbra is megtalálható az eredeti adat és pivot tábla.
* A **Copy** lapon egy azonos pivot tábla látható ugyanazzal a elrendezéssel, szűrőkkel és formázással.
* Minden képlet és adatkapcsolat érintetlen, mivel a pivot gyorsítótár a sorokkal együtt lett másolva.

## Hogyan másoljuk a pivot táblát egy másik lapra ugyanabban a munkafüzetben

Ha csak egy már létező másik lapon (például „Report”) szeretné a pivot táblát, cserélje le a cél lap létrehozásának lépését a cél lapra mutató hivatkozásra:

```csharp
Worksheet destinationSheet = workbook.Worksheets["Report"]; // existing sheet
sourceSheet.CopyRows(sourceArea.StartRow, destinationSheet, 0,
                     sourceArea.RowCount, CopyOptions.CopyAll);
```

Ez a kódrészlet bemutatja a **pivot tábla másolását egy másik lapra** anélkül, hogy új munkalapot hozna létre.

## Pivot tábla exportálása új munkafüzetbe

Néha a pivot táblát teljesen külön fájlba szeretné helyezni. A másolási művelet után eltávolíthatja az összes munkalapot, kivéve azt, amelyik a másolt pivot táblát tartalmazza, majd mentheti:

```csharp
// Keep only the copied sheet
for (int i = workbook.Worksheets.Count - 1; i >= 0; i--)
{
    if (workbook.Worksheets[i].Name != "Copy")
        workbook.Worksheets.RemoveAt(i);
}

// Save as a new workbook containing only the pivot table
workbook.Save(@"YOUR_DIRECTORY\pivot_only.xlsx");
```

Most a `pivot_only.xlsx` egyetlen lappal rendelkezik, amely a duplikált pivot táblát tartalmazza, ezzel teljesítve a **pivot tábla exportálása új munkafüzetbe** követelményt.

## Hogyan másoljon Excel sorokat formázás elvesztése nélkül

Ugyanez a `CopyRows` hívás bármely tartományra működik, nem csak pivot táblákra. Ha **Excel sorokat** kell másolnia, amelyek feltételes formázást, adatérvényesítést vagy egyesített cellákat tartalmaznak, használja ugyanazt a metódust:

```csharp
// Example: copy rows 30‑40 from Sheet1 to Sheet2
sourceSheet.CopyRows(29, // zero‑based index for row 30
                     workbook.Worksheets["Sheet2"],
                     0,
                     11, // rows 30‑40 = 11 rows
                     CopyOptions.CopyAll);
```

Mivel a `CopyOptions.CopyAll` mindent átvitel, a cél sorok pontosan úgy fognak kinézni, mint a forrás sorok.

## Gyakori hibák és elkerülésük módjai

| Hiba | Tünet | Megoldás |
|------|-------|----------|
| A forrás tartomány nem fedi le a teljes pivot táblát | A másolt pivot tábla csonkoltnak tűnik. | Ellenőrizze, hogy a `CellArea` lefedi a pivot tábla összes sorát/oszlopát. |
| A cél lap már tartalmaz adatot | A felülírt sorok adatvesztést okoznak. | Válasszon egy üres lapot, vagy kezdje a másolást egy magasabb sor indexnél. |
| A pivot tábla külső adatforrást használ | A másolat elveszíti a kapcsolatot. | Másolás után hívja meg a `pivotTable.RefreshData()` metódust a kapcsolat helyreállításához. |
| Rejtett sorok kimaradnak | Néhány sor nem jelenik meg a másolatban. | A `CopyRows` automatikusan másolja a rejtett sorokat; ügyeljen arra, hogy ne használja a `CopyOptions.CopyValuesOnly` beállítást. |

## Teljes, futtatható példa

Az alábbi önálló programot beillesztheti egy új konzolos projektbe. Bemutatja a fent tárgyalt minden lépést.

```csharp
using System;
using Aspose.Cells;

namespace PivotTableCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains the pivot table
            string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2️⃣ Get source and destination worksheets
            Worksheet sourceSheet = workbook.Worksheets[0]; // first sheet
            Worksheet destinationSheet = workbook.Worksheets.Add("Copy");

            // 3️⃣ Define the cell area that holds the pivot table (A1:G20)
            CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");

            // 4️⃣ Copy rows with formatting and keep the pivot cache
            sourceSheet.CopyRows(
                sourceArea.StartRow,      // start row index (0‑based)
                destinationSheet,        // target sheet
                0,                        // start row in destination
                sourceArea.RowCount,      // number of rows to copy
                CopyOptions.CopyAll);    // copy everything

            // 5️⃣ Save the workbook with the copied pivot table
            string destPath = @"YOUR_DIRECTORY\pivot_copied.xlsx";
            workbook.Save(destPath);

            Console.WriteLine("Pivot table copied successfully to " + destPath);
        }
    }
}
```

**A program futtatása** létrehozza a `pivot_copied.xlsx` fájlt, amely egy új **Copy** nevű lapon tartalmazza az eredeti pivot tábla másolatát.

## Összegzés

Most már tudja, **hogyan másoljon pivot táblát** C#-ban az Aspose.Cells használatával.


## Mit érdemes még tanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy Pivot Table in C# – Complete Step‑by‑Step Guide](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [How to copy range with pivot tables in C# – Complete Guide](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}