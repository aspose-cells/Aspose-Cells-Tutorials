---
"description": "Tanuld meg, hogyan hozhatsz létre adatjelölőkkel ellátott vonaldiagramot Excelben az Aspose.Cells for .NET használatával. Kövesd ezt a lépésről lépésre szóló útmutatót a diagramok egyszerű létrehozásához és testreszabásához."
"linktitle": "Vonaldiagram létrehozása adatjelölővel"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Vonaldiagram létrehozása adatjelölővel"
"url": "/hu/net/working-with-chart-data/create-line-with-data-marker-chart/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vonaldiagram létrehozása adatjelölővel

## Bevezetés

Elgondolkodtál már azon, hogyan hozhatsz létre lenyűgöző diagramokat Excelben programozottan? Nos, akkor kapd fel a csatodat, mert ma belevágunk egy vonaldiagram létrehozásába adatjelölőkkel az Aspose.Cells for .NET használatával. Ez az oktatóanyag végigvezet téged minden lépésen, biztosítva, hogy szilárdan elsajátítsd a diagramgenerálást, még akkor is, ha most ismerkedsz az Aspose.Cells-szel.

## Előfeltételek

Mielőtt elkezdenénk, győződjünk meg róla, hogy minden a helyén van a zökkenőmentes követéshez.

