---
date: '2026-04-08'
description: Tanulja meg, hogyan generáljon oszlopdiagramot Java-ban az Aspose.Cells
  használatával, beleértve a diagram létrehozását Java-ban, a diagramlap hozzáadását
  és a munkafüzet Excel-be exportálását.
keywords:
- generate column chart
- create chart java
- add chart sheet
- populate excel cells
- set chart title
- export workbook excel
title: Oszlopdiagram generálása az Aspose.Cells Java útmutatóval
url: /hu/java/charts-graphs/aspose-cells-java-create-customize-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Oszlopdiagram létrehozása Aspose.Cells Java-val

A mai adat‑központú alkalmazásokban az **oszlopdiagram generálása** gyorsan és programozottan nyers számokat alakíthat át világos vizuális betekintéssé. Legyen szó jelentés‑műszerfalról, elemző eszközről vagy egyszerű export funkcióról, az Aspose.Cells for Java egy folyékony API‑t biztosít a **chart java** projektekhez anélkül, hogy az Excel felületével kellene foglalkozni. Ebben az útmutatóban megtanulja, hogyan állítsa be a könyvtárat, **populate Excel cells**, adjon hozzá egy **chart sheet**‑et, testre szabja a **chart title**‑t, és végül **export workbook excel**‑t fájlba.

## Gyors válaszok
- **Mi jelent a „generate column chart”?** Olyan függőleges sáv típusú vizualizációt hoz létre táblázatos adatokból.  
- **Melyik könyvtár szükséges?** Aspose.Cells for Java (ingyenes próba elérhető).  
- **Szükség van Excel telepítésre?** Nem, a könyvtár független a Microsoft Exceltől.  
- **Exportálhatok más formátumokba, mint az XLS?** Igen – PDF, PNG, SVG stb., a `workbook.save()` segítségével.  
- **Kötelező licenc a termeléshez?** Igen, vásárolt vagy ideiglenes licenc szükséges.

## Mi az a generate column chart?
Az oszlopdiagram az adat sorozatokat függőleges sávokként jeleníti meg, így könnyen összehasonlíthatók az értékek kategóriák, például régiók, hónapok vagy termékcsoportok szerint. Az Aspose.Cells lehetővé teszi, hogy ezt a diagramot teljesen kódból építsd fel, teljes kontrollt biztosítva az adatok, a stílus és a kimeneti formátum felett.

## Miért használjuk az Aspose.Cells-et chart java létrehozásához?
- **Nincs COM interop** – bármely operációs rendszeren működik JVM-mel.  
- **Gazdag stíluslehetőségek** – képek, színátmenetek, jelmagyarázatok és egyedi betűtípusok.  
- **Magas teljesítmény** – nagy adathalmazokhoz alkalmas.  
- **Több export formátum** – XLS, XLSX, PDF, PNG és továbbiak.

## Előkövetelmények
- **Java Development Kit (JDK) 8+** telepítve.  
- Alap Java ismeretek és Excel koncepciók ismerete.  

### Szükséges könyvtárak
Add Aspose.Cells to your project using one of the snippets below.

#### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

#### Gradle
```gradle
implementation group: 'com.aspose', name: 'aspose-cells', version: '25.3'
```

### Licenc beszerzése
Az Aspose ingyenes próbaverziót és ideiglenes licencet kínál alapos teszteléshez.

