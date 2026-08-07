---
category: general
date: 2026-07-17
description: Πώς να χρησιμοποιήσετε το WRAPCOLS σε Java με το Aspose.Cells – δείτε
  ένα σαφές παράδειγμα Excel WRAPCOLS, καθώς και πώς να χρησιμοποιήσετε το WRAPROWS,
  να υπολογίσετε τύπους και να αποθηκεύσετε το βιβλίο εργασίας ως XLSX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- excel wrapcols example
- save workbook as xlsx
- how to use wraprows
- calculate formulas aspose.cells
language: el
lastmod: 2026-07-17
og_description: Πώς η χρήση του WRAPCOLS στο Aspose.Cells σας επιτρέπει να χωρίζετε
  δεδομένα σε στήλες· αυτό το σεμινάριο παρουσιάζει ένα πλήρες παράδειγμα Java, συμπεριλαμβανομένου
  του WRAPROWS, υπολογισμού τύπων και αποθήκευσης του βιβλίου εργασίας ως XLSX.
og_image_alt: Screenshot of Java code using WRAPCOLS and WRAPROWS in Aspose.Cells
  to create an XLSX file
og_title: Πώς να χρησιμοποιήσετε το WRAPCOLS στο Aspose.Cells – Οδηγός Java
schemas:
- author: Aspose
  dateModified: '2026-07-17'
  description: How to use WRAPCOLS in Java with Aspose.Cells – see a clear Excel WRAPCOLS
    example, plus how to use WRAPROWS, calculate formulas, and save workbook as XLSX.
  headline: How to Use WRAPCOLS in Aspose.Cells – Complete Java Example
  type: TechArticle
- description: How to use WRAPCOLS in Java with Aspose.Cells – see a clear Excel WRAPCOLS
    example, plus how to use WRAPROWS, calculate formulas, and save workbook as XLSX.
  name: How to Use WRAPCOLS in Aspose.Cells – Complete Java Example
  steps:
  - name: 1. Create a New Workbook and Access the First Worksheet
    text: Before any formulas can live in a sheet, you need a `Workbook` object. Think
      of it as the Excel file container.
  - name: 2. Apply the WRAPCOLS Function – Excel WRAPCOLS Example
    text: '`WRAPCOLS` takes an array and a column count, then spreads the values across
      that many columns. It’s ideal for turning a linear list into a matrix without
      looping manually.'
  - name: 3. Apply the WRAPROWS Function – How to Use WRAPROWS
    text: '`WRAPROWS` does the opposite: it spreads an array into a given number of
      rows. This can be handy when you need a vertical layout.'
  - name: 4. Calculate Formulas – calculate formulas aspose.cells
    text: Aspose.Cells does not evaluate formulas until you ask it to. By invoking
      `calculateFormula()`, you ensure that the wrap functions produce actual cell
      values you can read or export.
  - name: 5. Save the Workbook – save workbook as XLSX
    text: Now that the sheet is populated, it’s time to persist it. Aspose.Cells supports
      many formats; here we stick with the modern, widely compatible **XLSX**.
  - name: Handling Larger Arrays
    text: If your source array exceeds the target dimensions, Excel will continue
      spilling into additional rows/columns. For example, `WRAPCOLS({1..20},4)` creates
      a 5‑row by 4‑column block. Test with realistic data sizes to avoid unexpected
      overflow.
  - name: Empty or Null Arrays
    text: Passing an empty array (`{}`) returns a `#VALUE!` error. Guard against this
      by checking your data source before setting the formula.
  - name: Performance Considerations
    text: 'Calling `calculateFormula()` on a massive workbook can be expensive. If
      you only need the two wrap cells evaluated, you can limit the calculation scope:'
  - name: Licensing Note
    text: 'Aspose.Cells is a commercial library. The free trial imposes a watermark
      on the first few rows. For production, purchase a license and apply it early:'
  type: HowTo
