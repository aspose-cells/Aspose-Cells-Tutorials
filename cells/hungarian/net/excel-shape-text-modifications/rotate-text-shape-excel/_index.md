---
"description": "Tanuld meg, hogyan forgathatsz szöveget alakzatokkal Excelben az Aspose.Cells for .NET használatával. Kövesd ezt a lépésről lépésre szóló útmutatót a tökéletes Excel-bemutatóhoz."
"linktitle": "Szöveg elforgatása alakzattal az Excelben"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Szöveg elforgatása alakzattal az Excelben"
"url": "/hu/net/excel-shape-text-modifications/rotate-text-shape-excel/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Szöveg elforgatása alakzattal az Excelben

## Bevezetés
Az Excel világában a vizuális ábrázolás ugyanolyan fontos, mint maga az adat. Akár egy jelentést készítesz, akár egy dinamikus irányítópultot tervezel, az információk elrendezése drámaian befolyásolhatja az olvashatóságot és az általános megjelenést. Szóval, szerettél volna már elforgatni a szöveget, hogy stílusosan illeszkedjen az alakzatokhoz? Szerencséd van! Ebben az oktatóanyagban belemerülünk abba, hogyan forgathatod el a szöveget az alakzatokkal az Aspose.Cells for .NET használatával, biztosítva, hogy a táblázataid ne csak informatívak, hanem lenyűgözőek is legyenek.
## Előfeltételek
Mielőtt belekezdenénk, győződjünk meg róla, hogy minden megvan, amire szükséged van:
1. Visual Studio: Győződjön meg róla, hogy a Visual Studio telepítve van a gépén, mivel ott fogjuk írni a kódot.
2. Aspose.Cells .NET-hez: Szükséged lesz az Aspose.Cells könyvtárra. [töltsd le a legújabb verziót itt](https://releases.aspose.com/cells/net/) vagy próbáld ki ingyen egy [ingyenes próba](https://releases.aspose.com/).
3. C# alapismeretek: A C# és a .NET környezet ismerete előnyös, bár minden lépésben végigvezetünk.
4. Excel-fájl: Egy minta Excel-fájl, nevezzük el `sampleRotateTextWithShapeInsideWorksheet.xlsx`, szükséges a kódunk teszteléséhez. Ezt a fájlt egy könnyen elérhető könyvtárba kell helyezni.
Minden készen áll? Fantasztikus! Akkor jöjjön a mókás rész!
## Csomagok importálása
A kezdéshez importálnunk kell a szükséges csomagokat a projektünkbe. Ezt így teheted meg:
### Új projekt létrehozása
1. Nyisd meg a Visual Studio-t.
2. Válassza az „Új projekt létrehozása” lehetőséget.
3. Válaszd a „Konzolalkalmazás” lehetőséget, és a C#-t válaszd ki a kívánt programozási nyelvként.
### Az Aspose.Cells telepítése
Most adjuk hozzá az Aspose.Cells-t a projektedhez. Ezt a NuGet csomagkezelővel teheted meg:
1. Nyissa meg az "Eszközök" menüpontot a felső menüben.
2. Válassza a „NuGet csomagkezelő”, majd a „Megoldáshoz tartozó NuGet csomagok kezelése” lehetőséget.
3. Keresd meg az „Aspose.Cells” kifejezést.
4. Kattintson a „Telepítés” gombra a projekthez való hozzáadáshoz.
### User Directive hozzáadása
A fő C# fájl tetején a következő direktívát kell hozzáadni:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
Most már készen állunk a kódolás elkezdésére!
Bontsuk le a folyamatot könnyen emészthető lépésekre. Így forgathatja el a szöveget alakzatokkal egy Excel-fájlban:
## 1. lépés: Állítsa be a könyvtár elérési útjait
Először is be kell állítania a forrás- és kimeneti könyvtárakat, ahová az Excel-fájljait tárolni fogja. Így teheti meg:
```csharp
//Forráskönyvtár
string sourceDir = "Your Document Directory"; // Állítsa be a dokumentum könyvtárát
//Kimeneti könyvtár
string outputDir = "Your Document Directory"; // Állítsa be a kimeneti könyvtárat
```
Csere `"Your Document Directory"` a tényleges útvonallal, ahol a `sampleRotateTextWithShapeInsideWorksheet.xlsx` a fájl található.
## 2. lépés: Töltse be a minta Excel-fájlt
Most töltsük be a minta Excel fájlt. Ez kulcsfontosságú, mivel a meglévő adatokat szeretnénk manipulálni.
```csharp
//Minta Excel fájl betöltése.
Workbook wb = new Workbook(sourceDir + "sampleRotateTextWithShapeInsideWorksheet.xlsx");
```
## 3. lépés: A munkalap elérése
Miután a fájl betöltődött, hozzá kell férnünk ahhoz a munkalaphoz, amelyet módosítani szeretnénk. Esetünkben ez az első munkalap.
```csharp
//Első munkalap elérése.
Worksheet ws = wb.Worksheets[0];
```
## 4. lépés: Cella módosítása
Következőként módosítunk egy adott cellát, hogy üzenetet jelenítsen meg. Példánkban a B4 cellát fogjuk használni.
```csharp
//Nyisd meg a B4 cellát, és írj bele egy üzenetet.
Cell b4 = ws.Cells["B4"];
b4.PutValue("Text is not rotating with shape because RotateTextWithShape is false.");
```
Ez a lépés a kommunikációról szól – annak biztosítására, hogy aki megnyitja ezt a lapot, megértse, mit módosítunk.
## 5. lépés: Az első alakzat elérése
A szöveg elforgatásához szükségünk van egy alakzatra, amellyel dolgozhatunk. Itt a munkalap első alakzatát fogjuk elérni.
```csharp
//Első alakzat elérése.
Shape sh = ws.Shapes[0];
```
## 6. lépés: Alakzat szövegének igazításának beállítása
Itt történik a varázslat. Módosítjuk az alakzat szövegigazítási tulajdonságait.
```csharp
//Hozzáférés az alakzat szövegének igazításához.
Aspose.Cells.Drawing.Texts.ShapeTextAlignment shapeTextAlignment = sh.TextBody.TextAlignment;
//Ne forgasd el a szöveget az alakzattal együtt a RotateTextWithShape beállítás hamis értékre állításával.
shapeTextAlignment.RotateTextWithShape = false;
```
Beállítással `RotateTextWithShape` A „hamis” beállításnál biztosítjuk, hogy a szöveg függőleges maradjon, és ne forogjon az alakzattal együtt, így minden rendezett és szervezett marad.
## 7. lépés: Mentse el a kimeneti Excel fájlt
Végül mentsük el a módosításokat egy új Excel-fájlba. Így biztosítjuk, hogy ne veszítsük el a szerkesztéseket, és rendezett eredményt kapjunk.
```csharp
//Mentse el a kimeneti Excel fájlt.
wb.Save(outputDir + "outputRotateTextWithShapeInsideWorksheet.xlsx");
```
És ennyi! A kimeneti fájl mentésre került, beleértve a B4 cellában lévő szöveget és az alakzaton végrehajtott módosításokat is.
## 8. lépés: A kód végrehajtása
A te `Main` metódust, csomagold be az összes fenti kódrészletet, és futtasd a projektedet. Figyeld, ahogy a változások megjelennek a kimeneti fájlban!
```csharp
Console.WriteLine("RotateTextWithShapeInsideWorksheet executed successfully.");
```
## Következtetés
Az Aspose.Cells for .NET használatával az Excelben a szöveg alakzatokkal való forgatása elsőre bonyolult folyamatnak tűnhet, de ha részletesen lebontjuk, meglehetősen egyszerűvé válik. Ezeket az egyszerű lépéseket követve testreszabhatod a táblázataidat, hogy professzionálisabbak és vizuálisan vonzóbbak legyenek. Mostantól, akár egy ügyfélnek, akár személyes projektekhez csinálod ezt, mindenki áradozni fog a munkád minőségéről!
## GYIK
### Ingyenesen használhatom az Aspose.Cells-t?
Igen! Használhatod a [ingyenes próba](https://releases.aspose.com/) kipróbálni a könyvtárat.
### Az Excel mely verzióit támogatja az Aspose.Cells?
Az Aspose.Cells számos Excel formátumot támogat, beleértve az XLS, XLSX, CSV és egyebeket.
### Lehetséges a szöveg elforgatása alakzatokkal régebbi Excel verziókban?
Igen, a funkció alkalmazható az Aspose.Cells által támogatott régebbi formátumokra is.
### Hol találok további dokumentációt az Aspose.Cells-ről?
Átfogó áttekintést nyújthat [dokumentáció](https://reference.aspose.com/cells/net/) további információkért.
### Hogyan kaphatok támogatást az Aspose.Cells-hez?
Támogatást kérhetsz a következő címen: [Aspose fórum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}