---
title: Állítsa be a diagram adatcímkéinek alaktípusát
linktitle: Állítsa be a diagram adatcímkéinek alaktípusát
second_title: Aspose.Cells .NET Excel Processing API
description: Az Aspose.Cells for .NET segítségével testreszabott adatcímke-alakzatokkal javíthatja Excel-diagramjait. Kövesse ezt a lépésről-lépésre szóló útmutatót az adatok megjelenítésének javításához.
weight: 14
url: /hu/net/advanced-chart-operations/set-shape-type-of-data-labels-of-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Állítsa be a diagram adatcímkéinek alaktípusát

## Bevezetés

Az adatvizualizáció világában a diagramok az összetett információk hozzáférhető módon történő bemutatásának egyik fő módszere. Azonban nem minden adatcímke egyforma! Néha meg kell jeleníteni a címkéket, és a különböző formák használata jelentős változást hozhat. Ha egyéni alakzatokkal szeretné bővíteni az Excel-diagramok adatcímkéit, akkor a megfelelő helyre került. Ez az útmutató végigvezeti Önt, hogyan állíthatja be az adatcímkék alaktípusát egy diagramon az Aspose.Cells for .NET segítségével. Merüljünk el benne!

## Előfeltételek

Mielőtt belevágnánk a kódolásba, győződjünk meg arról, hogy minden megfelelően van beállítva. Íme, amire szüksége lesz:

