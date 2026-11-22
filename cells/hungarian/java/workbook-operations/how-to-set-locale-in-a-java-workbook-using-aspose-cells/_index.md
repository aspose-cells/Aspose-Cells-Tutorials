---
category: general
date: 2026-11-22
description: Tanulja meg, hogyan állíthatja be a területi beállítást egy Java munkafüzetben,
  hogyan változtathatja meg a munkafüzet nyelvét, és hogyan állíthatja a naptárat
  japánra, világos kódrészletekkel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set locale
- change workbook language
- set locale to japanese
- how to set calendar
language: hu
lastmod: 2026-11-22
og_description: Hogyan állítsuk be gyorsan a területi beállítást egy Java munkafüzetben.
  Kövesse ezt az útmutatót a munkafüzet nyelvének megváltoztatásához, a területi beállítás
  japánra állításához, és a japán naptár konfigurálásához.
og_image_alt: Screenshot showing how to set locale in a Java workbook
og_title: Hogyan állítsuk be a helyi beállítást egy Java munkafüzetben – lépésről
  lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  headline: How to set locale in a Java workbook using Aspose.Cells
  type: TechArticle
- description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  name: How to set locale in a Java workbook using Aspose.Cells
  steps:
  - name: Run the **FullLocaleExample** class.
    text: Run the **FullLocaleExample** class.
  - name: Open the generated `FullJapaneseLocale.xlsx` in Excel.
    text: Open the generated `FullJapaneseLocale.xlsx` in Excel.
  - name: 'Verify that:'
    text: 'Verify that:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Internationalization
- Workbook
title: Hogyan állítsuk be a helyi beállítást egy Java munkafüzetben az Aspose.Cells
  használatával
url: /hu/java/workbook-operations/how-to-set-locale-in-a-java-workbook-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan állítsuk be a locale-t egy Java munkafüzetben az Aspose.Cells használatával

A locale beállítása egy Java munkafüzetben gyakori követelmény, amikor a táblázatot különböző régiókhoz kell igazítani. Ebben az útmutatóban megtanulja, hogyan állítsa be a locale-t, hogyan változtassa meg a munkafüzet nyelvét, és hogyan állítsa be a naptárat japánra az Aspose.Cells API használatával.

Az egy munkafüzet nemzetköziesítése túlmutat a szöveg fordításán; befolyásolja a számformátumokat, a dátumfeldolgozást és az alapértelmezett naptárrendszert is. A tutorial végére képes lesz:

* Állítsa be a munkafüzet locale-ját japánra (Japán) – **set locale to japanese**.  
* Módosítsa a munkafüzet nyelvét, hogy a képletek és a felhasználói felület szövegei a célkultúrát kövessék – **change workbook language**.  
* Cserélje le a naptárat a japán császári naptárra – **how to set calendar**.  

A lépések bármelyik friss Aspose.Cells for Java (v23.9 vagy újabb) verzióval működnek, és csak egy szabványos Java fejlesztői környezetet igényelnek.

## Előkövetelmények

| Követelmény | Indoklás |
|-------------|----------|
| Java 8 vagy újabb | A könyvtár a Java 8+ verzióra céloz. |
| Aspose.Cells for Java (v23.9+) | Biztosítja a `Workbook`, `WorkbookSettings` és a locale segédfüggvényeket. |
| IDE (IntelliJ IDEA, Eclipse vagy VS Code) | A minta lefordításához és futtatásához. |
| Alapvető Java ismeretek | A kódrészletek megértéséhez szükséges. |

Adja hozzá az Aspose.Cells Maven függőséget a `pom.xml` fájlhoz (vagy töltse le a JAR-t manuálisan):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust for your JDK version -->
</dependency>
```

## Hogyan állítsuk be a locale-t és a naptárat egy munkafüzetben

Az első lépés egy munkafüzet példány létrehozása és a beállítási objektum lekérése. A beállítási objektum biztosítja a locale és a naptár API-kat.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookSettings;
import java.util.Locale;
import java.util.Calendar;

public class WorkbookLocaleDemo {
    public static void main(String[] args) {
        // Step 1: Create a new workbook (empty by default)
        Workbook workbook = new Workbook();

        // Step 2: Access the workbook's settings
        WorkbookSettings settings = workbook.getSettings();

        // Step 3: Set the calendar to the Japanese calendar
        // Aspose.Cells uses java.util.Calendar; the Japanese calendar is available via Calendar.JAPANESE
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // Step 4: Set the locale to Japanese (Japan)
        // This influences number formats, date formats, and built‑in function behaviour.
        settings.setLocale(new Locale("ja", "JP"));

        // Optional: Save the workbook to verify the settings
        workbook.save("LocaleDemo.xlsx");
    }
}
```

