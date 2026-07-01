---
category: general
date: 2026-06-30
description: Rendezze a egyedi értékeket Excelben Java használatával. Tanulja meg,
  hogyan állítson be képletet, számítsa újra a képleteket, és generáljon egyedi listát
  Excelben az Aspose.Cells segítségével.
draft: false
keywords:
- sort unique values excel
- how to set formula
- how to recalculate formulas
- generate unique list excel
- set array formula
language: hu
og_description: Rendezd a egyedi értékeket Excelben Java-val. Ez az útmutató megmutatja,
  hogyan állíts be képletet, hogyan számítsd újra a képleteket, és hogyan generálj
  egyedi listát Excelben percek alatt.
og_title: Egyedi értékek rendezése Excelben – Java útmutató tömbképletekhez
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  headline: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  type: TechArticle
- description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  name: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  steps:
  - name: How It Works
    text: '- `UNIQUE(B1:B10)` scans the range and returns a vertical array of distinct
      strings. - `SORT(...)` takes that array and orders it in ascending order. -
      Wrapping the whole thing in `=` and calling `setFormulaArray` tells Aspose.Cells
      to treat the result as a **spilled array**, just like Excel would.'
  - name: Empty Cells in the Source Range
    text: 'If `B1:B10` contains blanks, `UNIQUE` will treat them as a distinct entry.
      To ignore blanks, wrap the range with `FILTER`:'
  - name: Non‑Contiguous Data
    text: 'When your data lives in multiple columns, you can join them with `CHOOSE`
      or `TEXTJOIN` before applying `UNIQUE`. For example:'
  - name: ' ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Sort Excel Files by Cell Color Using Aspose.Cells Java&#58; A Comprehensive
      Guide](/cells/english/java/data-analysis/excel-file-sorting-aspose-cells-java/)
      - [Mastering Aspose.Cells Java&#58; How to Interrupt Formula Calculation in
      Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
      - [How to Create an Excel Data Validation List with Aspose.Cells for Java&#58;
      A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)

      {{< /blocks/products/pf/tutorial-page-section >}}'
    text: '{{< /blocks/products/pf/main-container >}} {{< /blocks/products/pf/main-wrap-class
      >}} {{< blocks/products/products-backtop-button >}}'
  type: HowTo
- questions:
  - answer: The `SORT` and `UNIQUE` functions are part of the Dynamic Array engine
      introduced in Excel 365. For legacy files you’d need to use classic array formulas
      like `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells
      can still evaluate them, but the syntax is more verbose.
    question: Does this work with older Excel versions (pre‑Office 365)?
  - answer: Absolutely. Just change the address in `cells.get("A1")`. The spilled
      array will always start at the cell you specify and expand right‑and‑down as
      needed.
    question: Can I set the array formula on a range other than `A1`?
  - answer: 'Replace the static range with a dynamic one, e.g., `B:B` or a named range.
      The formula becomes `=SORT(UNIQUE(B:B))`. Be cautious with whole‑column references
      on very large sheets; they can impact performance. --- ## Conclusion We’ve just
      covered **how to set formula** in Java to **sort unique values'
    question: What if my source data is larger than `B1:B10`?
  type: FAQPage
tags:
- Excel automation
- Java
- Aspose.Cells
title: Egyedi értékek rendezése Excelben – Teljes Java útmutató a tömbképletek beállításához
url: /hu/java/formulas-functions/sort-unique-values-excel-complete-java-guide-to-set-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Egyedi értékek rendezése Excelben – Teljes Java útmutató a tömbképletek beállításához

Gondolkodtál már azon, hogyan **rendezheted az egyedi értékeket Excelben** anélkül, hogy a képleteket húznád? Nem vagy egyedül. Sok jelentéskészítési helyzetben szükség van egy tiszta, ábécé sorrendbe rendezett listára a különböző bejegyzésekről, és a kézi megoldás fájdalmas.  

A jó hír? Néhány Java sorral **tömbképletet állíthatsz be** egy munkalapon, majd **újraszámíthatod a képleteket**, így a kiterjesztett tartomány automatikusan kitöltődik. Ebben az útmutatóban mindent végigvezetünk – a munkafüzet létrehozásától az Excel‑stílusú egyedi lista generálásáig – hogy a megoldást közvetlenül beágyazhasd az alkalmazásodba.

## Amit ez az útmutató lefed

- Java projekt beállítása az Aspose.Cells segítségével (az a könyvtár, amely a kódrészletet működteti).  
- `SORT` és `UNIQUE` függvények együttes használata a **egyedi lista Excelben** eredmények előállításához.  
- Programozottan **tömbképlet** alkalmazása egy cellára.  
- Számítási lépés indítása, hogy a **hogyan számítsuk újra a képleteket** lépés azonnal megtörténjen.  
- Az eredmény ellenőrzése és a megoldás finomhangolása olyan széljegyekre, mint az üres cellák vagy a nem összefüggő tartományok.

A útmutató végére képes leszel egy kész, használatra kész metódust beilleszteni bármely Java szolgáltatásba, amelynek tiszta Excel‑lapokat kell exportálnia.

> **Pro tipp:** Ha már Maven‑t használsz, az Aspose.Cells függőségként való hozzáadása megkímél a JAR fájlok kézi kezelésétől.

---

## Előfeltételek

| Requirement | Why it matters |
|-------------|----------------|
| Java 8 vagy újabb | Az Aspose.Cells a Java 8+ verziókat célozza. |
| Maven (vagy Gradle) | Megkönnyíti a függőségkezelést. |
| Aspose.Cells for Java | Biztosítja a `Workbook`, `Worksheet` és képlet API‑kat, amelyeket használni fogunk. |
| Alapvető ismeretek az Excel függvényekről | A `SORT` és `UNIQUE` megértése segít a kód testreszabásában. |

> *Ha még nincs Aspose.Cells, add hozzá ezt a `pom.xml`-hez*:

```xml
<!-- Aspose.Cells for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- latest as of June 2026 -->
</dependency>
```

---

## 1. lépés: Új munkafüzet létrehozása (A képlet beállítása itt kezdődik)

Először egy üres munkafüzetre van szükségünk. Gondolj rá úgy, mint egy üres vászonra, ahol később **tömbképletet állítunk be** az `A1` cellában.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // The rest of the steps follow...
```