- questions:
  - answer: Absolutely. They operate independently, so you can place each result wherever
      you like.
    question: Can I combine WRAPCOLS and WRAPROWS in the same sheet?
  - answer: 'Compute the column count in Java first, then inject it into the formula
      string: ```java int cols = 4; sheet.getCells().get("A1") .setFormula("=WRAPCOLS({1,2,3,4,5,6,7,8},
      " + cols + ")"); ```'
    question: What if I need dynamic column counts based on data size?
  - answer: 'Yes. Aspose.Cells supports over 500 functions, including newer dynamic
      array functions like `FILTER` and `SORT`. ## Wrap‑Up You now know **how to use
      WRAPCOLS** (and its sibling **WRAPROWS**) with Aspose.Cells for Java, how to
      **calculate formulas aspose.cells**, and the exact steps to **save workbo'
    question: Does `calculateFormula()` also evaluate other Excel functions?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Πώς να χρησιμοποιήσετε το WRAPCOLS στο Aspose.Cells – Πλήρες παράδειγμα Java
url: /el/java/formatting/how-to-use-wrapcols-in-aspose-cells-complete-java-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χρησιμοποιήσετε το WRAPCOLS στο Aspose.Cells – Πλήρες παράδειγμα Java

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε το WRAPCOLS** όταν χρειάζεται να μετασχηματίσετε μια επίπεδη λίστα σε μια τακτική διάταξη στηλών στο Excel; Δεν είστε ο μόνος. Πολλοί προγραμματιστές Java αντιμετωπίζουν αυτό το ακριβές εμπόδιο όταν δημιουργούν αναφορές με το Aspose.Cells. Τα καλά νέα; Η λύση είναι μερικές γραμμές κώδικα, και θα δείτε ένα πλήρες **παράδειγμα Excel WRAPCOLS** εδώ, μαζί με την συνοδευτική τεχνική **WRAPROWS**, τον υπολογισμό τύπων, και πώς να **αποθηκεύσετε το βιβλίο εργασίας ως XLSX**.

Σε αυτό το tutorial θα περάσουμε από κάθε βήμα — από τη δημιουργία ενός βιβλίου εργασίας, την εφαρμογή των δύο συναρτήσεων wrap, την ανάγκαση του Aspose.Cells να υπολογίσει τους τύπους, και τέλος την αποθήκευση του αρχείου. Στο τέλος θα έχετε ένα εκτελέσιμο πρόγραμμα Java που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο. Χωρίς ελλιπείς εισαγωγές, χωρίς ασαφείς αναφορές — μόνο μια σαφή, έτοιμη για αντιγραφή‑επικόλληση λύση.

## Τι θα χρειαστείτε

- Java 17 (ή οποιοδήποτε πρόσφατο JDK) – το API λειτουργεί το ίδιο και σε παλαιότερες εκδόσεις, αλλά το 17 είναι το ιδανικό.
- Aspose.Cells for Java 23.12 (ή νεότερο) – μπορείτε να κατεβάσετε μια δωρεάν δοκιμή από τον ιστότοπο της Aspose.
- Ένα IDE ή απλός επεξεργαστής κειμένου και ένα τερματικό για τη μεταγλώττιση/εκτέλεση του κώδικα.
- Δικαίωμα εγγραφής σε φάκελο όπου θα **αποθηκεύσετε το βιβλίο εργασίας ως XLSX**.

Αυτό είναι όλο. Αν τα έχετε ήδη, ας βουτήξουμε.

## Πώς να χρησιμοποιήσετε το WRAPCOLS – Βήμα‑Βήμα

Παρακάτω είναι η καρδιά του tutorial. Κάθε υπο‑ενότητα προσθέτει ένα μόνο κομμάτι λειτουργικότητας, εξηγεί *γιατί* το κάνουμε, και δείχνει το ακριβές Java που χρειάζεστε.

### 1. Δημιουργία νέου Workbook και πρόσβαση στο πρώτο Worksheet

