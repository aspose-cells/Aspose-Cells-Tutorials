---
title: Formázás alkalmazása egy Excel-sorra programozottan
linktitle: Formázás alkalmazása egy Excel-sorra programozottan
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan alkalmazhat formázást programozottan egy Excel-sorra az Aspose.Cells for .NET használatával. Ez a részletes, lépésenkénti útmutató az igazítástól a szegélyekig mindenre kiterjed.
weight: 11
url: /hu/net/formatting-rows-and-columns-in-excel/applying-formatting-to-an-excel-row/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formázás alkalmazása egy Excel-sorra programozottan

## Bevezetés
Ebben az oktatóanyagban bemutatjuk, hogyan alkalmazhat formázást egy Excel-sorra programozottan az Aspose.Cells for .NET használatával. Mindent lefedünk a környezet beállításától a különféle formázási lehetőségek, például a betűszín, az igazítás és a szegélyek alkalmazásáig – mindezt úgy, hogy az egyszerű és vonzó. Merüljünk el!
## Előfeltételek
Mielőtt elkezdenénk, győződjünk meg arról, hogy minden megvan, ami az oktatóanyag követéséhez szükséges. Íme, amire szüksége lesz:
1.  Aspose.Cells for .NET Library – Letöltheti a[Aspose.Cells for .NET letöltési oldal](https://releases.aspose.com/cells/net/).
2. IDE – Bármilyen .NET fejlesztői környezet, például a Visual Studio.
3. Alapszintű C# ismerete – Ismernie kell a C# programozási nyelvet és a .NET alkalmazásokkal való munkát.
Ügyeljen arra, hogy az Aspose.Cells legújabb verzióját is telepítse, közvetlenül letöltve vagy a NuGet Package Manager használatával a Visual Studioban.
## Csomagok importálása
A kezdéshez feltétlenül importálja a szükséges csomagokat. Ez elengedhetetlen az Excel-fájlokkal való munkavégzéshez és a stílusok programozott alkalmazásához szükséges funkciók eléréséhez.
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
A beállítás végeztével készen állunk az izgalmas részre – a sorok formázására!
Ebben a részben a folyamat egyes lépéseit részletezzük. Minden lépést kódrészletek és részletes magyarázat kísér, így még akkor is könnyedén követheti a lépést, ha még nem ismeri az Aspose.Cells-t.
## 1. lépés: Állítsa be a munkafüzetet és a munkalapot
Mielőtt bármilyen formázást alkalmazna, létre kell hoznia a munkafüzet egy példányát, és el kell érnie az első munkalapot. Ez olyan, mintha kinyitnánk egy üres vásznat a festés megkezdése előtt.
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
// Hozzon létre könyvtárat, ha még nincs jelen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Munkafüzet objektum példányosítása
Workbook workbook = new Workbook();
// Az első (alapértelmezett) munkalap hivatkozásának megszerzése a lapindex átadásával
Worksheet worksheet = workbook.Worksheets[0];
```
Itt létrehozunk egy új munkafüzet objektumot, és lekérjük az első munkalapot. Ezen a lapon alkalmazzuk a formázásunkat.
## 2. lépés: Stílus létrehozása és testreszabása
Most, hogy a munkalap készen van, a következő lépés a sorra alkalmazni kívánt stílusok meghatározása. Kezdjük egy új stílus létrehozásával és olyan tulajdonságok beállításával, mint a betűszín, az igazítás és a szegélyek.
```csharp
// Új stílus hozzáadása a stílusokhoz
Style style = workbook.CreateStyle();
// A szöveg függőleges igazításának beállítása az "A1" cellában
style.VerticalAlignment = TextAlignmentType.Center;
// A szöveg vízszintes igazításának beállítása az "A1" cellában
style.HorizontalAlignment = TextAlignmentType.Center;
// Az "A1" cellában lévő szöveg betűszínének beállítása
style.Font.Color = Color.Green;
```
Ebben a részben beállítjuk a sorban lévő szöveg igazítását (függőleges és vízszintes egyaránt), és megadjuk a betűszínt. Itt kezdheti meg annak meghatározását, hogy a tartalom hogyan jelenjen meg vizuálisan az Excel-lapon.
## 3. lépés: Alkalmazza a Shrink to Fit
Néha a cellában lévő szöveg túl hosszú lehet, ami túlcsordulást okozhat. Egy ügyes trükk az, hogy a szöveget úgy szűkítjük, hogy az olvashatóság megőrzése mellett illeszkedjen a cellába.
```csharp
// A szöveg szűkítése, hogy elférjen a cellában
style.ShrinkToFit = true;
```
 Vel`ShrinkToFit`, biztosítja, hogy a hosszú szöveg átméretezzen a cella határain belülre, így az Excel munkalapja rendezettebbnek tűnik.
## 4. lépés: Állítsa be a sor határait
Annak érdekében, hogy a sorok kiemelkedjenek, a szegélyek alkalmazása nagyszerű lehetőség. Ebben a példában testre szabjuk az alsó szegélyt, színét pirosra, stílusát közepesre állítva.
```csharp
// A cella alsó szegélyének színének beállítása pirosra
style.Borders[BorderType.BottomBorder].Color = Color.Red;
// A cella alsó szegélyének típusának beállítása közepesre
style.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Medium;
```
A szegélyek segíthetnek a tartalom vizuális elkülönítésében, így az adatok könnyebben olvashatóak és esztétikusabbak.
## 5. lépés: Hozzon létre egy StyleFlag objektumot
 A`StyleFlag`Az objektum megmondja az Aspose.Cells-nek, hogy a stílus mely aspektusait kell alkalmazni. Ez lehetővé teszi, hogy pontosan szabályozza, hogy mi kerüljön alkalmazásra, és biztosítja, hogy csak a kívánt formázás legyen beállítva.
```csharp
// StyleFlag létrehozása
StyleFlag styleFlag = new StyleFlag();
styleFlag.HorizontalAlignment = true;
styleFlag.VerticalAlignment = true;
styleFlag.ShrinkToFit = true;
styleFlag.Borders = true;
styleFlag.FontColor = true;
```
Ebben az esetben megadjuk, hogy a vízszintes és függőleges igazítást, a betűszínt, a szöveg zsugorítását és a szegélyeket egyaránt alkalmazni kell.
## 6. lépés: Nyissa meg a kívánt sort
A stílus létrehozása után a következő lépés annak a sornak a elérése, ahol a formázást alkalmazni szeretnénk. Ebben a példában az első sort fogjuk formázni (0. sorindex).
```csharp
// Egy sor elérése a Rows gyűjteményből
Row row = worksheet.Cells.Rows[0];
```
Itt lekérjük a munkalap első sorát. Módosíthatja az indexet bármely másik sor formázásához.
## 7. lépés: Alkalmazza a stílust a sorra
 Végre itt az ideje alkalmazni a stílust a sorra! Használjuk a`ApplyStyle` módszerrel alkalmazhatja a meghatározott stílust a kiválasztott sorra.
```csharp
// A Style objektum hozzárendelése a sor Stílus tulajdonságához
row.ApplyStyle(style, styleFlag);
```
stílust a rendszer most a teljes sorra alkalmazza, így az adatok pontosan úgy néznek ki, ahogyan azt elképzelte.
## 8. lépés: Mentse el a munkafüzetet
Ha végzett a formázással, el kell mentenie a munkafüzetet egy Excel-fájlba. Ez olyan, mintha a módosítások elvégzése után megnyomná a „Mentés” gombot az Excelben.
```csharp
// Az Excel fájl mentése
workbook.Save(dataDir + "book1.out.xls");
```
Most már van egy teljesen formázott Excel munkalapja a megadott könyvtárba mentve!
## Következtetés
Ennyi! Néhány egyszerű lépésben megtanulta, hogyan alkalmazhat formázást egy Excel-sorra programozottan az Aspose.Cells for .NET segítségével. A szövegigazítástól a szegélyek testreszabásáig ez az oktatóanyag bemutatta azokat a lényeges dolgokat, amelyek segítségével professzionális és tetszetős Excel-jelentéseket készíthet programozottan. 
Az Aspose.Cells a lehetőségek széles skáláját kínálja, és az itt bemutatott módszerek egyszerűen kiterjeszthetők bonyolultabb stílusok és formázások alkalmazására az Excel-fájlokra. Akkor miért nem próbálja ki, és tegye közzé adatait?
## GYIK
### Alkalmazhatok különböző stílusokat egymás után az egyes cellákra?  
Igen, különböző stílusokat alkalmazhat az egyes cellákra, ha közvetlenül a következőn keresztül éri el őket`Cells` gyűjtemény ahelyett, hogy a stílust a teljes sorra alkalmazná.
### Alkalmazható-e feltételes formázás az Aspose.Cells segítségével?  
Teljesen! Az Aspose.Cells támogatja a feltételes formázást, lehetővé téve a cellaértékeken alapuló szabályok meghatározását.
### Hogyan alkalmazhatok formázást több sorra?  
 Több sorban is lépkedhet az a segítségével`for` hurok, és ugyanazt a stílust alkalmazza minden sorra külön-külön.
### Az Aspose.Cells támogatja a stílusok alkalmazását teljes oszlopokra?  
 Igen, hasonlóan a sorokhoz, az oszlopokhoz a`Columns` összegyűjteni és stílusokat alkalmazni rájuk.
### Használhatom az Aspose.Cells-t .NET Core alkalmazásokkal?  
Igen, az Aspose.Cells teljes mértékben kompatibilis a .NET Core programmal, így különböző platformokon is használható.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
