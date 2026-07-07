---
category: general
date: 2026-07-03
description: Μάθετε πώς να επεκτείνετε έναν πίνακα στο Excel χρησιμοποιώντας Java.
  Αυτό το σεμινάριο καλύπτει την επέκταση του πίνακα σε σειρές, πώς να χρησιμοποιείτε
  την επέκταση και πώς να εισάγετε τύπο αποδοτικά.
draft: false
keywords:
- expand array in excel
- expand array to rows
- how to use expand
- how to insert formula
- set formula in cell
language: el
og_description: Επεκτείνετε τον πίνακα στο Excel χρησιμοποιώντας Java. Ακολουθήστε
  αυτόν τον οδηγό για να μάθετε πώς να χρησιμοποιείτε το expand, να ορίζετε τύπο σε
  κελί και να επεκτείνετε τον πίνακα σε γραμμές αμέσως.
og_title: Επέκταση Πίνακα στο Excel με Java – Πλήρης Οδηγός Προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to expand array in Excel using Java. This tutorial covers
    expand array to rows, how to use expand, and how to insert formula efficiently.
  headline: Expand Array in Excel with Java – Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to expand array in Excel using Java. This tutorial covers
    expand array to rows, how to use expand, and how to insert formula efficiently.
  name: Expand Array in Excel with Java – Step‑by‑Step Guide
  steps:
  - name: Why Use EXPAND?
    text: '`EXPAND` removes the tedious step of dragging the fill handle. It also
      works with dynamic arrays, meaning if your source array changes, the spilled
      range updates automatically. This is especially handy when generating reports
      programmatically.'
  - name: 1. Expanding a Horizontal Array to Multiple Columns
    text: 'If you need to **expand array to rows** *and* columns, just change the
      third argument:'
  - name: 2. Using a Named Range as the Source
    text: 'Instead of a literal `{1,2,3}`, you can reference a named range that may
      change at runtime:'
  - name: 3. Handling Non‑Numeric Data
    text: '`EXPAND` works with text as well. For example:'
  - name: 4. Avoiding Zero Fill with `IFERROR`
    text: 'If you’d rather see blanks instead of zeros, wrap the `EXPAND` in `IFERROR`:'
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
title: Επέκταση Πίνακα στο Excel με Java – Οδηγός Βήμα‑προς‑Βήμα
url: /el/java/spreadsheet-automation/expand-array-in-excel-with-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Επέκταση Πίνακα στο Excel με Java – Πλήρης Οδηγός Προγραμματισμού

Έχετε αναρωτηθεί ποτέ πώς να **επεκτείνετε έναν πίνακα στο Excel** χωρίς να σύρετε τα κελιά χειροκίνητα; Δεν είστε μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν πρόβλημα όταν πρέπει να δημιουργήσουν δυναμικό εύρος προγραμματιστικά—ειδικά τώρα που η νέα λειτουργία `EXPAND` του Excel είναι ακόμη φρέσκια. Σε αυτόν τον οδηγό θα σας δείξουμε ακριβώς **πώς να χρησιμοποιήσετε το EXPAND**, πώς να εισάγετε τον τύπο σε ένα φύλλο εργασίας και πώς να κάνετε το αποτέλεσμα να «χύνεται» στις γραμμές που θέλετε. Στο τέλος θα μπορείτε να **επεκτείνετε πίνακα σε γραμμές** με μία μόνο γραμμή κώδικα Java.

Θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα χρησιμοποιώντας τη βιβλιοθήκη Aspose.Cells for Java. Χωρίς ασαφείς αναφορές, μόνο συγκεκριμένος κώδικας που μπορείτε να αντιγράψετε‑επικολλήσετε, να μεταγλωττίσετε και να εκτελέσετε. Καθ' όλη τη διάρκεια θα εξηγήσουμε γιατί κάθε βήμα είναι σημαντικό, θα καλύψουμε περιπτώσεις όπως μη συνεχόμενοι πίνακες, και θα προσθέσουμε μερικές επαγγελματικές συμβουλές που δεν βρίσκονται στα επίσημα έγγραφα. Έτοιμοι; Ας βουτήξουμε.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

* Java 17 (ή οποιοδήποτε πρόσφατο JDK) εγκατεστημένο.
* Maven ή Gradle για τη διαχείριση εξαρτήσεων.
* Ένα έγκυρο άδεια χρήσης Aspose.Cells for Java (η δωρεάν δοκιμή λειτουργεί για δοκιμές).
* Βασική εξοικείωση με τύπους Excel—αν έχετε χρησιμοποιήσει `VLOOKUP` ή `SUMIF` πριν, είστε έτοιμοι.

