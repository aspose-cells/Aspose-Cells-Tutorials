---
category: general
date: 2026-07-03
description: Dátum elemzése a helyi beállítások szerint a Java java.time API-jával.
  Tanulja meg a japán korszakformátum kezelését, a helyi dátumkonverziót és a robusztus
  Java dátumfeldolgozási technikákat.
draft: false
keywords:
- parse date with locale
- java date parsing
- japanese era format
- locale date conversion
- java time API
language: hu
og_description: Dátum elemzése helyi beállítással Java-ban a java.time API használatával.
  Ez az útmutató bemutatja a japán korszakformátum kezelését, a helyi beállítású dátumkonverziót,
  valamint a megbízható dátumfeldolgozás legjobb gyakorlatait.
og_title: Dátum feldolgozása helyi beállítással Java-ban – Teljes programozási útmutató
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Parse date with locale using Java’s java.time API. Learn Japanese era
    format handling, locale date conversion, and robust java date parsing techniques.
  headline: Parse Date with Locale in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Parse date with locale using Java’s java.time API. Learn Japanese era
    format handling, locale date conversion, and robust java date parsing techniques.
  name: Parse Date with Locale in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Define the Era Date String
    text: First, store the Japanese era string exactly as you receive it (e.g., from
      a CSV file or UI).
  - name: Build a Locale‑Aware Formatter
    text: Java’s **java.time API** lets you tie a `DateTimeFormatter` to a specific
      chronology (calendar system) and `Locale`. For the Japanese era we use `JapaneseChronology`.
  - name: Parse and Convert to Gregorian `LocalDate`
    text: Now we actually parse the string and transform the result into a classic
      `LocalDate` that any Java library can consume.
  - name: What if the input uses a different era symbol?
    text: Japanese eras change roughly every few decades. The formatter automatically
      recognises `M` (Meiji), `T` (Taisho), `S` (Showa), `H` (Heisei), and `R` (Reiwa).
      If you receive an older era not covered by the default `JapaneseChronology`,
      you’ll get a `DateTimeParseException`. In that case, verify the s
  - name: How to support other non‑Gregorian calendars?
    text: 'The pattern is identical; you just swap the chronology and locale. For
      example, Thai Buddhist dates (`BuddhistChronology`) look like this:'
  - name: Can I parse without an era symbol (pure year‑month‑day)?
    text: Yes—simply omit `G` from the pattern and use the default `ISO_LOCAL_DATE`
      formatter. That’s the classic *java date parsing* route for Gregorian strings.
  - name: What about lenient parsing (e.g., missing leading zeros)?
    text: Switch `ResolverStyle.STRICT` to `ResolverStyle.LENIENT`. Be aware that
      lenient mode may silently roll over invalid dates (e.g., `R5/13/40` becomes
      `2024‑02‑09`). For production code, strict mode is usually safer.
  type: HowTo
tags:
- java
- date-time
- localization
title: Dátum feldolgozása helyi beállítással Java-ban – Teljes lépésről‑lépésre útmutató
url: /hu/java/advanced-features/parse-date-with-locale-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dátum elemzése helyi beállítással Java‑ban – Teljes lépésről‑lépésre útmutató

Valaha szükséged volt már **parse date with locale** Java‑ban, de nem tudtad, mely osztályokat kellene használnod? Nem vagy egyedül – a nem‑görög naptárakkal vagy regionális formátumokkal való munka olyan, mintha egy titkos nyelvet kellene megfejteni. Ebben az útmutatóban egy valós példán keresztül mutatjuk be: hogyan alakítsunk át egy japán era karakterláncot, például `R5/04/01`-t egy szabványos gregorián `2023‑04‑01` `Date` objektummá. A végére egy újrahasználható mintát kapsz bármely helyi beállításhoz specifikus dátumformátumhoz.

Mindent lefedünk a szükséges importálásoktól a szélsőséges esetek kezeléséig, és néhány kapcsolódó koncepciót is belevágunk – *java date parsing*, *japanese era format*, *locale date conversion* és a modern *java time API* – hogy a megoldást saját projektjeidhez tudod igazítani. Nincsenek külső könyvtárak, csak tiszta Java 8+.

---

## Mit fed le ez az útmutató

- A **Japanese era** (`Reiwa`) formátumú karakterlánc beállítása.
- `DateTimeFormatter` használata `JapaneseChronology`-val és egy `Locale`-al.
- Az eredményül kapott `JapaneseDate` átalakítása `LocalDate`-ra (Gregorian).
- A végső ISO‑8601 dátum kiírása.
- Gyakori buktatók, például nem támogatott korszakok vagy nem egyező minták.
- Gyors variációk más helyi beállításokhoz (Thai Buddhist, Islamic, stb.).

**Előfeltételek**  
JDK 8 vagy újabb, alapvető ismeret a `java.time`-ról, valamint egy IDE vagy CLI a Java kód futtatásához. Ennyi—nincs extra Maven függőség.

