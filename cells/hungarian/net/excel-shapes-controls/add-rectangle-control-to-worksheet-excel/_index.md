---
"description": "Tanuld meg, hogyan adhatsz hozzá egy téglalap vezérlőt egy Excel munkalaphoz az Aspose.Cells for .NET használatával egy részletes, lépésről lépésre szóló útmutató segítségével."
"linktitle": "Téglalapvezérlő hozzáadása a munkalaphoz az Excelben"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Téglalapvezérlő hozzáadása a munkalaphoz az Excelben"
"url": "/hu/net/excel-shapes-controls/add-rectangle-control-to-worksheet-excel/"
"weight": 25
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Téglalapvezérlő hozzáadása a munkalaphoz az Excelben

## Bevezetés
Az Excel-feladatok automatizálása terén az Aspose.Cells for .NET egy hatékony eszköz, amely számos cél elérésében segíthet, például alakzatok, például téglalapok hozzáadása a munkalapokhoz. Ebben az útmutatóban megvizsgáljuk, hogyan adhatunk hozzá téglalap vezérlőt egy Excel-munkalaphoz az Aspose.Cells for .NET segítségével. Végre képes leszel létrehozni, testreszabni és menteni egy olyan munkalapot, amelybe beágyazva van egy téglalap vezérlő.
De mielőtt belevágnánk, beszéljünk az előfeltételekről.
## Előfeltételek
A bemutató követéséhez győződjön meg arról, hogy a következő előfeltételek teljesülnek:
1. Aspose.Cells .NET könyvtárhoz: Ha még nem tette meg, [töltse le a könyvtárat](https://releases.aspose.com/cells/net/) vagy telepítse a NuGet használatával a Visual Studio-ban.
2. .NET-keretrendszer: A .NET fejlesztői környezetnek telepítve kell lennie a gépén.
3. C# alapismeretek: Bár lépésről lépésre vezetünk végig, a C# és az objektumorientált programozás alapvető ismerete előnyös.
4. Licenc: Az Aspose.Cells használata kiértékelési módban jól működik az alapvető feladatokhoz, de a teljes funkcionalitás eléréséhez érdemes lehet beszerezni egy [ideiglenes engedély](https://purchase.aspose.com/temporary-license/) vagy vásároljon egyet innen [itt](https://purchase.aspose.com/buy).
Most pedig merüljünk el a kódban!
## Csomagok importálása
Az Aspose.Cells használatának megkezdéséhez győződj meg róla, hogy importáltad a szükséges névtereket a projektedbe. Ezek az importálások hozzáférést biztosítanak a különféle osztályokhoz és metódusokhoz, amelyekre szükséged van az Excel fájlokkal való interakcióhoz.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Ezek a sorok biztosítják, hogy a projekted interakcióba léphessen a fájlkönyvtárakkal (`System.IO`), Excel-munkafüzetek (`Aspose.Cells`), és alakzatrajzolás (`Aspose.Cells.Drawing`).
Most bontsuk le a folyamatot egyszerű lépésekre, hogy könnyen követhesd és megismételhesd a saját projektjeidben.
## 1. lépés: A könyvtár elérési útjának beállítása
Az első dolog, amit tenned kell, az az, hogy meghatározd azt a könyvtárat, ahová az Excel-fájlod mentésre kerül. Ez a lépés biztosítja, hogy a projekted tudja, hol kell létrehozni és tárolni a kimeneti fájlt.
### Az adatkönyvtár meghatározása
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
```
Itt adhatja meg az Excel-fájl tárolására szolgáló könyvtár elérési útját. Lecserélheti `"Your Document Directory"` a gépeden található tényleges elérési úttal, vagy dinamikusan hozz létre egy mappát, ha az nem létezik.
### A könyvtár ellenőrzése és létrehozása
```csharp
// Hozz létre egy könyvtárat, ha az még nem létezik.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Ez a blokk ellenőrzi, hogy létezik-e a könyvtár. Ha nem, létrehoz egyet. Gondoljon erre úgy, mintha előkészítené az irattárolóját, mielőtt bármilyen dokumentumot tárolna.
## 2. lépés: Új munkafüzet létrehozása
Ebben a lépésben létrehoz egy új Excel-munkafüzetet a következő használatával: `Aspose.Cells.Workbook` osztály. Ez fog tárolóként szolgálni a munkalapodnak és az alakzatoknak.
```csharp
// Hozz létre egy új munkafüzetet.
Workbook excelbook = new Workbook();
```
Azzal, hogy felhívja a `Workbook` konstruktorral most már van egy üres Excel-munkafüzeted, amely készen áll a testreszabásra.
## 3. lépés: Téglalap vezérlő hozzáadása
Itt történik a varázslat. Hozzáadsz egy téglalap alakzatot a munkafüzeted első munkalapjához.
```csharp
// Téglalap vezérlő hozzáadása.
Aspose.Cells.Drawing.RectangleShape rectangle = excelbook.Worksheets[0].Shapes.AddRectangle(3, 0, 2, 0, 70, 130);
```
Bontsuk ezt le:
- `excelbook.Worksheets[0]`Ezzel a munkafüzet első munkalapjához férhet hozzá.
- `.Shapes.AddRectangle(3, 0, 2, 0, 70, 130)`: Ez egy téglalap alakzatot ad hozzá a munkalaphoz. Az itt található paraméterek határozzák meg a téglalap pozícióját (sor és oszlop), valamint szélességét és magasságát.
## 4. lépés: A téglalap testreszabása
Nem elég csak egy téglalapot hozzáadni – érdemes testre szabni. Ebben a lépésben beállítjuk a téglalap elhelyezését, vonalvastagságát és szaggatott vonal stílusát.
### Az elhelyezés beállítása
```csharp
// Állítsa be a téglalap helyét.
rectangle.Placement = PlacementType.FreeFloating;
```
Ez azt határozza meg, hogy a téglalap szabadon lebegő, ami azt jelenti, hogy nem lesznek cellaméretekhez kötve.
### A vonalvastagság beállítása
```csharp
// Állítsa be a vonalvastagságot.
rectangle.Line.Weight = 4;
```
Itt a téglalap vonalvastagságát 4 pontra állítottuk be. Minél nagyobb a szám, annál vastagabb a vonal.
### A kötőjel stílusának beállítása
```csharp
// Állítsa be a téglalap szaggatott vonal stílusát.
rectangle.Line.DashStyle = MsoLineDashStyle.Solid;
```
Ez a vonal a téglalap szegélyének szaggatott stílusát folytonosra állítja. Kísérletezhetsz különböző stílusokkal, például `Dash` vagy `Dot` az igényeidtől függően.
## 5. lépés: A munkafüzet mentése
Miután a téglalapot hozzáadta és testre szabta, az utolsó lépés a munkafüzet mentése a megadott könyvtárba.
```csharp
// Mentse el az excel fájlt.
excelbook.Save(dataDir + "book1.out.xls");
```
Ez a munkafüzetet fájlként menti el. `.xls` fájlt a korábban meghatározott mappában. A fájlformátumot a kiterjesztés módosításával módosíthatja, például `.xlsx` ha az újabb Excel formátumot részesíted előnyben.
## Következtetés
És íme! Egy téglalap vezérlő hozzáadása egy Excel munkalaphoz az Aspose.Cells for .NET segítségével egy egyszerű folyamat, ha lépésről lépésre lebontjuk. Akár alakzatokat kell hozzáadnunk a vizuális megjelenés érdekében, akár az adatok egyes részeit kell kiemelnünk, akár a jelentéseinket kell testre szabnunk, az Aspose.Cells rugalmasságot biztosít ehhez programozott módon.
Ez az útmutató minden szükséges tudással felvértezett ahhoz, hogy elkezdj alakzatokat, például téglalapokat hozzáadni az Excel-táblázataidhoz az Aspose.Cells segítségével. Most itt az ideje kísérletezni, és megnézni, mit érhetsz el még ezzel a hatékony könyvtárral!
## GYIK
### Hozzáadhatok más alakzatokat, például köröket vagy vonalakat az Aspose.Cells for .NET használatával?  
Igen, az Aspose.Cells lehetővé teszi különféle alakzatok hozzáadását, beleértve köröket, vonalakat, nyilakat és egyebeket.
### Milyen egyéb tulajdonságokat állíthatok be a téglalap vezérlőhöz?  
Testreszabhatod a kitöltőszínt, a vonalszínt, az átlátszóságot, sőt szöveget is hozzáadhatsz a téglalapon belül.
### Az Aspose.Cells kompatibilis a .NET Core-ral?  
Igen, az Aspose.Cells támogatja a .NET Core-t, valamint a .NET Frameworköt és más .NET alapú platformokat.
### Elhelyezhetem a téglalapot egy adott cellához képest?  
Igen, a téglalapot elhelyezheti adott sorokba és oszlopokba, vagy használhatja a `PlacementType` hogy szabályozza a rögzítés módját.
### Van ingyenes próbaverzió az Aspose.Cells-hez?  
Igen, kaphatsz egy [ingyenes próba](https://releases.aspose.com/) a weboldalról, hogy vásárlás előtt kipróbálhassa a könyvtár funkcióit.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}