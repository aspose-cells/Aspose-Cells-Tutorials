---
category: general
date: 2026-08-14
description: Πώς να ορίσετε διαχωριστικό και να αποθηκεύσετε ως CSV χρησιμοποιώντας
  το Aspose.Cells, να περιορίσετε τα ψηφία, να εξάγετε συμβολοσειρές CSV και να επαναϋπολογίσετε
  τύπους σε Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set delimiter
- save as csv
- recalculate formulas
- how to export csv
- how to limit digits
language: el
lastmod: 2026-08-14
og_description: Πώς να ορίσετε το διαχωριστικό και να αποθηκεύσετε ως CSV με το Aspose.Cells,
  να περιορίσετε τα ψηφία, να εξάγετε συμβολοσειρές CSV και να επαναϋπολογίσετε τύπους
  σε Java.
og_image_alt: Screenshot of Java code that sets a CSV delimiter and saves an Excel
  workbook as CSV using Aspose.Cells
og_title: Πώς να ορίσετε το διαχωριστικό και να αποθηκεύσετε ως CSV – Οδηγός Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  headline: How to set delimiter and save as CSV with Aspose.Cells
  type: TechArticle
- description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  name: How to set delimiter and save as CSV with Aspose.Cells
  steps:
  - name: Why this works
    text: "- `CsvSaveOptions.setDelimiter(char)` tells Aspose.Cells which character
      separates fields. By default it’s a comma, but any character (tab `'\t'`, pipe
      `'|'`, etc.) works. - `setSignificantDigits(int)` limits numeric precision,
      satisfying the **how to limit digits** requirement without manually form"
  - name: When to use this
    text: '- Returning CSV from a REST endpoint (`@RestController` in Spring) - Embedding
      CSV data into an email attachment without writing to disk - Performing quick
      sanity checks during unit tests'
  - name: Why recalculate?
    text: '- Formulas may reference external data or volatile functions (`NOW()`,
      `RAND()`) that need fresh values. - Dynamic‑array formulas (e.g., `=SORT(A1:A10)`)
      are evaluated automatically, but calling `calculateFormula()` guarantees consistency
      across all sheets.'
  - name: Verifying the result
    text: 1. Open `output.csv` in a text editor – you should see a semicolon (`;`)
      separating each column. 2. Confirm that numeric columns display at most five
      significant digits. 3. The console output will print the CSV string generated
      in step 4. 4. Open `japan_updated.xlsx` in Excel – any formulas that pre
  type: HowTo
tags:
- Aspose.Cells
- Java
- CSV export
- Excel automation
title: Πώς να ορίσετε το διαχωριστικό και να αποθηκεύσετε ως CSV με το Aspose.Cells
url: /el/java/excel-import-export/how-to-set-delimiter-and-save-as-csv-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ορίσετε το διαχωριστικό και να αποθηκεύσετε ως CSV με το Aspose.Cells

Αν χρειάζεστε **πώς να ορίσετε το διαχωριστικό** κατά την εξαγωγή δεδομένων από ένα βιβλίο εργασίας Excel, αυτός ο οδηγός σας παρουσιάζει μια πλήρη, ολοκληρωμένη λύση χρησιμοποιώντας το Aspose.Cells for Java. Θα μάθετε πώς να ρυθμίσετε το διαχωριστικό CSV, να περιορίσετε τον αριθμό των σημαντικών ψηφίων, να εξάγετε μια συμβολοσειρά CSV και να ανανεώσετε τους τύπους dynamic‑array μετά τη φόρτωση ενός βιβλίου εργασίας.

Το σεμινάριο καλύπτει όλα όσα χρειάζεστε για να εκτελέσετε τον κώδικα στο μηχάνημά σας, συμπεριλαμβανομένου του χειρισμού ειδικών ημερολογίων όπως η περίοδος των Ιαπώνων αυτοκρατόρων. Στο τέλος, θα μπορείτε να δημιουργήσετε ακριβή αρχεία CSV, να ελέγχετε την αριθμητική ακρίβεια και να διασφαλίζετε ότι οι τύποι είναι ενημερωμένοι.

