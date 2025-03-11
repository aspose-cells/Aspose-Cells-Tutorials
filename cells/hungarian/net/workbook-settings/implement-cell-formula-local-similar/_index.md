---
title: Helyi cellaképlet megvalósítása a Helyi tartományképlethez hasonlóan
linktitle: Helyi cellaképlet megvalósítása a Helyi tartományképlethez hasonlóan
second_title: Aspose.Cells .NET Excel Processing API
description: Fedezze fel, hogyan valósíthat meg cellaképletet, amely hasonló az Aspose.Cells for .NET tartományképlet helyi funkciójához. Ismerje meg a beépített Excel-függvénynevek testreszabását és egyebeket.
weight: 13
url: /hu/net/workbook-settings/implement-cell-formula-local-similar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Helyi cellaképlet megvalósítása a Helyi tartományképlethez hasonlóan

## Bevezetés
Az Aspose.Cells for .NET egy hatékony és rugalmas táblázatkezelő API, amely lehetővé teszi Excel-fájlok programozott létrehozását, kezelését és konvertálását. Az Aspose.Cells által kínált számos szolgáltatás egyike a beépített Excel-függvények viselkedésének testreszabásának képessége, beleértve a saját helyi függvénynevek létrehozásának lehetőségét is. Ebben az oktatóanyagban végigvezetjük az Aspose.Cells for .NET tartományképlet helyi funkciójához hasonló cellaképlet megvalósításának lépésein.
## Előfeltételek
Mielőtt elkezdené, győződjön meg arról, hogy rendelkezik a következőkkel:
1. A Microsoft Visual Studio 2010 vagy újabb verziója telepítve van a rendszerére.
2.  A projektben telepített Aspose.Cells for .NET könyvtár legújabb verziója. A könyvtár letölthető a[Aspose.Cells for .NET letöltési oldal](https://releases.aspose.com/cells/net/).
## Csomagok importálása
A kezdéshez importálnia kell a szükséges csomagokat a C# projektbe. Adja hozzá a következőket a kódfájl tetején található utasításokkal:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## 1. lépés: Hozzon létre egy egyéni globalizációs beállítások osztályt
 Az első lépés egy egyéni létrehozása`GlobalizationSettings`osztály, amely lehetővé teszi az Excel függvények alapértelmezett viselkedésének felülbírálását. Ebben a példában megváltoztatjuk a nevét`SUM` és`AVERAGE` funkciókat`UserFormulaLocal_SUM` és`UserFormulaLocal_AVERAGE`, ill.
```csharp
class GS : GlobalizationSettings
{
    public override string GetLocalFunctionName(string standardName)
    {
        //Változtassa meg a SUM függvény nevét igényei szerint.
        if (standardName == "SUM")
        {
            return "UserFormulaLocal_SUM";
        }
        //Változtassa meg az AVERAGE függvény nevét igényeinek megfelelően.
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## 2. lépés: Hozzon létre egy új munkafüzetet, és rendelje hozzá az egyéni globalizációs beállításokat
 Ezután hozzon létre egy új munkafüzet-példányt, és rendelje hozzá az egyéni példányt`GlobalizationSettings` megvalósítási osztályt a munkafüzethez`Settings.GlobalizationSettings` ingatlan.
```csharp
//Munkafüzet létrehozása
Workbook wb = new Workbook();
//Rendelje hozzá a GlobalizationSettings megvalósítási osztályt
wb.Settings.GlobalizationSettings = new GS();
```
## 3. lépés: Nyissa meg az első munkalapot és egy cellát
Most pedig érjük el a munkafüzet első munkalapját és a munkalapon belül egy adott cellát.
```csharp
//Az első munkalap elérése
Worksheet ws = wb.Worksheets[0];
//Hozzáférés valamelyik cellához
Cell cell = ws.Cells["C4"];
```
## 4. lépés: Képletek hozzárendelése és a FormulaLocal kinyomtatása
 Végül rendeljük hozzá a`SUM` és`AVERAGE` képleteket a cellába, és nyomtassa ki az eredményt`FormulaLocal` értékeket.
```csharp
//Rendelje hozzá a SUM képletet, és nyomtassa ki a FormulaLocal-t
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//Rendeljen AVERAGE képletet, és nyomtassa ki a FormulaLocal-t
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## Következtetés
Ebben az oktatóanyagban megtanulta, hogyan implementálhat olyan cellaképletet, amely hasonló az Aspose.Cells for .NET tartományképlet helyi funkciójához. Egyéni létrehozásával`GlobalizationSettings` osztályban felülbírálhatja az Excel-függvények alapértelmezett viselkedését, és testreszabhatja a helyi függvényneveket az igényeinek megfelelően. Ez különösen akkor lehet hasznos, ha honosított vagy nemzetköziesített Excel-dokumentumokkal dolgozik.
## GYIK
###  Mi a célja a`GlobalizationSettings` class in Aspose.Cells?
 A`GlobalizationSettings` osztály az Aspose.Cells-ben lehetővé teszi a beépített Excel-függvények viselkedésének testreszabását, beleértve a helyi függvénynevek módosításának lehetőségét is.
###  Felülírhatom-e más függvények viselkedését, mint`SUM` and `AVERAGE`?
 Igen, felülírhatja bármely beépített Excel-függvény viselkedését, ha módosítja a`GetLocalFunctionName` módszer az Ön szokásában`GlobalizationSettings` osztály.
### Van mód a függvénynevek visszaállítására az alapértelmezett értékekre?
 Igen, visszaállíthatja a függvényneveket az egyéni eltávolításával`GlobalizationSettings` osztályban vagy egy üres karakterlánc visszaadásával a`GetLocalFunctionName` módszer.
### Használhatom ezt a funkciót egyéni függvények létrehozására az Aspose.Cellsben?
 Nem, a`GlobalizationSettings`osztályt úgy tervezték, hogy felülbírálja a beépített Excel-függvények viselkedését, nem pedig egyéni függvények létrehozására. Ha egyéni funkciókat kell létrehoznia, használhatja a`UserDefinedFunction` osztályban Aspose.Cells.
### Elérhető ez a funkció az Aspose.Cells for .NET összes verziójában?
 Igen, a`GlobalizationSettings` osztály, és a függvénynevek testreszabásának lehetősége az Aspose.Cells for .NET összes verziójában elérhető.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
