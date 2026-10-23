---
category: general
date: 2026-10-23
description: Μάθετε πώς να αντιγράψετε ένα φύλλο Excel σε Java διατηρώντας τους συγκεντρωτικούς
  πίνακες. Αυτός ο οδηγός δείχνει επίσης πώς να αντιγράψετε συγκεντρωτικούς πίνακες,
  να αντιγράψετε περιοχές Excel και να αντιγράψετε ένα φύλλο με δεδομένα συγκεντρωτικού
  πίνακα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- duplicate excel sheet
- how to copy pivot
- copy excel range
- copy sheet with pivot
- copy pivot to workbook
language: el
lastmod: 2026-10-23
og_description: Δημιουργήστε αντίγραφο ενός φύλλου Excel σε Java διατηρώντας τους
  συγκεντρωτικούς πίνακες. Ακολουθήστε αυτό το πλήρες σεμινάριο για να αντιγράψετε
  συγκεντρωτικούς πίνακες, να αντιγράψετε περιοχές Excel και να αντιγράψετε ένα φύλλο
  με δεδομένα συγκεντρωτικού πίνακα.
og_image_alt: Screenshot showing a duplicated Excel sheet with pivot tables preserved
og_title: Αντιγραφή φύλλου Excel με πίνακες Pivot σε Java – οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  headline: How to duplicate an Excel sheet and keep pivot tables intact in Java
  type: TechArticle
- description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  name: How to duplicate an Excel sheet and keep pivot tables intact in Java
  steps:
  - name: Expected output
    text: 'Running the program creates `DuplicatedWithPivot.xlsx` in the target directory.
      Open the file in Excel and you will see:'
  - name: How to copy pivot to another workbook without copying the whole sheet?
    text: If you only need the pivot and its underlying data, copy the range that
      contains both the source data and the pivot, then use `setCopyPivotTable(true)`.
      The same code from **Step 4** applies; just ensure the range covers the data
      source.
  - name: What if the source workbook has multiple worksheets with pivots?
    text: 'Repeat **Step 3** for each worksheet you want to duplicate:'
  - name: Does this work with protected worksheets?
    text: 'Aspose.Cells can copy protected sheets, but you must unprotect them first
      if you need to modify the pivot after copying:'
  - name: Can I copy a pivot table to an existing workbook that already contains a
      sheet with the same name?
    text: 'Yes. Use `addCopy` with a unique name:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot tables
title: Πώς να αντιγράψετε ένα φύλλο Excel και να διατηρήσετε τους συγκεντρωτικούς
  πίνακες ανέπαφους στην Java
url: /el/java/excel-pivot-tables/how-to-duplicate-an-excel-sheet-and-keep-pivot-tables-intact/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αντιγράψετε ένα φύλλο Excel και να διατηρήσετε τα pivot tables αμετάβλητα σε Java

Αν χρειάζεστε **να αντιγράψετε ένα φύλλο Excel** ενώ διατηρείτε κάθε pivot table ενεργό, αυτός ο οδηγός σας δείχνει ακριβώς πώς. Θα δείτε μια σύντομη λύση που αντιγράφει ένα φύλλο, αντιγράφει μια συγκεκριμένη περιοχή και ακόμη αντιγράφει ένα pivot table σε άλλο βιβλίο εργασίας — όλα σε καθαρή Java χρησιμοποιώντας το Aspose.Cells.

Η αντιγραφή ενός φύλλου Excel είναι μια κοινή εργασία όταν δημιουργείτε μηνιαίες αναφορές από ένα πρότυπο ή όταν χρειάζεστε ένα αντίγραφο sandbox για δοκιμές. Ο παρακάτω κώδικας λειτουργεί με το Aspose.Cells 25.11 ή νεότερο, το οποίο εισήγαγε την επιλογή `setCopyPivotTable(true)`.

## Τι θα χρειαστείτε

- Java 17 (ή οποιοδήποτε πρόσφατο JDK) εγκατεστημένο
- Aspose.Cells for Java 25.11 ή νεότερο στο έργο σας (συντεταγμένη Maven `com.aspose:aspose-cells:25.11`)
- Ένα πηγαίο βιβλίο εργασίας (`SourceWithPivot.xlsx`) που ήδη περιέχει ένα pivot table
- Ένα IDE ή εργαλείο κατασκευής της επιλογής σας (IntelliJ IDEA, Eclipse, Maven, Gradle, κ.λπ.)

