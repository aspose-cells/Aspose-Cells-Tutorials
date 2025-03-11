---
title: Forgassa el a szöveget az alakzattal az Excelben
linktitle: Forgassa el a szöveget az alakzattal az Excelben
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan forgathat el szöveget alakzatokkal az Excelben az Aspose.Cells for .NET segítségével. Kövesse ezt a lépésről lépésre útmutatót a tökéletes Excel-prezentáció érdekében.
weight: 12
url: /hu/net/excel-shape-text-modifications/rotate-text-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Forgassa el a szöveget az alakzattal az Excelben

## Bevezetés
Az Excel világában a vizuális megjelenítés ugyanolyan fontos, mint maga az adat. Akár jelentést készít, akár dinamikus irányítópultot tervez, az információk elrendezésének módja drámai hatással lehet az olvashatóságra és az általános megjelenésre. Szóval, szeretted volna elforgatni a szöveget, hogy stílusosan igazítsa az alakzatokhoz? szerencséd van! Ebben az oktatóanyagban belemerülünk abba, hogyan lehet szöveget alakzatokkal forgatni az Aspose.Cells for .NET segítségével, így biztosítva, hogy a táblázatok ne csak tájékozódjanak, hanem lenyűgözőek is.
## Előfeltételek
Mielőtt elkezdenénk, győződjünk meg arról, hogy mindennel megvan, amire szüksége van:
1. Visual Studio: Győződjön meg arról, hogy a Visual Studio telepítve van a gépén, mert ott írjuk majd a kódunkat.
2.  Aspose.Cells for .NET: Szüksége lesz az Aspose.Cells könyvtárra. Tudod[töltse le a legújabb verziót innen](https://releases.aspose.com/cells/net/) vagy próbálja ki ingyen a[ingyenes próbaverzió](https://releases.aspose.com/).
3. Alapvető C# ismerete: Hasznos lesz a C# és a .NET környezet ismerete, bár mi minden lépésnél eligazodunk.
4.  Excel fájl: egy példa Excel fájl, nevezzük`sampleRotateTextWithShapeInsideWorksheet.xlsx`, kódunk teszteléséhez szükséges. Ezt a fájlt egy könnyen elérhető könyvtárba kell helyeznie.
Minden készen van? Fantasztikus! Ugorjunk a szórakoztató részre.
## Csomagok importálása
Az induláshoz importálnunk kell a szükséges csomagokat a projektünkbe. Íme, hogyan kell ezt megtenni:
### Hozzon létre egy új projektet
1. Nyissa meg a Visual Studio-t.
2. Válassza az "Új projekt létrehozása" lehetőséget.
3. Válassza a "Konzolalkalmazás" lehetőséget, és válassza ki a C#-t preferált programozási nyelvként.
### Telepítse az Aspose.Cells programot
Most adjuk hozzá az Aspose.Cells elemet a projekthez. Ezt a NuGet Package Manager segítségével teheti meg:
1. Nyissa meg az "Eszközök" elemet a felső menüben.
2. Válassza a „NuGet Package Manager”, majd a „Manage NuGet Packages for Solution” lehetőséget.
3. Keresse meg az "Aspose.Cells" kifejezést.
4. Kattintson a "Telepítés" gombra, hogy hozzáadja a projekthez.
### Használati irányelv hozzáadása
fő C# fájl tetején hozzá kell adnia a következő direktívát:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
Most már készen állunk a kódolás megkezdésére!
Bontsuk a folyamatot könnyen emészthető lépésekre. Így forgathatja el a szöveget alakzatokkal egy Excel-fájlban:
## 1. lépés: Állítsa be a címtár elérési útjait
Először is be kell állítania a forrás- és kimeneti könyvtárakat, ahol az Excel-fájlokat tárolni fogja. Íme, hogyan:
```csharp
//Forrás könyvtár
string sourceDir = "Your Document Directory"; // Állítsa be a dokumentumkönyvtárat
//Kimeneti könyvtár
string outputDir = "Your Document Directory"; // Állítsa be a kimeneti könyvtárat
```
 Cserélje ki`"Your Document Directory"` a tényleges útvonallal, ahol az Ön`sampleRotateTextWithShapeInsideWorksheet.xlsx` fájl található.
## 2. lépés: Töltse be az Excel mintafájlt
Most töltsük be az Excel mintafájlt. Ez döntő fontosságú, mivel a meglévő adatokat szeretnénk manipulálni.
```csharp
//Töltsön be minta Excel fájlt.
Workbook wb = new Workbook(sourceDir + "sampleRotateTextWithShapeInsideWorksheet.xlsx");
```
## 3. lépés: Nyissa meg a munkalapot
A fájl betöltése után el kell érnünk azt a konkrét munkalapot, amelyet módosítani szeretnénk. Esetünkben ez az első munkalap.
```csharp
//Az első munkalap elérése.
Worksheet ws = wb.Worksheets[0];
```
## 4. lépés: Módosítson egy cellát
Ezután egy adott cellát módosítunk, hogy üzenet jelenjen meg. Példánkban a B4 cellát fogjuk használni.
```csharp
//Nyissa meg a B4 cellát, és adjon hozzá egy üzenetet.
Cell b4 = ws.Cells["B4"];
b4.PutValue("Text is not rotating with shape because RotateTextWithShape is false.");
```
Ez a lépés a kommunikációról szól – annak biztosítása, hogy aki megnyitja ezt a lapot, megértse, mit módosítunk.
## 5. lépés: Nyissa meg az első alakzatot
A szöveg elforgatásához szükségünk van egy alakzatra, amellyel dolgozhatunk. Itt elérjük a munkalap első alakját.
```csharp
//Hozzáférés az első alakzathoz.
Shape sh = ws.Shapes[0];
```
## 6. lépés: Állítsa be az alakzat szövegigazítását
Itt történik a varázslat. Beállítjuk az alakzat szövegigazítási tulajdonságait.
```csharp
//Az alakzat szövegigazításának elérése.
Aspose.Cells.Drawing.Texts.ShapeTextAlignment shapeTextAlignment = sh.TextBody.TextAlignment;
//Ne forgassa el a szöveget alakzattal a RotateTextWithShape beállításával hamis.
shapeTextAlignment.RotateTextWithShape = false;
```
 Beállítás által`RotateTextWithShape` hamisra, biztosítjuk, hogy a szöveg függőleges maradjon, és ne forogjon az alakzattal együtt, így minden rendben és rendezett marad.
## 7. lépés: Mentse el a kimeneti Excel fájlt
Végül mentsük el a változtatásainkat egy új Excel fájlba. Ez biztosítja, hogy ne vesszenek el a szerkesztéseink, és a kimenet rendezett legyen.
```csharp
//Mentse el a kimeneti Excel fájlt.
wb.Save(outputDir + "outputRotateTextWithShapeInsideWorksheet.xlsx");
```
És ennyi! A kimeneti fájl most mentésre került, beleértve a B4 cellában lévő szöveget és az alakzaton végzett módosításokat.
## 8. lépés: Hajtsa végre a kódot
 A tiédben`Main` módszert, csomagolja be az összes fenti kódrészletet, és futtassa a projektet. Lásd a változásokat a kimeneti fájlban!
```csharp
Console.WriteLine("RotateTextWithShapeInsideWorksheet executed successfully.");
```
## Következtetés
Szöveg alakzatokkal történő forgatása az Excelben az Aspose.Cells for .NET használatával elsőre bonyolultnak tűnhet, de ha felbontja, ez meglehetősen egyszerű. Ezeket az egyszerű lépéseket követve személyre szabhatja táblázatait, hogy professzionálisabbak és látványosabbak legyenek. Mostantól függetlenül attól, hogy ezt ügyfeleiért vagy személyes projektjeiért csinálja, mindenki áradozni fog a munkája minőségéről!
## GYIK
### Használhatom ingyenesen az Aspose.Cells-t?
 Igen! Használhatja a[ingyenes próbaverzió](https://releases.aspose.com/) kipróbálni a könyvtárat.
### Az Excel mely verzióit támogatja az Aspose.Cells?
Az Aspose.Cells számos Excel-formátumot támogat, beleértve az XLS-t, az XLSX-et, a CSV-t és még sok mást.
### Lehetséges a szöveg alakzatokkal való elforgatása a régebbi Excel verziókban?
Igen, a funkció alkalmazható az Aspose.Cells által támogatott régebbi formátumokra.
### Hol találok további dokumentációt az Aspose.Cellsről?
 Megtekintheti az átfogó[dokumentáció](https://reference.aspose.com/cells/net/) további betekintésekért.
### Hogyan kaphatok támogatást az Aspose.Cells-hez?
 Támogatást kérhet az alábbi címen[Aspose fórum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
