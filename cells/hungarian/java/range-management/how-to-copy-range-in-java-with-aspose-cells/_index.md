---
category: general
date: 2026-09-08
description: Hogyan másoljuk a tartományt Java-ban az Aspose.Cells használatával –
  tanulja meg a pivot tábla másolását, a pivot tábla duplikálását és a pivot tábla
  exportálását a formázás megőrzése mellett.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- duplicate pivot table
- export pivot table
- copy range with formatting
language: hu
lastmod: 2026-09-08
og_description: Hogyan másoljunk tartományt Java-ban az Aspose.Cells segítségével.
  Ez az útmutató megmutatja, hogyan másoljunk pivot táblát, duplikáljunk pivot táblát,
  és exportáljunk pivot táblát a formázás megőrzése mellett.
og_image_alt: Screenshot of Java code copying a pivot table range in Aspose.Cells
og_title: Hogyan másoljunk tartományt Java-ban – teljes Aspose.Cells útmutató
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  headline: How to copy range in Java with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  name: How to copy range in Java with Aspose.Cells
  steps:
  - name: Copy pivot table to an existing workbook
    text: 'If you need to **duplicate pivot table** inside a workbook that already
      has data, use the same `copyRange` call but point to a different destination
      address:'
  - name: Export pivot table only (without surrounding data)
    text: 'Sometimes you want just the pivot table, not the source data. Identify
      the pivot table’s display range via its `getPivotTable` method:'
  - name: Preserve conditional formatting
    text: 'Conditional formatting rules are part of the style collection. The `PasteType.ALL`
      flag already copies them, but you can be explicit:'
  - name: Edge cases and troubleshooting
    text: '| Situation | What to watch for | Recommended fix | |-----------|-------------------|-----------------|
      | Source and destination workbooks use different Excel versions | Some newer
      pivot features (e.g., data model) may not render correctly | Use the latest
      Aspose.Cells version and set `Workbook.setF'
  - name: Next steps
    text: '- Explore **copy range with formatting** for charts and images (use `PasteType.PICTURES`).
      - Automate batch processing: loop over multiple source files and consolidate
      their pivot tables into a summary workbook. - Combine this technique with Aspose.Slides
      to generate PowerPoint reports that embed th'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Hogyan másolhatunk tartományt Java-ban az Aspose.Cells segítségével
url: /hu/java/range-management/how-to-copy-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan másolhatunk tartományt Java-ban az Aspose.Cells segítségével

Ha **hogyan másolhat tartományt** Java-ban, az Aspose.Cells egyszerűvé teszi a feladatot. Akár egy egyszerű cellatömböt, akár egy teljes funkcionalitású pivot táblát mozgat, a könyvtár kezeli a másolási műveletet, miközben megőrzi a képleteket, stílusokat és a pivot gyorsítótárat. Ebben az útmutatóban megtanulja, hogyan **másolhat pivot táblát**, **duplikálhat pivot táblát**, és akár **exportálhat pivot táblát** egy új munkafüzetbe teljes formázással.

Az oktatóanyag mindent lefed a projekt beállításától a végső ellenőrzési lépésig, így a kódot azonnal futtathatja az olvasás után. Nincs szükség külső eszközökre az Aspose.Cells for Java JAR-on kívül.

## Előkövetelmények

- Java 17 (vagy bármely támogatott JDK) telepítve és konfigurálva az IDE-ben.
- Maven vagy Gradle a függőségkezeléshez (a példák Maven-t használnak).
- Egy forrás Excel fájl (`source.xlsx`), amely pivot táblát tartalmaz a `A1:H20` tartományban.
- Alapvető ismeretek a Java programozásban.

## 1. lépés: Aspose.Cells hozzáadása a projekthez

Az Aspose.Cells egy kereskedelmi könyvtár, de elérhető egy ingyenes értékelő verzió is. Adja hozzá a függőséget a `pom.xml`-hez:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

> **Pro tipp:** Ha inkább Gradle-t használ, az ekvivalens bejegyzés:
> ```gradle
> implementation 'com.aspose:aspose-cells:24.9'
> ```

A JAR hozzáadása hozzáférést biztosít a `Workbook`, `Worksheet`, `Range` és `CopyOptions` osztályokhoz, amelyeket a teljes útmutató során használunk.

## 2. lépés: A forrás munkafüzet betöltése és az első munkalap kiválasztása

A **hogyan másolhat tartományt** első része a munkafüzet megnyitása, amely a mozgatni kívánt adatokat tartalmazza.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // Select the first worksheet (index 0)
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

> **Miért fontos:** A munkafüzet megnyitása egy memóriában lévő reprezentációt hoz létre, amelyet az API a lemezre írt eredeti fájl érintése nélkül manipulálhat.

## 3. lépés: A pivot táblát tartalmazó tartomány meghatározása

A pivot tábla egy téglalap alakú blokkban él. Meg kell adnia ezt a blokkot, hogy az Aspose.Cells tudja, mit kell másolni.

```java
        // Define the range that holds the pivot table and its source data
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");
```

> **Megjegyzés:** A `createRange` metódus **még nem** másol semmit; csak egy `Range` objektumot hoz létre, amely a duplikálni kívánt cellákra mutat.

## 4. lépés: Új munkafüzet létrehozása és az első munkalap lekérése

Most hozza létre a cél munkafüzetet, ahol a másolt tartomány elhelyezkedik.

```java
        // Create an empty workbook for the destination
        Workbook destWorkbook = new Workbook();
        // Get its first (and only) worksheet
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);
```

> **Miért új munkafüzet?** Egy friss fájl garantálja, hogy rejtett stílusok vagy névvel ellátott tartományok ne zavarják a másolási műveletet, ami különösen fontos, amikor **exportálja a pivot táblát** egy külön fájlba.

## 5. lépés: A tartomány (a pivot táblával együtt) másolása a cél munkalapra

Ez a **hogyan másolhat tartományt formázással** magja. A `CopyOptions` objektum azt mondja az Aspose.Cells-nek, hogy mindent őrizzen meg: értékeket, képleteket, stílusokat és a pivot gyorsítótárat.

```java
        // Prepare copy options – preserve formatting and pivot cache
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // copies everything
        copyOptions.setSkipBlanks(false);        // keep blank cells

        // Copy the defined range to cell A1 of the destination sheet
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);
```

> **Pivot tábla másolása:** Mivel a forrás tartomány tartalmazza a pivot táblát, az API automatikusan duplikálja a pivot gyorsítótárat, így az új munkalap egy teljesen működőképes pivot táblát tartalmaz, amely pontosan úgy viselkedik, mint az eredeti.

## 6. lépés: A cél munkafüzet mentése

Végül írja a végeredményt a lemezre.

```java
        // Save the destination workbook
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

