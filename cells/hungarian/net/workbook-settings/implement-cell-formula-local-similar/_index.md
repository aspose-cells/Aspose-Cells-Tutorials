---
"description": "Ismerd meg, hogyan valósíthatsz meg egy olyan cellaképletet, amely hasonló a .NET-ben található Aspose.Cells tartományképlet helyi funkcionalitásához. Tanuld meg a beépített Excel függvények nevének testreszabását és egyebeket."
"linktitle": "Cellaképlet Lokális implementálása Hasonlóan a Tartományképlet Lokálishoz"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Cellaképlet Lokális implementálása Hasonlóan a Tartományképlet Lokálishoz"
"url": "/hu/net/workbook-settings/implement-cell-formula-local-similar/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Cellaképlet Lokális implementálása Hasonlóan a Tartományképlet Lokálishoz

## Bevezetés
Az Aspose.Cells for .NET egy hatékony és rugalmas táblázatkezelő API, amely lehetővé teszi Excel-fájlok programozott létrehozását, kezelését és konvertálását. Az Aspose.Cells számos funkciójának egyike a beépített Excel-függvények viselkedésének testreszabása, beleértve a saját helyi függvénynevek létrehozásának lehetőségét is. Ebben az oktatóanyagban végigvezetjük Önt azon lépéseken, hogyan valósíthat meg egy olyan cellaképletet, amely hasonló az Aspose.Cells for .NET helyi tartományképlet-funkcionalitásához.
## Előfeltételek
Mielőtt elkezdené, győződjön meg arról, hogy a következőkkel rendelkezik:
1. A rendszerére telepítve van a Microsoft Visual Studio 2010 vagy újabb verziója.
2. Az Aspose.Cells for .NET könyvtár legújabb verziója telepítve van a projektedben. A könyvtárat letöltheted innen: [Aspose.Cells .NET letöltési oldal](https://releases.aspose.com/cells/net/).
## Csomagok importálása
kezdéshez importálnod kell a szükséges csomagokat a C# projektedbe. Add hozzá a következő using utasításokat a kódfájl elejéhez:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## 1. lépés: Egyéni globalizációs beállítások osztályának létrehozása
Az első lépés egy egyéni beállítás létrehozása `GlobalizationSettings` osztály, amely lehetővé teszi az Excel függvények alapértelmezett viselkedésének felülbírálását. Ebben a példában a következő neveket fogjuk megváltoztatni: `SUM` és `AVERAGE` funkciók `UserFormulaLocal_SUM` és `UserFormulaLocal_AVERAGE`, rendre.
```csharp
class GS : GlobalizationSettings
{
    public override string GetLocalFunctionName(string standardName)
    {
        //Módosítsa a SZUM függvény nevét az igényei szerint.
        if (standardName == "SUM")
        {
            return "UserFormulaLocal_SUM";
        }
        //Módosítsa az ÁTLAG függvény nevét az igényei szerint.
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## 2. lépés: Új munkafüzet létrehozása és az egyéni globalizációs beállítások hozzárendelése
Ezután hozzon létre egy új munkafüzet-példányt, és rendelje hozzá az egyéni `GlobalizationSettings` megvalósítási osztály a munkafüzethez `Settings.GlobalizationSettings` ingatlan.
```csharp
//Munkafüzet létrehozása
Workbook wb = new Workbook();
//Globalizációs beállítások implementációs osztály hozzárendelése
wb.Settings.GlobalizationSettings = new GS();
```
## 3. lépés: Az első munkalap és egy cella elérése
Most pedig lépjünk be a munkafüzet első munkalapjába és egy adott cellába azon belül.
```csharp
//Első munkalap elérése
Worksheet ws = wb.Worksheets[0];
//Hozzáférés bizonyos cellákhoz
Cell cell = ws.Cells["C4"];
```
## 4. lépés: Képletek hozzárendelése és a FormulaLocal kinyomtatása
Végül rendeljük hozzá a `SUM` és `AVERAGE` képleteket a cellába, és kinyomtatja az eredményt `FormulaLocal` értékek.
```csharp
//Rendeljen hozzá SZUM képletet, és írja ki a FormulaLocal értékét
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//Rendeljen hozzá ÁTLAG képletet, és írja ki a FormulaLocal értékét.
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## Következtetés
Ebben az oktatóanyagban megtanultad, hogyan valósíthatsz meg egy olyan cellaképletet, amely hasonló az Aspose.Cells for .NET helyi tartományképlet-funkcionalitásához. Egyéni `GlobalizationSettings` osztályban felülbírálhatja az Excel-függvények alapértelmezett viselkedését, és testreszabhatja a helyi függvényneveket az igényeinek megfelelően. Ez különösen hasznos lehet lokalizált vagy nemzetközi Excel-dokumentumokkal való munka esetén.
## GYIK
### Mi a célja a `GlobalizationSettings` osztály az Aspose.Cells-ben?
A `GlobalizationSettings` Az Aspose.Cells osztálya lehetővé teszi a beépített Excel-függvények viselkedésének testreszabását, beleértve a helyi függvénynevek módosításának lehetőségét is.
### Felülírhatom-e a függvények viselkedését a következőn kívül? `SUM` és `AVERAGE`?
Igen, bármelyik beépített Excel-függvény viselkedését felülírhatja a következő módosításával: `GetLocalFunctionName` módszer az Ön egyéni `GlobalizationSettings` osztály.
### Van mód arra, hogy a függvények neveit visszaállítsuk az alapértelmezett értékekre?
Igen, a függvényneveket visszaállíthatod az egyéni nevek eltávolításával `GlobalizationSettings` osztályból, vagy egy üres karakterlánc visszaadásával a `GetLocalFunctionName` módszer.
### Használhatom ezt a funkciót egyéni függvények létrehozására az Aspose.Cells-ben?
Nem, a `GlobalizationSettings` Az osztály célja a beépített Excel-függvények viselkedésének felülbírálása, nem pedig egyéni függvények létrehozása. Ha egyéni függvényeket kell létrehoznia, használhatja a `UserDefinedFunction` osztály az Aspose.Cells-ben.
### Ez a funkció az Aspose.Cells for .NET összes verziójában elérhető?
Igen, a `GlobalizationSettings` osztály és a függvénynevek testreszabásának lehetősége az Aspose.Cells for .NET összes verziójában elérhető.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}