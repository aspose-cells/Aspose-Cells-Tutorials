---
title: Új kimutatástábla létrehozása programozottan a .NET-ben
linktitle: Új kimutatástábla létrehozása programozottan a .NET-ben
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan lehet programozottan pivot táblát létrehozni .NET-ben az Aspose.Cells használatával lépésről lépésre. Hatékonyan elemezze adatait.
weight: 13
url: /hu/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Új kimutatástábla létrehozása programozottan a .NET-ben

## Bevezetés
A pivot tábla létrehozása megfélemlítő feladatnak tűnhet, különösen, ha programozottan csinálja. De ne félj! Az Aspose.Cells for .NET segítségével a pivot tábla összeállítása nem csak egyszerű, hanem az adatelemzés szempontjából is meglehetősen hatékony. Ebben az oktatóanyagban lépésről lépésre bemutatjuk, hogyan hozhat létre új pivot táblát egy .NET-alkalmazásban. Akár értékesítési, sport- vagy bármilyen más üzleti mutató adatait ad hozzá, ez az útmutató segít abban, hogy pillanatok alatt üzembe helyezze a kimutatási táblázatokat.

## Előfeltételek
Mielőtt belemerülne, győződjön meg róla, hogy minden készen áll az útra. A következőket kell tennie:

1. A .NET-keretrendszer telepítése: Győződjön meg arról, hogy a .NET-keretrendszer telepítve van a számítógépen. Az Aspose.Cells különféle verziókat támogat, de a legjobb, ha ragaszkodunk a legújabbhoz.
2.  Aspose.Cells Library: rendelkeznie kell az Aspose.Cells könyvtárral. Tudod[töltse le itt](https://releases.aspose.com/cells/net/)vagy kap a[ideiglenes engedély](https://purchase.aspose.com/temporary-license/) értékeléshez.
3. IDE beállítása: Készítsen egy C#-kompatibilis IDE-t, például a Visual Studio-t, ahol új projektet indíthat.
4. Alapvető C# ismeretek: A C# programozás ismerete segít abban, hogy haladjon anélkül, hogy túlságosan elakadna.

Minden készen áll? Nagy! Térjünk át a szükséges csomagok importálására.

## Csomagok importálása
Először is importálnia kell a szükséges névtereket a C# projektbe. Nyissa meg a C# fájlt, és direktívák segítségével adja hozzá a következőket:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Ezek a névterek hozzáférést biztosítanak az oktatóanyagban használt munkafüzetek, munkalapok és kimutatástábla funkciókhoz.

## 1. lépés: Hozzon létre egy munkafüzet-objektumot
A munkafüzet készítése az utazás kezdete. Kezdjük egy új munkafüzet példányosításával, és nyissa meg az első munkalapot.

```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
// Munkafüzet objektum példányosítása
Workbook workbook = new Workbook();

// Az újonnan hozzáadott munkalap hivatkozásának beszerzése
Worksheet sheet = workbook.Worksheets[0];
```

 Ebben a lépésben létrehozzuk a`Workbook`példányt, amely az Excel fájlunkat képviseli, és megragadja a legelső munkalapot, amely a pivot tábla játszóterévé válik.

## 2. lépés: Szúrjon be adatokat a cellákba
Ezután töltsük fel a munkalapunkat néhány mintaadattal. Sorokat fogunk bevinni a különböző sportágak, negyedévek és értékesítési adatokhoz, hogy összefoglaljuk a pivot táblázatunkat.

```csharp
Cells cells = sheet.Cells;

// A cellák értékének beállítása
Cell cell = cells["A1"];
cell.PutValue("Sport");
cell = cells["B1"];
cell.PutValue("Quarter");
cell = cells["C1"];
cell.PutValue("Sales");

// Adatcella kitöltése = cellák["A2"];
cell.PutValue("Golf");
// ... További adatbevitelek
```

Itt meghatározzuk az oszlopfejléceinket, és az egyes fejlécek alá értékeket szúrunk be. Ezek az adatok szolgálnak majd a kimutatástáblánk forrásaként, ezért ügyeljen a rendszerezettségre! Kövesse ezt a blokkot, és létrehoz egy átfogó adatkészletet.

## 3. lépés: Pivot tábla hozzáadása
Ha készen állnak az adataink, ideje elkészíteni a kimutatástáblát. Az új pivot tábla hozzáadásához a munkalap pivot table gyűjteményét fogjuk használni.

```csharp
Aspose.Cells.Pivot.PivotTableCollection pivotTables = sheet.PivotTables;

// PivotTable hozzáadása a munkalaphoz
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```

Ebben a részletben hozzáadunk egy pivot táblát a munkalaphoz, amely hivatkozik az adattartományunkra (ebben az esetben az A1-C8 cellákra). Elhelyezzük a pivot táblát az E3 cellától kezdve, és elnevezzük "PivotTable2"-nek. Elég egyszerű, igaz?

## 4. lépés: A Pivot Table testreszabása
Most, hogy megvan a kimutatástáblázatunk, szabjuk személyre, hogy értelmes összefoglalókat jelenítsen meg. Szabályozhatjuk, hogy mi jelenjen meg a pivot tábla soraiban, oszlopaiban és adatterületein.

```csharp
// Az újonnan hozzáadott kimutatáspéldány elérése
Aspose.Cells.Pivot.PivotTable pivotTable = pivotTables[index];

// A sorok végösszegei nem jelennek meg.
pivotTable.RowGrand = false;

// Az első mező húzása a sorterületre.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Row, 0);

// A második mező húzása az oszlopterületre.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Column, 1);

// A harmadik mező húzása az adatterületre.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Data, 2);
```

Ebben a lépésben azt mondjuk a pivot táblának, hogy rejtse el a sorok végösszegét, majd adja meg, hogy mely mezők kerüljenek a sorba, oszlopba és adatterületre. A sportágak nevei töltik ki a sorokat, a negyedévek az oszlopokat, az eladási adatok pedig az összefoglalókat.

## 5. lépés: Mentse el a munkafüzetet
Végül el akarjuk menteni az újonnan készített munkafüzetünket, hogy lássuk munkánk gyümölcsét.

```csharp
// Az Excel fájl mentése
workbook.Save(dataDir + "pivotTable_test_out.xls");
```

Csak adja meg a megfelelő elérési utat, és a kimutatástáblázat kimenetét egy Excel-fájlba menti, amelyet megnyithat és áttekinthet.

## Következtetés
A pivot táblák programozott létrehozása az Aspose.Cells for .NET használatával jelentősen időt takaríthat meg, különösen nagy adatkészletek kezelésekor. Megtanulta a projekt beállítását, a szükséges csomagok importálását, az adatok feltöltését és a testreszabható pivot tábla létrehozását a semmiből. Tehát, amikor legközelebb belefullad a számokba, emlékezzen erre az oktatóanyagra, és hagyja, hogy az Aspose.Cells elvégezze helyette a nehézségeket.

## GYIK
### Mi az Aspose.Cells?
Az Aspose.Cells egy hatékony .NET-könyvtár Excel-táblázatok programozott létrehozásához és kezeléséhez.

### Létezik ingyenes próbaverzió az Aspose.Cells számára?
 Igen, ingyenes próbaverziót kaphat[itt](https://releases.aspose.com/).

### Testreszabhatom a pivot tábla megjelenését?
Teljesen! Igényei szerint testreszabhatja a pivot tábla formázását, elrendezését és akár stílusait is.

### Hol találok további példákat és dokumentációt az Aspose.Cells webhelyen?
 Ellenőrizheti a[dokumentáció](https://reference.aspose.com/cells/net/) átfogó útmutatókért és példákért.

### Hogyan kaphatok támogatást az Aspose.Cells-hez?
 A támogatást a[Aspose fórum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
