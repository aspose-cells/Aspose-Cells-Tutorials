---
category: general
date: 2026-06-08
description: Szerezze meg a dátum‑idő értéket a cellából az Aspose.Cells Java segítségével,
  és tanulja meg, hogyan írjon értéket egy Excel‑cellába néhány lépésben.
draft: false
keywords:
- get datetime from cell
- write value to excel cell
- Aspose.Cells Java date parsing
- Japanese era calendar Excel
- Excel formula recalculation Java
language: hu
og_description: Szerezze meg a dátum‑idő értéket a cellából az Aspose.Cells Java segítségével.
  Ez a bemutató azt is megmutatja, hogyan írjon értéket hatékonyan egy Excel cellába.
og_title: Dátum és idő lekérése cellából Java Excelben – Teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Get datetime from cell using Aspose.Cells Java and learn how to write
    value to excel cell in just a few steps.
  headline: Get datetime from cell in Java Excel – Complete Guide
  type: TechArticle
- description: Get datetime from cell using Aspose.Cells Java and learn how to write
    value to excel cell in just a few steps.
  name: Get datetime from cell in Java Excel – Complete Guide
  steps:
  - name: What if the cell already contains a true Excel date?
    text: 'If `cell.getType()` returns `CellValueType.IS_DATE_TIME`, you can skip
      the recalculation step and read the value directly:'
  - name: How to process a whole column of era strings?
    text: 'Loop through the used range and apply the same settings once:'
  - name: Can I disable the Japanese era handling later?
    text: 'Yes—just flip the flag back:'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
title: Dátum és idő lekérése cellából Java Excelben – Teljes útmutató
url: /hu/java/cell-operations/get-datetime-from-cell-in-java-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dátum és idő lekérése cellából Java Excelben – Teljes útmutató

Valaha is szükséged volt **cellából dátum és idő lekérése**-re, de az érték japán era karakterláncnak tűnt? Nem vagy egyedül. Sok régi táblázatban a dátumok úgy vannak tárolva, mint „Reiwa 3/04/01”, és egy megfelelő `java.time.LocalDateTime` kinyerése úgy érződik, mintha egy titkos üzenetet kellene megfejteni.  

Szerencsére az Aspose.Cells for Java képes elvégezni a konverziót, és közben megmutatjuk, hogyan **érték írása Excel cellába** (A1), hogy adatot körkörösen mozoghass anélkül, hogy a munkalap logikáját megsértenéd.

Ebben az útmutatóban megtanulod:

* Hogyan hozzunk létre egy munkafüzetet, és célozzunk meg egy adott munkalapot.  
* A pontos lépések a japán era naptár engedélyezéséhez a feldolgozáshoz.  
* Miért kell újraszámolni a képleteket a dátum olvasása előtt.  
* Hogyan írjunk új értéket vissza egy cellába a formázás elvesztése nélkül.  

Nincs külső eszköz, nincs varázslat – csak egyszerű Java kód, amelyet ma bármely Maven projektbe beilleszthetsz.

---

## Előfeltételek

* **Java 8+** (a példa a modern `java.time` API-t használja).  
* **Aspose.Cells for Java** ≥ 23.9.0 – add hozzá a függőséget Maven vagy Gradle segítségével.  
* Alapvető ismeretek az Excel fogalmairól (munkalapok, cellák, képletek).  

Ha hiányzik a könyvtár, szerezd be a hivatalos Aspose tárolóból:

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9.0</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## 1. lépés: Új munkafüzet létrehozása és az első munkalap elérése

A kezdéshez szükségünk van egy friss `Workbook` objektumra. Gondolj rá úgy, mintha egy új Excel fájlt nyitnánk meg a memóriában.

