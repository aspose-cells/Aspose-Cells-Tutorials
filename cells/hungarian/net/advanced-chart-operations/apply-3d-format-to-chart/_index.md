---
title: 3D formátum alkalmazása a diagramra
linktitle: 3D formátum alkalmazása a diagramra
second_title: Aspose.Cells .NET Excel Processing API
description: Fedezze fel, hogyan készíthet lenyűgöző 3D diagramokat Excelben az Aspose.Cells for .NET segítségével. Kövesse egyszerű lépésről lépésre útmutatónkat.
weight: 10
url: /hu/net/advanced-chart-operations/apply-3d-format-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 3D formátum alkalmazása a diagramra

## Bevezetés

Egy olyan korban, ahol az adatok megjelenítése a legfontosabb, az adatok bemutatásának módja túlmutat az alapvető grafikonokon és diagramokon. Az olyan eszközökkel, mint az Aspose.Cells for .NET, lenyűgöző 3D-s diagramokkal emelheti az adatprezentációkat, amelyek nemcsak felkeltik a figyelmet, hanem hatékonyan továbbítják az információkat. Ez az útmutató végigvezeti Önt a 3D formátum diagramon történő alkalmazásának lépésein az Aspose.Cells segítségével, így a nyers adatokat vonzó megjelenítéssé alakítja át.

## Előfeltételek

Mielőtt belemerülnénk a 3D-s formátum diagramokra való alkalmazásának aprólékos dolgaiba, győződjön meg arról, hogy mindennel rendelkezik, amire szüksége van.

### Szoftverkövetelmények

