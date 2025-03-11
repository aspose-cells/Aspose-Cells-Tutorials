---
title: A Pivot Table forrásadatainak programozott módosítása .NET-ben
linktitle: A Pivot Table forrásadatainak programozott módosítása .NET-ben
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan módosíthatja programozottan a kimutatási táblázat forrásadatait az Aspose.Cells for .NET használatával átfogó, lépésről lépésre mutató oktatóanyagunkból.
weight: 10
url: /hu/net/creating-and-configuring-pivot-tables/changing-source-data/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# A Pivot Table forrásadatainak programozott módosítása .NET-ben

## Bevezetés
Az adatelemzés világában kevés eszköz ragyog olyan fényesen, mint a Microsoft Excel. Nap mint nap számtalan felhasználó támaszkodik az Excelre az adatok kezelésében és elemzésében, de a színfalak mögött ez sokkal bonyolultabb, mint a kattintás és a húzás. Ha valaha is szerette volna programozottan kezelni az Excel-fájlokat – konkrétan a pivot tábla forrásadatainak módosítására –, akkor jó helyen jár! Ebben az útmutatóban megvizsgáljuk, hogyan érheti el ezt az Aspose.Cells for .NET használatával. Akár tapasztalt fejlesztő, akár csak belemerül a programozás tengerébe, ez az oktatóanyag értékes, könnyen követhető információkkal gazdagodik.
## Előfeltételek
Mielőtt elkezdené a pivot tábla forrásadatainak módosítását, győződjön meg arról, hogy minden be van állítva, és készen áll a használatra:
1. Visual Studio: Győződjön meg arról, hogy telepítve van a Microsoft Visual Studio egy példánya, mivel itt írjuk majd a kódunkat.
2. Aspose.Cells Library: Le kell töltenie az Aspose.Cells könyvtárat, és hivatkoznia kell rá a projektben. Letöltheti[itt](https://releases.aspose.com/cells/net/).
3. Alapvető C# ismerete: Bár ez az oktatóanyag leegyszerűsített, a C# ismerete segít jobban megérteni a kódot.
4. Excel-fájl: rendelkeznie kell egy minta Excel-fájllal (például "Book1.xlsx"), amely tartalmaz egy pivot táblát, amelyet kezelhetünk.
Rendben, ezeknek az előfeltételeknek az ellenőrzésével folytathatjuk a szükséges csomagok importálását és a kódolást!
## Csomagok importálása
Először is – importáljuk a szükséges csomagokat. Nyissa meg C#-projektjét a Visual Studióban, és adja hozzá a következőket a kódfájl tetején található direktívák használatával:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Ezek a névterek hozzáférést biztosítanak az Excel-fájlokkal való munkavégzéshez és azok tartalmának Aspose.Cells segítségével történő kezeléséhez szükséges alapvető osztályokhoz.

Most bontsuk le a folyamatot kezelhető lépésekre. Végigvezetjük az Excel-fájl megnyitását, a munkalap módosítását, a kimutatástábla adatforrásának módosítását és az eredmények mentését.
## 1. lépés: Határozza meg a dokumentumkönyvtárat
 Először is meg kell adnia, hol található az Excel-fájl. Módosítsa a`dataDir` változót, amely a "Book1.xlsx" fájlt tartalmazó mappára mutat.
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
```
Ez a sor beállítja azt a könyvtárat, ahol az Excel-fájlt tárolja, így könnyebben elérhető a későbbiekben.
## 2. lépés: Adja meg a beviteli útvonalat
Ezután hozzunk létre egy karakterláncot, amely megadja a bemeneti Excel-fájl teljes elérési útját:
```csharp
string InputPath = dataDir + "Book1.xlsx";
```
Ez segít a fájlhozzáférés egyszerűsítésében; nem kell ugyanazt az elérési utat többször beírnia a kód során.
## 3. lépés: Fájlfolyam létrehozása
 Most itt az ideje megnyitni az Excel fájlt. Létrehozunk a`FileStream` amely lehetővé teszi az Excel fájl tartalmának olvasását:
```csharp
// A megnyitandó Excel fájlt tartalmazó fájlfolyam létrehozása
FileStream fstream = new FileStream(InputPath, FileMode.Open);
```
Ez a sor megnyitja a fájlt olvasási módban, lehetővé téve számunkra, hogy hozzáférjünk az adataihoz.
## 4. lépés: Töltse be a munkafüzetet
Ha a fájlfolyam a helyén van, a következő lépés a munkafüzet betöltése:
```csharp
// Az Excel fájl megnyitása a fájlfolyamon keresztül
Workbook workbook = new Workbook(fstream);
```
 Ez a parancs veszi az Excel fájlt, és betölti a`Workbook` objektum. Betöltés után szükség szerint módosíthatja a fájlt.
## 5. lépés: Nyissa meg a munkalapot
Ideje belemerülni a részletekbe. Elérjük a munkafüzet első munkalapját:
```csharp
// Az Excel fájl első munkalapjának elérése
Worksheet worksheet = workbook.Worksheets[0];
```
Ez közvetlen hozzáférést biztosít az első munkalapon lévő adatokhoz, így könnyen módosítható.
## 6. lépés: Töltse fel az új adatokat
Ezután új adatokat szeretnénk beszúrni a cellákba. Ebben a példában néhány mintaadatot adunk hozzá:
```csharp
// Új adatok feltöltése a munkalap celláiba
worksheet.Cells["A9"].PutValue("Golf");
worksheet.Cells["B9"].PutValue("Qtr4");
worksheet.Cells["C9"].PutValue(7000);
```
 Itt a „Golf”, „Qtr4” és az értékeket helyezzük el`7000` meghatározott sejtekbe. Ezeket az értékeket az igényeinek megfelelően módosíthatja.
## 7. lépés: Módosítsa az elnevezett tartományt
Most megváltoztatjuk azt a megnevezett tartományt, amelyre a pivot tábla hivatkozik. Ez magában foglalja egy tartomány létrehozását vagy frissítését:
```csharp
// A "DataSource" nevű tartomány módosítása
Range range = worksheet.Cells.CreateRange(0,0,9,3);
range.Name = "DataSource";
```
Egy új tartomány meghatározásával biztosítjuk, hogy a kimutatástábla ezeket az új adatokat használja a frissítés során.
## 8. lépés: Mentse el a módosított Excel-fájlt
Minden változtatás után kulcsfontosságú, hogy megmentse munkáját! Mentsük el a módosított munkafüzetet:
```csharp
// A módosított Excel fájl mentése
workbook.Save(dataDir + "output.xls");
```
Ez a parancs egy új fájlba menti a munkafüzetet, így nem írja felül az eredeti fájlt, hacsak nem akarja!
## 9. lépés: Zárja be a Fájlfolyamot
Végül elengedhetetlen a fájlfolyam bezárása a használt erőforrások felszabadításához:
```csharp
// A fájlfolyam bezárása az összes erőforrás felszabadításához
fstream.Close();
```
Ez a lépés biztosítja, hogy az alkalmazás ne hagyja ki a memóriát, és hatékony maradjon.
## Következtetés
Gratulálok! Sikeresen módosította egy pivot tábla forrásadatait programozottan a .NET-ben az Aspose.Cells használatával. Ez a funkció számos lehetőséget nyit meg az Excel-feladatok automatizálására és a munkafolyamat javítására. Függetlenül attól, hogy frissíti a pénzügyi jelentéseket, nyomon követi az értékesítési adatokat, vagy akár csak játszik az adatkészletekkel, ha ezt programozottan megteheti, rengeteg időt takaríthat meg, és csökkentheti a hibák kockázatát.

## GYIK
### Mi az Aspose.Cells?
Az Aspose.Cells egy hatékony .NET-könyvtár az Excel-fájlokkal való munkavégzéshez, lehetővé téve a felhasználók számára az Excel-dokumentumok programozott létrehozását, módosítását és kezelését.
### Módosíthatom a meglévő pivot táblák forrásadatait ezzel a módszerrel?
Teljesen! Ez a módszer lehetővé teszi az Excel-munkafüzetben lévő meglévő kimutatások adatforrásának frissítését.
### Az Aspose.Cells használatához telepíteni kell az Office-t?
Dehogy! Az Aspose.Cells egy önálló könyvtár, ami azt jelenti, hogy nem kell telepítenie a Microsoft Office-t az Excel-fájlok kezeléséhez.
### Az Aspose.Cells ingyenesen használható?
Az Aspose.Cells ingyenes próbaverziót kínál, de a teljes funkcionalitás érdekében licencet kell vásárolnia. A részleteket megtalálod[itt](https://purchase.aspose.com/buy).
### Hol találhatok további példákat és támogatást?
 További példákért és támogatásért tekintse meg a[Aspose.Cells dokumentáció](https://reference.aspose.com/cells/net/) és közösségi fórumuk[itt](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
