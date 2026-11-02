---
category: general
date: 2026-09-21
description: Μάθετε πώς να αντιγράψετε μια περιοχή σε Java διατηρώντας τον συγκεντρωτικό
  πίνακα. Αυτός ο οδηγός βήμα‑προς‑βήμα σας δείχνει πώς να εξάγετε έναν συγκεντρωτικό
  πίνακα με ασφάλεια.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- preserve pivot table
- export pivot table
- how to preserve pivot
language: el
lastmod: 2026-09-21
og_description: Πώς να αντιγράψετε μια περιοχή σε Java διατηρώντας τον συγκεντρωτικό
  πίνακα. Ακολουθήστε αυτόν τον πλήρη οδηγό για να εξάγετε τους συγκεντρωτικούς πίνακες
  με ασφάλεια.
og_image_alt: Screenshot of Java code copying a range and preserving a pivot table
og_title: Πώς να αντιγράψετε μια περιοχή και να διατηρήσετε έναν συγκεντρωτικό πίνακα
  σε Java
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  headline: How to copy range and preserve a pivot table in Java
  type: TechArticle
- description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  name: How to copy range and preserve a pivot table in Java
  steps:
  - name: Load the source workbook
    text: '```java // Load the source workbook that contains the pivot table Workbook
      srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx"); Worksheet srcWs = srcWb.getWorksheets().get(0);
      ```'
  - name: Define the range that covers the pivot table
    text: '```java // Define the range covering the pivot table (including its data
      source) Range srcRange = srcWs.getCells().createRange("A1:G20"); ```'
  - name: Create an empty destination workbook
    text: '```java // Create a new, empty destination workbook Workbook destWb = new
      Workbook(); Worksheet destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range – the pivot table is preserved
    text: '```java // Copy the defined range to the destination sheet – the pivot
      table is preserved destWs.getCells().copyRange(srcRange, new CellArea("A1",
      "G20")); ```'
  - name: Save the destination workbook
    text: '```java // Save the destination workbook with the copied pivot table destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
      ```'
  - name: Copy pivot table across different workbook versions
    text: Aspose.Cells supports older `.xls` files as well as the newer `.xlsx` format.
      The same code works regardless of the file extension, making it a universal
      solution for **how to preserve pivot** across versions.
  - name: Preserving pivot table when using a filtered source
    text: 'If the source pivot is filtered, the filter state is also copied. Should
      you need to reset filters in the destination, call `PivotTable.refreshData()`
      after copying:'
  - name: Export pivot table as a static snapshot
    text: Sometimes you may want a static copy (values only) rather than a live pivot.
      Replace `copyRange` with `copyRange` followed by `pt.setEnableRefresh(false)`
      to disable further calculations.
  - name: Handling large workbooks
    text: For workbooks with many worksheets, limit the copy operation to the specific
      sheet to reduce memory usage. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to fine‑tune performance.
  type: HowTo
tags:
- Java
- Aspose.Cells
- pivot table
- Excel automation
- range copy
title: Πώς να αντιγράψετε μια περιοχή και να διατηρήσετε έναν πίνακα Pivot σε Java
url: /el/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αντιγράψετε μια περιοχή και να διατηρήσετε έναν πίνακα Pivot σε Java

Αν χρειάζεστε **how to copy range** που περιέχει έναν πίνακα pivot, αυτός ο οδηγός σας δείχνει έναν αξιόπιστο τρόπο να διατηρήσετε τον pivot αμετάβλητο. Πολλοί προγραμματιστές αντιμετωπίζουν το πρόβλημα της απώλειας του pivot όταν εξάγουν δεδομένα, αλλά η παρακάτω προσέγγιση σας επιτρέπει να **copy pivot table** δεδομένα χωρίς να σπάσει η λειτουργικότητά του. Στο τέλος αυτού του tutorial θα μπορείτε να **preserve pivot table** τη δομή, **export pivot table** αρχεία, και να καταλάβετε **how to preserve pivot** σε διαφορετικά σενάρια.

Το παράδειγμα χρησιμοποιεί το Aspose.Cells for Java, μια δημοφιλής βιβλιοθήκη για αυτοματοποίηση Excel. Δεν απαιτείται πρόσθετο εργαλείο πέρα από ένα τυπικό περιβάλλον ανάπτυξης Java.

## Προαπαιτούμενα

* Java 17 (ή νεότερη) εγκατεστημένη.
* Maven ή Gradle για διαχείριση εξαρτήσεων.
* Aspose.Cells for Java (έκδοση 23.9 ή νεότερη). Προσθέστε την ακόλουθη εξάρτηση Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

* Ένα βιβλίο εργασίας προέλευσης (`Source.xlsx`) που περιέχει τον πίνακα pivot που θέλετε να αντιγράψετε.

## Πώς να αντιγράψετε μια περιοχή και να διατηρήσετε τον πίνακα pivot αμετάβλητο

Η κύρια ιδέα είναι να αντιγράψετε το **range** που περιβάλλει ολόκληρο τον pivot—συμπεριλαμβανομένης της πηγής δεδομένων του—χρησιμοποιώντας το `copyRange`. Αυτή η μέθοδος αντιγράφει τόσο τα ακατέργαστα δεδομένα όσο και τον ορισμό του pivot, διασφαλίζοντας ότι το βιβλίο εργασίας προορισμού λαμβάνει έναν πλήρως λειτουργικό pivot.

### Βήμα 1: Φόρτωση του βιβλίου εργασίας προέλευσης

```java
// Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*Γιατί αυτό το βήμα;*  
Η φόρτωση του βιβλίου εργασίας σας δίνει πρόσβαση στο φύλλο εργασίας που φιλοξενεί τον pivot. Η κλάση `Workbook` αφαιρεί την αφηρημένη αναπαράσταση ολόκληρου του αρχείου Excel, ενώ η `Worksheet` παρέχει λειτουργίες σε επίπεδο κελιού.

