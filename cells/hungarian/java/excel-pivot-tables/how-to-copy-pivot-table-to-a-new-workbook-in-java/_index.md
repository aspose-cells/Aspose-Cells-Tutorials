---
category: general
date: 2026-10-26
description: Tanulja meg, hogyan másolhatja a pivot táblát egy új munkafüzetbe Java
  segítségével, megőrizve a formázást és a pivot definíciót, miközben az Excel-tartományt
  formázással másolja az Aspose.Cells segítségével.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- create empty workbook
- copy range with formatting
language: hu
lastmod: 2026-10-26
og_description: Pivot tábla másolása új munkafüzetbe Java-ban az Aspose.Cells segítségével.
  Ez az útmutató bemutatja, hogyan másolhatja az Excel-tartományt, megőrizheti a formázást,
  és hatékonyan hozhat létre üres munkafüzetet.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new Excel
  workbook
og_title: Pivot tábla másolása új munkafüzetbe Java-ban – lépésről‑lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  headline: How to copy pivot table to a new workbook in Java
  type: TechArticle
- description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  name: How to copy pivot table to a new workbook in Java
  steps:
  - name: Prerequisites
    text: '* Java 17 or later. * Aspose.Cells for Java (version 23.10 or newer). *
      Basic familiarity with Java IDEs (IntelliJ IDEA, Eclipse, etc.).'
  - name: Why this works
    text: '* `new Workbook()` **creates empty workbook** with a default sheet, avoiding
      the need to delete existing data. * `CopyOptions` tells Aspose.Cells to copy
      **pivot table** metadata, not just raw values. The `PASTE_ALL` mode also carries
      cell styles, number formats, and conditional formatting—fulfillin'
  - name: Edge cases to consider
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Source workbook has multiple pivots | Copy each pivot’s range separately or
      copy the whole sheet. | | Destination already contains data | Choose a non‑conflicting
      start cell (e.g., "H1") when cal'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Hogyan másolhatunk pivot táblát egy új munkafüzetbe Java-ban
url: /hu/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan másoljuk a pivot táblát egy új munkafüzetbe Java‑ban

Ha **pivot táblát** kell másolni egy Excel‑fájlból a másikba, ez az útmutató egy teljes, futtatható megoldást mutat be. Megtudja, hogyan őrizze meg a pivot definíciót, tartsa meg az összes formázást, és kerülje el a gyakori buktatókat egy Excel‑tartomány másolásakor.

A pivot táblák másolása gyakran felveti a kérdést, hogy *hogyan másoljuk a pivot‑t* anélkül, hogy megsértenénk az adatforrást vagy elveszítenénk a stílusokat. A tutorial végére egy önálló Java‑programmal rendelkezik, amely létrehoz egy üres munkafüzetet, átmásolja a kívánt tartományt, és elmenti az eredményt a pivot érintetlenül hagyásával.

## Amit el fog érni

* Betölt egy forrásmunkafüzetet, amely tartalmaz egy pivot táblát.  
* **Üres munkafüzet létrehozása**, amely a másolt adatokat fogja fogadni.  
* **Excel tartomány másolása**, amely magában foglalja a pivot‑t, a formázást megtartó beállításokkal.  
* A célfájl mentése és annak ellenőrzése, hogy a pivot pontosan úgy működik, mint az eredeti.

### Előfeltételek

* Java 17 vagy újabb.  
* Aspose.Cells for Java (23.10 vagy újabb verzió).  
* Alapvető ismeretek Java IDE‑kről (IntelliJ IDEA, Eclipse stb.).  

> **Pro tip:** Használja az ingyenes Aspose.Cells értékelő licencet a gyors teszteléshez; a termelésben cserélje le egy teljes licencre.

## Pivot tábla másolása egy új munkafüzetbe

