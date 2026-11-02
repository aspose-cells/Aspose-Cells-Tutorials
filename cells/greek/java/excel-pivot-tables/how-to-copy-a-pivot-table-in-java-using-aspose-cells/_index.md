---
category: general
date: 2026-09-27
description: Αντιγραφή πίνακα Pivot σε Java με το Aspose.Cells – ένας οδηγός βήμα‑προς‑βήμα
  που δείχνει πώς να αντιγράψετε την περιοχή και να διατηρήσετε τους ορισμούς του
  pivot.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot table
- copy range aspose cells
language: el
lastmod: 2026-09-27
og_description: Αντιγραφή συγκεντρωτικού πίνακα σε Java χρησιμοποιώντας το Aspose.Cells.
  Ακολουθήστε αυτό το πλήρες σεμινάριο για να αντιγράψετε την περιοχή με το Aspose.Cells
  και να διατηρήσετε αμετάβλητους τους ορισμούς του συγκεντρωτικού πίνακα.
og_image_alt: Screenshot of copy pivot table operation in Aspose.Cells Java
og_title: Αντιγραφή πίνακα Pivot σε Java – σύντομος οδηγός Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Copy pivot table in Java with Aspose.Cells – a step‑by‑step guide that
    shows how to copy range and preserve pivot definitions.
  headline: How to copy a pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Πώς να αντιγράψετε έναν πίνακα Pivot σε Java χρησιμοποιώντας το Aspose.Cells
url: /el/java/excel-pivot-tables/how-to-copy-a-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αντιγράψετε έναν Πίνακα Pivot σε Java χρησιμοποιώντας το Aspose.Cells

Αν χρειάζεστε **αντιγραφή πίνακα pivot** από ένα βιβλίο εργασίας σε άλλο, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε με το Aspose.Cells για Java. Η λύση λειτουργεί για οποιονδήποτε πίνακα pivot έχετε δημιουργήσει και διατηρεί τον ορισμό του pivot χωρίς χειροκίνητη αναδημιουργία.

Θα μάθετε πώς να φορτώσετε το αρχικό αρχείο, να ορίσετε την περιοχή που περιέχει το pivot, να αντιγράψετε αυτήν την περιοχή σε νέο βιβλίο εργασίας και, τέλος, να αποθηκεύσετε το αποτέλεσμα. Το tutorial καλύπτει επίσης κοινά προβλήματα, όπως η διατήρηση των πηγών δεδομένων και η διαχείριση μεγάλων βιβλίων εργασίας.

## Τι θα χρειαστείτε

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Java 17 ή νεότερη (ο κώδικας συντάσσεται επίσης με JDK 8+)
* Aspose.Cells for Java 23.9 ή νεότερη – η πιο πρόσφατη έκδοση προσφέρει την πιο αξιόπιστη υποστήριξη **copy range aspose cells**
* Ένα αρχείο Excel που περιέχει πίνακα pivot (π.χ., `SourceWithPivot.xlsx`)
* Ένα IDE ή εργαλείο κατασκευής (Maven/Gradle) που μπορεί να αναφέρει το JAR του Aspose.Cells

## Βήμα 1: Φορτώστε το βιβλίο εργασίας προέλευσης που περιέχει τον πίνακα pivot

Η πρώτη ενέργεια είναι να ανοίξετε το βιβλίο εργασίας που κρατά το pivot που θέλετε να αντιγράψετε. Η φόρτωση του αρχείου δημιουργεί μια αναπαράσταση στη μνήμη όλων των φύλλων, των κελιών και των κρυφών cache του pivot.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Access the first worksheet (adjust the index if needed)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Γιατί είναι σημαντικό:**  
Το Aspose.Cells διαβάζει ολόκληρο το βιβλίο εργασίας, συμπεριλαμβανομένων των κρυφών φύλλων cache του pivot. Αν παραλείψετε αυτό το βήμα, η επόμενη λειτουργία **copy pivot table** θα χάσει την υποκείμενη πηγή δεδομένων.

## Βήμα 2: Δημιουργήστε ένα κενό βιβλίο εργασίας προορισμού

Στη συνέχεια, δημιουργήστε ένα νέο βιβλίο εργασίας που θα λάβει το αντιγραμμένο pivot. Ξεκινώντας από ένα καθαρό βιβλίο αποφεύγετε τυχαίες αντικαταστάσεις.

```java
        // Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Συμβουλή:** Το προεπιλεγμένο βιβλίο εργασίας περιέχει ένα κενό φύλλο, το οποίο είναι ιδανικό για μια απλή αντιγραφή. Αν χρειάζεται να αντιγράψετε σε συγκεκριμένο όνομα φύλλου, μετονομάστε το `destWs` με `destWs.setName("TargetSheet")`.

## Βήμα 3: Ορίστε την περιοχή προέλευσης που περιλαμβάνει τον πίνακα pivot

Ένας πίνακας pivot καταλαμβάνει ένα ορθογώνιο μπλοκ κελιών. Πρέπει να καθορίσετε την ακριβή περιοχή· διαφορετικά θα αντιγραφούν μόνο τα ακατέργαστα δεδομένα. Σε αυτό το παράδειγμα υποθέτουμε ότι το pivot καταλαμβάνει **A1:G20**, αλλά μπορείτε να προσαρμόσετε τη διεύθυνση ώστε να ταιριάζει στο αρχείο σας.

```java
        // Define the range that includes the pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Γιατί λειτουργεί:**  