## Dátum elemzése helyi beállítással – Lépésről‑lépésre

Az alábbiakban a megoldást három logikus lépésre bontjuk. Minden lépés tartalmazza a szükséges pontos kódot, egy rövid magyarázatot arra, *miért* fontos, és egy tippet, amit a hivatalos dokumentációban nem biztos, hogy megtalálsz.

### 1. lépés: Az era dátum karakterlánc definiálása

Először tárold a japán era karakterláncot pontosan úgy, ahogy kapod (pl. CSV fájlból vagy felhasználói felületről).

```java
// Step 1: Define a date string using the Japanese era format (Reiwa 5)
String eraDateString = "R5/04/01";
```

> **Miért fontos ez:**  
> Az elején lévő `R` a *Reiwa* korszakot jelöli, Japán jelenlegi era. Ha figyelmen kívül hagyod az era jelölőt, a parser a gregorián naptárat fogja feltételezni, és helytelen évet eredményez.

### 2. lépés: Helyi beállításra érzékeny formázó létrehozása

A Java **java.time API** lehetővé teszi, hogy egy `DateTimeFormatter`-t egy adott kronológiához (naptárrendszer) és `Locale`-hoz kössünk. A japán era esetén a `JapaneseChronology`-t használjuk.

```java
import java.time.chrono.JapaneseChronology;
import java.time.format.DateTimeFormatter;
import java.time.format.ResolverStyle;
import java.util.Locale;

// Step 2: Create a formatter that understands the Japanese era pattern
DateTimeFormatter japaneseFormatter = new DateTimeFormatterBuilder()
        .parseCaseInsensitive()
        .appendPattern("Gyy/MM/dd")          // G = era symbol, yy = year-of-era
        .toFormatter(Locale.JAPAN)           // Locale for Japanese symbols
        .withChronology(JapaneseChronology.INSTANCE)
        .withResolverStyle(ResolverStyle.STRICT);
```

**Fontos pontok**  
- `G` elemzi az era szöveget (`R` a Reiwa, `H` a Heisei, stb.).  
- `ResolverStyle.STRICT` arra kényszeríti a parse‑t, hogy elutasítsa a lehetetlen dátumokat, mint például `R0/13/32`.  
- A `Locale` `Locale.JAPAN`-ra állítása biztosítja, hogy az era szimbólumok megfeleljenek a japán konvencióknak.

> **Pro tipp:** Ha *több* era formátumot kell támogatnod (pl. `HEISEI` teljes névben), add hozzá a `.parseCaseInsensitive()`-t a példában látható módon, és bővítsd a mintát `Guuuu`-ra a teljes nevekhez.

### 3. lépés: Parsolás és átalakítás gregorián `LocalDate`-ra

Most ténylegesen parse‑oljuk a karakterláncot, és az eredményt egy klasszikus `LocalDate`-ra alakítjuk, amelyet bármely Java könyvtár felhasználhat.

```java
import java.time.LocalDate;
import java.time.chrono.JapaneseDate;

// Step 3: Parse the era string and convert to Gregorian LocalDate
JapaneseDate japaneseDate = JapaneseDate.from(japaneseFormatter.parse(eraDateString));
LocalDate gregorianDate = LocalDate.from(japaneseDate);

// Verify the conversion
System.out.println(gregorianDate);   // Expected output: 2023-04-01
```

**Magyarázat**  
`JapaneseDate.from(...)` egy a japán naptárhoz kötött dátumobjektumot hoz létre. A `LocalDate.from(...)` meghívásával eltávolítjuk az era információt, és megkapjuk az ekvivalens ISO‑8601 dátumot – tökéletes tároláshoz, összehasonlításhoz vagy API hívásokhoz.

> **Miért konvertálunk?** A legtöbb adatbázis, REST szolgáltatás és harmadik fél könyvtára gregorián dátumot vár. A konverzió a parse‑olási rutinon belül tartása megakadályozza a későbbi finom hibákat.

## Teljes működő példa

Mindent összevonva, itt egy önálló, azonnal futtatható Java osztály. Nyugodtan másold be a `ParseDateWithLocale.java` fájlba és futtasd.

```java
import java.time.LocalDate;
import java.time.chrono.JapaneseChronology;
import java.time.chrono.JapaneseDate;
import java.time.format.DateTimeFormatter;
import java.time.format.DateTimeFormatterBuilder;
import java.time.format.ResolverStyle;
import java.util.Locale;

public class ParseDateWithLocale {

    public static void main(String[] args) {
        // --- Step 1: Input ---
        String eraDateString = "R5/04/01";

        // --- Step 2: Formatter ---
        DateTimeFormatter japaneseFormatter = new DateTimeFormatterBuilder()
                .parseCaseInsensitive()
                .appendPattern("Gyy/MM/dd")
                .toFormatter(Locale.JAPAN)
                .withChronology(JapaneseChronology.INSTANCE)
                .withResolverStyle(ResolverStyle.STRICT);

        // --- Step 3: Parse & Convert ---
        JapaneseDate japaneseDate = JapaneseDate.from(japaneseFormatter.parse(eraDateString));
        LocalDate gregorianDate = LocalDate.from(japaneseDate);

        // Output
        System.out.println("Original era string: " + eraDateString);
        System.out.println("Converted Gregorian date: " + gregorianDate);
    }
}
```

