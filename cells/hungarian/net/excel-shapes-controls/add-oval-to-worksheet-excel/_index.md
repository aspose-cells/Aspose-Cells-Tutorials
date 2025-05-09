---
"description": "Tanuld meg, hogyan adhatsz hozzá oválist egy Excel-munkalaphoz az Aspose.Cells for .NET használatával. Lépésről lépésre útmutató részletes kódmagyarázatokkal."
"linktitle": "Ovális hozzáadása a munkalaphoz Excelben"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Ovális hozzáadása a munkalaphoz Excelben"
"url": "/hu/net/excel-shapes-controls/add-oval-to-worksheet-excel/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ovális hozzáadása a munkalaphoz Excelben

## Bevezetés
Lenyűgöző és interaktív Excel-fájlok létrehozása többet jelenthet, mint pusztán számokat és képleteket. Az olyan alakzatok, mint az oválisok, vizuális megjelenést kölcsönözhetnek, vagy funkcionális elemeket biztosíthatnak a munkalapokon. Ebben az oktatóanyagban megvizsgáljuk, hogyan használhatjuk az Aspose.Cells for .NET-et oválisok programozott hozzáadásához egy Excel-munkalaphoz. Akár egy kis csillogást, akár funkcionalitást szeretnél hozzáadni, lépésről lépésre bemutatjuk a részleteket.
## Előfeltételek
Mielőtt belemerülnél a kódba, van néhány dolog, amire szükséged van:
1. Aspose.Cells .NET könyvtárhoz: Letöltheti innen: [itt](https://releases.aspose.com/cells/net/) vagy telepítse a NuGet használatával a Visual Studio-ban.
2. Fejlesztői környezet: AC# IDE, mint például a Visual Studio.
3. C# alapismeretek: Ismernie kell a C# alapvető kódolási koncepcióit.
Ne felejtsd el beállítani a projektedet az Aspose.Cells for .NET könyvtár telepítésével. Ha még nincs licenced, igényelhetsz egyet. [ideiglenes engedély](https://purchase.aspose.com/temporary-license/) vagy használja a [ingyenes próba](https://releases.aspose.com/) változat.
## Csomagok importálása
Mielőtt bármilyen kódot írnál, győződj meg róla, hogy megadtad a szükséges névtereket. Íme a C# kódrészlet, hogy biztosan a megfelelő könyvtárakat használd:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## 1. lépés: Állítsa be a címtárát
Az ovális Excel-táblázathoz való hozzáadásának első lépése annak megadása, hogy hová mentsük az Excel-fájlt. Definiáljuk a könyvtár elérési útját, és a mentés előtt ellenőrizzük, hogy a könyvtár létezik-e.

Létrehozunk egy könyvtár elérési utat, és ellenőrizzük, hogy létezik-e. Ha a mappa nem létezik, akkor létrejön.
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
// Hozz létre egy könyvtárat, ha az még nem létezik.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Ez a lépés kulcsfontosságú, mivel biztosítja, hogy a fájl a megfelelő helyre kerüljön mentésre, és később ne merüljenek fel fájlelérési útvonallal kapcsolatos problémák.
## 2. lépés: Új munkafüzet inicializálása
Ezután létre kell hoznunk egy új munkafüzetet, amelybe beillesztjük az ovális alakzatokat. A munkafüzet egy Excel-fájlt ábrázol, és tartalmat vagy alakzatokat adhatunk hozzá.

Ebben a lépésben létrehozunk egy új példányt `Workbook` objektum, amely az Excel-fájlunk tárolójaként fog szolgálni.
```csharp
// Hozz létre egy új munkafüzetet.
Workbook excelbook = new Workbook();
```
## 3. lépés: Adja hozzá az első ovális alakot
Most jön a mókás rész – egy ovális alakzat hozzáadása a munkalaphoz. Ez az ovális ábrázolhat egy vizuális elemet, például egy gombot vagy egy kiemelést. Először az első ovális alakzatot adjuk hozzá a munkafüzetünk első munkalapjához.

Itt használjuk a `Shapes.AddOval()` metódus egy ovális létrehozásához a munkalapon egy adott sorban és oszlopban.
```csharp
// Adjon hozzá egy ovális formát.
Aspose.Cells.Drawing.Oval oval1 = excelbook.Worksheets[0].Shapes.AddOval(2, 0, 2, 0, 130, 160);
```
A belső paraméterek `AddOval()` a következők:
- Az első két szám az ovális bal felső sarkának sorát és oszlopát jelöli.
- A következő két szám az ovális magasságát és szélességét jelöli.
## 4. lépés: Állítsa be az ovális elhelyezését és stílusát
Miután az ovális elkészült, beállíthatjuk a pozícióját, a vonalvastagságát és a szaggatott vonal stílusát. `Placement` tulajdonság határozza meg, hogyan viselkedjen az ovális a munkalap celláinak átméretezésekor vagy áthelyezésekor.

Az oválist szabadon lebegővé tesszük, és beállítjuk a megjelenését.
```csharp
// Állítsa be az ovális helyét.
oval1.Placement = PlacementType.FreeFloating;
// Állítsa be a vonalvastagságot.
oval1.Line.Weight = 1;
// Állítsa be az ovális vonalstílusát.
oval1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Ez lehetővé teszi, hogy az ovális szabadon mozoghasson a munkalapon belül, vonalvastagsága és stílusa pedig a vizuális egységesség érdekében van beállítva.
## 5. lépés: Adjon hozzá egy másik ovális (kör) alakot
Miért állnánk meg egynél? Ebben a lépésben egy újabb ovális alakzatot adunk hozzá, ezúttal egy tökéletes kört hozva létre a magasság és a szélesség megegyezésével.

Létrehozunk egy másik oválist, egy másik helyre helyezzük, és azonos magasság és szélesség beállításával biztosítjuk, hogy kör alakú legyen.
```csharp
// Adjon hozzá egy újabb ovális (kör) alakot.
Aspose.Cells.Drawing.Oval oval2 = excelbook.Worksheets[0].Shapes.AddOval(9, 0, 2, 15, 130, 130);
```
## 6. lépés: A második ovális formázása
A korábbiakhoz hasonlóan most is módosítjuk a második ovális (vagy kör) elhelyezését, vastagságát és vonalstílusát.

Hasonló tulajdonságokat alkalmazunk a második oválisra, hogy illeszkedjen az első stílusához.
```csharp
// Állítsa be az ovális helyét.
oval2.Placement = PlacementType.FreeFloating;
// Állítsa be a vonalvastagságot.
oval2.Line.Weight = 1;
// Állítsa be az ovális vonalstílusát.
oval2.Line.DashStyle = MsoLineDashStyle.Solid;
```
## 7. lépés: A munkafüzet mentése
Végül mentenünk kell a munkafüzetet az imént hozzáadott oválisokkal. A fájl mentése biztosítja, hogy minden módosításunk mentésre kerüljön.

A munkafüzetet a korábban meghatározott könyvtárba mentjük.
```csharp
// Mentse el az excel fájlt.
excelbook.Save(dataDir + "book1.out.xls");
```
És ennyi! Sikeresen hozzáadtad az oválisokat az Excel munkalapodhoz, és mentetted a fájlt.
## Következtetés
Az Aspose.Cells for .NET segítségével az Excel-táblázatokhoz alakzatok, például oválisok hozzáadása nemcsak egyszerű, de szórakoztató módja is a táblázatok vizuális elemekkel való kiegészítésének. Akár tervezési célokról, akár kattintható elemek hozzáadásáról van szó, az alakzatok jelentős szerepet játszhatnak az Excel-fájlok megjelenésében és működésében. Tehát, amikor legközelebb egy interaktív vagy vizuálisan vonzó Excel-táblázatokat igénylő projekten dolgozol, pontosan tudod, hogyan kell hozzáadni ezeket a tökéletes oválisokat!
## GYIK
### Hozzáadhatok más alakzatokat, például téglalapokat vagy vonalakat az Aspose.Cells for .NET használatával?
Igen, hozzáadhatsz különféle alakzatokat, például téglalapokat, vonalakat és nyilakat a `Shapes` gyűjtemény az Aspose.Cells-ben.
### Lehetséges az oválisok átméretezése a hozzáadásuk után?
Természetesen! A hozzáadásuk után módosíthatod az oválisok magasságát és szélességét.
### Milyen fájlformátumban menthetem el a munkafüzetet az XLS-en kívül?
Az Aspose.Cells több formátumot is támogat, például az XLSX-et, a CSV-t és a PDF-et.
### Módosíthatom az ovális körvonalának színét?
Igen, az ovális vonal színét megváltoztathatod a `Line.Color` ingatlan.
### Szükséges-e licenc az Aspose.Cells használatához?
Bár kipróbálhatod az Aspose.Cells-t ingyenes próbaverzióval, szükséged lesz egy [engedély](https://purchase.aspose.com/buy) hosszú távú használatra vagy a speciális funkciók eléréséhez.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}