---
title: Az egyesített cellák egyesítésének megszüntetése az Excelben
linktitle: Az egyesített cellák egyesítésének megszüntetése az Excelben
second_title: Aspose.Cells .NET Excel Processing API
description: Könnyen bonthatja fel az egyesített cellákat az Excelben az Aspose.Cells for .NET segítségével. Kövesse lépésenkénti útmutatónkat jobb táblázatok létrehozásához.
weight: 10
url: /hu/net/excel-merging-unmerging-cells/unmerge-merged-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Az egyesített cellák egyesítésének megszüntetése az Excelben

## Bevezetés

Belefáradt az egyesített cellák kezelésébe az Excel-táblázatokban? Nem vagy egyedül! Az egyesített cellák praktikus formázási funkciót jelenthetnek, de gyakran fejfájáshoz vezethetnek az adatok manipulálása és elemzése során. De mit gondol? A bosszantó cellák összevonása egyszerűbb, mint gondolná – különösen, ha az Aspose.Cells-t használja .NET-hez. Ebben a cikkben lépésről lépésre bemutatom, hogyan bonthatja fel az egyesített cellák egyesítését, így biztosítva, hogy adatai tiszták, rendezettek és készen állnak a használatra! Tehát, fogd meg a kódoló kalapot, és merüljünk el az Aspose.Cells világában.

## Előfeltételek

Mielőtt bemocskolnánk a kezünket, néhány alapvető dolgot meg kell tennie:

### C# és .NET Framework alapismeretek
Ha ismeri a C# programozást, és alapjaiban ismeri a .NET keretrendszert, máris remekül indul. Ha nem, ne aggódj! Ezt az oktatóanyagot úgy tervezték, hogy egyszerű legyen, így útközben felveszi a szükséges fogalmakat.

