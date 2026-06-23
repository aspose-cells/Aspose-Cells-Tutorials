---
category: general
date: 2026-06-18
description: Διαγραφή γραμμών σε φύλλο εργασίας χρησιμοποιώντας το Aspose.Cells για
  Java. Μάθετε πώς να αφαιρέσετε τη γραμμή κεφαλίδας του πίνακα και να διαγράψετε
  γραμμές από τον πίνακα Excel με ασφάλεια.
draft: false
keywords:
- delete rows in worksheet
- remove table header row
- remove rows from excel table
language: el
og_description: Διαγραφή γραμμών σε φύλλο εργασίας με το Aspose.Cells για Java. Αυτός
  ο οδηγός δείχνει πώς να αφαιρέσετε τη γραμμή κεφαλίδας του πίνακα και να διαγράψετε
  γραμμές από έναν πίνακα Excel αποδοτικά.
og_title: Διαγραφή γραμμών σε φύλλο εργασίας με Java – Βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Delete rows in worksheet using Aspose.Cells for Java. Learn how to
    remove table header row and delete rows from Excel table safely.
  headline: Delete rows in worksheet with Java – Complete Guide
  type: TechArticle
- description: Delete rows in worksheet using Aspose.Cells for Java. Learn how to
    remove table header row and delete rows from Excel table safely.
  name: Delete rows in worksheet with Java – Complete Guide
  steps:
  - name: '`table.unlist()` strips the table metadata, turning the block into ordinary
      cells.'
    text: '`table.unlist()` strips the table metadata, turning the block into ordinary
      cells.'
  - name: With the header now a regular row, `deleteRows(0, …)` works without complaints.
    text: With the header now a regular row, `deleteRows(0, …)` works without complaints.
  - name: If you still need a table after the cleanup, you can recreate it using `ws.getTables().add(...)`.
    text: If you still need a table after the cleanup, you can recreate it using `ws.getTables().add(...)`.
  - name: Loads a workbook.
    text: Loads a workbook.
  - name: Checks if the first table exists.
    text: Checks if the first table exists.
  - name: Deletes **all** rows *including* the header safely.
    text: Deletes **all** rows *including* the header safely.
  - name: Re‑creates the table from the remaining rows (if any).
    text: Re‑creates the table from the remaining rows (if any).
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Worksheet
title: Διαγραφή γραμμών σε φύλλο εργασίας με Java – Πλήρης οδηγός
url: /el/java/worksheet-management/delete-rows-in-worksheet-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Διαγραφή γραμμών σε φύλλο εργασίας – Πλήρες Java Tutorial

Έχετε χρειαστεί ποτέ να **διαγράψετε γραμμές σε φύλλο εργασίας** αλλά να συναντήσετε εμπόδιο επειδή η κεφαλίδα του πίνακα αρνείται να κινηθεί; Δεν είστε οι μόνοι. Σε πολλές περιπτώσεις αυτοματοποίησης του Excel η πρώτη γραμμή ανήκει σε έναν δομημένο πίνακα, και μια αφελής κλήση στο `deleteRows` ρίχνει μια εξαίρεση ή απλώς αφήνει την κεφαλίδα αμετάβλητη.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα πώς να *αφαιρέσετε τη γραμμή κεφαλίδας του πίνακα* και *αφαιρέσετε γραμμές από πίνακα Excel* χωρίς να καταστρέψετε το φύλλο. Στο τέλος θα έχετε ένα καθαρό, εκτελέσιμο snippet που λειτουργεί με την πιο πρόσφατη έκδοση του Aspose.Cells for Java (v23.10 τη στιγμή της συγγραφής).

Θα καλύψουμε προαπαιτούμενα, τρεις πρακτικές προσεγγίσεις και μερικές συμβουλές που θα θέλετε να αποθηκεύσετε. Χωρίς περιττές πληροφορίες — μόνο η απάντηση που θα περιμένατε από έναν έμπειρο προγραμματιστή με έναν καφέ.

## Προαπαιτούμενα

Πριν βουτήξουμε, βεβαιωθείτε ότι έχετε:

