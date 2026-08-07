---
category: general
date: 2026-07-03
description: Tartalmazza a képletek exportálását Java-ban, hogy az Excel cellákat
  szöveggé konvertálja az Aspose.Cells segítségével. Tanulja meg, hogyan nyomtassa
  ki az Excel tartományt, és hogyan szerezze meg hatékonyan a cellaértékek karakterláncát.
draft: false
keywords:
- include formulas export
- convert excel cells text
- print excel range
- export table options
- get cell values string
language: hu
og_description: Tartalmazza a képletek exportálását Java-ban az Excel cellák szöveggé
  konvertálásához. Lépésről lépésre útmutató, amely megmutatja, hogyan nyomtassuk
  ki az Excel tartományt, és hogyan szerezzük meg a cellaértékeket karakterláncként.
og_title: Formulák exportálása Java-ban – Excel cellák szöveggé konvertálása
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  headline: Include Formulas Export in Java – Convert Excel Cells to Text
  type: TechArticle
- description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  name: Include Formulas Export in Java – Convert Excel Cells to Text
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles with older versions but we’ll stick
      to the latest LTS). - Aspose.Cells for Java 23.10 (or any recent release)—you
      can grab it from Maven Central. - A sample `input.xlsx` placed in a folder you
      control (the path is hard‑coded in the example for clarity).'
  - name: Optional Tweaks
    text: '- `eto.setExportHiddenRows(true);` – include rows hidden in Excel. - `eto.setExportHiddenColumns(true);`
      – same for columns. - `eto.setExportAsHTML(true);` – get HTML instead of plain
      text.'
  - name: Expected Output (sample)
    text: '``` =SUM(A2:A3) 42 Hello =IF(B1>10,"Yes","No") =AVERAGE(C1:C3) =VLOOKUP(A1,Sheet2!A:B,2,FALSE)
      ```'
  - name: What if the range contains merged cells?
    text: Merged cells are treated as the value of the top‑left cell. The rest of
      the merged area will appear as empty strings. If you need the merged region’s
      address, query `Cell.getMergedRange()` before export.
  - name: Can I export a massive sheet (hundreds of thousands of rows)?
    text: Yes, but beware of memory consumption. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to let Aspose.Cells stream data to disk. Also, consider exporting in chunks
      (e.g., 10 000 rows at a time) to keep the string manageable.
  - name: How do I change the column delimiter?
    text: '`ExportTableOptions` exposes `setSeparator(char separator)`. For CSV‑style
      output, set it to `'',''`:'
  - name: Do formulas respect external references?
    text: If a formula points to another workbook, Aspose.Cells will keep the reference
      text (`='[Other.xlsx]Sheet1'!A1`). It won’t evaluate the external value unless
      you load that workbook as well.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Export
title: Formulák exportálása Java-ban – Excel cellák szöveggé konvertálása
url: /hu/java/excel-import-export/include-formulas-export-in-java-convert-excel-cells-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Képletek exportálásának beillesztése Java-ban – Excel cellák szöveggé konvertálása

Valaha szükséged volt **include formulas export** funkcióra, amikor adatot nyertél ki egy Excel munkafüzetből? Lehet, hogy egy jelentési szolgáltatást építesz, amelynek meg kell őriznie az eredeti képleteket, miközben egy rendezett szöveges adatblokkot ad vissza. Ebben az esetben jó helyen vagy. Ez az útmutató végigvezet a Excel cellák egyszerű szöveggé konvertálásán—*beleértve* minden beágyazott képletet—az Aspose.Cells for Java használatával.

Meg fogunk érinteni azt is, hogyan **print Excel range**, módosíthatod a **export table options** beállításokat, és végül **get cell values string**-et, amelyet naplózhatsz, elküldhetsz egy API-n keresztül, vagy elhelyezhetsz egy adatbázisban. A végére egy teljesen futtatható kódrészletet és szilárd megértést kapsz arról, hogy miért kell minden hívást használni.

## Mit fogsz elsajátítani

- Egy teljes, másolás‑és‑beillesztésre kész Java program, amely beolvassa a `.xlsx` fájlt, kiválaszt egy tartományt, és formázott karakterláncként exportálja.
- A `ExportTableOptions` osztály megértése, és hogy miért fontos a `setExportAsString` és a `setIncludeFormula` kapcsolása.
- Tippek nagy munkalapok kezeléséhez, különböző adattípusokkal való munkához, és a kimeneti formátum testreszabásához.
- Egy gyors ellenőrzőlista a gyakori buktatókhoz (gondolj egyesített cellákra, rejtett sorokra és a helyi beállításokhoz kötött számformátumokra).

### Előfeltételek

- Java 17 vagy újabb (a kód régebbi verziókkal is lefordítható, de a legújabb LTS-t használjuk).
- Aspose.Cells for Java 23.10 (vagy bármely friss kiadás) — letöltheted a Maven Centralból.
- Egy minta `input.xlsx` egy általad irányított mappában (az útvonal a példában keménykódolt a tisztaság kedvéért).

Ha már megvannak ezek, merüljünk el.

## 1. lépés: Projekt beállítása és függőségek hozzáadása

Először hozz létre egy Maven projektet (vagy Gradle-t, ha azt részesíted előnyben). Add hozzá az Aspose.Cells függőséget a `pom.xml`-hez:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Pro tipp:** Ha vállalati proxy-t használsz, győződj meg róla, hogy a tároló elérhető; különben a build “Could not resolve dependencies” hibával fog meghiúsulni.

Miután a Maven befejezte a letöltést, készen állsz Java kód írására.

## 2. lépés: A munkafüzet betöltése és a kívánt munkalap lekérése

A kódrészlet első sorában látható, hogyan nyiss meg egy meglévő munkafüzetet:

```java
// Step 1: Load the workbook
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Cseréld le a `YOUR_DIRECTORY`-t a fájl abszolút vagy relatív útvonalára. A `Workbook` konstruktor automatikusan felismeri a fájlformátumot (XLS, XLSX, CSV, stb.), így nem kell megadnod.

