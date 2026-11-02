---
date: 2026-09-02
description: Ismerje meg, hogyan exportálhat diagramot PNG-be, adhat hozzá adat sorozatot,
  kombinálhat vonal- és oszlopdiagramot, mentheti a munkafüzetet XLSX formátumban,
  és hozzáadhat jelmagyarázatot a diagramhoz az Aspose.Cells for Java használatával.
keywords:
- export chart to png
- combine line and column chart
- save workbook as xlsx
- generate chart image java
lastmod: 2026-09-02
linktitle: Diagram exportálása PNG-be és adat sorozat hozzáadása kombinált diagramhoz
og_description: Diagram exportálása PNG-be az Aspose.Cells for Java segítségével,
  vonal- és oszlopdiagram kombinálása, adat sorozat hozzáadása, és munkafüzet mentése
  XLSX formátumban egyetlen útmutatóban.
og_image_alt: Developer guide showing combined line‑column chart export to PNG using
  Aspose.Cells for Java
og_title: Diagram exportálása PNG-be és adat sorozat hozzáadása kombinált diagramhoz
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  headline: Export chart to PNG and add data series for combined chart
  type: TechArticle
- description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  name: Export chart to PNG and add data series for combined chart
  steps:
  - name: import aspose.cells classes
    text: '`Workbook` is Aspose.Cells’ core object that represents an entire Excel
      file in memory.'
  - name: create a new workbook
    text: '`Worksheet` represents a single sheet inside a `Workbook` and provides
      access to cells, rows, and charts.'
  - name: access the first worksheet
    text: '`Chart` is the object that holds all chart‑related settings, series, and
      rendering options.'
  - name: add a combined chart object to the worksheet
    text: We’ll start with a line chart and later add a column series to achieve a
      **combined line column chart** effect.
  - name: define the data ranges and add data series
    text: '`NSeries` is the collection that stores each data series for a chart. Adding
      a series links a range of cells to the chart. > **Pro tip:** The first parameter
      (`"A1:A5"`) is the range for the first series, and the second (`"B1:B5"`) creates
      a second series that will be combined with the first.'
  - name: set the category (X‑axis) data
    text: '`CategoryAxis` represents the horizontal axis of the chart, controlling
      the labels displayed along the X‑axis.'
  - name: set chart axis labels and title
    text: '`Title` sets the main title of the chart, and `Axis` objects represent
      the X and Y axes.'
  - name: add legend chart and adjust its position
    text: '`Legend` controls the placement and appearance of the series legend in
      the chart.'
  - name: save the workbook as an Excel file (XLSX)
    text: '`Workbook.save` writes the in‑memory workbook to a file in the specified
      format.'
  - name: export chart to PNG
    text: '`Chart.toImage` renders the chart as an image file in the chosen format.
      > The `chart.toImage` method **generates Excel chart** images that can be used
      in web pages, reports, or emails.'
  type: HowTo
