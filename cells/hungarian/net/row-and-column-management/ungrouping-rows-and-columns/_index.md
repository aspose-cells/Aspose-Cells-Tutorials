---
title: sorok és oszlopok csoportosítása az Excelben az Aspose.Cells segítségével
linktitle: sorok és oszlopok csoportosítása az Excelben az Aspose.Cells segítségével
second_title: Aspose.Cells .NET Excel Processing API
description: Ebből az átfogó útmutatóból megtudhatja, hogyan bonthatja le a sorokat és oszlopokat az Excelben az Aspose.Cells for .NET használatával. Egyszerűsítse Excel adatkezelését.
weight: 15
url: /hu/net/row-and-column-management/ungrouping-rows-and-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# sorok és oszlopok csoportosítása az Excelben az Aspose.Cells segítségével

## Bevezetés
Az Excel fájlok kezelése során előfordulhat, hogy olyan helyzetekbe kerül, amikor sorokat és oszlopokat kell csoportosítania. Akár egy táblázatot tisztít meg, akár újraformázza az adatokat a jobb megjelenítés érdekében, az Aspose.Cells for .NET egy fantasztikus eszköz, amely leegyszerűsíti a folyamatot. Ebben az oktatóanyagban végigvezetem a sorok és oszlopok csoportosításának lépésein az Excelben az Aspose.Cells használatával. A végére alaposan megérti, hogyan kell programozottan dolgozni az Excel-fájlokkal.
## Előfeltételek
Mielőtt belemerülne a kódba, győződjön meg arról, hogy mindent beállított. Íme, amire szüksége lesz:
1.  Visual Studio: A Visual Studio működőképes verziójának telepítve kell lennie a gépére. Ha még nincs meg, letöltheti innen[A Visual Studio webhelye](https://visualstudio.microsoft.com/).
2. Aspose.Cells for .NET: Le kell töltenie az Aspose.Cells könyvtárat. Megragadhatja a[Aspose Releases oldal](https://releases.aspose.com/cells/net/) . Győződjön meg arról, hogy rendelkezik a szükséges licencekkel, amelyek megvásárolhatók vagy beszerezhetők a[ideiglenes engedély](https://purchase.aspose.com/temporary-license/).
3. Alapvető C# ismerete: A C# programozás alapjainak ismerete segít a könnyebb követésben.
Ha minden készen van, ugorhatunk a szórakoztató részbe: a kódba!
## Csomagok importálása
A kezdéshez importálnia kell a szükséges csomagokat a C# projektbe. Íme, hogyan kell csinálni:
1. Nyissa meg projektjét a Visual Studióban.
2. Adjon hozzá egy hivatkozást az Aspose.Cells könyvtárhoz. Ezt úgy teheti meg, hogy jobb gombbal kattint a Referenciákra a projektben, és kiválasztja a Referencia hozzáadása lehetőséget. Keresse meg azt a helyet, ahová az Aspose.Cells DLL-t mentette.
3. Adja hozzá a következőket a C# fájl tetejéhez direktívák segítségével:
```csharp
using System.IO;
using Aspose.Cells;
```
Most, hogy minden be van állítva, nézzük meg a sorok és oszlopok csoportosításának lépéseit az Excel-lapon. 
## 1. lépés: Határozza meg a dokumentumkönyvtárat
Először is meg kell adnia azt a könyvtárat, ahol az Excel fájl található. Ezt a következőképpen állíthatja be:
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
```
 Cserélje ki`"Your Document Directory"` azzal a tényleges elérési úttal a számítógépen, ahová az Excel fájlt menti. 
## 2. lépés: Fájlfolyam létrehozása
Ezután létre kell hoznia egy fájlfolyamot az Excel fájl megnyitásához. Ezt így teheti meg:
```csharp
// A megnyitandó Excel fájlt tartalmazó fájlfolyam létrehozása
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
 Itt megnyitja a nevű fájlt`book1.xls`. Győződjön meg arról, hogy ez a fájl létezik a megadott könyvtárban, különben a fájl nem található hibaüzenetet kap.
## 3. lépés: Példányosítson egy munkafüzet-objektumot
Most töltsük be az Excel fájlt egy munkafüzet objektumba. Ez lehetővé teszi a munkafüzet programozott kezelését:
```csharp
// Munkafüzet objektum példányosítása
// Az Excel fájl megnyitása a fájlfolyamon keresztül
Workbook workbook = new Workbook(fstream);
```
Ezzel a kódsorral sikeresen betöltötte az Excel fájlt a memóriába, és készen áll a használatra.
## 4. lépés: Nyissa meg a munkalapot
A munkafüzet megszerzése után a következő lépés az adott munkalap elérése, amelyen a sorokat és oszlopokat fel szeretné csoportosítani. Ezt a következőképpen teheti meg:
```csharp
// Az Excel fájl első munkalapjának elérése
Worksheet worksheet = workbook.Worksheets[0];
```
Ebben az esetben az első munkalapot érjük el. Ha az adatok egy másik lapon vannak, akkor ennek megfelelően módosíthatja az indexet.
## 5. lépés: Bontsa fel a sorok csoportosítását
Most jön az izgalmas rész! Bontsuk szét az első hat sort (a 0. sortól az 5. sorig). Használja a következő kódot:
```csharp
// Az első hat sor csoportosítása (0-tól 5-ig)
worksheet.Cells.UngroupRows(0, 5);
```
Ez a módszer eltávolít minden olyan csoportosítást, amelyet a megadott sorokra alkalmaztak. Ez olyan egyszerű!
## 6. lépés: Az oszlopok csoportosítása
Csakúgy, mint a sorokat, az oszlopokat is szétválaszthatja. Az első három oszlop csoportosításának megszüntetése (a 0. oszloptól a 2. oszlopig):
```csharp
// Az első három oszlop csoportosításának megszüntetése (0-tól 2-ig)
worksheet.Cells.UngroupColumns(0, 2);
```
## 7. lépés: Mentse el a módosított Excel-fájlt
 Miután megszüntette a sorok és oszlopok csoportosítását, a következő lépés a módosítások visszamentése egy Excel-fájlba. Ezt a`Save` módszer:
```csharp
// A módosított Excel fájl mentése
workbook.Save(dataDir + "output.xls");
```
 Ebben a példában a módosított fájlt a következő néven mentjük`output.xls`. A fájlnevet tetszőlegesre módosíthatja.
## 8. lépés: Zárja be a Fájlfolyamot
Végül az erőforrások felszabadításához zárja be a fájlfolyamot:
```csharp
// A fájlfolyam bezárása az összes erőforrás felszabadításához
fstream.Close();
```
Ez egy jó gyakorlat annak biztosítására, hogy az alkalmazás ne tartsa a szükségesnél hosszabb ideig a fájlkezelőket.
## Következtetés
És megvan! Sikeresen megtanulta, hogyan lehet Excel-fájlban sorokat és oszlopokat csoportosítani az Aspose.Cells for .NET segítségével. Néhány sornyi kóddal jelentős változtatásokat hajthat végre az Excel-fájlokon programozottan. Függetlenül attól, hogy automatizálja a jelentéseket vagy előkészíti az adatokat elemzésre, ezen technikák elsajátításával rengeteg időt takaríthat meg.
## GYIK
### Mi az Aspose.Cells?
Az Aspose.Cells egy hatékony könyvtár az Excel-fájlokkal való munkavégzéshez .NET-alkalmazásokban, lehetővé téve az egyszerű kezelést, konvertálást és táblázatok létrehozását.
### Felbonthatom a sorok és oszlopok csoportosítását az Excelben más könyvtárak használatával?
Igen, más könyvtárak is elérhetők az Excel kezeléséhez a .NET-ben, de az Aspose.Cells kiterjedt szolgáltatásokat és egyszerű használatot kínál.
### Van mód a változtatások visszavonására a mentés után?
Miután mentett egy Excel-fájlt, az előző állapot nem állítható vissza, hacsak nincs biztonsági másolata az eredeti fájlról.
### Hogyan kaphatok támogatást az Aspose.Cells-hez?
 Támogatást találhat, ha ellátogat a[Aspose támogatási fórum](https://forum.aspose.com/c/cells/9), ahol kérdéseket tehet fel és megoldásokat találhat.
### Használhatom az Aspose.Cells-t licenc nélkül?
Igen, bizonyos korlátozásokkal ingyenesen használhatod az Aspose.Cells-t, és kezdheted a[ideiglenes engedély](https://purchase.aspose.com/temporary-license/) a teljes funkcionalitás érdekében.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
