---
category: general
date: 2026-08-08
description: Πώς να αντιγράψετε έναν συγκεντρωτικό πίνακα στο Aspose.Cells και να
  αντιγράψετε μια περιοχή σε βιβλίο εργασίας χρησιμοποιώντας Java. Μάθετε τα ακριβή
  βήματα για την αντιγραφή ενός συγκεντρωτικού πίνακα με το CopyOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range to workbook
- aspose.cells copy range
language: el
lastmod: 2026-08-08
og_description: Πώς να αντιγράψετε έναν συγκεντρωτικό πίνακα στο Aspose.Cells και
  να αντιγράψετε περιοχή σε βιβλίο εργασίας με Java. Ακολουθήστε αυτόν τον πλήρη οδηγό
  για να διπλασιάσετε έναν συγκεντρωτικό πίνακα χρησιμοποιώντας το CopyOptions.
og_image_alt: Diagram showing how to copy pivot in Aspose.Cells
og_title: Πώς να αντιγράψετε τον πίνακα Pivot στο Aspose.Cells – αντιγραφή περιοχής
  σε βιβλίο εργασίας
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  headline: How to copy pivot in Aspose.Cells – copy range to workbook
  type: TechArticle
- description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  name: How to copy pivot in Aspose.Cells – copy range to workbook
  steps:
  - name: Add Aspose.Cells to your project
    text: 'If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Configure copy options to include the pivot table
    text: '```java // Define copy options to include the pivot table in the copied
      range CopyOptions copyOptions = new CopyOptions() .setCopyPivotTable(true);
      ```'
  - name: Copy the desired range with the pivot table
    text: '```java // Copy the range A1:H20, preserving the pivot table workbook.getWorksheets().get(0).getCells()
      .copyRange("A1:H20", copyOptions); ```'
  - name: Save the modified workbook
    text: '```java // Save the workbook with the copied pivot table workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected result
    text: '* `output.xlsx` contains the same data as `input.xlsx`. * The pivot table
      that originally occupied the source range appears in the destination cells,
      fully functional (filters, refresh capability, etc.). * All cell formatting,
      formulas, and column widths are preserved because `copyRange` copies the '
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- CopyRange
title: Πώς να αντιγράψετε το pivot στο Aspose.Cells – αντιγραφή περιοχής σε βιβλίο
  εργασίας
url: /el/java/excel-pivot-tables/how-to-copy-pivot-in-aspose-cells-copy-range-to-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αντιγράψετε pivot σε Aspose.Cells – αντιγραφή περιοχής σε βιβλίο εργασίας

Αν χρειάζεστε **how to copy pivot** σε ένα αρχείο Excel χρησιμοποιώντας Aspose.Cells, αυτός ο οδηγός σας δείχνει τη συγκεκριμένη διαδικασία. Στο τέλος του tutorial θα μπορείτε να **copy range to workbook** διατηρώντας τον ορισμό του πίνακα pivot.

Το παράδειγμα χρησιμοποιεί Java, αλλά οι ίδιες έννοιες ισχύουν για οποιαδήποτε γλώσσα .NET που λειτουργεί με Aspose.Cells. Δεν απαιτούνται εξωτερικά εργαλεία—μόνο η βιβλιοθήκη Aspose.Cells for Java και ένα βασικό περιβάλλον ανάπτυξης.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Java Development Kit (JDK) 8 ή νεότερο.
* Maven ή Gradle για διαχείριση εξαρτήσεων (το παράδειγμα χρησιμοποιεί Maven).
* Aspose.Cells for Java 23.9 (ή η πιο πρόσφατη έκδοση) προστέθηκε στο έργο σας.
* Ένα αρχείο εργασίας εισόδου (`input.xlsx`) που περιέχει τουλάχιστον έναν πίνακα pivot στο πρώτο φύλλο εργασίας.

Η προετοιμασία αυτών των στοιχείων αποτρέπει σφάλματα χρόνου εκτέλεσης όταν ο κώδικας προσπελάζει το βιβλίο εργασίας.

