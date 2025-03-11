---
title: Frissítse a Power Query képletelemet a munkafüzetben
linktitle: Frissítse a Power Query képletelemet a munkafüzetben
second_title: Aspose.Cells .NET Excel Processing API
description: Ebből az átfogó, lépésenkénti útmutatóból megtudhatja, hogyan frissítheti a Power Query képleteket Excelben az Aspose.Cells for .NET segítségével.
weight: 27
url: /hu/net/workbook-operations/update-power-query-formula-item/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Frissítse a Power Query képletelemet a munkafüzetben

## Bevezetés
Minden adatelemző vagy Excel-rajongó számára rendkívül fontos, hogy megértse, hogyan kezelheti hatékonyan az adatokat az Excel Power Query használatával. Ha valaha is frissítenie kellett a Power Query-munkafüzet képletelemeit, akkor jó helyen jár. Ez az útmutató személyre szabottan segít megtanulni, hogyan használhatja az Aspose.Cells for .NET alkalmazást a Power Query képletek zökkenőmentes frissítéséhez egy Excel-munkafüzetben. Néhány egyszerű lépéssel manipulálhatja és racionalizálhatja adatait, így biztosítva, hogy munkafüzetei dinamikusak és központiak maradjanak.
## Előfeltételek
Mielőtt belemerülne a példakódba és a lépésekbe, nézzük meg, mire lesz szüksége:
1. A C# és a .NET alapvető ismerete: A C# programozási koncepcióinak ismerete hasznos lesz, mivel kódot írunk.
2.  Az Aspose.Cells telepítése .NET-hez: Az Aspose.Cells könyvtárat integrálni kell a .NET-projektbe. Letöltheti[itt](https://releases.aspose.com/cells/net/).
3. Módosításra kész Excel-fájl: Győződjön meg arról, hogy rendelkezik olyan Excel-fájllal, amely tartalmazza a frissíteni kívánt Power Query-t. Szüksége van egy minta munkafüzetre, mint pl`SamplePowerQueryFormula.xlsx` az Ön rendelkezésére.
## Csomagok importálása
A kezdéshez győződjön meg arról, hogy a következő névterek szerepelnek a C# fájlban:
```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```
Ez lehetővé teszi az Aspose.Cells könyvtár által biztosított funkciók elérését, különösen a munkafüzetek és a Power Query adatok kezeléséhez.
## 1. lépés: Állítsa be munkakönyvtárait
Először is meg kell határoznia, hogy hol találhatók a forrás- és kimeneti fájlok. 
```csharp
string SourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
```
 Ebben a lépésben adja meg a könyvtár elérési útjait. Cserélje ki`"Your Document Directory"` az Excel-fájlok mentési útvonalával. Ez megmondja a programnak, hogy hol keresse a forrásfájlt, és hova mentse a frissített fájlt.
## 2. lépés: Töltse be a munkafüzetet
Most, hogy beállította a munkakönyvtárakat, a következő lépés az Excel fájl betöltése a programba.
```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
 Itt létrehoz egy`Workbook` objektum, amely betölti a megadott Excel fájlt. A`Workbook`osztály az Aspose.Cells könyvtár része, és nélkülözhetetlen minden olyan művelethez, amelyet az adott Excel-fájlon fog végrehajtani.
## 3. lépés: A Power Query adatok elérése
A munkafüzet betöltése után ideje elérni a benne tárolt Power Query képleteket.
```csharp
DataMashup mashupData = workbook.DataMashup;
```
 Ebben a sorban a`DataMashup` tulajdonság segít elérni a Power Query adatstruktúrákat a munkafüzeten belül. Ez a tulajdonság lehetővé teszi az Excel-fájlban található Power Query-adatok különféle aspektusainak kezelését.
## 4. lépés: Hurok a Power Query képletek között
Amikor a Power Query adatok elérhetők, a következő lépés az egyes jelenlévő képletek megismétlése.
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
 Itt történik a varázslat. Mindegyiket átkutatjuk`PowerQueryFormula` majd mindegyiken keresztül`PowerQueryFormulaItem` . A`if` Az utasítás megkeresi a „Forrás” nevű képletelemet, és frissíti annak értékét annak a forrásfájlnak az elérési útjára, amelyre a Power Query által hivatkozni kíván. Ez lehetővé teszi, hogy dinamikusan módosítsa, hogy a Power Query melyik fájlból kérjen adatokat.
## 5. lépés: Mentse el a frissített munkafüzetet
A szükséges képletelemek frissítése után az utolsó lépés a munkafüzet mentése.
```csharp
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
```
Ez a sor a módosított munkafüzetet egy új fájlba menti, így megőrzi az eredetit, miközben lehetővé teszi a frissített verzióval való munkát.
## 6. lépés: Megerősítő üzenet
Végül célszerű ellenőrizni, hogy a kód megfelelően fut-e le.
```csharp
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
Ez az egyszerű üzenet megerősíti Önt a konzolon, hogy a művelet sikeres volt, és megnyugtatóan lezárja a folyamatot.
## Következtetés
És megvan! A Power Query képletelemeinek frissítése az Excelben az Aspose.Cells for .NET használatával néhány egyszerű lépésben elvégezhető. Az útmutató követésével hatékonyan kezelheti Excel adatkapcsolatait, és zökkenőmentesen futhat munkafüzetei. Akár tapasztalt profi, akár csak most kezdi az adatkezelést, az Aspose.Cells hatékony módszert kínál az Excel-munkafolyamatok automatizálására és javítására. 
## GYIK
### Használhatom az Aspose.Cells-t a .NET bármely verziójával?
Az Aspose.Cells a .NET több verziójával kompatibilis, beleértve a .NET Framework-et és a .NET Core-t.
### Az Aspose.Cells ingyenesen használható?
 Az Aspose.Cells ingyenes próbaverziót kínál, de a folyamatos használathoz licenc szükséges. Kaphat ideiglenes engedélyt[itt](https://purchase.aspose.com/temporary-license/).
### Mi a teendő, ha a meglévő Excel-fájlomban nincs Power Query?
A leírt folyamat a Power Query-elemek frissítésére összpontosít, ezért ha a fájlból hiányoznak ezek, először be kell építenie a Power Query-t.
### Hol találhatok több információt az Aspose.Cells-ről?
 Tekintse meg a dokumentációt átfogó útmutatásért és példákért. Látogassa meg a[dokumentáció](https://reference.aspose.com/cells/net/).
### Hogyan jelenthetem az Aspose.Cells hibáit?
Bármilyen felmerülő problémával kapcsolatban segítségért fordulhat a támogatott fórumukhoz.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
