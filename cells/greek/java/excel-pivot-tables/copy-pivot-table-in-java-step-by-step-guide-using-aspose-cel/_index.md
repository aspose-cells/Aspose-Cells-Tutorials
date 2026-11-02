---
category: general
date: 2026-08-04
description: Αντιγράψτε πίνακα Pivot με το Aspose.Cells για Java. Μάθετε πώς να αντιγράψετε
  περιοχή Excel, να διπλασιάσετε πίνακα Pivot και να αντιγράψετε φύλλο εργασίας με
  Pivot σε λίγες μόνο γραμμές.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- copy excel range
- copy range java
- duplicate pivot table
- copy worksheet with pivot
language: el
lastmod: 2026-08-04
og_description: Αντιγραφή συγκεντρωτικού πίνακα χρησιμοποιώντας το Aspose.Cells για
  Java. Αυτό το σεμινάριο σας καθοδηγεί στη διαδικασία αντιγραφής μιας περιοχής Excel,
  της αντιγραφής ενός συγκεντρωτικού πίνακα και της διατήρησης όλων των δεδομένων
  σε νέο φύλλο εργασίας.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new worksheet
og_title: Αντιγραφή συγκεντρωτικού πίνακα σε Java – πλήρες σεμινάριο Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  headline: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  type: TechArticle
- description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  name: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  steps:
  - name: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
    text: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
  - name: Opening the file in Excel shows a new sheet named **CopySheet**.
    text: Opening the file in Excel shows a new sheet named **CopySheet**.
  - name: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
    text: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
  - name: All formatting, filters, and calculated fields are preserved.
    text: All formatting, filters, and calculated fields are preserved.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- PivotTable
- Data copying
title: Αντιγραφή συγκεντρωτικού πίνακα σε Java – βήμα‑βήμα οδηγός με τη χρήση του
  Aspose.Cells
url: /el/java/excel-pivot-tables/copy-pivot-table-in-java-step-by-step-guide-using-aspose-cel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αντιγραφή πίνακα pivot σε Java – βήμα‑βήμα οδηγός με χρήση Aspose.Cells

Αν χρειάζεστε **να αντιγράψετε έναν πίνακα pivot** από ένα φύλλο εργασίας σε άλλο σε Java, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε με το Aspose.Cells. Είτε δημιουργείτε αναφορές προγραμματιστικά είτε χτίζετε ένα εργαλείο μεταφοράς δεδομένων, θα δείτε ένα πλήρες, εκτελέσιμο παράδειγμα που διατηρεί τον ορισμό και τα δεδομένα του πίνακα pivot.

Η αντιγραφή ενός πίνακα pivot είναι περισσότερο από απλή αντιγραφή περιοχής κελιών· η υποκείμενη cache και η πηγή δεδομένων πρέπει να παραμείνουν αμετάβλητες. Σε αυτό το tutorial καλύπτουμε επίσης πώς να **αντιγράψετε ένα εύρος Excel**, πώς να **duplicate pivot table** μεταξύ φύλλων εργασίας, και πώς να **copy worksheet with pivot** χρησιμοποιώντας το ίδιο API.

## Προαπαιτούμενα

* Java Development Kit (JDK) 8 ή νεότερο.
* Maven ή Gradle για διαχείριση εξαρτήσεων.
* Aspose.Cells for Java (η τελευταία έκδοση, π.χ., 23.12). Προσθέστε την ακόλουθη συντεταγμένη Maven στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

* Ένα βιβλίο εργασίας προέλευσης (`Source.xlsx`) που περιέχει έναν πίνακα pivot στο πρώτο φύλλο εργασίας.

## Πώς να αντιγράψετε πίνακα pivot σε Java με Aspose.Cells

Η κύρια ιδέα είναι να αντιγράψετε το *source range* που περιβάλλει τον πίνακα pivot και στη συνέχεια να το επικολλήσετε σε ένα νέο φύλλο εργασίας. Το Aspose.Cells αντιγράφει αυτόματα την cache του pivot, έτσι το προκύπτον φύλλο περιέχει έναν πλήρως λειτουργικό **duplicate pivot table**.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the PivotTable
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

        // Step 2: Define the source range (including the PivotTable) to be copied
        // The range must cover the entire pivot table area, e.g., A1:G20
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)                 // first worksheet
                                    .getCells()
                                    .createRange("A1:G20");

        // Step 3: Add a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("CopySheet");

        // Step 4: Copy the source range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Step 5: Save the workbook with the copied PivotTable intact
        workbook.save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

