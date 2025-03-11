---
title: Kép hozzáadása a diagramhoz
linktitle: Kép hozzáadása a diagramhoz
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan adhat hozzá egyszerűen képeket Excel-diagramokhoz az Aspose.Cells for .NET segítségével. Növelje diagramjait és prezentációit néhány egyszerű lépésben.
weight: 11
url: /hu/net/inserting-controls-in-charts/add-picture-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kép hozzáadása a diagramhoz

## Bevezetés

Eleged van az unalmas grafikonokból, amelyekből hiányzik a személyes érintés? Szeretné megtanulni, hogyan fűszerezheti Excel vizualitását képek hozzáadásával? Nos, szerencséd van! Ebben az oktatóanyagban belemerülünk az Aspose.Cells for .NET világába, és megtanuljuk, hogyan lehet képeket hozzáadni az Excel diagramjaihoz. Szóval, fogd meg kedvenc kávédat, és kezdjük is!

## Előfeltételek

Mielőtt belevágnánk a kódolás finomságába, van néhány előfeltétel, amelyeket simán be kell tartania:

- Visual Studio: Itt írhatja és futtathatja a .NET kódot. Győződjön meg arról, hogy telepítve van.
-  Aspose.Cells for .NET: Erre a könyvtárra lesz szüksége az Excel fájlokkal való munkavégzéshez. Tudod[töltse le itt](https://releases.aspose.com/cells/net/).
- A C# alapismeretei: Miközben végigvezetem a kódon, a C# alapjaival kapcsolatos fogantyú tisztább lesz a dolgokon.

### Telepítési lépések

1. Az Aspose.Cells telepítése: Az Aspose.Cells elemet a NuGet Package Manager segítségével adhatja hozzá Visual Studio projektjéhez. Ehhez nyissa meg az Eszközök > NuGet Csomagkezelő > NuGet Packages for Solution menüpontot, és keresse meg az „Aspose.Cells” kifejezést. Kattintson a Telepítés gombra.
2. A projekt beállítása: Hozzon létre egy új C#-konzolalkalmazás-projektet a Visual Studióban.

## Csomagok importálása

Miután mindent beállított, a következő lépés a szükséges csomagok importálása a projektbe. Íme, hogyan kell csinálni:

### Importálja a szükséges névtereket

A C# kódfájl tetején a következő névtereket kell importálnia:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
using System.IO;
```

Ez azt mondja a programodnak: „Hé! Használni fogom az Aspose.Cells nagyszerű szolgáltatásait.”

Most, hogy megvannak az előfeltételeink, bontsuk le a folyamatot falatnyi lépésekre. 

## 1. lépés: Határozza meg a könyvtárait

Először is be kell állítanunk a bemeneti és kimeneti fájljaink elérési útját. Ez a lépés döntő fontosságú, mert tudnunk kell, hol találjuk a meglévő Excel fájlunkat, és hova mentsük a módosított fájlt.

```csharp
//Forrás könyvtár
string sourceDir = "Your Document Directory/";

//Kimeneti könyvtár
string outputDir = "Your Output Directory/";
```

 Cserélje ki`Your Document Directory` és`Your Output Directory` tényleges elérési utakkal a számítógépén. 

## 2. lépés: Töltse be a meglévő munkafüzetet

Most töltsük be a meglévő Excel fájlt, ahová a képünket hozzá szeretnénk adni a diagramhoz.

```csharp
// Nyissa meg a meglévő fájlt.
Workbook workbook = new Workbook(sourceDir + "sampleAddingPictureInChart.xls");
```

Ez a kód megnyitja a munkafüzetet, és készen áll a szerkesztésre.

## 3. lépés: Készítse elő az Image Stream-et

A kép hozzáadása előtt el kell olvasnunk a diagramba beszúrni kívánt képet. 

```csharp
// Szerezzen be egy képfájlt az adatfolyamba.
FileStream stream = new FileStream(sourceDir + "sampleAddingPictureInChart.png", FileMode.Open, FileAccess.Read);
```

Győződjön meg arról, hogy a képet a megadott könyvtárba mentette.

## 4. lépés: Célozza meg a diagramot

Most pedig határozzuk meg, hogy melyik diagramhoz adjuk hozzá a képünket. Ebben a példában az első munkalap első diagramját célozzuk meg.

```csharp
// Szerezze be a tervezői diagramot a második lapon.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

Bármely munkalapot elérheti az index megfelelő módosításával.

## 5. lépés: Adja hozzá a képet a diagramhoz

Miután kiválasztotta a diagramot, ideje hozzáadni a képet! 

```csharp
// Adjon hozzá egy új képet a diagramhoz.
Aspose.Cells.Drawing.Picture pic0 = chart.Shapes.AddPictureInChart(50, 50, stream, 200, 200);
```

 Itt,`50` és`50` azok az X és Y koordináták, ahová a kép kerül, és`200` a kép szélessége és magassága.

## 6. lépés: A kép vonalformátumának testreszabása

Szeretnél némi hangulatot adni a képednek? A szegélyét személyre szabhatja! Íme, hogyan kell csinálni:

```csharp
// Szerezze be a kép vonalformátumának típusát.
Aspose.Cells.Drawing.LineFormat lineformat = pic0.Line; 

// Állítsa be a vonal stílusát.
lineformat.DashStyle = MsoLineDashStyle.Solid;

// Állítsa be a vonalvastagságot.
lineformat.Weight = 4;    
```

Ez a részlet lehetővé teszi a szegély megjelenésének és vastagságának kiválasztását. Válasszon bármilyen stílust, amely összecseng az előadásával!

## 7. lépés: Mentse el a módosított munkafüzetet

Ennyi kemény munka után mentsük el a módosításokat a következő kódsor végrehajtásával:

```csharp
// Mentse el az excel fájlt.
workbook.Save(outputDir + "outputAddingPictureInChart.xls");
```

Most a kép sikeresen beépült a diagramba, és a kimeneti fájl készen áll a megtekintésre!

## 8. lépés: Jelezze a sikert

Végül hozzáadhat egy egyszerű üzenetet, amely megerősíti, hogy a művelet sikeres volt:

```csharp
Console.WriteLine("AddingPictureInChart executed successfully.");
```

## Következtetés

Ebben az oktatóanyagban megvizsgáltuk, hogyan lehet egy kis egyéniséget adni Excel-diagramjainak képek hozzáadásával az Aspose.Cells for .NET segítségével. Néhány egyszerű lépéssel prezentációit hétköznapiból emlékezetessé emelheti. Szóval, mire vársz? Próbálja ki, és hagyja, hogy a diagramok ragyogjanak!

## GYIK

### Hozzáadhatok több képet egyetlen diagramhoz?
 Igen! Felhívhatja a`AddPictureInChart` módszerrel többször is hozzáadhat annyi képet, amennyit csak szeretne.

### Milyen képformátumokat támogat az Aspose.Cells?
Az Aspose.Cells számos képformátumot támogat, beleértve a PNG, JPEG, BMP és GIF formátumokat.

### Testreszabhatom a kép helyzetét?
 Biztosan! Az X és Y koordináták a`AddPictureInChart` módszer lehetővé teszi a pontos pozicionálást.

### Az Aspose.Cells ingyenesen használható?
Az Aspose.Cells ingyenes próbaverziót kínál, de a teljes szolgáltatáshoz licenc szükséges. Az árat megtalálod[itt](https://purchase.aspose.com/buy).

### Hol találok több példát?
 Nézze meg a[Aspose.Cells dokumentáció](https://reference.aspose.com/cells/net/) részletesebb példákért és funkciókért.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