### Miért fontos minden sor

* **`new Workbook()`** – Létrehoz egy üres munkafüzetet, amelyet a mentés előtt módosíthat.  
* **`getSettings()`** – Visszaad egy `WorkbookSettings` objektumot; itt találhatók az összes regionális beállítás.  
* **`setCalendar(...)`** – Lecseréli az alapértelmezett gregorián naptárat a japán császári naptárra, befolyásolva a dátumok megjelenítését és feldolgozását.  
* **`setLocale(new Locale("ja","JP"))`** – Megváltoztatja a nyelvet és a regionális konvenciókat (pl. hónapok, tizedeselválasztók). Ez a **how to set locale** magja a munkafüzetben.  

A program futtatása létrehozza a `LocaleDemo.xlsx` fájlt. Nyissa meg Excelben vagy LibreOffice-ban, és láthatja a japán hónapneveket, a japán jen pénznem jeleit, valamint a japán naptár szerint formázott dátumokat.

## Munkafüzet nyelvének módosítása (locale beállítása japánra)

Ha az elsődleges célja a **munkafüzet nyelvének módosítása**, akkor csak a `setLocale` hívásra koncentrálhat. A következő kódrészlet elkülöníti ezt a lépést:

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Change only the language to Japanese (Japan)
settings.setLocale(new Locale("ja", "JP"));
workbook.save("JapaneseLanguage.xlsx");
```

**Mi változik?**  
* A cellaformázási karakterláncok japánra váltanak (pl. `#,##0.00` lesz `#,##0.00` jen jellel).  
* A beépített függvénynevek (például `SUM`) angolul maradnak, mivel az Excel függvénylocale-ja független, de a dátumkarakterláncok és hibaüzenetek japán konvenciókat követnek.

**Mikor használja?**  
* Amikor olyan táblázatra van szükség, amely számokat és dátumokat jelenít meg japán közönségnek, de az alapul szolgáló naptár maradhat gregorián.  
* Jelentések esetén, amelyeket PDF-be exportálnak vagy nyomtatnak, biztosítva, hogy a megjelenített nyelv megfeleljen a célpiacnak.

## Hogyan állítsuk be a naptárat a japán naptárra

Néha a **how to set calendar** igény különálló a locale-től. Régi rendszerek esetén, amelyek a japán császári korszakban tárolják a dátumokat, kifejezetten be kell állítani a naptárat, miközben opcionálisan megtartja az alapértelmezett locale-t.

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Set only the calendar; keep the default (US) locale
settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

// Verify the calendar by creating a date cell
int row = 0, column = 0;
workbook.getWorksheets().get(0).getCells().putValue(row, column, new java.util.Date());

// Save to see the Japanese era (e.g., "R3/04/01" for Reiwa 3)
workbook.save("JapaneseCalendar.xlsx");
```

**Kulcsfontosságú pontok:**

* `Calendar.getInstance(Locale.JAPAN)` egy `java.util.Calendar` objektumot ad vissza, amely a japán korszakra van beállítva.  
* A munkafüzet most már a korszak szimbólumait (R a Reiwa, H a Heisei stb.) használja a dátumok megjelenítéséhez.  
* Ez a beállítás **nem** befolyásolja a számformátumot vagy a felhasználói felület nyelvét; ha mindkettőre szükség van, kombinálja a `setLocale`-lel.

## Teljes, vég‑től‑végig példája

Az alábbiakban egy teljes, futtatható program látható, amely bemutatja a **how to set locale**, **change workbook language**, és **set the calendar** lépéseket egy koherens folyamatban. Emellett egy minta cellát is hozzáad a hatás illusztrálásához.

```java
import com.aspose.cells.*;
import java.util.*;

