---
category: general
date: 2026-08-08
description: Hogyan másoljuk a pivot táblát az Aspose.Cells-ben, és másoljunk tartományt
  munkafüzetbe Java használatával. Ismerje meg a pontos lépéseket a pivot tábla másolásához
  a CopyOptions segítségével.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range to workbook
- aspose.cells copy range
language: hu
lastmod: 2026-08-08
og_description: Hogyan másoljuk a pivot táblát az Aspose.Cells-ben, és hogyan másoljuk
  a tartományt egy munkafüzetbe Java-val. Kövesse ezt a teljes útmutatót a pivot tábla
  duplikálásához a CopyOptions használatával.
og_image_alt: Diagram showing how to copy pivot in Aspose.Cells
og_title: Hogyan másoljuk a pivot táblát az Aspose.Cells-ben – tartomány másolása
  munkafüzetbe
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  headline: How to copy pivot in Aspose.Cells – copy range to workbook
  type: TechArticle
- description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  name: How to copy pivot in Aspose.Cells – copy range to workbook
  steps:
  - name: Add Aspose.Cells to your project
    text: 'If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Configure copy options to include the pivot table
    text: '```java // Define copy options to include the pivot table in the copied
      range CopyOptions copyOptions = new CopyOptions() .setCopyPivotTable(true);
      ```'
  - name: Copy the desired range with the pivot table
    text: '```java // Copy the range A1:H20, preserving the pivot table workbook.getWorksheets().get(0).getCells()
      .copyRange("A1:H20", copyOptions); ```'
  - name: Save the modified workbook
    text: '```java // Save the workbook with the copied pivot table workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected result
    text: '* `output.xlsx` contains the same data as `input.xlsx`. * The pivot table
      that originally occupied the source range appears in the destination cells,
      fully functional (filters, refresh capability, etc.). * All cell formatting,
      formulas, and column widths are preserved because `copyRange` copies the '
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- CopyRange
title: Hogyan másoljuk a pivotot az Aspose.Cells-ben – tartomány másolása munkafüzetbe
url: /hu/java/excel-pivot-tables/how-to-copy-pivot-in-aspose-cells-copy-range-to-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan másoljuk a pivot táblát az Aspose.Cells‑ben – tartomány másolása munkafüzetbe

Ha **how to copy pivot**‑t szeretne egy Excel‑fájlban az Aspose.Cells használatával, ez az útmutató pontosan bemutatja a folyamatot. A tutorial végére képes lesz **copy range to workbook** műveletet végrehajtani a pivot tábla definíciójának megőrzésével.

A példa Java‑t használ, de ugyanazok a koncepciók alkalmazhatók bármely .NET nyelvre, amely az Aspose.Cells‑et támogatja. Nincs szükség külső eszközökre – csak az Aspose.Cells for Java könyvtárra és egy alap fejlesztői környezetre.

## Előfeltételek

Mielőtt elkezdené, győződjön meg róla, hogy rendelkezik:

* Java Development Kit (JDK) 8 vagy újabb verzióval.
* Maven vagy Gradle a függőségek kezeléséhez (a példában Maven‑t használunk).
* Aspose.Cells for Java 23.9 (vagy a legújabb verzió) a projektjéhez hozzáadva.
* Egy bemeneti munkafüzet (`input.xlsx`), amely legalább egy pivot táblát tartalmaz az első munkalapon.

Ezeknek az elemeknek a rendelkezésre állása megakadályozza a futásidejű hibákat, amikor a kód a munkafüzethez fér hozzá.

## Hogyan másoljuk a pivot táblát az Aspose.Cells‑szel

Ez a szakasz lépésről lépésre bemutatja, hogyan **how to copy pivot**‑t másolhatunk egy munkalap egy részéről a másikra a `CopyOptions` osztály segítségével.

### 1. lépés: Aspose.Cells hozzáadása a projekthez

Ha Maven‑t használ, adja hozzá a következő függőséget a `pom.xml`‑hez:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust JDK version as needed -->
</dependency>
```

*Miért fontos ez a lépés*: A könyvtár biztosítja a `Workbook`, `CopyOptions` és más osztályokat, amelyek a **aspose.cells copy range** műveletekhez szükségesek. Függőség nélkül a fordító nem tudja feloldani ezeket a típusokat.

### 2. lépés: A forrás munkafüzet betöltése

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

A fájl betöltése egy memóriában létező táblázat‑reprezentációt hoz létre. A `Workbook` objektum hozzáférést biztosít a munkalapokhoz, cellákhoz és pivot táblákhoz.

### 3. lépés: Másolási beállítások konfigurálása a pivot tábla megtartásához

```java
        // Define copy options to include the pivot table in the copied range
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);
```

A `CopyOptions.setCopyPivotTable(true)` azt mondja az Aspose.Cells‑nek, hogy a művelet megőrizze a pivot tábla metaadatait. Ha ezt a jelzőt kihagyja, a pivot tábla statikus adatokra redukálódik, elveszítve interaktivitását.

### 4. lépés: A kívánt tartomány másolása a pivot táblával együtt

```java
        // Copy the range A1:H20, preserving the pivot table
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);
```

A `copyRange` metódus másolja a cellákat, a formázást, és – a korábbi lépésben beállított opciók miatt – minden olyan pivot táblát, amely a tartományba esik. Ez a **copy range to workbook** funkció magja.

### 5. lépés: A módosított munkafüzet mentése

```java
        // Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

