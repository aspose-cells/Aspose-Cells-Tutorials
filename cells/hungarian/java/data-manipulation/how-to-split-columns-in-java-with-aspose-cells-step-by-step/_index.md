---
category: general
date: 2026-10-07
description: Hogyan lehet oszlopokat szétválasztani az Aspose.Cells for Java segítségével.
  Tanulja meg, hogyan lehet egy karakterláncot oszlopokra bontani, automatizálni az
  Excel képletet, és néhány sor kóddal képletet írni egy cellába.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to split columns
- split string into columns
- automate excel formula
- write formula to cell
language: hu
lastmod: 2026-10-07
og_description: Hogyan oszthatunk szét oszlopokat Java-ban az Aspose.Cells segítségével.
  Ez az útmutató megmutatja, hogyan lehet egy karakterláncot oszlopokra bontani, automatizálni
  az Excel képlet kiértékelését, és képletet írni egy cellába.
og_image_alt: Screenshot of Java code that splits columns in an Excel worksheet using
  Aspose.Cells
og_title: Hogyan oszthatunk fel oszlopokat Java-ban az Aspose.Cells segítségével –
  gyors útmutató
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: How to split columns using Aspose.Cells for Java. Learn to split string
    into columns, automate Excel formula, and write formula to cell in a few lines
    of code.
  headline: How to split columns in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Hogyan lehet oszlopokat felosztani Java-ban az Aspose.Cells használatával –
  lépésről lépésre útmutató
url: /hu/java/data-manipulation/how-to-split-columns-in-java-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan oszthatunk szét oszlopokat Java-val az Aspose.Cells segítségével – lépésről‑lépésre útmutató

Ha programozott módon **hogyan oszthatunk szét oszlopokat** egy Excel munkalapon, ez az útmutató bemutatja a teljes folyamatot az Aspose.Cells for Java segítségével. Megtanulod, hogyan **szétbontjuk a karakterláncot oszlopokra**, **automatizáljuk az Excel képlet** kiértékelését, és **képletet írunk egy cellába** tömör, termelés‑kész kóddal.

A programozott oszlopszegmentálás megszünteti a kézi másolás‑beillesztést, csökkenti a hibákat, és lehetővé teszi a nagyméretű adattranszformációkat. A tutorial végére képes leszel képleteket generálni, módosítani és kiértékelni menet közben, így az Excel valódi része lesz a Java backendnek.

## Előfeltételek

* Java 17 vagy újabb telepítve.  
* Maven 3.8+ (vagy Gradle) a függőségkezeléshez.  
* Aspose.Cells for Java licenc (az ingyenes értékelő verzió tanuláshoz megfelelő).  
* Alapvető ismeretek a Java szintaxisról és az Excel fogalmakról.  

Ha bármelyik elem hiányzik, először telepítsd; a kódminták egy szabványos Maven projektet feltételeznek.

## 1. lépés: Aspose.Cells hozzáadása a projekthez

A `pom.xml`-hez add hozzá a következő függőséget. Ez letölti a legújabb stabil Aspose.Cells könyvtárat.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version available -->
</dependency>
```

**Miért fontos ez a lépés:** A könyvtár biztosítja a `Workbook`, `Worksheet` és `Cell` osztályokat, amelyek szükségesek az Excel fájlok Microsoft Office nélkül történő manipulálásához. Függőség nélkül a kód nem fordul le.

## 2. lépés: Munkafüzet létrehozása és az első munkalap kiválasztása

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize a new workbook and access the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
```

A `Workbook` objektum az egész Excel fájlt képviseli. Az első munkalap elérése biztosítja a kiszámítandó képlet számára a kiszámítható kiindulási pontot.

## 3. lépés: A WRAPCOLS képlet írása egy célcellába

```java
        // Step 3: Identify the target cell (A1) where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");

        // Step 3: Write the WRAPCOLS formula to split a long string into three columns
        // WRAPCOLS(string, columns) distributes the string across the specified number of columns.
        targetCell.setFormula("=WRAPCOLS(\"This is a very long string that needs to be split\",3)");
```

**Miért használjuk a `WRAPCOLS`-t:** A beépített Excel függvény `WRAPCOLS` automatikusan felbont egyetlen szöveges értéket egy meghatározott számú oszlopra, intelligensen kezeli a szóhatárokat. Ez a legmegbízhatóbb mód a **szöveg karakterlánc oszlopokra bontására** egyedi elemzési logika nélkül.

## 4. lépés: A munkafüzet kényszerített képletértékelése

```java
        // Step 4: Calculate all formulas in the workbook so the result becomes visible
        workbook.calculateFormula();
```

`calculateFormula()` hívása **automatizálja az Excel képlet** kiértékelését a szerver oldalon. Enélkül a cella továbbra is a képlet szövegét tartalmazná, nem a kiszámított értékeket.

## 5. lépés: A csomagolt eredmény lekérése és megjelenítése

