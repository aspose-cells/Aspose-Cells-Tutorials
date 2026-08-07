---
category: general
date: 2026-06-21
description: Πώς να χρησιμοποιήσετε το WRAPCOLS με το Aspose.Cells Java για να μετατρέψετε
  έναν πίνακα σε σειρές, να γράψετε τύπο σε κελί και να γεμίσετε κελιά με τύπο – βήμα‑βήμα
  οδηγός.
draft: false
keywords:
- how to use wrapcols
- convert array to rows
- write formula to cell
- excel wrapcols example
- populate cells with formula
language: el
og_description: Πώς να χρησιμοποιήσετε το WRAPCOLS στη Java με το Aspose.Cells για
  να μετατρέψετε έναν πίνακα σε σειρές, να γράψετε έναν τύπο σε ένα κελί και να γεμίσετε
  κελιά με τύπο—όλα σε έναν οδηγό.
og_title: Πώς να χρησιμοποιήσετε το WRAPCOLS στη Java – Πλήρες παράδειγμα WRAPCOLS
  σε Excel
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  headline: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  type: TechArticle
- description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  name: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  steps:
  - name: What the Formula Does
    text: '- `{1,2,3}` – a literal array containing three numbers. - `2` – the number
      of columns per row. - Result: - **A1** = 1, **B1** = 2 - **A2** = 3, **B2**
      = (blank)'
  - name: 1. Empty Arrays
    text: 'If the array literal is empty (`{}`), `WRAPCOLS` returns a `#VALUE!` error.
      To avoid breaking your sheet, guard the formula generation:'
  - name: 2. Non‑Numeric Data
    text: '`WRAPCOLS` works with text as well. For example, `WRAPCOLS({"A","B","C","D"},2)`
      produces a two‑column layout of strings. Just remember to quote strings inside
      the array literal.'
  - name: 3. Compatibility
    text: The `WRAPCOLS` function is available in Excel 365 and Excel 2019+ (Office
      2019, Excel for the web). If you need to support older versions, you’ll have
      to fall back to manual looping or use a different spill‑compatible function.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel formulas
- WRAPCOLS
title: Πώς να χρησιμοποιήσετε το WRAPCOLS σε Java – Πλήρες παράδειγμα Excel WRAPCOLS
url: /el/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε το WRAPCOLS σε Java – Πλήρες Παράδειγμα Excel WRAPCOLS

Έχετε αναρωτηθεί **πώς να χρησιμοποιήσετε το WRAPCOLS** όταν χρειάζεται να μετατρέψετε έναν απλό πίνακα σε μια τακτοποιημένη λίστα στο Excel; Δεν είστε οι μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν δυσκολίες όταν βλέπουν για πρώτη φορά τη συνάρτηση `WRAPCOLS` και σκέφτονται: «Πώς θα γράψω αυτή τη φόρμουλα σε ένα κελί από τη Java;» Τα καλά νέα; Είναι αρκετά απλό μόλις γνωρίζετε τα σωστά βήματα.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρως εκτελέσιμο παράδειγμα Aspose.Cells για Java που **μετατρέπει έναν πίνακα σε σειρές**, γράφει τη φόρμουλα απευθείας σε ένα κελί και σας δείχνει πώς να **συμπληρώσετε κελιά με φόρμουλα** για πραγματικές περιπτώσεις. Στο τέλος θα έχετε μια σαφή εικόνα του **excel wrapcols example** και θα είστε έτοιμοι να το προσαρμόσετε στα δικά σας έργα.

## Προαπαιτούμενα

Πριν βουτήξουμε, βεβαιωθείτε ότι έχετε:

- Java 17 ή νεότερη (ο κώδικας λειτουργεί με οποιοδήποτε πρόσφατο JDK).
- Βιβλιοθήκη Aspose.Cells for Java (μπορείτε να κατεβάσετε το τελευταίο JAR από το Maven Central).
- Βασική κατανόηση της σύνταξης Java και των τύπων Excel.
- Ένα IDE ή απλό κειμενογράφο—δεν απαιτούνται ειδικά εργαλεία.

Τα έχετε όλα; Τέλεια, ας ξεκινήσουμε.

## Βήμα 1: Ρύθμιση του Έργου και Φόρτωση ενός Workbook

Πρώτα απ’ όλα—δημιουργήστε ένα νέο έργο Maven (ή Gradle) και προσθέστε την εξάρτηση Aspose.Cells:

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Τώρα μπορούμε να φορτώσουμε ένα υπάρχον workbook (ή να δημιουργήσουμε ένα καινούργιο) και να πάρουμε το πρώτο φύλλο εργασίας:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook (or create a new one)
        Workbook wb = new Workbook();               // creates a blank workbook
        // Alternatively, load an existing file:
        // Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);