1.  Aspose.Cells for .NET: Ha még nem tette meg, töltse le a[Aspose honlapja](https://releases.aspose.com/cells/net/). Ez a könyvtár mindenféle manipulációt tesz lehetővé az Excel dokumentumokkal.
2. Visual Studio: A .NET-alkalmazások írásához és futtatásához ezt telepítenie kell a rendszerére. Győződjön meg arról, hogy az a verzió támogatja a .NET-keretrendszert vagy a .NET Core-t a projekt igényei szerint.
3. C# alapvető ismerete: Az alapvető programozási fogalmak és a C# szintaxis ismerete minden bizonnyal segít a kódrészletek jobb megértésében.
4. Excel-fájl: A munkavégzéshez szükség lesz egy minta Excel-munkafüzetre is. Létrehozhat sajátot, vagy használhat bármilyen meglévőt.

Most, hogy megvannak az előfeltételek, ugorjunk bele!

## Csomagok importálása

A kódolás megkezdése előtt importálnia kell a megfelelő Aspose.Cells névtereket. Ez hozzáférést biztosít a könyvtár által kínált gazdag funkciókhoz. Íme, hogyan kell csinálni:

### Az Aspose.Cells importálása

Nyissa meg a Visual Studio projektet, és adja hozzá a következőket a C#-fájl tetejéhez.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
```

Ezek a névterek lehetővé teszik a munkafüzetek, munkalapok és diagramok egyszerű létrehozását és kezelését.

Most, hogy készen vagyunk, merüljünk bele a kódolási részbe! Az egyértelműség kedvéért lépésről lépésre bontjuk le.

## 1. lépés: Határozza meg a könyvtárait

Először is határozzuk meg, hol találhatók a fájlok – mind a forrásfájlban, mind a célmappában, ahová menteni szeretné a módosított fájlt.

```csharp
// Forrás könyvtár
string sourceDir = "Your Document Directory";

// Kimeneti könyvtár
string outputDir = "Your Output Directory";
```

 Cserélje ki`"Your Document Directory"` és`"Your Output Directory"` a gépén lévő tényleges útvonalakkal.

## 2. lépés: Töltse be az Excel forrásfájlt

Ezután be kell töltenie azt az Excel-fájlt, amellyel dolgozni szeretne. Itt kezdődik a varázslat!

```csharp
// Forrás Excel fájl betöltése
Workbook wb = new Workbook(sourceDir + "sampleSetShapeTypeOfDataLabelsOfChart.xlsx");
```

 Ez a sor újat hoz létre`Workbook` objektumot, és rámutat a meglévő fájljára. Győződjön meg arról, hogy a fájl elérési útja helyes!

## 3. lépés: Nyissa meg az első munkalapot

Most, hogy megvan a munkafüzetünk, hozzá kell férnünk a testreszabni kívánt diagramot tartalmazó munkalaphoz.

```csharp
// Az első munkalap elérése
Worksheet ws = wb.Worksheets[0];
```

 Itt elérjük az első munkalapot (index`0`). Állítsa be az indexet, ha a diagram egy másik lapon található.

## 4. lépés: Nyissa meg az első diagramot

Miután megkapta a munkalapot, ideje elérni a diagramot. Minden munkalap több diagramot is tartalmazhat, de az egyszerűség kedvéért itt maradunk az elsőnél.

```csharp
// Hozzáférés az első diagramhoz
Chart ch = ws.Charts[0];
```

Ismételten, ha a kívánt diagram nem az első, egyszerűen módosítsa az indexet ennek megfelelően.

## 5. lépés: Nyissa meg a diagramsorozatot

Mivel a diagram már elérhető, mélyebbre kell merülnie az adatcímkék módosításához. A sorozat a diagram adatpontjait képviseli.

```csharp
// Hozzáférés az első sorozathoz
Series srs = ch.NSeries[0];
```

Itt az első sorozatot célozzuk meg, amely általában azokat a címkéket tartalmazza, amelyeket esetleg módosítani szeretne.

## 6. lépés: Állítsa be az adatcímkék alaktípusát

Most jöjjön a döntő rész! Állítsuk be az adatcímkék alaktípusát. Az Aspose.Cells különféle alakzatokat támogat, és ebben a példában egy ovális beszédbuborékot választunk a szórakoztató érintés érdekében.

```csharp
// Állítsa be az adatcímkék alaktípusát, pl. Speech Bubble Oval
srs.DataLabels.ShapeType = DataLabelShapeType.WedgeEllipseCallout;
```

 Nyugodtan kísérletezzen különböző alaktípusokkal a változtatással`DataLabelShapeType.WedgeEllipseCallout` más elérhető lehetőségekre!

## 7. lépés: Mentse el a kimeneti Excel fájlt

Elvégezte a nehéz emelést, és most itt az ideje, hogy mentse a munkáját. Tegyük vissza a módosított adatcímke alakzatot egy Excel-fájlba.

```csharp
// Mentse el a kimeneti Excel fájlt
wb.Save(outputDir + "outputSetShapeTypeOfDataLabelsOfChart.xlsx");
```

Ezzel elmenti a módosított munkafüzetet a megadott kimeneti könyvtárba.

## 8. lépés: Végezze el és hagyja jóvá

Végül itt az ideje a program futtatásának. A végrehajtás után látnia kell az üzenetet, amely megerősíti, hogy minden simán ment!

```csharp
Console.WriteLine("SetShapeTypeOfDataLabelsOfChart executed successfully.");
```

Ha látja ezt az üzenetet, lépjen a kimeneti könyvtárba az új Excel-fájl ellenőrzéséhez. Nyissa ki, és engedje szabadjára kreativitását az új formájú adatcímkékkel!

## Következtetés

És itt van – egy egyszerű útmutató az Excel diagramok adatcímkéinek javításához az Aspose.Cells for .NET használatával! Az alaktípusok testreszabása nemcsak látványosabbá teszi a diagramokat, hanem az adattörténet hatékonyabb közvetítését is segíti. Ne feledje, az adatvizualizáció a tisztaságról és az elkötelezettségről szól. Tehát ne habozzon eljátszani a különböző formákkal és stílusokkal – elvégre adatai megérdemlik a legjobb megjelenítést.

## GYIK

### Mi az Aspose.Cells?  
Az Aspose.Cells egy hatékony .NET-könyvtár, amely lehetővé teszi a fejlesztők számára az Excel-fájlok programozott kezelését.

### Módosíthatom az Excel diagramok különböző aspektusait az Aspose segítségével?  
Teljesen! Az Aspose.Cells kiterjedt funkciókat kínál a diagramok módosításához, beleértve az adatsorokat, címkéket, stílusokat és egyebeket.

### Milyen programozási nyelveket használhatok az Aspose.Cells-ben?  
Míg ez a cikk a .NET-re összpontosít, az Aspose.Cells a Java, a PHP, a Python és más funkciókat is támogatja a REST API-kon keresztül.

### Fizetnem kell az Aspose.Cellsért?  
Az Aspose.Cells kereskedelmi termék, de ingyenes próbaverziót kínál, amelyet megtalálhat[itt](https://releases.aspose.com/).

### Hol kaphatok segítséget, ha problémáim vannak az Aspose.Cells-szel?  
 Ha bármilyen problémával találkozik, ők[támogatási fórum](https://forum.aspose.com/c/cells/9) kiváló forrás a szakértők segítségére.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
