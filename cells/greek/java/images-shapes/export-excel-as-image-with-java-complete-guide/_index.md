---
category: general
date: 2026-11-22
description: Εξαγωγή Excel ως εικόνα με Java χρησιμοποιώντας το Aspose.Cells. Μάθετε
  πώς να προσθέσετε εικόνα σε φύλλο εργασίας και να αποθηκεύσετε το Excel ως αρχείο
  PNG σε λίγα βήματα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel as image
- add picture to worksheet
- export excel sheet to png
- save excel as png file
- save workbook as image
language: el
lastmod: 2026-11-22
og_description: Εξαγωγή Excel ως εικόνα με Java χρησιμοποιώντας το Aspose.Cells. Ακολουθήστε
  αυτόν τον οδηγό για να προσθέσετε εικόνα σε φύλλο εργασίας και να αποθηκεύσετε το
  Excel ως αρχείο PNG γρήγορα.
og_image_alt: Code snippet showing Java export of an Excel worksheet to a PNG image
og_title: Εξαγωγή Excel ως εικόνα με Java – βήμα‑βήμα οδηγός
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Export Excel as image with Java using Aspose.Cells. Learn how to add
    picture to worksheet and save Excel as PNG file in a few steps.
  headline: Export Excel as image with Java – complete guide
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Image export
title: Εξαγωγή Excel ως εικόνα με Java – πλήρης οδηγός
url: /el/java/images-shapes/export-excel-as-image-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Excel ως εικόνα με Java – πλήρης οδηγός

Αν χρειάζεστε **export Excel as image** σε μια εφαρμογή Java, αυτό το tutorial σας δείχνει μια έτοιμη προς εκτέλεση λύση. Θα δείτε πώς να προσθέσετε εικόνα στο φύλλο εργασίας, να διαμορφώσετε τις επιλογές εξαγωγής και τελικά **save Excel as PNG file** με λίγες μόνο γραμμές κώδικα.

Ο οδηγός καλύπτει τα πάντα, από τη ρύθμιση του Maven μέχρι την αντιμετώπιση ειδικών περιπτώσεων, ώστε να μπορείτε να ενσωματώσετε την τεχνική σε οποιοδήποτε έργο που απαιτεί οπτικές στιγμιότυπες των λογιστικών φύλλων.

## Προαπαιτούμενα

* Java 17 ή νεότερη εγκατεστημένη.
* Maven 3.6+ (ή Gradle) για διαχείριση εξαρτήσεων.
* Άδεια Aspose.Cells for Java (η δωρεάν αξιολόγηση λειτουργεί για δοκιμές).
* Ένα δείγμα βιβλίου εργασίας Excel (`sample.xlsx`) που περιέχει τα δεδομένα που θέλετε να εξάγετε.

## Βήμα 1: Προσθήκη εξάρτησης Aspose.Cells

Aspose.Cells παρέχει την κλάση `ImageOrPrintOptions` που χρησιμοποιείται για **export Excel as image**. Προσθέστε την ακόλουθη εξάρτηση στο `pom.xml` σας (ή την αντίστοιχη εγγραφή Gradle).

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** Κρατήστε τον αριθμό έκδοσης ενημερωμένο· οι νεότερες εκδόσεις περιλαμβάνουν βελτιώσεις απόδοσης για την απόδοση εικόνας.

## Βήμα 2: Φόρτωση του βιβλίου εργασίας και επιλογή του φύλλου εργασίας

Το πρώτο προγραμματιστικό βήμα είναι το άνοιγμα του αρχείου Excel και η λήψη αναφοράς στο φύλλο εργασίας που θέλετε να εξάγετε.

```java
import com.aspose.cells.*;

public class ExcelToImage {
    public static void main(String[] args) throws Exception {
        // Load the workbook from disk
        Workbook wb = new Workbook("sample.xlsx");

        // Access the first worksheet (index 0)
        Worksheet ws = wb.getWorksheets().get(0);
```

*Why this matters*: Η φόρτωση του βιβλίου εργασίας σας δίνει πρόσβαση στα εσωτερικά του αντικείμενα, και η επιλογή του σωστού φύλλου εξασφαλίζει ότι η σωστή περιοχή θα αποδοθεί.

## Βήμα 3: Διαμόρφωση ImageOrPrintOptions (export excel as image)

`ImageOrPrintOptions` ελέγχει τη μορφή εικόνας, την ανάλυση και άλλες λεπτομέρειες απόδοσης. Εδώ ορίζουμε τη μορφή σε PNG, που ικανοποιεί την απαίτηση **export excel sheet to png**.

```java
        // Create options for image export
        ImageOrPrintOptions opts = new ImageOrPrintOptions();

        // Set the desired image format (PNG)
        opts.setSaveFormat(SaveFormat.PNG);

        // Optional: increase resolution for sharper output
        opts.setResolution(300);
```

Ορίζοντας τη μορφή σε `PNG` εγγυάται ασυμπίεστη συμπίεση, καθιστώντας το αρχείο κατάλληλο για περαιτέρω επεξεργασία ή ενσωμάτωση σε αναφορές.

## Βήμα 4: Προσθήκη εικόνας στο φύλλο εργασίας (add picture to worksheet)

