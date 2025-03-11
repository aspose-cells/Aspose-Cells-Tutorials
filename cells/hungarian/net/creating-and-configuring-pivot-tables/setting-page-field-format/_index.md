---
title: Az oldalmező formátumának programozott beállítása .NET-ben
linktitle: Az oldalmező formátumának programozott beállítása .NET-ben
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan állíthat be programozottan oldalmezőformátumokat a kimutatásokban az Aspose.Cells for .NET használatával. Kövesse lépésről lépésre bemutató oktatóanyagunkat a zökkenőmentes adatkezelés érdekében.
weight: 21
url: /hu/net/creating-and-configuring-pivot-tables/setting-page-field-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Az oldalmező formátumának programozott beállítása .NET-ben

## Bevezetés
Az Excel-fájlok kódon keresztüli létrehozása és manipulálása igen hasznos lehet, különösen akkor, ha nagy adatkészleteket kell elemeznie. Az egyik fantasztikus eszköz az Ön arzenáljában az Aspose.Cells for .NET, amely lehetővé teszi az Excel-fájlokkal való programozott interakciót és összetett jelentési struktúrák létrehozását. Ebben az oktatóanyagban megvizsgáljuk, hogyan állíthat be oldalmezőformátumokat egy kimutatástáblán belül ennek a hatékony könyvtárnak a használatával. Akár tapasztalt fejlesztő, akár kezdő, ennek az útmutatónak a végére alaposan átlátja, hogyan kell kezelni a kimutatástáblákat és azok különféle beállításait a .NET-ben.
## Előfeltételek
Mielőtt belemerülnénk a kódolásba, győződjünk meg arról, hogy minden megfelelően van beállítva. A következőkre lesz szüksége:
- Visual Studio: Olyan munkakörnyezet, ahol megírhatja és végrehajthatja .NET kódját.
-  Aspose.Cells: Letöltheti a könyvtárat[itt](https://releases.aspose.com/cells/net/).
- Alapvető C# ismerete: A C# programozás ismerete segít jobban megérteni a kódrészleteket.
-  Excel-fájl: Készítsen Excel-fájlt (pl`Book1.xls`) tartalmazza a kimutatás létrehozására alkalmas adatokat. 
 Ha még nem tette meg, szerezze be az Aspose.Cells ingyenes próbaverzióját[itt](https://releases.aspose.com/).
## Csomagok importálása
A dolgok elindításához importálnia kell a megfelelő csomagokat a projektbe. Kezdje azzal, hogy a C# projektben adjon hozzá hivatkozásokat az Aspose.Cells könyvtárhoz. Íme, hogyan kell csinálni:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Ez az összes szükséges osztályt és módszert be fogja vonni az Excel-fájlok Aspose.Cells használatával történő kezeléséhez.
## 1. lépés: Állítsa be a munkaterületet
Kezdje azzal, hogy meghatározza a munkakönyvtárát, ahol az Excel-fájlokat tárolni fogja. Például deklarálhat egy változót így:
```csharp
string dataDir = "Your Document Directory";
```
## A munkafüzet betöltése
Ezután be kell töltenünk az Excel sablonunkat. Ez elengedhetetlen lépés, mert ez határozza meg működésünk kontextusát:
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Ez a sor betölti a meglévő munkafüzetet a megadott könyvtárból.
## 2. lépés: Nyissa meg a munkalapot
A munkafüzet betöltése után ideje elérni a kimutatást vagy az elemezni kívánt adatokat tartalmazó munkalapot. Ezt a következőképpen teheti meg:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Ez megragadja a betöltött munkafüzet első munkalapját. Könnyen módosíthatja az indexet, ha több lappal dolgozik.
## 3. lépés: A kimutatás elérése
 Folytatva, érjük el a kiválasztott munkalapunkon található PivotTable-t. Ha egyetlen kimutatástáblát használ, beállíthatja az indexét`0`:
```csharp
int pivotindex = 0;
// A PivotTable elérése
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
Ez a kódrészlet kiválasztja az első kimutatást a munkalapon. 
## 4. lépés: A kimutatás konfigurálása
Most jön az izgalmas rész! Állítsuk be a kimutatást úgy, hogy a sorok végösszegeit mutassa:
```csharp
pivotTable.RowGrand = true;
```
Ez a sor biztosítja, hogy a jelentés végösszegeket jelenítsen meg, amelyek hasznos összegzést jelenthetnek az adatok elemzéséhez.
## 5. lépés: A sormezők elérése és konfigurálása
Ezután el kell érnünk a kimutatás sormezőit:
```csharp
Aspose.Cells.Pivot.PivotFieldCollection pivotFields = pivotTable.RowFields;
```
Ez a gyűjtemény lehetővé teszi a mezők szükség szerinti kezelését.
## Konfigurálja az Első sor mezőt
Konkrét részösszeg-típusokat szeretne beállítani? Lépjünk be gyűjteményünk első mezőjébe, és állítsuk be:
```csharp
Aspose.Cells.Pivot.PivotField pivotField = pivotFields[0];
// Részösszegek beállítása.
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Sum, true);
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Count, true);
```
 Engedélyezésével`Sum` és`Count` részösszegeket, gyorsan összefoglalhatjuk az adatokat jelentésünkben.
## 6. lépés: Az automatikus rendezési beállítások megadása
Ezután vessünk játékba egy okos válogatást. Így a kimutatás értelmes sorrendbe rendezi az adatokat:
```csharp
// Automatikus rendezési beállítások megadása.
pivotField.IsAutoSort = true;
pivotField.IsAscendSort = true;
pivotField.AutoSortField = -5; // Egy előre meghatározott rendezési mező használata.
```
Ez a kódrészlet lehetővé teszi az automatikus rendezést, és növekvő sorrendet határoz meg. 
## 7. lépés: Az automatikus megjelenítési beállítások megadása
Szeretné tovább szűrni adatait? Az AutoShow opció hasznos bizonyos adatpontok meghatározott feltételek melletti megjelenítéséhez:
```csharp
// AutoShow opciók beállítása.
pivotField.IsAutoShow = true;
pivotField.IsAscendShow = false;
pivotField.AutoShowField = 0; // Adja meg az automatikusan megjelenítendő mezőt.
```
Ez biztosítja, hogy a kimutatás csak releváns adatokat jelenítsen meg, javítva az áttekinthetőséget és a fókuszt.
## 8. lépés: Mentse el munkáját
Ennyi konfiguráció után nem szeretné elveszíteni a munkáját! Mentse el a módosított munkafüzetet így:
```csharp
workbook.Save(dataDir + "output.xls");
```
Most már megtalálhatja az újonnan létrehozott Excel fájlt a dokumentumok könyvtárában.
## Következtetés
És megvan! Átfogó és gyakorlatias megközelítést mutattunk be az oldalmezőformátumok programozott beállításához egy kimutatásban az Aspose.Cells for .NET használatával. A megadott egyszerű lépésekkel magabiztosan módosíthatja Excel-adatait jelentéskészítési igényeinek megfelelően. Hihetetlen, hogy mit érhet el, ha egyesíti a C# erejét az Aspose.Cells-szel.
## GYIK
### Mi az Aspose.Cells?
Az Aspose.Cells egy .NET-könyvtár, amely lehetővé teszi a fejlesztők számára Excel-fájlok programozott létrehozását, kezelését és konvertálását.
### Hogyan telepíthetem az Aspose.Cells-t?
 Letöltheti közvetlenül a[Aspose honlapja](https://releases.aspose.com/cells/net/).
### Használhatom az Aspose.Cells-t Excel telepítése nélkül?
Igen, az Aspose.Cells egy önálló könyvtár, amelyhez nem szükséges a Microsoft Excel telepítése.
### Hol találok részletes támogatást?
 Részletes támogatást és fórumot a címen érhet el[Aspose támogatás](https://forum.aspose.com/c/cells/9).
### Hogyan szerezhetek ideiglenes engedélyt?
 Ideiglenes jogosítványt szerezhet be[itt](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
