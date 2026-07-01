---
category: general
date: 2026-06-30
description: Exportálja a diagramot képként, és tanulja meg, hogyan exportálja a diagramot,
  mentse az Excelt Word-be, konvertálja az Excelt Word-be, valamint konvertálja az
  XLSX-et DOCX-be néhány egyszerű lépésben.
draft: false
keywords:
- export chart as image
- how to export chart
- save excel as word
- convert excel to word
- convert xlsx to docx
language: hu
og_description: Exportálja a diagramot képként, és gyorsan konvertálja az Excelt Wordbe.
  Kövesse ezt az útmutatót az Excel Wordbe mentéséhez, a diagramok exportálásához
  és az XLSX DOCX formátumba konvertálásához.
og_title: Diagram exportálása képként – Lépésről lépésre Excel‑ról Word‑re konvertálás
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Export chart as image and learn how to export chart, save Excel as
    Word, convert Excel to Word, and convert XLSX to DOCX in a few easy steps.
  headline: Export Chart as Image – Complete Guide to Convert Excel to Word
  type: TechArticle
- description: Export chart as image and learn how to export chart, save Excel as
    Word, convert Excel to Word, and convert XLSX to DOCX in a few easy steps.
  name: Export Chart as Image – Complete Guide to Convert Excel to Word
  steps:
  - name: What if my workbook has multiple charts?
    text: You don’t need to change anything—setting `setExportChartAsImage(true)`
      applies to **all** charts in the workbook. If you only want specific charts
      as images, you’ll have to export them manually using `chart.toImage()` and then
      insert them into the Word file yourself.
  - name: Can I control the image format (PNG vs JPEG)?
    text: 'Aspose.Cells uses PNG by default for chart‑as‑image exports. To switch
      to JPEG, you can adjust the `ImageOrPrintOptions` before saving:'
  - name: Does this work with older Excel files (.xls)?
    text: Absolutely. The same code works for both `.xls` and `.xlsx`. Aspose.Cells
      auto‑detects the format, so you can **save Excel as Word** regardless of the
      source version.
  - name: How does this differ from “convert Excel to Word” with native Office interop?
    text: Native interop often requires a Windows machine with Office installed, and
      charts may lose fidelity. Using Aspose.Cells is platform‑agnostic, works on
      Linux/macOS, and preserves chart quality by rasterizing them.
  type: HowTo
tags:
- Excel
- Word
- Chart
- Java
- Aspose.Cells
title: Diagram exportálása képként – Teljes útmutató az Excel Word-be konvertálásához
url: /hu/java/excel-import-export/export-chart-as-image-complete-guide-to-convert-excel-to-wor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Diagram exportálása képként – Teljes útmutató az Excel Word-be konvertálásához

Valaha is elgondolkodtál, hogyan lehet egy diagramot képként exportálni egy Excel munkafüzetből, és közvetlenül egy Word dokumentumba helyezni? Nem vagy egyedül – a fejlesztők állandóan kérdezik: „Hogyan exportálhatok diagramot XLSX‑ből, és ágyazhatom be DOCX‑be minőségromlás nélkül?”  

A jó hír, hogy néhány Java kódsorral **exportálhatod a diagramot képként**, majd **elmentheted az Excelt Word‑ként** egy zökkenőmentes folyamatban. Ebben az útmutatóban végigvezetünk a teljes folyamaton, a munkafüzet betöltésétől a mentési beállítások konfigurálásáig, amelyek a diagramjaidat éles PNG‑kké alakítják egy DOCX fájlban.  

Érinteni fogjuk a kapcsolódó feladatokat is, mint a **convert Excel to Word**, **save Excel as Word**, és **convert XLSX to DOCX** – mindezt úgy, hogy a kód tiszta és futtatható marad. Nem felesleges részletek, csak egy gyakorlati megoldás, amit ma is be‑másolhatsz.

---

## Amire szükséged lesz

Mielőtt belemerülnénk, győződj meg róla, hogy a következőkkel rendelkezel:

- **Java Development Kit (JDK) 8+** – a kód bármely modern JDK‑n fut.
- **Aspose.Cells for Java** library (version 23.10 vagy újabb). Letöltheted a Maven Central‑ról vagy közvetlenül a JAR‑t.
- Egy **Excel fájl** (`charts.xlsx`), amely legalább egy exportálni kívánt diagramot tartalmaz.
- Egy **Java IDE** (IntelliJ IDEA, Eclipse vagy VS Code) – bármelyik megfelel.
- Alapvető ismeretek a Java‑ról és a Maven/Gradle‑ról (opcionális, de hasznos).

