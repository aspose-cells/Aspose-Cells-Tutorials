---
category: general
date: 2026-11-22
description: Tanulja meg, hogyan használjon egyéni számformátumot egy oszlop pénznemkénti
  formázásához az Excelben Java segítségével. Állítsa be az Excel számformátumát gyorsan
  egy egyszerű stílussal.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format
- format column as currency
- set excel number format
- set currency format
- style first column
language: hu
lastmod: 2026-11-22
og_description: Alkalmazzon egyedi számformátumot az Excelben Java-val. Ez az útmutató
  bemutatja, hogyan állítsa be az Excel számformátumát, és formázza az első oszlopot
  pénznemként.
og_image_alt: Java code snippet that applies a custom number format to an Excel column
og_title: Egyéni számformátum alkalmazása Excelben Java-val – lépésről‑lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to use a custom number format to format a column as currency
    in Excel using Java. Set Excel number format quickly with a simple style.
  headline: How to apply a custom number format in Excel with Java
  type: TechArticle
tags:
- Java
- Excel
- Apache POI
- Spreadsheet Automation
title: Hogyan alkalmazzunk egyedi számformátumot az Excelben Java segítségével
url: /hu/java/formatting/how-to-apply-a-custom-number-format-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan alkalmazzunk egyedi számformátumot az Excelben Java-val

Ha egy oszlopot **custom number format** szeretnél formázni egy Excel munkalapon, ez az útmutató pontosan megmutatja, hogyan teheted ezt Java-val. Akár pénzügyi jelentéseket generálsz, akár könyvelési adatokat exportálsz, az első oszlop valutakénti formázása azonnal olvashatóvá teszi a kimenetet.

Az alábbi példában **format column as currency** alkalmazzuk, a stílust az első oszlopra alkalmazzuk, majd importálunk egy `DataTable`-t a munkalapba. Ugyanez a megközelítés bármilyen numerikus formátumra működik, amelyet meg szeretnél jeleníteni.

## Mit fogsz megtanulni

* Hogyan hozzunk létre egy **custom number format**-ot az Apache POI `Style` objektumával.  
* Hogyan **set Excel number format**-ot állítsunk be egy adott oszlopra, beleértve a **set currency format** esetet.  
* Hogyan **style first column**-t alkalmazzunk egy `DataTable` importálása közben.  
* Hogyan mentsük el a munkafüzetet és ellenőrizzük, hogy a formázás helyesen jelenik-e meg.

### Előfeltételek

* Java 17 vagy újabb.  
* Apache POI 5.x (az a könyvtár, amely biztosítja a `Workbook`, `Worksheet` és `Style` objektumokat).  
* `DataTable` implementáció, amely iterálható, mint a kódmintában szereplő.  
* Alapvető ismeretek a Java és az Excel fogalmairól.

---

## 1. lépés: A projekt beállítása és az adatok importálása

Először add hozzá az Apache POI-t a projekthez. Ha Maven-t használsz, a következő függőséget kell beletenned:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

Ezután szerezzük be a forrásadatokat `DataTable`-ként. Valós környezetben ez egy adatbázis lekérdezésből, CSV fájlból vagy API válaszból származhat.

```java
// Step 1: Obtain the source data as a DataTable
DataTable dataTable = getData();   // replace with your own data‑fetching logic
```

> **Pro tip:** Győződj meg róla, hogy a `DataTable` oszlopok a megfelelő Java típusokkal (`Integer`, `Double`, stb.) rendelkeznek, mivel a számformátum csak a numerikus cellákat érinti.

---

## 2. lépés: **custom number format** létrehozása az első oszlophoz

A **custom number format** megmondja az Excelnek, hogyan jelenítse meg a numerikus értékeket. Az értékek valutaként való megjelenítéséhez a beépített `CURRENCY` formátumot használjuk, de definiálhatsz olyan mintákat is, mint például `"$#,##0.00"`.

