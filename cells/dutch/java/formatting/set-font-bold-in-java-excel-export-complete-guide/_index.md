---
category: general
date: 2026-06-30
description: Stel het lettertype vet in bij het importeren van een DataTable naar
  Excel met Java. Leer code voor voorwaardelijke opmaak, importeer een datatable naar
  Excel en style tabellen moeiteloos.
draft: false
keywords:
- set font bold
- conditional formatting code
- import datatable excel
- how to import datatable
- import table with styles
language: nl
og_description: Stel lettertype vet in Java in bij het exporteren van een DataTable
  naar Excel. Deze gids behandelt code voor voorwaardelijke opmaak, het importeren
  van een datatable naar Excel en het stylen van de tabel.
og_title: Lettertype vet maken in Java Excel‑export – Stapsgewijze tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set font bold while importing a DataTable to Excel using Java. Learn
    conditional formatting code, import datatable excel and style tables effortlessly.
  headline: Set Font Bold in Java Excel Export – Complete Guide
  type: TechArticle
- description: Set font bold while importing a DataTable to Excel using Java. Learn
    conditional formatting code, import datatable excel and style tables effortlessly.
  name: Set Font Bold in Java Excel Export – Complete Guide
  steps:
  - name: '**Create a mock `DataTable`** that mimics data you’d normally pull from
      a database.'
    text: '**Create a mock `DataTable`** that mimics data you’d normally pull from
      a database.'
  - name: '**Generate a `CellStyle` array** where every even column gets a bold font
      – that’s the core of **set font bold**.'
    text: '**Generate a `CellStyle` array** where every even column gets a bold font
      – that’s the core of **set font bold**.'
  - name: '**Grab the first worksheet** from the workbook.'
    text: '**Grab the first worksheet** from the workbook.'
  - name: '**Import the `DataTable`** with column headers, starting at cell `A1`,
      and apply the prepared styles.'
    text: '**Import the `DataTable`** with column headers, starting at cell `A1`,
      and apply the prepared styles.'
  - name: (Optional) **Add a conditional formatting rule** to illustrate the **conditional
      formatting code** keyword.
    text: (Optional) **Add a conditional formatting rule** to illustrate the **conditional
      formatting code** keyword.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DataTable
title: Lettertype vet maken in Java Excel-export – Complete gids
url: /nl/java/formatting/set-font-bold-in-java-excel-export-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vetgedrukte Lettertype Instellen in Java Excel Export – Complete Gids

Heb je je ooit afgevraagd **hoe je lettertype vetgedrukt kunt maken** voor specifieke kolommen terwijl je **datatabel‑excelbestanden importeert**? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze een mooi gestileerde spreadsheet nodig hebben zonder handmatig elke cel aan te passen. Het goede nieuws? Met een paar regels Java kun je een `DataTable` importeren, vetgedrukte lettertypen toepassen en zelfs wat **conditional formatting code** toevoegen—alles programmatically.

In deze tutorial lopen we een volledig, uitvoerbaar voorbeeld door dat laat zien **hoe je datatable importeert** in een Excel‑werkmap, **vetgedrukt lettertype instelt** op elke even‑geïndexeerde kolom, en optioneel een eenvoudige voorwaardelijke opmaak toevoegt. Aan het einde heb je een kant‑klaar fragment en een duidelijk begrip van **import table with styles** voor elk project.

## Vereisten

- Java 8 of nieuwer (de code werkt ook op Java 17)  
- Aspose.Cells for Java (een gratis proefversie is voldoende) – voeg de Maven‑dependency of de JAR toe aan je classpath.  
- Basiskennis van `java.sql` `ResultSet` → `DataTable` conversie (we mocken een tabel voor de eenvoud).  
- Een IDE of een build‑tool zoals Maven/Gradle.

