---
"description": "Tanuld meg, hogyan adhatsz hozzá egyszerűen képeket Excel-diagramokhoz az Aspose.Cells for .NET segítségével. Javítsd diagramjaidat és prezentációidat néhány egyszerű lépésben."
"linktitle": "Kép hozzáadása a diagramhoz"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Kép hozzáadása a diagramhoz"
"url": "/hu/net/inserting-controls-in-charts/add-picture-to-chart/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Kép hozzáadása a diagramhoz

## Bevezetés

Elege van az unalmas, személyeskedés nélküli diagramokból? Szeretné megtanulni, hogyan dobhatja fel Excel-vizualizációit képek hozzáadásával? Nos, szerencséje van! Ebben az oktatóanyagban elmerülünk az Aspose.Cells for .NET világában, és megtanuljuk, hogyan adhat hozzá képeket diagramokhoz Excelben. Szóval, fogja meg kedvenc csésze kávéját, és kezdjük is!

## Előfeltételek

Mielőtt belevágnánk a kódolás részleteibe, van néhány előfeltétel, aminek teljesülnie kell a zökkenőmentes végrehajtáshoz:

- Visual Studio: Itt fogod megírni és futtatni a .NET kódodat. Győződj meg róla, hogy telepítve van.
- Aspose.Cells .NET-hez: Erre a könyvtárra szükséged lesz az Excel-fájlok kezeléséhez. [töltsd le itt](https://releases.aspose.com/cells/net/).
- C# alapismeretek: Bár végigvezetlek a kódon, a C# alapjainak ismerete segít tisztábban látni a dolgokat.

### Telepítési lépések

1. Az Aspose.Cells telepítése: Az Aspose.Cells fájlt a NuGet csomagkezelőn keresztül adhatod hozzá a Visual Studio projektedhez. Ehhez lépj az Eszközök > NuGet csomagkezelő > Megoldáshoz tartozó NuGet csomagok kezelése menüpontra, és keresd meg az „Aspose.Cells” fájlt. Kattints a Telepítés gombra.
2. Projekt beállítása: Hozz létre egy új C# konzolos alkalmazásprojektet a Visual Studióban.

## Csomagok importálása

Miután mindent beállítottál, a következő lépés a szükséges csomagok importálása a projektedbe. Így csináld:

### Importálja a szükséges névtereket

A C# kódfájl tetején a következő névtereket kell importálnod:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
using System.IO;
```

Ez azt mondja a programodnak: „Hé! Használni fogom ezeket a klassz funkciókat az Aspose.Cells-ből.”

Most, hogy megvannak az előfeltételeink, bontsuk le a folyamatot apró lépésekre. 

## 1. lépés: A könyvtárak meghatározása

Először is be kell állítanunk a bemeneti és kimeneti fájlok elérési útját. Ez a lépés azért kulcsfontosságú, mert tudnunk kell, hol találjuk a meglévő Excel-fájlt, és hová mentsük a módosított fájlt.

```csharp
//Forráskönyvtár
string sourceDir = "Your Document Directory/";

//Kimeneti könyvtár
string outputDir = "Your Output Directory/";
```

Csere `Your Document Directory` és `Your Output Directory` a számítógépeden található tényleges elérési utakkal. 

## 2. lépés: A meglévő munkafüzet betöltése

Most töltsük be a meglévő Excel fájlt, ahová a képet hozzá szeretnénk adni a diagramhoz.

```csharp
// Nyissa meg a meglévő fájlt.
Workbook workbook = new Workbook(sourceDir + "sampleAddingPictureInChart.xls");
```

Ez a kód megnyitja a munkafüzetet, így az szerkesztésre kész.

## 3. lépés: A képfolyam előkészítése

Mielőtt hozzáadnánk a képet, el kell olvasnunk a diagramba beszúrni kívánt képet. 

```csharp
// Szerezz be egy képfájlt a streambe.
FileStream stream = new FileStream(sourceDir + "sampleAddingPictureInChart.png", FileMode.Open, FileAccess.Read);
```

Győződjön meg róla, hogy a kép a megadott könyvtárba van mentve.

## 4. lépés: Célozd meg a diagramot

Most adjuk meg, hogy melyik diagramhoz adjuk hozzá a képet. Ebben a példában az első munkalap első diagramját fogjuk célba venni.

```csharp
// A tervezői táblázatot a második lapon találod.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

Bármelyik munkalapot elérheti az index megfelelő módosításával.

## 5. lépés: Kép hozzáadása a diagramhoz

Miután kiválasztottad a diagramot, itt az ideje hozzáadni a képet! 

```csharp
// Adjon hozzá egy új képet a diagramhoz.
Aspose.Cells.Drawing.Picture pic0 = chart.Shapes.AddPictureInChart(50, 50, stream, 200, 200);
```

Itt, `50` és `50` azok az X és Y koordináták, ahová a kép kerül, és `200` a kép szélessége és magassága.

## 6. lépés: A kép vonalformátumának testreszabása

Szeretnél egy kis csillogást adni a képednek? Testreszabhatod a szegélyét! Így teheted meg:

```csharp
// Szerezd meg a kép vonalformátum típusát.
Aspose.Cells.Drawing.LineFormat lineformat = pic0.Line; 

// Állítsa be a kötőjel stílusát.
lineformat.DashStyle = MsoLineDashStyle.Solid;

// Állítsa be a vonalvastagságot.
lineformat.Weight = 4;    
```

Ebben a kódrészletben kiválaszthatod a szegély kinézetét és vastagságát. Válassz bármilyen stílust, amely illik a prezentációdhoz!

## 7. lépés: A módosított munkafüzet mentése

Mindezen kemény munka után mentsük el a módosításokat a következő kódsor végrehajtásával:

```csharp
// Mentse el az excel fájlt.
workbook.Save(outputDir + "outputAddingPictureInChart.xls");
```

A képed sikeresen integrálva lett a diagramba, és a kimeneti fájlod készen áll a megtekintésre!

## 8. lépés: Siker jelzése

Végül hozzáadhat egy egyszerű üzenetet a művelet sikerességének megerősítéséhez:

```csharp
Console.WriteLine("AddingPictureInChart executed successfully.");
```

## Következtetés

Ebben az oktatóanyagban azt vizsgáltuk meg, hogyan adhatsz egy kis személyiséget Excel-diagramjaidhoz képek hozzáadásával az Aspose.Cells for .NET segítségével. Néhány egyszerű lépéssel a hétköznapi prezentációidat emlékezetessé teheted. Szóval, mire vársz? Próbáld ki, és hagyd, hogy a diagramjaid ragyogjanak!

## GYIK

### Több képet is hozzáadhatok egyetlen diagramhoz?
Igen! Felhívhatod a `AddPictureInChart` módszert többször, hogy annyi képet adj hozzá, amennyit csak szeretnél.

### Milyen képformátumokat támogat az Aspose.Cells?
Az Aspose.Cells számos képformátumot támogat, beleértve a PNG, JPEG, BMP és GIF fájlokat.

### Testreszabhatom a kép pozícióját?
Természetesen! Az X és Y koordináták a `AddPictureInChart` módszer lehetővé teszi a pontos pozicionálást.

### Ingyenesen használható az Aspose.Cells?
Az Aspose.Cells ingyenes próbaverziót kínál, de a teljes funkciók használatához licenc szükséges. Az árakat itt találja. [itt](https://purchase.aspose.com/buy).

### Hol találok további példákat?
Nézd meg a [Aspose.Cells dokumentáció](https://reference.aspose.com/cells/net/) részletesebb példákért és funkciókért.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}