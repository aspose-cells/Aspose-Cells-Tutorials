---
category: general
date: 2026-10-07
description: Tanulja meg, hogyan hozhat létre PNG-t egy tartományból, és exportálhatja
  az adatokat PNG-ként Java-ban. Ez az útmutató megmutatja, hogyan menthet Excel-tartomány
  képet az Aspose.Cells segítségével.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create png from range
- export data as png
- save excel range image
- convert worksheet to png
- save cells as png
language: hu
lastmod: 2026-10-07
og_description: Készíts PNG-t egy tartományból Java-ban, és exportáld az adatokat
  PNG formátumban az Aspose.Cells segítségével. Kövesd ezt a teljes útmutatót, hogy
  azonnal elmentsd az Excel-tartomány képét.
og_image_alt: Screenshot of Java code that creates a PNG from an Excel range
og_title: PNG létrehozása tartományból Java-ban – lépésről lépésre Aspose.Cells útmutató
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  headline: How to create PNG from range in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  name: How to create PNG from range in Java with Aspose.Cells
  steps:
  - name: Maven dependency
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-cells</artifactId>
      <version>23.12</version> </dependency> ```'
  - name: Expected output
    text: '* A file named `PivotImage.png` located in `YOUR_DIRECTORY`. * The image
      shows the exact layout, fonts, colors, and borders from the selected range.
      * If the source range contains a pivot table, the rendered image includes the
      same styling and calculated values as displayed in Excel.'
  - name: Exporting a non‑contiguous range
    text: Aspose.Cells does not render disjoint ranges in a single image. To export
      multiple areas, create separate images for each range and combine them later
      with an image‑processing library (e.g., ImageIO).
  - name: Saving a large worksheet as PNG
    text: 'Rendering an entire sheet that spans thousands of rows can consume significant
      memory. Mitigate this by:'
  - name: Preserving cell formulas
    text: A PNG image is a raster format; formulas are not retained. If downstream
      consumers need the raw data, also export the range as CSV or JSON using `Range.exportDataTable()`.
  - name: Next steps
    text: '* Experiment with different `Resolution` values to balance quality and
      file size. * Use `ImageOrPrintOptions.setTransparent(true)` if you need a PNG
      with a transparent background. * Combine multiple range images into a single
      PDF using `PdfSaveOptions` for multi‑page reports. * Explore exporting to '
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Hogyan készítsünk PNG-t egy tartományból Java-ban az Aspose.Cells segítségével
url: /hu/java/images-shapes/how-to-create-png-from-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan hozhatunk létre PNG-t tartományból Java-ban az Aspose.Cells segítségével

Ha **PNG-t szeretne létrehozni egy tartományból** egy Excel munkafüzetben, ez a bemutató pontosan megmutatja, hogyan teheti meg. A útmutató végére képes lesz **adatok PNG-ként exportálására**, egy Excel tartomány képének mentésére, és a fájl újrahasználatára jelentésekben vagy weboldalakon.

Megtekint egy teljes, futtatható Java programot, amely betölti a munkafüzetet, kiválasztja a kívánt cellákat, PNG-ként rendereli őket, és elmenti az eredményt a lemezre. Külső eszközök nem szükségesek – az Aspose.Cells mindent belsőleg kezel.

## Amire ez a bemutató kitér

* Előkövetelmények és Maven beállítás az Aspose.Cells-hez
* Munkafüzet betöltése, amely tartalmaz pivot táblát vagy bármilyen adat‑tartományt
* A pontos cellatartomány meghatározása, amelyet konvertálni szeretne
* Képkimeneti beállítások konfigurálása PNG‑hez
* A tartomány renderelése és a PNG fájl mentése
* Gyakori buktatók és tippek a magas minőségű képekhez

A lépések elvégzése után képes lesz **munkalap PNG‑re konvertálására** bármely tartomány esetén, legyen az egyszerű táblázat vagy összetett pivot diagram.

## Előkövetelmények

* Java 17 vagy újabb (a kód JDK 11+ verzióval is fordítható)
* Maven 3.6+ (vagy Gradle, ha azt részesíti előnyben)
* Aspose.Cells for Java 23.12 vagy újabb – adja hozzá az alább látható függőséget
* Egy meglévő Excel fájl (`PivotWithStyle.xlsx`), amely tartalmazza a rögzíteni kívánt tartományt

> **Pro tipp:** Ha nincs licence, kérhet ideiglenes értékelő kulcsot az Aspose‑tól. A könyvtár értékelő módban működik további konfiguráció nélkül.

### Maven függőség

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

## 1. lépés: A munkafüzet betöltése, amely a céltartományt tartalmazza

Az első művelet az Excel fájl megnyitása. Az Aspose.Cells a fájlt memóriába olvassa be, Microsoft Office nélkül.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the data you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");
```

