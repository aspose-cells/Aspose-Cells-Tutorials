---
category: general
date: 2026-09-11
description: Új munkalap létrehozása és Excel-tartomány másolása az Aspose.Cells használatával.
  Tanulja meg, hogyan másolhat tartományt munkalapok között a pivot táblák megőrzése
  mellett.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new worksheet
- copy excel range
- copy range between sheets
- copy range aspose.cells
language: hu
lastmod: 2026-09-11
og_description: Új munkalap létrehozása és Excel-tartomány másolása az Aspose.Cells
  segítségével. Ez az útmutató pontos lépéseket mutat be a tartomány másolásához a
  munkalapok között, miközben a kimutatások érintetlenek maradnak.
og_image_alt: Screenshot of a Java IDE showing code that creates a new worksheet and
  copies an Excel range
og_title: Új munkalap létrehozása és Excel-tartomány másolása – Aspose.Cells útmutató
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Create new worksheet and copy Excel range using Aspose.Cells. Learn
    how to copy range between sheets while preserving pivot tables.
  headline: Create new worksheet and copy Excel range with Aspose.Cells
  type: TechArticle
- questions:
  - answer: The `copy` method also copies merge information, so merged cells appear
      unchanged on the destination sheet.
    question: What if the source range contains merged cells?
  - answer: Yes. Load a second `Workbook` instance, create a destination range in
      that workbook, and call `sourceRange.copy(destinationRange)`. The method handles
      cross‑workbook copying automatically.
    question: Can I copy to a different workbook?
  - answer: The copy operation overwrites any existing cells that intersect the destination
      range. To avoid data loss, ensure the destination area is empty or use a different
      start cell (e.g., `"B2"`).
    question: What if the destination sheet already has data?
  - answer: Aspose.Cells reuses the original pivot cache, which means the new pivot
      table remains linked to the same source data. If you need an independent cache,
      you must recreate the pivot table after copying.
    question: Is the pivot cache duplicated?
  type: FAQPage
tags:
- Aspose.Cells
- Excel automation
- Java
title: Új munkalap létrehozása és Excel-tartomány másolása az Aspose.Cells segítségével
url: /hu/java/range-management/create-new-worksheet-and-copy-excel-range-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Új munkalap létrehozása és Excel tartomány másolása az Aspose.Cells segítségével

Ha **új munkalapot kell létrehozni** és adatokat mozgatni egy Excel fájlban, az Aspose.Cells egyszerűvé teszi. Ez az útmutató pontosan bemutatja, hogyan másolhatunk egy Excel tartományt az egyik lapról a másikra, miközben megőrzik a tartományon belüli pivot táblákat.

Megtanulja, hogyan **copy excel range**, hogyan **copy range between sheets**, és miért tartja meg az Aspose.Cells `copy` metódusa a pivot tábla definíciókat érintetlenül. Nem szükséges külső eszköz—csak egy Java projekt az Aspose.Cells könyvtárral.

## Előkövetelmények

- Java 17 vagy újabb telepítve
- Aspose.Cells for Java (23.12 vagy újabb verzió) hozzáadva a projekt osztályútvonalához
- Egy forrás munkafüzet (`input.xlsx`), amely tartalmaz pivot táblát a másolni kívánt tartományban
- Alapvető ismeretek a Java szintaxisról és a Maven/Gradle függőségkezelésről

## 1. lépés: A projekt beállítása és az Aspose.Cells importálása

Hozzon létre egy egyszerű Maven projektet (vagy Gradle-t, ha azt részesíti előnyben), és adja hozzá az Aspose.Cells függőséget:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

Ezután importálja a szükséges osztályokat a Java forrásfájlban:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

*Miért fontos ez a lépés*: A megfelelő osztályok importálása hozzáférést biztosít a `Workbook`, `Worksheet`, `Range` és a `copy` metódushoz, amely a tartomány átvitelét kezeli.

## 2. lépés: A forrás munkafüzet betöltése

Nyissa meg a munkafüzetet, amely a másolni kívánt adatokat tartalmazza. Az alábbi kód betölti a `input.xlsx` fájlt egy megadott könyvtárból:

```java
public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Magyarázat*: A `Workbook` az egész Excel fájlt képviseli. Egyszeri betöltése olvasási/írási hozzáférést biztosít minden laphoz és cellagyűjteményhez.

## 3. lépés: A pivot táblát tartalmazó forrás tartomány azonosítása

Válassza ki azt a munkalapot, amely a pivot táblát tartalmazza, és határozza meg a pontos cellatartományt, amelyet másolni szeretne. Ebben a példában az A1‑től D20‑ig terjedő cellákat másoljuk:

```java
        // Get the first worksheet (index 0) that contains the pivot table
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the source range – this range includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");
```

*Miért fontos*: A `Range` objektum létrehozásával pontosan megmondja az Aspose.Cells-nek, mely cellákat (beleértve a beágyazott objektumokat, például a pivot táblákat) kell duplikálni.

## 4. lépés: **Új munkalap létrehozása**, amely a másolt adatokat fogadja

Most egy új lapot adunk hozzá ugyanahhoz a munkafüzethez. Itt jelenik meg a fő kulcsszó:

```java
        // Create a new worksheet named "Copy"
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // Define the top‑left cell of the destination range
        Range destinationRange = destinationSheet.getCells().createRange("A1");
