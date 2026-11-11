---
category: general
date: 2026-10-16
description: Hogyan másoljuk a pivot táblát Java-ban az Aspose.Cells segítségével
  – tanulja meg, hogyan másoljon tartományt egy másik munkalapra, és hatékonyan másoljon
  tartományt munkalapok között.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to another sheet
- copy range between worksheets
language: hu
lastmod: 2026-10-16
og_description: Hogyan másolhatunk pivot táblát Java-ban az Aspose.Cells használatával.
  Ez az útmutató megmutatja, hogyan másolhatunk tartományt egy másik munkalapra, valamint
  hogyan másolhatunk tartományt munkalapok között teljes kóddal.
og_image_alt: Diagram illustrating how to copy pivot table from one worksheet to another
  in Java
og_title: Hogyan másoljunk pivot táblát munkalapok között Java‑ban – lépésről‑lépésre
  útmutató
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  headline: How to copy a pivot table between worksheets in Java
  type: TechArticle
- description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  name: How to copy a pivot table between worksheets in Java
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Locate the source range that contains the pivot table
    text: '```java // The first worksheet (index 0) holds the pivot table. Worksheet
      sourceSheet = workbook.getWorksheets().get(0);'
  - name: Define the destination range on another sheet
    text: '```java // The second worksheet (index 1) will receive the copied pivot
      table. Worksheet destSheet = workbook.getWorksheets().get(1);'
  - name: Copy the source range while preserving the pivot table
    text: '```java // Configure copy options to keep all formatting, formulas, and
      pivot data. CopyOptions copyOptions = new CopyOptions(); copyOptions.setPasteType(PasteType.PASTE_ALL);
      // copies everything copyOptions.setSkipEmptyRows(false); copyOptions.setSkipEmptyColumns(false);'
  - name: Save the workbook and verify the result
    text: '```java // Save the modified workbook to a new file. workbook.save("output.xlsx");
      System.out.println("Pivot table copied successfully."); } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- Excel automation
title: Hogyan másolhatunk pivot táblát munkalapok között Java‑ban
url: /hu/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan másoljon pivot táblát munkalapok között Java-ban

Ha **hogyan másoljon pivot táblát** egy munkalapról a másikra ugyanabban a munkafüzetben, ez az útmutató egy teljes, azonnal futtatható megoldást nyújt. Megmutatjuk, hogyan másolja a pivot táblát tartalmazó forrás tartományt, hogyan őrizze meg a funkcióját, és hogyan ellenőrizze az eredményt – mindezt az Aspose.Cells for Java használatával.

Pivot tábla másolása gyakori feladat, amikor programozottan generál jelentéseket, és a helyes eljárás megakadályozza a pivot gyorsítótár elvesztését vagy a képletek megszakadását. A tutorial végére képes lesz **tartomány másolására egy másik munkalapra** és **tartomány másolására munkalapok között** manuális lépések nélkül.

## Mit fog megtanulni

* Egy meglévő pivot táblát tartalmazó Excel fájl betöltése.
* A pivot táblát tartalmazó forrás tartomány meghatározása.
* Cél tartomány meghatározása egy másik munkalapon.
* `CopyOptions` használata a pivot tábla érintetlen megtartásához.
* Ellenőrizze, hogy a másolt pivot tábla a várt módon működik.

**Előfeltételek**

* Java 17 vagy újabb.
* Aspose.Cells for Java (23.12 vagy újabb verzió).
* Egy Excel fájl (`input.xlsx`), amely az első munkalapon pivot táblát tartalmaz.

---

## Pivot tábla másolása Aspose.Cells segítségével

A művelet központja egy négylépéses folyamat: a munkafüzet betöltése, a forrás tartomány megtalálása, a cél tartomány beállítása és a másolás végrehajtása. Az alábbiakban minden lépést részletesen magyarázunk.

### 1. lépés: A munkafüzet betöltése

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the original pivot table
        Workbook workbook = new Workbook("input.xlsx");
```

*Miért ez a lépés?*  
A munkafüzet betöltése a teljes fájlt a memóriába helyezi, így hozzáférhet a munkalapokhoz, cellákhoz és a pivot gyorsítótárhoz. Az Aspose.Cells automatikusan olvassa a fájlformátumot, így nem kell aggódnia a `.xls` és `.xlsx` közti különbség miatt.

### 2. lépés: A pivot táblát tartalmazó forrás tartomány megtalálása

```java
        // The first worksheet (index 0) holds the pivot table.
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the exact area that includes the pivot table.
        // Adjust the address if your pivot table spans a different range.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*Miért ez a lépés?*  
A pivot tábla egy cellablokkban tárolódik, amely egy rejtett gyorsítótárra is hivatkozik. A pontos tartomány (`A1:G20` ebben a példában) kiválasztásával biztosítja, hogy a másolás során a gyorsítótár kapcsolata megmarad.

### 3. lépés: Cél tartomány meghatározása egy másik munkalapon

```java
        // The second worksheet (index 1) will receive the copied pivot table.
        Worksheet destSheet = workbook.getWorksheets().get(1);

        // Destination starts at cell A1 of the second sheet.
        Range destRange = destSheet.getCells().createRange("A1");
```

*Miért ez a lépés?*  
Cél kiválasztása egy másik munkalapon lehetővé teszi a **tartomány másolását egy másik munkalapra**. A bal‑felső cella (`A1`) gyakori kiindulási pont, de a címet módosítva bárhová elhelyezhető.

### 4. lépés: A forrás tartomány másolása a pivot tábla megőrzésével

