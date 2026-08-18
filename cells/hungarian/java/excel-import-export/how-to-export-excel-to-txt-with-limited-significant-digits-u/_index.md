---
category: general
date: 2026-08-17
description: Exportálja az Excelt TXT formátumba a jelentős számjegyek korlátozásával
  – tanulja meg, hogyan állíthat be számjegyeket, és konvertálhatja az Excelt szöveggé
  Java‑ban egy teljes Aspose.Cells példával.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- how to set digits
- convert excel to text
- how to limit decimals
- limit significant digits
language: hu
lastmod: 2026-08-17
og_description: Exportálja az Excelt TXT formátumba, miközben korlátozza a jelentős
  számjegyeket. Ez az útmutató bemutatja, hogyan állíthatja be a számjegyeket, és
  konvertálhatja az Excelt szöveggé az Aspose.Cells for Java használatával.
og_image_alt: Java code exporting Excel to TXT with 4 significant digits
og_title: Excel exportálása TXT-be korlátozott számjegyekkel – Java útmutató
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  headline: How to export Excel to TXT with limited significant digits using Java
  type: TechArticle
- description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  name: How to export Excel to TXT with limited significant digits using Java
  steps:
  - name: Prerequisites
    text: '- Java 17 or later (the code compiles with Java 8 as well). - Aspose.Cells
      for Java 25.10 or newer. Download the JAR from the [Aspose website](https://products.aspose.com/cells/java)
      and add it to your project’s classpath. - An IDE or a simple text editor and
      command‑line build tool (Maven/Gradle).'
  - name: How the setting differs from “limit decimals”
    text: '- **limit decimals** (`setDecimalPlaces`) trims digits *after* the decimal
      point, regardless of the integer part. - **significant digits** (`setSignificantDigits`)
      counts digits from the first non‑zero digit, which is useful when numbers vary
      in magnitude.'
  - name: Expected output
    text: '| Cell | Original value | Exported (4 significant digits) | |------|----------------|---------------------------------|
      | A1 | 123.456789 | 123.5 |'
  - name: Exporting a whole range
    text: 'If you want to export more than one cell, simply fill the range before
      saving:'
  - name: Handling locale‑specific decimal separators
    text: 'Aspose.Cells respects the system locale when writing text. To force a dot
      (`.`) as the decimal separator, set the `TxtSaveOptions` culture:'
  - name: Overwriting existing files
    text: 'The `save` method overwrites the target file by default. If you need to
      avoid accidental data loss, check for file existence first:'
  - name: Large workbooks and memory usage
    text: 'When exporting very large worksheets, consider streaming the output:'
  - name: Next steps
    text: "- Explore other `TxtSaveOptions` properties such as `setDelimiter('\t')`
      to customize column separators. - Combine the exporter with `CsvSaveOptions`
      if you need comma‑separated values instead of plain text. - Integrate the routine
      into a web service that accepts uploaded Excel files and returns tri"
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel export
- TXT conversion
title: Hogyan exportáljunk Excel-t TXT-be korlátozott számjegyekkel Java használatával
url: /hu/java/excel-import-export/how-to-export-excel-to-txt-with-limited-significant-digits-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Excel to TXT with limited significant digits using Java

Ha **Excel‑t TXT‑be szeretnél exportálni** úgy, hogy a jelentős számjegyek számát szabályozod, ez az útmutató egy azonnal futtatható megoldást nyújt. Megmutatjuk, hogyan állítsd be a számjegyeket, konvertáld az Excelt szöveggé, és tartsd tisztán a kimenetet egyetlen konfigurációs módosítással.

A példa az Aspose.Cells for Java 25.10‑et használja, amely bevezeti a `setSignificantDigits` opciót. A tutorial végére olyan TXT fájlt tudsz generálni, amely csak a kívánt számjegyeket tartalmazza, extra kerekítési kód nélkül.

## What you’ll achieve

- Programozottan létrehozni egy munkafüzetet.
- Numerikus értéket beilleszteni egy cellába.
- TXT mentési beállításokat konfigurálni a jelentős számjegyek korlátozásához.
- A munkafüzetet egyszerű szövegfájlként menteni.
- Megérteni, hogyan működik a `significantDigits` beállítás, és hogyan alkalmazható más helyzetekben.

### Prerequisites

- Java 17 vagy újabb (a kód Java 8‑kal is lefordítható).
- Aspose.Cells for Java 25.10 vagy újabb. Töltsd le a JAR‑t a [Aspose website](https://products.aspose.com/cells/java) oldaláról, és add hozzá a projekt classpath‑éhez.
- IDE vagy egyszerű szövegszerkesztő és parancssori build eszköz (Maven/Gradle).

## Step 1: Set up the project and import Aspose.Cells

Hozz létre egy új Java projektet, és add hozzá az Aspose.Cells JAR‑t a build útvonalhoz. Ha Maven‑t használsz, add a következő függőséget a `pom.xml`‑hez:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Pro tip:** Használd a `jdk17` classifier‑t a legújabb Java futtatókörnyezethez; ez csökkenti a kompatibilitási figyelmeztetések kockázatát.

## Step 2: Create a workbook and write a value

A munkafüzet a memóriában lévő Excel‑fájlt reprezentálja. Bármely cellába adatot írhatsz a `putValue` metódussal.

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Put a numeric value into cell A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue(123.456789);
```

A `123.456789` szám lesz a forrásunk a TXT exporthoz. Alapértelmezés szerint az Aspose.Cells az összes tizedesjegyet kiírja, ami gyakran zajos szövegfájlokhoz vezet.

## Step 3: Configure TXT save options to limit significant digits

Az Aspose.Cells a `TxtSaveOptions`‑t biztosítja a szöveges kimenet finomhangolásához. A `setSignificantDigits` metódus azt mondja az exportálónak, hogy **összesen** hány számjegyet tartson meg, nem csak a tizedespont után.

```java
        // Configure TXT save options to keep only 4 significant digits
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4); // new option in 25.10
```

Ha a `significantDigits` értéke `4`, az exportáló a `123.456789` értéket `123.5`‑re kerekíti. Ez a viselkedés megfelel a jelentős számjegyek matematikai definíciójának: az első négy nem nulla számjegy marad meg.

### How the setting differs from “limit decimals”

- **limit decimals** (`setDecimalPlaces`) a tizedespont **utáni** számjegyeket vágja le, függetlenül az egész résztől.
- **significant digits** (`setSignificantDigits`) a legelső nem nulla számjegytől számolja a számjegyeket, ami akkor hasznos, ha a számok nagyságrendje változik.

Ha helyette fix számú tizedesjegyet szeretnél, cseréld le a fenti sort a következőre:

```java
saveOptions.setDecimalPlaces(2); // keeps two digits after the decimal point
```

## Step 4: Save the workbook as a TXT file

Most írd a munkafüzetet a lemezre a konfigurált beállításokkal.

```java
        // Save the workbook as a TXT file using the configured options
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

A program futtatása létrehozza a `significant_digits.txt` fájlt a munkakönyvtárban. A fájl egyetlen sort tartalmaz:

```
123.5
```

### Expected output

| Cell | Original value | Exported (4 significant digits) |
|------|----------------|---------------------------------|
| A1   | 123.456789     | 123.5                           |

Ha a `setSignificantDigits(4)`‑et `6`‑ra változtatod, a kimenet `123.457` lesz. Kísérletezz különböző értékekkel, hogy lásd, hogyan alkalmazkodik a kerekítés.

## Step 5: Common variations and edge cases

### Exporting a whole range

Ha több cellát szeretnél exportálni, egyszerűen töltsd fel a tartományt mentés előtt:

```java
worksheet.getCells().get("B1").putValue(0.0012345);
worksheet.getCells().get("C1").putValue(98765.4321);
```

Ugyanaz a `significantDigits` beállítás minden numerikus cellára vonatkozik, biztosítva a konzisztens pontosságot a teljes fájlban.

### Handling locale‑specific decimal separators

Az Aspose.Cells a rendszer locale‑ját veszi figyelembe szöveg írásakor. Ha pontot (`.`) szeretnél kényszeríteni a tizedeselválasztóként, állítsd be a `TxtSaveOptions` kultúráját:

```java
saveOptions.setCultureInfo(java.util.Locale.US);
```

Ez akkor hasznos, ha a célalkalmazás egy adott formátumot vár, például CSV‑parszerek, amelyek csak `.`‑t fogadnak el.

### Overwriting existing files

A `save` metódus alapértelmezés szerint felülírja a célfájlt. Ha el szeretnéd kerülni a véletlen adatvesztést, előbb ellenőrizd a fájl létezését:

```java
java.io.File outFile = new java.io.File("significant_digits.txt");
if (outFile.exists()) {
    throw new IllegalStateException("File already exists. Choose a different name or delete the existing file.");
}
workbook.save(outFile.getPath(), saveOptions);
```

### Large workbooks and memory usage

Nagyon nagy munkalapok exportálásakor fontold meg a kimenet streaming‑jét:

```java
saveOptions.setEnableMemorySaving(true);
```

Ez a beállítás csökkenti a heap fogyasztást, mivel soronként írja ki az adatokat.

## Full working example

Az alábbi teljes programot másold, illeszd be, és futtasd azonnal:

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 2: Put numeric values into cells
        worksheet.getCells().get("A1").putValue(123.456789);
        worksheet.getCells().get("B1").putValue(0.0012345);
        worksheet.getCells().get("C1").putValue(98765.4321);

        // Step 3: Configure TXT save options
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4);          // limit to 4 significant digits
        saveOptions.setCultureInfo(java.util.Locale.US); // enforce dot as decimal separator
        saveOptions.setEnableMemorySaving(true);      // optional for large files

        // Step 4: Save the workbook as a TXT file
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

