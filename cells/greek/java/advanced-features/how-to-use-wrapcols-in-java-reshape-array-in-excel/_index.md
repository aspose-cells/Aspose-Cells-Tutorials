---
category: general
date: 2026-08-04
description: πώς να χρησιμοποιήσετε το wrapcols με ένα πλήρες παράδειγμα Java, να
  αναδιαμορφώσετε έναν πίνακα στο Excel και να αποθηκεύσετε το βιβλίο εργασίας σε
  αρχείο χρησιμοποιώντας το Aspose.Cells
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- save workbook to file
- reshape array in excel
- excel wrapcols example
- create excel workbook java
language: el
lastmod: 2026-08-04
og_description: πώς να χρησιμοποιήσετε το wrapcols για να αναδιαμορφώσετε έναν πίνακα
  στο Excel με Java. Μάθετε ένα πλήρες παράδειγμα wrapcols στο Excel, δημιουργήστε
  βιβλίο εργασίας Excel με Java και αποθηκεύστε το βιβλίο εργασίας σε αρχείο.
og_image_alt: Screenshot showing how to use WRAPCOLS in Java to reshape an array in
  Excel
og_title: πώς να χρησιμοποιήσετε το wrapcols στη Java – βήμα‑βήμα οδηγός
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: how to use wrapcols with a complete Java example, reshape array in
    Excel and save workbook to file using Aspose.Cells
  headline: how to use wrapcols in Java – reshape array in Excel
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: πώς να χρησιμοποιήσετε το wrapcols στη Java – επαναδιαμόρφωση πίνακα στο Excel
url: /el/java/advanced-features/how-to-use-wrapcols-in-java-reshape-array-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# πώς να χρησιμοποιήσετε το wrapcols σε Java – επανασχηματισμός πίνακα στο Excel

Αν χρειάζεστε **how to use wrapcols** για να μετατρέψετε μια επίπεδη λίστα τιμών σε μια περιοχή πολλαπλών γραμμών, αυτός ο οδηγός σας δείχνει τα ακριβή βήματα. Θα δείτε ένα **excel wrapcols example** που επανασχηματίζει έναν 1‑Δ πίνακα σε μπλοκ 3‑γραμμών × 2‑στηλών, και θα μάθετε πώς να **save workbook to file** με το Aspose.Cells.

Στο τέλος αυτού του tutorial θα μπορείτε να γράψετε κώδικα **create excel workbook java** που:

* Αρχικοποιεί ένα νέο workbook και επιλέγει το κελί A1.  
* Εφαρμόζει τη συνάρτηση `WRAPCOLS` για να επανασχηματίσει τα δεδομένα.  
* Αναγκάζει τον υπολογισμό του τύπου ώστε το αποτέλεσμα να εμφανίζεται άμεσα.  
* Ανακτά μια τιμή από τον υπολογισμένο πίνακα.  
* Αποθηκεύει το workbook στο δίσκο.

Η μόνη προϋπόθεση είναι ένα περιβάλλον ανάπτυξης Java (JDK 8 ή νεότερο) και η βιβλιοθήκη Aspose.Cells for Java.

---

## Προαπαιτούμενα

* JDK 8 + (ή οποιαδήποτε μεταγενέστερη έκδοση).  
* Maven ή Gradle για τη διαχείριση της εξάρτησης Aspose.Cells.  
* Βασική εξοικείωση με τη σύνταξη της Java και τους τύπους του Excel.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** Αν χρησιμοποιείτε Gradle, αντικαταστήστε το απόσπασμα XML με την αντίστοιχη γραμμή `implementation`.

---

## Βήμα 1: Δημιουργία Excel workbook σε Java

