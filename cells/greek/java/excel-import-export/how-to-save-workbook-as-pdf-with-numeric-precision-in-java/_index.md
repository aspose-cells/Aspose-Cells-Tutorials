---
category: general
date: 2026-10-16
description: Μάθετε πώς να αποθηκεύετε το βιβλίο εργασίας ως PDF και να εξάγετε το
  Excel σε PDF, ορίζοντας τα σημαντικά ψηφία για την ακρίβεια των αριθμών.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save workbook as pdf
- export excel to pdf
- convert xlsx to pdf
- set significant digits
- set numeric precision
language: el
lastmod: 2026-10-16
og_description: Αποθηκεύστε το βιβλίο εργασίας ως PDF και εξάγετε το Excel σε PDF
  με ακριβή αριθμητική μορφοποίηση. Αυτός ο οδηγός δείχνει πώς να ορίσετε σημαντικά
  ψηφία και αριθμητική ακρίβεια.
og_image_alt: Screenshot of Java code that saves workbook as PDF with numeric precision
og_title: Αποθήκευση βιβλίου εργασίας ως PDF σε Java – έλεγχος αριθμητικής ακρίβειας
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: Learn how to save workbook as PDF and export Excel to PDF while setting
    significant digits for numeric precision.
  headline: How to save workbook as PDF with numeric precision in Java
  type: TechArticle
tags:
- Java
- Aspose.Cells
- PDF conversion
title: Πώς να αποθηκεύσετε ένα βιβλίο εργασίας ως PDF με αριθμητική ακρίβεια στη Java
url: /el/java/excel-import-export/how-to-save-workbook-as-pdf-with-numeric-precision-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αποθηκεύσετε το βιβλίο εργασίας ως PDF με αριθμητική ακρίβεια σε Java

Αν χρειάζεται να **αποθηκεύσετε το βιβλίο εργασίας ως PDF** διατηρώντας την ακριβή αριθμητική μορφή, αυτός ο οδηγός σας δείχνει ακριβώς πώς. Θα μάθετε να **εξάγετε το Excel σε PDF**, να ελέγχετε τον αριθμό των σημαντικών ψηφίων και να διασφαλίζετε ότι το παραγόμενο PDF ταιριάζει με την ακρίβεια του φύλλου σας.

Το tutorial καλύπτει όλα, από την προσθήκη της απαιτούμενης βιβλιοθήκης μέχρι την εκτέλεση ενός πλήρους, εκτελέσιμου προγράμματος. Στο τέλος, θα μπορείτε να **μετατρέψετε xlsx σε PDF** με σιγουριά και ακριβή ρύθμιση αριθμητικής ακρίβειας.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Java 17 ή νεότερη εγκατεστημένη  
* Maven 3.8+ (ή άλλο εργαλείο κατασκευής που προτιμάτε)  
* Άδεια Aspose.Cells for Java (η δωρεάν δοκιμή λειτουργεί για δοκιμές)  
* Ένα δείγμα αρχείου `input.xlsx` τοποθετημένο σε γνωστό φάκελο  

Αυτά είναι τα μόνα εξωτερικά απαιτούμενα στοιχεία· ο κώδικας εκτελείται σε οποιαδήποτε πλατφόρμα που υποστηρίζει Java.

## Βήμα 1: Προσθήκη Aspose.Cells στο έργο σας

Η βιβλιοθήκη παρέχει τις κλάσεις `Workbook` και `PdfSaveOptions` που χρησιμοποιούνται για τη μετατροπή.

**Maven εξάρτηση**

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

Αν προτιμάτε Gradle, η αντίστοιχη καταχώρηση είναι:

```groovy
implementation 'com.aspose:aspose-cells:24.9'
```

Η προσθήκη της εξάρτησης καθιστά διαθέσιμα τα API **save workbook as pdf** κατά τη φάση μεταγλώττισης.

## Βήμα 2: Φόρτωση του βιβλίου εργασίας που θέλετε να μετατρέψετε

Πρέπει πρώτα να φορτώσετε το αρχείο Excel (`.xlsx`) σε ένα αντικείμενο `Workbook`. Αυτό το βήμα είναι η βάση για οποιαδήποτε λειτουργία **export excel to pdf**.

```java
import com.aspose.cells.Workbook;

public class ExcelToPdf {
    public static void main(String[] args) throws Exception {
        // Adjust the path to your actual file location
        String inputPath = "YOUR_DIRECTORY/input.xlsx";

        // Step 2: Load the workbook you want to export
        Workbook workbook = new Workbook(inputPath);
```

Η κλάση `Workbook` διαβάζει όλα τα φύλλα, τους τύπους και τη μορφοποίηση, εξασφαλίζοντας ότι το PDF αντικατοπτρίζει το αρχικό φύλλο εργασίας.

## Βήμα 3: Διαμόρφωση επιλογών αποθήκευσης PDF – ορισμός σημαντικών ψηφίων

Ο έλεγχος της αριθμητικής ακρίβειας είναι κρίσιμος όταν εμπλέκονται οικονομικά ή επιστημονικά δεδομένα. Το αντικείμενο `PdfSaveOptions` σας επιτρέπει να καθορίσετε πόσα **σημαντικά ψηφία** θα διατηρηθούν.