A kód futtatása `significant_digits.txt`‑t hoz létre a következő tartalommal (tabulátorral elválasztott oszlopok):

```
123.5	0.001235	98770
```

Minden szám a **4 jelentős számjegy** szabályt követi, ami azt mutatja, hogy a beállítás különböző nagyságrendeknél is működik.

## Conclusion

Most már tudod, hogyan **exportálj Excel‑t TXT‑be** miközben a jelentős számjegyek számát szabályozod. A `TxtSaveOptions.setSignificantDigits` használatával **hogyan állíts be számjegyeket**, **hogyan korlátozd a tizedeseket**, és **hogyan limitáld a jelentős számjegyeket** egyetlen, karbantartható sor kóddal. A megközelítés egyes cellákra, teljes tartományokra és nagy munkafüzetekre egyaránt alkalmazható.

### Next steps

- Fedezd fel a `TxtSaveOptions` további tulajdonságait, például a `setDelimiter('\t')`‑t az oszlopelválasztók testreszabásához.
- Kombináld az exportálót `CsvSaveOptions`‑szal, ha vesszővel elválasztott értékekre (CSV) van szükséged a sima szöveg helyett.
- Integráld a rutinot egy webszolgáltatásba, amely feltöltött Excel‑fájlokat fogad, és helyben visszaadja a levágott TXT‑kimenetet.

Nyugodtan kísérletezz különböző számjegy‑korlátozásokkal és locale‑kkal. Ha olyan helyzettel találkozol, ahol a beépített opciók nem fednek le egy speciális igényt, mindig utófeldolgozhatod a generált TXT‑fájlt a szokásos Java I/O segédeszközökkel.

Happy coding!


## What Should You Learn Next?


Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [How to Convert Text to Numbers in Excel Using Aspose.Cells for Java](/cells/english/java/cell-operations/convert-text-to-numbers-excel-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Export Custom Excel Properties to PDF Using Aspose.Cells for Java](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}