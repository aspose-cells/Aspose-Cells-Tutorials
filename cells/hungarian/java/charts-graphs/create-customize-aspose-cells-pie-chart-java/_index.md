---
date: '2026-09-27'
description: Ismerje meg, hogyan készítsen kördiagramot Java-ban az Aspose.Cells használatával.
  Lépésről‑lépésre útmutató az Excel kördiagram testreszabásához, a Maven függőség
  beállításához és professzionális diagramok generálásához.
keywords:
- create pie chart java
- customize excel pie chart
- maven dependency aspose cells
lastmod: '2026-09-27'
og_description: Kördiagram készítése Java-ban az Aspose.Cells for Java segítségével.
  Ismerje meg, hogyan testreszabja az Excel kördiagramot, adjon hozzá Maven függőséget,
  és generáljon professzionális diagramokat percek alatt.
og_image_alt: Java code generating a customized pie chart in Excel with Aspose.Cells
og_title: Kördiagram készítése Java-ban az Aspose.Cells segítségével – Teljes Java
  útmutató
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to create pie chart java using Aspose.Cells. Step‑by‑step
    guide to customize Excel pie chart, set up Maven dependency, and generate professional
    charts.
  headline: How to create pie chart java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes, repeat the chart‑creation steps for each data range; each chart is
      independent.
    question: Can I generate multiple pie charts in the same workbook?
  - answer: It does; set the chart type to `ChartType.PIE_3D` when adding the chart.
    question: Does Aspose.Cells support 3‑D pie charts?
  - answer: Use the `Workbook.setDefaultTheme` method before creating any charts.
    question: How do I apply a custom theme to all charts?
  - answer: Over 30 formats, including XLSX, CSV, PDF, and HTML.
    question: What file formats can I export the workbook to?
  - answer: Yes, a valid license removes evaluation watermarks and unlocks full functionality.
    question: Is a license required for commercial deployment?
  type: FAQPage
tags:
- Aspose.Cells
- Java charting
- Excel automation
- data visualization
title: Hogyan készítsünk kördiagramot Java-ban az Aspose.Cells segítségével
url: /hu/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan hozzunk létre kördiagramot Java-val az Aspose.Cells segítségével

## Bevezetés
A **pie chart** programozott létrehozása gyakran olyan, mint egy kirakós, különösen, ha finomhangolt vezérlést igényel a színek, jelmagyarázatok és címek felett. Ebben az útmutatóban megtanulja, hogyan **kördiagramot Java-ban létrehozni** az Aspose.Cells használatával, majd testre szabhatja az Excel kördiagramot, hogy illeszkedjen a márkájához vagy a jelentésstílusához. Végigvezetjük a környezet beállításán, az adatok feltöltésén, a diagram generálásán és a vizuális finomhangoláson — mindezt anélkül, hogy elhagyná a Java IDE-jét.

**Mit fog megtanulni**
- Adja hozzá a **Maven dependency Aspose.Cells**-t a projektjéhez.
- Hozzon létre egy munkafüzetet, töltse fel a cellákat adatokkal, és generáljon egy kördiagramot.
- Alkalmazzon egyedi színeket, címeket és jelmagyarázatokat a diagramra.
- Exportálja a munkafüzetet egy megosztásra kész XLSX fájlba.

Mielőtt elkezdené, legyen jártas az alapvető Java szintaxisban, és legyen telepítve a Maven vagy a Gradle.

## Gyors válaszok
- **Melyik könyvtár hoz létre kördiagramokat Java-ban?** Aspose.Cells for Java.
- **Szükségem van licencre?** Egy ingyenes próba a fejlesztéshez működik; a termeléshez fizetett licenc szükséges.
- **Mely Maven koordináták szükségesek?** `com.aspose:aspose-cells:24.10`.
- **Módosíthatom a szelet színeit?** Igen, a `setAreaColor` metódussal minden sorozatra.
- **Exportálható a diagram XLSX-be?** Teljesen — egyszerűen hívja a `workbook.save("output.xlsx")`-t.

## Mi az a kördiagram az Excelben?
A kördiagram egyetlen adat sorozatot ábrázol arányos szeletekkel egy körben, megkönnyítve a teljeshez viszonyított részek összehasonlítását. Minden szelet szöge az értékének a teljeshez viszonyított arányát tükrözi, így gyors betekintést nyújt a megoszlásba különböző kategóriák, például piaci részesedés, költségvetési elosztás vagy demográfiai arányok esetén.

## Miért használja az Aspose.Cells-t kördiagram Java-ban történő létrehozásához?
Az Aspose.Cells több mint 50 diagramtípust támogat, és akár egy millió soros munkalapokat is kezel anélkül, hogy az egész fájlt a memóriába töltené. Ez a teljesítményelőny lehetővé teszi nagy jelentések generálását közepes hardveren, miközben finomhangolt vezérlést biztosít a diagram megjelenése, adatkapcsolata és exportformátumai felett, így felülmúlja számos nyílt forráskódú könyvtárat.

## Előfeltételek
- **Java Development Kit (JDK)** 8 vagy újabb.
- **IDE**, például IntelliJ IDEA vagy Eclipse.
- **Maven** vagy **Gradle** a függőségkezeléshez.
- Egy **trial vagy megvásárolt Aspose.Cells licenc**.

