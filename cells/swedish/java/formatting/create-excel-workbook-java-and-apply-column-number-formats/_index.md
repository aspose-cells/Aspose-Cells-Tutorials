---
category: general
date: 2026-09-27
description: Skapa Excel-arbetsbok i Java, importera SQL-data, ange talformat för
  kolumnen och spara arbetsboken som XLSX med Aspose.Cells i Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- import sql data excel
- add number format excel
- set number format column
language: sv
lastmod: 2026-09-27
og_description: Skapa Excel‑arbetsbok i Java, importera SQL‑data, ange talformat för
  kolumn och spara arbetsboken som XLSX med ett fullt fungerande Java‑exempel.
og_image_alt: Screenshot of a Java program creating an Excel workbook with styled
  numeric columns
og_title: Skapa Excel-arbetsbok i Java – importera SQL-data och ange kolumners talformat
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
title: Skapa Excel-arbetsbok i Java och tillämpa kolumners nummerformat
url: /sv/java/formatting/create-excel-workbook-java-and-apply-column-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel-arbetsbok i Java och tillämpa kolumnnummerformat

Om du behöver **create Excel workbook java** och formatera numeriska kolumner, visar den här guiden exakt hur. Du kommer att lära dig att importera SQL-data till Excel, ange ett talformat för varje kolumn och **save workbook as XLSX** med Aspose.Cells-biblioteket.

Att arbeta med kalkylblad från Java känns ofta fragmenterat—utvecklare kopierar‑och‑klistrar kodsnuttar, glömmer att formatera tal eller slutar med CSV-filer istället för riktiga Excel-filer. Denna handledning tar bort den friktionen genom att erbjuda en enda, end‑to‑end‑lösning som du kan lägga in i vilket Java‑projekt som helst.

By the end of the article you will be able to:

* Ansluta till en databas och hämta en `DataTable` (eller `ResultSet`)  
* Skapa en ny arbetsbok med Aspose.Cells  
* Tillämpa en konsekvent **add number format excel**-stil på varje kolumn  
* **Save workbook as XLSX** till en plats du själv väljer  

Det enda förutsättningen är en Java‑utvecklingsmiljö (JDK 8+ rekommenderas) och Aspose.Cells for Java‑JAR‑filen på din klassökväg.

## Förutsättningar

| Krav | Varför det är viktigt |
|------|-----------------------|
| JDK 8 or newer | Tillhandahåller språkfunktionerna som används i exemplet. |
| Aspose.Cells for Java (latest version) | Hanterar skapande, formatering och sparande av Excel utan att Office är installerat. |
| A JDBC‑compatible database (e.g., MySQL, PostgreSQL) | Tillhandahåller de SQL‑data vi kommer att importera. |
| Maven or Gradle (optional) | Förenklar beroendehantering. |

Lägg till Aspose.Cells i din Maven `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- use the latest stable version -->
</dependency>
```

Eller ladda ner JAR‑filen direkt från Aspose‑webbplatsen och lägg till den i ditt projekts klassökväg.

## Steg 1: Skapa Excel-arbetsbok i Java

Det första logiska steget är att instansiera ett nytt `Workbook`. Detta objekt representerar hela Excel‑filen i minnet och ger dig åtkomst till kalkylblad, celler och stilar.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

Att skapa arbetsboken i förväg ger oss också en `Style`‑fabrik som vi kommer att behöva senare när vi **set number format column**.

## Steg 2: Hämta data från SQL (import sql data excel)

Nedan öppnar vi en JDBC‑anslutning, kör ett enkelt `SELECT`‑uttryck och laddar resultatmängden i en Aspose `DataTable`. `DataTable`‑klassen efterliknar .NET `DataTable` och fungerar sömlöst med `importDataTable`‑metoden.

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

> **Tips:** Om du redan har en `DataTable` från en annan källa (t.ex. CSV‑parsing), kan du hoppa över JDBC‑koden och returnera den tabellen direkt.

## Steg 3: Förbered en återanvändbar stil (add number format excel)

Vi vill att varje numerisk kolumn ska visa tal med två decimaler och en tusentalsseparator. Istället för att formatera varje cell individuellt skapar vi ett `Style`‑objekt en gång per kolumn och återanvänder det vid import. Detta är det mest effektiva sättet att **add number format excel**.

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

Du kan anpassa formatsträngen (`"#,##0.00"`) till vilket Excel‑talformat du behöver. För datum, använd `styles[i].setCustom("mm-dd-yyyy")` osv.

## Steg 4: Importera DataTable och tillämpa kolumnstilarna

Nu sätter vi ihop allt. Överlagringen av `importDataTable` låter oss skicka `DataTable`, ange om den första raden ska behandlas som kolumnrubriker och leverera stil‑arrayen. Detta automatiskt **set number format column** för varje cell i motsvarande kolumn.

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

Eftersom vi skickade `true` för flaggan `importColumnNames` innehåller den första raden i kalkylbladet kolumnnamnen från `DataTable`. Varje efterföljande rad får data, redan formaterade enligt den stil vi definierade.

## Steg 5: Spara arbetsbok som xlsx

Det sista steget är att skriva den minnesbaserade arbetsboken till en fysisk fil. Aspose.Cells stöder många format; vi kommer att använda det moderna XLSX‑formatet, vilket de flesta program förväntar sig idag.

```java
// Step 5: Save the workbook to an .xlsx file
private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
    workbook.save(filePath, com.aspose.cells.SaveFormat.XLSX);
}
```

Du kan ändra `filePath` till någon giltig plats på ditt system. Metoden kastar `IOException` om katalogen inte finns eller om du saknar skrivbehörighet.

## Fullt, körbart exempel

Att sätta ihop alla delar ger ett fristående program som du kan kompilera och köra omedelbart.

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

### Förväntat resultat

När programmet körs skapas en fil med namnet **DataTableWithNumberFormat.xlsx** i arbetskatalogen. Öppna den med Microsoft Excel, LibreOffice Calc eller någon XLSX‑kompatibel visare så ser du:

| Id | Amount | CreatedDate |
|----|--------|-------------|
| 1  | 1,234.56 | 2023‑01‑15 |
| 2  | 78,900.00 | 2023‑02‑20 |
| …  | … | … |

*Kolumnen **Amount** visar tal med två decimaler och en tusentalsseparator, tack vare den **add number format excel**‑stil vi tillämpade.*

## Vanliga frågor och hantering av kantfall

| Fråga | Svar |
|----------|--------|
| **Vad händer om min fråga inte returnerar några rader?** | `DataTable`‑en blir tom men innehåller fortfarande kolumndefinitioner. Arbetsboken kommer bara att innehålla rubrikraden, vilket ofta är tillräckligt för efterföljande processer. |
| **Hur applicerar jag olika format per kolumn?** | Ändra `buildColumnStyles` så att den inspekterar kolumnnamnet eller datatypen och tilldelar ett anpassat format (t.ex. datum, procent). |
| **Kan jag skriva direkt till en `ByteArrayOutputStream`?** | Ja. Ersätt `workbook.save(filePath, SaveFormat.XLSX);` med |

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig behärska ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}