- Java 17 ή νεότερη (ο κώδικας μεταγλωττίζεται με παλαιότερες εκδόσεις, αλλά συνιστάται η 17).
- Aspose.Cells for Java 23.10 ή νεότερη προστεθεί στο Maven `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
</dependency>
```

- Ένα δείγμα αρχείου Excel (`Sample.xlsx`) που περιέχει έναν πίνακα στο πρώτο φύλλο εργασίας. Η κεφαλίδα του πίνακα βρίσκεται στη γραμμή 0 (γραμμή Excel 1).

Αυτό είναι όλο. Έτοιμοι; Ας ξεκινήσουμε.

## Διαγραφή γραμμών σε φύλλο εργασίας – γιατί η γραμμή κεφαλίδας μετρά

Όταν καλείτε:

```java
ws.getCells().deleteRows(0, 2, true);
```

Το Aspose.Cells αρνείται να διαγράψει τη γραμμή 0 επειδή είναι μέρος ενός **πίνακα**. Το API προστατεύει την ακεραιότητα του πίνακα· η αφαίρεση της κεφαλίδας θα άφηνε τις γραμμές δεδομένων ορφανά. Η εξαίρεση που θα δείτε είναι κάτι σαν *«Η καθορισμένη γραμμή ανήκει σε πίνακα και δεν μπορεί να διαγραφεί.»*  

Η κατανόηση αυτού του περιορισμού είναι το πρώτο βήμα για μια επιτυχημένη λύση.

## Προσέγγιση 1 – Διαγραφή γραμμών **κάτω** από την κεφαλίδα (το πιο κοινό)

Αν απλώς θέλετε να εκκαθαρίσετε τα δεδομένα διατηρώντας τη δομή του πίνακα, ξεκινήστε τη διαγραφή από τη γραμμή **μετά** την κεφαλίδα.

```java
import com.aspose.cells.*;

public class DeleteRowsBelowHeader {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook wb = new Workbook("Sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);

        // Determine how many data rows the table currently has
        Table table = ws.getTables().get(0);
        int dataRowCount = table.getDataRange().getRowCount();

        // Delete all data rows (keep header)
        // startRow = 1 because row index 0 is the header
        ws.getCells().deleteRows(1, dataRowCount, true);

        // Save the result
        wb.save("Result_DeleteRowsBelowHeader.xlsx");
    }
}
```

**Γιατί λειτουργεί:** `deleteRows` λαμβάνει ως αρχικό δείκτη το 1, έτσι η κεφαλίδα παραμένει αμετάβλητη. Η σημαία `true` μετατοπίζει τις υπόλοιπες γραμμές προς τα πάνω, διατηρώντας τυχόν τύπους που τις αναφέρονται. Μετά την εκτέλεση του κώδικα θα δείτε έναν καθαρό πίνακα με μόνο τη γραμμή κεφαλίδας.

### Γρήγορη συμβουλή

Αν χρειαστεί να διαγράψετε ένα *συγκεκριμένο* εύρος γραμμών (π.χ. γραμμές 5‑10), απλώς προσαρμόστε τον αρχικό δείκτη και τον αριθμό ανάλογα. Ο πίνακας θα αλλάξει αυτόματα μέγεθος ώστε να ταιριάζει με το νέο εύρος δεδομένων.

## Προσέγγιση 2 – Μετατροπή του πίνακα σε απλό εύρος, έπειτα διαγραφή

Μερικές φορές χρειάζεται πραγματικά να **αφαιρέσετε τη γραμμή κεφαλίδας του πίνακα** και να αντιμετωπίσετε τα δεδομένα ως κανονικό εύρος. Το κόλπο είναι να *unlist* πρώτα τον πίνακα.

