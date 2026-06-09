---
category: general
date: 2026-06-08
description: Hogyan használjuk a reduce függvényt az Excelben Java-val az Aspose.Cells
  segítségével. Tanulja meg a lambda képletet Excelben, a dinamikus tömböket Java-ban,
  hogyan írjon lambdát, és a reduce segítségével történő összeadást egy világos lépésről‑lépésre
  útmutatóban.
draft: false
keywords:
- how to use reduce
- lambda formula excel
- dynamic arrays java
- how to write lambda
- sum with reduce
language: hu
og_description: Hogyan használjuk a reduce-et Excelben Java-val. Mesteri szintű lambda
  képletek Excelben, dinamikus tömbök Java-ban, és a reduce használata összegzéshez
  egy teljes, futtatható példával.
og_title: Hogyan használjuk a Reduce-et Excelben Java-val – Lambda képlet útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  headline: How to Use Reduce in Excel with Java – Lambda Formula Guide
  type: TechArticle
- description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  name: How to Use Reduce in Excel with Java – Lambda Formula Guide
  steps:
  - name: What if I need a horizontal array instead of vertical?
    text: 'Swap the column/row arguments in `EXPAND`. For a horizontal spill across
      B1:F1:'
  - name: Can I use REDUCE to multiply instead of sum?
    text: 'Absolutely. Just change the lambda body:'
  - name: Does Aspose.Cells support custom LAMBDA functions?
    text: Yes, you can define named LAMBDA functions via the workbook’s `Names` collection,
      then call them like any built‑in formula. That’s a deeper dive for a later tutorial
      on **how to write lambda** functions that live beyond a single cell.
  - name: What about older Excel versions that don’t recognize REDUCE?
    text: If you target Excel 2019 or earlier, the engine will return `#NAME?`. In
      such cases
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
title: Hogyan használjuk a Reduce-et Excelben Java-val – Lambda képlet útmutató
url: /hu/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjuk a Reduce-et Excelben Java‑val – Lambda képlet útmutató

Gondolkodtál már azon, **hogyan használjuk a reduce-et** Excelben, amikor Java‑kódot írsz? Nem vagy egyedül. Sok fejlesztő akad el, amikor megpróbálja kombinálni az Excel új dinamikus tömb függvényeit a Java‑alapú automatizálással, és a válasz nem olyan titokzatos, mint elsőre tűnik.

Ebben az útmutatóban egy konkrét példán keresztül mutatjuk be, hogyan használjuk a **reduce-et** együtt egy **lambda formula Excel** kifejezéssel, mindezt az Aspose.Cells for Java könyvtár segítségével. A végére képes leszel dinamikus tömböket generálni Java‑ban, lambda függvényeket írni, és egy **összeget reduce‑el** kiszámolni – manuális táblázatkezelés nélkül.

---

## Amit építeni fogsz

- Egy teljesen Java‑ból létrehozott új munkafüzet.  
- Egy **EXPAND** dinamikus tömb, amely az A1:A5 cellákat tölti fel az 1‑5 számokkal.  
- Egy **REDUCE** képlet, amely összeadja ezeket a számokat egy **lambda formula Excel** segítségével.  
- Egy mentett `.xlsx` fájl, amelyet bármely táblázatkezelő programban megnyithatsz az eredmény ellenőrzéséhez.

Nincs külső makró, nincs VBA – csak tiszta Java kód és az Excel modern függvényei.

## Előfeltételek

- Java 17 (vagy bármely friss JDK) – a régebbi verziók is működnek, de lemaradsz a `var` szintaxis kényelmével.  
- Aspose.Cells for Java (az ingyenes próba verzió tökéletesen működik ebben a bemutatóban).  
- Alapvető ismeretek a Java szintaxisról és az Excel képletekről.

Ha újonc vagy a **dynamic arrays java** terén, ne aggódj – ez az útmutató minden részt részletesen elmagyaráz.

## 1. lépés: Projekt beállítása és az Aspose.Cells importálása

