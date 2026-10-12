---
category: general
date: 2026-06-18
description: Parsolja a japán korszak dátumát Java-ban az Aspose.Cells segítségével.
  Tanulja meg, hogyan olvassa be a dátumot egy Excel cellából, és hogyan nyerje ki
  gyorsan a dátum‑idő értéket az Excel cellából.
draft: false
keywords:
- parse japanese era date
- read date from excel cell
- extract datetime from excel cell
language: hu
og_description: Parsolja a japán korszak dátumát Java-ban az Aspose.Cells használatával.
  Ez az útmutató megmutatja, hogyan olvassa be a dátumot egy Excel cellából, és hogyan
  nyerje ki a dátum‑idő értéket néhány lépésben.
og_title: Japán korszak dátumának feldolgozása Excelből Java-ban – Teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Parse Japanese era date in Java using Aspose.Cells. Learn how to read
    date from Excel cell and extract datetime from Excel cell quickly.
  headline: Parse Japanese Era Date from Excel in Java – Full Guide
  type: TechArticle
- description: Parse Japanese era date in Java using Aspose.Cells. Learn how to read
    date from Excel cell and extract datetime from Excel cell quickly.
  name: Parse Japanese Era Date from Excel in Java – Full Guide
  steps:
  - name: Multiple Eras
    text: Japan has had several eras (Meiji, Taishō, Shōwa, Heisei, Reiwa). The `setParseDateUsingJapaneseEra(true)`
      flag covers all of them automatically, but be aware that older dates may fall
      outside the library’s supported range (typically 1868‑present). If you encounter
      a date like “昭和45年12月31日”, the sam
  - name: Blank or Invalid Cells
    text: 'If a cell is empty or contains a malformed string, `cell.getDateTime()`
      throws a `CellsException`. Guard against this with a simple check:'
  - name: Time Component
    text: The example only includes a date, but if your Excel file also stores time
      (e.g., “令和3年5月10日 14:30”), Aspose.Cells will preserve the time portion. The
      `LocalDateTime` you receive will include hours, minutes, and seconds.
  type: HowTo
tags:
- Java
- Excel
- DateTime
title: Japán korszak dátumának feldolgozása Excelből Java-ban – Teljes útmutató
url: /hu/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Japán era dátum feldolgozása Excelből Java‑ban – Teljes útmutató

Valaha is szükséged volt **parse Japanese era date** értékek feldolgozására, amelyek egy Excel munkafüzetben vannak tárolva, de nem tudtad, hogyan alakítsd át őket egy szokásos gregorián `DateTime`‑ná? Nem vagy egyedül – sok fejlesztő ütközik ebben a problémában, amikor régi japán könyvelési táblázatokkal vagy kormányzati űrlapokkal dolgozik. A jó hír, hogy néhány Java sorral és a megfelelő könyvtárral könnyedén **read date from Excel cell** és **extract datetime from Excel cell** anélkül, hogy manuális karakterlánc‑manőverekre lenne szükség.

Ebben a tutorialban egy teljes, futtatható példán keresztül mutatjuk be, hogyan lehet **parse Japanese era date** karakterláncokat, például a „令和3年5月10日” értéket Java `java.time.LocalDateTime`‑ná alakítani. Bemutatjuk a szükséges Maven függőséget, elmagyarázzuk, miért kell engedélyezni az era‑érzékeny feldolgozást, és rámutatunk a gyakori buktatókra. A végére egy stabil, production‑ready kódrészletet kapsz, amelyet bármely Java projektbe be lehet illeszteni.

## Prerequisites

- Java 17 vagy újabb (a kód Java 8‑on is működik)
- Maven vagy Gradle build rendszer
- Alapvető ismeretek az Excel fájlokról
- Az **Aspose.Cells for Java** könyvtár (a ingyenes próba verzió teszteléshez elegendő)

Ha bármelyik pont ismeretlennek tűnik, ne aggódj – pontosan megmutatom, hogyan adhatod hozzá a könyvtárat és hogyan kezdhetsz bele.

## Step 1: Add Aspose.Cells to Your Project

Először is szükséged van arra a könyvtárra, amely érti a japán era dátumokat. Az Aspose.Cells elvégzi a nehéz munkát helyetted.

