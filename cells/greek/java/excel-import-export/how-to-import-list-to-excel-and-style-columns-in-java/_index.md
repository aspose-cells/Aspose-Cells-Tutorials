---
category: general
date: 2026-08-17
description: Εισαγωγή λίστας στο Excel σε Java χρησιμοποιώντας το Aspose.Cells, μάθετε
  πώς να μορφοποιείτε στήλη, εξάγετε δεδομένα σε xlsx και δημιουργήστε προγραμματιστικά
  ένα βιβλίο εργασίας Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- import list to excel
- how to style column
- export data to xlsx
- import data with header
- create excel workbook java
language: el
lastmod: 2026-08-17
og_description: Εισαγωγή λίστας στο Excel σε Java με το Aspose.Cells, μορφοποίηση
  των κεφαλίδων στηλών, εξαγωγή δεδομένων σε xlsx και δημιουργία βιβλίου εργασίας
  Excel αποδοτικά.
og_image_alt: Screenshot of a Java‑generated Excel file showing bold column headers
og_title: Εισαγωγή λίστας στο Excel με Java – πλήρης οδηγός με στυλ στηλών
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Import list to Excel in Java using Aspose.Cells, learn how to style
    column, export data to xlsx, and create an Excel workbook programmatically.
  headline: How to import list to Excel and style columns in Java
  type: TechArticle
- description: Import list to Excel in Java using Aspose.Cells, learn how to style
    column, export data to xlsx, and create an Excel workbook programmatically.
  name: How to import list to Excel and style columns in Java
  steps:
  - name: Why this works
    text: '* **`importDataTable`** reads the keys of each map (`"Name"` and `"Score"`)
      as column headers when the `true` flag is set. This satisfies the **import data
      with header** requirement. * The **style array** aligns with the column order.
      By setting `columnStyles[1].getFont().setBold(true)`, we answer t'
  - name: Null values and type safety
    text: 'If a map contains `null` or mixed‑type values, Aspose.Cells automatically
      writes an empty cell. To guarantee consistent typing, you can pre‑process the
      list:'
  - name: Mismatched column counts
    text: '`importDataTable` expects the style array length to match the number of
      columns. If you add a new column later, remember to expand `columnStyles` accordingly,
      otherwise Aspose.Cells throws `IndexOutOfBoundsException`.'
  - name: Large data sets
    text: For more than 10 000 rows, consider using the **`importArray`** overload,
      which streams data directly to the worksheet and reduces memory consumption.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Data export
title: Πώς να εισάγετε λίστα στο Excel και να μορφοποιήσετε στήλες σε Java
url: /el/java/excel-import-export/how-to-import-list-to-excel-and-style-columns-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εισάγετε λίστα σε Excel και να μορφοποιήσετε στήλες σε Java

Αν χρειάζεστε **import list to Excel** από μια εφαρμογή Java, αυτός ο οδηγός σας παρουσιάζει μια πλήρη, έτοιμη‑για‑εκτέλεση λύση. Θα δείτε πώς να δημιουργήσετε ένα Excel workbook, να εισάγετε μια λίστα χαρτών ως πίνακα δεδομένων, να εφαρμόσετε έντονο στυλ σε μια συγκεκριμένη στήλη και να αποθηκεύσετε το αποτέλεσμα ως αρχείο **xlsx**.

Η εργασία με υπολογιστικά φύλλα είναι συχνή απαίτηση για αναφορές, ανταλλαγή δεδομένων ή αυτοματοποίηση. Στο τέλος αυτού του tutorial θα μπορείτε να **export data to xlsx** με προσαρμοσμένη μορφοποίηση στηλών χωρίς να βγείτε από τον κώδικα Java.

## Τι θα χρειαστείτε

* Java 17 ή νεότερη (ο κώδικας λειτουργεί επίσης με Java 8+)
* Βιβλιοθήκη Aspose.Cells for Java – έκδοση 23.10 (ή η πιο πρόσφατη έκδοση)
* Περιβάλλον ανάπτυξης όπως IntelliJ IDEA ή Eclipse
* Βασική εξοικείωση με τις συλλογές της Java (`List`, `Map`)

> **Συμβουλή:** Προσθέστε την εξάρτηση Maven του Aspose.Cells για να διατηρείτε τη βιβλιοθήκη ενημερωμένη:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

## Εισαγωγή λίστας σε Excel με Aspose.Cells