> *Miért hozzunk létre új munkafüzetet?*  
> Garantálja a tiszta környezetet, elkerülve a rejtett képleteket, amelyek befolyásolhatják a tesztadatainkat.

---

## 2. lépés: Mintaadatok feltöltése (Opcionális, de hasznos)

A végeredmény tiszta láthatóságához töltsük fel a **B** oszlopot néhány ismétlődő bejegyzéssel.

```java
        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Sample data in B1:B10
        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }
```

> *Miért a B oszlopot használjuk?*  
> A képlet, amelyet írni fogunk, a `B1:B10` tartományra hivatkozik, így az adat ott tartása tükrözi a klasszikus Excel példát.

---

## 3. lépés: Tömbképlet beállítása, amely **rendez egyedi értékeket Excelben**

Most jön a varázslat. Kombináljuk a `UNIQUE`‑t (az ismétlődések eltávolításához) a `SORT`‑tal (az ábécé sorrendbe rendezéshez). Az eredmény egy **tömbképlet**, ami azt jelenti, hogy automatikusan kiterjed a szomszédos cellákra.

```java
        // Step 3: Set an array formula that sorts the unique values from B1:B10
        // This is the core of “how to set formula” for our scenario.
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");
```

### Hogyan működik

- `UNIQUE(B1:B10)` beolvassa a tartományt és egy függőleges tömböt ad vissza a különböző karakterláncokkal.  
- `SORT(...)` veszi ezt a tömböt és növekvő sorrendbe rendezi.  
- Az egész kifejezést `=`-vel körülvéve és a `setFormulaArray` hívásával az Aspose.Cells úgy kezeli az eredményt, mint egy **kiterjesztett tömböt**, akárcsak az Excel.

> **Megjegyzés:** Ha régebbi Excel‑verziót használsz, amelyik nem tartalmazza a `SORT` vagy `UNIQUE` függvényeket, visszatérhetsz a `SORT(UNIQUE(...))` megoldásra a **LET** függvénnyel, vagy használhatsz régi tömbképleteket (`=INDEX(...)`). Az útmutató a modern dinamikus tömb megközelítést helyezi előtérbe, mivel ez a legletisztább módja a **egyedi lista Excelben** generálásának ma.

## 4. lépés: Képletek újraszámítása, hogy a kiterjesztett tartomány feltöltődjön

Miután a képlet a helyén van, a munkafüzet nem értékeli ki automatikusan. Itt jön a **hogyan számítsuk újra a képleteket** lépés.

```java
        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();
```

`calculateFormula()` meghívása arra kényszeríti az Aspose.Cells‑t, hogy futtassa az Excel motorját, és kitöltse az `A1`, `A2`, … cellákat a rendezett egyedi értékekkel.

> *Miért ne hagyatkozzunk a lusta kiértékelésre?*  
> Szerver‑oldali környezetben gyakran szükség van az adat exportálásra (CSV, PDF, stb.) készen a számítás után, ezért egy explicit hívás garantálja a konzisztenciát.

## 5. lépés: Az eredmény ellenőrzése (Opcionális hibakeresés)