**Maven**:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for latest version -->
</dependency>
```

**Gradle**:

```groovy
implementation 'com.aspose:aspose-cells:24.9'
```

Miután a függőség feloldódott, elkezdheted írni a kódot, amely *reads date from Excel cell* és *extracts datetime from Excel cell*.

## Step 2: Create a Workbook and Target the First Worksheet

Kezdjük egy új munkafüzet létrehozásával a memóriában, és vegyük a első lapot. Ez tükrözi az eredeti példa első két sorát.

```java
import com.aspose.cells.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize workbook and worksheet
        Workbook workbook = new Workbook();               // creates a blank workbook
        Worksheet sheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

Miért kezdünk egy friss munkafüzettel? Ez garantálja a tiszta környezetet, ahol minden beállítást kontrollálhatunk – ez kritikus, amikor később engedélyezzük az era‑érzékeny feldolgozást.

## Step 3: Put a Japanese Era Date String into Cell A1

Most szimulálunk egy Excel fájlt, amely már tartalmaz egy japán era dátumot. Valódi környezetben valószínűleg egy meglévő `.xlsx`‑t töltesz be, de a bemutatáshoz **write**-eljük a értéket magunk.

```java
        // Step 3: Insert a Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日"); // Reiwa 3rd year = 2021-05-10
```

A karakterlánc a szabványos japán jelölést követi: *Era* + *Year* + *Month* + *Day*. Extra konfiguráció nélkül az Aspose.Cells ezt egyszerű szövegként kezeli, nem dátumként.

## Step 4: Enable Era‑Aware Date Parsing

Itt jön a lényeg: mondd meg a munkafüzetnek, hogy **parse Japanese era date** karakterláncokkal találkozik, akkor konvertálja őket. Ezt a `ParseDateUsingJapaneseEra` kapcsolóval teheted meg.

```java
        // Step 4: Turn on era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);
```

Miért szükséges ez? Alapértelmezés szerint az Aspose.Cells a gregorián naptárat használja, így a „令和3年5月10日” szöveg marad karakterlánc. A kapcsoló engedélyezése azt mondja a motornak, hogy a háttérben `java.util.Date`‑re (vagy a `java.time` megfelelőjére) konvertálja.

## Step 5: Retrieve the Parsed DateTime Value

Most, hogy a munkafüzet tudja, hogyan értelmezze az era‑dátumot, kérhetjük a cellát a `DateTime` reprezentációjáért.

```java
        // Step 5: Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime(); // returns java.util.Date
        // Convert to java.time.LocalDateTime for modern APIs
        java.time.Instant instant = javaDate.toInstant();
        java.time.ZoneId zone = java.time.ZoneId.systemDefault();
        java.time.LocalDateTime dateTime = java.time.LocalDateTime.ofInstant(instant, zone);
```

Vedd észre, hogy **read date from Excel cell** a `cell.getDateTime()`‑vel történik. A metódus egy `java.util.Date`‑et ad vissza, amelyet azonnal `LocalDateTime`‑ra konvertálunk a jobb típusbiztonság érdekében. Ez teljesíti az **extract datetime from excel cell** követelményt egy tiszta, idiomatikus módon.

## Step 6: Verify the Result

Végül nyomtassuk ki a gregorián dátumot, hogy megerősítsük a konverzió sikerességét.

```java
        // Step 6: Output the Gregorian date
        System.out.println(dateTime); // Expected output: 2021-05-10T00:00
    }
}
```

A program futtatásakor a következőt kell látnod:

```
2021-05-10T00:00
```

Ez a kimenet bizonyítja, hogy sikeresen **parse Japanese era date**, **read date from Excel cell**, és **extract datetime from Excel cell** egyetlen folyamatban.

## Handling Real‑World Edge Cases

### Multiple Eras

Japánnak több era van (Meiji, Taishō, Shōwa, Heisei, Reiwa). A `setParseDateUsingJapaneseEra(true)` kapcsoló automatikusan lefedi mindet, de vedd figyelembe, hogy a régebbi dátumok esetleg kívül esnek a könyvtár támogatott tartományán (általában 1868‑tól napjainkig). Ha például a „昭和45年12月31日” értékkel találkozol, ugyanaz a kód 1970‑12‑31‑re konvertálja.

