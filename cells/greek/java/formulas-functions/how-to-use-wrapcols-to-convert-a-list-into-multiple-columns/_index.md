---
category: general
date: 2026-10-16
description: πώς να χρησιμοποιήσετε το wrapcols στη Java και να μετατρέψετε γρήγορα
  μια λίστα σε στήλες με έναν τύπο – μάθετε πώς να ορίσετε τύπο για μια πολυστήλη
  διάταξη
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- convert list to columns
- how to set formula
- create multi‑column layout
language: el
lastmod: 2026-10-16
og_description: πώς να χρησιμοποιήσετε το wrapcols για να μετατρέψετε μια λίστα σε
  στήλες σε Java. Ακολουθήστε αυτόν τον πλήρη οδηγό για να ορίσετε τύπο και να δημιουργήσετε
  διάταξη πολλαπλών στηλών στο Excel.
og_image_alt: Screenshot of an Excel sheet showing a wrapped list in three columns
og_title: Πώς να χρησιμοποιήσετε το wrapcols – βήμα‑βήμα οδηγός για προγραμματιστές
  Java
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: how to use wrapcols in Java and quickly convert list to columns with
    a formula – learn how to set formula for a multi‑column layout
  headline: How to use wrapcols to convert a list into multiple columns in Java
  type: TechArticle
- description: how to use wrapcols in Java and quickly convert list to columns with
    a formula – learn how to set formula for a multi‑column layout
  name: How to use wrapcols to convert a list into multiple columns in Java
  steps:
  - name: What happens behind the scenes
    text: 'When the workbook is saved, Aspose.Cells evaluates the formula and writes
      the expanded values to the file. If you open `WrapColsResult.xlsx` in Excel,
      you’ll see:'
  - name: Changing the number of columns
    text: If you need a different column count, modify the second argument of `WRAPCOLS`.
      For example, `=WRAPCOLS(A2:A100,5)` creates five columns. The function automatically
      adjusts the row count to accommodate the new layout.
  - name: Handling a non‑even list size
    text: When the source range length isn’t divisible by the column count, `WRAPCOLS`
      pads the final column with blanks. This behavior is useful for creating balanced
      tables without manual trimming.
  - name: Using a dynamic range
    text: You can replace `A2:A100` with a named range or a formula that calculates
      the last row, such as `A2:INDEX(A:A, COUNTA(A:A))`. This makes the solution
      robust when the list length changes.
  - name: Avoiding circular references
    text: Place the formula in a cell that isn’t part of the source range. If you
      accidentally set the formula inside `A2:A100`, Excel will report a circular
      reference error. Always write the formula to a separate cell (commonly `A1`).
  type: HowTo
tags:
- wrapcols
- Aspose.Cells
- Java
- Excel automation
title: Πώς να χρησιμοποιήσετε το wrapcols για να μετατρέψετε μια λίστα σε πολλές στήλες
  στη Java
url: /el/java/formulas-functions/how-to-use-wrapcols-to-convert-a-list-into-multiple-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χρησιμοποιήσετε το wrapcols για να μετατρέψετε μια λίστα σε πολλαπλές στήλες σε Java

Αν χρειάζεστε **how to use wrapcols** σε ένα έργο Java, αυτός ο οδηγός σας δείχνει τα ακριβή βήματα. Θα μάθετε πώς να ορίσετε τον τύπο, να μετατρέψετε μια λίστα σε στήλες και να δημιουργήσετε μια πολυ‑στήλη διάταξη χωρίς χειροκίνητη αντιγραφή‑επικόλληση.

Το tutorial καλύπτει τα πάντα, από τη ρύθμιση του έργου μέχρι τη διαχείριση edge‑case, ώστε να μπορείτε να εφαρμόσετε τη λύση σε οποιοδήποτε φύλλο εργασίας που περιέχει μια λίστα μονοστήλης. Δεν απαιτούνται πρόσθετα εργαλεία εκτός από το Aspose.Cells for Java.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Java 17 ή νεότερη εγκατεστημένη  
* Maven 3.8+ (ή Gradle) για διαχείριση εξαρτήσεων  
* Άδεια για **Aspose.Cells for Java** – η δωρεάν αξιολόγηση λειτουργεί για δοκιμές  
* Βασική εξοικείωση με τύπους Excel  

Αυτά τα στοιχεία εξασφαλίζουν ότι ο κώδικας θα εκτελεστεί χωρίς σφάλματα μεταγλώττισης.

## Βήμα 1: Προσθήκη Aspose.Cells στο έργο σας

Προσθέστε την ακόλουθη εξάρτηση Maven στο `pom.xml`. Αν χρησιμοποιείτε Gradle, ισχύουν οι ίδιες συντεταγμένες.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

