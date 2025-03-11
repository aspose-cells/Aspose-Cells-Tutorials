---
title: Kördiagram módosítása
linktitle: Kördiagram módosítása
second_title: Aspose.Cells .NET Excel Processing API
description: Felszabadítja az Aspose.Cells for .NET erejét, amellyel könnyedén módosíthatja Excel kördiagramjait. Kövesse ezt az oktatóanyagot a lépésről lépésre történő útmutatásért.
weight: 16
url: /hu/net/manipulating-chart-types/modify-pie-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kördiagram módosítása

## Bevezetés

Elgondolkodott már azon, hogyan tudná feldobni ezeket a kördiagramokat Excel-lapjaiban? A kördiagramok fantasztikus módjai lehetnek az adatok vizualizálásának, így biztosítva a közönség érdeklődését és tájékoztatását. Néha azonban ezek a diagramok nem azt a történetet mondják el, amit szeretnél, ha azonnal elmesélnek. Itt jön képbe az Aspose.Cells for .NET. Ez a nagy teljesítményű könyvtár lehetővé teszi az Excel-fájlok programozott kezelését, biztosítva a kördiagramok legapróbb részletekig történő testreszabásához szükséges eszközöket. Ebben az oktatóanyagban egy kördiagram Aspose.Cells használatával történő módosításával foglalkozunk. Legyen szó az adatcímkék megváltoztatásáról vagy a diagram esztétikájának módosításáról.

## Előfeltételek

Mielőtt belemerülnénk a kördiagramok módosításának aprólékos részleteibe, meg kell felelnie néhány előfeltételnek:

- Alapvető C# ismerete: A C# programozás alapvető ismerete segít a könnyű követésben.
- Aspose.Cells for .NET: telepítenie kell az Aspose.Cells könyvtárat. Akár a teljes verzió mellett dönt, akár az ingyenes próbaverziót választja, győződjön meg arról, hogy az használatra kész.
- Visual Studio vagy bármely C# IDE: Szüksége lesz egy környezetre a C# kód írásához és végrehajtásához.
-  Excel-mintafájl: ehhez az oktatóanyaghoz egy Excel-mintafájl neve`sampleModifyPieChart.xlsx` felhasználásra kerül.

 Letöltheti az Aspose.Cells könyvtárat[itt](https://releases.aspose.com/cells/net/).

## Csomagok importálása

Utunk első lépése a szükséges csomagok importálása a C# projektünkbe. Ezt a következőképpen teheti meg:

## Állítsa be projektjét

A kezdéshez nyissa meg a C# IDE-t (a Visual Studio erősen ajánlott), és hozzon létre egy új projektet:

1. Nyissa meg a Visual Studio-t.
2. Válassza az "Új projekt létrehozása" lehetőséget.
3. Válasszon egy C# konzolalkalmazást.
4.  Nevezze el projektjét (pl.`ModifyPieChartDemo`).
5. Kattintson a Létrehozás gombra.

## Telepítse az Aspose.Cells programot

Ha a projekt elkészült, ideje hozzáadni az Aspose.Cells könyvtárat. A NuGet segítségével telepítheti:

1. A „Megoldásböngészőben” kattintson a jobb gombbal a projektre.
2. Válassza a NuGet-csomagok kezelése lehetőséget.
3. Lépjen a Tallózás lapra.
4. Aspose.Cells keresése.
5. Kattintson a Telepítés gombra, és fogadjon el minden licencszerződést.

Most, hogy a könyvtár telepítve van, importáljuk a szükséges névtereket a kódba.

## Névterek importálása

 A te tetején`Program.cs` fájlt, importálja a következő névtereket:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

Ezzel készen állunk, hogy továbblépjünk a tényleges kódra!

## 1. lépés: Határozza meg a bemeneti és kimeneti könyvtárakat

Kezdjük a bemeneti és kimeneti fájlok könyvtárainak meghatározásával. Itt adhatja meg, hogy az Excel-fájl hol található, és hova szeretné menteni a módosított fájlt.

 A tiédben`Main` módszerrel írja be a következő kódot:

```csharp
// Kimeneti könyvtár
string outputDir = "Your Output Directory Path";

// Forrás könyvtár
string sourceDir = "Your Document Directory Path";
```

 Mindenképpen cserélje ki`Your Output Directory Path` és`Your Document Directory Path` a rendszer tényleges elérési útjaival.

## 2. lépés: Nyissa meg a Meglévő munkafüzetet

 Ezután meg kell nyitnunk a módosítani kívánt kördiagramot tartalmazó Excel fájlt. Ehhez használja a`Workbook` osztály:

```csharp
// Nyissa meg a meglévő fájlt.
Workbook workbook = new Workbook(sourceDir + "sampleModifyPieChart.xlsx");
```

 Ebben a részletben egy újat hozunk létre`Workbook` objektumot, és betöltjük az Excel fájlunkat.

## 3. lépés: Nyissa meg a munkalapot

Most merüljünk bele az adott lapba, amely a kördiagramot tartalmazza. Feltételezzük, hogy a kördiagram a második munkalapon található (1. index):

```csharp
// Szerezze be a tervezői diagramot a második lapon.
Worksheet sheet = workbook.Worksheets[1];
```

 A hozzáféréssel a`Worksheets` gyűjtemény, eljuthatunk a szükséges laphoz.

## 4. lépés: Szerezze meg a diagramot

Most készen állunk, hogy hozzáférjünk a diagramhoz. Feltéve, hogy csak egy diagram van a munkalapon, azt közvetlenül lekérhetjük:

```csharp
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

Itt megragadjuk az első diagramot a megadott munkalapról.

## 5. lépés: Az adatcímkék elérése

Most jön az izgalmas rész – a kördiagram adatcímkéinek módosítása. Lépjünk hozzá az adatsorok adatcímkéihez:

```csharp
// Szerezze be az adatcímkéket a harmadik adatpont adatsoraiban.
Aspose.Cells.Charts.DataLabels datalabels = chart.NSeries[0].Points[2].DataLabels;
```

Ezzel a sorral az adatcímkéket kifejezetten adatsorunk harmadik pontjára célozzuk meg. 

## 6. lépés: Módosítsa a címke szövegét

Következő, itt az ideje, hogy módosítsa a címkén található tartalmat. Példánkban frissíteni fogjuk az "Egyesült Királyság, 400 000"-ra:

```csharp
// Módosítsa a címke szövegét.
datalabels.Text = "United Kingdom, 400K";
```

Éppen ezért frissítettük a címkét! 

## 7. lépés: Mentse el a munkafüzetet

Most, hogy elvégeztük a módosításokat, mentsük el a módosított munkafüzetet. 

```csharp
// Mentse el az excel fájlt.
workbook.Save(outputDir + "outputModifyPieChart.xlsx");
```

Ez a sor a munkafüzetet a megadott kimeneti könyvtárba menti. 

## 8. lépés: Erősítse meg a végrehajtást

Végül adjunk ki egy megerősítő üzenetet, hogy minden zökkenőmentesen menjen:

```csharp
Console.WriteLine("ModifyPieChart executed successfully.");
```

Ez egy kis megnyugvást ad arra vonatkozóan, hogy a változtatások a várt módon történtek.

# Következtetés

Megvan! Néhány egyszerű lépéssel sikeresen módosított egy kördiagramot az Aspose.Cells for .NET használatával. Ez a hatékony könyvtár nemcsak megkönnyíti az Excel-fájlok kezelését, hanem lehetővé teszi az adatvizualizációk személyre szabását is a maximális hatás érdekében. Ha munkája során az adatok bemutatásával foglalkozik, az Aspose.Cells használatának elsajátításába fektetett időt biztosan megtérül. Tehát folytassa, játsszon ezekkel a diagramokkal, és nézze meg, hogyan keltheti életre adatait!

# GYIK

### Mi az Aspose.Cells a .NET számára?  
Az Aspose.Cells for .NET egy hatékony könyvtár, amely Excel-fájlok létrehozására, kezelésére és konvertálására szolgál programozottan, Microsoft Excel nélkül.

### Módosíthatok-e a kördiagramokon kívül más diagramokat is?  
Teljesen! Az Aspose.Cells különféle diagramtípusokat támogat, beleértve a sáv-, vonal- és területdiagramokat, lehetővé téve az adatok rugalmas megjelenítését.

### Létezik az Aspose.Cells ingyenes verziója?  
Igen! Az Aspose ingyenes próbaverziót kínál, amely lehetővé teszi a könyvtár tesztelését a vásárlás előtt.

### Hol találok támogatást az Aspose.Cells számára?  
Támogatást találhat az Aspose fórumain, ahol a közösség tagjai és az Aspose munkatársai segíthetnek Önnek.

### Az Aspose.Cells használatához telepítenem kell a Microsoft Excelt?  
Nem, az Aspose.Cells a Microsoft Exceltől függetlenül működik. Nem kell telepítenie a rendszerére.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