Amikor megnyitja a `dest.xlsx` fájlt, egy pontos másolatát fogja látni az eredeti pivot táblának, beleértve a formázást, szeletelőket és számított mezőket.

## Várható kimenet

- `dest.xlsx` egy **Sheet1** nevű munkalapot tartalmaz.
- A `A1:H20` cellák ugyanazt az adatot és pivot táblát tartalmazzák, mint a forrás.
- Minden cellastílus (betűtípusok, színek, szegélyek) megmarad.
- A pivot tábla teljesen interaktív; a frissítése tükrözi a másolt tartomány alatti adatokat.

## Hogyan másolhatunk tartományt formázással – mélyebb bemutató

Az előző példa a legegyszerűbb forgatókönyvet mutatja, de előfordulhatnak olyan változatok, amelyek kissé eltérő megközelítést igényelnek.

### Pivot tábla másolása meglévő munkafüzetbe

Ha egy **duplikálni kívánt pivot táblát** egy már adatot tartalmazó munkafüzetben szeretne, használja ugyanazt a `copyRange` hívást, de mutasson egy másik célcímre:

```java
// Assume destWorkbook already contains other sheets
Worksheet targetSheet = destWorkbook.getWorksheets().get(2);
targetSheet.getCells().copyRange(sourceRange, "B5", copyOptions);
```

