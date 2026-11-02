---
category: general
date: 2026-07-16
description: Ορίστε προσαρμοσμένο διαχωριστικό κελιών κατά την εξαγωγή πίνακα Excel
  σε TXT χρησιμοποιώντας το Aspose.Cells. Μάθετε πώς να εξάγετε τύπους Excel σε κείμενο
  και να αποθηκεύσετε το φύλλο εργασίας ως αρχείο txt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom cell separator
- export excel table to txt
- export excel formulas to text
- save worksheet as txt file
- export excel data as plain text
language: el
lastmod: 2026-07-16
og_description: Ο καθορισμός προσαρμοσμένου διαχωριστή κελιών στο Aspose.Cells σας
  επιτρέπει να εξάγετε πίνακα Excel σε TXT με ακριβή μορφοποίηση. Εξάγετε τύπους Excel
  σε κείμενο και αποθηκεύστε το φύλλο εργασίας ως αρχείο txt εύκολα.
og_image_alt: Screenshot showing set custom cell separator option in Aspose.Cells
  export settings
og_title: Ορισμός προσαρμοσμένου διαχωριστή κελιών – Εξαγωγή πίνακα Excel σε TXT
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Set custom cell separator when exporting Excel table to TXT using Aspose.Cells.
    Learn how to export Excel formulas to text and save worksheet as txt file.
  headline: Set Custom Cell Separator – Export Excel Table to TXT
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Export
title: Ορισμός προσαρμοσμένου διαχωριστή κελιών – Εξαγωγή πίνακα Excel σε TXT
url: /el/java/excel-import-export/set-custom-cell-separator-export-excel-table-to-txt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ορισμός Προσαρμοσμένου Διαχωριστικού Κελιών – Εξαγωγή Πίνακα Excel σε TXT

Ο ορισμός προσαρμοσμένου διαχωριστικού κελιών είναι η μυστική σάλτσα που χρειάζεστε όταν θέλετε μια τακτοποιημένη εξαγωγή κειμένου από ένα φύλλο Excel. Αναρωτηθήκατε ποτέ πώς να **export excel table to txt** χωρίς να καταλήξετε σε ένα μπερδεμένο μίγμα από κόμματα και αλλαγές γραμμής; Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία χρησιμοποιώντας το Aspose.Cells for Java, από τη φόρτωση ενός βιβλίου εργασίας μέχρι το **save worksheet as txt file** με έναν διαχωριστή της επιλογής σας.

## Τι Θα Μάθετε

- Πώς να **set custom cell separator** για εξαγωγές κειμένου.  
- Τα ακριβή βήματα για **export excel formulas to text** ώστε οι υπολογισμένες τιμές να μεταφερθούν μαζί σας.  
- Τρόπους για **export excel data as plain text** διατηρώντας τη διάταξη.  
- Ένα πλήρες, έτοιμο‑για‑εκτέλεση δείγμα κώδικα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο έργο σας.

Στο τέλος αυτού του οδηγού θα μπορείτε να πάρετε οποιοδήποτε βιβλίο εργασίας Excel, να επιλέξετε ένα pipe (`|`), ένα tab (`\t`) ή οποιονδήποτε χαρακτήρα θέλετε, και να δημιουργήσετε ένα καθαρό, διαχωρισμένο αρχείο κειμένου που αγαπούν τα downstream συστήματα.

### Προαπαιτούμενα

- Java 8 ή νεότερη εγκατεστημένη.  
- Maven (ή οποιοδήποτε εργαλείο κατασκευής) για να κατεβάσετε τη βιβλιοθήκη Aspose.Cells for Java.  
- Ένα δείγμα βιβλίου εργασίας (`TableDemo.xlsx`) που περιέχει έναν πίνακα με τύπους.

Αν έχετε όλα αυτά, ας ξεκινήσουμε — χωρίς περιττές εξηγήσεις, μόνο πρακτικά βήματα.

## Βήμα 1: Προσθήκη Aspose.Cells στο Έργο Σας

Πριν μπορέσετε να **set custom cell separator**, χρειάζεστε το JAR του Aspose.Cells στο classpath. Ο πιο εύκολος τρόπος είναι μέσω Maven:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

Αν προτιμάτε Gradle, αντικαταστήστε το XML με το ισοδύναμο `implementation 'com.aspose:aspose-cells:24.10'`. Μόλις η εξάρτηση λυθεί, είστε έτοιμοι να γράψετε κώδικα Java που αλληλεπιδρά με αρχεία Excel.

## Βήμα 2: Φόρτωση του Workbook – Προετοιμασία για Export Excel Table to TXT

Η πρώτη πραγματική γραμμή κώδικα είναι πάντα η ίδια: ανοίξτε το workbook που περιέχει τον πίνακα που θέλετε να εξάγετε.

