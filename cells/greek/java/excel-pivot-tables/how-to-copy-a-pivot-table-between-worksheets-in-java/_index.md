---
category: general
date: 2026-10-16
description: Πώς να αντιγράψετε έναν συγκεντρωτικό πίνακα σε Java με το Aspose.Cells
  – μάθετε πώς να αντιγράψετε μια περιοχή σε άλλο φύλλο και να αντιγράψετε περιοχή
  μεταξύ φύλλων εργασίας αποδοτικά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to another sheet
- copy range between worksheets
language: el
lastmod: 2026-10-16
og_description: Πώς να αντιγράψετε έναν πίνακα Pivot σε Java χρησιμοποιώντας το Aspose.Cells.
  Αυτό το σεμινάριο σας δείχνει πώς να αντιγράψετε μια περιοχή σε άλλο φύλλο και πώς
  να αντιγράψετε μια περιοχή μεταξύ φύλλων εργασίας με πλήρες κώδικα.
og_image_alt: Diagram illustrating how to copy pivot table from one worksheet to another
  in Java
og_title: Πώς να αντιγράψετε έναν πίνακα Pivot μεταξύ φύλλων εργασίας σε Java – βήμα‑βήμα
  οδηγός
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  headline: How to copy a pivot table between worksheets in Java
  type: TechArticle
- description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  name: How to copy a pivot table between worksheets in Java
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Locate the source range that contains the pivot table
    text: '```java // The first worksheet (index 0) holds the pivot table. Worksheet
      sourceSheet = workbook.getWorksheets().get(0);'
  - name: Define the destination range on another sheet
    text: '```java // The second worksheet (index 1) will receive the copied pivot
      table. Worksheet destSheet = workbook.getWorksheets().get(1);'
  - name: Copy the source range while preserving the pivot table
    text: '```java // Configure copy options to keep all formatting, formulas, and
      pivot data. CopyOptions copyOptions = new CopyOptions(); copyOptions.setPasteType(PasteType.PASTE_ALL);
      // copies everything copyOptions.setSkipEmptyRows(false); copyOptions.setSkipEmptyColumns(false);'
  - name: Save the workbook and verify the result
    text: '```java // Save the modified workbook to a new file. workbook.save("output.xlsx");
      System.out.println("Pivot table copied successfully."); } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- Excel automation
title: Πώς να αντιγράψετε έναν συγκεντρωτικό πίνακα μεταξύ φύλλων εργασίας στη Java
url: /el/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αντιγράψετε έναν πίνακα Pivot μεταξύ φύλλων εργασίας σε Java

Αν χρειάζεστε **πώς να αντιγράψετε πίνακα pivot** από ένα φύλλο σε άλλο στο ίδιο βιβλίο εργασίας, αυτός ο οδηγός παρέχει μια πλήρη, έτοιμη‑για‑εκτέλεση λύση. Θα δείτε πώς να αντιγράψετε την περιοχή προέλευσης που περιέχει τον πίνακα pivot, να διατηρήσετε τη λειτουργικότητά του και να επαληθεύσετε το αποτέλεσμα—όλα χρησιμοποιώντας το Aspose.Cells for Java.

Η αντιγραφή ενός πίνακα pivot είναι μια συνηθισμένη εργασία όταν δημιουργείτε αναφορές προγραμματιστικά, και η σωστή εκτέλεσή της αποτρέπει την απώλεια της κρυφής μνήμης (pivot cache) ή τη διακοπή των τύπων. Στο τέλος αυτού του σεμιναρίου θα μπορείτε να **αντιγράψετε περιοχή σε άλλο φύλλο** και **αντιγράψετε περιοχή μεταξύ φύλλων εργασίας** χωρίς κανένα χειροκίνητο βήμα.

## Τι θα μάθετε

* Φόρτωση υπάρχοντος αρχείου Excel με πίνακα pivot.
* Ορισμός της περιοχής προέλευσης που περιέχει τον πίνακα pivot.
* Ορισμός μιας περιοχής προορισμού σε διαφορετικό φύλλο εργασίας.
* Χρήση του `CopyOptions` για να διατηρηθεί αμετάβλητος ο πίνακας pivot.
* Επαλήθευση ότι ο αντιγραμμένος πίνακας pivot λειτουργεί όπως αναμένεται.

**Προαπαιτούμενα**

* Java 17 ή νεότερη.
* Aspose.Cells for Java (έκδοση 23.12 ή νεότερη).  
* Ένα αρχείο Excel (`input.xlsx`) που περιέχει έναν πίνακα pivot στο πρώτο φύλλο.

---

## Πώς να αντιγράψετε πίνακα pivot με Aspose.Cells

Ο πυρήνας της λειτουργίας είναι μια διαδικασία τεσσάρων βημάτων: φόρτωση του βιβλίου εργασίας, εντοπισμός της περιοχής προέλευσης, ορισμός της περιοχής προορισμού και εκτέλεση της αντιγραφής. Κάθε βήμα εξηγείται λεπτομερώς παρακάτω.

