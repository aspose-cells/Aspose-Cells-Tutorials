---
category: general
date: 2026-07-23
description: Δημιουργήστε νέο βιβλίο εργασίας σε Java και μάθετε πώς να αντιγράψετε
  έναν πίνακα Pivot, να αντιγράψετε ένα εύρος Excel και να εξάγετε τον πίνακα Pivot
  με το Aspose.Cells σε λίγα λεπτά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- how to copy pivot
- copy excel range
- export pivot table
language: el
lastmod: 2026-07-23
og_description: Δημιουργήστε νέο βιβλίο εργασίας σε Java και αμέσως αντιγράψτε τον
  πίνακα Pivot, αντιγράψτε το εύρος Excel, στη συνέχεια εξάγετε τον πίνακα Pivot χρησιμοποιώντας
  το Aspose.Cells. Ακολουθήστε αυτό το πλήρες σεμινάριο.
og_image_alt: Screenshot of Java code copying a pivot table from one workbook to another
og_title: Δημιουργία νέου βιβλίου εργασίας σε Java – Αντιγραφή Πίνακα Pivot βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Create new workbook in Java and learn how to copy pivot table, copy
    excel range, and export pivot table with Aspose.Cells in minutes.
  headline: Create New Workbook in Java – Full Guide to Copy Pivot Table
  type: TechArticle
- questions:
  - answer: You’ll need to copy each relevant range separately, then recreate the
      pivot on the destination sheet using `PivotTable` APIs.
    question: What if the source pivot spans more than one worksheet?
  - answer: Set `sourceRange.setCopyDataOnly(false)` before the copy. This tells Aspose
      to keep the cache but not the underlying source data.
    question: Can I copy only the pivot layout without the data?
  - answer: CSV doesn’t support pivots, but you can export the pivot’s *result* by
      calling `pivotTable.calculate()` and then saving the sheet as CSV.
    question: Is there a way to copy the pivot to a CSV file?
  - answer: Formatting lives in the style collection. After copying, you can call
      `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())`
      to transfer styles.
    question: Why does the copied pivot lose its formatting?
  type: FAQPage
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Δημιουργία νέου βιβλίου εργασίας σε Java – Πλήρης οδηγός για την αντιγραφή
  πίνακα Pivot
url: /el/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Νέου Φύλλου Εργασίας σε Java – Πλήρης Οδηγός για Αντιγραφή Πίνακα Pivot

Έχετε αναρωτηθεί ποτέ πώς να **create new workbook** σε Java διατηρώντας έναν πολύπλοκο πίνακα pivot; Δεν είστε ο μόνος που σκεπάζει το κεφάλι του για αυτό. Σε πολλές εφαρμογές αναφοράς χρειάζεται να μεταφέρετε έναν pivot από ένα αρχείο προέλευσης σε ένα νέο φύλλο εργασίας, ίσως για να το στείλετε σε πελάτη ή να εκτελέσετε περαιτέρω υπολογισμούς. Τα καλά νέα; Με λίγες γραμμές κώδικα μπορείτε να το κάνετε ακριβώς αυτό—χωρίς χειροκίνητη αντιγραφή‑επικόλληση.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: φόρτωση του αρχείου προέλευσης, ορισμός της περιοχής που περιέχει τον pivot, **copying the Excel range**, δημιουργία ενός **new workbook**, και τελικά **exporting the pivot table** σε νέο αρχείο. Στο τέλος θα έχετε ένα αυτόνομο, εκτελέσιμο πρόγραμμα Java που απαντά στην ερώτηση “**how to copy pivot**” χωρίς καμιά εικασία.

## Προαπαιτούμενα

- Java 17 ή νεότερη (ο κώδικας λειτουργεί με οποιοδήποτε πρόσφατο JDK)
- Βιβλιοθήκη Aspose.Cells for Java (δωρεάν δοκιμή ή έκδοση με άδεια)
- Ένα δείγμα `source.xlsx` που περιέχει πίνακα pivot στην περιοχή `A1:G20`
- Ένα IDE ή εργαλείο κατασκευής (Maven/Gradle) για τη διαχείριση του Aspose.Cells JAR

Τα έχετε; Τέλεια—ας ξεκινήσουμε.

## Βήμα 1: Ρύθμιση του Έργου και Εισαγωγή του Aspose.Cells

