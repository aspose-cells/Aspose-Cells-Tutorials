---
"description": "Az Aspose.Cells for .NET segítségével könnyedén frissítheti Power Query képletelemeit az Excelben. Lépésről lépésre útmutató az adatkezelési folyamatok egyszerűsítéséhez."
"linktitle": "Power Query képletelemének frissítése"
"second_title": "Aspose.Cells .NET API-referencia"
"title": "Power Query képletelemének frissítése"
"url": "/hu/net/excel-workbook/update-power-query-formula-item/"
"weight": 160
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Power Query képletelemének frissítése

## Bevezetés

Ha valaha is dolgoztál már Excellel, akkor tudod, milyen hatékony tud lenni – különösen, ha elkezded elmerülni a Power Queryk világában. Ezek a titkos összetevők, amelyek lehetővé teszik az adatok egyszerű átalakítását, tisztítását és elemzését. A Power Query-képletek Excelben történő kezelésének egyik ügyes módja az Aspose.Cells for .NET használata. Ma lépésről lépésre végigvezetünk a Power Query-képletelemek frissítésén. Szóval, ragadd meg a programozó sapkádat, és kezdjük is!

## Előfeltételek

Mielőtt belemerülnél a kódba, érdemes néhány dolgot beállítani:

1. Visual Studio: Integrált fejlesztői környezetre (IDE) lesz szükséged a .NET kódod írásához és futtatásához. A Visual Studio a legjobb választás.
2. Aspose.Cells könyvtár: Győződjön meg arról, hogy az Aspose.Cells könyvtár elérhető a projektjében. Letöltheti innen: [telek](https://releases.aspose.com/cells/net/).
3. C# alapismeretek: Bár ezt együtt fogjuk végigvenni, a C# alapvető ismeretei mindenképpen hasznosak lesznek, különösen a különböző osztályok és metódusok közötti eligazodás során.
4. Minta Excel fájlok: Szükséged lesz a kódrészletben említett Excel fájlokra. Győződj meg róla, hogy rendelkezel a következőkkel:
   - `SamplePowerQueryFormula.xlsx`
   - `SamplePowerQueryFormulaSource.xlsx`

5. .NET-keretrendszer: Győződjön meg arról, hogy a projekt a .NET-keretrendszer egy kompatibilis verzióját célozza meg.

Most, hogy készen áll a készletünk, folytathatjuk a mókás részt: a kódírást!

## Csomagok importálása

Először is importálnod kell a szükséges névtereket. Így teheted meg:

```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```

Ezen névterek hozzáadásával tudatod a fordítóval, hogy az Aspose.Cells könyvtár osztályait és metódusait kívánod használni. Ez a lépés kulcsfontosságú, mivel lefekteti az alapokat a következő kódhoz.

Nézzük meg részletesebben a megadott kódrészletet. Ez az oktatóanyag végigvezet az egyes részeken, biztosítva, hogy megértsd, miről is van szó.

## 1. lépés: Munkakönyvtárak beállítása

Ebben a lépésben meghatározzuk a forrás- és kimeneti fájlok helyét. Ez biztosítja, hogy az Aspose tudja, hol keresse az Excel-fájlokat.

```csharp
// Munkakönyvtárak
string SourceDir = "Your Document Directory";
string outputDir = "Your Output Directory";
```

## 2. lépés: A munkafüzet betöltése

Most töltsük be azt az Excel-fájlt, amelyben a Power Query található.

```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
A `Workbook` Az osztály a belépési pont az Excel-fájlba. A forrásfájl elérési útjának átadásával létrehozunk egy példányt, amely lehetővé teszi számunkra, hogy manipuláljuk azt. Elképzelhetjük úgy, mintha megnyitnánk egy könyvet – éppen a tartalmának olvasására (vagy szerkesztésére) készülünk.

## 3. lépés: Hozzáférés az adatmashuphoz

Ezután hozzáférünk a munkafüzet adategyesítésében tárolt Power Query-képletekhez.

```csharp
DataMashup mashupData = workbook.DataMashup;
```
A `DataMashup` Az osztály tartalmazza a munkafüzetedhez társított összes Power Query-képletet. Itt fogjuk elvégezni a nehéz munkát, hasonlóan ahhoz, mint amikor megnyitsz egy eszköztárat a javításokhoz.

## 4. lépés: Power Query képletek cikluson keresztüli végigjátszása

Most jön az a rész, ahol végigmegyünk a Power Query képletein, hogy megtaláljuk a frissíteni kívánt képletet.

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

- Végigmegyünk mindegyiken `PowerQueryFormula` ban `mashupData`.
- Ezen a körön belül belemerülünk mindegyikbe `PowerQueryFormulaItem`.
- Ellenőrizzük, hogy az elem neve megegyezik-e a „Forrás” nevével. Ha igen, akkor frissítjük az értékét, hogy az az új forrásfájlunkra mutasson.

Ez ahhoz hasonlít, mintha egy kézikönyvben megkeresnénk a megfelelő oldalt, majd elvégeznénk a szükséges frissítéseket – ez egy egyszerű és aprólékos folyamat.

## 5. lépés: A frissített munkafüzet mentése

A frissítések elvégzése után itt az ideje menteni a módosításokat.

```csharp
// Mentse el a kimeneti munkafüzetet.
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
A `Save` metódus a frissített munkafüzetet a megadott kimeneti könyvtárba írja. Olyan ez, mintha a szerkesztéseket a kézikönyv egy új verziójába zárnánk, hogy mások is használhassák őket!

## Következtetés

Gratulálunk! Sikeresen frissített egy Power Query képletelemet az Aspose.Cells for .NET használatával. Ezzel a módszerrel automatizálhatja a Power Query képletek módosítását az Excel-fájlokban, így értékes időt és energiát takaríthat meg.

## GYIK

### Mi az Aspose.Cells?
Az Aspose.Cells egy hatékony függvénykönyvtár, amellyel Excel fájlokat lehet kezelni .NET alkalmazásokban anélkül, hogy telepíteni kellene a Microsoft Excelt.

### Szükségem van Microsoft Excelre az Aspose.Cells futtatásához?
Nem, az Aspose.Cells lehetővé teszi Excel fájlok programozott létrehozását és szerkesztését anélkül, hogy az Excelre lenne szükség a szerveren vagy a fejlesztőgépen.

### Milyen típusú Excel fájlokkal dolgozhatok az Aspose.Cells segítségével?
Az Aspose.Cells segítségével .xlsx, .xls, .xlsm és számos más Excel formátummal dolgozhatsz.

### Van elérhető próbaverzió az Aspose.Cells-hez?
Igen, letölthet egy ingyenes próbaverziót a következő címről: [Aspose Cells kiadási oldal](https://releases.aspose.com/).

### Hogyan kaphatok támogatást az Aspose.Cells-hez?
A támogatást a következőn keresztül veheti igénybe: [Aspose fórum](https://forum.aspose.com/c/cells/9), ahol kérdéseket tehetsz fel és válaszokat kaphatsz a közösségtől és az Aspose csapatától.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}