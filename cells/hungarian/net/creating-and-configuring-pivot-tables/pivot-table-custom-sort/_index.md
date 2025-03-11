---
title: Pivot Table Egyéni rendezés programozottan .NET-ben
linktitle: Pivot Table Egyéni rendezés programozottan .NET-ben
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan lehet programozottan rendezni a kimutatástáblákat .NET-ben az Aspose.Cells használatával. Lépésről lépésre szóló útmutató a beállításról, a konfigurálásról, a rendezésről és az eredmények Excel- és PDF-fájlként történő mentéséről.
weight: 29
url: /hu/net/creating-and-configuring-pivot-tables/pivot-table-custom-sort/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pivot Table Egyéni rendezés programozottan .NET-ben

## Bevezetés
Ha az Excellel .NET környezetben kell dolgozni, egy könyvtár kiemelkedik a többi közül: Aspose.Cells. Nos, nem szereti, ha egy eszköz lehetővé teszi a táblázatok programozott kezelését? Az Aspose.Cells pontosan ezt teszi! A mai oktatóanyagban mélyen elmerülünk a Pivot Tables világában, és megmutatjuk, hogyan valósíthat meg egyéni rendezést programozottan ennek a sokoldalú könyvtárnak a használatával.
## Előfeltételek
Mielőtt feltűrjük az ingujjunkat és belevágunk a kódba, győződjön meg arról, hogy a helyén van néhány dolog:
1. Visual Studio: Szüksége lesz a Visual Studio működő verziójára. Ez a játszótér, ahol minden varázslat megtörténik.
2. .NET-keretrendszer: A .NET-programozás ismerete elengedhetetlen. Legyen szó a .NET Core vagy a .NET Framework rajongóiról, készen áll.
3.  Aspose.Cells Library: Telepítenie kell az Aspose.Cells könyvtárat. Beszerezheti a[Letöltési link](https://releases.aspose.com/cells/net/) és add hozzá a projektedhez.
4. A kimutatások alapjai: Noha nem kell szakértőnek lenned, hasznos lesz egy kis ismeret a kimutatások működéséről, miközben végignézzük ezt az oktatóanyagot.
5.  Minta Excel-fájl: Nevezzen el egy Excel-mintafájlt`SamplePivotSort.xlsx` készen áll a munkakönyvtárban a tesztelésre.
## Csomagok importálása
Miután az összes előfeltételt rendezte, az első lépés a szükséges csomagok importálása. Ehhez írja be a következő sorokat a kód tetejére:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Pivot;
```
Ez a csomag minden olyan funkciót biztosít, amelyre szüksége van az Excel-fájlok Aspose.Cells használatával történő kezeléséhez.

Rendben, térjünk rá a mókás részre! A Pivot Table létrehozásának és az egyéni rendezés alkalmazásának folyamatát kezelhető lépésekre bontjuk.
## 1. lépés: Állítsa be a munkafüzetet
A dolgok elindításához fel kell állítanunk a munkafüzetünket. Íme, hogyan kell csinálni:
```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
Workbook wb = new Workbook(sourceDir + "SamplePivotSort.xlsx");
```
 Ebben a lépésben inicializálunk egy újat`Workbook` példányt az Excel fájl elérési útjával. Ez a vászon, ahol a kimutatástáblázatunk életre kel.
## 2. lépés: Nyissa meg a munkalapot
Ezután el kell érnünk a munkalapot, ahol hozzáadjuk a Pivot Table-nkat.
```csharp
Worksheet sheet = wb.Worksheets[0];
PivotTableCollection pivotTables = sheet.PivotTables;
```
 Itt megragadjuk a munkafüzetünk első munkalapját, és felszólítjuk a`PivotTableCollection`. Ez a gyűjtemény lehetővé teszi számunkra, hogy kezeljük a munkalapon található összes kimutatást.
## 3. lépés: Hozd létre az első kimutatástábládat
Most itt az ideje létrehozni a kimutatástáblázatunkat.
```csharp
int index = pivotTables.Add("=Sheet1!A1:C10", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables[index];
```
Új Pivot Table-t adunk a munkalapunkhoz, amely megadja az adattartományt és annak helyét. Az „E3” azt jelzi, hogy hol kezdjük a kimutatástáblázatunkat. Ezután az indexe segítségével hivatkozunk erre az új kimutatásra.
## 4. lépés: Konfigurálja a Pivot Table beállításokat
Konfiguráljuk a Pivot Table-t! Ez olyan szempontok ellenőrzését jelenti, mint a végösszeg és a tereprendezés.
```csharp
pivotTable.RowGrand = false;
pivotTable.ColumnGrand = false;
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
PivotField rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
Biztosítjuk, hogy a sorok és oszlopok végösszege ne jelenjen meg, ami tisztábbá teheti az adatokat. Ezután hozzáadjuk az első mezőt a sorterülethez, lehetővé téve az automatikus rendezést és a növekvő rendezést.
## 5. lépés: Oszlop és adatmezők hozzáadása
A sorok beállítása után adjuk hozzá az oszlopot és az adatmezőket.
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Column,0);
PivotField colField = pivotTable.ColumnFields[0];
colField.NumberFormat = "dd/mm/yyyy";
colField.IsAutoSort = true;
colField.IsAscendSort = true;
```
A második mezőt oszlopként adjuk hozzá, és dátumként formázzuk. Ismét engedélyezzük az automatikus rendezést és a növekvő sorrendet, hogy rendszerezzük a dolgokat. Végül hozzá kell adnunk a harmadik mezőt az adatterületünkhöz:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Data,2);
```
## 6. lépés: Frissítse és számítsa ki a Pivot Table-t
Az összes szükséges mező hozzáadása után győződjön meg arról, hogy kimutatásunk friss és készen áll.
```csharp
pivotTable.RefreshData();
pivotTable.CalculateData();
```
Ezek a módszerek frissítik és újraszámítják az adatokat, biztosítva, hogy minden naprakész legyen, és helyesen jelenjen meg a kimutatástáblázatunkban.
## 7. lépés: Egyéni rendezés a sormezők értékei alapján
Adjunk hozzá egy kis érzéket azzal, hogy a kimutatástáblázatot meghatározott értékek, például „tengeri ételek” alapján rendezzük.
```csharp
index = pivotTables.Add("=Sheet1!A1:C10", "E10", "PivotTable2");
pivotTable = pivotTables[index];
```
Megismételjük a folyamatot úgy, hogy létrehozunk egy másik kimutatást, és az elsőhöz hasonlóan állítjuk be. Most már tovább testreszabhatjuk:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
## 8. lépés: További rendezési testreszabás Próbáljunk ki egy másik rendezési módszert egy adott dátum alapján:
```csharp
// Egy másik kimutatás hozzáadása a dátum szerinti rendezéshez
index = pivotTables.Add("=Sheet1!A1:C10", "E18", "PivotTable3");
pivotTable = pivotTables[index];
// Ismételje meg a sor- és oszlopbeállításokat az előző lépésekhez hasonlóan
```
Csak ismételheti ugyanazt a folyamatot, létrehozva egy harmadik kimutatást, amelynek rendezési kritériumai az Ön igényeihez vannak szabva.
## 9. lépés: Mentse el a WorkbookTime-ot, hogy megmentse az általunk fektetett kemény munkát!
```csharp
wb.Save(outputDir + "out.xlsx");
PdfSaveOptions options = new PdfSaveOptions();
options.OnePagePerSheet = true;
wb.Save(outputDir + "out.pdf", options);
```
 Itt mentheti a munkafüzetet Excel-fájlként és PDF-fájlként. A`PdfSaveOptions` jobb formázást tesz lehetővé, biztosítva, hogy minden lap külön oldalon jelenjen meg konvertáláskor.
## 10. lépés: Fejezze be az egészet Csomagolja be az egészet úgy, hogy tudatja a felhasználóval, hogy minden rendben van.
```csharp
Console.WriteLine("PivotTableCustomSort executed successfully.");
```
## Következtetés
Mostanra megtanulta, hogyan használhatja ki az Aspose.Cells erejét a kimutatástáblázatok létrehozásához és testreszabásához .NET-alkalmazásaiban. A kezdeti beállítástól az egyéni rendezésig minden egyes lépés zökkenőmentes élményt biztosít. Akár éves értékesítési adatokat kell bemutatnia, akár készletstatisztikai adatokat kell követnie, ezek a készségek jól szolgálják majd Önt!
## GYIK
### Mi az a Pivot Table?
A Pivot Table egy adatfeldolgozó eszköz az Excelben, amely lehetővé teszi az adatok összegzését és elemzését, rugalmas módot biztosítva a betekintések egyszerű kinyerésére.
### Hogyan telepíthetem az Aspose.Cells-t?
 Telepítheti a NuGet segítségével a Visual Studio alkalmazásban, vagy letöltheti közvetlenül a webhelyről[Letöltési link](https://releases.aspose.com/cells/net/).
### Létezik az Aspose.Cells próbaverziója?
 Igen! Ingyenesen kipróbálhatja, ha ellátogat a[Ingyenes próba link](https://releases.aspose.com/).
### Rendezhetek több mezőt egy kimutatástáblázatban?
Teljesen! Igényei szerint több mezőt is felvehet és rendezhet.
### Hol találok támogatást az Aspose.Cells számára?
 A közösség meglehetősen aktív, és kérdéseket tehet fel a fórumukon[itt](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
