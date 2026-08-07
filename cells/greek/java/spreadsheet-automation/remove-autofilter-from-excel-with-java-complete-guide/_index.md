---
category: general
date: 2026-07-16
description: Αφαιρέστε το αυτόματο φίλτρο από το Excel χρησιμοποιώντας το Aspose.Cells
  σε Java. Μάθετε πώς να απενεργοποιήσετε το φίλτρο πίνακα του Excel γρήγορα και αξιόπιστα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- remove autofilter from excel
- disable excel table filter
language: el
lastmod: 2026-07-16
og_description: Αφαιρέστε αμέσως το αυτόματο φίλτρο από το Excel. Αυτό το σεμινάριο
  δείχνει πώς να απενεργοποιήσετε το φίλτρο πίνακα του Excel χρησιμοποιώντας το Aspose.Cells
  για Java.
og_image_alt: Screenshot showing remove autofilter from excel in a Java IDE
og_title: Αφαίρεση του Autofilter από το Excel με Java – Βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Remove autofilter from Excel using Aspose.Cells in Java. Learn how
    to disable Excel table filter quickly and reliably.
  headline: Remove Autofilter from Excel with Java – Complete Guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Αφαίρεση του Autofilter από το Excel με Java – Πλήρης Οδηγός
url: /el/java/spreadsheet-automation/remove-autofilter-from-excel-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αφαίρεση Autofilter από το Excel με Java – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ πώς να **αφαιρέσετε το autofilter από το Excel** χωρίς να κάνετε χειροκίνητα κλικ στη διεπαφή; Δεν είστε ο μόνος. Είτε καθαρίζετε ένα πρότυπο αναφοράς είτε προετοιμάζετε ένα βιβλίο εργασίας για διανομή, η δυνατότητα να **απενεργοποιήσετε το φίλτρο πίνακα του Excel** προγραμματιστικά εξοικονομεί χρόνο και αποτρέπει σφάλματα χρήστη.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα ένα πρακτικό, ολοκληρωμένο παράδειγμα χρησιμοποιώντας τη βιβλιοθήκη Aspose.Cells for Java. Στο τέλος θα έχετε ένα αυτόνομο πρόγραμμα Java που φορτώνει ένα βιβλίο εργασίας, βρίσκει τον πρώτο πίνακα, απενεργοποιεί το UI του φίλτρου και γράφει το αποτέλεσμα πίσω στο δίσκο.

## Προαπαιτούμενα

- Java 8 ή νεότερη εγκατεστημένη στο σύστημα σας.  
- Aspose.Cells for Java (η δωρεάν δοκιμαστική έκδοση λειτουργεί καλά για δοκιμές).  
- Βασική κατανόηση της ρύθμισης έργου Java (Maven/Gradle ή απλό .jar).  
- Ένα αρχείο Excel (`TableWithFilter.xlsx`) που ήδη περιέχει έναν πίνακα με εφαρμοσμένο AutoFilter.

> **Συμβουλή:** Αν χρησιμοποιείτε Maven, προσθέστε την ακόλουθη εξάρτηση στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

Τώρα που καλύψαμε τα βασικά, ας βουτήξουμε στον κώδικα.

## Βήμα 1: Αφαίρεση Autofilter από το Excel – Φόρτωση του Workbook

Το πρώτο που χρειαζόμαστε είναι μια παρουσία `Workbook` που δείχνει στο αρχείο προέλευσης μας. Αυτό το αντικείμενο αντιπροσωπεύει ολόκληρο το αρχείο Excel στη μνήμη.

```java
// Load the workbook that contains a table with an AutoFilter
Workbook workbook = new Workbook("YOUR_DIRECTORY/TableWithFilter.xlsx");
```

*Γιατί είναι σημαντικό:* Η φόρτωση του workbook μας δίνει πρόσβαση σε κάθε φύλλο εργασίας, πίνακα και κελί. Αν το αρχείο δεν βρεθεί, το Aspose ρίχνει μια σαφή εξαίρεση, ώστε να γνωρίζετε αμέσως ότι η διαδρομή είναι λανθασμένη.

## Βήμα 2: Πρόσβαση στο Στόχο Φύλλο Εργασίας

Τα περισσότερα υπολογιστικά φύλλα ξεκινούν με τα δεδομένα που σας ενδιαφέρουν στο πρώτο φύλλο. Τα ανακτούμε με βάση το δείκτη (από το 0).

```java
// Access the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);
```

*Τι μπορεί να πάει στραβά;* Αν το βιβλίο εργασίας σας χρησιμοποιεί διαφορετική σειρά φύλλων, απλώς αντικαταστήστε το `0` με το κατάλληλο δείκτη ή χρησιμοποιήστε `get("SheetName")`.

## Βήμα 3: Εντοπισμός του Πίνακα (ListObject)

Οι πίνακες του Excel εκτίθενται μέσω της συλλογής `ListObjects`. Πιάνουμε τον πρώτο για απλότητα.

```java
// Retrieve the first table (ListObject) on the worksheet
ListObject table = worksheet.getListObjects().get(0);
```

*Γιατί επιλέγουμε τον πρώτο πίνακα:* Σε πολλές αυτοματοποιημένες περιπτώσεις υπάρχει μόνο ένας πίνακας ανά φύλλο. Αν έχετε πολλούς, επαναλάβετε μέσω `getListObjects()` και επιλέξτε αυτόν που το όνομα του ταιριάζει με τις προσδοκίες σας.

## Βήμα 4: Απενεργοποίηση Φίλτρου Πίνακα Excel

