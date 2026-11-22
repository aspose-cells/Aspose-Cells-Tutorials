---
category: general
date: 2026-11-22
description: Μάθετε πώς να χρησιμοποιείτε το wrapcols στη Java για να μετατρέψετε
  μια περιοχή σε στήλες χρησιμοποιώντας το Aspose.Cells. Αυτός ο οδηγός εξηγεί βήμα-βήμα
  τη λειτουργία wrap columns του Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- convert range to columns
- wrap columns excel function
language: el
lastmod: 2026-11-22
og_description: Πώς να χρησιμοποιήσετε το wrapcols στη Java για να μετατρέψετε μια
  περιοχή σε στήλες. Ακολουθήστε αυτό το σεμινάριο για να κατακτήσετε τη λειτουργία
  wrap columns του Excel με το Aspose.Cells.
og_image_alt: Screenshot showing how to use wrapcols formula in Excel
og_title: Πώς να χρησιμοποιήσετε το wrapcols στη Java – οδηγός βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to use wrapcols in Java to convert a range to columns using
    Aspose.Cells. This guide walks through the wrap columns excel function step by
    step.
  headline: How to use wrapcols in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to use wrapcols in Java to convert a range to columns using
    Aspose.Cells. This guide walks through the wrap columns excel function step by
    step.
  name: How to use wrapcols in Java with Aspose.Cells
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Access the first worksheet
    text: '```java // Step 2: Access the first worksheet Worksheet worksheet = workbook.getWorksheets().get(0);
      ```'
  - name: Set the WRAPCOLS formula
    text: '```java // Step 3: Set the WRAPCOLS formula in cell A1 worksheet.getCells().get("A1").setFormula("=WRAPCOLS(A1:A10,
      3)"); ```'
  - name: Save the workbook
    text: '```java // Step 4: Save the workbook with the formula applied workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected output
    text: 'When you open `output.xlsx`, cells `A1:C4` (or however many rows are needed)
      will contain the original list from `A1:A10` spread across three columns. The
      layout looks like this:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
title: Πώς να χρησιμοποιήσετε το wrapcols σε Java με το Aspose.Cells
url: /el/java/range-management/how-to-use-wrapcols-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χρησιμοποιήσετε το wrapcols σε Java με Aspose.Cells

Αν χρειάζεστε **πώς να χρησιμοποιήσετε το wrapcols** για να αναδιαμορφώσετε δεδομένα σε ένα βιβλίο εργασίας Excel, αυτό το tutorial δείχνει τη διαδικασία από την αρχή μέχρι το τέλος. Θα δείτε πώς ο τύπος WRAPCOLS μετατρέπει μια κάθετη περιοχή σε σύνολο στηλών, καθιστώντας εύκολο το πλάσιμο λιστών πλάι‑πλάι.

Ο οδηγός καλύπτει όλα όσα χρειάζεστε: φόρτωση βιβλίου εργασίας, εφαρμογή του τύπου WRAPCOLS και αποθήκευση του αποτελέσματος. Δεν απαιτούνται εξωτερικές αναφορές, ώστε να μπορείτε να αντιγράψετε τον κώδικα και να τον εκτελέσετε αμέσως. Καθ' όλη τη διάρκεια εξηγούμε επίσης τη *wrap columns excel function* και δείχνουμε πώς να **μετατρέψετε περιοχή σε στήλες** για κοινά σενάρια αναφοράς.

## Τι θα χρειαστείτε

- Java 17 ή νεότερη  
- Aspose.Cells for Java (τελευταία έκδοση)  
- Ένα IDE Java (IntelliJ IDEA, Eclipse ή VS Code)  
- Ένα αρχείο Excel εισόδου (`input.xlsx`) που περιέχει δεδομένα στη στήλη A  

## Πώς να χρησιμοποιήσετε το wrapcols σε Java με Aspose.Cells

Τα παρακάτω τέσσερα βήματα υλοποιούν τη ροή εργασίας **πώς να χρησιμοποιήσετε το wrapcols**. Κάθε βήμα περιλαμβάνει ένα απόσπασμα κώδικα, εξήγηση του γιατί είναι σημαντικό και μια συμβουλή για αποφυγή κοινών παγίδων.

### Βήμα 1: Φόρτωση του βιβλίου εργασίας

```java
import com.aspose.cells.*;

public class WrapColsExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load a workbook (or create a new one)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Γιατί είναι σημαντικό αυτό το βήμα*: `Workbook` είναι το σημείο εισόδου για όλες τις λειτουργίες Excel στο Aspose.Cells. Η φόρτωση του αρχείου σας δίνει πρόσβαση σε φύλλα, κελιά και τύπους.  

**Pro tip**: Χρησιμοποιήστε απόλυτη διαδρομή κατά την ανάπτυξη για να αποφύγετε το `FileNotFoundException`. Μεταβείτε σε σχετική διαδρομή μόλις το έργο πακεταριστεί.

### Βήμα 2: Πρόσβαση στο πρώτο φύλλο εργασίας

```java
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Το πρώτο φύλλο εργασίας (`index 0`) συνήθως περιέχει τα δεδομένα που θέλετε να μετασχηματίσετε. Αν τα δεδομένα σας βρίσκονται σε διαφορετικό φύλλο, αλλάξτε το δείκτη ή χρησιμοποιήστε `get("SheetName")`.  