*Miért fontos*: A munkafüzet betöltése hozzáférést biztosít a munkalapokhoz, cellákhoz és a nyomtatási beállításokhoz, amelyek a rendereléshez szükségesek.

## 2. lépés: A tartományt tartalmazó munkalap elérése

A legtöbb munkafüzetnek van egy alapértelmezett lapja a 0‑s indexen, de használhatja a lap nevét is.

```java
        // Retrieve the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Ha az adatai egy másik lapon vannak, cserélje le a `0`‑t a megfelelő indexre, vagy használja a `workbook.getWorksheets().get("SheetName")` metódust.

## 3. lépés: A konvertálni kívánt cellatartomány meghatározása

Bármely téglalap alakú területet megadhat A1 jelöléssel. Ebben a példában a `A1:D15` tartományt rögzítjük, amely lehet egy pivot tábla vagy egy szokásos adatblokk.

```java
        // Create a range object for cells A1:D15
        Range pivotRange = worksheet.getCells().createRange("A1:D15");
```

*Szélhelyzet*: Ha a tartomány egyes cellái egyesülnek (merged cells), az Aspose.Cells automatikusan kiterjeszti a képet, hogy magában foglalja az egyesült területet.

## 4. lépés: PNG képbeállítások előkészítése

Az `ImageOrPrintOptions` lehetővé teszi a formátum, felbontás és egyéb renderelési részletek szabályozását. A mentési formátum PNG‑re állítása biztosítja a veszteségmentes minőséget.

```java
        // Configure image options – we want a PNG file
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        // Optional: increase DPI for sharper output (default is 96)
        imageOptions.setImageFormat(ImageFormat.getPng());
        imageOptions.setResolution(150); // 150 DPI for clearer text
```

A DPI növelése hasznos, ha a forráscellák kis betűket vagy részletes diagramokat tartalmaznak.

## 5. lépés: A renderelési terület korlátozása a kiválasztott tartományra

A tartományt nyomtatási területként beállítva az Aspose.Cells csak ezeket a cellákat rendereli, a lap többi részét figyelmen kívül hagyva.

```java
        // Set the print area so only the defined range is rendered
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());
```

Ha kihagyja ezt a lépést, az egész munkalap rasterizálódik, ami memóriafogyasztást növel és nagyobb képet eredményez.

## 6. lépés: A tartomány renderelése és a kép hozzáadása a munkalaphoz (opcionális)

Ha a generált PNG‑t vissza szeretné ágyazni a munkafüzetbe (például előnézethez), hozzáadhatja képként. Ez a lépés opcionális, ha csak exportálni szeretné a képet.

```java
        // Add the rendered image back to the worksheet at cell (0,0) – optional
        worksheet.getPictures().add(0, 0, imageOptions);
```

*Miért lehet erre szükség*: Egyes munkafolyamatok megkövetelik, hogy a kép a munkafüzet része legyen a terjesztés előtt, például nyomtatható jelentés készítésekor, amely natív cellákat és képeket egyaránt tartalmaz.

## 7. lépés: A PNG fájl mentése a lemezre

Végül írja a képet egy fájlba. A `save` metódus a `imageOptions`‑ban megadott formátumot veszi figyelembe.

```java
        // Save the rendered PNG image to the specified path
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

A program befejezésekor a `PivotImage.png` egy pixel‑pontos pillanatképet tartalmaz a `A1:D15` cellákról.

### Várt kimenet

* Egy `PivotImage.png` nevű fájl a `YOUR_DIRECTORY` könyvtárban.
* A kép pontosan mutatja a kiválasztott tartomány elrendezését, betűtípusait, színeit és szegélyeit.
* Ha a forrástartomány pivot táblát tartalmaz, a renderelt kép ugyanazt a stílust és a számított értékeket jeleníti meg, mint az Excelben.

