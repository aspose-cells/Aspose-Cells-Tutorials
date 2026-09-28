---
category: general
date: 2026-09-27
description: Εξαγωγή φύλλου εργασίας σε CSV σε Java χρησιμοποιώντας το Aspose.Cells
  και ορισμός ακρίβειας σε 5 σημαντικά ψηφία – ένας πλήρης οδηγός βήμα‑βήμα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export worksheet to csv
- save workbook as csv
- how to set precision
- save excel as csv
- export excel to csv
language: el
lastmod: 2026-09-27
og_description: Εξαγωγή φύλλου εργασίας σε CSV σε Java με το Aspose.Cells, μάθετε
  πώς να ορίζετε την ακρίβεια και να αποθηκεύετε το βιβλίο εργασίας ως CSV σε λίγα
  μόνο βήματα.
og_image_alt: Screenshot showing Java code that exports worksheet to CSV with precision
og_title: Εξαγωγή φύλλου εργασίας σε CSV με ακρίβεια στη Java – πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Export worksheet to CSV in Java using Aspose.Cells and set precision
    to 5 significant digits – a complete step‑by‑step guide.
  headline: How to export worksheet to CSV with precision in Java
  type: TechArticle
- description: Export worksheet to CSV in Java using Aspose.Cells and set precision
    to 5 significant digits – a complete step‑by‑step guide.
  name: How to export worksheet to CSV with precision in Java
  steps:
  - name: Exporting a specific worksheet
    text: 'If your workbook has multiple sheets and you only want to export one, use
      the `Worksheet` object directly:'
  - name: Exporting without losing leading zeros
    text: 'CSV treats all fields as text, but some parsers may strip leading zeros.
      To preserve them, wrap the value in double quotes:'
  - name: Using a different delimiter
    text: 'If you prefer semicolons instead of commas (common in European locales),
      set the delimiter:'
  - name: Handling large files
    text: 'For workbooks exceeding several hundred megabytes, consider streaming the
      export:'
  - name: Next steps
    text: '* Explore additional `ExportTableOptions` properties such as `setEncoding`,
      `setQuoteAllFields`, and `setSeparator` to fine‑tune your CSV output. * Combine
      the export with Java’s `java.nio.file` APIs to automate batch processing of
      multiple Excel files. * Dive into Aspose.Cells’ **export excel to CS'
  type: HowTo
tags:
- Aspose.Cells
- Java
- CSV export
- Excel automation
title: Πώς να εξάγετε το φύλλο εργασίας σε CSV με ακρίβεια στη Java
url: /el/java/excel-import-export/how-to-export-worksheet-to-csv-with-precision-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή φύλλου εργασίας σε CSV με ακρίβεια σε Java

Αν χρειάζεστε **export worksheet to CSV** ενώ ελέγχετε τον αριθμό των σημαντικών ψηφίων, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε με το Aspose.Cells for Java. Θα μάθετε πώς να φορτώσετε ένα αρχείο Excel, να ορίσετε την επιθυμητή ακρίβεια και **save workbook as CSV** σε μερικά απλά βήματα.

Η εξαγωγή δεδομένων σε CSV είναι μια κοινή απαίτηση όταν ενσωματώνετε εκθέσεις βασισμένες σε Excel με άλλα συστήματα, και η διατήρηση της αριθμητικής ακρίβειας μπορεί να αποτρέψει σφάλματα υπολογισμών στο downstream. Στο τέλος αυτού του tutorial θα μπορείτε να **save Excel as CSV** με προσαρμοσμένη ακρίβεια, και επίσης θα δείτε πώς η ίδια προσέγγιση λειτουργεί για γενικά σενάρια **export excel to CSV**.

## Προαπαιτούμενα

* Java Development Kit (JDK) 8 ή νεότερο εγκατεστημένο.
* Maven ή Gradle για διαχείριση εξαρτήσεων (θα χρησιμοποιήσουμε Maven στο παράδειγμα).
* Άδεια Aspose.Cells for Java (η δωρεάν αξιολόγηση λειτουργεί για δοκιμές).
* Ένα δείγμα αρχείου Excel (`Numbers.xlsx`) που περιέχει τους αριθμούς που θέλετε να εξάγετε.

## Βήμα 1: Προσθήκη Aspose.Cells στο έργο σας

Προσθέστε την εξάρτηση Maven του Aspose.Cells στο `pom.xml` σας. Αυτό σας δίνει πρόσβαση στις κλάσεις `Workbook`, `ExportTableOptions` και `SaveFormat` που απαιτούνται για την εξαγωγή.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

