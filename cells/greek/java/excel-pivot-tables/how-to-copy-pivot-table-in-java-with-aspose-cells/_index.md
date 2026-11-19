---
category: general
date: 2026-11-19
description: Μάθετε πώς να αντιγράψετε έναν συγκεντρωτικό πίνακα σε Java, διατηρώντας
  τα δεδομένα και τη διάταξή του. Αυτός ο οδηγός βήμα‑βήμα δείχνει επίσης πώς να αντιγράψετε
  αποδοτικά συγκεντρωτικούς πίνακες του Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- how to preserve pivot
- preserve pivot table
- copy excel pivot
language: el
lastmod: 2026-11-19
og_description: Αντιγράψτε τον πίνακα Pivot σε Java με το Aspose.Cells. Ακολουθήστε
  αυτόν τον οδηγό για να μάθετε πώς να διατηρείτε τους πίνακες Pivot και να αντιγράφετε
  τα δεδομένα του Excel Pivot με ακρίβεια.
og_image_alt: Illustration of the copy pivot table workflow in Java
og_title: Αντιγραφή πίνακα Pivot σε Java – πλήρης οδηγός Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy pivot table in Java while preserving its data and
    layout. This step‑by‑step guide also shows how to copy excel pivot tables efficiently.
  headline: How to copy pivot table in Java with Aspose.Cells
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Pivot tables
title: Πώς να αντιγράψετε έναν συγκεντρωτικό πίνακα σε Java με το Aspose.Cells
url: /el/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αντιγράψετε έναν πίνακα pivot σε Java με το Aspose.Cells

Αν χρειάζεστε να **copy pivot table** από ένα βιβλίο εργασίας σε άλλο, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε σε Java. Είτε δημιουργείτε μια μηχανή αναφορών είτε μεταφέρετε δεδομένα, θα δείτε έναν αξιόπιστο τρόπο για να διατηρήσετε την κρυφή μνήμη (cache) του pivot, τα πεδία και τη μορφοποίηση.

Η αντιγραφή ενός πίνακα pivot μπορεί να είναι δύσκολη επειδή μια απλή αντιγραφή περιοχής συχνά χάνει την υποκείμενη πηγή δεδομένων. Σε αυτό το tutorial θα χρησιμοποιήσουμε το Aspose.Cells για **how to copy pivot** διατηρώντας κάθε υπολογισμό αμετάβλητο, και θα καλύψουμε επίσης **how to preserve pivot** πίνακες όταν το βιβλίο εργασίας προορισμού είναι κενό.

## Προαπαιτούμενα

* Java 17 ή νεότερη έκδοση εγκατεστημένη.
* Aspose.Cells for Java (έκδοση 23.9 ή νεότερη) προστέθηκε στο classpath του έργου σας.
* Δύο αρχεία Excel: ένα βιβλίο εργασίας προέλευσης που περιέχει τον πίνακα pivot και ένα κενό βιβλίο εργασίας προορισμού (ή ένα βιβλίο εργασίας στο οποίο θέλετε να συγχωνεύσετε).

Δεν χρειάζεστε ειδική άδεια για το δείγμα κώδικα, αλλά μια έγκυρη άδεια Aspose.Cells αφαιρεί τα υδατογράμματα αξιολόγησης.

## Βήμα 1: Φορτώστε το βιβλίο εργασίας προέλευσης που περιέχει τον πίνακα pivot

Το πρώτο βήμα είναι να ανοίξετε το βιβλίο εργασίας που περιέχει το αρχικό pivot. Η φόρτωση του αρχείου σας δίνει πρόσβαση στο φύλλο εργασίας, τα κελιά και την κρυφή μνήμη (cache) του pivot.

```java
// Step 1: Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
```

*Γιατί είναι σημαντικό*: Το Aspose.Cells διαβάζει ολόκληρο το βιβλίο εργασίας, συμπεριλαμβανομένων των κρυφών δεδομένων cache που τροφοδοτούν το pivot. Χωρίς τη φόρτωση του πλήρους αρχείου, η λειτουργία αντιγραφής θα χάσει τον ορισμό του pivot.

## Βήμα 2: Προετοιμάστε το βιβλίο εργασίας προορισμού

Δημιουργήστε ένα νέο βιβλίο εργασίας (ή ανοίξτε ένα υπάρχον) και πάρτε το πρώτο του φύλλο εργασίας. Εδώ θα τοποθετηθεί το pivot.

```java
// Step 2: Create a new destination workbook and get its first worksheet
Workbook destWb = new Workbook();                     // empty workbook
Worksheet destWs = destWb.getWorksheets().get(0);    // first sheet
```

*Συμβουλή*: Εάν έχετε ήδη ένα βιβλίο εργασίας-στόχο, αντικαταστήστε την κλήση `new Workbook()` με `new Workbook("target.xlsx")`. Αυτό σας επιτρέπει να **copy excel pivot** σε ένα προ‑συμπληρωμένο βιβλίο εργασίας.