A mentés a változásokat egy új fájlba (`output.xlsx`) írja. Most már megnyithatja ezt a fájlt Excelben, és láthatja, hogy a pivot tábla pontosan ott lett duplikálva, ahová a tartományt másolta.

## Teljes, futtatható példa

Az összes részt összevonva, itt a komplett program, amelyet lefordíthat és futtathat:

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Define copy options to include the pivot table
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);

        // 3. Copy the range A1:H20 with the specified options
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);

        // 4. Save the modified workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### Várt eredmény

* Az `output.xlsx` ugyanazt az adatot tartalmazza, mint az `input.xlsx`.
* A pivot tábla, amely eredetileg a forrás tartományt foglalta, megjelenik a célcellákban, teljesen működőképes (szűrők, frissítési lehetőség stb.).
* Minden cellaformázás, képlet és oszlopszélesség megmarad, mivel a `copyRange` az egész cellablokkot másolja.

## Gyakori kérdések és szélhelyzetek

**Mi van, ha a cél tartomány átfed egy már létező pivot táblával?**  
Az Aspose.Cells felülírja a célcellákat. Az adatvesztés elkerülése érdekében győződjön meg róla, hogy a célterület üres, vagy előbb mozgassa el a meglévő pivot táblát.

**Másolhatok pivot táblát munkalapok között?**  
Igen. Használja a `workbook.getWorksheets().get(targetSheetIndex).getCells().copyRange(sourceRange, copyOptions);` kifejezést, ahol a `targetSheetIndex` a cél munkalap indexét jelöli.

**A `setCopyPivotTable(true)` másolja az adatforrást is?**  
A metódus csak a pivot cache hivatkozást másolja. Ha a forrásadat ugyanabban a munkafüzetben van, a cél pivot ugyanarra a cache‑re mutat. A cache duplikálásához manuálisan kell új pivot cache‑t létrehozni.

**Hogyan másoljak nagy tartományt hatékonyan?**  
Nagyon nagy tartományok másolásakor fontolja meg a `CopyOptions.setCopyFormula(true)` és `setCopyDataValidation(true)` használatát csak akkor, ha szükséges. Az opciók számának csökkentése javíthatja a teljesítményt.

## Tippek a megbízható **aspose.cells copy range** használathoz

* **Pro tipp:** Mindig hívja meg a `workbook.calculateFormula()`‑t a másolás után, ha a tartomány képleteket tartalmaz, amelyek a pivot cache‑re támaszkodnak.
* **Vigyázzon:** Rejtett munkalapokra. A `copyRange` csak látható munkalapokon működik, hacsak nem hivatkozik kifejezetten a rejtett lap indexére.
* **Verzió ellenőrzés:** A `setCopyPivotTable` jelző a Aspose.Cells 20.9‑től érhető el. Ellenőrizze, hogy a könyvtár verziója támogatja‑e.

## Összegzés

Most már tudja, **how to copy pivot**‑t használni az Aspose.Cells‑ben, és hogyan **copy range to workbook** úgy, hogy a pivot funkció teljes egészében megmarad. A lépések – a könyvtár hozzáadása, a munkafüzet betöltése, a `CopyOptions` beállítása, a másolás végrehajtása és a mentés – egy ismételhető mintát alkotnak, amelyet más másol‑beillesztési forgatókönyvekre is adaptálhat.

Ezután fedezze fel a kapcsolódó témákat, például a **aspose.cells copy range** diagramok, feltételes formázás és adatellenőrzés másolásához. Kísérletezzen különböző fájlformátumok (XLSX → XLS) közötti másolással, hogy bővítse automatizálási képességeit. Boldog kódolást!

## Mit érdemes még megtanulni?

A következő tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [Hogyan hozzunk létre pivot táblákat Excelben Aspose.Cells for Java‑val: Átfogó útmutató](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Hogyan frissítsük az Excel pivot tábla forrását Aspose.Cells for Java‑val: Átfogó útmutató](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Hogyan valósítsuk meg a szeletelőket pivot táblákban Aspose.Cells for Java‑val: Átfogó útmutató](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}