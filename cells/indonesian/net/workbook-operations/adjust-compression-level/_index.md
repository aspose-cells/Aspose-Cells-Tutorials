---
"description": "Tanulja meg, hogyan állíthatja be az Excel-munkafüzetek tömörítési szintjét az Aspose.Cells for .NET használatával ebből a lépésenkénti útmutatóból. Optimalizálja a fájlkezelést."
"linktitle": "Tömörítési szint beállítása a munkafüzetben"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Tömörítési szint beállítása a munkafüzetben"
"url": "/id/net/workbook-operations/adjust-compression-level/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tömörítési szint beállítása a munkafüzetben

## Bevezetés
Nagyméretű Excel-fájlok kezelésekor a tömörítés gyökeresen megváltoztatja a játékszabályokat. Nemcsak helyet takarít meg, hanem gyorsabbá és hatékonyabbá is teszi a fájlátvitelt. Ha az Aspose.Cells for .NET-tel dolgozol, könnyedén beállíthatod a munkafüzeteid tömörítési szintjét. Ebben az útmutatóban lépésről lépésre végigvezetünk a folyamaton, biztosítva, hogy megértsd a kód minden részét és annak működését.
## Előfeltételek
Mielőtt belemerülnél a kódba, van néhány előfeltétel, aminek teljesülnie kell:
1. C# alapismeretek: A C# programozással való ismeret segít jobban megérteni a kódrészleteket.
2. Aspose.Cells könyvtár: Telepítenie kell az Aspose.Cells könyvtárat. Letöltheti innen: [itt](https://releases.aspose.com/cells/net/).
3. Visual Studio: A kód futtatásához egy fejlesztői környezet, például a Visual Studio szükséges.
4. .NET-keretrendszer: Győződjön meg arról, hogy a projektje a .NET-keretrendszer kompatibilis verziójával van beállítva.
## Csomagok importálása
kezdéshez importálnod kell a szükséges csomagokat a C# projektedbe. Így teheted meg:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```
Ezek a csomagok elengedhetetlenek az Excel fájlokkal való munkához az Aspose.Cells könyvtár használatával. `Aspose.Cells` A névtér tartalmazza az Excel fájlok kezeléséhez szükséges összes osztályt, míg `Aspose.Cells.Xlsb` lehetőséget biztosít a fájlok XLSB formátumban történő mentésére.
Most bontsuk le kezelhető lépésekre a munkafüzet tömörítési szintjének beállítását.
## 1. lépés: Forrás- és kimeneti könyvtárak meghatározása
Először is meg kell adnia, hogy hol találhatók a forrásfájlok, és hová szeretné menteni a kimeneti fájlokat. Ez elengedhetetlen ahhoz, hogy a program tudja, hol találja meg a szükséges fájlokat.
```csharp
// Forráskönyvtár
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```
Csere `"Your Document Directory"` a könyvtárak tényleges elérési útjával. Ez segít a programnak megtalálni a tömöríteni kívánt fájlokat.
## 2. lépés: A munkafüzet betöltése
Ezután betöltöd a tömöríteni kívánt munkafüzetet. Itt kezdődik a varázslat!
```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```
Ebben a sorban létrehozunk egy új példányt a `Workbook` osztályt, és töltsön be egy meglévő Excel fájlt. Győződjön meg arról, hogy a fájlnév megegyezik a forráskönyvtárban található névvel.
## 3. lépés: Mentési beállítások megadása
Most itt az ideje a mentési beállítások konfigurálásának. Beállítjuk a kimeneti fájl tömörítési típusát. 
```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```
A `XlsbSaveOptions` Az osztály lehetővé teszi a munkafüzet XLSB formátumban történő mentésekor különféle beállítások megadását, beleértve a tömörítési szinteket is.
## 4. lépés: Mérje meg az 1. szintű kompressziós időt
Kezdjük az első tömörítési szinttel. Megmérjük, hogy mennyi időbe telik a munkafüzet mentése ezzel a tömörítési szinttel.
```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```
Itt a tömörítési típust 1-es szintre állítjuk, mentjük a munkafüzetet, majd megmérjük az eltelt időt. Ez képet ad arról, hogy mennyi ideig tart a folyamat.
## 5. lépés: Mérje meg a 6. szintű kompressziós időt
Következő lépésként nézzük meg, hogyan teljesít a 6. szintű tömörítés.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level6;
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```
Ez a lépés hasonló az előzőhöz, de a tömörítési szintet 6-os szintre módosítjuk. Észre fogja venni, hogy a szükséges idő a munkafüzet összetettségétől függően változhat.
## 6. lépés: Mérje meg a 9. szintű kompressziós időt
Végül nézzük meg a teljesítményt a legmagasabb tömörítési szinttel.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level9;
workbook.Save(outDir + "LargeSampleFile_level_9_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 9 Elapsed Time: " + elapsedMs);
```
Ebben a lépésben a tömörítési szintet 9-es szintre állítjuk. Általában itt tapasztalható a fájlméret legjelentősebb csökkenése, de a feldolgozás tovább tarthat.
## 7. lépés: Végső kimenet
Az összes tömörítési szint futtatása után egy üzenetet küldhet, amely jelzi, hogy a folyamat sikeresen befejeződött.
```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```
Ez az egyszerű kódsor megerősíti, hogy a programod futása mindenféle probléma nélkül befejeződött.
## Következtetés
munkafüzetek tömörítési szintjének beállítása az Aspose.Cells for .NET segítségével egy egyszerű folyamat, amely jelentős előnyökkel járhat a fájlméret és a teljesítmény tekintetében. Az útmutatóban ismertetett lépéseket követve könnyedén megvalósíthatja a tömörítést az alkalmazásaiban, és javíthatja az Excel fájlkezelés hatékonyságát.
## GYIK
### Mi az Aspose.Cells?  
Az Aspose.Cells egy hatékony .NET könyvtár, amely lehetővé teszi a fejlesztők számára Excel fájlok létrehozását, kezelését és konvertálását Microsoft Excel nélkül.
### Hogyan telepítsem az Aspose.Cells-t?  
Az Aspose.Cells programot letöltheted és telepítheted a következő címről: [Aspose weboldal](https://releases.aspose.com/cells/net/).
### Milyen tömörítési szintek érhetők el?  
Az Aspose.Cells több tömörítési szintet támogat az 1. szinttől (legalacsonyabb tömörítés) a 9. szintig (legmagasabb tömörítés).
### Ingyenesen kipróbálhatom az Aspose.Cells-t?  
Igen! Ingyenes próbaverziót kaphatsz az Aspose.Cells-ből. [itt](https://releases.aspose.com/).
### Hol találok támogatást az Aspose.Cells-hez?  
Bármilyen kérdés vagy támogatás esetén látogassa meg az Aspose támogatási fórumot. [itt](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}