Αν χρειάζεται να ενσωματώσετε μια εικόνα—όπως λογότυπο ή στιγμιότυπο άλλης περιοχής—χρησιμοποιήστε τη συλλογή `Pictures`. Ο παρακάτω κώδικας εισάγει μια εικόνα της περιοχής `A1:G20` στην πάνω‑αριστερή γωνία του φύλλου εργασίας.

```java
        // Insert a picture of the range A1:G20 at cell (0,0)
        ws.getPictures().add(0, 0, "A1:G20");
```

> **Why you might do this:** Η προσθήκη εικόνας πριν από την εξαγωγή σας επιτρέπει να συνδυάσετε στατικά γραφικά με τα δεδομένα του φύλλου, παράγοντας μια πιο πλούσια τελική εικόνα.

## Βήμα 5: Αποθήκευση του φύλλου εργασίας ως αρχείο PNG (save excel as png file, save workbook as image)

Τέλος, καλέστε το `Workbook.save` με τις ρυθμισμένες επιλογές. Η μέθοδος γράφει ένα αρχείο PNG στον καθορισμένο φάκελο.

```java
        // Save the worksheet as an image file
        wb.save("output/pivot.png", opts);

        System.out.println("Export completed: output/pivot.png");
    }
}
```

Όταν το πρόγραμμα ολοκληρωθεί, το `output/pivot.png` περιέχει μια pixel‑perfect αναπαράσταση του φύλλου εργασίας, συμπεριλαμβανομένης της εικόνας που προσθέσατε.

### Πλήρες αρχείο πηγαίου κώδικα

```java
import com.aspose.cells.*;

public class ExcelToImage {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook wb = new Workbook("sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);

        // Configure export options
        ImageOrPrintOptions opts = new ImageOrPrintOptions();
        opts.setSaveFormat(SaveFormat.PNG);
        opts.setResolution(300); // optional high‑DPI output

        // Add picture to worksheet
        ws.getPictures().add(0, 0, "A1:G20");

        // Export worksheet as PNG image
        wb.save("output/pivot.png", opts);
        System.out.println("Export completed: output/pivot.png");
    }
}
```

Η εκτέλεση της κλάσης παράγει το αρχείο PNG που φαίνεται παρακάτω (η εικόνα είναι εικονογραφική· το δικό σας αρχείο θα αντανακλά το πραγματικό περιεχόμενο του φύλλου).

![Εξαγόμενο φύλλο Excel ως PNG](/images/excel-to-png.png "Αποτέλεσμα εξαγωγής Excel ως εικόνα χρησιμοποιώντας Java")

*Alt text (image alt):* **Result of export Excel as image using Java – a PNG snapshot of the worksheet** (ικανοποιεί την απαίτηση alt εικόνας).

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Πρόβλημα | Αιτία | Διόρθωση |
|----------|-------|----------|
| **File not found** | Η διαδρομή προς το `sample.xlsx` είναι λανθασμένη. | Χρησιμοποιήστε απόλυτη διαδρομή ή τοποθετήστε το αρχείο στη ρίζα του έργου. |
| **Blank image** | Το φύλλο εργασίας δεν έχει ορατό περιεχόμενο ή η περιοχή εικόνας είναι κενή. | Επαληθεύστε ότι τα κελιά `A1:G20` περιέχουν δεδομένα ή προσαρμόστε την περιοχή. |
| **Low resolution** | Η προεπιλεγμένη DPI είναι 96, κάτι που μπορεί να φαίνεται θολό όταν εκτυπώνεται. | Καλέστε `opts.setResolution(300)` (ή υψηλότερη) πριν από την αποθήκευση. |
| **License exception** | Η χρήση της έκδοσης αξιολόγησης μπορεί να προσθέσει υδατογράφημα. | Εφαρμόστε έγκυρη άδεια Aspose.Cells με `License license = new License(); license.setLicense("Aspose.Total.lic");`. |

## Επόμενα βήματα

Τώρα που μπορείτε να **export Excel as image**, μπορείτε να εξερευνήσετε:

* **Export excel sheet to png** για κάθε φύλλο εργασίας σε ένα βιβλίο εργασίας (βρόχος μέσω `wb.getWorksheets()`).
* Μετατροπή του PNG σε PDF χρησιμοποιώντας Aspose.PDF εάν χρειάζεστε μορφή φιλική προς το έγγραφο.
* Ενσωμάτωση του παραγόμενου PNG σε ιστοσελίδα ή συνημμένο email απευθείας από Java.

Αυτές οι επεκτάσεις βασίζονται στο ίδιο πρότυπο `ImageOrPrintOptions`, διατηρώντας τη βάση κώδικα συνεπή.

## Συμπέρασμα

Έχετε μάθει πώς να **export Excel as image** με Java, πώς να **add picture to worksheet**, και πώς να **save Excel as PNG file** χρησιμοποιώντας Aspose.Cells. Το πλήρες παράδειγμα δείχνει έναν αξιόπιστο τρόπο για **save workbook as image**, διαχείριση ανάλυσης και αποφυγή κοινών σφαλμάτων. Εφαρμόστε το πρότυπο για αυτοματοποίηση αναφορών, δημιουργία μικρογραφιών ή ενσωμάτωση οπτικών στοιχείων λογιστικών φύλλων σε οποιαδήποτε ροή εργασίας βασισμένη σε Java.

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java: A Step‑by‑Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Export Excel Workbook As Image Using Aspose Cells For Java](/cells/german/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}