Πρώτα απ’ όλα, πρέπει να προσθέσετε το Aspose.Cells στο έργο σας. Αν χρησιμοποιείτε Maven, προσθέστε αυτήν την εξάρτηση στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.8</version> <!-- check for the latest version -->
</dependency>
```

Αν προτιμάτε Gradle, το ισοδύναμο είναι:

```groovy
implementation 'com.aspose:aspose-cells:24.8'
```

Μόλις η βιβλιοθήκη βρίσκεται στο classpath, εισάγετε τις κλάσεις που θα χρειαστείτε:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

> **Pro tip:** Aspose.Cells είναι εμπορική βιβλιοθήκη, αλλά προσφέρει πλήρως λειτουργική 30‑ήμερη αξιολόγηση που προσθέτει υδατογράφημα στην έξοδο—τέλεια για δοκιμή.

## Βήμα 2: Φόρτωση του Φύλλου Εργασίας Πηγής

Τώρα θα **create new workbook** αντικείμενα, αλλά πρώτα χρειαζόμαστε την πηγή που περιέχει τον pivot. Αυτό το βήμα είναι το θεμέλιο για οποιαδήποτε λειτουργία **copy excel range**, επειδή το αντικείμενο περιοχής γνωρίζει ακριβώς ποιες κυψέλες (συμπεριλαμβανομένης της cache του pivot) πρέπει να μεταφερθούν.

```java
// Load the source workbook that contains the pivot table
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0) – adjust if your pivot lives elsewhere
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

Γιατί να μην διαβάσουμε απλώς την περιοχή απευθείας; Επειδή τα μεταδεδομένα του πίνακα pivot ζουν στην cache του φύλλου εργασίας, και το Aspose.Cells τα ενσωματώνει αυτόματα όταν αντιγράφετε την περιοχή.

## Βήμα 3: Ορισμός της Περιοχής που Περιέχει τον Πίνακα Pivot

Σε πολλά πραγματικά αρχεία ο pivot καταλαμβάνει ένα ορθογώνιο μπλοκ. Για αυτό το παράδειγμα υποθέτουμε ότι βρίσκεται στο `A1:G20`. Φυσικά μπορείτε να προσαρμόσετε τη διεύθυνση ώστε να ταιριάζει με τη δική σας διάταξη.

```java
// Define the exact area that includes the pivot table
Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

Αν δεν είστε σίγουροι για την ακριβή διεύθυνση, μπορείτε να χρησιμοποιήσετε `sourceSheet.getCells().getMaxDataRow()` και `getMaxDataColumn()` για να υπολογίσετε τα όρια δυναμικά. Είναι ένα χρήσιμο κόλπο όταν το μέγεθος του pivot αλλάζει με τον χρόνο.

## Βήμα 4: **Create New Workbook** και Φύλλο Προορισμού

Εδώ είναι η στιγμή που πραγματικά **create new workbook** που θα λάβει το αντιγραμμένο περιεχόμενο. Σκεφτείτε το ως το κενό καμβά πάνω στον οποίο θα επικολλήσετε τον pivot.

```java
// Create an empty workbook – this is our destination
Workbook destinationWorkbook = new Workbook();

// By default a new workbook comes with one worksheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Γιατί να ξεκινήσουμε με ένα κενό φύλλο εργασίας; Εγγυάται ότι δεν υπάρχουν κρυφά στυλ ή προηγούμενοι pivots που να παρεμβαίνουν στην αντιγραφή, δίνοντάς σας ένα καθαρό αποτέλεσμα έτοιμο για **export pivot table**.

## Βήμα 5: Αντιγραφή του Πίνακα Pivot (και της Υποκείμενης Περιοχής)

Τώρα το κύριο μέρος του tutorial: **copy pivot table**. Το Aspose.Cells αντιμετωπίζει την αντιγραφή μιας περιοχής ως βαθιά αντιγραφή, πράγμα που σημαίνει ότι η cache του pivot μεταφέρεται μαζί με τις κυψέλες. Γι’ αυτό αυτή η μία γραμμή κάνει το σκληρό έργο.

