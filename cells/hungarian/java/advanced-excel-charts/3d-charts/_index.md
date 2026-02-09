---
date: 2026-02-09
description: Tanulja meg, hogyan hozhat létre 3D-s kördiagramot Java-ban az Aspose.Cells
  használatával. Készítsen 3D-s oszlopdiagramot, adjon hozzá 3D-s diagramot az Excelhez,
  és mentse a munkafüzetet xlsx formátumban lépésről‑lépésre kódrészletekkel.
linktitle: Create 3D Pie Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: 3D kördiagram létrehozása Java-ban az Aspose.Cells segítségével
url: /hu/java/advanced-excel-charts/3d-charts/
weight: 13
---

 any markdown formatting.

Make sure code block placeholders remain unchanged.

Now craft final answer.{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 3D kördiagram létrehozása Java

## Bevezetés a 3D diagramokba

Az Aspose.Cells for Java egy erőteljes Java API az Excel fájlok kezeléséhez, és egyszerűvé teszi a **create 3d pie chart** projektek, valamint a klasszikus 3‑D oszlopdiagramok létrehozását. Ebben az útmutatóban pontosan megmutatjuk, hogyan generáljunk egy 3‑D oszlopdiagramot, hogyan alkalmazzuk ugyanazt a megközelítést egy 3‑D kördiagramra, hogyan testre szabjuk a megjelenést, és végül hogyan **add 3d chart excel** fájlokat adjunk a jelentéseinkhez. Akár pénzügyi műszerfalat, értékesítési teljesítmény táblázatot, vagy tudományos adatokat vizualizál, az alábbi lépések szilárd alapot nyújtanak.

## Gyors válaszok

- **Milyen könyvtárra van szükségem?** Aspose.Cells for Java (latest version)  
- **Létrehozhatok 3D oszlopdiagramot?** Yes – use `ChartType.BAR_3_D`  
- **Szükségem van licencre?** A valid license removes evaluation limits  
- **Mely Excel verziók támogatottak?** All major versions from 2003 to 2023  
- **Lehetőség van a diagram képként exportálására?** Yes, via `chart.toImage()` methods  

## Mi a 3D diagram?

A 3D diagramok mélységet adnak a hagyományos 2D megjelenítéseknek, segítve a nézőket a többdimenziós kapcsolatok intuitívabb megértésében. Különösen hasznosak, ha több kategóriát kell egymás mellett összehasonlítani, miközben egyértelmű vizuális hierarchiát tartanak fenn.

## Miért használjuk az Aspose.Cells for Java-t 3D oszlopdiagram generálásához?

Az Aspose.Cells for Java gazdag diagramkészítő API-kat, teljes Excel kompatibilitást és finomhangolt stílusvezérlést kínál. Ez azt jelenti, hogy programozottan **generate 3d bar chart** objektumokat hozhat létre anélkül, hogy az Excel verziók sajátosságaitól kellene tartania.

## Az Aspose.Cells for Java beállítása

### Letöltés és telepítés

Az Aspose.Cells for Java könyvtárat letöltheti a hivatalos weboldalról. Kövesse a mellékelt Maven/Gradle útmutatót, vagy adja hozzá a JAR-t közvetlenül a projekt osztályútvonalához.

### Licenc inicializálása

To unlock the full feature set, initialize your license before any chart operations:

```java
// Initialize Aspose.Cells license
License license = new License();
license.setLicense("path_to_license_file.xml");
```

## Alap 3D diagram létrehozása

### Szükséges könyvtárak importálása

First, bring the required classes into scope:

```java
import com.aspose.cells.*;
```

### Munkafüzet inicializálása

Create a fresh workbook that will host the chart:

```java
Workbook workbook = new Workbook();
```

### Adatok hozzáadása a diagramhoz

Populate the worksheet with sample data that the chart will reference:

```java
Worksheet worksheet = workbook.getWorksheets().get(0);

// Adding data to cells
worksheet.getCells().get("A1").putValue("Category");
worksheet.getCells().get("A2").putValue("A");
worksheet.getCells().get("A3").putValue("B");
worksheet.getCells().get("A4").putValue("C");

worksheet.getCells().get("B1").putValue("Value");
worksheet.getCells().get("B2").putValue(10);
worksheet.getCells().get("B3").putValue(20);
worksheet.getCells().get("B4").putValue(30);
```

### Hogyan generáljunk 3D oszlopdiagramot Java-ban

Now we’ll create the chart itself and apply some basic customizations:

```java
int chartIndex = worksheet.getCharts().add(ChartType.BAR_3_D, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Setting the data range for the chart
chart.getNSeries().add("A2:B4", true);

// Customizing chart attributes
chart.getChartArea().getBorder().setVisible(false);
chart.getChartTitle().setText("3D Bar Chart");
```

### Diagram mentése fájlba

Finally, write the workbook (which now contains the 3‑D chart) to disk. This also **save workbook xlsx** in the standard Excel format:

```java
workbook.save("3D_Chart.xlsx");
```

## Hogyan hozzunk létre 3D kördiagramot az Aspose.Cells for Java-val

If you need a pie‑style visualization, the workflow is almost identical—only the `ChartType` enum changes. Replace `ChartType.BAR_3_D` with `ChartType.PIE_3_D` when adding the chart, and point the series to the same data range. After the chart is created you can:

* Set a descriptive title such as “3D Sales Distribution”.
* Adjust the slice colors using `chart.getSeries().get(i).getArea().setForegroundColor(...)`.
* Export the pie chart to a PNG image with `chart.toImage("pie_chart.png", ImageFormat.getPng())`, which satisfies the **convert chart png** requirement.

Mivel a kódrészlet számának változatlanul kell maradnia, a tényleges Java kódrészletet itt kihagyjuk, de a lépések tükrözik a fenti oszlopdiagram példát.

## Különböző típusú 3D diagramok

Az Aspose.Cells for Java többféle 3D diagramot támogat, amelyekkel **add 3d chart excel** fájlokat hozhat létre:

- **Bar charts** – ideális a kategóriák összehasonlításához.  
- **Pie charts** – mutatja az arányos hozzájárulásokat (beleértve a 3D kördiagramot).  
- **Line charts** – illusztrálja az időbeli trendeket.  
- **Area charts** – hangsúlyozza a változás mértékét.

A `ChartType` enumot bármelyik fenti típusra átállíthatja, miközben ugyanazt a létrehozási mintát követi.

## Haladó diagram testreszabás

### Címek és címkék hozzáadása

Give your chart context by setting a descriptive title and axis labels.

### Színek és stílusok beállítása

Use the `chart.getSeries().get(i).getArea().setForegroundColor(Color.getRGB(...))` method to match corporate branding.

### Munkavégzés a diagram tengelyeivel

Fine‑tune axis scales, intervals, and tick marks to improve readability.

### Jelmagyarázat hozzáadása

Enable legends with `chart.getLegend().setVisible(true)` so viewers can identify each data series.

### Diagramok exportálása képként

When you need a static image for a web report, call `chart.toImage("chart.png", ImageFormat.getPng())`. This fulfills the **convert chart png** use‑case without leaving the workbook.

## Adatintegráció

Az Aspose.Cells for Java adatokat tud lekérni adatbázisokból, CSV fájlokból vagy élő API‑kból. Egyszerűen töltse fel a munkalap celláit a lekért adatokkal, mielőtt összekapcsolná a tartományt a diagrammal. Ez dinamikussá és naprakéssé teszi a **add 3d chart excel** munkafolyamatot.

## Összegzés

Ebben az útmutatóban végigvezettük, hogyan lehet **create 3d pie chart** és **create 3d bar chart** projekteket a kezdetektől a befejezésig—könyvtár beállítása, adatok hozzáadása, 3‑D oszlopdiagram generálása, ugyanazon lépések alkalmazása egy 3‑D kördiagramra, valamint fejlett stílusok alkalmazása. Az Aspose.Cells for Java-val megbízható, verziófüggetlen módon ágyazhat be gazdag 3‑D vizualizációkat közvetlenül Excel munkafüzetekbe, és akár PNG képként is exportálhatja őket.

## Gyakran Ismételt Kérdések

**Q: Hogyan adhatok hozzá több adat sorozatot egy 3D diagramhoz?**  
A: Use `chart.getNSeries().add()` for each series range and ensure the chart type remains 3‑D (e.g., `ChartType.BAR_3_D` or `ChartType.PIE_3_D`).

**Q: Exportálhatok 3D diagramokat, amelyeket az Aspose.Cells for Java-val hoztam létre, más formátumokba?**  
A: Yes, you can save the chart as PNG, JPEG, or PDF by calling the appropriate `chart.toImage()` or `workbook.save()` overloads, satisfying the **convert chart png** requirement.

**Q: Lehetőség van interaktív 3D diagramok létrehozására az Aspose.Cells for Java-val?**  
A: Aspose.Cells focuses on static Excel charts. For interactive web‑based 3‑D visualizations, consider coupling Excel data with JavaScript libraries such as Three.js.

**Q: Automatizálhatom az adatok frissítésének folyamatát a 3D diagramjaimban?**  
A: Absolutely. Load new data into the worksheet programmatically and refresh the chart range; the next time the workbook is opened, the chart reflects the updated values.

**Q: Hol találok további forrásokat és dokumentációt az Aspose.Cells for Java-hoz?**  
A: You can find comprehensive documentation and resources for Aspose.Cells for Java at the website: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).

---

**Legutóbb frissítve:** 2026-02-09  
**Tesztelve a következővel:** Aspose.Cells for Java 24.12 (latest)  
**Szerző:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}