Αν κάτι από αυτά σας φαίνεται άγνωστο, κάντε παύση και ρυθμίστε το πρώτα· το υπόλοιπο του οδηγού υποθέτει ότι είναι έτοιμο.

## Βήμα 1: Ρύθμιση του Maven Project και Προσθήκη Aspose.Cells

Για να διατηρήσουμε τα πράγματα οργανωμένα, δημιουργήστε ένα νέο Maven project με όνομα `ExpandArrayDemo`. Προσθέστε την εξάρτηση Aspose.Cells στο `pom.xml`:

```xml
<!-- pom.xml -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ExpandArrayDemo</artifactId>
    <version>1.0.0</version>
    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.12</version> <!-- Use the latest version -->
        </dependency>
    </dependencies>
</project>
```

> **Pro tip:** Αν χρησιμοποιείτε Gradle, η ίδια εξάρτηση φαίνεται ως `implementation 'com.aspose:aspose-cells:23.12'`.

Μόλις το Maven ολοκληρώσει τη λήψη, είστε έτοιμοι να γράψετε κώδικα Java που **θέτει τύπο σε κελί**.

## Βήμα 2: Δημιουργία Workbook και Πρόσβαση στο Πρώτο Worksheet

Το πρώτο κομμάτι κώδικα αντικατοπτρίζει το απόσπασμα που ήδη είδατε, αλλά θα προσθέσουμε ελέγχους ασφαλείας και σχόλια ώστε να καταλάβετε το *γιατί* πίσω από κάθε γραμμή.

```java
import com.aspose.cells.*;

public class ExpandArrayDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook – this gives us a blank Excel file.
        Workbook wb = new Workbook();

        // 2️⃣ Access the first worksheet (index 0). 
        //    If you ever need a different sheet, just change the index or name.
        Worksheet ws = wb.getWorksheets().get(0);

        // From here on we’ll work with ws (the active sheet).
```

*Γιατί είναι σημαντικό:* Η δημιουργία αντικειμένου `Workbook` διανέμει τις εσωτερικές δομές που χρειάζεται το Aspose για τη διαχείριση κελιών, τύπων και στυλ. Η πρόσβαση στο πρώτο φύλλο εργασίας είναι το πιο κοινό σημείο εκκίνησης, ειδικά όταν πειραματίζεστε.

## Βήμα 3: Εισαγωγή του Τύπου EXPAND – «Πώς να Εισάγετε Τύπο»

Τώρα έρχεται η καρδιά του οδηγού: **πώς να εισάγετε τύπο** που επεκτείνει έναν πίνακα. Η λειτουργία Excel `EXPAND` δέχεται τρία ορίσματα—πηγαίο array, απαιτούμενες γραμμές και απαιτούμενες στήλες. Στην περίπτωσή μας θέλουμε να επεκτείνουμε το `{1,2,3}` σε **5 γραμμές** και **1 στήλη**.

```java
        // 3️⃣ Put the EXPAND formula into cell A1.
        //    The formula string must be exactly as Excel would see it.
        String formula = "=EXPAND({1,2,3},5,1)";
        ws.getCells().putFormula("A1", formula);
```

Παρατηρήστε ότι χρησιμοποιήσαμε `putFormula` αντί για `putValue`. Αυτό λέει στο Aspose να αντιμετωπίσει τη συμβολοσειρά ως πραγματικό τύπο Excel, όχι ως απλό κείμενο. Η μέθοδος `putFormula` αναλύει αυτόματα τη συμβολοσειρά και αποθηκεύει το δέντρο τύπου εσωτερικά.

### Γιατί να Χρησιμοποιήσετε το EXPAND;

`EXPAND` αφαιρεί το κουραστικό βήμα του σύρματος του fill handle. Επίσης λειτουργεί με δυναμικούς πίνακες, πράγμα που σημαίνει ότι αν αλλάξει ο πηγαίος πίνακας, το «χυστό» εύρος ενημερώνεται αυτόματα. Αυτό είναι ιδιαίτερα χρήσιμο όταν δημιουργείτε αναφορές προγραμματιστικά.

## Βήμα 4: Εξαναγκασμός Υπολογισμού – Υλοποίηση του Αποτελέσματος

