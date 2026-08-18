---
category: general
date: 2026-08-17
description: Πώς να αντιγράψετε φύλλο εργασίας σε Java χρησιμοποιώντας το Aspose.Cells,
  διατηρώντας τον πίνακα Pivot, αντιγράφοντας τον Pivot σε νέο βιβλίο εργασίας και
  δημιουργώντας βιβλίο εργασίας από ένα φύλλο.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate worksheet
- how to copy pivot
- how to preserve pivot
- copy pivot to workbook
- create workbook from sheet
language: el
lastmod: 2026-08-17
og_description: Πώς να αντιγράψετε ένα φύλλο εργασίας σε Java χρησιμοποιώντας το Aspose.Cells,
  διατηρώντας τον πίνακα Pivot, αντιγράφοντας τον Pivot σε νέο βιβλίο εργασίας και
  δημιουργώντας βιβλίο εργασίας από ένα φύλλο—όλα τα βήματα εξηγούνται.
og_image_alt: Screenshot of Java code duplicating an Excel worksheet with a pivot
  table using Aspose.Cells
og_title: Πώς να αντιγράψετε φύλλο εργασίας και να διατηρήσετε τους πίνακες Pivot
  – Οδηγός Java
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  headline: How to duplicate worksheet and preserve pivot tables in Java
  type: TechArticle
- description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  name: How to duplicate worksheet and preserve pivot tables in Java
  steps:
  - name: – Load the workbook that contains the pivot table
    text: '```java import com.aspose.cells.*;'
  - name: – Create a new workbook and duplicate the entire worksheet
    text: '```java // Create an empty destination workbook Workbook destinationWorkbook
      = new Workbook();'
  - name: – Save the new workbook
    text: '```java // Save the duplicated workbook; the pivot remains functional destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
      } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
- Workbook
title: Πώς να αντιγράψετε ένα φύλλο εργασίας και να διατηρήσετε τους πίνακες Pivot
  σε Java
url: /el/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αντιγράψετε φύλλο εργασίας και να διατηρήσετε πίνακες Pivot σε Java

Η αντιγραφή ενός φύλλου εργασίας ενώ διατηρείται αμετάβλητος ο πίνακας Pivot είναι συχνή ανάγκη όταν αυτοματοποιείτε την αναφορά σε Excel. Αυτός ο οδηγός σας δείχνει πώς να αντιγράψετε έναν πίνακα Pivot σε ένα νέο βιβλίο εργασίας χρησιμοποιώντας το Aspose.Cells for Java, και επίσης καλύπτει πώς να διατηρήσετε τον Pivot όταν δημιουργείτε ένα βιβλίο εργασίας από ένα φύλλο.

Θα μάθετε πώς να φορτώσετε ένα υπάρχον βιβλίο εργασίας, να αντιγράψετε το φύλλο εργασίας που περιέχει έναν πίνακα Pivot και να αποθηκεύσετε το αποτέλεσμα ως νέο αρχείο. Το tutorial υποθέτει ότι έχετε ένα βασικό περιβάλλον ανάπτυξης Java και μια έγκυρη άδεια Aspose.Cells (η δωρεάν αξιολόγηση λειτουργεί για δοκιμές). Δεν απαιτούνται εξωτερικά εργαλεία πέρα από το Aspose.Cells JAR.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Java Development Kit (JDK) 8 ή νεότερο.
* Maven ή Gradle για τη διαχείριση της εξάρτησης Aspose.Cells.
* Ένα αρχείο Excel (`source.xlsx`) που περιέχει τουλάχιστον έναν πίνακα Pivot στο πρώτο φύλλο εργασίας.
* Έναν φάκελο όπου μπορείτε να διαβάσετε το αρχείο προέλευσης και να γράψετε το αντιγραμμένο βιβλίο εργασίας.

Προσθέστε την εξάρτηση Aspose.Cells στο `pom.xml` (Maven) ή στο `build.gradle` (Gradle). Για Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

## Πώς να αντιγράψετε φύλλο εργασίας με πίνακα Pivot