Αυτή είναι η καρδιά του tutorial—απενεργοποίηση του UI του φίλτρου. Η μέθοδος `setShowAutoFilter` κάνει ακριβώς αυτό που χρειάζομαστε.

```java
// Disable the AutoFilter UI for the table
table.setShowAutoFilter(false);
```

*Τι κάνει αυτό:* Ο πίνακας παραμένει λειτουργικός, αλλά τα βελάκια του αναπτυσσόμενου μενού εξαφανίζονται, απενεργοποιώντας ουσιαστικά **disable excel table filter** για αυτό το φύλλο. Οι χρήστες μπορούν ακόμη να προσθέσουν φίλτρο αργότερα αν θέλουν, αλλά η προεπιλεγμένη προβολή είναι καθαρή.

## Βήμα 5: Αποθήκευση του Τροποποιημένου Workbook

Τέλος, γράψτε τις αλλαγές πίσω σε ένα νέο αρχείο. Η διατήρηση του αρχικού αμετάβλητου είναι καλή πρακτική.

```java
// Save the modified workbook without the filter UI
workbook.save("YOUR_DIRECTORY/TableNoFilter.xlsx");
```

*Επαλήθευση:* Ανοίξτε το `TableNoFilter.xlsx` στο Excel. Θα παρατηρήσετε ότι τα βελάκια φίλτρου έχουν εξαφανιστεί—η ενέργεια **remove autofilter from excel** ολοκληρώθηκε με επιτυχία.

---

![Στιγμιότυπο αφαίρεσης autofilter από το Excel](https://example.com/placeholder.png "αφαίρεση autofilter από το Excel")

*Η παραπάνω εικόνα δείχνει το βιβλίο εργασίας πριν και μετά την αφαίρεση του φίλτρου.*

## Διαχείριση Συνηθισμένων Περιπτώσεων Άκρων

| Κατάσταση                              | Πώς να Προσαρμόσετε τον Κώδικα |
|----------------------------------------|-------------------------------|
| **Πολλαπλοί πίνακες**                  | Κάντε βρόχο μέσω `worksheet.getListObjects()` και καλέστε `setShowAutoFilter(false)` σε κάθε έναν. |
| **Ο πίνακας έχει ήδη το φίλτρο απενεργοποιημένο** | Η μέθοδος είναι ιδεομετρική· η επανάκληση δεν προκαλεί καμία ζημιά. |
| **Διαφορετικό όνομα φύλλου**           | Χρησιμοποιήστε `workbook.getWorksheets().get("MySheet")` αντί για πρόσβαση με δείκτη. |
| **Μεγάλο βιβλίο εργασίας (προβλήματα μνήμης)** | Χρησιμοποιήστε τις υπερφορτώσεις του κατασκευαστή `Workbook` που διαβάζουν από `InputStream`. |

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται η πλήρης, έτοιμη προς εκτέλεση κλάση Java. Επικολλήστε την στο IDE σας, προσαρμόστε τις διαδρομές αρχείων και πατήστε **Run**.

```java
import com.aspose.cells.*;

public class RemoveTableAutoFilter {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains a table with an AutoFilter
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableWithFilter.xlsx");

        // Step 2: Access the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Retrieve the first table (ListObject) on the worksheet
        ListObject table = worksheet.getListObjects().get(0);

        // Step 4: Disable the AutoFilter UI for the table
        table.setShowAutoFilter(false);

        // Step 5: Save the modified workbook without the filter UI
        workbook.save("YOUR_DIRECTORY/TableNoFilter.xlsx");
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Η εκτέλεση του προγράμματος παράγει το `TableNoFilter.xlsx`. Ανοίγοντας το στο Excel εμφανίζεται ο πίνακας **χωρίς** τα βελάκια του αναπτυσσόμενου φίλτρου, επιβεβαιώνοντας ότι αφαιρέσαμε επιτυχώς το **remove autofilter from excel**.

## Συμπέρασμα

Μόλις δείξαμε πώς να **remove autofilter from excel** χρησιμοποιώντας το Aspose.Cells for Java, και στην πορεία μάθαμε επίσης πώς να **disable excel table filter** προγραμματιστικά. Τα βήματα είναι απλά: φόρτωση, εντοπισμός, εναλλαγή και αποθήκευση.

Αν είστε έτοιμοι να προχωρήσετε, σκεφτείτε:

- Αφαίρεση φίλτρων από **όλους** τους πίνακες σε ένα βιβλίο εργασίας.  
- Προσθήκη προσαρμοσμένου στυλ στον πίνακα μετά την αφαίρεση του φίλτρου.  
- Εξαγωγή του βιβλίου εργασίας χωρίς φίλτρο σε PDF ή CSV.

Νιώστε ελεύθεροι να πειραματιστείτε και ενημερώστε μας στα σχόλια αν αντιμετωπίσετε προβλήματα. Καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εφαρμογή AutoFilter 'Αρχίζει Με' στο Excel χρησιμοποιώντας Aspose.Cells Java](/cells/english/java/data-analysis/implement-autofilter-begins-with-aspose-cells-java/)
- [Εφαρμογή Autofilter 'Τελειώνει Με' στο Excel χρησιμοποιώντας Aspose.Cells for Java: Ένας Πλήρης Οδηγός](/cells/english/java/data-analysis/aspose-cells-java-autofilter-ends-with/)
- [Πώς να Φιλτράρετε Αποτελεσματικά Δεδομένα Κατά τη Φόρτωση Βιβλίων Εργασίας Excel Χρησιμοποιώντας Aspose.Cells σε Java](/cells/english/java/data-analysis/filter-data-excel-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}