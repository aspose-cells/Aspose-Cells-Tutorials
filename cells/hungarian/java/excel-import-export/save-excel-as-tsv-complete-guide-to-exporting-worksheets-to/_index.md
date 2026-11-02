---
category: general
date: 2026-06-27
description: Mentse az Excel fájlt gyorsan TSV formátumba Java-val. Tanulja meg, hogyan
  exportálja a munkalapot szövegként, a lapot egyszerű szövegként, valamint az Excel
  adatokat karakterláncként az Aspose.Cells segítségével.
draft: false
keywords:
- save excel as tsv
- export worksheet to text
- export sheet plain text
- export excel data string
language: hu
og_description: Excel mentése TSV formátumban Java-val. Ez az útmutató bemutatja,
  hogyan lehet munkalapot szövegként exportálni, lapot egyszerű szövegként exportálni,
  és az Excel adatokat hatékonyan karakterláncként exportálni.
og_title: Excel mentése TSV‑ként – Lépésről‑lépésre exportálási útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Save Excel as TSV quickly using Java. Learn how to export worksheet
    to text, export sheet plain text, and export Excel data string with Aspose.Cells.
  headline: Save Excel as TSV – Complete Guide to Exporting Worksheets to Text
  type: TechArticle
- description: Save Excel as TSV quickly using Java. Learn how to export worksheet
    to text, export sheet plain text, and export Excel data string with Aspose.Cells.
  name: Save Excel as TSV – Complete Guide to Exporting Worksheets to Text
  steps:
  - name: Pro tip
    text: If you’re dealing with password‑protected files, call `new Workbook("file.xlsx",
      new LoadOptions(LoadFormat.XLSX) {{ setPassword("yourPassword"); }})`.
  - name: 'Edge case: Custom delimiters'
    text: 'If your downstream system expects a pipe (`|`) instead of a tab, just change
      the delimiter:'
  - name: Pro tip
    text: 'After exporting, you can also capture the string directly:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
title: Excel mentése TSV-ként – Teljes útmutató a munkalapok szövegfájlba exportálásához
url: /hu/java/excel-import-export/save-excel-as-tsv-complete-guide-to-exporting-worksheets-to/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel mentése TSV formátumban – Teljes útmutató a munkalapok szövegként történő exportálásához

Valaha szükséged volt **save Excel as TSV**-re, de nem tudtad, melyik API hívást kell használni? Nem vagy egyedül. Sok fejlesztő akad el, amikor megpróbál egy táblázatot tabulátorral elválasztott fájlba konvertálni az utófeldolgozáshoz. A jó hír? Néhány Java és Aspose.Cells sorral exportálhatod a munkalapot szövegként, exportálhatod a lap tiszta szövegét, és még az Excel adatkarakterláncot is anélkül, hogy izzadnál.

Ebben az útmutatóban végigvezetünk a teljes munkafolyamaton – a munkafüzet betöltésétől az exportálási beállítások konfigurálásáig, egészen a TSV fájl lemezre írásáig. A végére képes leszel **save Excel as TSV**-re bármely Java projektben, akár egyetlen lapot, akár tucatnyi fájlt dolgozol fel.

## Mit fed le ez az útmutató

* Excel munkafüzet betöltése lemezről  
* A megfelelő munkalap kiválasztása (vagy többön keresztül iterálás)  
* `ExportTableOptions` konfigurálása tiszta szöveges kimenet előállításához  
* Az adatok írása tabulátorral elválasztott értékek (TSV) fájlként  
* Tippek nagy tartományok, különböző elválasztók és Unicode karakterek kezeléséhez  

Nincs szükség külső eszközökre – csak Aspose.Cells for Java és egy Java 8+ futtatókörnyezet.

## 1. lépés: Projekt beállítása és a munkafüzet betöltése

Mielőtt belevágnánk a kódba, győződj meg róla, hogy hozzáadtad az Aspose.Cells JAR-t a projekted classpath-jához. Ha Maven-t használsz, a függőség így néz ki:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

Most betölthetjük a munkafüzetet:

```java
// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Quick sanity check – print the number of worksheets
System.out.println("Worksheets count: " + workbook.getWorksheets().getCount());
```

