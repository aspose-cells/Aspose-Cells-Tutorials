---
category: general
date: 2026-08-20
description: Μάθετε πώς να εξάγετε το Excel σε TXT περιορίζοντας τα δεκαδικά ψηφία,
  διατηρώντας τα σημαντικά ψηφία και αποθηκεύοντας το βιβλίο εργασίας ως TXT χρησιμοποιώντας
  Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- limit decimal places
- keep significant digits
- save workbook as txt
language: el
lastmod: 2026-08-20
og_description: Εξαγωγή Excel σε TXT με το Aspose.Cells. Αυτός ο οδηγός δείχνει πώς
  να περιορίσετε τα δεκαδικά ψηφία, να διατηρήσετε τα σημαντικά ψηφία και να αποθηκεύσετε
  το βιβλίο εργασίας ως TXT σε Java.
og_image_alt: Result of export excel to txt showing limited decimal places and kept
  significant digits
og_title: Εξαγωγή Excel σε TXT σε Java – έλεγχος δεκαδικών θέσεων και σημαντικών ψηφίων
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn to export Excel to TXT while limiting decimal places, keeping
    significant digits, and saving workbook as TXT using Java.
  headline: How to export Excel to TXT with Aspose.Cells and control decimal precision
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Text export
title: Πώς να εξάγετε το Excel σε TXT με το Aspose.Cells και να ελέγχετε την ακρίβεια
  των δεκαδικών
url: /el/java/excel-import-export/how-to-export-excel-to-txt-with-aspose-cells-and-control-dec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εξάγετε το Excel σε TXT με το Aspose.Cells και να ελέγξετε την ακρίβεια των δεκαδικών

Αν χρειάζεστε να **εξάγετε το Excel σε TXT** και να διασφαλίσετε ότι η έξοδος σέβεται έναν συγκεκριμένο αριθμό δεκαδικών θέσεων, αυτός ο οδηγός παρέχει μια πλήρη λύση. Θα δείτε πώς να περιορίσετε τις δεκαδικές θέσεις, να διατηρήσετε τα σημαντικά ψηφία και να **αποθηκεύσετε το βιβλίο εργασίας ως TXT** χρησιμοποιώντας τη βιβλιοθήκη Aspose.Cells για Java.

Ο οδηγός περνάει από τη δημιουργία ενός βιβλίου εργασίας, την εισαγωγή μιας τιμής υψηλής ακρίβειας, τη διαμόρφωση των επιλογών αποθήκευσης TXT και τη γραφή του αρχείου στο δίσκο. Στο τέλος θα μπορείτε να δημιουργήσετε ένα αρχείο κειμένου που περιέχει ακριβώς την ακρίβεια που απαιτείτε, χωρίς χειροκίνητη επεξεργασία.

## Τι θα χρειαστείτε

- Java 17 (ή οποιοδήποτε υποστηριζόμενο JDK)
- Aspose.Cells for Java 23.10 ή νεότερο
- Ένα IDE ή εργαλείο κατασκευής (Maven/Gradle) για διαχείριση εξαρτήσεων
- Δικαιώματα εγγραφής στον φάκελο εξόδου

## Βήμα 1: Δημιουργία βιβλίου εργασίας και πρόσβαση στο πρώτο φύλλο εργασίας

Η δημιουργία ενός βιβλίου εργασίας είναι το πρώτο βήμα όταν θέλετε να **εξάγετε το Excel σε TXT**. Η κλάση `Workbook` αντιπροσωπεύει ολόκληρο το αρχείο Excel, και η `Worksheet` σας δίνει πρόσβαση στα κελιά.

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
```

*Γιατί είναι σημαντικό*: Το αντικείμενο workbook περιέχει όλα τα δεδομένα, τα στυλ και τα μεταδεδομένα. Ξεκινώντας με ένα νέο βιβλίο εργασίας εξασφαλίζει ότι καμία κρυφή μορφοποίηση δεν επηρεάζει την εξαγωγή κειμένου.

## Βήμα 2: Προσθήκη αριθμητικής τιμής και περιορισμός δεκαδικών θέσεων

Εισάγετε έναν αριθμό με πολλές δεκαδικές θέσεις ώστε να μπορείτε να δείξετε πώς να **περιορίσετε τις δεκαδικές θέσεις** κατά την εξαγωγή.

```java
        // Put a high‑precision number into cell A1
        sheet.getCells().putValue("A1", 0.000123456789);
```

*Γιατί είναι σημαντικό*: Το Excel αποθηκεύει την πλήρη ακρίβεια, αλλά όταν εξάγετε αργότερα, μπορεί να θέλετε να περικόψετε ή να στρογγυλοποιήσετε την τιμή. Η ρύθμιση `limit decimal places` θα το διαχειριστεί αυτόματα.

## Βήμα 3: Διαμόρφωση επιλογών αποθήκευσης TXT για διατήρηση σημαντικών ψηφίων

Το Aspose.Cells παρέχει `TxtSaveOptions`. Ορίζοντας το `significantDigits` λέει στον εξαγωγέα να διατηρήσει μόνο τον απαιτούμενο αριθμό σημαντικών ψηφίων, αγνοώντας τα αρχικά μηδενικά.

```java
        // Configure TXT export options
        TxtSaveOptions txtOptions = new TxtSaveOptions();

        // Keep exactly 5 significant digits (e.g., 0.00012346)
        txtOptions.setSignificantDigits(5);
