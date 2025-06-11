---
"description": "Tanuld meg, hogyan hozhatsz létre pivot táblát programozottan .NET-ben az Aspose.Cells segítségével lépésről lépésre bemutató útmutatónkkal. Elemezd hatékonyan az adataidat."
"linktitle": "Új pivot tábla létrehozása programozottan .NET-ben"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Új pivot tábla létrehozása programozottan .NET-ben"
"url": "/hu/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Új pivot tábla létrehozása programozottan .NET-ben

## Bevezetés
Egy pivot tábla létrehozása ijesztő feladatnak tűnhet, különösen, ha programozottan csinálod. De ne félj! Az Aspose.Cells for .NET segítségével egy pivot tábla összeállítása nemcsak egyszerű, de meglehetősen hatékony is az adatelemzés szempontjából. Ebben az oktatóanyagban lépésről lépésre végigvezetünk azon, hogyan hozhatsz létre egy új pivot táblát egy .NET alkalmazásban. Akár értékesítési, sport- vagy bármilyen más üzleti mutatóhoz adsz hozzá adatokat, ez az útmutató segít abban, hogy a pivot tábláid pillanatok alatt működőképesek legyenek.

## Előfeltételek
Mielőtt belevágnánk, győződjünk meg róla, hogy minden elő van készítve. Íme, mit kell tenned:

1. Telepítse a .NET keretrendszert: Győződjön meg róla, hogy a .NET keretrendszer telepítve van a gépén. Az Aspose.Cells számos verziót támogat, de a legjobb, ha a legújabbat használja.
2. Aspose.Cells könyvtár: Szükséged lesz az Aspose.Cells könyvtárra. [töltsd le itt](https://releases.aspose.com/cells/net/) vagy szerezz egy [ideiglenes engedély](https://purchase.aspose.com/temporary-license/) értékeléshez.
3. IDE beállítás: Készíts elő egy C#-kompatibilis IDE-t, például a Visual Studio-t, ahol új projektet indíthatsz.
4. C# alapismeretek: A C# programozásban való jártasság segít abban, hogy ne kalandozz el túlságosan.

Készen állsz? Remek! Most pedig ugorjunk bele a szükséges csomagok importálásába.

## Csomagok importálása
Először is importálnod kell a szükséges névtereket a C# projektedbe. Nyisd meg a C# fájlt, és add hozzá a következőket direktívák használatával:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Ezek a névterek hozzáférést biztosítanak a munkafüzet, a munkalap és a kimutatástábla funkcióihoz, amelyeket ebben az oktatóanyagban fogunk használni.

## 1. lépés: Munkafüzet-objektum létrehozása
Egy munkafüzet létrehozása az utazásod kezdete. Kezdjük egy új munkafüzet létrehozásával és az első munkalap elérésével.

```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
// Workbook objektum példányosítása
Workbook workbook = new Workbook();

// Az újonnan hozzáadott munkalap hivatkozásának beszerzése
Worksheet sheet = workbook.Worksheets[0];
```

Ebben a lépésben létrehozunk egy `Workbook` példányt, amely az Excel-fájlunkat képviseli, és vedd elő az első munkalapot, amely a pivot tábla játszótere lesz.

## 2. lépés: Adatok beszúrása cellákba
Következő lépésként töltsük fel a munkalapunkat néhány mintaadattal. Különböző sportágak, negyedévek és értékesítési adatok sorait fogjuk megadni, hogy legyen mit összefoglalnunk a pivot táblázatunkban.

```csharp
Cells cells = sheet.Cells;

// A cellák értékének beállítása
Cell cell = cells["A1"];
cell.PutValue("Sport");
cell = cells["B1"];
cell.PutValue("Quarter");
cell = cells["C1"];
cell.PutValue("Sales");

// Kitöltés adatcella = cells["A2"];
cell.PutValue("Golf");
// ... További adatbevitelek
```

Itt az oszlopfejléceket definiáljuk, és értékeket szúrunk be az egyes fejlécek alá. Ezek az adatok szolgálnak majd a pivot tábla forrásaként, ezért ügyeljünk a rendszerezésre! Kövessük ezt a blokkot, és egy átfogó adathalmazt fogunk létrehozni.

## 3. lépés: Pivot tábla hozzáadása
Miután az adataink készen állnak, itt az ideje létrehozni a pivot táblát. A munkalapon található pivot táblagyűjteményt fogjuk használni az új pivot tábla hozzáadásához.

```csharp
Aspose.Cells.Pivot.PivotTableCollection pivotTables = sheet.PivotTables;

// Kimutatás hozzáadása a munkalaphoz
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```

Ebben a kódrészletben egy kimutatástáblát adunk a munkalaphoz, amely az adattartományunkra hivatkozik (ebben az esetben az A1-től C8-ig terjedő cellák). A kimutatástáblát az E3 cellától kezdődően helyezzük el, és „Kimutatás2. táblázat”-nak nevezzük el. Elég egyszerű, ugye?

## 4. lépés: A kimutatástábla testreszabása
Most, hogy elkészült a pivot táblánk, szabjuk testre, hogy értelmes összefoglalásokat jelenítsen meg. Beállíthatjuk, hogy mi jelenjen meg a pivot tábla soraiban, oszlopaiban és adatterületein.

```csharp
// Az újonnan hozzáadott PivotTable példányának elérése
Aspose.Cells.Pivot.PivotTable pivotTable = pivotTables[index];

// Sorok végösszegeinek megjelenítésének kikapcsolása.
pivotTable.RowGrand = false;

// Az első mező áthúzása a sorterületre.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Row, 0);

// A második mező áthúzása az oszlopterületre.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Column, 1);

// A harmadik mező áthúzása az adatterületre.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Data, 2);
```

Ebben a lépésben azt utasítjuk a pivot táblának, hogy rejtse el a sorok végösszegeit, majd megadjuk, hogy mely mezők kerüljenek a sor-, oszlop- és adatmezőkbe. A sportágak nevei töltik ki a sorokat, a negyedévek az oszlopokat, az értékesítési adatok pedig az összesítéseket.

## 5. lépés: A munkafüzet mentése
Végül szeretnénk elmenteni az újonnan létrehozott munkafüzetünket, hogy lássuk munkánk gyümölcsét.

```csharp
// Az Excel fájl mentése
workbook.Save(dataDir + "pivotTable_test_out.xls");
```

Csak adjon meg egy megfelelő elérési utat, és a pivot tábla kimenete egy Excel-fájlba lesz mentve, amelyet megnyithat és áttekinthet.

## Következtetés
Az Aspose.Cells for .NET segítségével programozottan létrehozott pivot táblák jelentős időt takaríthatnak meg, különösen nagy adathalmazok kezelésekor. Megtanultad, hogyan állítsd be a projektedet, hogyan importáld a szükséges csomagokat, hogyan töltsd fel az adatokat, és hogyan hozz létre egy testreszabható pivot táblát a nulláról. Tehát, amikor legközelebb számokban fuldoklodsz, ne feledd ezt az oktatóanyagot, és hagyd, hogy az Aspose.Cells elvégezze a nehéz munkát helyetted.

## GYIK
### Mi az Aspose.Cells?
Az Aspose.Cells egy hatékony .NET könyvtár Excel-táblázatok programozott létrehozásához és kezeléséhez.

### Van ingyenes próbaverzió az Aspose.Cells-hez?
Igen, kérhetsz ingyenes próbaverziót [itt](https://releases.aspose.com/).

### Testreszabhatom a pivot tábla megjelenését?
Természetesen! A pivot tábla formázását, elrendezését és még a stílusait is testreszabhatja az igényei szerint.

### Hol találok további példákat és dokumentációt az Aspose.Cells-ről?
Ellenőrizheti a [dokumentáció](https://reference.aspose.com/cells/net/) átfogó útmutatókért és példákért.

### Hogyan kaphatok támogatást az Aspose.Cells-hez?
Támogatást kaphatsz a következőn keresztül: [Aspose fórum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}