---
title: Adja hozzá a rádiógombot az Excel munkalapjához
linktitle: Adja hozzá a rádiógombot az Excel munkalapjához
second_title: Aspose.Cells .NET Excel Processing API
description: Ebből az egyszerű, lépésenkénti útmutatóból megtudhatja, hogyan adhat hozzá választógombokat egy Excel-munkalaphoz az Aspose.Cells for .NET használatával. Tökéletes interaktív Excel űrlapok létrehozásához.
weight: 19
url: /hu/net/excel-shapes-controls/add-radio-button-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adja hozzá a rádiógombot az Excel munkalapjához

## Bevezetés
Gondolkozott már azon, hogyan teheti meg Excel-lapjait interaktív elemekkel, például rádiógombokkal? Legyen szó felmérésről, űrlapról vagy elemzőeszközről, a rádiógombok hozzáadása valóban javíthatja a felhasználói interakciót. Ebben az oktatóanyagban végigvezetjük a választógombok Excel-lapokhoz való hozzáadásának folyamatán az Aspose.Cells for .NET segítségével. Mindent egyszerűen követhető lépésekre bontunk, így biztosítva, hogy a cikk végére profi lesz. Készen állsz a merülésre? Kezdjük is!
## Előfeltételek
Mielőtt belevágnánk a rádiógombok hozzáadásának szórakoztató részébe, győződjön meg arról, hogy minden be van állítva a kezdéshez.
1.  Aspose.Cells for .NET: Először győződjön meg arról, hogy letöltötte és telepítette a[Aspose.Cells for .NET](https://releases.aspose.com/cells/net/) könyvtár. Megragadhatja a NuGet segítségével a Visual Studio-ban vagy a letöltési oldalról.
2. IDE (Integrated Development Environment): A C# kód írásához és végrehajtásához olyan IDE-re lesz szüksége, mint a Visual Studio.
3. .NET-keretrendszer: Győződjön meg arról, hogy a .NET-keretrendszer 4.0-s vagy újabb verziója telepítve van a számítógépen. Az Aspose.Cells működéséhez ez szükséges.
4. A C# alapvető ismerete: A C# szintaxis és a .NET programozás ismerete megkönnyíti a dolgokat, ahogy követi.
Ha minden a helyére került, készen állunk a görgetésre!
## Csomagok importálása
A kódolás előtt elengedhetetlen a szükséges névterek importálása a későbbi hibák elkerülése érdekében. Adja hozzá a következőt a kódhoz:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Drawing;
```
Ezek az importálások elengedhetetlenek a munkafüzet funkcióinak eléréséhez, választógombok hozzáadásához és a fájlműveletek kezeléséhez.
## 1. lépés: A munkafüzet beállítása
Először is hozzunk létre egy új Excel-munkafüzetet.
 A kezdéshez létre kell hoznia egy újat`Workbook` objektum. Ez az Excel-fájlt kódban fogja képviselni.
```csharp
// Példányosítson egy új munkafüzetet.
Workbook excelbook = new Workbook();
```
Ebben a lépésben egy üres munkafüzetet hoz létre. Képzelje el üres vászonként, ahol rádiógombokat ad hozzá a következő lépésekben.
## 2. lépés: Cellaérték hozzáadása és formázása
Ezután adjunk címet a munkalaphoz. Hozzáadunk néhány szöveget a cellához`C2` és formázza félkövérre. Ez a lépés kontextust ad a rádiógombokhoz.
### Szöveg beszúrása a cellába
```csharp
// Szúrjon be egy értéket a C2 cellába.
excelbook.Worksheets[0].Cells["C2"].PutValue("Age Groups");
```
### Tegye félkövérre a szöveget
```csharp
// Állítsa félkövérre a betűtípus szövegét a C2 cellában.
excelbook.Worksheets[0].Cells["C2"].GetStyle().Font.IsBold = true;
```
 Itt a cellába egy egyszerű címet adtunk: „Korcsoportok”.`C2`, és félkövérré tette, így kiemelkedik. Könnyű, igaz?
## 3. lépés: Az első rádiógomb hozzáadása
Most jön az izgalmas rész: az első rádiógomb hozzáadása a munkalaphoz!
### Adjon hozzá egy rádiógombot
```csharp
// Adjon hozzá egy rádiógombot az első laphoz.
Aspose.Cells.Drawing.RadioButton radio1 = excelbook.Worksheets[0].Shapes.AddRadioButton(3, 0, 2, 0, 30, 110);
```
Ez a sor hozzáadja a választógombot a munkalap egy adott pozíciójához. A számok az elhelyezését és méretét jelzik. Képzeld el úgy, mint a gomb X és Y koordinátáit.
### Állítsa be a rádiógomb szövegét
```csharp
// Állítsa be a szöveges karakterláncot.
radio1.Text = "20-29";
```
Itt a választógombot a „20-29” címkével láttuk el, amely egy korcsoportot jelöl.
### Kapcsolja össze a rádiógombot egy cellával
```csharp
// Állítsa be az A1 cellát a rádiógombhoz csatolt cellaként.
radio1.LinkedCell = "A1";
```
 Ez összekapcsolja a rádiógombot a cellával`A1`ami azt jelenti, hogy a gombválasztás eredménye abban a cellában lesz eltárolva.
### 3D effektus hozzáadása
```csharp
// Tegye a rádiógombot 3D-re.
radio1.Shadow = true;
```
Mivel azt akarjuk, hogy ez a rádiógomb felbukkanjon, 3D effektust adtunk hozzá.
### Szabja testre a rádiógomb vonalát
```csharp
// Állítsa be a rádiógomb vonalának súlyát.
radio1.Line.Weight = 4;
// Állítsa be a választógomb vonalának kötőjel stílusát.
radio1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Ezek a kódsorok beállítják a választógomb szegélyének vastagságát és szaggatott stílusát, hogy látványosabbá tegyék.
## 4. lépés: További rádiógombok hozzáadása
Adjunk hozzá még két választógombot a fennmaradó korcsoportokhoz: "30-39" és "40-49". A lépések ugyanazok, csak kis eltérésekkel a koordinátákban és a címkékben.
### Adja hozzá a második rádiógombot
```csharp
// Adjon hozzá egy másik rádiógombot az első laphoz.
Aspose.Cells.Drawing.RadioButton radio2 = excelbook.Worksheets[0].Shapes.AddRadioButton(6, 0, 2, 0, 30, 110);
// Állítsa be a szöveges karakterláncot.
radio2.Text = "30-39";
// Állítsa be az A1 cellát a rádiógombhoz csatolt cellaként.
radio2.LinkedCell = "A1";
// Tegye a rádiógombot 3D-re.
radio2.Shadow = true;
// Állítsa be a rádiógomb súlyát.
radio2.Line.Weight = 4;
// Állítsa be a választógomb kötőjel stílusát.
radio2.Line.DashStyle = MsoLineDashStyle.Solid;
```
### Adja hozzá a harmadik rádiógombot
```csharp
// Adjon hozzá egy másik rádiógombot az első laphoz.
Aspose.Cells.Drawing.RadioButton radio3 = excelbook.Worksheets[0].Shapes.AddRadioButton(9, 0, 2, 0, 30, 110);
// Állítsa be a szöveges karakterláncot.
radio3.Text = "40-49";
// Állítsa be az A1 cellát a rádiógombhoz csatolt cellaként.
radio3.LinkedCell = "A1";
// Tegye a rádiógombot 3D-re.
radio3.Shadow = true;
// Állítsa be a rádiógomb súlyát.
radio3.Line.Weight = 4;
// Állítsa be a választógomb kötőjel stílusát.
radio3.Line.DashStyle = MsoLineDashStyle.Solid;
```
## 5. lépés: Az Excel fájl mentése
Miután az összes rádiógombot hozzáadta és formázta, ideje elmenteni a fájlt.
```csharp
// Mentse el az excel fájlt.
string dataDir = "Your Document Directory";
excelbook.Save(dataDir + "book1.out.xls");
```
Ebben a lépésben a munkafüzet a megadott könyvtárba kerül. Ilyen egyszerű – az interaktív munkalap készen áll!
## Következtetés
Megvan! Az Aspose.Cells for .NET segítségével választógombokat adott hozzá egy Excel-munkalaphoz. Ez az oktatóanyag mindenre kiterjedt, kezdve a munkafüzet beállításától, egy érték beszúrásán és formázásán, több választógomb hozzáadásán és egy cellával való összekapcsolásán keresztül. Most már készen áll arra, hogy interaktív Excel-lapokat hozzon létre, amelyek nemcsak jól néznek ki, hanem továbbfejlesztett felhasználói élményt is nyújtanak. Jó szórakozást a további lehetőségek felfedezéséhez az Aspose.Cells segítségével!
## GYIK
### Hozzáadhatok több rádiógombot a különböző lapokhoz?  
Teljesen! A folyamatot a munkafüzet bármely lapján megismételheti a megfelelő munkalapindex megadásával.
### Tovább szabhatom a választógombok megjelenését?  
Igen, az Aspose.Cells számos testreszabási lehetőséget kínál, beleértve a színek, méretek és egyéb formázási attribútumok megváltoztatását.
### Hogyan tudom megállapítani, hogy melyik rádiógomb van kiválasztva?  
csatolt cellában (pl. A1) megjelenik a kiválasztott rádiógomb indexe. Ellenőrizheti a csatolt cella értékét, hogy megtudja, melyik van kiválasztva.
### Van-e korlátozás a hozzáadható választógombok számára?  
Nem, a hozzáadható választógombok számának nincs szigorú korlátozása. Mindazonáltal jó, ha a kezelőfelület felhasználóbarát marad.
### Használhatom az Aspose.Cells-t más programozási nyelvekkel?  
Igen, az Aspose.Cells több programozási nyelvet támogat, beleértve a Java-t is. Ez az oktatóanyag azonban kifejezetten a .NET-re összpontosít.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