## Προαπαιτούμενα

- Java 17 ή νεότερη (ο κώδικας μεταγλωττίζεται επίσης με JDK 11+)
- Aspose.Cells for Java 23.9 ή νεότερη – κατεβάστε από το [Aspose website](https://products.aspose.com/cells/java/)
- Βασική εξοικείωση με Maven ή Gradle για διαχείριση εξαρτήσεων
- Ένα IDE (IntelliJ IDEA, Eclipse, VS Code) ή έναν απλό επεξεργαστή κειμένου και γραμμή εντολών

> **Pro tip:** Χρησιμοποιήστε έναν dedicated `libs` φάκελο ή Maven Central για να διατηρήσετε το Aspose.Cells JAR στο classpath σας. Τα παραδείγματα παρακάτω υποθέτουν ένα Maven project.

## Βήμα 1: Ρύθμιση του Maven project

Δημιουργήστε ένα `pom.xml` με την εξάρτηση Aspose.Cells:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
                             http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>aspose-csv-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.9</version>
            <classifier>jdk17</classifier>
        </dependency>
    </dependencies>
</project>
```

Εκτελέστε `mvn clean compile` για να κατεβάσετε τη βιβλιοθήκη και να επαληθεύσετε ότι η κατασκευή ολοκληρώθηκε επιτυχώς.

## Βήμα 2: Πώς να ορίσετε το διαχωριστικό και να αποθηκεύσετε ως CSV

Ο κύριος στόχος είναι να αλλάξετε το προεπιλεγμένο διαχωριστικό κόμμα σε έναν προσαρμοσμένο χαρακτήρα (π.χ., semicolon) κατά την αποθήκευση ενός βιβλίου εργασίας Excel ως CSV. Το Aspose.Cells παρέχει το `CsvSaveOptions` για αυτό το σκοπό.

```java
package com.example;

import com.aspose.cells.*;

public class CsvDelimiterDemo {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook (replace the path with your file)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Configure CSV save options
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        // Primary requirement: set a custom delimiter
        csvOptions.setDelimiter(';');               // <-- how to set delimiter
        // Optional: limit the number of significant digits
        csvOptions.setSignificantDigits(5);         // <-- how to limit digits

        // Save the workbook as CSV using the configured options
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);

        System.out.println("CSV file saved with ';' delimiter and 5‑digit precision.");
    }
}
```

### Γιατί λειτουργεί αυτό

- `CsvSaveOptions.setDelimiter(char)` λέει στο Aspose.Cells ποιος χαρακτήρας διαχωρίζει τα πεδία. Από προεπιλογή είναι κόμμα, αλλά οποιοσδήποτε χαρακτήρας (tab `'\t'`, pipe `'|'`, κ.λπ.) λειτουργεί.
- `setSignificantDigits(int)` περιορίζει την αριθμητική ακρίβεια, ικανοποιώντας την απαίτηση **how to limit digits** χωρίς να μορφοποιείτε χειροκίνητα κάθε κελί.

#### Αναμενόμενη έξοδος

Το αρχείο `output.csv` θα περιέχει γραμμές όπως:

```
Name;Amount;Date
Alice;123.46;2024-01-15
Bob;78.90;2024-01-16
```

Παρατηρήστε ότι οι αριθμοί στρογγυλοποιούνται σε πέντε σημαντικά ψηφία (π.χ., `123.45678` → `123.46`).

## Βήμα 3: Πώς να περιορίσετε τα ψηφία κατά την αποθήκευση CSV

Αν χρειάζεστε πιο αυστηρό έλεγχο της αριθμητικής μορφοποίησης, μπορείτε επίσης να χρησιμοποιήσετε ένα αντικείμενο `CsvSaveOptions` για να καθορίσετε μια προσαρμοσμένη συμβολοσειρά μορφής αριθμού.

```java
CsvSaveOptions csvOptions = new CsvSaveOptions();
csvOptions.setDelimiter(',');                // standard comma delimiter
csvOptions.setNumberFormat("0.####");        // up to 4 decimal places
csvOptions.setSignificantDigits(6);          // overall significant digits
```

- `setNumberFormat` ακολουθεί μοτίβα τύπου .NET, τα οποία το Aspose.Cells σέβεται.
- Ο συνδυασμός τόσο του `setNumberFormat` όσο και του `setSignificantDigits` σας παρέχει προβλέψιμη στρογγυλοποίηση σε διαφορετικές τοπικές ρυθμίσεις.

## Βήμα 4: Πώς να εξάγετε CSV ως συμβολοσειρά με προσαρμοσμένο διαχωριστικό

Μερικές φορές δεν θέλετε ένα φυσικό αρχείο· χρειάζεστε τα δεδομένα CSV στη μνήμη (π.χ., για αποστολή ως HTTP response). Η κλάση `ExportTableOptions` σας επιτρέπει να εξάγετε μια περιοχή ως συμβολοσειρά.

```java
// Export a range (rows 0‑9, columns 0‑4) as a CSV string
ExportTableOptions exportOptions = new ExportTableOptions();
exportOptions.setExportAsString(true);   // return a string instead of a file
exportOptions.setDelimiter(',');         // <-- how to set delimiter for export
exportOptions.setIncludeColumnNames(true);

