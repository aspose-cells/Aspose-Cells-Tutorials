---
category: general
date: 2026-09-18
description: Hogyan duplikáljunk pivot táblát Java-ban az Aspose.Cells segítségével
  – pivot tábla gyors és megbízható másolása munkafüzetek között.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy range between workbooks
- how to copy pivot
- copy pivot to workbook
- load excel workbook java
language: hu
lastmod: 2026-09-18
og_description: hogyan duplikáljunk pivot táblát Java-ban az Aspose.Cells használatával.
  Kövesse ezt a teljes útmutatót, hogy tiszta Java kóddal másoljon pivot táblát a
  munkafüzetek között.
og_image_alt: Screenshot showing a Java IDE copying a pivot table between two Excel
  workbooks
og_title: Pivot tábla duplikálása Java-ban – lépésről lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  headline: How to duplicate pivot in Java using Aspose.Cells
  type: TechArticle
- description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  name: How to duplicate pivot in Java using Aspose.Cells
  steps:
  - name: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
    text: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
  - name: '**Define the cell area** that encloses the pivot.'
    text: '**Define the cell area** that encloses the pivot.'
  - name: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
    text: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
  - name: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
    text: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
  - name: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
    text: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Hogyan duplikáljuk a pivot táblát Java-ban az Aspose.Cells használatával
url: /hu/java/excel-pivot-tables/how-to-duplicate-pivot-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan duplikáljunk pivot táblát Java-ban az Aspose.Cells használatával

Ha **hogyan duplikáljunk pivot** táblát szeretne egy Java alkalmazásban, ez az útmutató bemutatja a pontos lépéseket. Az Excel munkafüzet betöltésével, a pivot cellatartományának meghatározásával és ennek a tartománynak egy új munkafüzetbe másolásával áthelyezhet egy pivot táblát anélkül, hogy elveszítené annak definícióját vagy adatait.

A pivot tábla másolása gyakori igény, amikor jelentéseket generál, elemzéseket archivál, vagy egy nagy munkafüzetet moduláris részekre oszt. Ebben az oktatóanyagban megtanulja, hogyan **copy range between workbooks**, hogyan **load Excel workbook Java**, és a **how to copy pivot** biztonságos részleteit.

A végén egy kész‑a‑futtatáshoz Java programmal rendelkezik, amely duplikálja a pivot táblát a `Source.xlsx`-ről a `PivotCopied.xlsx`-re az Aspose.Cells for Java használatával.

## Előkövetelmények

* JDK 8 vagy újabb telepítve.
* Maven (vagy más build eszköz) a függőségek kezeléséhez.
* Aspose.Cells for Java 23.10 vagy újabb verzió. Adja hozzá a következő Maven függőséget a `pom.xml`-hez:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier> <!-- adjust classifier to your JDK version -->
</dependency>
```

* Egy forrás munkafüzet (`Source.xlsx`), amely **A1:H30** tartományban pivot táblát tartalmaz.

## Hogyan duplikáljunk pivot táblát Java-ban

Az alapötlet egyszerű:

1. **Load the source workbook** – ez hozzáférést biztosít a pivotot tartalmazó munkalaphoz.
2. **Define the cell area** – a pivotot körülvevő cellatartomány meghatározása.
3. **Create a destination workbook** – egy üres fájl, amely a másolt tartományt fogadja.
4. **Copy the range** – az Aspose.Cells automatikusan duplikálja a pivot definíciót.
5. **Save the destination workbook** – most már egy külön fájlja van ugyanazzal a pivot táblával.

Az alábbiakban egy teljes, futtatható Java program látható, amely követi ezeket a lépéseket.

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {

    public static void main(String[] args) throws Exception {
        // ---------- Step 1: Load the source workbook ----------
        // Replace the path with the actual location of your source file.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWorkbook = new Workbook(srcPath);
        // The first worksheet (index 0) contains the pivot table.
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // ---------- Step 2: Define the cell area that contains the pivot ----------
        // The pivot occupies A1:H30 in the source sheet.
        CellArea srcRange = CellArea.create("A1", "H30");

        // ---------- Step 3: Create a new workbook for the copy ----------
        Workbook destWorkbook = new Workbook();               // creates a blank workbook
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // ---------- Step 4: Copy the range (pivot table is duplicated automatically) ----------
        // CopyOptions can be left default; it ensures that all formatting and pivot objects are preserved.
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // ---------- Step 5: Save the destination workbook ----------
        String destPath = "YOUR_DIRECTORY/PivotCopied.xlsx";
        destWorkbook.save(destPath);

        System.out.println("Pivot table duplicated successfully to " + destPath);
    }
}
```

### Miért működik ez

* **Aspose.Cells** a pivot táblát a munkalap cellagyűjteményének részeként kezeli. Amikor a `copyRange`-t meghívja, a könyvtár nem csak a cellaértékeket, hanem a mögöttes pivot gyorsítótárat és definíciót is másolja, így az új munkafüzet teljesen működőképes duplikátumot tartalmaz.
* A `CopyOptions` objektum alapértelmezés szerint megőrzi a képleteket, formátumokat és beágyazott objektumokat. Szükség esetén testreszabhatja (pl. `setCopyColumnWidths(true)`), ha további irányítást igényel.

## Tartomány másolása munkafüzetek között – mélyebb áttekintés

