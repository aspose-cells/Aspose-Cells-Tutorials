---
category: general
date: 2026-07-03
description: Hogyan formázzuk az Excel fájlokat Java-val. Tanulja meg, hogyan formázzuk
  a dátumoszlopot Excelben, hogyan alkalmazzunk számformátumot Excelben, hogyan exportáljunk
  DataTable-t XLSX-be, és hogyan importáljunk DataTable-t Excelbe az Aspose Cells
  segítségével.
draft: false
keywords:
- how to style excel
- format column date excel
- apply number format excel
- export datatable to xlsx
- import datatable into excel
language: hu
og_description: Hogyan formázzuk az Excel fájlokat Java-ban. Ez a bemutató megmutatja,
  hogyan formázhatunk oszlop dátumot Excelben, hogyan alkalmazhatunk számformátumot
  Excelben, hogyan exportálhatunk DataTable-t XLSX-be, és hogyan importálhatunk DataTable-t
  Excelbe.
og_title: Hogyan formázzuk az Excelt – Java útmutató egyéni oszlopformázáshoz
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to style Excel files using Java. Learn to format column date Excel,
    apply number format Excel, export DataTable to XLSX and import DataTable into
    Excel with Aspose Cells.
  headline: How to Style Excel – Import DataTable with Custom Formatting in Java
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: Hogyan formázzuk az Excelt – DataTable importálása egyedi formázással Java-ban
url: /hu/java/excel-import-export/how-to-style-excel-import-datatable-with-custom-formatting-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan formázzuk az Excelt – DataTable importálása egyedi formázással Java-ban

Gondolkodtál már azon, **hogyan formázzuk az Excelt** programozottan anélkül, hogy manuálisan megnyitnád a fájlt? Nem vagy egyedül. Sok fejlesztőnek kell jelentéseket generálnia, ahol az első oszlop félkövér, a második dátumokat mutat, a többi pedig tiszta elrendezést követ. Ebben az útmutatóban egy teljes, futtatható példán keresztül vezetünk, amely **importál egy DataTable-t Excelbe**, félkövér fejlécet alkalmaz, egy dátumoszlopot formáz, és végül **exportálja a DataTable-t XLSX-be**.

Az Aspose.Cells for Java-t fogjuk használni, de a koncepciók bármely, a stílusokkal dolgozó könyvtárra alkalmazhatók. A végére egy újrahasználható mintát kapsz a **apply number format Excel** cellákhoz, a **format column date Excel** oszlophoz, és egy kifinomult munkafüzet szállításához a felhasználóidnak.

## Előfeltételek

- Java 17 (vagy bármely friss JDK)  
- Aspose.Cells for Java 23.9 vagy újabb (az ingyenes próba is megfelelő)  
- Egy `DataTable`‑szerű struktúra (a példa egy egyszerű mock-ot használ)  
- A kedvenc IDE-d (IntelliJ IDEA, Eclipse, VS Code…)

Nem szükséges további Maven plugin; csak add hozzá az Aspose.Cells JAR-t az osztályútvonalhoz.

---

## 1. lépés: Szerezd meg a forrás DataTable-t – az “Export DataTable to XLSX” előkészítés

Mielőtt **importálni tudnánk a datatable-t Excelbe**, szükségünk van egy `DataTable` objektumra, amely a exportálni kívánt adatokat képviseli. Valós projektekben ezt adatbázisból, CSV fájlból vagy egy API-ból szerezheted be. Ehhez a bemutatóhoz egy apró táblát fogunk mock-olni:

```java
import java.util.*;
import com.aspose.cells.*;

public class DemoData {
    public static DataTable getDataTable() {
        // Create a simple table with three columns: ID, Date, Amount
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", DataType.INTEGER);
        dt.getColumns().add("OrderDate", DataType.DATE_TIME);
        dt.getColumns().add("Total", DataType.DOUBLE);

        // Add a few rows
        dt.getRows().add(new Object[]{1, new Date(), 125.50});
        dt.getRows().add(new Object[]{2, new Date(System.currentTimeMillis() - 86400000L), 99.99});
        dt.getRows().add(new Object[]{3, new Date(System.currentTimeMillis() - 2*86400000L), 250.00});
        return dt;
    }
}
```

