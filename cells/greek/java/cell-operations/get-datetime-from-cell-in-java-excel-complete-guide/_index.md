---
category: general
date: 2026-06-08
description: Αποκτήστε ημερομηνία και ώρα από κελί χρησιμοποιώντας το Aspose.Cells
  Java και μάθετε πώς να γράψετε τιμή σε κελί Excel σε λίγα μόνο βήματα.
draft: false
keywords:
- get datetime from cell
- write value to excel cell
- Aspose.Cells Java date parsing
- Japanese era calendar Excel
- Excel formula recalculation Java
language: el
og_description: Λάβετε ημερομηνία/ώρα από κελί χρησιμοποιώντας το Aspose.Cells Java.
  Αυτό το σεμινάριο δείχνει επίσης πώς να γράψετε τιμή σε κελί Excel αποδοτικά.
og_title: Ανάκτηση ημερομηνίας και ώρας από κελί σε Java Excel – Πλήρης Οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Get datetime from cell using Aspose.Cells Java and learn how to write
    value to excel cell in just a few steps.
  headline: Get datetime from cell in Java Excel – Complete Guide
  type: TechArticle
- description: Get datetime from cell using Aspose.Cells Java and learn how to write
    value to excel cell in just a few steps.
  name: Get datetime from cell in Java Excel – Complete Guide
  steps:
  - name: What if the cell already contains a true Excel date?
    text: 'If `cell.getType()` returns `CellValueType.IS_DATE_TIME`, you can skip
      the recalculation step and read the value directly:'
  - name: How to process a whole column of era strings?
    text: 'Loop through the used range and apply the same settings once:'
  - name: Can I disable the Japanese era handling later?
    text: 'Yes—just flip the flag back:'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
title: Ανάκτηση ημερομηνίας και ώρας από κελί σε Java Excel – Πλήρης Οδηγός
url: /el/java/cell-operations/get-datetime-from-cell-in-java-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Λήψη ημερομηνίας/ώρας από κελί σε Java Excel – Πλήρης Οδηγός

Έχετε ποτέ χρειαστεί να **get datetime from cell** αλλά η τιμή φαίνεται σαν συμβολοσειρά ιαπωνικής εποχής; Δεν είστε μόνοι. Σε πολλά παλαιά φύλλα εργασίας οι ημερομηνίες αποθηκεύονται ως “Reiwa 3/04/01”, και η εξαγωγή ενός σωστού `java.time.LocalDateTime` από αυτό μπορεί να μοιάζει με αποκρυπτογράφηση μυστικού μηνύματος.  

Ευτυχώς, το Aspose.Cells for Java μπορεί να διαχειριστεί τη μετατροπή για εσάς, και ενώ είμαστε εδώ, θα σας δείξουμε επίσης πώς να **write value to excel cell** ώστε να μπορείτε να μεταφέρετε δεδομένα με ασφάλεια χωρίς να διασπάτε τη λογική του φύλλου.

Σε αυτό το tutorial θα μάθετε:

* Πώς να δημιουργήσετε ένα workbook και να στοχεύσετε ένα συγκεκριμένο worksheet.  
* Τα ακριβή βήματα για την ενεργοποίηση του ημερολογίου ιαπωνικής εποχής για ανάλυση.  
* Γιατί πρέπει να επαναϋπολογίσετε τους τύπους πριν διαβάσετε την ημερομηνία.  
* Πώς να γράψετε μια νέα τιμή πίσω σε ένα κελί χωρίς να χάσετε τη μορφοποίηση.  

Χωρίς εξωτερικά εργαλεία, χωρίς μαγεία—απλός κώδικας Java που μπορείτε να ενσωματώσετε σε οποιοδήποτε Maven project σήμερα.

---

## Προαπαιτήσεις

* **Java 8+** (το παράδειγμα χρησιμοποιεί το σύγχρονο API `java.time`).  
* **Aspose.Cells for Java** ≥ 23.9.0 – προσθέστε την εξάρτηση μέσω Maven ή Gradle.  
* Βασική εξοικείωση με τις έννοιες του Excel (worksheets, cells, formulas).  