```java
// Step 2: Prepare a Style array – one entry per column in the DataTable
Style[] columnStyles = new Style[dataTable.getColumns().size()];

// Step 3: Create a style for the first column and set it to display values as currency
// wb – existing Workbook instance (e.g., XSSFWorkbook for .xlsx files)
Workbook wb = new XSSFWorkbook();
columnStyles[0] = wb.createCellStyle();               // style first column
columnStyles[0].setDataFormat(
        wb.createDataFormat().getFormat(Style.CustomNumberFormat.CURRENCY));
```

**Miért működik ez:**  
* `createCellStyle()` egy újrahasználható stílusobjektumot ad vissza.  
* `setDataFormat()` a **set currency format**-ot csatolja a stílushoz, amelyet az Excel minden, ezt a stílust használó cellára alkalmaz.  
* A stílus `columnStyles[0]`-ban való tárolásával biztosítjuk, hogy csak az első oszlop kapja meg a valutaformázást.

---

## 3. lépés: A `DataTable` importálása a oszlopsz styles alkalmazásával

Most importáljuk az adatokat a munkalapba. Az `importDataTable` metódus elfogadja a stílus tömböt, lehetővé téve, hogy **style first column**-t alkalmazzunk, míg a többi oszlop az alapértelmezett formázást kapja.

```java
// Step 4: Import the DataTable into the worksheet, applying the column styles
// ws – existing Worksheet instance
Worksheet ws = wb.createSheet("Report");

// true  → import column headers
// 0,0   → start at cell A1
ws.getCells().importDataTable(dataTable, true, 0, 0, columnStyles);
```

A fenti hívás csak az első oszlopra **sets Excel number format**-ot alkalmaz. Minden más oszlop a munkafüzet alapértelmezett stílusát örökli, ami egyszerűvé és hatékonnyá teszi a kódot.

---

## 4. lépés: A munkafüzet mentése és az eredmény ellenőrzése

Végül írd a munkafüzetet egy fájlba, és nyisd meg Excelben, hogy megerősítsd, az első oszlop valutajeleket jelenít meg.

```java
// Step 5: Save the workbook to disk
try (FileOutputStream fileOut = new FileOutputStream("FormattedReport.xlsx")) {
    wb.write(fileOut);
}
System.out.println("Workbook saved as FormattedReport.xlsx");
```

**Várható kimenet:**  
Amikor megnyitod a *FormattedReport.xlsx*-t, az A oszlop értékei a megfelelő valutajelzéssel jelennek meg (pl. `$1,234.00`). Minden más oszlop megtartja eredeti numerikus ábrázolását.

---

## Gyakori variációk és szélhelyzetek

| Helyzet | Módosítás |
|-----------|------------|
| **Más valuta** (pl. Euro) | Replace `Style.CustomNumberFormat.CURRENCY` with a custom pattern: <br>`wb.createDataFormat().getFormat("\"€\"#,##0.00")` |
| **Több, mint egy stílusos oszlop** | Töltsd fel a további bejegyzéseket a `columnStyles[]`-ben saját `CellStyle` objektumaikkal. |
| **Nagy adatállományok** | Használd az `importDataTable`-t kötegekben vagy sorok streamelésével, hogy elkerüld a `OutOfMemoryError`-t. |
| **Helyspecifikus elválasztók** | Használd a `java.text.NumberFormat`-ot egy helyspecifikus mintához, és add át a `setDataFormat`-nek. |

> **Figyelj:** Egyetlen `CellStyle` objektum sok oszlopban való újrahasználata váratlan formázáshoz vezethet, mivel az Excel korlátozza a munkafüzetben létező különböző stílusok számát. Hozz létre külön stílust minden egyedi formátumhoz, amelyre szükséged van.

---

## Teljes futtatható példa

Az alábbi önálló program bemutatja a teljes munkafolyamatot, az adatok létrehozásától a formázott munkafüzet mentéséig.

