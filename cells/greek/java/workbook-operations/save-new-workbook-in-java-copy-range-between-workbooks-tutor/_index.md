---
category: general
date: 2026-07-29
description: Αποθήκευση νέου βιβλίου εργασίας σε Java ενώ αντιγράφετε περιοχή μεταξύ
  βιβλίων εργασίας. Μάθετε πώς να μεταφέρετε μια περιοχή Excel και να διατηρήσετε
  τη μορφοποίηση κατά την αντιγραφή σε λίγα μόνο βήματα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save new workbook
- copy range between workbooks
- transfer excel range
- load excel workbook java
- preserve formatting copy
language: el
lastmod: 2026-07-29
og_description: Αποθηκεύστε νέο βιβλίο εργασίας σε Java με το Aspose.Cells—μάθετε
  πώς να αντιγράψετε περιοχή μεταξύ βιβλίων εργασίας διατηρώντας τη μορφοποίηση, όλα
  σε έναν σύντομο οδηγό βήμα‑βήμα.
og_image_alt: Java code that saves new workbook after transferring an Excel range
og_title: Αποθήκευση νέου βιβλίου εργασίας σε Java – Αντιγραφή περιοχής μεταξύ βιβλίων
  εργασίας
schemas:
- author: Aspose
  dateModified: '2026-07-29'
  description: Save new workbook in Java while copy range between workbooks. Learn
    to transfer Excel range and preserve formatting copy in just a few steps.
  headline: Save New Workbook in Java – Copy Range Between Workbooks Tutorial
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
- Workbook
- File I/O
title: Αποθήκευση νέου βιβλίου εργασίας σε Java – Οδηγός αντιγραφής περιοχής μεταξύ
  βιβλίων εργασίας
url: /el/java/workbook-operations/save-new-workbook-in-java-copy-range-between-workbooks-tutor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αποθήκευση Νέου Φύλλου Εργασίας σε Java – Αντιγραφή Περιοχής μεταξύ Φύλλων Εργασίας

Έχετε χρειαστεί ποτέ να **save new workbook** μετά τη μεταφορά δεδομένων από ένα αρχείο Excel σε άλλο, αλλά δεν ήσασταν σίγουροι πώς να διατηρήσετε το αρχικό στυλ; Δεν είστε μόνοι. Σε πολλές επιχειρηματικές εφαρμογές πρέπει να **transfer Excel range** από ένα πρότυπο σε ένα αρχείο που δημιουργείται από τον χρήστη, και το κόλπο είναι να εξασφαλίσουμε ότι η μορφοποίηση παραμένει ανέπαφη.

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που **load Excel workbook java**‑style χρησιμοποιώντας Aspose.Cells, **copy range between workbooks**, και τελικά **save new workbook** με όλα τα αρχικά χρώματα, περιγράμματα και μορφές αριθμών αμετάβλητα. Χωρίς περιττές πληροφορίες—απλώς ο κώδικας που μπορείτε να ενσωματώσετε στο πρότζεκτ σας σήμερα.

> **Pro tip:** Αν ήδη χρησιμοποιείτε Maven, προσθέστε τη εξάρτηση Aspose.Cells μία φορά και θα είστε έτοιμοι για οποιαδήποτε εργασία χειρισμού φύλλων εργασίας.

## Prerequisites

- Java 17 (ή οποιοδήποτε πρόσφατο JDK)
- Aspose.Cells for Java (έκδοση 23.10 ή νεότερη)
- Βασική εξοικείωση με Java I/O
- Δύο αρχεία Excel: ένα πηγαίο (`source.xlsx`) που περιέχει τα δεδομένα που θέλετε να μετακινήσετε, και ένα κενό προορισμό (`dest.xlsx`) που θα δημιουργηθεί από τον κώδικα

Τώρα, ας βουτήξουμε στα βήματα.

## Step 1 – Load Excel Workbook Java Style

Το πρώτο που κάνουμε είναι **load Excel workbook java**‑wise. Η Aspose.Cells αφαιρεί την πολυπλοκότητα του μορφότυπου αρχείου, ώστε να μην χρειάζεται να ανησυχείτε για το υποκείμενο XML.

```java
import com.aspose.cells.*;

public class ExcelRangeTransfer {
    public static void main(String[] args) throws Exception {
        // Load the source workbook (make sure the path is correct)
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // ------------------------------------------------------------
        // At this point the source workbook is fully loaded in memory.
        // ------------------------------------------------------------
```

