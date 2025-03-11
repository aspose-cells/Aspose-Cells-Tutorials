---
title: Szerezzen be alakzati pontokat az Excelben
linktitle: Szerezzen be alakzati pontokat az Excelben
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan szerezhet be alakzati kapcsolódási pontokat az Excelben az Aspose.Cells for .NET segítségével. Kövesse lépésenkénti útmutatónkat az alakpontok egyszerű kivonásához és programozott megjelenítéséhez.
weight: 11
url: /hu/net/excel-shapes-controls/get-connection-points-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Szerezzen be alakzati pontokat az Excelben

## Bevezetés
Amikor programozottan dolgozunk Excel fájlokkal, gyakran kell interakcióba lépnünk a lapokba ágyazott alakzatokkal. Az egyik legfejlettebb feladat, amelyet elvégezhet, a csatlakozási pontok kinyerése egy alakzatból. A csatlakozási pontok alakzatok csatlakozókkal történő rögzítésére és elrendezésük pontosabb kezelésére szolgálnak. Ha egy alakzat kapcsolódási pontjait szeretné megszerezni az Excelben, akkor az Aspose.Cells for .NET a szükséges eszköz. Ebben az oktatóanyagban lépésről lépésre végigvezetjük Önt ennek eléréséhez.
## Előfeltételek
Mielőtt belemerülne a kódba, győződjön meg arról, hogy rendelkezik a következő előfeltételekkel:
- Aspose.Cells for .NET: Az Aspose.Cells programot telepíteni kell a fejlesztői környezetbe. Ha még nincs meg, megteheti[töltse le a legújabb verziót innen](https://releases.aspose.com/cells/net/).
- Fejlesztői környezet: Győződjön meg arról, hogy rendelkezik működő Visual Studio vagy bármely más .NET-kompatibilis IDE telepítéssel.
- Alapvető C# ismerete: Ez az oktatóanyag feltételezi, hogy rendelkezik a C# programozás és az objektumorientált elvek alapvető ismereteivel.
 Jelentkezni is lehet a[Az Aspose.Cells ingyenes próbaverziója](https://releases.aspose.com/) ha még nem tetted meg. Ezzel hozzáférést biztosít az útmutatóhoz szükséges összes funkcióhoz.

## Csomagok importálása
Az Aspose.Cells használatához a projektben fel kell vennie a szükséges névtereket. A következő importálási utasításokat kell elhelyezni a kód tetején:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Ezek a névterek hozzáférést biztosítanak az Aspose.Cells alapvető funkcióihoz, és lehetővé teszik a munkalapok és alakzatok kezelését.

## Lépésről lépésre egy alakzat kapcsolódási pontjainak megszerzéséhez
Ebben a részben végigvezetjük, hogyan bonthatja ki egy alakzat kapcsolódási pontjait egy Excel-munkalapon. Kövesse gondosan az egyes lépéseket a világos megértés érdekében.
## 1. lépés: Példányosítson egy új munkafüzetet
 Először is létre kell hoznunk egy példányt a`Workbook` osztály. Ez egy Excel-fájlt jelöl az Aspose.Cells-ben. Ha nincs meglévő fájlja, semmi gond – kezdheti egy üres munkafüzettel.
```csharp
// Példányosítson egy új munkafüzetet
Workbook workbook = new Workbook();
```
 Ebben a lépésben létrehoztunk egy üres Excel-munkafüzetet, de betölthet egy meglévőt is, ha átadja a fájl elérési útját a`Workbook` konstruktőr.
## 2. lépés: Nyissa meg az első munkalapot
Ezután el kell érnünk azt a munkalapot, ahol az alakzatokkal szeretnénk dolgozni. Ebben az esetben a munkafüzet első munkalapját használjuk.
```csharp
// Szerezd meg az első munkalapot a munkafüzetben
Worksheet worksheet = workbook.Worksheets[0];
```
 Ez a sor a munkafüzet munkalapgyűjteményének első munkalapját éri el. Ha egy adott lappal dolgozik, lecserélheti az indexet`0` a kívánt indexszel.
## 3. lépés: Új szövegmező hozzáadása (alakzat)
Most adjunk hozzá egy új alakzatot a munkalaphoz. Létrehozunk egy szövegdobozt, amely egy alakzattípus. Más típusú alakzatokat is hozzáadhat, de az egyszerűség kedvéért ebben az oktatóanyagban maradunk egy szövegdoboznál.
```csharp
// Új szövegdoboz hozzáadása a gyűjteményhez
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
Íme, mit tettünk:
-  Hozzáadott egy szövegmezőt a sorhoz`2` , oszlop`1`.
-  Állítsa be a szövegdoboz méreteit`160` egységek szélességében és`200` egységek magasságban.
## 4. lépés: Nyissa meg az Alakzatot az Alakzatgyűjteményből
 Miután hozzáadtuk a szövegdobozt, az a munkalap alakzatgyűjteményének részévé válik. Most elérjük ezt az alakzatot a`Shapes`gyűjtemény.
```csharp
// Hozzáférés az alakzathoz (szövegdoboz) az alakzatgyűjteményből
Shape shape = workbook.Worksheets[0].Shapes[0];
```
Ebben a lépésben lekérjük az első alakzatot (a szövegdobozunkat) a gyűjteményből. Ha több alakzata van, megadhatja az indexet, vagy akár név szerint is megkeresheti az alakzatot.
## 5. lépés: Kapcsolódási pontok lekérése
Most, hogy megvan az alakunk, vegyük ki a kapcsolódási pontjait. Ezeket a pontokat a csatlakozók alakhoz való rögzítésére használják. A`ConnectionPoints` Az alakzat tulajdonsága visszaadja az összes elérhető kapcsolódási pontot.
```csharp
// Szerezzen be minden csatlakozási pontot ebben az alakban
var connectionPoints = shape.ConnectionPoints;
```
Ez az alakzathoz rendelkezésre álló összes csatlakozási pont gyűjteményét adja.
## 6. lépés: Csatlakozási pontok megjelenítése
Végül az egyes csatlakozási pontok koordinátáit szeretnénk megjeleníteni. Itt áthurkoljuk a csatlakozási pontokat, és kinyomtatjuk a konzolra.
```csharp
// Az összes alakpont megjelenítése
foreach (var pt in connectionPoints)
{
    System.Console.WriteLine(string.Format("X = {0}, Y = {1}", pt.X, pt.Y));
}
```
 Ez a ciklus minden kapcsolódási ponton áthalad, és kinyomtatja a`X` és`Y` koordináták. Ez hasznos lehet a hibakereséshez vagy egy alakzat kapcsolódási pontjainak vizuális megerősítéséhez.
## 7. lépés: Végezze el és fejezze be
Miután beállította az összes fenti lépést, futtathatja a kódot. Íme az utolsó sor, amely biztosítja a folyamat sikeres befejezését:
```csharp
System.Console.WriteLine("GetShapeConnectionPoints executed successfully.");
```
Ez a sor egyszerűen egy üzenetet naplóz a konzolon, jelezve, hogy a folyamat befejeződött.

## Következtetés
Ebben az oktatóanyagban bemutattuk, hogyan lehet lekérni egy alakzat kapcsolódási pontjait az Excelben az Aspose.Cells for .NET használatával. A feladatot apró, emészthető lépésekre bontva feltártuk a munkafüzet létrehozásának, az alakzat hozzáadásának és a kapcsolódási pontok kinyerésének folyamatát.
Az alakzatok programozott kezelésének megértésével a lehetőségek világa nyílik meg a dinamikus és interaktív Excel-lapok készítésében. Mindegy, hogy jelentéseket készít, irányítópultokat vagy diagramokat készít, ez a tudás hasznos lesz.
## GYIK
### Mi az a kapcsolódási pont egy alakzatban?
A csatlakozási pont egy adott pont az alakzaton, ahol csatlakozókat csatlakoztathat, vagy más alakzatokhoz kapcsolhatja.
### Lekérhetem a kapcsolódási pontokat egy munkalapon lévő összes alakzathoz?
Igen, az Aspose.Cells lehetővé teszi bármely olyan alakzat csatlakozási pontjainak lekérését, amely támogatja azokat. Egyszerűen lapozzon át az alakzatgyűjteményben a munkalapon.
### Szükségem van engedélyre az Aspose.Cells használatához?
Igen, bár ingyenesen kipróbálhatja, a teljes szolgáltatáshoz licenc szükséges. Tudod[vásároljon itt licencet](https://purchase.aspose.com/buy)vagy kap a[ideiglenes engedély](https://purchase.aspose.com/temporary-license/).
### Hogyan adhatok hozzá különböző típusú alakzatokat az Aspose.Cells-hez?
Használhatja a`Add` módszer alakzatokhoz, például téglalapokhoz, ellipszisekhez stb. Minden alakzatnak sajátos paraméterei vannak, amelyeket személyre szabhat.
### Hogyan tölthetek be egy meglévő Excel-fájlt egy új létrehozása helyett?
 Meglévő fájl betöltéséhez adja át a fájl elérési útját a`Workbook` konstruktor, így:  
```csharp
Workbook workbook = new Workbook("path_to_file.xlsx");
```
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
