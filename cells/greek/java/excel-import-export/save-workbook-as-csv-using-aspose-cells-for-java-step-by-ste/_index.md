---
category: general
date: 2026-09-27
description: Αποθήκευση βιβλίου εργασίας ως CSV με το Aspose.Cells για Java. Μάθετε
  πώς να εξάγετε το Excel σε CSV, να μετατρέψετε τα κελιά του Excel σε συμβολοσειρά
  και να προσαρμόσετε την εξαγωγή ως συμβολοσειρά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save workbook as csv
- export excel to csv
- convert excel cells to string
- how to export as string
language: el
lastmod: 2026-09-27
og_description: Αποθήκευση βιβλίου εργασίας ως CSV χρησιμοποιώντας το Aspose.Cells
  για Java. Αυτός ο οδηγός δείχνει πώς να εξάγετε το Excel σε CSV, να μετατρέψετε
  τα κελιά του Excel σε συμβολοσειρά και να εφαρμόσετε προσαρμοσμένη επεξεργασία συμβολοσειρών.
og_image_alt: Screenshot of Java code that saves a workbook as CSV using Aspose.Cells
og_title: Αποθήκευση βιβλίου εργασίας ως CSV με το Aspose.Cells – Εγχειρίδιο Java
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Save workbook as CSV with Aspose.Cells for Java. Learn to export Excel
    to CSV, convert Excel cells to string, and customize export as string.
  headline: Save workbook as CSV using Aspose.Cells for Java – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- CSV export
- Excel automation
title: Αποθήκευση βιβλίου εργασίας ως CSV χρησιμοποιώντας το Aspose.Cells για Java
  – βήμα‑βήμα οδηγός
url: /el/java/excel-import-export/save-workbook-as-csv-using-aspose-cells-for-java-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αποθήκευση βιβλίου εργασίας ως CSV χρησιμοποιώντας Aspose.Cells για Java – βήμα‑βήμα οδηγός

Αν χρειάζεστε να **αποθηκεύσετε βιβλίο εργασίας ως CSV** γρήγορα και αξιόπιστα, αυτό το σεμινάριο σας καθοδηγεί μέσα από τη διαδικασία με το Aspose.Cells για Java. Είτε δημιουργείτε μια γραμμή δεδομένων, παράγετε αναφορές για συστήματα downstream, είτε απλώς χρειάζεστε μια φορητή κειμενική αναπαράσταση ενός αρχείου Excel, θα μάθετε πώς να **εξάγετε το Excel σε CSV**, να αναγκάσετε κάθε κελί να αντιμετωπίζεται ως συμβολοσειρά, και ακόμη να εφαρμόσετε προσαρμοσμένες μετατροπές όπως η μετατροπή τιμών σε κεφαλαία.

Το παρακάτω παράδειγμα καλύπτει όλα όσα χρειάζεστε: ρύθμιση έργου, δημιουργία επιλογών εξαγωγής, μετατροπή κελιών Excel σε συμβολοσειρά και επαλήθευση του αποτελέσματος. Δεν απαιτούνται εξωτερικά σενάρια ή χειροκίνητη επεξεργασία μετά την εξαγωγή.

## Τι θα χρειαστείτε

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Java 17 (ή οποιαδήποτε συμβατή έκδοση JDK 8+)  
* Maven 3.6+ ή Gradle για διαχείριση εξαρτήσεων  
* Έγκυρη άδεια Aspose.Cells για Java (η δωρεάν αξιολόγηση λειτουργεί για δοκιμές)  
* Ένα αρχείο Excel (`input.xlsx`) που περιέχει μικτοί τύποι δεδομένων (αριθμοί, ημερομηνίες, κείμενο)  

Η ύπαρξη αυτών των προαπαιτούμενων εξασφαλίζει ότι ο κώδικας εκτελείται χωρίς προβλήματα στο class‑path.

## Βήμα 1: Ρυθμίστε το έργο Maven και προσθέστε το Aspose.Cells

Δημιουργήστε ένα νέο έργο Maven (ή ανοίξτε ένα υπάρχον) και προσθέστε την εξάρτηση Aspose.Cells στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** Αν προτιμάτε Gradle, η ισοδύναμη καταχώρηση είναι:
> ```gradle
> implementation 'com.aspose:aspose-cells:24.9'
> ```

Αφού προσθέσετε την εξάρτηση, εκτελέστε `mvn clean install` (ή `gradle build`) για να κατεβάσετε τα JAR.

## Βήμα 2: Φορτώστε το βιβλίο εργασίας που θέλετε να εξάγετε

Το πρώτο προγραμματιστικό βήμα είναι να ανοίξετε το αρχείο Excel που σκοπεύετε να μετατρέψετε. Το Aspose.Cells αφαιρεί την εξάρτηση από τη μορφή αρχείου, έτσι ο ίδιος κώδικας λειτουργεί για `.xlsx`, `.xls` και ακόμη και `.ods`.