Ezután lekérjük az első lapot:

```java
// Step 2: Get the first worksheet
Worksheet ws = wb.getWorksheets().get(0);
```

Miért az első lap? Sok sablonban az adatok az első fülön vannak, de megadhatsz bármely indexet, vagy akár a `get("SheetName")`-t is használhatod, ha név alapján szeretnéd.

## 3. lépés: A kívánt exportálási tartomány meghatározása

Most jön a **convert excel cells text** művelet szíve. Az Aspose.Cells-nek megmondod, mely cellákat szeretnéd lekérni egy `Range` objektum létrehozásával:

```java
// Step 3: Create a range covering cells A1 to C3
Range rng = ws.getCells().createRange("A1:C3");
```

A `"A1:C3"` karakterlánc egy klasszikus A1‑stílusú cím. Programozottan is felépíthető:

```java
int firstRow = 0, firstCol = 0, totalRows = 3, totalCols = 3;
Range rng = ws.getCells().createRange(firstRow, firstCol, totalRows, totalCols);
```

Ez a rugalmasság akkor hasznos, ha a tartomány mérete dinamikus – például a legutóbb használt sort a `ws.getCells().getMaxDataRow()` segítségével olvasod.

## 4. lépés: Export Table Options beállítása a képletek belefoglalásához

Itt található a **include formulas export** varázslat. Alapértelmezés szerint az Aspose.Cells a *megjelenített* értékeket adja vissza. Ha egy cella `=SUM(A1:A3)` képletet tartalmaz, a számított értéket kapod, nem a képlet szövegét. Ennek módosításához állítsd be a `ExportTableOptions`-t:

```java
// Step 4: Set up export options to return the range as a string and include formulas
ExportTableOptions eto = new ExportTableOptions();
eto.setExportAsString(true);      // Forces the result to be a single string
eto.setIncludeFormula(true);      // Includes the underlying formula instead of the evaluated value
```

Miért mindkét jelző? A `setExportAsString(true)` azt mondja az API-nak, hogy a cellákat az alapértelmezett elválasztóval (oszlopoknál tab, soroknál új sor) fűzze össze. A `setIncludeFormula(true)` a forrásértéket a „megjelenített értékről” a „nyers képletre” változtatja. Ha csak értékeket akarsz, hagyd `false`-on.

### Opcionális finomhangolások

