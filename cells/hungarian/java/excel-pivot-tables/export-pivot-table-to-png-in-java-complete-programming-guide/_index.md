---
category: general
date: 2026-06-27
description: Exportálja a pivot táblát Excel pivot képként Java-ban. Ismerje meg,
  hogyan állíthatja be a PNG formátumot, konfigurálhatja a beállításokat, és mentheti
  a fájlt néhány egyszerű lépésben.
draft: false
keywords:
- export pivot table
- excel pivot image
- set png format
language: hu
og_description: Exportálja a pivot táblát Excel pivot képként Java-val. Ez az útmutató
  bemutatja, hogyan állítható be a PNG formátum, és hogyan menthető a kép magabiztosan.
og_title: Pivot tábla exportálása PNG-be Java-ban – Lépésről lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Export pivot table as an Excel pivot image in Java. Learn how to set
    PNG format, configure options, and save the file in just a few steps.
  headline: Export pivot table to PNG in Java – Complete Programming Guide
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Pivot tábla exportálása PNG-re Java-ban – Teljes programozási útmutató
url: /hu/java/excel-pivot-tables/export-pivot-table-to-png-in-java-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pivot tábla exportálása PNG-be Java‑ban – Teljes programozási útmutató

Valaha szükséged volt **pivot tábla** exportálására egy Excel munkafüzetből, de nem tudtad, hogyan kapj tiszta képfájlt? Nem vagy egyedül – sok fejlesztő ütközik ebbe a problémába jelentés‑dashboardok építésekor. A jó hír, hogy néhány Java sorral bármely pivot táblát átalakíthatsz egy éles **Excel pivot képpé**, amely PNG‑ként menthető.  

Ebben az útmutatóban végigvezetünk a teljes folyamaton: a munkafüzet beolvasása, az első pivot tábla megtalálása, a **PNG formátum beállítása** az exporthoz, majd a kép lemezre írása. A végére egy újrahasználható kódrészletet kapsz, amelyet bármely projektbe beilleszthetsz.

## Mit fogsz megtanulni

- Hogyan töltsünk be egy Excel fájlt az Aspose.Cells (vagy Apache POI, ha azt részesíted előnyben) segítségével.  
- A pontos API hívások, amelyek szükségesek a **pivot tábla** PNG‑ként való **exportálásához**.  
- Miért fontos a képformátum beállítása, és hogyan **állítsuk be a PNG formátumot** helyesen.  
- Gyakori buktatók – például több pivot tábla kezelése vagy hiányzó munkalapok – és hogyan kerüld el őket.  
- Egy teljes, azonnal futtatható Java példa, amelyet egyszerűen másolhatsz.

> **Előfeltételek**  
> • Java 17 vagy újabb (a kód korábbi verziókkal is működik, de a 17‑et ajánljuk).  
> • Aspose.Cells for Java könyvtár (az ingyenes próba verzió is megfelelő).  
> • Alapvető ismeretek az Excel fájlokról és a Java I/O‑ról.

---

## 1. lépés: Aspose.Cells függőség hozzáadása

Ha Maven‑t használsz, illeszd be a következő függőséget a `pom.xml`‑be. Egyébként töltsd le a JAR‑t az Aspose weboldaláról, és add hozzá a classpath‑hoz.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- latest as of June 2026 -->
</dependency>
```

*Pro tip:* Tartsd a könyvtár verziókat szinkronban a hivatalos kiadási jegyzetekkel, hogy elkerüld a váratlan hibákat.

## 2. lépés: A munkafüzet betöltése és a pivot tábla megtalálása

Először megnyitjuk az Excel fájlt, majd lekérjük az első pivot táblát az első munkalapon. Ha a munkafüzet nem tartalmaz pivot táblákat, akkor elegánsan kilépünk.

```java
import com.aspose.cells.*;

public class PivotTableExporter {

