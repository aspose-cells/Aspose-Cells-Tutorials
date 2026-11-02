---
category: general
date: 2026-08-20
description: Μάθετε πώς να διαγράψετε μια γραμμή πίνακα Excel με το Aspose.Cells διατηρώντας
  την ακεραιότητα του πίνακα. Αυτός ο οδηγός βήμα‑βήμα δείχνει ασφαλή διαγραφή γραμμής
  και διαχείριση σφαλμάτων.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to delete excel table row
- delete rows aspose.cells
language: el
lastmod: 2026-08-20
og_description: Πώς να διαγράψετε μια γραμμή πίνακα Excel χρησιμοποιώντας το Aspose.Cells.
  Ακολουθήστε αυτόν τον πλήρη οδηγό για να αφαιρέσετε με ασφάλεια γραμμές και να αντιμετωπίσετε
  τυχόν σφάλματα.
og_image_alt: Screenshot of Java code deleting a row from an Excel table with Aspose.Cells
og_title: Πώς να διαγράψετε μια γραμμή πίνακα Excel με το Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to delete Excel table row with Aspose.Cells while preserving
    table integrity. This step‑by‑step guide shows safe row deletion and error handling.
  headline: How to delete Excel table row safely using Aspose.Cells
  type: TechArticle
- description: Learn how to delete Excel table row with Aspose.Cells while preserving
    table integrity. This step‑by‑step guide shows safe row deletion and error handling.
  name: How to delete Excel table row safely using Aspose.Cells
  steps:
  - name: Why each step matters
    text: 1. **Load the workbook** – `Workbook` reads the `.xlsx` file into memory,
      giving you programmatic access to its sheets, tables, and cells. 2. **Access
      the worksheet** – `getWorksheets().get(0)` selects the first sheet, which is
      where the target table lives. 3. **Retrieve the table** – In Excel, a st
  - name: Expected console output
    text: '*If the deletion is allowed*:'
  - name: Deleting multiple rows
    text: 'To delete three consecutive rows starting at the second data row:'
  - name: Deleting the last data row
    text: 'Attempting to delete the final data row will also raise an exception because
      a table cannot exist without at least one data row. Handle it the same way:'
  type: HowTo
tags:
- Aspose.Cells
- Excel
- Java
title: Πώς να διαγράψετε με ασφάλεια μια γραμμή πίνακα Excel χρησιμοποιώντας το Aspose.Cells
url: /el/java/tables-structured-references/how-to-delete-excel-table-row-safely-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να διαγράψετε με ασφάλεια μια σειρά πίνακα Excel χρησιμοποιώντας το Aspose.Cells

Αν χρειάζεστε **how to delete Excel table row** χωρίς να σπάσετε τη δομή του πίνακα, αυτός ο οδηγός δείχνει μια αξιόπιστη προσέγγιση με το Aspose.Cells για Java. Θα δείτε ένα πλήρες, εκτελέσιμο παράδειγμα που εντοπίζει την εξαίρεση ασφαλείας και αποθηκεύει το βιβλίο εργασίας μετά την προσπάθεια διαγραφής.

Ο οδηγός καλύπτει επίσης **delete rows aspose.cells** με τρόπο που λειτουργεί για σενάρια μονής‑γραμμής και πολλαπλών γραμμών, ώστε να μπορείτε να προσαρμόσετε τον κώδικα στα δικά σας έργα.

## Τι καλύπτει αυτός ο οδηγός

* Φόρτωση ενός υπάρχοντος βιβλίου εργασίας που περιέχει έναν πίνακα Excel (ListObject).  
* Πρόσβαση στο πρώτο φύλλο εργασίας και στον πρώτο πίνακα σε αυτό το φύλλο.  
* Προσπάθεια διαγραφής μιας γραμμής ενώ το Aspose.Cells επικυρώνει τη λειτουργία.  
* Διαχείριση της εξαίρεσης που ρίχνει το Aspose.Cells όταν η διαγραφή θα διαφθάσει τον πίνακα.  
* Αποθήκευση του βιβλίου εργασίας μετά από μια ασφαλή προσπάθεια διαγραφής.  