```java
// Copy the defined range (including the pivot) to the destination sheet at A1
sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

Αν ποτέ αναρωτηθήκατε **how to copy pivot** χωρίς να χάσετε τη λειτουργικότητά του, αυτή είναι η απάντηση. Το φύλλο προορισμού περιέχει τώρα έναν πλήρως λειτουργικό pivot που μπορείτε να ανανεώσετε, να τροποποιήσετε ή απλώς να εξάγετε.

### Ακραία Περίπτωση: Διατήρηση Ρυθμίσεων Ανανέωσης

Μερικές φορές ο pivot στην πηγή είναι ρυθμισμένος να ανανεώνεται κατά το άνοιγμα. Για να διατηρήσετε αυτή τη συμπεριφορά, μπορείτε να αντιγράψετε ρητά τις επιλογές του pivot:

```java
// Optional: retain the original pivot's refresh settings
PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
PivotTable destPivot = destinationSheet.getPivotTables().get(0);
destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
```

Αυτό το απόσπασμα κώδικα εξασφαλίζει ότι ο αντιγραμμένος pivot συμπεριφέρεται ακριβώς όπως ο αρχικός.

## Βήμα 6: Αποθήκευση του Φύλλου Εργασίας Προορισμού – **Export Pivot Table**

Τέλος, **export pivot table** αποθηκεύοντας το νέο φύλλο εργασίας στο δίσκο. Μπορείτε να επιλέξετε οποιαδήποτε μορφή υποστηρίζει το Aspose: XLSX, XLS, CSV, PDF, κ.λπ. Για αυτόν τον οδηγό θα μείνουμε στο XLSX.

```java
// Save the workbook that now contains the copied pivot
destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);
```

Αν χρειαστεί να στείλετε το αρχείο μέσω web service, μπορείτε να το γράψετε σε ένα `ByteArrayOutputStream` αντί για διαδρομή αρχείου—το Aspose το κάνει αυτό εύκολα.

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι ένα πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Μη διστάσετε να το αντιγράψετε, να το επικολλήσετε και να το εκτελέσετε στο IDE σας.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 3️⃣ Copy the range (pivot table included) to the destination sheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Optional: Preserve refresh settings if needed
        if (!sourceSheet.getPivotTables().isEmpty()) {
            PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
            PivotTable destPivot = destinationSheet.getPivotTables().get(0);
            destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
        }

        // 4️⃣ Save the result – this effectively **export pivot table**
        destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);

        System.out.println("Pivot table copied successfully!");
    }
}
```

### Αναμενόμενη Έξοδος

Όταν τρέξετε το πρόγραμμα, η κονσόλα εκτυπώνει:

```
Pivot table copied successfully!
```

Και το αρχείο `copied_with_pivot.xlsx` εμφανίζεται στο `YOUR_DIRECTORY`. Ανοίξτε το στο Excel και θα δείτε τον πίνακα pivot άθικτο, έτοιμο για ανανέωση ή επεξεργασία.

## Συχνές Ερωτήσεις & Επίλυση Προβλημάτων

- **Τι γίνεται αν ο pivot στην πηγή εκτείνεται σε περισσότερα από ένα φύλλα εργασίας;**  
  Θα χρειαστεί να αντιγράψετε κάθε σχετική περιοχή ξεχωριστά, έπειτα να δημιουργήσετε ξανά τον pivot στο φύλλο προορισμού χρησιμοποιώντας τις API του `PivotTable`.

- **Μπορώ να αντιγράψω μόνο τη διάταξη του pivot χωρίς τα δεδομένα;**  
  Ορίστε `sourceRange.setCopyDataOnly(false)` πριν από την αντιγραφή. Αυτό λέει στο Aspose να διατηρήσει την cache αλλά όχι τα υποκείμενα δεδομένα πηγής.

- **Υπάρχει τρόπος να αντιγράψω τον pivot σε αρχείο CSV;**  
  Το CSV δεν υποστηρίζει pivots, αλλά μπορείτε να εξάγετε το *αποτέλεσμα* του pivot καλώντας `pivotTable.calculate()` και στη συνέχεια αποθηκεύοντας το φύλλο ως CSV.

- **Γιατί ο αντιγραμμένος pivot χάνει τη μορφοποίηση του;**  
  Η μορφοποίηση βρίσκεται στη συλλογή στυλ. Μετά την αντιγραφή, μπορείτε να καλέσετε `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())` για να μεταφέρετε τα στυλ.

## Συμπέρασμα

Σας δείξαμε πώς να **create new workbook** σε Java, **copy pivot table**, και **export pivot table**—όλα με καθαρό, επαναλήψιμο δείγμα κώδικα. Ορίζοντας ακριβώς το **copy excel range**, αξιοποιώντας τη βαθιά αντιγραφή του Aspose.Cells και διατηρώντας προαιρετικές ρυθμίσεις, μπορείτε να αυτοματοποιήσετε πρακτικά οποιαδήποτε εργασία μεταφοράς pivot.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να αλλάξετε τη μορφή εξόδου σε PDF ή να κάνετε βρόχο σε πολλά αρχεία προέλευσης για μαζική επεξεργασία δεκάδων pivots. Το ίδιο μοτίβο ισχύει—απλώς προσαρμόστε τις διαδρομές αρχείων και τις διευθύνσεις περιοχών.

Αν αντιμετωπίσετε κάποιο πρόβλημα, αφήστε ένα σχόλιο παρακάτω ή ελέγξτε την τεκμηρίωση του Aspose.Cells για προχωρημένη διαχείριση pivots. Καλή προγραμματιστική δουλειά και απολαύστε τον χρόνο που κερδίσατε αυτοματοποιώντας αυτές τις κουραστικές εργασίες αντιγραφής‑επικόλλησης!

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}