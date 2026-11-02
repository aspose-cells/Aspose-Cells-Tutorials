---
category: general
date: 2026-09-18
description: πώς να αντιγράψετε έναν πίνακα Pivot σε Java με το Aspose.Cells – αντιγράψτε
  έναν πίνακα Pivot μεταξύ βιβλίων εργασίας γρήγορα και αξιόπιστα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy range between workbooks
- how to copy pivot
- copy pivot to workbook
- load excel workbook java
language: el
lastmod: 2026-09-18
og_description: πώς να αντιγράψετε έναν πίνακα Pivot σε Java χρησιμοποιώντας το Aspose.Cells.
  Ακολουθήστε αυτό το πλήρες σεμινάριο για να αντιγράψετε έναν πίνακα Pivot μεταξύ
  βιβλίων εργασίας με καθαρό κώδικα Java.
og_image_alt: Screenshot showing a Java IDE copying a pivot table between two Excel
  workbooks
og_title: Αντιγραφή πίνακα Pivot στη Java – οδηγός βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  headline: How to duplicate pivot in Java using Aspose.Cells
  type: TechArticle
- description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  name: How to duplicate pivot in Java using Aspose.Cells
  steps:
  - name: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
    text: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
  - name: '**Define the cell area** that encloses the pivot.'
    text: '**Define the cell area** that encloses the pivot.'
  - name: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
    text: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
  - name: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
    text: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
  - name: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
    text: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Πώς να αντιγράψετε έναν πίνακα Pivot σε Java χρησιμοποιώντας το Aspose.Cells
url: /el/java/excel-pivot-tables/how-to-duplicate-pivot-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αντιγράψετε pivot σε Java χρησιμοποιώντας το Aspose.Cells

Αν χρειάζεστε **πώς να αντιγράψετε pivot** σε μια εφαρμογή Java, αυτός ο οδηγός σας δείχνει τα ακριβή βήματα. Φορτώνοντας ένα βιβλίο εργασίας Excel, ορίζοντας την περιοχή κελιών του pivot και αντιγράφοντας αυτήν την περιοχή σε ένα νέο βιβλίο εργασίας, μπορείτε να μετακινήσετε έναν πίνακα pivot χωρίς να χάσετε τον ορισμό ή τα δεδομένα του.

Η αντιγραφή ενός πίνακα pivot είναι μια συνηθισμένη ανάγκη όταν δημιουργείτε αναφορές, αρχειοθετείτε αναλύσεις ή χωρίζετε ένα μεγάλο βιβλίο εργασίας σε μονάδες. Σε αυτό το tutorial θα μάθετε πώς να **copy range between workbooks**, πώς να **load Excel workbook Java**, και τις λεπτομέρειες του **how to copy pivot** με ασφάλεια.

Θα ολοκληρώσετε με ένα έτοιμο‑για‑εκτέλεση πρόγραμμα Java που δημιουργεί αντίγραφο ενός πίνακα pivot από το `Source.xlsx` στο `PivotCopied.xlsx` χρησιμοποιώντας το Aspose.Cells for Java.

## Προαπαιτούμενα

* JDK 8 ή νεότερο εγκατεστημένο.
* Maven (ή άλλο εργαλείο κατασκευής) για διαχείριση εξαρτήσεων.
* Aspose.Cells for Java έκδοση 23.10 ή νεότερη. Προσθέστε την ακόλουθη εξάρτηση Maven στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier> <!-- adjust classifier to your JDK version -->
</dependency>
```

* Ένα βιβλίο εργασίας προέλευσης (`Source.xlsx`) που περιέχει έναν πίνακα pivot στην περιοχή **A1:H30**.

## Πώς να αντιγράψετε pivot σε Java

Η βασική ιδέα είναι απλή:

1. **Load the source workbook** – αυτό σας δίνει πρόσβαση στο φύλλο εργασίας που περιέχει το pivot.
2. **Define the cell area** – η περιοχή κελιών που περιβάλλει το pivot.
3. **Create a destination workbook** – ένα κενό αρχείο που θα λάβει την αντιγραμμένη περιοχή.
4. **Copy the range** – το Aspose.Cells αντιγράφει αυτόματα τον ορισμό του pivot.
5. **Save the destination workbook** – έχετε πλέον ένα ξεχωριστό αρχείο με το ίδιο pivot.

Παρακάτω υπάρχει ένα πλήρες, εκτελέσιμο πρόγραμμα Java που ακολουθεί αυτά τα βήματα.

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {

    public static void main(String[] args) throws Exception {
        // ---------- Step 1: Load the source workbook ----------
        // Replace the path with the actual location of your source file.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWorkbook = new Workbook(srcPath);
        // The first worksheet (index 0) contains the pivot table.
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // ---------- Step 2: Define the cell area that contains the pivot ----------
        // The pivot occupies A1:H30 in the source sheet.
        CellArea srcRange = CellArea.create("A1", "H30");

        // ---------- Step 3: Create a new workbook for the copy ----------
        Workbook destWorkbook = new Workbook();               // creates a blank workbook
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // ---------- Step 4: Copy the range (pivot table is duplicated automatically) ----------
        // CopyOptions can be left default; it ensures that all formatting and pivot objects are preserved.
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // ---------- Step 5: Save the destination workbook ----------
        String destPath = "YOUR_DIRECTORY/PivotCopied.xlsx";
        destWorkbook.save(destPath);

        System.out.println("Pivot table duplicated successfully to " + destPath);
    }
}
```