- **Free Trial**: [Download Free](https://releases.aspose.com/cells/java/)  
- **Temporary License**: [Request Here](https://purchase.aspose.com/temporary-license/)

## Az Aspose.Cells beállítása Java-hoz

Először hozzunk létre egy `Workbook` példányt – ez lesz a vászon az adataink és a diagram számára.

```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook
Workbook workbook = new Workbook();
```

## Lépésről‑lépésre útmutató

### 1. Munkalap létrehozása és elnevezése
A nyers adatokat egy **Data** nevű munkalapon tároljuk.

```java
import com.aspose.cells.Worksheet;

// Create a new Workbook instance
Workbook workbook = new Workbook();
```

```java
// Access the first worksheet and set its name to "Data"
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.setName("Data");
```

### 2. Excel cellák feltöltése
Helyezze be a régióneveket és az értékesítési adatokat, amelyeket az oszlopdiagram megjelenít.

```java
import com.aspose.cells.Cells;

// Get the cells collection from the "Data" sheet
Cells cells = sheet.getCells();
```

```java
// Insert region names and sales figures
cells.get("A1").putValue("Region");
cells.get("B1").putValue("Sale");

String[] regions = {"France", "Germany", "England", "Sweden", "Italy", "Spain", "Portugal"};
int[] sales = {70000, 55000, 30000, 40000, 35000, 32000, 10000};

for (int i = 0; i < regions.length; i++) {
    cells.get("A" + (i+2)).putValue(regions[i]);
    cells.get("B" + (i+2)).putValue(sales[i]);
}
```

### 3. Diagram munkalap hozzáadása
A diagram és a nyers adatok szétválasztása rendezetten tartja a munkafüzetet.

```java
import com.aspose.cells.SheetType;

// Add a new chart sheet
int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
Worksheet chartSheet = workbook.getWorksheets().get(sheetIndex);

// Name the worksheet "Chart"
chartSheet.setName("Chart");
```

### 4. Oszlopdiagram létrehozása
Most ténylegesen **generate column chart** objektumokat hozunk létre.

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartType;

// Add a new column chart to the "Chart" sheet
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 1, 1, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
```

### 5. Kép beállítása háttérkitöltésként a diagram területén
A háttérkép kiemelheti a diagramot.

```java
import java.io.FileInputStream;
import com.aspose.cells.Color;

String dataDir = "YOUR_DATA_DIRECTORY";
File file = new FileInputStream(dataDir + "aspose-logo.png");
byte[] data = new byte[(int)file.length()];
file.read(data);

chart.getPlotArea().getArea().getFillFormat().setImageData(data);
chart.getPlotArea().getBorder().setVisible(false);
```

### 6. Diagram címének beállítása
A **set chart title** testreszabása javítja az olvashatóságot.

```java
// Configure the chart's title properties
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```

### 7. Sorozatadatok és jelmagyarázat beállítása
Kapcsolja össze az adat tartományt a diagrammal és helyezze el a jelmagyarázatot.

```java
// Set series and category data for the chart
chart.getNSeries().add("Data!B2:B8", true);
chart.getNSeries().setCategoryData("Data!A2:A8");
chart.getNSeries().setColorVaried(true);

// Position the legend at the top of the chart
import com.aspose.cells.Legend;
import com.aspose.cells.LegendPositionType;

Legend legend = chart.getLegend();
legend.setPosition(LegendPositionType.TOP);
```

### 8. Workbook Excel exportálása
Végül **export workbook excel** egy XLS fájlba (vagy bármely támogatott formátumba).

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "SPAsBFillInChart_out.xls");
```

## Gyakorlati alkalmazások
- **Business Reports** – Automatikusan generálja az értékesítési diagramokat havi PDF-ekhez.  
- **Data Analysis Tools** – Dinamikus diagramok beágyazása egyedi analitikai műszerfalakba.  
- **Enterprise Dashboards** – A diagram képeket valós időben frissíti a monitorozáshoz.

## Teljesítményfontosságú szempontok
- Csoportos cella frissítések nagy adathalmazok esetén a terhelés csökkentése érdekében.  
- Erőforrások felszabadítása (`workbook.dispose()`), ha ciklusban sok munkafüzetet dolgozol fel.

## Gyakori problémák és megoldások
- **Image not showing** – Ellenőrizze a fájl útvonalát és hogy a képformátum (PNG, JPEG) támogatott-e.  
- **Chart appears blank** – Győződjön meg róla, hogy az adat tartomány hivatkozások (`Data!B2:B8`) egyeznek a feltöltött cellákkal.  
- **Out‑of‑memory errors** – Az adatokat darabokban dolgozza fel, és hívja a `System.gc()`‑t nagy mentések után.

## Gyakran Ismételt Kérdések

**Q: Hogyan adhatok hozzá több sorozatot egy oszlopdiagramhoz?**  
A: Hívja többször a `chart.getNSeries().add()`‑t különböző adat tartományokkal, például `"Data!C2:C8"` a második sorozathoz.

**Q: Megváltoztathatom a tengelycímkéket?**  
A: Igen. Használja a `chart.getCategoryAxis().setTitle("Regions")` és a `chart.getValueAxis().setTitle("Sales")` metódusokat.

**Q: Milyen formátumokba exportálhatok az XLS-en kívül?**  
A: Használja a `workbook.save("chart.pdf")`, `workbook.save("chart.png")`, vagy `workbook.save("chart.xlsx")` parancsokat PDF, PNG és XLSX esetén.

**Q: Szükséges licenc a fejlesztői buildhez?**  
A: Az ingyenes próba a kiértékeléshez megfelelő, de a termelési környezethez állandó vagy ideiglenes licenc szükséges.

**Q: Hogyan javíthatom a renderelés sebességét több ezer sor esetén?**  
A: Töltse fel a cellákat a `cells.importArray()` segítségével, és minimalizálja a diagram újrarajzolását úgy, hogy a diagramot az összes adat betöltése után hozza létre.

**Last Updated:** 2026-04-08  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose  

## Erőforrások

- [Aspose.Cells dokumentáció](https://reference.aspose.com/cells/java/)
- [Aspose.Cells letöltése](https://releases.aspose.com/cells/java/)
- [Licenc vásárlása](https://purchase.aspose.com/buy)
- [Ingyenes próba](https://releases.aspose.com/cells/java/)
- [Ideiglenes licenc kérése](https://purchase.aspose.com/temporary-license/)
- [Támogatási fórum](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}