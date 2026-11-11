---
category: general
date: 2026-10-23
description: Tanulja meg, hogyan duplikálhat egy Excel munkalapot Java-ban, miközben
  megőrzi a pivot táblákat. Ez az útmutató azt is bemutatja, hogyan másolhat pivot
  táblákat, Excel tartományokat, és egy munkalapot pivot adatokkal.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- duplicate excel sheet
- how to copy pivot
- copy excel range
- copy sheet with pivot
- copy pivot to workbook
language: hu
lastmod: 2026-10-23
og_description: Duplikáljon egy Excel munkalapot Java-ban, miközben megőrzi a pivot
  táblákat. Kövesse ezt a teljes útmutatót a pivot táblák másolásához, az Excel tartományok
  másolásához, és egy pivot adatokat tartalmazó munkalap másolásához.
og_image_alt: Screenshot showing a duplicated Excel sheet with pivot tables preserved
og_title: Excel munkalap másolása pivot táblákkal Java-ban – lépésről lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  headline: How to duplicate an Excel sheet and keep pivot tables intact in Java
  type: TechArticle
- description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  name: How to duplicate an Excel sheet and keep pivot tables intact in Java
  steps:
  - name: Expected output
    text: 'Running the program creates `DuplicatedWithPivot.xlsx` in the target directory.
      Open the file in Excel and you will see:'
  - name: How to copy pivot to another workbook without copying the whole sheet?
    text: If you only need the pivot and its underlying data, copy the range that
      contains both the source data and the pivot, then use `setCopyPivotTable(true)`.
      The same code from **Step 4** applies; just ensure the range covers the data
      source.
  - name: What if the source workbook has multiple worksheets with pivots?
    text: 'Repeat **Step 3** for each worksheet you want to duplicate:'
  - name: Does this work with protected worksheets?
    text: 'Aspose.Cells can copy protected sheets, but you must unprotect them first
      if you need to modify the pivot after copying:'
  - name: Can I copy a pivot table to an existing workbook that already contains a
      sheet with the same name?
    text: 'Yes. Use `addCopy` with a unique name:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot tables
title: Hogyan duplikáljunk egy Excel munkalapot, és tartsuk meg a pivot táblákat változatlanul
  Java-ban
url: /hu/java/excel-pivot-tables/how-to-duplicate-an-excel-sheet-and-keep-pivot-tables-intact/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan duplikáljunk egy Excel munkalapot, és tartsuk meg a pivot táblákat Java-ban

Ha **Excel munkalapot kell duplikálni**, miközben minden pivot táblát élő állapotban tart, ez az útmutató pontosan megmutatja, hogyan. Egy tömör megoldást láthatsz, amely egy munkalapot másol, egy meghatározott tartományt másol, és még egy pivot táblát is átmásol egy másik munkafüzetbe – mindezt tiszta Java-val az Aspose.Cells használatával.

Az Excel munkalap duplikálása gyakori feladat, amikor havi jelentéseket generálsz egy sablonból, vagy amikor teszteléshez egy sandbox másolatra van szükséged. Az alábbi kód az Aspose.Cells 25.11 vagy újabb verzióval működik, amely bevezette a `setCopyPivotTable(true)` opciót.

## Amire szükséged lesz

- Java 17 (vagy bármely friss JDK) telepítve
- Aspose.Cells for Java 25.11 vagy újabb a projektedben (Maven koordináta `com.aspose:aspose-cells:25.11`)
- Egy forrás munkafüzet (`SourceWithPivot.xlsx`), amely már tartalmaz pivot táblát
- Egy IDE vagy build eszköz, amit választasz (IntelliJ IDEA, Eclipse, Maven, Gradle, stb.)

## 1. lépés: Töltsd be a forrás munkafüzetet, amely tartalmazza a pivot táblát

Az első művelet a munkafüzet megnyitása, amely a megőrizni kívánt pivotot tartalmazza.

```java
import com.aspose.cells.*;

public class DuplicateExcelSheet {
    public static void main(String[] args) throws Exception {
        // Load the source workbook with the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

> **Miért fontos ez a lépés:** A forrás munkafüzet betöltése hozzáférést biztosít a munkalap objektumokhoz, cellákhoz és a beágyazott pivot táblákhoz. Enélkül nem tudod hivatkozni a másolni kívánt pivot adatokat.

## 2. lépés: Hozz létre egy üres cél munkafüzetet (vagy tölts be egy meglévőt)

Kezdhetsz egy üres munkafüzettel, vagy megnyithatsz egy meglévő fájlt, amely a duplikált munkalapot fogja fogadni.

```java
        // Create a new, empty destination workbook
        Workbook dstWb = new Workbook();
```

> **Tipp:** Ha már van egy jelentés munkafüzeted, cseréld le a fenti sort `new Workbook("ExistingReport.xlsx")`-re, hogy a duplikált munkalapot hozzáadd.

## 3. lépés: Másold le az egész munkalapot – a pivot tábla automatikusan megmarad

Az egész munkalap másolása a legegyszerűbb módja a **copy sheet with pivot**. Az Aspose.Cells automatikusan másolja a pivot definíciót és annak gyorsítótárát.

```java
        // Access the first worksheet (index 0) from the source workbook
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Add a copy of the source worksheet to the destination workbook
        Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
