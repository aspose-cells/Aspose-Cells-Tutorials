---
category: general
date: 2026-06-30
description: Ταξινόμηση μοναδικών τιμών στο Excel χρησιμοποιώντας Java. Μάθετε πώς
  να ορίζετε τύπους, να επαναϋπολογίζετε τύπους και να δημιουργείτε μοναδική λίστα
  στο Excel με το Aspose.Cells.
draft: false
keywords:
- sort unique values excel
- how to set formula
- how to recalculate formulas
- generate unique list excel
- set array formula
language: el
og_description: Ταξινόμηση μοναδικών τιμών στο Excel με Java. Αυτός ο οδηγός δείχνει
  πώς να ορίσετε τύπο, να επαναϋπολογίσετε τύπους και να δημιουργήσετε μια μοναδική
  λίστα στο Excel σε λίγα λεπτά.
og_title: Ταξινόμηση μοναδικών τιμών Excel – Java tutorial για τύπους πίνακα
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  headline: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  type: TechArticle
- description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  name: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  steps:
  - name: How It Works
    text: '- `UNIQUE(B1:B10)` scans the range and returns a vertical array of distinct
      strings. - `SORT(...)` takes that array and orders it in ascending order. -
      Wrapping the whole thing in `=` and calling `setFormulaArray` tells Aspose.Cells
      to treat the result as a **spilled array**, just like Excel would.'
  - name: Empty Cells in the Source Range
    text: 'If `B1:B10` contains blanks, `UNIQUE` will treat them as a distinct entry.
      To ignore blanks, wrap the range with `FILTER`:'
  - name: Non‑Contiguous Data
    text: 'When your data lives in multiple columns, you can join them with `CHOOSE`
      or `TEXTJOIN` before applying `UNIQUE`. For example:'
  - name: ' ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Sort Excel Files by Cell Color Using Aspose.Cells Java&#58; A Comprehensive
      Guide](/cells/english/java/data-analysis/excel-file-sorting-aspose-cells-java/)
      - [Mastering Aspose.Cells Java&#58; How to Interrupt Formula Calculation in
      Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
      - [How to Create an Excel Data Validation List with Aspose.Cells for Java&#58;
      A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)

      {{< /blocks/products/pf/tutorial-page-section >}}'
    text: '{{< /blocks/products/pf/main-container >}} {{< /blocks/products/pf/main-wrap-class
      >}} {{< blocks/products/products-backtop-button >}}'
  type: HowTo