### Βήμα 2: Ορισμός της περιοχής που καλύπτει τον πίνακα pivot

```java
// Define the range covering the pivot table (including its data source)
Range srcRange = srcWs.getCells().createRange("A1:G20");
```

*Γιατί αυτό το βήμα;*  
Ένας πίνακας pivot δεν είναι ένα μόνο κελί· εκτείνεται σε ένα μπλοκ που περιλαμβάνει κεφαλίδες, σειρές δεδομένων και την cache του pivot. Καθορίζοντας μια περιοχή που περιλαμβάνει πλήρως τον pivot, εξασφαλίζετε ότι το `copyRange` θα αντιγράψει επίσης την υποκείμενη cache, η οποία είναι απαραίτητη για τη συμπεριφορά **preserve pivot table**.

### Βήμα 3: Δημιουργία ενός κεντρικού βιβλίου εργασίας προορισμού

```java
// Create a new, empty destination workbook
Workbook destWb = new Workbook();
Worksheet destWs = destWb.getWorksheets().get(0);
```

*Γιατί αυτό το βήμα;*  
Ξεκινώντας με ένα καθαρό βιβλίο εργασίας αποφεύγετε τυχαίες συγκρούσεις με υπάρχοντα φύλλα ή ονομασμένες περιοχές. Το βιβλίο εργασίας προορισμού θα λάβει την αντιγραμμένη περιοχή, αποτελεσματικά το περιεχόμενο **export pivot table**.

### Βήμα 4: Αντιγραφή της περιοχής – ο πίνακας pivot διατηρείται

```java
// Copy the defined range to the destination sheet – the pivot table is preserved
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
```

*Γιατί αυτό το βήμα;*  
Το `copyRange` εκτελεί μια βαθιά αντιγραφή: τιμές κελιών, μορφοποίηση και μεταδεδομένα του pivot μεταφέρονται. Αυτή είναι η κρίσιμη λειτουργία που επιτρέπει το **copy pivot table** χωρίς να χάσει τη λειτουργικότητά του. Το αντικείμενο `CellArea` καθορίζει πού τοποθετείται η περιοχή στο φύλλο προορισμού.