    public static void main(String[] args) {
        try {
            // Load the workbook (replace with your actual path)
            Workbook workbook = new Workbook("C:/data/report.xlsx");

            // Access the first worksheet – you can also loop through all sheets
            Worksheet ws = workbook.getWorksheets().get(0);

            // Verify that the sheet actually contains pivot tables
            if (ws.getPivotTables().getCount() == 0) {
                System.out.println("No pivot tables found on the first sheet.");
                return;
            }

            // Retrieve the first pivot table (this is the target for export)
            PivotTable pivotTable = ws.getPivotTables().get(0);
```

> **Miért fontos ez a lépés** – A `PivotTable` objektum a belépési pont minden képexportáláshoz. Ha egy nem létező pivoton próbálod meghívni a `toImage`‑t, `NullPointerException` keletkezik, ezért először ellenőrizzük a darabszámot.

## 3. lépés: Képexportálási beállítások konfigurálása (PNG formátum beállítása)

Most létrehozunk egy `ImageOrPrintOptions` példányt, és kifejezetten **beállítjuk a PNG formátumot**. A PNG veszteségmentes, így megőrzi a rácsvonalak és betűk élességét.

```java
            // Step 3: Configure image export options – we want PNG
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
            imgOptions.setImageFormat(ImageFormat.PNG);   // <-- set png format
            imgOptions.setOnePagePerSheet(true);          // optional: force single‑page output
            imgOptions.setTransparent(true);              // optional: keep background transparent
```

*Note:* Ha JPEG‑et szeretnél, egyszerűen cseréld le az `ImageFormat.PNG`‑t `ImageFormat.JPEG`‑re. Ugyanaz az opcióobjektum mindkét formátumhoz működik.

## 4. lépés: A pivot tábla exportálása képfájlként

A beállítások készen állnak, meghívjuk a `toImage`‑t. A metódus közvetlenül írja a fájlt, így nincs szükség extra stream‑ekre.

```java
            // Step 4: Export the pivot table as an image file
            String outputPath = "C:/exports/pivot.png";
            pivotTable.toImage(outputPath, imgOptions);

            System.out.println("Pivot table exported successfully to: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

A program futtatása egy `pivot.png` nevű fájlt hoz létre, amely pontosan úgy néz ki, mint a pivot a Excelben. Nyisd meg bármely képnézővel a ellenőrzéshez.

### Várt kimenet

```
Pivot table exported successfully to: C:/exports/pivot.png
```

Az eredménykép megegyezik a képernyőn látható elrendezéssel, beleértve az oszlopszélességeket, sormagasságokat és az alkalmazott feltételes formázást.

## Több pivot tábla kezelése (Haladó)

Mi van, ha a munkalapon több pivot tábla is van, és csak egy konkrétat szeretnél? Végigiterálhatsz a `ws.getPivotTables()`‑en, és név alapján választhatsz:

```java
PivotTable target = null;
for (int i = 0; i < ws.getPivotTables().getCount(); i++) {
    PivotTable pt = ws.getPivotTables().get(i);
    if ("SalesByRegion".equals(pt.getName())) {
        target = pt;
        break;
    }
}
if (target == null) {
    System.out.println("Desired pivot table not found.");
    return;
}
target.toImage("C:/exports/sales_by_region.png", imgOptions);
```

*Why this is useful*: A valós jelentésekben gyakran van egy összegző pivot és egy részletes. A név szerinti kiválasztás megakadályozza a véletlen felülírásokat.

## Gyakori buktatók és megoldások

| Probléma | Tünet | Megoldás |
|------|----------|-----|
| **Hiányzó munkalap** | `IndexOutOfBoundsException` a `ws` elérésekor | Ellenőrizd, hogy `workbook.getWorksheets().getCount() > 0` mielőtt indexelnél. |
| **Nincs pivot tábla** | Csendes hiba vagy üres kép | Használd a `ws.getPivotTables().getCount()` ellenőrzést (lásd 2. lépés). |
| **Helytelen képformátum** | A kimenet elmosódott vagy hibákat mutat | Mindig `setImageFormat(ImageFormat.PNG)` a veszteségmentes kimenethez; kerüld a JPEG‑et szöveggel teli táblák esetén. |
| **A fájlútvonal nem írható** | `IOException` a `toImage`‑nél | Győződj meg róla, hogy a könyvtár létezik (`new File(outputPath).getParentFile().mkdirs()`). |

## Pro Tip: Exportálás byte tömbbe webes alkalmazásokhoz

Ha egy webszolgáltatást építesz, amely közvetlenül a böngészőnek adja vissza a PNG‑t, akkor a `ByteArrayOutputStream`‑be írhatsz fájl helyett:

```java
ByteArrayOutputStream baos = new ByteArrayOutputStream();
pivotTable.toImage(baos, imgOptions);
byte[] pngBytes = baos.toByteArray();
// Send pngBytes as HTTP response with Content-Type: image/png
```

Ez megszünteti az ideiglenes fájlok szükségességét, és felgyorsítja a választ.

---

## Teljes működő példa (Minden lépés egyben)

Az alábbiakban a komplett, másolás‑beillesztésre kész program látható, amely tartalmazza a megbeszélt legjobb gyakorlatokat.

```java
import com.aspose.cells.*;
import java.io.*;

public class PivotTableExporter {

    public static void main(String[] args) {
        // 1️⃣ Load workbook
        Workbook workbook;
        try {
            workbook = new Workbook("C:/data/report.xlsx");
        } catch (Exception e) {
            System.err.println("Failed to load workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Get first worksheet and ensure a pivot exists
        if (workbook.getWorksheets().getCount() == 0) {
            System.out.println("Workbook contains no worksheets.");
            return;
        }
        Worksheet ws = workbook.getWorksheets().get(0);
        if (ws.getPivotTables().getCount() == 0) {
            System.out.println("No pivot tables on the first sheet.");
            return;
        }
        PivotTable pivotTable = ws.getPivotTables().get(0); // export pivot table

        // 3️⃣ Configure export options – set png format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.PNG); // <-- set png format
        imgOptions.setOnePagePerSheet(true);
        imgOptions.setTransparent(true);

        // 4️⃣ Prepare output directory
        String outDir = "C:/exports";
        new File(outDir).mkdirs(); // create if missing

        // 5️⃣ Export the image
        String outPath = outDir + "/pivot.png";
        try {
            pivotTable.toImage(outPath, imgOptions);
            System.out.println("Pivot table exported successfully to: " + outPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

Ennek az osztálynak a futtatása `pivot.png`‑t generál a `C:/exports` mappában. Nyisd meg a fájlt, és egy pontos vizuális másolatot látsz az eredeti pivot tábláról – tökéletes beágyazáshoz jelentésekbe, e‑mailekbe vagy weboldalakra.

![Exportált pivot tábla PNG‑ként mentve – például egy excel pivot kép](https://example.com/images/pivot-export.png "export pivot tábla példa")

*Image alt text:* **export pivot tábla példa, amely PNG Excel pivot képet mutat**

---

## Összegzés

Most megmutattuk, hogyan **exportálhatod a pivot táblát** Excelből magas minőségű PNG‑be Java segítségével. A kulcsfontosságú lépések: a munkafüzet betöltése, a pivot megtalálása, az `ImageOrPrintOptions` **PNG formátumra** állítása, majd a `toImage` meghívása.  

Ezzel a tudással most automatizálhatod a jelentéskészítést, beágyazhatod a pivot pillanatképeket dashboardokba, vagy közvetlenül egy web API‑ból szolgálhatod ki őket. Következő lépésként érdemes lehet a **excel pivot image** méretezési lehetőségeket felfedezni, vízjelet hozzáadni, vagy akár a PNG‑t PDF‑be konvertálni nyomtatási jelentésekhez.  

Van kérdésed nagyobb munkafüzetek kezelése vagy a Spring Boot integrálása kapcsán? Írj egy megjegyzést alább, és jó kódolást!

## Mit érdemes még tanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes működő kódpéldákat és lépésről‑lépésre magyarázatokat tartalmaz, hogy további API‑funkciókat saját projektjeidben is könnyedén alkalmazhass.

- [Hogyan frissítsük az Excel Pivot Tábla forrását az Aspose.Cells for Java‑val: Átfogó útmutató](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Excel Pivot Tábla Stílusának és Mentésének automatizálása az Aspose.Cells for Java‑val: Átfogó útmutató](/cells/english/java/data-analysis/excel-pivot-table-styling-saving-aspose-cells-java/)
- [Excel Pivot Tábla Manipuláció az Aspose.Cells Java‑val: Átfogó útmutató](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}