**Γιατί είναι σημαντικό αυτό το βήμα**: Η εργασία με το σωστό φύλλο εξασφαλίζει ότι ο τύπος WRAPCOLS αναφέρεται στην επιθυμητή περιοχή.

### Βήμα 3: Ορισμός του τύπου WRAPCOLS

```java
        // Step 3: Set the WRAPCOLS formula in cell A1
        worksheet.getCells().get("A1").setFormula("=WRAPCOLS(A1:A10, 3)");
```

`WRAPCOLS(range, columns)` είναι η **wrap columns excel function** που διανέμει τις τιμές από το `range` στις καθορισμένες στήλες. Σε αυτό το παράδειγμα παίρνουμε τις τιμές από `A1:A10` και τις τοποθετούμε σε τρεις στήλες, ξεκινώντας από το `A1`.  

**Γιατί είναι σημαντικό αυτό το βήμα**: Ο τύπος κάνει το βαριά δουλειά—δεν απαιτείται χειροκίνητος βρόχος ή διαχείριση πινάκων.  

**Συμβουλή για convert range to columns**: Προσαρμόστε το δεύτερο όρισμα (`3`) ώστε να ταιριάζει με τον αριθμό των στηλών που χρειάζεστε. Αν το μήκος της περιοχής δεν είναι πολλαπλάσιο του αριθμού στηλών, η τελευταία στήλη θα περιέχει τα υπόλοιπα στοιχεία.

### Βήμα 4: Αποθήκευση του βιβλίου εργασίας

```java
        // Step 4: Save the workbook with the formula applied
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Η αποθήκευση γράφει τον τύπο WRAPCOLS στο `output.xlsx`. Όταν ανοίξετε το αρχείο στο Excel, ο τύπος θα υπολογιστεί και θα εμφανίσει τα δεδομένα τοποθετημένα σε στήλες.  

**Γιατί είναι σημαντικό αυτό το βήμα**: Η διατήρηση του βιβλίου εργασίας σας επιτρέπει να επαληθεύσετε το αποτέλεσμα και να μοιραστείτε το αρχείο με χρήστες που δεν χρησιμοποιούν Java.

![Wrapcols formula applied in Excel](wrapcols-example.png){: .align-center alt="Στιγμιότυπο οθόνης πώς να χρησιμοποιήσετε wrapcols σε Excel"}

### Αναμενόμενο αποτέλεσμα

Όταν ανοίξετε το `output.xlsx`, τα κελιά `A1:C4` (ή όσες γραμμές χρειάζονται) θα περιέχουν την αρχική λίστα από `A1:A10` διασπαρμένη σε τρεις στήλες. Η διάταξη φαίνεται ως εξής:

| A | B | C |
|---|---|---|
| Αντικείμενο 1 | Αντικείμενο 4 | Αντικείμενο 7 |
| Αντικείμενο 2 | Αντικείμενο 5 | Αντικείμενο 8 |
| Αντικείμενο 3 | Αντικείμενο 6 | Αντικείμενο 9 |
| Αντικείμενο 10 |   |   |

Η **wrap columns excel function** γεμίζει αυτόματα τα κενά κελιά με κενά, οπότε δεν χρειάζεται επιπλέον κώδικας καθαρισμού.

## Κατανόηση της wrap columns excel function

Ο τύπος WRAPCOLS είναι μέρος των δυναμικών συναρτήσεων πίνακα του Excel που εισήχθησαν στο Excel 365. Λειτουργεί παρόμοια με το `TEXTSPLIT` αλλά εστιάζει στη διανομή κατά στήλες.  

- **Σύνταξη**: `=WRAPCOLS(source_range, columns)`  
- **Παράμετροι**:  
  - `source_range` – η κάθετη περιοχή που θέλετε να αναδιαμορφώσετε.  
  - `columns` – ο αριθμός των στηλών στις οποίες θα τοποθετηθούν τα δεδομένα.  

Όταν καλείτε `=WRAPCOLS(A1:A10, 3)`, το Excel αντιμετωπίζει την πηγή ως μονοδιάστατο πίνακα και γεμίζει πρώτα την πρώτη στήλη, μετά τη δεύτερη κ.ο.κ., μέχρι να τοποθετηθούν όλες οι τιμές. Αυτό κάνει το **πώς να χρησιμοποιήσετε το wrapcols** ένα τέλειο εργαλείο για τη μετατροπή μιας λίστας μιας στήλης σε αναφορά πολλαπλών στηλών χωρίς VBA.

## Convert range to columns χωρίς τύπους (προαιρετικό)

Αν προτιμάτε να εκτελέσετε την **convert range to columns** εντελώς σε Java—χωρίς να βασίζεστε στη μηχανή υπολογισμού του Excel—μπορείτε να διαβάσετε τις πηγικές τιμές, να δημιουργήσετε έναν δισδιάστατο πίνακα και να τον γράψετε πίσω χειροκίνητα:

```java
        // Optional: programmatic conversion without WRAPCOLS
        Cells cells = worksheet.getCells();
        int rows = 10; // A1:A10
        int cols = 3;
        String[][] matrix = new String[rows][cols];

        // Fill matrix column‑wise
        for (int i = 0; i < rows; i++) {
            String value = cells.get(i, 0).getStringValue(); // column A
            int colIdx = i % cols;
            int rowIdx = i / cols;
            matrix[rowIdx][colIdx] = value;
        }

        // Write matrix back starting at A1
        for (int r = 0; r < rows / cols + 1; r++) {
            for (int c = 0; c < cols; c++) {
                if (matrix[r][c] != null) {
                    cells.get(r, c).putValue(matrix[r][c]);
                }
            }
        }