Ennyi. Nincs szükség extra pluginekre, COM interopra, csak tiszta Java.

## 1. lépés: Az Excel munkafüzet betöltése és a diagram megtalálása

Az első dolog, amit meg kell tennünk, hogy megnyissuk a diagramot tartalmazó munkafüzetet. Az Aspose.Cells ezt könnyedén megoldja – csak a fájl útvonalát kell megadni.

```java
// Step 1: Load the Excel workbook that contains the chart
Workbook workbook = new Workbook("YOUR_DIRECTORY/charts.xlsx");

// Grab the first worksheet (index 0) and its first chart (index 0)
Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
```

> **Miért fontos:** A munkafüzet betöltése hozzáférést biztosít a diagram objektumához, amelyet később az Aspose‑nek megmondunk, hogy képként rendereljen. Ha a munkafüzet több munkalapot vagy diagramot tartalmaz, módosíthatod a indexeket vagy ciklussal feldolgozhatod őket.

## 2. lépés: DOCX mentési beállítások konfigurálása a diagramok képként exportálásához

Az Aspose.Cells egy `DocxSaveOptions` osztályt biztosít, amely lehetővé teszi a konverzió viselkedésének szabályozását. A `setExportChartAsImage(true)` beállítása azt mondja a könyvtárnak, hogy minden diagramot raszterképpé alakítson, mielőtt a Word fájlba ágyazná.

```java
// Step 2: Create DOCX save options and enable chart‑as‑image export
DocxSaveOptions saveOptions = new DocxSaveOptions();
saveOptions.setExportChartAsImage(true); // This is the key line
```

> **Pro tipp:** Ha vektoros grafikát (EMF/WMF) részesítesz előnyben, kikapcsolhatod ezt a jelzőt, de a raszter képek általában konzisztensen jelennek meg a Word verziók között.

## 3. lépés: A munkafüzet mentése DOCX fájlként

Miután a beállítások készen vannak, egyszerűen mentjük a munkafüzetet. A könyvtár gondoskodik az összes munkalap, táblázat, és – a beállított jelzőnek köszönhetően – a diagramok képként történő konvertálásáról.

```java
// Step 3: Save the workbook as a DOCX file, applying the chart‑export option
workbook.save("YOUR_DIRECTORY/charts.docx", saveOptions);
```

> **Mi lesz az eredmény:** Egy `charts.docx` fájl, ahol az eredeti Excel diagram magas felbontású PNG‑ként (vagy JPEG‑ként, a beállításoktól függően) jelenik meg a Word dokumentumban. Nyisd meg Microsoft Word‑ben, hogy lásd az eredményt.

## 4. lépés: A kimenet ellenőrzése (opcionális, de ajánlott)

Mindig jó ötlet programozottan ellenőrizni, hogy a konverzió sikeres volt-e, különösen kötegelt folyamatok automatizálásakor.

```java
// Optional: Verify that the DOCX file exists and is not empty
File docxFile = new File("YOUR_DIRECTORY/charts.docx");
if (docxFile.exists() && docxFile.length() > 0) {
    System.out.println("Success! DOCX created with chart as image.");
} else {
    System.err.println("Conversion failed – check the source file and options.");
}
```

Ha futtatod a kódrészletet és látod a sikerüzenetet, akkor hatékonyan **convert XLSX to DOCX**-t hajtottál végre, miközben a diagramok vizuális elemei képként maradtak meg.

## Teljes működő példa

Az alábbiakban a teljes, azonnal futtatható Java program található, amely összevonja az összes lépést. Csak cseréld le a `YOUR_DIRECTORY`‑t a géped tényleges útvonalára.

```java
import com.aspose.cells.*;

import java.io.File;

public class ExportChartAsImageDemo {
    public static void main(String[] args) throws Exception {
        // Load the Excel workbook containing the chart
        Workbook workbook = new Workbook("YOUR_DIRECTORY/charts.xlsx");

        // Access the first worksheet and its first chart
        Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
        if (chart == null) {
            System.err.println("No chart found in the first worksheet.");
            return;
        }

        // Configure DOCX save options to export charts as images
        DocxSaveOptions saveOptions = new DocxSaveOptions();
        saveOptions.setExportChartAsImage(true);   // Export chart as image

        // Save as DOCX
        String outputPath = "YOUR_DIRECTORY/charts.docx";
        workbook.save(outputPath, saveOptions);

        // Verify the output file
        File outFile = new File(outputPath);
        if (outFile.exists() && outFile.length() > 0) {
            System.out.println("File saved successfully: " + outputPath);
        } else {
            System.err.println("Failed to create the DOCX file.");
        }
    }
}
```

