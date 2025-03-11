---
title: Körhivatkozás észlelése programozottan az Excelben
linktitle: Körhivatkozás észlelése programozottan az Excelben
second_title: Aspose.Cells .NET Excel Processing API
description: Könnyen észlelheti a körkörös hivatkozásokat az Excelben az Aspose.Cells for .NET segítségével. Kövesse lépésenkénti útmutatónkat a pontos számítások biztosításához a táblázatokban.
weight: 13
url: /hu/net/excel-formulas-and-calculation-options/detecting-circular-reference/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Körhivatkozás észlelése programozottan az Excelben

## Bevezetés
Az Excel-fájlokkal való munka során az egyik leginkább frusztráló probléma, amellyel találkozhat, a körkörös hivatkozás. Ez akkor fordul elő, ha egy képlet közvetlenül vagy közvetve a saját cellájára hivatkozik, és olyan ciklust hoz létre, amely megzavarhatja az Excel számítási motorját. De ne félj! Az Aspose.Cells for .NET segítségével programozottan észlelheti ezeket a kellemetlen körkörös hivatkozásokat, így biztosítva, hogy táblázatai működőképesek és pontosak maradjanak. Ebben az útmutatóban lépésről lépésre végigvezetjük a folyamaton, és ez olyan egyszerű, mint a pite.
## Előfeltételek
Mielőtt belemerülnénk a körkörös hivatkozások felderítésének aprólékos dolgaiba, győződjön meg arról, hogy rendelkezik mindennel, ami az induláshoz szükséges:
1. Visual Studio: Győződjön meg arról, hogy a Visual Studio telepítve van a gépen. Ez lesz az Ön fejlesztési környezete.
2. .NET-keretrendszer: Győződjön meg arról, hogy a .NET-keretrendszer kompatibilis verzióját használja (legalább .NET-keretrendszer 4.0).
3.  Aspose.Cells Library: rendelkeznie kell az Aspose.Cells könyvtárral. Letöltheti a[Aspose honlapja](https://releases.aspose.com/cells/net/).
4. Alapvető C# ismerete: A C# programozás ismerete előnyt jelent, mivel ezen a nyelven fogunk kódot írni.
5. Excel-fájl: Készítsen egy Excel-fájlt, amely körkörös hivatkozásokat tartalmaz teszteléshez. Létrehozhat egy egyszerűt, vagy letölthet egy mintát.
Most, hogy megvannak az előfeltételeink, térjünk át a szórakoztató részre!
## Csomagok importálása
A kódolás megkezdése előtt importálnia kell a szükséges csomagokat. Íme, hogyan kell csinálni:
### Hozzon létre egy új projektet
- Nyissa meg a Visual Studio-t, és hozzon létre egy új C# Console Application projektet.
### Adja hozzá az Aspose.Cells Reference hivatkozást
- Kattintson a jobb gombbal a projektre a Solution Explorerben.
- Válassza a "NuGet-csomagok kezelése" lehetőséget.
- Keresse meg az „Aspose.Cells” kifejezést, és telepítse a legújabb verziót.
### Importálja a szükséges névtereket
 A te tetején`Program.cs` fájlt, importálja a szükséges névtereket:
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Most, hogy mindent beállítottunk, merüljünk el a kódban, hogy felfedezzük a körkörös hivatkozásokat egy Excel-fájlban.
## 1. lépés: Határozza meg a beviteli könyvtárat
Először is meg kell adnia azt a könyvtárat, ahol az Excel fájl található. Itt töltheti be az Excel fájlt.
```csharp
// Bemeneti könyvtár
string sourceDir = "Your Document Directory";
```
 Cserélje ki`"Your Document Directory"` az Excel-fájl tényleges elérési útjával.
## 2. lépés: Töltse be a munkafüzetet a LoadOptions segítségével
Ezután töltse be az Excel-munkafüzetet. Itt kezdődik a varázslat!
```csharp
LoadOptions loadOptions = new LoadOptions();
var objWB = new Aspose.Cells.Workbook(sourceDir + "Circular Formulas.xls", loadOptions);
```
 Itt egy új példányt hozunk létre`LoadOptions` és a munkafüzet betöltése a megadott elérési útról. Győződjön meg róla, hogy az Excel fájl neve megegyezik!
## 3. lépés: Engedélyezze az iterációs beállításokat
A körkörös hivatkozások engedélyezéséhez engedélyeznie kell az iterációs beállításokat a munkafüzetben.
```csharp
objWB.Settings.Iteration = true;
```
Ez arra utasítja az Aspose.Cells-t, hogy engedélyezze a körkörös hivatkozásokat a számítás során.
## 4. lépés: Számítási beállítások és kör alakú monitor létrehozása
Most hozzuk létre a számítási lehetőségeket és az egyéni kör alakú monitorunkat.
```csharp
CalculationOptions copts = new CalculationOptions();
CircularMonitor cm = new CircularMonitor();
copts.CalculationMonitor = cm;
```
 Itt egy példányt hozunk létre`CalculationOptions` és egy szokás`CircularMonitor`Ez a monitor segít nyomon követni a számítások során talált körkörös hivatkozásokat.
## 5. lépés: Számítsa ki a képleteket
Most itt az ideje, hogy kiszámítsa a képleteket a munkafüzetében.
```csharp
objWB.CalculateFormula(copts);
```
Ez a sor hajtja végre a számítást és ellenőrzi a körkörös hivatkozásokat.
## 6. lépés: Számolja össze a körleveleket
A számítás után megszámolhatja, hogy hány körhivatkozást találtak.
```csharp
long lngCircularRef = cm.circulars.Count;
Console.WriteLine("Circular References found - " + lngCircularRef);
```
Ez kiírja az Excel-fájlban észlelt körkörös hivatkozások számát.
## 7. lépés: Eredmények megjelenítése
Végül jelenítsük meg az eredményeket, és erősítsük meg, hogy a módszerünk sikeresen végrehajtódott.
```csharp
Console.WriteLine("DetectCircularReference executed successfully.\r\n");
```
## 8. lépés: Valósítsa meg a CircularMonitor osztályt
 A folyamat befejezéséhez végre kell hajtania a`CircularMonitor` osztály. Ez az osztály örökölni fog`AbstractCalculationMonitor` és kezeli a körkörös hivatkozások észlelését.
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
Ez az osztály rögzíti az egyes talált körkörös hivatkozások részleteit, beleértve a munkalap nevét és a cella indexét.
## Következtetés
körkörös hivatkozások észlelése az Excelben az Aspose.Cells for .NET használatával egyszerű folyamat, miután kezelhető lépésekre bontja. Az útmutató követésével könnyedén azonosíthatja és kezelheti a körkörös hivatkozásokat a táblázatokban, így biztosítva, hogy számításai pontosak és megbízhatóak maradjanak. Akár tapasztalt fejlesztő, akár csak kezdő, az Aspose.Cells hatékony eszközöket kínál az Excel manipulációs képességeinek javításához. 
## GYIK
### Mi az a körkörös hivatkozás az Excelben?
A körkörös hivatkozás akkor fordul elő, amikor egy képlet a saját cellájára hivatkozik, ami végtelen ciklust okoz a számításokban.
### Hogyan ismerhetem fel programozottan a körkörös hivatkozásokat?
A .NET Aspose.Cells könyvtárát használhatja a körkörös hivatkozások programozott észlelésére egy egyéni számításfigyelő megvalósításával.
### Mik az Aspose.Cells használatának előfeltételei?
Telepíteni kell a Visual Studio-t, a .NET-keretrendszert és az Aspose.Cells könyvtárat.
### Használhatom ingyenesen az Aspose.Cells-t?
Igen, az Aspose.Cells ingyenes próbaverziót kínál, amellyel felfedezheti funkcióit.
### Hol találhatok több információt az Aspose.Cells-ről?
 Meglátogathatja a[Aspose.Cells dokumentáció](https://reference.aspose.com/cells/net/) részletes információkért és példákért.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