```

> **Γιατί φορτώνουμε ένα workbook** – Η Aspose.Cells λειτουργεί με μια αναπαράσταση σε μνήμη ενός αρχείου Excel. Φορτώνοντας (ή δημιουργώντας) ένα workbook αποκτούμε πρόσβαση σε κελιά, σειρές και φόρμουλες, κάτι απαραίτητο για οποιαδήποτε λειτουργία **write formula to cell**.

## Βήμα 2: Εισαγωγή της Φόρμουλας WRAPCOLS σε Κελί

Η καρδιά του tutorial είναι η συνάρτηση `WRAPCOLS`. Παίρνει έναν μονοδιάστατο πίνακα και τον «τυλίγει» σε έναν καθορισμένο αριθμό στηλών, ρίχνοντας αυτόματα το υπόλοιπο σε νέες σειρές. Η σύνταξη που θα χρησιμοποιήσουμε είναι η εξής:

```java
// Step 3: Set a formula that wraps a collection into rows of 2 columns
// The formula WRAPCOLS({1,2,3},2) will produce:
//   Row 1: 1, 2
//   Row 2: 3
ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");
```

Παρατηρήστε πώς η φόρμουλα είναι ένα απλό string που περνιέται στο `setFormula`. Η Aspose.Cells κάνει το σκληρό κομμάτι—αναλύει τη φόρμουλα, την αξιολογεί και ρίχνει τα αποτελέσματα στο φύλλο. Αυτός είναι ο πιο άμεσος τρόπος για **populate cells with formula** χωρίς να χρειάζεται να κάνετε χειροκίνητη επανάληψη πάνω σε σειρές και στήλες.

### Τι Κάνει η Φόρμουλα

- `{1,2,3}` – ένας κυριολεκτικός πίνακας με τρία νούμερα.
- `2` – ο αριθμός των στηλών ανά σειρά.
- Αποτέλεσμα:
  - **A1** = 1, **B1** = 2
  - **A2** = 3, **B2** = (κενό)

Αν θέλετε τρεις στήλες αντί για δύο, απλώς αλλάξτε το δεύτερο όρισμα σε `3` και ο πίνακας θα γεμίσει μια μόνο σειρά.

## Βήμα 3: Αποθήκευση του Workbook και Έλεγχος του Αποτελέσματος

Τώρα που η φόρμουλα βρίσκεται στο **A1**, ας αποθηκεύσουμε το workbook στο δίσκο ώστε να το ανοίξετε στο Excel και να δείτε το αποτέλεσμα:

```java
        // (Optional) Save the workbook to see the result
        wb.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Ανοίξτε το `output.xlsx` και θα δείτε ακριβώς ό,τι περιγράφει το σχόλιο—δύο στήλες στην πρώτη σειρά και την υπόλοιπη τιμή στη δεύτερη σειρά. Αυτό είναι το ουσιώδες του **excel wrapcols example**.

## Βήμα 4: Επέκταση του Παραδείγματος – Μετατροπή Μεγαλύτερων Πινάκων

Στην πράξη σπάνια δουλεύουμε μόνο με τρία νούμερα. Ας υποθέσουμε ότι έχετε μια μεγαλύτερη συλλογή, π.χ. `{10,20,30,40,50,60,70}` και θέλετε τρεις στήλες ανά σειρά. Να πώς θα προσαρμόσετε τον κώδικα:

```java
String largeArray = "{10,20,30,40,50,60,70}";
int columnsPerRow = 3;
String formula = String.format("=WRAPCOLS(%s,%d)", largeArray, columnsPerRow);
ws.getCells().get("C5").setFormula(formula);
```

Τώρα η «ρίψη» ξεκινά στο **C5**, παράγοντας:

| C5 | D5 | E5 |
|----|----|----|
|10  |20  |30  |
|40  |50  |60  |
|70  |    |    |

Αυτό δείχνει πώς μπορείτε να **convert array to rows** δυναμικά, απλώς τροποποιώντας το string της φόρμουλας. Χωρίς βρόχους, χωρίς χειροκίνητες αναθέσεις κελιών—η Aspose.Cells διαχειρίζεται το υπόλοιπο.

## Βήμα 5: Διαχείριση Ακραίων Περιπτώσεων και Συχνών Παγίδων

### 1. Κενά Πίνακες

Αν ο κυριολεκτικός πίνακας είναι κενός (`{}`), η `WRAPCOLS` επιστρέφει σφάλμα `#VALUE!`. Για να αποφύγετε το σπάσιμο του φύλλου, προστατέψτε τη δημιουργία της φόρμουλας:

```java
if (arrayContent.isEmpty()) {
    ws.getCells().get("F1").setValue("No data");
} else {
    ws.getCells().get("F1").setFormula(formula);
}
```

### 2. Μη‑Αριθμητικά Δεδομένα

Η `WRAPCOLS` λειτουργεί και με κείμενο. Για παράδειγμα, `WRAPCOLS({"A","B","C","D"},2)` παράγει διάταξη δύο στηλών με συμβολοσειρές. Απλώς θυμηθείτε να βάζετε τα κείμενα σε εισαγωγικά μέσα στον κυριολεκτικό πίνακα.