## Βήμα 3: Ορίστε την περιοχή κελιών που περιβάλλει τον πίνακα pivot

Πρέπει να καθορίσετε την ακριβή περιοχή που καλύπτει το pivot. Η περιοχή περιλαμβάνει τον πίνακα του pivot, τη λίστα πεδίων και τυχόν περιβάλλοντα δεδομένα που θέλετε να διατηρήσετε.

```java
// Step 3: Define the cell area that covers the pivot table in the source sheet
CellArea area = CellArea.createCellArea("A1", "H30"); // adjust as needed
```

*Γιατί είναι σημαντικό*: Το `CellArea` λέει στο Aspose.Cells τι να αντιγράψει. Εάν η περιοχή είναι πολύ μικρή, το pivot θα περικοπεί· εάν είναι πολύ μεγάλη, θα αντιγράψετε περιττά δεδομένα. Προσαρμόστε τις συντεταγμένες βάσει του πραγματικού μεγέθους του pivot.

## Βήμα 4: Εκτελέστε τη λειτουργία αντιγραφής με CopyOptions

Χρησιμοποιήστε τη μέθοδο `copy` στη συλλογή κελιών του φύλλου εργασίας προέλευσης. Η μεταβίβαση ενός νέου αντικειμένου `CopyOptions()` εξασφαλίζει ότι όλες οι μορφοποιήσεις, οι τύποι και η κρυφή μνήμη του pivot μεταφέρονται.

```java
// Step 4: Copy the defined range (including the pivot table) to the destination worksheet
srcWb.getWorksheets().get(0).getCells().copy(area, destWs.getCells(), new CopyOptions());
```

### Γιατί το `CopyOptions` διατηρεί το pivot

`CopyOptions` λέει στο Aspose.Cells να αντιμετωπίζει την περιοχή ως *ολόκληρο* αντικείμενο αντί για ένα επίπεδο σύνολο τιμών. Αυτό είναι το κλειδί για **how to preserve pivot** πίνακες: η υποκείμενη κρυφή μνήμη του pivot αντιγράφεται, ώστε το βιβλίο εργασίας προορισμού να μπορεί να επαναϋπολογίσει το pivot χωρίς χειροκίνητη παρέμβαση.

## Βήμα 5: Αποθηκεύστε το βιβλίο εργασίας προορισμού

Τέλος, γράψτε το αρχείο προορισμού στο δίσκο. Το αποθηκευμένο αρχείο θα περιέχει ένα πλήρως λειτουργικό αντίγραφο του αρχικού pivot.

```java
// Step 5: Save the destination workbook – the pivot table is preserved
destWb.save("YOUR_DIRECTORY/copied_with_pivot.xlsx");
```

*Αναμενόμενο αποτέλεσμα*: Το άνοιγμα του `copied_with_pivot.xlsx` στο Excel εμφανίζει τον ίδιο πίνακα pivot, πλήρη με slicers, φίλτρα και υπολογιζόμενα πεδία. Μπορείτε να το ανανεώσετε, και η πηγή δεδομένων θα δείχνει στην αντιγραμμένη περιοχή μέσα στο ίδιο βιβλίο εργασίας.

---

![Diagram showing copy pivot table process](/images/copy-pivot-table-workflow.png){.align-center width=600 alt="Diagram illustrating the copy pivot table workflow from source to destination workbook"}

## Πώς να αντιγράψετε πίνακες pivot σε πολλαπλά φύλλα εργασίας

