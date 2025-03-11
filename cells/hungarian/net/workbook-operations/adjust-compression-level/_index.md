---
title: Állítsa be a tömörítési szintet a munkafüzetben
linktitle: Állítsa be a tömörítési szintet a munkafüzetben
second_title: Aspose.Cells .NET Excel Processing API
description: Ebből a lépésenkénti útmutatóból megtudhatja, hogyan állíthatja be az Excel-munkafüzetek tömörítési szintjét az Aspose.Cells for .NET használatával. Optimalizálja a fájlkezelést.
weight: 14
url: /hu/net/workbook-operations/adjust-compression-level/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Állítsa be a tömörítési szintet a munkafüzetben

## Bevezetés
Ha nagy Excel-fájlok kezeléséről van szó, a tömörítés játékmódot jelent. Nemcsak tárhelyet takarít meg, hanem gyorsabbá és hatékonyabbá teszi a fájlátvitelt is. Ha az Aspose.Cells for .NET programmal dolgozik, könnyen beállíthatja a munkafüzetek tömörítési szintjét. Ebben az útmutatóban lépésről lépésre végigvezetjük a folyamaton, biztosítva, hogy megértse a kód egyes részeit és működését.
## Előfeltételek
Mielőtt belemerülne a kódba, meg kell felelnie néhány előfeltételnek:
1. Alapvető C# ismerete: A C# programozás ismerete segít jobban megérteni a kódrészleteket.
2.  Aspose.Cells Library: telepítenie kell az Aspose.Cells könyvtárat. Letöltheti innen[itt](https://releases.aspose.com/cells/net/).
3. Visual Studio: A kód futtatásához olyan fejlesztői környezetre lesz szükség, mint a Visual Studio.
4. .NET-keretrendszer: Győződjön meg arról, hogy projektje a .NET-keretrendszer kompatibilis verziójával van beállítva.
## Csomagok importálása
A kezdéshez importálnia kell a szükséges csomagokat a C# projektbe. A következőképpen teheti meg:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```
 Ezek a csomagok nélkülözhetetlenek az Aspose.Cells könyvtárat használó Excel-fájlok kezeléséhez. A`Aspose.Cells` A névtér tartalmazza az Excel-fájlok kezeléséhez szükséges összes osztályt`Aspose.Cells.Xlsb` lehetőséget biztosít a fájlok XLSB formátumban történő mentésére.
Most bontsuk fel a munkafüzet tömörítési szintjének beállítási folyamatát kezelhető lépésekre.
## 1. lépés: Forrás- és kimeneti könyvtárak meghatározása
Először is meg kell adnia, hogy a forrásfájlok hol találhatók, és hova szeretné menteni a kimeneti fájlokat. Ez döntő fontosságú annak biztosításához, hogy a program tudja, hol találja meg a munkához szükséges fájlokat.
```csharp
// Forrás könyvtár
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```
 Cserélje ki`"Your Document Directory"` a könyvtárak tényleges elérési útjával. Ez segít a programnak megtalálni a tömöríteni kívánt fájlokat.
## 2. lépés: Töltse be a munkafüzetet
Ezután töltse be a tömöríteni kívánt munkafüzetet. Itt kezdődik a varázslat!
```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```
Ebben a sorban létrehozunk egy új példányt a`Workbook` osztályt, és töltsön be egy meglévő Excel fájlt. Győződjön meg arról, hogy a fájlnév megegyezik a forráskönyvtárban található fájlnévvel.
## 3. lépés: Állítsa be a mentési beállításokat
Itt az ideje, hogy konfigurálja a mentési beállításokat. Beállítjuk a kimeneti fájl tömörítési típusát. 
```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```
 A`XlsbSaveOptions` osztály lehetővé teszi különböző beállítások megadását a munkafüzet XLSB formátumban történő mentésekor, beleértve a tömörítési szinteket is.
## 4. lépés: Mérje meg az 1. szint tömörítési idejét
Kezdjük az első tömörítési szinttel. Megmérjük, mennyi ideig tart a munkafüzet mentése ilyen tömörítés mellett.
```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```
Itt a tömörítési típust 1. szintre állítjuk, mentjük a munkafüzetet, majd mérjük az eltelt időt. Ez képet ad arról, hogy mennyi ideig tart a folyamat.
## 5. lépés: Mérje meg a 6. szint tömörítési idejét
Ezután nézzük meg, hogyan működik a 6. szintű tömörítés.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level6;
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```
Ez a lépés hasonló az előzőhöz, de a tömörítési szintet 6-os szintre változtatjuk. Észreveheti, hogy a munkafüzet bonyolultságától függően változhat a szükséges idő.
## 6. lépés: Mérje meg a 9. szint tömörítési idejét
Végül nézzük meg a teljesítményt a legmagasabb tömörítési szinten.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level9;
workbook.Save(outDir + "LargeSampleFile_level_9_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 9 Elapsed Time: " + elapsedMs);
```
Ebben a lépésben a tömörítési szintet 9-es szintre állítjuk. Általában itt tapasztalhatja a legjelentősebb fájlméret-csökkenést, de a feldolgozás tovább tarthat.
## 7. lépés: Végső kimenet
Az összes tömörítési szint futtatása után üzenetet küldhet ki, amely jelzi, hogy a folyamat sikeresen befejeződött.
```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```
Ez az egyszerű kódsor megerősíti, hogy a program végrehajtása probléma nélkül befejeződött.
## Következtetés
munkafüzetek tömörítési szintjének beállítása az Aspose.Cells for .NET segítségével egyszerű folyamat, amely jelentős előnyökhöz vezethet a fájlméret és a teljesítmény tekintetében. Az ebben az útmutatóban vázolt lépések követésével könnyedén megvalósíthatja a tömörítést az alkalmazásokban, és javíthatja az Excel fájlkezelés hatékonyságát.
## GYIK
### Mi az Aspose.Cells?  
Az Aspose.Cells egy hatékony .NET-könyvtár, amely lehetővé teszi a fejlesztők számára Excel-fájlok létrehozását, kezelését és konvertálását Microsoft Excel nélkül.
### Hogyan telepíthetem az Aspose.Cells-t?  
 Az Aspose.Cells letölthető és telepíthető a[Aspose honlapja](https://releases.aspose.com/cells/net/).
### Milyen tömörítési szintek állnak rendelkezésre?  
Az Aspose.Cells több tömörítési szintet támogat, az 1. szinttől (legalacsonyabb tömörítés) a 9. szintig (legmagasabb tömörítés).
### Ingyenesen tesztelhetem az Aspose.Cells-t?  
 Igen! Az Aspose.Cells ingyenes próbaverzióját kaphatja meg[itt](https://releases.aspose.com/).
### Hol találok támogatást az Aspose.Cells számára?  
 Bármilyen kérdéssel vagy támogatással kapcsolatban keresse fel az Aspose támogatási fórumát[itt](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