Az első lépés a forrás- és célmunkafüzetek beállítása. A célmunkafüzet egy **üres munkafüzet létrehozása** hívással indul, amely egy tiszta fájlt ad egyetlen munkalappal.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Create an empty workbook that will receive the copied range
        Workbook destWb = new Workbook();

        // Get the first worksheet from each workbook
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        Worksheet destSheet = destWb.getWorksheets().get(0);

        // Configure copy options to preserve the pivot table and formatting
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // ensures pivot and styles are kept

        // Copy the range that contains the pivot table
        srcSheet.getCells().copyRange("A1:D20", destSheet.getCells(), "A1", copyOptions);

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
    }
}
```

### Miért működik ez

* `new Workbook()` **üres munkafüzetet hoz létre** egy alapértelmezett lappal, elkerülve a meglévő adatok törlésének szükségességét.  
* A `CopyOptions` azt mondja az Aspose.Cells‑nek, hogy másolja a **pivot táblát** metaadataival, nem csak a nyers értékeket. A `PASTE_ALL` mód továbbá a cellastílusokat, számformátumokat és feltételes formázást is átviszi – ezzel teljesül a **tartomány másolása formázással** követelmény.  
* A `copyRange` egy **excel tartomány másolása** műveletet hajt végre, amely tiszteletben tartja a forrás belső struktúráit, így a pivot a másolás után is működőképes marad.

## Pivot másolása formázás elvesztése nélkül

Ha csak az alapértelmezett `CopyOptions`‑t használja, egyes stílusinformációk elmaradhatnak a régebbi Aspose.Cells verziókban. A beillesztési típus kifejezett beállítása garantálja, hogy a **tartomány másolása formázással** betartásra kerüljön.

```java
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);          // copy values, formulas, formats
copyOptions.setPasteSpecialType(PasteSpecialType.ALL); // include column widths and row heights
```

A `setPasteSpecialType` hozzáadása biztosítja, hogy az oszlopszélességek, sormagasságok és még az adatérvényesítési szabályok is a tartománnyal együtt kerüljenek át. Ez különösen hasznos, ha a pivot tábla több oszlopot fed le egyedi szélességekkel.

## Üres munkafüzet létrehozása másolás előtt

Néha a fejlesztők egy már létező, adatot tartalmazó munkafüzetbe próbálnak másolni. Ez átfedő tartományokat vagy váratlan felülírásokat okozhat. Egy **üres munkafüzet létrehozása** hívással kezdve a művelet izolálva van:

```java
Workbook destWb = new Workbook(); // fresh file with one sheet
Worksheet destSheet = destWb.getWorksheets().get(0); // reference the clean sheet
```

Ha a célmunkafüzetben több lapra van szükség, a másolás után hozzáadhatja őket:

```java
destWb.getWorksheets().add("Summary");
```

## Excel tartomány másolása formázással a CopyOptions használatával

A pivot táblákon túl ugyanaz a minta minden **excel tartomány másolása** esetén működik, ahol a formázás megőrzése szükséges – diagramok, táblázatok vagy feltételes formázások.

```java
// Example: copy a styled table from A1 to G15
srcSheet.getCells().copyRange("A1:G15", destSheet.getCells(), "A1", copyOptions);
```

A `CopyOptions` példány változatlan marad, így konzisztens viselkedést kapunk a különböző tartományoknál.

### Figyelembe veendő széljegyek

| Helyzet                                 | Ajánlott kezelés |
|----------------------------------------|------------------|
| A forrásmunkafüzet több pivot‑t tartalmaz | Minden pivot tartományát külön-külön másolja, vagy másolja az egész munkalapot. |
| A célmunkafüzet már tartalmaz adatot    | Válasszon egy nem ütköző kezdőcellát (pl. "H1") a `copyRange` hívásakor. |
| A pivot adatforrása külső (pl. DB)       | Győződjön meg róla, hogy a célmunkafüzet ugyanarra a külső adatforrásra mutat, vagy frissítse a pivot‑t a másolás után. |
| Nagy munkafüzet (> 10 MB)               | Növelje a Java heap méretét (`-Xmx2g`) az `OutOfMemoryError` elkerülése érdekében. |

## Az eredmény ellenőrzése

A program futtatása után nyissa meg a `destination.xlsx` fájlt. Ennek a következőket kell mutatnia:

* Ugyanaz a pivot tábla elrendezés, mint a `source.xlsx`‑ben.  
* Minden cellaszín, számformátum és oszlopszélesség megmaradt.  
* A pivot adatforrása továbbra is az új fájlban lévő eredeti adat tartományra mutat, így a pivot frissítésekor az értékek helyesen frissülnek.

Ha a pivot statikus táblaként jelenik meg, ellenőrizze, hogy a `CopyOptions.setPasteType(PasteType.PASTE_ALL)` be van-e állítva. Ennek hiányában az Aspose.Cells a pivot‑t egyszerű adatként kezeli.

## Összegzés

Most már tudja, hogyan **másolja a pivot táblát** egy új munkafüzetbe Java‑ban, miközben megőrzi a formázást, az adatkapcsolatokat és a lapelrendezést. A teljes megoldás bemutatja egy forrásfájl betöltését, **üres munkafüzet létrehozását**, a **excel tartomány másolása** beállításait, és az eredmény mentését.  

Innen tovább felfedezheti a kapcsolódó témákat, például a **pivot másolása** különböző munkalapok között, diagramok beágyazását a pivotok mellé, vagy több munkafüzet kötegelt feldolgozását. Kísérletezzen a `CopyOptions` beállításaival, hogy a saját automatizálási igényeihez igazítsa, és egy robusztus Excel‑kezelő eszköztárat kapjon a kezébe.

## Mit érdemes még tanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket és lépésről‑lépésre magyarázatot tartalmaz, hogy segítsen elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [Create New Workbook in Java – Full Guide to Copy Pivot Table](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Copy Pivot Table Between Workbooks – Step‑by‑Step Java Guide](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)
- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}