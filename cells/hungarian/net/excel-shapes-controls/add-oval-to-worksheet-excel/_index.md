---
title: Adjon hozzá oválist az Excel munkalaphoz
linktitle: Adjon hozzá oválist az Excel munkalaphoz
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan adhat hozzá oválist egy Excel-munkalaphoz az Aspose.Cells for .NET használatával. Lépésről lépésre, részletes kódmagyarázatokkal.
weight: 17
url: /hu/net/excel-shapes-controls/add-oval-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adjon hozzá oválist az Excel munkalaphoz

## Bevezetés
lenyűgöző és interaktív Excel-fájlok létrehozása nemcsak számokat és képleteket foglalhat magában. Az olyan formák, mint az oválisok, vizuális vonzerőt adhatnak, vagy funkcionális elemeket biztosíthatnak a munkalapokon. Ebben az oktatóanyagban megvizsgáljuk, hogyan használható az Aspose.Cells for .NET oválisok programozott hozzáadásához egy Excel-munkalaphoz. Akár egy kis ízelítőt, akár funkcionalitást szeretne hozzáadni, egy lépésről-lépésre szóló útmutatóval látjuk el, amely mindent lebont.
## Előfeltételek
Mielőtt belemerülne a kódba, néhány dolgot meg kell határoznia:
1.  Aspose.Cells for .NET Library: Letöltheti innen[itt](https://releases.aspose.com/cells/net/) vagy telepítse a NuGet segítségével a Visual Studio-ban.
2. Fejlesztési környezet: AC# IDE, mint a Visual Studio.
3. A C# alapvető ismerete: Ismernie kell a C# alapvető kódolási fogalmait.
 Ne felejtse el beállítani a projektet az Aspose.Cells for .NET könyvtár telepítésével. Ha még nincs jogosítványa, kérheti a[ideiglenes engedély](https://purchase.aspose.com/temporary-license/) vagy használja a[ingyenes próbaverzió](https://releases.aspose.com/) változat.
## Csomagok importálása
Mielőtt bármilyen kódot írna, győződjön meg arról, hogy megadta a szükséges névtereket. Íme a C# kódrészlet, amely biztosítja, hogy a megfelelő könyvtárakat használja:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## 1. lépés: Állítsa be a címtárat
Az ovális Excel-laphoz való hozzáadásának első lépése annak meghatározása, hogy az Excel-fájl hova kerüljön mentésre. Határozzuk meg a könyvtár elérési útját, és győződjön meg arról, hogy a könyvtár létezik, mielőtt elmentené a munkát.

Létrehozunk egy könyvtár elérési utat, és ellenőrizzük, hogy létezik-e. Ha a mappa nem létezik, akkor létrejön.
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
// Hozzon létre könyvtárat, ha még nincs jelen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Ez a lépés kulcsfontosságú, mivel biztosítja, hogy a fájl megfelelő helyre kerüljön mentésre, és a későbbiekben ne ütközzenek fájlelérési problémákba.
## 2. lépés: Új munkafüzet inicializálása
Ezután létre kell hoznunk egy új munkafüzetet, amelybe hozzáadjuk az ovális alakzatainkat. A munkafüzet egy Excel fájlt ábrázol, amelybe tartalmat vagy alakzatokat adhatunk.

 Ebben a lépésben egy új példányt készítünk`Workbook` objektum, amely Excel fájltárolóként fog szolgálni.
```csharp
// Példányosítson egy új munkafüzetet.
Workbook excelbook = new Workbook();
```
## 3. lépés: Adja hozzá az első ovális formát
Most jön a szórakoztató rész – ovális alak hozzáadása a munkalaphoz. Ez az ovális vizuális elemet, például gombot vagy kiemelést jelenthet. Kezdjük azzal, hogy hozzáadjuk az első ovális alakzatot a munkafüzetünk első munkalapjához.

 Itt használjuk a`Shapes.AddOval()` módszer ovális létrehozására a munkalapon egy adott sorban és oszlopban.
```csharp
// Adjon hozzá egy ovális formát.
Aspose.Cells.Drawing.Oval oval1 = excelbook.Worksheets[0].Shapes.AddOval(2, 0, 2, 0, 130, 160);
```
 A belső paraméterek`AddOval()` a következők:
- Az első két szám az ovális bal felső sarkának sorát és oszlopát jelöli.
- A következő két szám az ovális magasságát és szélességét jelenti.
## 4. lépés: Állítsa be az ovális elhelyezését és stílusát
 Az ovális létrehozása után beállíthatjuk a helyzetét, a vonalvastagságot és a vonal stílusát. A`Placement` tulajdonság határozza meg, hogy az ovális hogyan viselkedik, amikor átméretezi vagy áthelyezi a cellákat a munkalapon.

Az oválist szabadon lebegővé tesszük és alakítjuk a megjelenését.
```csharp
// Állítsa be az ovális elhelyezését.
oval1.Placement = PlacementType.FreeFloating;
// Állítsa be a vonalvastagságot.
oval1.Line.Weight = 1;
// Állítsa be az ovális vonal stílusát.
oval1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Ez lehetővé teszi az ovális szabad mozgását a munkalapon belül, vonalvastagsága és stílusa pedig a vizuális konzisztencia érdekében van beállítva.
## 5. lépés: Adjon hozzá egy másik ovális (kör) alakzatot
Miért álljunk meg egynél? Ebben a lépésben egy újabb ovális formát adunk hozzá, ezúttal tökéletes kört hozva létre úgy, hogy a magasság és a szélesség azonos lesz.

Létrehozunk egy másik oválist, más helyre helyezzük, és egyenlő magasság és szélesség beállításával biztosítjuk, hogy kör alakú legyen.
```csharp
// Adjon hozzá egy másik ovális (kör) formát.
Aspose.Cells.Drawing.Oval oval2 = excelbook.Worksheets[0].Shapes.AddOval(9, 0, 2, 15, 130, 130);
```
## 6. lépés: A második ovális stílus kialakítása
Csakúgy, mint korábban, ennek a második oválisnak (vagy körnek) az elhelyezését, súlyát és a vonal stílusát módosítjuk.

Hasonló tulajdonságokat alkalmazunk a második oválra is, hogy megfeleljen az első stílusának.
```csharp
// Állítsa be az ovális elhelyezését.
oval2.Placement = PlacementType.FreeFloating;
// Állítsa be a vonalvastagságot.
oval2.Line.Weight = 1;
// Állítsa be az ovális vonal stílusát.
oval2.Line.DashStyle = MsoLineDashStyle.Solid;
```
## 7. lépés: Mentse el a munkafüzetet
Végül el kell mentenünk a munkafüzetet az imént hozzáadott oválisokkal. A fájl mentése biztosítja, hogy minden módosításunk eltárolásra kerül.

A munkafüzetet a korábban meghatározott könyvtár elérési útjára mentjük.
```csharp
// Mentse el az excel fájlt.
excelbook.Save(dataDir + "book1.out.xls");
```
És ennyi! Sikeresen hozzáadta az oválisokat az Excel-munkalaphoz, és elmentette a fájlt.
## Következtetés
Az Aspose.Cells for .NET segítségével alakzatok, például oválisok hozzáadása egy Excel-laphoz nem csak egyszerű, hanem szórakoztató módszer is a táblázatok további vizuális elemekkel való bővítésére. Akár tervezési célból, akár kattintható elemek hozzáadásával, az alakzatok jelentős szerepet játszhatnak az Excel-fájlok megjelenésében és működésében. Tehát, amikor legközelebb olyan projekten dolgozik, amely interaktív vagy tetszetős Excel-lapokat igényel, pontosan tudja, hogyan kell hozzáadni a tökéletes oválisokat!
## GYIK
### Hozzáadhatok más alakzatokat, például téglalapokat vagy vonalakat az Aspose.Cells for .NET használatával?
 Igen, a segítségével különféle alakzatokat, például téglalapokat, vonalakat és nyilakat adhat hozzá`Shapes` gyűjtemény az Aspose.Cells-ben.
### Lehetséges-e átméretezni az oválisokat a hozzáadás után?
Teljesen! Hozzáadása után módosíthatja az oválisok magassági és szélességi tulajdonságait.
### Milyen fájlformátumokba menthetem a munkafüzetet az XLS-en kívül?
Az Aspose.Cells több formátumot támogat, többek között az XLSX-et, a CSV-t és a PDF-t.
### Módosíthatom az ovális körvonalának színét?
 Igen, megváltoztathatja az ovális vonal színét a`Line.Color` ingatlan.
### Szükséges-e az Aspose.Cells licence?
 Bár az Aspose.Cells ingyenes próbaverzióval is kipróbálható, szüksége lesz a[engedély](https://purchase.aspose.com/buy) hosszú távú használatra vagy speciális funkciók eléréséhez.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
