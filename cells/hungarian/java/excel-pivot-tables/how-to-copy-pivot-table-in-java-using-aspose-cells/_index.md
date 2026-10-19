---
category: general
date: 2026-07-06
description: Hogyan másolhatunk pivot táblát Java-ban az Aspose.Cells segítségével
  – lépésről lépésre útmutató az Excel pivot táblák programozott másolásához.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- duplicate excel pivot
language: hu
lastmod: 2026-07-06
og_description: Az Aspose.Cells használatával Java-ban a pivot tábla másolása lehetővé
  teszi, hogy gyorsan és megbízhatóan duplikálja az Excel pivot táblákat.
og_image_alt: Screenshot of Java code copying an Excel pivot table with Aspose.Cells
og_title: Hogyan másoljuk a pivot táblát Java-ban – Teljes Aspose.Cells útmutató
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
    to duplicate Excel pivot tables programmatically.
  headline: How to copy pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
title: Hogyan másoljuk a pivot táblát Java-ban az Aspose.Cells segítségével
url: /hu/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan másolhatunk pivot táblát Java-ban az Aspose.Cells használatával

Gondolkodtál már azon, **hogyan másolhatók a pivot** táblák egy Excel-fájlban a munkafüzet manuális megnyitása nélkül? Nem vagy egyedül. Sok jelentéskészítési folyamatban **másolni kell az Excel pivot** táblákat menet közben – akár egy pillanatfelvétel létrehozásához, egy új munkalapra való áthelyezéshez, vagy egy sablon generálásához a downstream felhasználók számára.

Ebben az útmutatóban egy teljes, futtatható példán keresztül mutatjuk be, hogyan lehet ezt megvalósítani. Az Aspose.Cells for Java könyvtár segítségével betöltünk egy munkafüzetet, megtaláljuk a forrás pivot tartományt, átmásoljuk egy új helyre, és elmentjük az eredményt. Nincs homályos hivatkozás, csak egy konkrét megoldás, amelyet már ma beilleszthetsz a projektedbe.

---

## Előfeltételek

* **Java Development Kit (JDK) 8+** – a kód bármely friss JDK-val lefordítható.
* **Aspose.Cells for Java** 25.11 vagy újabb verzió – a pivot táblákat támogató `Range.copy` metódus ebben a kiadásban került bevezetésre.
* Egy **input.xlsx** fájl, amely már tartalmaz egy pivot táblát (teszteléshez létrehozhatsz egyet az Excelben).
* A választott build eszközöd (Maven, Gradle vagy egyszerű `javac`). A gyors kezdéshez bemutatjuk a Maven függőséget.

```xml
<!-- Add this to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.12</version> <!-- Use the latest stable -->
</dependency>
```

---

## 1. lépés: A forrás munkafüzet betöltése

Az első lépés, hogy megnyissuk azt az Excel-fájlt, amely a eredeti pivot táblát tartalmazza. Az Aspose.Cells a munkafüzetet memóriában lévő objektumként kezeli, így manipulálhatod azt az Excel indítása nélkül.

```java
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

> **Miért fontos:** A munkafüzet betöltése hozzáférést biztosít a munkalapokhoz, cellákhoz, és ami még fontosabb, a pivot táblát támogató pivot cache-hez. Enélkül a lépés nélkül a könyvtárnak nincs mit másolnia.

---

## 2. lépés: A pivotot tartalmazó munkalap lekérése

Ha a munkafüzet több munkalappal rendelkezik, a megfelelőre kell mutatnod. Itt egyszerűen az első lapot veszük, de használhatod a `get("SheetName")` metódust is név alapján történő lekérdezéshez.

```java
// Obtain the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **Pro tipp:** Sok munkalappal dolgozva tedd az indexet vagy a nevet egy konfigurációs fájlba, hogy elkerüld a számok kemény kódolását.

---

## 3. lépés: A pivot táblát tartalmazó forrás tartomány meghatározása

A 25.11-es verziótól kezdve az Aspose.Cells lehetővé teszi, hogy a pivot táblát egy szokványos cellatartománynak tekintsd. Add meg a bal‑felső és jobb‑alsó cellákat, amelyek körülveszik a teljes pivotot.

```java
// The range A1:D20 covers the whole pivot table in this example
Range sourceRange = worksheet.getCells().createRange("A1:D20");
```

> **Szélsőséges eset:** Ha a pivot dinamikusan bővül (pl. később sorok kerülnek hozzáadásra), fontold meg a `worksheet.getPivotTables().get(0).getDataRange()` használatát a pontos tartomány programozott lekéréséhez.

---

## 4. lépés: A cél tartomány meghatározása, ahová a pivotot másolni kell

Válassz egy üres cellát, ahol a másolt pivot megjelenjen. Ebben a demóban a **F1**-től kezdünk, így az eredeti és a másolat között rés van.

```java
// Destination starts at cell F1 – adjust as needed
Range destinationRange = worksheet.getCells().createRange("F1");
```

> **Miért nem egy új munkalap?** Létrehozhatsz egy új munkalapot is (`workbook.getWorksheets().add("Copy")`), és annak celláit használhatod célként. Ugyanaz a `copy` metódus működik munkalapok között is.

---

## 5. lépés: A pivot tábla másolása az új helyre

