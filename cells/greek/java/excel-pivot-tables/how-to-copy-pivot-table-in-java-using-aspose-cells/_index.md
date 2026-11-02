---
category: general
date: 2026-07-06
description: Πώς να αντιγράψετε έναν πίνακα Pivot σε Java με το Aspose.Cells – βήμα‑βήμα
  οδηγός για την προγραμματική αντιγραφή πινάκων Pivot του Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- duplicate excel pivot
language: el
lastmod: 2026-07-06
og_description: Η αντιγραφή πίνακα Pivot σε Java με τη χρήση του Aspose.Cells σας
  επιτρέπει να δημιουργήσετε αντίγραφα πινάκων Pivot του Excel γρήγορα και αξιόπιστα.
og_image_alt: Screenshot of Java code copying an Excel pivot table with Aspose.Cells
og_title: Πώς να αντιγράψετε έναν πίνακα Pivot σε Java – Πλήρης οδηγός Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
    to duplicate Excel pivot tables programmatically.
  headline: How to copy pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
title: Πώς να αντιγράψετε έναν συγκεντρωτικό πίνακα σε Java χρησιμοποιώντας το Aspose.Cells
url: /el/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αντιγράψετε έναν πίνακα pivot σε Java χρησιμοποιώντας το Aspose.Cells

Έχετε αναρωτηθεί ποτέ **πώς να αντιγράψετε πίνακες pivot** μέσα σε ένα αρχείο Excel χωρίς να ανοίξετε το βιβλίο εργασίας χειροκίνητα; Δεν είστε οι μόνοι. Σε πολλές αλυσίδες αναφορών χρειάζεται να **διπλασιάσετε πίνακες pivot** του Excel επί τόπου — ίσως για να δημιουργήσετε ένα στιγμιότυπο, να το μετακινήσετε σε νέο φύλλο ή να δημιουργήσετε ένα πρότυπο για τους επόμενους χρήστες.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει ακριβώς αυτό. Χρησιμοποιώντας τη βιβλιοθήκη Aspose.Cells for Java θα φορτώσουμε ένα βιβλίο εργασίας, θα εντοπίσουμε την πηγή του εύρους pivot, θα το αντιγράψουμε σε νέα θέση και θα αποθηκεύσουμε το αποτέλεσμα. Χωρίς ασαφείς αναφορές, μόνο μια συγκεκριμένη λύση που μπορείτε να ενσωματώσετε στο πρόγραμμά σας σήμερα.

---

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

* **Java Development Kit (JDK) 8+** – ο κώδικας μεταγλωττίζεται με οποιοδήποτε πρόσφατο JDK.  
* **Aspose.Cells for Java** έκδοση 25.11 ή νεότερη – η μέθοδος `Range.copy` που υποστηρίζει πίνακες pivot εισήχθη σε αυτή την έκδοση.  
* Ένα αρχείο **input.xlsx** που ήδη περιέχει πίνακα pivot (μπορείτε να δημιουργήσετε έναν στο Excel για δοκιμή).  
* Ένα εργαλείο κατασκευής της επιλογής σας (Maven, Gradle ή απλό `javac`). Θα δείξουμε την εξάρτηση Maven για γρήγορη εκκίνηση.

```xml
<!-- Add this to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.12</version> <!-- Use the latest stable -->
</dependency>
```

---

## Βήμα 1: Φόρτωση του βιβλίου εργασίας προέλευσης

Το πρώτο που κάνουμε είναι να ανοίξουμε το αρχείο Excel που περιέχει τον αρχικό πίνακα pivot. Το Aspose.Cells αντιμετωπίζει το βιβλίο εργασίας ως αντικείμενο στη μνήμη, ώστε να μπορείτε να το χειριστείτε χωρίς να εκκινήσετε το Excel.

```java
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

> **Γιατί είναι σημαντικό:** Η φόρτωση του βιβλίου εργασίας μας δίνει πρόσβαση στα φύλλα, στα κελιά και, κυρίως, στην κρυφή μνήμη (cache) του pivot. Χωρίς αυτό το βήμα η βιβλιοθήκη δεν έχει τίποτα για να αντιγράψει.

---

## Βήμα 2: Λήψη του φύλλου που περιέχει το pivot

Αν το βιβλίο εργασίας σας έχει πολλά φύλλα, πρέπει να δείξετε στο σωστό. Εδώ απλώς παίρνουμε το πρώτο φύλλο, αλλά μπορείτε επίσης να χρησιμοποιήσετε `get("SheetName")` για αναζήτηση με όνομα.

```java
// Obtain the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **Pro tip:** Όταν εργάζεστε με πολλά φύλλα, αποθηκεύστε το δείκτη ή το όνομα σε αρχείο ρυθμίσεων ώστε να αποφύγετε το σκληρό κωδικοποίηση αριθμών.