### Blank or Invalid Cells

Ha egy cella üres vagy hibás karakterláncot tartalmaz, a `cell.getDateTime()` `CellsException`‑t dob. Ezt egyszerű ellenőrzéssel elkerülheted:

```java
if (cell.getType() == CellValueType.IS_DATE) {
    // safe to call getDateTime()
} else {
    System.out.println("Cell does not contain a parsable date.");
}
```

### Time Component

A példa csak dátumot tartalmaz, de ha az Excel fájlod időt is tárol (pl. „令和3年5月10日 14:30”), az Aspose.Cells megőrzi az időrészt is. A kapott `LocalDateTime` tartalmazni fogja az órákat, perceket és másodperceket.

## Full Working Example

Mindent egy helyen, itt a teljes, másolás‑beillesztés kész program:

```java
import com.aspose.cells.*;
import java.time.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Insert Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日");

        // Enable era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);

        // Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime();
        LocalDateTime dateTime = javaDate.toInstant()
                                         .atZone(ZoneId.systemDefault())
                                         .toLocalDateTime();

        // Output the Gregorian date
        System.out.println(dateTime); // 2021-05-10T00:00
    }
}
```

Mentsd el `JapaneseEraDateParser.java` néven, fordítsd `javac`‑vel, és futtasd `java`‑val. Ha minden helyesen van beállítva, a konzolra a gregorián dátum kerül kiírásra.

## Pro Tips & Common Pitfalls

- **Pro tip:** Mindig állítsd be a `setParseDateUsingJapaneseEra(true)`‑t **before** bármely cellaértéket olvasol. A kapcsoló módosítása egy cella olvasása után nem fogja retroaktívan konvertálni a már beolvasott értéket.
- **Watch out for locale:** A könyvtár az era karakterláncokat Unicode karakterek alapján dolgozza fel, így nem kell külön japán locale‑t beállítanod.
- **Performance note:** Az era‑feldolgozás engedélyezése apró teljesítménybeli többletet jelent. Ha csak néhány cellára van szükséged, ideiglenesen kapcsolhatod be a flag‑et, elolvashatod a cellákat, majd újra kikapcsolhatod.
- **Testing:** Használd az Aspose ingyenes próba verzióját, hogy valós Excel fájlon teszteld, amely több era dátumot tartalmaz. Így biztos lehetsz benne, hogy a production kódod a várt módon viselkedik.

## Conclusion

Most bemutattuk, hogyan **parse Japanese era date** értékeket olvashatsz közvetlenül egy Excel munkafüzetből Java és Aspose.Cells segítségével. Az era‑érzékeny feldolgozás engedélyezésével **read date from Excel cell** és **extract datetime from Excel cell** tiszta, típus‑biztos módon valósítható meg. A megközelítés bármely modern japán era‑ra működik, kezeli az időkomponenseket, és elegánsan kezeli a hibás adatokat.

Készen állsz a következő kihívásra? Próbáld meg betölteni egy valódi `.xlsx` fájlt, amely keverve tartalmaz gregorián és japán era dátumokat, vagy kísérletezz a kapott `LocalDateTime` formázásával a saját locale‑odnak megfelelően. Esetleg írd vissza a konvertált dátumokat Excelbe, hogy a downstream rendszerek csak gregorián dátumokat lássanak.

Van kérdésed vagy egy szokatlan edge case‑ba ütköztél? Hagyj egy megjegyzést alább, és jó kódolást!

## What Should You Learn Next?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutató technikáira építenek. Minden forrás komplett, működő kódrészleteket és lépésről‑lépésre magyarázatot tartalmaz, hogy további API funkciókat saját projektjeidben is könnyedén elsajátíthasd.

- [Mesteri 1904-es dátumrendszer az Excelben Aspose.Cells Java használatával a hatékony cellaműveletekhez](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Hatékony Excel‑PDF konvertálás egyedi dátumformátumokkal Aspose.Cells for Java segítségével](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Hogyan válassz cellatartományokat Excelben Aspose.Cells for Java használatával (2023-as útmutató)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}