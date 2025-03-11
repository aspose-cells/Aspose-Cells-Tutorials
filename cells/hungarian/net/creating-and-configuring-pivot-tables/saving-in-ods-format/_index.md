---
title: Pivot Table mentése ODS formátumban programozottan .NET-ben
linktitle: Pivot Table mentése ODS formátumban programozottan .NET-ben
second_title: Aspose.Cells .NET Excel Processing API
description: Ebből a lépésről lépésre szóló útmutatóból megtudhatja, hogyan mentheti el a kimutatástáblákat ODS formátumban az Aspose.Cells for .NET használatával.
weight: 25
url: /hu/net/creating-and-configuring-pivot-tables/saving-in-ods-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pivot Table mentése ODS formátumban programozottan .NET-ben

## Bevezetés
Amikor az adatok táblázatokban történő kezeléséről van szó, semmi sem vetekedhet a kimutatások erejével. Használható eszköz az összetett adatkészletek összegzésére, elemzésére és bemutatására. Ma az Aspose.Cells for .NET használatával fogunk foglalkozni egy kimutatás ODS formátumban való mentésére. Akár tapasztalt fejlesztő vagy, akár csak a .NET-et szeretnéd használni, ezt az útmutatót egyszerűnek találod. 
Kezdjük is!
## Előfeltételek
Mielőtt belevágnánk a kódba, néhány alapvető dologra lesz szüksége:
### 1. Alapvető ismeretek a .NET-ről
A .NET és annak programozási koncepcióinak alapszintű ismerete megkönnyíti a követést.
### 2. Aspose.Cells for .NET
 Telepíteni kell az Aspose.Cells for .NET programot. Letöltheti a[Az Aspose kiadási oldala](https://releases.aspose.com/cells/net/) . Próbaverzió is elérhető[itt](https://releases.aspose.com/).
### 3. Fejlesztési környezet
Győződjön meg arról, hogy rendelkezik egy IDE-vel, például a Visual Studio-val, ahol megírhatja és tesztelheti a .NET-kódot.
### 4. Egy kis türelem
Mint minden kódolási próbálkozásnál, itt is kulcsfontosságú a türelem. Ne aggódjon, ha a dolgok elsőre nem működnek tökéletesen; a hibakeresés a folyamat része.
## Csomagok importálása
Az Aspose.Cells használatához importálnia kell a szükséges névtereket. Adja hozzá a következőt az utasítás használatával a kódfájl elejéhez:
```csharp
using System;
using Aspose.Cells.Pivot;
```
Ez a sor lehetővé teszi az Aspose.Cells könyvtár összes funkciójának elérését, így a kódolási folyamat gyerekjáték.
Most bontsuk le a folyamatot kezelhető lépésekre.
## 1. lépés: Állítsa be a kimeneti könyvtárat
Először is meg kell határoznia, hová szeretné menteni az ODS fájlt. Ez egy könyvtárútvonal egyszerű hozzárendelése.
```csharp
string outputDir = "Your Document Directory";
```
 Ebben a sorban cserélje ki`"Your Document Directory"` azzal az elérési úttal, ahová a fájlt menteni szeretné.
## 2. lépés: Hozzon létre egy új munkafüzetet
Ezután egy új munkafüzet-objektumot fog létrehozni, amely az összes adatot és struktúrát tartalmazza, beleértve a kimutatástáblát is.
```csharp
Workbook workbook = new Workbook();
```
Itt alapvetően frissen kezdi – tekintse úgy, mint egy üres vászonra, ahol elkészítheti remekművét.
## 3. lépés: Nyissa meg a munkalapot
Most, hogy megvan a munkafüzetünk, hozzá kell kezdenünk a munkalapunkhoz. Az Aspose.Cells segítségével könnyedén elérheti az első elérhető munkalapot.
```csharp
Worksheet sheet = workbook.Worksheets[0];
```
Ezzel a sorral eljutunk a legelső laphoz, amely készen áll az adatbevitelre.
## 4. lépés: Töltse fel a cellákat adatokkal
Ideje kitölteni a munkalapunkat néhány adattal. Egy egyszerű példát fogunk használni a sportértékesítési adatokra. 
A következőképpen állíthat be értékeket a különböző cellákban:
```csharp
Cells cells = sheet.Cells;
cells["A1"].PutValue("Sport");
cells["B1"].PutValue("Quarter");
cells["C1"].PutValue("Sales");
cells["A2"].PutValue("Golf");
cells["A3"].PutValue("Golf");
cells["A4"].PutValue("Tennis");
cells["A5"].PutValue("Tennis");
cells["A6"].PutValue("Tennis");
cells["A7"].PutValue("Tennis");
cells["A8"].PutValue("Golf");
cells["B2"].PutValue("Qtr3");
cells["B3"].PutValue("Qtr4");
cells["B4"].PutValue("Qtr3");
cells["B5"].PutValue("Qtr4");
cells["B6"].PutValue("Qtr3");
cells["B7"].PutValue("Qtr4");
cells["B8"].PutValue("Qtr3");
cells["C2"].PutValue(1500);
cells["C3"].PutValue(2000);
cells["C4"].PutValue(600);
cells["C5"].PutValue(1500);
cells["C6"].PutValue(4070);
cells["C7"].PutValue(5000);
cells["C8"].PutValue(6430);
```
Ezekben a sorokban definiáljuk a címsorokat és feltöltjük az értékesítési adatokat. Gondoljon erre a lépésre úgy, mint a kamra telepakolása étkezés előtt; minél jobbak az összetevők (adatok), annál jobb az étkezés (analízis).
## 5. lépés: Hozzon létre egy kimutatástáblát
Most jön a mókás rész – a Pivot Table létrehozása! A következőképpen adhatja hozzá a munkalaphoz:
```csharp
PivotTableCollection pivotTables = sheet.PivotTables;
// PivotTable hozzáadása a munkalaphoz
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```
 Ebben a kódrészletben megadjuk a kimutatástábla adattartományát, és azt, hogy hol helyezzük el a munkalapon. Az adattartomány`=A1:C8` lefedi azt a területet, ahol adataink léteznek.
## 6. lépés: A Pivot Table testreszabása
Ezután testre kell szabnia a kimutatástáblázatot az igényeinek megfelelően. Ez magában foglalja a megjelenített tartalmak, a kategorizálás és az adatok kiszámításának módját.
```csharp
PivotTable pivotTable = pivotTables[index];
// A sorok végösszegei nem jelennek meg.
pivotTable.RowGrand = false;
// Az első mező húzása a sorterületre.
pivotTable.AddFieldToArea(PivotFieldType.Row, 0);
// A második mező húzása az oszlopterületre.
pivotTable.AddFieldToArea(PivotFieldType.Column, 1);
// A harmadik mező húzása az adatterületre.
pivotTable.AddFieldToArea(PivotFieldType.Data, 2);
pivotTable.CalculateData();
```
Itt Ön dönti el, hogy mely adatmezőket foglalja össze, és hogyan ábrázolja azokat. Ez olyan, mint a vacsora megterítése; Ön dönti el, mi illik a legjobban, és hogyan mutassa be.
## 7. lépés: Mentse el a munkafüzetet
Végül készen áll, hogy elmentse munkáját a kívánt ODS formátumba. Íme, hogyan kell csinálni:
```csharp
workbook.Save(outputDir + "PivotTableSaveInODS_out.ods");
```
Ezzel a lépéssel lezárja projektjét, és rögzíti azt a kiválasztott könyvtárban – ez egy kielégítő befejezés!
## 8. lépés: Ellenőrizze a kimenetet
Végül mindig jó ötlet ellenőrizni, hogy a folyamat sikeresen befejeződött-e. Hozzáadhat egy egyszerű konzolüzenetet:
```csharp
Console.WriteLine("PivotTableSaveInODS executed successfully.");
```
Ez az üzenet jelenik meg a konzolon, hogy megerősítse, hogy minden probléma nélkül ment. Akárcsak egy szakács, aki tálalás előtt ellenőrzi, hogy minden tökéletesre sült-e!
## Következtetés 
És megvan! Ön nemcsak létrehozta a kimutatástáblázatot az Aspose.Cells használatával, hanem ODS formátumban is elmentette. Ez az útmutató végigvezette Önt minden lépésen, és biztosítja, hogy megfelelő tudással és önbizalommal felvértezve tudja megbirkózni a hasonló feladatokkal a jövőben.
## GYIK
### Mi az Aspose.Cells?
Az Aspose.Cells egy kifinomult könyvtár, amely lehetővé teszi Excel-fájlok létrehozását és kezelését .NET-alkalmazásokban.
### Használhatom ingyenesen az Aspose.Cells-t?
 Igen, letölthet egy ingyenes próbaverziót a webhelyről[Aspose honlapja](https://releases.aspose.com/).
### Milyen formátumokat támogat az Aspose.Cells?
Számos formátumot támogat, beleértve az XLSX, XLS, ODS, PDF és sok más formátumot.
### Hogyan kaphatok támogatást az Aspose.Cells-hez?
 Segítséget találhat a[Aspose támogatási fórum](https://forum.aspose.com/c/cells/9).
### Van ideiglenes engedély?
 Igen, kérhet ideiglenes licencet az Aspose webhelyén[itt](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