## Πώς να αντιγράψετε pivot με Aspose.Cells

Αυτή η ενότητα περιγράφει κάθε βήμα που απαιτείται για **how to copy pivot** από ένα τμήμα ενός φύλλου σε άλλο, χρησιμοποιώντας την κλάση `CopyOptions`.

### Βήμα 1: Προσθέστε Aspose.Cells στο έργο σας

Αν χρησιμοποιείτε Maven, προσθέστε την ακόλουθη εξάρτηση στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust JDK version as needed -->
</dependency>
```

*Γιατί είναι σημαντικό αυτό το βήμα*: Η βιβλιοθήκη παρέχει τις κλάσεις `Workbook`, `CopyOptions` και άλλες που απαιτούνται για λειτουργίες **aspose.cells copy range**. Χωρίς την εξάρτηση, ο μεταγλωττιστής δεν μπορεί να εντοπίσει αυτούς τους τύπους.

### Βήμα 2: Φορτώστε το πηγαίο βιβλίο εργασίας

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Η φόρτωση του αρχείου δημιουργεί μια αναπαράσταση του υπολογιστικού φύλλου στη μνήμη. Το αντικείμενο `Workbook` σας δίνει πρόσβαση σε φύλλα εργασίας, κελιά και πίνακες pivot.

### Βήμα 3: Διαμορφώστε τις επιλογές αντιγραφής ώστε να περιλαμβάνεται ο πίνακας pivot

```java
        // Define copy options to include the pivot table in the copied range
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);
```

`CopyOptions.setCopyPivotTable(true)` ενημερώνει το Aspose.Cells ότι η λειτουργία πρέπει να διατηρήσει τα μεταδεδομένα του πίνακα pivot. Εάν παραλείψετε αυτή τη σημαία, ο πίνακας pivot θα μετατραπεί σε στατικά δεδομένα, χάνοντας την αλληλεπιδραστικότητά του.

### Βήμα 4: Αντιγράψτε την επιθυμητή περιοχή με τον πίνακα pivot

```java
        // Copy the range A1:H20, preserving the pivot table
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);
```

Η μέθοδος `copyRange` αντιγράφει κελιά, μορφοποίηση και—λόγω των επιλογών που ορίστηκαν στο προηγούμενο βήμα—οποιονδήποτε πίνακα pivot που τέμνει την περιοχή. Αυτό είναι το βασικό στοιχείο της λειτουργίας **copy range to workbook**.

### Βήμα 5: Αποθηκεύστε το τροποποιημένο βιβλίο εργασίας

```java
        // Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Η αποθήκευση γράφει τις αλλαγές σε ένα νέο αρχείο (`output.xlsx`). Μπορείτε τώρα να ανοίξετε αυτό το αρχείο στο Excel και να δείτε ότι ο πίνακας pivot έχει αντιγραφεί ακριβώς στην περιοχή όπου έγινε η αντιγραφή.

## Πλήρες, εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα τα μέρη, εδώ είναι το πλήρες πρόγραμμα που μπορείτε να μεταγλωττίσετε και να εκτελέσετε:

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Define copy options to include the pivot table
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);

        // 3. Copy the range A1:H20 with the specified options
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);

        // 4. Save the modified workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### Αναμενόμενο αποτέλεσμα

* `output.xlsx` περιέχει τα ίδια δεδομένα με το `input.xlsx`.
* Ο πίνακας pivot που αρχικά κατείχε την πηγαία περιοχή εμφανίζεται στα κελιά προορισμού, πλήρως λειτουργικός (φίλτρα, δυνατότητα ανανέωσης κ.λπ.).
* Όλη η μορφοποίηση κελιών, οι τύποι και τα πλάτη των στηλών διατηρούνται επειδή η `copyRange` αντιγράφει ολόκληρο το μπλοκ κελιών.

## Συχνές ερωτήσεις και ειδικές περιπτώσεις