Η βασική λειτουργία είναι μια διαδικασία τριών βημάτων: φόρτωση, αντιγραφή και αποθήκευση. Κάθε βήμα εξηγείται παρακάτω.

### Βήμα 1 – Φόρτωση του βιβλίου εργασίας που περιέχει τον πίνακα Pivot

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceWorksheet = sourceWorkbook.getWorksheets().get(0);
```

*Γιατί είναι σημαντικό αυτό το βήμα*: Το αντικείμενο `Workbook` αντιπροσωπεύει ολόκληρο το αρχείο Excel. Ανακτώντας το πρώτο φύλλο εργασίας (`get(0)`), στοχεύετε στο φύλλο που περιέχει τον πίνακα Pivot που θέλετε να αντιγράψετε.

### Βήμα 2 – Δημιουργία νέου βιβλίου εργασίας και αντιγραφή ολόκληρου του φύλλου εργασίας

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // Duplicate the source worksheet, preserving its pivot table
        destinationWorkbook.getWorksheets().addCopy(sourceWorksheet);
```

`addCopy` κλωνοποιεί το φύλλο εργασίας **συμπεριλαμβανομένων** όλων των ενσωματωμένων αντικειμένων, τύπων και κρυπτοθηκών Pivot. Αυτή είναι η συνιστώμενη μέθοδος για **πώς να αντιγράψετε pivot** επειδή ο ορισμός του Pivot και η πηγή δεδομένων του μεταφέρονται μαζί.

### Βήμα 3 – Αποθήκευση του νέου βιβλίου εργασίας

```java
        // Save the duplicated workbook; the pivot remains functional
        destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
    }
}
```

Μετά την εκτέλεση, το `copy_with_pivot.xlsx` περιέχει ακριβή αντίγραφο του αρχικού φύλλου, και ο πίνακας Pivot λειτουργεί χωρίς πρόσθετη διαμόρφωση.

**Αναμενόμενο αποτέλεσμα**: Το άνοιγμα του `copy_with_pivot.xlsx` στο Excel εμφανίζει το αντιγραμμένο φύλλο εργασίας με την ίδια διάταξη Pivot, τα φίλτρα και τα υπολογιζόμενα πεδία όπως στο αρχικό αρχείο.

## Πώς να αντιγράψετε pivot σε άλλο βιβλίο εργασίας

Εάν χρειάζεται να μετακινήσετε έναν πίνακα Pivot χωρίς να αντιγράψετε ολόκληρο το φύλλο, μπορείτε να εξάγετε την κρυπτοθήκη Pivot και να την προσθέσετε σε ένα νέο φύλλο εργασίας. Το παρακάτω απόσπασμα κώδικα δείχνει αυτήν την προσέγγιση:

```java
// Assume sourceWorkbook and sourceWorksheet are already loaded
PivotTable pivot = sourceWorksheet.getPivotTables().get(0);

// Create a new workbook and a blank worksheet
Workbook targetWorkbook = new Workbook();
Worksheet targetSheet = targetWorkbook.getWorksheets().add("PivotCopy");

// Import the pivot table definition
targetSheet.getPivotTables().addCopy(pivot);
targetWorkbook.save("YOUR_DIRECTORY/pivot_only_copy.xlsx");
```

Αυτός ο κώδικας απαντά στο **πώς να αντιγράψετε pivot** αντιγράφοντας μόνο το αντικείμενο pivot, όχι ολόκληρο το φύλλο εργασίας. Η μέθοδος `addCopy` στη συλλογή `PivotTables` εξασφαλίζει ότι η κρυπτοθήκη pivot αντιγράφεται, ικανοποιώντας τις απαιτήσεις **πώς να διατηρήσετε pivot**.

## Πώς να διατηρήσετε pivot όταν δημιουργείτε βιβλίο εργασίας από ένα φύλλο

