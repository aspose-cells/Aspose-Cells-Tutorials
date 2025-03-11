---
title: Vonal létrehozása adatjelölő diagrammal
linktitle: Vonal létrehozása adatjelölő diagrammal
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan hozhat létre adatjelölőkkel ellátott vonaldiagramot Excelben az Aspose.Cells for .NET használatával. Kövesse ezt a lépésenkénti útmutatót a diagramok egyszerű létrehozásához és testreszabásához.
weight: 10
url: /hu/net/working-with-chart-data/create-line-with-data-marker-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vonal létrehozása adatjelölő diagrammal

## Bevezetés

Gondolkozott már azon, hogyan hozhat létre lenyűgöző diagramokat az Excelben programozottan? Nos, kösd be, mert ma belemerülünk egy vonal adatjelölő diagram létrehozásába az Aspose.Cells for .NET használatával. Ez az oktatóanyag végigvezeti Önt az egyes lépéseken, biztosítva, hogy határozottan megértse a diagramkészítést, még akkor is, ha még csak most kezdi használni az Aspose.Cells-t.

## Előfeltételek

Mielőtt elkezdené, győződjön meg arról, hogy minden a helyén van, hogy zökkenőmentesen kövesse az utat.

1. Aspose.Cells for .NET Library – Ezt telepítenie kell. Megfoghatod[itt](https://releases.aspose.com/cells/net/).
2. .NET-keretrendszer – Győződjön meg arról, hogy a fejlesztői környezet a .NET legújabb verziójával van beállítva.
3. IDE (Integrated Development Environment) – a Visual Studio ajánlott.
4.  Érvényes Aspose.Cells licenc – Ha nem rendelkezik ilyennel, kérhet a[ideiglenes engedély](https://purchase.aspose.com/temporary-license/) vagy nézze meg őket[ingyenes próbaverzió](https://releases.aspose.com/).

Készen állsz? Bontsuk szét!

## A szükséges csomagok importálása

A kezdéshez feltétlenül importálja a következő névtereket a projektbe. Ezek biztosítják a diagram létrehozásához szükséges osztályokat és módszereket.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

Ha ezt megtudtad, elkezdhetjük a kódolást!

## 1. lépés: Állítsa be a munkafüzetet és a munkalapot

Először is létre kell hoznia egy új munkafüzetet, és hozzá kell férnie az első munkalaphoz.

```csharp
//Kimeneti könyvtár
static string outputDir = "Your Document Directory";
		
// Munkafüzet példányosítása
Workbook workbook = new Workbook();

// Az első munkalap elérése
Worksheet worksheet = workbook.Worksheets[0];
```

Tekintse a munkafüzetet az Excel-fájlnak, a munkalapot pedig a benne lévő konkrét lapnak. Ebben az esetben az első lappal dolgozunk.

## 2. lépés: Töltse fel a munkalapot adatokkal

Most, hogy megvan a munkalapunk, töltsük fel néhány adattal. Véletlenszerű adatpontokat hozunk létre két értéksorozathoz.

```csharp
// Állítsa be az oszlopok címét
worksheet.Cells[0, 0].Value = "X";
worksheet.Cells[0, 1].Value = "Y";

// Véletlenszerű adatok a diagram létrehozásához
Random R = new Random();

// Hozzon létre véletlenszerű adatokat, és mentse a cellákba
for (int i = 1; i < 21; i++)
{
    worksheet.Cells[i, 0].Value = i;
    worksheet.Cells[i, 1].Value = 0.8;
}

for (int i = 21; i < 41; i++)
{
    worksheet.Cells[i, 0].Value = i - 20;
    worksheet.Cells[i, 1].Value = 0.9;
}
```

Itt véletlen számokat használunk az adatok szimulálására, de a valós alkalmazásokban feltöltheti azokat az adatkészletből származó tényleges értékekkel.

## 3. lépés: Adja hozzá a diagramot a munkalaphoz

Ezután hozzáadjuk a diagramot a munkalaphoz, és kiválasztjuk a típust – ebben az esetben egy vonal adatjelölőkkel diagramot.

```csharp
// Adjon hozzá egy diagramot a munkalaphoz
int idx = worksheet.Charts.Add(ChartType.LineWithDataMarkers, 1, 3, 20, 20);

// Nyissa meg az újonnan létrehozott diagramot
Chart chart = worksheet.Charts[idx];
```

Ez a részlet egy adatjelölőkkel ellátott vonaldiagramot ad a munkalaphoz, és egy adott tartományba (1,3–20,20) helyezi el. Elég egyszerű, igaz?

## 4. lépés: A diagram megjelenésének testreszabása

A diagram elkészítése után ízlése szerint alakíthatja. Változtassuk meg a hátteret, a címet és a diagram stílusát.

```csharp
// Állítsa be a diagram stílusát
chart.Style = 3;

// Állítsa az automatikus skálázás értékét igazra
chart.AutoScaling = true;

// Állítsa az előtér színét fehérre
chart.PlotArea.Area.ForegroundColor = Color.White;

//Állítsa be a diagram címének tulajdonságait
chart.Title.Text = "Sample Chart";

// Állítsa be a diagram típusát
chart.Type = ChartType.LineWithDataMarkers;
```

Itt fehér hátteret állítunk be, automatikus skálázást és értelmes címet adunk a diagramnak.

## 5. lépés: Sorozatok és adatpontok ábrázolása

Most, hogy a diagramunk jól néz ki, meg kell határoznunk az ábrázolandó adatsorokat.

```csharp
// Állítsa be a kategóriatengely címének tulajdonságait
chart.CategoryAxis.Title.Text = "Units";

// Határozzon meg két sorozatot a diagramhoz
int s2_idx = chart.NSeries.Add("A2: A21", true);
int s3_idx = chart.NSeries.Add("A22: A41", true);
```

Ezek a sorozatok az általunk korábban feltöltött adatpont-tartományoknak felelnek meg.

## 6. lépés: Színek hozzáadása és sorozatjelzők testreszabása

Tegyük még vonzóbbá ezt a diagramot azáltal, hogy egyedi színeket adunk adatjelölőinkhez.

```csharp
// Az első sorozat testreszabása
chart.NSeries[s2_idx].Marker.Area.ForegroundColor = Color.Yellow;
chart.NSeries[s2_idx].Marker.Border.IsVisible = false;

// A második sorozat testreszabása
chart.NSeries[s3_idx].Marker.Area.ForegroundColor = Color.Green;
chart.NSeries[s3_idx].Marker.Border.IsVisible = false;
```

A színek testreszabásával a diagramot nemcsak funkcionálissá, hanem vizuálisan is vonzóvá varázsolja!

## 7. lépés: Állítsa be az X és Y értékeket minden sorozathoz

Végül rendeljük hozzá az X és Y értékeket minden sorozatunkhoz.

```csharp
// Állítsa be az első sorozat X és Y értékét
chart.NSeries[s2_idx].XValues = "A2: A21";
chart.NSeries[s2_idx].Values = "B2: B21";

// Állítsa be a második sorozat X és Y értékét
chart.NSeries[s3_idx].XValues = "A22: A41";
chart.NSeries[s3_idx].Values = "B22: B41";
```

Az értékek a 2. lépésben feltöltött adatokon alapulnak.

## 8. lépés: Mentse el a munkafüzetet

Most, hogy minden be van állítva, mentsük el a munkafüzetet, hogy működés közben lássuk a diagramot.

```csharp
// Mentse el a munkafüzetet
workbook.Save(outputDir + @"LineWithDataMarkerChart.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```

És ennyi! Most hozott létre egy vonaldiagramot adatjelölőkkel az Aspose.Cells for .NET használatával.

## Következtetés

A diagramok programozott létrehozása az Excelben ijesztőnek tűnhet, de az Aspose.Cells for .NET segítségével ez olyan egyszerű, mint egy lépésről lépésre leírt receptek követése. A munkafüzet beállításától a diagram megjelenésének testreszabásáig ez a hatékony könyvtár mindent kezel. Függetlenül attól, hogy jelentéseket, irányítópultokat vagy adatvizualizációkat készít, az Aspose.Cells segítségével gyorsan megteheti.

## GYIK

### Testreszabhatom a diagramot tovább?  
Teljesen! Az Aspose.Cells rengeteg testreszabási lehetőséget kínál, a betűtípusoktól a rácsvonalakig és egyebekig.

### Szükségem van engedélyre az Aspose.Cells használatához?  
 Igen, a teljes funkcionalitáshoz licenc szükséges. Kaphatsz a[ideiglenes engedély](https://purchase.aspose.com/temporary-license/) vagy kezdje a-val[ingyenes próbaverzió](https://releases.aspose.com/).

### Hogyan adhatok hozzá további adatsorokat?  
 Csak adjon hozzá további sorozatokat a`NSeries.Add` módszerrel, megadva az új adatok cellatartományát.

### Exportálhatom a diagramot képként?  
 Igen, a diagramokat közvetlenül képként exportálhatja a`Chart.ToImage` módszer.

### Az Aspose.Cells támogatja a 3D diagramokat?  
Igen, az Aspose.Cells a diagramtípusok széles skáláját támogatja, beleértve a 3D diagramokat is.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