String csvData = workbook.getWorksheets()
                         .get(0)                     // first worksheet
                         .getCells()
                         .exportDataTableAsString(0, 0, 10, 5, exportOptions);

System.out.println("Exported CSV string:");
System.out.println(csvData);
```

### Πότε να το χρησιμοποιήσετε

- Επιστροφή CSV από ένα REST endpoint (`@RestController` στο Spring)
- Ενσωμάτωση δεδομένων CSV σε συνημμένο email χωρίς εγγραφή στο δίσκο
- Εκτέλεση γρήγορων ελέγχων εγκυρότητας κατά τη διάρκεια unit tests

## Βήμα 5: Πώς να επαναϋπολογίσετε τύπους μετά τη φόρτωση ενός βιβλίου εργασίας

Αν το βιβλίο εργασίας σας περιέχει τύπους—ιδιαίτερα **dynamic‑array formulas** που εισήχθησαν σε πρόσφατες εκδόσεις του Excel—πρέπει να τους επαναϋπολογίσετε μετά τη φόρτωση του αρχείου. Το Aspose.Cells αυτόματα ανανεώνει τα αποτελέσματα των dynamic‑array, αλλά εξακολουθεί να χρειάζεται να καλέσετε `calculateFormula()` για τους κανονικούς τύπους.

```java
// Load a workbook that uses the Japanese Emperor calendar (optional step)
LoadOptions loadOptions = new LoadOptions();
loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

// Recalculate all formulas in the workbook
japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

// Save the refreshed workbook (preserves the original calendar)
japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
System.out.println("Formulas recalculated and workbook saved.");
```

### Γιατί να επαναϋπολογίσετε;

- Οι τύποι μπορεί να αναφέρονται σε εξωτερικά δεδομένα ή σε μεταβλητές συναρτήσεις (`NOW()`, `RAND()`) που χρειάζονται νέες τιμές.
- Οι dynamic‑array formulas (π.χ., `=SORT(A1:A10)`) αξιολογούνται αυτόματα, αλλά η κλήση του `calculateFormula()` εγγυάται τη συνέπεια σε όλα τα φύλλα.

## Βήμα 6: Πλήρες παράδειγμα από την αρχή μέχρι το τέλος

Παρακάτω υπάρχει μια μοναδική κλάση που δείχνει **how to set delimiter**, **save as CSV**, **limit digits**, **export a CSV string**, **load a workbook with a special calendar**, και **recalculate formulas**. Ο κώδικας είναι έτοιμος για αντιγραφή‑επικόλληση στο πρόγραμμά σας.

```java
package com.example;

