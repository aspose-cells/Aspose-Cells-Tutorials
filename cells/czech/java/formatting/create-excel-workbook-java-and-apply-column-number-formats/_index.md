---
category: general
date: 2026-09-27
description: Vytvořte Excel sešit v Javě, importujte data z SQL, nastavte formát čísla
  ve sloupci a uložte sešit jako XLSX pomocí Aspose.Cells v Javě.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- import sql data excel
- add number format excel
- set number format column
language: cs
lastmod: 2026-09-27
og_description: Vytvořte Excel sešit v Javě, importujte data ze SQL, nastavte formát
  čísla ve sloupci a uložte sešit jako XLSX s plně funkčním příkladem v Javě.
og_image_alt: Screenshot of a Java program creating an Excel workbook with styled
  numeric columns
og_title: Vytvořit Excel sešit v Javě – importovat SQL data a nastavit formáty čísel
  ve sloupcích
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
title: Vytvořte Excel sešit v Javě a aplikujte formáty čísel ve sloupcích
url: /cs/java/formatting/create-excel-workbook-java-and-apply-column-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořte Excel workbook java a aplikujte formáty čísel sloupců

Pokud potřebujete **create Excel workbook java** a stylovat číselné sloupce, tento průvodce vám přesně ukáže, jak na to. Naučíte se importovat SQL data do Excelu, nastavit formát čísla pro každý sloupec a **save workbook as XLSX** pomocí knihovny Aspose.Cells.

Práce s tabulkami z Javy často působí roztříštěně — vývojáři kopírují a vkládají úryvky kódu, zapomínají formátovat čísla nebo končí s CSV soubory místo skutečných Excel souborů. Tento tutoriál odstraňuje tuto tření tím, že poskytuje jediné, end‑to‑end řešení, které můžete vložit do libovolného Java projektu.

Do konce článku budete schopni:

* Připojit se k databázi a načíst `DataTable` (nebo `ResultSet`)  
* Vytvořit nový sešit pomocí Aspose.Cells  
* Aplikovat konzistentní styl **add number format excel** na každý sloupec  
* **Save workbook as XLSX** na místo dle vašeho výběru  

Jedinou podmínkou je vývojové prostředí Java (doporučeno JDK 8+ ) a JAR Aspose.Cells pro Java ve vaší classpath.

## Požadavky

| Požadavek | Proč je důležité |
|-------------|----------------|
| JDK 8 nebo novější | Poskytuje jazykové funkce použité v příkladu. |
| Aspose.Cells for Java (nejnovější verze) | Zajišťuje tvorbu Excelu, stylování a ukládání bez nainstalovaného Office. |
| JDBC‑kompatibilní databáze (např. MySQL, PostgreSQL) | Poskytuje SQL data, která budeme importovat. |
| Maven nebo Gradle (volitelné) | Zjednodušuje správu závislostí. |

Přidejte Aspose.Cells do vašeho Maven `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- use the latest stable version -->
</dependency>
```

Nebo si stáhněte JAR přímo z webu Aspose a přidejte jej do classpath vašeho projektu.

## Krok 1: Create Excel workbook java

Prvním logickým blokem je vytvořit novou instanci `Workbook`. Tento objekt představuje celý Excel soubor v paměti a poskytuje přístup k listům, buňkám a stylům.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

Vytvoření sešitu předem nám také poskytne továrnu `Style`, kterou budeme později potřebovat při **set number format column**.

## Krok 2: Retrieve data from SQL (import sql data excel)

Níže otevřeme JDBC připojení, spustíme jednoduchý `SELECT` dotaz a načteme výsledek do Aspose `DataTable`. Třída `DataTable` napodobuje .NET `DataTable` a funguje hladce s metodou `importDataTable`.

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

> **Tip:** Pokud již máte `DataTable` z jiného zdroje (např. parsování CSV), můžete JDBC kód přeskočit a vrátit tuto tabulku přímo.

## Krok 3: Prepare a reusable style (add number format excel)

Chceme, aby každý číselný sloupec zobrazoval čísla se dvěma desetinnými místy a oddělovačem tisíců. Místo stylování každé buňky zvlášť vytvoříme objekt `Style` jednou pro každý sloupec a znovu jej použijeme během importu. Toto je nejefektivnější způsob, jak **add number format excel**.

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

Můžete upravit řetězec formátu (`"#,##0.00"`) na libovolný Excel formát čísla, který potřebujete. Pro data použijte `styles[i].setCustom("mm-dd-yyyy")` atd.

## Krok 4: Import the DataTable and apply the column styles

Nyní spojíme vše dohromady. Přetížení `importDataTable` nám umožňuje předat `DataTable`, určit, zda má být první řádek považován za záhlaví sloupců, a poskytnout pole stylů. Toto automaticky **set number format column** pro každou buňku ve odpovídajícím sloupci.

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

Protože jsme pro příznak `importColumnNames` předali `true`, první řádek listu obsahuje názvy sloupců z `DataTable`. Každý následující řádek získá data, již naformátovaná podle stylu, který jsme definovali.

## Krok 5: Save workbook as xlsx

Posledním krokem je uložit sešit z paměti do fyzického souboru. Aspose.Cells podporuje mnoho formátů; použijeme moderní formát XLSX, který dnes očekává většina aplikací.

```java
// Step 5: Save the workbook to an .xlsx file
private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
    workbook.save(filePath, com.aspose.cells.SaveFormat.XLSX);
}
```

Můžete změnit `filePath` na libovolné platné umístění ve vašem systému. Metoda vyhodí `IOException`, pokud adresář neexistuje nebo nemáte oprávnění k zápisu.

## Kompletní, spustitelný příklad

Složení všech částí dohromady poskytne samostatný program, který můžete okamžitě zkompilovat a spustit.

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

### Očekávaný výsledek

Spuštěním programu se vytvoří soubor pojmenovaný **DataTableWithNumberFormat.xlsx** v pracovním adresáři. Otevřete jej v Microsoft Excel, LibreOffice Calc nebo jakémkoli prohlížeči podporujícím XLSX a uvidíte:

| Id | Částka | DatumVytvoření |
|----|--------|-----------------|
| 1  | 1,234.56 | 2023‑01‑15 |
| 2  | 78,900.00 | 2023‑02‑20 |
| …  | … | … |

*Sloupec **Částka** zobrazuje čísla se dvěma desetinnými místy a oddělovačem tisíců, díky stylu **add number format excel**, který jsme použili.*

## Časté otázky a řešení okrajových případů

| Otázka | Odpověď |
|----------|--------|
| **Co když můj dotaz nevrátí žádné řádky?** | `DataTable` bude prázdná, ale stále bude obsahovat definice sloupců. Sešit bude obsahovat jen řádek s hlavičkou, což je často dostačující pro následné procesy. |
| **Jak aplikovat různé formáty na jednotlivé sloupce?** | Upravte `buildColumnStyles`, aby kontroloval název sloupce nebo typ dat a přiřadil vlastní formát (např. data, procenta). |
| **Mohu zapisovat přímo do `ByteArrayOutputStream`?** | Ano. Nahraďte `workbook.save(filePath, SaveFormat.XLSX);` za

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}