> **Miért fontos:** A fájl betöltése az első lépés minden **export Excel data string** munkafolyamatban. Ha a fájlt nem lehet megnyitni, semmi más nem fog működni.

### Profi tipp
Ha jelszóval védett fájlokkal dolgozol, hívd a `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("yourPassword"); }})`-t.

## 2. lépés: Válaszd ki az exportálni kívánt munkalapot

Megszerezheted az első lapot, egy lapot név alapján, vagy iterálhatsz mindet. Íme a legegyszerűbb eset – az első munkalap exportálása:

```java
// Step 2: Access the first worksheet (or any specific sheet)
Worksheet ws = workbook.getWorksheets().get(0);
System.out.println("Exporting sheet: " + ws.getName());
```

Ha minden laphoz **export worksheet to text**-et kell végrehajtani, csomagold be a fenti kódot egy `for` ciklusba:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    // Export each sheet separately...
}
```

## 3. lépés: Exportálási beállítások létrehozása és konfigurálása

A **export sheet plain text** lényege az `ExportTableOptions`. Néhány tulajdonság átkapcsolásával a tartományt egy tabulátorral elválasztott tiszta szöveges karakterlánccá alakítjuk:

```java
// Step 3: Create export options for the table
ExportTableOptions exportOptions = new ExportTableOptions();

// Step 4: Configure the options – export as plain text and use a tab delimiter
exportOptions.setExportAsString(true);   // Returns a string instead of binary Excel format
exportOptions.setDelimiter('\t');        // Tab character makes it TSV
```

> **Miért használjuk a `setExportAsString(true)`-t?**  
> Azt mondja az Aspose.Cells-nek, hogy a kimenetet nyers szövegként kezelje, ami pontosan az, amire szükséged van, amikor **save Excel as TSV**-t akarsz. Az alternatíva egy CSV vagy HTML export lenne, egyik sem biztosít tiszta tabulátor elválasztást.

### Szélsőséges eset: Egyéni elválasztók
Ha az utófeldolgozó rendszered egy csővezeték (`|`) karaktert vár a tabulátor helyett, egyszerűen változtasd meg az elválasztót:

```java
exportOptions.setDelimiter('|');
```

## 4. lépés: A kívánt tartomány exportálása szövegfájlba

Most ténylegesen írjuk a TSV fájlt. Az `exportTable` metódus három argumentumot vár: a cellatartományt, a kimeneti útvonalat és a most konfigurált `ExportTableOptions`-t.

```java
// Step 5: Export the range A1:D20 to a text file using the configured options
ws.getCells().exportTable("A1:D20", "YOUR_DIRECTORY/out.tsv", exportOptions);
System.out.println("TSV file created successfully!");
```

Ha az *összes* használt tartományt szeretnéd exportálni, cseréld le a `"A1:D20"`-t `ws.getCells().getMaxDisplayRange()`-re:

```java
String fullRange = ws.getCells().getMaxDisplayRange();
ws.getCells().exportTable(fullRange, "out.tsv", exportOptions);
```

### Profi tipp
Exportálás után a karakterláncot közvetlenül is lekérheted:

```java
String tsvContent = ws.getCells().exportTable("A1:D20", exportOptions);
System.out.println(tsvContent); // Handy for debugging or sending over a network
```

Ez megadja a nyers **export Excel data string**-et anélkül, hogy a fájlrendszert érintenéd.

## 5. lépés: Nagy fájlok kezelése és teljesítmény tippek

Masszív táblázatok (több százezer sor) kezelésekor vedd figyelembe ezeket a optimalizációkat:

| Probléma | Megoldás |
|----------|----------|
| Memória nyomás | Use `WorkbookFactory.create(InputStream)` to stream the file instead of loading it fully. |
| Lassú I/O | Write to a `BufferedWriter` or use NIO `Files.newBufferedWriter`. |
| Unicode karakterek | Ensure the output file is written with UTF‑8: `exportTable(..., "out.tsv", exportOptions, Encoding.getUTF8())`. |

Az alábbi kódrészlet a streaminget és az UTF‑8 kódolást egyesíti:

```java
try (InputStream is = Files.newInputStream(Paths.get("input.xlsx"));
     BufferedWriter writer = Files.newBufferedWriter(Paths.get("out.tsv"), StandardCharsets.UTF_8)) {

    Workbook wb = new Workbook(is);
    Worksheet sheet = wb.getWorksheets().get(0);
    ExportTableOptions opts = new ExportTableOptions();
    opts.setExportAsString(true);
    opts.setDelimiter('\t');

    String tsv = sheet.getCells().exportTable("A1:D20", opts);
    writer.write(tsv);
}
```

## Gyakori hibák és hogyan kerüld el őket

1. **Elfelejtetted beállítani a `setExportAsString(true)`-t.**  
   Enélkül az Aspose bináris Excel fájlt generál, ami meghiúsítja a **export worksheet to text** célodat.

2. **Rossz elválasztó használata.**  
   Egy vessző a tabulátor helyett CSV-t eredményez, nem TSV-t. Ellenőrizd a `setDelimiter('\t')` beállítást.

3. **Helytelen tartomány szintaxis.**  
   A `"A1:D20"` rendben van, de a `"A1:D20:"` (több pont) `IllegalArgumentException`-t dob.

4. **Fájl jogosultságok.**  
   Győződj meg róla, hogy a célkönyvtár írható. Linuxon a `chmod 755` gyakran megoldja a problémát.

## Összegzés – Teljes működő példa

Itt a teljes, azonnal futtatható program, amely bemutatja a **save Excel as TSV** folyamatot az elejétől a végéig:

```java
import com.aspose.cells.*;