Αν χρειάζεστε να **copy excel pivot** πίνακες από πολλά φύλλα, επαναλάβετε τα Βήματα 3‑4 για κάθε φύλλο προέλευσης. Μπορείτε επίσης να κάνετε βρόχο μέσω του `srcWb.getWorksheets()` και να αντιγράψετε κάθε pivot σε ένα αντίστοιχο φύλλο στο `destWb`. Ακολουθεί ένα σύντομο παράδειγμα βρόχου:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet srcWs = srcWb.getWorksheets().get(i);
    Worksheet newDestWs = destWb.getWorksheets().add();
    // Assume each pivot occupies A1:H30 – adjust per sheet if needed
    CellArea area = CellArea.createCellArea("A1", "H30");
    srcWs.getCells().copy(area, newDestWs.getCells(), new CopyOptions());
}
destWb.save("YOUR_DIRECTORY/multi_sheet_copy.xlsx");
```

*Pro tip*: Χρησιμοποιήστε το `srcWs.getPivotTables().getCount()` για να εντοπίσετε αν ένα φύλλο περιέχει πραγματικά pivot πριν την αντιγραφή. Αυτό αποτρέπει την αντιγραφή άσχετων δεδομένων.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **Pivot loses its cache** | Χρησιμοποιώντας το `Worksheet.copy()` χωρίς `CopyOptions` αντιγράφει μόνο τις τιμές των κελιών. | Πάντα χρησιμοποιείτε το `srcWs.getCells().copy(..., new CopyOptions())`. |
| **Destination shows #REF! errors** | Το αντιγραμμένο pivot εξακολουθεί να αναφέρεται στην εξωτερική πηγή δεδομένων του αρχικού βιβλίου εργασίας. | Μετά την αντιγραφή, καλέστε το `destWs.getPivotTables().get(0).refresh();` για να επανασυνδέσετε την κρυφή μνήμη στη νέα περιοχή. |
| **Slicers disappear** | Τα slicers αποθηκεύονται εκτός της κύριας περιοχής κελιών. | Επεκτείνετε το `CellArea` ώστε να περιλαμβάνει τις περιοχές των slicer, ή αντιγράψτε ολόκληρο το φύλλο (`srcWs.copy(destWs, new CopyOptions())`). |
| **Performance slowdown on large pivots** | Η αντιγραφή τεράστιων περιοχών με μορφοποίηση μπορεί να είναι αργή. | Χρησιμοποιήστε το `CopyOptions.setOnlyData(true)` εάν δεν χρειάζεστε μορφοποίηση, και στη συνέχεια εφαρμόστε ξανά τα στυλ χειροκίνητα. |

## Πώς να διατηρήσετε τη μορφοποίηση του πίνακα pivot κατά την ενημέρωση των δεδομένων

Μερικές φορές χρειάζεται να **how to preserve pivot** τη διάταξη μετά από αλλαγές στα δεδομένα προέλευσης. Μετά την αντιγραφή, μπορείτε να κλειδώσετε το στυλ του pivot:

```java
PivotTable pt = destWs.getPivotTables().get(0);
pt.setPreserveFormatting(true);   // keeps colors, fonts, and layout
pt.refresh();                     // recalculates with new data
```

Ο ορισμός του `PreserveFormatting` εξασφαλίζει ότι τυχόν προσαρμοσμένα στυλ που εφαρμόσατε στην προέλευση παραμένουν μετά την αντιγραφή.

## Επαλήθευση της αντιγραφής

Ένας γρήγορος τρόπος για να επιβεβαιώσετε ότι η αντιγραφή πέτυχε είναι να συγκρίνετε τους ορισμούς του pivot:

```java
PivotTable srcPt = srcWb.getWorksheets().get(0).getPivotTables().get(0);
PivotTable destPt = destWs.getPivotTables().get(0);

System.out.println("Source fields: " + srcPt.getFields().size());
System.out.println("Destination fields: " + destPt.getFields().size());
// Both numbers should match
```

Εάν οι μετρήσεις ταιριάζουν και το προορισμό ανοίγει χωρίς σφάλματα, έχετε επιτυχώς **copy pivot table**.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **copy pivot table** από ένα βιβλίο εργασίας Excel σε άλλο χρησιμοποιώντας το Aspose.Cells για Java, και έχετε δει τα ακριβή βήματα για **how to copy pivot** διασφαλίζοντας ότι η κρυφή μνήμη, η μορφοποίηση και τα slicers του pivot παραμένουν αμετάβλητα. Το ίδιο μοτίβο λειτουργεί για σενάρια **copy excel pivot** σε πολλαπλά φύλλα, και μπορείτε να προσαρμόσετε τον κώδικα για ειδικές περιπτώσεις όπως η διατήρηση της μορφοποίησης του pivot ή η διαχείριση μεγάλων συνόλων δεδομένων.

### Επόμενα βήματα

* Εξερευνήστε τις επιλογές **preserve pivot table** όπως `setPreserveFormatting` και `refresh` για δυναμικές πηγές δεδομένων.  
* Δοκιμάστε την αντιγραφή πινάκων pivot μεταξύ βιβλίων εργασίας με διαφορετική σειρά στηλών — προσαρμόστε το `CellArea` αναλόγως.  
* Συνδυάστε αυτήν την τεχνική με το Aspose.Slides για να ενσωματώσετε στιγμιότυπα pivot σε παρουσιάσεις PowerPoint.

Καλή προγραμματιστική, και μη διστάσετε να πειραματιστείτε με παραλλαγές ώστε να ταιριάζουν στο συγκεκριμένο pipeline αυτοματοποίησής σας!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να αντιγράψετε περιοχή και να διατηρήσετε έναν πίνακα pivot σε Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)
- [Πώς να αντιγράψετε έναν πίνακα pivot μεταξύ φύλλων εργασίας σε Java](/cells/english/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/)
- [Πώς να αντιγράψετε πίνακα pivot σε νέο βιβλίο εργασίας σε Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}