---
category: general
date: 2026-11-25
description: Tanulja meg, hogyan hozhat létre Excel munkafüzetet, általános cellaformázást
  végezzen, Excel cellára stílust alkalmazzon, és mentse a munkafüzetet XLSX formátumban
  Java és az Aspose.Cells használatával.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- format cell general
- apply style excel cell
- save workbook xlsx
language: hu
lastmod: 2026-11-25
og_description: Excel munkafüzet létrehozása Java-ban, cella általános formázása,
  Excel cella stílusának alkalmazása, és a munkafüzet XLSX formátumban mentése japán
  korszak dátumok kezelése közben.
og_image_alt: Screenshot of a Java IDE showing code that creates an Excel workbook
  with a formatted date cell
og_title: Excel munkafüzet létrehozása japán korszak dátumokkal – lépésről‑lépésre
  Java útmutató
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to create Excel workbook, format cell general, apply style
    Excel cell, and save workbook XLSX using Java and Aspose.Cells.
  headline: How to create Excel workbook with Japanese era dates in Java
  type: TechArticle
tags:
- Java
- Excel automation
- Aspose.Cells
title: Hogyan hozzunk létre Excel-munkafüzetet japán korszak dátumokkal Java-ban
url: /hu/java/formatting/how-to-create-excel-workbook-with-japanese-era-dates-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan hozzunk létre Excel munkafüzetet japán era dátumokkal Java-ban

Ha **Excel munkafüzetet** kell létrehoznod, amely japán era dátumokat tárol, ez az útmutató pontos lépéseket mutat. Megtanulod, hogyan formázd a cellát General‑ként, hogyan alkalmazz stílust az Excel cellára, és végül hogyan **mentsd el a munkafüzetet XLSX‑ként**, hogy a dátum helyesen legyen értelmezve.

A japán era karakterláncok (például „R3‑04‑01”) kezelése nehéz lehet, mivel az Excel valódi `DateTime` értéket vár, nem csak szöveget. A tutorial végére egy teljesen működő `.xlsx` fájlt kapsz, amely a megfelelő gregorián dátumot jeleníti meg, miközben megőrzi az eredeti era jelölést.

## Előfeltételek

- Java 17 vagy újabb (a kód korábbi verziókkal is lefordítható)
- Aspose.Cells for Java könyvtár (`aspose-cells-xx.x.jar`) – a könyvtár ingyenes értékelésre, és teljes funkcionalitással rendelkezik termeléshez
- Alapvető Java és Maven/Gradle ismeretek (vagy a képesség, hogy JAR‑t adj a classpath‑hoz)
- IDE, például IntelliJ IDEA, Eclipse vagy VS Code (bármelyik megfelel)

## 1. lépés – Excel munkafüzet létrehozása

Az első művelet egy új workbook objektum példányosítása. Ez az objektum a teljes Excel fájlt reprezentálja a memóriában, és hozzáférést biztosít a munkalapokhoz, cellákhoz és stílusokhoz.

```java
import com.aspose.cells.*;

public class JapaneseEraExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook (an empty .xlsx file in memory)
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

**Miért fontos:**  
A munkafüzet programozott létrehozása kiküszöböli a sablonfájl szükségességét, és garantálja, hogy a keletkező fájl tiszta állapottal indul. A `Workbook` konstruktor automatikusan létrehoz egy alapértelmezett lapot, amelyet a további manipulációhoz lekérünk.

## 2. lépés – A cella formázása General‑ként

Az Excel különböző formátumokkal tárolja a számokat. Egy olyan dátum esetén, amelyet később japán era karakterláncból konvertálunk, először a cella számformátumát *General*‑ra állítjuk, hogy az Excel ne próbálja meg előre értelmezni a szöveget.

```java
        // Step 2: Get the target cell (A1) where the era date will be placed
        Cell targetCell = worksheet.getCells().get("A1");

        // Write the raw Japanese era string (e.g., "R3-04-01")
        targetCell.putValue("R3-04-01");

        // Ensure the cell uses the General number format
        Style cellStyle = targetCell.getStyle();
        cellStyle.setNumber(0); // 0 = General format in Aspose.Cells
        targetCell.setStyle(cellStyle);
