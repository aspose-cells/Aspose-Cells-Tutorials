---
category: general
date: 2026-10-20
description: Μάθετε πώς να αντιγράψετε έναν πίνακα Pivot χρησιμοποιώντας το Aspose.Cells
  σε Java. Αυτό το σεμινάριο δείχνει πώς να αντιγράψετε μια περιοχή σε νέο φύλλο και
  να αντιγράψετε με ασφάλεια το φύλλο του πίνακα Pivot.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new sheet
- duplicate pivot table sheet
language: el
lastmod: 2026-10-20
og_description: Πώς να αντιγράψετε έναν συγκεντρωτικό πίνακα με το Aspose.Cells σε
  Java. Ακολουθήστε αυτόν τον οδηγό για να αντιγράψετε την περιοχή σε νέο φύλλο και
  να διπλασιάσετε το φύλλο του συγκεντρωτικού πίνακα χωρίς να χάσετε δεδομένα.
og_image_alt: Screenshot showing how to copy pivot table from one worksheet to another
  in a Java program
og_title: Πώς να αντιγράψετε έναν συγκεντρωτικό πίνακα σε Java – πλήρης οδηγός Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  headline: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  name: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Load the workbook that holds the original pivot table.
    text: Load the workbook that holds the original pivot table.
  - name: Identify the exact range that includes the pivot table.
    text: Identify the exact range that includes the pivot table.
  - name: Create a new worksheet that will receive the copied data.
    text: Create a new worksheet that will receive the copied data.
  - name: Use the `Range.copy` method to transfer the range to the new sheet.
    text: Use the `Range.copy` method to transfer the range to the new sheet.
  - name: Save the workbook to a new file.
    text: Save the workbook to a new file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Πώς να αντιγράψετε πίνακα Pivot σε Java με το Aspose.Cells – οδηγός βήμα‑προς‑βήμα
url: /el/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-with-aspose-cells-step-by-st/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αντιγράψετε έναν πίνακα Pivot σε Java με Aspose.Cells – βήμα‑βήμα οδηγός

Αν χρειάζεστε **πώς να αντιγράψετε έναν πίνακα Pivot** σε μια εφαρμογή Java, αυτός ο οδηγός σας καθοδηγεί βήμα προς βήμα. Είτε δημιουργείτε μια μηχανή αναφορών είτε αυτοματοποιείτε τη μεταφορά δεδομένων, θα δείτε πώς να αντιγράψετε μια περιοχή σε νέο φύλλο διατηρώντας τον ορισμό και τα δεδομένα του πίνακα Pivot.

Η αντιγραφή ενός πίνακα Pivot μπορεί να φαίνεται επικίνδυνη επειδή η υποκείμενη cache και οι ρυθμίσεις πεδίων συχνά χάνονται. Αυτό το tutorial παρουσιάζει μια αξιόπιστη προσέγγιση χρησιμοποιώντας Aspose.Cells, δείχνει τον πλήρη εκτελέσιμο κώδικα και εξηγεί γιατί κάθε γραμμή είναι σημαντική. Στο τέλος, θα μπορείτε να διπλασιάζετε το φύλλο του πίνακα Pivot σε δευτερόλεπτα.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Java 8 ή νεότερη εγκατεστημένη.
* Aspose.Cells for Java (έκδοση 23.10 ή νεότερη) προστεθειμένη στο classpath του έργου σας.
* Ένα πηγαίο βιβλίο εργασίας (`source.xlsx`) που περιέχει έναν πίνακα Pivot στην περιοχή `A1:G20`.
* Βασική εξοικείωση με τις έννοιες της Java και του Excel.

Δεν απαιτούνται πρόσθετες βιβλιοθήκες· το Aspose.Cells διαχειρίζεται όλες τις λειτουργίες του Excel εσωτερικά.

## Πώς να αντιγράψετε έναν πίνακα Pivot – γενική στρατηγική

Η βασική ιδέα είναι απλή:

1. Φορτώστε το βιβλίο εργασίας που περιέχει τον αρχικό πίνακα Pivot.
2. Προσδιορίστε την ακριβή περιοχή που περιλαμβάνει τον πίνακα Pivot.
3. Δημιουργήστε ένα νέο φύλλο εργασίας που θα λάβει τα αντίγραφα δεδομένων.
4. Χρησιμοποιήστε τη μέθοδο `Range.copy` για να μεταφέρετε την περιοχή στο νέο φύλλο.  
   Αυτή η μέθοδος αντιγράφει αυτόματα την cache του Pivot, ώστε ο πίνακας Pivot να παραμείνει λειτουργικός.
5. Αποθηκεύστε το βιβλίο εργασίας σε νέο αρχείο.

Επειδή η λειτουργία αντιγραφής δουλεύει σε επίπεδο περιοχής, το **αντιγραμμένο φύλλο πίνακα Pivot** διατηρεί όλες τις ρυθμίσεις πεδίων, τα φίλτρα και τα υπολογιζόμενα στοιχεία.