Η πρώτη ενέργεια είναι να γράψετε κώδικα **create excel workbook java** που ανοίγει ένα νέο workbook και παίρνει το πρώτο φύλλο εργασίας και το κελί A1.

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Access cell A1 where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");
```

Δημιουργώντας το workbook με αυτόν τον τρόπο έχετε ένα καθαρό ξεκίνημα, εξασφαλίζοντας ότι το παράδειγμα λειτουργεί σε οποιονδήποτε υπολογιστή χωρίς υπάρχον αρχείο.

---

## Βήμα 2: Εφαρμογή της συνάρτησης WRAPCOLS – ένα excel wrapcols example

`WRAPCOLS` παίρνει έναν μονοδιάστατο πίνακα και έναν αριθμό στηλών, και επιστρέφει μια περιοχή που γεμίζει πρώτα τις γραμμές. Αυτό είναι ο πυρήνας του **reshape array in excel**.

```java
        // Step 2: Set the WRAPCOLS formula
        // {1,2,3,4,5,6} is the source 1‑D array
        // 2 tells WRAPCOLS to create 2 columns per row
        targetCell.setFormula("=WRAPCOLS({1,2,3,4,5,6}, 2)");
```

Γιατί αυτό λειτουργεί:

* Ο κυριολεκτικός πίνακας `{1,2,3,4,5,6}` παρέχει έξι αριθμούς.  
* `WRAPCOLS(..., 2)` λέει στο Excel να τοποθετήσει τις τιμές σε 2 στήλες, δημιουργώντας αυτόματα αρκετές γραμμές (σε αυτήν την περίπτωση 3) για να φιλοξενήσει όλα τα στοιχεία.  
* Η προκύπτουσα περιοχή καταλαμβάνει τα κελιά **A1:B3**:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |
| 5 | 6 |

---

## Βήμα 3: Εξαναγκασμός υπολογισμού ώστε το workbook να αντανακλά τον τύπο

Το Aspose.Cells δεν αξιολογεί τους τύπους αυτόματα όταν τους ορίζετε. Πρέπει να καλέσετε `calculateFormula()` για να υλοποιήσετε το αποτέλεσμα.

```java
        // Step 3: Recalculate all formulas in the workbook
        workbook.calculateFormula();
```

Η κλήση αυτής της μεθόδου διασφαλίζει ότι ο πίνακας που παράγεται από το `WRAPCOLS` γράφεται στα κελιά, επιτρέποντάς σας να διαβάσετε τις τιμές αμέσως.

---

## Βήμα 4: Ανάκτηση τιμής από τον επανασχηματισμένο πίνακα

Για να αποδείξετε ότι ο τύπος λειτούργησε, διαβάστε την αναπαράσταση κειμένου του κελιού-στόχου. Επειδή το `WRAPCOLS` επιστρέφει έναν πίνακα, το Excel εμφανίζει το **πρώτο στοιχείο** (τιμή `1`) στο κελί όπου βρίσκεται ο τύπος.

```java
        // Step 4: Print the first element of the array (cell A1)
        System.out.println("First element: " + targetCell.getStringValue());
```

**Αναμενόμενη έξοδος κονσόλας**

```
First element: 1
```

Αν εξετάσετε το φύλλο εργασίας στο Excel, θα δείτε το πλήρες μπλοκ 3 × 2 όπως περιγράφηκε παραπάνω.

---

## Βήμα 5: Αποθήκευση του workbook σε αρχείο – how to save workbook to file

Η αποθήκευση του workbook σας επιτρέπει να το ανοίξετε αργότερα στο Excel ή να το μοιραστείτε με συναδέλφους. Χρησιμοποιήστε τη μέθοδο `save` με πλήρη διαδρομή.

```java
        // Step 5: Save the workbook to disk
        String outputPath = "WrapFunctions.xlsx"; // adjust directory as needed
        workbook.save(outputPath);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

Η εκτέλεση του προγράμματος παράγει το `WrapFunctions.xlsx` στον τρέχοντα φάκελο. Το άνοιγμα του αρχείου αποκαλύπτει τον επανασχηματισμένο πίνακα στα κελιά A1:B3, επιβεβαιώνοντας ότι η **save workbook to file** πέτυχε.

---

