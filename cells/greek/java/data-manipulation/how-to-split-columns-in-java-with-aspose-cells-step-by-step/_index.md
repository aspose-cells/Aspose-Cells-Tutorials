---
category: general
date: 2026-10-07
description: Πώς να διαχωρίσετε στήλες χρησιμοποιώντας το Aspose.Cells για Java. Μάθετε
  πώς να διαχωρίζετε συμβολοσειρές σε στήλες, να αυτοματοποιείτε τύπους Excel και
  να γράφετε τύπο σε κελί με λίγες γραμμές κώδικα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to split columns
- split string into columns
- automate excel formula
- write formula to cell
language: el
lastmod: 2026-10-07
og_description: Πώς να χωρίσετε στήλες σε Java με το Aspose.Cells. Αυτό το σεμινάριο
  σας δείχνει πώς να χωρίσετε μια συμβολοσειρά σε στήλες, να αυτοματοποιήσετε την
  αξιολόγηση τύπων του Excel και να γράψετε τύπο σε ένα κελί.
og_image_alt: Screenshot of Java code that splits columns in an Excel worksheet using
  Aspose.Cells
og_title: Πώς να χωρίσετε στήλες σε Java με το Aspose.Cells – γρήγορο σεμινάριο
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: How to split columns using Aspose.Cells for Java. Learn to split string
    into columns, automate Excel formula, and write formula to cell in a few lines
    of code.
  headline: How to split columns in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Πώς να χωρίσετε στήλες στη Java με το Aspose.Cells – οδηγός βήμα‑βήμα
url: /el/java/data-manipulation/how-to-split-columns-in-java-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χωρίσετε στήλες σε Java με το Aspose.Cells – οδηγός βήμα‑βήμα

Αν χρειάζεστε **πώς να χωρίσετε στήλες** σε ένα φύλλο εργασίας Excel προγραμματιστικά, αυτός ο οδηγός σας δείχνει τη πλήρη διαδικασία με το Aspose.Cells για Java. Θα μάθετε επίσης πώς να **διαχωρίσετε συμβολοσειρά σε στήλες**, **αυτοματοποιήσετε την αξιολόγηση τύπων Excel** και **γράψετε τύπο σε κελί** χρησιμοποιώντας σύντομο, έτοιμο για παραγωγή κώδικα.

Η προγραμματιστική διαίρεση στηλών εξαλείφει την χειροκίνητη αντιγραφή‑επικόλληση, μειώνει τα σφάλματα και επιτρέπει μετασχηματισμούς δεδομένων μεγάλης κλίμακας. Στο τέλος αυτού του tutorial μπορείτε να δημιουργείτε, να τροποποιείτε και να αξιολογείτε τύπους άμεσα, καθιστώντας το Excel πραγματικό μέρος του backend Java σας.

## Προαπαιτούμενα

* Java 17 ή νεότερη εγκατεστημένη.
* Maven 3.8+ (ή Gradle) για διαχείριση εξαρτήσεων.
* Άδεια Aspose.Cells για Java (η δωρεάν έκδοση αξιολόγησης λειτουργεί για εκμάθηση).
* Βασική εξοικείωση με τη σύνταξη Java και τις έννοιες του Excel.

Αν κάποιο από αυτά τα στοιχεία λείπει, εγκαταστήστε το πρώτα· τα παραδείγματα κώδικα υποθέτουν ένα τυπικό έργο Maven.

## Βήμα 1: Προσθέστε το Aspose.Cells στο έργο σας

Προσθέστε την ακόλουθη εξάρτηση στο `pom.xml`. Αυτό θα κατεβάσει τη νεότερη σταθερή βιβλιοθήκη Aspose.Cells.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version available -->
</dependency>
```

**Γιατί είναι σημαντικό αυτό το βήμα:** Η βιβλιοθήκη παρέχει τις κλάσεις `Workbook`, `Worksheet` και `Cell` που απαιτούνται για τη διαχείριση αρχείων Excel χωρίς το Microsoft Office. Χωρίς την εξάρτηση ο κώδικας δεν θα μεταγλωττιστεί.

## Βήμα 2: Δημιουργήστε ένα βιβλίο εργασίας και επιλέξτε το πρώτο φύλλο εργασίας

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize a new workbook and access the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
```

Το αντικείμενο `Workbook` αντιπροσωπεύει ολόκληρο το αρχείο Excel. Η πρόσβαση στο πρώτο φύλλο εργασίας εξασφαλίζει ένα προβλέψιμο σημείο εκκίνησης για τον τύπο που θα γράψουμε.