```java
// Step 1: Initialize workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

*Miért fontos ez:*  
A munkafüzet programozott létrehozása teljes ellenőrzést ad a beállítások felett, mielőtt bármilyen adat a fájlrendszert érné. Az első munkalap (`index 0`) lesz, ahol a beolvasást és az írást is bemutatjuk.

---

## 2. lépés: Japán era dátum karakterlánc írása az A1 cellába

Most **érték írása Excel cellába** A1. Ez egy valós helyzetet tükröz, ahol egy felhasználó manuálisan beírta a „Reiwa 3/04/01” értéket.

```java
// Step 2: Write the era date string into A1
Cell cell = worksheet.getCells().get("A1");
cell.putValue("Reiwa 3/04/01"); // raw string, not yet a date
```

*Gyors tipp:* A `putValue` sokoldalú – elfogad karakterláncokat, számokat, dátumokat és még képleteket is. Ha egyszerű szöveget adsz át, az Aspose pontosan úgy tárolja, ahogy megadod, ami tökéletes a bemutatónkhoz.

---

## 3. lépés: Japán era naptár engedélyezése a dátumfeldolgozáshoz

Alapértelmezés szerint az Aspose.Cells a Gergely-naptárat használja. A „Reiwa” értelmezéséhez egy beállítást kapcsolunk át.

```java
// Step 3: Turn on Japanese era calendar support
WorkbookSettings settings = workbook.getSettings();
settings.setUseJapaneseEraCalendar(true);
```

*Miért engedélyezzük ezt?*  
A japán era naptár az era neveket (Reiwa, Heisei, Showa) a Gergely-egyenértékekhez rendeli. E flag nélkül a könyvtár a karakterláncot egyszerű szövegként kezeli, és soha nem kapsz megfelelő `DateTime` objektumot.

---

## 4. lépés: Képletek újraszámolása, hogy az era karakterlánc Gergely-dátummá alakuljon

Az Aspose nem automatikusan dolgozza fel a karakterláncot dátummá. Ehelyett a cellát egy képlet eredményeként kezeli egy számítási lépés után.

```java
// Step 4: Force a recalculation to convert the era string
workbook.calculateFormula(); // processes all cells, including A1
System.out.println(cell.getDateTime()); // → 2021‑04‑01
```

Amikor a `calculateFormula()` lefut, a motor felismeri az era mintát, alkalmazza a japán naptárat, és belsőleg tárolja a kapott Gergely-dátumot. A `getDateTime()` hívás ezután egy `java.util.Date` objektumot ad vissza (vagy átalakíthatod `java.time` típusra).

**Várható kimenet**

```
2021-04-01T00:00:00.000+00:00
```

---

## 5. lépés: Új érték írása vissza ugyanabba a cellába (vagy egy másikba)

Tegyük fel, hogy felül kell írnod az eredeti karakterláncot egy tiszta ISO‑8601 dátummal. Így **érték írása Excel cellába** biztonságosan, a cella stílusának megőrzésével.

```java
// Step 5: Overwrite A1 with a formatted date string
java.time.LocalDateTime now = java.time.LocalDateTime.now();
cell.putValue(now); // Aspose will store it as a proper Excel date
// Optional: apply a date format style
Style style = cell.getStyle();
style.setNumber(14); // built‑in "m/d/yyyy" format
cell.setStyle(style);
```

*Mi történik?*  
A `putValue` felismeri a `LocalDateTime` típust, és átalakítja Excel sorozatszám ábrázolásává. A számformátum beállítása biztosítja, hogy a cella a dátumot pontosan úgy jelenítse meg, ahogy elvárod, amikor Excelben nyitod meg.

---

## Teljes működő példa

Összegezve, itt egyetlen Java osztály, amelyet lefordíthatsz és futtathatsz. Létrehozza a munkafüzetet, beír egy era karakterláncot, konvertálja, majd végül elmenti a fájlt.

```java
import com.aspose.cells.*;