- questions:
  - answer: 'Download the JAR from the official site and add it to your project’s
      classpath. The download link is: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).'
    question: How do I install Aspose.Cells for Java?
  - answer: Yes, Aspose.Cells supports bar, pie, scatter, area, and many more chart
      types. Refer to the API documentation for the full list.
    question: Can I create other chart types besides line and column?
  - answer: A valid Aspose.Cells license is required for production deployments. A
      free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Use `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (or similar)
      after adding the series.
    question: How can I change the colors of each series?
  - answer: 'Comprehensive documentation and additional samples are available at the
      Aspose reference site: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more code examples?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart to png
- Aspose.Cells
- Java Excel charts
title: Diagram exportálása PNG-be és adat sorozat hozzáadása kombinált diagramhoz
url: /hu/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Diagram exportálása PNG formátumba és adat sorozatok hozzáadása kombinált diagramhoz

Ebben az oktatóanyagban **adat sorozatokat** adsz hozzá egy Excel munkafüzethez, **összevonod** a vonal- és oszlopdiagram elemeket, és megtanulod, hogyan **exportálj diagramot PNG‑be** az Aspose.Cells for Java segítségével. Lépésről lépésre végigvezetünk – a munkafüzet beállításától, a diagram hozzáadásán a munkalaphoz, a jelmagyarázat testreszabásáig, egészen a **munkafüzet mentéséig XLSX‑ként** és a diagram PNG képének generálásáig. A végére egy kész, használatra kész kombinált diagramod lesz, amelyet beágyazhatsz jelentésekbe vagy műszerfalakba.

## Gyors válaszok
- **Melyik könyvtár hoz létre kombinált diagramokat?** Aspose.Cells for Java.  
- **Hogyan adhatok hozzá adat sorozatot?** Hívd meg a `chart.getNSeries().add(...)` metódust a megfelelő tartománnyal.  
- **Hogyan exportálhatom a diagramot PNG‑be?** Használd a `chart.toImage("chart.png", ImageFormat.getPng())` metódust.  
- **Milyen fájlformátumban menthetem a munkafüzetet?** Standard `.xlsx` (munkafüzet mentése XLSX‑ként).  
- **Szükségem van licencre a termeléshez?** Igen – egy érvényes Aspose.Cells licenc szükséges a termelési környezetben.

## Mi az exportálás diagram PNG‑be az Aspose.Cells‑ben?
A diagram PNG‑be exportálása egy raszteres képet hoz létre az Excel diagramról, amely weboldalakon, jelentésekben vagy e‑mailben megjeleníthető anélkül, hogy az Excel alkalmazásra lenne szükség. Ez a módszer pontosan rögzíti a vizuális elrendezést, a színeket és az adatjelölőket, így hordozható képfájlt eredményez.

## Miért hozunk létre kombinált vonal‑oszlop diagramot?
A kombinált vonal‑oszlop diagram lehetővé teszi, hogy különböző adatcsoportokat eltérő vizuális ábrázolással (pl. egy vonal sorozat egy oszlop sorozat felett) jeleníts meg egyetlen nézetben. Ez a megközelítés ideális a trendek összehasonlításához a teljes értékekkel, a korrelációk kiemeléséhez, vagy gazdagabb betekintés nyújtásához, miközben a vizuális lábnyom kicsi marad.

## Előfeltételek
- Java Development Kit (JDK) 8 vagy újabb  
- Aspose.Cells for Java könyvtár (letölthető az alábbi hivatkozásból)  
- Alapvető ismeretek a Java szintaxisról és az Excel koncepciókról  

## Kezdés

Először töltsd le az Aspose.Cells for Java könyvtárat a hivatalos oldalról:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Miután a JAR-t hozzáadtad a projekted osztályútvonalához, elkezdheted a diagram építését.

### 1. lépés: aspose.cells osztályok importálása
`Workbook` az Aspose.Cells alapobjektuma, amely egy teljes Excel fájlt reprezentál a memóriában.  
```java
import com.aspose.cells.*;
```

### 2. lépés: új munkafüzet létrehozása
`Worksheet` egyetlen munkalapot képvisel egy `Workbook`-on belül, és hozzáférést biztosít a cellákhoz, sorokhoz és diagramokhoz.  
```java
Workbook workbook = new Workbook();
```

### 3. lépés: az első munkalap elérése
`Chart` az az objektum, amely minden diagrammal kapcsolatos beállítást, sorozatot és renderelési opciót tartalmaz.  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### 4. lépés: kombinált diagram objektum hozzáadása a munkalaphoz
Először egy vonaldiagrammal kezdünk, majd később hozzáadunk egy oszlopsorozatot, hogy elérjük a **kombinált vonal‑oszlop diagram** hatást.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Adatok hozzáadása a diagramhoz

Miután a diagram konténer létezik, adatokat kell betáplálnunk.

### 5. lépés: adat tartományok meghatározása és adat sorozatok hozzáadása
`NSeries` az a gyűjtemény, amely a diagram minden adat sorozatát tárolja. Sorozat hozzáadása egy cellatartományt köt a diagramhoz.  
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Pro tipp:** Az első paraméter (`"A1:A5"`) az első sorozat tartománya, a második (`"B1:B5"`) egy második sorozatot hoz létre, amely az elsővel kombinálódik.

### 6. lépés: a kategória (X‑tengely) adat beállítása
`CategoryAxis` a diagram vízszintes tengelyét jelöli, amely a X‑tengelyen megjelenő címkéket szabályozza.  
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## A diagram testreszabása

Egy jó diagram történetet mesél. Adjunk neki címeket, tengelycímkéket és egyértelmű jelmagyarázatot.

### 7. lépés: diagram tengelycímkék és cím beállítása
`Title` a diagram fő címét állítja be, és az `Axis` objektumok a X és Y tengelyeket képviselik.  
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### 8. lépés: jelmagyarázat hozzáadása a diagramhoz és a pozíciójának beállítása
`Legend` a sorozat jelmagyarázatának elhelyezését és megjelenését szabályozza a diagramon.  
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## A diagram mentése és exportálása

A testreszabás után **munkafüzet mentése XLSX‑ként** és egy kép generálása lesz a cél.

### 9. lépés: a munkafüzet mentése Excel fájlként (XLSX)
`Workbook.save` a memóriában lévő munkafüzetet a megadott formátumban egy fájlba írja.  
```java
workbook.save("CombinedChart.xlsx");
```

### 10. lépés: diagram exportálása PNG‑be
`Chart.toImage` a diagramot a kiválasztott formátumban képfájlként rendereli.  
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> A `chart.toImage` metódus **Excel diagram** képeket generál, amelyeket weboldalakon, jelentésekben vagy e‑mailben lehet használni.

## Gyakori problémák és hibaelhárítás

| Probléma | Megoldás |
|----------|----------|
| **Nincs adat** | Ellenőrizd, hogy a cellatartományok (`A1:A5`, `B1:B5`, `C1:C5`) valóban tartalmaznak adatot a diagram létrehozása előtt. |
| **A jelmagyarázat átfedi a diagramot** | Állítsd be a `chart.getLegend().setOverlay(false)` értéket, vagy helyezd át a jelmagyarázatot más pozícióba (pl. `RIGHT`). |
| **A kép fájl üres** | Győződj meg róla, hogy a diagramnak legalább egy sorozata van, és a `chart.toImage` a teljes testreszabás után kerül meghívásra. |
| **Mentés hibát dob** | Ellenőrizd, hogy írási jogosultsággal rendelkezel a célkönyvtárban, és a fájl nincs megnyitva Excelben. |

## Gyakran feltett kérdések

**Q: Hogyan telepíthetem az Aspose.Cells for Java‑t?**  
A: Töltsd le a JAR‑t a hivatalos oldalról, és add hozzá a projekted osztályútvonalához. A letöltési hivatkozás: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: Készíthetek más diagramtípusokat is a vonal és oszlop mellett?**  
A: Igen, az Aspose.Cells támogatja az oszlop, kör, szórt, terület és még sok más diagramtípust. Tekintsd meg az API dokumentációt a teljes listáért.

**Q: Szükséges licenc a termelési használathoz?**  
A: Egy érvényes Aspose.Cells licenc szükséges a termelési környezetben. Ingyenes próba verzió is elérhető értékeléshez.

**Q: Hogyan változtathatom meg az egyes sorozatok színeit?**  
A: Használd a `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (vagy hasonló) metódust a sorozatok hozzáadása után.

**Q: Hol találok további kódrészleteket?**  
A: Átfogó dokumentáció és további példák érhetők el az Aspose referencia oldalon: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).

---

**Utoljára frissítve:** 2026-09-02  
**Tesztelve a következővel:** Aspose.Cells for Java legújabb verzió  
**Szerző:** Aspose

## Kapcsolódó oktatóanyagok

- [Hogyan adjunk címkéket az Excel diagramokhoz az Aspose.Cells for Java használatával](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)
- [Hogyan hozzunk létre Excel diagramot trendvonallal és exportáljuk képként az Aspose.Cells for Java használatával](/cells/java/advanced-excel-charts/trendline-analysis/)
- [Excel diagramok exportálása PDF‑be az Aspose.Cells for Java használatával: egyedi oldalméretek útmutató](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}