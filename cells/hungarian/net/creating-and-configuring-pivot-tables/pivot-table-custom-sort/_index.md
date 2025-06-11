---
"description": "Ismerje meg, hogyan rendezheti programozottan a pivot táblázatokat .NET-ben az Aspose.Cells használatával. Lépésről lépésre útmutató a beállításhoz, a konfigurációhoz, a rendezéshez és az eredmények Excel és PDF fájlokként történő mentéséhez."
"linktitle": "Pivot tábla egyéni rendezés programozottan .NET-ben"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Pivot tábla egyéni rendezés programozottan .NET-ben"
"url": "/hu/net/creating-and-configuring-pivot-tables/pivot-table-custom-sort/"
"weight": 29
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Pivot tábla egyéni rendezés programozottan .NET-ben

## Bevezetés
Ha .NET környezetben szeretnél Excellel dolgozni, egy könyvtár kiemelkedik a többi közül: az Aspose.Cells. Ugye, mennyire tetszik, amikor egy eszköz lehetővé teszi a táblázatok programozott kezelését? Pontosan ezt teszi az Aspose.Cells! A mai oktatóanyagban mélyen elmerülünk a pivot táblák világában, és megmutatjuk, hogyan valósíthatsz meg programozottan egyéni rendezést ennek a sokoldalú könyvtárnak a segítségével.
## Előfeltételek
Mielőtt feltűrnénk az ingujjunkat és belevágnánk a kódba, győződjünk meg róla, hogy van néhány dolog a helyén:
1. Visual Studio: Szükséged lesz a Visual Studio egy működő verziójára. Ez az a játszótér, ahol minden varázslat megtörténik.
2. .NET keretrendszer: A .NET programozásban való jártasság elengedhetetlen. Akár a .NET Core, akár a .NET keretrendszer rajongója vagy, nyugodtan belevághatsz.
3. Aspose.Cells könyvtár: Telepítenie kell az Aspose.Cells könyvtárat. Letöltheti innen: [Letöltési link](https://releases.aspose.com/cells/net/) és add hozzá a projektedhez.
4. pivot táblák alapvető ismerete: Bár nem kell szakértőnek lenned, a pivot táblák működésének némi ismerete hasznos lesz a bemutató során.
5. Minta Excel fájl: Készítsen egy minta Excel fájlt, amelynek neve `SamplePivotSort.xlsx` készen áll a munkakönyvtáradban tesztelésre.
## Csomagok importálása
Miután minden előfeltételt rendeztél, az első lépés a szükséges csomagok importálása. Ehhez a következő sorokat kell a kód elejére illesztened:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Pivot;
```
Ez a csomag az Excel fájlok Aspose.Cells használatával történő kezeléséhez szükséges összes funkciót biztosítja.

Rendben, akkor térjünk rá a mókára! Most lebontjuk a kimutatástábla létrehozásának és az egyéni rendezés alkalmazásának folyamatát kezelhető lépésekre.
## 1. lépés: A munkafüzet beállítása
A kezdéshez be kell állítanunk a munkafüzetünket. Így csináld:
```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
Workbook wb = new Workbook(sourceDir + "SamplePivotSort.xlsx");
```
Ebben a lépésben inicializálunk egy újat `Workbook` példány az Excel-fájlunk elérési útjával. Ez vászonként szolgál, ahol a Pivot-táblázat életre kel.
## 2. lépés: A munkalap elérése
Ezután el kell érnünk azt a munkalapot, ahová hozzáadjuk a Pivot táblánkat.
```csharp
Worksheet sheet = wb.Worksheets[0];
PivotTableCollection pivotTables = sheet.PivotTables;
```
Itt elővesszük a munkafüzetünk első munkalapját, és felhívjuk a figyelmet a `PivotTableCollection`Ez a gyűjtemény lehetővé teszi számunkra, hogy kezeljük az összes kimutatástáblát ezen a munkalapon.
## 3. lépés: Az első pivot táblázat létrehozása
Most itt az ideje, hogy létrehozzuk a Pivot táblánkat.
```csharp
int index = pivotTables.Add("=Sheet1!A1:C10", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables[index];
```
Hozzáadunk egy új kimutatástáblát a munkalapunkhoz, megadva az adattartományt és annak helyét. Az „E3” azt jelzi, hogy hol szeretnénk kezdeni a kimutatástáblát. Ezután az indexével hivatkozunk erre az új kimutatástáblára.
## 4. lépés: A kimutatástábla beállításainak konfigurálása
Konfiguráljuk a pivot táblánkat! Ez olyan aspektusok szabályozását jelenti, mint a végösszegek és a mezőelrendezések.
```csharp
pivotTable.RowGrand = false;
pivotTable.ColumnGrand = false;
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
PivotField rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
Biztosítjuk, hogy a sorok és oszlopok végösszegei ne jelenjenek meg, ami áttekinthetőbbé teheti az adatokat. Ezután hozzáadjuk az első mezőt a sorterülethez, engedélyezve az automatikus rendezést és a növekvő rendezést.
## 5. lépés: Oszlop- és adatmezők hozzáadása
Miután a sorok be vannak állítva, adjuk hozzá az oszlopokat és az adatmezőket.
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Column,0);
PivotField colField = pivotTable.ColumnFields[0];
colField.NumberFormat = "dd/mm/yyyy";
colField.IsAutoSort = true;
colField.IsAscendSort = true;
```
A második mezőt oszlopként adjuk hozzá, és dátumként formázzuk. Ismét engedélyezzük az automatikus rendezést és a növekvő sorrendet a rendszerezés érdekében. Végül hozzá kell adnunk a harmadik mezőt az adatterületünkhöz:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Data,2);
```
## 6. lépés: A pivottábla frissítése és kiszámítása
Miután hozzáadtuk az összes szükséges mezőt, győződjünk meg róla, hogy a Pivot táblánk friss és használatra kész.
```csharp
pivotTable.RefreshData();
pivotTable.CalculateData();
```
Ezek a módszerek frissítik az adatokat és újraszámolják azokat, biztosítva, hogy minden naprakész és helyesen jelenjen meg a kimutatástáblázatban.
## 7. lépés: Egyéni rendezés sormezőértékek alapján
Adjunk hozzá egy kis csillogást a kimutatástáblázat adott értékek, például a „Tengeri ételek” szerinti rendezésével.
```csharp
index = pivotTables.Add("=Sheet1!A1:C10", "E10", "PivotTable2");
pivotTable = pivotTables[index];
```
Megismételjük a folyamatot egy újabb pivot tábla létrehozásával és az elsőhöz hasonló beállításával. Most tovább testreszabhatjuk:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
## 8. lépés: További rendezési testreszabásPróbáljunk ki egy másik rendezési módszert egy adott dátum alapján:
```csharp
// Egy másik kimutatástábla hozzáadása dátum szerinti rendezéshez
index = pivotTables.Add("=Sheet1!A1:C10", "E18", "PivotTable3");
pivotTable = pivotTables[index];
// Ismételje meg a sor- és oszlopbeállításokat az előző lépésekhez hasonlóan
```
Egyszerűen végigmész ugyanazon a folyamaton, létrehozva egy harmadik kimutatástáblát, amelynek rendezési feltételei az igényeidhez igazodnak.
## 9. lépés: A munkafüzet mentéseIdőt szánunk arra, hogy elmentsük az összes kemény munkát, amit belefektettünk!
```csharp
wb.Save(outputDir + "out.xlsx");
PdfSaveOptions options = new PdfSaveOptions();
options.OnePagePerSheet = true;
wb.Save(outputDir + "out.pdf", options);
```
Itt mentheti el a munkafüzetet Excel-fájlként és PDF-ként. `PdfSaveOptions` jobb formázást tesz lehetővé, biztosítva, hogy minden munkalap külön oldalon jelenjen meg konvertáláskor.
## 10. lépés: BefejezésZárd le az egészet azzal, hogy tudatod a felhasználóval, hogy minden rendben van.
```csharp
Console.WriteLine("PivotTableCustomSort executed successfully.");
```
## Következtetés
Mostanra már megtanultad, hogyan használd ki az Aspose.Cells erejét a Pivot táblák létrehozásához és testreszabásához .NET alkalmazásaidban. A kezdeti beállítástól az egyéni rendezésig minden lépés zökkenőmentes élményt nyújt. Akár éves értékesítési adatokat kell bemutatnod, akár készletstatisztikákat kell nyomon követned, ezek a készségek jól fognak szolgálni!
## GYIK
### Mi az a pivot tábla?
kimutatástábla egy adatfeldolgozó eszköz az Excelben, amely lehetővé teszi az adatok összegzését és elemzését, rugalmas módot biztosítva az információk egyszerű kinyerésére.
### Hogyan telepítsem az Aspose.Cells-t?
Telepítheted a Visual Studio NuGet programján keresztül, vagy letöltheted közvetlenül a következő oldalról: [Letöltési link](https://releases.aspose.com/cells/net/).
### Van az Aspose.Cells próbaverziója?
Igen! Ingyenesen kipróbálhatod, ha ellátogatsz a következő oldalra: [Ingyenes próbaverzió linkje](https://releases.aspose.com/).
### Rendezhetek több mezőt egy kimutatástáblázatban?
Természetesen! Több mezőt is hozzáadhatsz és rendezhetsz az igényeid szerint.
### Hol találok támogatást az Aspose.Cells-hez?
A közösség elég aktív, és kérdéseket is feltehetsz a fórumukon. [itt](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}