- questions:
  - answer: The `SORT` and `UNIQUE` functions are part of the Dynamic Array engine
      introduced in Excel 365. For legacy files you’d need to use classic array formulas
      like `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells
      can still evaluate them, but the syntax is more verbose.
    question: Does this work with older Excel versions (pre‑Office 365)?
  - answer: Absolutely. Just change the address in `cells.get("A1")`. The spilled
      array will always start at the cell you specify and expand right‑and‑down as
      needed.
    question: Can I set the array formula on a range other than `A1`?
  - answer: 'Replace the static range with a dynamic one, e.g., `B:B` or a named range.
      The formula becomes `=SORT(UNIQUE(B:B))`. Be cautious with whole‑column references
      on very large sheets; they can impact performance. --- ## Conclusion We’ve just
      covered **how to set formula** in Java to **sort unique values'
    question: What if my source data is larger than `B1:B10`?
  type: FAQPage
tags:
- Excel automation
- Java
- Aspose.Cells
title: Ταξινόμηση μοναδικών τιμών στο Excel – Πλήρης οδηγός Java για τον ορισμό τύπων
  πίνακα
url: /el/java/formulas-functions/sort-unique-values-excel-complete-java-guide-to-set-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ταξινόμηση Μοναδικών Τιμών στο Excel – Πλήρης Οδηγός Java για Ορισμό Πίνακα Τύπων

Έχετε αναρωτηθεί ποτέ πώς να **ταξινομήσετε μοναδικές τιμές Excel** χωρίς να σύρετε τύπους; Δεν είστε ο μόνος. Σε πολλές περιπτώσεις αναφοράς χρειάζεστε μια καθαρή, αλφαβητικά‑ταξινομημένη λίστα διακριτών καταχωρίσεων, και η χειροκίνητη εκτέλεση είναι επίπονη.  

Τα καλά νέα; Με λίγες γραμμές κώδικα Java μπορείτε να **ορίσετε τύπο πίνακα** σε ένα φύλλο εργασίας, μετά να **επαναϋπολογίσετε τους τύπους** ώστε η περιοχή που εκτίθεται (spilled range) να γεμίσει αυτόματα. Σε αυτό το tutorial θα περάσουμε από όλα — από τη δημιουργία ενός workbook μέχρι τη δημιουργία μιας μοναδικής λίστας με στυλ Excel — ώστε να ενσωματώσετε τη λύση απευθείας στην εφαρμογή σας.

## Τι Καλύπτει Αυτός ο Οδηγός

- Ρύθμιση ενός έργου Java με Aspose.Cells (η βιβλιοθήκη που τροφοδοτεί το απόσπασμα κώδικα).  
- Χρήση των συναρτήσεων `SORT` και `UNIQUE` μαζί για **δημιουργία μοναδικής λίστας Excel**.  
- Εφαρμογή **τύπου πίνακα** (array formula) σε ένα κελί προγραμματιστικά.  
- Εκκίνηση μιας διαδικασίας υπολογισμού ώστε το βήμα **πώς να επαναϋπολογίσετε τύπους** να συμβαίνει άμεσα.  
- Επαλήθευση του αποτελέσματος και προσαρμογή της λύσης για ειδικές περιπτώσεις όπως κενά κελιά ή μη συνεχόμενες περιοχές.

Στο τέλος αυτού του οδηγού θα μπορείτε να ενσωματώσετε μια έτοιμη‑για‑χρήση μέθοδο σε οποιαδήποτε υπηρεσία Java χρειάζεται να εξάγει καθαρά φύλλα Excel.

> **Pro tip:** Αν ήδη χρησιμοποιείτε Maven, η προσθήκη του Aspose.Cells ως εξάρτηση σας εξοικονομεί το χειροκίνητο χειρισμό αρχείων JAR.

---

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντικό |
|-------------|----------------|
| Java 8 ή νεότερη | Το Aspose.Cells στοχεύει σε Java 8+. |
| Maven (ή Gradle) | Απλοποιεί τη διαχείριση εξαρτήσεων. |
| Aspose.Cells for Java | Παρέχει τα API `Workbook`, `Worksheet` και τύπων που θα χρησιμοποιήσουμε. |
| Βασική εξοικείωση με συναρτήσεις Excel | Η κατανόηση των `SORT` και `UNIQUE` σας βοηθά να προσαρμόσετε τον κώδικα. |

> *Αν δεν έχετε ακόμη Aspose.Cells, προσθέστε αυτό στο `pom.xml`*:

```xml
<!-- Aspose.Cells for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- latest as of June 2026 -->
</dependency>
```

---

## Βήμα 1: Δημιουργία Νέου Workbook (Η διαδικασία Ορισμού Τύπου Ξεκινά Εδώ)

Πρώτα χρειάζεται ένα κενό workbook. Σκεφτείτε το ως το άδειο καμβά όπου αργότερα θα **ορίσουμε τύπο πίνακα** στο κελί `A1`.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // The rest of the steps follow...
```

> *Γιατί να δημιουργήσουμε νέο workbook;*  
> Εξασφαλίζει ένα καθαρό περιβάλλον, αποφεύγοντας κρυφούς τύπους που θα μπορούσαν να επηρεάσουν τα δεδομένα δοκιμής μας.

---

## Βήμα 2: Συμπλήρωση Δειγματικών Δεδομένων (Προαιρετικό αλλά Χρήσιμο)

Για να δείτε το αποτέλεσμα καθαρά, ας γεμίσουμε τη στήλη **B** με κάποιες διπλότυπες καταχωρίσεις.

```java
        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Sample data in B1:B10
        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }
```

> *Γιατί η στήλη B;*  
> Ο τύπος που θα γράψουμε αναφέρεται στο `B1:B10`, οπότε η τοποθέτηση των δεδομένων εκεί αντανακλά το κλασικό παράδειγμα Excel.

---

## Βήμα 3: Ορισμός Τύπου Πίνακα που **Ταξινομεί Μοναδικές Τιμές Excel**

