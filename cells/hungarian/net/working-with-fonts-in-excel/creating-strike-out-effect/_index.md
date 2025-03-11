---
title: Áthúzási effektus létrehozása szövegen Excelben
linktitle: Áthúzási effektus létrehozása szövegen Excelben
second_title: Aspose.Cells .NET Excel Processing API
description: Ebből a részletes, lépésenkénti oktatóanyagból megtudhatja, hogyan alkalmazhat áthúzási effektust a szövegen az Excelben az Aspose.Cells for .NET segítségével.
weight: 15
url: /hu/net/working-with-fonts-in-excel/creating-strike-out-effect/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Áthúzási effektus létrehozása szövegen Excelben

## Bevezetés
Amikor az Excelről van szó, a vizuális elemek ugyanolyan fontosak, mint maguk az adatok. Akár fontos változtatásokat emel ki, akár olyan elemeket jelöl meg, amelyek már nem relevánsak, a szövegen lévő áthúzási effektus klasszikus módja a táblázatok vizuális megjelenítésének kezelésének. Ebben az útmutatóban végigvezetjük az áthúzási effektus végrehajtásának folyamatán az Excelben az Aspose.Cells for .NET használatával. Ez az oktatóanyag nem csak a szükséges előfeltételeket fedi le, hanem lépésenkénti megközelítést is biztosít annak biztosítására, hogy ezt a hatást könnyedén megismételhesse.
## Előfeltételek
Mielőtt belevágna az oktatóanyagba, győződjön meg arról, hogy a következő előfeltételek teljesülnek:
1. Fejlesztői környezet: Be kell állítania egy .NET fejlesztői környezetet. Ez lehet a Visual Studio vagy bármely más olyan IDE, amely támogatja a .NET fejlesztést.
2. Aspose.Cells for .NET: Győződjön meg arról, hogy az Aspose.Cells telepítve van a projektben. Az alábbi linkről tudod letölteni:[Töltse le az Aspose.Cells-t](https://releases.aspose.com/cells/net/).
3. Alapvető C# ismerete: A C# programozás alapvető ismerete hasznos, mivel a példák C#-ban lesznek kódolva.
4. .NET-keretrendszer: Győződjön meg arról, hogy projektje egy kompatibilis .NET-keretrendszer-verziót céloz meg, általában .NET Core vagy .NET-keretrendszer 4.5 vagy újabb verziót.
## Csomagok importálása
Mielőtt bármilyen kódot írna, importálnia kell a szükséges névtereket az Aspose.Cellsből. Ez kulcsfontosságú a könyvtár által biztosított különféle funkciók eléréséhez. A következőképpen importálhatja a szükséges névtereket:
```csharp
using System.IO;
using Aspose.Cells;
```
Ezekkel az importálásokkal hozzáférhet a munkafüzet, a munkalap és a stílus osztályokhoz, amelyeket az oktatóanyag során használni fog.
Most, hogy elkészítettük a terepet, bontsuk le a folyamatot kezelhető lépésekre. Minden lépést egyértelmű utasítások kísérnek, amelyek végigvezetik Önt a szövegen az Excelben lévő áthúzási hatás létrehozásán.
## 1. lépés: Határozza meg a dokumentumkönyvtárat
Kezdje az Excel-dokumentumok tárolási útvonalának meghatározásával. Ez lesz a kimeneti fájlok mentési helye.
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
```
 Cserélje ki`"Your Document Directory"` a tényleges könyvtár elérési útjával, ahová menteni szeretné az Excel-fájlt. Ez beállítja a kimeneti könyvtárat.
## 2. lépés: Hozza létre a könyvtárat
Ezután meg kell győződnie arról, hogy az előző lépésben megadott könyvtár létezik. Ha nem létezik, akkor programozottan létrehozhatja.
```csharp
// Hozzon létre könyvtárat, ha még nincs jelen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Ez a kód ellenőrzi, hogy létezik-e a könyvtár, és ha nem, létrehozza. Ez segít elkerülni a hibákat, amikor később megpróbálja menteni a fájlt.
## 3. lépés: Példányosítson egy munkafüzet-objektumot
Most itt az ideje egy új munkafüzet objektum létrehozásának. Ez az Excel-fájl alapja, amelybe adatokat adhat hozzá és formátumokat alkalmazhat.
```csharp
// Munkafüzet objektum példányosítása
Workbook workbook = new Workbook();
```
 A`Workbook` osztály egy Excel fájlt jelent. Az osztály példányának létrehozásával lényegében egy új Excel-dokumentumot hoz létre.
## 4. lépés: Új munkalap hozzáadása
Minden munkafüzet több munkalapot is tartalmazhat. Lépjünk tovább, és hozzunk létre egy új munkalapot a munkafüzetünkben.
```csharp
// Új munkalap hozzáadása az Excel objektumhoz
int i = workbook.Worksheets.Add();
```
 A`Add` módszere a`Worksheets` gyűjtemény új munkalapot ad a munkafüzethez, és visszaadja az indexét. 
## 5. lépés: Szerezze meg az új munkalap hivatkozását
Miután elkészítette a munkalapot, hivatkoznia kell rá a jövőbeni műveletekhez.
```csharp
// Az újonnan hozzáadott munkalap hivatkozásának megszerzése a lapindex átadásával
Worksheet worksheet = workbook.Worksheets[i];
```
Itt lekérjük az újonnan létrehozott munkalapot az indexével (`i`). Ez hozzáférést biztosít a munkalap kezeléséhez.
## 6. lépés: Hozzáférés egy cellához
 Hozzá kell férnie a munkalap egy adott cellájához, ahol alkalmazni fogja az áthúzott formátumot. Ebben a példában cellát használunk`A1`.
```csharp
// Az "A1" cella elérése a munkalapról
Aspose.Cells.Cell cell = worksheet.Cells["A1"];
```
 Az Excelben a cellákra az oszlop- és sorazonosítóik hivatkoznak (pl. "A1"). Hivatkozást kapunk a cellára`A1` további manipulációhoz.
## 7. lépés: Adjon értéket a cellához
 Ezután szúrjunk be szöveget a cellába. Azt írjuk, hogy „Hello Aspose!” cellában`A1`.
```csharp
// Némi érték hozzáadása az "A1" cellához
cell.PutValue("Hello Aspose!");
```
 A`PutValue` metódus segítségével karakterlánc-értéket rendelünk a cellához. Ezt a karakterláncot bármire módosíthatja, amit meg szeretne jeleníteni.
## 8. lépés: Szerezze meg a cella stílusát
Most, hogy van szöveg a cellánkban, ideje elérni a cella stílusát, hogy alkalmazzuk a kívánt formázást, beleértve az áthúzási effektust.
```csharp
// A cella stílusának megszerzése
Style style = cell.GetStyle();
```
 A`GetStyle` metódus lekéri a cella aktuális stílusát, lehetővé téve a tulajdonságok, például a betűtípus, a méret és a hatások módosítását.
## 9. lépés: Állítsa be az áthúzási effektust
Alkalmazzuk az áthúzási effektust a cellában lévő szövegre. Módosítjuk a cella betűstílusát.
```csharp
// ExStart:SetStrikeout
// A betűtípus áthúzási hatásának beállítása
style.Font.IsStrikeout = true;
// ExEnd:SetStrikeout
```
 Beállítás által`IsStrikeout` igaz, akkor arra utasítja az Excelt, hogy vizuálisan húzza ki a szöveget a kijelölt cella áthúzásában – hasonlóan ahhoz, mintha vizuálisan jelölne ki valamit a listáról.
## 10. lépés: Alkalmazza a stílust a cellára
A stílus módosítása után vissza kell alkalmazni a cellára, hogy tükrözze a változásokat.
```csharp
// A stílus alkalmazása a cellára
cell.SetStyle(style);
```
 A`SetStyle` metódus frissíti a cellát az új stílussal, amely mostantól tartalmazza az áthúzott formázást.
## 11. lépés: Mentse el az Excel fájlt
 Végül itt az ideje, hogy a munkafüzetet a megadott könyvtárba mentse. Ebben a példában a fájlt a névvel mentjük`book1.out.xls`.
```csharp
// Az Excel fájl mentése
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
 A`Save`módszer 97-2003 Excel formátumban írja a munkafüzetet a lemezre. Szükség esetén különböző formátumokat is megadhat.
## Következtetés
A szövegen áthúzott hatás létrehozása az Excelben az Aspose.Cells for .NET használatával egyszerű folyamat, ha lépésről lépésre bontja le. Ha követi ezt az útmutatót, akkor most már rendelkezik azzal a képességgel, hogy vizuális jelzésekkel bővítse táblázatait, így adatai nemcsak informatívak, hanem vizuálisan is vonzóak.
## GYIK
### Mi az Aspose.Cells?
Az Aspose.Cells egy hatékony könyvtár az Excel-fájlok kezelésére .NET-alkalmazásokban, amely lehetővé teszi Excel-dokumentumok programozott létrehozását, kezelését és konvertálását.
### Használhatom ingyenesen az Aspose.Cells-t?
 Igen, a próbaidőszak alatt ingyenesen használhatod. Ingyenes próbaverzió elérhető a címen[Aspose.Cells ingyenes próbaverzió](https://releases.aspose.com/).
### Hogyan vásárolhatom meg az Aspose.Cells-t?
 Az Aspose.Cells licencet a webhelyükön keresztül vásárolhatja meg[Vásároljon Aspose.Cells-t](https://purchase.aspose.com/buy).
### Vannak példák az Aspose.Cells használatára?
 Igen, rengeteg példát és kódrészletet találhat a[Aspose.Cells Documentation](https://reference.aspose.com/cells/net/).
### Hol kaphatok támogatást az Aspose.Cells-hez?
 Közösségi támogatást és segítséget kaphat a[Aspose fórum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
