---
category: general
date: 2026-03-01
description: Pivot tábla másolása Java-ban a pivot megőrzésével, majd az Excel exportálása
  PPTX-be, az Excel AutoFilter letiltása, és a Smart Marker használata JSON tömbökhöz
  – teljes lépésről lépésre útmutató.
draft: false
keywords:
- copy pivot table
- preserve pivot table
- use smart marker
- disable excel autofilter
- export excel to pptx
language: hu
og_description: Másolja a pivot táblát Java-ban, őrizze meg a pivot definíciót, exportálja
  PPTX-be, tiltsa le az AutoFilter-t, és használja a Smart Marker-t – teljes útmutató
  fejlesztőknek.
og_title: Pivot tábla másolása Java-ban – megőrizze, exportálja PPTX-be
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Pivot tábla másolása Java-ban – megőrizze, exportálja PPTX-be
url: /hu/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pivot tábla másolása Java‑ban – Megőrzés, Exportálás PPTX‑be

Valaha is szükséged volt **pivot tábla másolása** egy munkafüzetből a másikba anélkül, hogy elveszítenéd az alatta lévő pivot definíciót? Nem vagy egyedül, aki ezen agyazik. Sok valós projektben adatot kell áthelyezned, és az utolsó dolog, amit akarsz, egy hibás pivot, amely futásidőben hibákat dob.  

Ebben az útmutatóban egy teljes megoldáson vezetünk végig, amely nem csak **pivot tábla másolását** valósítja meg, hanem megmutatja, hogyan **megőrizheted a pivot táblát** másoláskor, **Excel exportálása PPTX‑be**, **Excel AutoFilter letiltása**, és **smart marker használata** egy JSON tömb egyetlen cellába helyezéséhez. A végére egyetlen, futtatható Java programod lesz, amely lefedi mind a négy szcenáriót.

## Előfeltételek

- Java 8 vagy újabb (a kód Java 11‑kel is működik)  
- Aspose.Cells for Java könyvtár (23.9‑es vagy újabb verzió) – letöltheted a Maven Central‑ról  
- Alapvető ismeretek az Excel fogalmakról, mint például pivot táblák, táblázatok és szövegdobozok  

Ha hiányzik az Aspose.Cells JAR, add hozzá ezt a `pom.xml`-hez:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

Most merüljünk el.

## 1. lépés: Pivot tábla másolása – a pivot definíció megőrzése