> **Miért fontos:** Az adatok helyes előzetes megszerzése azt jelenti, hogy a stíluslogika többi része kizárólag a megjelenítésre koncentrálhat, nem az adatkezelésre.

---

## 2. lépés: Hozz létre egy tömböt, amely az egyes oszlopok stílusdefinícióit tárolja

Aspose.Cells lehetővé teszi, hogy egy **Style[]** tömböt adj át a `DataTable` importálásakor. Minden bejegyzés egy oszlopnak felel meg, és meghatározza, hogyan fog kinézni az importálás után. Allokáljuk a tömböt az oszlopok száma alapján:

```java
DataTable dataTable = DemoData.getDataTable();
Style[] columnStyles = new Style[dataTable.getColumns().size()];
```

> **Tipp:** Ha sok oszlopod van, fontold meg a tömb ciklusban történő felépítését, és egyetlen `Style` objektum újrahasználatát, ahol a formázás azonos. Ez csökkenti a memóriahasználatot.

---

## 3. lépés: Definiáld a stílusokat – Félkövér fejléc és dátumformázás

Most megválaszoljuk a klasszikus **format column date excel** kérdést, és bemutatjuk a **apply number format excel** használatát más oszlopokhoz.

```java
// --- Style for the first column (header bold) ---
columnStyles[0] = new Style();
columnStyles[0].getFont().setBold(true);          // Makes header text bold

// --- Style for the second column (date formatting) ---
columnStyles[1] = new Style();
columnStyles[1].setNumber(StyleNumberFormat.DATE); // Uses the built‑in DATE format

// --- Optional: Style for the third column (currency) ---
columnStyles[2] = new Style();
columnStyles[2].setNumber(StyleNumberFormat.CURRENCY_USD);
```

**Mi történik itt?**  
- `StyleNumberFormat.DATE` azt mondja az Excelnek, hogy a cella értékét rövid dátumként kezelje (pl. *01/31/2024*).  
- `StyleNumberFormat.CURRENCY_USD` automatikusan hozzáadja a `$` szimbólumot és két tizedesjegyet.  
- Az első oszlop betűtípusának félkövérre állítása kiemeli a fejlécet, ami gyakori követelmény, amikor **how to style excel** táblázatokat olvashatóvá teszel.

> **Szélsőséges eset:** Ha a forrásadatok már formázott karakterláncokat tartalmaznak, előfordulhat, hogy `java.util.Date` objektumokká kell konvertálni őket importálás előtt; különben az Excel egyszerű szövegként kezeli őket.

---

## 4. lépés: Hozz létre egy új munkafüzetet és érj el az első munkalapot

Egy új munkafüzet tiszta vásznat biztosít. Az első munkalapot fogjuk megszerezni, ahová az importálás kerül.

```java
Workbook workbook = new Workbook();               // New empty workbook
Worksheet worksheet = workbook.getWorksheets().get(0); // First sheet (index 0)
```

> **Miért új munkafüzet?** A semmiből indulás garantálja, hogy semmilyen maradék stílus vagy rejtett sor ne befolyásolja a végső eredményt – ez elengedhetetlen, amikor **how to style excel** fájlokat szeretnél konzisztensen kezelni több futtatás során.

---

## 5. lépés: Importáld a DataTable-t az oszlopszámok stílusával

Itt van a művelet szíve: a `DataTable` betáplálása a munkalapba, miközben alkalmazzuk a korábban épített stílostömböt.

```java
// The third argument (true) tells Aspose.Cells to include column headers.
worksheet.getCells().importDataTable(dataTable, true, columnStyles);
```

**Magyarázat:**  
- `importDataTable` másolja a fejléc sort és az adat sorokat is.  
- A `columnStyles` tömb minden oszloppal egyezik, így az első oszlop fejléce félkövér lesz, a második oszlop dátumokat mutat, a harmadik oszlop pedig pénznemként jelenik meg.  
- Ez egyetlen sor helyettesíti a tucatnyi manuális cellánkénti formázási lépést, bemutatva egy tiszta módot a **apply number format excel** programozott alkalmazására.

---

## 6. lépés: Mentsd el a formázott munkafüzetet – az “Export DataTable to XLSX” befejezése

Végül a munkafüzetet lemezre mentjük. Állítsd be az elérési utat egy írható mappára a gépeden.