### 3. Συμβατότητα

Η συνάρτηση `WRAPCOLS` είναι διαθέσιμη στο Excel 365 και στο Excel 2019+ (Office 2019, Excel για το web). Αν πρέπει να υποστηρίξετε παλαιότερες εκδόσεις, θα χρειαστεί να επιστρέψετε σε χειροκίνητους βρόχους ή να χρησιμοποιήσετε άλλη συνάρτηση συμβατή με spill.

## Βήμα 6: Πρακτικές Συμβουλές και Pro Tricks

- **Pro tip:** Χρησιμοποιήστε `Cell.setFormulaLocal` αν χρειάζεστε διαχωριστικό που εξαρτάται από την τοπική ρύθμιση (κόμμα vs ερωτηματικό) ανάλογα με τις περιφερειακές ρυθμίσεις του χρήστη.
- **Προσοχή:** Μην αντικαθιστάτε υπάρχοντα δεδομένα. Η περιοχή spill θα αντικαταστήσει οποιοδήποτε περιεχόμενο υπάρχει ήδη στην περιοχή-στόχο.
- **Σημείωση απόδοσης:** Η ρύθμιση μιας φόρμουλας είναι φθηνή· το σκληρό κομμάτι συμβαίνει όταν **αποθηκεύετε** ή **επαναϋπολογίζετε** το workbook. Αν δημιουργείτε χιλιάδες φόρμουλες, σκεφτείτε να απενεργοποιήσετε τον αυτόματο υπολογισμό (`wb.calculateFormula()` αργότερα) για να επιταχύνετε την επεξεργασία.

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω βρίσκεται η πλήρης, έτοιμη‑για‑εκτέλεση κλάση Java που ενσωματώνει όλα όσα συζητήσαμε:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook
        Workbook wb = new Workbook();

        // 2️⃣ Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // 3️⃣ Simple WRAPCOLS formula – basic excel wrapcols example
        ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");

        // 4️⃣ Larger array with three columns per row
        String largeArray = "{10,20,30,40,50,60,70}";
        int cols = 3;
        String largeFormula = String.format("=WRAPCOLS(%s,%d)", largeArray, cols);
        ws.getCells().get("C5").setFormula(largeFormula);

        // 5️⃣ Text array demonstration
        ws.getCells().get("G1").setFormula("=WRAPCOLS({\"Apple\",\"Banana\",\"Cherry\",\"Date\"},2)");

        // 6️⃣ Save the result
        wb.save("output.xlsx");
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Ανοίξτε το `output.xlsx` και θα δείτε τρεις ξεχωριστές περιοχές spill:

- **A1:B2** – αριθμοί 1‑3 τυλιγμένοι σε δύο στήλες.
- **C5:E7** – αριθμοί 10‑70 τυλιγμένοι σε τρεις στήλες.
- **G1:H2** – ονόματα φρούτων τυλιγμένα σε δύο στήλες.

## Συμπέρασμα

Καλύψαμε **πώς να χρησιμοποιήσετε το WRAPCOLS** με την Aspose.Cells για Java, δείχνοντάς σας πώς να **convert array to rows**, **write formula to cell**, και **populate cells with formula** με καθαρό, επαναχρησιμοποιήσιμο τρόπο. Η προσέγγιση εξαλείφει την κουραστική επανάληψη, αξιοποιεί τη φυσική συμπεριφορά spill του Excel και διατηρεί τον κώδικά σας σύντομο.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να συνδυάσετε το `WRAPCOLS` με δυναμικές πηγές δεδομένων—ίσως να αντλήσετε τιμές από μια βάση δεδομένων, να δημιουργήσετε το string του πίνακα κατά το χρόνο εκτέλεσης, και να αφήσετε το Excel να κάνει τη διάταξη. Μπορείτε επίσης να πειραματιστείτε με άλλες συναρτήσεις spill όπως `SEQUENCE` ή `FILTER` για πιο πλούσιες αναφορές.

Αν αντιμετωπίσετε δυσκολίες, αφήστε ένα σχόλιο παρακάτω ή εξερευνήστε την εκτενή τεκμηρίωση της Aspose. Καλό κώδικα και απολαύστε τη δύναμη των σύγχρονων τύπων Excel απευθείας από τη Java!

![πώς να χρησιμοποιήσετε το wrapcols παράδειγμα](/images/wrapcols-demo.png "πώς να χρησιμοποιήσετε το wrapcols σε Java – στιγμιότυπο δεδομένων που έχουν ριχτεί")


## Τι Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση στα δικά σας έργα.

- [How to Select Cell Ranges in Excel Using Aspose.Cells for Java (2023 Guide)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)
- [How to Set an Active Cell in Excel Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [How to Insert Rows into Excel Workbooks Using Aspose.Cells for Java](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}