*Γιατί αυτό το βήμα είναι σημαντικό*: Χωρίς τη βιβλιοθήκη δεν μπορείτε να χειριστείτε αρχεία Excel προγραμματιστικά. Η χρήση του Maven εξασφαλίζει ότι τα σωστά JAR θα ληφθούν και θα διατηρούνται ενημερωμένα.

## Βήμα 2: Φόρτωση του workbook που περιέχει τους αριθμούς

Δημιουργήστε μια παρουσία `Workbook` που δείχνει στο πηγαίο αρχείο Excel σας. Αυτό το βήμα προετοιμάζει το φύλλο εργασίας για εξαγωγή.

```java
import com.aspose.cells.*;

public class SignificantDigitsExport {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the numbers
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Numbers.xlsx");
```

*Επεξήγηση*: Η κλάση `Workbook` αντιπροσωπεύει ολόκληρο το αρχείο Excel. Η φόρτωσή του μία φορά σας επιτρέπει να επαναχρησιμοποιήσετε το ίδιο αντικείμενο για πολλαπλές λειτουργίες εξαγωγής, όπως **save workbook as CSV** με διαφορετικές ρυθμίσεις.

## Βήμα 3: Διαμόρφωση επιλογών εξαγωγής για ορισμό ακρίβειας

Το Aspose.Cells σας επιτρέπει να περιορίσετε τον αριθμό των σημαντικών ψηφίων μέσω του `ExportTableOptions`. Ο σωστός ορισμός του υλοποιεί την απαίτηση **how to set precision**.

```java
        // Create export options and limit the output to 5 significant digits
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setSignificantDigits(5); // keep only 5 significant digits
```

*Γιατί αυτό είναι σημαντικό*: Τα αρχεία CSV αποθηκεύουν αριθμούς ως απλό κείμενο. Εάν τα αρχικά κελιά Excel περιέχουν πολλά δεκαδικά ψηφία, το CSV μπορεί να γίνει δύσχρηστο. Καλώντας το `setSignificantDigits`, διασφαλίζετε ότι κάθε αριθμητική τιμή στρογγυλοποιείται στην καθορισμένη ακρίβεια πριν γραφτεί στο αρχείο.

## Βήμα 4: Εξαγωγή των δεδομένων του φύλλου εργασίας σε CSV χρησιμοποιώντας τις διαμορφωμένες επιλογές

Τώρα καλέστε το `Workbook.save` με το enum `SaveFormat.CSV` και περάστε το `exportOptions`. Αυτό εκτελεί την πραγματική λειτουργία **export excel to CSV**.

```java
        // Export the worksheet data to CSV using the configured options
        workbook.save("YOUR_DIRECTORY/Numbers_SigDigits.csv",
                      SaveFormat.CSV,
                      exportOptions);
    }
}
```

*Τι συμβαίνει στο παρασκήνιο*: Το Aspose.Cells διασχίζει κάθε κελί, εφαρμόζει τον κανόνα ακρίβειας και γράφει το προκύπτον κείμενο σε ροή CSV. Το αρχείο εξόδου (`Numbers_SigDigits.csv`) βρίσκεται στον ίδιο φάκελο που καθορίσατε.

## Αναμενόμενη έξοδος

Υποθέτουμε ότι το `Numbers.xlsx` περιέχει τις παρακάτω τιμές στη στήλη **A**:

| A          |
|------------|
| 123.456789 |
| 0.00123456 |
| 98765.4321 |

Αφού εκτελέσετε τον κώδικα με `setSignificantDigits(5)`, το `Numbers_SigDigits.csv` θα περιέχει:

```
123.46
0.0012346
98765
```

Παρατηρήστε πώς κάθε αριθμός στρογγυλοποιείται σε πέντε σημαντικά ψηφία, ταιριάζοντας με την ακρίβεια που ορίσατε.

## Βήμα 5: Επαλήθευση του αρχείου CSV

Ανοίξτε το παραγόμενο CSV με έναν επεξεργαστή κειμένου ή εισάγετέ το σε άλλη εφαρμογή (π.χ., μια βάση δεδομένων ή εργαλείο ανάλυσης δεδομένων) για να επιβεβαιώσετε ότι:

1. Το αρχείο είναι σωστά μορφοποιημένο (τιμές χωρισμένες με κόμμα).
2. Οι αριθμητικές τιμές τηρούν την ακρίβεια των 5 ψηφίων.
3. Δεν εμφανίζονται επιπλέον εισαγωγικά ή χαρακτήρες διαφυγής, εκτός εάν τα αρχικά δεδομένα τα απαιτούσαν.

Αν χρειάζεστε διαφορετική ακρίβεια, απλώς αλλάξτε το όρισμα που περνάτε στο `setSignificantDigits`.

## Συνηθισμένες παραλλαγές και ειδικές περιπτώσεις

### Εξαγωγή συγκεκριμένου φύλλου εργασίας