> **Pro tip:** Als je Maven gebruikt, voeg dit toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for the latest version -->
</dependency>
```

## Overzicht van de Oplossing

1. **Maak een mock `DataTable`** die de gegevens nabootst die je normaal uit een database zou halen.  
2. **Genereer een `CellStyle`‑array** waarbij elke even kolom een vet lettertype krijgt – dat is de kern van **set font bold**.  
3. **Haal het eerste werkblad** uit de werkmap.  
4. **Importeer de `DataTable`** met kolomkoppen, beginnend bij cel `A1`, en pas de voorbereide stijlen toe.  
5. (Optioneel) **Voeg een voorwaardelijke opmaakregel toe** om het **conditional formatting code**‑trefwoord te illustreren.

Elke stap wordt in duidelijk Nederlands uitgelegd, en de codeblokken zijn volledig zelf‑voorzien zodat je ze direct kunt kopiëren, plakken en uitvoeren.

---

## Stap 1: Haal de DataTable op of bouw deze

In real‑world apps roep je waarschijnlijk `ResultSet` → `DataTable` conversie‑utilities aan. Voor deze gids bouwen we handmatig een eenvoudige `DataTable` zodat je je kunt concentreren op het Excel‑gedeelte.

```java
import com.aspose.cells.*;
import java.util.*;

public class ExcelExportDemo {

    /** Creates a sample DataTable with three columns and a few rows. */
    private static DataTable getDataTable() {
        // Define column names
        List<String> columns = Arrays.asList("ID", "Name", "Score");

        // Create the DataTable and add columns
        DataTable table = new DataTable();
        for (String col : columns) {
            table.getColumns().add(col);
        }

        // Populate rows
        Object[][] rows = {
            {1, "Alice", 85},
            {2, "Bob", 92},
            {3, "Charlie", 78},
            {4, "Diana", 88}
        };

        for (Object[] row : rows) {
            DataRow dr = table.getRows().add();
            for (int i = 0; i < row.length; i++) {
                dr.get(i).setValue(row[i]);
            }
        }
        return table;
    }
```

> **Waarom dit belangrijk is:** Een kant‑klare `DataTable` laat ons focussen op de **import datatable excel**‑API en de stijl‑logica. De bovenstaande methode is herbruikbaar—vervang gewoon de hard‑gecodeerde rijen door een database‑query wanneer je naar productie gaat.

---

## Stap 2: Stijlen Voorbereiden – Hier **Set Font Bold** Toevoegen

Nu bouwen we een array van `CellStyle`‑objecten, één per kolom. De regel is simpel: **set font bold** voor elke even‑geïndexeerde kolom (0, 2, 4,…). De oneven kolommen blijven normaal.

```java
    /** Creates a CellStyle array where even columns have a bold font. */
    private static CellStyle[] createColumnStyles(Workbook wb, DataTable table) {
        int columnCount = table.getColumns().size();
        CellStyle[] styles = new CellStyle[columnCount];

        for (int i = 0; i < columnCount; i++) {
            // Create a new style instance for the column
            styles[i] = wb.createStyle();

            // Set the font to bold if the column index is even
            Font font = styles[i].getFont();
            font.setBold(i % 2 == 0);   // <-- this line performs the set font bold action
        }
        return styles;
    }
```

### Waarom een Array van Stijlen Gebruiken?

- **Prestaties:** Een stijl per kolom toepassen is sneller dan elke cel afzonderlijk te stijlen.  
- **Consistentie:** Elke cel in een kolom erft dezelfde opmaak, wat een uniform uiterlijk garandeert.  
- **Schaalbaarheid:** Later meer kolommen toevoegen vereist alleen het uitbreiden van de array—geen code‑herziening.

---

## Stap 3: Toegang tot het Eerste Werkblad in de Werkmap

Aspose.Cells maakt een standaard werkblad voor ons aan, maar het is goede gewoonte om dit expliciet op te halen. Dit laat ook zien **hoe je datatable importeert** in een specifiek blad.

```java
    /** Retrieves the first worksheet from the workbook. */
    private static Worksheet getFirstWorksheet(Workbook wb) {
        // Worksheets are zero‑based; index 0 is the first sheet.
        return wb.getWorksheets().get(0);
    }
```

---

## Stap 4: De DataTable Importeren met Stijlen – De Kern **Import Table With Styles** Operatie

De `importDataTable`‑methode doet het zware werk. Ze kopieert de gegevens, voegt kolomkoppen toe en past de eerder gebouwde stijl‑array toe.

```java
    /** Imports the DataTable into the worksheet, applying column styles. */
    private static void importTableWithStyles(Worksheet sheet, DataTable table, CellStyle[] styles) {
        // Parameters: (DataTable, import column headers?, start row, start column, styles)
        sheet.getCells().importDataTable(table, true, 0, 0, styles);
    }
```

Wanneer je het voorbeeld uitvoert, zie je **set font bold** toegepast op de kolommen `ID` en `Score`, terwijl `Name` normaal blijft.

---

## Stap 5 (Optioneel): Voorwaardelijke Opmaak Toevoegen – Een Snel **Conditional Formatting Code** Voorbeeld

Wil je rijen markeren waar de score hoger is dan 90, dan volstaat een paar extra regels. Dit toont het **conditional formatting code**‑trefwoord zonder de hoofdflow te verstoren.

```java
    /** Adds a simple conditional format that colors scores > 90 in green. */
    private static void addConditionalFormatting(Worksheet sheet) {
        // Define the range: rows 2‑5 (zero‑based), column C (index 2)
        int firstRow = 1;  // row after header
        int lastRow = sheet.getCells().getMaxDataRow();
        int scoreCol = 2;  // zero‑based index for "Score"

        // Build the range string, e.g., "C2:C5"
        String range = new StyleRegion(firstRow, scoreCol, lastRow, scoreCol).getRefersTo();

        // Create a new conditional formatting collection
        FormatConditionCollection fcc = sheet.getConditionalFormattings().add();

        // Add a condition: cell value > 90
        FormatCondition condition = fcc.addCondition(FormatConditionType.CELL_VALUE, OperatorType.GREATER_THAN, "90", null);
        condition.getStyle().setBackgroundColor(Color.getLightGreen());

        // Apply the condition to the range
        fcc.addArea(new CellArea(firstRow, scoreCol, lastRow, scoreCol));
    }
```

> **Opmerking:** Het bovenstaande fragment is optioneel maar laat zien hoe je **conditional formatting code** bovenop de reeds gestylede tabel kunt stapelen.

---

## Alles Samenvoegen – Volledig, Uitvoerbaar Voorbeeld

```java
import com.aspose.cells.*;
import java.util.*;

public class ExcelExportDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook (in‑memory)
        Workbook wb = new Workbook();