Αν λείπει η βιβλιοθήκη, κατεβάστε την από το επίσημο αποθετήριο της Aspose:

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9.0</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Βήμα 1: Δημιουργία νέου workbook και πρόσβαση στο πρώτο worksheet

Για αρχή, χρειαζόμαστε ένα νέο αντικείμενο `Workbook`. Σκεφτείτε το ως το άνοιγμα ενός νέου αρχείου Excel στη μνήμη.

```java
// Step 1: Initialize workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

*Γιατί είναι σημαντικό:*  
Η δημιουργία του workbook προγραμματιστικά σας δίνει πλήρη έλεγχο των ρυθμίσεων πριν τα δεδομένα αγγίξουν το σύστημα αρχείων. Το πρώτο worksheet (`index 0`) είναι όπου θα δείξουμε τόσο την ανάγνωση όσο και τη γραφή.

---

## Βήμα 2: Εγγραφή συμβολοσειράς ημερομηνίας ιαπωνικής εποχής στο κελί A1

Τώρα θα **write value to excel cell** A1. Αυτό αντικατοπτρίζει ένα πραγματικό σενάριο όπου ένας χρήστης εισήγαγε χειροκίνητα “Reiwa 3/04/01”.

```java
// Step 2: Write the era date string into A1
Cell cell = worksheet.getCells().get("A1");
cell.putValue("Reiwa 3/04/01"); // raw string, not yet a date
```

*Γρήγορη συμβουλή:* `putValue` είναι ευέλικτο—δέχεται συμβολοσειρές, αριθμούς, ημερομηνίες και ακόμη και τύπους. Όταν περνάτε μια απλή συμβολοσειρά, το Aspose την αποθηκεύει ακριβώς όπως είναι, κάτι που είναι τέλειο για την επίδειξή μας.

---

## Βήμα 3: Ενεργοποίηση του ημερολογίου ιαπωνικής εποχής για ανάλυση ημερομηνίας

Από προεπιλογή, το Aspose.Cells χρησιμοποιεί το Γρηγοριανό ημερολόγιο. Για να καταλάβουμε το “Reiwa”, ενεργοποιούμε μια ρύθμιση.

```java
// Step 3: Turn on Japanese era calendar support
WorkbookSettings settings = workbook.getSettings();
settings.setUseJapaneseEraCalendar(true);
```

*Γιατί να το ενεργοποιήσετε;*  
Το ημερολόγιο ιαπωνικής εποχής αντιστοιχίζει τα ονόματα εποχών (Reiwa, Heisei, Showa) στα Γρηγοριανά ισοδύναμά τους. Χωρίς αυτή τη σημαία, η βιβλιοθήκη θα αντιμετωπίζει τη συμβολοσειρά ως απλό κείμενο, και δεν θα λάβετε ποτέ ένα σωστό αντικείμενο `DateTime`.

---

## Βήμα 4: Επαναϋπολογισμός τύπων ώστε η συμβολοσειρά εποχής να μετατραπεί σε Γρηγοριανή ημερομηνία

Το Aspose δεν μετατρέπει αυτόματα τη συμβολοσειρά σε ημερομηνία. Αντίθετα, αντιμετωπίζει το κελί ως αποτέλεσμα τύπου μετά από έναν υπολογισμό.

```java
// Step 4: Force a recalculation to convert the era string
workbook.calculateFormula(); // processes all cells, including A1
System.out.println(cell.getDateTime()); // → 2021‑04‑01
```

Όταν εκτελείται το `calculateFormula()`, η μηχανή αναγνωρίζει το μοτίβο εποχής, εφαρμόζει το ιαπωνικό ημερολόγιο και αποθηκεύει εσωτερικά την προκύπτουσα Γρηγοριανή ημερομηνία. Η κλήση `getDateTime()` επιστρέφει τότε ένα `java.util.Date` (ή μπορείτε να το μετατρέψετε σε `java.time`).

**Αναμενόμενη έξοδος**

```
2021-04-01T00:00:00.000+00:00
```

---

## Βήμα 5: Εγγραφή νέας τιμής πίσω στο ίδιο κελί (ή σε άλλο κελί)

Υποθέστε ότι πρέπει να αντικαταστήσετε την αρχική συμβολοσειρά με μια καθαρή ημερομηνία ISO‑8601. Εδώ είναι πώς να **write value to excel cell** με ασφάλεια, διατηρώντας το στυλ του κελιού.

```java
// Step 5: Overwrite A1 with a formatted date string
java.time.LocalDateTime now = java.time.LocalDateTime.now();
cell.putValue(now); // Aspose will store it as a proper Excel date
// Optional: apply a date format style
Style style = cell.getStyle();
style.setNumber(14); // built‑in "m/d/yyyy" format
cell.setStyle(style);
```

*Τι συμβαίνει;*  
`putValue` εντοπίζει τον τύπο `LocalDateTime` και τον μετατρέπει στην αριθμητική αναπαράσταση του Excel. Ο ορισμός της μορφής αριθμού εξασφαλίζει ότι το κελί εμφανίζει την ημερομηνία ακριβώς όπως περιμένετε όταν ανοίγει στο Excel.

---

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα, εδώ είναι μια μοναδική κλάση Java που μπορείτε να μεταγλωττίσετε και να εκτελέσετε. Δημιουργεί ένα workbook, γράφει μια συμβολοσειρά εποχής, τη μετατρέπει και τέλος αποθηκεύει το αρχείο.

```java
import com.aspose.cells.*;