```

> **Miért működik:** Az `addCopy` klónozza a munkalap szerkezetét, a cella értékeket, a stílusokat és minden beágyazott pivot táblát. Az új munkalap a `dstWb`-ben azonos lesz az eredetivel, beleértve a pivot gyorsítótárát is.

## 4. lépés: (Opcionális) Csak egy meghatározott tartomány másolása, amely tartalmazza a pivot táblát

Néha nem akarod az egész munkalapot – lehet, hogy csak egy olyan részt kell másolnod, amely a pivotot tartalmazza. Itt jön képbe a **copy Excel range**, és kifejezetten kérheted a pivot másolását.

```java
        // Define the source range that covers the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G30");

        // Define the target range in the destination worksheet
        Range dstRange = dstWs.getCells().createRange("A1");

        // Copy the range and tell Aspose.Cells to include the pivot table
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setCopyPivotTable(true); // new option in 25.11
        dstRange.copy(srcRange, copyOptions);
```

> **Hogyan segít:** A `setCopyPivotTable(true)` arra kényszeríti a motorot, hogy a pivot definíciót is duplikálja, még ha korlátozott tartományt másolsz is. Enélkül csak a nyers adatokat másolná, és a pivot elveszne.

## 5. lépés: Mentsd el a cél munkafüzetet

Végül írd ki a duplikált tartalmat egy új fájlba.

```java
        // Save the destination workbook to a new file
        dstWb.save("YOUR_DIRECTORY/DuplicatedWithPivot.xlsx");
    }
}
```

### Várható kimenet

A program futtatása létrehozza a `DuplicatedWithPivot.xlsx` fájlt a célkönyvtárban. Nyisd meg a fájlt Excelben, és a következőket fogod látni:

- Egy új munkalap `Sheet1 (Copy)` néven (vagy az eredeti név „Copy” hozzáfűzésével)
- A pivot tábla pontosan úgy jelenik meg, mint a forrás munkalapon, teljesen működőképes
- Ha az opcionális tartománymásolást használtad, csak az A1:G30 cellák vannak jelen, de a pivot még mindig működik, mert a gyorsítótár másolva lett

## Gyakori kérdések és szélhelyzetek

### Hogyan másoljuk a pivotot egy másik munkafüzetbe anélkül, hogy az egész munkalapot másolnánk?

Ha csak a pivotra és annak alapadataira van szükséged, másold le azt a tartományt, amely tartalmazza a forrás adatokat és a pivotot is, majd használd a `setCopyPivotTable(true)`-t. Ugyanaz a kód a **4. lépésből** alkalmazható; csak győződj meg róla, hogy a tartomány lefedi az adatforrást.

### Mi a teendő, ha a forrás munkafüzetnek több pivot táblát tartalmazó munkalapja van?

Ismételd meg a **3. lépést** minden olyan munkalapra, amelyet duplikálni szeretnél:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet ws = srcWb.getWorksheets().get(i);
    dstWb.getWorksheets().addCopy(ws);
}
```

### Működik ez védett munkalapok esetén?

Az Aspose.Cells képes védett munkalapokat másolni, de először fel kell oldani a védelmet, ha a pivotot a másolás után módosítani szeretnéd:

```java
srcWs.unprotect("password");
dstWs.unprotect("password");
```

### Másolhatok pivot táblát egy meglévő munkafüzetbe, amely már tartalmaz ugyanazzal a névvel rendelkező munkalapot?

Igen. Használd az `addCopy`-t egy egyedi névvel:

```java
Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
dstWs.setName("PivotCopy_" + System.currentTimeMillis());
```

## Profi tipp: ellenőrizd a pivot gyorsítótárat

Másolás után programozottan ellenőrizheted, hogy a pivot gyorsítótár létezik-e:

```java
PivotTable pt = dstWs.getPivotTables().get(0);
System.out.println("Pivot cache ID: " + pt.getCacheIndex());
```

Ha a gyorsítótár ID-je nem negatív számot ad ki, a pivot sikeresen duplikálva lett.

## Összegzés

Most már tudod, hogyan **duplicate Excel sheet** Java-ban, miközben megőrzöd minden pivot táblát, hogyan **copy pivot** táblákat közvetlenül, hogyan **copy Excel range**-t, amely tartalmaz egy pivotot, és hogyan **copy sheet with pivot** vagy **copy pivot to workbook** az Aspose.Cells 25.11+ használatával. Alkalmazd ezeket a mintákat a jelentésgenerálás automatizálásához, sablonklónok létrehozásához vagy tesztkörnyezetek építéséhez, amelyeknek azonos pivot‑vezérelt elemzésekre van szükségük.

Készen állsz további felfedezésre? Próbáld meg exportálni a duplikált munkafüzetet PDF-be, vagy programozottan frissítsd a pivot gyorsítótárát a másolás után, hogy a legújabb adatok tükröződjenek. Boldog kódolást!

## Mit érdemes legközelebb megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [How to duplicate worksheet and preserve pivot tables in Java](/cells/english/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/)
- [How to Copy Pivot Table in Java – Complete Aspose.Cells Guide](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}