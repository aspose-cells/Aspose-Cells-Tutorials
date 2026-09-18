---
category: general
date: 2026-09-18
description: Készítsen PowerPointot Excelből az Aspose.Cells segítségével – másolja
  a kimutatásokat, exportálja a tartományokat, és néhány C# sorral mentse PPTX formátumban.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create powerpoint from excel
- how to copy pivot table
- copy range between workbooks
- how to export excel to pptx
- save workbook as pptx
language: hu
lastmod: 2026-09-18
og_description: Készítsen PowerPoint-ot Excelből gyorsan. Tanulja meg, hogyan másolhat
  pivot táblákat, exportálhat tartományokat, és mentheti a munkafüzetet PPTX formátumban
  az Aspose.Cells segítségével.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel data
og_title: PowerPoint létrehozása Excelből az Aspose.Cells segítségével – lépésről
  lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  headline: How to create PowerPoint from Excel using Aspose.Cells
  type: TechArticle
- description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  name: How to create PowerPoint from Excel using Aspose.Cells
  steps:
  - name: Load the source workbook and define the range
    text: You must load the workbook that holds the source data and the pivot table.
      Selecting a precise range ensures that only the needed cells are transferred,
      which keeps the resulting slide lightweight.
  - name: Prepare the destination workbook
    text: Aspose.Cells treats a PowerPoint slide as a workbook when you save it in
      PPTX format. Creating a fresh workbook gives you a clean canvas for the copied
      range.
  - name: Copy the range while preserving the pivot table
    text: The `CopyRange` method accepts a `PasteOptions` object. Setting `CopyPivotTables
      = true` tells Aspose.Cells to keep the pivot table structure intact, not just
      the rendered values.
  - name: Save the workbook as a PowerPoint file
    text: Finally, export the workbook to PPTX format. The `SaveFormat.Pptx` flag
      tells Aspose.Cells to write the worksheet as a PowerPoint slide.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel to PowerPoint
title: Hogyan hozhatunk létre PowerPoint prezentációt Excelből az Aspose.Cells használatával
url: /hu/net/converting-excel-files-to-other-formats/how-to-create-powerpoint-from-excel-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PowerPoint létrehozása Excelből az Aspose.Cells használatával

Ha PowerPointot kell létrehoznia Excelből, ez az útmutató egy tömör, vég‑től‑végig megoldást mutat be. Megmutatjuk, hogyan másolhat pivot táblát, exportálhat egy kiválasztott tartományt, és mentheti az eredményt PPTX fájlként néhány C# sorral.

Diavetítés közvetlen generálása a táblázat adataiból eltávolítja a manuális másolás‑beillesztés lépést, amely lelassítja a jelentéskészítési munkafolyamatokat. Az útmutató mindent lefed, amire szüksége van, a projekt beállításától a végső PPTX fájlig, és a legújabb Aspose.Cells for .NET‑tel működik.

## Előfeltételek

* **Aspose.Cells for .NET** (verzió 23.12 vagy újabb). Telepítse NuGet‑en keresztül: `Install-Package Aspose.Cells`.
* **.NET 6+** fejlesztői környezet (Visual Studio 2022 vagy VS Code működik).
* Egy Excel munkafüzet (`Source.xlsx`), amely tartalmazza a felhasználandó adatokat és a pivot táblát.
* Írási jogosultság a kimeneti mappához.

Nem szükséges további harmadik‑féltől származó könyvtár.

## PowerPoint létrehozása Excelből – lépésről‑lépésre

A folyamat négy logikai lépésből áll, amelyek közvetlenül a később bemutatott kódrészlethez kapcsolódnak.

### 1. lépés: Forrás munkafüzet betöltése és a tartomány meghatározása

Be kell töltenie azt a munkafüzetet, amely a forrás adatokat és a pivot táblát tartalmazza. Egy pontos tartomány kiválasztása biztosítja, hogy csak a szükséges cellák kerüljenek átvitelre, ezáltal a létrejövő dia könnyű marad.

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// Select the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that contains the pivot table and surrounding data
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");
```

**Miért fontos:**  
`CreateRange` egy `Range` objektumot hoz létre, amely egészben másolható. A tartomány `A1:G20`‑ra korlátozásával elkerülheti a nem kapcsolódó cellák átvitelét, ami egyébként felnyomhatná a PowerPoint fájl méretét.

### 2. lépés: Cél munkafüzet előkészítése

Az Aspose.Cells egy PowerPoint diát munkafüzettel kezeli, amikor PPTX formátumban menti. Egy új munkafüzet létrehozása tiszta vásznat biztosít a másolt tartomány számára.

```csharp
// Create a new empty workbook that will become the PowerPoint slide
Workbook destinationWorkbook = new Workbook();

// Use the first worksheet of the new workbook
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

**Tip:** Ha több diára van szüksége, további munkalapokat adhat hozzá, majd később mindegyiket külön PPTX fájlként mentheti.

### 3. lépés: Tartomány másolása a pivot tábla megőrzésével

A `CopyRange` metódus egy `PasteOptions` objektumot vár. A `CopyPivotTables = true` beállítás azt mondja az Aspose.Cells‑nek, hogy a pivot tábla szerkezetét érintetlenül tartsa, ne csak a megjelenített értékeket.