```java
String outputPath = "C:/temp/styledImport.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Nyisd meg a fájlt Excelben, és a következőket kell látnod:

- Az **ID** oszlop fejléce félkövér.  
- **OrderDate** oszlop dátumként formázva (pl. *04/27/2024*).  
- **Total** oszlop dollárjellel és két tizedesjeggyel jelenik meg.

> **Pro tipp:** Ha régebbi Excel verziókat kell támogatnod, hívd a `workbook.save(outputPath, SaveFormat.XLS)` metódust az alapértelmezett XLSX helyett.

---

## 7. lépés: Ellenőrizd az eredményt és opcionális finomhangolások

Jó gyakorlat a generált fájl kétszeres ellenőrzése, különösen, ha a jelentéseket érintettek számára automatizálod.

```java
// Quick verification: read the first cell's style
Cell firstHeader = worksheet.getCells().get(0, 0);
boolean isBold = firstHeader.getStyle().getFont().isBold();
System.out.println("Header bold? " + isBold);
```

Ha az `isBold` `true`-t nyomtat, a **how to style excel** rutinod a várt módon működött. Innen tovább:

- Adj hozzá feltételes formázást (pl. kiemelni a > $200 összegű totalokat).  
- Fagyaszd be a felső sort a könnyebb görgetéshez.  
- Helyezz be egy diagramot, amely a importált adatokat hivatkozza.

Mindez a kiterjesztés ugyanazt a mintát követi: definiálj egy `Style`-t, alkalmazd, és mentsd.

---

## Gyakori kérdések és szélsőséges esetek

| Kérdés | Válasz |
|----------|--------|
| **Stílusozhatok több oszlopot ugyanúgy?** | Igen – használj egyetlen `Style` példányt minden olyan oszlophoz, amely ugyanazt a formázást használ. |
| **Mi van, ha a DataTable több oszloppal rendelkezik, mint a stílusok?** | Bármely oszlop, amelynek nincs megfelelő bejegyzése a `columnStyles`-ben, az alapértelmezett stílust használja. |
| **Hogyan változtathatom meg a dátumformátumot „dd‑MMM‑yyyy” formára?** | Használd a `columnStyles[1].setCustom("#dd-MMM-yyyy#");` kifejezést a beépített `DATE` helyett. |
| **Van mód az oszlopok automatikus méretezésére importálás után?** | Hívd meg a `worksheet.autoFitColumns();` metódust az `importDataTable` után. |
| **Működik ez Linuxon/macOS-en?** | Természetesen – az Aspose.Cells platformfüggetlen, amíg kompatibilis JDK-val rendelkezel. |

---

## Összegzés

Most már egy szilárd, vég‑től‑végig példát rendelkezel arra, hogyan **style Excel** munkafüzeteket **importálva a datatable-t Excelbe**, **format column date excel**, és **apply number format excel** Java használatával. A kód bemutatja a teljes folyamatot a **export datatable to xlsx** lépéstől a fájl Excelben való megnyitásáig, lefedve mindazt, *miért* és *mi* történik minden lépésben.

Próbáld ki: módosítsd a stílustömböt, adj hozzá több oszlopot, vagy csatlakoztass egy valódi adatbázis‑lekérdezést. Ugyanaz a minta lehetővé teszi, hogy egy gombnyomásra professzionális kinézetű jelentéseket generálj, manuális formázás nélkül.

![A tutorial kód által generált formázott Excel munkalap](https://example.com/images/styled-worksheet.png "Képernyőkép a Java és Aspose.Cells használatával létrehozott formázott Excel munkalapról")

*Kép alternatív szöveg: „Java és Aspose.Cells által létrehozott formázott Excel munkalap, félkövér fejléc és formázott dátumoszlop megjelenítésével.”*

## Mit érdemes legközelebb megtanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Hogyan hozzunk létre és formázzunk Excel cellákat az Aspose.Cells for Java használatával: Lépésről‑lépésre útmutató](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Hogyan formázzunk Excel cellákat és adjunk hozzá hiperhivatkozásokat az Aspose.Cells for Java használatával](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Aspose.Cells for Java: Hogyan hozzunk létre és formázzunk Excel munkafüzeteket hatékonyan](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}