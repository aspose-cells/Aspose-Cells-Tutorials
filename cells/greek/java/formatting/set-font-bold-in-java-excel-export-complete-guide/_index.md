---
category: general
date: 2026-06-30
description: Ορίστε τη γραμματοσειρά σε έντονη μορφή κατά την εισαγωγή ενός DataTable
  στο Excel χρησιμοποιώντας Java. Μάθετε κώδικα υπό συνθήκες μορφοποίησης, εισάγετε
  DataTable στο Excel και μορφοποιήστε πίνακες χωρίς κόπο.
draft: false
keywords:
- set font bold
- conditional formatting code
- import datatable excel
- how to import datatable
- import table with styles
language: el
og_description: Ορίστε τη γραμματοσειρά σε έντονη στην Java κατά την εξαγωγή ενός
  DataTable σε Excel. Αυτός ο οδηγός καλύπτει κώδικα υπό συνθήκες μορφοποίησης, εισαγωγή
  DataTable σε Excel και στυλιζάρισμα του πίνακα.
og_title: Ορισμός έντονης γραμματοσειράς στην εξαγωγή Excel με Java – Βήμα‑βήμα οδηγός
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
title: Ορισμός έντονης γραμματοσειράς στην εξαγωγή Excel με Java – Πλήρης οδηγός
url: /el/java/formatting/set-font-bold-in-java-excel-export-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Set Font Bold in Java Excel Export – Complete Guide

Έχετε αναρωτηθεί ποτέ **how to set font bold** για συγκεκριμένες στήλες ενώ **import datatable excel** αρχεία; Δεν είστε ο μόνος. Πολλοί προγραμματιστές συναντούν δυσκολίες όταν χρειάζονται ένα καλά μορφοποιημένο φύλλο εργασίας χωρίς να πρέπει να τροποποιούν κάθε κελί χειροκίνητα. Τα καλά νέα; Με λίγες γραμμές Java μπορείτε να εισάγετε ένα `DataTable`, να εφαρμόσετε έντονη γραμματοσειρά και ακόμη να προσθέσετε λίγο **conditional formatting code**—όλα προγραμματιστικά.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει **how to import datatable** σε ένα Excel workbook, εφαρμόζει **set font bold** σε κάθε στήλη με ζυγό δείκτη, και προαιρετικά προσθέτει μια απλή conditional format. Στο τέλος θα έχετε ένα έτοιμο snippet και μια σαφή κατανόηση του **import table with styles** για οποιοδήποτε έργο.

## Προαπαιτούμενα

- Java 8 ή νεότερη (ο κώδικας λειτουργεί και σε Java 17)  
- Aspose.Cells for Java (η δωρεάν δοκιμαστική έκδοση είναι εντάξει) – προσθέστε την εξάρτηση Maven ή το JAR στο classpath σας.  
- Βασική εξοικείωση με τη μετατροπή `java.sql` `ResultSet` → `DataTable` (θα δημιουργήσουμε ένα mock πίνακα για απλότητα).  
- Ένα IDE ή ένα εργαλείο κατασκευής όπως Maven/Gradle.