Όταν καλείτε `createRange` στη συλλογή `Cells` του φύλλου, το Aspose.Cells συμπεριλαμβάνει τον ορισμό του pivot, το cache του και οποιαδήποτε μορφοποίηση. Αυτό είναι το κλειδί για το **how to copy pivot table** σωστά.

## Βήμα 4: Αντιγράψτε την ορισμένη περιοχή στο φύλλο προορισμού

Τώρα χρησιμοποιήστε τη μέθοδο `copy` για να διπλασιάσετε την περιοχή. Η μέθοδος αντιγράφει τα πάντα μέσα στην περιοχή, συμπεριλαμβανομένου του ορισμού του pivot, των τύπων και των στυλ.

```java
        // Copy the range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));
```

**Σημαντική σημείωση:**  
Αν χρειάζεστε μόνο τα δεδομένα χωρίς το pivot, μπορείτε να χρησιμοποιήσετε `srcRange.copyData`. Ωστόσο, για μια πραγματική **copy pivot table** πρέπει να αντιγράψετε ολόκληρη την περιοχή όπως φαίνεται παραπάνω.

## Βήμα 5: Αποθηκεύστε το βιβλίο εργασίας προορισμού

Τέλος, γράψτε το νέο βιβλίο εργασίας στο δίσκο. Το παραγόμενο αρχείο θα περιέχει έναν πλήρως λειτουργικό πίνακα pivot που είναι ταυτόσημος με τον πηγαίο.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

Η εκτέλεση του προγράμματος παράγει το `CopyPivotResult.xlsx` με την ίδια διάταξη pivot, φίλτρα και υπολογισμούς όπως το αρχικό αρχείο.

## Αναμενόμενο αποτέλεσμα

Όταν ανοίξετε το `CopyPivotResult.xlsx` στο Excel:

* Ο πίνακας pivot εμφανίζεται στο **A1:G20** του πρώτου φύλλου.
* Όλα τα πεδία γραμμής/στήλης, τα φίλτρα και τα πεδία τιμών παραμένουν ανέπαφα.
* Η ανανέωση του pivot ενημερώνει την ίδια πηγή δεδομένων όπως το βιβλίο εργασίας προέλευσης (αν τα δεδομένα είναι ενσωματωμένα).

## Ακραίες περιπτώσεις και πρακτικές συμβουλές

| Situation | How to handle it |
|-----------|------------------|
| **Pivot spans more columns than anticipated** | Χρησιμοποιήστε `srcWs.getPivotTables().get(0).getPivotTableArea()` για να λάβετε την ακριβή διεύθυνση προγραμματιστικά. |
| **Source workbook contains multiple pivots** | Επανάληψη μέσω `srcWs.getPivotTables()` και αντιγραφή κάθε περιοχής ξεχωριστά, προσαρμόζοντας τις διευθύνσεις προορισμού. |
| **Large workbooks cause memory pressure** | Ενεργοποιήστε `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` πριν τη φόρτωση του πηγαίου αρχείου. |
| **You need to copy only the pivot definition, not the data** | Μετά την αντιγραφή, διαγράψτε τις γραμμές δεδομένων στην προορισμένη περιοχή με `destWs.getCells().deleteRows(startRow, count)`. |
| **Destination file must keep original formatting** | Ορίστε `CopyOptions` με `options.setPasteType(PasteType.ALL)` για πλήρη αντιγραφή πιστότητας. |

**Pro tip:** Πάντα επαληθεύετε το αντιγραμμένο pivot καλώντας προγραμματιστικά `destWs.getPivotTables().get(0).refresh()`. Αυτό εξασφαλίζει ότι η cache είναι ενημερωμένη, ειδικά όταν η πηγή δεδομένων βρίσκεται σε εξωτερική σύνδεση.

## Πλήρες εκτελέσιμο παράδειγμα

Παρακάτω βρίσκεται ολόκληρο το πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο IDE σας. Αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή στο σύστημά σας.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 3: Define the range that includes the pivot table in the source sheet
        // Adjust the address if your pivot occupies a different area
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 4: Copy the defined range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

Η εκτέλεση αυτού του κώδικα θα **copy pivot table** ακριβώς όπως περιγράφηκε, και δείχνει τον πιο απλό τρόπο για **copy range aspose cells** διατηρώντας τη λειτουργικότητα του pivot.

## Συμπέρασμα

Τώρα ξέρετε πώς να **copy pivot table** σε Java χρησιμοποιώντας το Aspose.Cells, από τη φόρτωση του βιβλίου εργασίας προέλευσης μέχρι την αποθήκευση του αρχείου προορισμού. Ο οδηγός κάλυψε τα βασικά βήματα, εξήγησε γιατί κάθε βήμα είναι σημαντικό και αντιμετώπισε κοινές ακραίες περιπτώσεις.  

Στη συνέχεια, μπορείτε να εξερευνήσετε:

* **how to copy pivot table** μεταξύ διαφορετικών φύλλων εντός του ίδιου βιβλίου εργασίας
* Χρήση του **copy range aspose cells** για αντιγραφή γραφημάτων ή μορφοποίησης υπό όρους
* Αυτοματοποίηση της ανανέωσης του pivot μετά την αντιγραφή για διατήρηση των δεδομένων ενημερωμένων

Μη διστάσετε να πειραματιστείτε με μεγαλύτερες περιοχές, πολλαπλά pivots ή να ενσωματώσετε αυτή τη λογική σε ένα μεγαλύτερο pipeline επεξεργασίας Excel. Καλή προγραμματιστική!

## Τι θα πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Copy Pivot Table in Java – Preserve It, Export to PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}