Αν το workbook σας έχει πολλαπλά φύλλα και θέλετε να εξάγετε μόνο ένα, χρησιμοποιήστε απευθείας το αντικείμενο `Worksheet`:

```java
Worksheet sheet = workbook.getWorksheets().get(0); // first sheet
sheet.getCells().exportTableOptions(exportOptions);
sheet.getCells().exportCsv("YOUR_DIRECTORY/Sheet1_SigDigits.csv", exportOptions);
```

### Εξαγωγή χωρίς απώλεια αρχικών μηδενικών

Το CSV αντιμετωπίζει όλα τα πεδία ως κείμενο, αλλά ορισμένοι αναλυτές μπορεί να αφαιρέσουν τα αρχικά μηδενικά. Για να τα διατηρήσετε, τυλίξτε την τιμή σε διπλά εισαγωγικά:

```java
exportOptions.setQuoteAllFields(true);
```

### Χρήση διαφορετικού διαχωριστικού

Αν προτιμάτε το ερωτηματικό (;) αντί για κόμμα (συνηθισμένο σε ευρωπαϊκές ρυθμίσεις), ορίστε το διαχωριστικό:

```java
exportOptions.setSeparator(';');
```

### Διαχείριση μεγάλων αρχείων

Για workbooks που υπερβαίνουν μερικές εκατοντάδες megabytes, σκεφτείτε τη ροή εξαγωγής:

```java
Workbook workbook = new Workbook("largeFile.xlsx", new LoadOptions(LoadFormat.XLSX));
workbook.save("largeFile.csv", SaveFormat.CSV, exportOptions);
```

Το Aspose.Cells επεξεργάζεται το αρχείο σε τμήματα, μειώνοντας την κατανάλωση μνήμης.

## Pro συμβουλές

* **License early** – Καταχωρίστε την άδεια Aspose.Cells πριν από τη δημιουργία του πρώτου `Workbook` για να αποφύγετε το υδατογράφημα αξιολόγησης.
* **Reuse ExportTableOptions** – Εάν χρειάζεται να εξάγετε πολλά φύλλα εργασίας με την ίδια ακρίβεια, δημιουργήστε μία παρουσία `ExportTableOptions` και επαναχρησιμοποιήστε την.
* **Validate numeric columns** – Μετά την εξαγωγή, εκτελέστε ένα γρήγορο script για να επιβεβαιώσετε ότι ο αριθμός των ψηφίων ταιριάζει με την προσδοκία σας, ειδικά όταν εργάζεστε με επιστημονική σημειογραφία.

## Συμπέρασμα

Τώρα έχετε μια πλήρη, εκτελέσιμη λύση για **export worksheet to CSV** σε Java, με πλήρη έλεγχο της αριθμητικής ακρίβειας. Φορτώνοντας το workbook, διαμορφώνοντας το `ExportTableOptions` και καλώντας το `save` με `SaveFormat.CSV`, μπορείτε να **save workbook as CSV** εφαρμόζοντας τον κανόνα **how to set precision** που χρειάζεστε. Αυτή η προσέγγιση λειτουργεί για οποιαδήποτε εργασία **save excel as CSV** και μπορεί να επεκταθεί σε άλλες απαιτήσεις μορφοποίησης CSV.

### Επόμενα βήματα

* Εξερευνήστε πρόσθετες ιδιότητες του `ExportTableOptions` όπως `setEncoding`, `setQuoteAllFields` και `setSeparator` για να βελτιώσετε την έξοδο CSV.
* Συνδυάστε την εξαγωγή με τα APIs `java.nio.file` της Java για να αυτοματοποιήσετε την επεξεργασία παρτίδας πολλαπλών αρχείων Excel.
* Εμβαθύνετε στην τεκμηρίωση του Aspose.Cells **export excel to CSV** για προχωρημένα σενάρια όπως συγκέντρωση πολλαπλών φύλλων ή διατήρηση μορφοποίησης υπό συνθήκες.

Καλό προγραμματισμό, και απολαύστε τις εξαγωγές CSV με ελεγχόμενη ακρίβεια!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Φορτώσετε και να Αποθηκεύσετε Excel ως CSV Χρησιμοποιώντας Aspose.Cells for Java: Ένας Πλήρης Οδηγός](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [Πώς να Εξάγετε CSV με Java – Ορισμός Σημαντικών Ψηφίων & Εξαγωγή Περιοχής σε CSV](/cells/english/java/excel-import-export/how-to-export-csv-with-java-set-significant-digits-export-ra/)
- [Περικοπή & Αποθήκευση Αρχείων Excel ως CSV Χρησιμοποιώντας Aspose.Cells σε Java](/cells/english/java/workbook-operations/excel-aspose-cells-java-trim-save-csv/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}