Πριν οποιοσδήποτε τύπος μπορεί να ζήσει σε ένα φύλλο, χρειάζεστε ένα αντικείμενο `Workbook`. Σκεφτείτε το ως το δοχείο του αρχείου Excel.

```java
import com.aspose.cells.*;

public class WrapFunctionsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // in‑memory workbook
        Worksheet sheet = workbook.getWorksheets().get(0); // default first sheet
```

*Γιατί είναι σημαντικό:* Η δημιουργία ενός `Workbook` με τον προεπιλεγμένο κατασκευαστή σας δίνει ένα καθαρό βιβλίο εργασίας με ένα φύλλο, το οποίο είναι ιδανικό για σκοπούς επίδειξης. Αν έχετε ήδη ένα υπάρχον αρχείο, θα περάσετε τη διαδρομή του αρχείου στον κατασκευαστή.

### 2. Εφαρμογή της συνάρτησης WRAPCOLS – Παράδειγμα Excel WRAPCOLS

`WRAPCOLS` λαμβάνει έναν πίνακα και έναν αριθμό στηλών, και διανέμει τις τιμές σε αυτές τις στήλες. Είναι ιδανικό για τη μετατροπή μιας γραμμικής λίστας σε πίνακα χωρίς χειροκίνητο βρόχο.

```java
        // Step 2: Apply the WRAPCOLS function to cell A1 (wrap into 3 columns)
        sheet.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3,4,5,6},3)");
```

*Γιατί είναι σημαντικό:* Ο τύπος `=WRAPCOLS({1,2,3,4,5,6},3)` λέει στο Excel να τοποθετήσει τους αριθμούς 1‑6 σε τρεις στήλες, δημιουργώντας ένα μπλοκ 2‑γραμμών επί 3‑στηλών:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

Παρατηρήστε πώς χρησιμοποιούμε τη συντακτική μορφή κυριολεκτικού πίνακα `{…}`· το Aspose.Cells αντικατοπτρίζει τη δική του γλώσσα τύπων του Excel, ώστε να μπορείτε να αντιγράψετε/επικολλήσετε τύπους απευθείας από ένα βιβλίο εργασίας αν το επιθυμείτε.

### 3. Εφαρμογή της συνάρτησης WRAPROWS – Πώς να χρησιμοποιήσετε το WRAPROWS

`WRAPROWS` κάνει το αντίστροφο: διανέμει έναν πίνακα σε έναν δεδομένο αριθμό γραμμών. Αυτό μπορεί να είναι χρήσιμο όταν χρειάζεστε κατακόρυφη διάταξη.

```java
        // Step 3: Apply the WRAPROWS function to cell A2 (wrap into 2 rows)
        sheet.getCells().get("A2").setFormula("=WRAPROWS({1,2,3,4,5,6},2)");
```

*Γιατί είναι σημαντικό:* Η προκύπτουσα διάταξη είναι ως εξής:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |
| 5 | 6 |

Και οι δύο συναρτήσεις είναι *volatile* — επαναϋπολογίζονται αυτόματα όταν ανοίγει το βιβλίο εργασίας, αλλά θα αναγκάσουμε έναν υπολογισμό στην επόμενη ενότητα ώστε οι τιμές να υλοποιηθούν αμέσως.

### 4. Υπολογισμός τύπων – calculate formulas aspose.cells

Το Aspose.Cells δεν αξιολογεί τους τύπους μέχρι να το ζητήσετε. Καλώντας το `calculateFormula()`, εξασφαλίζετε ότι οι συναρτήσεις wrap παράγουν πραγματικές τιμές κελιών που μπορείτε να διαβάσετε ή να εξάγετε.

```java
        // Step 4: Calculate formulas so the results are materialized in the cells
        workbook.calculateFormula();   // triggers full workbook calculation
```