## Gyakori helyzetek kezelése

### Nem összefüggő tartomány exportálása

Az Aspose.Cells nem tud széttagolt tartományokat egyetlen képen megjeleníteni. Több terület exportálásához hozzon létre külön képeket minden tartományhoz, majd később egy képfeldolgozó könyvtárral (pl. ImageIO) egyesítse őket.

```java
Range first = worksheet.getCells().createRange("A1:B10");
Range second = worksheet.getCells().createRange("D1:E10");
// Render each range individually using the same ImageOrPrintOptions
```

### Nagy munkalap mentése PNG‑ként

Egy teljes lap, amely több ezer sort tartalmaz, jelentős memóriát igényelhet. Ennek mérséklésére:

* Csökkentse a DPI‑t (`imageOptions.setResolution(72)`) a kisebb fájl érdekében.
* Használja a `setPageCount`‑t a renderelt oldalak számának korlátozásához.
* Exportáljon egy nyomtatható oldalt egyszerre a `worksheet.getPageSetup().setPrintArea(...)` segítségével.

### Cellaképletek megőrzése

A PNG egy raszteres formátum; a képletek nem maradnak meg. Ha a downstream felhasználóknak a nyers adat szükséges, exportálja a tartományt CSV‑ként vagy JSON‑ként a `Range.exportDataTable()` metódussal.

## Teljes, futtatható példa

Az alábbiakban a teljes Java osztály látható, amelyet egyszerűen másolhat be az IDE‑jébe. Cserélje le a `YOUR_DIRECTORY`‑t egy abszolút vagy relatív útvonalra a gépén.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the workbook containing the data
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");

        // 2️⃣ Access the first worksheet (adjust index or name as needed)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Define the exact cell range you want to convert (A1:D15 in this case)
        Range pivotRange = worksheet.getCells().createRange("A1:D15");

        // 4️⃣ Prepare PNG image options – set format and optional resolution
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        imageOptions.setResolution(150); // sharper output

        // 5️⃣ Restrict rendering to the selected range
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());

        // 6️⃣ (Optional) Add the rendered image back to the worksheet for preview
        worksheet.getPictures().add(0, 0, imageOptions);

        // 7️⃣ Save the PNG file – this creates the final image on disk
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Futtassa a programot `mvn compile exec:java` (vagy a kedvenc build eszközével). A futtatás után nyissa meg a `PivotImage.png` fájlt a végeredmény ellenőrzéséhez.

## Összegzés

Most már tudja, hogyan **hozzon létre PNG‑t tartományból** Java‑ban az Aspose.Cells használatával, hatékonyan **exportálja az adatokat PNG‑ként**, és **mentse el az Excel tartomány képet** bármilyen jelentéshez vagy megosztási forgatókönyvhöz. A lépések – a munkafüzet betöltése, a tartomány meghatározása, a képbeállítások konfigurálása, a nyomtatási terület beállítása és a fájl mentése – lefedik a teljes munkafolyamatot a **munkalap PNG‑re konvertálásához** és a **cellák PNG‑ként mentéséhez**.

### Következő lépések

* Kísérletezzen különböző `Resolution` értékekkel a minőség és a fájlméret egyensúlyozásához.
* Használja a `ImageOrPrintOptions.setTransparent(true)`‑t, ha átlátszó háttérrel rendelkező PNG‑ra van szüksége.
* Több tartomány képet egyetlen PDF‑be kombinálhat a `PdfSaveOptions` segítségével többoldalas jelentésekhez.
* Fedezze fel a többi raszteres formátum exportálását (JPEG, BMP) a `setSaveFormat` módosításával.

Nyugodtan alkalmazza ezt a mintát diagramokhoz, táblázatokhoz vagy akár teljes munkalapokhoz is. Boldog kódolást!


## Mit érdemes még megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket és lépésről‑lépésre magyarázatokat tartalmaz, hogy segítsen további API‑funkciók elsajátításában és alternatív megvalósítási megközelítések felfedezésében saját projektjeiben.

- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Convert Excel to PNG Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/workbook-operations/convert-excel-to-png-aspose-cells-java/)
- [Create Union Range in Excel using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/range-management/create-union-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}