- Visual Studio: Győződjön meg arról, hogy telepítve van a Visual Studio a .NET-alkalmazásokkal való együttműködéshez.
-  Aspose.Cells for .NET: Ha még nem tette meg, töltse le és telepítse az Aspose.Cells fájlt innen:[itt](https://releases.aspose.com/cells/net/).

### Kódolási környezet beállítása

1. Új .NET-projekt létrehozása: Nyissa meg a Visual Studio-t, válassza az „Új projekt létrehozása” lehetőséget, és válasszon egy konzolalkalmazást.
2. Az Aspose.Cells hivatkozás hozzáadása: A NuGet Package Manageren keresztül adja hozzá az Aspose.Cells fájlt a rákereséssel vagy a Package Manager konzolon keresztül:

```bash
Install-Package Aspose.Cells
```

3. Kimeneti könyvtár beállítása: Jelöljön ki egy kimeneti könyvtárat, ahová a létrehozott fájlok mentésre kerülnek – ez olyan egyszerű lehet, mint egy mappa létrehozása az asztalon.

Most, hogy minden készen van, ideje belevágni a kódba, és káprázatos 3D diagramokat készíteni!

## Csomagok importálása

A kezdéshez importálnia kell a szükséges névtereket. Ez segít elérni az Aspose.Cells által biztosított osztályokat és metódusokat. Íme, hogyan kell ezt megtenni:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

Ez a rész a folyamatot kezelhető lépésekre bontja, így világosan megértheti az egyes szakaszokat.

## 1. lépés: Inicializálja a munkafüzetet

 Először is létre kell hoznia egy példányt a`Workbook` osztály. Ez az objektum szolgál majd az Excel dokumentum alapjául.

```csharp
//Kimeneti könyvtár
string outputDir = "Your Document Directory";
Workbook book = new Workbook();
```
 Gondolj erre`Workbook` üres vászonként – készen áll arra, hogy színes adatokkal és hatásos vizualizációkkal töltse meg.

## 2. lépés: Nevezze át az első munkalapot

Ezután nevezzük át az első munkalapot. Ez egyértelművé teszi, hogy milyen adatokkal dolgozunk.

```csharp
book.Worksheets[0].Name = "DataSheet";
```

A neveknek intuitívaknak kell lenniük. Ebben az esetben "DataSheet"-nek nevezzük el, hogy tudjuk, hol vannak az adataink.

## 3. lépés: Hozzon létre adatokat a diagramhoz

Most hozzáadunk néhány adatot az „Adatlapunkhoz”. Töltsük fel a diagramunk által használt értékekkel.

```csharp
Worksheet dataSheet = book.Worksheets["DataSheet"];
dataSheet.Cells["B1"].PutValue(1);
dataSheet.Cells["B2"].PutValue(2);
dataSheet.Cells["B3"].PutValue(3);
dataSheet.Cells["A1"].PutValue("A");
dataSheet.Cells["A2"].PutValue("B");
dataSheet.Cells["A3"].PutValue("C");
```

Ahogy a recept az összetevőktől függ, a diagram hatékonysága a bemeneti adatok minőségétől és szervezettségétől függ.

## 4. lépés: Állítson be egy új diagrammunkalapot

Ideje új munkalapot létrehozni magának a diagramnak. Ez segít megőrizni az adatok vizualizációját.

```csharp
Worksheet sheet = book.Worksheets.Add("MyChart");
```

Tekintse ezt a munkalapot a saját színpadának – ahol az adatok teljesítménye kibontakozik.

## 5. lépés: Adjon hozzá egy diagramot

Itt egy oszlopdiagramot adunk hozzá az újonnan létrehozott munkalaphoz.  

```csharp
ChartCollection charts = sheet.Charts;
int chartSheetIdx = charts.Add(ChartType.Column, 5, 0, 25, 15);
```

Meghatározunk egy helyet a diagramunk számára, és meghatározzuk, hogy milyen típusú. Gondoljon csak úgy, mint a keret típusának kiválasztására a műalkotáshoz.

## 6. lépés: A diagram megjelenésének testreszabása

Most pedig szabjuk testre diagramunk kinézetét a háttérszínek beállításával. 

```csharp
Aspose.Cells.Charts.Chart chart = book.Worksheets["MyChart"].Charts[0];
chart.PlotArea.Area.BackgroundColor = Color.White;
chart.ChartArea.Area.BackgroundColor = Color.White;
chart.PlotArea.Area.ForegroundColor = Color.White;
chart.ChartArea.Area.ForegroundColor = Color.White;
chart.ShowLegend = false;
```

A tiszta fehér háttér gyakran kiemeli az adatok színeit, javítva a láthatóságot.

## 7. lépés: Adja hozzá az adatsorokat a diagramhoz

Ideje betáplálni a diagramunkat az adatokkal. Hozzáadunk egy adatsort az „Adatlapunkból”, hogy biztosítsuk, hogy diagramunk tükrözze a szükséges adatokat.

```csharp
chart.NSeries.Add("DataSheet!B1:B3", true);
chart.NSeries.CategoryData = "DataSheet!A1:A3";
```

Ez hasonló ahhoz, hogy a szakács meghatározott összetevőkből készítsen ételt. Minden adatpont számít!

## 8. lépés: Az adatsorozat elérése és formázása

Most, hogy adataink össze vannak kapcsolva, fogjuk meg az adatsorokat, és kezdjünk el néhány 3D hatást alkalmazni.

```csharp
Aspose.Cells.Charts.Series ser = chart.NSeries[0];
ShapePropertyCollection spPr = ser.ShapeProperties;
Format3D fmt3d = spPr.Format3D;
```

Arra készülünk, hogy egy kis ízt adjunk ételünkhöz – gondoljon rá úgy, mint egy fűszerezésre, amely javítja az általános ízt.

## 9. lépés: Alkalmazza a 3D ferde hatásokat

Ezután egy ferde hatást adunk hozzá, hogy a diagramunknak némi dimenziót adjunk.

```csharp
Bevel bevel = fmt3d.TopBevel;
bevel.Type = BevelPresetType.Circle;
bevel.Height = 2;
bevel.Width = 5;
```

Csakúgy, mint a szobrász a követ formálja, mi is mélységet hozunk létre, amely életre kelt diagramunkat!

## 10. lépés: A felület anyagának és világításának testreszabása

Tegyük fényessé diagramunkat! Beállítjuk a felület anyagát és a világítás beállításait.

```csharp
fmt3d.SurfaceMaterialType = PresetMaterialType.WarmMatte;
fmt3d.SurfaceLightingType = LightRigType.ThreePoint;
fmt3d.LightingAngle = 20;
```

A megfelelő világítás és anyag a lapos tárgyat magával ragadó látványvilággá alakíthatja. Gondoljon egy professzionálisan megvilágított filmre, amely minden jelenetet kiemel.

## 11. lépés: Utolsó simítások a sorozat megjelenésén

Most véglegesítsük adatsoraink megjelenését a színének módosításával.

```csharp
ser.Area.BackgroundColor = Color.Maroon;
ser.Area.ForegroundColor = Color.Maroon;
ser.Border.Color = Color.Maroon;
```

A megfelelő szín bizonyos érzéseket és reakciókat válthat ki – a gesztenyebarna egy csipetnyi eleganciát és kifinomultságot kölcsönöz.

## 12. lépés: Mentse el a munkafüzetet

Végre itt az ideje, hogy megmentse remekművét! Ne felejtse el megadni a célhelyet, ahol tárolni szeretné.

```csharp
book.Save(outputDir + "outputApplying3DFormat.xlsx");
Console.WriteLine("Applying3DFormat executed successfully.");
```

Munkájának mentése olyan, mintha művészetét egy galériába tenné; ez egy pillanat a dédelgetésre és a megosztásra.

## Következtetés

Gratulálok! Sikeresen készített egy tetszetős 3D diagramot az Aspose.Cells for .NET segítségével. Ha követi ezeket a lépéseket, akkor most egy hatékony eszköz áll rendelkezésére, amellyel javíthatja adatbemutatóit, így azok nem csak informatívak, hanem vizuálisan is lenyűgözőek. A diagramok finomítása során ne feledje, hogy minden vizualizáció egy történet – legyen vonzó, világos és hatásos!

## GYIK

### Mi az Aspose.Cells a .NET számára?
Az Aspose.Cells for .NET egy hatékony könyvtár, amely lehetővé teszi a fejlesztők számára az Excel-dokumentumok programozott kezelését, beleértve diagramok és diagramok létrehozását.

### Testreszabhatom a diagramtípusokat az Aspose.Cellsben?
Igen! Az Aspose.Cells különféle diagramtípusokat támogat, például oszlopot, vonalat, kört és még sok mást, amelyek könnyen testreszabhatók.

### Létezik ingyenes próbaverzió az Aspose.Cells számára?
 Teljesen! Ingyenes próbaverziót letölthet a webhelyről[itt](https://releases.aspose.com/).

### Alkalmazhatok más effektusokat a diagramokra a 3D formátumokon kívül?
Igen, alkalmazhat különféle effektusokat, például árnyékokat, színátmeneteket és különböző stílusokat, hogy a diagramjait a 3D-n túlmutatóan javítsa.

### Hol találok támogatást az Aspose.Cells számára?
 Támogatásért látogassa meg a[Aspose fórum](https://forum.aspose.com/c/cells/9) közösségi segítségért és segítségért.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