### Βήμα 5: Αποθήκευση του βιβλίου εργασίας προορισμού

```java
// Save the destination workbook with the copied pivot table
destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
```

*Γιατί αυτό το βήμα;*  
Η αποθήκευση ολοκληρώνει τη διαδικασία **export pivot table**. Το προκύπτον αρχείο (`DestWithPivot.xlsx`) περιέχει έναν πλήρως λειτουργικό pivot που μπορείτε να ανοίξετε σε Excel, Google Sheets ή οποιονδήποτε άλλο προβολέα υπολογιστικών φύλλων.

## Επαλήθευση ότι ο πίνακας pivot διατηρήθηκε

Ανοίξτε το `DestWithPivot.xlsx` στο Excel και ελέγξτε τα εξής:

1. Ο πίνακας pivot εμφανίζεται στην ίδια θέση (A1:G20) όπως στην προέλευση.
2. Η ανανέωση του pivot ενημερώνει τα δεδομένα σωστά, αποδεικνύοντας ότι η cache αντιγράφηκε.
3. Όλη η μορφοποίηση (πλάτη στηλών, μορφές αριθμών) ταιριάζει με το αρχικό.

Αν κάποιος από αυτούς τους ελέγχους αποτύχει, βεβαιωθείτε ότι η περιοχή προέλευσης περιλαμβάνει πλήρως τον pivot και την πηγή δεδομένων του. Ένα κοινό λάθος είναι η επιλογή περιοχής που δεν καλύπτει πλήρως την cache δεδομένων, κάτι που οδηγεί σε σπασμένο pivot.

## Πρόσθετες παρατηρήσεις

### Αντιγραφή πίνακα pivot μεταξύ διαφορετικών εκδόσεων βιβλίου εργασίας

Το Aspose.Cells υποστηρίζει παλαιότερα αρχεία `.xls` καθώς και τη νεότερη μορφή `.xlsx`. Ο ίδιος κώδικας λειτουργεί ανεξάρτητα από την επέκταση του αρχείου, καθιστώντας το μια καθολική λύση για **how to preserve pivot** μεταξύ εκδόσεων.

### Διατήρηση πίνακα pivot όταν χρησιμοποιείται φιλτραρισμένη πηγή

Αν ο pivot προέλευσης είναι φιλτραρισμένος, η κατάσταση του φίλτρου αντιγράφεται επίσης. Εάν χρειάζεται να επαναφέρετε τα φίλτρα στον προορισμό, καλέστε `PivotTable.refreshData()` μετά την αντιγραφή:

```java
PivotTable pt = destWs.getPivotTables().get(0);
pt.refreshData();   // Clears filters but keeps the pivot definition
```

### Εξαγωγή πίνακα pivot ως στατική λήψη

Μερικές φορές μπορεί να θέλετε μια στατική αντίγραφο (μόνο τιμές) αντί για έναν ζωντανό pivot. Αντικαταστήστε το `copyRange` με `copyRange` ακολουθούμενο από `pt.setEnableRefresh(false)` για να απενεργοποιήσετε περαιτέρω υπολογισμούς.

```java
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
PivotTable pt = destWs.getPivotTables().get(0);
pt.setEnableRefresh(false); // Makes the pivot static
```

### Διαχείριση μεγάλων βιβλίων εργασίας

Για βιβλία εργασίας με πολλά φύλλα, περιορίστε τη λειτουργία αντιγραφής στο συγκεκριμένο φύλλο για να μειώσετε τη χρήση μνήμης. Χρησιμοποιήστε `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` για να ρυθμίσετε λεπτομερώς την απόδοση.

## Πλήρες εκτελέσιμο παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε, επικολλήσετε και εκτελέσετε. Προσαρμόστε τις διαδρομές αρχείων ώστε να ταιριάζουν με το περιβάλλον σας.