import com.aspose.cells.*;

public class AsposeCsvFullDemo {
    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // 1. Load an existing workbook
        // -----------------------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // -----------------------------------------------------------------
        // 2. Configure CSV save options (delimiter + digit limit)
        // -----------------------------------------------------------------
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        csvOptions.setDelimiter(';');          // <-- how to set delimiter
        csvOptions.setSignificantDigits(5);    // <-- how to limit digits

        // -----------------------------------------------------------------
        // 3. Save the workbook as CSV
        // -----------------------------------------------------------------
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);
        System.out.println("Saved CSV with ';' delimiter.");

        // -----------------------------------------------------------------
        // 4. Export a range as a CSV string (custom delimiter)
        // -----------------------------------------------------------------
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);
        exportOptions.setDelimiter(',');       // <-- how to set delimiter for export
        exportOptions.setIncludeColumnNames(true);

        String csvString = workbook.getWorksheets()
                                   .get(0)
                                   .getCells()
                                   .exportDataTableAsString(0, 0, 10, 5, exportOptions);
        System.out.println("CSV string exported:");
        System.out.println(csvString);

        // -----------------------------------------------------------------
        // 5. Load a workbook that uses the Japanese Emperor calendar
        // -----------------------------------------------------------------
        LoadOptions loadOptions = new LoadOptions();
        loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
        Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

        // -----------------------------------------------------------------
        // 6. Recalculate formulas (including dynamic‑array formulas)
        // -----------------------------------------------------------------
        japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

        // -----------------------------------------------------------------
        // 7. Save the refreshed workbook
        // -----------------------------------------------------------------
        japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
        System.out.println("Japanese workbook refreshed and saved.");
    }
}
```

### Επαλήθευση του αποτελέσματος

1. Ανοίξτε το `output.csv` σε έναν επεξεργαστή κειμένου – θα πρέπει να δείτε ένα semicolon (`;`) που διαχωρίζει κάθε στήλη.
2. Επιβεβαιώστε ότι οι αριθμητικές στήλες εμφανίζουν το πολύ πέντε σημαντικά ψηφία.
3. Η έξοδος της κονσόλας θα εκτυπώσει τη συμβολοσειρά CSV που δημιουργήθηκε στο βήμα 4.
4. Ανοίξτε το `japan_updated.xlsx` στο Excel – οποιοσδήποτε τύπος που προηγουμένως έδειχνε `#REF!` ή παλιές τιμές θα εμφανίσει τώρα τα σωστά αποτελέσματα.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Πρόβλημα | Αιτία | Διόρθωση |
|----------|-------|----------|
| Το CSV εμφανίζει επιπλέον εισαγωγικά | Τα κελιά περιέχουν κόμματα ενώ το διαχωριστικό είναι επίσης κόμμα | Χρησιμοποιήστε διαφορετικό διαχωριστικό (`;` ή `\t`) μέσω του `setDelimiter` |
| Οι αριθμοί στρογγυλοποιούνται λανθασμένα | `setSignificantDigits` εφαρμόστηκε μετά την προσαρμοσμένη μορφή αριθμού | Εφαρμόστε `setNumberFormat` **πριν** `setSignificantDigits` |

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω σεμινάρια καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να φορτώσετε και να αποθηκεύσετε Excel ως CSV χρησιμοποιώντας το Aspose.Cells for Java: Ένας ολοκληρωμένος οδηγός](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [Πώς να φορτώσετε ένα αρχείο CSV χρησιμοποιώντας το Aspose.Cells for Java: Ένας ολοκληρωμένος οδηγός](/cells/english/java/workbook-operations/load-csv-aspose-cells-java-tutorial/)
- [Πώς να φορτώσετε αρχεία CSV χρησιμοποιώντας προσαρμοσμένους αναλυτές σε Java με το Aspose.Cells](/cells/english/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}