Ha egyszerűen csak a pivot táblát tartalmazó cellatartományt másolod, a pivot metaadatok gyakran hátramaradnak. Az Aspose.Cells egy praktikus módot biztosít a definíció érintetlen megtartására a `copyRange` és egy `CopyOptions` példány használatával.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot (A1:G20 is just an example)
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Prepare the destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot definition travels with it
        destSheet.getCells().copyRange(pivotRange,
                new CellArea(0, 0, 19, 6), // destination area (rows 0‑19, cols 0‑6)
                new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Miért működik:** A `CopyOptions` azt mondja az Aspose.Cells‑nek, hogy mindent vigyen át, beleértve a pivot gyorsítótárat és a mezőbeállításokat. Enélkül csak egyszerű értékek maradnak, és elveszíted a pivot frissítésének lehetőségét.

**Szélsőséges eset:** Ha a forrás pivot több, mint a keménykódolt `A1:G20` tartomány, állítsd be ennek megfelelően a tartományt, vagy használd a `sourceSheet.getPivotTables().get(0).getDataRange()`‑t a dinamikus lekéréshez.

![Pivot tábla másolásának példája](image.png "Pivot tábla másolása Java‑ban")

*Kép alternatív szövege: pivot tábla másolása Java‑ban diagram*

## 2. lépés: Munkalap exportálása szerkeszthető szövegdobozzal PPTX‑be

Gyakran szükség van arra, hogy egy Excel munkalapot PowerPoint diára alakítsunk – gondolj a heti műszerfalakra, amelyeket bemutatni kell. Az Aspose.Cells közvetlenül ment egy munkalapot PPTX fájlként, miközben megőrzi a formákat, például a szövegdobozokat.

```java
import com.aspose.cells.*;

public class ExportToPptxDemo {

    public static void main(String[] args) throws Exception {
        // Load workbook that contains a TextBox shape
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Export the first worksheet to PPTX
        wb.save("YOUR_DIRECTORY/output.pptx", SaveFormat.PPTX);

        System.out.println("Worksheet exported to PPTX successfully.");
    }
}
```

**Mi történik:** A `save` metódus `SaveFormat.PPTX`‑szel az egész munkalapot, beleértve a szerkeszthető TextBox‑ot, PowerPoint diává konvertálja. A dobozban lévő szöveg szerkeszthető marad, amikor a PPTX‑et PowerPoint‑ban megnyitod.

**Tipp:** Ha több munkalapod van, és csak egyet szeretnél, hívd meg a `wb.getWorksheets().removeAt(index)`‑t a többi eltávolításához a mentés előtt.

## 3. lépés: Excel AutoFilter letiltása egy táblázatból

Az AutoFilter kényelmes a végfelhasználók számára, de néha programozottan kell kikapcsolni – például adat exportálása vagy tiszta jelentés készítése előtt. Íme, hogyan **tiltsd le az Excel autofiltert** egy Excel táblázaton.

```java
import com.aspose.cells.*;

public class DisableAutoFilterDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");
        Worksheet sheet = wb.getWorksheets().get(0);

        // Assume the first table in the sheet is the target
        Table table = sheet.getTables().get(0);

        // Turn off the AutoFilter arrows
        table.setShowAutoFilter(false);

        // Save the modified workbook
        wb.save("YOUR_DIRECTORY/noFilter.xlsx");
        System.out.println("AutoFilter disabled and workbook saved.");
    }
}
```

**Miért lehet erre szükség:** Olyan formátumokba exportálás, amelyek nem támogatják az AutoFiltert (például CSV vagy PDF), felesleges szűrőikonok megjelenését okozhatja. A letiltás tiszta kimenetet biztosít.

**Gyakori buktató:** Ha a munkalapon nincs táblázat, a `getTables().get(0)` `IndexOutOfBoundsException`‑t dob. Mindig ellenőrizd először a `sheet.getTables().size()` értékét a produkciós kódban.

## 4. lépés: Smart Marker használata – JSON tömb beillesztése egyetlen cellaértékként

A Smart Marker az Aspose sablonmotorja. Egy hasznos trükk, hogy egy teljes JSON tömböt egyetlen cellaértékként kezelünk, ami tökéletes naplózáshoz vagy strukturált adatok továbbításához. Használjuk a **smart marker‑t** ennek eléréséhez.

```java
import com.aspose.cells.*;

public class SmartMarkerDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Initialise the SmartMarker processor with the workbook
        SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

        // JSON array we want to embed
        String jsonArray = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Configure the processor to treat arrays as a single cell
        processor.setOptions(SmartMarkerOptions.ArrayAsSingle);

        // Apply the marker – assume cell A1 contains the marker ${json}
        processor.apply(jsonArray);

        // Save the result
        wb.save("YOUR_DIRECTORY/smartMarkerResult.xlsx");
        System.out.println("JSON array inserted via Smart Marker.");
    }
}
```

**Hogyan működik:** A munkafüzetben a `${json}` jelzőt a teljes JSON karakterlánc helyettesíti, mivel beállítottuk az `ArrayAsSingle` opciót. Enélkül az Aspose megpróbálná minden tömb elemet külön sorba bontani.

**Variáció:** Ha a tömböt sorokra szeretnéd bontani, egyszerűen hagyd ki az `ArrayAsSingle` opciót, és a Smart Marker automatikusan kezeli a kiterjesztést.

## Teljes működő példa – minden lépés egyben

Az alábbi egyetlen Java osztály, amely összefűzi a bemutatott összes műveletet. Futtasd szokásos `main` metódusként; csak állítsd be a fájlutakat a környezetednek megfelelően.

```java
import com.aspose.cells.*;

public class CompleteExcelAutomation {

    public static void main(String[] args) throws Exception {
        // ----------- Step 1: Copy Pivot Table -----------
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet srcSheet = srcWb.getWorksheets

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}