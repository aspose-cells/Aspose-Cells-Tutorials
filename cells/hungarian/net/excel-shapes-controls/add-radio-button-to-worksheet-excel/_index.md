---
"description": "Tanuld meg, hogyan adhatsz hozzá választógombokat egy Excel-munkalaphoz az Aspose.Cells for .NET használatával ezzel az egyszerű, lépésről lépésre haladó útmutatóval. Tökéletes interaktív Excel-űrlapok létrehozásához."
"linktitle": "Rádiógomb hozzáadása a munkalaphoz Excelben"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Rádiógomb hozzáadása a munkalaphoz Excelben"
"url": "/hu/net/excel-shapes-controls/add-radio-button-to-worksheet-excel/"
"weight": 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Rádiógomb hozzáadása a munkalaphoz Excelben

## Bevezetés
Gondolkodtál már azon, hogyan dobhatod fel Excel-táblázataidat interaktív elemekkel, például választógombokkal? Akár egy kérdőívet, egy űrlapot vagy egy elemzőeszközt készítesz, a választógombok hozzáadása valóban javíthatja a felhasználói interakciót. Ebben az oktatóanyagban végigvezetünk a választógombok Excel-táblázatokhoz való hozzáadásának folyamatán az Aspose.Cells for .NET használatával. Mindent könnyen követhető lépésekre bontunk, így biztosítva, hogy a cikk végére profi legyél. Készen állsz a belevágni? Kezdjük is!
## Előfeltételek
Mielőtt belevágnánk a rádiógombok hozzáadásának szórakoztató részébe, győződjünk meg róla, hogy mindent beállítottunk az induláshoz.
1. Aspose.Cells .NET-hez: Először is győződjön meg róla, hogy letöltötte és telepítette a [Aspose.Cells .NET-hez](https://releases.aspose.com/cells/net/) könyvtár. Letöltheted a NuGet segítségével a Visual Studio-ban, vagy a letöltési oldalról.
2. IDE (Integrált fejlesztői környezet): C# kód írásához és végrehajtásához szükséged lesz egy IDE-re, például a Visual Studio-ra.
3. .NET-keretrendszer: Győződjön meg róla, hogy a gépén telepítve van a .NET-keretrendszer 4.0-s vagy újabb verziója. Az Aspose.Cells működéséhez erre van szükség.
4. C# alapismeretek: A C# szintaxis és a .NET programozás ismerete megkönnyíti a dolgokat a haladás során.
Miután mindent a helyére tettünk, indulhatunk is!
## Csomagok importálása
A kódolás megkezdése előtt elengedhetetlen a szükséges névterek importálása a későbbi hibák elkerülése érdekében. Adja hozzá a következőket a kódjához:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Drawing;
```
Ezek az importálások elengedhetetlenek a munkafüzet funkcióinak eléréséhez, a választógombok hozzáadásához és a fájlműveletek kezeléséhez.
## 1. lépés: A munkafüzet beállítása
Először is, hozzunk létre egy új Excel munkafüzetet.
Kezdéshez létre kell hoznod egy új példányt `Workbook` objektum. Ez fogja az Excel-fájlt a kódban ábrázolni.
```csharp
// Hozz létre egy új munkafüzetet.
Workbook excelbook = new Workbook();
```
Ebben a lépésben egy üres munkafüzetet hozol létre. Képzeld el úgy, mint egy üres vásznat, ahová a következő lépésekben választógombokat fogsz hozzáadni.
## 2. lépés: Cellaérték hozzáadása és formázása
Következő lépésként adjunk címet a munkalaphoz. Hozzáadunk szöveget a cellához. `C2` és formázd félkövérre. Ez a lépés kontextust ad a választógombokhoz.
### Szöveg beszúrása cellába
```csharp
// Írjon be egy értéket a C2 cellába.
excelbook.Worksheets[0].Cells["C2"].PutValue("Age Groups");
```
### Tedd a szöveget félkövérré
```csharp
// Állítsd a C2 cellában lévő szöveg betűtípusát félkövérre.
excelbook.Worksheets[0].Cells["C2"].GetStyle().Font.IsBold = true;
```
Itt egy egyszerű címet adtunk hozzá, „Korcsoportok” címmel, a cellában. `C2`, és félkövérré tette, hogy kitűnjön. Könnyű, ugye?
## 3. lépés: Az első választógomb hozzáadása
Most jön az izgalmas rész: az első rádiógomb hozzáadása a munkalaphoz!
### Választógomb hozzáadása
```csharp
// Adjon hozzá egy választógombot az első munkalaphoz.
Aspose.Cells.Drawing.RadioButton radio1 = excelbook.Worksheets[0].Shapes.AddRadioButton(3, 0, 2, 0, 30, 110);
```
Ez a sor a választógombot a munkalap egy adott pozíciójához adja hozzá. A számok a gomb elhelyezkedését és méretét jelölik. Úgy kell elképzelni, mintha a gomb X és Y koordinátáit állítanánk be.
### Rádiógomb szövegének beállítása
```csharp
// Állítsa be a szöveges karakterláncot.
radio1.Text = "20-29";
```
Itt a választógombnak egy „20-29” feliratot adtunk, amely egy korcsoportot jelöl.
### Rádiógomb csatolása egy cellához
```csharp
// Az A1 cellát állítsa be csatolt cellának a választógombhoz.
radio1.LinkedCell = "A1";
```
Ez összekapcsolja a rádiógombot a cellával `A1`, ami azt jelenti, hogy a gomb kiválasztásának eredménye ebben a cellában lesz tárolva.
### 3D effektus hozzáadása
```csharp
// Tegye a rádiógombot háromdimenzióssá.
radio1.Shadow = true;
```
Mivel azt szeretnénk, hogy ez a választógomb kinyíljon, hozzáadtunk egy 3D effektust.
### A rádiógomb sorának testreszabása
```csharp
// Állítsa be a választógomb sorának vastagságát.
radio1.Line.Weight = 4;
// Állítsa be a választógomb sorának szaggatott vonal stílusát.
radio1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Ezek a kódsorok a választógomb szegélyének vastagságát és szaggatott vonal stílusát módosítják, hogy vizuálisan vonzóbbá tegyék.
## 4. lépés: További választógombok hozzáadása
Adjunk hozzá még két választógombot a fennmaradó korcsoportokhoz: „30-39” és „40-49”. A lépések ugyanazok, csak apró eltérésekkel a koordinátákban és a címkékben.
### Második választógomb hozzáadása
```csharp
// Adjon hozzá egy másik választógombot az első munkalaphoz.
Aspose.Cells.Drawing.RadioButton radio2 = excelbook.Worksheets[0].Shapes.AddRadioButton(6, 0, 2, 0, 30, 110);
// Állítsa be a szöveges karakterláncot.
radio2.Text = "30-39";
// Az A1 cellát állítsa be csatolt cellának a választógombhoz.
radio2.LinkedCell = "A1";
// Tegye a rádiógombot háromdimenzióssá.
radio2.Shadow = true;
// Állítsa be a választógomb súlyát.
radio2.Line.Weight = 4;
// Állítsa be a választógomb kötőjelének stílusát.
radio2.Line.DashStyle = MsoLineDashStyle.Solid;
```
### Harmadik választógomb hozzáadása
```csharp
// Adjon hozzá egy másik választógombot az első munkalaphoz.
Aspose.Cells.Drawing.RadioButton radio3 = excelbook.Worksheets[0].Shapes.AddRadioButton(9, 0, 2, 0, 30, 110);
// Állítsa be a szöveges karakterláncot.
radio3.Text = "40-49";
// Az A1 cellát állítsa be csatolt cellának a választógombhoz.
radio3.LinkedCell = "A1";
// Tegye a rádiógombot háromdimenzióssá.
radio3.Shadow = true;
// Állítsa be a választógomb súlyát.
radio3.Line.Weight = 4;
// Állítsa be a választógomb kötőjelének stílusát.
radio3.Line.DashStyle = MsoLineDashStyle.Solid;
```
## 5. lépés: Az Excel-fájl mentése
Miután az összes rádiógombot hozzáadtad és formázod, itt az ideje menteni a fájlt.
```csharp
// Mentse el az excel fájlt.
string dataDir = "Your Document Directory";
excelbook.Save(dataDir + "book1.out.xls");
```
Ebben a lépésben a munkafüzet a megadott könyvtárba kerül mentésre. Ilyen egyszerű – az interaktív munkalapod most már készen is áll!
## Következtetés
Íme! Most adtál hozzá választógombokat egy Excel munkalaphoz az Aspose.Cells for .NET segítségével. Ez az oktatóanyag mindent lefed, a munkafüzet beállításától kezdve az értékek beszúrásán és formázásán át több választógomb hozzáadásáig és cellához csatolásukig. Most már készen állsz arra, hogy interaktív Excel munkalapokat hozz létre, amelyek nemcsak remekül néznek ki, hanem fokozott felhasználói élményt is nyújtanak. Jó szórakozást az Aspose.Cells további lehetőségeinek felfedezéséhez!
## GYIK
### Hozzáadhatok több választógombot különböző munkalapokhoz?  
Természetesen! A folyamatot a munkafüzet bármelyik munkalapján megismételheti a megfelelő munkalapindex megadásával.
### Testreszabhatom a rádiógombok megjelenését?  
Igen, az Aspose.Cells számos testreszabási lehetőséget kínál, beleértve a színek, méretek és egyéb formázási attribútumok módosítását.
### Hogyan tudom megállapítani, hogy melyik rádiógomb van kiválasztva?  
csatolt cella (pl. A1) megjeleníti a kiválasztott választógomb indexét. A csatolt cella értékének ellenőrzésével megtudhatja, melyik van kiválasztva.
### Van-e korlátozás a hozzáadható rádiógombok számára?  
Nem, nincs szigorú korlátozás a hozzáadható választógombok számára vonatkozóan. Azonban jó, ha a felület felhasználóbarát marad.
### Használhatom az Aspose.Cells-t más programozási nyelvekkel?  
Igen, az Aspose.Cells több programozási nyelvet is támogat, beleértve a Javát is. De ez az oktatóanyag kifejezetten a .NET-re összpontosít.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}