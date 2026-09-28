---
category: general
date: 2026-09-27
description: Maak een Excel-werkmap in Java, importeer SQL-gegevens, stel het getalformaat
  van een kolom in en sla de werkmap op als XLSX met Aspose.Cells in Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- import sql data excel
- add number format excel
- set number format column
language: nl
lastmod: 2026-09-27
og_description: Maak een Excel-werkmap in Java, importeer SQL-gegevens, stel het getalformaat
  van een kolom in en sla de werkmap op als XLSX met een volledig werkend Java‑voorbeeld.
og_image_alt: Screenshot of a Java program creating an Excel workbook with styled
  numeric columns
og_title: Excel-werkboek maken in Java – SQL-gegevens importeren en kolomnummerformaten
  instellen
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
title: Maak een Excel-werkboek in Java en pas kolomnummerformaten toe
url: /nl/java/formatting/create-excel-workbook-java-and-apply-column-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak een Excel‑werkmap in Java en pas kolomnummerformaten toe

Als je een **Excel workbook java** moet maken en numerieke kolommen moet opmaken, laat deze gids je precies zien hoe. Je leert SQL‑gegevens naar Excel te importeren, een getalnotatie voor elke kolom in te stellen, en **de werkmap op te slaan als XLSX** met de Aspose.Cells‑bibliotheek.

Werken met spreadsheets vanuit Java voelt vaak versnipperd aan — ontwikkelaars kopiëren‑en‑plakken fragmenten, vergeten getallen op te maken, of eindigen met CSV‑bestanden in plaats van echte Excel‑bestanden. Deze tutorial verwijdert die wrijving door een enkele, end‑to‑end‑oplossing te bieden die je in elk Java‑project kunt plaatsen.

Aan het einde van dit artikel kun je:

* Verbinden met een database en een `DataTable` (of `ResultSet`) ophalen  
* Een nieuwe werkmap maken met Aspose.Cells  
* Een consistente **add number format excel**‑stijl toepassen op elke kolom  
* **De werkmap opslaan als XLSX** op een locatie naar keuze  

De enige vereiste is een Java‑ontwikkelomgeving (JDK 8+ aanbevolen) en de Aspose.Cells for Java‑JAR op je classpath.

---

## Prerequisites

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| JDK 8 of nieuwer | Biedt de taalfeatures die in het voorbeeld worden gebruikt. |
| Aspose.Cells for Java (latest version) | Behandelt het maken, opmaken en opslaan van Excel zonder dat Office geïnstalleerd is. |
| Een JDBC‑compatibele database (bijv. MySQL, PostgreSQL) | Levert de SQL‑gegevens die we gaan importeren. |
| Maven of Gradle (optioneel) | Vereenvoudigt afhankelijkheidsbeheer. |

Add Aspose.Cells to your Maven `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- use the latest stable version -->
</dependency>
```

Of download de JAR rechtstreeks van de Aspose‑website en voeg deze toe aan de classpath van je project.

---

## Step 1: Create Excel workbook java

Het eerste logische blok is het instantieren van een nieuwe `Workbook`. Dit object vertegenwoordigt het volledige Excel‑bestand in het geheugen en geeft je toegang tot werkbladen, cellen en stijlen.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

Het vooraf aanmaken van de werkmap geeft ons ook een `Style`‑factory die we later nodig hebben wanneer we **set number format column**.

## Step 2: Retrieve data from SQL (import sql data excel)

Hieronder openen we een JDBC‑verbinding, voeren een eenvoudige `SELECT`‑statement uit, en laden de resultset in een Aspose `DataTable`. De `DataTable`‑klasse bootst de .NET `DataTable` na en werkt naadloos met de `importDataTable`‑methode.

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

> **Tip:** Als je al een `DataTable` hebt van een andere bron (bijv. CSV‑parsing), kun je de JDBC‑code overslaan en die tabel direct retourneren.

## Step 3: Prepare a reusable style (add number format excel)

We willen dat elke numerieke kolom getallen weergeeft met twee decimalen en een duizendtalseparator. In plaats van elke cel afzonderlijk op te maken, maken we één `Style`‑object per kolom aan en hergebruiken dit tijdens het importeren. Dit is de meest efficiënte manier om **add number format excel** toe te passen.

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

Je kunt de opmaak‑string (`"#,##0.00"`) aanpassen aan elke Excel‑getalnotatie die je nodig hebt. Voor datums gebruik je `styles[i].setCustom("mm-dd-yyyy")`, enzovoort.

## Step 4: Import the DataTable and apply the column styles

Nu brengen we alles samen. De `importDataTable`‑overload laat ons de `DataTable` doorgeven, specificeren of de eerste rij als kolomkoppen moet worden behandeld, en de stijl‑array leveren. Dit stelt automatisch **set number format column** in voor elke cel in de bijbehorende kolom.

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

Omdat we `true` hebben doorgegeven voor de `importColumnNames`‑vlag, bevat de eerste rij van het werkblad de kolomnamen uit de `DataTable`. Elke volgende rij ontvangt de gegevens, al opgemaakt volgens de stijl die we hebben gedefinieerd.

## Step 5: Save workbook as xlsx

De laatste stap is het opslaan van de in‑memory werkmap naar een fysiek bestand. Aspose.Cells ondersteunt vele formaten; we gebruiken het moderne XLSX‑formaat, wat de meeste applicaties vandaag de dag verwachten.

```java
// Step 5: Save the workbook to an .xlsx file
private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
    workbook.save(filePath, com.aspose.cells.SaveFormat.XLSX);
}
```

Je kunt `filePath` wijzigen naar elke geldige locatie op je systeem. De methode gooit een `IOException` als de map niet bestaat of je geen schrijfrechten hebt.

## Full, runnable example

Door alle onderdelen samen te voegen ontstaat een zelfstandige applicatie die je direct kunt compileren en uitvoeren.

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

### Expected result

Het uitvoeren van het programma maakt een bestand genaamd **DataTableWithNumberFormat.xlsx** aan in de werkmap. Open het met Microsoft Excel, LibreOffice Calc, of een andere XLSX‑compatibele viewer en je ziet:

| Id | Amount | CreatedDate |
|----|--------|-------------|
| 1  | 1,234.56 | 2023‑01‑15 |
| 2  | 78,900.00 | 2023‑02‑20 |
| …  | … | … |

*De **Amount**‑kolom toont getallen met twee decimalen en een duizendtalseparator, dankzij de **add number format excel**‑stijl die we hebben toegepast.*

---

## Common questions and edge‑case handling

| Vraag | Antwoord |
|-------|----------|
| **Wat als mijn query geen rijen retourneert?** | De `DataTable` zal leeg zijn maar nog steeds kolomdefinities bevatten. De werkmap zal alleen de header‑rij bevatten, wat vaak voldoende is voor downstream‑processen. |
| **Hoe pas ik verschillende opmaken per kolom toe?** | Pas `buildColumnStyles` aan om de kolomnaam of datatype te inspecteren en een aangepaste notatie toe te wijzen (bijv. datums, percentages). |
| **Kan ik direct naar een `ByteArrayOutputStream` schrijven?** | Ja. Vervang `workbook.save(filePath, SaveFormat.XLSX);` door 

## What Should You Learn Next?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}