Η βιβλιοθήκη παρέχει τις κλάσεις `Cell` και `Worksheet` που χρησιμοποιούνται αργότερα όταν **how to set formula** για μια περιοχή.

## Βήμα 2: Δημιουργία βιβλίου εργασίας και συμπλήρωση της πηγής λίστας

Το πρώτο καθήκον είναι η δημιουργία ενός βιβλίου εργασίας που περιέχει μια κάθετη λίστα (A2:A100). Αυτή η λίστα αντιπροσωπεύει τα δεδομένα που θέλετε να **convert list to columns**.

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Populate A2:A100 with sample data
        for (int i = 0; i < 99; i++) {
            cells.get("A" + (i + 2)).setValue("Item " + (i + 1));
        }

        // Apply WRAPCOLS formula (see next step)
        applyWrapCols(cells);

        // Save the result
        workbook.save("WrapColsResult.xlsx");
    }
```

Ο βρόχος γεμίζει την πρώτη στήλη με 99 στοιχεία, παρέχοντάς σας μια ρεαλιστική λίστα για εργασία. Μπορείτε να αντικαταστήσετε τις παραγόμενες τιμές με δεδομένα που διαβάζονται από βάση δεδομένων ή άλλη πηγή.

## Βήμα 3: Πώς να χρησιμοποιήσετε το wrapcols για να ορίσετε τον τύπο

Τώρα θα δείτε τον πυρήνα του tutorial: τη χρήση της συνάρτησης `WRAPCOLS` για **create multi‑column layout**. Η συνάρτηση δέχεται δύο ορίσματα – την πηγαία περιοχή και τον αριθμό των στηλών που θέλετε.

```java
    private static void applyWrapCols(Cells cells) {
        // Step 1: Get the cell where the formula will be placed (A1)
        Cell target = cells.get("A1");

        // Step 2: Apply the WRAPCOLS function to wrap A2:A100 into 3 columns
        target.setFormula("=WRAPCOLS(A2:A100,3)");
    }
}
```

*Γιατί λειτουργεί* – Η `WRAPCOLS` διαβάζει την κάθετη περιοχή `A2:A100` και κατανέμει τις τιμές γραμμή‑με‑γραμμή σε τρεις στήλες (B, C και D). Το αποτέλεσμα εμφανίζεται ξεκινώντας από το κελί που περιέχει τον τύπο (`A1`). Επειδή ο τύπος επιστρέφει έναν πίνακα, το Aspose.Cells επεκτείνει αυτόματα το αποτέλεσμα στα απαιτούμενα κελιά.

### Τι συμβαίνει στο παρασκήνιο

Όταν το βιβλίο εργασίας αποθηκευτεί, το Aspose.Cells αξιολογεί τον τύπο και γράφει τις επεκταμένες τιμές στο αρχείο. Αν ανοίξετε το `WrapColsResult.xlsx` στο Excel, θα δείτε:

| A1 | B1 | C1 | D1 |
|----|----|----|----|
| Στοιχείο 1 | Στοιχείο 34 | Στοιχείο 67 |
| Στοιχείο 2 | Στοιχείο 35 | Στοιχείο 68 |
| … | … | … |

Η διάταξη αυτή δείχνει ένα πρότυπο **create multi‑column layout** χρήσιμο για αναφορές, dashboards ή εκτυπώσιμες φόρμες.

## Βήμα 4: Επαλήθευση του αποτελέσματος προγραμματιστικά (προαιρετικό)

Αν θέλετε να επιβεβαιώσετε ότι ο τύπος παρήγαγε τον αναμενόμενο πίνακα χωρίς να ανοίξετε το Excel, μπορείτε να διαβάσετε ξανά τις τιμές μετά τον υπολογισμό.

```java
        // Force calculation to ensure the array result is materialized
        workbook.calculateFormula();

        // Print the first three rows of the wrapped layout
        for (int row = 0; row < 3; row++) {
            StringBuilder line = new StringBuilder();
            for (int col = 0; col < 4; col++) { // A‑D columns
                line.append(cells.get(row, col).getStringValue()).append("\t");
            }
            System.out.println(line.toString().trim());
        }
