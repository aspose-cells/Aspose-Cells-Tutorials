---
category: general
date: 2026-09-11
description: Δημιουργήστε νέο φύλλο εργασίας και αντιγράψτε μια περιοχή Excel χρησιμοποιώντας
  το Aspose.Cells. Μάθετε πώς να αντιγράφετε μια περιοχή μεταξύ φύλλων διατηρώντας
  τους πίνακες Pivot.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new worksheet
- copy excel range
- copy range between sheets
- copy range aspose.cells
language: el
lastmod: 2026-09-11
og_description: Δημιουργήστε νέο φύλλο εργασίας και αντιγράψτε περιοχή Excel με το
  Aspose.Cells. Αυτό το σεμινάριο δείχνει τα ακριβή βήματα για την αντιγραφή περιοχής
  μεταξύ φύλλων και τη διατήρηση των πινάκων Pivot αμετάβλητους.
og_image_alt: Screenshot of a Java IDE showing code that creates a new worksheet and
  copies an Excel range
og_title: Δημιουργία νέου φύλλου εργασίας και αντιγραφή περιοχής Excel – Οδηγός Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Create new worksheet and copy Excel range using Aspose.Cells. Learn
    how to copy range between sheets while preserving pivot tables.
  headline: Create new worksheet and copy Excel range with Aspose.Cells
  type: TechArticle
- questions:
  - answer: The `copy` method also copies merge information, so merged cells appear
      unchanged on the destination sheet.
    question: What if the source range contains merged cells?
  - answer: Yes. Load a second `Workbook` instance, create a destination range in
      that workbook, and call `sourceRange.copy(destinationRange)`. The method handles
      cross‑workbook copying automatically.
    question: Can I copy to a different workbook?
  - answer: The copy operation overwrites any existing cells that intersect the destination
      range. To avoid data loss, ensure the destination area is empty or use a different
      start cell (e.g., `"B2"`).
    question: What if the destination sheet already has data?
  - answer: Aspose.Cells reuses the original pivot cache, which means the new pivot
      table remains linked to the same source data. If you need an independent cache,
      you must recreate the pivot table after copying.
    question: Is the pivot cache duplicated?
  type: FAQPage
tags:
- Aspose.Cells
- Excel automation
- Java
title: Δημιουργία νέου φύλλου εργασίας και αντιγραφή περιοχής Excel με το Aspose.Cells
url: /el/java/range-management/create-new-worksheet-and-copy-excel-range-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία νέου φύλλου εργασίας και αντιγραφή περιοχής Excel με Aspose.Cells

Αν χρειάζεστε **create new worksheet** και να μετακινήσετε δεδομένα σε ένα αρχείο Excel, το Aspose.Cells το κάνει απλό. Αυτός ο οδηγός δείχνει ακριβώς πώς να αντιγράψετε μια περιοχή Excel από ένα φύλλο σε άλλο διατηρώντας τυχόν πίνακες Pivot μέσα στην περιοχή.

Θα μάθετε πώς να **copy excel range**, πώς να **copy range between sheets**, και γιατί η μέθοδος `copy` του Aspose.Cells διατηρεί αμετάβλητους τους ορισμούς των πινάκων Pivot. Δεν απαιτούνται εξωτερικά εργαλεία — μόνο ένα έργο Java με τη βιβλιοθήκη Aspose.Cells.

## Προαπαιτούμενα

- Java 17 ή νεότερη εγκατεστημένη
- Aspose.Cells for Java (έκδοση 23.12 ή νεότερη) προστέθηκε στο classpath του έργου σας
- Ένα πηγαίο βιβλίο εργασίας (`input.xlsx`) που περιέχει πίνακα Pivot στην περιοχή που θέλετε να αντιγράψετε
- Βασική εξοικείωση με τη σύνταξη Java και τη διαχείριση εξαρτήσεων Maven/Gradle

## Βήμα 1: Ρύθμιση του έργου και εισαγωγή του Aspose.Cells

Δημιουργήστε ένα απλό έργο Maven (ή Gradle, αν προτιμάτε) και προσθέστε την εξάρτηση Aspose.Cells:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

Στη συνέχεια, εισάγετε τις απαιτούμενες κλάσεις στο αρχείο πηγαίου κώδικα Java:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

*Γιατί αυτό το βήμα είναι σημαντικό*: Η εισαγωγή των σωστών κλάσεων σας δίνει πρόσβαση στα `Workbook`, `Worksheet`, `Range` και στη μέθοδο `copy` που θα διαχειριστεί τη μεταφορά της περιοχής.