import java.io.*;
import java.nio.charset.StandardCharsets;
import java.nio.file.*;

public class ExcelToTsv {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Choose worksheet (first sheet in this case)
        Worksheet ws = workbook.getWorksheets().get(0);

        // Set up export options for plain‑text TSV output
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);   // Export as string
        exportOptions.setDelimiter('\t');        // Tab delimiter for TSV

        // Define the range you want to export
        String range = "A1:D20"; // Change as needed or use ws.getCells().getMaxDisplayRange()

        // Export to a file
        ws.getCells().exportTable(range, "YOUR_DIRECTORY/out.tsv", exportOptions);
        System.out.println("Successfully saved Excel as TSV at YOUR_DIRECTORY/out.tsv");
    }
}
```

A program futtatása egy tabulátorral elválasztott fájlt (`out.tsv`) hoz létre, amelyet bármely utófeldolgozó rendszer – legyen az adatbázis betöltő, Unix `awk` szkript vagy egyszerű táblázatnéző – felhasználhat.

## Következtetés

Mindezt lefedtük, ami szükséges a **save Excel as TSV** megvalósításához Java és Aspose.Cells segítségével. A munkafüzet betöltésétől, a megfelelő lap kiválasztásán, az `ExportTableOptions` konfigurálásán, egészen a fájl írásáig most egy stabil, termelés‑kész mintát kapsz a **export worksheet to text**, **export sheet plain text** és **export Excel data string** forgatókönyvekhez.

Mi a következő? Próbáld ki több tartomány exportálását, az elválasztók dinamikus cseréjét, vagy a kimenet közvetlen streamingjét egy HTTP válaszba web‑alapú letöltésekhez. Ugyanazok az elvek érvényesek, és rájössz, hogy az Excel adatok tiszta szövegként való kezelése gyerekjáték, ha az alapok megvannak.

Van kérdésed vagy furcsa széljegyet találsz? Hagyj egy megjegyzést alább, és jó kódolást!

## Mit érdemes legközelebb megtanulni?

Az alábbi útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Hogyan exportáljunk Excel adatokat HTML5-be Aspose.Cells Java használatával](/cells/english/java/import-export/aspose-cells-java-export-excel-html5/)
- [Könnyed adat exportálás Excelből Aspose.Cells for Java használatával](/cells/english/java/import-export/aspose-cells-java-excel-data-export/)
- [Hogyan exportáljunk egy Excel munkalapot PNG-be Aspose.Cells Java használatával](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}