### Szükséges könyvtárak és függőségek
Add the Aspose.Cells Maven artifact to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Or the Gradle equivalent:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Licenc beszerzésének lépései
Az Aspose.Cells for Java kereskedelmi termék, de ingyenes próba verzióval is elkezdhet. Látogassa meg a [purchase page](https://purchase.aspose.com/buy) oldalt, hogy ideiglenes licenckulcsot szerezzen.

## Az Aspose.Cells beállítása Java-hoz
First, make sure the library is on your classpath. After adding the dependency, you can initialize the API as shown below.

```java
import com.aspose.cells.Workbook;

// Initialize a new workbook instance
Workbook workbook = new Workbook();
```

## Implementációs útmutató

### Munkafüzet létrehozása és konfigurálása
The `Workbook` class represents an entire Excel file in memory.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### 1. lépés: munkafüzet példányosítása
```java
// Creates an empty workbook instance to work with.
Workbook workbook = new Workbook();
```  
Ez egy új, üres munkafüzetet hoz létre, amelyet azonnal elkezdhet feltölteni.

### Munkalap celláinak elérése vagy módosítása
A `Worksheet` represents a single sheet within the workbook, containing cells, rows, and columns.  
You’ll write the data that drives the pie chart into a worksheet.

#### 2. lépés: az első munkalap és annak celláinak lekérése
```java
// Access the first worksheet in the workbook.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Put sample values used for a pie chart into specific cells.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Put percentage values for a pie chart into specific cells.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```  
Töltse fel a cellákat kategória nevekkel és értékekkel, amelyeket a diagram felhasznál.

### Kördiagram létrehozása
`Chart` objects visualize data in a worksheet and support various types such as pie, column, and line.

#### 3. lépés: kördiagram hozzáadása a munkalaphoz
```java
// Create a pie chart in the worksheet.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```  

### Kördiagram sorozat és adat konfigurálása
`Series` defines the data range and formatting for a chart, linking worksheet cells to visual elements.

#### 4. lépés: a sorozat beállítása a diagramhoz
```java
// Configure the series data range for the chart.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Link the pie chart title to a cell containing the title text.
pie.getTitle().setLinkedSource("D2");
```  

### Diagram jelmagyarázat és cím megjelenésének konfigurálása
A chart `Legend` displays the series names and colors, helping readers identify each slice.

#### 5. lépés: diagram jelmagyarázat és cím testreszabása
```java
// Set legend position at bottom of the chart.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Set font properties for the chart title.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```  

### Diagram sorozat színeinek testreszabása
`setAreaColor` sets the fill color of a chart series slice using an RGB value.

#### 6. lépés: a kördiagram szeletek színének megváltoztatása
```java
import com.aspose.cells.Color;

// Access and customize colors of individual pie chart segments.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```  

### Oszlopok automatikus méretezése és munkafüzet mentése
`autoFitColumns` automatically adjusts column widths to fit the cell contents.

#### 7. lépés: oszlopszélességek beállítása és a fájl mentése
```java
// Autofit all columns.
worksheet.autoFitColumns();

// Define output directory placeholder path for saving the workbook.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Save the modified workbook to an Excel file in the specified directory.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```  

## Gyakori felhasználási esetek
- **Demográfiai elemzés:** A népesség eloszlásának megjelenítése régiók szerint.
- **Piaci részesedés jelentés:** Egy pillantással megjeleníti minden versenytárs részesedését.
- **Költségvetés elosztása:** Kiemeli, hogyan oszlanak meg a pénzeszközök a részlegek között.

## Teljesítménybeli megfontolások
- Szabadítsa fel az objektumokat (`workbook.dispose()`), amikor már nincs rájuk szükség, hogy felszabadítsa a natív memóriát.
- Nagy adathalmazok esetén használja a `WorkbookDesigner`-t az adatok streameléséhez ahelyett, hogy egyszerre betöltené az összeset.
- Profilozza a Java Flight Recorder-rel, hogy felfedezze a diagramgenerálás esetleges szűk keresztmetszetét.

## Gyakran ismételt kérdések

**K: Létrehozhatok több kördiagramot ugyanabban a munkafüzetben?**  
V: Igen, ismételje meg a diagramkészítési lépéseket minden adatcsoporthoz; minden diagram független.

**K: Az Aspose.Cells támogatja a 3‑D kördiagramokat?**  
V: Igen; a diagram hozzáadásakor állítsa a diagram típusát `ChartType.PIE_3D`-ra.

**K: Hogyan alkalmazhatok egyedi témát minden diagramra?**  
V: Használja a `Workbook.setDefaultTheme` metódust a diagramok létrehozása előtt.

**K: Milyen fájlformátumokba exportálhatom a munkafüzetet?**  
V: Több mint 30 formátum, beleértve az XLSX, CSV, PDF és HTML formátumokat.

**K: Szükséges licenc a kereskedelmi üzembe helyezéshez?**  
V: Igen, egy érvényes licenc eltávolítja a kiértékelési vízjeleket és feloldja a teljes funkcionalitást.

## Következtetés
Most már rendelkezik egy teljes, vég‑től‑végig útmutatóval a **create pie chart java** (kördiagram Java-ban) létrehozásához az Aspose.Cells segítségével. A fenti lépések követésével kifinomult Excel kördiagramokat generálhat, testreszabhatja a színeket és címeket, és beágyazhatja őket bármely jelentési folyamatba. Fedezzen fel más diagramtípusokat — oszlop, vonal, radar — hogy bővítse adat‑vizualizációs eszköztárát.

---

**Last Updated:** 2026-09-27  
**Tested with:** Aspose.Cells 24.10 for Java  
**Author:** Aspose

## Kapcsolódó oktatóanyagok

- [Excel diagram adatcímkék testreszabása Aspose.Cells for Java segítségével: Lépésről lépésre útmutató](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Dinamikus Excel diagramok létrehozása Aspose.Cells Java-val: Átfogó útmutató fejlesztőknek](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Excel munkafüzetek létrehozása és testreszabása Aspose.Cells Java-val: Lépésről lépésre útmutató](/cells/java/workbook-operations/create-customize-excel-workbooks-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}