```java
import com.aspose.cells.*;

public class ExportAsStringDemo {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing mixed data types
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Γιατί είναι σημαντικό:* Η φόρτωση του βιβλίου εργασίας σας δίνει πρόσβαση σε κάθε φύλλο, κελί και στυλ. Το αντικείμενο `Workbook` είναι το σημείο εισόδου για όλες τις επόμενες λειτουργίες εξαγωγής.

## Βήμα 3: Διαμορφώστε τις επιλογές εξαγωγής – εξαγωγή Excel σε CSV ενώ μετατρέπετε τα κελιά σε συμβολοσειρά

Το Aspose.Cells παρέχει το `ExportTableOptions` για να ελέγξετε πώς γράφονται τα δεδομένα σε CSV. Ορίζοντας το `exportAsString` αναγκάζει κάθε τιμή κελιού να εκτυπώνεται ως συμβολοσειρά, εξαλείφοντας την εξάρτηση από τοπικές ρυθμίσεις μορφοποίησης αριθμών και διατηρώντας τα αρχικά μηδενικά.

```java
        // Create export options and force all cells to be treated as strings
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);   // <-- key for "convert excel cells to string"
```

Σε αυτό το σημείο το βιβλίο εργασίας θα **εξάγει το Excel σε CSV** με κάθε τιμή να είναι σε εισαγωγικά ως συμβολοσειρά, ικανοποιώντας την απαίτηση «μετατροπή κελιών Excel σε συμβολοσειρά».

## Βήμα 4: (Προαιρετικό) Εφαρμόστε προσαρμοσμένη επεξεργασία – πώς να εξάγετε ως συμβολοσειρά με προσαρμοσμένη λογική

Μερικές φορές χρειάζεστε κάτι παραπάνω από μια απλή μετατροπή σε συμβολοσειρά. Για παράδειγμα, μπορεί να θέλετε να μετατρέψετε κάθε κελί σε κεφαλαία, να καλύψετε ευαίσθητα δεδομένα ή να προσθέσετε πρόθεμα. Το Aspose.Cells σας επιτρέπει να ενσωματώσετε μια υλοποίηση `CustomExportTableOptions`.

```java
        // Define custom processing to transform each cell value (e.g., to uppercase)
        exportOptions.setCustomExportTableOptions(new ExportTableOptions.CustomExportTableOptions() {
            @Override
            public String processCell(Cell cell) {
                // Return the cell's string value in upper case
                return cell.getStringValue().toUpperCase();
            }
        });
```

**Πώς λειτουργεί:** Η μέθοδος `processCell` λαμβάνει το αρχικό αντικείμενο `Cell`. Καλώντας `cell.getStringValue()` παίρνετε το ακατέργαστο κείμενο και μπορείτε να το επεξεργαστείτε όπως χρειάζεται. Αυτή είναι η τυπική απάντηση στο «**πώς να εξάγετε ως συμβολοσειρά**» όταν απαιτείται επίσης προσαρμοσμένη μορφοποίηση.

## Βήμα 5: Αποθηκεύστε το βιβλίο εργασίας ως CSV χρησιμοποιώντας τις διαμορφωμένες επιλογές

Τέλος, καλέστε `Workbook.save` με τρία ορίσματα: τη διαδρομή προορισμού, το enum μορφής (`SaveFormat.CSV`) και το `ExportTableOptions` που μόλις δημιουργήσατε.

```java
        // Save the workbook as a CSV file using the configured options
        workbook.save("YOUR_DIRECTORY/output.csv", SaveFormat.CSV, exportOptions);
    }
}
```

Όταν εκτελεστεί αυτή η γραμμή, το Aspose.Cells γράφει **save workbook as CSV** με κάθε κελί να εμφανίζεται ως συμβολοσειρά και να έχει μετατραπεί σε κεφαλαία. Το παραγόμενο `output.csv` μπορεί να ανοιχθεί σε οποιονδήποτε επεξεργαστή κειμένου, πρόγραμμα λογιστικών φύλλων ή να εισαχθεί σε βάση δεδομένων.

## Βήμα 6: Επαληθεύστε το παραγόμενο αρχείο CSV

Μια γρήγορη επιβεβαίωση σας βοηθά να βεβαιωθείτε ότι η εξαγωγή λειτουργεί όπως αναμενόταν:

```java
import java.nio.file.*;
import java.util.List;

