---
category: general
date: 2026-10-07
description: Olvassa be a dátumot az Excelből Java-val az Aspose.Cells segítségével.
  Ez az útmutató megmutatja, hogyan kell feldolgozni a Japanese era dates, beolvasni
  a dátumot az Excel cellákból, és gyorsan kinyerni a datetime értékeket az Excel
  cellákból.
draft: false
keywords:
- read date from excel
- extract datetime from excel
- java excel date conversion
- japanese era date parsing
- aspose.cells java
lastmod: 2026-10-07
og_description: Olvassa be a dátumot az Excelből Java-val az Aspose.Cells segítségével.
  Ez az útmutató megmutatja, hogyan kell feldolgozni a Japanese era dates, beolvasni
  a dátumot az Excel cellákból, és néhány lépésben kinyerni a datetime értékeket az
  Excel cellákból.
og_image_alt: 'Developer guide: Read date from Excel in Java using Aspose.Cells'
og_title: Olvassa be a dátumot az Excelből Java-val az Aspose.Cells segítségével –
  teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Read date from Excel in Java with Aspose.Cells. This guide shows you
    how to parse Japanese era dates, read date from Excel cells, and extract datetime
    from Excel cells quickly.
  headline: Read date from Excel in Java with Aspose.Cells – full guide
  type: TechArticle
- description: Read date from Excel in Java with Aspose.Cells. This guide shows you
    how to parse Japanese era dates, read date from Excel cells, and extract datetime
    from Excel cells quickly.
  name: Read date from Excel in Java with Aspose.Cells – full guide
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
- read date from excel
- java excel date conversion
title: Olvassa be a dátumot az Excelből Java-val az Aspose.Cells segítségével – teljes
  útmutató
url: /hu/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dátum beolvasása Excelből Java-val az Aspose.Cells segítségével – teljes útmutató

Ha **read date from Excel** munkalapokat kell olvasnod, amelyek japán korszak karakterláncokat tartalmaznak, jó helyen jársz. Sok régi könyvelési vagy kormányzati táblázatban a dátum a „令和3年5月10日” formában van tárolva, és ennek átalakítása egy szabványos gregorián `LocalDateTime`-ra hibára hajlamos lehet. Ez a bemutató lépésről lépésre megmutatja, hogyan lehet engedélyezni a korszak‑érzékeny elemzést, beolvasni a cella értékét, és **extract datetime from Excel** az Aspose.Cells for Java használatával.

## Gyors válaszok
- **Melyik könyvtár kezeli a japán korszak dátumokat?** Aspose.Cells for Java.
- **Milyen Java verzió szükséges?** Java 17 vagy újabb (Java 8 is működik).
- **Szükség van licencre a teszteléshez?** Egy ingyenes próba elegendő a fejlesztéshez.
- **Ugyanaz a kód képes gregorián dátumok beolvasására?** Igen, az API automatikusan felismeri a formátumot.
- **Megmaradnak az időinformációk?** Teljesen – órák, percek és másodpercek is megmaradnak a konverzió során.

## Mi az a read date from Excel?
A “read date from Excel” kifejezés arra utal, hogy egy cella dátumértékét lekérjük, és azt egy Java dátum‑idő objektummá, például `java.time.LocalDateTime`‑má konvertáljuk. Az Aspose.Cells elrejti az alacsony szintű Excel bináris formátumot, így a dátumokkal manuális karakterlánc‑elemzés nélkül dolgozhatsz.

## Miért használjuk az Aspose.Cells-et a japán korszak elemzéséhez?
Az Aspose.Cells **50+ bemeneti és kimeneti formátumot** támogat, és több száz oldalas munkafüzeteket képes feldolgozni anélkül, hogy az egész fájlt a memóriába töltené. A beépített korszak‑érzékeny elemzője minden japán korszakot (Meiji, Taishō, Shōwa, Heisei, Reiwa) egyetlen API hívással gregorián dátummá alakít, ezzel megszüntetve a törékeny reguláris‑kifejezés kódot.