Το πρώτο σημαντικό βήμα είναι η μετατροπή ενός Java `List<Map<String,Object>>` σε ένα φύλλο εργασίας Excel. Το Aspose.Cells παρέχει τη μέθοδο `importDataTable`, η οποία δέχεται μια συλλογή, μια σημαία κεφαλίδας, μια αρχική γραμμή/στήλη και έναν προαιρετικό πίνακα στυλ.

```java
import com.aspose.cells.*;
import java.util.*;

public class ImportListToExcel {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Prepare the source data (simulating a DataTable)
        List<Map<String, Object>> dataRows = new ArrayList<>();
        dataRows.add(Map.of("Name", "Alice", "Score", 95));
        dataRows.add(Map.of("Name", "Bob",   "Score", 82));
        dataRows.add(Map.of("Name", "Charlie", "Score", 78));

        // 2️⃣ Create style objects – make the "Score" column bold
        Style[] columnStyles = new Style[2];               // two columns: Name, Score
        Workbook styleWorkbook = new Workbook();           // temporary workbook for style creation
        columnStyles[0] = styleWorkbook.createStyle();    // default style for "Name"
        columnStyles[1] = styleWorkbook.createStyle();    // custom style for "Score"
        columnStyles[1].getFont().setBold(true);          // **how to style column** – bold font

        // 3️⃣ Import the list into a worksheet using the style array
        Workbook workbook = new Workbook();                // **create excel workbook java**
        Worksheet sheet = workbook.getWorksheets().get(0);
        // true → include column headers from the map keys
        sheet.getCells().importDataTable(dataRows, true, 0, 0, columnStyles);

        // 4️⃣ Save the workbook to an .xlsx file
        String outputPath = "output/datatable_with_style.xlsx";
        workbook.save(outputPath, SaveFormat.XLSX);

        System.out.println("Workbook saved to: " + outputPath);
    }
}
```

### Γιατί λειτουργεί αυτό

* **`importDataTable`** διαβάζει τα κλειδιά κάθε χάρτη (`"Name"` και `"Score"`) ως κεφαλίδες στηλών όταν το flag `true` είναι ορισμένο. Αυτό ικανοποιεί την απαίτηση **import data with header**.
* Ο **style array** ευθυγραμμίζεται με τη σειρά των στηλών. Ορίζοντας `columnStyles[1].getFont().setBold(true)`, απαντάμε στην ερώτηση **how to style column** χωρίς να επηρεάσουμε άλλες στήλες.
* Η χρήση ενός προσωρινού `Workbook` μόνο για τη δημιουργία στυλ αποτρέπει τη ρύπανση του τελικού βιβλίου εργασίας με περιττά κελιά.

## Εξαγωγή δεδομένων σε xlsx – αντιμετώπιση κοινών περιπτώσεων άκρων

### Τιμές null και ασφάλεια τύπων
Αν ένας χάρτης περιέχει `null` ή τιμές μικτής τύπου, το Aspose.Cells αυτόματα γράφει ένα κενό κελί. Για να εγγυηθείτε συνεπή τυποποίηση, μπορείτε να προεπεξεργαστείτε τη λίστα:

```java
for (Map<String, Object> row : dataRows) {
    row.replaceAll((k, v) -> v == null ? "" : v);
}
```

### Μη ταιριασμένοι αριθμοί στηλών
Η `importDataTable` απαιτεί το μήκος του style array να ταιριάζει με τον αριθμό των στηλών. Αν προσθέσετε μια νέα στήλη αργότερα, θυμηθείτε να επεκτείνετε το `columnStyles` αναλόγως, διαφορετικά το Aspose.Cells θα ρίξει `IndexOutOfBoundsException`.

### Μεγάλα σύνολα δεδομένων
Για περισσότερες από 10 000 γραμμές, σκεφτείτε να χρησιμοποιήσετε την υπερφόρτωση **`importArray`**, η οποία μεταδίδει τα δεδομένα απευθείας στο φύλλο εργασίας και μειώνει την κατανάλωση μνήμης.

## Πώς να μορφοποιήσετε πρόσθετες στήλες

Μπορείτε να μορφοποιήσετε οποιαδήποτε στήλη επεκτείνοντας τον πίνακα `columnStyles`. Παρακάτω υπάρχει ένα παράδειγμα που κάνει τόσο το “Name” όσο και το “Score” έντονα και προσθέτει χρώμα φόντου στη στήλη “Score”.