public class JapaneseEraDateDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first sheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ Write Japanese era date string to A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue("Reiwa 3/04/01");

        // 3️⃣ Enable Japanese era calendar
        WorkbookSettings settings = workbook.getSettings();
        settings.setUseJapaneseEraCalendar(true);

        // 4️⃣ Recalculate so the string becomes a Gregorian date
        workbook.calculateFormula();
        System.out.println("Converted date: " + cell.getDateTime());

        // 5️⃣ Overwrite with a clean LocalDateTime (optional)
        java.time.LocalDateTime now = java.time.LocalDateTime.now();
        cell.putValue(now);
        Style style = cell.getStyle();
        style.setNumber(14); // m/d/yyyy
        cell.setStyle(style);

        // 6️⃣ Save the workbook
        workbook.save("output.xlsx");
        System.out.println("Workbook saved as output.xlsx");
    }
}
```

Futtasd ezt a `java -cp aspose-cells-23.9.jar;. JapaneseEraDateDemo` paranccsal, és nyisd meg a **output.xlsx** fájlt. Látni fogod, hogy az A1 cella a jelenlegi dátumot mutatja, míg a konzol a konvertált „2021‑04‑01” értéket naplózza.

---

## Különleges esetek kezelése és gyakori kérdések

### Mi van, ha a cella már tartalmaz egy valódi Excel dátumot?

Ha a `cell.getType()` `CellValueType.IS_DATE_TIME` értéket ad vissza, kihagyhatod az újraszámolási lépést, és közvetlenül olvashatod az értéket:

```java
if (cell.getType() == CellValueType.IS_DATE_TIME) {
    System.out.println("Already a date: " + cell.getDateTime());
}
```

### Hogyan dolgozzunk fel egy egész oszlop era karakterláncait?

Iterálj a használt tartományon, és egyszer alkalmazd ugyanazokat a beállításokat:

```java
Range used = worksheet.getCells().getMaxDisplayRange();
for (int row = 0; row < used.getRowCount(); row++) {
    Cell c = used.getCell(row, 0); // column A
    c.putValue(c.getStringValue()); // re‑assign to trigger parsing
}
workbook.calculateFormula();
```

### Később letiltható a japán era kezelése?

Igen – egyszerűen állítsd vissza a flag-et:

```java
settings.setUseJapaneseEraCalendar(false);
```

Ne feledd, hogy újraszámolásra van szükség, ha az írás után módosítod a beállítást.

---

## Pro tippek és buktatók

* **Teljesítmény:** A japán era naptár engedélyezése kis teljesítménybeli többletet jelent. Ha csak néhány cellához szükséges, fontold meg a beállítás be- és kikapcsolását a feldolgozás során.  
* **Területi beállítások tudatossága:** Az era karakterláncnak pontosan a “EraName yy/MM/dd” mintát kell követnie. A „Reiwa” elírása (pl. „Rewa”) a cellát egyszerű szövegként hagyja.  
* **Mentési formátum:** A `Workbook.save("output.xlsx")` XLSX fájlt ír. Használd a `"output.xls"`-t, ha a régebbi bináris formátumra van szükség, de vedd figyelembe, hogy egyes funkciók (például az era feldolgozása) korlátozottak lehetnek.

---

## Összegzés

Most már tudod, hogyan **cellából dátum és idő lekérése** történik, ha a forrás japán era jelölést használ, és láttad, hogyan **érték írása Excel cellába** történik megfelelő formázással. A `setUseJapaneseEraCalendar(true)` beállítás és a képlet újraszámolásának kényszerítésével az Aspose.Cells áthidalja a régi era karakterláncok és a modern Gergely-dátumok közötti szakadékot – mindezt néhány Java sorral.

Mi a következő? Próbáld meg kiterjeszteni ezt a mintát más kulturális naptárakra (thai, hijri) vagy nagy munkafüzeteket kötegelt feldolgozni ugyanazzal a megközelítéssel. Ugyanazok az elvek – a megfelelő naptár engedélyezése, újraszámolás, majd olvasás/írás – mindenhol érvényesek.

Van egy nehéz dátumformátum, amit nem tudsz megoldani? Írj egy megjegyzést alább, és oldjuk meg együtt. Boldog kódolást!  

![Get datetime from cell example](https://example.com/images/get-datetime-from-cell.png "Get datetime from cell example")

## Mit érdemes legközelebb megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd az API további funkcióit, és alternatív megvalósítási megközelítéseket fedezhess fel saját projektjeidben.

- [Mesteri a 1904-es dátumrendszer használata Excelben Aspose.Cells Java-val a hatékony cellaműveletekhez](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Hogyan valósítsunk meg rekurzív cellaszámítást Aspose.Cells Java-val az Excel automatizálás fejlesztéséhez](/cells/english/java/calculation-engine/aspose-cells-java-recursive-cell-calculations/)
- [Hogyan konvertáljuk az Excel cellaneveket indexekre az Aspose.Cells for Java használatával: lépésről‑lépésre útmutató](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}