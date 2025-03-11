---
title: Kép elhelyezése (arányos) Excelben
linktitle: Kép elhelyezése (arányos) Excelben
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan helyezheti el arányosan a képeket az Excelben az Aspose.Cells for .NET segítségével. Tegye a táblázatait látványosabbá.
weight: 14
url: /hu/net/excel-ole-picture-objects/position-picture-proportional-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kép elhelyezése (arányos) Excelben

## Bevezetés
Eleged van a pixeles képekből, amelyek úgy tűnik, hogy soha nem férnek el pontosan az Excel-táblázatokban? Képzelje el ezt: van egy gyönyörű logója, amelyet jól láthatóan kell megjeleníteni az Excel-lapon, de végül összenyomódik, megnyúlik vagy rosszul van elhelyezve. Ezt senki sem akarja! Nos, ragaszkodjon a helyéhez, mert ma megtanulja, hogyan helyezze el arányosan a képeket az Excelben az Aspose.Cells könyvtár segítségével a .NET-hez. Ezzel a nagy teljesítményű könyvtárral gyerekjáték az Excel-fájlok kezelése, legyen szó jelentéskészítésről, adatelemzésről vagy csak a prezentációk felfrissítéséről. Merüljünk el a képek tökéletes igazításának aprólékos dolgaiban!
## Előfeltételek
Mielőtt belemerülnénk a tényleges kódolásba, néhány dolgot be kell állítania a gépén:
1. Visual Studio: Győződjön meg arról, hogy telepítve van a Visual Studio, mivel ez kényelmes környezetet biztosít a .NET-projekthez.
2.  Aspose.Cells Library: Szüksége lesz az Aspose.Cells könyvtárra. Megragadhat egy ingyenes próbaverziót, vagy megvásárolhatja a[Aspose honlapja](https://purchase.aspose.com/buy).
3. Alapvető C# ismerete: A C# programozás egy kis ismerete sokat segít a tárgyalt példák megértésében.
4. Képfájl: Készítsen egy képet (például az emblémáját), amelyet be szeretne szúrni az Excel munkalapba.
Most, hogy minden a helyén van, lássuk a kódolást!
## Csomagok importálása
Az Aspose.Cells használatának megkezdéséhez a projektben importálnia kell az adott névtereket. Ezt a következőképpen teheti meg:
### Hozzon létre egy új projektet
A Visual Studióban hozzon létre egy új projektet:
- Nyissa meg a Visual Studio-t.
- Kattintson az "Új projekt létrehozása" gombra.
- Válassza az „Osztálykönyvtár (.NET-keretrendszer)” vagy a „Konzolalkalmazás” lehetőséget, a preferenciáitól függően.
### Telepítse az Aspose.Cells programot
Az Aspose.Cells csomagot a NuGet segítségével adhatja hozzá a projekthez. Íme, hogyan:
- Kattintson a jobb gombbal a projektre a Solution Explorerben.
- Válassza a "NuGet-csomagok kezelése" lehetőséget.
- Keresse meg az "Aspose.Cells" elemet, és kattintson az "Install" gombra.
### Add Irányelvek használatával
A kódfájl tetején írja be a következő direktívákat:
```csharp
using System.IO;
using Aspose.Cells;
```
Ezek az utasítások hozzáférést biztosítanak az Excel-fájlok kezeléséhez szükséges osztályokhoz.
Most bontsuk ezt le részletes lépésekre a kép sikeres arányos elhelyezéséhez az Excelben.
## 1. lépés: Állítsa be a címtárat
Először is győződjön meg arról, hogy rendelkezik egy kijelölt mappával a dokumentumok számára. A következőképpen hozhat létre könyvtárat, ha nem létezik:
```csharp
string dataDir = "Your Document Directory";
// Hozzon létre könyvtárat, ha még nincs jelen.
bool isExists = System.IO.Directory.Exists(dataDir);
if (!isExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
 Ez a kódrészlet létrehoz egy új könyvtárat (ha nem létezik) az Excel-fájlok tárolására. Csak cseréld ki`"Your Document Directory"` a tényleges elérési úttal, ahová a fájlokat menteni szeretné.
## 2. lépés: Példányosítson munkafüzetet
Ezután hozzunk létre egy új munkafüzetet:
```csharp
Workbook workbook = new Workbook();
```
Ez a sor inicializál egy új munkafüzet-objektumot, így egy üres vásznat kaphat, amelyen dolgozhat.
## 3. lépés: Új munkalap hozzáadása
Most, hogy beállítottuk a munkafüzetünket, adjunk hozzá egy új munkalapot:
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
Ez hozzáad egy új munkalapot, és visszaadja annak indexét, amellyel később manipulálhatjuk.
## 4. lépés: Nyissa meg az új munkalapot
Az újonnan hozzáadott munkalap kezeléséhez hozzá kell férnie:
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
 Jelenleg,`worksheet` lehetővé teszi számunkra, hogy tartalmat és képeket adjunk hozzá az adott laphoz.
## 5. lépés: Helyezze be a képet
Most jön az izgalmas rész! Adjuk hozzá a gyönyörű képedet. Cserélje ki`"logo.jpg"` a képfájl nevével:
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
 Ez a sor hozzáadja a képet az F6 cellához (mivel a sorok és oszlopok nulla indexeltek,`5` a hatodik cellára utal).
## 6. lépés: Nyissa meg a hozzáadott képet
A kép beszúrása után a következőképpen érheti el:
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
Ez lehetővé teszi a kép tulajdonságainak módosítását.
## 7. lépés: Helyezze el arányosan a képet
Most helyezzük el arányosan a képet:
```csharp
picture.UpperDeltaX = 200;
picture.UpperDeltaY = 200;
```
 Itt,`UpperDeltaX` és`UpperDeltaY` állítsa be a kép helyzetét a cella méreteihez képest. Ezeket az értékeket módosíthatja, hogy a kép megfelelő legyen.
## 8. lépés: Mentse el a változtatásokat
Végül mentse el a munkafüzetet az összes módosítás megőrzéséhez:
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
 Ez a sor másként menti a munkafüzetet`book1.out.xls` a kijelölt könyvtárban.
## Következtetés
És megvan! Most tanulta meg, hogyan helyezze el arányosan a képeket az Excelben az Aspose.Cells for .NET segítségével. Nem csak képek beszúrásáról van szó; arról van szó, hogy tökéletesnek tűnjenek a táblázatokban. Ne feledje: egy jól elhelyezett kép jelentősen javíthatja az adatok megjelenítését.
Jó szórakozást kíván a különböző képekkel és elhelyezésekkel való kísérletezéshez, és ne habozzon mélyebben belemerülni az Aspose.Cells által kínált gazdag funkciókba. Az Excel-lapjai komoly átalakítás előtt állnak!
## GYIK
### Mi az Aspose.Cells?
Az Aspose.Cells egy hatékony .NET-könyvtár, amely lehetővé teszi a felhasználók számára, hogy a Microsoft Excel telepítése nélkül hozzanak létre, kezeljenek és konvertáljanak Excel fájlokat.
### Használhatom ingyenesen az Aspose.Cells-t?
 Igen, az Aspose.Cells ingyenes próbaverziót kínál, amelyet letölthet[itt](https://releases.aspose.com/).
### Hol találom a dokumentációt?
 Hozzáférhet az átfogóhoz[dokumentáció](https://reference.aspose.com/cells/net/) mert Aspose.Cells.
### Az Aspose.Cells támogatja az összes képformátumot?
Az Aspose.Cells különféle formátumokat támogat, beleértve a JPEG, PNG, BMP, GIF és TIFF formátumokat.
### Hogyan kaphatok támogatást az Aspose.Cells-hez?
 Bármilyen kérdés esetén keresse fel a[támogatási fórum](https://forum.aspose.com/c/cells/9)ahol felteheti kérdéseit.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
