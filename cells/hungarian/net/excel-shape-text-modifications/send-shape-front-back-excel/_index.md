---
"description": "Fedezze fel, hogyan küldhet alakzatokat az Excelben előre vagy hátra az Aspose.Cells for .NET használatával. Ez az útmutató lépésről lépésre bemutatja a tippeket."
"linktitle": "Alakzat küldése előre vagy hátra az Excelben"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Alakzat küldése előre vagy hátra az Excelben"
"url": "/hu/net/excel-shape-text-modifications/send-shape-front-back-excel/"
"weight": 16
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Alakzat küldése előre vagy hátra az Excelben

## Bevezetés
Amikor Excel-fájlokkal dolgozol, előfordulhat, hogy nagyobb kontrollra van szükséged a táblázat vizuális elemei felett. Az alakzatok, például a képek és grafikák, javíthatják az adatok megjelenítését. De mi történik, ha ezek az alakzatok átfedésben vannak, vagy át kell rendezni őket? Itt ragyog az Aspose.Cells for .NET. Ebben az oktatóanyagban végigvezetünk az Excel-munkafüzetben lévő alakzatok manipulálásának lépésein, konkrétan az alakzatok más alakzatok elejére vagy mögé küldésének folyamatán. Ha készen állsz arra, hogy felturbózd az Excel-játékodat, vágjunk bele!
## Előfeltételek
Mielőtt belekezdenénk, néhány dolgot elő kell készíteni:
1. Az Aspose.Cells könyvtár telepítése: Győződjön meg róla, hogy telepítve van az Aspose.Cells .NET könyvtár. Megtalálhatja itt: [itt](https://releases.aspose.com/cells/net/).
2. Fejlesztői környezet: Győződjön meg arról, hogy rendelkezik egy .NET-támogatással rendelkező fejlesztői környezettel, például a Visual Studio-val.
3. C# alapismeretek: A C# programozással való ismeret segít jobban megérteni a kódrészleteket.
Rendben, kipipáltad az összes előfeltételt? Remek! Térjünk át a mókás részre – a kódírásra!
## Csomagok importálása
Mielőtt belevágnánk a tényleges kódolásba, importáljuk a szükséges csomagokat. Ehhez csak adjuk hozzá a következő using direktívát a C# fájl elejéhez:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
Ezek a névterek kulcsfontosságúak, mivel tartalmazzák azokat az osztályokat és metódusokat, amelyeket az Excel-fájlok és -alakzatok kezeléséhez fogunk használni.
## 1. lépés: A fájlútvonalak meghatározása
Ebben az első lépésben létre kell hoznunk a forrás- és kimeneti könyvtárakat. Itt található az Excel-fájl, és ide szeretnéd menteni a módosított fájlt.
```csharp
//Forráskönyvtár
string sourceDir = "Your Document Directory";
//Kimeneti könyvtár
string outputDir = "Your Document Directory";
```
Csere `"Your Document Directory"` az Excel-fájlok tényleges tárolási útvonalával.
## 2. lépés: A munkafüzet betöltése
Most, hogy beállítottuk a könyvtárainkat, töltsük be a munkafüzetet (az Excel fájlt), amely a manipulálni kívánt alakzatokat tartalmazza.
```csharp
//Forrás Excel fájl betöltése
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
Ez a kódsor inicializál egy új `Workbook` objektum, betöltve a megadott Excel fájlt a memóriába, hogy dolgozhassunk vele.
## 3. lépés: A munkalap elérése 
Ezután el kell érnünk azt a munkalapot, amelyen az alakzataink találhatók. Ebben a példában az első munkalapot fogjuk használni.
```csharp
//Első munkalap elérése
Worksheet ws = wb.Worksheets[0];
```
Hivatkozással `Worksheets[0]`, a munkafüzet első munkalapját célozzuk meg. Ha az alakzatok egy másik munkalapon vannak, ennek megfelelően állítsa be az indexet.
## 4. lépés: Hozzáférés az alakzatokhoz
Miután hozzáfértünk a munkalaphoz, válasszuk ki a minket érdeklő alakzatokat. Ebben a példában az első és a negyedik alakzatot fogjuk használni.
```csharp
//Első és negyedik alakzat elérése
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
Ezek a sorok az indexük alapján a munkalapról veszik ki a konkrét alakzatokat.
## 5. lépés: Alakzatok Z-sorrendű pozíciójának kinyomtatása
Mielőtt bármilyen alakzatot áthelyeznénk, nyomtassuk ki az aktuális Z-sorrendű pozíciójukat. Ez segít nyomon követni a pozíciójukat, mielőtt változtatásokat hajtanánk végre.
```csharp
//Az alakzat Z-sorrendű pozíciójának kinyomtatása
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
Hívással `ZOrderPosition`, láthatjuk, hogy az egyes alakzatok hol helyezkednek el a rajzolási sorrendben.
## 6. lépés: Küldd az első alakzatot előre
Most pedig itt az ideje a cselekvésnek! Küldjük az első alakzatot a Z-sor elejére.
```csharp
//Küldje ezt az alakzatot előre
sh1.ToFrontOrBack(2);
```
Elhaladva `2` hogy `ToFrontOrBack`, arra utasítjuk az Aspose.Cells függvényt, hogy ezt az alakzatot hozza előtérbe. 
## 7. lépés: Nyomtassa ki a második alakzat Z-tengelyirányú pozícióját
Mielőtt a második alakzatot hátraküldenénk, ellenőrizzük, hová van elhelyezve.
```csharp
//Az alakzat Z-sorrendű pozíciójának kinyomtatása
Console.WriteLine("Z-Order Shape 4: " + sh4.ZOrderPosition);
```
Ez betekintést nyújt a negyedik alakzat helyzetébe, mielőtt bármilyen változtatást végrehajtanánk.
## 8. lépés: Küldd a negyedik alakzatot hátra
Végül a negyedik alakzatot a Z-Order verem végére küldjük.
```csharp
//Küldje ezt az alakzatot hátra
sh4.ToFrontOrBack(-2);
```
Használat `-2` mivel a paraméter a verem hátulja felé küldi az alakzatot, biztosítva, hogy az ne takarja el a többi alakzatot vagy szöveget.
## 9. lépés: A munkafüzet mentése 
Az utolsó lépés a munkafüzet mentése az újonnan elhelyezett alakzatokkal.
```csharp
//Mentse el a kimeneti Excel fájlt
wb.Save(outputDir + "outputToFrontOrBack.xlsx");
```
Ez a parancs a módosított munkafüzetet a megadott kimeneti könyvtárba menti.
## 10. lépés: Megerősítő üzenet
Végül egy egyszerű visszaigazolással tudassuk velünk, hogy a feladatunk sikeresen befejeződött.
```csharp
Console.WriteLine("SendShapeFrontOrBackInWorksheet executed successfully.\r\n");
```
És ezzel véget is ért a bemutatónk kódja!
## Következtetés
Az alakzatok kezelése az Excelben az Aspose.Cells for .NET segítségével nemcsak egyszerű, de hatékony is. Az útmutató követésével most már könnyedén tud alakzatokat küldeni az elejére vagy a hátuljára, ami lehetővé teszi az Excel-prezentációi feletti jobb irányítást. Ezekkel az eszközökkel készen állsz arra, hogy fokozd a táblázataid vizuális vonzerejét.
## GYIK
### Milyen programozási nyelvre van szükségem az Aspose.Cells-hez?  
C#-t vagy bármilyen .NET által támogatott nyelvet kell használnod az Aspose.Cells használatához.
### Kipróbálhatom ingyen az Aspose.Cells-t?  
Igen, kipróbálhatod az Aspose.Cells ingyenes próbaverzióját. [itt](https://releases.aspose.com/).
### Milyen alakzatokat tudok manipulálni az Excelben?  
Különböző alakzatokat, például téglalapokat, köröket, vonalakat és képeket manipulálhatsz.
### Hogyan kaphatok támogatást az Aspose.Cells-hez?  
Bármilyen segítségért vagy kérdésért látogassa meg közösségi fórumukat [itt](https://forum.aspose.com/c/cells/9).
### Van ideiglenes licenc az Aspose.Cells-hez?  
Igen, kérhet ideiglenes engedélyt [itt](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}