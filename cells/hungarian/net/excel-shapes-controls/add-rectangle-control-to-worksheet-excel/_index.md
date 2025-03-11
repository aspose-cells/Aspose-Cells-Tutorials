---
title: Adja hozzá a Téglalap vezérlőelemet az Excel munkalapjához
linktitle: Adja hozzá a Téglalap vezérlőelemet az Excel munkalapjához
second_title: Aspose.Cells .NET Excel Processing API
description: Részletes, lépésenkénti útmutatóból megtudhatja, hogyan adhat hozzá téglalap vezérlőt egy Excel-munkalaphoz az Aspose.Cells for .NET segítségével.
weight: 25
url: /hu/net/excel-shapes-controls/add-rectangle-control-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adja hozzá a Téglalap vezérlőelemet az Excel munkalapjához

## Bevezetés
Ha az Excel-feladatok automatizálásáról van szó, az Aspose.Cells for .NET egy hatékony eszköz, amellyel számos célt elérhet, amelyek közül az egyik az, hogy alakzatokat, például téglalapokat ad hozzá a munkalapokhoz. Ebben az útmutatóban megvizsgáljuk, hogyan adhatunk téglalap vezérlőt egy Excel-munkalaphoz az Aspose.Cells for .NET segítségével. A végére létrehozhat, testreszabhat és menthet egy munkalapot, amelybe egy téglalap alakú vezérlőelem van beágyazva.
De mielőtt belemerülnénk, beszéljünk az előfeltételekről.
## Előfeltételek
Az oktatóanyag követéséhez győződjön meg arról, hogy a következő előfeltételeket teljesíti:
1.  Aspose.Cells .NET könyvtárhoz: Ha még nem tette meg,[töltse le a könyvtárat](https://releases.aspose.com/cells/net/) vagy telepítse a NuGet segítségével a Visual Studio-ban.
2. .NET-keretrendszer: A .NET fejlesztői környezetet be kell állítani a gépen.
3. C# alapismeretek: Bár lépésről lépésre végigvezetjük Önt, a C# és az objektum-orientált programozás alapismerete előnyös.
4.  Licenc: Az Aspose.Cells kiértékelési módban történő használata jól működik az alapvető feladatokhoz, de a teljes funkcionalitás érdekében fontolja meg egy[ideiglenes engedély](https://purchase.aspose.com/temporary-license/)vagy vásárol egyet innen[itt](https://purchase.aspose.com/buy).
Most pedig merüljünk el a kódban!
## Csomagok importálása
Az Aspose.Cells használatának megkezdéséhez győződjön meg arról, hogy a szükséges névtereket importálta a projektbe. Ezek az importálások lehetővé teszik a hozzáférést különböző osztályokhoz és metódusokhoz, amelyekre szüksége van az Excel-fájlokkal való interakcióhoz.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Ezek a sorok biztosítják, hogy a projekt kölcsönhatásba tudjon lépni a fájlkönyvtárakkal (`System.IO`), Excel munkafüzetek (`Aspose.Cells`), és alakrajz (`Aspose.Cells.Drawing`).
Most bontsuk le a folyamatot egyszerű lépésekre, így könnyedén követheti és megismételheti ezt saját projektjeiben.
## 1. lépés: A címtár elérési útjának beállítása
Az első dolog, amit meg kell tennie, hogy meghatározza azt a könyvtárat, ahová az Excel fájl mentésre kerül. Ez a lépés biztosítja, hogy a projekt tudja, hol kell létrehozni és tárolni a kimeneti fájlt.
### Az adatkönyvtár meghatározása
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
```
 Itt adja meg az Excel fájl tárolási útvonalát. Cserélheted`"Your Document Directory"` a gép tényleges elérési útjával, vagy dinamikusan hozzon létre egy mappát, ha nem létezik.
### A címtár ellenőrzése és létrehozása
```csharp
// Hozzon létre könyvtárat, ha még nincs jelen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Ez a blokk ellenőrzi, hogy létezik-e a könyvtár. Ha nem, akkor létrehoz egyet. Gondoljon erre úgy, mintha az irattárat készen tartaná, mielőtt bármilyen dokumentumot tárolna.
## 2. lépés: Új munkafüzet példányosítása
 Ebben a lépésben új Excel-munkafüzetet hoz létre a`Aspose.Cells.Workbook` osztály. Ez a munkalap és az alakzatok tárolójaként fog szolgálni.
```csharp
// Példányosítson egy új munkafüzetet.
Workbook excelbook = new Workbook();
```
 Felhívva a`Workbook` konstruktor, most már van egy üres Excel-munkafüzete, amely készen áll a testreszabásra.
## 3. lépés: Téglalap vezérlő hozzáadása
Itt történik a varázslat. Egy téglalap alakzatot ad hozzá a munkafüzet első munkalapjához.
```csharp
// Adjon hozzá egy téglalap vezérlőt.
Aspose.Cells.Drawing.RectangleShape rectangle = excelbook.Worksheets[0].Shapes.AddRectangle(3, 0, 2, 0, 70, 130);
```
Bontsuk fel ezt:
- `excelbook.Worksheets[0]`: Ezzel eléri a munkafüzet első munkalapját.
- `.Shapes.AddRectangle(3, 0, 2, 0, 70, 130)`: Ez egy téglalap alakzatot ad a munkalaphoz. Az itt található paraméterek határozzák meg a téglalap helyzetét (sor és oszlop), valamint szélességét és magasságát.
## 4. lépés: A téglalap testreszabása
Nem elég egy téglalap hozzáadása – érdemes személyre szabni. Ebben a lépésben beállítjuk a téglalap elhelyezését, vonalvastagságát és kötőjelstílusát.
### Az elhelyezés beállítása
```csharp
// Állítsa be a téglalap elhelyezését.
rectangle.Placement = PlacementType.FreeFloating;
```
Ez azt határozza meg, hogy a téglalap szabadon lebegő, vagyis nem kötődik a cellaméretekhez.
### A vonalvastagság beállítása
```csharp
// Állítsa be a vonalvastagságot.
rectangle.Line.Weight = 4;
```
Itt a téglalap vonalvastagságát 4 pontra állítjuk. Minél nagyobb a szám, annál vastagabb a vonal.
### A Dash stílus beállítása
```csharp
// Állítsa be a téglalap kötőjelstílusát.
rectangle.Line.DashStyle = MsoLineDashStyle.Solid;
```
 Ez a vonal a téglalap szegélyének kötőjelstílusát tömörre állítja. Kísérletezhet különféle stílusokkal, pl`Dash` vagy`Dot` az Ön igényeitől függően.
## 5. lépés: A munkafüzet mentése
A téglalap hozzáadása és testreszabása után az utolsó lépés a munkafüzet mentése a megadott könyvtárba.
```csharp
// Mentse el az excel fájlt.
excelbook.Save(dataDir + "book1.out.xls");
```
 Ezzel a munkafüzetet an`.xls` fájlt a korábban meghatározott mappában. Módosíthatja a fájlformátumot a kiterjesztés megváltoztatásával, pl`.xlsx` ha az újabb Excel formátumot részesíti előnyben.
## Következtetés
És megvan! Egy téglalap vezérlőelem hozzáadása egy Excel-munkalaphoz az Aspose.Cells for .NET használatával egyszerű folyamat, ha lépésről lépésre lebontja. Függetlenül attól, hogy alakzatokat kell hozzáadnia a látványossághoz, kiemelni az adatok részeit, vagy személyre szabni a jelentéseket, az Aspose.Cells rugalmasságot biztosít a programozáshoz.
Ennek az útmutatónak fel kellett volna adnia minden olyan tudást, amelyre szüksége van ahhoz, hogy az Aspose.Cells segítségével téglalapokhoz hasonló alakzatokat adjon az Excel-lapokhoz. Itt az ideje, hogy kísérletezzen, és nézze meg, mit érhet el még ezzel a hatékony könyvtárral!
## GYIK
### Hozzáadhatok más alakzatokat, például köröket vagy vonalakat az Aspose.Cells for .NET használatával?  
Igen, az Aspose.Cells segítségével különféle alakzatokat adhat hozzá, beleértve a köröket, vonalakat, nyilakat stb.
### Milyen egyéb tulajdonságokat állíthatok be a téglalap vezérlőhöz?  
Testreszabhatja a kitöltési színt, a vonal színét, az átlátszóságot, és még szöveget is hozzáadhat a téglalaphoz.
### Az Aspose.Cells kompatibilis a .NET Core-al?  
Igen, az Aspose.Cells támogatja a .NET Core-t, valamint a .NET-keretrendszert és más .NET-alapú platformokat.
### Elhelyezhetem a téglalapot egy adott cellához képest?  
 Igen, elhelyezheti a téglalapot adott sorokba és oszlopokba, vagy használhatja a`PlacementType` rögzítésének szabályozására.
### Létezik ingyenes próbaverzió az Aspose.Cells számára?  
 Igen, kaphat a[ingyenes próbaverzió](https://releases.aspose.com/) a webhelyről, hogy vásárlás előtt tesztelje a könyvtár funkcióit.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