```

**Miért fontos:**  
A **format cell general** beállítása megakadályozza, hogy az Excel automatikusan egyedi formátummal szövegként kezelje az era karakterláncot, ami megakadályozná a későbbi valódi `DateTime` értékké alakítást. A `setNumber(0)` hívás az Aspose.Cells megfelelője az Excel „General” formátumának.

## 3. lépés – Stílus alkalmazása az Excel cellára

Bár az elsődleges cél egy dátum tárolása, előfordulhat, hogy a cellát a lap többi részével egységesen szeretnéd megjeleníteni – például vékony szegéllyel vagy egy adott betűtípussal. A stílus alkalmazása azt is bemutatja, hogyan manipulálhatók a cella esztétikai tulajdonságai programból.

```java
        // Step 3: Apply additional styling (optional but common)
        // Example: add a thin border around the cell
        cellStyle.setBorder(BorderType.TOP_BORDER, CellBorderType.THIN);
        cellStyle.setBorder(BorderType.BOTTOM_BORDER, CellBorderType.THIN);
        cellStyle.setBorder(BorderType.LEFT_BORDER, CellBorderType.THIN);
        cellStyle.setBorder(BorderType.RIGHT_BORDER, CellBorderType.THIN);

        // Set a light gray background to highlight the date cell
        cellStyle.setPattern(BackgroundType.SOLID);
        cellStyle.setBackgroundColor(Color.getGray());

        // Apply the updated style back to the cell
        targetCell.setStyle(cellStyle);
```

**Miért fontos:**  
A **apply style excel cell** lépés megmutatja, hogyan gazdagítható a vizuális megjelenés anélkül, hogy az adat alapszerkezetét befolyásolná. A szegélyek és háttérszínek a cella stílusobjektum részeként kerülnek tárolásra, biztosítva, hogy a végső munkafüzet megnyitáskor kifinomult legyen.

## 4. lépés – A japán era karakterlánc konvertálása DateTime objektummá

Most a nyers szöveget helyettesítjük egy megfelelő `DateTime` értékkel. Az Aspose.Cells egy adott `CultureInfo` használatával tud karakterláncot értelmezni. A japán kultúra (`ja-JP`) megadásával a könyvtár helyesen értelmezi a „R3‑04‑01” karakterláncot, ami a Reiwa 3. évét jelenti, és a gregorián naptárban 2021‑04‑01‑nek felel meg.

```java
        // Step 4: Convert the era string to a DateTime using Japanese culture
        // The fromString method respects the culture’s calendar (Japanese Imperial)
        DateTime japaneseDate = DateTime.fromString(
                "R3-04-01", // era string
                CultureInfo.createSpecificCulture("ja-JP") // Japanese locale
        );

        // Overwrite the cell value with the parsed DateTime
        targetCell.setValue(japaneseDate);