        // 2️⃣ Retrieve the DataTable we want to export
        DataTable dataTable = getDataTable();

        // 3️⃣ Prepare column styles – this is where we set font bold
        CellStyle[] columnStyles = createColumnStyles(wb, dataTable);

        // 4️⃣ Grab the first worksheet
        Worksheet sheet = getFirstWorksheet(wb);

        // 5️⃣ Import the table with headers and our styles
        importTableWithStyles(sheet, dataTable, columnStyles);

        // 6️⃣ OPTIONAL: add a conditional formatting rule
        addConditionalFormatting(sheet);

        // 7️⃣ Save the workbook to disk
        String outPath = "StyledDataTable.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);
    }

    // ----- Helper methods from earlier sections -----
    private static DataTable getDataTable() {
        List<String> columns = Arrays.asList("ID", "Name", "Score");
        DataTable table = new DataTable();
        for (String col : columns) {
            table.getColumns().add(col);
        }
        Object[][] rows = {
            {1, "Alice", 85},
            {2, "Bob", 92},
            {3, "Charlie", 78},
            {4, "Diana", 88}
        };
        for (Object[] row : rows) {
            DataRow dr = table.getRows().add();
            for (int i = 0; i < row.length; i++) {
                dr.get(i).setValue(row[i]);
            }
        }
        return table;
    }

    private static CellStyle[] createColumnStyles(Workbook wb, DataTable table) {
        int colCount = table.getColumns().size();
        CellStyle[] styles = new CellStyle[colCount];
        for (int i = 0; i < colCount; i++) {
            styles[i] = wb.createStyle();
            Font font = styles[i].getFont();
            font.setBold(i % 2 == 0);   // set font bold for even columns
        }
        return styles;
    }

    private static Worksheet getFirstWorksheet(Workbook wb) {
        return wb.getWorksheets().get(0);
    }

    private static void importTableWithStyles(Worksheet sheet, DataTable table, CellStyle[] styles) {
        sheet.getCells().importDataTable(table, true, 0, 0, styles);
    }

    private static void addConditionalFormatting(Worksheet sheet


## Wat Moet Je Nu Leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Automate Excel Conditional Formatting Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [How to Implement Custom Font Settings in Aspose.Cells Java for Excel Formatting](/cells/english/java/formatting/aspose-cells-java-custom-fonts/)
- [Set Font Size in Excel Using Aspose.Cells Java - Comprehensive Guide](/cells/english/java/formatting/aspose-cells-java-set-font-size-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}