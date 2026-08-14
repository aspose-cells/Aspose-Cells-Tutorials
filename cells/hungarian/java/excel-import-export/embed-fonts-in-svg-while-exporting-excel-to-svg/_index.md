---
category: general
date: 2026-08-14
description: Betűtípusok beágyazása SVG-be az Excel SVG formátumba exportálásakor
  az Aspose.Cells használatával. Tanulja meg, hogyan állítsa be a nyomtatási területet,
  a nyomtatási beállításokat, és hogyan használja a WRAPCOLS függvényt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in svg
- export excel to svg
- set print area
- set print options
- use wrapcols function
language: hu
lastmod: 2026-08-14
og_description: Betűk beágyazása SVG-be Excel SVG exportálásakor az Aspose.Cells használatával.
  Ez az útmutató megmutatja, hogyan állítsa be a nyomtatási területet, konfigurálja
  a nyomtatási beállításokat, és alkalmazza a WRAPCOLS függvényt.
og_image_alt: Screenshot of Java code exporting an Excel sheet to SVG with embedded
  fonts
og_title: Betűtípusok beágyazása SVG-be Excel SVG-be exportálásakor – lépésről lépésre
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  headline: Embed fonts in SVG while exporting Excel to SVG
  type: TechArticle
- description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  name: Embed fonts in SVG while exporting Excel to SVG
  steps:
  - name: Run the program.
    text: Run the program.
  - name: Open `output.svg` in a web browser.
    text: Open `output.svg` in a web browser.
  - name: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
    text: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
  - name: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
    text: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
title: Betűk beágyazása SVG-be Excel SVG exportálásakor
url: /hu/java/excel-import-export/embed-fonts-in-svg-while-exporting-excel-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Betűkészletek beágyazása SVG-be Excel SVG exportálásakor

Ha **betűkészleteket kell beágyazni SVG-be Excel SVG exportálásakor**, ez a bemutató pontosan megmutatja, hogyan teheted ezt meg az Aspose.Cells for Java segítségével. Emellett bemutatjuk, hogyan **állíts be nyomtatási területet**, **állíts be nyomtatási beállításokat**, és **használd a WRAPCOLS függvényt** az adatok formázásához anélkül, hogy elveszítenéd az elrendezést.

Egy teljes, futtatható példán keresztül vezetünk végig, amely betölti a meglévő munkafüzetet, alkalmazza a `WRAPCOLS` képletet, konfigurálja az SVG-specifikus képbeállításokat, definiálja a nyomtatási területet, és végül SVG‑ként menti a fájlt beágyazott betűkészletekkel. Külső dokumentációra nincs szükség – csak másold a kódot, futtasd, és ellenőrizd a kapott SVG‑t.

## Betűkészletek beágyazása SVG‑be – ImageOrPrintOptions konfigurálása

A betűkészletek beágyazása biztosítja, hogy az SVG pontosan úgy jelenjen meg, ahogy az Excelben látható, még olyan gépeken is, ahol az eredeti betűtípusok nincsenek telepítve.

```java
// Create ImageOrPrintOptions for SVG output
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);          // Target format
imgOptions.setEmbedFonts(true);                     // <-- embed fonts in SVG
imgOptions.setFontVariationSelectors(true);        // Preserve variation selectors
```

*Miért fontos*: Amikor a `setEmbedFonts(true)` be van kapcsolva, az Aspose.Cells a betűkészlet adatokat közvetlenül a SVG `<defs>` szekciójába írja. Az eredmény egy önálló fájl, amely minden böngészőben és platformon azonosan néz ki.

## Excel exportálása SVG‑be – teljes munkafolyamat

Az alábbi lépések bemutatják a teljes folyamatot a munkafüzet betöltésétől az SVG fájl mentéséig.

```java
// Step 1: Load a workbook and access the first worksheet
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = workbook.getWorksheets().get(0);

// Step 2: Apply the WRAPCOLS formula to cell A1
Cell cell = ws.getCells().get("A1");
cell.setFormula("=WRAPCOLS(A2:A10,3)");

// Step 3: Configure image options (see previous section)
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);
imgOptions.setEmbedFonts(true);
imgOptions.setFontVariationSelectors(true);

// Step 4: Define the print area and assign the image options
ws.getPageSetup().setPrintArea("A1:H30");           // <-- set print area
ws.getPageSetup().setPrintOptions(imgOptions);     // <-- set print options

// Step 5: Save the worksheet as an SVG file
ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);
```

**Várt kimenet**: az `output.svg` megjelenik a `YOUR_DIRECTORY` könyvtárban. A böngészőben megnyitva a munkalap minden betűkészlettel beágyazva, az adatok három oszlopba vannak tördelve a `WRAPCOLS`-nek köszönhetően, és csak az `A1:H30` tartományban lévő cellák láthatók.

## Nyomtatási terület beállítása a munkalaphoz

A nyomtatási terület definiálása korlátozza az exportált SVG‑t egy adott tartományra, ami csökkenti a fájlméretet és a nézőt a releváns adatokra fókuszálja.

```java
// Define a rectangular region that will be exported
ws.getPageSetup().setPrintArea("A1:H30");   // you can change the range as needed
```

*Tippek*: A tartomány az Excel A1 jelölését követi. Ha dinamikus tartományra van szükséged, programozottan kiszámíthatod a `ws.getCells().getMaxDisplayRange()` segítségével.

## Nyomtatási beállítások megadása SVG kimenethez

A nyomtatási beállítások szabályozzák, hogyan alakítja az Aspose.Cells a munkalapot képpé. A betűkészletek beágyazása mellett beállíthatod a felbontást, a méretezést és az oldalelrendezést is.

```java
// Assign the previously configured ImageOrPrintOptions
ws.getPageSetup().setPrintOptions(imgOptions);
```