```

Η εκτέλεση του προγράμματος εκτυπώνει κάτι όπως:

```
Item 1    Item 34    Item 67    Item 100
Item 2    Item 35    Item 68    Item 101
Item 3    Item 36    Item 69    Item 102
```

Αυτό επιβεβαιώνει ότι **how to use wrapcols** λειτουργεί όπως προβλέπεται και ότι η λειτουργία **convert list to columns** ολοκληρώθηκε με επιτυχία.

## Βήμα 5: Συνηθισμένες παραλλαγές και edge cases

### Αλλαγή του αριθμού των στηλών

Αν χρειάζεστε διαφορετικό αριθμό στηλών, τροποποιήστε το δεύτερο όρισμα της `WRAPCOLS`. Για παράδειγμα, `=WRAPCOLS(A2:A100,5)` δημιουργεί πέντε στήλες. Η συνάρτηση προσαρμόζει αυτόματα τον αριθμό των γραμμών για να φιλοξενήσει τη νέα διάταξη.

### Διαχείριση λίστας με μη ισομερή μέγεθος

Όταν το μήκος της πηγής δεν είναι διαιρετό με τον αριθμό των στηλών, η `WRAPCOLS` συμπληρώνει την τελική στήλη με κενά. Αυτή η συμπεριφορά είναι χρήσιμη για τη δημιουργία ισορροπημένων πινάκων χωρίς χειροκίνητη περικοπή.

### Χρήση δυναμικής περιοχής

Μπορείτε να αντικαταστήσετε το `A2:A100` με μια ονομαστική περιοχή ή έναν τύπο που υπολογίζει την τελευταία γραμμή, όπως `A2:INDEX(A:A, COUNTA(A:A))`. Αυτό κάνει τη λύση πιο ανθεκτική όταν το μήκος της λίστας αλλάζει.

### Αποφυγή κυκλικών παραπομπών

Τοποθετήστε τον τύπο σε κελί που δεν ανήκει στην πηγαία περιοχή. Αν κατά λάθος θέσετε τον τύπο μέσα στο `A2:A100`, το Excel θα αναφέρει σφάλμα κυκλικής παραπομπής. Γράψτε πάντα τον τύπο σε ξεχωριστό κελί (συνήθως `A1`).

## Βήμα 6: Συμβουλές για παραγωγική χρήση

* **Cache το βιβλίο εργασίας** – Αν δημιουργείτε πολλές αναφορές σε βρόχο, επαναχρησιμοποιήστε ένα ενιαίο αντικείμενο `Workbook` και καθαρίστε τα προηγούμενα δεδομένα για μείωση του φορτίου μνήμης.  
* **Ορίστε τη λειτουργία υπολογισμού** – Χρησιμοποιήστε `workbook.getSettings().setCalculateFormulaOnOpen(false)` όταν χρειάζεστε μόνο τον ακατέργαστο τύπο χωρίς άμεση αξιολόγηση.  
* **Διεθνοποίηση** – Το όνομα της συνάρτησης `WRAPCOLS` είναι ανεξάρτητο από τη γλώσσα, αλλά οι δεκαδικοί διαχωριστές σε άλλους τύπους μπορεί να διαφέρουν. Κρατήστε τους τύπους στα Αγγλικά για να αποφύγετε ασυμφωνίες.  
* **Απόδοση** – Για λίστες που υπερβαίνουν τις 10 000 γραμμές, αξιολογήστε τον τύπο μία φορά και στη συνέχεια διαβάστε τις τιμές του πίνακα απευθείας, ώστε να αποφύγετε επαναλαμβανόμενους υπολογισμούς.

## Συμπέρασμα

Τώρα γνωρίζετε **how to use wrapcols** σε Java για **convert list to columns** και **create multi‑column layout** με έναν μόνο τύπο. Το πλήρες, εκτελέσιμο παράδειγμα δείχνει τη συνολική ροή εργασίας: προσθήκη της βιβλιοθήκης, συμπλήρωση δεδομένων, εφαρμογή του τύπου και επαλήθευση του αποτελέσματος.  

Από εδώ μπορείτε:

* Να προσαρμόσετε τον αριθμό των στηλών ώστε να ταιριάζει στο στυλ αναφοράς σας  
* Να συνδυάσετε το `WRAPCOLS` με άλλες συναρτήσεις όπως `SORT` ή `FILTER` για πιο προχωρημένο σχήμα δεδομένων  
* Να εξάγετε το βιβλίο εργασίας σε PDF, CSV ή HTML χρησιμοποιώντας τους ενσωματωμένους μετατροπείς του Aspose.Cells  

Δοκιμάστε αυτές τις παραλλαγές για να βελτιώσετε τις εργασίες αυτοματοποίησης του Excel. Αν αντιμετωπίσετε προβλήματα, ανατρέξτε στην ενότητα διαχείρισης edge‑case ή συμβουλευτείτε την τεκμηρίωση του Aspose.Cells για πρόσθετη υποστήριξη τύπων. Καλή προγραμματιστική δουλειά!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Use WRAPCOLS in Java – Complete Guide to Excel Array Formulas](/cells/english/java/integration-interoperability/how-to-use-wrapcols-in-java-complete-guide-to-excel-array-fo/)
- [How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example](/cells/english/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/)
- [How to Use Reduce in Excel with Java – Lambda Formula Guide](/cells/english/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}