---
"description": "Tanuld meg, hogyan készíthetsz kördiagramot Excelben az Aspose.Cells for .NET használatával ezzel a lépésről lépésre szóló útmutatóval. Vizualizáld az adataid könnyedén."
"linktitle": "Kördiagram létrehozása"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Kördiagram létrehozása"
"url": "/hu/net/manipulating-chart-types/create-pie-chart/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Kördiagram létrehozása

## Bevezetés

A diagramok létrehozása elengedhetetlen az adatok vizuális ábrázolásához, és a kördiagramok az egyik legnépszerűbb módja annak, hogy bemutassuk, hogyan alkotnak az alkatrészek egy egészet. Az Aspose.Cells for .NET segítségével könnyedén automatizálhatod a kördiagramok generálását Excel fájlokban. Ebben az oktatóanyagban elmerülünk abban, hogyan hozhatsz létre kördiagramot a semmiből az Aspose.Cells for .NET segítségével, lépésről lépésre bemutatva, hogyan lehet a folyamatot zökkenőmentessé és egyszerűvé tenni. Akár most ismerkedsz az eszközzel, akár szeretnéd fejleszteni az Excel automatizálási készségeidet, ez az útmutató mindent segít!

## Előfeltételek

Mielőtt belemerülnénk a kódba, győződjünk meg arról, hogy a következőket beállítottuk:

1. Aspose.Cells .NET könyvtárhoz: Győződjön meg róla, hogy az Aspose.Cells telepítve van a projektjében. Ha még nem telepítette, letöltheti innen: [itt](https://releases.aspose.com/cells/net/).
2. .NET fejlesztői környezet: Győződjön meg arról, hogy a projektje a .NET Framework vagy a .NET Core használatára van beállítva.
3. C# alapismeretek: Jártasnak kell lenned a C# programozásban, különösen az objektumorientált programozásban (OOP).

Haladó felhasználók ideiglenes licencet igényelhetnek az Aspose.Cells összes funkciójának feloldásához. Igényelhet egyet a következő címen: [itt](https://purchase.aspose.com/temporary-license/).

## Csomagok importálása

Kezdésként importáld a szükséges névtereket és csomagokat, amelyekre ebben az oktatóanyagban szükség van. Ezek közé tartoznak az alapvető I/O műveletek és az Aspose.Cells csomag.

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## 1. lépés: Új munkafüzet létrehozása

Először is létre kell hoznunk egy példányt a `Workbook` osztály, amely az Excel-fájlt jelöli. Egy munkafüzet több munkalapot tartalmaz, és a példánkban két munkalappal fogunk dolgozni – egy az adatoknak és egy a kördiagramnak.

```csharp
Workbook workbook = new Workbook();
```

Ez inicializál egy új Excel-munkafüzetet. De hová kerülnek az adatok? Ezzel foglalkozzunk a következő lépésben.

## 2. lépés: Adatok hozzáadása a munkalaphoz

Miután létrehoztuk a munkafüzetet, el kell érnünk az első munkalapot, és nevet kell adnunk neki. Ide fogjuk beírni a kördiagramhoz szükséges adatokat.

```csharp
Worksheet sheet = workbook.Worksheets[0];
sheet.Name = "Data";
Cells cells = sheet.Cells;
```

Most beírhatunk néhány, különböző régiókat reprezentáló fiktív értékesítési adatot:

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

Itt két oszlopot adunk hozzá: egyet a régióknak, egy másikat pedig az értékesítési adatoknak. Ezeket az adatokat a kördiagram fogja ábrázolni.

## 3. lépés: Diagramlap hozzáadása

Ezután adjunk hozzá egy külön munkalapot a kördiagramhoz.

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

Ez az új munkalap fogja tárolni a kördiagramot. Ha nevet ad neki, például „Diagram”, akkor a felhasználók tudni fogják, mire számíthatnak a fájl megnyitásakor.

## 4. lépés: A kördiagram létrehozása

Most itt az ideje elkészíteni magát a diagramot. Megadjuk, hogy kördiagramot szeretnénk, és meghatározzuk a helyét a munkalapon.

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

A módszer `Add()` elfogadja a diagramtípus paramétereit (ebben az esetben `ChartType.Pie`), és a munkalapon elfoglalt helyét. A számok a sor- és oszloppozíciókat jelölik.

## 5. lépés: A diagram megjelenésének testreszabása

Egy kördiagram nem lenne teljes némi testreszabás nélkül! Tegyük vizuálisan vonzóbbá a diagramunkat a színek, a feliratok és a cím finomhangolásával.

### Diagram címének beállítása
```csharp
chart.Title.Text = "Sales By Region";
chart.Title.Font.Color = Color.Blue;
chart.Title.Font.IsBold = true;
chart.Title.Font.Size = 12;
```

### Telekterület testreszabása
```csharp
chart.PlotArea.Area.ForegroundColor = Color.Coral;
chart.PlotArea.Area.FillFormat.SetTwoColorGradient(Color.Yellow, Color.White, GradientStyleType.Vertical, 2);
chart.PlotArea.Border.IsVisible = false;
```

Beállítottuk a színátmenetes kitöltést a nyomtatási területre, és elrejtettük a szegélyt a tisztább megjelenés érdekében.

## 6. lépés: Diagramadatok definiálása

Ideje összekapcsolni a diagramot az adatainkkal. A `NSeries` A diagram tulajdonsága az értékesítési adatokat és a régiókat a kördiagramhoz köti.

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

Az első sor azt határozza meg, hogy a cellákból származó értékesítési adatokat használjuk. `B2:B8`Azt is utasítjuk a diagramnak, hogy a régióneveket használja a következőből: `A2:A8` kategóriacímkékként.

## 7. lépés: Adatcímkék hozzáadása

diagram szegmenseihez közvetlenül hozzáadott címkék megkönnyíthetik a megértést. A kördiagram szeleteiben szerepeljenek a régiók nevei és az értékesítési értékek.

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

Végül adjunk néhány utolsó simítást a diagramterületnek és a feliratoknak. Ez javítja a diagram összképét.

### Diagramterület
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

## 9. lépés: A munkafüzet mentése

Végül a munkafüzetet egy Excel-fájlba mentjük. Szükség szerint megadhatja a kimeneti könyvtárat és a fájlnevet.

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## Következtetés

A kördiagram létrehozása az Aspose.Cells for .NET segítségével egy egyszerű és testreszabható folyamat. Ezt az útmutatót követve professzionális megjelenésű diagramot készíthet, amely mindössze néhány lépésben értékes információkat közvetít. Akár üzleti jelentéskészítésről, akár oktatási célokról van szó, a diagramkészítés elsajátítása fejleszti Excel automatizálási készségeit. Ne feledje, az Aspose.Cells biztosítja azt a rugalmasságot, amelyre szüksége van ahhoz, hogy lenyűgöző, adatvezérelt Excel fájlokat hozzon létre könnyedén.

## GYIK

### Létrehozhatok más típusú diagramokat az Aspose.Cells for .NET használatával?
Igen! Az Aspose.Cells különféle diagramtípusokat támogat, beleértve az oszlopdiagramokat, vonaldiagramokat és szóródási diagramokat.

### Szükségem van fizetős licencre az Aspose.Cells for .NET használatához?
Az ingyenes verziót bizonyos korlátozásokkal használhatod. A teljes funkciók használatához licencre lesz szükséged, amelyet megvásárolhatsz. [itt](https://purchase.aspose.com/buy).

### Exportálhatom a diagramot PDF vagy kép formátumba?
Abszolút! Az Aspose.Cells lehetővé teszi diagramok exportálását különféle formátumokba, beleértve a PDF-et és a PNG-t is.

### Lehetséges minden piteszeletet különböző színekkel díszíteni?
Igen, minden szeletre különböző színeket alkalmazhat a beállítással. `IsColorVaried` ingatlan `true`, ahogy az az oktatóanyagban is látható.

### Automatizálhatom több diagram létrehozását egyetlen munkafüzetben?
Igen, egyetlen Excel-fájlon belül annyi diagramot hozhat létre és testreszabhat, amennyire szüksége van.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}