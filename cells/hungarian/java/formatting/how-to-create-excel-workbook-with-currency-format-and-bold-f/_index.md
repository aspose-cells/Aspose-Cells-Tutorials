---
category: general
date: 2026-08-20
description: Excel munkafüzet létrehozása Java-ban az Aspose.Cells segítségével, pénznem
  formátum beállítása, félkövér betű hozzáadása, és stílus tömb importálása a formázott
  cellákhoz.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set currency format
- format cells currency
- how to import style
- add bold font
language: hu
lastmod: 2026-08-20
og_description: Excel munkafüzet létrehozása Java-ban, pénznem formátum beállítása,
  félkövér betűk hozzáadása, és a stílus importálásának megtanulása az Aspose.Cells
  segítségével.
og_image_alt: Screenshot of an excel workbook created with currency format and bold
  font using Aspose.Cells
og_title: Excel munkafüzet létrehozása stílusos pénznem cellákkal Java‑ban
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  headline: How to create excel workbook with currency format and bold font in Java
  type: TechArticle
- description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  name: How to create excel workbook with currency format and bold font in Java
  steps:
  - name: Initialise the workbook and worksheet
    text: Creating a fresh workbook gives you a clean container for all subsequent
      formatting.
  - name: Build a DataTable with numeric data
    text: A `DataTable` mimics a database table, making it easy to import rows in
      bulk.
  - name: Define a style – currency format and bold font
    text: Here we **set currency format** and **add bold font** to a `Style` object.
  - name: Configure import options to use the style array
    text: Aspose.Cells lets you pass a `Style[]` via `ImportTableOptions`. This is
      the official **how to import style** method.
  - name: Import the DataTable into the worksheet
    text: Now we bring the data into the sheet at cell `A1`, applying the style array
      automatically.
  - name: Save the workbook to disk
    text: Finally, write the in‑memory workbook to a physical file.
  - name: Expected output
    text: 'When you open `DataTableWithStyleArray.xlsx` in Microsoft Excel, you should
      see:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Formatting
title: Hogyan hozzunk létre Excel munkafüzetet pénznem formátummal és félkövér betűtípussal
  Java-ban
url: /hu/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan hozzunk létre Excel munkafüzetet pénznemformátummal és félkövér betűtípussal Java-ban

Ha programozott módon **szeretnél Excel munkafüzetet létrehozni**, ez az útmutató pontosan megmutatja, hogyan. Végigvezetünk egy munkafüzet felépítésén, egy pénznemformátum alkalmazásán, félkövér betűtípus hozzáadásán, valamint az Aspose.Cells **style importálás** funkciójának használatán, hogy minden importált cella konzisztens legyen.

A végén egy kész `DataTableWithStyleArray.xlsx` fájlt kapsz, amely a számokat dollárként jeleníti meg és félkövérrel emeli ki őket. Nincs szükség kézi formázásra az Excelben.

## Előfeltételek

Mielőtt elkezdenéd, győződj meg róla, hogy a következők rendelkezésre állnak:

- Java 17 vagy újabb telepítve.
- Aspose.Cells for Java licenc (vagy egy ingyenes értékelő kulcs).
- Maven vagy Gradle a `aspose-cells` függőség kezeléséhez.
- Alapvető ismeretek a Java gyűjteményekről és a `DataTable`-ról.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

> **Pro tipp:** Ha `LicenseException` hibát kapsz, helyezd a licencfájlt a classpath-ba, és hívd meg a `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` sort a munkafüzet létrehozása előtt.

## Hogyan hozzunk létre Excel munkafüzetet stílusos pénznemcellákkal

Ez a szakasz tartalmazza a fő lépéseket. Minden lépés elmagyarázza, **miért** fontos, nem csak **mit** kell beírni.

### 1. lépés: A munkafüzet és a munkalap inicializálása

