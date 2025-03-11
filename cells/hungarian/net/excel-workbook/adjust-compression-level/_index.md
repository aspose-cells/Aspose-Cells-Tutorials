---
title: Állítsa be a tömörítési szintet
linktitle: Állítsa be a tömörítési szintet
second_title: Aspose.Cells for .NET API Reference
description: Ismerje meg, hogyan állíthatja be az Excel-fájlok tömörítési szintjét az Aspose.Cells for .NET segítségével. Ezzel a lépésenkénti útmutatóval hatékonyan optimalizálhatja fájlméreteit.
weight: 50
url: /hu/net/excel-workbook/adjust-compression-level/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Állítsa be a tömörítési szintet

## Bevezetés

A nagy Excel-fájlok kezelésénél kulcsfontosságú a hatékony tárolás. Akár fejlesztő, aki optimalizálni szeretné a fájlméreteket, akár adatelemző, aki fel akarja gyorsítani a fájlátvitelt, az Aspose.Cells for .NET tömörítési szintjei beállításának ismerete jót tehet a játékban. Ebben az útmutatóban végigvezetjük az Excel-fájlok mentésekor a tömörítési szintek beállításának lépésein, így biztosítva a teljesítmény megőrzését a minőség feláldozása nélkül.

## Előfeltételek

Mielőtt belemerülnénk a tömörítési szintek finomságába, győződjünk meg arról, hogy mindennel rendelkezünk, ami az induláshoz szükséges:

1. Alapvető C# ismerete: A C# programozás alapjainak ismerete elengedhetetlen. Ha kényelmesen kezeli a változókat, a ciklusokat és az alapvető fájlműveleteket, akkor kész!
2. Aspose.Cells for .NET Library: Győződjön meg arról, hogy telepítve van az Aspose.Cells könyvtár. Letöltheti a[weboldal](https://releases.aspose.com/cells/net/) . Ha még csak most kezdi, fontolja meg az ingyenes próbaidőszak igénybevételét[itt](https://releases.aspose.com/).
3. Fejlesztői környezet: Állítsa be a fejlesztői környezetét, ideális esetben a Visual Studio-t, hogy megírja és végrehajtsa a C# kódot. 
4. Minta Excel-fájl: Készítsen egy nagyméretű Excel-fájlt tesztelésre. Létrehozhat egyet, vagy használhat bármilyen meglévő fájlt, de győződjön meg arról, hogy elég nagy ahhoz, hogy lássa a tömörítés hatásait.

Ha ezekkel az előfeltételekkel rendelkezik, kezdjük!

## Csomagok importálása

Mielőtt manipulálhatnánk az Excel fájlokat, importálnunk kell a szükséges névtereket. Ez egy döntő lépés, amely lehetővé teszi számunkra, hogy hozzáférjünk az Aspose.Cells által biztosított osztályokhoz és metódusokhoz.

### Importálja az Aspose.Cells névteret

```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```

 Ez a kódrészlet importálja a`Aspose.Cells` névtér, amely az Excel fájlokkal való munkához szükséges összes osztályt tartalmazza. A`Aspose.Cells.Xlsb` névtér kifejezetten az XLSB fájlformátumok kezelésére szolgál.

Most, hogy mindent beállítottunk, bontsuk fel a tömörítési szintek beállításának folyamatát kezelhető lépésekre. Elmentünk egy munkafüzetet különböző tömörítési szintekkel, és mérjük az egyes műveletekhez szükséges időt. 

## 1. lépés: Állítsa be a címtárakat

Először is meg kell határoznunk, hogy hol tároljuk a fájljainkat. Ez magában foglalja a forráskönyvtár megadását a bemeneti fájlunkhoz és a kimeneti könyvtárat a tömörített fájlokhoz.

```csharp
// Forrás könyvtár
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```

## 2. lépés: Töltse be a munkafüzetet

Ezután betöltjük a tömöríteni kívánt Excel-munkafüzetet. Itt mutathat a nagyméretű Excel-fájlra.

```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```

 Ez a sor inicializál egy újat`Workbook` objektum a megadott fájllal. Győződjön meg arról, hogy a fájl elérési útja helyes; különben hibákba ütközhet.

## 3. lépés: Hozzon létre mentési beállításokat az XLSB számára

 Most létrehozunk egy példányt`XlsbSaveOptions`, amely lehetővé teszi, hogy megadjuk, hogyan akarjuk menteni a munkafüzetünket, beleértve a tömörítési szintet is.

```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```

Ez a sor előkészíti azokat a beállításokat, amelyeket a munkafüzet XLSB formátumban történő mentéséhez használunk.

## 4. lépés: Állítsa be és mérje meg a tömörítési szinteket

Most jön a szórakoztató rész! Különböző tömörítési szintekkel mentjük a munkafüzetet, és mérjük az egyes műveletekhez szükséges időt. 

### 1. szintű tömörítés

Kezdjük a legalacsonyabb tömörítési szinttel:

```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = System.Diagnostics.Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```

Ebben a részletben a tömörítési típust 1-es szintre állítjuk, mentjük a munkafüzetet, és naplózzuk a szükséges időt. 

### 6. szintű tömörítés

Ezután egy közepes tömörítési szinttel próbálkozunk:

```csharp
options.CompressionType = OoxmlCompressionType.Level6;
watch = System.Diagnostics.Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```

Ezúttal a tömörítési típust 6-os szintre állítjuk, és megismételjük a mentési műveletet.

### 9. szintű tömörítés

Végül mentsünk a legmagasabb tömörítési szint használatával:

```csharp
options.CompressionType = OoxmlCompressionType.Level9;
watch = System.Diagnostics.Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_9_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 9 Elapsed Time: " + elapsedMs);
```

Ebben a lépésben a tömörítési típust 9-es szintre állítjuk, ami a legkisebb fájlméretet eredményezi, de a mentés tovább tarthat.

## 5. lépés: Végső kimenet

A fenti lépések végrehajtása után látni fogja a konzolra nyomtatott egyes tömörítési szintek eltelt idejét. 

```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```

Ez a sor megerősíti, hogy a teljes folyamat problémamentesen lezajlott.

## Következtetés

tömörítési szintek beállítása Excel-fájlok mentésekor az Aspose.Cells for .NET segítségével egyszerű, de hatékony technika. Az ebben az útmutatóban ismertetett lépések követésével könnyedén módosíthatja a fájlméreteket, így könnyebben kezelhetővé válik a tárolás és átvitel során. Akár gyors hozzáférésre van szüksége az adatokhoz, akár optimalizálni szeretné alkalmazása teljesítményét, ezeknek a technikáknak az elsajátítása kétségtelenül fejleszti fejlesztői készségeit.

## GYIK

### Mi az Aspose.Cells?
Az Aspose.Cells egy .NET-könyvtár, amely lehetővé teszi a fejlesztők számára Excel-fájlok programozott létrehozását, kezelését és konvertálását.

### Hogyan tölthetem le az Aspose.Cells-t?
 Letöltheti az Aspose.Cells könyvtárat a[weboldal](https://releases.aspose.com/cells/net/).

### Használhatom ingyenesen az Aspose.Cells-t?
 Igen, az Aspose ingyenes próbaverziót kínál, amelyhez hozzáférhet[itt](https://releases.aspose.com/).

### Melyek a különböző tömörítési szintek?
Az Aspose.Cells több tömörítési szintet támogat, az 1. szinttől (legkisebb tömörítés) a 9. szintig (maximális tömörítés).

### Hol találok támogatást az Aspose.Cells számára?
 Támogatást kaphat és kérdéseket tehet fel a[Aspose fórum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