### Γιατί λειτουργεί αυτό

* **Range copy includes the pivot cache** – Το Aspose.Cells αντιμετωπίζει έναν πίνακα pivot ως ειδικό αντικείμενο ενσωματωμένο στην περιοχή κελιών. Όταν καλείτε `Range.copy`, η βιβλιοθήκη αντιγράφει τόσο τα ορατά κελιά όσο και την κρυφή cache που τροφοδοτεί το pivot.
* **No manual recreation needed** – Δεν χρειάζεται να ξαναχτίσετε τα πεδία του pivot ή την πηγή δεδομένων· το αντίγραφο είναι έτοιμο να ανανεωθεί αμέσως.
* **Works with any Excel version** – Το παραγόμενο αρχείο ακολουθεί το πρότυπο Office Open XML (XLSX), έτσι το Excel 2007+ μπορεί να το ανοίξει χωρίς προειδοποιήσεις.

## Αντιγραφή εύρους Excel – επαναχρησιμοποίηση του ίδιου κώδικα για δεδομένα χωρίς pivot

Αν χρειάζεστε μόνο να **copy excel range** χωρίς πίνακα pivot, το ίδιο μοτίβο ισχύει. Απλώς προσαρμόστε τη διεύθυνση του εύρους στην περιοχή που θέλετε να αντιγράψετε.

```java
// Example: copy A1:D10 from Sheet1 to Sheet2
Range dataRange = workbook.getWorksheets()
                          .get(0)
                          .getCells()
                          .createRange("A1:D10");
Worksheet sheet2 = workbook.getWorksheets().add("DataCopy");
dataRange.copy(sheet2.getCells().createRange("A1"));
```

Η μέθοδος `copy` διατηρεί τύπους, μορφοποίηση και σχόλια, καθιστώντας την μια καθολική λύση για οποιοδήποτε τμήμα δεδομένων Excel.

## Duplicate pivot table σε πολλαπλά φύλλα εργασίας

Μερικές φορές χρειάζεται να **duplicate pivot table** πολλές φορές—π.χ., ένα ανά τμήμα. Επαναλάβετε (loop) πάνω στα προορισμένα φύλλα εργασίας και ξαναχρησιμοποιήστε την ίδια κλήση `sourceRange.copy`:

```java
String[] departments = {"Sales", "Marketing", "Finance"};
for (String dept : departments) {
    Worksheet ws = workbook.getWorksheets().add(dept + "Pivot");
    sourceRange.copy(ws.getCells().createRange("A1"));
}
```

Κάθε νέο φύλλο περιέχει ένα ανεξάρτητο pivot που μπορεί να ανανεωθεί ξεχωριστά. Η cache αντιγράφεται, έτσι οι αλλαγές σε ένα φύλλο δεν θα επηρεάσουν τα άλλα.

## Αντιγραφή φύλλου εργασίας με pivot – διατήρηση ρυθμίσεων επιπέδου φύλλου

Αν θέλετε να **copy worksheet with pivot** ενώ διατηρείτε επίσης τις ρυθμίσεις σελίδας, το πλάτος των στηλών και τις ονομαστικές περιοχές, χρησιμοποιήστε το `Worksheet.copy` αντί για χειροκίνητη αντιγραφή περιοχής. Αυτή η μέθοδος κλωνοποιεί ολόκληρο το φύλλο, συμπεριλαμβανομένου του πίνακα pivot.

```java
Worksheet original = workbook.getWorksheets().get(0);
Worksheet clone = workbook.getWorksheets().addCopy(original);
clone.setName("FullCopy");
workbook.save("YOUR_DIRECTORY/FullCopy.xlsx");
```