## Βήμα 1: Φορτώστε το πηγαίο βιβλίο εργασίας που περιέχει το pivot table

Η πρώτη ενέργεια είναι να ανοίξετε το βιβλίο εργασίας που περιέχει το pivot που θέλετε να διατηρήσετε.

```java
import com.aspose.cells.*;

public class DuplicateExcelSheet {
    public static void main(String[] args) throws Exception {
        // Load the source workbook with the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

> **Γιατί είναι σημαντικό αυτό το βήμα:** Η φόρτωση του πηγαίου βιβλίου εργασίας σας δίνει πρόσβαση στα αντικείμενα των φύλλων εργασίας, στα κελιά και στα ενσωματωμένα pivot tables. Χωρίς αυτό, δεν μπορείτε να αναφερθείτε στα δεδομένα του pivot που σκοπεύετε να αντιγράψετε.

## Βήμα 2: Δημιουργήστε ένα κενό βιβλίο εργασίας προορισμού (ή φορτώστε ένα υπάρχον)

Μπορείτε είτε να ξεκινήσετε από ένα κενό βιβλίο εργασίας είτε να ανοίξετε ένα υπάρχον αρχείο που θα λάβει το αντιγραμμένο φύλλο.

```java
        // Create a new, empty destination workbook
        Workbook dstWb = new Workbook();
```

> **Συμβουλή:** Εάν έχετε ήδη ένα βιβλίο εργασίας αναφορών, αντικαταστήστε τη γραμμή παραπάνω με `new Workbook("ExistingReport.xlsx")` για να προσθέσετε το αντιγραμμένο φύλλο σε αυτό.

## Βήμα 3: Αντιγράψτε ολόκληρο το φύλλο εργασίας – το pivot table διατηρείται αυτόματα

Η αντιγραφή ολόκληρου του φύλλου εργασίας είναι ο πιο απλός τρόπος για **να αντιγράψετε φύλλο με pivot**. Το Aspose.Cells αντιγράφει αυτόματα τον ορισμό του pivot και την κρυφή μνήμη του.

```java
        // Access the first worksheet (index 0) from the source workbook
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Add a copy of the source worksheet to the destination workbook
        Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
```

> **Γιατί λειτουργεί:** Η μέθοδος `addCopy` κλωνοποιεί τη δομή του φύλλου, τις τιμές των κελιών, τα στυλ και τυχόν ενσωματωμένα pivot tables. Το νέο φύλλο εργασίας στο `dstWb` θα φαίνεται ταυτόσημο με το αρχικό, συμπεριλαμβανομένης της κρυφής μνήμης του pivot.

## Βήμα 4: (Προαιρετικό) Αντιγράψτε μόνο μια συγκεκριμένη περιοχή που περιλαμβάνει το pivot table

Μερικές φορές δεν θέλετε ολόκληρο το φύλλο — ίσως χρειάζεστε μόνο ένα τμήμα που περιέχει το pivot. Εδώ είναι που **αντιγράφετε περιοχή Excel** και ζητάτε ρητά το pivot να αντιγραφεί.

```java
        // Define the source range that covers the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G30");

        // Define the target range in the destination worksheet
        Range dstRange = dstWs.getCells().createRange("A1");

        // Copy the range and tell Aspose.Cells to include the pivot table
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setCopyPivotTable(true); // new option in 25.11
        dstRange.copy(srcRange, copyOptions);