```csharp
// Copy the defined range, preserving the pivot table definition
destinationSheet.Cells.CopyRange(
    sourceRange,
    new PasteOptions { CopyPivotTables = true });
```

**Hogyan működik:**  
Amikor a `CopyPivotTables` igaz, a cél munkalap megkapja a forrás adatokat és a pivot gyorsítótárat is. Ez azt jelenti, hogy a pivot tábla teljesen funkcionális marad, és később frissíthető, ha a forrás adatok változnak.

### 4. lépés: Munkafüzet mentése PowerPoint fájlként

Végül exportálja a munkafüzetet PPTX formátumba. A `SaveFormat.Pptx` jelző azt mondja az Aspose.Cells‑nek, hogy a munkalapot PowerPoint diaként írja ki.

```csharp
// Save the destination workbook as a PowerPoint presentation
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);
```

**Eredmény:**  
A `CopyWithPivot.pptx` megnyílik a Microsoft PowerPointban (vagy bármely kompatibilis megjelenítőben) egyetlen diával, amely a másolt tartományt mutatja, beleértve egy élő pivot táblát, amellyel a PowerPointban is interakcióba léphet.

## Teljes futtatható példa

Az alábbiakban a teljes program látható, amelyet beilleszthet egy új konzolprojektbe, és azonnal futtathat.

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook and select the range containing the pivot table
            Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
            Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
            Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

            // 2️⃣ Create a fresh workbook that will become the PowerPoint slide
            Workbook destinationWorkbook = new Workbook();
            Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

            // 3️⃣ Copy the range, preserving the pivot table definition
            destinationSheet.Cells.CopyRange(
                sourceRange,
                new PasteOptions { CopyPivotTables = true });

            // 4️⃣ Export the workbook as a PPTX file
            destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);

            Console.WriteLine("PowerPoint file created successfully.");
        }
    }
}
```

**Várt kimenet:**  
A program futtatása kiírja, hogy „PowerPoint file created successfully.”, és létrehozza a `CopyWithPivot.pptx` nevű fájlt. A fájl PowerPointban történő megnyitása egyetlen diát mutat, ahol a másolt Excel tartomány pontosan úgy jelenik meg, mint a forrás munkalapon, egy aktív pivot táblával, amely a PowerPointon belül frissíthető.

## Gyakori variációk és szélhelyzetek

| Helyzet | Mit kell módosítani |
|-----------|----------------|
| **Több pivot tábla** | Definiáljon külön `Range` objektumokat minden táblához, és hívja meg a `CopyRange`‑t minden egyeshez, vagy másolja az egész munkalapot, ha ugyanazt az adatforrást használják. |
| **Nagy adathalmazok** | Növelje a tartományt (pl. `"A1:Z5000"`). Fontolja meg a `PasteOptions.CompressData = true` engedélyezését a PPTX méretének csökkentése érdekében. |
| **Különböző diák elrendezései** | PPTX‑ként mentés után nyissa meg a fájlt PowerPointban, és alkalmazzon egy egyedi elrendezést vagy témát; az adatok szerkeszthetőek maradnak. |
| **Mentés streambe** | Használja a `destinationWorkbook.Save(stream, SaveFormat.Pptx)`‑t, ha a PPTX‑et web‑API‑n keresztül kell visszaadni. |
| **Cellák formázásának megőrzése** | Állítsa be a `PasteOptions.PasteType = PasteType.All`‑t a betűtípusok, színek és szegélyek megtartásához. |

**Pro tip:** Mindig ellenőrizze, hogy a célmappa létezik‑e, mielőtt meghívná a `Save`‑et. Ha a mappa hiányzik, a `Save` `DirectoryNotFoundException`‑t dob.

## Következtetés

Most már tudja, hogyan hozhat létre PowerPointot Excelből, másolhat pivot táblát, és exportálhatja az eredményt PPTX fájlként az Aspose.Cells segítségével. A lépések – a forrás munkafüzet betöltése, a tartomány meghatározása, a `CopyPivotTables`‑szel másolás és a PPTX‑ként mentés – lefedik az egész munkafolyamatot megbízható, termelés‑kész módon.

Ezután fedezze fel, **hogyan exportáljunk Excel‑t PPTX‑be** több munkalap esetén, vagy tanulja meg, **hogyan másoljunk tartományt munkafüzetek között**, amikor több forrásból kell adatot egyesíteni a diavetítés generálása előtt. Mindkét téma ugyanazon API‑felületre épül, és kombinálható a komplex jelentéskészítési folyamatok automatizálásához.

Boldog kódolást, és élvezze, ahogy a táblázatai kifinomult prezentációkká válnak!

## Mit érdemes legközelebb megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [Hogyan másoljuk a pivot táblát C#‑ban – Excel konvertálása PPTX‑be, tartomány másolása és szövegdoboz létrehozása](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Új munkafüzet létrehozása – Hogyan másoljunk munkalapot pivot táblával](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Hogyan hozzunk létre és mentsünk Excel fájlokat az Aspose.Cells for .NET‑tel: Teljes útmutató](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}