## Előfeltételek
- Java 17 (vagy Java 8+) telepítve a gépeden.
- Maven vagy Gradle build rendszer.
- Alapvető ismeretek az Excel fájlokkal kapcsolatban.
- Aspose.Cells for Java könyvtár (próba vagy licencelt verzió).

Ha bármelyik ismeretlennek tűnik, ne aggódj – a következő lépésben pontosan megmutatjuk, hogyan adhatod hozzá a könyvtárat.

## Hogyan olvassuk be a dátumot Excelből Java-ban?
Töltsd be a munkafüzetet, engedélyezd a korszak‑érzékeny elemzést, és kérd le a cellát a `DateTime` értékéért. A teljes folyamat **két sor funkcionális kóddal** megoldható, amint a könyvtár a classpath‑on van.

### 1. lépés: add Aspose.Cells a projektedhez

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

Miután a függőség feloldódik, elkezdheted használni az API-t a **read date from Excel** cellákhoz.

### 2. lépés: hozd létre a munkafüzetet és célozd meg az első munkalapot

A `Workbook` osztály egy teljes Excel fájlt képvisel a memóriában. Egy új példány létrehozása tiszta környezetet biztosít a következő elemzési lépésekhez.

```java
import com.aspose.cells.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize workbook and worksheet
        Workbook workbook = new Workbook();               // creates a blank workbook
        Worksheet sheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

### 3. lépés: helyezz egy japán korszak dátum karakterláncot az A1 cellába

Bemutatásként mi magunk írjuk be a korszak karakterláncot; a gyakorlatban egy meglévő `.xlsx` fájlt töltenél be.

```java
        // Step 3: Insert a Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日"); // Reiwa 3rd year = 2021-05-10
```

A szöveg a hagyományos japán mintát követi: *Era* + *Year* + *Month* + *Day*.

### 4. lépés: engedélyezd a korszak‑érzékeny dátum elemzést

Mondd meg az Aspose.Cells-nek, hogy a korszak karakterláncokat dátumként kezelje a `ParseDateUsingJapaneseEra` jelző beállításával.  
A `ParseDateUsingJapaneseEra` egy olyan tulajdonság, amely true értéknél automatikusan átalakítja a japán korszak karakterláncokat gregorián dátumokká.

```java
        // Step 4: Turn on era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);
```

Ezzel a jelzővel a könyvtár a „令和3年5月10日” karakterláncot egyszerű szövegként kezeli, és elveszítenéd az automatikus konverziót.

### 5. lépés: lekérni a feldolgozott DateTime értéket

Most kérd le a cellát a dátumábrázolásért. A `cell.getDateTime()` a cella értékét `java.util.Date` objektumként adja vissza. A metódus egy `java.util.Date`-et ad vissza, amelyet azonnal a modern `java.time.LocalDateTime`-re konvertálunk. A `LocalDateTime` egy Java osztály, amely dátumot és időt ábrázol időzóna nélkül.

```java
        // Step 5: Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime(); // returns java.util.Date
        // Convert to java.time.LocalDateTime for modern APIs
        java.time.Instant instant = javaDate.toInstant();
        java.time.ZoneId zone = java.time.ZoneId.systemDefault();
        java.time.LocalDateTime dateTime = java.time.LocalDateTime.ofInstant(instant, zone);