> **Pro tip:** Αν χρησιμοποιείτε Maven, προσθέστε αυτό στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for the latest version -->
</dependency>
```

## Επισκόπηση της Λύσης

1. **Create a mock `DataTable`** που προσομοιώνει τα δεδομένα που συνήθως θα αντλούσατε από μια βάση δεδομένων.  
2. **Generate a `CellStyle` array** όπου κάθε ζυγή στήλη λαμβάνει έντονη γραμματοσειρά – αυτό είναι ο πυρήνας του **set font bold**.  
3. **Grab the first worksheet** από το workbook.  
4. **Import the `DataTable`** με τις κεφαλίδες των στηλών, ξεκινώντας από το κελί `A1`, και εφαρμόστε τα προετοιμασμένα στυλ.  
5. (Προαιρετικά) **Add a conditional formatting rule** για να εικονογραφήσετε τη λέξη‑κλειδί **conditional formatting code**.

Κάθε βήμα εξηγείται με απλά αγγλικά, και τα μπλοκ κώδικα είναι πλήρως αυτόνομα ώστε να μπορείτε να τα αντιγράψετε‑επικολλήσετε και να τα εκτελέσετε αμέσως.

---

## Βήμα 1: Ανάκτηση ή Δημιουργία του DataTable για Εισαγωγή

Σε πραγματικές εφαρμογές πιθανότατα θα καλέσετε βοηθητικές λειτουργίες μετατροπής `ResultSet` → `DataTable`. Για αυτόν τον οδηγό θα δημιουργήσουμε ένα απλό `DataTable` χειροκίνητα ώστε να μπορείτε να εστιάσετε στο κομμάτι του Excel.

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

> **Why this matters:** Έχοντας ένα `DataTable` έτοιμο μας επιτρέπει να εστιάσουμε στο API **import datatable excel** και στη λογική του στυλ. Η παραπάνω μέθοδος είναι επαναχρησιμοποιήσιμη—απλώς αντικαταστήστε τις σκληρά κωδικοποιημένες γραμμές με ένα ερώτημα βάσης δεδομένων όταν μεταβείτε στην παραγωγή.

## Βήμα 2: Προετοιμασία Στυλ – Εδώ είναι που **Set Font Bold**

Τώρα θα δημιουργήσουμε έναν πίνακα αντικειμένων `CellStyle`, ένα ανά στήλη. Ο κανόνας είναι απλός: **set font bold** για κάθε στήλη με ζυγό δείκτη (0, 2, 4,…). Οι περιττές στήλες παραμένουν κανονικές.

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

### Γιατί να Χρησιμοποιήσουμε έναν Πίνακα Στυλ;

- **Performance:** Η εφαρμογή στυλ ανά στήλη είναι ταχύτερη από το στυλιζάρισμα κάθε κελιού ξεχωριστά.  
- **Consistency:** Κάθε κελί σε μια στήλη κληρονομεί την ίδια μορφοποίηση, εξασφαλίζοντας ομοιόμορφη εμφάνιση.  
- **Scalability:** Η προσθήκη περισσότερων στηλών αργότερα απαιτεί μόνο την επέκταση του πίνακα—χωρίς επαναγραφή κώδικα.

## Βήμα 3: Πρόσβαση στο Πρώτο Worksheet του Workbook

Το Aspose.Cells δημιουργεί ένα προεπιλεγμένο worksheet για εμάς, αλλά είναι καλή πρακτική να το ανακτήσουμε ρητά. Αυτό επίσης δείχνει **how to import datatable** σε ένα συγκεκριμένο φύλλο.

```java
    /** Retrieves the first worksheet from the workbook. */
    private static Worksheet getFirstWorksheet(Workbook wb) {
        // Worksheets are zero‑based; index 0 is the first sheet.
        return wb.getWorksheets().get(0);
    }
```

## Βήμα 4: Εισαγωγή του DataTable με Στυλ – Η Κεντρική Λειτουργία **Import Table With Styles**

Η μέθοδος `importDataTable` κάνει τη σκληρή δουλειά. Αντιγράφει τα δεδομένα, προσθέτει τις κεφαλίδες των στηλών και εφαρμόζει τον πίνακα στυλ που δημιουργήσαμε νωρίτερα.

```java
    /** Imports the DataTable into the worksheet, applying column styles. */
    private static void importTableWithStyles(Worksheet sheet, DataTable table, CellStyle[] styles) {
        // Parameters: (DataTable, import column headers?, start row, start column, styles)
        sheet.getCells().importDataTable(table, true, 0, 0, styles);
    }
```

Όταν εκτελέσετε το παράδειγμα, θα δείτε το **set font bold** εφαρμοσμένο στις στήλες `ID` και `Score`, ενώ η `Name` παραμένει κανονική.

## Βήμα 5 (Προαιρετικό): Προσθήκη Conditional Formatting – Ένα Σύντομο Παράδειγμα **Conditional Formatting Code**

Αν θέλετε να επισημάνετε γραμμές όπου η βαθμολογία υπερβαίνει το 90, μερικές επιπλέον γραμμές θα κάνουν τη δουλειά. Αυτό παρουσιάζει τη λέξη‑κλειδί **conditional formatting code** χωρίς να αποσπάσει την κύρια ροή.

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

> **Note:** Το παραπάνω snippet είναι προαιρετικό αλλά δείχνει πώς μπορείτε να προσθέσετε **conditional formatting code** πάνω στον ήδη μορφοποιημένο πίνακα.

## Συνδυασμός Όλων – Πλήρες, Εκτελέσιμο Παράδειγμα

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


## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Automate Excel Conditional Formatting Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [How to Implement Custom Font Settings in Aspose.Cells Java for Excel Formatting](/cells/english/java/formatting/aspose-cells-java-custom-fonts/)
- [Set Font Size in Excel Using Aspose.Cells Java - Comprehensive Guide](/cells/english/java/formatting/aspose-cells-java-set-font-size-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}