```java
import com.aspose.cells.*;

public class RemoveHeaderAndDeleteRows {
    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("Sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Table table = ws.getTables().get(0);

        // 1️⃣ Unlist the table – it becomes a normal range
        table.unlist();

        // 2️⃣ Now you can delete the header row (row 0) and any other rows
        // Delete header + first two data rows (total 3 rows)
        ws.getCells().deleteRows(0, 3, true);

        // 3️⃣ (Optional) Re‑create a table from the remaining data
        // Assuming you still have data starting at row 0
        int firstDataRow = 0;
        int lastDataRow = ws.getCells().getMaxDataRow();
        int firstCol = ws.getCells().getMaxDataColumn();
        int lastCol = ws.getCells().getMaxDataColumn();

        String range = new CellArea(firstDataRow, 0, lastDataRow, firstCol).format();
        ws.getTables().add(range, true);
        ws.getTables().get(0).setName("NewTable");

        wb.save("Result_RemoveHeaderAndDeleteRows.xlsx");
    }
}
```

**Εξήγηση:**  

1. `table.unlist()` αφαιρεί τα μεταδεδομένα του πίνακα, μετατρέποντας το μπλοκ σε κανονικά κελιά.  
2. Με τη κεφαλίδα πλέον ως κανονική γραμμή, το `deleteRows(0, …)` λειτουργεί χωρίς προβλήματα.  
3. Αν χρειάζεστε ξανά πίνακα μετά τον καθαρισμό, μπορείτε να τον δημιουργήσετε ξανά με `ws.getTables().add(...)`.

Αυτή η προσέγγιση είναι χρήσιμη όταν η ίδια η κεφαλίδα είναι λανθασμένη ή θέλετε να αντικαταστήσετε ολόκληρο τον ορισμό του πίνακα.

## Προσέγγιση 3 – Χρήση του Table API για διαγραφή συγκεκριμένων γραμμών

Το Aspose.Cells προσφέρει επίσης μια **μεθόδο επιπέδου πίνακα** για διαγραφή γραμμών, η οποία διαχειρίζεται αυτόματα την προστασία της κεφαλίδας.

```java
import com.aspose.cells.*;

public class DeleteRowsViaTableAPI {
    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("Sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Table table = ws.getTables().get(0);

        // Delete the first two data rows (index 0 = first data row, not the header)
        // The Table API counts only data rows, so we don't touch the header.
        table.deleteRows(0, 2);

        wb.save("Result_DeleteRowsViaTableAPI.xlsx");
    }
}
```

**Γιατί μπορεί να την επιλέξετε:** Είναι ο πιο *σημασιολογικός* τρόπος — λέτε στον πίνακα, «αφαιρέστε τις γραμμές δεδομένων μου». Το API ενημερώνει αυτόματα το εύρος του πίνακα και δεν χρειάζεται να παίζετε με ακατέργαστους δείκτες γραμμών.

## Ακραίες Περιπτώσεις & Συνηθισμένα Πιθανά Σφάλματα

| Κατάσταση | Τι πρέπει να προσέξετε | Προτεινόμενη διόρθωση |
|-----------|------------------------|-----------------------|
| **Πολλοί πίνακες στο ίδιο φύλλο** | `ws.getTables().get(0)` μπορεί να στοχεύει τον λάθος πίνακα. | Χρησιμοποιήστε `ws.getTables().stream().filter(t -> t.getName().equals("MyTable")).findFirst().orElse(null)` |
| **Συγχωνευμένα κελιά στην κεφαλίδα** | Η διαγραφή γραμμών μπορεί να χωρίσει τις συγχωνευμένες περιοχές, προκαλώντας προβλήματα διάταξης. | Αποσυγχωνεύστε πριν τη διαγραφή: `ws.getCells().get("A1").getMergedRange().unmerge();` |
| **Τύποι που αναφέρονται στην κεφαλίδα** | Η αφαίρεση της κεφαλίδας διακόπτει τις εξωτερικές αναφορές. | Ενημερώστε τους τύπους μετά τη διαγραφή ή διατηρήστε μια γραμμή κράτησης. |
| **Μεγάλα φύλλα εργασίας (>10 000 γραμμές)** | `deleteRows` μπορεί να είναι πιο αργό λόγω εσωτερικής μετατόπισης. | Χρησιμοποιήστε `ws.getCells().clearRows(start, count)` εάν δεν χρειάζεται μετατόπιση. |