Mindig jó ötlet a kiterjesztett értékeket a konzolra kiírni – különösen, ha egy új API‑t tanulsz.

```java
        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break; // stop at first empty cell
            System.out.println("- " + value);
            row++;
        }

        // Optionally, save the workbook to inspect in Excel
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

A program futtatása kiírja:

```
Sorted unique list:
- Apple
- Banana
- Cherry
- Date
- Elderberry
- Fig
- Grape
```

Nyisd meg a `SortedUniqueValues.xlsx` fájlt, és ugyanazt az adatot fogod látni, amely `A1`‑től lefelé terjed.

## Széljegyek kezelése

### Üres cellák a forrástartományban

Ha a `B1:B10` tartalmaz üres cellákat, a `UNIQUE` külön bejegyzésként kezeli őket. Az üres cellák figyelmen kívül hagyásához a tartományt `FILTER`‑rel kell körülvenni:

```java
cells.get("A1").setFormulaArray("=SORT(UNIQUE(FILTER(B1:B10, B1:B10<>\"\")))");
```

### Nem összefüggő adatok

Ha az adataid több oszlopban vannak, a `UNIQUE` alkalmazása előtt összekapcsolhatod őket `CHOOSE` vagy `TEXTJOIN` segítségével. Például:

```java
cells.get("A1").setFormulaArray(
    "=SORT(UNIQUE(CHOOSE({1,2}, B1:B10, C1:C10)))"
);
```

Ezek a finomhangolások bemutatják a **képlet beállításának** rugalmasságát összetettebb helyzetekben.

## Teljes működő példa (Minden lépés egyben)

Az alábbiakban a teljes, futtatható Java program látható. Másold be a fejlesztői környezetedbe, add hozzá az Aspose.Cells függőséget, és nyomd meg a *Run* gombot.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2: Get the first worksheet and fill sample data
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }

        // Step 3: Set an array formula that sorts the unique values from B1:B10
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");

        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();

        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break;
            System.out.println("- " + value);
            row++;
        }

        // Save the workbook for visual verification
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

**Várt kimenet** (a konzolon látható) megegyezik a korábban tárgyalt rendezett, duplikátumoktól mentes listával. A generált Excel fájl megnyitása ugyanazokat az értékeket mutatja, amelyek `A1`‑től lefelé terjednek.

## Gyakran Ismételt Kérdések

**Q: Működik ez régebbi Excel verziókkal (Office 365 előtti)?**  
A: A `SORT` és `UNIQUE` függvények a Excel 365‑ben bevezetett Dinamikus Tömb motor részei. Régi fájlok esetén klasszikus tömbképleteket kell használni, például `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Az Aspose.Cells még mindig ki tudja értékelni őket, de a szintaxis bőbeszédűbb.

**Q: Beállíthatok tömbképletet más cellára, mint az `A1`?**  
A: Természetesen. Csak módosítsd a címet a `cells.get("A1")`‑ben. A kiterjesztett tömb mindig a megadott cellától indul, és jobbra‑lefelé bővül, ahogy szükséges.

**Q: Mi van, ha a forrásadatok nagyobbak, mint a `B1:B10`?**  
A: Cseréld le a statikus tartományt egy dinamikusra, például `B:B` vagy egy névvel ellátott tartományra. A képlet így lesz `=SORT(UNIQUE(B:B))`. Legyél óvatos a teljes oszlopra hivatkozásokkal nagyon nagy munkalapokon; ez befolyásolhatja a teljesítményt.

## Összegzés

Most átvettük, hogyan **állítsunk be képletet** Java‑ban a **egyedi értékek rendezéséhez Excelben**, hogyan **újraszámítsuk a képleteket**, és hogyan **generáljunk egyedi listát Excelben** az Aspose.Cells erőteljes API‑jával. A lépések egyszerűek: hozz létre egy munkafüzetet, töltsd fel az adatokat, alkalmazz egy tömbképletet, indítsd el a számítást, és ellenőrizd az eredményt.  

Innen tovább bővítheted – hozzáadhatsz feltételes formázást, exportálhatsz PDF‑be, vagy integrálhatod a metódust egy webszolgáltatásba, amely kész jelentéseket szolgáltat. A lényeg ugyanaz: hagyd, hogy az Excel saját függvényei végezzék a nehéz munkát, a Java pedig irányítsa a folyamatot.

Készen állsz az Excel automatizálásod fejlesztésére? Próbáld ki a `SORT` helyett a `SORTBY` használatát, hogy egy másodlagos oszlop szerint rendezz, vagy kísérletezz a `FILTER`‑rel, hogy kizárd azokat a sorokat, amelyek nem felelnek meg az üzleti szabályoknak. A lehetőségek gyakorlatilag végtelenek.

###

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}