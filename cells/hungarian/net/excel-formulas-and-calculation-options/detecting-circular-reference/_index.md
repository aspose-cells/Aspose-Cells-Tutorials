---
"description": "Könnyedén felismerheti a körkörös hivatkozásokat az Excelben az Aspose.Cells for .NET segítségével. Kövesse lépésről lépésre szóló útmutatónkat a táblázataiban szereplő pontos számítások biztosítása érdekében."
"linktitle": "Körhivatkozások észlelése Excelben programozottan"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Körhivatkozások észlelése Excelben programozottan"
"url": "/hu/net/excel-formulas-and-calculation-options/detecting-circular-reference/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Körhivatkozások észlelése Excelben programozottan

## Bevezetés
Az Excel-fájlokkal való munka során az egyik legbosszantóbb probléma, amivel találkozhatsz, a körkörös hivatkozás. Ez akkor fordul elő, amikor egy képlet közvetlenül vagy közvetve a saját cellájára hivatkozik vissza, ami egy ciklust hoz létre, ami megzavarhatja az Excel számítási motorját. De ne aggódj! Az Aspose.Cells for .NET segítségével programozottan észlelheted ezeket a bosszantó körkörös hivatkozásokat, biztosítva, hogy a táblázataid működőképesek és pontosak maradjanak. Ebben az útmutatóban lépésről lépésre végigvezetünk a folyamaton, így az gyerekjáték.
## Előfeltételek
Mielőtt belemerülnénk a körkörös hivatkozások észlelésének részleteibe, győződjünk meg róla, hogy minden a rendelkezésünkre áll, amire a kezdéshez szükségünk van:
1. Visual Studio: Győződjön meg róla, hogy a Visual Studio telepítve van a gépén. Ez lesz a fejlesztői környezete.
2. .NET-keretrendszer: Győződjön meg arról, hogy a .NET-keretrendszer kompatibilis verzióját használja (legalább a .NET-keretrendszer 4.0-s verzióját).
3. Aspose.Cells könyvtár: Szükséged lesz az Aspose.Cells könyvtárra. Letöltheted innen: [Aspose weboldal](https://releases.aspose.com/cells/net/).
4. C# alapismeretek: A C# programozásban való jártasság előnyös, mivel ebben a nyelvben fogunk kódot írni.
5. Excel fájl: Készítsen elő egy Excel fájlt, amely körhivatkozásokat tartalmaz teszteléshez. Létrehozhat egy egyszerűt, vagy letölthet egy mintát.
Most, hogy megvannak az előfeltételeink, térjünk át a mókás részre!
## Csomagok importálása
Mielőtt elkezdhetnéd a kódolást, importálnod kell a szükséges csomagokat. Így teheted meg:
### Új projekt létrehozása
- Nyisd meg a Visual Studiot, és hozz létre egy új C# konzolalkalmazás-projektet.
### Aspose.Cells hivatkozás hozzáadása
- Kattintson jobb gombbal a projektjére a Megoldáskezelőben.
- Válassza a „NuGet-csomagok kezelése” lehetőséget.
- Keresd meg az „Aspose.Cells” fájlt, és telepítsd a legújabb verziót.
### Szükséges névterek importálása
A te tetején `Program.cs` fájlban importálja a szükséges névtereket:
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Most, hogy mindent beállítottunk, nézzük meg a kódot, amely körkörös hivatkozásokat észlel egy Excel-fájlban.
## 1. lépés: A bemeneti könyvtár meghatározása
Először meg kell adnod azt a könyvtárat, ahol az Excel fájlod található. Ide fogod betölteni az Excel fájlt.
```csharp
// Beviteli könyvtár
string sourceDir = "Your Document Directory";
```
Csere `"Your Document Directory"` az Excel-fájl tényleges elérési útjával.
## 2. lépés: A munkafüzet betöltése a LoadOptions paranccsal
Ezután betöltöd az Excel munkafüzetedet. Itt kezdődik a varázslat!
```csharp
LoadOptions loadOptions = new LoadOptions();
var objWB = new Aspose.Cells.Workbook(sourceDir + "Circular Formulas.xls", loadOptions);
```
Itt létrehozunk egy új példányt a következőből: `LoadOptions` és a munkafüzet betöltése a megadott elérési útról. Győződjön meg róla, hogy az Excel fájlneve megegyezik!
## 3. lépés: Iterációs beállítások engedélyezése
körkörös hivatkozások engedélyezéséhez engedélyeznie kell az iterációs beállításokat a munkafüzetben.
```csharp
objWB.Settings.Iteration = true;
```
Ez arra utasítja az Aspose.Cells-t, hogy engedélyezze a körkörös hivatkozásokat a számítás során.
## 4. lépés: Számítási beállítások és kör alakú monitor létrehozása
Most hozzuk létre a számítási beállításokat és az egyéni kör alakú monitorunkat.
```csharp
CalculationOptions copts = new CalculationOptions();
CircularMonitor cm = new CircularMonitor();
copts.CalculationMonitor = cm;
```
Itt létrehozunk egy példányt a következőből: `CalculationOptions` és egy szokás `CircularMonitor`Ez a monitor segít nyomon követni a számítások során talált körhivatkozásokat.
## 5. lépés: Számítsa ki a képleteket
Most itt az ideje, hogy kiszámítsd a képleteket a munkafüzetedben.
```csharp
objWB.CalculateFormula(copts);
```
Ez a sor végrehajtja a számítást és ellenőrzi a körhivatkozásokat.
## 6. lépés: Kör alakú hivatkozások számlálása
A számítás után megszámolhatod, hogy hány körhivatkozást találtál.
```csharp
long lngCircularRef = cm.circulars.Count;
Console.WriteLine("Circular References found - " + lngCircularRef);
```
Ez kimenetileg megjeleníti az Excel-fájlban észlelt körhivatkozások számát.
## 7. lépés: Eredmények megjelenítése
Végül jelenítsük meg az eredményeket, és ellenőrizzük, hogy a metódusunk sikeresen végrehajtódott-e.
```csharp
Console.WriteLine("DetectCircularReference executed successfully.\r\n");
```
## 8. lépés: A CircularMonitor osztály megvalósítása
A folyamat befejezéséhez végre kell hajtania a következőt: `CircularMonitor` osztály. Ez az osztály örökölni fog ettől `AbstractCalculationMonitor` és kezeli a körkörös referenciák észlelését.
```csharp
public class CircularMonitor : AbstractCalculationMonitor
{
    public ArrayList circulars = new ArrayList();
    public ArrayList Circulars { get { return circulars; } }
    public override bool OnCircular(IEnumerator circularCellsData)
    {
        CalculationCell cc = null;
        ArrayList cur = new ArrayList();
        while (circularCellsData.MoveNext())
        {
            cc = (CalculationCell)circularCellsData.Current;
            cur.Add(cc.Worksheet.Name + "!" + CellsHelper.CellIndexToName(cc.CellRow, cc.CellColumn));
        }
        circulars.Add(cur);
        return true;
    }
}
```
Ez az osztály rögzíti az egyes talált körhivatkozások részleteit, beleértve a munkalap nevét és a cellaindexet.
## Következtetés
A körkörös hivatkozások észlelése Excelben az Aspose.Cells for .NET segítségével egy egyszerű folyamat, ha könnyen kezelhető lépésekre bontjuk. Ezt az útmutatót követve könnyedén azonosíthatja és kezelheti a körkörös hivatkozásokat a táblázataiban, biztosítva, hogy a számításai pontosak és megbízhatóak maradjanak. Akár tapasztalt fejlesztő, akár most kezd, az Aspose.Cells hatékony eszközöket kínál az Excel-manipulációs képességek fejlesztéséhez. 
## GYIK
### Mi az a körhivatkozás az Excelben?
Körhivatkozásról akkor beszélünk, amikor egy képlet a saját cellájára hivatkozik vissza, ami végtelen ciklust eredményez a számításokban.
### Hogyan tudom programozottan felismerni a körkörös hivatkozásokat?
A .NET Aspose.Cells könyvtárával programozottan észlelheti a körkörös hivatkozásokat egy egyéni számítási monitor megvalósításával.
### Milyen előfeltételei vannak az Aspose.Cells használatának?
Telepítenie kell a Visual Studio-t, a .NET-keretrendszert és az Aspose.Cells könyvtárat.
### Ingyenesen használhatom az Aspose.Cells-t?
Igen, az Aspose.Cells ingyenes próbaverziót kínál, amellyel felfedezheti a funkcióit.
### Hol találok több információt az Aspose.Cells-ről?
Meglátogathatod a [Aspose.Cells dokumentáció](https://reference.aspose.com/cells/net/) részletes információkért és példákért.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}