Most jön a varázslat. A `copy` metódus klónozza a pivotot, annak cache-ét, formázását, sőt a kapcsolódó szeletelőket is (a legújabb verziótól kezdve).

```java
// Perform the copy – the pivot is now duplicated at the destination
sourceRange.copy(destinationRange);
```

> **Fontos:** A másolási művelet *mély*; **nem** hoz létre hivatkozást az eredeti pivotra. A új pivotot önállóan módosíthatod, anélkül, hogy a forrást befolyásolnád.

---

## 6. lépés: A munkafüzet mentése a másolt pivottal

Végül írjuk vissza a módosított munkafüzetet a lemezre. Felülírhatod az eredetit vagy létrehozhatsz egy új fájlt; itt a másodikat választjuk, hogy az eredeti érintetlen maradjon.

```java
// Save the workbook – the duplicated pivot lives in output.xlsx
workbook.save("YOUR_DIRECTORY/output.xlsx");
```

Amikor megnyitod a **output.xlsx**-t Excelben, az eredeti pivotot az A‑D oszlopokban, és egy tökéletes másolatot a F oszloptól kezdve fogod látni. Mindkét pivot külön-külön frissíthető.

---

## Teljes működő példa

Mindent összerakva, itt a teljes Java osztály, amelyet közvetlenül lefordíthatsz és futtathatsz:

```java
import com.aspose.cells.*;

public class ExportPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Define the source range that includes the pivot table (supported from version 25.11)
        // Adjust the range to match your actual pivot dimensions
        Range sourceRange = worksheet.getCells().createRange("A1:D20");

        // Step 4: Define the destination range where the pivot table will be copied
        // Change "F1" to any starting cell you prefer
        Range destinationRange = worksheet.getCells().createRange("F1");

        // Step 5: Copy the pivot table to the new location
        sourceRange.copy(destinationRange);

        // Step 6: Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Várható eredmény:** A `output.xlsx` megnyitása az eredeti pivotot (A1:D20) és egy azonos pivotot mutat a F1-től kezdve. Mindkét tábla megtartja a szűrőket, stílusokat és a számított mezőket.

---

## Gyakori változatok kezelése

| Situation | What to adjust |
|-----------|----------------|
| **Több pivot** ugyanazon a munkalapon | Iterálj a `worksheet.getPivotTables()`-en, és másold mindegyiket a saját cél tartományával. |
| **Dinamikus adat tartomány** | Használd a `worksheet.getPivotTables().get(0).getDataRange()`-t a forrás terület automatikus felismeréséhez. |
| **Másolás egy másik munkafüzetbe** | Tölts be egy második `Workbook` példányt, hozz létre egy cél munkalapot, majd hívd meg a `sourceRange.copy(destWorksheet.getCells().createRange("A1"))` metódust. |
| **Szeletelők megőrzése** | A 25.12-es verziótól kezdve a szeletelők automatikusan másolódnak, ha a tartomány tartalmazza őket. Ellenőrizd Excelben a mentés után. |

---

## Pro tippek és buktatók

* **Verzió ellenőrzés:** A pivotokat támogató `copy` metódus a **Aspose.Cells 25.11**‑ben került bevezetésre. Ha régebbi verziót használsz, kivételt kapsz. Mindig ellenőrizd az `aspose-cells` verziót a `pom.xml`‑ben.
* **Teljesítmény:** Nagy pivotok másolása memóriaigényes lehet. Ha csak az adatokat kell használnod, fontold meg a pivot exportálását egy lapos táblába a teljes objektum klónozása helyett.
* **Frissítési viselkedés:** A másolt pivot saját cache‑el rendelkezik. Ha módosítod az alapadatokat, hívd meg a `pivotTable.refresh()` metódust az új pivoton a újraszámításhoz.
* **Formázási sajátosságok:** Egyes egyedi számformátumok nem maradhatnak meg a másolás során nagyon régi Excel verziókban (<2007). Teszteld a célközönség Excel verziójával.

---

## Összegzés

Most már van egy átfogó, vég‑a‑vég megoldásod a **pivot táblák másolására** az Aspose.Cells for Java használatával, és láttad, hogyan **másolhatók az Excel pivot** táblák néhány kódsorral. A megközelítés működik egy vagy több pivot esetén, munkalapok között, sőt munkafüzetek között is.

Az elkövetkező lépések lehetnek:

* A másolás automatizálása minden pivotra egy kötegelt feladatban.
* Kód hozzáadása a másolt pivot átnevezéséhez (pl. `pivotTable.setName("Copy_of_Sales")`).
* A rutin integrálása egy nagyobb jelentéskészítő szolgáltatásba, amely PDF‑eket vagy CSV‑exportokat generál.

Próbáld ki, állítsd be a tartományokat a saját adataidhoz, és hagyd, hogy a könyvtár végezze a nehéz munkát. Boldog kódolást!

## Mit érdemes legközelebb megtanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Hogyan hozzunk létre pivot táblákat Excelben az Aspose.Cells for Java&#58; Átfogó útmutató](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Excel pivot tábla manipuláció Aspose.Cells Java&#58; Átfogó útmutató](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [Hogyan frissítsük az Excel pivot tábla forrását az Aspose.Cells for Java&#58; Átfogó útmutató](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}