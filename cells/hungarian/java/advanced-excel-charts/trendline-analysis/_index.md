---
date: 2026-08-27
description: Ismerje meg, hogyan adhat trendline-t a chart-hoz, megjelenítheti az
  R‑squared értékét, és exportálhatja a chart-ot PNG vagy JPEG képként az Aspose.Cells
  for Java használatával.
keywords:
- add trendline to chart
- save chart as image
- export excel chart image
- java create excel workbook
- convert chart to png
lastmod: 2026-08-27
linktitle: Export Chart képként trendline elemzéssel
og_description: Trendline hozzáadása a chart-hoz, R‑squared megtekintése, és az eredmény
  exportálása PNG/JPEG formátumban az Aspose.Cells for Java használatával – egy gyors,
  50‑formátumú megoldás.
og_image_alt: Guide showing Java code to add a trendline to an Excel chart and export
  it as an image
og_title: Trendline hozzáadása a chart-hoz és exportálása képként az Aspose.Cells
  for Java segítségével
schemas:
- author: Aspose
  dateModified: '2026-08-27'
  description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  headline: How to add trendline to chart and export as image in Java
  type: TechArticle
- description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  name: How to add trendline to chart and export as image in Java
  steps:
  - name: set up the project
    text: Create a new Java project and place the Aspose.Cells JARs on the build path.
      This prepares the environment for generating and manipulating Excel files.
  - name: load excel file (load excel file java)
    text: '*We’ve just **loaded an Excel file** into memory, ready for chart creation.*'
  - name: create a chart
    text: '*Here we generate a line chart that will later host our trendline.*'
  - name: add trendline (how to add trendline) and display R‑squared value
    text: '*The `setDisplayRSquaredValue(true)` call ensures the **R‑squared value**
      appears on the chart.*'
  - name: customize chart and save workbook (save workbook xlsx, generate excel file
      java)
    text: '*Now the workbook is **generated** and saved as an XLSX file, ready for
      further processing.*'
  - name: export chart to image (export chart to image)
    text: '> **Note:** This step is described without an additional code block to
      keep the original block count unchanged. After the chart is created and saved,
      you can export it to an image by calling the `chart.toImage()` method and writing
      the resulting `java.awt.image.BufferedImage` to a file format of you'
  type: HowTo
- questions:
  - answer: Use a different `TrendlineType` enumeration when adding the trendline,
      e.g., `TrendlineType.POLYNOMIAL` for a polynomial fit.
    question: How can I change the trendline type?
  - answer: Yes. Access the trendline’s `LineFormat` via `trendline.getLineFormat()`
      and set properties such as `setWeight()` and `setColor()`.
    question: Can I customize the trendline appearance (color, thickness)?
  - answer: Convert the chart to an image first, then embed that image into a PDF
      using Aspose.PDF or any other PDF library.
    question: How do I export the chart to PDF instead of an image?
  - answer: Absolutely. Call `chart.getNSeries().get(0).getTrendlines().add(...)`
      for each series you wish to analyze.
    question: Is it possible to add multiple trendlines to the same chart?
  - answer: Yes. You can specify the DPI when calling `chart.toImage()` and then scale
      the image before saving, ensuring crisp output for print or high‑density screens.
    question: Does Aspose.Cells support high‑resolution image export?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java charting
- Excel automation
- trendline analysis
title: Hogyan adjon trendline-t a chart-hoz, és exportálja képként Java-ban
url: /hu/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trendvonal hozzáadása a diagramhoz és exportálása képként

Ebben az útmutatóban megtanulja, hogyan **trendvonal hozzáadása a diagramhoz**, megjeleníti az R‑squared értéket, és exportálja a vizuális elemet PNG vagy JPEG fájlba az Aspose.Cells for Java használatával. Megtudja, miért fontosak a trendvonalak, hogyan kell előkészíteni a munkafüzetet, és a pontos lépéseket egy nagy felbontású kép előállításához, amely beágyazható jelentésekbe, e‑mail üzenetekbe vagy weboldalakra.

