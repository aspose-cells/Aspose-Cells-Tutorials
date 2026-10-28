---
category: general
date: 2026-08-04
description: Excel munkafüzet létrehozása Java-ban és a japán korszak dátumok feldolgozása,
  majd a munkafüzet mentése xlsx formátumban az Aspose.Cells for Java használatával.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- java excel date conversion
- Aspose.Cells Java
- japanese era date parsing
language: hu
lastmod: 2026-08-04
og_description: Excel munkafüzet létrehozása Java-val, a japán korszak dátumok automatikus
  átalakítása gregoriánra, majd a munkafüzet mentése xlsx formátumban az Aspose.Cells
  segítségével.
og_image_alt: Java code creating an Excel workbook and converting a Japanese era date
  to Gregorian
og_title: Excel munkafüzet létrehozása Java‑ban – Japán dátum konverziós útmutató
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create excel workbook java and parse Japanese era dates, then save
    workbook as xlsx using Aspose.Cells for Java.
  headline: 'Create excel workbook java: handle Japanese era dates'
  type: TechArticle
tags:
- java
- excel
- Aspose.Cells
- date conversion
- xlsx
title: 'Excel munkafüzet létrehozása Java-ban: japán korszak dátumok kezelése'
url: /hu/java/workbook-operations/create-excel-workbook-java-handle-japanese-era-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create excel workbook java: japán era dátumok kezelése

Ha **create excel workbook java**-ra van szükséged, és japán era dátumokkal szeretnél dolgozni, ez a tutorial pontosan megmutatja, hogyan. Megtanulod, hogyan adhatunk meg egy dátumot, például „R3/05/01”, és hagyjuk, hogy az Aspose.Cells azt gregorián dátumként értelmezze, majd **save workbook as xlsx**.

Az era‑alapú naptárakkal való munka zavaró lehet, különösen, ha az alapértelmezett Excel elemző egy szabványos gregorián formátumot vár. A japán era feldolgozás engedélyezésével elkerülheted a manuális karakterlánc‑manipulációt, és a könyvtárra bízhatod a konverziót. Ez az útmutató a fájl végleges `.xlsx` formátumban való mentését is lefedi.

## Előfeltételek

* Java 17 vagy újabb telepítve.
* Maven 3.6+ (vagy Gradle) a függőségek kezeléséhez.
* IDE, például IntelliJ IDEA vagy Eclipse.
* Az Aspose.Cells for Java könyvtár (a példa a 23.10-es verziót használja, de bármely friss kiadás működik).

## 1. lépés: Aspose.Cells hozzáadása a projekthez

A könyvtár biztosítja a `Workbook`, `Worksheet` és `WorkbookSettings` osztályokat, amelyeket a tutorial során használunk.

**Maven**

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

**Gradle**

```gradle
implementation 'com.aspose:aspose-cells:23.10:jdk17'
```

> **Pro tip:** Használd a `javadoc` JAR-t, hogy a kódolás közben inline dokumentációt kapj.

## 2. lépés: A munkafüzet létrehozása és az első munkalap elérése

Most létrehozunk egy új workbook objektumot, és lekérjük az alapértelmezett első lapot.

```java
import com.aspose.cells.*;

public class JapaneseEraExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();                // create an empty workbook
        Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet (index 0)
```

*Miért fontos ez a lépés:* A `Workbook` az egész Excel fájlt képviseli, míg a `Worksheet` a vászon, ahová a cellákat helyezed. Egy tiszta munkafüzetből indulva biztosítható, hogy semmilyen rejtett formázás ne zavarja a dátumfeldolgozást.

## 3. lépés: Japán era dátum beírása egy cellába

A japán era dátumok a „<EraLetter><Year>/<Month>/<Day>” mintát követik. Ebben a példában a „R3”-at (Reiwa 3 = 2021) használjuk.

```java
        // Step 3: Put a Japanese era date into cell A1
        Cell dateCell = worksheet.getCells().get("A1");
        dateCell.putValue("R3/05/01");   // Reiwa 3, May 1st
```

*Miért fontos ez a lépés:* A era karakterlánc közvetlen beírásával az Aspose.Cells később végzi el a konverziót. Elkerülöd, hogy magadnak kelljen a „R3”-at „2021”-re fordítani.

## 4. lépés: Japán era feldolgozás engedélyezése és képletek újraszámítása

Mondd meg a munkafüzetnek, hogy az era karakterláncokat dátumként kezelje. A beállítás átkapcsolása után hívd meg a `calculateFormula()`-t, hogy minden függő képlet (ha később hozzáadsz) a helyes gregorián értéket lássa.

