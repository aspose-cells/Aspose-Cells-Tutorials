---
title: Adja hozzá az ívet az Excel munkalapjához
linktitle: Adja hozzá az ívet az Excel munkalapjához
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan adhat hozzá íveket az Excel munkalapokhoz az Aspose.Cells for .NET segítségével. Kövesse lépésenkénti útmutatónkat a táblázatok kialakításának javításához.
weight: 16
url: /hu/net/excel-shapes-controls/add-arc-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adja hozzá az ívet az Excel munkalapjához

## Bevezetés
tetszetős Excel-táblázatok készítése kulcsfontosságú az adatok megjelenítéséhez, az Aspose.Cells könyvtár pedig robusztus eszközöket biztosít a fejlesztőknek e feladat elvégzéséhez. Az egyik érdekes funkció, amelyet érdemes beépíteni Excel-dokumentumaiba, az alakzatok, például ívek hozzáadásának képessége. Ebben az oktatóanyagban lépésről lépésre végigvezetjük, hogyan adhatunk íveket egy Excel-munkalaphoz az Aspose.Cells for .NET használatával. A cikk végére nemcsak az ívek hozzáadását tanulja meg, hanem általánosságban is betekintést nyerhet az alakzatok kezelésébe.
## Előfeltételek
Mielőtt belevetnénk magunkat az ívek munkalaphoz adásának bonyolultságába, elengedhetetlen, hogy bizonyos dolgok a helyükön legyenek. Íme az induláshoz szükséges előfeltételek:
1. Visual Studio: A Visual Studio-t telepítenie kell a számítógépére, mivel programozási nyelvként a C#-t fogjuk használni.
2. .NET-keretrendszer: Győződjön meg arról, hogy telepítve van a .NET-keretrendszer vagy a .NET Core. Az Aspose.Cells mindkettőt támogatja.
3. Aspose.Cells for .NET: rendelkeznie kell az Aspose.Cells könyvtárral. Letöltheti a[Aspose.Cells Letöltések](https://releases.aspose.com/cells/net/) oldalon.
4. A C# alapvető ismerete: A C# ismerete segít a kódrészletek követésében különösebb gond nélkül.
## Csomagok importálása
Az Aspose.Cells használatának megkezdéséhez a projektben importálnia kell a szükséges csomagokat. Íme, hogyan kell csinálni:
### Hozzon létre egy új projektet
- Nyissa meg a Visual Studio-t.
- Válassza az "Új projekt létrehozása" lehetőséget.
- Válasszon egy sablont, amely együttműködik a .NET-tel (például a konzolalkalmazással).
  
### Adja hozzá az Aspose.Cells hivatkozásokat
- Kattintson a jobb gombbal a projektre a Solution Explorerben.
- Válassza a "NuGet-csomagok kezelése" lehetőséget.
- Keresse meg az „Aspose.Cells” kifejezést, és telepítse.
Most készen áll az ívösszeadás kódolására.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Itt található a kód lépésenkénti lebontása, amely bemutatja, hogyan lehet íveket hozzáadni egy munkalaphoz az Excelben.
## 1. lépés: A címtár beállítása
Az első lépés egy könyvtár létrehozása, ahová menteni fogja az Excel-fájlt. Ez segít a kimeneti fájlok egyszerű kezelésében.
```csharp
string dataDir = "Your Document Directory";
// Hozzon létre könyvtárat, ha még nincs jelen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Ebben a kódrészletben megadjuk a dokumentumkönyvtár elérési útját. Azt is ellenőrizzük, hogy a könyvtár létezik-e; ha nem, akkor létrehozzuk. Ez megalapozza a teljesítményünket.
## 2. lépés: Példányosítson munkafüzetet
Ezután hozzunk létre egy új munkafüzet-példányt.
```csharp
// Példányosítson egy új munkafüzetet.
Workbook excelbook = new Workbook();
```
Ez a sor egy új Excel-munkafüzetet hoz létre. Tekintse ezt egy üres vászonnak, ahol alakzatokat, adatokat és egyebeket adhatunk hozzá.
## 3. lépés: Adja hozzá az első ív alakzatot
Most adjuk hozzá az első ívalakunkat a munkalaphoz.
```csharp
// Adjon hozzá egy ív alakzatot.
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
 Itt egy ívet adunk az első munkalaphoz. A paraméterek határozzák meg az ív helyzetét és méretét:`(left, top, width, height, startAngle, endAngle)`. Ez olyan, mint egy kör szakaszának ábrázolása!
## 4. lépés: Az első ív testreszabása
Az ív hozzáadása után érdemes lehet testreszabni a megjelenését.
```csharp
// Állítsa be a kitöltési forma színét
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
// Állítsa be az ív elhelyezését.
arc1.Placement = PlacementType.FreeFloating;           
// Állítsa be a vonalvastagságot.
arc1.Line.Weight = 1;      
// Állítsa be az ív kötőjel stílusát.
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Ebben a részben az ívet testreszabjuk. A kitöltési típust egyszínűre (ebben az esetben kékre) állítjuk, meghatározzuk az elhelyezését, meghatározzuk a vonalvastagságot, és kiválasztunk egy kötőjelstílust. Alapvetően felújítjuk az ívünket, hogy látványosan vonzó legyen!
## 5. lépés: Adjon hozzá egy második ív alakzatot
Adjunk hozzá egy másik ív alakzatot, hogy több kontextust biztosítsunk.
```csharp
// Adjon hozzá egy másik ív alakzatot.
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Az első ívhez hasonlóan egy második ívet adunk hozzá ugyanarra a munkalapra. A koordináták itt egy kicsit el vannak tolva, hogy másképp helyezkedjenek el.
## 6. lépés: A második ív testreszabása
Csakúgy, mint az első ívnél, a másodikat is testre szabjuk.
```csharp
// Állítsa be a vonal színét
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
// Állítsa be az ív elhelyezését.
arc2.Placement = PlacementType.FreeFloating;          
// Állítsa be a vonalvastagságot.
arc2.Line.Weight = 1;           
// Állítsa be az ív kötőjel stílusát.
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Itt a második ívnek ugyanazt a stílust adjuk, mint az elsőnek. A színt vagy a stílust tetszés szerint módosíthatja egyediség vagy tematikus célok érdekében.
## 7. lépés: Mentse el a munkafüzetet
Végül itt az ideje elmenteni az újonnan létrehozott munkafüzetet az ívekkel.
```csharp
// Mentse el az excel fájlt.
excelbook.Save(dataDir + "book1.out.xls");
```
Ez a sor úgy működik, mint a mentés gomb megnyomása. A munkánkat a megadott helyre mentjük, kijelölt fájlnévvel. Ügyeljen arra, hogy ellenőrizze a könyvtárát, hogy megtalálja remekművét Excel formátumban!
## Következtetés
Ebben az oktatóanyagban az Aspose.Cells for .NET segítségével ív alakzatok Excel-munkalapokhoz való hozzáadásának folyamatát vizsgáltuk. Egy egyszerű, lépésenkénti útmutatón keresztül megtanulta, hogyan hozhat létre új munkafüzetet, hogyan adhat hozzá íveket, testreszabhatja azok megjelenését, és hogyan mentheti el a dokumentumot. Ez a képesség nemcsak a táblázatok vizuális vonzerejét javítja, hanem az adatbemutatókat is informatívabbá teszi. Akár diagramokat, jelentéseket készít, akár csak kísérletezik, az olyan alakzatok, mint az ívek, kreatív csavart adhat projektjeihez.
## GYIK
### Mi az Aspose.Cells?
Az Aspose.Cells egy hatékony könyvtár, amely lehetővé teszi a fejlesztők számára Excel-fájlok létrehozását, kezelését és konvertálását programozottan, Microsoft Excel nélkül.
### Telepítenem kell a Microsoft Excelt az Aspose.Cells használatához?
Nem, az Aspose.Cells teljesen független, és nem szükséges a Microsoft Excel telepítése.
### Kipróbálhatom az Aspose.Cells-t ingyen?
 Igen, kipróbálhatja az Aspose.Cells-t a saját használatával[Ingyenes próbaverzió](https://releases.aspose.com/).
### Milyen programozási nyelveket támogat az Aspose.Cells?
Az Aspose.Cells több nyelvet támogat, beleértve a C#-ot, a VB.NET-et és még sok mást.
### Hol kaphatok támogatást az Aspose.Cells-hez?
 A támogatást a[Aspose fórum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
