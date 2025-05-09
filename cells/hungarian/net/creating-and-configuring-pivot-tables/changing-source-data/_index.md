---
"description": "Tanulja meg, hogyan módosíthatja a kimutatástábla forrásadatait programozottan az Aspose.Cells for .NET használatával átfogó, lépésről lépésre bemutató oktatóanyagunkkal."
"linktitle": "A pivot tábla forrásadatainak programozott módosítása .NET-ben"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "A pivot tábla forrásadatainak programozott módosítása .NET-ben"
"url": "/hu/net/creating-and-configuring-pivot-tables/changing-source-data/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# A pivot tábla forrásadatainak programozott módosítása .NET-ben

## Bevezetés
Az adatelemzés világában kevés eszköz ragyog olyan fényesen, mint a Microsoft Excel. Nap mint nap számtalan felhasználó támaszkodik az Excelre az adatok kezeléséhez és elemzéséhez, de a színfalak mögött ez sokkal összetettebb, mint a kattintás és a húzás. Ha valaha is szerettél volna programozottan manipulálni az Excel-fájlokat – konkrétan egy pivottábla forrásadatait –, akkor jó helyen jársz! Ebben az útmutatóban megvizsgáljuk, hogyan érheted el ezt az Aspose.Cells for .NET használatával. Akár tapasztalt fejlesztő vagy, akár csak most ismerkedsz a programozás tengerével, ez az oktatóanyag tele van értékes információkkal, amelyek könnyen követhetők.
## Előfeltételek
Mielőtt belekezdenénk a pivot tábla forrásadatainak módosításába, győződjünk meg róla, hogy minden be van állítva és készen áll a használatra:
1. Visual Studio: Győződjön meg róla, hogy telepítve van a Microsoft Visual Studio egy példánya, mivel ide fogjuk írni a kódot.
2. Aspose.Cells könyvtár: Le kell töltened az Aspose.Cells könyvtárat, és hivatkoznod kell rá a projektedben. Letöltheted [itt](https://releases.aspose.com/cells/net/).
3. C# alapismeretek: Bár ez az oktatóanyag leegyszerűsített, a C# ismerete segít jobban megérteni a kódot.
4. Excel fájl: Kell egy minta Excel fájlod (például "Book1.xlsx"), amely egy általunk manipulálható kimutatástáblát tartalmaz.
Rendben, ha ezeket az előfeltételeket ellenőriztük, folytathatjuk a szükséges csomagok importálását és a kódolás megkezdését!
## Csomagok importálása
Először is importáljuk a szükséges csomagokat. Nyissuk meg a C# projektünket a Visual Studio-ban, és adjuk hozzá a következőket direktívák használatával a kódfájl elejéhez:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Ezek a névterek hozzáférést biztosítanak az Excel-fájlokkal való munkához és tartalmuk Aspose.Cells használatával történő kezeléséhez szükséges alapvető osztályokhoz.

Most bontsuk le a folyamatot kezelhető lépésekre. Végigmegyünk egy Excel-fájl megnyitásán, a munkalap módosításán, a kimutatástábla adatforrásának módosításán és az eredmények mentésén.
## 1. lépés: Dokumentumkönyvtár meghatározása
Először meg kell adnia, hogy hol található az Excel-fájl. Módosítsa a `dataDir` változót, amely a „Book1.xlsx” fájlt tartalmazó mappára mutat.
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
```
Ez a sor beállítja azt a könyvtárat, ahol az Excel-fájl tárolva van, így később könnyebben elérhető.
## 2. lépés: Adja meg a bemeneti útvonalat
Következő lépésként hozzunk létre egy karakterláncot, amely megadja a bemeneti Excel-fájl teljes elérési útját:
```csharp
string InputPath = dataDir + "Book1.xlsx";
```
Ez segít a fájlokhoz való hozzáférés egyszerűsítésében; nem kell ugyanazt az elérési utat többször beírnod a kódban.
## 3. lépés: Fájlfolyam létrehozása
Most itt az ideje megnyitni az Excel fájlt. Létrehozunk egy `FileStream` amely lehetővé teszi az Excel fájl tartalmának beolvasását:
```csharp
// Létrehoz egy fájlfolyamot, amely tartalmazza a megnyitni kívánt Excel-fájlt.
FileStream fstream = new FileStream(InputPath, FileMode.Open);
```
Ez a sor olvasási módban nyitja meg a fájlt, lehetővé téve számunkra az adatainak elérését.
## 4. lépés: A munkafüzet betöltése
Miután a fájlfolyam a helyén van, a következő lépés a munkafüzet betöltése:
```csharp
// Az Excel fájl megnyitása a fájlfolyamon keresztül
Workbook workbook = new Workbook(fstream);
```
Ez a parancs betölti az Excel fájlt egy `Workbook` objektum. A betöltés után szükség szerint módosíthatja a fájlt.
## 5. lépés: A munkalap elérése
Ideje belemerülni a részletekbe. Lássuk a munkafüzet első munkalapját:
```csharp
// Az Excel fájl első munkalapjának elérése
Worksheet worksheet = workbook.Worksheets[0];
```
Ez közvetlen hozzáférést biztosít az első munkalapon található adatokhoz, így könnyen módosíthatók.
## 6. lépés: Új adatok feltöltése
Ezután új adatokat szeretnénk beszúrni a cellákba. Ebben a példában néhány mintaadatot fogunk hozzáadni:
```csharp
// Új adatok feltöltése a munkalap celláiba
worksheet.Cells["A9"].PutValue("Golf");
worksheet.Cells["B9"].PutValue("Qtr4");
worksheet.Cells["C9"].PutValue(7000);
```
Itt a „Golf”, a „Qtr4” és az értékeket tesszük közzé. `7000` adott cellákba. Ezeket az értékeket igényei szerint módosíthatja.
## 7. lépés: A megnevezett tartomány módosítása
Most módosítjuk az elnevezett tartományt, amelyre a pivot tábla hivatkozik. Ez egy tartomány létrehozását vagy frissítését jelenti:
```csharp
// A „DataSource” nevű tartomány módosítása
Range range = worksheet.Cells.CreateRange(0,0,9,3);
range.Name = "DataSource";
```
Egy új tartomány definiálásával biztosítjuk, hogy a pivot tábla frissítéskor ezeket az új adatokat használja.
## 8. lépés: Mentse el a módosított Excel-fájlt
Az összes módosítás után kulcsfontosságú a munkád mentése! Mentsük el a módosított munkafüzetet:
```csharp
// A módosított Excel fájl mentése
workbook.Save(dataDir + "output.xls");
```
Ez a parancs új fájlba menti a munkafüzetet, így nem kell felülírni az eredeti fájlt, hacsak nem szeretnéd!
## 9. lépés: Zárja be a fájlfolyamot
Végül elengedhetetlen a fájlfolyam bezárása az összes használt erőforrás felszabadításához:
```csharp
// A fájlfolyam bezárása az összes erőforrás felszabadításához
fstream.Close();
```
Ez a lépés biztosítja, hogy az alkalmazás ne szivárogjon memória, és hatékony maradjon.
## Következtetés
Gratulálunk! Sikeresen módosítottad egy pivot tábla forrásadatait programozottan .NET-ben az Aspose.Cells használatával. Ez a funkció számos lehetőséget nyit meg az Excel-feladatok automatizálására és a munkafolyamatok javítására. Akár pénzügyi jelentéseket frissítesz, akár értékesítési adatokat követsz nyomon, vagy akár csak adathalmazokkal játszol, a programozott beavatkozás rengeteg időt takaríthat meg és csökkentheti a hibák kockázatát.

## GYIK
### Mi az Aspose.Cells?
Az Aspose.Cells egy hatékony .NET könyvtár Excel-fájlokkal való munkához, amely lehetővé teszi a felhasználók számára Excel-dokumentumok programozott létrehozását, módosítását és kezelését.
### Módosíthatom a meglévő pivot táblák forrásadatait ezzel a módszerrel?
Természetesen! Ez a módszer lehetővé teszi a meglévő kimutatástáblák adatforrásának frissítését az Excel-munkafüzetben.
### Telepíteni kell az Office-t az Aspose.Cells használatához?
Nem! Az Aspose.Cells egy önálló függvénykönyvtár, ami azt jelenti, hogy nincs szükség telepített Microsoft Office-ra az Excel fájlok kezeléséhez.
### Ingyenesen használható az Aspose.Cells?
Az Aspose.Cells ingyenes próbaverziót kínál, de a teljes funkcionalitás eléréséhez licencet kell vásárolnia. A részleteket itt találja. [itt](https://purchase.aspose.com/buy).
### Hol találok további példákat és támogatást?
További példákért és támogatásért tekintse meg a [Aspose.Cells dokumentáció](https://reference.aspose.com/cells/net/) és a közösségi fórumuk [itt](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}