```java
// Extend to three columns (Name, Score, Date)
Style[] extendedStyles = new Style[3];
Workbook tmp = new Workbook();
extendedStyles[0] = tmp.createStyle(); // Name – bold
extendedStyles[0].getFont().setBold(true);

extendedStyles[1] = tmp.createStyle(); // Score – bold + yellow background
extendedStyles[1].getFont().setBold(true);
extendedStyles[1].getPattern().setBackgroundColor(Color.getYellow());

extendedStyles[2] = tmp.createStyle(); // Date – default
```

Αντικαταστήστε το αρχικό `columnStyles` με `extendedStyles` και προσαρμόστε την πηγή δεδομένων αναλόγως. Αυτό δείχνει **how to style column** για πολλαπλά σενάρια.

## Επαλήθευση του αποτελέσματος

Ανοίξτε το `output/datatable_with_style.xlsx` στο Microsoft Excel, Google Sheets ή LibreOffice Calc. Θα πρέπει να δείτε:

| **Name**   | **Score** |
|------------|----------|
| Alice      | **95**   |
| Bob        | **82**   |
| Charlie    | **78**   |

Η κεφαλίδα **Score** και τα κελιά της εμφανίζονται έντονα, επιβεβαιώνοντας ότι το στυλ εφαρμόστηκε σωστά.

## Πλήρες παράδειγμα από την αρχή μέχρι το τέλος (έτοιμο για αντιγραφή‑επικόλληση)

```java
import com.aspose.cells.*;
import java.util.*;

public class ImportListToExcelFull {
    public static void main(String[] args) throws Exception {
        // ----- Prepare sample data -----
        List<Map<String, Object>> rows = new ArrayList<>();
        rows.add(Map.of("Name", "Alice",   "Score", 95));
        rows.add(Map.of("Name", "Bob",     "Score", 82));
        rows.add(Map.of("Name", "Charlie", "Score", 78));

        // ----- Create column styles (Score column bold) -----
        Style[] styles = new Style[2];
        Workbook styleWB = new Workbook();                // temporary workbook for style objects
        styles[0] = styleWB.createStyle();                // Name – default
        styles[1] = styleWB.createStyle();                // Score – custom
        styles[1].getFont().setBold(true);                // apply bold font

        // ----- Build the workbook and import the list -----
        Workbook wb = new Workbook();                     // **create excel workbook java**
        Worksheet ws = wb.getWorksheets().get(0);
        ws.getCells().importDataTable(rows, true, 0, 0, styles); // true = import header row

        // ----- Save as XLSX -----
        String outFile = "output/datatable_with_style.xlsx";
        wb.save(outFile, SaveFormat.XLSX);

        System.out.println("Excel file created at: " + outFile);
    }
}
```

Η εκτέλεση αυτού του προγράμματος παράγει το ακριβές workbook που εμφανίστηκε νωρίτερα.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **import list to Excel**, να εφαρμόσετε προσαρμοσμένη μορφοποίηση σε μια συγκεκριμένη στήλη και να **export data to xlsx** χρησιμοποιώντας το Aspose.Cells for Java. Το tutorial κάλυψε:

* Δημιουργία ενός Excel workbook σε Java (`create excel workbook java`)
* Εισαγωγή λίστας χαρτών με κεφαλίδες στηλών (`import data with header`)
* Μορφοποίηση στήλης (`how to style column`) μέσω ενός style array
* Αποθήκευση του αποτελέσματος ως αρχείο XLSX

Από εδώ μπορείτε να εξερευνήσετε πιο προχωρημένη μορφοποίηση (περιγράμματα, μορφές αριθμών), να προσθέσετε γραφήματα ή να δημιουργήσετε πολλαπλά φύλλα εργασίας στο ίδιο workbook. Πειραματιστείτε με διαφορετικές πηγές δεδομένων — αρχεία CSV, βάσεις δεδομένων ή απαντήσεις REST API — για να επεκτείνετε το μοτίβο που παρουσιάστηκε σε αυτόν τον οδηγό.

Καλό κώδικα!

## Τι πρέπει να μάθετε στη συνέχεια;

Οι παρακάτω οδηγίες καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να δημιουργήσετε μια λίστα επικύρωσης δεδομένων Excel με Aspose.Cells για Java: Οδηγός βήμα‑βήμα](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [Δημιουργία & Εισαγωγή δεδομένων XML σε Excel χρησιμοποιώντας Aspose.Cells για Java](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)
- [Μαθήματα εισαγωγής και εξαγωγής δεδομένων Excel για Aspose.Cells Java](/cells/english/java/import-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}