*Why this matters:* Η φόρτωση του φύλλου εργασίας σας δίνει πρόσβαση σε κάθε φύλλο, κελί και αντικείμενο στυλ. Αν παραλείψετε αυτό το βήμα και προσπαθήσετε να αντιγράψετε απευθείας από ροή αρχείου, θα χάσετε τη δυνατότητα διατήρησης της μορφοποίησης αργότερα.

## Step 2 – Define the Source Range (Preserve Formatting Copy)

Στη συνέχεια εντοπίζουμε ακριβώς την περιοχή που θέλουμε να μετακινήσουμε. Στο παράδειγμά μας η περιοχή `A1:G20` περιέχει έναν πίνακα Pivot και μερικές γραμμές κεφαλίδας. Δημιουργώντας ένα αντικείμενο `Range` μπορούμε αργότερα να πούμε στην Aspose.Cells να διατηρήσει κάθε στυλ αμετάβλητο—αυτή είναι η ουσία μιας **preserve formatting copy**.

```java
        // Grab the first worksheet
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // Define the range that includes the data we want to copy
        // Using createRange ensures we capture formulas, formats, and comments.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*Tip:* Αν χρειάζεται να αντιγράψετε μια δυναμική περιοχή, μπορείτε να υπολογίσετε την τελευταία χρησιμοποιημένη γραμμή/στήλη με `sourceSheet.getCells().getMaxDataRow()` και να δημιουργήσετε τη διεύθυνση on‑the‑fly.

## Step 3 – Create Destination Workbook (Where We'll Save New Workbook)

Τώρα δημιουργούμε ένα νέο φύλλο εργασίας που θα λάβει τα δεδομένα. Εδώ θα συμβεί τελικά η ενέργεια **save new workbook**.

```java
        // Create a brand‑new workbook that will become our destination file
        Workbook destinationWorkbook = new Workbook();

        // Get its first worksheet – this is where we’ll paste the range
        Worksheet destSheet = destinationWorkbook.getWorksheets().get(0);
```

*Why we create a new one:* Ξεκινώντας με ένα καθαρό φύλλο εργασίας εξασφαλίζουμε ότι δεν υπάρχουν υπόλοιπα στυλ που θα μπορούσαν να συγκρούονται με την εισερχόμενη περιοχή. Επίσης, το τελικό μέγεθος του αρχείου γίνεται μικρότερο επειδή αποθηκεύονται μόνο οι απαιτούμενοι πόροι.

## Step 4 – Copy Range Between Workbooks

Αυτή είναι η καρδιά του οδηγού: **copy range between workbooks** ενώ διατηρούμε κάθε οπτική ένδειξη. Η κλάση `CopyOptions` μας επιτρέπει να ορίσουμε ότι θέλουμε πλήρη αντιγραφή, όχι μόνο τιμές.

```java
        // Set up copy options to keep everything—values, formulas, formats, comments.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // ensures formatting stays

        // Perform the copy. The destination starts at cell A1 (row 0, column 0).
        destSheet.getCells().copyRange(sourceRange, 0, 0, copyOptions);
```

*Common question:* *Τι γίνεται αν χρειάζομαι μόνο τις τιμές, χωρίς μορφοποίηση;* Αλλάξτε το `PasteType.ALL` σε `PasteType.VALUES` και η μορφοποίηση θα αγνοηθεί.

## Step 5 – Save New Workbook

Τέλος, γράφουμε το αρχείο προορισμού στον δίσκο. Αυτή είναι η στιγμή που πραγματικά **save new workbook** και βλέπουμε το αποτέλεσμα των προηγούμενων βημάτων.

```java
        // Persist the destination workbook to the file system
        destinationWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Destination workbook saved successfully.");
    }
}
```

Όταν ανοίξετε το `dest.xlsx` θα δείτε ακριβώς την ίδια εμφάνιση και αίσθηση όπως η αρχική περιοχή του `source.xlsx`—χρώματα, περιγράμματα και μορφές αριθμών όλα αμετάβλητα.

<img src="excel-copy.png" alt="Κώδικας Java που αποθηκεύει νέο φύλλο εργασίας μετά τη μεταφορά μιας περιοχής Excel" />

## Full Working Example (All Steps Combined)

Παρακάτω βρίσκεται το πλήρες, αυτόνομο πρόγραμμα. Αντιγράψτε το σε ένα αρχείο με όνομα `ExcelRangeTransfer.java`, προσαρμόστε τις διαδρομές αρχείων και τρέξτε το με `javac`/`java`.

```java
import com.aspose.cells.*;