```java
import com.aspose.cells.PdfSaveOptions;

        // Step 3: Create PDF save options and set numeric precision
        PdfSaveOptions pdfOptions = new PdfSaveOptions();

        // setSignificantDigits defines how many digits are retained for numeric values
        pdfOptions.setSignificantDigits(5); // keeps 5 significant digits

        // Alternatively, you can use setPrecision if you prefer fixed decimal places
        // pdfOptions.setPrecision(4); // sets 4 decimal places
```

Τanto `setSignificantDigits` όσο και `setPrecision` είναι τρόποι **set numeric precision**· το πρώτο λειτουργεί με επιστημονική σημειογραφία, ενώ το δεύτερο επιβάλλει σταθερό αριθμό δεκαδικών θέσεων. Επιλέξτε τη μέθοδο που ταιριάζει στις απαιτήσεις της αναφοράς σας.

## Βήμα 4: Αποθήκευση του φύλλου ως PDF – export Excel to PDF

Τώρα μπορείτε τελικά να **αποθηκεύσετε το βιβλίο εργασίας ως PDF** χρησιμοποιώντας τις ρυθμισμένες επιλογές. Η μέθοδος `save` δέχεται τη διαδρομή εξόδου και το στιγμιότυπο `PdfSaveOptions`.

```java
        // Step 4: Save the worksheet as a PDF using the configured options
        String outputPath = "YOUR_DIRECTORY/Result.pdf";
        workbook.save(outputPath, pdfOptions);

        System.out.println("PDF generated successfully at: " + outputPath);
    }
}
```

Η εκτέλεση αυτού του προγράμματος παράγει ένα PDF που αντικατοπτρίζει τη διάταξη του αρχικού Excel ενώ σέβεται τα **set significant digits** που ορίσατε.

## Βήμα 5: Επαλήθευση του αποτελέσματος – convert xlsx to PDF σωστά

Ανοίξτε το `Result.pdf` με οποιονδήποτε προβολέα PDF και ελέγξτε:

* Τα αριθμητικά κελιά εμφανίζουν τον αναμενόμενο αριθμό ψηφίων (π.χ., `123.45678` → `123.46` αν ορίσατε 5 σημαντικά ψηφία).  
* Οι τύποι έχουν υπολογιστεί και εμφανίζονται ως στατικές τιμές.  
* Η διάταξη, τα χρώματα και τα περιγράμματα ταιριάζουν με το πηγαίο βιβλίο εργασίας.

Αν η ακρίβεια φαίνεται λανθασμένη, επιστρέψτε στο **Βήμα 3** και προσαρμόστε το `setSignificantDigits` ή το `setPrecision` ανάλογα.

## Συνηθισμένα προβλήματα και επαγγελματικές συμβουλές

| Πρόβλημα | Γιατί συμβαίνει | Πώς να το αποφύγετε |
|----------|----------------|----------------------|
| Τα νούμερα εμφανίζονται στρογγυλοποιημένα λανθασμένα | Η χρήση `setSignificantDigits` σε κελιά με προσαρμοσμένη μορφή αριθμού μπορεί να συγκρούεται | Βεβαιωθείτε ότι η μορφή του κελιού είναι “General” ή ταιριάζει με την επιθυμητή σημασία ψηφίων |
| Λείπει ένα φύλλο στο PDF | Το βιβλίο εργασίας περιέχει κρυμμένα φύλλα που δεν εξάγονται από προεπιλογή | Καλέστε `pdfOptions.setOnePagePerSheet(true)` αν χρειάζεστε κάθε φύλλο σε ξεχωριστή σελίδα |
| Προειδοποίηση άδειας στην έξοδο | Η δοκιμαστική έκδοση χωρίς άδεια προσθέτει υδατογράφημα | Εφαρμόστε την άδεια Aspose.Cells πριν δημιουργήσετε το `Workbook` (`License license = new License(); license.setLicense("Aspose.Cells.lic");`) |

## Συμπέρασμα

Τώρα ξέρετε πώς να **αποθηκεύσετε το βιβλίο εργασίας ως PDF** ελέγχοντας με ακρίβεια την αριθμητική έξοδο. Η πλήρης λύση δείχνει πώς να φορτώσετε ένα αρχείο XLSX, να ρυθμίσετε **set significant digits** και να εκτελέσετε την **export excel to pdf** λειτουργία σε Java. Χρησιμοποιήστε το ίδιο μοτίβο για **convert xlsx to pdf** σε επεξεργασία παρτίδας, υπηρεσίες web ή επιτραπέζιες εφαρμογές.

Έτοιμοι για περισσότερα; Δοκιμάστε να προσθέσετε κεφαλίδες/υποσέλιδα, να ενσωματώσετε εικόνες ή να προστατεύσετε το PDF με κωδικό πρόσβασης—κάθε δυνατότητα είναι προσβάσιμη μέσω `PdfSaveOptions`. Καλό κώδικα!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Export PDF from Excel – Complete Guide to Save Workbook as PDF](/cells/english/net/conversion-to-pdf/how-to-export-pdf-from-excel-complete-guide-to-save-workbook/)
- [How to Set PDF Options in C# – Export Excel to PDF with Full Control](/cells/english/net/conversion-to-pdf/how-to-set-pdf-options-in-c-export-excel-to-pdf-with-full-co/)
- [Save Workbook as PDF in C# – Export Excel to PDF/A‑3b](/cells/english/net/conversion-to-pdf/save-workbook-as-pdf-in-c-export-excel-to-pdf-a-3b/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}