```java
        // Step 4: Turn on Japanese era parsing
        WorkbookSettings settings = workbook.getSettings();
        settings.setUseJapaneseEra(true);   // enable era conversion
        workbook.calculateFormula();        // refresh any formulas
```

*Miért fontos ez a lépés:* A `setUseJapaneseEra(true)` jelző azt utasítja az Aspose.Cells-t, hogy a „R3/05/01” típusú karakterláncokat gregorián dátumként értelmezze. Enélkül a cella a szöveget tartaná, ami a további számításokat megtöri.

## 5. lépés: A konverzió ellenőrzése és **save workbook as xlsx**

Írd ki a konvertált értéket a konzolra, és mentsd el a munkafüzetet.

```java
        // Step 5: Verify conversion and save the file
        System.out.println("Converted date: " + dateCell.getStringValue()); // → 2021-05-01
        workbook.save("JapaneseEra.xlsx");   // saves as .xlsx by default
    }
}
```

**Várható konzolkimenet**

```
Converted date: 2021-05-01
```

A `JapaneseEra.xlsx` fájl most már a gregorián `2021‑05‑01` dátumot tartalmazza az A1 cellában, annak ellenére, hogy a forrás karakterlánc japán era formátumot használt.

## 6. lépés: Gyakori variációk és szélsőséges esetek kezelése

| Szituáció | Hogyan kell módosítani a kódot |
|----------|-------------------------------|
| Másik era (pl. Heisei) | Használd a „H30/12/31” formátumot a Heisei 30 = 2018‑12‑31 esetén. Ugyanaz a `setUseJapaneseEra(true)` jelző minden támogatott era esetén működik. |
| Üres vagy hibás karakterlánc | Tedd a `putValue`-t try‑catch blokkba, és ellenőrizd egy regex-szel, például `^[RHS][0-9]+/[0-9]{2}/[0-9]{2}$`. |
| Az eredeti era karakterlánc auditálásra való megőrzése | Tárold a nyers karakterláncot egy rejtett oszlopban a konverzió előtt, majd a végső munkafüzetben rejtetté teheted azt az oszlopot. |
| Nagy adathalmazok | Engedélyezd a `WorkbookSettings.setEnableThreadedCalculation(true)`-t a képletújraszámítás felgyorsításához, ha sok sor használ era dátumokat. |

> **Figyelj:** Ha egy régebbi Aspose.Cells verziót használsz, amely a japán era támogatása előtt (2020 előtti) jelent meg, akkor a `setUseJapaneseEra` jelzőt figyelmen kívül hagyja, és a cella változatlan marad.

## 7. lépés: Példa futtatása

Fordítsd le és futtasd a osztályt az IDE-ből vagy a parancssorból:

```bash
javac -cp "path/to/aspose-cells-23.10.jar" JapaneseEraExample.java
java -cp ".:path/to/aspose-cells-23.10.jar" JapaneseEraExample
```

A futtatás után nyisd meg a `JapaneseEra.xlsx` fájlt Excelben. Az A1 cella `2021-05-01` értéket mutat, ami megerősíti, hogy a **java excel date conversion** sikeres volt.

## Következtetés

Most már tudod, hogyan **create excel workbook java**, hogyan adj meg egy japán era dátumot, engedélyezd az automatikus era feldolgozást, és **save workbook as xlsx**. Ez a megközelítés megszünteti a manuális dátumaritmetikát, és biztosítja, hogy az Excel fájljaid kompatibilisek legyenek a szabványos gregorián naptárral.

### Mit érdemes még felfedezni

* **Formatting dates** – alkalmazz cellastílusokat (`Style style = workbook.createStyle(); style.setNumber(14);`), hogy a dátumokat a kívánt helyi beállításban jelenítsd meg.
* **Bulk conversion** – iterálj egy era karakterláncok oszlopán, és egy ciklusban konvertáld minden cellát.
* **Export to other formats** – az Aspose.Cells támogatja a PDF, CSV és ODS formátumokat is; egyszerűen változtasd meg a fájl kiterjesztését a `workbook.save(...)` hívásban.

Nyugodtan kísérletezz más erákkal, egyedi formátumokkal, vagy kombináld ezt a technikát képlettel vezérelt jelentésekkel. Jó kódolást!

## Mit kellene legközelebb megtanulnod?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a bemutatott technikákra épülnek. Minden forrás teljes, működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Hogyan hozzunk létre és mentsünk el egy Excel munkafüzetet SVG formátumban az Aspose.Cells for Java segítségével](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Excel munkafüzet létrehozása és mentése Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Excel munkafüzet létrehozása és mentése Aspose Cells Java](/cells/french/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}