**Várható kimenet a program futtatásakor:**

```
File saved successfully: YOUR_DIRECTORY/charts.docx
```

Nyisd meg a `charts.docx`‑t Microsoft Word‑ben, és látni fogod, hogy a diagram tiszta képként jelenik meg, pontosan ott, ahol az eredeti Excel diagram volt.

## Gyakori kérdések és szélhelyzetek

### Mi van, ha a munkafüzet több diagramot tartalmaz?

Nem kell semmit módosítanod – a `setExportChartAsImage(true)` beállítás **minden** diagramra érvényes a munkafüzetben. Ha csak bizonyos diagramokat szeretnél képként, akkor manuálisan kell exportálnod őket a `chart.toImage()` segítségével, majd saját magadnak be kell illesztened a Word fájlba.

### Vezérelhetem a képformátumot (PNG vs JPEG)?

Az Aspose.Cells alapértelmezés szerint PNG‑t használ a diagram‑képként exportáláshoz. JPEG‑re váltáshoz módosíthatod a `ImageOrPrintOptions`‑t a mentés előtt:

```java
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.getJpeg());
saveOptions.setImageOrPrintOptions(imgOptions);
```

### Működik ez régebbi Excel fájlokkal (.xls)?

Természetesen. Ugyanaz a kód működik mind `.xls`, mind `.xlsx` esetén. Az Aspose.Cells automatikusan felismeri a formátumot, így **save Excel as Word**-t végezhetsz a forrás verziójától függetlenül.

### Miben különbözik a natív Office interop‑os „convert Excel to Word” megoldástól?

A natív interop gyakran Windows gépet igényel, ahol az Office telepítve van, és a diagramok minősége romolhat. Az Aspose.Cells platform‑független, Linux/macOS rendszereken is működik, és a diagramok minőségét raszterképpé alakítva őrzi meg.

## Tippek a termelés‑kész megvalósításhoz

- **Batch processing:** Egy könyvtárban lévő XLSX fájlokon iterálj, ugyanazt a `DocxSaveOptions`‑t alkalmazva. A konverziót try‑catch blokkba tedd, hogy a sérült fájlokat elegánsan kezeld.
- **Memory management:** Nagyon nagy munkafüzetek esetén hívd meg a `workbook.dispose()`‑t a mentés után, hogy felszabadítsd a natív erőforrásokat.
- **Customization:** Beállíthatod a `saveOptions.setPreserveCellFormatting(true)`‑t is, ha a cellastílusokat meg akarod őrizni a konvertálás során.
- **Logging:** Integrálj egy naplózási keretrendszert (SLF4J, Log4j), hogy rögzítsd a konverziós statisztikákat – hasznos audit nyomvonalakhoz.

## Összegzés

Most már egy szilárd, vég‑a‑végig megoldással rendelkezel, amely **export chart as image**, **save Excel as Word**, és **convert XLSX to DOCX** csak néhány Java utasítással. A fő tanulság, hogy az Aspose.Cells `DocxSaveOptions` lehetővé teszi a diagramkezelés egyszerűségét – nincs manuális képkinyerés, nincs COM interop, és teljes platform‑független támogatás.  

Nyugodtan kísérletezz: próbálj meg több munkalapot exportálni, állítsd be a kép felbontását, vagy kombináld ezt a megközelítést más Aspose könyvtárakkal (például Aspose.Words) még gazdagabb Word dokumentumokhoz. A lehetőségek határtalanok, ha tudod, hogyan exportáld helyesen a diagramot.  

További kérdéseid vannak az Excel fájlok konvertálásával, képek beágyazásával vagy a teljesítmény optimalizálásával kapcsolatban? Hagyj egy megjegyzést alább, és jó kódolást!

## Mit érdemes legközelebb megtanulni?

Az alábbi útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljesen működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Excel diagram képként konvertálása Aspose.Cells .NET‑tel](/cells/english/net/charts-graphs/convert-excel-chart-image-aspose-cells-dotnet/)
- [Hogyan hozzunk létre Excel diagramot trendvonallal, és exportáljuk képként az Aspose.Cells for Java segítségével](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Excel kördiagram képként konvertálása Aspose.Cells .NET‑tel: lépésről‑lépésre útmutató](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}