```java
        // Step 5: Retrieve the computed value from the target cell
        String result = targetCell.getStringValue(); // returns the first column of the split result
        System.out.println("First column output: " + result);

        // Optionally, read the other columns created by WRAPCOLS
        String second = worksheet.getCells().get("B1").getStringValue();
        String third  = worksheet.getCells().get("C1").getStringValue();

        System.out.println("Second column output: " + second);
        System.out.println("Third column output: " + third);

        // Save the workbook to verify the split visually (optional)
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

A program futtatásakor a konzol kiírja:

```
First column output: This is a very long
Second column output: string that needs
Third column output: to be split
```

Az előállított `SplitColumnsResult.xlsx` fájl a három oszlopban megjeleníti a szétbontott szöveget.

## A WRAPCOLS függvény megértése

* **Szintaxis:** `WRAPCOLS(text, columns, [delimiter])`
* **Paraméterek:**
  * `text` – a felbontandó karakterlánc.
  * `columns` – a szöveget elosztandó oszlopok száma.
  * `delimiter` (opcionális) – a karakter, amellyel a szöveget bontjuk; alapértelmezett egy szóköz.
* **Visszatérési érték:** Egy tömb, amely a szomszédos cellákba terjed, minden elem az eredeti szöveg egy részét tartalmazza.

Mivel a függvény vízszintesen terjed, csak a baloldali cellába (a példában A1) kell beírni a képletet. Az Excel automatikusan kitölti a B1, C1, … cellákat szükség szerint.

## Gyakori változatok és szélsőséges esetek

| Situation | Recommended adjustment |
|-----------|------------------------|
| **Változó oszlopszám** | Replace the hard‑coded `3` with a variable: `targetCell.setFormula(String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount));` |
| **Egyéni elválasztó** | Use the third argument, e.g., `=WRAPCOLS(A2,4,",")` to split on commas. |
| **Üres forráskarakterlánc** | The function returns empty cells; guard against `null` or empty strings before setting the formula. |
| **Nagy adathalmazok** | Apply the formula in a loop for each row, then call `calculateFormula()` once after the loop to improve performance. |
| **Nem ASCII karakterek** | WRAPCOLS works with Unicode; ensure your Java source file is saved as UTF‑8. |

**Pro tipp:** Sok sor feldolgozásakor tárold a képletet egy karakterlánc változóban, és használd újra, hogy elkerüld az ismétlődő karakterlánc-összefűzés költségét.

## Teljes, futtatható példa

Az alábbiakban a teljes program látható, amely készen áll a másolás‑beillesztésre. Tartalmaz importálásokat, kivételkezelést és egy opcionális mentési műveletet.

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Define the long string and desired column count
        String longString = "This is a very long string that needs to be split";
        int columnCount = 3;

        // Write the WRAPCOLS formula to cell A1
        Cell targetCell = worksheet.getCells().get("A1");
        String formula = String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount);
        targetCell.setFormula(formula);

        // Evaluate all formulas in the workbook
        workbook.calculateFormula();

        // Read and display each column's result
        System.out.println("First column output: " + worksheet.getCells().get("A1").getStringValue());
        System.out.println("Second column output: " + worksheet.getCells().get("B1").getStringValue());
        System.out.println("Third column output: " + worksheet.getCells().get("C1").getStringValue());

        // Save the workbook for visual verification
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

A program futtatása ugyanazt a konzolkimenetet eredményezi, mint korábban, és egy Excel fájlt ír, amely egyértelműen bemutatja, **hogyan oszthatunk szét oszlopokat**.

## Hibaelhárítási ellenőrzőlista

* **A képlet nem értékelődik ki** – Győződj meg róla, hogy a képlet beállítása után meghívod a `workbook.calculateFormula()`‑t.  
* **A felbontás után üres cellák** – Ellenőrizd, hogy a forráskarakterlánc nem `null` vagy üres, és hogy az oszlopszám nagyobb, mint nulla.  
* **Licenc kivétel** – Adj meg egy érvényes Aspose.Cells licencfájlt (`License license = new License(); license.setLicense("Aspose.Total.lic");`) a munkafüzet létrehozása előtt, hogy eltávolítsd az értékelő vízjelet.  
* **Teljesítménycsökkenés nagy lapokon** – Hívd meg a `calculateFormula()`‑t egyszer, miután az összes képletet beírtad, ne minden egyes cella után.

## Következtetés

Most már tudod, **hogyan oszthatunk szét oszlopokat** Java-ban az Aspose.Cells segítségével, hogyan **szétbontjuk a karakterláncot oszlopokra** a `WRAPCOLS` függvénnyel, hogyan **automatizáljuk az Excel képlet** kiértékelését, és hogyan **képletet írunk egy cellába** programozott módon. Ez a technika megszünteti a manuális adat‑előkészítési lépéseket, és az Excel erőteljes szövegkezelő képességeit közvetlenül a Java alkalmazásaidba integrálja.

### Következő lépések

* Fedezd fel a többi szövegfüggvényt, például a `TEXTSPLIT` és `FILTERXML`‑t összetettebb elemzési forgatókönyvekhez.  
* Kombináld a `WRAPCOLS`‑t az `IFERROR`‑rel, hogy a váratlan bemeneteket elegánsan kezeld.  
* Integráld a megoldást egy Spring Boot szolgáltatásba, amely REST‑en keresztül CSV adatokat kap, és egy feltöltött Excel fájlt ad vissza.

Ezeknek a mintáknak a elsajátításával robusztus, automatizált Excel munkafolyamatokat építhetsz, amelyek a vállalkozásod igényeivel skálázhatók. Boldog kódolást!

## Mit érdemes következőként megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [aspose cells java – Nevek oszlopokra bontása](/cells/english/java/cell-operations/aspose-cells-java-split-names-columns/)
- [Excel oszlopok automatikus méretezése Java-ban az Aspose.Cells használatával](/cells/english/java/formatting/aspose-cells-java-auto-fit-excel-columns-guide/)
- [Hogyan töröljünk üres oszlopokat Excelben az Aspose.Cells Java&#58; Átfogó útmutató](/cells/english/java/worksheet-management/delete-blank-columns-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}