Τώρα συμβαίνει η μαγεία. Συνδυάζουμε το `UNIQUE` (για αφαίρεση διπλοτύπων) με το `SORT` (για αλφαβητική σειρά). Η τελική έκφραση είναι ένας **τύπος πίνακα**, που σημαίνει ότι θα «χύνεται» (spill) αυτόματα στα γειτονικά κελιά.

```java
        // Step 3: Set an array formula that sorts the unique values from B1:B10
        // This is the core of “how to set formula” for our scenario.
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");
```

### Πώς Λειτουργεί

- `UNIQUE(B1:B10)` σαρώει την περιοχή και επιστρέφει έναν κάθετο πίνακα με διακριτές συμβολοσειρές.  
- `SORT(...)` παίρνει αυτόν τον πίνακα και τον ταξινομεί σε αύξουσα σειρά.  
- Τοποθετώντας όλο αυτό σε `=` και καλώντας `setFormulaArray` λέμε στο Aspose.Cells να το αντιμετωπίσει ως **spilled array**, όπως θα έκανε το Excel.

> **Σημείωση:** Αν χρησιμοποιείτε παλαιότερη έκδοση του Excel που δεν διαθέτει `SORT` ή `UNIQUE`, μπορείτε να επιστρέψετε σε `SORT(UNIQUE(...))` με τη συνάρτηση **LET** ή να χρησιμοποιήσετε κλασικούς τύπους πίνακα (`=INDEX(...)`). Το tutorial εστιάζει στην σύγχρονη προσέγγιση δυναμικών πινάκων επειδή είναι ο πιο καθαρός τρόπος για **δημιουργία μοναδικής λίστας Excel** σήμερα.

---

## Βήμα 4: Επαναϋπολογισμός Τύπων ώστε η Περιοχή που Χύνεται να Συμπληρωθεί

Αφού ο τύπος τοποθετηθεί, το workbook δεν τον αξιολογεί αυτόματα. Εδώ έρχεται το βήμα **πώς να επαναϋπολογίσετε τύπους**.

```java
        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();
```

Η κλήση `calculateFormula()` αναγκάζει το Aspose.Cells να τρέξει τη μηχανή Excel, γεμίζοντας τα κελιά `A1`, `A2`, … με τις ταξινομημένες μοναδικές τιμές.

> *Γιατί να μην βασιστούμε στην «τεμπέλικη» αξιολόγηση;*  
> Σε περιβάλλον διακομιστή συχνά χρειάζεστε τα δεδομένα έτοιμα για εξαγωγή (CSV, PDF, κλπ.) αμέσως μετά τον υπολογισμό, οπότε μια ρητή κλήση εγγυάται συνέπεια.

---

## Βήμα 5: Επαλήθευση του Αποτελέσματος (Προαιρετική Αποσφαλμάτωση)

Πάντα είναι καλή ιδέα να εκτυπώσετε τις «χυμένες» τιμές στην κονσόλα — ειδικά όταν μαθαίνετε μια νέα API.