```

*Magyarázat*: Új lap hozzáadása elkülöníti a másolt adatokat, így könnyen ellenőrizhető, hogy a **copy excel range** művelet sikeres volt-e, anélkül hogy az eredeti lapot befolyásolná.

## 5. lépés: Tartomány másolása – a pivot tábla automatikusan megmarad

Használja a `copy` metódust a tartomány áthelyezéséhez a forráslapról a cél lapra. Az Aspose.Cells másolja a képleteket, a formázást és a pivot‑tábla definíciókat:

```java
        // Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);
```

*Miért működik*: A `copy` metódus mélymásolatot készít a forráscellákról. Nem csak az értékeket másolja, hanem az egész cellastruktúrát, amely tartalmazza a pivot gyorsítótárat is. Ezért használhatja a **copy range aspose.cells** kifejezést, és még mindig működő pivot táblát lát az új lapon.

## 6. lépés: A munkafüzet mentése az új munkalappal

Végül írja a módosított munkafüzetet a lemezre:

```java
        // Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

*Eredmény*: A `output.xlsx` most már tartalmazza az eredeti lapot és egy **Copy** nevű új lapot, amely pontosan ugyanazt a tartományt, a pivot táblát is tartalmazza.

## Teljes működő példa

Az összes részt összeállítva, itt a teljes, futtatható program:

```java
import com.aspose.cells.*;
import java.io.IOException;

public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table and define the source range
        Worksheet sourceSheet = workbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");

        // Step 3: Create a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
        Range destinationRange = destinationSheet.getCells().createRange("A1");

        // Step 4: Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);

        // Step 5: Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Várt kimenet**: Nyissa meg az `output.xlsx` fájlt Excelben. Látni fog egy **Copy** nevű lapot, amelynek A1:D20 cellái ugyanazt az adatot, formázást és egy aktív pivot táblát tartalmaznak, amely az eredetivel azonos.

## Gyakori kérdések és szélhelyzetek

- **Mi van, ha a forrás tartomány egyesített cellákat tartalmaz?**  
  A `copy` metódus másolja az egyesítési információkat is, így az egyesített cellák változatlanul jelennek meg a cél lapon.

- **Másik munkafüzetbe is másolhatok?**  
  Igen. Töltsön be egy második `Workbook` példányt, hozza létre a cél tartományt abban a munkafüzetben, és hívja a `sourceRange.copy(destinationRange)` metódust. A metódus automatikusan kezeli a munkafüzetek közötti másolást.

- **Mi van, ha a cél lap már tartalmaz adatokat?**  
  A másolási művelet felülírja a cél tartományba ütköző meglévő cellákat. Az adatvesztés elkerülése érdekében győződjön meg róla, hogy a cél terület üres, vagy használjon más kezdőcellát (pl. `"B2"`).

- **Megkettőződik a pivot gyorsítótár?**  
  Az Aspose.Cells újrahasználja az eredeti pivot gyorsítótárat, ami azt jelenti, hogy az új pivot tábla továbbra is ugyanahhoz a forrásadatokhoz kapcsolódik. Ha független gyorsítótárra van szüksége, a másolás után újra kell hoznia a pivot táblát.

## Tippek és bevált gyakorlatok

- **Pro tipp**: Használja a `Workbook.setForceFormulaRecalculation(true)` metódust mentés előtt, ha a tartomány olyan képleteket tartalmaz, amelyek a másolt blokkon kívüli adatoktól függenek.
- **Figyeljen** a nagy tartományokra: hatalmas lapok másolása jelentős memóriát fogyaszthat. Fontolja meg a kisebb darabokban történő másolást, ha `OutOfMemoryError`-t kap.
- **Teljesítmény tipp**: Tiltsa le a képernyő frissítését (`workbook.getSettings().setCalculateFormulaOnOpen(false)`) nagyon nagy fájlok esetén a másolási folyamat felgyorsítása érdekében.

## Következtetés

Most már tudja, hogyan **create new worksheet** és **copy excel range** hajthat végre lapok között az Aspose.Cells segítségével, megőrizve a pivot táblákat és minden cellajellemzőt. Ez a technika lehetővé teszi, hogy programozottan duplikáljon adatblokkokat, jelentés sablonokat építsen, vagy munkafüzeteket átszervezzen manuális másolás‑beillesztés nélkül.

Ezután fedezze fel a kapcsolódó témákat, például a **copy range aspose.cells** kereszt‑munkafüzet műveletekhez, a pivot‑táblák frissítésének automatizálását, vagy a másolt lap PDF‑be exportálását. Kísérletezzen különböző forrás tartományokkal és lapnevekkel, hogy megfeleljenek az adott automatizálási forgatókönyvének. Boldog kódolást!

## Mit érdemes következőként megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeiben.

- [Copy Shapes Between Excel Sheets Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/images-shapes/copy-shapes-between-sheets-aspose-cells-dotnet/)
- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}