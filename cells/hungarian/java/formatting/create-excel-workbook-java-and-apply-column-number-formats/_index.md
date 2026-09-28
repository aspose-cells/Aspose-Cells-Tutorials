---
category: general
date: 2026-09-27
description: Excel munkafüzet létrehozása Java-ban, SQL adatok importálása, számformátum
  beállítása az oszlopban, és a munkafüzet mentése XLSX formátumban az Aspose.Cells
  Java használatával.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- import sql data excel
- add number format excel
- set number format column
language: hu
lastmod: 2026-09-27
og_description: Excel munkafüzet létrehozása Java-val, SQL adatok importálása, számformátum
  beállítása oszlopban, és a munkafüzet mentése XLSX formátumban egy teljesen működő
  Java példával.
og_image_alt: Screenshot of a Java program creating an Excel workbook with styled
  numeric columns
og_title: Excel munkafüzet létrehozása Java‑ban – SQL adatok importálása és oszlopszám
  formátumok beállítása
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Create Excel workbook java, import SQL data, set number format column,
    and save workbook as XLSX using Aspose.Cells in Java.
  headline: Create Excel workbook java and apply column number formats
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Data import
title: Excel munkafüzet létrehozása Java-val és oszlopszám formátumok alkalmazása
url: /hu/java/formatting/create-excel-workbook-java-and-apply-column-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel munkafüzet létrehozása Java-ban és oszlopszámformátumok alkalmazása

Ha **Excel munkafüzetet kell létrehoznod Java-ban** és numerikus oszlopokat szeretnél formázni, ez az útmutató pontosan megmutatja, hogyan. Megtanulod, hogyan importálj SQL adatokat Excelbe, hogyan állíts be számformátumot minden oszlopra, és hogyan **mentsd el a munkafüzetet XLSX formátumban** az Aspose.Cells könyvtár segítségével.

A táblázatokkal való munka Java-ból gyakran töredezettnek tűnik — a fejlesztők kódrészleteket másolnak‑beillesztenek, elfelejtik a számok formázását, vagy CSV fájlokba végződnek ahelyett, hogy valódi Excel fájlok lennének. Ez az útmutató megszünteti ezt a súrlódást egyetlen, vég‑végi megoldás biztosításával, amelyet bármely Java projektbe beilleszthetsz.

A cikk végére képes leszel:

* Kapcsolódni egy adatbázishoz és lekérni egy `DataTable` (vagy `ResultSet`) objektumot  
* Új munkafüzetet létrehozni az Aspose.Cells segítségével  
* Konzisztens **add number format excel** stílust alkalmazni minden oszlopra  
* **Mentsd el a munkafüzetet XLSX** formátumban a választott helyre  

Az egyetlen előfeltétel egy Java fejlesztői környezet (JDK 8+ ajánlott) és az Aspose.Cells for Java JAR a classpath-odban.

---

## Előkövetelmények

| Követelmény | Miért fontos |
|-------------|----------------|
| JDK 8 vagy újabb | Biztosítja a példában használt nyelvi funkciókat. |
| Aspose.Cells for Java (legújabb verzió) | Kezeli az Excel létrehozását, stílusozását és mentését Office telepítése nélkül. |
| JDBC‑kompatibilis adatbázis (pl. MySQL, PostgreSQL) | Biztosítja a beimportálandó SQL adatokat. |
| Maven vagy Gradle (opcionális) | Megkönnyíti a függőségkezelést. |