- `eto.setExportHiddenRows(true);` – a Excelben rejtett sorok exportálása.
- `eto.setExportHiddenColumns(true);` – ugyanaz oszlopokra.
- `eto.setExportAsHTML(true);` – HTML-t kap a sima szöveg helyett.

Nyugodtan kísérletezz; az options osztály egy **export table options** játszótér.

## 5. lépés: A tartomány lekérése formázott karakterláncként

Most lekérjük az adatokat:

```java
// Step 5: Retrieve the range values as a formatted string using the options
String txt = rng.getValueAsString(eto);
```

A visszakapott `txt` valahogy így néz ki (feltételezve, hogy az A1:C3 keverék értékeket és képleteket tartalmaz):

```
=SUM(A2:A3)	42	"Hello"
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Vedd észre, hogy a tab (`\t`) választja el az oszlopokat, az új sor (`\n`) pedig a sorokat. Később feloszthatod a karakterláncot, ha 2‑D tömbre van szükséged:

```java
String[] rows = txt.split("\n");
for (String row : rows) {
    String[] cells = row.split("\t");
    // Process each cell...
}
```

## 6. lépés: Az eredmény kiíratása – “Print Excel Range” egyszerűen

Végül a karakterláncot a konzolra írjuk:

```java
// Step 6: Print the resulting string
System.out.println(txt);
```

A program futtatása kiírja a fenti pontos kimenetet. Innen a karakterláncot naplófájlba írhatod, HTTP-n keresztül elküldheted, vagy NoSQL dokumentumban tárolhatod.

## Teljes, azonnal futtatható példa

Összeállítva, itt a teljes program. Másold, illeszd be, és nyomd meg a **Run**‑t – nincs hiányzó import.

```java
import com.aspose.cells.*;

public class ExportFormulaRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook
        Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // Define the range A1:C3 (adjust as needed)
        Range rng = ws.getCells().createRange("A1:C3");

        // Configure export options: string output + include formulas
        ExportTableOptions eto = new ExportTableOptions();
        eto.setExportAsString(true);
        eto.setIncludeFormula(true);

        // Get the string representation of the range
        String txt = rng.getValueAsString(eto);

        // Print the resulting text
        System.out.println(txt);
    }
}
```

### Várt kimenet (példa)

```
=SUM(A2:A3)	42	Hello
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Ha a munkafüzetben a számok dátumként vannak formázva, akkor a helyi beállításoknak megfelelő formátumban jelennek meg (pl. `2026‑07‑03`). Az ISO dátumok kényszerítéséhez módosíthatod a `ExportTableOptions`-t egy egyedi `NumberFormat`-tal.

## Szélsőséges esetek kezelése és gyakori kérdések

### Mi van, ha a tartomány egyesített cellákat tartalmaz?

Az egyesített cellákat a bal‑felső cella értékeként kezelik. A többi egyesített terület üres karakterláncként jelenik meg. Ha az egyesített terület címére van szükséged, a export előtt kérdezd le a `Cell.getMergedRange()`-t.

### Exportálhatok-e egy hatalmas munkalapot (több százezer sort)?

Igen, de vigyázz a memóriahasználatra. Használd a `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`-t, hogy az Aspose.Cells adatot a lemezre streamelje. Emellett fontold meg a darabolt exportálást (pl. 10 000 soronként), hogy a karakterlánc kezelhető maradjon.

### Hogyan változtathatom meg az oszlopelválasztót?

A `ExportTableOptions` rendelkezik a `setSeparator(char separator)` metódussal. CSV‑stílusú kimenethez állítsd `','`-ra:

```java
eto.setSeparator(',');
```

### A képletek figyelembe veszik a külső hivatkozásokat?

Ha egy képlet egy másik munkafüzetre mutat, az Aspose.Cells megőrzi a hivatkozás szövegét (`='[Other.xlsx]Sheet1'!A1`). Nem értékeli ki a külső értéket, hacsak nem töltöd be azt a munkafüzetet is.

## Pro tippek a termelésre kész kódhoz

- **Cache the workbook** ha a munkafüzetet olvasod a

## Mit érdemes következőként megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészletet tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Convert Excel to PDF in Java Using Aspose.Cells&#58; A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}