Egy friss munkafüzet létrehozása tiszta tárolót biztosít a további formázásokhoz.

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
Cells cells = worksheet.getCells();                     // shortcut to work with cells
```

> **Miért:** A `Workbook` objektum az egész Excel fájlt képviseli. Az első `Worksheet` elérése lehetővé teszi, hogy azonnal elkezdj adatot feltölteni.

### 2. lépés: DataTable felépítése numerikus adatokkal

A `DataTable` egy adatbázistáblát utánoz, így könnyű tömegesen importálni a sorokat.

```java
// Step 2: Build a DataTable with sample numeric data
DataTable dataTable = new DataTable();
dataTable.getColumns().add("Amount", DataType.DOUBLE); // column type DOUBLE ensures numeric handling
dataTable.getRows().add(new Object[]{1234.56});
dataTable.getRows().add(new Object[]{7890.12});
```

> **Miért:** A `DOUBLE` használata garantálja, hogy az értékek megtartják a tizedes pontosságukat, ami elengedhetetlen a későbbi **cellák pénznemformázásához**.

### 3. lépés: Stílus definiálása – pénznemformátum és félkövér betűtípus

Itt **beállítjuk a pénznemformátumot** és **hozzáadjuk a félkövér betűtípust** egy `Style` objektumhoz.

```java
// Step 3: Define a style (currency format and bold font) for the imported cells
Style currencyStyle = workbook.createStyle();                // create a reusable style instance
currencyStyle.getNumber().setFormat("$#,##0.00");            // set currency format (e.g., $1,234.56)
currencyStyle.getFont().setBold(true);                      // make the font bold
Style[] styleArray = new Style[] { currencyStyle };          // style array required by ImportTableOptions
```

> **Miért:** A `Number` formátum string `$#,##0.00` azt mondja az Excelnek, hogy a cellát pénzügyi értékként kezelje, míg a `setBold(true)` kiemeli a számokat. A stílus tömbbe helyezése felkészít a **style importálás** lépésre.

### 4. lépés: Importálási beállítások konfigurálása a stílus tömb használatához

Az Aspose.Cells lehetővé teszi, hogy egy `Style[]`-t adjunk át `ImportTableOptions`‑on keresztül. Ez a hivatalos **style importálás** módszer.

```java
// Step 4: Set up import options to use the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(styleArray); // tells the importer to apply our currencyStyle to every column
```

> **Miért:** `ImportTableOptions` nélkül az importált cellák az alapértelmezett stílust öröklik, elveszítve a pénznemformázást és a félkövér megjelenést, amelyet definiáltunk.

### 5. lépés: DataTable importálása a munkalapba

Most a `DataTable`-t a `A1` cellától kezdve importáljuk, a stílus tömböt automatikusan alkalmazva.

```java
// Step 5: Import the DataTable into the worksheet at A1, applying the style
cells.importDataTable(dataTable, true, "A1", importOptions);
```

- `true` jelzi, hogy a `DataTable` első sora oszlopfejléceket tartalmaz.
- `"A1"` a bal‑felső sarok, ahol az importálás kezdődik.

> **Miért:** A stílus tömbbel történő importálás garantálja, hogy minden importált cella megkapja a korábban előkészített **cellák pénznemformázása** stílust.

### 6. lépés: A munkafüzet mentése lemezre

Végül az memóriában lévő munkafüzetet egy fizikai fájlba írjuk.

```java
// Step 6: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/DataTableWithStyleArray.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to: " + outputPath);
```

> **Miért:** A mentés rögzíti a formázást, lehetővé téve, hogy te vagy a downstream folyamatok a fájlt a kívánt megjelenéssel nyissák meg Excelben.

## Teljes forráskód

Az alábbiakban a komplett, azonnal futtatható Java osztály látható. Másold be a kedvenc IDE-dbe, cseréld le a `YOUR_DIRECTORY`‑t egy létező mappára, és futtasd.