public class ExcelRangeTransfer {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // 2️⃣ Get the first worksheet and define the range we want to copy
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Create a fresh destination workbook
        Workbook destinationWorkbook = new Workbook();
        Worksheet destSheet = destinationWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the defined range – preserving formatting
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        destSheet.getCells().copyRange(sourceRange, 0, 0, copyOptions);

        // 5️⃣ Save new workbook to disk
        destinationWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Destination workbook saved successfully.");
    }
}
```

**Expected output** όταν τρέξετε το πρόγραμμα:

```
Destination workbook saved successfully.
```

Ανοίξτε το `dest.xlsx` και θα δείτε το ακριβές αντίγραφο του `A1:G20` από το πηγαίο αρχείο, πλήρως εξοπλισμένο με το αρχικό στυλ.

## Frequently Asked Questions & Edge Cases

| Question | Answer |
|----------|--------|
| *Can I copy between workbooks that use different Excel versions?* | Ναι. Η Aspose.Cells κανονικοποιεί το μορφότυπο εσωτερικά, ώστε ένα πηγαίο `.xls` να μπορεί να αντιγραφεί σε προορισμό `.xlsx` χωρίς επιπλέον εργασία. |
| *What if the destination already contains data?* | Χρησιμοποιήστε `copyRange` με διαφορετική αρχική γραμμή/στήλη (π.χ., `5, 2`) για να επικολλήσετε αλλού, ή καθαρίστε το φύλλο πρώτα με `destSheet.getCells().clearAll()`. |
| *Do formulas stay linked to the original workbook?* | Από προεπιλογή γίνονται **relative** προς τον προορισμό. Αν χρειάζεστε εξωτερικές αναφορές, ορίστε `copyOptions.setPasteType(PasteType.FORMULAS)` και διαχειριστείτε χειροκίνητα τους συνδέσμους των βιβλίων εργασίας. |
| *How do I preserve column widths?* | Τα πλάτη των στηλών είναι μέρος της μορφής· το `PasteType.ALL` τα αντιγράφει ήδη. Αν παρατηρήσετε διαφορές, καλέστε `destSheet.autoFitColumns()` μετά την αντιγραφή. |

## Next Steps – Going Beyond the Basics

Τώρα που ξέρετε πώς να **save new workbook**, **copy range between workbooks**, και **preserve formatting copy**, ίσως θέλετε να εξερευνήσετε:

- **Batch processing** – επανάληψη σε φάκελο πηγαίων αρχείων και δημιουργία ενοποιημένης αναφοράς.
- **Conditional formatting transfer** – χρησιμοποιήστε `CopyOptions.setPasteType(PasteType.FORMATS)` για να εστιάσετε μόνο στα στυλ.
- **Streaming API** – για τεράστια αρχεία, η κλάση `Workbook` προσφέρει λειτουργία χαμηλής μνήμης που εξακολουθεί να υποστηρίζει την αντιγραφή περιοχών.

Κάθε ένα από αυτά τα θέματα βασίζεται φυσικά στις έννοιες που καλύψαμε εδώ, και όλα περιστρέφονται γύρω από την ίδια κεντρική ιδέα: να χειρίζεστε αρχεία Excel σε Java με σιγουριά και ακρίβεια.

---

### TL;DR

Ξεκινήσαμε με **load excel workbook java**, ορίσαμε μια **transfer excel range**, χρησιμοποιήσαμε **copy range between workbooks** με `CopyOptions` για **preserve formatting copy**, δημιουργήσαμε ένα νέο αρχείο, και τελικά **save new workbook**. Το αποτέλεσμα είναι ένα πλήρως λειτουργικό `dest.xlsx` που αντικατοπτρίζει την πηγαία περιοχή μέχρι το τελευταίο στυλ κελιού.

Δοκιμάστε το, τροποποιήστε τη διεύθυνση της περιοχής, και δείτε πόσο γρήγορα μπορείτε να αυτοματοποιήσετε εργασίες αναφοράς Excel σε Java. Happy coding!

## What Should You Learn Next?

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει ολοκληρωμένα παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Implement a Named Range with Workbook Scope in Aspose.Cells Java for Enhanced Excel Data Management](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
- [Save Excel Workbook with Aspose.Cells for Java – Complete Guide](/cells/english/java/automation-batch-processing/excel-workbook-automation-aspose-cells-java/)
- [Save Excel File Java with Aspose.Cells – Mastering Workbook Automation](/cells/english/java/automation-batch-processing/aspose-cells-java-excel-workbook-automation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}