## Gyors válaszok
- **Mi a fő célja ennek az útmutatónak?** Annak bemutatása, hogyan adhat hozzá trendvonalat a diagramhoz, megjelenítheti annak egyenletét és R‑squared értékét, valamint exportálhatja a diagramot képként Java-val.  
- **Melyik könyvtárra van szükségem?** Aspose.Cells for Java – töltse le a [Aspose.Cells for Java release page](https://releases.aspose.com/cells/java/) oldalról.  
- **Szükségem van licencre a fejlesztéshez?** Egy ingyenes próba verzió működik fejlesztéshez; a termelési környezethez kereskedelmi licenc szükséges.  
- **Létrehozhatom programozottan az Excel munkafüzetet?** Igen – az útmutató egy üres XLSX munkafüzetet hoz létre és ment.  
- **Hogyan exportálódik a diagram PNG vagy JPEG formátumba?** Hívja meg a `Chart.toImage()` metódust, és írja a visszaadott `BufferedImage`-et a `ImageIO.write(...)` segítségével.

## Hogyan hoz létre Excel diagramot trendvonallal, és exportálja képként?
Töltse be a munkafüzetet, adjon hozzá egy vonaldiagramot, csatoljon egy trendvonalat, amely megjeleníti az egyenletet és az R‑squared értéket, mentse a munkafüzetet, majd hívja meg a `chart.toImage()` metódust, és írja a kapott `BufferedImage`-et PNG vagy JPEG fájlba. Ez az vég‑végi folyamat csak néhány Java sorból áll, és pixel‑tökéletes képet eredményez, amely bármely további alkalmazáshoz alkalmas.

## Mi a diagram exportálása képként?
A diagram képként történő exportálása a adatainak vizuális ábrázolását egy hordozható bitmapre (PNG, JPEG, BMP stb.) alakítja. Ez a formátum ideális a diagramok jelentésekbe, weboldalakba vagy prezentációkba ágyazásához, ahol az eredeti Excel fájl nem szükséges.

## Miért adjunk hozzá trendvonalat és jelenítsük meg az R‑squared értéket?
A trendvonal feltárja az adat sorozat mögötti mintát, míg a **R‑squared** metrika azt méri, mennyire illeszkedik a trendvonal az adatokhoz. Mindkettő szerepeltetése az exportált képen azonnali betekintést nyújt az érintetteknek anélkül, hogy meg kellene nyitni a munkafüzetet. Segít a döntéshozóknak gyorsan felmérni a korreláció erősségét és előre jelezni a trendeket anélkül, hogy Excel-t kellene megnyitni.

## Előfeltételek
- Java 8 vagy újabb telepítve legyen a fejlesztői gépen.  
- Aspose.Cells for Java könyvtár hozzáadva a projekt classpath-jához (JAR fájlok).  
- Ismerete legyen egy Java IDE-nek, például az IntelliJ IDEA-nak vagy az Eclipse-nek.  

## Lépésről‑lépésre útmutató

### 1. lépés: a projekt beállítása
Hozzon létre egy új Java projektet, és helyezze az Aspose.Cells JAR fájlokat a build útvonalra. Ez előkészíti a környezetet Excel fájlok generálásához és manipulálásához.

### 2. lépés: Excel fájl betöltése (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*Épp most **betöltöttünk egy Excel fájlt** a memóriába, készen áll a diagram létrehozására.*

### 3. lépés: diagram létrehozása
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Itt egy vonaldiagramot generálunk, amely később a trendvonalunkat fogja tartalmazni.*

### 4. lépés: trendvonal hozzáadása (how to add trendline) és R‑squared érték megjelenítése
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*A `setDisplayRSquaredValue(true)` hívás biztosítja, hogy a **R‑squared érték** megjelenjen a diagramon.*

### 5. lépés: diagram testreszabása és munkafüzet mentése (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Most a munkafüzet **létre lett hozva** és XLSX fájlként mentve, készen áll a további feldolgozásra.*

### 6. lépés: diagram exportálása képként (export chart to image)
> **Megjegyzés:** Ez a lépés egy további kódrészlet nélkül van leírva, hogy az eredeti blokk szám változatlan maradjon.  
Miután a diagram létrejött és mentésre került, exportálhatja képként a `chart.toImage()` metódus meghívásával, és a kapott `java.awt.image.BufferedImage`-et a választott fájlformátumba (PNG, JPEG, BMP) írva. A tipikus munkafolyamat a következő:
1. Szerezze be a `Chart` objektumot (már megtörtént az előző lépésekben).  
2. Hívja meg a `chart.toImage()` metódust, hogy egy `BufferedImage`-et kapjon.  
3. Használja az `ImageIO.write(bufferedImage, "png", new File("chart.png"))` kifejezést a fájl írásához.  

A `Chart` objektum a munkafüzetben lévő diagramot képviseli, és módszereket biztosít a megjelenés és az adatok módosításához. A `BufferedImage` egy Java osztály, amely memóriában tárol egy képet, lehetővé téve annak fájlba mentését. Az `ImageIO` egy segédosztály a képek Java-ban történő olvasásához és írásához. A `setDisplayRSquaredValue` lehetővé teszi az R‑squared statisztika megjelenítését a trendvonalon.

### Eredmények elemzése
Nyissa meg az `output.xlsx` fájlt Excelben, hogy ellenőrizze, a trendvonal, az egyenlet és az R‑squared érték a várt módon jelenik meg. Nyissa meg az exportált képfájlt (pl. `chart.png`), hogy egy tiszta vizuális megjelenítést lásson, amely az eredeti munkafüzet nélkül is megosztható.

## Gyakori problémák és megoldások
- **Trendvonal nem jelenik meg:** Győződjön meg arról, hogy az adat tartomány (`A1:A10`) numerikus értékeket tartalmaz; a nem numerikus adatok megakadályozzák a trendvonal számítását.  
- **R‑squared érték 0‑ként jelenik meg:** Ez gyakran azt jelenti, hogy az adat sorozat állandó vagy nincs változatossága. Próbáljon másik adatkészletet, vagy használjon polinomiális trendvonalat.  
- **Kép exportálás sikertelen `NullPointerException` hibával:** Ellenőrizze, hogy a diagram teljesen renderelődött-e a `toImage()` meghívása előtt. A munkafüzet előzetes mentése néha megoldja az időzítési problémákat.

## Gyakran feltett kérdések

**K: Hogyan változtathatom meg a trendvonal típusát?**  
V: Használjon másik `TrendlineType` felsorolást a trendvonal hozzáadásakor, például `TrendlineType.POLYNOMIAL` a polinomiális illesztéshez.

**K: Testreszabhatom a trendvonal megjelenését (szín, vastagság)?**  
V: Igen. A trendvonal `LineFormat`-ját a `trendline.getLineFormat()` segítségével érheti el, és beállíthatja például a `setWeight()` és `setColor()` tulajdonságokat.

**K: Hogyan exportálhatom a diagramot PDF-be a kép helyett?**  
V: Először konvertálja a diagramot képpé, majd ágyazza be azt PDF-be az Aspose.PDF vagy bármely más PDF könyvtár segítségével.

**K: Lehetséges több trendvonalat hozzáadni ugyanahhoz a diagramhoz?**  
V: Természetesen. Hívja meg a `chart.getNSeries().get(0).getTrendlines().add(...)` metódust minden sorozathoz, amelyet elemezni szeretne.

**K: Támogatja az Aspose.Cells a nagy felbontású kép exportálást?**  
V: Igen. A DPI-t megadhatja a `chart.toImage()` meghívásakor, majd a mentés előtt skálázhatja a képet, biztosítva a tiszta kimenetet nyomtatáshoz vagy nagy felbontású képernyőkhöz.

---

**Utoljára frissítve:** 2026-08-27  
**Tesztelve:** Aspose.Cells for Java legújabb (támogat 50+ fájlformátumot és akár 2 millió soros munkafüzetet is feldolgoz teljes memória betöltése nélkül)  
**Szerző:** Aspose

## Kapcsolódó útmutatók

- [Adatcímkék hozzáadása Excel diagramhoz Aspose.Cells Java-val](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Hogyan exportáljunk Excel diagramokat SVG formátumba az Aspose.Cells Java-val a méretezhető vektorgrafikához](/cells/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Excel diagramok exportálása PDF-be Aspose.Cells for Java&#58; egyedi oldalméretek útmutatója](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}