### Γιατί λειτουργεί αυτό

* **Aspose.Cells** θεωρεί έναν πίνακα pivot ως μέρος της συλλογής κελιών του φύλλου εργασίας. Όταν καλείτε `copyRange`, η βιβλιοθήκη αντιγράφει όχι μόνο τις τιμές των κελιών αλλά και την υποκείμενη κρυφή μνήμη (cache) και τον ορισμό του pivot, έτσι ώστε το νέο βιβλίο εργασίας να περιέχει ένα πλήρως λειτουργικό αντίγραφο.
* Το αντικείμενο `CopyOptions` προεπιλεγμένα διατηρεί τύπους, μορφές και ενσωματωμένα αντικείμενα. Μπορείτε να το προσαρμόσετε (π.χ., `setCopyColumnWidths(true)`) εάν χρειάζεστε επιπλέον έλεγχο.

## Αντιγραφή περιοχής μεταξύ βιβλίων εργασίας – πιο βαθιά ματιά

Ενώ το παραπάνω παράδειγμα αντιγράφει ένα ενιαίο συνεχές μπλοκ, το `copyRange` μπορεί να χειριστεί οποιαδήποτε ορθογώνια περιοχή. Εάν το pivot σας εκτείνεται σε μη‑συνεχείς περιοχές, μπορείτε να καλέσετε το `copyRange` πολλές φορές ή να χρησιμοποιήσετε το `Worksheet.copy` για να αντιγράψετε ολόκληρο το φύλλο.

```java
// Example: copy the whole sheet, preserving all pivots and charts
srcWorksheet.copy(destWorksheet, new CopyOptions());
```

**Συμβουλή:** Κατά την αντιγραφή μεγάλων βιβλίων εργασίας, ενεργοποιήστε το `CopyOptions.setPreserveCellStyle(true)` για να αποφύγετε περιττή αντιγραφή στυλ, κάτι που μπορεί να βελτιώσει την απόδοση.

## Πώς να αντιγράψετε pivot σε βιβλίο εργασίας – διαχείριση πολλαπλών pivots

Εάν το φύλλο προέλευσης περιέχει περισσότερους από έναν πίνακα pivot, μπορείτε να επαναλάβετε τις πίνακες pivot του φύλλου και να αντιγράψετε καθέναν ξεχωριστά:

```java
for (int i = 0; i < srcWorksheet.getPivotTables().getCount(); i++) {
    PivotTable pt = srcWorksheet.getPivotTables().get(i);
    // Determine the range that the pivot occupies
    CellArea pivotArea = pt.getPivotTableArea();
    srcWorksheet.copyRange(pivotArea, destWorksheet, pt.getName() + "!A1", new CopyOptions());
}
```

Αυτή η προσέγγιση διασφαλίζει ότι κάθε pivot διατηρεί το αρχικό του όνομα και την πηγή δεδομένων.

## Φόρτωση βιβλίου εργασίας Excel σε Java – κοινά προβλήματα