## Πλήρες, εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα IDE και να το εκτελέσετε:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cell targetCell = worksheet.getCells().get("A1");

        // Apply WRAPCOLS to reshape a 1‑D array into a 3‑row × 2‑col range
        targetCell.setFormula("=WRAPCOLS({1,2,3,4,5,6}, 2)");

        // Force formula evaluation
        workbook.calculateFormula();

        // Output the first element of the resulting array
        System.out.println("First element: " + targetCell.getStringValue());

        // Save the workbook to a file
        String outputPath = "WrapFunctions.xlsx";
        workbook.save(outputPath);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

**Επαλήθευση αποτελέσματος**

1. Η κονσόλα εκτυπώνει `First element: 1`.  
2. Το παραγόμενο `WrapFunctions.xlsx` περιέχει:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |
| 5 | 6 |

Αν χρειαστεί να αναφερθείτε στον πίνακα αλλού, μπορείτε να διαβάσετε οποιοδήποτε από τα γεμισμένα κελιά χρησιμοποιώντας `worksheet.getCells().get("B2").getIntValue()`, για παράδειγμα.

---

## Συχνές ερωτήσεις και ειδικές περιπτώσεις

| Question | Answer |
|----------|--------|
| *Μπορεί το WRAPCOLS να διαχειριστεί μη‑αριθμητικούς πίνακες;* | Ναι. Μπορείτε να περάσετε συμβολοσειρές, ημερομηνίες ή λογικές τιμές μέσα στις αγκύλες, και το Excel θα τις τοποθετήσει αναλόγως. |
| *Τι γίνεται αν χρειαστώ περισσότερες γραμμές από όσες μπορεί να εμφανίσει το Excel;* | Το WRAPCOLS θα συνεχίσει να επεκτείνεται σε επιπλέον γραμμές μέχρι να εξαντληθεί ο πηγαίος πίνακας. Βεβαιωθείτε ότι το φύλλο εργασίας έχει αρκετές γραμμές (προεπιλεγμένο όριο είναι 1.048.576). |
| *Πώς αλλάζω τον αριθμό των στηλών;* | Τροποποιήστε το δεύτερο όρισμα του `WRAPCOLS`. Για τρεις στήλες, χρησιμοποιήστε `=WRAPCOLS({1,2,3,4,5,6}, 3)`, το οποίο παράγει ένα μπλοκ 2 × 3. |
| *Μπορεί να γραφτεί το αποτέλεσμα σε διαφορετικό αρχικό κελί;* | Ναι. Ορίστε τον τύπο σε οποιοδήποτε κελί (π.χ., `C5`) και η περιορισμένη περιοχή θα επεκταθεί σχετικά με αυτό το κελί. |
| *Πρέπει να καλέσω το `calculateFormula` κάθε φορά που αλλάζω τον τύπο;* | Κάθε φορά που τροποποιείτε έναν τύπο προγραμματιστικά, καλέστε `calculateFormula` ή `calculateFormula(true)` για να ενημερώσετε τα εξαρτημένα κελιά. |

---

## Συμπέρασμα

Αυτό το tutorial έδειξε **how to use wrapcols** σε Java για **reshape array in excel**, παρείχε ένα σαφές **excel wrapcols example**, και έδειξε τον σωστό τρόπο για **save workbook to file**. Τώρα έχετε μια ισχυρή βάση για έργα **create excel workbook java** που χρειάζονται δυναμικούς μετασχηματισμούς πίνακα.

Στη συνέχεια, εξερευνήστε συναφή θέματα όπως **using other array functions** (`TRANSPOSE`, `SEQUENCE`) ή **writing large data sets** με το streaming API του Aspose.Cells. Πειραματιστείτε με διαφορετικούς πηγαίους πίνακες, αριθμούς στηλών και αρχικές θέσεις για να προσαρμόσετε το μοτίβο στις δικές σας ροές αναφοράς ή επεξεργασίας δεδομένων. Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε σε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Open an Excel File Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/getting-started/open-excel-aspose-cells-java-guide/)
- [How to Create and Merge Excel Workbooks Using Aspose.Cells for Java | Complete Guide](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)
- [How to Render Excel Sheets as Images Using Aspose.Cells for Java (Workbook Operations)](/cells/english/java/workbook-operations/render-excel-sheets-images-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}