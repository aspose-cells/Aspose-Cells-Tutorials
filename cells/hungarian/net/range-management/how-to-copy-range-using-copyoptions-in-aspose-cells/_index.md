---
category: general
date: 2026-11-19
description: Tanulja meg, hogyan másolhat tartományt a CopyOptions segítségével az
  Aspose.Cells-ben, miközben megőrzi a formázást és a pivot táblákat, amikor formázott
  Excel‑tartományt másol.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range using copyoptions
- copy excel range with formatting
- Aspose.Cells copy range
- preserve pivot tables Aspose
- Excel automation C#
language: hu
lastmod: 2026-11-19
og_description: A CopyOptions használatával az Aspose.Cells-ben a tartomány másolása
  lehetővé teszi az Excel adatok teljes formázással és a pivot táblák megőrzésével
  történő duplikálását, megbízható munkafüzet-kezelést biztosítva.
og_image_alt: Screenshot of C# code that copies an Excel range using Aspose.Cells
  CopyOptions
og_title: Tartomány másolása CopyOptions használatával az Aspose.Cells-ben – lépésről
  lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  headline: How to copy range using CopyOptions in Aspose.Cells
  type: TechArticle
- description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  name: How to copy range using CopyOptions in Aspose.Cells
  steps:
  - name: Why `CopyOptions` matters
    text: '* **Performance** – The library performs a single internal operation rather
      than copying cells one‑by‑one. * **Accuracy** – All visual aspects (fonts, colors,
      borders) survive the move, which eliminates visual drift in generated reports.
      * **Reliability** – Pivot tables remain functional because the'
  - name: What if the destination area overlaps the source?
    text: 'Aspose.Cells throws an `ArgumentException`. To avoid this, calculate a
      destination that does not intersect the source, or copy to a different worksheet:'
  - name: How to copy between different workbooks?
    text: 'Create a second `Workbook` instance for the target file and use the same
      `CopyOptions` object:'
  - name: Does `CopyOptions` also copy merged cells?
    text: Yes. The `CopyStyle` flag includes merged‑cell information. If you need
      finer control, set `options.CopyMergedCells = true` (available in newer versions).
  - name: What about large ranges (thousands of rows)?
    text: The operation is memory‑efficient, but you may want to increase the `WorkbookSettings`
      `MemorySetting` to `MemorySetting.MemoryPreference` for very large files.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hogyan másolhatunk tartományt a CopyOptions segítségével az Aspose.Cells-ben
url: /hu/net/range-management/how-to-copy-range-using-copyoptions-in-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan másolhatunk tartományt a CopyOptions használatával az Aspose.Cells-ben

Ha **copy range using CopyOptions**-t szeretne használni az Aspose.Cells-ben, ez az útmutató pontosan megmutatja, hogyan másolhat meg egy cellatömböt, miközben minden formázás és beágyazott kimutatás érintetlen marad. Sok fejlesztőnek nehézségei vannak a stílus megőrzésével a munkalapok közötti adatmozgatás során, és a `CopyOptions` osztály megoldja ezt a problémát extra kézi lépések nélkül.

Ebben az oktatóanyagban megtanulja:

* Forrás- és célterületek meghatározása egy Excel munkafüzetben.  
* `CopyOptions` használata a cellaformázás, oszlopszélességek és kimutatások megőrzéséhez.  
* Az eredmény mentése egy új fájlba, amely készen áll a további feldolgozásra.

A példa bármely `.xlsx` fájllal működik, és csak az Aspose.Cells for .NET könyvtárra van szükség.

## Előkövetelmények

Mielőtt elkezdené, győződjön meg róla, hogy rendelkezik:

* Telepítve legyen a .NET 6.0 vagy újabb.  
* Érvényes Aspose.Cells for .NET licenc (vagy egy ingyenes értékelő kulcs).  
* Visual Studio 2022 vagy bármely kedvelt C# IDE.

A `Aspose.Cells`-en kívül nincs szükség további NuGet csomagokra.

## 1. lépés: A projekt beállítása és a névterek importálása

Hozzon létre egy új konzolos alkalmazást, és adja hozzá az Aspose.Cells hivatkozást:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Your code will go here
        }
    }
}
```

A `using Aspose.Cells;` direktíva hozzáférést biztosít a `Workbook`, `CellArea` és `CopyOptions` osztályokhoz.

## 2. lépés: A módosítandó munkafüzet betöltése

```csharp
// Step 2: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

`Workbook` az egész Excel fájlt képviseli. Cserélje le a `YOUR_DIRECTORY`-t arra a mappára, amely a forrásfájlt tartalmazza.

## 3. lépés: A forrás- és célterületek meghatározása

```csharp
// Step 3: Define the source range (A1:H30)
CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");

// Step 3b: Define the destination range (A35:H64)
CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");
```

`CellArea.CreateCellArea` egy téglalap alakú területet hoz létre a bal‑felső és jobb‑alsó cellacímek alapján. A koordinátákat úgy állíthatja be, hogy megfeleljenek a másolandó blokk méretének.

## 4. lépés: A tartomány másolása a formázás és a kimutatások megőrzésével

```csharp
// Step 4: Copy the range using CopyOptions
CopyOptions options = new CopyOptions
{
    // Preserve all cell styles, number formats, and column widths
    CopyStyle = true,
    // Keep formulas unchanged (they will still reference the original sheet)
    CopyFormula = true,
    // Preserve any pivot tables that intersect the copied area
    CopyPivotTables = true,
    // Retain data validation and conditional formatting
    CopyDataValidation = true,
    CopyConditionalFormatting = true
};

workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
```

