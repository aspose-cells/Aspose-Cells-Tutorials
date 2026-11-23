---
category: general
date: 2026-11-22
description: Tanulja meg, hogyan hozhat létre SVG-t Excelből az Aspose.Cells for Java
  segítségével. Exportálja az Excelt SVG formátumba, mentse a munkafüzetet SVG-ként,
  és tekintse meg a teljes kódrészletet.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create svg from excel
- export excel to svg
- how to export excel as svg
- save excel file as svg
- save workbook as svg
language: hu
lastmod: 2026-11-22
og_description: SVG létrehozása Excelből az Aspose.Cells for Java használatával. Ez
  az útmutató bemutatja, hogyan exportálhatja az Excelt SVG formátumba, hogyan mentheti
  a munkafüzetet SVG-ként, és egy teljesen futtatható példát is tartalmaz.
og_image_alt: Screenshot showing an Excel worksheet exported as an SVG file
og_title: SVG létrehozása Excelből Java-val – teljes export útmutató
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to create SVG from Excel using Aspose.Cells for Java. Export
    Excel to SVG, save workbook as SVG, and see full code example.
  headline: How to create SVG from Excel with Java – step‑by‑step guide
  type: TechArticle
tags:
- Excel
- SVG
- Java
- Aspose.Cells
- Export
title: Hogyan hozhatunk létre SVG-t Excelből Java-val – lépésről lépésre útmutató
url: /hu/java/excel-import-export/how-to-create-svg-from-excel-with-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan hozzunk létre SVG-t Excelből Java-val – lépésről‑lépésre útmutató

Ha **SVG-t kell létrehozni Excelből**, ez a tutorial pontosan megmutatja, hogyan kell ezt megtenni. Megtanulja, hogyan **exportálja az Excelt SVG-be**, hogyan mentse a munkafüzetet SVG fájlként, és hogyan ellenőrizze az eredményt—mindezt egyetlen, önálló Java programmal.

A táblázat adatok skálázható vektorgrafikaként való exportálása akkor hasznos, ha éles diagramokra van szükség weboldalakhoz, nyomtatható ábrákhoz vagy nagy felbontású bélyegképekhez. Az útmutató mindent lefed, amire szüksége van, a projekt beállításától a szélsőséges esetek kezeléséig, így azonnal elkezdheti használni a megoldást.

## Amire szüksége lesz

* Java Development Kit (JDK) 8 vagy újabb  
* Maven vagy Gradle a függőségkezeléshez (a példában Maven-t használunk)  
* Érvényes licenc a **Aspose.Cells for Java**-hoz (a könyvtár ingyenes próbaverziót kínál)  
* Egy Excel fájl (`sample.xlsx`), amely a konvertálni kívánt adatokat tartalmazza  

Ezek az előfeltételek biztosítják, hogy a kód fordítható és futtatható legyen további konfiguráció nélkül.

## 1. lépés: Maven projekt beállítása és Aspose.Cells hozzáadása

Hozzon létre egy új Maven projektet, vagy adja hozzá a következő függőséget a meglévő `pom.xml`-hez:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

A függőség hozzáadása letölti a **Aspose.Cells** könyvtárat, amely biztosítja a `ImageOrPrintOptions` osztályt, amelyet a **munkafüzet SVG-ként való mentéséhez** használnak. A Maven automatikusan feloldja a tranzitív függőségeket, így nincs szükség további JAR fájlokra.

> **Pro tipp:** Ha Gradlet használ, az ekvivalens bejegyzés:  
> `implementation 'com.aspose:aspose-cells:23.12'`.

## 2. lépés: Az Excel munkafüzet betöltése

Az első kódrészlet létrehoz egy `Workbook` példányt, amely a konvertálni kívánt Excel fájlt képviseli. Cserélje le a `"sample.xlsx"`-t a forrásfájl elérési útjára.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.LoadOptions;

public class ExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Load the Excel workbook from disk
        LoadOptions loadOptions = new LoadOptions();
        Workbook workbook = new Workbook("sample.xlsx", loadOptions);
        // Continue with export steps...
    }
}
```

A munkafüzet betöltése elengedhetetlen, mivel a **excel exportálása SVG-be** folyamat egy memóriában lévő táblázat-reprezentáción alapul. A `LoadOptions` objektum lehetővé teszi a fájl beolvasásának szabályozását, de az alapértelmezett beállítások a legtöbb esetben megfelelőek.

## 3. lépés: `ImageOrPrintOptions` konfigurálása SVG kimenethez

`ImageOrPrintOptions` megmondja az Aspose.Cells-nek, milyen formátumot kell előállítania. A `SaveFormat.SVG` beállítása azt utasítja a könyvtárat, hogy skálázható vektorgrafikát (SVG) generáljon raszteres képek helyett.

```java
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.SaveFormat;

ImageOrPrintOptions options = new ImageOrPrintOptions();
options.setSaveFormat(SaveFormat.SVG);   // Export Excel as SVG
options.setOnePagePerSheet(true);        // Optional: one SVG per sheet
```

A `setOnePagePerSheet(true)` jelző biztosítja, hogy minden munkalap egyetlen SVG fájlként legyen mentve, ami a leggyakoribb követelmény, amikor **excel fájlt ment SVG-ként** a webes közzétételhez.

## 4. lépés: A munkafüzet (vagy egyetlen munkalap) mentése SVG-ként

Exportálhatja az egész munkafüzetet vagy csak egy adott munkalapot. A következő példa az első munkalapot menti egy `output.svg` nevű SVG fájlba.

```java
import com.aspose.cells.Worksheet;
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.SheetRender;

// Choose the first worksheet (index 0)
Worksheet sheet = workbook.getWorksheets().get(0);

