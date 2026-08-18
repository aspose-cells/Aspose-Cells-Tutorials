---
category: general
date: 2026-08-17
description: Hogyan duplikáljunk munkalapot Java-ban az Aspose.Cells használatával,
  megőrizve a pivot táblát, a pivot másolása egy új munkafüzetbe, és munkafüzet létrehozása
  egy lapból.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate worksheet
- how to copy pivot
- how to preserve pivot
- copy pivot to workbook
- create workbook from sheet
language: hu
lastmod: 2026-08-17
og_description: Hogyan duplikáljuk a munkalapot Java-ban az Aspose.Cells használatával,
  megőrizve a pivot táblát, a pivot átmásolása egy új munkafüzetbe, és egy munkafüzet
  létrehozása egy lapból – minden lépés részletesen.
og_image_alt: Screenshot of Java code duplicating an Excel worksheet with a pivot
  table using Aspose.Cells
og_title: Hogyan duplikáljunk munkalapot és tartsuk meg a pivot táblákat – Java útmutató
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  headline: How to duplicate worksheet and preserve pivot tables in Java
  type: TechArticle
- description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  name: How to duplicate worksheet and preserve pivot tables in Java
  steps:
  - name: – Load the workbook that contains the pivot table
    text: '```java import com.aspose.cells.*;'
  - name: – Create a new workbook and duplicate the entire worksheet
    text: '```java // Create an empty destination workbook Workbook destinationWorkbook
      = new Workbook();'
  - name: – Save the new workbook
    text: '```java // Save the duplicated workbook; the pivot remains functional destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
      } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
- Workbook
title: Munkalap duplikálása és pivot táblák megőrzése Java-ban
url: /hu/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan duplikáljunk munkalapot és megőrizzük a pivot táblákat Java-ban

A munkalap duplikálása, miközben a pivot tábla érintetlen marad, gyakori igény az Excel jelentések automatizálásakor. Ez az útmutató bemutatja, hogyan másolhatja a pivotot egy új munkafüzetbe az Aspose.Cells for Java használatával, valamint azt is, hogyan őrizheti meg a pivotot, amikor egy munkafüzetet hoz létre egy munkalapról.

Megtanulja, hogyan töltsön be egy meglévő munkafüzetet, duplikálja azt a munkalapot, amely pivot táblát tartalmaz, és mentse az eredményt egy új fájlként. Az útmutató feltételezi, hogy rendelkezik egy alap Java fejlesztői környezettel és egy érvényes Aspose.Cells licenccel (az ingyenes értékelő verzió teszteléshez megfelelő). Nem szükséges külső eszköz az Aspose.Cells JAR-on kívül.

## Előfeltételek

* Java Development Kit (JDK) 8 vagy újabb.
* Maven vagy Gradle az Aspose.Cells függőség kezeléséhez.
* Egy Excel fájl (`source.xlsx`), amely legalább egy pivot táblát tartalmaz az első munkalapon.
* Egy könyvtár, ahol olvashatja a forrásfájlt és írhatja a duplikált munkafüzetet.

Adja hozzá az Aspose.Cells függőséget a `pom.xml` (Maven) vagy `build.gradle` (Gradle) fájlhoz. Maven esetén:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

## Hogyan duplikáljunk munkalapot pivot táblával

A fő művelet egy háromlépéses folyamat: betöltés, másolás és mentés. Az egyes lépéseket alább részletezzük.

### 1. lépés – A pivot táblát tartalmazó munkafüzet betöltése

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceWorksheet = sourceWorkbook.getWorksheets().get(0);
```

*Miért fontos ez a lépés*: A `Workbook` objektum az egész Excel fájlt képviseli. Az első munkalap (`get(0)`) lekérdezésével a pivot táblát tartalmazó lapra céloz, amelyet duplikálni kíván.

### 2. lépés – Új munkafüzet létrehozása és a teljes munkalap duplikálása

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // Duplicate the source worksheet, preserving its pivot table
        destinationWorkbook.getWorksheets().addCopy(sourceWorksheet);
```

`addCopy` klónozza a munkalapot **beleértve** az összes beágyazott objektumot, képletet és pivot gyorsítótárat. Ez a javasolt mód a **how to copy pivot**, mivel a pivot definíció és adatforrása együtt kerül átvitelre.

### 3. lépés – Az új munkafüzet mentése

```java
        // Save the duplicated workbook; the pivot remains functional
        destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
    }
}
```

A futtatás után a `copy_with_pivot.xlsx` pontos másolatát tartalmazza az eredeti munkalapnak, és a pivot tábla további beállítások nélkül működik.

**Várt eredmény**: A `copy_with_pivot.xlsx` megnyitása Excelben a duplikált munkalapot mutatja, amely ugyanazzal a pivot elrendezéssel, szűrőkkel és számított mezőkkel rendelkezik, mint a forrásfájl.

