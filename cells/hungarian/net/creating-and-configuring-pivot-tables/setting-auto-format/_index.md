---
title: A kimutatástábla automatikus formátumának programozott beállítása .NET-ben
linktitle: A kimutatástábla automatikus formátumának programozott beállítása .NET-ben
second_title: Aspose.Cells .NET Excel Processing API
description: Ebből a részletes, lépésenkénti oktatóanyagból megtudhatja, hogyan állíthatja be programozottan az Excel kimutatástábláinak automatikus formátumát az Aspose.Cells for .NET használatával.
weight: 18
url: /hu/net/creating-and-configuring-pivot-tables/setting-auto-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# A kimutatástábla automatikus formátumának programozott beállítása .NET-ben

## Bevezetés
Amikor az adatok elemzéséről van szó, az Excel pivot táblái megváltoztathatják a játékot. Lehetővé teszik az adatok dinamikus összegzését és elemzését, így olyan betekintést nyerhet, amelyet szinte lehetetlen manuálisan kinyerni. De mi van akkor, ha automatizálni szeretné a pivot táblák formázását a .NET-ben? Itt megmutatom, hogyan állíthatja be programozottan a pivot tábla automatikus formátumát a hatékony Aspose.Cells .NET könyvtár használatával.
Ebben az útmutatóban megvizsgáljuk a lényeget, végigjárjuk az előfeltételeket, importáljuk a szükséges csomagokat, majd belevágunk egy lépésről lépésre bemutatott oktatóanyagba, amellyel profi módon formázhatja a pivot táblázatokat. Jól hangzik? Egyből ugorjunk be!
## Előfeltételek
Mielőtt elkezdené, győződjön meg arról, hogy mindennel rendelkezik, ami az induláshoz szükséges:
1. .NET fejlesztői környezet: Győződjön meg arról, hogy rendelkezik a Visual Studio (vagy bármely .NET-t támogató IDE) működő példányával.
2.  Aspose.Cells Library: Az Excel-fájlok zökkenőmentes használatához telepítenie kell az Aspose.Cells könyvtárat. Ha még nem tette meg, megragadhatja a[letöltési oldal](https://releases.aspose.com/cells/net/).
3. Alapvető C# ismerete: A C# programozás ismerete segít a lépések jobb megértésében.
4.  Excel-fájl (sablon): Kezdésként szüksége lesz egy Excel-sablonfájlra, amelyet a példánkban dolgozunk fel. Az egyszerűség kedvéért létrehozhat egy mintafájlt, melynek neve`Book1.xls`.
## Csomagok importálása
Az Aspose.Cells használatához a projektben importálnia kell a szükséges csomagokat. A következőképpen állíthatja be ezt a .NET-projektben:
### Hozzon létre egy új projektet
Kezdje egy új .NET-projekt létrehozásával a kívánt IDE-ben. 
### Referenciák hozzáadása
Ügyeljen arra, hogy adjon hivatkozást az Aspose.Cells könyvtárra. Ha letöltötte a könyvtárat, adja hozzá a DLL-eket a kicsomagolásból. Ha NuGetet használ, egyszerűen futtassa:
```bash
Install-Package Aspose.Cells
```
### Névterek importálása
Most a kódfájlban importálnia kell az Aspose.Cells névteret. Ezt úgy teheti meg, hogy hozzáadja a következő sort a C# fájl tetejéhez:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
A lépések elvégzése után készen áll egy kód írására!
Most bontsuk le az Ön által megadott kódot részletes lépésekre, az egyes részek működésének magyarázatával. 
## 1. lépés: Határozza meg a dokumentumkönyvtárat
Kezdésként be kell állítania annak a dokumentumkönyvtárnak az elérési útját, ahol az Excel-fájlok találhatók. Példánkban a következőképpen fogjuk meghatározni:
```csharp
string dataDir = "Your Document Directory";  // Szükség szerint módosítsa
```
 Ez a sor karakterlánc-változót hoz létre`dataDir`amely tartalmazza a dokumentumok elérési útját. Ügyeljen arra, hogy cserélje ki`"Your Document Directory"` a rendszer tényleges elérési útjával.
## 2. lépés: Töltse be a sablonfájlt
Ezután be kell töltenie egy meglévő munkafüzetet, amely tartalmazza a pivot táblát:
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
 Ez a sor inicializál egy újat`Workbook` objektumot a megadott Excel fájl betöltésével. A fájlnak legalább egy pivot táblát kell tartalmaznia, hogy a következő lépések hatékonyak legyenek.
## 3. lépés: Nyissa meg a kívánt munkalapot
Határozza meg, melyik munkalapon kell dolgoznia a pivot tábla eléréséhez. Ebben az esetben csak az elsőt kapjuk:
```csharp
int pivotIndex = 0;  // A Pivot Table indexe
Worksheet worksheet = workbook.Worksheets[0];
```
 Itt,`worksheet` lekéri az első munkalapot a munkafüzetből. A kimutatástábla indexe a következőre van állítva`0`, ami azt jelenti, hogy a munkalap első pivot tábláját érjük el.
## 4. lépés: Keresse meg a Pivot Table-t
Amikor a munkalap készen áll, ideje elérni a kimutatástáblázatot:
```csharp
PivotTable pivotTable = worksheet.PivotTables[pivotIndex];
```
 Ez inicializál egy újat`PivotTable` objektumot úgy, hogy a munkalapról lekéri a pivot táblát a megadott indexen.
## 5. lépés: Állítsa be az Automatikus formátum tulajdonságot
Most térjünk rá a lédús részre: állítsa be a pivot táblázat automatikus formázási beállításait.
```csharp
pivotTable.IsAutoFormat = true; // Automatikus formázás engedélyezése
```
 Ez a sor lehetővé teszi a pivot tábla automatikus formázását. Amikor be van állítva`true`, a pivot tábla automatikusan formázza magát az előre meghatározott stílusok alapján.
## 6. lépés: Válasszon egy adott automatikus formátumtípust
Azt is szeretnénk megadni, hogy a pivot tábla melyik automatikus formázási stílust alkalmazza. Az Aspose.Cells különféle formátumokkal rendelkezik, amelyek közül választhatunk. A következőképpen állíthatja be:
```csharp
pivotTable.AutoFormatType = Aspose.Cells.Pivot.PivotTableAutoFormatType.Report5;
```
 Ezzel a sorral egy adott automatikus formátumtípust rendelünk a pivot táblához.`Report5` csak egy példa egy stílusra; igényeinek megfelelően többféle lehetőség közül választhat. 
## 7. lépés: Mentse el a munkafüzetet
Végül ne felejtse el menteni a munkafüzetet az összes módosítás után:
```csharp
workbook.Save(dataDir + "output.xls");
```
 Ez a kódsor a módosított munkafüzetet egy új, nevű fájlba menti`output.xls` a megadott könyvtárban. A gyönyörűen formázott pivot táblázat megtekintéséhez feltétlenül ellenőrizze ezt a fájlt!
## Következtetés
Gratulálok! Ön éppen most programozott egy Excel pivot táblát automatikus formátumra az Aspose.Cells segítségével a .NET-ben. Ez a folyamat nemcsak időt takarít meg a jelentések elkészítésekor, hanem biztosítja az adatok konzisztenciáját minden futtatáskor. Néhány sornyi kóddal jelentősen javíthatja Excel-fájljait – akár egy digitális bűvész.
## GYIK
### Mi az Aspose.Cells?
Az Aspose.Cells egy hatékony .NET-könyvtár az Excel-fájlok kezeléséhez anélkül, hogy a Microsoft Excel telepítése szükséges lenne.
### Formázhatok több pivot táblát egy munkafüzetben?
Igen, a munkafüzeten belül több pivot table objektumon keresztül is formázza őket egyenként.
### Létezik ingyenes próbaverzió az Aspose.Cells számára?
 Teljesen! Kezdheti egy ingyenes próbaverzióval[itt](https://releases.aspose.com/).
### Mi a teendő, ha a kimutatástáblám formázása nem megfelelő?
Győződjön meg arról, hogy a pivot táblára megfelelően hivatkozik, és létezik az automatikus formázás típusa – ellenkező esetben előfordulhat, hogy visszaáll az alapértelmezett beállításokra.
### Automatizálhatom ezt a folyamatot ütemezett feladatokkal?
Igen! Ha ezt a kódot beépíti egy ütemezett feladatba, akkor rendszeresen automatizálhatja a jelentések létrehozását és formázását.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