### Βήμα 1: Φόρτωση του βιβλίου εργασίας

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the original pivot table
        Workbook workbook = new Workbook("input.xlsx");
```

*Γιατί αυτό το βήμα;*  
Η φόρτωση του βιβλίου εργασίας φέρνει ολόκληρο το αρχείο στη μνήμη, δίνοντάς σας πρόσβαση σε φύλλα, κελιά και την κρυφή μνήμη του pivot. Το Aspose.Cells διαβάζει αυτόματα τη μορφή του αρχείου, οπότε δεν χρειάζεται να ανησυχείτε για `.xls` vs `.xlsx`.

### Βήμα 2: Εντοπισμός της περιοχής προέλευσης που περιέχει τον πίνακα pivot

```java
        // The first worksheet (index 0) holds the pivot table.
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the exact area that includes the pivot table.
        // Adjust the address if your pivot table spans a different range.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*Γιατί αυτό το βήμα;*  
Ένας πίνακας pivot αποθηκεύεται σε ένα μπλοκ κελιών που επίσης αναφέρεται σε μια κρυφή μνήμη. Επιλέγοντας ακριβώς την περιοχή (`A1:G20` σε αυτό το παράδειγμα), εξασφαλίζετε ότι η μνήμη παραμένει συνδεδεμένη όταν η περιοχή αντιγράφεται.

### Βήμα 3: Ορισμός της περιοχής προορισμού σε άλλο φύλλο

```java
        // The second worksheet (index 1) will receive the copied pivot table.
        Worksheet destSheet = workbook.getWorksheets().get(1);

        // Destination starts at cell A1 of the second sheet.
        Range destRange = destSheet.getCells().createRange("A1");
```

*Γιατί αυτό το βήμα;*  
Η επιλογή προορισμού σε διαφορετικό φύλλο εργασίας σας επιτρέπει να **αντιγράψετε περιοχή σε άλλο φύλλο**. Το κελί επάνω‑αριστερά (`A1`) είναι ένα κοινό σημείο εκκίνησης, αλλά μπορείτε να το τοποθετήσετε οπουδήποτε αλλάζοντας τη διεύθυνση.

### Βήμα 4: Αντιγραφή της περιοχής προέλευσης διατηρώντας τον πίνακα pivot

```java
        // Configure copy options to keep all formatting, formulas, and pivot data.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // copies everything
        copyOptions.setSkipEmptyRows(false);
        copyOptions.setSkipEmptyColumns(false);

        // Perform the copy operation.
        sourceRange.copy(destRange, copyOptions);
```

*Γιατί αυτό το βήμα;*  
Το `CopyOptions` ελέγχει τι μεταφέρεται. Η χρήση του `PasteType.PASTE_ALL` εγγυάται ότι ο πίνακας pivot, η μορφοποίηση και οι υποκείμενοι τύποι αντιγράφονται. Χωρίς αυτές τις επιλογές, μπορεί να αντιγραφούν μόνο οι ακατέργαστες τιμές, σπάζοντας τη λειτουργικότητα του pivot.

### Βήμα 5: Αποθήκευση του βιβλίου εργασίας και επαλήθευση του αποτελέσματος

```java
        // Save the modified workbook to a new file.
        workbook.save("output.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

Ανοίξτε το `output.xlsx` στο Excel και επιβεβαιώστε ότι:

* Το δεύτερο φύλλο περιέχει έναν πλήρως λειτουργικό πίνακα pivot που είναι ταυτόσιος με τον αρχικό.
* Η ανανέωση του πίνακα pivot ενημερώνει τα δεδομένα, αποδεικνύοντας ότι η μνήμη παραμένει ακεραιότητα.

---

## Αντιγραφή περιοχής σε άλλο φύλλο χρησιμοποιώντας Java

Αν ο στόχος σας είναι απλώς **αντιγράψετε περιοχή σε άλλο φύλλο** χωρίς πίνακα pivot, ο ίδιος κώδικας λειτουργεί με μια κανονική περιοχή κελιών. Η μόνη αλλαγή είναι η διεύθυνση προέλευσης. Η διαμόρφωση του `CopyOptions` παραμένει η ίδια, διασφαλίζοντας ότι οι τύποι και η μορφοποίηση διατηρούνται.

```java
// Example: copy a plain data table from Sheet1!B2:D10 to Sheet3!A1
Range plainSource = workbook.getWorksheets().get(0)
                            .getCells().createRange("B2:D10");
Range plainDest = workbook.getWorksheets().get(2)
                          .getCells().createRange("A1");