**Τι γίνεται αν η περιοχή προορισμού επικαλύπτεται με έναν υπάρχοντα πίνακα pivot;**  
Το Aspose.Cells θα αντικαταστήσει τα κελιά-στόχο. Για να αποφύγετε απώλεια δεδομένων, βεβαιωθείτε ότι η περιοχή προορισμού είναι κενή ή μετακινήστε πρώτα τον υπάρχοντα πίνακα pivot.

**Μπορώ να αντιγράψω έναν πίνακα pivot μεταξύ φύλλων εργασίας;**  
Ναι. Χρησιμοποιήστε `workbook.getWorksheets().get(targetSheetIndex).getCells().copyRange(sourceRange, copyOptions);` όπου το `targetSheetIndex` δείχνει στο φύλλο προορισμού.

**Η μέθοδος `setCopyPivotTable(true)` αντιγράφει την υποκείμενη πηγή δεδομένων;**  
Η μέθοδος αντιγράφει μόνο την αναφορά στην κρυφή μνήμη (pivot cache). Εάν τα δεδομένα προέλευσης βρίσκονται στο ίδιο βιβλίο εργασίας, ο πίνακας pivot προορισμού θα δείχνει στην ίδια κρυφή μνήμη. Για να αντιγράψετε την κρυφή μνήμη, πρέπει να δημιουργήσετε μια νέα pivot cache χειροκίνητα.

**Πώς να αντιγράψετε μια μεγάλη περιοχή αποδοτικά;**  
Κατά την αντιγραφή πολύ μεγάλων περιοχών, εξετάστε το ενδεχόμενο χρήσης `CopyOptions.setCopyFormula(true)` και `setCopyDataValidation(true)` μόνο εάν είναι απαραίτητο. Η μείωση του αριθμού των επιλογών μπορεί να βελτιώσει την απόδοση.

## Συμβουλές για αξιόπιστη χρήση **aspose.cells copy range**

* **Pro tip:** Πάντα καλέστε `workbook.calculateFormula()` μετά την αντιγραφή εάν η περιοχή περιέχει τύπους που εξαρτώνται από την κρυφή μνήμη pivot.
* **Προσοχή:** Κρυφά φύλλα εργασίας. Η `copyRange` λειτουργεί μόνο σε ορατά φύλλα εκτός εάν αναφέρετε ρητά το κρυφό φύλλο με το δείκτη του.
* **Έλεγχος έκδοσης:** Η σημαία `setCopyPivotTable` είναι διαθέσιμη από το Aspose.Cells 20.9. Βεβαιωθείτε ότι η έκδοση της βιβλιοθήκης σας την υποστηρίζει.

## Συμπέρασμα

Τώρα γνωρίζετε **how to copy pivot** στο Aspose.Cells και πώς να **copy range to workbook** διατηρώντας πλήρη λειτουργικότητα του pivot. Τα βήματα—προσθήκη της βιβλιοθήκης, φόρτωση του βιβλίου εργασίας, διαμόρφωση του `CopyOptions`, εκτέλεση της αντιγραφής και αποθήκευση—αποτελούν ένα επαναλαμβανόμενο πρότυπο που μπορείτε να προσαρμόσετε σε άλλες περιπτώσεις αντιγραφής‑επικόλλησης.

Στη συνέχεια, εξερευνήστε συναφή θέματα όπως **aspose.cells copy range** για γραφήματα, μορφοποίηση υπό όρους και επικύρωση δεδομένων. Πειραματιστείτε με την αντιγραφή μεταξύ διαφορετικών μορφών αρχείων (XLSX → XLS) για να επεκτείνετε τις δυνατότητες αυτοματοποίησής σας. Καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να δημιουργήσετε πίνακες Pivot στο Excel χρησιμοποιώντας Aspose.Cells για Java: Ένας ολοκληρωμένος οδηγός](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Πώς να ενημερώσετε την πηγή πίνακα Pivot του Excel με Aspose.Cells για Java: Ένας ολοκληρωμένος οδηγός](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Πώς να εφαρμόσετε Slicers σε πίνακες Pivot χρησιμοποιώντας Aspose.Cells για Java: Ένας ολοκληρωμένος οδηγός](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}