Κάποιες φορές ξεκινάτε με ένα φύλλο που δεν ανήκει σε βιβλίο εργασίας (π.χ., δημιουργείτε ένα φύλλο στη μνήμη). Για **create workbook from sheet** ενώ διατηρείτε τον Pivot, ακολουθήστε τα παρακάτω βήματα:

```java
// Create a worksheet in memory
Worksheet tempSheet = new Worksheet();
PivotTable pivot = tempSheet.getPivotTables().add("A1", "B10", "MyPivot");

// Configure the pivot source range, rows, columns, data fields, etc.
// (Omitted for brevity – see Aspose.Cells docs for detailed setup)

// Wrap the worksheet in a new workbook
Workbook newWorkbook = new Workbook();
newWorkbook.getWorksheets().addCopy(tempSheet);
newWorkbook.save("YOUR_DIRECTORY/created_from_sheet.xlsx");
```

Προσθέτοντας το φύλλο εργασίας σε ένα νέο `Workbook` αφού ο Pivot έχει οριστεί πλήρως, εξασφαλίζετε ότι το **πώς να διατηρήσετε pivot** λειτουργεί ακόμη και όταν το φύλλο προέρχεται εκτός υπάρχοντος αρχείου.

## Πρακτικές συμβουλές και κοινά προβλήματα

| Συμβουλή | Γιατί είναι σημαντικό |
|----------|------------------------|
| Χρησιμοποιήστε `addCopy` αντί για `copy` | `addCopy` κλωνοποιεί την υποκείμενη κρυπτοθήκη pivot· ένα απλό `copy` μπορεί να χάσει τη σύνδεση με την πηγή δεδομένων. |
| Διατηρήστε τα αρχεία προέλευσης και προορισμού στο ίδιο σύστημα αρχείων | Οι σχετικές διαδρομές στην πηγή δεδομένων του pivot επιλύονται σωστά, μειώνοντας τα σφάλματα “source not found”. |
| Επαληθεύστε την κρυπτοθήκη του pivot μετά την αντιγραφή | Καλέστε `pivot.refresh()` εάν τα δεδομένα προέλευσης άλλαξαν μεταξύ της αντιγραφής και της αποθήκευσης. |
| Αποδεσμεύστε τα βιβλία εργασίας όταν τελειώσετε | `sourceWorkbook.dispose();` ελευθερώνει τους εγγενείς πόρους, κάτι που είναι σημαντικό για μεγάλα αρχεία. |

## Περιπτώσεις άκρων που μπορεί να αντιμετωπίσετε

* **Multiple worksheets with inter‑dependent pivots** – Αντιγράψτε κάθε φύλλο ξεχωριστά· οι κοινές κρυπτοθήκες αντιγράφονται αυτόματα, αλλά ίσως χρειαστεί να επαναορίσετε εξωτερικές συνδέσεις δεδομένων.
* **Pivot tables based on external SQL queries** – Βεβαιωθείτε ότι το περιβάλλον προορισμού μπορεί να προσπελάσει την ίδια βάση δεδομένων· διαφορετικά ο Pivot θα εμφανίσει σφάλματα “#REF!”.
* **Large workbooks (>100 MB)** – Χρησιμοποιήστε `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` για να μειώσετε την πίεση μνήμης κατά τη διαδικασία αντιγραφής.

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που ενσωματώνει όλα τα βήματα που συζητήθηκαν. Αποθηκεύστε το ως `CopyPivotTable.java`, προσαρμόστε τις διαδρομές αρχείων και εκτελέστε το με το αγαπημένο σας IDE ή μέσω `javac`/`java`.



## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να δημιουργήσετε πίνακες Pivot στο Excel χρησιμοποιώντας το Aspose.Cells for Java: Ένας ολοκληρωμένος οδηγός](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Πώς να ενημερώσετε την πηγή πίνακα Pivot του Excel με το Aspose.Cells for Java: Ένας ολοκληρωμένος οδηγός](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Πώς να εφαρμόσετε Slicers σε πίνακες Pivot χρησιμοποιώντας το Aspose.Cells for Java: Ένας ολοκληρωμένος οδηγός](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}