### Csak a pivot tábla exportálása (a környező adatok nélkül)

Néha csak a pivot táblát szeretné, nem a forrás adatokat. Határozza meg a pivot tábla megjelenítési tartományát a `getPivotTable` metódus segítségével:

```java
PivotTable pt = sourceSheet.getPivotTables().get(0);
String ptArea = pt.getDisplayRange(); // e.g., "C5:G15"
Range pivotOnly = sourceSheet.getCells().createRange(ptArea);
destSheet.getCells().copyRange(pivotOnly, "A1", copyOptions);
```

### Feltételes formázás megőrzése

A feltételes formázási szabályok a stílusgyűjtemény részei. A `PasteType.ALL` jelző már másolja őket, de kifejezetten is beállíthatja:

```java
copyOptions.setPasteType(PasteType.FORMATS);
copyOptions.setPasteType(PasteType.ALL); // overrides previous, ensures everything
```

### Szélsőséges esetek és hibaelhárítás

| Helyzet | Mire kell figyelni | Javasolt megoldás |
|-----------|-------------------|-----------------|
| A forrás és a cél munkafüzetek különböző Excel verziókat használnak | Néhány újabb pivot funkció (pl. adatmodell) nem jelenik meg helyesen | Használja a legújabb Aspose.Cells verziót, és állítsa be a `Workbook.setFileFormatType(FileFormatType.XLSX)`-t mindkét munkafüzetnél |
| Nagyon nagy pivot táblák (> 10 000 sor) memória nyomást okoznak | Memóriahiányos hibák a másolás során | Engedélyezze a `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` beállítást a betöltés előtt |
| A cél munkalap már tartalmaz egy nevű tartományt, amelynek ugyanaz a neve, mint a forrásé | Névütközés `CopyOptions` hibához vezet | Hívja meg a `copyOptions.setIgnoreNameConflicts(true)` metódust |

## Teljes, futtatható példa

Az alábbiakban a teljes programot találja, amelyet egyszerűen beilleszthet egy Java osztályba. Tartalmazza az összes importot, hibakezelést és megjegyzéseket.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");

        // 3️⃣ Create a new destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Configure copy options to keep everything (values, formulas, formatting, pivot cache)
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        copyOptions.setSkipBlanks(false);
        copyOptions.setIgnoreNameConflicts(true); // avoid name collisions

        // 5️⃣ Perform the copy
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);

        // 6️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Copy completed – dest.xlsx now contains the duplicated pivot table.");
    }
}
```

Futtassa a programot, majd nyissa meg a `dest.xlsx` fájlt, hogy ellenőrizze, a pivot tábla pontosan úgy működik-e, mint az eredeti.

## Összegzés

Most már tudja, **hogyan másolhat tartományt** Java-ban az Aspose.Cells használatával, beleértve a **pivot tábla másolását**, **pivot tábla duplikálását**, és **pivot tábla exportálását** miközben minden formázást megőriz. A könyvtár elrejti az Excel XML struktúrájának alacsony szintű részleteit, így Ön a üzleti logikára koncentrálhat.

### Következő lépések

- Fedezze fel a **copy range with formatting** lehetőséget diagramok és képek esetén (használja a `PasteType.PICTURES`-t).
- Automatizálja a kötegelt feldolgozást: iteráljon több forrásfájl felett, és konszolidálja a pivot tábláikat egy összefoglaló munkafüzetbe.
- Kombinálja ezt a technikát az Aspose.Slides-szel, hogy PowerPoint jelentéseket generáljon, amelyek beágyazzák a másolt pivot táblát.

## Mihez érdemes tovább tanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [Hogyan frissíthető az Excel pivot tábla forrása Aspose.Cells for Java-val: Átfogó útmutató](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Pivot tábla betöltésének optimalizálása Java-ban az Aspose.Cells használatával – Átfogó útmutató](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [Hogyan másolhat pivot táblát C#‑ban – Excel konvertálása PPTX‑be, tartomány másolása és szövegdoboz létrehozása](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}