plainSource.copy(plainDest, copyOptions);
```

Αυτό το απόσπασμα δείχνει την ευελιξία του API για σενάρια με ή χωρίς pivot.

---

## Αντιγραφή περιοχής μεταξύ φύλλων εργασίας χωρίς απώλεια τύπων

Όταν **αντιγράψετε περιοχή μεταξύ φύλλων εργασίας**, οι τύποι που αναφέρονται σε άλλα φύλλα μπορεί να σπαστούν αν αλλάξουν οι σχετικές αναφορές. Για να το αποφύγετε:

1. Χρησιμοποιήστε `CopyOptions.setPasteType(PasteType.PASTE_FORMULAS)` αν χρειάζεστε μόνο τύπους.
2. Κρατήστε το φύλλο προορισμού στο ίδιο βιβλίο εργασίας ώστε οι εσωτερικές αναφορές να παραμείνουν έγκυρες.
3. Μετά την αντιγραφή, καλέστε `workbook.calculateFormula();` για να εξαναγκάσετε επανυπολογισμό.

```java
copyOptions.setPasteType(PasteType.PASTE_FORMULAS);
sourceRange.copy(destRange, copyOptions);
workbook.calculateFormula();
```

Αυτά τα επιπλέον βήματα διασφαλίζουν ότι η αντιγραμμένη περιοχή συμπεριφέρεται ακριβώς όπως η αρχική, ακόμη και όταν εκτείνεται σε πολλά φύλλα εργασίας.

---

## Συμβουλές επαγγελματιών και κοινές παγίδες

| Κατάσταση | Συμβουλή |
|-----------|----------|
| **Η μνήμη του pivot δεν ενημερώνεται** | Μετά την αντιγραφή, καλέστε `destSheet.getPivotTables().get(0).refresh();` για να ανανεώσετε τη μνήμη. |
| **Αντιγραφή σε διαφορετικό βιβλίο εργασίας** | Χρησιμοποιήστε `Workbook destWorkbook = new Workbook();` και στη συνέχεια `sourceRange.copy(destWorkbook.getWorksheets().get(0).getCells().createRange("A1"), copyOptions);`. Θυμηθείτε να αντιγράψετε τη μνήμη του pivot ξεχωριστά αν χρειάζεται. |
| **Μεγάλοι πίνακες pivot** | Αυξήστε το μέγεθος της μνήμης heap της Java (`-Xmx2g`) για να αποφύγετε `OutOfMemoryError` κατά την αντιγραφή. |
| **Διατήρηση στυλ** | Ορίστε `copyOptions.setPasteType(PasteType.PASTE_ALL)`· διαφορετικά θα αντιγραφούν μόνο οι τιμές. |

---

## Αναμενόμενο αποτέλεσμα

Η εκτέλεση του πλήρους προγράμματος παράγει το `output.xlsx`. Όταν ανοίξει στο Excel:

* **Sheet2!A1:G20** εμφανίζει τον ίδιο πίνακα pivot με το **Sheet1!A1:G20**.
* Η λίστα πεδίων του pivot, οι ετικέτες γραμμών/στηλών και οι τιμές δεδομένων ταιριάζουν με την πηγή.
* Η ανανέωση του pivot ενημερώνει τους αριθμούς, επιβεβαιώνοντας ότι η μνήμη λειτουργεί.

Η κονσόλα θα εκτυπώσει:

```
Pivot table copied successfully.
```

---

## Συμπέρασμα

Σε αυτόν τον οδηγό μάθατε **πώς να αντιγράψετε πίνακα pivot** από ένα φύλλο εργασίας σε άλλο χρησιμοποιώντας το Aspose.Cells for Java. Φορτώνοντας το βιβλίο εργασίας, επιλέγοντας τη σωστή περιοχή προέλευσης, ορίζοντας προορισμό και διαμορφώνοντας το `CopyOptions`, μπορείτε αξιόπιστα να **αντιγράψετε περιοχή σε άλλο φύλλο** και **αντιγράψετε περιοχή μεταξύ φύλλων εργασίας** διατηρώντας όλη τη λειτουργικότητα του pivot.  

Στη συνέχεια, μπορείτε να εξερευνήσετε:

* Εξαγωγή του αντιγραμμένου πίνακα pivot σε PDF ή HTML.
* Αυτοματοποίηση της ανανέωσης των πινάκων pivot σε πολλαπλά βιβλία εργασίας.
* Χρήση του `CopyOptions` για αντιγραφή μόνο συγκεκριμένων στοιχείων (π.χ. τιμές, μορφοποιήσεις).

Μη διστάσετε να πειραματιστείτε με διαφορετικές διευθύνσεις περιοχών, δομές βιβλίων εργασίας ή ακόμη και αντιγραφές μεταξύ βιβλίων. Καλή προγραμματιστική δημιουργία!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω σεμινάρια καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Πώς να αντιγράψετε περιοχή σε Java – Αντιγραφή Πίνακα Pivot με Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)
- [Πώς να αντιγράψετε Πίνακα Pivot σε Java – Πλήρης Οδηγός Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Αντιγραφή Πίνακα Pivot Excel – Οδηγός βήμα‑βήμα χρησιμοποιώντας Java](/cells/english/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}