```java
        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break; // stop at first empty cell
            System.out.println("- " + value);
            row++;
        }

        // Optionally, save the workbook to inspect in Excel
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

Η εκτέλεση του προγράμματος εκτυπώνει:

```
Sorted unique list:
- Apple
- Banana
- Cherry
- Date
- Elderberry
- Fig
- Grape
```

Ανοίξτε το `SortedUniqueValues.xlsx` και θα δείτε τα ίδια δεδομένα να «χέονται» από το `A1` προς τα κάτω.

---

## Διαχείριση Ειδικών Περιπτώσεων

### Κενά Κελιά στην Πηγή

Αν το `B1:B10` περιέχει κενά, το `UNIQUE` θα τα θεωρήσει ως ξεχωριστή καταχώρηση. Για να αγνοήσετε τα κενά, τυλίξτε την περιοχή με `FILTER`:

```java
cells.get("A1").setFormulaArray("=SORT(UNIQUE(FILTER(B1:B10, B1:B10<>\"\")))");
```

### Μη Συνεχόμενα Δεδομένα

Όταν τα δεδομένα σας βρίσκονται σε πολλαπλές στήλες, μπορείτε να τα ενώσετε με `CHOOSE` ή `TEXTJOIN` πριν εφαρμόσετε το `UNIQUE`. Για παράδειγμα:

```java
cells.get("A1").setFormulaArray(
    "=SORT(UNIQUE(CHOOSE({1,2}, B1:B10, C1:C10)))"
);
```

Αυτές οι προσαρμογές δείχνουν την ευελιξία του **πώς να ορίσετε τύπο** για πιο σύνθετα σενάρια.

---

## Πλήρες Παράδειγμα Εργασίας (Όλα τα Βήματα Συνδυασμένα)

Παρακάτω είναι το πλήρες, εκτελέσιμο πρόγραμμα Java. Αντιγράψτε‑και‑επικολλήστε το στο IDE σας, προσθέστε την εξάρτηση Aspose.Cells και τρέξτε *Run*.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2: Get the first worksheet and fill sample data
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }

        // Step 3: Set an array formula that sorts the unique values from B1:B10
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");

        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();

        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break;
            System.out.println("- " + value);
            row++;
        }

        // Save the workbook for visual verification
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

**Αναμενόμενο αποτέλεσμα** (εμφανίζεται στην κονσόλα) ταιριάζει με τη ταξινομημένη, αφαιρεμένη λίστα που συζητήσαμε νωρίτερα. Ανοίγοντας το παραγόμενο αρχείο Excel θα δείτε τις ίδιες τιμές να «χέονται» από το `A1` προς τα κάτω.

---

## Συχνές Ερωτήσεις

**Ε: Λειτουργεί αυτό με παλαιότερες εκδόσεις του Excel (πριν το Office 365);**  
Α: Οι συναρτήσεις `SORT` και `UNIQUE` είναι μέρος της μηχανής Dynamic Array που εισήχθη στο Excel 365. Για παλαιότερα αρχεία θα πρέπει να χρησιμοποιήσετε κλασικούς τύπους πίνακα όπως `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Το Aspose.Cells μπορεί ακόμη να τους αξιολογήσει, αλλά η σύνταξη είναι πιο εκτενής.

**Ε: Μπορώ να ορίσω τον τύπο πίνακα σε περιοχή διαφορετική από το `A1`;**  
Α: Φυσικά. Απλώς αλλάξτε τη διεύθυνση στο `cells.get("A1")`. Ο «χυμένος» πίνακας θα ξεκινά πάντα από το κελί που καθορίζετε και θα επεκτείνεται δεξιά‑και‑κάτω όπως χρειάζεται.

**Ε: Τι γίνεται αν τα δεδομένα πηγής είναι μεγαλύτερα από το `B1:B10`;**  
Α: Αντικαταστήστε την στατική περιοχή με μια δυναμική, π.χ. `B:B` ή μια ονομαστική περιοχή. Ο τύπος γίνεται `=SORT(UNIQUE(B:B))`. Να είστε προσεκτικοί με αναφορές σε ολόκληρη στήλη σε πολύ μεγάλα φύλλα· μπορεί να επηρεάσουν την απόδοση.

---

## Συμπέρασμα

Μόλις καλύψαμε **πώς να ορίσετε τύπο** σε Java για **ταξινόμηση μοναδικών τιμών Excel**, πώς να **επαναϋπολογίσετε τύπους**, και πώς να **δημιουργήσετε μοναδική λίστα Excel** χρησιμοποιώντας το ισχυρό API του Aspose.Cells. Τα βήματα είναι απλά: δημιουργήστε ένα workbook, γεμίστε τα δεδομένα, εφαρμόστε έναν τύπο πίνακα, ενεργοποιήστε τον υπολογισμό και ελέγξτε το αποτέλεσμα.  

Από εδώ μπορείτε να επεκτείνετε — προσθέστε μορφοποίηση υπό όρους, εξαγωγή σε PDF, ή ενσωματώστε τη μέθοδο σε μια web υπηρεσία που παρέχει έτοιμες αναφορές. Η βασική ιδέα παραμένει η ίδια: αφήστε τις δικές του συναρτήσεις του Excel να κάνουν το βαρέως φορτίου έργο, και αφήστε τη Java να συντονίζει τη διαδικασία.

Έτοιμοι να ανεβάσετε το επίπεδο της αυτοματοποίησης Excel; Δοκιμάστε να αντικαταστήσετε το `SORT` με `SORTBY` για ταξινόμηση κατά δευτερεύουσα στήλη, ή πειραματιστείτε με το `FILTER` για να εξαιρέσετε γραμμές που δεν πληρούν επιχειρηματικούς κανόνες. Οι δυνατότητες είναι πρακτικά απεριόριστες.

###

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}