---

## Βήμα 3: Ορισμός του εύρους προέλευσης που περιλαμβάνει τον πίνακα pivot

Από την έκδοση 25.11 το Aspose.Cells σας επιτρέπει να αντιμετωπίζετε έναν πίνακα pivot ως κανονικό εύρος κελιών. Καθορίστε τα κελιά πάνω‑αριστερά και κάτω‑δεξιά που περικλείουν ολόκληρο το pivot.

```java
// The range A1:D20 covers the whole pivot table in this example
Range sourceRange = worksheet.getCells().createRange("A1:D20");
```

> **Edge case:** Αν το pivot σας επεκτείνεται δυναμικά (π.χ. προστίθενται γραμμές αργότερα), σκεφτείτε να χρησιμοποιήσετε `worksheet.getPivotTables().get(0).getDataRange()` για να λάβετε το ακριβές εύρος προγραμματιστικά.

---

## Βήμα 4: Ορισμός του εύρους προορισμού όπου θα αντιγραφεί το pivot

Διαλέξτε οποιοδήποτε κενό κελί όπου θέλετε να εμφανιστεί το αντίγραφο του pivot. Σε αυτή τη demo ξεκινάμε στο **F1**, αφήνοντας κενό μεταξύ του αρχικού και του αντιγράφου.

```java
// Destination starts at cell F1 – adjust as needed
Range destinationRange = worksheet.getCells().createRange("F1");
```

> **Γιατί όχι νέο φύλλο;** Μπορείτε επίσης να δημιουργήσετε ένα νέο φύλλο (`workbook.getWorksheets().add("Copy")`) και να χρησιμοποιήσετε τα κελιά του ως προορισμό. Η ίδια μέθοδος `copy` λειτουργεί και μεταξύ διαφορετικών φύλλων.

---

## Βήμα 5: Αντιγραφή του πίνακα pivot στη νέα θέση

Τώρα συμβαίνει η μαγεία. Η μέθοδος `copy` κλωνοποιεί το pivot, τη μνήμη του, τη μορφοποίηση και ακόμη και τυχόν συνδεδεμένα slicers (από την τελευταία έκδοση).

```java
// Perform the copy – the pivot is now duplicated at the destination
sourceRange.copy(destinationRange);
```

> **Important:** Η λειτουργία αντιγραφής είναι *deep*· **δεν** δημιουργεί αναφορά πίσω στο αρχικό pivot. Μπορείτε να τροποποιήσετε το νέο pivot ανεξάρτητα χωρίς να επηρεάσετε την πηγή.

---

## Βήμα 6: Αποθήκευση του βιβλίου εργασίας με το διπλότυπο pivot

Τέλος, γράψτε το τροποποιημένο βιβλίο εργασίας στον δίσκο. Μπορείτε να αντικαταστήσετε το αρχικό ή να δημιουργήσετε νέο αρχείο· εδώ επιλέγουμε το δεύτερο ώστε το αρχικό να παραμείνει αμετάβλητο.

```java
// Save the workbook – the duplicated pivot lives in output.xlsx
workbook.save("YOUR_DIRECTORY/output.xlsx");
```

Όταν ανοίξετε το **output.xlsx** στο Excel, θα δείτε το αρχικό pivot στις στήλες A‑D και ένα τέλειο αντίγραφο που αρχίζει στη στήλη F. Και τα δύο pivots μπορούν να ανανεωθούν ξεχωριστά.

---

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι η πλήρης κλάση Java που μπορείτε να μεταγλωττίσετε και να εκτελέσετε άμεσα:

```java
import com.aspose.cells.*;

public class ExportPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Define the source range that includes the pivot table (supported from version 25.11)
        // Adjust the range to match your actual pivot dimensions
        Range sourceRange = worksheet.getCells().createRange("A1:D20");

        // Step 4: Define the destination range where the pivot table will be copied
        // Change "F1" to any starting cell you prefer
        Range destinationRange = worksheet.getCells().createRange("F1");

        // Step 5: Copy the pivot table to the new location
        sourceRange.copy(destinationRange);

        // Step 6: Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Το άνοιγμα του `output.xlsx` εμφανίζει το αρχικό pivot (A1:D20) και ένα ταυτόσημο pivot που αρχίζει στο F1. Και οι δύο πίνακες διατηρούν τα φίλτρα, τα στυλ και τα υπολογιζόμενα πεδία τους.

---

## Διαχείριση Συνηθισμένων Παραλλαγών

| Κατάσταση | Τι πρέπει να προσαρμόσετε |
|-----------|---------------------------|
| **Πολλαπλά pivots** στο ίδιο φύλλο | Επανάληψη μέσω `worksheet.getPivotTables()` και αντιγραφή του καθενός με το δικό του εύρος προορισμού. |
| **Δυναμικό εύρος δεδομένων** | Χρησιμοποιήστε `worksheet.getPivotTables().get(0).getDataRange()` για αυτόματη ανίχνευση της περιοχής προέλευσης. |
| **Αντιγραφή σε άλλο βιβλίο εργασίας** | Φορτώστε ένα δεύτερο αντικείμενο `Workbook`, δημιουργήστε φύλλο προορισμού, μετά καλέστε `sourceRange.copy(destWorksheet.getCells().createRange("A1"))`. |
| **Διατήρηση slicers** | Από την έκδοση 25.12, τα slicers αντιγράφονται αυτόματα όταν το εύρος τα περιλαμβάνει. Επαληθεύστε στο Excel μετά την αποθήκευση. |

---

## Pro Tips & Pitfalls

* **Έλεγχος έκδοσης:** Η μέθοδος `copy` που υποστηρίζει pivots προστέθηκε στο **Aspose.Cells 25.11**. Αν χρησιμοποιείτε παλαιότερη έκδοση, θα λάβετε εξαίρεση. Πάντα ελέγξτε την έκδοση `aspose-cells` στο `pom.xml`.  
* **Απόδοση:** Η αντιγραφή μεγάλων pivots μπορεί να καταναλώσει πολύ μνήμη. Αν χρειάζεστε μόνο τα δεδομένα, σκεφτείτε να εξάγετε το pivot σε επίπεδο πίνακα αντί να κλωνοποιήσετε ολόκληρο το αντικείμενο.  
* **Συμπεριφορά ανανέωσης:** Το αντίγραφο του pivot διατηρεί τη δική του μνήμη. Αν τροποποιήσετε τα υποκείμενα δεδομένα, καλέστε `pivotTable.refresh()` στο νέο pivot για επανυπολογισμό.  
* **Προβλήματα μορφοποίησης:** Ορισμένες προσαρμοσμένες μορφές αριθμών μπορεί να μην επιβιώσουν στην αντιγραφή σε πολύ παλιές εκδόσεις Excel (<2007). Δοκιμάστε με την έκδοση Excel του τελικού χρήστη.

---

## Συμπέρασμα

Τώρα έχετε μια ολοκληρωμένη, άκρη‑σε‑άκρη λύση για **πώς να αντιγράψετε πίνακες pivot** χρησιμοποιώντας το Aspose.Cells for Java, και έχετε δει πώς να **διπλασιάσετε πίνακες pivot** του Excel με λίγες γραμμές κώδικα. Η προσέγγιση λειτουργεί για μοναδικά ή πολλαπλά pivots, σε διαφορετικά φύλλα, ακόμη και μεταξύ βιβλίων εργασίας.

Επόμενα βήματα μπορεί να περιλαμβάνουν:

* Αυτοματοποίηση της αντιγραφής για κάθε pivot σε μια εργασία batch.  
* Προσθήκη κώδικα για μετονομασία του αντιγραφόμενου pivot (π.χ. `pivotTable.setName("Copy_of_Sales")`).  
* Ενσωμάτωση της διαδικασίας σε μια μεγαλύτερη υπηρεσία αναφορών που παράγει PDF ή CSV εξαγωγές.

Δοκιμάστε το, προσαρμόστε τα εύρη ώστε να ταιριάζουν στα πραγματικά σας δεδομένα, και αφήστε τη βιβλιοθήκη να κάνει το δύσκολο μέρος. Καλή προγραμματιστική!

## Τι Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}