```

> **Πώς βοηθά:** Η `setCopyPivotTable(true)` αναγκάζει τη μηχανή να διπλασιάσει τον ορισμό του pivot ακόμα και όταν αντιγράφετε περιορισμένη περιοχή. Χωρίς αυτή τη σημαία, θα αντιγραφούν μόνο τα ακατέργαστα δεδομένα και το pivot θα χαθεί.

## Βήμα 5: Αποθηκεύστε το βιβλίο εργασίας προορισμού

Τέλος, γράψτε το αντιγραμμένο περιεχόμενο σε ένα νέο αρχείο.

```java
        // Save the destination workbook to a new file
        dstWb.save("YOUR_DIRECTORY/DuplicatedWithPivot.xlsx");
    }
}
```

### Αναμενόμενο αποτέλεσμα

Η εκτέλεση του προγράμματος δημιουργεί το `DuplicatedWithPivot.xlsx` στον φάκελο προορισμού. Ανοίξτε το αρχείο στο Excel και θα δείτε:

- Ένα νέο φύλλο εργασίας με όνομα `Sheet1 (Copy)` (ή το αρχικό όνομα με προσθήκη “Copy”)
- Το pivot table εμφανίζεται ακριβώς όπως στο πηγαίο φύλλο, πλήρως λειτουργικό
- Εάν χρησιμοποιήσατε την προαιρετική αντιγραφή περιοχής, θα υπάρχουν μόνο τα κελιά A1:G30, αλλά το pivot λειτουργεί ακόμη επειδή η κρυφή μνήμη του αντιγράφηκε

## Συχνές ερωτήσεις και ειδικές περιπτώσεις

### Πώς να αντιγράψετε το pivot σε άλλο βιβλίο εργασίας χωρίς να αντιγράψετε ολόκληρο το φύλλο;

Αν χρειάζεστε μόνο το pivot και τα υποκείμενα δεδομένα του, αντιγράψτε την περιοχή που περιέχει τόσο τα δεδομένα πηγής όσο και το pivot, και στη συνέχεια χρησιμοποιήστε τη `setCopyPivotTable(true)`. Ο ίδιος κώδικας από το **Βήμα 4** ισχύει· απλώς βεβαιωθείτε ότι η περιοχή καλύπτει την πηγή δεδομένων.

### Τι γίνεται αν το πηγαίο βιβλίο εργασίας έχει πολλά φύλλα εργασίας με pivots;

Επαναλάβετε το **Βήμα 3** για κάθε φύλλο εργασίας που θέλετε να αντιγράψετε:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet ws = srcWb.getWorksheets().get(i);
    dstWb.getWorksheets().addCopy(ws);
}
```

### Λειτουργεί αυτό με προστατευμένα φύλλα εργασίας;

Το Aspose.Cells μπορεί να αντιγράψει προστατευμένα φύλλα, αλλά πρέπει πρώτα να τα αποπροστατεύσετε εάν χρειάζεται να τροποποιήσετε το pivot μετά την αντιγραφή:

```java
srcWs.unprotect("password");
dstWs.unprotect("password");
```

### Μπορώ να αντιγράψω ένα pivot table σε υπάρχον βιβλίο εργασίας που ήδη περιέχει φύλλο με το ίδιο όνομα;

Ναι. Χρησιμοποιήστε τη `addCopy` με ένα μοναδικό όνομα:

```java
Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
dstWs.setName("PivotCopy_" + System.currentTimeMillis());
```

## Συμβουλή επαγγελματία: επαληθεύστε την κρυφή μνήμη του pivot

Μετά την αντιγραφή, μπορείτε προγραμματιστικά να επιβεβαιώσετε ότι η κρυφή μνήμη του pivot υπάρχει:

```java
PivotTable pt = dstWs.getPivotTables().get(0);
System.out.println("Pivot cache ID: " + pt.getCacheIndex());
```

Αν το ID της κρυφής μνήμης εκτυπώσει έναν μη‑αρνητικό αριθμό, το pivot αντιγράφηκε επιτυχώς.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **αντιγράψετε ένα φύλλο Excel** σε Java διατηρώντας κάθε pivot table, πώς να **αντιγράψετε pivot** tables απευθείας, πώς να **αντιγράψετε περιοχή Excel** που περιλαμβάνει ένα pivot, και πώς να **αντιγράψετε φύλλο με pivot** ή **αντιγράψετε pivot σε βιβλίο εργασίας** χρησιμοποιώντας το Aspose.Cells 25.11+. Εφαρμόστε αυτά τα πρότυπα για να αυτοματοποιήσετε τη δημιουργία αναφορών, να δημιουργήσετε κλώνα προτύπων ή να χτίσετε περιβάλλοντα δοκιμών που χρειάζονται πανομοιότυπη ανάλυση με pivot.

Έτοιμοι να εξερευνήσετε περισσότερα; Δοκιμάστε να εξάγετε το αντιγραμμένο βιβλίο εργασίας σε PDF, ή προγραμματιστικά να ανανεώσετε την κρυφή μνήμη του pivot μετά την αντιγραφή για να διασφαλίσετε ότι τα πιο πρόσφατα δεδομένα αντικατοπτρίζονται. Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να αντιγράψετε φύλλο εργασίας και να διατηρήσετε τα pivot tables σε Java](/cells/english/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/)
- [Πώς να αντιγράψετε Pivot Table σε Java – Πλήρης Οδηγός Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Πώς να αντιγράψετε περιοχή και να διατηρήσετε ένα pivot table σε Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}