// Render the worksheet to SVG using the configured options
SheetRender render = new SheetRender(sheet, options);
render.toImage(0, "output.svg");   // Saves as SVG
```

Ha inkább **munkafüzetet ment SVG-ként** (minden munkalap egy SVG-ben) szeretné, használja a `workbook.save("output.svg", options);` hívást a `SheetRender` helyett. A könyvtár automatikusan egyetlen SVG dokumentummá fűzi össze a munkalapokat.

## 5. lépés: A generált SVG fájl ellenőrzése

A program befejezése után a projekt munkakönyvtárában meg kell jelennie az `output.svg` fájlnak. Nyissa meg egy webböngészőben vagy egy SVG‑t támogató szerkesztőben, hogy megerősítse, a vizuális elrendezés megegyezik az eredeti Excel munkalappal.

```text
✅ SVG file created: output.svg
```

Ha az SVG üresnek tűnik, ellenőrizze a következőket:

* A munkafüzet ténylegesen tartalmaz adatot az exportált munkalapon.  
* `setOnePagePerSheet(true)` megfelel az elrendezési elvárásainak.  
* Az Aspose.Cells licenc megfelelően be van állítva (licenc nélküli mód vízjelet ad hozzá).

### Gyakori szélsőséges esetek kezelése

| Helyzet                                   | Megoldás                                                                                         |
|-------------------------------------------|--------------------------------------------------------------------------------------------------|
| Több munkalapnak külön SVG-re van szüksége | Iteráljon a `workbook.getWorksheets()`-en, és hívja meg a `SheetRender.toImage`-t minden munkalapra. |
| Nagy munkalapok meghaladják a memória korlátokat | Engedélyezze a `options.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`-t a lemez‑alapú puffereléshez. |
| Egyedi betűtípusok nem jelennek meg helyesen | Regisztrálja a betűkészlet mappát a `FontConfigs.setFontFolder("path/to/fonts")` segítségével. |
| Átlátszó háttérre van szükség               | Hívja meg a `options.setTransparent(true)`-t a mentés előtt.                                   |

Ezek a tippek a **excel exportálása SVG-be** folyamatot robusztusabbá teszik a termelési környezetekben.

## Teljes futtatható példa

Az alábbiakban egy teljes Java program látható, amely tartalmazza az összes korábbi lépést. Másolja a kódot a `src/main/java/ExcelToSvg.java` fájlba, állítsa be a fájlutakat, és futtassa a `mvn compile exec:java -Dexec.mainClass=ExcelToSvg` parancsot.

```java
package com.example.excelsvg;

import com.aspose.cells.*;

public class ExcelToSvg {
    public static void main(String[] args) {
        try {
            // 1️⃣ Load the Excel workbook
            String excelPath = "sample.xlsx";          // ← replace with your file
            Workbook workbook = new Workbook(excelPath);

            // 2️⃣ Configure export options for SVG
            ImageOrPrintOptions options = new ImageOrPrintOptions();
            options.setSaveFormat(SaveFormat.SVG);
            options.setOnePagePerSheet(true);          // one SVG per worksheet
            options.setTransparent(true);              // optional: transparent background

            // 3️⃣ Export each worksheet as a separate SVG file
            for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
                Worksheet sheet = workbook.getWorksheets().get(i);
                String sheetName = sheet.getName().replaceAll("[^a-zA-Z0-9]", "_");
                String svgPath = "output_" + sheetName + ".svg";

                SheetRender render = new SheetRender(sheet, options);
                render.toImage(0, svgPath);            // 0 = first page of the sheet

                System.out.println("✅ Saved sheet \"" + sheetName + "\" as " + svgPath);
            }

        } catch (Exception e) {
            System.err.println("❌ Error during SVG export: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

**Várható kimenet** (konzol):

```
✅ Saved sheet "Sheet1" as output_Sheet1.svg
✅ Saved sheet "Sheet2" as output_Sheet2.svg
```

Minden SVG fájl tükrözi a megfelelő munkalap megjelenését, megőrizve a diagramokat, alakzatokat és a cellaformázást bármilyen nagyítási szinten.

## Összegzés

Most már tudja, hogyan **hozzon létre SVG-t Excelből** az Aspose.Cells for Java használatával. A tutorial mindent lefedett a projekt beállításától a tipikus szélsőséges esetek kezeléséig, és a teljes forráskód lehetővé teszi, hogy **exportálja az Excelt SVG-be** egyetlen futtatással.  

Innen tovább:

* **Excel fájlt menteni SVG-ként** webes irányítópultokhoz vagy dokumentációhoz.  
* Fedezze fel a többi export formátumot (PDF, PNG) a `SaveFormat` módosításával.  
* Integrálja a konverziót egy nagyobb Java szolgáltatásba, amely valós időben dolgozza fel a táblázatokat.  

Nyugodtan kísérletezzen a beállításokkal—különböző `ImageOrPrintOptions` beállításokkal szabályozhatja az oldal méretét, DPI-t és a háttérszínt. Ha bármilyen problémába ütközik, nézze át újra a szélsőséges esetek táblázatát, vagy konzultáljon az Aspose.Cells API referenciával a mélyebb testreszabásért.

Boldog kódolást, és élvezze az éles, skálázható grafikákat, amelyeket az SVG nyújt!

## Mit érdemes még megtanulni?

A következő tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódpéldákat lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeiben.

- [Hogyan hozzunk létre és mentsünk egy Excel munkafüzetet SVG-ként az Aspose.Cells for Java használatával](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Hogyan exportáljunk Excel diagramokat SVG-be az Aspose.Cells Java segítségével skálázható vektorgrafikához](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Hogyan konvertáljunk SVG-t Excel diagramokból az Aspose.Cells Java használatával](/cells/english/java/charts-graphs/convert-excel-charts-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}