## Βήμα 3: Γράψτε τον τύπο WRAPCOLS σε ένα κελί-στόχο

```java
        // Step 3: Identify the target cell (A1) where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");

        // Step 3: Write the WRAPCOLS formula to split a long string into three columns
        // WRAPCOLS(string, columns) distributes the string across the specified number of columns.
        targetCell.setFormula("=WRAPCOLS(\"This is a very long string that needs to be split\",3)");
```

**Γιατί χρησιμοποιούμε το `WRAPCOLS`:** Η ενσωματωμένη λειτουργία του Excel `WRAPCOLS` χωρίζει αυτόματα μια μοναδική τιμή κειμένου σε έναν καθορισμένο αριθμό στηλών, διαχειριζόμενη τα όρια των λέξεων έξυπνα. Αυτή είναι η πιο αξιόπιστη μέθοδος για **διαχωρισμό συμβολοσειράς σε στήλες** χωρίς προσαρμοσμένη λογική ανάλυσης.

## Βήμα 4: Αναγκάστε το βιβλίο εργασίας να αξιολογήσει τον τύπο

```java
        // Step 4: Calculate all formulas in the workbook so the result becomes visible
        workbook.calculateFormula();
```

Η κλήση του `calculateFormula()` **αυτοματοποιεί την αξιολόγηση τύπων Excel** στην πλευρά του διακομιστή. Χωρίς αυτήν την κλήση το κελί θα περιείχε ακόμα το κείμενο του τύπου, όχι τις υπολογισμένες τιμές.

## Βήμα 5: Ανακτήστε και εμφανίστε το αποτέλεσμα του WRAPCOLS

