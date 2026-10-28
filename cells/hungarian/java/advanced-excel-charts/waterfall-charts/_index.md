---
date: 2026-09-02
description: Ismerje meg, hogyan hozhat létre excel vízesés diagramot Java-ban az
  Aspose.Cells segítségével, állítsa be a diagram adat tartományát, testreszabja a
  címkéket, és exportálja XLSX formátumba.
keywords:
- create excel waterfall chart
- waterfall chart data labels
- Aspose.Cells Java chart
lastmod: 2026-09-02
linktitle: Vízesés diagramok
og_description: Excel vízesés diagram létrehozása az Aspose.Cells for Java használatával
  – állítsa be a diagram adat tartományát, adjon hozzá adatcímkéket, és néhány lépésben
  exportálja XLSX formátumba.
og_image_alt: 'Tutorial: create excel waterfall chart with Aspose.Cells Java'
og_title: Excel vízesés diagram létrehozása az Aspose.Cells for Java segítségével
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  headline: Create excel waterfall chart with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  name: Create excel waterfall chart with Aspose.Cells for Java
  steps:
  - name: import Aspose.Cells
    text: The `com.aspose.cells` package contains all classes required for Excel manipulation,
      including workbook creation, worksheet handling, and chart generation.
  - name: initialize workbook and worksheet
    text: A **Workbook** represents an Excel file, and a **Worksheet** is a single
      sheet within that file. Creating these objects provides the canvas for both
      raw data and the chart.
  - name: enter data
    text: Column A holds category labels, while column B contains the numeric values
      for the waterfall. This layout matches the typical profit‑and‑loss flow used
      in financial analysis.
  - name: create the waterfall chart
    text: The **Chart** object creates a visual representation; setting its type to
      `ChartType.WATERFALL` configures it as a waterfall chart. Use the `add` method
      to set the chart data range for the series (`"B2:B6"`), and link the category
      axis to `"A2:A6"`.
  - name: save the workbook
    text: Saving the workbook writes the chart and data to the specified file format.
      Call `workbook.save("WaterfallChart.xlsx")` to generate an XLSX file, or change
      the format parameter to export to PDF, CSV, or HTML.
  type: HowTo
- questions:
  - answer: Use the `add` method on the chart’s series, passing the cell range that
      contains your values, e.g., `"B2:B6"`.
    question: How do I set the chart data range for a financial waterfall chart?
  - answer: Yes, call `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` to generate
      a PDF version.
    question: Can I export the workbook to PDF instead of XLSX?
  - answer: Extend the data range in both the values column and the category column,
      then update the `add` and `setCategoryData` calls accordingly.
    question: What if I need to create a waterfall chart with more categories?
  - answer: Iterate through the `Series` collection and set the `FillFormat` color
      based on each value’s sign; Aspose.Cells lets you apply conditional formatting
      programmatically.
    question: Is there a way to automatically format positive and negative bars?
  - answer: Yes. After modifying cell values, simply re‑save the workbook—the chart
      will reflect the new data automatically.
    question: Does Aspose.Cells support dynamic data updates for charts?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- waterfall chart
- Aspose.Cells
- java excel charts
- excel automation
title: Excel vízesés diagram létrehozása az Aspose.Cells for Java segítségével
url: /hu/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vízárapály diagramok

## Bevezetés a vízárapály diagramokhoz az Aspose.Cells for Java használatával

Ebben az útmutatóban megtanulja, hogyan **hozzon létre Excel vízárapály diagramot** és **állítsa be a diagram adat tartományát** az Aspose.Cells for Java segítségével. A vízárapály diagramok egy sor pozitív és negatív számot alakítanak át egyértelmű vizuális történetté, így ideálisak pénzügyi kimutatásokhoz, értékesítési teljesítmény‑értékelésekhez, és bármilyen helyzetben, ahol látni kell, hogyan járulnak hozzá az egyes elemek az összeghez.

## Gyors válaszok
- **Mi az a vízárapály diagram?** Egy vizuális ábrázolás, amely megmutatja, hogyan növekszik és csökken egy kezdeti érték egy sor közbenső érték által, végül egy végső összeggel.  
- **Melyik könyvtárat használják?** Aspose.Cells for Java.  
- **Szükségem van licencre?** Egy ingyenes próba verzió fejlesztéshez működik; a termeléshez kereskedelmi licenc szükséges.  
- **Menthetem a fájlt XLSX formátumban?** Igen – használja a `workbook.save("FileName.xlsx")` parancsot.  
- **Alkalmas‑e Java adatvizualizációra?** Teljesen; az Aspose.Cells gazdag diagramkészítési funkciókat biztosít Office telepítése nélkül.

