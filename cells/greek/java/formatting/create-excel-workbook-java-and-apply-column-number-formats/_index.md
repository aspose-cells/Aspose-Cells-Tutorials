---
category: general
date: 2026-09-27
description: Δημιουργήστε βιβλίο εργασίας Excel με Java, εισάγετε δεδομένα SQL, ορίστε
  μορφή αριθμού στη στήλη και αποθηκεύστε το βιβλίο εργασίας ως XLSX χρησιμοποιώντας
  το Aspose.Cells σε Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- import sql data excel
- add number format excel
- set number format column
language: el
lastmod: 2026-09-27
og_description: Δημιουργήστε βιβλίο εργασίας Excel με Java, εισάγετε δεδομένα SQL,
  ορίστε μορφή αριθμού στη στήλη και αποθηκεύστε το βιβλίο εργασίας ως XLSX με ένα
  πλήρως λειτουργικό παράδειγμα Java.
og_image_alt: Screenshot of a Java program creating an Excel workbook with styled
  numeric columns
og_title: Δημιουργία βιβλίου εργασίας Excel με Java – εισαγωγή δεδομένων SQL και ορισμός
  μορφών αριθμών στήλης
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
title: Δημιουργία βιβλίου εργασίας Excel με Java και εφαρμογή μορφοποιήσεων αριθμών
  στήλης
url: /el/java/formatting/create-excel-workbook-java-and-apply-column-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία βιβλίου εργασίας Excel java και εφαρμογή μορφοποίησης αριθμών στήλης

Αν χρειάζεστε **create Excel workbook java** και να μορφοποιήσετε αριθμητικές στήλες, αυτός ο οδηγός σας δείχνει ακριβώς πώς. Θα μάθετε να εισάγετε δεδομένα SQL στο Excel, να ορίσετε μορφή αριθμού για κάθε στήλη, και **save workbook as XLSX** χρησιμοποιώντας τη βιβλιοθήκη Aspose.Cells.

Η εργασία με υπολογιστικά φύλλα από τη Java συχνά φαίνεται κατακερματισμένη—οι προγραμματιστές αντιγράφουν‑επικολλούν αποσπάσματα, ξεχνούν να μορφοποιήσουν αριθμούς, ή καταλήγουν με αρχεία CSV αντί για πραγματικά αρχεία Excel. Αυτός ο οδηγός αφαιρεί αυτή τη δυσκολία παρέχοντας μια ενιαία, ολοκληρωμένη λύση που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Java.

Με το τέλος του άρθρου θα μπορείτε να:

* Συνδεθείτε σε μια βάση δεδομένων και ανακτήστε ένα `DataTable` (ή `ResultSet`)  
* Δημιουργήσετε ένα νέο βιβλίο εργασίας με Aspose.Cells  
* Εφαρμόσετε ένα συνεπές στυλ **add number format excel** σε κάθε στήλη  
* **Save workbook as XLSX** σε μια τοποθεσία της επιλογής σας  

Η μόνη προϋπόθεση είναι ένα περιβάλλον ανάπτυξης Java (συνιστάται JDK 8+ ) και το JAR Aspose.Cells for Java στο classpath σας.

---

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|------------------------|
| JDK 8 ή νεότερο | Παρέχει τις δυνατότητες της γλώσσας που χρησιμοποιούνται στο παράδειγμα. |
| Aspose.Cells for Java (τελευταία έκδοση) | Διαχειρίζεται τη δημιουργία, το στυλ και την αποθήκευση Excel χωρίς εγκατεστημένο Office. |
| Μια βάση δεδομένων συμβατή με JDBC (π.χ., MySQL, PostgreSQL) | Παρέχει τα δεδομένα SQL που θα εισάγουμε. |
| Maven ή Gradle (προαιρετικό) | Απλοποιεί τη διαχείριση εξαρτήσεων. |

Προσθέστε το Aspose.Cells στο Maven `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- use the latest stable version -->
</dependency>
```

Ή κατεβάστε το JAR απευθείας από τον ιστότοπο Aspose και προσθέστε το στο classpath του έργου σας.

---

## Βήμα 1: Δημιουργία βιβλίου εργασίας Excel java

Το πρώτο λογικό μπλοκ είναι η δημιουργία ενός νέου `Workbook`. Αυτό το αντικείμενο αντιπροσωπεύει ολόκληρο το αρχείο Excel στη μνήμη και σας δίνει πρόσβαση σε φύλλα εργασίας, κελιά και στυλ.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

Η δημιουργία του βιβλίου εργασίας εκ των προτέρων μας παρέχει επίσης ένα εργοστάσιο `Style` που θα χρειαστούμε αργότερα όταν **set number format column**.

---

## Βήμα 2: Retrieve data from SQL (import sql data excel)

Παρακάτω ανοίγουμε μια σύνδεση JDBC, εκτελούμε μια απλή δήλωση `SELECT` και φορτώνουμε το σύνολο αποτελεσμάτων σε ένα Aspose `DataTable`. Η κλάση `DataTable` μιμείται το .NET `DataTable` και λειτουργεί άψογα με τη μέθοδο `importDataTable`.

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

> **Tip:** Αν έχετε ήδη ένα `DataTable` από άλλη πηγή (π.χ., ανάλυση CSV), μπορείτε να παραλείψετε τον κώδικα JDBC και να επιστρέψετε αυτόν τον πίνακα απευθείας.