Όταν *θέτετε τύπο σε κελί* μέσω του API, το βιβλίο εργασίας δεν επαναϋπολογίζει αυτόματα. Πρέπει να ενεργοποιήσετε έναν κύκλο υπολογισμού ώστε ο πίνακας να **επεκταθεί σε γραμμές** και οι τιμές να εμφανιστούν στο φύλλο.

```java
        // 4️⃣ Recalculate the worksheet so the formula result is materialized.
        ws.getCells().calculate();
```

Αν παραλείψετε αυτό το βήμα, το άνοιγμα του παραγόμενου `.xlsx` στο Excel θα δείξει τον τύπο αλλά όχι τις «χυστές» τιμές μέχρι να πατήσετε **F9**. Καλώντας το `calculate()`, διασφαλίζετε ότι το βιβλίο εργασίας είναι έτοιμο για χρήση αμέσως.

## Βήμα 5: Αποθήκευση του Workbook και Επαλήθευση του Αποτελέσματος

Τέλος, γράψτε το workbook σε αρχείο και προαιρετικά εκτυπώστε τις «χυστές» τιμές στην κονσόλα για επαλήθευση.

```java
        // 5️⃣ Save the workbook to disk.
        String outPath = "ExpandArrayResult.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);

        // 6️⃣ (Optional) Read back the spilled values to prove it worked.
        for (int row = 0; row < 5; row++) {
            Cell cell = ws.getCells().get(row, 0); // Column A = index 0
            System.out.println("Row " + (row + 1) + ": " + cell.getStringValue());
        }
    }
}
```

Όταν εκτελέσετε το πρόγραμμα, θα πρέπει να δείτε την έξοδο στην κονσόλα:

```
Workbook saved to ExpandArrayResult.xlsx
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

Το Excel γεμίζει τις υπόλοιπες γραμμές με μηδενικά επειδή ο πηγαίος πίνακας είχε μόνο τρία στοιχεία. Αυτή είναι η προεπιλεγμένη συμπεριφορά του `EXPAND`. Αν προτιμάτε κενά αντί για μηδενικά, μπορείτε να τυλίξετε τον πίνακα σε `IFERROR` ή να χρησιμοποιήσετε τεχνικές `CHOOSE`—περισσότερα στο τμήμα «Προχωρημένες Παραλλαγές» παρακάτω.

## Προχωρημένες Παραλλαγές & Περιπτώσεις Ορίων

### 1. Επέκταση Οριζόντιου Πίνακα σε Πολλές Στήλες

Αν χρειάζεται να **επεκτείνετε πίνακα σε γραμμές** *και* στήλες, απλώς αλλάξτε το τρίτο όρισμα:

```java
ws.getCells().putFormula("B2", "=EXPAND({1,2,3},5,3)");
```

Τώρα η περιοχή «χύνεται» σε ένα μπλοκ 5 × 3, γεμίζοντας τα κενά κελιά με μηδενικά.

### 2. Χρήση Ονομαστικού Εύρους ως Πηγή

Αντί για κυριολεκτικό `{1,2,3}`, μπορείτε να αναφέρετε ένα ονομαστικό εύρος που μπορεί να αλλάξει κατά το χρόνο εκτέλεσης:

```java
ws.getCells().putFormula("C1", "=EXPAND(MySourceRange,10,1)");
```

Βεβαιωθείτε ότι το `MySourceRange` υπάρχει (μπορείτε να το δημιουργήσετε μέσω `ws.getNames().add("MySourceRange", "Sheet1!$D$1:$D$3")`).

### 3. Διαχείριση Μη‑Αριθμητικών Δεδομένων

`EXPAND` λειτουργεί και με κείμενο. Για παράδειγμα:

```java
ws.getCells().putFormula("D1", "=EXPAND({\"Jan\",\"Feb\",\"Mar\"},4,1)");
```

Η επιπλέον γραμμή θα εμφανιστεί ως κενή συμβολοσειρά, όχι ως μηδέν.

### 4. Αποφυγή Γέμισης με Μηδενικά με `IFERROR`

Αν προτιμάτε κενά αντί για μηδενικά, τυλίξτε το `EXPAND` σε `IFERROR`:

```java
ws.getCells().putFormula("E1", "=IFERROR(EXPAND({1,2,3},5,1), \"\")");
```

Τώρα οι γραμμές 4 και 5 θα είναι πραγματικά κενές.

## Συνηθισμένα Πιθανά Σφάλματα και Πώς να τα Αποφύγετε

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Ο τύπος δεν επαναϋπολογίζεται** | Παράλειψη του `ws.getCells().calculate()` | Πάντα να καλείτε `calculate()` μετά το `putFormula`. |
| **Μηδενικές τιμές όπου αναμένονται κενά** | Το `EXPAND` γεμίζει με μηδενικά εξ ορισμού | Χρησιμοποιήστε `IFERROR(..., "")` ή τυλίξτε με `CHOOSE`. |
| **Λάθος διεύθυνση κελιού** | Χρήση `"A0"` ή `"1A"` | Οι διευθύνσεις Excel ξεκινούν από 1· το Aspose απαιτεί μορφή `"A1"`. |
| **Ασυμφωνία έκδοσης βιβλιοθήκης** | Χρήση παλιάς έκδοσης Aspose.Cells που δεν υποστηρίζει `EXPAND` | Αναβαθμίστε στην πιο πρόσφατη έκδοση (23.12 τη στιγμή της συγγραφής). |

## Πλήρες Παράδειγμα Λειτουργίας (Όλα τα Βήματα Συνδυασμένα)

Παρακάτω βρίσκεται το ολοκληρωμένο, έτοιμο‑για‑αντιγραφή πρόγραμμα. Αποθηκεύστε το ως `ExpandArrayDemo.java`, μεταγλωττίστε και τρέξτε.

```java
import com.aspose.cells.*;