```java
import java.io.FileOutputStream;
import java.util.ArrayList;
import java.util.List;

import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

/* Mock DataTable implementation for demonstration purposes */
class DataTable {
    private final List<String> columns = List.of("Amount", "Description");
    private final List<Object[]> rows = new ArrayList<>();

    public DataTable() {
        rows.add(new Object[]{1234.5, "Consulting"});
        rows.add(new Object[]{5678.9, "Licensing"});
    }

    public List<String> getColumns() { return columns; }
    public List<Object[]> getRows() { return rows; }
}

/* Helper that mimics the importDataTable method used in the original snippet */
class WorksheetHelper {
    private final Sheet sheet;
    private final Workbook wb;

    public WorksheetHelper(Workbook wb, Sheet sheet) {
        this.wb = wb;
        this.sheet = sheet;
    }

    public void importDataTable(DataTable dt, boolean includeHeaders,
                                int startRow, int startCol, Style[] styles) {
        int rowIdx = startRow;
        if (includeHeaders) {
            Row header = sheet.createRow(rowIdx++);
            for (int c = 0; c < dt.getColumns().size(); c++) {
                Cell cell = header.createCell(startCol + c);
                cell.setCellValue(dt.getColumns().get(c));
            }
        }
        for (Object[] rowData : dt.getRows()) {
            Row row = sheet.createRow(rowIdx++);
            for (int c = 0; c < rowData.length; c++) {
                Cell cell = row.createCell(startCol + c);
                Object value = rowData[c];
                if (value instanceof Number) {
                    cell.setCellValue(((Number) value).doubleValue());
                } else {
                    cell.setCellValue(value.toString());
                }
                // Apply custom style if provided
                if (styles != null && c < styles.length && styles[c] != null) {
                    cell.setCellStyle((CellStyle) styles[c]);
                }
            }
        }
    }
}

/* Main class that puts everything together */
public class CustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Obtain the source data
        DataTable dataTable = new DataTable();

        // 2️⃣ Create a workbook and a sheet
        Workbook wb = new XSSFWorkbook();
        Sheet ws = wb.createSheet("Report");

        // 3️⃣ Prepare a style array – one entry per column
        Style[] columnStyles = new Style[dataTable.getColumns().size()];

        // 4️⃣ Create a style for the first column (currency)
        CellStyle currencyStyle = wb.createCellStyle();
        DataFormat fmt = wb.createDataFormat();
        currencyStyle.setDataFormat(fmt.getFormat("$#,##0.00"));
        columnStyles[0] = currencyStyle;   // style first column

        // 5️⃣ Import the DataTable, applying the column styles
        WorksheetHelper helper = new WorksheetHelper(wb, ws);
        helper.importDataTable(dataTable, true, 0, 0, columnStyles);

        // 6️⃣ Save the workbook
        try (FileOutputStream out = new FileOutputStream("FormattedReport.xlsx")) {
            wb.write(out);
        }
        System.out.println("Workbook written to FormattedReport.xlsx");
    }
}
```

A program futtatása létrehozza a **FormattedReport.xlsx** fájlt, ahol az A oszlop (az „Amount” oszlop) **custom number format**-tal jelenik meg, amely dollárjelet és két tizedesjegyet mutat.

---

## Összegzés

Most már tudod, hogyan **custom number format**-ot alkalmazz egy Excel munkalapra Java-ból, hogyan **format column as currency**, és hogyan **style first column**-t végezz az adatok importálása közben. Újrahasználható `CellStyle` létrehozásával és az `importDataTable`-nek való átadásával **set Excel number format**-ot alkalmazhatsz bármely oszlopra anélkül, hogy manuálisan ciklusba lépnél minden cellán.

Next, try:

* `setDataFormat` használata helyspecifikus mintákkal a **set currency format**-hoz

## Mit érdemes következőként megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Excel számformátum beállítása Java-ban – Teljes útmutató](/cells/english/java/formatting/set-number-format-excel-in-java-complete-guide/)
- [Számformátum alkalmazása Excelben Java-val – Teljes Aspose.Cells útmutató](/cells/english/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/)
- [Hogyan hozzunk létre Excel munkafüzetet valutaformátummal és félkövér betűtípussal Java-ban](/cells/english/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}