Απαιτήσεις: Java 17 ή νεότερη, Aspose.Cells for Java (έκδοση 23.12 ή νεότερη) και βασική κατανόηση της σύνταξης της Java. Δεν απαιτούνται πρόσθετες βιβλιοθήκες.

---

## Πώς να διαγράψετε μια σειρά πίνακα Excel με το Aspose.Cells

Παρακάτω βρίσκεται το πλήρες, αυτόνομο πρόγραμμα. Κάθε βήμα εξηγείται και ο κώδικας μπορεί να αντιγραφεί σε ένα έργο Java και να εκτελεστεί αμέσως.

```java
import com.aspose.cells.*;

public class SafeTableDeletion {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the workbook containing the table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Retrieve the first table (ListObject) on the worksheet
        ListObject table = worksheet.getListObjects().get(0);

        // Step 4: Attempt to delete a row that would break the table structure
        //         The operation is wrapped in a try‑catch to demonstrate the safety check
        try {
            // Row index is zero‑based; this tries to delete the third data row.
            table.deleteRows(2, 1);
            System.out.println("Row deleted successfully.");
        } catch (Exception ex) {
            // Aspose.Cells throws an exception if the deletion would leave the table invalid.
            System.out.println("Partial‑deletion prevented: " + ex.getMessage());
        }

        // Step 5: Save the workbook after the safe‑deletion attempt
        workbook.save("YOUR_DIRECTORY/TableSafeDelete.xlsx");
    }
}
```

### Γιατί είναι σημαντικό κάθε βήμα

1. **Load the workbook** – `Workbook` διαβάζει το αρχείο `.xlsx` στη μνήμη, παρέχοντάς σας προγραμματική πρόσβαση στα φύλλα, τους πίνακες και τα κελιά του.  
2. **Access the worksheet** – `getWorksheets().get(0)` επιλέγει το πρώτο φύλλο, όπου βρίσκεται ο στόχος πίνακας.  
3. **Retrieve the table** – Στο Excel, ένας δομημένος πίνακας αντιπροσωπεύεται από ένα `ListObject`. Αυτό το αντικείμενο παρέχει μεθόδους όπως `deleteRows`.  
4. **Safe deletion** – `deleteRows` ελέγχει την ακεραιότητα του πίνακα. Εάν η αφαίρεση της γραμμής θα σπάσει τον πίνακα (π.χ., αφήνοντας μια κεφαλίδα χωρίς δεδομένα), το Aspose.Cells ρίχνει μια εξαίρεση. Το μπλοκ `try‑catch` δείχνει τη διαχείριση ασφαλείας **delete rows aspose.cells**.  
5. **Save the workbook** – `workbook.save` γράφει τις αλλαγές στο δίσκο, δημιουργώντας ένα νέο αρχείο που αντανακλά την προσπάθεια διαγραφής.

### Αναμενόμενη έξοδος κονσόλας

*Αν η διαγραφή επιτραπεί*:

```
Row deleted successfully.
```

*Αν η διαγραφή θα διαφθάσει τον πίνακα* (συνηθισμένο όταν ο πίνακας έχει μόνο μία γραμμή δεδομένων απομένει):

```
Partial‑deletion prevented: Deleting the specified rows would break the table structure.
```

---

## Φόρτωση του βιβλίου εργασίας (βήμα 1)

Ο κατασκευαστής `Workbook` δέχεται μια διαδρομή αρχείου. Βεβαιωθείτε ότι η διαδρομή δείχνει σε ένα υπάρχον αρχείο Excel που περιέχει τουλάχιστον έναν πίνακα. Εάν το αρχείο λείπει, το Aspose.Cells ρίχνει `FileNotFoundException`, το οποίο μπορείτε να εντοπίσετε παρόμοια με την εξαίρεση διαγραφής πίνακα.