## Βήμα 2: Φόρτωση του πηγαίου βιβλίου εργασίας

Ανοίξτε το βιβλίο εργασίας που περιέχει τα δεδομένα που θέλετε να αντιγράψετε. Ο παρακάτω κώδικας φορτώνει το `input.xlsx` από έναν κατάλογο που καθορίζετε:

```java
public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Επεξήγηση*: Το `Workbook` αντιπροσωπεύει ολόκληρο το αρχείο Excel. Η φόρτωσή του μία φορά σας παρέχει πρόσβαση ανάγνωσης/εγγραφής σε κάθε φύλλο και συλλογή κελιών.

## Βήμα 3: Προσδιορισμός της πηγαίας περιοχής που περιλαμβάνει τον πίνακα Pivot

Επιλέξτε το φύλλο εργασίας που περιέχει τον πίνακα Pivot και ορίστε το ακριβές μπλοκ κελιών που θέλετε να αντιγράψετε. Σε αυτό το παράδειγμα αντιγράφουμε τα κελιά A1 έως D20:

```java
        // Get the first worksheet (index 0) that contains the pivot table
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the source range – this range includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");
```

*Γιατί αυτό είναι σημαντικό*: Δημιουργώντας ένα αντικείμενο `Range`, λέτε στο Aspose.Cells ακριβώς ποια κελιά (συμπεριλαμβανομένων τυχόν ενσωματωμένων αντικειμένων όπως πίνακες Pivot) πρέπει να αντιγραφούν.

## Βήμα 4: **Create new worksheet** που θα λάβει τα αντιγραμμένα δεδομένα

Τώρα προσθέτουμε ένα νέο φύλλο στο ίδιο βιβλίο εργασίας. Αυτό είναι το σημείο όπου εμφανίζεται η κύρια λέξη-κλειδί:

```java
        // Create a new worksheet named "Copy"
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // Define the top‑left cell of the destination range
        Range destinationRange = destinationSheet.getCells().createRange("A1");
```

*Επεξήγηση*: Η προσθήκη νέου φύλλου απομονώνει τα αντιγραμμένα δεδομένα, καθιστώντας εύκολο να επαληθευτεί ότι η λειτουργία **copy excel range** ολοκληρώθηκε επιτυχώς χωρίς να επηρεάσει το αρχικό φύλλο.

## Βήμα 5: Αντιγραφή της περιοχής – ο πίνακας Pivot διατηρείται αυτόματα

Χρησιμοποιήστε τη μέθοδο `copy` για να μετακινήσετε την περιοχή από το πηγαίο φύλλο στο προορισμένο φύλλο. Το Aspose.Cells αντιγράφει τύπους, μορφοποίηση και ορισμούς πινάκων Pivot:

```java
        // Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);
```

*Γιατί λειτουργεί*: Η μέθοδος `copy` εκτελεί μια βαθιά αντιγραφή των πηγαίων κελιών. Δεν αντιγράφει μόνο τις τιμές· αντιγράφει ολόκληρη τη δομή του κελιού, που περιλαμβάνει την κρυφή μνήμη του Pivot. Γι' αυτό μπορείτε να **copy range aspose.cells** και να δείτε ακόμη έναν λειτουργικό πίνακα Pivot στο νέο φύλλο.

## Βήμα 6: Αποθήκευση του βιβλίου εργασίας με το νέο φύλλο

Τέλος, γράψτε το τροποποιημένο βιβλίο εργασίας στο δίσκο:

```java
        // Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

*Αποτέλεσμα*: Το `output.xlsx` περιέχει τώρα το αρχικό φύλλο συν ένα νέο φύλλο που ονομάζεται **Copy** και περιέχει ακριβώς την ίδια περιοχή, συμπεριλαμβανομένου του πίνακα Pivot.

## Πλήρες λειτουργικό παράδειγμα

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι το πλήρες, εκτελέσιμο πρόγραμμα:

```java
import com.aspose.cells.*;
import java.io.IOException;

public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table and define the source range
        Worksheet sourceSheet = workbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");

        // Step 3: Create a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
        Range destinationRange = destinationSheet.getCells().createRange("A1");

        // Step 4: Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);

        // Step 5: Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Αναμενόμενο αποτέλεσμα**: Ανοίξτε το `output.xlsx` στο Excel. Θα δείτε ένα φύλλο με όνομα **Copy** του οποίου τα κελιά A1:D20 περιέχουν τα ίδια δεδομένα, τη μορφοποίηση και έναν ενεργό πίνακα Pivot πανομοιότυπο με το αρχικό.

## Συχνές ερωτήσεις και ειδικές περιπτώσεις

- **Τι γίνεται αν η πηγαία περιοχή περιέχει συγχωνευμένα κελιά;**  
  Η μέθοδος `copy` αντιγράφει επίσης τις πληροφορίες συγχώνευσης, έτσι τα συγχωνευμένα κελιά παραμένουν αμετάβλητα στο προορισμένο φύλλο.

- **Μπορώ να αντιγράψω σε διαφορετικό βιβλίο εργασίας;**  
  Ναι. Φορτώστε μια δεύτερη παρουσία `Workbook`, δημιουργήστε μια περιοχή προορισμού σε αυτό το βιβλίο και καλέστε `sourceRange.copy(destinationRange)`. Η μέθοδος διαχειρίζεται αυτόματα την αντιγραφή μεταξύ βιβλίων εργασίας.

- **Τι γίνεται αν το προορισμένο φύλλο έχει ήδη δεδομένα;**  
  Η λειτουργία αντιγραφής αντικαθιστά τυχόν υπάρχοντα κελιά που τέμνονται με την περιοχή προορισμού. Για να αποφύγετε απώλεια δεδομένων, βεβαιωθείτε ότι η περιοχή προορισμού είναι κενή ή χρησιμοποιήστε διαφορετικό αρχικό κελί (π.χ., `"B2"`).

- **Διπλασιάζεται η κρυφή μνήμη του Pivot;**  
  Το Aspose.Cells επαναχρησιμοποιεί την αρχική κρυφή μνήμη του Pivot, πράγμα που σημαίνει ότι ο νέος πίνακας Pivot παραμένει συνδεδεμένος με τα ίδια δεδομένα προέλευσης. Αν χρειάζεστε ανεξάρτητη κρυφή μνήμη, πρέπει να δημιουργήσετε ξανά τον πίνακα Pivot μετά την αντιγραφή.

## Συμβουλές και βέλτιστες πρακτικές

- **Pro tip**: Χρησιμοποιήστε `Workbook.setForceFormulaRecalculation(true)` πριν από την αποθήκευση εάν η περιοχή σας περιέχει τύπους που εξαρτώνται από δεδομένα εκτός του αντιγραμμένου μπλοκ.
- **Προσέξτε** μεγάλες περιοχές: η αντιγραφή τεράστιων φύλλων μπορεί να καταναλώσει σημαντική μνήμη. Σκεφτείτε να αντιγράψετε σε μικρότερα τμήματα αν αντιμετωπίσετε `OutOfMemoryError`.
- **Performance tip**: Απενεργοποιήστε την ενημέρωση οθόνης (`workbook.getSettings().setCalculateFormulaOnOpen(false)`) όταν εργάζεστε με πολύ μεγάλα αρχεία για να επιταχύνετε τη διαδικασία αντιγραφής.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **create new worksheet** και **copy excel range** μεταξύ φύλλων χρησιμοποιώντας το Aspose.Cells, διατηρώντας τους πίνακες Pivot και όλα τα χαρακτηριστικά των κελιών. Αυτή η τεχνική σας επιτρέπει να αντιγράφετε προγραμματιστικά μπλοκ δεδομένων, να δημιουργείτε πρότυπα αναφορών ή να αναδιαρθρώνετε βιβλία εργασίας χωρίς χειροκίνητη αντιγραφή‑επικόλληση.

Στη συνέχεια, εξερευνήστε συναφή θέματα όπως **copy range aspose.cells** για λειτουργίες μεταξύ βιβλίων εργασίας, αυτοματοποίηση ανανεώσεων πινάκων Pivot ή εξαγωγή του αντιγραμμένου φύλλου σε PDF. Πειραματιστείτε με διαφορετικές πηγαίες περιοχές και ονόματα φύλλων για να ταιριάζουν στο συγκεκριμένο σενάριο αυτοματοποίησής σας. Καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Αντιγραφή Σχημάτων μεταξύ Φύλλων Excel χρησιμοποιώντας Aspose.Cells για .NET: Πλήρης Οδηγός](/cells/english/net/images-shapes/copy-shapes-between-sheets-aspose-cells-dotnet/)
- [Αντιγραφή Εικόνων μεταξύ Φύλλων στο Excel χρησιμοποιώντας Aspose.Cells για Java: Αναλυτικός Οδηγός](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Excel Aspose Cells Dotnet Αντιγραφή Δεδομένων Περιοχής](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}