Add Aspose.Cells a Maven `pom.xml`-hez:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- use the latest stable version -->
</dependency>
```

Vagy töltsd le a JAR-t közvetlenül az Aspose weboldaláról, és add hozzá a projekted classpath-jához.

---

## 1. lépés: Excel munkafüzet létrehozása Java-ban

Az első logikai blokk egy új `Workbook` példányosítása. Ez az objektum a teljes Excel fájlt reprezentálja a memóriában, és hozzáférést biztosít munkalapokhoz, cellákhoz és stílusokhoz.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

A munkafüzet előzetes létrehozása egy `Style` gyárat is biztosít, amelyre később szükségünk lesz, amikor **set number format column**-t állítunk be.

## 2. lépés: Adatok lekérése SQL-ből (import sql data excel)

Az alábbiakban megnyitunk egy JDBC kapcsolatot, végrehajtunk egy egyszerű `SELECT` lekérdezést, és betöltjük az eredményhalmazt egy Aspose `DataTable`-be. A `DataTable` osztály a .NET `DataTable`-t utánozza, és zökkenőmentesen működik az `importDataTable` metódussal.

```java
// Step 2: Pull data from a database and fill a DataTable
private static DataTable getDataTableFromDb() throws SQLException {
    // Replace with your actual connection string, user, and password
    String url = "jdbc:mysql://localhost:3306/yourdb";
    String user = "your_user";
    String password = "your_password";

    try (Connection conn = DriverManager.getConnection(url, user, password);
         Statement stmt = conn.createStatement();
         ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

        // Aspose.Cells provides a utility to convert ResultSet → DataTable
        return CellsHelper.getDataTableFromResultSet(rs);
    }
}
```

> **Tippek:** Ha már rendelkezel egy `DataTable`-lel egy másik forrásból (pl. CSV feldolgozás), kihagyhatod a JDBC kódot, és közvetlenül visszaadhatod azt a táblát.

## 3. lépés: Újrafelhasználható stílus előkészítése (add number format excel)

Szeretnénk, hogy minden numerikus oszlop két tizedesjegyű számokat és ezres elválasztót jelenítsen meg. Az egyes cellák egyenkénti formázása helyett egy `Style` objektumot hozunk létre oszloponként, és az importálás során újra felhasználjuk. Ez a leghatékonyabb módja a **add number format excel**-nek.

```java
// Step 3: Build a style array – one style per column
private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
    Style[] styles = new Style[columnCount];
    for (int i = 0; i < columnCount; i++) {
        styles[i] = workbook.createStyle();
        // "0.00" = two decimal places; "#,##0.00" adds thousands separator
        styles[i].setNumber("#,##0.00");
    }
    return styles;
}
```

A formátum karakterláncot (`"#,##0.00"`) bármilyen szükséges Excel számformátumra módosíthatod. Dátumokhoz használd a `styles[i].setCustom("mm-dd-yyyy")`-t, stb.

## 4. lépés: A DataTable importálása és az oszlopsz styles alkalmazása

Most minden elemet összehozunk. Az `importDataTable` túlterhelés lehetővé teszi, hogy átadjuk a `DataTable`-t, megadjuk, hogy az első sor oszlopfejlécként legyen-e kezelve, és átadjuk a stílus tömböt. Ez automatikusan **set number format column**-t alkalmaz minden cellára a megfelelő oszlopban.

```java
// Step 4: Import data with styles into the first worksheet
private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
    // Build a style for each column based on the number of columns in the DataTable
    Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());

    // Import the DataTable starting at cell A1 (row 0, column 0)
    workbook.getWorksheets().get(0).getCells()
            .importDataTable(dataTable, true, 0, 0, columnStyles);
}
```

Mivel a `importColumnNames` jelzőnek `true`-t adtunk, a munkalap első sora a `DataTable` oszlopneveit tartalmazza. Minden következő sor megkapja az adatokat, már a definiált stílus szerint formázva.

## 5. lépés: Munkafüzet mentése xlsx formátumban

Az utolsó lépés a memóriában lévő munkafüzet fizikai fájlba mentése. Az Aspose.Cells számos formátumot támogat; a modern XLSX formátumot fogjuk használni, amelyet a legtöbb alkalmazás ma elvár.

```java
// Step 5: Save the workbook to an .xlsx file
private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
    workbook.save(filePath, com.aspose.cells.SaveFormat.XLSX);
}
```

A `filePath`-t bármely érvényes helyre módosíthatod a rendszereden. A metódus `IOException`-t dob, ha a könyvtár nem létezik vagy nincs írási jogosultságod.

## Teljes, futtatható példa

Az összes elem összeállítása egy önálló programot eredményez, amelyet azonnal lefordíthatsz és futtathatsz.

```java
import com.aspose.cells.*;
import java.sql.*;

public class CreateExcelWorkbookJava {
    public static void main(String[] args) {
        try {
            // 1️⃣ Obtain data from the database
            DataTable dataTable = getDataTableFromDb();

            // 2️⃣ Create a new workbook that will hold the imported data
            Workbook workbook = new Workbook();

            // 3️⃣ Import the DataTable with a numeric style per column
            importDataWithStyles(workbook, dataTable);

            // 4️⃣ Save the workbook as XLSX
            String outputPath = "DataTableWithNumberFormat.xlsx";
            saveWorkbook(workbook, outputPath);

            System.out.println("Workbook created successfully at: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    // ---- Helper methods (see earlier sections) ----
    private static DataTable getDataTableFromDb() throws SQLException {
        String url = "jdbc:mysql://localhost:3306/yourdb";
        String user = "your_user";
        String password = "your_password";

        try (Connection conn = DriverManager.getConnection(url, user, password);
             Statement stmt = conn.createStatement();
             ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

            return CellsHelper.getDataTableFromResultSet(rs);
        }
    }

    private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
        Style[] styles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++) {
            styles[i] = workbook.createStyle();
            styles[i].setNumber("#,##0.00"); // two decimals with thousands separator
        }
        return styles;
    }

    private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
        Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());
        workbook.getWorksheets().get(0).getCells()
                .importDataTable(dataTable, true, 0, 0, columnStyles);
    }

    private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
        workbook.save(filePath, SaveFormat.XLSX);
    }
}
```

### Várt eredmény

A program futtatása egy **DataTableWithNumberFormat.xlsx** nevű fájlt hoz létre a munkakönyvtárban. Nyisd meg Microsoft Excel, LibreOffice Calc vagy bármely XLSX‑kompatibilis megjelenítővel, és a következőt fogod látni:

| Id | Amount | CreatedDate |
|----|--------|-------------|
| 1  | 1,234.56 | 2023‑01‑15 |
| 2  | 78,900.00 | 2023‑02‑20 |
| …  | … | … |

*A **Amount** oszlop két tizedesjegyű számokat és ezres elválasztót jelenít meg, köszönhetően a **add number format excel** stílusnak, amelyet alkalmaztunk.*

## Gyakori kérdések és szélsőséges esetek kezelése

| Kérdés | Válasz |
|----------|--------|
| **Mi van, ha a lekérdezésem nem ad vissza sorokat?** | A `DataTable` üres lesz, de továbbra is tartalmazza az oszlopdefiníciókat. A munkafüzet csak a fejléc sort fogja tartalmazni, ami gyakran elegendő az utólagos folyamatokhoz. |
| **Hogyan alkalmazzak különböző formátumokat oszloponként?** | Módosítsd a `buildColumnStyles`-t, hogy ellenőrizze az oszlop nevét vagy adattípusát, és egyedi formátumot rendelj (pl. dátumok, százalékok). |
| **Írhatok közvetlenül egy `ByteArrayOutputStream`-be?** | Igen. Cseréld le a `workbook.save(filePath, SaveFormat.XLSX);` sort a következőre |

## Mit érdemes még megtanulni?

Az alábbi útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}