*Miért érdemes nyomtatási beállításokat megadni*: Kifejezett beállítások nélkül az Aspose.Cells alapértelmezéseket használ, amelyek elhagyhatják a betűkészlet beágyazását vagy nem kívánt méretezési tényezőt alkalmazhatnak, ami elmosódott vagy hibásan formázott SVG‑ket eredményez.

## WRAPCOLS függvény használata oszlopadatok tördeléséhez

A `WRAPCOLS` egy Excel képlet, amely egy függőleges tartományt egy megadott számú oszlopra oszt el. Hasznos, ha egy hosszú listát kompakt rácsban szeretnél megjeleníteni.

```java
// Insert the WRAPCOLS formula into cell A1
cell.setFormula("=WRAPCOLS(A2:A10,3)");
```

Amikor a munkafüzetet mentjük, az Aspose.Cells kiértékeli a képletet, és a definiált nyomtatási területen háromoszlopos elrendezést hoz létre. Ez a technika bármilyen méretű tartományra alkalmazható – csak a második argumentumot állítsd a kívánt oszlopszámra.

## Teljes futtatható példa

Az alábbiakban a teljes Java program látható, amelyet bármely IDE‑be beilleszthetsz. Győződj meg róla, hogy az Aspose.Cells for Java könyvtár a classpath‑on van.

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.getWorksheets().get(0);

        // Apply WRAPCOLS to reorganize data
        Cell wrapCell = ws.getCells().get("A1");
        wrapCell.setFormula("=WRAPCOLS(A2:A10,3)");

        // Configure SVG options with embedded fonts
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.SVG);
        imgOptions.setEmbedFonts(true);
        imgOptions.setFontVariationSelectors(true);

        // Set the region that will appear in the SVG
        ws.getPageSetup().setPrintArea("A1:H30");

        // Attach the image options to the worksheet
        ws.getPageSetup().setPrintOptions(imgOptions);

        // Export the worksheet as an SVG file
        ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);

        System.out.println("SVG exported successfully with embedded fonts.");
    }
}
```

**Ellenőrzési lépések**

1. Futtasd a programot.  
2. Nyisd meg az `output.svg`‑t egy webböngészőben.  
3. Ellenőrizd, hogy a szöveg ugyanazt a betűtípust használja, mint az eredeti Excel‑fájl (a betűkészletek be vannak ágyazva).  
4. Győződj meg arról, hogy csak az `A1:H30` tartományban lévő cellák jelennek meg, és hogy az `A2:A10` adatok három oszlopban vannak megjelenítve.

## Gyakori hibák és elkerülésük módja

| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| A betűkészletek hiányoznak az SVG-ben | `setEmbedFonts(false)` vagy a betűkészlet fájl nem érhető el | Győződj meg róla, hogy `setEmbedFonts(true)` van beállítva, és a betűkészlet telepítve van a kódot futtató gépen |
| A WRAPCOLS nem értékelődik | A számítási motor le van tiltva | Hívd meg a `workbook.calculateFormula()`‑t exportálás előtt, vagy engedd, hogy az Aspose.Cells a mentés során értékelje |
| Az exportált SVG üres | A nyomtatási terület nem tartalmaz adatot | Ellenőrizd a `setPrintArea`‑nek átadott tartományt |
| Az SVG fájl hatalmas | Nincs alkalmazva méretezés, nagy képfelbontás | Állítsd be a `imgOptions.setResolution(96)`‑t vagy hasonlót a DPI szabályozásához |

## Pro tipp: ImageOrPrintOptions újrahasználata több munkalaphoz

Ha a munkafüzet több olyan lapot tartalmaz, amelyeknek azonos SVG beállításokra van szükségük, hozz létre egyetlen `ImageOrPrintOptions` példányt, és rendeld hozzá minden munkalap `PageSetup`‑jához. Ez csökkenti a memóriahasználatot és garantálja a betűkészlet beágyazásának konzisztenciáját az összes exportált fájlban.

```java
ImageOrPrintOptions sharedOptions = new ImageOrPrintOptions();
sharedOptions.setImageFormat(ImageFormat.SVG);
sharedOptions.setEmbedFonts(true);
sharedOptions.setFontVariationSelectors(true);

for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    sheet.getPageSetup().setPrintOptions(sharedOptions);
    sheet.getPageSetup().setPrintArea("A1:H30");
    sheet.getPageSetup().save("YOUR_DIRECTORY/sheet" + i + ".svg", SaveFormat.SVG);
}
```

## Következő lépések

* **Exportálás más vektorfájl formátumokba** – Cseréld a `ImageFormat.SVG`‑t `ImageFormat.PDF`‑re a magas minőségű PDF‑ekhez.  
* **Kötegelt feldolgozás** – Iterálj egy `.xlsx` fájlokból álló mappán, és generálj SVG‑ket automatikusan.  
* **Egyedi betűkészlet kezelése** – Használd a `FontSettings`‑et, hogy betűkészleteket tölts be egy adott könyvtárból, ha a rendszer betűkészletei nem elegendőek.  

Az **betűkészletek beágyazása SVG‑be**, **excel exportálása SVG‑be**, **nyomtatási terület beállítása**, **nyomtatási beállítások megadása** és a **WRAPCOLS függvény használata** elsajátításával automatizálhatod a magas hűségű SVG generálást jelentések, műszerfalak és webes vizualizációk számára közvetlenül az Excel‑adatokból. Boldog kódolást!

## Mit érdemes legközelebb megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Hogyan állíts be nyomtatási területet Excelben az Aspose.Cells for .NET használatával](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Nyomtatási terület beállítása Excelben Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Nyomtatási terület beállítása Excelben Aspose Cells Net](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}