```java
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

**Συμβουλή:** Χρησιμοποιήστε απόλυτη διαδρομή κατά την ανάπτυξη για να αποφύγετε τη σύγχυση σχετικών διαδρομών, ειδικά όταν εκτελείτε από ένα IDE.

---

## Πρόσβαση στο φύλλο εργασίας (βήμα 2)

Ένα βιβλίο εργασίας μπορεί να περιέχει πολλά φύλλα εργασίας. Το παράδειγμα χρησιμοποιεί το πρώτο (`index 0`). Εάν χρειάζεστε ένα συγκεκριμένο φύλλο με όνομα, αντικαταστήστε την κλήση με:

```java
Worksheet worksheet = workbook.getWorksheets().get("SheetName");
```

---

## Ανάκτηση του πίνακα (βήμα 3)

`ListObject` αντιπροσωπεύει έναν πίνακα Excel. Εάν το φύλλο εργασίας δεν έχει πίνακες, το `getListObjects().size()` επιστρέφει `0`, και η κλήση `get(0)` θα προκαλέσει `IndexOutOfBoundsException`. Μια προφυλακτική έλεγχος φαίνεται ως εξής:

```java
if (worksheet.getListObjects().getCount() == 0) {
    System.out.println("No tables found on the worksheet.");
    return;
}
ListObject table = worksheet.getListObjects().get(0);
```

---

## Διαγραφή γραμμών χρησιμοποιώντας το Aspose.Cells (βήμα 4)

Ο πυρήνας του **how to delete Excel table row** είναι η μέθοδος `deleteRows`:

```java
table.deleteRows(startIndex, count);
```

* `startIndex` – δείκτης μηδενικής βάσης της πρώτης γραμμής προς διαγραφή εντός της περιοχής δεδομένων του πίνακα.  
* `count` – αριθμός γραμμών προς αφαίρεση.

Το Aspose.Cells επικυρώνει τη λειτουργία σε σχέση με την κεφαλίδα του πίνακα, τις συνολικές γραμμές και τυχόν τύπους που αναφέρονται στον πίνακα. Εάν η διαγραφή θα αφήσει τον πίνακα σε μη έγκυρη κατάσταση, ρίχνεται εξαίρεση, γι' αυτό το πρότυπο `try‑catch` είναι ουσιώδες.

### Διαγραφή πολλαπλών γραμμών

Για να διαγράψετε τρεις διαδοχικές γραμμές ξεκινώντας από τη δεύτερη γραμμή δεδομένων:

```java
table.deleteRows(1, 3);
```

### Διαγραφή της τελευταίας γραμμής δεδομένων

Η προσπάθεια διαγραφής της τελευταίας γραμμής δεδομένων θα προκαλέσει επίσης εξαίρεση επειδή ένας πίνακας δεν μπορεί να υπάρχει χωρίς τουλάχιστον μία γραμμή δεδομένων. Διαχειριστείτε το με τον ίδιο τρόπο:

```java
try {
    table.deleteRows(table.getDataRows().getCount() - 1, 1);
} catch (Exception ex) {
    System.out.println("Cannot delete the last row: " + ex.getMessage());
}
```

---

## Αποθήκευση του βιβλίου εργασίας (βήμα 5)

Μετά την ασφαλή προσπάθεια διαγραφής, η αποθήκευση των αλλαγών είναι απλή:

```java
workbook.save("YOUR_DIRECTORY/TableSafeDelete.xlsx");
```

Μπορείτε να επιλέξετε οποιαδήποτε υποστηριζόμενη μορφή (`.xlsx`, `.xls`, `.csv`, κ.λπ.) αλλάζοντας την επέκταση του αρχείου.

---

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Pitfall | Why it happens | Fix |
|---------|----------------|-----|
| **Δεν υπάρχει πίνακας στο φύλλο** | `getListObjects().get(0)` ρίχνει `IndexOutOfBoundsException`. | Ελέγξτε `getCount()` πριν την πρόσβαση. |
| **Λάθος δείκτης γραμμής** | `deleteRows` χρησιμοποιεί δείκτη μηδενικής βάσης σε σχέση με τον πίνακα, όχι με το φύλλο εργασίας. | Επιβεβαιώστε το δείκτη εκτυπώνοντας `table.getDataRows().getCount()`. |
| **Διαγραφή της μοναδικής γραμμής δεδομένων** | Το Aspose.Cells προστατεύει την ακεραιότητα του πίνακα και ρίχνει εξαίρεση. | Είτε προσθέστε πρώτα μια γραμμή placeholder είτε αποφασίστε να αφαιρέσετε ολόκληρο τον πίνακα με `table.remove()`. |
| **Προβλήματα διαδρομής αρχείου** | Οι σχετικές διαδρομές μπορεί να λυθούν στον κατάλογο εργασίας του IDE, προκαλώντας `FileNotFoundException`. | Χρησιμοποιήστε απόλυτες διαδρομές ή ρυθμίστε τον κατάλογο εργασίας του IDE. |

---

## Συνοπτικό παράδειγμα πλήρους λειτουργίας

Παρακάτω βρίσκεται ολόκληρο το πρόγραμμα ξανά για γρήγορη αντιγραφή‑επικόλληση. Περιλαμβάνει τους προφυλακτικούς ελέγχους που συζητήθηκαν νωρίτερα.

```java
import com.aspose.cells.*;