*Γιατί είναι σημαντικό:* Χωρίς αυτήν την κλήση, τα κελιά θα περιείχαν μόνο τη συμβολοσειρά του τύπου. Όταν ανοίξετε το παραγόμενο αρχείο στο Excel, θα δείτε τις σωστές τιμές, αλλά οποιοδήποτε αυτοματοποιημένο σύστημα που διαβάζει το αρχείο προγραμματιστικά θα δει ακόμα τους τύπους. Αυτό το βήμα εγγυάται ότι το βιβλίο εργασίας είναι πλήρως επιλυμένο.

### 5. Αποθήκευση του βιβλίου εργασίας – save workbook as XLSX

Τώρα που το φύλλο είναι γεμάτο, ήρθε η ώρα να το αποθηκεύσετε. Το Aspose.Cells υποστηρίζει πολλές μορφές· εδώ παραμένουμε στη σύγχρονη, ευρέως συμβατή **XLSX**.

```java
        // Step 5: Save the workbook to a file
        String outputPath = "YOUR_DIRECTORY/WrapFunctionsDemo.xlsx";
        workbook.save(outputPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

*Γιατί είναι σημαντικό:* Η χρήση του `SaveFormat.XLSX` εγγυάται ότι όλα τα νεότερα χαρακτηριστικά του Excel (συμπεριλαμβανομένων των δυναμικών πινάκων) διατηρούνται. Αν χρειάζεστε ένα παλαιότερο αρχείο `.xls`, απλώς αντικαταστήστε τη σταθερά μορφής.

#### Αναμενόμενο αποτέλεσμα

Όταν ανοίξετε το `WrapFunctionsDemo.xlsx` θα πρέπει να δείτε:

- **A1:C2** γεμάτο με το αποτέλεσμα του WRAPCOLS (1‑6 σε τρεις στήλες).
- **A2:B4** γεμάτο με το αποτέλεσμα του WRAPROWS (1‑6 σε δύο στήλες).
- Καμία τύπος να παραμένει — μόνο στατικές τιμές.

Αυτή είναι η πλήρης ροή από την αρχή μέχρι το τέλος.

## Περιπτώσεις Άκρων & Πρακτικές Συμβουλές

### Διαχείριση Μεγαλύτερων Πινάκων

Αν ο πηγαίος πίνακας υπερβαίνει τις διαστάσεις στόχου, το Excel θα συνεχίσει να εκχελίζει σε επιπλέον γραμμές/στήλες. Για παράδειγμα, `WRAPCOLS({1..20},4)` δημιουργεί ένα μπλοκ 5‑γραμμών επί 4‑στηλών. Δοκιμάστε με ρεαλιστικά μεγέθη δεδομένων για να αποφύγετε απρόσμενη υπερχείλιση.

### Κενά ή Null Πίνακες

Η μεταβίβαση ενός κεννού πίνακα (`{}`) επιστρέφει σφάλμα `#VALUE!`. Προστατέψτε το ελέγχοντας την πηγή δεδομένων σας πριν ορίσετε τον τύπο.

### Σκέψεις Απόδοσης

Η κλήση του `calculateFormula()` σε ένα τεράστιο βιβλίο εργασίας μπορεί να είναι δαπανηρή. Αν χρειάζεστε μόνο τα δύο κελιά wrap να υπολογιστούν, μπορείτε να περιορίσετε το πεδίο υπολογισμού:

```java
        workbook.calculateFormula(sheet.getName(), "A1:B4");
```

Αυτή η στοχευμένη προσέγγιση μειώνει τη χρήση μνήμης και επιταχύνει την επεξεργασία.

### Σημείωση Αδειοδότησης

Το Aspose.Cells είναι εμπορική βιβλιοθήκη. Η δωρεάν δοκιμή επιβάλλει υδατογράφημα στις πρώτες λίγες γραμμές. Για παραγωγή, αγοράστε άδεια και εφαρμόστε την νωρίς:

```java
        License license = new License();
        license.setLicense("Aspose.Total.Java.lic");
```

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```java
import com.aspose.cells.*;

public class WrapFunctionsDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();                       // in-memory workbook
        Worksheet sheet = workbook.getWorksheets().get(0);        // default sheet

        // 2️⃣ Apply WRAPCOLS – Excel WRAPCOLS example (3 columns)
        sheet.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3,4,5,6},3)");

        // 3️⃣ Apply WRAPROWS – how to use WRAPROWS (2 rows)
        sheet.getCells().get("A2").setFormula("=WRAPROWS({1,2,3,4,5,6},2)");

        // 4️⃣ Force calculation – calculate formulas aspose.cells
        workbook.calculateFormula();   // full workbook evaluation

        // 5️⃣ Persist the file – save workbook as XLSX
        String outputPath = "YOUR_DIRECTORY/WrapFunctionsDemo.xlsx";
        workbook.save(outputPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

Εκτελέστε το πρόγραμμα (`javac WrapFunctionsDemo.java && java WrapFunctionsDemo`). Μετά την εκτέλεση, ανοίξτε το αρχείο XLSX στο Excel ή σε οποιονδήποτε συμβατό προβολέα για να επαληθεύσετε τη διάταξη.

## Συχνές Ερωτήσεις

**Ε: Μπορώ να συνδυάσω τα WRAPCOLs και WRAPROWS στο ίδιο φύλλο;**  
**Α:** Απόλυτα. Λειτουργούν ανεξάρτητα, οπότε μπορείτε να τοποθετήσετε κάθε αποτέλεσμα όπου θέλετε.

**Ε: Τι γίνεται αν χρειάζομαι δυναμικό αριθμό στηλών βάσει του μεγέθους των δεδομένων;**  
**Α:** Υπολογίστε πρώτα τον αριθμό στηλών σε Java, έπειτα ενσωματώστε τον στη συμβολοσειρά τύπου:  
```java
int cols = 4;
sheet.getCells().get("A1")
     .setFormula("=WRAPCOLS({1,2,3,4,5,6,7,8}, " + cols + ")");
```

**Ε: Η `calculateFormula()` αξιολογεί επίσης άλλες συναρτήσεις του Excel;**  
**Α:** Ναι. Το Aspose.Cells υποστηρίζει πάνω από 500 συναρτήσεις, συμπεριλαμβανομένων των νεότερων συναρτήσεων δυναμικών πινάκων όπως `FILTER` και `SORT`.

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να χρησιμοποιήσετε το WRAPCOLS** (και το αδερφό του **WRAPROWS**) με το Aspose.Cells για Java, πώς να **υπολογίσετε τύπους aspose.cells**, και τα ακριβή βήματα για **αποθήκευση βιβλίου εργασίας ως XLSX**. Αυτό το πλήρες, εκτελέσιμο παράδειγμα θα ενσωματωθεί άμεσα στην αναφορά ή τη διαδικασία εξαγωγής δεδομένων σας.

Έτοιμοι για το επόμενο επίπεδο; Δοκιμάστε να τροφοδοτήσετε μια πραγματική συλλογή δεδομένων στο κυριολεκτικό array, πειραματιστείτε με μορφοποίηση υπό όρους, ή δημιουργήστε πολλαπλά φύλλα σε μια ενέργεια. Το ίδιο μοτίβο ισχύει

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να χρησιμοποιήσετε το Aspose Cells – Μαθήματα μηχανής Excel για Java](/cells/english/java/calculation-engine/)
- [Πώς να αποθηκεύσετε ένα βιβλίο εργασίας Excel σε Java χρησιμοποιώντας το Aspose.Cells](/cells/english/java/automation-batch-processing/excel-automation-java-aspose-cells-guide/)
- [Πώς να φορτώσετε και να αποθηκεύσετε Excel ως CSV χρησιμοποιώντας το Aspose.Cells για Java: Ένας ολοκληρωμένος οδηγός](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}