```

Ez típus‑biztonságosan teljesíti a **extract datetime from Excel** követelményt.

### 6. lépés: ellenőrizd az eredményt

Írd ki a gregorián dátumot, hogy megerősítsd a konverzió sikerességét.

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

A kimenet bizonyítja, hogy sikeresen **read date from Excel**, feldolgoztuk a japán korszakot, és egyetlen folyamatban **extracted datetime from Excel**.

## Valós környezetben előforduló szélsőséges esetek kezelése

### Több korszak

Japánnak több korszakja van (Meiji, Taishō, Shōwa, Heisei, Reiwa). A `setParseDateUsingJapaneseEra(true)` jelző automatikusan lefedi mindet, de vedd figyelembe, hogy a régebbi dátumok kívül eshetnek a könyvtár támogatott tartományán (általában 1868‑napjainkig). Ha például a „昭和45年12月31日” dátummal találkozol, ugyanaz a kód 1970‑12‑31‑re konvertálja.

### Üres vagy érvénytelen cellák

Ha egy cella üres vagy hibás karakterláncot tartalmaz, a `cell.getDateTime()` `CellsException`-t dob. Védd meg ezt egy egyszerű ellenőrzéssel:

```java
if (cell.getType() == CellValueType.IS_DATE) {
    // safe to call getDateTime()
} else {
    System.out.println("Cell does not contain a parsable date.");
}
```

### Idő komponens

A példa csak dátumot tartalmaz, de ha az Excel fájlod időt is tárol (pl. „令和3年5月10日 14:30”), az Aspose.Cells megőrzi az idő részt. A kapott `LocalDateTime` órákat, perceket és másodperceket is tartalmazni fog.

## Teljes működő példa

Mindent összevonva, itt a teljes, másolás‑beillesztés‑kész program:

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

## Pro tippek és gyakori buktatók

- **Pro tip:** Engedélyezd a `setParseDateUsingJapaneseEra(true)` **előtt**, mielőtt bármilyen cellaértéket olvasnál. A jelző későbbi módosítása nem konvertálja retroaktívan a már beolvasott cellákat.
- **Locale note:** Az elemző a Unicode karaktereken dolgozik, így nem szükséges explicit japán helyi beállítást megadni.
- **Performance:** A korszak elemzés elhanyagolható terhelést ad hozzá. Ha csak néhány cellához kell, csak azoknál kapcsolod be a jelzőt.
- **Testing:** Használd az Aspose ingyenes próbaverzióját, hogy egy valós munkafüzeten ellenőrizd, amely keveri a gregorián és korszak dátumokat. Ez biztosítja, hogy a termelési kód a várt módon működjön.

## Gyakran feltett kérdések

**Q: Használhatom ezt a megközelítést egy meglévő .xlsx fájllal?**  
A: Igen. Töltsd be a fájlt `new Workbook("path/to/file.xlsx")`‑vel, és ugyanaz a jelző feldolgozza a megtalált korszak karakterláncokat.

**Q: Mi történik, ha a cella gregorián dátumot tartalmaz?**  
A: A könyvtár a gregorián értéket változatlanul visszaadja; a korszak elemzés csak a korszak mintának megfelelő karakterláncokra hat.

**Q: Támogatja az Aspose.Cells a Meiji (1868) előtti dátumokat?**  
A: Nem. A 1868 előtti dátumok kívül esnek a támogatott tartományon, és egyszerű szövegként kezelődnek.

**Q: Hogyan kezeljem a nagy munkafüzeteket anélkül, hogy kimeríteném a memóriát?**  
A: Használd a `Workbook` konstruktort, amely `LoadOptions`‑t fogad a `setMemorySetting(MemorySetting.MemoryPreference)` beállítással, hogy adatfolyamon olvassa a fájlt a teljes betöltés helyett.

**Q: Szükséges-e kereskedelmi licenc a termelési használathoz?**  
A: Igen, egy érvényes Aspose.Cells licenc eltávolítja a kiértékelési korlátozásokat és lehetővé teszi a teljes teljesítményt.

## Mit érdemes legközelebb megtanulni?

Az alábbi bemutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Mesteri 1904-es dátumrendszer az Excelben Aspose.Cells Java használatával a hatékony cellaműveletekhez](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Hatékony Excel‑PDF konvertálás egyéni dátumformátumokkal az Aspose.Cells for Java használatával](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Hogyan válasszunk cellatartományokat Excelben az Aspose.Cells for Java használatával (2023-as útmutató)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

---

**Utolsó frissítés:** 2026-10-07  
**Tesztelve a következővel:** Aspose.Cells 24.12 for Java  
**Szerző:** Aspose

## Kapcsolódó bemutatók

- [Japán korszak dátum elemzése Excelből Java-ban – teljes útmutató](/cells/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/)
- [Excel fájl olvasása Java-val az Aspose.Cells segítségével – teljes útmutató](/cells/java/automation-batch-processing/aspose-cells-java-excel-manipulation/)
- [Excel munkafüzet mentése Aspose.Cells for Java‑val – teljes útmutató](/cells/java/automation-batch-processing/excel-workbook-automation-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}