A `CopyOptions` objektum pontosan megmondja az Aspose.Cells-nek, mit kell megtartani. A `CopyPivotTables = true` beállítása a kulcs a **copy range using CopyOptions**-hez, ha a forrás kimutatásokat tartalmaz. A többi jelző biztosítja, hogy a **copy excel range with formatting** automatikusan megvalósuljon – a másolás után nincs szükség extra kódra a stílusok újbóli alkalmazásához.

### Miért fontos a `CopyOptions`

* **Performance** – A könyvtár egyetlen belső műveletet hajt végre a cellák egy‑esével történő másolása helyett.  
* **Accuracy** – Minden vizuális elem (betűtípusok, színek, szegélyek) megmarad a áthelyezés során, ami kiküszöböli a generált jelentésekben jelentkező vizuális eltéréseket.  
* **Reliability** – A kimutatások működőképesek maradnak, mivel a gyorsítótáruk és forráshivatkozásaik megkettőződnek.

## 5. lépés: A módosított munkafüzet mentése

```csharp
// Step 5: Save the workbook with the copied range
workbook.Save("YOUR_DIRECTORY/output.xlsx");
Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
```

A `Save` hívása után az `output.xlsx` fájl az eredeti adatokat és a célhelyen megkettőzött blokkot tartalmazza, teljes formázással és kimutatásokkal.

## Teljes forráskód referenciaként

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // Define source and destination ranges
            CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");
            CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");

            // Configure copy options to preserve everything
            CopyOptions options = new CopyOptions
            {
                CopyStyle = true,
                CopyFormula = true,
                CopyPivotTables = true,
                CopyDataValidation = true,
                CopyConditionalFormatting = true
            };

            // Perform the copy operation
            workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);

            // Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");
            Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
        }
    }
}
```

A program futtatása a következőt írja ki:

```
Range copied successfully. Output saved to output.xlsx
```

Nyissa meg az `output.xlsx` fájlt Excelben – láthatja, hogy az A1:H30 blokk megkettőződött az A35:H64 helyen, minden cellaszín, szegély, számformátum és a kimutatások érintetlenek.

## Gyakori kérdések és szél‑esetek kezelése

### Mi van, ha a célterület átfedésben van a forrással?

Az Aspose.Cells `ArgumentException`-t dob. Ennek elkerülése érdekében számoljon ki egy olyan célterületet, amely nem metszi a forrást, vagy másoljon egy másik munkalapra:

```csharp
Worksheet destSheet = workbook.Worksheets.Add("CopySheet");
destSheet.Cells.CopyRange(sourceRange, CellArea.CreateCellArea("A1", "H30"), options);
```

### Hogyan másolhatunk különböző munkafüzetek között?

Hozzon létre egy második `Workbook` példányt a célfájlhoz, és használja ugyanazt a `CopyOptions` objektumot:

```csharp
Workbook target = new Workbook();
target.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
target.Save("target.xlsx");
```

### A `CopyOptions` másolja-e a egyesített cellákat is?

Igen. A `CopyStyle` jelző tartalmazza az egyesített cellák információját. Ha finomabb vezérlésre van szüksége, állítsa be a `options.CopyMergedCells = true` értéket (újabb verziókban elérhető).

### Mi a helyzet a nagy tartományokkal (több ezer sor)?

A művelet memóriahatékony, de nagyon nagy fájlok esetén érdemes lehet a `WorkbookSettings` `MemorySetting` értékét `MemorySetting.MemoryPreference`-re állítani.

## Profi tippek

* **Használja újra ugyanazt a `CopyOptions`** példányt több másolási művelethez – csökkenti az objektum‑allokáció terhelését.  
* **Érvényesítse a tartományokat** a másolás előtt: `if (!CellArea.IsValid(sourceRange) || !CellArea.IsValid(destinationRange))` segít időben felfedezni a gépelési hibákat.  
* **Kapcsolja ki a számítást** (`workbook.Settings.CalcMode = CalculationMode.Manual`) nagy adathalmazok másolása közben a folyamat felgyorsítása érdekében, majd a másolás után hívja meg a `workbook.CalculateFormula()`-t, ha friss eredményekre van szüksége.

## Következtetés

Most már tudja, hogyan **copy range using CopyOptions**-t használjon az Aspose.Cells-ben, teljes **copy excel range with formatting** elérésével, miközben megőrzi a kimutatásokat és egyéb fejlett funkciókat. Ez a megközelítés megszünteti a kézi stílusújraalkalmazást, és biztosítja, hogy az Excel automatizálása robusztus és karbantartható marad.

Az alábbi lépéseket érdemes megvizsgálni:

* Használja a `CopyOptions`-t teljes munkalapok megkettőzéséhez.  
* Kombinálja a másolási műveletet a `WorksheetCollection.AddCopy`-val sablon‑alapú jelentéskészítéshez.  
* Integrálja a kódot egy ASP.NET Core API-ba, hogy valós időben nyújtson Excel átalakításokat.

Nyugodtan kísérletezzen különböző forrás/cél koordinátákkal, és ossza meg eredményeit a megjegyzésekben!

## Mit érdemes még megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljesen működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeiben.

- [Excel Aspose Cells Dotnet Copy Range Data](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/french/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}