## Πλήρες Παράδειγμα Εργασίας – Συνδυάστε το Καλύτερο από Όλα τα Κόσμε

Παρακάτω υπάρχει ένα αυτόνομο πρόγραμμα που:

1. Φορτώνει ένα βιβλίο εργασίας.
2. Ελέγχει αν υπάρχει ο πρώτος πίνακας.
3. Διαγράφει **όλες** τις γραμμές *συμπεριλαμβανομένης* της κεφαλίδας με ασφάλεια.
4. Ξαναδημιουργεί τον πίνακα από τις υπόλοιπες γραμμές (αν υπάρχουν).

```java
import com.aspose.cells.*;

public class DeleteRowsInWorksheetFullDemo {
    public static void main(String[] args) throws Exception {
        // ① Load the workbook
        Workbook wb = new Workbook("Sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);

        // ② Guard: make sure a table is present
        if (ws.getTables().getCount() == 0) {
            System.out.println("No tables found – nothing to delete.");
            return;
        }

        // ③ Grab the first table (adjust if you have a named table)
        Table table = ws.getTables().get(0);

        // ④ Unlist so we can delete the header row
        table.unlist();

        // ⑤ Determine total rows to delete (header + data)
        int totalRows = table.getRange().getRowCount(); // includes header
        ws.getCells().deleteRows(0, totalRows, true);

        // ⑥ If there are still rows left, rebuild the table
        int maxRow = ws.getCells().getMaxDataRow();
        int maxCol = ws.getCells().getMaxDataColumn();

        if (maxRow >= 0) { // there is at least one row left
            String newRange = new CellArea(0, 0, maxRow, maxCol).format();
            Table newTable = ws.getTables().add(newRange, true);
            newTable.setName("RebuiltTable");
        }

        // ⑦ Save the result
        wb.save("Result_DeleteRowsInWorksheetFullDemo.xlsx");
        System.out.println("Rows deleted and table rebuilt successfully.");
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Μετά την εκτέλεση θα βρείτε το `Result_DeleteRowsInWorksheetFullDemo.xlsx` με τον αρχικό πίνακα αφαιρεμένο, και — αν επιβίωσε κάποιο δεδομένο — έναν νέο πίνακα που ονομάζεται `RebuiltTable`. Η κονσόλα εκτυπώνει ένα σύντομο μήνυμα επιτυχίας.

## Οπτική Σύνοψη

![Excel worksheet before and after deleting rows](https://example.com/images/delete-rows-workbook.png "Before and after deleting rows in worksheet")

*Alt text:* “Πριν και μετά τη διαγραφή γραμμών σε φύλλο εργασίας – η κεφαλίδα αφαιρέθηκε, οι γραμμές δεδομένων εκκαθαρίστηκαν.”

## Συμπέρασμα

Καλύψαμε τρεις αξιόπιστους τρόπους για **διαγραφή γραμμών σε φύλλο εργασίας** ενώ αντιμετωπίζουμε το δύσκολο σενάριο *αφαίρεσης γραμμής κεφαλίδας πίνακα* και ασφαλώς **αφαιρούμε γραμμές από πίνακα Excel**. Είτε προτιμάτε άμεσες λειτουργίες κελιών, το Table API, ή έναν πλήρη κύκλο unlist‑relist, τα παραπάνω snippets είναι έτοιμα να ενσωματωθούν στο έργο σας.

Τι θα πρέπει να μάθετε στη σύντομη επόμενη;

Οι παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Αποτελεσματική Διαχείριση Γραμμών σε Excel με Aspose.Cells for Java: Εισαγωγή και Διαγραφή Γραμμών](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)
- [Πώς να Αφαιρέσετε Κενές Γραμμές από Αρχεία Excel χρησιμοποιώντας Aspose.Cells for Java](/cells/english/java/data-manipulation/delete-blank-rows-aspose-cells-java/)
- [Πώς να Διαγράψετε Γραμμές σε Excel Χρησιμοποιώντας Aspose.Cells for Java | Οδηγός & Tutorial](/cells/english/java/worksheet-management/delete-row-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}