## Mi az a vízárapály diagram?
A vízárapály diagram sorozatos pozitív és negatív hozzájárulásokat jelenít meg egy kiinduló értékhez, segítve megérteni, hogyan befolyásolja az egyes komponensek az összesített eredményt. A nyereségek és veszteségek egymás mellé helyezésével a komplex pénzügyi áramlás azonnal olvashatóvá válik.

## Miért használjuk az Aspose.Cells for Java‑t vízárapály diagram hozzáadásához?
Az Aspose.Cells lehetővé teszi Excel diagramok generálását bármely szerveren, CI‑pipeline‑ban vagy asztali gépen anélkül, hogy a Microsoft Excelre lenne szükség. Támogat **15+ kimeneti formátumot** (XLSX, PDF, HTML, CSV és továbbiak), **500+ sort** dolgoz fel egy másodpercnél gyorsabban, és programozott vezérlést biztosít minden diagram elem felett – a színektől az adatcímkékig.

## Előfeltételek

Mielőtt belemerülnénk a kódba, győződjön meg róla, hogy a következő előfeltételek teljesülnek:

- Aspose.Cells for Java: Telepítenie kell az Aspose.Cells for Java‑t. Letöltheti az Aspose.Cells for Java kiadási oldaláról: [Aspose.Cells for Java releases](https://releases.aspose.com/cells/java/).
- Java fejlesztői környezet: Győződjön meg róla, hogy a Java telepítve van a rendszerén, és egy build eszköz (Maven/Gradle) készen áll.

Most pedig lépésről‑lépésre elkezdhetjük a vízárapály diagram létrehozását.

## Hogyan állítsuk be a diagram adat tartományát egy vízárapály diagramhoz Java‑ban
Töltsön be egy új munkafüzetet, töltse fel adatokka­l, adjon hozzá egy `Chart` objektumot, határozza meg a sorozat tartományát, majd mentse a fájlt. Ez a folyamat egyszerű: létrehoz egy munkafüzetet, kitölti a cellákat kategóriákkal és értékekkel, létrehoz egy diagramot, összekapcsolja az adat‑tartományokat, és exportálja a munkafüzetet. Az eredmény egy teljesen funkcionális vízárapály diagram, amely készen áll a jelentésekben vagy irányítópultokon való használatra.

### 1. lépés: Aspose.Cells importálása
A `com.aspose.cells` csomag tartalmazza az összes osztályt, amely az Excel manipulációhoz szükséges, beleértve a munkafüzet‑létrehozást, munkalap‑kezelést és diagram‑generálást.

### 2. lépés: munkafüzet és munkalap inicializálása
A **Workbook** egy Excel fájlt képvisel, a **Worksheet** pedig egyetlen lapot ebben a fájlban. Ezeknek az objektumoknak a létrehozása biztosítja a vásznat a nyers adatok és a diagram számára.

### 3. lépés: adatok bevitele
Az A oszlop a kategória címkéket, a B oszlop pedig a vízárapály numerikus értékeit tartalmazza. Ez a felépítés megfelel a pénzügyi elemzésekben gyakran használt nyereség‑ és veszteség‑folyamatnak.

### 4. lépés: vízárapály diagram létrehozása
A **Chart** objektum vizuális ábrát hoz létre; a típusának `ChartType.WATERFALL`‑ra állítása vízárapály diagramot eredményez. Használja az `add` metódust a sorozat adat‑tartományának beállításához (`"B2:B6"`), és kapcsolja a kategória‑tengelyt az `"A2:A6"`‑hoz.

### 5. lépés: munkafüzet mentése
A munkafüzet mentése a diagramot és az adatokat a megadott fájlformátumba írja. Hívja meg a `workbook.save("WaterfallChart.xlsx")`‑t XLSX fájl generálásához, vagy módosítsa a formátum‑paramétert PDF, CSV vagy HTML exportálásához.

## Gyakori problémák és megoldások

- **A diagram üresen jelenik meg** – Ellenőrizze, hogy az adat‑tartomány hivatkozások (`B2:B6` és `A2:A6`) megegyeznek a ténylegesen értékeket és kategóriákat tartalmazó cellákkal.  
- **A negatív értékek nem jelennek meg helyesen** – Győződjön meg róla, hogy a sorozat típusa `ChartType.WATERFALL`‑ra van állítva; más diagramtípusok másként kezelik a negatív értékeket.  
- **A fájl nem nyílik meg Excelben** – Használja a legújabb Aspose.Cells kiadást, és ellenőrizze, hogy a fájlkiterjesztés megegyezik a formátummal (`.xlsx` az Excelhez).

## Gyakran ismételt kérdések

### Hogyan testreszabhatom a vízárapály diagram megjelenését?
Módosíthatja a tulajdonságokat, például `Chart.getSeries().get(0).getFillFormat().setColor(Color.getRed())` a sávszínek változtatásához, engedélyezheti az adatcímkéket a `setShowDataLabels(true)`‑val, és a tengelycímeket a `getCategoryAxis().setTitle("Stage")`‑vel állíthatja be. Az Aspose.Cells API referencia teljes listát nyújt a testreszabható beállításokról.

### Létrehozhatok több vízárapály diagramot ugyanabban a munkalapban?
Igen. Az első diagram hozzáadása után ismételje meg a diagram‑létrehozási lépéseket egy másik adat‑tartománnyal és egy új `Chart` objektummal. Minden diagram független, és a lap bármely pontjára elhelyezhető.

### Az Aspose.Cells kompatibilis különböző Java fejlesztői környezetekkel?
Teljesen. A könyvtár működik Eclipse‑el, IntelliJ IDEA‑val, NetBeans‑szel, és bármely build rendszerrel, amely támogatja a Maven‑t vagy a Gradle‑t. Nem szükséges további plug‑in.

### Hozzáadhatok további adat sorozatokat a vízárapály diagramomhoz?
További sorozatokat adhat hozzá a `chart.getNSeries().add("C2:C6", true)` hívással, és minden sorozatot külön konfigurálhat. Ez lehetővé teszi több forgatókönyv oldal‑oldali összehasonlítását.

### Hol találok további forrásokat és példákat az Aspose.Cells for Java‑hoz?
Fedezze fel a teljes dokumentációt az Aspose.Cells Java API referenciában: [Aspose.Cells Java API reference](https://reference.aspose.com/cells/java/).

## GyIK

**Q: Hogyan állítom be a diagram adat‑tartományát egy pénzügyi vízárapály diagramhoz?**  
A: Használja a `add` metódust a diagram sorozatán, megadva a cellatartományt, amely az értékeket tartalmazza, például `"B2:B6"`.

**Q: Exportálhatom a munkafüzetet PDF‑be az XLSX helyett?**  
A: Igen, hívja meg a `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);`‑t PDF verzió generálásához.

**Q: Mi a teendő, ha több kategóriával szeretnék vízárapály diagramot létrehozni?**  
A: Bővítse a adat‑tartományt mind az érték‑oszlopban, mind a kategória‑oszlopban, majd ennek megfelelően frissítse az `add` és a `setCategoryData` hívásokat.

**Q: Van mód a pozitív és negatív sávok automatikus formázására?**  
A: Iteráljon a `Series` gyűjteményen, és állítsa be a `FillFormat` színt az egyes értékek előjelének megfelelően; az Aspose.Cells lehetővé teszi a feltételes formázás programozott alkalmazását.

**Q: Támogatja az Aspose.Cells a diagramok dinamikus adatfrissítését?**  
A: Igen. A cellaértékek módosítása után egyszerűen mentse újra a munkafüzetet – a diagram automatikusan tükrözi az új adatokat.

---

**Last Updated:** 2026-09-02  
**Tested with:** Aspose.Cells for Java (latest)  
**Author:** Aspose  









```java
import com.aspose.cells.*;
```

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

```java
workbook.save("WaterfallChart.xlsx");
```

## Kapcsolódó oktatóanyagok

- [Excel diagram adatcímkék testreszabása Aspose.Cells for Java használatával: lépésről‑lépésre útmutató](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Adatcímkék hozzáadása Excel diagramhoz Aspose.Cells Java‑val](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Hogyan hozzunk létre és exportáljunk diagramokat Java‑ban az Aspose.Cells segítségével: teljes útmutató](/cells/java/charts-graphs/aspose-cells-java-create-export-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}