Először is, add hozzá az Aspose.Cells Maven függőséget a `pom.xml` fájlodhoz (vagy manuálisan szerezd be a JAR‑t).

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- latest as of June 2026 -->
</dependency>
```

> **Pro tipp:** Tartsd naprakészen a függőségeket; az újabb verziók javítják a képletértékelés sebességét, ami fontos, amikor **hogyan használjuk a reduce-et** nagy táblázatokban.

## 2. lépés: Munkafüzet létrehozása és az első munkalap elérése

Most létrehozunk egy vadon új munkafüzetet. Ez a kiindulópont a **hogyan használjuk a reduce-et** megtanulásához, mivel a munkafüzet objektum egy játszóteret biztosít a képletek elhelyezéséhez.

```java
// Step 2: Initialize a new workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet by default
```

*Miért fontos:* A `Workbook` osztály az egész Excel fájlt absztrahálja, míg a `Worksheet` egyetlen lapot képvisel. Később látni fogod, hogyan tud a **dynamic arrays java** egyetlen A1‑be helyezett képlettel sok cellát kitölteni.

## 3. lépés: Függőleges tömb generálása EXPAND‑del

Az Excel `EXPAND` függvénye képes értékeket kiterjeszteni egy tartományba. Ezt fogjuk használni az 1‑től 5‑ig terjedő számok oszlop A‑ban való létrehozásához.

```java
// Step 3: Write an EXPAND formula to produce 1‑5 vertically
Cell expandCell = worksheet.getCells().get("A1");
expandCell.setFormula("=EXPAND({1},5,1)"); // {1} is the seed, 5 rows, 1 column
expandCell.calculate(); // forces the engine to evaluate the formula now
```

Ha megnyitod a létrejött munkafüzetet, az A1:A5 cellák értéke 1, 2, 3, 4, 5 lesz. Ez a **dynamic arrays java** része – egy képlet tölti ki az egész tartományt.

## 4. lépés: REDUCE lambda írása a tömb összegzéséhez

Itt válaszolunk a fő kérdésre: **hogyan használjuk a reduce-et** Excelben Java‑ból. A `REDUCE` függvény egy tömbön iterál, és a megadott lambda‑t alkalmazza. Ebben az esetben összeadjuk a számokat.

```java
// Step 4: Use REDUCE with a LAMBDA to compute the sum of A1:A5
Cell reduceCell = worksheet.getCells().get("B1");
reduceCell.setFormula(
    "=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))"
);
reduceCell.calculate(); // forces evaluation immediately
```

Elemezzük ezt:

- `0` – a kezdeti akkumulátor érték (`acc`).  
- `A1:A5` – a **EXPAND**‑del generált tömb.  
- `LAMBDA(acc, x, acc + x)` – a **lambda formula Excel**, amely minden elemet (`x`) hozzáad az akkumulátorhoz (`acc`).  

Amikor a képlet fut, a `B1` **15**‑öt tartalmaz, ami a számok 1‑5 **összege reduce‑el**.

> **Hogyan írjunk lambda‑t** Excelben? Tekintsd úgy, mint egy névtelen függvényt, ahol az első argumentumok a paraméterek, és az utolsó kifejezés a visszatérési érték. Java‑ban csak beágyazzuk a szöveget; az Excel motor végzi a nehéz munkát.

## 5. lépés: Munkafüzet mentése

Végül a munkafüzetet lemezre mentjük, hogy megnyithasd Excelben, Google Sheets‑ben vagy bármely `.xlsx`‑et támogató megjelenítőben.

```java
// Step 5: Persist the workbook
String outputPath = "YOUR_DIRECTORY/new-functions.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Open the file and you’ll see:

| A | B |
|---|---|
| 1 | 15 |
| 2 |   |
| 3 |   |
| 4 |   |
| 5 |   |

A **összeg reduce‑el** a B1‑ben jelenik meg, ami megerősíti, hogy sikeresen bemutattuk, hogyan használjuk a **reduce-et** együtt egy **lambda formula Excel**‑lel Java‑ból.

## Teljes működő példa

Az alábbiakban a teljes, azonnal futtatható Java program található. Másold be a kedvenc IDE‑dbe, állítsd be a kimeneti könyvtárat, és nyomd meg a **Run** gombot.

```java
import com.aspose.cells.*;

public class ReduceLambdaDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ EXPAND – generate vertical array 1‑5 in A1:A5
        Cell expandCell = worksheet.getCells().get("A1");
        expandCell.setFormula("=EXPAND({1},5,1)");
        expandCell.calculate(); // evaluate now

        // 3️⃣ REDUCE – sum the values using a lambda
        Cell reduceCell = worksheet.getCells().get("B1");
        reduceCell.setFormula("=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))");
        reduceCell.calculate(); // evaluate now

        // 4️⃣ Save the workbook
        String outPath = "new-functions.xlsx";
        workbook.save(outPath);
        System.out.println("Workbook created at: " + outPath);
    }
}
```

**Várható kimenet** a `new-functions.xlsx` megnyitásakor:

- Az **A1:A5** cellák `1, 2, 3, 4, 5` értéket tartalmaznak.  
- A **B1** cella `15`‑öt jelenít meg, ami megerősíti a **összeg reduce‑el**.

## Gyakori kérdések és szélhelyzetek

### Mi van, ha vízszintes tömbre van szükségem a függőleges helyett?

Cseréld fel a `EXPAND` oszlop/sor argumentumait. Egy vízszintes kiterjesztéshez B1:F1 között:

```java
expandCell.setFormula("=EXPAND({1},1,5)");
```

### Használhatom a REDUCE‑t szorzásra az összeg helyett?

Természetesen. Csak módosítsd a lambda testét:

```java
reduceCell.setFormula("=REDUCE(1, A1:A5, LAMBDA(acc, x, acc * x))");
```

Ekkor a B1 `120`‑at fog mutatni (5 ! = 120).

### Támogatja az Aspose.Cells az egyedi LAMBDA függvényeket?

Igen, a munkafüzet `Names` gyűjteményén keresztül definiálhatsz névvel ellátott LAMBDA függvényeket, majd úgy hívhatod őket, mint bármely beépített képletet. Ez egy részletesebb bemutató egy későbbi útmutatóban a **hogyan írjunk lambda** függvényekről, amelyek egy cellán túl is léteznek.

### Mi van a régebbi Excel verziókkal, amelyek nem ismerik a REDUCE‑t?

Ha az Excel 2019 vagy korábbi verzióra célozol, a motor `#NAME?` hibát ad vissza. Ilyen esetekben

## Mit érdemes legközelebb tanulni?

Az alábbi útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes működő kódpéldákat és lépésről‑lépésre magyarázatokat tartalmaz, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Az Aspose.Cells Java mesterfogásai: Hogyan szakítsuk meg a képlet számítást Excel munkafüzetekben](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
- [Hogyan konvertáljunk Excel cellaneveket indexekre az Aspose.Cells for Java segítségével: Lépésről‑lépésre útmutató](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)
- [Hogyan hozzunk létre és formázzunk Excel cellákat az Aspose.Cells for Java segítségével: Lépésről‑lépésre útmutató](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}