```java
import com.aspose.cells.*;

public class CopyPivotRange {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Define the range covering the pivot table (including its data source)
        // Adjust the range as needed to fully contain your pivot
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 3: Create a new, empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 4: Copy the defined range – the pivot table is preserved
        destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));

        // Optional: If you need a static snapshot, disable refresh
        // PivotTable pt = destWs.getPivotTables().get(0);
        // pt.setEnableRefresh(false);

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");

        System.out.println("Pivot table copied successfully. File saved as DestWithPivot.xlsx");
    }
}
```

**Αναμενόμενη έξοδος**

```
Pivot table copied successfully. File saved as DestWithPivot.xlsx
```

Όταν ανοίξετε το `DestWithPivot.xlsx`, θα πρέπει να δείτε τον αρχικό πίνακα pivot πλήρως λειτουργικό, επιβεβαιώνοντας ότι έχετε επιτυχώς **how to copy range** ενώ **preserve pivot table**.

## Συνηθισμένα προβλήματα και επαγγελματικές συμβουλές

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|------------------|----------|
| Ο πίνακας pivot εμφανίζεται αλλά εμφανίζει σφάλματα `#REF!` | Η αντιγραμμένη περιοχή παραλείπει το κρυφό φύλλο cache | Επεκτείνετε την περιοχή προέλευσης ώστε να περιλαμβάνει ολόκληρη την cache (συνήθως τις γραμμές κάτω από τον pivot) |
| Το βιβλίο εργασίας προορισμού είναι μεγαλύτερο από το αναμενόμενο | `copyRange` αντιγράφει επίσης τη μορφοποίηση | Χρησιμοποιήστε `CopyOptions` για να εξαιρέσετε τη μορφοποίηση εάν το μέγεθος είναι πρόβλημα |
| Η ανανέωση αποτυγχάνει με το μήνυμα “Data source not found” | Το βιβλίο εργασίας προέλευσης χρησιμοποίησε εξωτερικές συνδέσεις δεδομένων | Αναπαράγετε τη σύνδεση στον προορισμό ή αντιγράψτε πρώτα το φύλλο πηγής δεδομένων |

**Συμβουλή:** Εκτελέστε πάντα έναν γρήγορο έλεγχο `destWs.getPivotTables().size()` μετά την αντιγραφή. Εάν ο αριθμός είναι μηδέν, η περιοχή δεν περιλάμβανε τον ορισμό του pivot και πρέπει να την επεκτείνετε.

## Συμπέρασμα

Σε αυτό το tutorial δείξαμε **how to copy range** που περιέχει έναν πίνακα pivot και εγγυηθήκαμε ότι η συμπεριφορά **preserve pivot table** παραμένει αμετάβλητη. Φορτώνοντας το βιβλίο εργασίας προέλευσης, ορίζοντας μια ολοκληρωμένη περιοχή, χρησιμοποιώντας το `copyRange` και αποθηκεύοντας το αρχείο προορισμού, μπορείτε αξιόπιστα να **export pivot table** δεδομένα και να απαντήσετε στην ερώτηση **how to preserve pivot** σε έργα Java.

Τα επόμενα βήματα που μπορείτε να εξερευνήσετε περιλαμβάνουν:

* Αυτοματοποίηση της αντιγραφής για πολλαπλά φύλλα (χρησιμοποιήστε τη δευτερεύουσα λέξη‑κλειδί **copy pivot table** σε βρόχο).
* Μετατροπή του εξαγόμενου βιβλίου εργασίας σε CSV διατηρώντας τα ακατέργαστα δεδομένα (ακόμη λογική **preserve pivot table** για την πηγή).

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Copy Pivot Table in Java – Preserve It, Export to PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Export Pivot Table as an Image in C# – Step‑by‑Step Guide](/cells/english/net/pivot-tables/how-to-export-pivot-table-as-an-image-in-c-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}