**Várt konzolkimenet**

```
Original era string: R5/04/01
Converted Gregorian date: 2023-04-01
```

Futtasd a programot a `javac ParseDateWithLocale.java && java ParseDateWithLocale` paranccsal. Ha a fenti két sort látod, sikeresen **parse date with locale**-t hajtottál végre.

## Szélsőséges esetek kezelése és gyakori kérdések

### Mi van, ha a bemenet más era szimbólumot használ?

A japán korszakok körülbelül néhány évtizedenként változnak. A formázó automatikusan felismeri a `M` (Meiji), `T` (Taisho), `S` (Showa), `H` (Heisei) és `R` (Reiwa) szimbólumokat. Ha egy régebbi era szimbólumot kapsz, amelyet az alapértelmezett `JapaneseChronology` nem fed le, `DateTimeParseException`-t kapsz. Ebben az esetben ellenőrizd a forrásadatot vagy biztosíts egy egyedi leképezést.

### Hogyan támogassunk más nem‑görög naptárakat?

A minta azonos; csak a kronológiát és a locale‑t cseréled. Például a thai buddhista dátumok (`BuddhistChronology`) így néznek ki:

```java
DateTimeFormatter thaiFormatter = new DateTimeFormatterBuilder()
        .appendPattern("Gyy/MM/dd")
        .toFormatter(new Locale("th", "TH"))
        .withChronology(java.time.chrono.ThaiBuddhistChronology.INSTANCE);
```

### Parse‑olhatok era szimbólum nélkül (csak év‑hónap‑nap)?

Igen – egyszerűen hagyd ki a `G`-t a mintából, és használd az alapértelmezett `ISO_LOCAL_DATE` formázót. Ez a klasszikus *java date parsing* útvonal a gregorián karakterláncokhoz.

### Mi a helyzet a laza (lenient) parsolással (pl. hiányzó vezető nullák)?

Cseréld a `ResolverStyle.STRICT`-t `ResolverStyle.LENIENT`-re. Vedd figyelembe, hogy a laza mód csendben átalakíthatja a hibás dátumokat (pl. `R5/13/40` → `2024‑02‑09`). Gyártási kódban a szigorú mód általában biztonságosabb.

## Pro tippek a robusztus helyi beállítású dátumkonverzióhoz

1. **Cache the formatter** – A `DateTimeFormatter` létrehozása viszonylag olcsó, de ha másodpercenként ezrek dátumát parse‑olod, tárold egy static final mezőben.  
2. **Validate input length** – Egy egyszerű `if (eraDateString.length() != 8)` ellenőrzés elkerülheti a felesleges parse‑kivételket.  
3. **Log the original string** – A helyi beállítási problémák hibakeresésekor a nyers bemenet gyakran felfedi a láthatatlan karaktereket (null‑szélességű szóközök), amelyek megtörik a parse‑t.  
4. **Unit‑test each era** – Írj JUnit teszteket a `R`, `H`, `S` stb. era‑kra, hogy biztosítsd, a jövőbeli Java frissítések ne változtassák meg a leképezést.

## Következtetés

Most bemutattuk, hogyan **parse date with locale** Java‑ban a modern *java time API*, egy helyi beállításra érzékeny `DateTimeFormatter` és a `JapaneseChronology` segítségével. A teljes példa bemutatja az egész folyamatot – egy nyers japán era karakterlánctól egy tiszta gregorián `LocalDate`-ig – és felvértez a tudással, hogy a mintát más naptárakhoz, például a thai buddhista vagy iszlám rendszerekhez is adaptáld.

Következő lépések? Próbáld megcserélni a `JapaneseChronology`-t `ThaiBuddhistChronology`-ra vagy `HijrahChronology`-ra, és nézd meg, hogyan kezeli ugyanaz a kódszerkezet a teljesen eltérő kulturális naptárakat. Emellett felfedezheted a kapott `LocalDate` visszaformázását helyi beállítású karakterláncra a `DateTimeFormatter.ofLocalizedDate(FormatStyle.FULL)` használatával.

Van egy bonyolult locale vagy váratlan parse‑hiba? Írj egy megjegyzést alább, és közösen megoldjuk. Boldog kódolást!

## Mit érdemes legközelebb megtanulni?

Az alábbi útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Mastering Data Presentation in Excel: Number and Custom Date Formatting with Aspose.Cells for Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Efficiently Convert Excel to PDF with Custom Date Formats Using Aspose.Cells for Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Master the 1904 Date System in Excel Using Aspose.Cells Java for Effective Cell Operations](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}