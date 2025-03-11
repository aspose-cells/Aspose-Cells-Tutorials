---
title: A PDF létrehozási idejének beállítása .NET-ben
linktitle: A PDF létrehozási idejének beállítása .NET-ben
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan állíthatja be a PDF létrehozási idejét .NET-ben az Aspose.Cells használatával. Kövesse lépésenkénti útmutatónkat a zökkenőmentes Excelből PDF-be konvertáláshoz.
weight: 11
url: /hu/net/xps-and-pdf-operations/setting-pdf-creation-time/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# A PDF létrehozási idejének beállítása .NET-ben

## Bevezetés
mai digitális korban a dokumentumok különböző formátumokba konvertálhatósága számos alkalmazás számára kulcsfontosságú. Az egyik gyakori igény az Excel-táblázatok PDF-fájlokká konvertálása. Ez nem csak a formázást őrzi meg, hanem a megosztást és a nyomtatást is sokkal egyszerűbbé teszi. Ha Ön .NET-tel dolgozó fejlesztő, az Aspose.Cells egy fantasztikus könyvtár, amely leegyszerűsíti ezt a folyamatot. Ebben az oktatóanyagban bemutatjuk, hogyan állíthatja be a PDF létrehozási idejét, amikor egy Excel-fájlt PDF-formátumba konvertál az Aspose.Cells for .NET használatával.
## Előfeltételek
Mielőtt belevágnánk a kód apró részleteibe, győződjünk meg arról, hogy mindennel rendelkezünk, ami az induláshoz szükséges.
### Amire szüksége van
1. Visual Studio: Győződjön meg arról, hogy a Visual Studio telepítve van a gépen. Ez lesz az Ön fejlesztési környezete.
2.  Aspose.Cells for .NET: Töltse le az Aspose.Cells könyvtárat a[weboldal](https://releases.aspose.com/cells/net/). Kezdje egy ingyenes próbaverzióval is, hogy tesztelje a funkcióit.
3. Alapvető C# ismerete: A C# programozás ismerete segít jobban megérteni a kódrészleteket.
4.  Excel-fájl: Készítsen Excel-fájlt a konvertálásra. Ebben a példában egy nevű fájlt fogunk használni`Book1.xlsx`.
Most, hogy az előfeltételeket rendezte, térjünk rá a szórakoztató részre – a szükséges csomagok importálására és a kód megírására!
## Csomagok importálása
A kezdéshez importálnia kell a szükséges névtereket a C# fájlba. Ez döntő fontosságú, mivel lehetővé teszi az Aspose.Cells könyvtár által biztosított osztályok és metódusok elérését.
### Nyissa meg C# projektjét
Nyissa meg a Visual Studio-t, és hozzon létre egy új projektet, vagy nyisson meg egy meglévőt, ahol meg szeretné valósítani a PDF-konverziós funkciót.
### Adja hozzá az Aspose.Cells Reference hivatkozást
Hozzáadhatja az Aspose.Cells könyvtárat a projekthez, ha a Solution Explorerben jobb gombbal rákattint a projektre, kiválasztja a „NuGet-csomagok kezelése” lehetőséget, és rákeres az „Aspose.Cells” kifejezésre. Telepítse a csomagot.
### Névterek importálása
A C# fájl tetején adja meg a következő névtereket:
```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Charts;
```
Ezek a névterek hozzáférést biztosítanak a Workbook osztályhoz és más alapvető funkciókhoz.

Most, hogy a csomagjainkat importáltuk, bontsuk le az Excel-fájl PDF-be konvertálásának folyamatát, miközben beállítjuk a létrehozási időt.
## 1. lépés: Határozza meg a dokumentumkönyvtárat
Először is meg kell adnia a könyvtárat, ahol a dokumentumokat tárolja. Itt található az Excel-fájl, és a kimeneti PDF mentésre kerül.
```csharp
string dataDir = "Your Document Directory"; // Adja meg a dokumentumkönyvtárat
```
 Cserélje ki`"Your Document Directory"` a tényleges útvonallal, ahol az Ön`Book1.xlsx` fájl található. Ez az útvonal segít az alkalmazásnak megtalálni a feldolgozásra szánt fájlt.
## 2. lépés: Töltse be az Excel fájlt
 Ezután töltse be az Excel fájlt a`Workbook` objektum. Ez az a hely, ahol az Aspose.Cells ragyog, mivel lehetővé teszi az Excel-fájlok könnyű kezelését.
```csharp
string inputPath = dataDir + "Book1.xlsx"; // Az Excel-fájl elérési útja
Workbook workbook = new Workbook(inputPath); // Töltse be az Excel fájlt
```
 A`Workbook` osztály az Excel fájlok betöltésére és kezelésére szolgál. A beviteli útvonal átadásával megmondja az alkalmazásnak, hogy melyik fájllal dolgozzon.
## 3. lépés: PdfSaveOptions létrehozása
 Most itt az ideje létrehozni egy példányt`PdfSaveOptions`. Ez az osztály lehetővé teszi a munkafüzet PDF formátumban történő mentésére vonatkozó különféle beállítások megadását, beleértve a létrehozási időt is.
```csharp
PdfSaveOptions options = new PdfSaveOptions(); // Hozzon létre PdfSaveOptions példányt
options.CreatedTime = DateTime.Now; // Állítsa be a létrehozás idejét most
```
 Beállítás által`options.CreatedTime` hogy`DateTime.Now`, akkor biztosítja, hogy a PDF tükrözze a létrehozásának dátumát és időpontját.
## 4. lépés: Mentse el a munkafüzetet PDF formátumban
Végül a munkafüzetet PDF-fájlként menti az imént meghatározott beállításokkal.
```csharp
workbook.Save(dataDir + "output.pdf", options); //Mentés PDF-ként
```
 Ez a kódsor veszi a munkafüzetet, és PDF formátumban menti a megadott helyre. A`options` paramétert adunk át, hogy a létrehozási idő szerepeljen a PDF metaadatokban.

## Következtetés
És megvan! Sikeresen konvertált egy Excel-fájlt PDF formátumba az Aspose.Cells for .NET használatával, kiegészítve egy létrehozási időbélyeggel. Ez a funkció hihetetlenül hasznos lehet, ha nyomon kell követnie a dokumentumok verzióit, vagy ha információkat szeretne adni a címzetteknek a dokumentum létrehozásának időpontjáról.
 Ha az Aspose.Cells további funkcióit szeretné felfedezni, ne habozzon, nézze meg a[dokumentáció](https://reference.aspose.com/cells/net/).
## GYIK
### Mi az Aspose.Cells?
Az Aspose.Cells egy hatékony .NET-könyvtár, amely lehetővé teszi a fejlesztők számára Excel-fájlok létrehozását, kezelését és konvertálását.
### Használhatom ingyenesen az Aspose.Cells-t?
 Igen, elkezdheti egy ingyenes próbaverzióval, amely elérhető a webhelyen[Aspose honlapja](https://releases.aspose.com/).
### Hogyan állíthatok be más PDF-tulajdonságokat?
 Különféle PDF-tulajdonságokat állíthat be a`PdfSaveOptions` osztály, például az oldalméret, a tömörítés stb.
### Lehetséges egyszerre több Excel fájl konvertálása?
Igen, végignézheti a fájlok listáját, és mindegyikre ugyanazt az átalakítási folyamatot alkalmazhatja.
### Hol kaphatok támogatást az Aspose.Cells-hez?
 Támogatást kaphat az Aspose közösségtől[támogatási fórum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