public class FullLocaleExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Access settings
        WorkbookSettings settings = workbook.getSettings();

        // 1️⃣ Set the locale to Japanese (Japan) – changes language & number formats
        settings.setLocale(new Locale("ja", "JP"));

        // 2️⃣ Set the calendar to the Japanese imperial calendar
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // 3️⃣ Add a sample date and number to visualize the changes
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Date cell – will show Japanese era after applying the calendar
        cells.putValue(0, 0, new Date());

        // Number cell – will use Japanese Yen symbol and comma separator
        cells.putValue(1, 0, 1234567.89);

        // Apply a style to the number cell for currency formatting
        Style style = cells.getRows().get(1).getStyle();
        style.setNumber(3); // Built‑in currency format
        cells.getRows().get(1).setStyle(style);

        // Save the workbook
        workbook.save("FullJapaneseLocale.xlsx");
        System.out.println("Workbook created with Japanese locale and calendar.");
    }
}
```

**Várható kimenet:**  
A `FullJapaneseLocale.xlsx` megnyitása mutatja, hogy az első cellában `R3/04/01` (Reiwa 3) típusú dátum, a második cella pedig `¥1,234,567.89` formátumban jelenik meg. Ez megerősíti, hogy a **how to set locale**, **change workbook language**, és **how to set calendar** mind együtt működik.

## Gyakori buktatók és hogyan kerüljük el őket

| Buktató | Miért fordul elő | Megoldás |
|---------|------------------|----------|
| A `Locale.CHINA` használata a `new Locale("ja","JP")` helyett | `Locale.CHINA` kínai nyelvet állít be, nem japánt. | Mindig a `Locale`-t `"ja", "JP"` értékekkel hozza létre japánhoz. |
| `settings.setCalendar(...)` hívás elfelejtése a `setLocale` után | A naptár alapértelmezés szerint gregorián, így a dátumok a rossz korszakban jelennek meg. | `setCalendar` hívása **a** locale beállítása **után**, vagy mindkettőt egyszerre beállítani, ahogy a példában látható. |
| A munkafüzet mentése a beállítások alkalmazása előtt | A beállítások csak a memóriában lévő objektumra vonatkoznak; a korai mentés az alapértelmezett locale-t írja. | Minden locale/naptár módosítást **a** `workbook.save()` hívása **előtt** alkalmazzon. |
| Elavult Aspose.Cells verzió használata | A régebbi verziók nem tartalmazzák a `setCalendar` túlterheléseket. | Frissítsen v23.9+ verzióra, vagy ellenőrizze a kiadási jegyzeteket a locale támogatásért. |

## A konfiguráció tesztelése

1. Futtassa a **FullLocaleExample** osztályt.  
2. Nyissa meg a generált `FullJapaneseLocale.xlsx` fájlt Excelben.  
3. Ellenőrizze, hogy:  
   * A dátum oszlop japán korszak szimbólumokat mutat (`R`, `H`, stb.).  
   * A szám oszlop jen jelet és vessző elválasztókat használ.  
   * A beépített hibaüzenetek (pl. `#DIV/0!`) japánul jelennek meg, ha a munkafüzet hibákat tartalmaz.

Ha bármelyik ellenőrzés nem sikerül, ellenőrizze újra, hogy a módosított `WorkbookSettings` objektum ugyanaz az példány-e, amelyet a mentéskor használ.

## Következő lépések

* **Képletek lokalizálása** – Bár a locale a formázást szabályozza, a `FormulaParser` segítségével egyéni függvényneveket is lefordíthat.  
* **Locale alkalmazása meglévő munkafüzetekre** – Töltsön be egy munkafüzetet a `new Workbook` segítségével

## Mit érdemes következőként megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeiben.

- [Aspose Cells Date Format: How to Set Custom Date Format in Java](/cells/english/java/formatting/aspose-cells-date-format-how-to-set-custom-date-format-in-ja/)
- [How to Set Language in Excel Files Using Aspose.Cells .NET for Multilingual Support](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [How to set cell number format and convert Japanese dates in C# using Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}