public class JapaneseEraDateDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first sheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ Write Japanese era date string to A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue("Reiwa 3/04/01");

        // 3️⃣ Enable Japanese era calendar
        WorkbookSettings settings = workbook.getSettings();
        settings.setUseJapaneseEraCalendar(true);

        // 4️⃣ Recalculate so the string becomes a Gregorian date
        workbook.calculateFormula();
        System.out.println("Converted date: " + cell.getDateTime());

        // 5️⃣ Overwrite with a clean LocalDateTime (optional)
        java.time.LocalDateTime now = java.time.LocalDateTime.now();
        cell.putValue(now);
        Style style = cell.getStyle();
        style.setNumber(14); // m/d/yyyy
        cell.setStyle(style);

        // 6️⃣ Save the workbook
        workbook.save("output.xlsx");
        System.out.println("Workbook saved as output.xlsx");
    }
}
```

Τρέξτε το με `java -cp aspose-cells-23.9.jar;. JapaneseEraDateDemo` και ανοίξτε το **output.xlsx**. Θα δείτε το κελί A1 να εμφανίζει την τρέχουσα ημερομηνία, ενώ η κονσόλα καταγράφει την μετατρεπόμενη τιμή “2021‑04‑01”.

---

## Διαχείριση Ακραίων Περιπτώσεων & Συχνές Ερωτήσεις

### Τι γίνεται αν το κελί περιέχει ήδη μια πραγματική ημερομηνία Excel;

Αν το `cell.getType()` επιστρέφει `CellValueType.IS_DATE_TIME`, μπορείτε να παραλείψετε το βήμα επαναϋπολογισμού και να διαβάσετε την τιμή απευθείας:

```java
if (cell.getType() == CellValueType.IS_DATE_TIME) {
    System.out.println("Already a date: " + cell.getDateTime());
}
```

### Πώς να επεξεργαστείτε ολόκληρη στήλη συμβολοσειρών εποχής;

Κάντε βρόχο μέσω της χρησιμοποιημένης περιοχής και εφαρμόστε τις ίδιες ρυθμίσεις μία φορά:

```java
Range used = worksheet.getCells().getMaxDisplayRange();
for (int row = 0; row < used.getRowCount(); row++) {
    Cell c = used.getCell(row, 0); // column A
    c.putValue(c.getStringValue()); // re‑assign to trigger parsing
}
workbook.calculateFormula();
```

### Μπορώ να απενεργοποιήσω τη διαχείριση ιαπωνικής εποχής αργότερα;

Ναι—απλώς αλλάξτε ξανά τη σημαία:

```java
settings.setUseJapaneseEraCalendar(false);
```

Θυμηθείτε να επαναϋπολογίσετε ξανά αν αλλάξετε τη ρύθμιση μετά την εγγραφή δεδομένων.

---

## Επαγγελματικές Συμβουλές & Πιθανά Προβλήματα

* **Performance:** Η ενεργοποίηση του ημερολογίου ιαπωνικής εποχής προσθέτει μικρή επιβάρυνση. Αν το χρειάζεστε μόνο για λίγα κελιά, σκεφτείτε να ενεργοποιήσετε τη ρύθμιση, να επεξεργαστείτε, και μετά να την απενεργοποιήσετε.  
* **Locale awareness:** Η συμβολοσειρά εποχής πρέπει να ταιριάζει ακριβώς με το μοτίβο “EraName yy/MM/dd”. Λάθος ορθογραφία του “Reiwa” (π.χ., “Rewa”) θα αφήσει το κελί ως απλό κείμενο.  
* **Saving format:** `Workbook.save("output.xlsx")` γράφει αρχείο XLSX. Χρησιμοποιήστε `"output.xls"` αν χρειάζεστε την παλαιότερη δυαδική μορφή, αλλά σημειώστε ότι ορισμένες δυνατότητες (όπως η ανάλυση εποχής) μπορεί να είναι περιορισμένες.

---

## Συμπέρασμα

Τώρα ξέρετε πώς να **get datetime from cell** όταν η πηγή χρησιμοποιεί σημειογραφία ιαπωνικής εποχής, και επίσης είδατε έναν καθαρό τρόπο να **write value to excel cell** με σωστή μορφοποίηση. Με την εναλλαγή του `setUseJapaneseEraCalendar(true)` και την εξαναγκαστική επαναϋπολογισμό τύπων, το Aspose.Cells γεφυρώνει το χάσμα μεταξύ παλαιών συμβολοσειρών εποχής και σύγχρονων Γρηγοριανών ημερομηνιών—όλα με λίγες γραμμές Java.

Τι ακολουθεί; Δοκιμάστε να επεκτείνετε αυτό το μοτίβο σε άλλα πολιτιστικά ημερολόγια (Thai, Hijri) ή να επεξεργαστείτε μαζικά μεγάλα workbooks χρησιμοποιώντας την ίδια προσέγγιση. Οι ίδιες αρχές—ενεργοποίηση του σωστού ημερολογίου, επαναϋπολογισμός, έπειτα ανάγνωση/εγγραφή—εφαρμόζονται παντού.

Έχετε μια δύσκολη μορφή ημερομηνίας που δεν μπορείτε να αποκρυπτογραφήσετε; Αφήστε ένα σχόλιο παρακάτω και ας το λύσουμε μαζί. Καλή προγραμματιστική!

![Παράδειγμα λήψης ημερομηνίας/ώρας από κελί](https://example.com/images/get-datetime-from-cell.png "Παράδειγμα λήψης ημερομηνίας/ώρας από κελί")

## Τι Θα Μάθετε Στη Σύντομη Επόμενη Φάση;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας projects.

- [Κατακτήστε το Σύστημα Ημερομηνίας 1904 στο Excel Χρησιμοποιώντας Aspose.Cells Java για Αποτελεσματικές Λειτουργίες Κελιών](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Πώς να Εφαρμόσετε Αναδρομικό Υπολογισμό Κελιών στο Aspose.Cells Java για Βελτιωμένη Αυτοματοποίηση Excel](/cells/english/java/calculation-engine/aspose-cells-java-recursive-cell-calculations/)
- [Πώς να Μετατρέψετε Ονόματα Κελιών Excel σε Δείκτες Χρησιμοποιώντας Aspose.Cells για Java: Οδηγός Βήμα‑Βήμα](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}