1. Aspose.Cells for .NET Library – Telepítened kell ezt. Letöltheted. [itt](https://releases.aspose.com/cells/net/).
2. .NET-keretrendszer – Győződjön meg arról, hogy fejlesztői környezete a .NET legújabb verziójával van beállítva.
3. IDE (Integrált fejlesztői környezet) – Visual Studio ajánlott.
4. Érvényes Aspose.Cells licenc – Ha nincs ilyen, igényelhet egyet [ideiglenes engedély](https://purchase.aspose.com/temporary-license/) vagy nézd meg az övékét [ingyenes próba](https://releases.aspose.com/).

Készen állsz? Nézzük részletesen!

## Szükséges csomagok importálása

Kezdésként importáld a következő névtereket a projektedbe. Ezek biztosítják majd a diagram létrehozásához szükséges osztályokat és metódusokat.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

Ha ezzel megvagyunk, elkezdhetjük a kódolást!

## 1. lépés: A munkafüzet és a munkalap beállítása

Először is létre kell hoznia egy új munkafüzetet, és el kell érnie az első munkalapot.

```csharp
//Kimeneti könyvtár
static string outputDir = "Your Document Directory";
		
// Munkafüzet példányosítása
Workbook workbook = new Workbook();

// Első munkalap elérése
Worksheet worksheet = workbook.Worksheets[0];
```

Gondolj a munkafüzetre úgy, mint egy Excel-fájlra, a munkalapra pedig úgy, mint egy adott munkalapra benne. Ebben az esetben az első munkalappal dolgozunk.

## 2. lépés: A munkalap feltöltése adatokkal

Most, hogy megvan a munkalapunk, töltsük fel néhány adattal. Két értéksorozathoz hozunk létre véletlenszerű adatpontokat.

```csharp
// Oszlopcím beállítása
worksheet.Cells[0, 0].Value = "X";
worksheet.Cells[0, 1].Value = "Y";

// Véletlenszerű adatok a diagram létrehozásához
Random R = new Random();

// Véletlenszerű adatok létrehozása és mentése a cellákba
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

Itt véletlenszerű számokat használunk az adatok szimulálására, de a valós alkalmazásokban feltölthetjük az adathalmazunkból származó tényleges értékekkel.

## 3. lépés: A diagram hozzáadása a munkalaphoz

Ezután hozzáadjuk a diagramot a munkalaphoz, és kiválasztjuk a típust – ebben az esetben egy adatjelölőkkel ellátott vonaldiagramot.

```csharp
// Diagram hozzáadása a munkalaphoz
int idx = worksheet.Charts.Add(ChartType.LineWithDataMarkers, 1, 3, 20, 20);

// Hozzáférés az újonnan létrehozott diagramhoz
Chart chart = worksheet.Charts[idx];
```

Ez a kódrészlet egy adatjelölőkkel ellátott vonaldiagramot ad a munkalaphoz, egy adott tartományba helyezve azt (1,3-tól 20,20-ig). Elég egyszerű, ugye?

## 4. lépés: A diagram megjelenésének testreszabása

Miután a diagram elkészült, ízlés szerint formázhatja. Változtassuk meg a hátteret, a címet és a diagram stílusát.

```csharp
// Diagramstílus beállítása
chart.Style = 3;

// Az automatikus skálázás értékének igazra állítása
chart.AutoScaling = true;

// Előtérszín beállítása fehérre
chart.PlotArea.Area.ForegroundColor = Color.White;

// Diagram címtulajdonságainak beállítása
chart.Title.Text = "Sample Chart";

// Diagramtípus beállítása
chart.Type = ChartType.LineWithDataMarkers;
```

Itt letisztult megjelenést kölcsönözünk a diagramnak egy fehér háttér beállításával, automatikus skálázással és egy értelmes címmel.

## 5. lépés: Sorozatok definiálása és adatpontok ábrázolása

Most, hogy a diagramunk jól néz ki, meg kell határoznunk az ábrázolandó adatsorokat.

```csharp
// Kategóriatengely címének tulajdonságainak beállítása
chart.CategoryAxis.Title.Text = "Units";

// Két sorozat definiálása a diagramhoz
int s2_idx = chart.NSeries.Add("A2: A21", true);
int s3_idx = chart.NSeries.Add("A22: A41", true);
```

Ezek a sorozatok megfelelnek a korábban feltöltött adatpontok tartományainak.

## 6. lépés: Színek hozzáadása és sorozatjelölők testreszabása

Tegyük még vonzóbbá ezt a diagramot azáltal, hogy egyéni színeket adunk az adatjelölőinkhez.

```csharp
// Első sorozat testreszabása
chart.NSeries[s2_idx].Marker.Area.ForegroundColor = Color.Yellow;
chart.NSeries[s2_idx].Marker.Border.IsVisible = false;

// Második sorozat testreszabása
chart.NSeries[s3_idx].Marker.Area.ForegroundColor = Color.Green;
chart.NSeries[s3_idx].Marker.Border.IsVisible = false;
```

A színek testreszabásával a diagramot nemcsak funkcionálissá, hanem vizuálisan is vonzóvá teheted!

## 7. lépés: X és Y értékek beállítása minden sorozathoz

Végül rendeljük hozzá az X és Y értékeket az egyes sorozatainkhoz.

```csharp
// Az első sorozat X és Y értékeinek beállítása
chart.NSeries[s2_idx].XValues = "A2: A21";
chart.NSeries[s2_idx].Values = "B2: B21";

// A második sorozat X és Y értékeinek beállítása
chart.NSeries[s3_idx].XValues = "A22: A41";
chart.NSeries[s3_idx].Values = "B22: B41";
```

Az értékek a 2. lépésben feltöltött adatokon alapulnak.

## 8. lépés: A munkafüzet mentése

Most, hogy minden beállított, mentsük el a munkafüzetet, hogy működés közben is láthassuk a diagramot.

```csharp
// A munkafüzet mentése
workbook.Save(outputDir + @"LineWithDataMarkerChart.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```

És ennyi! Most készítettél egy vonaldiagramot adatjelölőkkel az Aspose.Cells for .NET használatával.

## Következtetés

Diagramok programozott létrehozása Excelben ijesztőnek tűnhet, de az Aspose.Cells for .NET segítségével ez olyan egyszerű, mint egy lépésről lépésre haladó recept követése. A munkafüzet beállításától a diagram megjelenésének testreszabásáig ez a hatékony könyvtár mindent kezel. Akár jelentéseket, irányítópultokat vagy adatvizualizációkat készít, az Aspose.Cells segítségével mindezt könnyedén megteheti.

## GYIK

### Testreszabhatom a diagramot tovább?  
Abszolút! Az Aspose.Cells rengeteg testreszabási lehetőséget kínál, a betűtípusoktól a rácsvonalakig és egyebekig.

### Szükségem van licencre az Aspose.Cells használatához?  
Igen, a teljes funkcionalitáshoz licenc szükséges. Szerezhet egyet. [ideiglenes engedély](https://purchase.aspose.com/temporary-license/) vagy kezdj egy [ingyenes próba](https://releases.aspose.com/).

### Hogyan adhatok hozzá több adatsort?  
Csak adjon hozzá további sorozatokat a `NSeries.Add` metódus, amely megadja az új adatok cellatartományait.

### Exportálhatom a diagramot képként?  
Igen, a diagramokat közvetlenül képként exportálhatja a `Chart.ToImage` módszer.

### Az Aspose.Cells támogatja a 3D-s diagramokat?  
Igen, az Aspose.Cells a diagramtípusok széles skáláját támogatja, beleértve a 3D-s diagramokat is.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}