Το `addCopy` είναι χρήσιμο όταν το φύλλο εργασίας περιέχει γραφήματα, εικόνες ή προσαρμοσμένα στυλ που πρέπει να μεταφερθούν μαζί με το pivot.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **Απώλεια της cache του Pivot μετά την αντιγραφή** | Χρήση του `Cell.copy` σε μεμονωμένα κελιά (αντί για μια περιοχή) απορρίπτει την κρυφή cache. | Πάντα αντιγράψτε ολόκληρη τη *range* που περιβάλλει τον πίνακα pivot, όπως φαίνεται στο Βήμα 2. |
| **Περιοχή προέλευσης πολύ μικρή** | Η περιοχή δεν περιλαμβάνει την περιοχή δεδομένων του pivot, έτσι το νέο φύλλο εμφανίζει μόνο στατικές τιμές. | Επεκτείνετε τη διεύθυνση (π.χ., `A1:G20`) ώστε να καλύπτει ολόκληρο τον πίνακα pivot καθώς και τυχόν slicers ή φίλτρα. |
| **Ασυμφωνία έκδοσης βιβλίου εργασίας προορισμού** | Η αποθήκευση ως XLS (παραδοσιακό) αφαιρεί τις σύγχρονες δυνατότητες του pivot. | Αποθηκεύστε ως XLSX (προεπιλογή) ή ορίστε ρητά `SaveFormat.XLSX`. |
| **Κατεστραμμένη εξωτερική πηγή δεδομένων** | Το pivot δείχνει σε πηγή δεδομένων εκτός του βιβλίου εργασίας· η αντιγραφή δεν την ενσωματώνει. | Χρησιμοποιήστε `PivotTable.refreshData()` μετά την αντιγραφή, ή ενσωματώστε τα δεδομένα προέλευσης στο ίδιο βιβλίο εργασίας. |

## Αναμενόμενο αποτέλεσμα

Μετά την εκτέλεση του προγράμματος:

1. `CopyWithPivot.xlsx` εμφανίζεται στο `YOUR_DIRECTORY`.
2. Ανοίγοντας το αρχείο στο Excel εμφανίζεται ένα νέο φύλλο με όνομα **CopySheet**.
3. **CopySheet** περιέχει έναν πλήρως λειτουργικό πίνακα pivot που είναι ταυτόσιος με το αρχικό, έτοιμο για ανανέωση.
4. Όλη η μορφοποίηση, τα φίλτρα και τα υπολογιζόμενα πεδία διατηρούνται.

Αν ανοίξετε το `FullCopy.xlsx`, θα δείτε ένα πλήρες αντίγραφο του αρχικού φύλλου εργασίας, συμπεριλαμβανομένων τυχόν γραφημάτων ή εικόνων που υπήρχαν στο φύλλο προέλευσης.

## Περίληψη

* Μάθατε πώς να **copy pivot table** σε Java χρησιμοποιώντας το Aspose.Cells.
* Η ίδια προσέγγιση λειτουργεί για ένα απλό **copy excel range** ή σενάρια **copy range java**.
* Για μαζικές λειτουργίες, μπορείτε να **duplicate pivot table** σε πολλά φύλλα.
* Όταν χρειάζεστε ολόκληρο το φύλλο, **copy worksheet with pivot** χρησιμοποιώντας το `addCopy`.

## Επόμενα βήματα

* Εξερευνήστε το **PivotTable.refreshData()** για προγραμματιστική ενημέρωση της cache μετά την αντιγραφή.
* Συνδυάστε τη λογική αντιγραφής με το **Excel file streaming** για διαχείριση μεγάλων βιβλίων εργασίας χωρίς να φορτώνετε τα πάντα στη μνήμη.
* Δείτε την υποστήριξη του Aspose.Cells για **pivot slicers** εάν οι αναφορές σας βασίζονται σε διαδραστικά φίλτρα.

Νιώστε ελεύθεροι να προσαρμόσετε τον κώδικα στη δική σας δομή έργου, να πειραματιστείτε με διαφορετικά μεγέθη περιοχών, ή να τον ενσωματώσετε σε ένα μεγαλύτερο pipeline επεξεργασίας δεδομένων. Καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Ενημερώσετε την Πηγή του Πίνακα Pivot του Excel με Aspose.Cells για Java: Ένας Πλήρης Οδηγός](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Διαχείριση Πίνακα Pivot Excel Aspose Cells Java](/cells/hongkong/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [Δημιουργία Νέου Βιβλίου Εργασίας Excel – Αντιγραφή & Διπλασιασμός Πίνακα Pivot](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}