Míg a fenti példa egyetlen összefüggő blokkot másol, a `copyRange` bármilyen téglalap alakú területet kezelhet. Ha a pivot nem szomszédos tartományokra terjed, többször is meghívhatja a `copyRange`-t, vagy használhatja a `Worksheet.copy`-t a teljes munkalap duplikálásához.

```java
// Example: copy the whole sheet, preserving all pivots and charts
srcWorksheet.copy(destWorksheet, new CopyOptions());
```

**Tip:** Nagy munkafüzetek másolásakor engedélyezze a `CopyOptions.setPreserveCellStyle(true)` beállítást, hogy elkerülje a felesleges stílusduplikációt, ami javíthatja a teljesítményt.

## Hogyan másoljuk a pivot táblát munkafüzetbe – több pivot kezelése

Ha a forrás munkalap több mint egy pivot táblát tartalmaz, végigiterálhat a munkalap pivot tábláin, és mindegyiket egyenként másolhatja:

```java
for (int i = 0; i < srcWorksheet.getPivotTables().getCount(); i++) {
    PivotTable pt = srcWorksheet.getPivotTables().get(i);
    // Determine the range that the pivot occupies
    CellArea pivotArea = pt.getPivotTableArea();
    srcWorksheet.copyRange(pivotArea, destWorksheet, pt.getName() + "!A1", new CopyOptions());
}
```

Ez a megközelítés biztosítja, hogy minden pivot megtartsa eredeti nevét és adatforrását.

## Excel munkafüzet betöltése Java-ban – gyakori buktatók

* **File path separators:** Használjon előre írt perjeleket (`/`) vagy `File.separator`-t a kód platform‑független megtartásához.
* **Missing license:** Az Aspose.Cells értékelő módban működik, de a kimenet vízjelet tartalmaz. Regisztráljon licencet a `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` kóddal a munkafüzet betöltése előtt a vízjel eltávolításához.
* **Large files:** 100 MB-nál nagyobb munkafüzetek esetén fontolja meg a `WorkbookFactory.create(InputStream, new LoadOptions(LoadFormat.XLSX))` használatát streaming opciókkal a memóriahasználat csökkentése érdekében.

## Teljes vég‑től‑végig példa összefoglaló

Mindent egy helyre téve, itt a végleges program, amelyet egyszerűen beilleszthet az IDE-jébe:

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {
    public static void main(String[] args) throws Exception {
        // Load license (optional, removes evaluation watermark)
        // License lic = new License();
        // lic.setLicense("Aspose.Total.Java.lic");

        // 1️⃣ Load source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // 2️⃣ Define pivot range (A1:H30)
        CellArea srcRange = CellArea.create("A1", "H30");

        // 3️⃣ Prepare destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the pivot (Aspose.Cells handles the pivot cache automatically)
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/PivotCopied.xlsx");

        System.out.println("Pivot table duplicated successfully.");
    }
}
```

**Expected output:** A futtatás után a `PivotCopied.xlsx` megjelenik a megadott könyvtárban. Excelben megnyitva ugyanazt a pivot tábla elrendezést, szűrőket és adatokat mutatja, mint a `Source.xlsx`-ben. Minden számított mező és formázás megmarad.

## Gyakran ismételt kérdések

* **Does this work with older Excel formats (.xls)?**  
  Igen. Az Aspose.Cells automatikusan felismeri a formátumot. Használja a `new Workbook("file.xls")`-t, és ugyanaz a másolási logika érvényes.

* **What if the pivot references external data sources?**  
  A másolat megtartja az eredeti adatforrás hivatkozást. Ha a célkörnyezet nem éri el azt a forrást, a pivot `#REF!` hibákat fog mutatni. Ennek elkerülése érdekében frissítse a pivotot a másolás után, vagy módosítsa az adatforrást a `PivotTable.setDataSource(...)` segítségével.

* **Can I copy a pivot to a specific sheet name?**  
  Természetesen. A cél munkalap létrehozása után nevezze át:

  ```java
  destWorksheet.setName("ReportPivot");
  srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());
  ```

## Következtetés

Most már tudja, hogyan **duplicate pivot** táblákat Java-ban az Aspose.Cells használatával, hogyan **copy range between workbooks**, és a legjobb gyakorlatokat a **load Excel workbook Java**-hez. Az öt lépésből álló folyamat – betöltés, meghatározás, cél létrehozása, másolás és mentés – segítségével automatizálhatja a jelentéskészítést, archiválhatja az elemzéseket, vagy feloszthatja a komplex munkafüzeteket anélkül, hogy a pivot funkcionalitást elveszítené.

Ezután fedezze fel a kapcsolódó témákat, például a **copy pivot to workbook** több munkalappal, vagy integrálja a duplikált pivotot egy nagyobb adatfeldolgozó csővezetékbe az Apache POI használatával nem‑Aspose esetekben. Kísérletezzen különböző `CopyOptions` beállításokkal a teljesítmény finomhangolásához hatalmas munkafüzetek esetén.

Boldog kódolást!

## Mit érdemes még megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljesen működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeiben.

- [Hogyan hozzunk létre pivot táblákat Excelben az Aspose.Cells for Java&#58; Átfogó útmutató](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Hogyan frissítsük az Excel pivot tábla forrását az Aspose.Cells for Java&#58; Átfogó útmutató](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Pivot mezők csoportosítása Excel munkafüzetekben az Aspose.Cells for Java használatával - Átfogó útmutató](/cells/english/java/data-analysis/aspose-cells-java-group-pivot-fields-excel-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}