### Aspose.Cells Library
Győződjön meg arról, hogy az Aspose.Cells könyvtár telepítve van a .NET-környezetben. Ezt könnyen megszerezheti, ha ellátogat a[Aspose.Cells letöltési oldal](https://releases.aspose.com/cells/net/).

### IDE beállítás
Be kell állítania egy fejlesztői környezetet, például a Visual Studio-t, ahol megírhatja és végrehajthatja a C# kódot.

### Minta Excel fájl
Fogjon meg egy minta Excel-fájlt, amely egyesített cellákat tartalmaz – ezt a fájlt fogja használni az egyesítés megszüntetésének gyakorlására.

Ha ezeket az előfeltételeket rendeztük, most nekivághatunk az izgalmas résznek – a megoldásunk kódolásának!

## Csomagok importálása

Először is importáljuk a szükséges csomagokat. Az Aspose.Cells segítségével különféle osztályokkal kommunikálhat az Excel-fájlok hatékony kezeléséhez. A következőket kell szerepeltetnie a C# fájl tetején:

```csharp
using System;
using System.IO;

using Aspose.Cells;
```

A csomag hozzáadásával hozzáférhet az Aspose.Cells által kínált összes szolgáltatáshoz.

Bontsuk fel az összevonás folyamatát kezelhető lépésekre. Minden lépés egyértelműen meghatározott lesz, így könnyen követheti a lépést.

## 1. lépés: Adja meg a könyvtárakat

Az első lépés az, hogy meghatározza azokat a könyvtárakat, amelyekben a bemeneti Excel fájl (amely egyesített cellákkal rendelkezik) és a kimeneti fájl (amely a nem egyesített adatokat menti) található. A következőképpen állíthatja be:

```csharp
// Forrás könyvtár
string sourceDir = "Your Document Directory"; 

// Kimeneti könyvtár
string outputDir = "Your Document Directory"; 
```

 Mindenképpen cserélje ki`"Your Document Directory"` a fájlok tényleges elérési útjával.

## 2. lépés: Hozzon létre egy munkafüzetet

Most, hogy beállította a könyvtárakat, ideje létrehozni egy munkafüzet objektumot. Ez az objektum lehetővé teszi az Excel-fájl kezelését. Ezt a következő kóddal teheti meg:

```csharp
// Hozzon létre egy munkafüzetet
Workbook wbk = new Aspose.Cells.Workbook(sourceDir + "sampleUnMergingtheMergedCells.xlsx");
```

Ez a kódsor beolvassa a minta Excel-fájlt, és előkészíti a feldolgozásra. 

## 3. lépés: Nyissa meg a munkalapot

Minden munkafüzet lapokból áll. Hozzá kell férnie ahhoz a munkalaphoz, amelyen meg szeretné szüntetni a cellák egyesítését. Ezt a következőképpen teheti meg:

```csharp
// Hozzon létre egy munkalapot, és szerezze be az első lapot
Worksheet worksheet = wbk.Worksheets[0];
```

Ez a kód megragadja az első munkalapot. Ha az egyesített cellák egy másik lapon vannak, frissítse ennek megfelelően az indexet.

## 4. lépés: Hozzáférés a cellákhoz a munkalapon

Ezután hivatkozást kell kapnia a munkalap celláira. Ez a következőkkel valósítható meg:

```csharp
//Hozzon létre egy Cells objektumot az összes cella lekéréséhez
Cells cells = worksheet.Cells;
```

Ezzel a sorral mostantól hozzáférhet a munkalap összes cellájához, így szükség szerint módosíthatja azokat.

## 5. lépés: Szüntesse meg a cellák egyesítését

Itt jön a döntő lépés – a sejtek összevonása! Meg kell adnia az egyesített cellák tartományát, amelyeket meg kíván szüntetni. Használja a következő kódot:

```csharp
// Oldja ki a sejteket
cells.UnMerge(5, 2, 2, 3);
```

 Ebben a példában a`UnMerge` A metódus négy paramétert vesz igénybe: a kezdősor indexét (5), a kezdő oszlop indexét (2), a feloldandó sorok számát (2) és a feloldandó oszlopok számát (3). Állítsa be ezeket a paramétereket, hogy megfeleljenek az Excel-fájl egyes egyesített celláinak.

## 6. lépés: Mentse el a munkafüzetet

Az egyesítés megszüntetése után a módosításokat egy új Excel-fájlba szeretné menteni. Ezt a következőképpen teheti meg:

```csharp
// Mentse el a fájlt
wbk.Save(outputDir + "outputUnMergingtheMergedCells.xlsx");
```

Ez a sor a nem egyesített adatokat a megadott kimeneti könyvtárba menti. Ilyen egyszerű!

## 7. lépés: Erősítse meg a folyamatot

Végül jó ötlet megerősíteni, hogy minden simán ment. A művelet sikeres végrehajtásáról üzenetet nyomtathat a konzolra:

```csharp
Console.WriteLine("UnMerging the Cells executed successfully.");
```

És megvan! Sikeresen megszüntette a cellák egyesítését egy Excel-fájlban az Aspose.Cells for .NET használatával.

## Következtetés

A cellák egyesítésének megszüntetése fárasztónak tűnhet, különösen, ha nagy táblázatokkal dolgozik, de az Aspose.Cells for .NET használatával gyerekjáték! Ez az oktatóanyag végigvezeti Önt a környezet beállításától a cellák hatékony egyesítéséhez szükséges kód végrehajtásáig. Az Aspose.Cells könyvtár által kínált rugalmasság lehetővé teszi a táblázatok hatékony feldolgozását, így ideális választás az Excel fájlokkal dolgozó fejlesztők számára. Tehát merüljön el, és élvezze a tisztább, jobban kezelhető táblázatokat.

## GYIK

### Mi az Aspose.Cells?  
Az Aspose.Cells egy hatékony könyvtár Excel-dokumentumok létrehozásához, kezeléséhez és konvertálásához .NET-alkalmazásokban.

### Szükségem van engedélyre az Aspose.Cells használatához?  
 Míg az Aspose.Cells ingyenes próbaverziót kínál, a teljes használathoz licenc szükséges. Kaphatsz a[ideiglenes engedély itt](https://purchase.aspose.com/temporary-license/).

### Felbonthatom a cellák egyesítését több lapon egyszerre?  
Igen, egy munkafüzeten belül több munkalapon is átfuthat, és szükség szerint megszüntetheti a cellák egyesítését.

### Az Aspose.Cells kompatibilis a .NET Core-al?  
Igen, az Aspose.Cells kompatibilis a .NET Core programmal, így sokoldalúan használható különféle .NET-alkalmazásokhoz.

### Hol találok további dokumentációt az Aspose.Cells-ről?  
 A teljes dokumentációt megtekintheti a[Aspose.Cells referenciaoldal](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