```

Αυτό το απόσπασμα δείχνει έναν εναλλακτικό τρόπο για **convert range to columns** όταν χρειάζεστε πλήρη έλεγχο του αποτελέσματος (π.χ., εφαρμογή προσαρμοσμένης μορφοποίησης ανά στήλη). Ωστόσο, η χρήση της **wrap columns excel function** μέσω WRAPCOLS είναι συνήθως πιο σύντομη και αφήνει το Excel να διαχειριστεί τον επαναϋπολογισμό αυτόματα.

## Περιπτώσεις άκρων και βέλτιστες πρακτικές

- **Κενά κελιά**: Το WRAPCOLS αντιμετωπίζει τα κενά κελιά ως κενά. Αν η πηγή σας περιέχει κενά, το αποτέλεσμα θα διατηρήσει αυτά τα κενά.  
- **Δυναμικές περιοχές**: Χρησιμοποιήστε μια ονομασμένη περιοχή ή αναφορά πίνακα (`Table1[Column]`) ώστε ο τύπος να προσαρμόζεται όταν προστεθούν γραμμές.  
- **Απόδοση**: Η εφαρμογή του τύπου είναι O(1) επειδή το Excel τον αξιολογεί αργά. Η μετατροπή από Java που φαίνεται παραπάνω είναι O(n) και μπορεί να είναι πιο αργή για πολύ μεγάλες περιοχές.  
- **Συμβατότητα εκδόσεων**: Η λειτουργία WRAPCOLS απαιτεί Excel 365 ή νεότερο. Αν πρέπει να υποστηρίξετε παλαιότερες εκδόσεις, χρησιμοποιήστε τη μέθοδο μετατροπής από τη Java.

## Πώς να χρησιμοποιήσετε το wrapcols σε άλλα σενάρια

- **Πίνακες αναφορών**: Μετατρέψτε μια κάθετη λίστα ονομάτων KPI σε έναν συμπαγή πίνακα με τρεις στήλες ανά γραμμή.  
- **Φόρμες εισαγωγής δεδομένων**: Μετατρέψτε μια στήλη εισόδων χρήστη σε διάταξη πλάι‑πλάι για ευκολότερη οπτική σύγκριση.  
- **Εξαγωγή σε CSV**: Αφού εφαρμόσετε το WRAPCOLS, αποθηκεύστε το βιβλίο εργασίας ως CSV για να λάβετε μια διαχωρισμένη προβολή που ταιριάζει στη διάταξη στηλών.

Κάθε μία από αυτές τις περιπτώσεις ακολουθεί το ίδιο μοτίβο **πώς να χρησιμοποιήσετε το wrapcols**: φόρτωση, αναφορά, ορισμός τύπου, αποθήκευση.

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να χρησιμοποιήσετε το wrapcols** σε Java με Aspose.Cells για να **convert range to columns** αποδοτικά. Εφαρμόζοντας τον τύπο `WRAPCOLS` εκμεταλλεύεστε τη φυσική *wrap columns excel function*, διατηρώντας τον κώδικά σας σύντομο ενώ δίνετε στο Excel τον πλήρη έλεγχο του υπολογισμού και της εμφάνισης.  

Πειραματιστείτε με διαφορετικούς αριθμούς στηλών, δυναμικές περιοχές ή τη προαιρετική μετατροπή μόνο σε Java για να ταιριάξετε στις ανάγκες του έργου σας. Όταν κυριαρχήσετε αυτήν την τεχνική, η αναδιαμόρφωση δεδομένων στο Excel γίνεται μια ενέργεια μίας γραμμής αντί για χειροκίνητη εργασία.

---


## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to use wrapcols to convert a list into multiple columns in Java](/cells/english/java/formulas-functions/how-to-use-wrapcols-to-convert-a-list-into-multiple-columns/)
- [How to Use WRAPCOLS in Java – Complete Guide to Excel Array Formulas](/cells/english/java/integration-interoperability/how-to-use-wrapcols-in-java-complete-guide-to-excel-array-fo/)
- [How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example](/cells/english/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}