```java
import com.aspose.cells.*;

public class ExportTableWithOptions {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableDemo.xlsx");
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Εδώ παίρνουμε το πρώτο φύλλο εργασίας (`get(0)`). Αν τα δεδομένα σας βρίσκονται σε διαφορετικό φύλλο, απλώς αλλάξτε το δείκτη ή χρησιμοποιήστε `get("SheetName")`. Αυτό το τμήμα είναι ουσιώδες για **export excel table to txt** επειδή ο εξαγωγέας λειτουργεί σε επίπεδο φύλλου εργασίας.

## Βήμα 3: Set Custom Cell Separator – Η Καρδιά της Εξαγωγής

Τώρα έρχεται το αστέρι της παράστασης: η διαμόρφωση του `ExportTableOptions`. Αυτό το αντικείμενο σας επιτρέπει να αποφασίσετε ακριβώς πώς θα εμφανίζεται κάθε κελί στο τελικό αρχείο κειμένου.

```java
        // Define how the table should be exported
        ExportTableOptions exportTableOptions = new ExportTableOptions();

        // 1️⃣ Export cell contents as plain strings (no rich formatting)
        exportTableOptions.setExportAsString(true);

        // 2️⃣ Include the evaluated formula result, not the formula itself
        exportTableOptions.setFormulaValueInCell(true);

        // 3️⃣ Set the custom separator – this is where we set custom cell separator
        exportTableOptions.setCellValueSeparator("|"); // you can use any char you like
```

Γιατί **set custom cell separator**; Επειδή ο προεπιλεγμένος διαχωριστής είναι ένα tab, το οποίο μπορεί να συγκρούεται με δεδομένα που ήδη περιέχουν tabs. Επιλέγοντας ένα pipe (`|`) ή ένα ερωτηματικό, εξασφαλίζετε ότι κάθε στήλη παραμένει διακριτή όταν ένας downstream parser διαβάσει το αρχείο.

### Export Excel Formulas to Text

Η γραμμή `setFormulaValueInCell(true)` λέει στο Aspose.Cells να γράψει το **export excel formulas to text** ως το *αποτέλεσμα* του τύπου, όχι ως τη συμβολοσειρά του τύπου. Αν το παραλείψετε, ένα κελί που περιέχει `=SUM(A1:A5)` θα εμφανιστεί ως `=SUM(A1:A5)` στο TXT, κάτι που σπάνια θέλετε.

## Βήμα 4: Σύνδεση Export Options με TXT Save Options

Τώρα συνδέουμε αυτές τις επιλογές πίνακα με τη γενική διαμόρφωση εξαγωγής TXT.

```java
        // Attach the table export options to TXT save options
        TxtSaveOptions txtSaveOptions = new TxtSaveOptions();
        txtSaveOptions.setExportTableOptions(exportTableOptions);
```

Το `TxtSaveOptions` είναι το αντικείμενο που ελέγχει πώς θα γραφτεί ολόκληρο το φύλλο εργασίας. Ενσωματώνοντας το `exportTableOptions` σε αυτό, διασφαλίζετε ότι κάθε πίνακας στο φύλλο ακολουθεί τον κανόνα **set custom cell separator**.

## Βήμα 5: Αποθήκευση του Φύλλου Εργασίας ως Αρχείο TXT – Ολοκλήρωση της Εξαγωγής

Τέλος, γράφουμε το αρχείο στο δίσκο.

```java
        // Save the worksheet as a TXT file using the configured options
        workbook.save("YOUR_DIRECTORY/TableExported.txt", txtSaveOptions);
    }
}
```

Η εκτέλεση αυτού του προγράμματος δημιουργεί το `TableExported.txt`. Κάθε σειρά του αρχικού πίνακα Excel θα εμφανίζεται τώρα ως μια γραμμή τιμών χωρισμένων με pipe, π.χ.:

```
Name|Quantity|Price|Total
Apple|10|0.50|5.00
Banana|5|0.30|1.50
```

Παρατηρήστε πώς ο τύπος στη στήλη **Total** αξιολογήθηκε πριν γραφτεί — χάρη στο `setFormulaValueInCell(true)`. Αυτή είναι η ουσία του **export excel data as plain text** διατηρώντας τα υπολογισμένα αποτελέσματα.

## Βήμα 6: Επαλήθευση του Αποτελέσματος – Είναι Όλα Σωστά;

Ανοίξτε το παραγόμενο `TableExported.txt` σε οποιονδήποτε επεξεργαστή κειμένου. Θα πρέπει να δείτε:

- Μία γραμμή ανά σειρά του Excel.  
- Στήλες χωρισμένες με τον χαρακτήρα pipe που ορίσατε με `setCellValueSeparator`.  
- Καμία τυχαία κόμματα ή tabs εκτός αν ήταν μέρος των αρχικών τιμών κελιών.  
- Αποτελέσματα τύπων, όχι τους ίδιους τους τύπους.

Αν εντοπίσετε ανεπιθύμητους χαρακτήρες, ελέγξτε ξανά τον διαχωριστή που επιλέξατε. Κάποιοι χαρακτήρες (όπως το pipe) είναι ασφαλείς για τους περισσότερους parsers τύπου CSV, αλλά αν τα δεδομένα σας περιέχουν ήδη pipes, σκεφτείτε έναν διαφορετικό διαχωριστή όπως `~` ή ένα tab (`\t`).

## Συμβουλές, Edge Cases και Best Practices – Export Excel Data as Plain Text

| Situation | What to Do |
|-----------|------------|
| **Data already contains your chosen separator** | Switch to a less common character (`^`, `~`, or Unicode non‑printing chars). |
| **You need UTF‑8 encoding** | Ensure `TxtSaveOptions` has `setEncoding(Encoding.getUTF8())` set. |
| **Large worksheets** | Process in chunks or use streaming to avoid high memory usage. |
| **Preserve cell formatting** | Use `setPreserveCellFormatting(true)` if you need visual cues in the text. |

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step‑by‑step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Save Excel as Text File with Custom Separator using Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Save Excel Text Custom Separator Aspose Cells Net](/cells/german/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Save Excel Text Custom Separator Aspose Cells Net](/cells/french/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}