---
title: Frissítse a Power Query képletelemet
linktitle: Frissítse a Power Query képletelemet
second_title: Aspose.Cells for .NET API Reference
description: Könnyen frissítheti a Power Query képletelemeit az Excelben az Aspose.Cells for .NET segítségével. Lépésről lépésre szóló útmutató az adatkezelési folyamatok egyszerűsítéséhez.
weight: 160
url: /hu/net/excel-workbook/update-power-query-formula-item/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Frissítse a Power Query képletelemet

## Bevezetés

Ha valaha is dolgozott az Excellel, tudja, milyen hatékony lehet – különösen akkor, ha elkezdi a Power Queries-t. Ezek azok a titkos szószok, amelyek segítségével könnyedén átalakíthatja, tisztíthatja és elemezheti adatait. A Power Query képletek Excelben való kezelésének egyik remek módja az Aspose.Cells for .NET. Ma lépésről lépésre végigvezetjük a Power Query képletelemeinek frissítésén. Szóval, fogd meg a kódoló kalapot, és kezdjük is!

## Előfeltételek

Mielőtt belevágna a kódba, be kell állítania néhány dolgot:

1. Visual Studio: A .NET-kód írásához és futtatásához integrált fejlesztői környezetre (IDE) lesz szüksége. A Visual Studio a legjobb választás.
2.  Aspose.Cells Library: Győződjön meg arról, hogy az Aspose.Cells könyvtár elérhető a projektben. Letöltheti a[telek](https://releases.aspose.com/cells/net/).
3. Alapvető C# ismerete: Noha ezt együtt fogjuk végigjárni, a C# alapvető ismerete minden bizonnyal segít, különösen a különböző osztályok és módszerek közötti navigálás során.
4. Minta Excel-fájlok: Szüksége lesz a kódrészletben említett Excel-fájlokra. Győződjön meg arról, hogy rendelkezik:
   - `SamplePowerQueryFormula.xlsx`
   - `SamplePowerQueryFormulaSource.xlsx`

5. .NET-keretrendszer: Győződjön meg arról, hogy projektje a .NET-keretrendszer kompatibilis verzióját célozza meg.

Most, hogy készen van a készletünk, folytathatjuk a szórakoztató részt: a kód írását!

## Csomagok importálása

Először is importálnia kell a szükséges névtereket. Íme, hogyan kell csinálni:

```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```

A névterek hozzáadásával tudatja a fordítóval, hogy az Aspose.Cells könyvtár osztályait és metódusait kívánja használni. Ez a lépés kulcsfontosságú, mivel megalapozza a következő kódot.

Bontsuk fel az Ön által megadott kódrészletet. Ez az oktatóanyag végigvezeti Önt az egyes részeken, és biztosítja, hogy megértse, mi történik.

## 1. lépés: Állítsa be a munkakönyvtárakat

Ebben a lépésben meghatározzuk, hogy hol találhatók a forrás- és kimeneti fájljaink. Ez biztosítja, hogy az Aspose tudja, hol keresse az Excel-fájlokat.

```csharp
// Munkakönyvtárak
string SourceDir = "Your Document Directory";
string outputDir = "Your Output Directory";
```

## 2. lépés: Töltse be a munkafüzetet

Most töltsük be az Excel-fájlt, ahol a Power Query található.

```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
 A`Workbook` osztály a belépési pont az Excel fájlba. A forrásfájlunk elérési útjának átadásával létrehozunk egy példányt, amely lehetővé teszi a fájl manipulálását. Úgy képzelheti el, mintha kinyitna egy könyvet – a tartalmának elolvasására (vagy szerkesztésére) készül.

## 3. lépés: Lépjen be a Data Mashupba

Ezután elérjük a munkafüzet Data Mashupjában tárolt Power Query képleteket.

```csharp
DataMashup mashupData = workbook.DataMashup;
```
 A`DataMashup` osztály tartalmazza a munkafüzethez társított összes Power Query képletet. Itt fogjuk elvégezni a nehézemeléseket, hasonlóan ahhoz, mint amikor kinyit egy szerszámosládát a javításhoz.

## 4. lépés: Hurok a Power Query képletek között

Most jön az a rész, ahol a Power Query képleteket iteráljuk, hogy megtaláljuk a frissíteni kívánt konkrétat.

```csharp
foreach (PowerQueryFormula formula in mashupData.PowerQueryFormulas)
{
    foreach (PowerQueryFormulaItem item in formula.PowerQueryFormulaItems)
    {
        if (item.Name == "Source")
        {
            item.Value = "Excel.Workbook(File.Contents(\"" + SourceDir + "SamplePowerQueryFormulaSource.xlsx\"), null, true)";
        }
    }
}
```

-  Mindegyiket átkutatjuk`PowerQueryFormula` be`mashupData`.
- Ezen a hurkon belül mindegyikbe belemerülünk`PowerQueryFormulaItem`.
- Ellenőrizzük, hogy az elem neve megegyezik-e a „Forrás”-val. Ha igen, frissítjük az értékét, hogy az új forrásfájlunkra hivatkozzon.

Ez olyan, mintha egy kézikönyvben megtalálná a megfelelő oldalt, majd elvégezné a szükséges frissítéseket – ez egy egyszerű és aprólékos folyamat.

## 5. lépés: Mentse el a frissített munkafüzetet

A frissítések elvégzése után ideje elmenteni a módosításainkat.

```csharp
// Mentse el a kimeneti munkafüzetet.
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
 A`Save` metódus a frissített munkafüzetet a megadott kimeneti könyvtárba írja. Ez olyan, mintha a szerkesztéseidet a kézikönyv új verziójába zárnád, amely készen áll mások használatra!

## Következtetés

Gratulálok! Sikeresen frissített egy Power Query képletelemet az Aspose.Cells for .NET használatával. Ezzel a módszerrel automatizálhatja a Power Query képletek módosítását az Excel-fájlokban, így értékes időt és erőfeszítést takaríthat meg.

## GYIK

### Mi az Aspose.Cells?
Az Aspose.Cells egy hatékony könyvtár az Excel-fájlok kezeléséhez .NET-alkalmazásokban a Microsoft Excel telepítése nélkül.

### Szükségem van Microsoft Excelre az Aspose.Cells futtatásához?
Nem, az Aspose.Cells lehetővé teszi az Excel-fájlok programozott létrehozását és szerkesztését anélkül, hogy a kiszolgálón vagy a fejlesztőgépen Excelre lenne szükség.

### Milyen típusú Excel-fájlokkal dolgozhatok az Aspose.Cells használatával?
Az Aspose.Cells használatával dolgozhat .xlsx, .xls, .xlsm és számos más Excel formátummal.

### Elérhető az Aspose.Cells próbaverziója?
 Igen, letölthet egy ingyenes próbaverziót a webhelyről[Az Aspose Cells kiadási oldala](https://releases.aspose.com/).

### Hogyan kaphatok támogatást az Aspose.Cells-hez?
 A támogatást a következőn keresztül érheti el[Aspose fórum](https://forum.aspose.com/c/cells/9), ahol kérdéseket tehet fel, és választ kaphat a közösségtől és az Aspose csapatától.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
