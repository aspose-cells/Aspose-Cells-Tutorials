---
title: Kategóriaadatok beállítása
linktitle: Kategóriaadatok beállítása
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan állíthat be kategóriaadatokat Excel-diagramokon az Aspose.Cells for .NET használatával. Kövesse lépésről lépésre bemutató oktatóanyagunkat az egyszerű megvalósítás érdekében.
weight: 15
url: /hu/net/advanced-chart-operations/setting-category-data/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kategóriaadatok beállítása

## Bevezetés

Ha az Excel-fájlok programozott kezeléséről és kezeléséről van szó, a megfelelő eszközök birtokában mindent megtehet. Az Aspose.Cells for .NET kiemelkedik ilyen eszközként, amely lehetővé teszi a fejlesztők számára az Excel-fájlok könnyű létrehozását, szerkesztését és konvertálását. Akár összetett adatelemző alkalmazást épít, akár egyszerűen csak automatizálnia kell a jelentéskészítést, az Aspose.Cells mindent megtesz. 

## Előfeltételek 

Mielőtt belemerülnénk a finom részletekbe, győződjünk meg arról, hogy mindennel megvan, amire szüksége van:

1. Fejlesztői környezet: Győződjön meg arról, hogy be van állítva .NET fejlesztői környezet. A Visual Studio ajánlott.
2.  Aspose.Cells for .NET Library: Töltse le a könyvtár legújabb verzióját a[Aspose.Cells letöltési oldal](https://releases.aspose.com/cells/net/).
3. A C# alapvető ismerete: A C# és Excel fogalmak ismerete segít a tartalom zökkenőmentesebb megértésében.
4.  Hozzáférés a dokumentációhoz: hozzáféréssel rendelkezik[Aspose.Cells Documentation](https://reference.aspose.com/cells/net/) további betekintést nyújthat, ha elakad. 

Ha minden a helyén van, lépésről lépésre feloldjuk az Excel-manipuláció varázsát.

## Csomagok importálása 

A kódolás megkezdése előtt döntő fontosságú a szükséges csomagok importálása. Ez lehetővé teszi számunkra, hogy hozzáférjünk az Aspose.Cells által biztosított funkciókhoz.

## 1. lépés: A névtér importálása

A kezdéshez importáljuk az Aspose.Cells névteret a C# fájlba.

```csharp
using System;
using System.IO;
using Aspose.Cells;
```

Ha felveszi ezt a sort a fájl tetejére, elérheti az Aspose.Cells könyvtár összes vonatkozó osztályát és metódusát.

Most, hogy ismerjük az előfeltételeket, és importáltuk a szükséges könyvtárat, nézzük meg, hogyan állíthatunk be kategóriaadatokat egy Excel diagramon.

## 2. lépés: Határozza meg a kimeneti könyvtárát

Először meg kell adnia, hogy az Excel fájl hova kerüljön mentésre. Hozzon létre egy változót a kimeneti könyvtárhoz. 

```csharp
string outputDir = "Your Output Directory";
```

 Cserélje ki`"Your Output Directory"` annak a helynek a tényleges elérési útjával, ahová menteni szeretné a kimeneti Excel-fájlt. Ez biztosítja, hogy pontosan tudja, hol találja meg a kész terméket!

## 3. lépés: Munkafüzet-objektum példányosítása

Ezután létrehozza a munkafüzet objektum új példányát. Ez az objektum az Excel-fájl tárolójaként szolgál.

```csharp
Workbook workbook = new Workbook();
```

## 4. lépés: Az első munkalap elérése

A munkafüzet első munkalapjával kell dolgoznia. A munkalap elérése olyan egyszerű, mint:

```csharp
Worksheet worksheet = workbook.Worksheets[0];
```

 Az index`0` mutat az első munkalapra. Az Excelben úgy képzelje el, mintha megnyitná a munkafüzet első lapját.

## 5. lépés: Mintaértékek hozzáadása a cellákhoz

Töltsünk ki néhány adatot a munkához. Az első két oszlophoz számértékeket is hozzáadhat. 

```csharp
worksheet.Cells["A1"].PutValue(10);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(170);
worksheet.Cells["A4"].PutValue(200);
worksheet.Cells["B1"].PutValue(120);
worksheet.Cells["B2"].PutValue(320);
worksheet.Cells["B3"].PutValue(50);
worksheet.Cells["B4"].PutValue(40);
```

Ebben a részletben az A1–A4 sorokat különböző számértékekkel töltjük fel, és a B1–B4 oszlopokat is kitöltjük. Ezek az adatok szolgálnak majd diagramunk alapjául.

## 6. lépés: Kategóriaadatok hozzáadása

Most címkézzük fel adatkategóriáinkat. Ez a harmadik oszlopban történik (C oszlop):

```csharp
worksheet.Cells["C1"].PutValue("Q1");
worksheet.Cells["C2"].PutValue("Q2");
worksheet.Cells["C3"].PutValue("Y1");
worksheet.Cells["C4"].PutValue("Y2");
```

Itt minden adatkészletet kategóriákkal jelölünk, például „Q1” és „Y1”, így könnyebben értelmezhető a diagramunk később.

## diagram létrehozása

Ha adataink a helyükön vannak, készen állunk egy diagram hozzáadására az adatok vizuális megjelenítésére.

## 7. lépés: Diagram hozzáadása a munkalaphoz

Most adjunk hozzá egy „Oszlop” típusú diagramot a munkalaphoz.

```csharp
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 15, 5);
```

Ez a sor egy új oszlopdiagramot hoz létre a munkalap 5. sorától és 0. oszlopától kezdve.

## 8. lépés: A diagrampéldány elérése

Mielőtt feltölthetnénk a diagramot adatokkal, el kell érnünk az újonnan létrehozott diagram példányát:

```csharp
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

Ezzel a lépéssel készen állunk arra, hogy adatsorainkat hozzáadjuk a diagramhoz.

## 9. lépés: Adatsorok hozzáadása a diagramhoz

Ezután hozzáadja a sorozatgyűjteményt, amely meghatározza a diagramon megjelenítendő adatokat. 

```csharp
chart.NSeries.Add("A1:B4", true);
```

Ez a sor azt határozza meg, hogy a diagramnak az A1–B4 tartományból kell adatokat vennie, lehetővé téve az értékek vizuális megjelenítését.

## 10. lépés: A kategóriaadatok beállítása

Itt jön a döntő rész – a kategóriaadataink meghatározása. Ez jelzi az adatpontjainkat az x tengelyen.

```csharp
chart.NSeries.CategoryData = "C1:C4";
```

Ennek a tartománynak a hozzárendelésével megmondjuk a diagramnak, hogy mely cellák felelnek meg adatsorunk kategóriáinak. E lépés nélkül a diagram csak számok halmaza lenne!

## 11. lépés: Az Excel fájl mentése

Ha minden be van állítva, itt az ideje, hogy megmentsük kemény munkánkat. 

```csharp
workbook.Save(outputDir + "outputSettingCategoryData.xlsx");
```

Ez a parancs a munkafüzetet a megadott kimeneti könyvtárba menti "outputSettingCategoryData.xlsx" néven. 

## 12. lépés: Megerősítő üzenet

Végül hozzáadhatunk egy kis visszajelzést, hogy megbizonyosodjunk arról, hogy minden zökkenőmentesen működött:

```csharp
Console.WriteLine("SettingCategoryData executed successfully.");
```

Ez egy üzenetet nyomtat a konzolon, amely jelzi, hogy a folyamat befejeződött. Egyszerű, igaz?

## Következtetés

És megvan! Sikeresen beállította a kategóriaadatokat egy Excel-munkafüzet diagramjához az Aspose.Cells for .NET segítségével. Ennek a megközelítésnek a szépsége abban rejlik, hogy lehetővé teszi az Excel-fájlok kezelésének automatizálását anélkül, hogy az Excel telepítve lenne a gépére. 

## GYIK

### Mi az Aspose.Cells?
Az Aspose.Cells egy .NET-könyvtár, amellyel az Excel-fájlokat Microsoft Excel nélkül kezelheti. Lehetővé teszi Excel-dokumentumok programozott létrehozását, szerkesztését és konvertálását.

### Használhatom ingyenesen az Aspose.Cells-t?
 Igen, ingyenesen kipróbálhatja az Aspose.Cells-t. Ingyenes próbaverziót kínálnak[itt](https://releases.aspose.com/).

### Az Aspose.Cells alkalmas nagy adatkészletekhez?
Teljesen! Az Aspose.Cells-t úgy tervezték, hogy hatékonyan kezelje a nagy adatkészleteket, így megbízható választás az adatintenzív alkalmazásokhoz.

### Hogyan adhatok hozzá diagramokat az Aspose.Cells használatával?
Diagramokat úgy adhat hozzá, hogy létrehoz egy új diagramobjektumot, és összekapcsolja az adatokat tartalmazó cellatartományokkal, amint az ebben az oktatóanyagban látható.

### Hol találhatok további példákat az Aspose.Cells használatára?
 További példákat és részletes dokumentációt találhat a webhelyen[Aspose.Cells Dokumentációs oldal](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