## Βήμα 1: Φόρτωση του πηγαίου βιβλίου εργασίας

```java
// Import Aspose.Cells classes
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
```

*Γιατί είναι σημαντικό*: Η φόρτωση του βιβλίου εργασίας σας δίνει πρόσβαση στα φύλλα, τα κελιά και την cache του Pivot. Το Aspose.Cells διαβάζει ολόκληρο το αρχείο στη μνήμη, ώστε οι επόμενες λειτουργίες να είναι γρήγορες και thread‑safe.

## Βήμα 2: Ορισμός της πηγαίας περιοχής που περιέχει τον πίνακα Pivot

```java
        // Locate the first worksheet (index 0) and create a range covering the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)               // first sheet
                                    .getCells()
                                    .createRange("A1:G20"); // adjust if your pivot table is larger
```

*Γιατί είναι σημαντικό*: Η κλήση `createRange` λέει στο Aspose.Cells ακριβώς ποια κελιά να αντιγράψει. Η συμπερίληψη ολόκληρης της περιοχής του πίνακα Pivot εξασφαλίζει ότι οι κρυφές γραμμές cache μεταφέρονται επίσης. Αν παραλείψετε οποιοδήποτε τμήμα της cache, ο αντιγραμμένος πίνακας Pivot θα εμφανιστεί κενός.

## Βήμα 3: Προσθήκη φύλλου προορισμού για τα αντίγραφα δεδομένων

```java
        // Add a new worksheet that will hold the duplicated pivot table
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");
```

*Γιατί είναι σημαντικό*: Η προσθήκη ενός αφιερωμένου φύλλου απομονώνει τον αντιγραμμένο πίνακα Pivot από το αρχικό, καθιστώντας εύκολο το σύγκριση των αποτελεσμάτων ή τη χρήση του φύλλου ως πρότυπο για περαιτέρω επεξεργασία.

## Βήμα 4: Αντιγραφή της περιοχής στο φύλλο προορισμού (ο πίνακας Pivot διατηρείται)

```java
        // Copy the defined range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

*Γιατί είναι σημαντικό*: Η μέθοδος `copy` όχι μόνο αντιγράφει τις τιμές και τη μορφοποίηση των κελιών, αλλά επίσης αναπαράγει την cache του Pivot. Αυτό είναι το κλειδί που σας επιτρέπει να **αντιγράψετε το φύλλο πίνακα Pivot** χωρίς να χάσετε λειτουργικότητα.

## Βήμα 5: Αποθήκευση του βιβλίου εργασίας με την αντιγραμμένη περιοχή

```java
        // Persist the workbook to a new file
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

*Γιατί είναι σημαντικό*: Η αποθήκευση δημιουργεί ένα νέο αρχείο Excel (`result.xlsx`) που περιέχει τόσο το αρχικό όσο και το διπλότυπο φύλλο πίνακα Pivot. Μπορείτε τώρα να ανοίξετε το αρχείο στο Excel για να επαληθεύσετε ότι ο πίνακας Pivot λειτουργεί ακριβώς όπως πριν.

## Πλήρες, εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα τα παραπάνω, ορίστε το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο IDE σας:

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1. Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // 2. Define the source range that contains the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)
                                    .getCells()
                                    .createRange("A1:G20");

        // 3. Add a destination worksheet for the copied data
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");

        // 4. Copy the range to the destination worksheet (pivot table is preserved)
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // 5. Save the workbook with the copied range
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

### Αναμενόμενο αποτέλεσμα

* Το άνοιγμα του `result.xlsx` εμφανίζει δύο φύλλα εργασίας:
  * **Sheet1** – τα αρχικά δεδομένα και ο πίνακας Pivot.
  * **CopyResult** – ακριβές αντίγραφο του πίνακα Pivot, πλήρως λειτουργικό.
* Όλα τα πεδία Pivot, τα φίλτρα και τα υπολογιζόμενα στοιχεία συμπεριφέρονται ταυτόσημα με την πηγή.