```java
        // Step 5: Retrieve the computed value from the target cell
        String result = targetCell.getStringValue(); // returns the first column of the split result
        System.out.println("First column output: " + result);

        // Optionally, read the other columns created by WRAPCOLS
        String second = worksheet.getCells().get("B1").getStringValue();
        String third  = worksheet.getCells().get("C1").getStringValue();

        System.out.println("Second column output: " + second);
        System.out.println("Third column output: " + third);

        // Save the workbook to verify the split visually (optional)
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

Όταν εκτελέσετε το πρόγραμμα, η κονσόλα εκτυπώνει:

```
First column output: This is a very long
Second column output: string that needs
Third column output: to be split
```

Το παραγόμενο αρχείο `SplitColumnsResult.xlsx` εμφανίζει τις τρεις στήλες γεμάτες με το διαχωρισμένο κείμενο.

## Κατανόηση της λειτουργίας WRAPCOLS

* **Σύνταξη:** `WRAPCOLS(text, columns, [delimiter])`
* **Παράμετροι:**
  * `text` – η συμβολοσειρά που θέλετε να διαχωρίσετε.
  * `columns` – ο αριθμός των στηλών για την κατανομή του κειμένου.
  * `delimiter` (προαιρετικό) – ο χαρακτήρας που χρησιμοποιείται για το διαχωρισμό της συμβολοσειράς· η προεπιλογή είναι το κενό.
* **Τιμή επιστροφής:** Ένας πίνακας που εκσπώνεται σε γειτονικά κελιά, κάθε στοιχείο περιέχει ένα τμήμα του αρχικού κειμένου.

Επειδή η λειτουργία εκσπώνεται οριζόντια, χρειάζεται μόνο να γράψετε τον τύπο στο αριστερότερο κελί (A1 στο παράδειγμα). Το Excel συμπληρώνει αυτόματα τα B1, C1, … όπως χρειάζεται.

## Συνηθισμένες παραλλαγές και ειδικές περιπτώσεις

| Κατάσταση | Συνιστώμενη προσαρμογή |
|-----------|------------------------|
| **Variable column count** | Replace the hard‑coded `3` with a variable: `targetCell.setFormula(String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount));` |
| **Custom delimiter** | Use the third argument, e.g., `=WRAPCOLS(A2,4,",")` to split on commas. |
| **Empty source string** | The function returns empty cells; guard against `null` or empty strings before setting the formula. |
| **Large datasets** | Apply the formula in a loop for each row, then call `calculateFormula()` once after the loop to improve performance. |
| **Non‑ASCII characters** | WRAPCOLS works with Unicode; ensure your Java source file is saved as UTF‑8. |

**Συμβουλή:** Όταν επεξεργάζεστε πολλές γραμμές, αποθηκεύστε τον τύπο σε μια μεταβλητή συμβολοσειράς και επαναχρησιμοποιήστε την για να αποφύγετε το επαναλαμβανόμενο κόστος συνένωσης συμβολοσειρών.

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα έτοιμο για αντιγραφή‑επικόλληση. Περιλαμβάνει δηλώσεις import, διαχείριση εξαιρέσεων και μια προαιρετική λειτουργία αποθήκευσης.

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Define the long string and desired column count
        String longString = "This is a very long string that needs to be split";
        int columnCount = 3;

        // Write the WRAPCOLS formula to cell A1
        Cell targetCell = worksheet.getCells().get("A1");
        String formula = String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount);
        targetCell.setFormula(formula);

        // Evaluate all formulas in the workbook
        workbook.calculateFormula();

        // Read and display each column's result
        System.out.println("First column output: " + worksheet.getCells().get("A1").getStringValue());
        System.out.println("Second column output: " + worksheet.getCells().get("B1").getStringValue());
        System.out.println("Third column output: " + worksheet.getCells().get("C1").getStringValue());

        // Save the workbook for visual verification
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

Η εκτέλεση αυτού του προγράμματος παράγει την ίδια έξοδο κονσόλας όπως προηγουμένως και γράφει ένα αρχείο Excel που δείχνει σαφώς **πώς να χωρίσετε στήλες**.

## Λίστα ελέγχου αντιμετώπισης προβλημάτων

* **Ο τύπος δεν αξιολογείται** – Βεβαιωθείτε ότι καλείται το `workbook.calculateFormula()` μετά τον ορισμό του τύπου.
* **Κελία κενά μετά το διαχωρισμό** – Επαληθεύστε ότι η πηγή συμβολοσειράς δεν είναι `null` ή κενή, και ότι ο αριθμός στηλών είναι μεγαλύτερος του μηδενός.
* **Απόρριψη άδειας** – Παρέχετε ένα έγκυρο αρχείο άδειας Aspose.Cells (`License license = new License(); license.setLicense("Aspose.Total.lic");`) πριν δημιουργήσετε το βιβλίο εργασίας για να αφαιρέσετε τα υδατογραφήματα αξιολόγησης.
* **Καθυστέρηση απόδοσης σε μεγάλα φύλλα** – Καλέστε το `calculateFormula()` μία φορά μετά την εγγραφή όλων των τύπων, όχι μετά από κάθε μεμονωμένο κελί.

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να χωρίσετε στήλες** σε Java χρησιμοποιώντας το Aspose.Cells, πώς να **διαχωρίσετε συμβολοσειρά σε στήλες** με τη λειτουργία `WRAPCOLS`, πώς να **αυτοματοποιήσετε την αξιολόγηση τύπων Excel**, και πώς να **γράψετε τύπο σε κελί** προγραμματιστικά. Αυτή η τεχνική αφαιρεί τα χειροκίνητα βήματα προετοιμασίας δεδομένων και ενσωματώνει τις ισχυρές δυνατότητες επεξεργασίας κειμένου του Excel απευθείας στις εφαρμογές Java σας.

### Επόμενα βήματα

* Εξερευνήστε άλλες λειτουργίες κειμένου όπως `TEXTSPLIT` και `FILTERXML` για πιο σύνθετα σενάρια ανάλυσης.
* Συνδυάστε το `WRAPCOLS` με το `IFERROR` για να διαχειρίζεστε απρόσμενες εισόδους με ευγένεια.
* Ενσωματώστε τη λύση σε μια υπηρεσία Spring Boot που λαμβάνει δεδομένα CSV μέσω REST και επιστρέφει ένα γεμάτο αρχείο Excel.

Με την εξοικείωση με αυτά τα πρότυπα μπορείτε να δημιουργήσετε ανθεκτικές, αυτοματοποιημένες ροές εργασίας Excel που κλιμακώνονται με τις επιχειρηματικές σας ανάγκες. Καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να εξοικειωθείτε με πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [aspose cells java – Διαχωρισμός Ονομάτων σε Στήλες](/cells/english/java/cell-operations/aspose-cells-java-split-names-columns/)
- [Αυτόματη Προσαρμογή Στηλών Excel σε Java Χρησιμοποιώντας Aspose.Cells](/cells/english/java/formatting/aspose-cells-java-auto-fit-excel-columns-guide/)
- [Πώς να Διαγράψετε Κενές Στήλες στο Excel Χρησιμοποιώντας Aspose.Cells Java&#58; Ένας Πλήρης Οδηγός](/cells/english/java/worksheet-management/delete-blank-columns-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}