```java
        // Configure copy options to keep all formatting, formulas, and pivot data.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // copies everything
        copyOptions.setSkipEmptyRows(false);
        copyOptions.setSkipEmptyColumns(false);

        // Perform the copy operation.
        sourceRange.copy(destRange, copyOptions);
```

*Miért ez a lépés?*  
`CopyOptions` határozza meg, hogy mi kerül átvitelre. A `PasteType.PASTE_ALL` használata garantálja, hogy a pivot tábla, annak formázása és az alatta lévő képletek is másolódnak. Ezek nélkül csak a nyers értékek másolódhatnak, ami a pivot funkciót tönkreteheti.

### 5. lépés: A munkafüzet mentése és az eredmény ellenőrzése

```java
        // Save the modified workbook to a new file.
        workbook.save("output.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

Nyissa meg az `output.xlsx` fájlt Excelben, és ellenőrizze, hogy:

* A második munkalap teljesen működő pivot táblát tartalmaz, amely az eredetihez azonos.
* A pivot tábla frissítése frissíti az adatokat, bizonyítva, hogy a gyorsítótár érintetlen.

## Tartomány másolása egy másik munkalapra Java-val

Ha a célja egyszerűen **tartomány másolása egy másik munkalapra** pivot tábla nélkül, ugyanaz a kód egy szabályos cellatartománnyal is működik. Az egyetlen változás a forráscím. A `CopyOptions` beállítás változatlan marad, biztosítva a képletek és a formázás megőrzését.

```java
// Example: copy a plain data table from Sheet1!B2:D10 to Sheet3!A1
Range plainSource = workbook.getWorksheets().get(0)
                            .getCells().createRange("B2:D10");
Range plainDest = workbook.getWorksheets().get(2)
                          .getCells().createRange("A1");
plainSource.copy(plainDest, copyOptions);
```

Ez a kódrészlet bemutatja az API rugalmasságát mind pivot, mind nem‑pivot esetekben.

## Tartomány másolása munkalapok között képletek elvesztése nélkül

Amikor **tartományt másol munkalapok között**, a más munkalapokra hivatkozó képletek megszakadhatnak, ha a relatív hivatkozások megváltoznak. Ennek elkerülése érdekében:

1. `CopyOptions.setPasteType(PasteType.PASTE_FORMULAS)` használata, ha csak képletekre van szükség.
2. A cél munkalapot ugyanabban a munkafüzetben tartsa, hogy a belső hivatkozások érvényesek maradjanak.
3. Másolás után hívja meg a `workbook.calculateFormula();` metódust a számítás kényszerítéséhez.

```java
copyOptions.setPasteType(PasteType.PASTE_FORMULAS);
sourceRange.copy(destRange, copyOptions);
workbook.calculateFormula();
```

Ezek a további lépések biztosítják, hogy a másolt tartomány pontosan úgy viselkedjen, mint az eredeti, még akkor is, ha több munkalapot érint.

## Profi tippek és gyakori buktatók

| Helyzet | Tipp |
|-----------|-----|
| **Pivot gyorsítótár nem frissül** | Másolás után hívja meg a `destSheet.getPivotTables().get(0).refresh();` metódust a gyorsítótár frissítéséhez. |
| **Másolás másik munkafüzetbe** | Használja a `Workbook destWorkbook = new Workbook();` kódot, majd `sourceRange.copy(destWorkbook.getWorksheets().get(0).getCells().createRange("A1"), copyOptions);`. Ne felejtse el szükség esetén a pivot gyorsítótárat külön másolni. |
| **Nagy pivot táblák** | Növelje a Java heap méretét (`-Xmx2g`), hogy elkerülje az `OutOfMemoryError` hibát a másolás során. |
| **Stílusok megőrzése** | Állítsa be a `copyOptions.setPasteType(PasteType.PASTE_ALL)` értéket; egyébként csak az értékek másolódnak. |

## Várt kimenet

A teljes program futtatása `output.xlsx` fájlt hoz létre. Excelben megnyitva:

* **Sheet2!A1:G20** ugyanazt a pivot táblát jeleníti meg, mint **Sheet1!A1:G20**.
* A pivot mezőlista, a sor/oszlop címkék és az adatértékek megegyeznek a forrással.
* A pivot frissítése frissíti a számokat, megerősítve, hogy a gyorsítótár működik.

A konzol a következőt fogja kiírni:

```
Pivot table copied successfully.
```

## Következtetés

Ebben a tutorialban megtanulta, **hogyan másoljon pivot táblát** egy munkalapról a másikra az Aspose.Cells for Java használatával. A munkafüzet betöltésével, a megfelelő forrás tartomány kiválasztásával, a cél meghatározásával és a `CopyOptions` konfigurálásával megbízhatóan **másolhat tartományt egy másik munkalapra** és **tartományt munkalapok között**, miközben megőrzi a pivot funkciókat.

Ezután érdemes lehet felfedezni:

* A másolt pivot tábla exportálása PDF vagy HTML formátumba.
* Pivot táblák frissítésének automatizálása több munkafüzetben.
* `CopyOptions` használata csak bizonyos elemek másolására (pl. értékek, formátumok).

Nyugodtan kísérletezzen különböző tartománycímekkel, munkafüzet struktúrákkal, vagy akár munkafüzetek közötti másolásokkal. Jó kódolást!

## Mit érdemes még megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeiben.

- [Hogyan másoljon tartományt Java-ban – Pivot tábla másolása Aspose.Cells segítségével](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)
- [Pivot tábla másolása Java-ban – Teljes Aspose.Cells útmutató](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Pivot tábla másolása Excel – Lépésről‑lépésre útmutató Java használatával](/cells/english/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}