public class SafeTableDeletion {
    public static void main(String[] args) throws Exception {

        // Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Ensure a table exists
        if (worksheet.getListObjects().getCount() == 0) {
            System.out.println("No tables found on the worksheet.");
            return;
        }

        // Retrieve the first table
        ListObject table = worksheet.getListObjects().get(0);

        // Attempt safe deletion
        try {
            table.deleteRows(2, 1); // zero‑based index
            System.out.println("Row deleted successfully.");
        } catch (Exception ex) {
            System.out.println("Partial‑deletion prevented: " + ex.getMessage());
        }

        // Save the result
        workbook.save("YOUR_DIRECTORY/TableSafeDelete.xlsx");
    }
}
```

Η εκτέλεση αυτού του προγράμματος εκτυπώνει είτε ένα μήνυμα επιτυχίας είτε το προστατευτικό μήνυμα εξαίρεσης, και στη συνέχεια γράφει το `TableSafeDelete.xlsx` στον καθορισμένο φάκελο.

---

## Συμπέρασμα

Τώρα ξέρετε **how to delete Excel table row** με ασφάλεια χρησιμοποιώντας το Aspose.Cells για Java. Ο οδηγός έδειξε τη φόρτωση ενός βιβλίου εργασίας, την εντόπιση ενός πίνακα, την εκτέλεση μιας προστατευμένης διαγραφής γραμμής, τη διαχείριση της εξαίρεσης ασφαλείας **delete rows aspose.cells**, και την αποθήκευση του ενημερωμένου αρχείου.

Από εδώ μπορείτε να:

* Διαγράψετε πολλαπλές γραμμές με μία κλήση.  
* Επανάληψη πάνω σε μια λίστα δεικτών γραμμών για εκτέλεση μαζικών διαγραφών.  
* Αντικαταστήσετε το `try‑catch` με προσαρμοσμένη καταγραφή για περιβάλλοντα παραγωγής.  

Πειραματιστείτε με διαφορετικές διατάξεις πινάκων, τύπους και κανόνες επικύρωσης δεδομένων για να δείτε πώς το Aspose.Cells επιβάλλει την ακεραιότητα. Όταν χρειάζεται να χειριστείτε αρχεία Excel προγραμματιστικά, το μοτίβο που παρουσιάστηκε εδώ παρέχει μια σταθερή, σφαλμα‑συνειδητή βάση.

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικό θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Insert and Delete Rows in Excel with Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [How to Delete Blank Rows in Excel Using Aspose.Cells .NET for Data Cleanup](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)
- [How to Delete a Column in Excel Using Aspose.Cells .NET in C# - A Comprehensive Guide](/cells/english/net/worksheet-management/delete-column-aspose-cells-dotnet-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}