```

**Miért fontos:**  
Kultúra megadása nélkül a „R3‑04‑01” egyszerű szövegként lenne kezelve, elveszítve a dátum szemantikai jelentését. A `CultureInfo` objektum azt mondja meg az Aspose.Cells‑nek, hogy a japán naptár rendszert használja, automatikusan kezelve az era konverziót. A cella most már valódi Excel dátumot tartalmaz, ami lehetővé teszi a rendezést, szűrést és dátum számításokat.

## 5. lépés – A munkafüzet mentése XLSX‑ként

Végül az in‑memory munkafüzetet egy fizikai fájlba írjuk. A `.xlsx` formátum használata garantálja a kompatibilitást a modern Excel verziókkal, a Google Sheets‑szel és más táblázatkezelőkkel.

```java
        // Step 5: Save the workbook to the desired location
        String outputPath = "JapaneseEra.xlsx"; // adjust the path as needed
        workbook.save(outputPath, SaveFormat.XLSX);

        System.out.println("Workbook saved successfully to " + outputPath);
    }
}
```

**Miért fontos:**  
A **save workbook xlsx** művelet véglegesíti az összes módosítást. Az Aspose.Cells a munkafüzetet Open XML formátumban írja, megőrizve az adatot és a korábbi lépésekben alkalmazott stílusokat. A keletkező fájl közvetlenül megnyitható Excelben, ahol a cella `2021‑04‑01`‑et (a gregorián megfelelőjét) jeleníti meg, de az eredeti era karakterlánc továbbra is visszanyerhető az Excel „Formátum cellák → Szám → Egyéni” menüpontjával, ha szükséges.

## Várt kimenet

Amikor megnyitod a `JapaneseEra.xlsx` fájlt a Microsoft Excelben:

- Az **A1** cella a `2021‑04‑01` dátumot mutatja (az Excel alapértelmezett dátumformátuma).  
- A cellának vékony szürke szegélye és világosszürke háttérszíne van, ami igazolja, hogy a **apply style excel cell** lépés sikeres volt.  
- Ha a cella formátumát „General”‑re változtatod, az alaptárolt érték továbbra is valódi dátum marad, nem az eredeti szöveg.

A konzol a következőt írja ki:

```
Workbook saved successfully to JapaneseEra.xlsx
```

## Gyakori variációk és edge case‑ek

| Helyzet | Mit kell módosítani |
|-----------|----------------|
| **Másik era (pl. Heisei)** | Használd a megfelelő era előtagot (`H` a Heisei‑hez) a bemeneti karakterláncban. Ugyanaz a `CultureInfo` kezeli a konverziót. |
| **Több dátum** | Iterálj egy cellatartományon, és alkalmazd ugyanazt a konverziós logikát mindegyikre. |
| **Egyedi dátumformátum** | A `setValue(japaneseDate)` után hívd meg `cellStyle.setNumber(14)`‑et (vagy bármely Excel számformátum ID‑t), hogy a dátum `yyyy/MM/dd` formátumban jelenjen meg. |
| **Nagy munkafüzetek** | Teljesítményjavításként használj egyetlen `Style` objektumot újra, vagy alkalmazz `StyleFlag`‑et csak a szükséges attribútumok módosításához. |
| **Mentés stream‑be** | Cseréld le a `workbook.save(outputPath, SaveFormat.XLSX)`‑t `workbook.save(outputStream, SaveFormat.XLSX)`‑re, ha a fájlt HTTP‑n keresztül küldöd. |

## Gyakorlati tippek

- **Pro tipp:** Mindig állítsd be a cella számformátumát *mielőtt* `DateTime`‑ot rendelnél hozzá. A formátum későbbi módosítása miatt az Excel rossz vizuális megjelenítést adhat.
- **Vigyázz:** A `CultureInfo("ja-JP")` használata `createSpecificCulture` nélkül visszaeshet a gregorián naptárra, ami helytelen dátumokhoz vezet.
- **Teljesítményjegyzet:** Sok stílusos cella létrehozásakor klónozz egy meglévő `Style`‑t a `getStyle()` minden cellához való hívása helyett; ez csökkenti a belső másolási terhelést.

## Összegzés

Ebben a tutorialban megtanultad, hogyan **hozz létre Excel munkafüzetet** Java‑ban, hogyan **formázd a cellát General‑ként**, hogyan **alkalmazz stílust az Excel cellára**, és hogyan **mentsd el a munkafüzetet XLSX‑ként**, miközben helyesen kezeled a japán era dátumokat. A teljes kódminta készen áll a másolásra, beillesztésre és futtatásra, megbízható alapot nyújtva minden olyan Excel‑automatizáláshoz, amely nem‑gregorián naptárakat érint.

Következő lépések:

- Képletek hozzáadása, amelyek a konvertált dátumokra hivatkoznak (pl. `=YEAR(A1)`).
- A munkafüzet exportálása PDF‑be a `workbook.save("output.pdf", SaveFormat.PDF)` használatával.
- Ennek a logikának a beágyazása egy Spring Boot REST végpontra, hogy igény szerint jelentéseket generáljon.

Nyugodtan kísérletezz különböző kultúrákkal, egyedi számformátumokkal vagy tömeges adatimporttal. Boldog kódolást!

## Mit érdemes még megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket és lépésről‑lépésre magyarázatokat tartalmaz, hogy még jobban elsajátíthasd az API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Excel Workbook Initialization & Cell Styling using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/formatting/excel-workbook-initialization-cell-styling-aspose-cells-java/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}