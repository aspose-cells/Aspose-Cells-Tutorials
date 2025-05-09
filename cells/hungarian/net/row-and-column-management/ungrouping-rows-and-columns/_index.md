---
"description": "Tanuld meg, hogyan bonthatod szét a sorok és oszlopok csoportosítását Excelben az Aspose.Cells for .NET használatával ezzel az átfogó útmutatóval. Egyszerűsítsd az Excelben végzett adatkezelést."
"linktitle": "Sorok és oszlopok csoportosításának szétválasztása Excelben az Aspose.Cells segítségével"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Sorok és oszlopok csoportosításának szétválasztása Excelben az Aspose.Cells segítségével"
"url": "/hu/net/row-and-column-management/ungrouping-rows-and-columns/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Sorok és oszlopok csoportosításának szétválasztása Excelben az Aspose.Cells segítségével

## Bevezetés
Amikor Excel-fájlok kezeléséről van szó, előfordulhat, hogy olyan helyzetbe kerülünk, amikor sorok és oszlopok csoportosítását kell szétbontani. Akár egy táblázatot tisztítunk, akár adatokat formázunk újra a jobb megjelenítés érdekében, az Aspose.Cells for .NET egy fantasztikus eszköz, amely leegyszerűsíti a folyamatot. Ebben az oktatóanyagban végigvezetlek a sorok és oszlopok csoportosításának lépésein az Excelben az Aspose.Cells használatával. A végére szilárd ismeretekkel fogunk rendelkezni arról, hogyan kell programozottan dolgozni az Excel-fájlokkal.
## Előfeltételek
Mielőtt belemerülnénk a kódba, győződjünk meg róla, hogy mindent beállítottunk. Íme, amire szükséged lesz:
1. Visual Studio: A gépeden telepítve kell lennie a Visual Studio egy működő verziójának. Ha még nincs telepítve, letöltheted innen: [A Visual Studio weboldala](https://visualstudio.microsoft.com/).
2. Aspose.Cells .NET-hez: Le kell töltened az Aspose.Cells könyvtárat. A következő helyről tölthető le: [Aspose Kiadások oldal](https://releases.aspose.com/cells/net/)Győződjön meg arról, hogy rendelkezik a szükséges engedélyekkel, amelyeket megvásárolhat vagy beszerezhet egy [ideiglenes engedély](https://purchase.aspose.com/temporary-license/).
3. C# alapismeretek: A C# programozás alapjainak ismerete segít abban, hogy könnyebben kövesd a feladatot.
Miután mindennel elkészültünk, jöhet a mókás rész: a kód!
## Csomagok importálása
A kezdéshez importálnod kell a szükséges csomagokat a C# projektedbe. Így teheted meg:
1. Nyisd meg a projektedet a Visual Studioban.
2. Adj hozzá egy hivatkozást az Aspose.Cells könyvtárhoz. Ezt úgy teheted meg, hogy jobb gombbal kattintasz a Referenciákra a projektedben, és kiválasztod a Referencia hozzáadása lehetőséget. Keresd meg azt a helyet, ahová az Aspose.Cells DLL-t mentetted.
3. A C# fájl tetejére add hozzá a következőket direktívák használatával:
```csharp
using System.IO;
using Aspose.Cells;
```
Most, hogy minden beállított, nézzük meg a sorok és oszlopok csoportosításának bontásának lépéseit az Excel-táblázatban. 
## 1. lépés: A dokumentumkönyvtár meghatározása
Először meg kell adnia azt a könyvtárat, ahol az Excel-fájl található. Ezt a következőképpen állíthatja be:
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
```
Csere `"Your Document Directory"` a számítógépén található tényleges elérési úttal, ahová az Excel-fájl mentésre került. 
## 2. lépés: Fájlfolyam létrehozása
Ezután létre kell hoznia egy fájlfolyamot az Excel-fájl megnyitásához. Ezt a következőképpen teheti meg:
```csharp
// Létrehoz egy fájlfolyamot, amely tartalmazza a megnyitni kívánt Excel-fájlt.
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
Itt megnyitod a következő nevű fájlt: `book1.xls`Győződjön meg róla, hogy a fájl létezik a megadott könyvtárban, különben „a fájl nem található” hibát kap.
## 3. lépés: Munkafüzet-objektum példányosítása
Most töltsük be az Excel-fájlt egy Workbook objektumba. Ez lehetővé teszi a munkafüzet programozott kezelését:
```csharp
// Workbook objektum példányosítása
// Az Excel fájl megnyitása a fájlfolyamon keresztül
Workbook workbook = new Workbook(fstream);
```
Ezzel a kódsorral sikeresen betöltötted az Excel fájlt a memóriába, és készen állsz a használatára.
## 4. lépés: A munkalap elérése
Miután elkészült a munkafüzet, a következő lépés annak a munkalapnak a elérése, amelyen a sorok és oszlopok csoportosítását szét szeretné bontani. Ezt a következőképpen teheti meg:
```csharp
// Az Excel fájl első munkalapjának elérése
Worksheet worksheet = workbook.Worksheets[0];
```
Ebben az esetben az első munkalapot érjük el. Ha az adatai egy másik munkalapon vannak, ennek megfelelően módosíthatja az indexet.
## 5. lépés: Sorok csoportosításának felbontása
Most jön az izgalmas rész! Bontsuk szét az első hat sort (a 0. sortól az 5. sorig). Használjuk a következő kódot:
```csharp
// Első hat sor csoportosításának felbontása (0-tól 5-ig)
worksheet.Cells.UngroupRows(0, 5);
```
Ez a metódus eltávolítja a megadott sorokra alkalmazott csoportosításokat. Ilyen egyszerű!
## 6. lépés: Oszlopok csoportosításának felbontása
A sorokhoz hasonlóan az oszlopok csoportosítását is szétbonthatja. Így bonthatja szét az első három oszlop csoportosítását (a 0. oszloptól a 2. oszlopig):
```csharp
// Első három oszlop csoportosításának felbontása (0-tól 2-ig)
worksheet.Cells.UngroupColumns(0, 2);
```
## 7. lépés: Mentse el a módosított Excel-fájlt
Miután szétválasztotta a sorok és oszlopok csoportosítását, a következő lépés a módosítások Excel-fájlba való visszamentése. Ezt a következővel teheti meg: `Save` módszer:
```csharp
// A módosított Excel fájl mentése
workbook.Save(dataDir + "output.xls");
```
Ebben a példában a módosított fájlt a következő néven mentjük el: `output.xls`A fájlnevet tetszés szerint módosíthatja.
## 8. lépés: Zárja be a fájlfolyamot
Végül az erőforrások felszabadításához zárja be a fájlfolyamot:
```csharp
// A fájlfolyam bezárása az összes erőforrás felszabadításához
fstream.Close();
```
Ez egy jó gyakorlat annak biztosítására, hogy az alkalmazás ne tartsa meg a fájlkezelőket a szükségesnél tovább.
## Következtetés
És íme! Sikeresen megtanultad, hogyan bonthatod szét a sorok és oszlopok csoportosítását egy Excel-fájlban az Aspose.Cells for .NET segítségével. Mindössze néhány sornyi kóddal jelentős módosításokat végezhetsz az Excel-fájljaidon programozott módon. Akár jelentéseket automatizálsz, akár adatokat készítesz elő elemzésre, ezeknek a technikáknak az elsajátítása rengeteg időt takaríthat meg.
## GYIK
### Mi az Aspose.Cells?
Az Aspose.Cells egy hatékony függvénykönyvtár, amely lehetővé teszi az Excel-fájlok egyszerű kezelését .NET alkalmazásokban, lehetővé téve a táblázatok egyszerű kezelését, konvertálását és létrehozását.
### Szétbonthatom a sorok és oszlopok csoportosítását az Excelben más könyvtárak használatával?
Igen, vannak más könyvtárak is az Excel manipulálásához a .NET-ben, de az Aspose.Cells kiterjedt funkciókat és egyszerű használatot kínál.
### Van mód a változtatások visszavonására mentés után?
Miután mentett egy Excel-fájlt, az előző állapot nem állítható vissza, kivéve, ha az eredeti fájlról biztonsági másolatot készített.
### Hogyan kaphatok támogatást az Aspose.Cells-hez?
Támogatást találhatsz, ha ellátogatsz a következő oldalra: [Aspose támogatási fórum](https://forum.aspose.com/c/cells/9), ahol kérdéseket tehet fel és megoldásokat találhat.
### Használhatom az Aspose.Cells-t licenc nélkül?
Igen, bizonyos korlátozásokkal ingyenesen használhatod az Aspose.Cells-t, és elkezdheted egy [ideiglenes engedély](https://purchase.aspose.com/temporary-license/) a teljes funkcionalitásért.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}