## Hogyan másoljuk a pivotot egy másik munkafüzetbe

Ha a pivot táblát a teljes munkalap másolása nélkül szeretné áthelyezni, kinyerheti a pivot gyorsítótárat és egy új munkalaphoz csatolhatja. Az alábbi kódrészlet ezt a megközelítést mutatja be:

```java
// Assume sourceWorkbook and sourceWorksheet are already loaded
PivotTable pivot = sourceWorksheet.getPivotTables().get(0);

// Create a new workbook and a blank worksheet
Workbook targetWorkbook = new Workbook();
Worksheet targetSheet = targetWorkbook.getWorksheets().add("PivotCopy");

// Import the pivot table definition
targetSheet.getPivotTables().addCopy(pivot);
targetWorkbook.save("YOUR_DIRECTORY/pivot_only_copy.xlsx");
```

Ez a kód megválaszolja a **how to copy pivot** kérdést úgy, hogy csak a pivot objektumot másolja, nem a teljes munkalapot. A `PivotTables` gyűjteményen lévő `addCopy` metódus biztosítja a pivot gyorsítótár duplikálását, megfelelve a **how to preserve pivot** követelményeknek.

## Hogyan őrizzük meg a pivotot munkafüzet létrehozásakor egy munkalapról

Néha egy olyan munkalappal kezd, amely nem tartozik munkafüzethez (például memóriában generál egy lapot). A **create workbook from sheet** elvégzéséhez a pivot megtartásával kövesse az alábbi lépéseket:

```java
// Create a worksheet in memory
Worksheet tempSheet = new Worksheet();
PivotTable pivot = tempSheet.getPivotTables().add("A1", "B10", "MyPivot");

// Configure the pivot source range, rows, columns, data fields, etc.
// (Omitted for brevity – see Aspose.Cells docs for detailed setup)

// Wrap the worksheet in a new workbook
Workbook newWorkbook = new Workbook();
newWorkbook.getWorksheets().addCopy(tempSheet);
newWorkbook.save("YOUR_DIRECTORY/created_from_sheet.xlsx");
```

A munkalap egy új `Workbook`-ba való hozzáadásával, miután a pivot teljesen definiálva van, garantálja, hogy a **how to preserve pivot** működik még akkor is, ha a munkalap egy meglévő fájlon kívül keletkezett.

## Gyakorlati tippek és gyakori buktatók

| Tip | Why it matters |
|-----|----------------|
| Használja az `addCopy`-t a `copy` helyett | `addCopy` klónozza az alapszintű pivot gyorsítótárat; egy egyszerű `copy` elveszítheti a kapcsolatot az adatforrással. |
| Tartsa a forrás- és célfájlokat ugyanazon a fájlrendszeren | A pivot adatforrásának relatív útvonalai helyesen feloldódnak, csökkentve a „source not found” hibákat. |
| Ellenőrizze a pivot gyorsítótárát a másolás után | Hívja a `pivot.refresh()`-t, ha a forrásadat megváltozott a másolás és a mentés művelete között. |
| Szabadítsa fel a munkafüzeteket a használat után | `sourceWorkbook.dispose();` felszabadítja a natív erőforrásokat, ami nagy fájlok esetén fontos. |

## Olyan szélhelyzetek, amelyekkel találkozhat

* **Több munkalap egymástól függő pivotokkal** – Másolja minden munkalapot külön-külön; a megosztott gyorsítótárak automatikusan duplikálódnak, de előfordulhat, hogy újra kell rendelni a külső adatkapcsolatokat.
* **Külső SQL lekérdezéseken alapuló pivot táblák** – Győződjön meg arról, hogy a célkörnyezet eléri ugyanazt az adatbázist; ellenkező esetben a pivot “#REF!” hibákat fog mutatni.
* **Nagy munkafüzetek (>100 MB)** – Használja a `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`-t a memória terhelés csökkentésére a másolási művelet során.

## Teljes, futtatható példa

Az alábbiakban a teljes program látható, amely tartalmazza az összes megvitatott lépést. Mentse `CopyPivotTable.java` néven, módosítsa a fájl útvonalakat, és futtassa a kedvenc IDE-jével vagy a `javac`/`java` parancsokkal.



## Mit tanuljon meg legközelebb?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek az ebben az útmutatóban bemutatott technikákra épülnek. Minden forrás teljes működő kódpéldákat tartalmaz lépésről lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeiben.

- [Hogyan hozzunk létre pivot táblákat Excelben az Aspose.Cells for Java használatával: átfogó útmutató](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Hogyan frissítsük az Excel pivot tábla forrását az Aspose.Cells for Java használatával: átfogó útmutató](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Hogyan valósítsuk meg a szeletelőket pivot táblákban az Aspose.Cells for Java használatával: átfogó útmutató](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}