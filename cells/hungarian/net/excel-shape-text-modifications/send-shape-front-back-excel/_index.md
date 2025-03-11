---
title: Küldje el az alakzatot elöl vagy hátul Excelben
linktitle: Küldje el az alakzatot elöl vagy hátul Excelben
second_title: Aspose.Cells .NET Excel Processing API
description: Fedezze fel, hogyan küldhet alakzatokat előre vagy hátra az Excelben az Aspose.Cells for .NET segítségével. Ez az útmutató lépésről lépésre ismerteti a tippeket.
weight: 16
url: /hu/net/excel-shape-text-modifications/send-shape-front-back-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Küldje el az alakzatot elöl vagy hátul Excelben

## Bevezetés
Amikor Excel-fájlokkal dolgozik, előfordulhat, hogy nagyobb ellenőrzésre van szüksége a táblázat vizuális elemei felett. A formák, például a képek és a grafikák javíthatják az adatok megjelenítését. De mi történik, ha ezek az alakzatok átfedik egymást, vagy át kell rendezni őket? Itt ragyog az Aspose.Cells for .NET. Ebben az oktatóanyagban végigvezetjük az Excel-munkalap alakzatainak kezelésének lépésein, különös tekintettel az alakzatok más alakzatok elejére vagy hátuljára küldésére. Ha készen áll arra, hogy felerősítse Excel-játékát, ugorjon bele!
## Előfeltételek
Mielőtt elkezdenénk, meg kell tennie néhány dolgot:
1.  Az Aspose.Cells Library telepítése: Győződjön meg arról, hogy telepítve van az Aspose.Cells könyvtár a .NET-hez. Megtalálhatod[itt](https://releases.aspose.com/cells/net/).
2. Fejlesztői környezet: Győződjön meg arról, hogy be van állítva .NET-támogatással rendelkező fejlesztői környezet, például a Visual Studio.
3. Alapvető C# ismerete: A C# programozás ismerete segít jobban megérteni a kódrészleteket.
Rendben, bejelölte az összes négyzetet az előfeltételek listáján? Nagy! Térjünk át a szórakoztató részre – írjunk egy kódot!
## Csomagok importálása
Mielőtt belemerülnénk a tényleges kódolásba, importáljuk a szükséges csomagokat. Csak adja hozzá a következőket a C# fájl tetején található direktíva használatával:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
Ezek a névterek kulcsfontosságúak, mivel tartalmazzák azokat az osztályokat és metódusokat, amelyeket az Excel-fájlok és -alakzatok kezeléséhez használunk.
## 1. lépés: Határozza meg a fájl elérési útját
Ebben az első lépésben létre kell hoznunk a forrás- és kimeneti könyvtárat. Itt található az Excel-fájl, és ahová menteni szeretné a módosított fájlt.
```csharp
//Forrás könyvtár
string sourceDir = "Your Document Directory";
//Kimeneti könyvtár
string outputDir = "Your Document Directory";
```
 Cserélje ki`"Your Document Directory"` az Excel-fájlok tárolási útvonalával.
## 2. lépés: Töltse be a munkafüzetet
Most, hogy beállítottuk a könyvtárainkat, töltsük be a munkafüzetet (az Excel-fájlt), amely a módosítani kívánt alakzatokat tartalmazza.
```csharp
//Forrás Excel fájl betöltése
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
 Ez a kódsor inicializál egy újat`Workbook` objektum, a megadott Excel fájl betöltése a memóriába, hogy dolgozhassunk vele.
## 3. lépés: Nyissa meg a munkalapot 
Ezután el kell érnünk azt a konkrét munkalapot, ahol az alakzataink vannak. Ebben a példában az első munkalapot fogjuk használni.
```csharp
//Az első munkalap elérése
Worksheet ws = wb.Worksheets[0];
```
 Hivatkozással`Worksheets[0]`, munkafüzetünk első lapját célozzuk meg. Ha az alakzatok egy másik lapon vannak, állítsa be ennek megfelelően az indexet.
## 4. lépés: Nyissa meg az alakzatokat
Ha készen áll a hozzáférés a munkalaphoz, fogjuk meg a minket érdeklő alakzatokat. Ebben a példában az első és a negyedik alakzatot fogjuk elérni.
```csharp
//Hozzáférés az első és a negyedik alakzathoz
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
Ezek a vonalak az indexük alapján kapják meg a konkrét alakzatokat a munkalapról.
## 5. lépés: Nyomtassa ki az alakzatok Z-rendű pozícióját
Mielőtt bármilyen alakzatot mozgatnánk, nyomtassuk ki az aktuális Z-sorrendű pozíciójukat. Ez segít nyomon követni a helyzetüket, mielőtt változtatásokat hajtunk végre.
```csharp
//Nyomtassa ki az alakzat Z-rendű pozícióját
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
 Hívással`ZOrderPosition`, láthatjuk, hogy az egyes alakzatok hol helyezkednek el a rajzi sorrendben.
## 6. lépés: Küldje el az első alakzatot elöl
Most itt az ideje a cselekvésnek! Küldjük az első alakzatot a Z-rend elejére.
```csharp
//Küldje el ezt a formát előre
sh1.ToFrontOrBack(2);
```
 Áthaladással`2` hogy`ToFrontOrBack`, utasítjuk az Aspose.Cells-t, hogy ezt az alakzatot vigye előtérbe. 
## 7. lépés: Nyomtassa ki a második alakzat Z-rendű pozícióját
Mielőtt a második alakzatot hátraküldené, nézzük meg, hol helyezkedik el.
```csharp
//Nyomtassa ki az alakzat Z-rendű pozícióját
Console.WriteLine("Z-Order Shape 4: " + sh4.ZOrderPosition);
```
Ez betekintést nyújt a negyedik alakzat helyzetébe, mielőtt bármilyen változtatást végzünk.
## 8. lépés: Küldje el a negyedik alakzatot hátra
Végül elküldjük a negyedik alakzatot a Z-Order verem hátuljára.
```csharp
//Küldje el ezt a formát hátra
sh4.ToFrontOrBack(-2);
```
 Használata`-2` mivel a paraméter az alakzatot a verem hátulja felé küldi, biztosítva, hogy ne akadályozza más alakzatokat vagy szöveget.
## 9. lépés: Mentse el a munkafüzetet 
Az utolsó lépés a munkafüzet mentése az újonnan elhelyezett alakzatokkal.
```csharp
//Mentse el a kimeneti Excel fájlt
wb.Save(outputDir + "outputToFrontOrBack.xlsx");
```
Ez a parancs a módosított munkafüzetet a megadott kimeneti könyvtárba menti.
## 10. lépés: Megerősítő üzenet
Végül adjunk egy egyszerű megerősítést, hogy tudassuk, hogy a feladatunk sikeresen befejeződött.
```csharp
Console.WriteLine("SendShapeFrontOrBackInWorksheet executed successfully.\r\n");
```
És ezzel lezárjuk az oktatóprogramunk kódját!
## Következtetés
Az alakzatok kezelése Excelben az Aspose.Cells for .NET használatával nem csak egyszerű, hanem hatékony is. Ha követi ezt az útmutatót, most már könnyedén elküldheti az alakzatokat előre vagy hátra, ami lehetővé teszi az Excel-prezentációk jobb irányítását. Ezekkel a rendelkezésre álló eszközökkel készen áll arra, hogy növelje táblázatai vizuális vonzerejét.
## GYIK
### Milyen programozási nyelvre van szükségem az Aspose.Cells-hez?  
Az Aspose.Cells használatához C#-t vagy bármely .NET által támogatott nyelvet kell használnia.
### Kipróbálhatom az Aspose.Cells-t ingyen?  
 Igen, elkezdheti az Aspose.Cells ingyenes próbaverziójával[itt](https://releases.aspose.com/).
### Milyen alakzatokat kezelhetek az Excelben?  
Különféle alakzatokat, például téglalapokat, köröket, vonalakat és képeket kezelhet.
### Hogyan kaphatok támogatást az Aspose.Cells-hez?  
 Bármilyen támogatásért vagy kérdésért felkeresheti közösségi fórumukat[itt](https://forum.aspose.com/c/cells/9).
### Van ideiglenes licenc az Aspose.Cells számára?  
 Igen, kérhet ideiglenes engedélyt[itt](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