public class ExpandArrayDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook (blank Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = wb.getWorksheets().get(0);

        // Insert the EXPAND formula in A1 to expand {1,2,3} to 5 rows × 1 column
        ws.getCells().putFormula("A1", "=EXPAND({1,2,3},5,1)");

        // Force calculation so the array is materialized
        ws.getCells().calculate();

        // Save the workbook to disk
        String outPath = "ExpandArrayResult.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);

        // Verify the spilled values
        System.out.println("Spilled values:");
        for (int row = 0; row < 5; row++) {
            Cell cell = ws.getCells().get(row, 0); // Column A
            System.out.println("Row " + (row + 1) + ": " + cell.getStringValue());
        }
    }
}
```

Η εκτέλεση αυτού του προγράμματος παράγει ένα αρχείο Excel όπου **το κελί A1** περιέχει τον τύπο `EXPAND`, και οι γραμμές 1‑5 της στήλης A εμφανίζουν `1, 2, 3, 0, 0`. Ανοίξτε το αρχείο στο Excel για να δείτε το ίδιο αποτέλεσμα αμέσως—χωρίς χειροκίνητη σύρση.

## Συμπέρασμα

Μάθατε πώς να **επεκτείνετε πίνακα στο Excel** χρησιμοποιώντας Java, **πώς να χρησιμοποιήσετε το EXPAND**, και τα ακριβή βήματα για **να θέσετε τύπο σε κελί** και **να επεκτείνετε πίνακα σε γραμμές** προγραμματιστικά. Εκμεταλλευόμενοι το Aspose.Cells, αποφεύγετε τα αδύναμα UI κόλπα και αφήνετε τον κώδικα να κάνει τη βαριά δουλειά. Είτε δημιουργείτε μηχανή αναφορών, εργαλείο αυτόματης εισαγωγής δεδομένων ή προσαρμοσμένο γεννήτρια φύλλων, αυτή η τεχνική θα σας εξοικονομήσει αμέτρητες ώρες.

Τι ακολουθεί; Δοκιμάστε να αντικαταστήσετε τον στατικό πίνακα με ένα δυναμικό εύρος που αντλείται από άλλο φύλλο, πειραματιστείτε με «χυστές» πολλαπλών στηλών, ή συνδυάστε το `EXPAND` με `FILTER` για ισχυρούς μετασχηματισμούς δεδομένων. Ο ουρανός είναι το όριο, και τώρα έχετε μια σταθερή βάση για να χτίσετε πάνω της.

Έχετε ερωτήσεις ή θέλετε να μοιραστείτε μια ενδιαφέρουσα περίπτωση χρήσης; Αφήστε ένα σχόλιο.

## Τι Θα Πρέπει να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην δική σας υλοποίηση.

- [Πώς να Εισάγετε Γραμμές σε Excel Workbooks Χρησιμοποιώντας Aspose.Cells for Java](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)
- [Πώς να Εισάγετε Στήλη σε Excel Χρησιμοποιώντας Aspose.Cells for Java - Ένας Πλήρης Οδηγός](/cells/english/java/worksheet-management/aspose-cells-java-insert-column-excel/)
- [Πώς να Επιλέξετε Περιοχές Κελιών σε Excel Χρησιμοποιώντας Aspose.Cells for Java (Οδηγός 2023)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}