Αν τροποποιήσετε τον πηγαίο πίνακα Pivot μετά την αντιγραφή, το διπλότυπο φύλλο **δεν** θα αντανακλά τις αλλαγές, επειδή η cache αντιγράφηκε τη στιγμή της αντιγραφής. Αυτή η απομόνωση είναι συχνά επιθυμητή όταν χρειάζεστε μια «στιγμιότυπη» έκδοση της αναφοράς.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Ο πίνακας Pivot εμφανίζεται κενός** | Η αντιγραμμένη περιοχή παραλείπει τις κρυφές γραμμές cache. | Βεβαιωθείτε ότι η περιοχή περιλαμβάνει ολόκληρη τη cache (συνήθως μερικές γραμμές κάτω από τον ορατό πίνακα). |
| **Το όνομα του φύλλου προορισμού υπάρχει ήδη** | Η κλήση `add("CopyResult")` πετάει εξαίρεση αν το όνομα είναι κατειλημμένο. | Χρησιμοποιήστε `workbook.getWorksheets().addUniqueName("CopyResult")` ή ελέγξτε `contains` πριν την προσθήκη. |
| **Σφάλματα διαδρομής αρχείου** | Λανθασμένο `YOUR_DIRECTORY` προκαλεί `FileNotFoundException`. | Χρησιμοποιήστε απόλυτες διαδρομές ή το `Paths.get(...).toAbsolutePath()` της Java για την επίλυση τοποθεσιών. |
| **Μείωση απόδοσης σε μεγάλα βιβλία εργασίας** | Η αντιγραφή τεράστιων περιοχών αντιγράφει περιττά κελιά. | Περιορίστε την περιοχή στην ακριβή περιοχή του Pivot ή χρησιμοποιήστε `Range.copy` με `CopyOptions` για να παραλείψετε τη μορφοποίηση αν δεν χρειάζεται. |

## Pro tip: Χρήση `CopyOptions` για πιο ακριβή έλεγχο

Αν χρειάζεστε μόνο τα δεδομένα του πίνακα Pivot και θέλετε να παραλείψετε τη μορφοποίηση κελιών, μπορείτε να περάσετε ένα αντικείμενο `CopyOptions`:

```java
CopyOptions options = new CopyOptions();
options.setCopyStyle(false);        // skip styles
options.setCopyMerged(true);        // keep merged cells
sourceRange.copy(destinationSheet.getCells().createRange("A1"), options);
```

Αυτό μειώνει το μέγεθος του αρχείου του διπλότυπου φύλλου και επιταχύνει τη λειτουργία αντιγραφής, ειδικά για μεγάλα βιβλία εργασίας.

## Πώς να αντιγράψετε περιοχή σε νέο φύλλο χωρίς να χάσετε τύπους

Το παραπάνω παράδειγμα ήδη αντιγράφει τύπους επειδή το `Range.copy` τους διατηρεί από προεπιλογή. Αν θέλετε μόνο τιμές (π.χ., για να «παγώσετε» την τρέχουσα κατάσταση), ορίστε `options.setPasteType(PasteType.VALUES)`.

```java
CopyOptions opt = new CopyOptions();
opt.setPasteType(PasteType.VALUES);
sourceRange.copy(destinationSheet.getCells().createRange("A1"), opt);
```

Τώρα το φύλλο προορισμού περιέχει στατικές τιμές, αλλά ο πίνακας Pivot θα λειτουργεί ακόμα επειδή η cache αποτελεί μέρος της περιοχής.

## Σύνοψη της λύσης

* **Πώς να αντιγράψετε έναν πίνακα Pivot** – φορτώστε το βιβλίο εργασίας, ορίστε την ακριβή περιοχή, προσθέστε νέο φύλλο, αντιγράψτε την περιοχή και αποθηκεύστε.
* Η διαδικασία δείχνει επίσης πώς να **αντιγράψετε περιοχή σε νέο φύλλο** και πώς να **αντιγράψετε το φύλλο πίνακα Pivot** με ασφάλεια.
* Μπορείτε να βελτιστοποιήσετε την αντιγραφή με `CopyOptions` για απόδοση ή σενάρια μόνο‑τιμών.

## Επόμενα βήματα και συναφή θέματα

* **Ανανέωση cache πίνακα Pivot προγραμματιστικά** – χρησιμοποιήστε `PivotTable.refreshData()` μετά την ενημέρωση των πηγών δεδομένων.
* **Εξαγωγή πίνακα Pivot σε PDF** – συνδυάστε αυτήν την τεχνική αντιγραφής με `PdfSaveOptions` για δημιουργία στιγμιότυπων αναφορών.
* **Αυτοματοποίηση πολλαπλών αντιγραφών φύλλων** – επαναλάβετε τη λογική για όλα τα φύλλα εργασίας.

Δοκιμάστε αυτές τις παραλλαγές για να προσαρμόσετε το πρότυπο στη δική σας διαδικασία αναφορών. Αν αντιμετωπίσετε ειδικές περιπτώσεις, όπως εξωτερικές πηγές δεδομένων ή πίνακες Pivot που ελέγχονται από VBA, η ίδια προσέγγιση αντιγραφής περιοχής λειτουργεί, αλλά ίσως χρειαστεί να αντιγράψετε και τα αντικείμενα σύνδεσης.

---

*Καλό προγραμματισμό! Αν αυτό το tutorial σας βοήθησε να μάθετε **πώς να αντιγράψετε έναν πίνακα Pivot**, μοιραστείτε το με συναδέλφους ή συνεισφέρετε βελτιώσεις.*

## Τι πρέπει να μάθετε στη συνέχεια;

Οι παρακάτω οδηγίες καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)
- [Create New Workbook in Java – Full Guide to Copy Pivot Table](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Copy Pivot Table Between Workbooks – Step‑by‑Step Java Guide](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}