```

*Γιατί είναι σημαντικό*: Η επιλογή **keep significant digits** διασφαλίζει ότι το αρχείο εξόδου περιέχει μια προβλέψιμη ποσότητα ακρίβειας, κάτι που είναι απαραίτητο για συστήματα downstream που αναμένουν μορφή αριθμού σταθερού πλάτους.

## Βήμα 4: Αποθήκευση του βιβλίου εργασίας ως TXT

Τέλος, γράψτε το βιβλίο εργασίας σε ένα αρχείο κειμένου. Η μέθοδος `save` σέβεται τις επιλογές που διαμορφώσατε, έτσι το παραγόμενο αρχείο θα περιέχει την περιορισμένη δεκαδική αναπαράσταση.

```java
        // Define the output path (replace with your own directory)
        String outputPath = "output/SignificantDigits.txt";

        // Export the workbook to TXT using the configured options
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

*Γιατί είναι σημαντικό*: Η χρήση του **save workbook as txt** με τις προετοιμασμένες `TxtSaveOptions` εγγυάται ότι το εξαγόμενο αρχείο ταιριάζει με τους περιορισμούς ακρίβειας που ορίσατε στο προηγούμενο βήμα.

### Αναμενόμενο περιεχόμενο του `SignificantDigits.txt`

```
0.00012346
```

Η τιμή δείχνει πέντε σημαντικά ψηφία (`12346`) μετά τη στρογγυλοποίηση, και τα αρχικά μηδενικά διατηρούνται σύμφωνα με τη μορφή TXT.

## Παραλλαγές και ειδικές περιπτώσεις

| Σενάριο | Προσαρμογή |
|----------|------------|
| **Διαφορετικός αριθμός σημαντικών ψηφίων** | Κλήση `txtOptions.setSignificantDigits(n)` όπου `n` είναι 1‑15. |
| **Εξαγωγή περιοχής αντί ολόκληρου φύλλου** | Χρήση `txtOptions.setExportRange("A1:B10")` πριν την αποθήκευση. |
| **Διατήρηση διαχωριστών στηλών** | Ορισμός `txtOptions.setSeparator('\t')` για έξοδο με διαχωριστικό tab. |
| **Μεγάλα φύλλα εργασίας** | Αύξηση `txtOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCES)` για αποφυγή `OutOfMemoryError`. |

## Συνηθισμένα λάθη και επαγγελματικές συμβουλές

- **Μην συγχέετε τα σημαντικά ψηφία με τις δεκαδικές θέσεις**. Τα αρχικά μηδενικά δεν μετρώνται ως σημαντικά· χρησιμοποιήστε `setSignificantDigits` για ουσιαστική ακρίβεια και `setDecimalPlaces` αν χρειάζεστε σταθερό αριθμό ψηφίων μετά την υποδιαστολή.
- **Πάντα να καθορίζετε απόλυτη διαδρομή εξόδου** όταν εκτελείτε από IDE για να αποφύγετε σφάλματα δικαιωμάτων.
- **Επικυρώστε το παραγόμενο αρχείο** με μια απλή κλήση `java.nio.file.Files.readAllLines(Paths.get(outputPath))` για να διασφαλίσετε ότι το περιεχόμενο ταιριάζει με τις προσδοκίες πριν το δώσετε σε downstream διαδικασίες.

## Πλήρης κώδικας πηγής για αναφορά

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 2: Insert a high‑precision number (will be limited later)
        sheet.getCells().putValue("A1", 0.000123456789);

        // Step 3: Set TXT options – keep 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(5);   // keep significant digits

        // Step 4: Save the workbook as TXT
        String outputPath = "output/SignificantDigits.txt";
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

Η εκτέλεση του προγράμματος παράγει το `SignificantDigits.txt` που περιέχει τη μοναδική γραμμή `0.00012346`, δείχνοντας ότι η διαδικασία **export excel to txt** σέβεται τόσο τις απαιτήσεις **limit decimal places** όσο και **keep significant digits**.

## Συμπέρασμα

Τώρα ξέρετε πώς να **εξάγετε το Excel σε TXT** χρησιμοποιώντας το Aspose.Cells για Java ενώ ελέγχετε την ακρίβεια των αριθμών. Διαμορφώνοντας το `TxtSaveOptions` μπορείτε να **περιορίσετε τις δεκαδικές θέσεις**, να **διατηρήσετε τα σημαντικά ψηφία**, και αξιόπιστα να **αποθηκεύσετε το βιβλίο εργασίας ως txt** χωρίς πρόσθετη επεξεργασία.

Επόμενα, μπορείτε να εξερευνήσετε:

- Εξαγωγή πολλαπλών φύλλων σε ξεχωριστά αρχεία TXT (`save workbook as txt` ανά φύλλο)
- Χρήση του `setSeparator` για δημιουργία εξόδου συμβατής με CSV
- Αυτοματοποίηση μαζικών μετατροπών για μεγάλα σύνολα δεδομένων

Μη διστάσετε να πειραματιστείτε με διαφορετικούς αριθμούς ψηφίων και διαχωριστές ώστε να ταιριάζουν στις ακριβείς ανάγκες του έργου σας. Καλό προγραμματισμό!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε σε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να δημιουργήσετε και να εξάγετε το Excel σε HTML χρησιμοποιώντας το Aspose.Cells Java | Οδηγός λειτουργιών βιβλίου εργασίας](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Αποθήκευση Excel ως κείμενο – Πλήρης οδηγός C# για εξαγωγή Excel σε TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Εξαγωγή βιβλίου εργασίας Excel ως εικόνα χρησιμοποιώντας το Aspose.Cells for Java&#58; Οδηγός βήμα‑βήμα](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}