public class VerifyCsv {
    public static void main(String[] args) throws Exception {
        List<String> lines = Files.readAllLines(Paths.get("YOUR_DIRECTORY/output.csv"));
        System.out.println("First 5 lines of the CSV:");
        lines.stream().limit(5).forEach(System.out::println);
    }
}
```

Θα πρέπει να δείτε όλες τις τιμές σε κεφαλαία, και τα αριθμητικά κελιά όπως `00123` να παραμένουν αμετάβλητα επειδή είχαν αναγκαστεί σε λειτουργία συμβολοσειράς. Αυτό το βήμα επαλήθευσης απαντά στο εσωτερικό ερώτημα «Διατηρεί η εξαγωγή τα αρχικά μηδενικά;».

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| Τα κελιά εμφανίζονται ως αριθμοί αντί για συμβολοσειρές | `exportAsString` δεν είχε οριστεί ή χρησιμοποιείται παλαιότερη έκδοση Aspose.Cells | Βεβαιωθείτε ότι `exportOptions.setExportAsString(true)` και χρησιμοποιήστε έκδοση 24.9+ |
| Οι χαρακτήρες Unicode εμφανίζονται αλλοιωμένοι | Η προεπιλεγμένη κωδικοποίηση CSV είναι ANSI σε ορισμένες πλατφόρμες | Περάστε ένα αντικείμενο `CsvSaveOptions` με `setEncoding(Encoding.getUTF8())` |
| Μεγάλα φύλλα εργασίας προκαλούν `OutOfMemoryError` | Όλες οι γραμμές φορτώνονται στη μνήμη πριν τη γραφή | Χρησιμοποιήστε `ExportTableOptions.setExportHiddenColumns(false)` και ρέξτε το βιβλίο εργασίας αν είναι δυνατόν |
| Η προσαρμοσμένη λογική προκαλεί `NullPointerException` | `processCell` κλήθηκε σε κενό κελί με τιμή `null` | Προστασία κατά του null: `if (cell.getStringValue() == null) return "";` |

Η αντιμετώπιση αυτών των ακραίων περιπτώσεων κάνει τη λύση σας ανθεκτική για παραγωγικά φορτία εργασίας.

## Πλήρες λειτουργικό παράδειγμα (ενιαίος αρχείο)

Ακολουθεί ένα αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε, επικολλήσετε και εκτελέσετε. Περιλαμβάνει όλες τις εισαγωγές, διαχείριση σφαλμάτων και σχόλια.

```java
import com.aspose.cells.*;
import java.nio.file.*;
import java.util.List;

/**
 * Demonstrates how to save workbook as CSV, export Excel to CSV,
 * convert Excel cells to string, and apply custom string processing.
 */
public class ExportAsStringDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2️⃣ Configure export options – force string output
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true); // convert Excel cells to string

        // 3️⃣ Optional: custom processing (e.g., upper‑case transformation)
        exportOptions.setCustomExportTableOptions(new ExportTableOptions.CustomExportTableOptions() {
            @Override
            public String processCell(Cell cell) {
                // Guard against null values
                String raw = cell.getStringValue();
                return raw != null ? raw.toUpperCase() : "";
            }
        });

        // 4️⃣ Save as CSV – this is the core "save workbook as CSV" step
        String outputPath = "YOUR_DIRECTORY/output.csv";
        workbook.save(outputPath, SaveFormat.CSV, exportOptions);
        System.out.println("Workbook saved as CSV at: " + outputPath);

        // 5️⃣ Verify the first few lines
        List<String> lines = Files.readAllLines(Paths.get(outputPath));
        System.out.println("\n--- First 5 lines of the generated CSV ---");
        lines.stream().limit(5).forEach(System.out::println);
    }
}
```

**Αναμενόμενο αποτέλεσμα** (δείγμα αποσπάσματος):

```
ID,NAME,DATE,AMOUNT
001,JOHN DOE,2024-01-15,1000
002,JANE SMITH,2024-01-16,2500
003,ALICE WONG,2024-01-17,750
```

Όλες οι τιμές των κελιών εμφανίζονται ως συμβολοσειρές κεφαλαίων, και οι αριθμητικές στήλες διατηρούν την αρχική μορφοποίηση επειδή είχαν αναγκαστεί σε λειτουργία συμβολοσειράς.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **αποθηκεύσετε βιβλίο εργασίας ως CSV** με το Aspose.Cells για Java, πώς να **εξάγετε το Excel σε CSV** διασφαλίζοντας ότι κάθε κελί αντιμετωπίζεται ως συμβολοσειρά, και πώς να υλοποιήσετε προσαρμοσμένη λογική για το σενάριο «**πώς να εξάγετε ως συμβολοσειρά**». Με τη διαμόρφωση του `ExportTableOptions` αποφεύγετε προβλήματα που σχετίζονται με τοπικές ρυθμίσεις, διατηρείτε τα αρχικά μηδενικά και αποκτάτε πλήρη έλεγχο της εξόδου CSV.

### Επόμενα βήματα

* Εξερευνήστε το `CsvSaveOptions` για να ορίσετε προσαρμοσμένους διαχωριστές, κωδικοποίηση ή κανόνες απόσπασης.  
* Συνδυάστε αυτήν την προσέγγιση

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω σεμινάρια καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να φορτώσετε και να αποθηκεύσετε το Excel ως CSV χρησιμοποιώντας Aspose.Cells για Java: Ένας ολοκληρωμένος οδηγός](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [Κοπή & Αποθήκευση αρχείων Excel ως CSV χρησιμοποιώντας Aspose.Cells σε Java](/cells/english/java/workbook-operations/excel-aspose-cells-java-trim-save-csv/)
- [Πώς να αποθηκεύσετε βιβλίο εργασίας Excel σε Java χρησιμοποιώντας Aspose.Cells](/cells/english/java/automation-batch-processing/excel-automation-java-aspose-cells-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}