---

## Βήμα 3: Προετοιμασία επαναχρησιμοποιήσιμου στυλ (add number format excel)

Θέλουμε κάθε αριθμητική στήλη να εμφανίζει αριθμούς με δύο δεκαδικά ψηφία και διαχωριστικό χιλιάδων. Αντί να μορφοποιούμε κάθε κελί ξεχωριστά, δημιουργούμε ένα αντικείμενο `Style` μία φορά ανά στήλη και το επαναχρησιμοποιούμε κατά την εισαγωγή. Αυτός είναι ο πιο αποδοτικός τρόπος για **add number format excel**.

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

Μπορείτε να προσαρμόσετε τη συμβολοσειρά μορφής (`"#,##0.00"`) σε οποιαδήποτε μορφή αριθμού Excel χρειάζεστε. Για ημερομηνίες, χρησιμοποιήστε `styles[i].setCustom("mm-dd-yyyy")`, κ.λπ.

---

## Βήμα 4: Εισαγωγή του DataTable και εφαρμογή των στυλ στήλης

Τώρα φέρνουμε όλα μαζί. Η υπερφόρτωση `importDataTable` μας επιτρέπει να περάσουμε το `DataTable`, να καθορίσουμε αν η πρώτη γραμμή πρέπει να θεωρηθεί ως επικεφαλίδες στήλης, και να παρέχουμε τον πίνακα στυλ. Αυτό αυτόματα **set number format column** για κάθε κελί στην αντίστοιχη στήλη.

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

Επειδή περάσαμε `true` για τη σημαία `importColumnNames`, η πρώτη γραμμή του φύλλου εργασίας περιέχει τα ονόματα των στηλών από το `DataTable`. Κάθε επόμενη γραμμή λαμβάνει τα δεδομένα, ήδη μορφοποιημένα σύμφωνα με το στυλ που ορίσαμε.

---

## Βήμα 5: Save workbook as xlsx

Το τελικό βήμα είναι να αποθηκεύσουμε το βιβλίο εργασίας στη μνήμη σε ένα φυσικό αρχείο. Το Aspose.Cells υποστηρίζει πολλές μορφές· θα χρησιμοποιήσουμε τη σύγχρονη μορφή XLSX, η οποία είναι αυτή που οι περισσότερες εφαρμογές αναμένουν σήμερα.

```java
// Step 5: Save the workbook to an .xlsx file
private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
    workbook.save(filePath, com.aspose.cells.SaveFormat.XLSX);
}
```

Μπορείτε να αλλάξετε το `filePath` σε οποιαδήποτε έγκυρη τοποθεσία στο σύστημά σας. Η μέθοδος ρίχνει `IOException` εάν ο φάκελος δεν υπάρχει ή δεν έχετε δικαίωμα εγγραφής.

---

## Πλήρες, εκτελέσιμο παράδειγμα

Η συνένωση όλων των τμημάτων δημιουργεί ένα αυτόνομο πρόγραμμα που μπορείτε να μεταγλωττίσετε και να εκτελέσετε αμέσως.

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

### Αναμενόμενο αποτέλεσμα

Η εκτέλεση του προγράμματος δημιουργεί ένα αρχείο με όνομα **DataTableWithNumberFormat.xlsx** στον τρέχοντα φάκελο. Ανοίξτε το με Microsoft Excel, LibreOffice Calc ή οποιονδήποτε προβολέα συμβατό με XLSX και θα δείτε:

| Id | Ποσό | ΗμερομηνίαΔημιουργίας |
|----|------|------------------------|
| 1  | 1,234.56 | 2023‑01‑15 |
| 2  | 78,900.00 | 2023‑02‑20 |
| …  | … | … |

*Η στήλη **Amount** εμφανίζει αριθμούς με δύο δεκαδικά ψηφία και διαχωριστικό χιλιάδων, χάρη στο στυλ **add number format excel** που εφαρμόσαμε.*

---

## Συχνές ερωτήσεις και διαχείριση ειδικών περιπτώσεων

| Ερώτηση | Απάντηση |
|----------|----------|
| **Τι γίνεται αν το ερώτημά μου δεν επιστρέψει γραμμές;** | Το `DataTable` θα είναι κενό αλλά θα περιέχει ακόμη τις ορισμούς των στηλών. Το βιβλίο εργασίας θα περιέχει μόνο τη γραμμή επικεφαλίδας, κάτι που συχνά είναι επαρκές για τις επόμενες διαδικασίες. |
| **Πώς μπορώ να εφαρμόσω διαφορετικές μορφές ανά στήλη;** | Τροποποιήστε το `buildColumnStyles` ώστε να ελέγχει το όνομα της στήλης ή τον τύπο δεδομένων και να εκχωρεί μια προσαρμοσμένη μορφή (π.χ., ημερομηνίες, ποσοστά). |
| **Μπορώ να γράψω απευθείας σε `ByteArrayOutputStream`;** | Ναι. Αντικαταστήστε το `workbook.save(filePath, SaveFormat.XLSX);` με |

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Δημιουργήσετε και να Αποθηκεύσετε ένα Βιβλίο Εργασίας Excel ως SVG χρησιμοποιώντας το Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Δημιουργία και Αποθήκευση Βιβλίου Εργασίας Excel Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Δημιουργία και Αποθήκευση Βιβλίου Εργασίας Excel Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}