* **File path separators:** Χρησιμοποιήστε διαγώνιες γραμμές (`/`) ή `File.separator` για να διατηρήσετε τον κώδικα ανεξάρτητο από την πλατφόρμα.
* **Missing license:** Το Aspose.Cells λειτουργεί σε λειτουργία αξιολόγησης, αλλά η έξοδος θα περιέχει υδατογράφημα. Καταχωρήστε μια άδεια με `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` πριν φορτώσετε το βιβλίο εργασίας για να αφαιρέσετε το υδατογράφημα.
* **Large files:** Για βιβλία εργασίας μεγαλύτερα από 100 MB, σκεφτείτε να χρησιμοποιήσετε `WorkbookFactory.create(InputStream, new LoadOptions(LoadFormat.XLSX))` με επιλογές streaming για να μειώσετε την κατανάλωση μνήμης.

## Πλήρης ανασκόπηση παραδείγματος από την αρχή μέχρι το τέλος

Συνδυάζοντας όλα, εδώ είναι το τελικό πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο IDE σας:

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {
    public static void main(String[] args) throws Exception {
        // Load license (optional, removes evaluation watermark)
        // License lic = new License();
        // lic.setLicense("Aspose.Total.Java.lic");

        // 1️⃣ Load source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // 2️⃣ Define pivot range (A1:H30)
        CellArea srcRange = CellArea.create("A1", "H30");

        // 3️⃣ Prepare destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the pivot (Aspose.Cells handles the pivot cache automatically)
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/PivotCopied.xlsx");

        System.out.println("Pivot table duplicated successfully.");
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Μετά την εκτέλεση, το `PivotCopied.xlsx` εμφανίζεται στον καθορισμένο φάκελο. Ανοίγοντας το στο Excel δείχνει την ίδια διάταξη πίνακα pivot, φίλτρα και δεδομένα όπως στο `Source.xlsx`. Όλα τα υπολογιζόμενα πεδία και η μορφοποίηση διατηρούνται.

## Συχνές ερωτήσεις

* **Does this work with older Excel formats (.xls)?**  
  Ναι. Το Aspose.Cells ανιχνεύει αυτόματα τη μορφή. Χρησιμοποιήστε `new Workbook("file.xls")` και η ίδια λογική αντιγραφής ισχύει.

* **What if the pivot references external data sources?**  
  Η αντιγραφή διατηρεί την αρχική αναφορά πηγής δεδομένων. Εάν το περιβάλλον προορισμού δεν μπορεί να προσεγγίσει αυτήν την πηγή, το pivot θα εμφανίσει σφάλματα `#REF!`. Για να το αποφύγετε, ανανεώστε το pivot μετά την αντιγραφή ή αλλάξτε την πηγή δεδομένων μέσω `PivotTable.setDataSource(...)`.

* **Can I copy a pivot to a specific sheet name?**  
  Απολύτως. Μετά τη δημιουργία του φύλλου προορισμού, μετονομάστε το:

  ```java
  destWorksheet.setName("ReportPivot");
  srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());
  ```

## Συμπέρασμα

Τώρα γνωρίζετε **how to duplicate pivot** πίνακες σε Java χρησιμοποιώντας το Aspose.Cells, πώς να **copy range between workbooks**, και τις βέλτιστες πρακτικές για **load Excel workbook Java**. Ακολουθώντας τη διαδικασία των πέντε βημάτων — φόρτωση, ορισμός, δημιουργία προορισμού, αντιγραφή και αποθήκευση — μπορείτε να αυτοματοποιήσετε τη δημιουργία αναφορών, την αρχειοθέτηση αναλύσεων ή το διαχωρισμό σύνθετων βιβλίων εργασίας χωρίς να χάσετε τη λειτουργικότητα του pivot.

Στη συνέχεια, εξερευνήστε συναφή θέματα όπως **copy pivot to workbook** με πολλαπλά φύλλα, ή ενσωματώστε το αντίγραφο pivot σε μια μεγαλύτερη αλυσίδα επεξεργασίας δεδομένων χρησιμοποιώντας το Apache POI για περιπτώσεις χωρίς Aspose. Πειραματιστείτε με διαφορετικές ρυθμίσεις `CopyOptions` για να βελτιστοποιήσετε την απόδοση σε τεράστια βιβλία εργασίας.

Καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Group Pivot Fields in Excel Workbooks Using Aspose.Cells for Java - Comprehensive Guide](/cells/english/java/data-analysis/aspose-cells-java-group-pivot-fields-excel-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}