```java
import com.aspose.cells.*;

public class StyleArrayImportTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Step 2: Build a DataTable with sample numeric data
        DataTable dataTable = new DataTable();
        dataTable.getColumns().add("Amount", DataType.DOUBLE);
        dataTable.getRows().add(new Object[]{1234.56});
        dataTable.getRows().add(new Object[]{7890.12});

        // Step 3: Define a style (currency format and bold font) for the imported cells
        Style currencyStyle = workbook.createStyle();
        currencyStyle.getNumber().setFormat("$#,##0.00");   // set currency format
        currencyStyle.getFont().setBold(true);             // add bold font
        Style[] styleArray = new Style[] { currencyStyle };

        // Step 4: Set up import options to use the style array
        ImportTableOptions importOptions = new ImportTableOptions();
        importOptions.setStyleArray(styleArray);           // how to import style

        // Step 5: Import the DataTable into the worksheet at A1, applying the style
        cells.importDataTable(dataTable, true, "A1", importOptions);

        // Step 6: Save the workbook to a file
        workbook.save("YOUR_DIRECTORY/DataTableWithStyleArray.xlsx");
        System.out.println("Workbook created successfully.");
    }
}
```

### Várt kimenet

Amikor megnyitod a `DataTableWithStyleArray.xlsx` fájlt a Microsoft Excelben, a következőt kell látnod:

| Amount |
|--------|
| **$1,234.56** |
| **$7,890.12** |

- A számok **pénznemformátummal** (`$` jel, két tizedesjegy) jelennek meg.
- Mindkét cella **félkövér** betűtípussal van formázva, így kiemelkednek.

## Gyakori variációk és szélhelyzetek

| Szenárió | Mit kell módosítani | Indoklás |
|----------|---------------------|----------|
| **Másik pénznem** | `currencyStyle.getNumber().setFormat("€#,##0.00");` | Euro szimbólum vagy bármely helyi specifikus formátum használata. |
| **Több oszlop különböző stílusokkal** | Hozz létre több `Style` objektumot, töltsd fel a `styleArray`‑t az oszlopok sorrendjének megfelelően. | Minden oszlop saját számformátummal, betűtípussal, háttérrel stb. rendelkezhet. |
| **Nagy adathalmazok** | `cells.importDataTable(dataTable, false, "A1", importOptions);` és állítsd be `importOptions.setImportDataOptions(ImportDataOptions.DATA_ONLY);` | Teljesítményjavítás fejlécek vagy felesleges metaadatok kihagyásával. |
| **Stílus alkalmazása import után** | `cells.get("A2").setStyle(currencyStyle);` egyedi cellákra. | Hasznos, ha csak a sorok egy részének kell speciális formázást adni. |

## Tippek a termeléshez

- **Licencelés előre**: Regisztráld az Aspose.Cells licencet a munkafüzet létrehozása előtt, hogy elkerüld az értékelő vízjelet.
- **Szálbiztonság**: A `Workbook` példányok **nem** szálbiztosak. Hozz létre külön példányt szálanként, ha sok fájlt generálsz párhuzamosan.
- **Memóriakezelés**: Nagyon nagy lapok esetén fontold meg a `Workbook` streaming API‑ját (`Workbook` → `WorkbookDesigner`) a memóriahasználat csökkentése érdekében.
- **Tesztelés**: Írj egységtesztet, amely Apache POI‑val megnyitja a mentett fájlt, és ellenőrzi, hogy a cella stílus számformátuma megegyezik a `"$#,##0.00"` értékkel.

## Összegzés

Most már tudod, hogyan **hozz létre Excel munkafüzetet** Java-ban, **állíts be pénznemformátumot**, **adj hozzá félkövér betűtípust**, és helyesen **importáld a stílust** az Aspose.Cells `ImportTableOptions` segítségével. Ez az end‑to‑end megoldás megszünteti a manuális Excel‑lépéseket, és garantálja, hogy minden importált cella ugyanazt a **cellák pénznemformázása** stílust kövesse.

Készen állsz a következő kihívásra? Próbáld ki a feltételes formázást, diagramok beágyazását, vagy a munkafüzet PDF‑be exportálását – mindezt ugyanazzal a stílus‑tömb technikával. Boldog kódolást!

## Mit érdemes következőként megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek az API további funkcióinak elsajátításában és alternatív megvalósítási megközelítések felfedezésében a saját projektjeidben.

- [Create an Excel Workbook using Aspose.Cells in Java: A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [How to Style Excel Cells and Add Hyperlinks Using Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}