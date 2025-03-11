---
title: Kördiagram létrehozása
linktitle: Kördiagram létrehozása
second_title: Aspose.Cells .NET Excel Processing API
description: Ebből a lépésenkénti útmutatóból megtudhatja, hogyan hozhat létre kördiagramot Excelben az Aspose.Cells for .NET használatával. Vizualizálja adatait erőfeszítés nélkül.
weight: 12
url: /hu/net/manipulating-chart-types/create-pie-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kördiagram létrehozása

## Bevezetés

A diagramok létrehozása elengedhetetlen az adatok vizuális megjelenítéséhez, és a kördiagramok az egyik legnépszerűbb módja annak, hogy szemléltesse, hogyan alkotják az alkatrészek egy egészet. Az Aspose.Cells for .NET segítségével könnyedén automatizálhatja a kördiagramok létrehozását Excel-fájlokban. Ebben az oktatóanyagban belemerülünk abba, hogyan lehet a semmiből kördiagramot létrehozni az Aspose.Cells for .NET használatával, lépésenkénti útmutatóval, hogy a folyamat zökkenőmentes és egyszerű legyen. Akár még új az eszközben, akár fejleszteni szeretné Excel automatizálási készségeit, ez az útmutató mindenre kiterjed!

## Előfeltételek

Mielőtt belemerülne a kódba, győződjön meg arról, hogy beállította a következőket:

1.  Aspose.Cells for .NET Library: Győződjön meg arról, hogy az Aspose.Cells telepítve van a projektben. Ha még nem telepítette, letöltheti innen[itt](https://releases.aspose.com/cells/net/).
2. .NET fejlesztői környezet: Győződjön meg arról, hogy projektje .NET-keretrendszer vagy .NET Core használatára van beállítva.
3. Alapvető C# ismerete: Kényelmesnek kell lennie a C# programozásban, különösen az objektum-orientált programozásban (OOP).

 Haladó felhasználók számára ideiglenes licenc alkalmazható az Aspose.Cells összes funkciójának feloldásához. Kérhetsz egyet innen[itt](https://purchase.aspose.com/temporary-license/).

## Csomagok importálása

A kezdéshez importálja az oktatóanyaghoz szükséges névtereket és csomagokat. Ide tartoznak az alapvető I/O műveletek és az Aspose.Cells csomag.

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## 1. lépés: Hozzon létre egy új munkafüzetet

 Először is létre kell hoznunk egy példányt a`Workbook` osztály, amely az Excel fájlt képviseli. Egy munkafüzet több lapot tartalmaz, és példánkban két lappal fogunk dolgozni – egy az adatokhoz és egy a kördiagramhoz.

```csharp
Workbook workbook = new Workbook();
```

Ezzel inicializálja az új Excel-munkafüzetet. De hova kerülnek az adatok? Gondoskodjunk erről a következő lépésben.

## 2. lépés: Adatok hozzáadása a munkalaphoz

A munkafüzet létrehozása után el kell érnünk az első munkalapot, és nevet kell adnunk neki. Ide írjuk be a kördiagramhoz szükséges adatokat.

```csharp
Worksheet sheet = workbook.Worksheets[0];
sheet.Name = "Data";
Cells cells = sheet.Cells;
```

Most bevihetünk néhány álértékesítési adatot, amelyek különböző régiókat képviselnek:

```csharp
cells["A1"].PutValue("Region");
cells["A2"].PutValue("France");
cells["A3"].PutValue("Germany");
cells["A4"].PutValue("England");
cells["A5"].PutValue("Sweden");
cells["A6"].PutValue("Italy");
cells["A7"].PutValue("Spain");
cells["A8"].PutValue("Portugal");

cells["B1"].PutValue("Sales");
cells["B2"].PutValue(70000);
cells["B3"].PutValue(55000);
cells["B4"].PutValue(30000);
cells["B5"].PutValue(40000);
cells["B6"].PutValue(35000);
cells["B7"].PutValue(32000);
cells["B8"].PutValue(10000);
```

Itt két oszlopot adunk hozzá: egyet a régiókhoz, egy másikat pedig az értékesítési adatokhoz. Ezek az adatok a kördiagramon jelennek meg.

## 3. lépés: Adjon hozzá egy diagramlapot

Ezután adjunk hozzá egy külön munkalapot a kördiagram tárolására.

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

Ezen az új munkalapon lesz a kördiagram. A „Chart” névhez hasonló elnevezés biztosítja, hogy a felhasználók tudják, mire számíthatnak a fájl megnyitásakor.

## 4. lépés: Készítse el a kördiagramot

Most itt az ideje létrehozni a tényleges diagramot. Meghatározzuk, hogy szeretnénk egy kördiagramot, és meghatározzuk a pozícióját a lapon.

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

 A módszer`Add()`elfogadja a diagramtípus paramétereit (ebben az esetben`ChartType.Pie`), és helyét a munkalapon. A számok a sorok és oszlopok pozícióját jelzik.

## 5. lépés: A diagram megjelenésének testreszabása

A kördiagram nem lenne teljes testreszabás nélkül! Tegyük tetszetőssé diagramunkat a színek, a címkék és a cím módosításával.

### Állítsa be a diagram címét
```csharp
chart.Title.Text = "Sales By Region";
chart.Title.Font.Color = Color.Blue;
chart.Title.Font.IsBold = true;
chart.Title.Font.Size = 12;
```

### A telekterület testreszabása
```csharp
chart.PlotArea.Area.ForegroundColor = Color.Coral;
chart.PlotArea.Area.FillFormat.SetTwoColorGradient(Color.Yellow, Color.White, GradientStyleType.Vertical, 2);
chart.PlotArea.Border.IsVisible = false;
```

Beállítjuk a színátmenet kitöltését a telek területén, és elrejtjük a szegélyt a tisztább megjelenés érdekében.

## 6. lépés: A diagramadatok meghatározása

 Ideje összekapcsolni a diagramot adatainkkal. A`NSeries` A diagram tulajdonsága az eladási adatokat és a régiókat a kördiagramhoz köti.

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

 Az első sor azt határozza meg, hogy a cellákból származó értékesítési adatokat használjuk`B2:B8` . Azt is elmondjuk a diagramnak, hogy használja a régióneveket`A2:A8` kategóriacímkékként.

## 7. lépés: Adjon hozzá adatcímkéket

Ha címkéket közvetlenül a diagram szegmenseihez ad hozzá, akkor könnyebben érthető. Tegyük bele a régióneveket és az értékesítési értékeket a kördiagram szeletekbe.

```csharp
for (int i = 0; i < chart.NSeries.Count; i++)
{
    DataLabels labels = chart.NSeries[i].DataLabels;
    labels.ShowCategoryName = true;
    labels.ShowValue = true;
    labels.Position = LabelPositionType.InsideBase;
}
```

## 8. lépés: A diagramterület és a jelmagyarázat testreszabása

Végül végezzünk néhány utolsó simítást a diagramterületen és a legendán. Ez javítja a diagram általános megjelenítését.

### Diagram terület
```csharp
ChartArea chartArea = chart.ChartArea;
chartArea.Area.Formatting = FormattingType.Custom;
chartArea.Area.FillFormat.Texture = TextureType.BlueTissuePaper;
```

### Legenda
```csharp
Legend legend = chart.Legend;
legend.Position = LegendPositionType.Left;
legend.Font.IsBold = true;
legend.Border.Color = Color.Blue;
legend.Area.FillFormat.Texture = TextureType.Bouquet;
```

## 9. lépés: Mentse el a munkafüzetet

Végül elmentjük a munkafüzetet egy Excel fájlba. Szükség szerint megadhatja a kimeneti könyvtárat és a fájlnevet.

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## Következtetés

A kördiagram létrehozása az Aspose.Cells segítségével .NET-hez egyszerű és testreszabható folyamat. Az útmutató követésével professzionális megjelenésű diagramot hozhat létre, amely néhány lépésben értékes betekintést nyújt. Legyen szó üzleti jelentéskészítésről vagy oktatási célról, a diagramkészítés elsajátítása javítja Excel automatizálási készségeit. Ne feledje, az Aspose.Cells biztosítja azt a rugalmasságot, amelyre szüksége van lenyűgöző, adatvezérelt Excel-fájlok könnyű létrehozásához.

## GYIK

### Létrehozhatok más típusú diagramokat az Aspose.Cells for .NET használatával?
Igen! Az Aspose.Cells különféle diagramtípusokat támogat, beleértve az oszlopdiagramokat, a vonaldiagramokat és a szóródiagramokat.

### Szükségem van fizetős licencre az Aspose.Cells for .NET használatához?
Használhatja az ingyenes verziót bizonyos korlátozásokkal. A teljes funkciók használatához licencre lesz szüksége, amelyet megvásárolhat[itt](https://purchase.aspose.com/buy).

### Exportálhatom a diagramot olyan formátumokba, mint például PDF vagy képek?
Teljesen! Az Aspose.Cells lehetővé teszi diagramok exportálását különféle formátumokba, beleértve a PDF és PNG formátumokat.

### Lehetséges minden piteszeletet különböző színekkel díszíteni?
 Igen, az egyes szeletekre különböző színeket alkalmazhat a`IsColorVaried` tulajdonát`true`, ahogy az az oktatóanyagban is látható.

### Automatizálhatom több diagram generálását egyetlen munkafüzetben?
Igen, tetszőleges számú diagramot hozhat létre és testreszabhat egyetlen Excel-fájlban.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
