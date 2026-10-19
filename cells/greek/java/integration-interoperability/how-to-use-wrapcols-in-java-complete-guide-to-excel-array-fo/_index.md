---
category: general
date: 2026-06-18
description: Μάθετε πώς να χρησιμοποιείτε το WRAPCOLS στη Java για να τυλίγετε μια
  λίστα σε στήλες, να εφαρμόζετε τύπο πίνακα σε στυλ Excel και να δημιουργείτε γρήγορα
  βιβλίο εργασίας Excel με Java.
draft: false
keywords:
- how to use wrapcols
- apply array formula excel
- list to matrix excel
- wrap list into columns
- create excel workbook java
language: el
og_description: Ανακαλύψτε πώς να χρησιμοποιήσετε το WRAPCOLS στη Java, να τυλίξετε
  λίστα σε στήλες, να εφαρμόσετε τύπο πίνακα στο Excel και να δημιουργήσετε βιβλίο
  εργασίας Excel με Java με ένα πλήρες, εκτελέσιμο παράδειγμα.
og_title: Πώς να χρησιμοποιήσετε το WRAPCOLS στη Java – Πλήρης οδηγός τύπων πίνακα
  Excel
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Learn how to use WRAPCOLS in Java to wrap a list into columns, apply
    array formula Excel style, and create Excel workbook Java quickly.
  headline: How to Use WRAPCOLS in Java – Complete Guide to Excel Array Formulas
  type: TechArticle
- questions:
  - answer: The library works in trial mode, which adds a watermark. For production
      you’ll need a commercial license, but the API usage stays the same.
    question: Do I need a license for Aspose.Cells?
  - answer: Absolutely. Replace `{1,2,3}` with a named range like `MyNumbers`. The
      formula becomes `=WRAPCOLS(MyNumbers,3)`.
    question: Can I use WRAPCOLS with named ranges instead of literal arrays?
  - answer: 'POI currently doesn’t evaluate array formulas out of the box, so you’d
      need a custom evaluator or switch to Aspose for full support. --- ## Conclusion
      We’ve covered **how to use WRAPCOLS** in Java, shown you how to **apply array
      formula Excel** techniques, and demonstrated a practical **list to matr'
    question: What if I’m using Apache POI instead of Aspose?
  type: FAQPage
tags:
- Excel
- Java
- Aspose.Cells
- Array Formula
title: Πώς να χρησιμοποιήσετε το WRAPCOLS στη Java – Πλήρης οδηγός για τους τύπους
  πίνακα του Excel
url: /el/java/integration-interoperability/how-to-use-wrapcols-in-java-complete-guide-to-excel-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε το WRAPCOLS σε Java – Πλήρης Οδηγός για Συναρτήσεις Πίνακα του Excel

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε το WRAPCOLS** όταν αυτοματοποιείτε λογιστικά φύλλα από τη Java; Δεν είστε μόνοι. Είτε μετατρέπετε μια επίπεδη λίστα τιμών σε έναν τακτοποιημένο πίνακα 3 στηλών, είτε χρειάζεστε απλώς έναν γρήγορο τρόπο για να αναδιαμορφώσετε δεδομένα, η συνάρτηση WRAPCOLs είναι σωτήρας.

Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό παράδειγμα που δείχνει **πώς να χρησιμοποιήσετε το WRAPCOLS**, πώς να **εφαρμόσετε τύπους πίνακα Excel** και ακόμη πώς να **δημιουργήσετε Excel workbook Java** από το μηδέν. Στο τέλος θα έχετε ένα πλήρως λειτουργικό αρχείο `.xlsx` που επιδεικνύει τη μετατροπή **list to matrix Excel**—όλα με σαφείς εξηγήσεις και κώδικα έτοιμο για εκτέλεση.

## Τι Θα Μάθετε

* Την ακριβή σύνταξη της συνάρτησης πίνακα `WRAPCOLS` και πότε είναι ιδανική.  
* Πώς να **εφαρμόσετε τύπους πίνακα Excel** χρησιμοποιώντας το Aspose.Cells for Java.  
* Τρόπους για **list to matrix Excel** – τόσο κατά στήλη όσο και κατά σειρά.  
* Συμβουλές για **wrap list into columns** αποδοτικά, και ένα πλήρες παράδειγμα **create Excel workbook Java**.  

Δεν έχετε εμπειρία με το Aspose.Cells; Κανένα πρόβλημα. Το μόνο που χρειάζεστε είναι ένα περιβάλλον ανάπτυξης Java και ένα αντίγραφο της βιβλιοθήκης Aspose.Cells for Java (η δωρεάν δοκιμή λειτουργεί εξαιρετικά).

---

## Πώς να Χρησιμοποιήσετε το WRAPCOLS – Βήμα‑Βήμα Υλοποίηση

> **Pro tip:** Το WRAPCOLS είναι μια *συνάρτηση πίνακα*, που σημαίνει ότι πρέπει να την εισάγετε ως τύπο που επιστρέφει πολλαπλά κελιά ταυτόχρονα. Στη Java, το Aspose.Cells διαχειρίζεται την αξιολόγηση του πίνακα για εσάς μόλις ενεργοποιήσετε μια επανυπολογισμό.

```java
// ---------------------------------------------------------------------
// 1️⃣  Import the Aspose.Cells library
// ---------------------------------------------------------------------
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {

        // -----------------------------------------------------------------
        // 2️⃣  Create a new workbook – this is the foundation of any Java‑Excel task
        // -----------------------------------------------------------------
        Workbook workbook = new Workbook();               // create excel workbook java

        // -----------------------------------------------------------------
        // 3️⃣  Grab the first worksheet (index 0) – the default sheet is ready
        // -----------------------------------------------------------------
        Worksheet sheet = workbook.getWorksheets().get(0);

        // -----------------------------------------------------------------
        // 4️⃣  Set a WRAPCOLS formula that turns a simple list into a 3‑column matrix
        // -----------------------------------------------------------------
        // The array {1,2,3,4,5,6} will be laid out column‑wise, three columns wide.
        sheet.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3,4,5,6},3)"); // how to use wrapcols

        // -----------------------------------------------------------------
        // 5️⃣  Set a WRAPROWS formula – just for comparison, creates a 2‑row matrix
        // -----------------------------------------------------------------
        sheet.getCells().get("B1").setFormula("=WRAPROWS({1,2,3,4,5,6},2)"); // apply array formula excel

        // -----------------------------------------------------------------
        // 6️⃣  Recalculate all formulas so the array results become actual cell values
        // -----------------------------------------------------------------
        workbook.calculateFormula();                     // forces evaluation of array formulas

        // -----------------------------------------------------------------
        // 7️⃣  Save the workbook to disk – you now have a real Excel file
        // -----------------------------------------------------------------
        workbook.save("wrap_demo.xlsx");                 // create excel workbook java
        System.out.println("Workbook saved successfully!");
    }
}
```

**Γιατί λειτουργεί αυτό:**  
* Το `Workbook` είναι το σημείο εισόδου για οποιαδήποτε επεξεργασία Excel στη Java.  
* Το `WRAPCOLS` δέχεται δύο ορίσματα – τον πηγαίο πίνακα και τον επιθυμητό αριθμό στηλών.  
* Καλώντας το `calculateFormula()`, το Aspose.Cells αξιολογεί τον τύπο πίνακα και γράφει το προκύπτοντα πλέγμα στο φύλλο, περιτυλίγοντας ουσιαστικά **μια λίστα σε στήλες**.  

> **Τι γίνεται αν χρειάζεστε δυναμικό αριθμό στηλών;** Απλώς αντικαταστήστε το σταθερό `3` με μια αναφορά κελιού ή μια μεταβλητή που υπολογίζετε κατά το χρόνο εκτέλεσης.

---

## Εφαρμογή Τύπων Πίνακα στο Excel με Java

Αν δεν έχετε ξανασυναντήσει τύπους πίνακα προγραμματιστικά, η έννοια μπορεί να φαίνεται μυστηριώδης. Στο UI του Excel πατάτε `Ctrl+Shift+Enter` για να «κλειδώσετε» τον τύπο· στη Java η βιβλιοθήκη κάνει το βάρος για εσάς.  

* **Ορίστε τον τύπο** – όπως φαίνεται παραπάνω, χρησιμοποιείτε `setFormula()` σε ένα κελί.  
* **Ενεργοποιήστε τον επανυπολογισμό** – `workbook.calculateFormula()` αναγκάζει τη μηχανή να αξιολογήσει κάθε τύπο, συμπεριλαμβανομένων των πινάκων.  

Αυτή η προσέγγιση είναι ο συνιστώμενος τρόπος για **εφαρμογή τύπων πίνακα Excel** όταν δημιουργείτε βιβλία εργασίας στην πλευρά του διακομιστή. Εξασφαλίζει ότι τα κελιά περιέχουν τις υπολογισμένες τιμές, όχι μόνο το κείμενο του τύπου.

---

## Μετατροπή Λίστας σε Πίνακα στο Excel

Οι συναρτήσεις `WRAPCOLS` και `WRAPROWS` είναι ιδανικές για τη μετατροπή μιας μονοδιάστατης λίστας σε δισδιάστατη διάταξη. Ακολουθεί μια σύντομη σύγκριση:

| Συνάρτηση   | Επιθυμητό Σχήμα | Παράδειγμα Κλήσης                               | Αποτέλεσμα (πρώτα κελιά) |
|------------|----------------|-----------------------------------------------|--------------------------|
| `WRAPCOLS` | 3 στήλες       | `=WRAPCOLS({1,2,3,4,5,6},3)`                  | A1=1, A2=2, A3=3, B1=4… |
| `WRAPROWS` | 2 σειρές       | `=WRAPROWS({1,2,3,4,5,6},2)`                  | A1=1, B1=2, C1=3, A2=4… |

Παρατηρήστε πώς η ίδια επίπεδη λίστα μπορεί να οπτικοποιηθεί με δύο εντελώς διαφορετικούς τρόπους. Όταν χρειάζεστε μια μετατροπή **list to matrix Excel**, επιλέξτε τη συνάρτηση που ταιριάζει με τον προσανατολισμό που θέλετε.

### Περιπτώσεις Ακρότητας που Πρέπει να Λάβετε Υπόψη

* **Μη ισομερή διαίρεση** – Αν το μήκος της λίστας δεν είναι τέλειο πολλαπλάσιο του αριθμού στηλών/γραμμών, η τελευταία στήλη/γραμμή θα περιέχει τα υπόλοιπα στοιχεία. Δεν εμφανίζεται σφάλμα.  
* **Κενός πηγαίος πίνακας** – Η χρήση `{}` θα παράγει σφάλμα #VALUE!· προστατεύστε το ελέγχοντας το μέγεθος της λίστας πριν ορίσετε τον τύπο.  
* **Μεγάλα σύνολα δεδομένων** – Για χιλιάδες στοιχεία, σκεφτείτε να χωρίσετε τη λειτουργία σε τμήματα ώστε να αποφύγετε αιχμές μνήμης κατά το `calculateFormula()`.

---

## Περιτύλιξη Λίστας σε Στήλες vs. Σειρές – Πότε να Επιλέξετε Ποιο;

* **Περιτύλιξη σε στήλες (`WRAPCOLS`)** όταν θέλετε κάθετη επέκταση σε σταθερό αριθμό στηλών – ιδανικό για αναφορές που καταχωρούν στοιχεία κάτω από κάθε στήλη.  
* **Περιτύλιξη σε σειρές (`WRAPROWS`)** όταν προτιμάτε οριζόντια διάταξη – χρήσιμο για dashboards όπου κάθε σειρά αντιπροσωπεύει μια κατηγορία.  

Και οι δύο συναρτήσεις ανήκουν στην οικογένεια των **array formula** του Excel, δηλαδή επιστρέφουν έναν πίνακα τιμών. Η επιλογή εξαρτάται από την οπτική διάταξη που αναμένουν οι ενδιαφερόμενοι.

---

## Δημιουργία Excel Workbook σε Java – Πλήρες Παράδειγμα

Παρακάτω βρίσκεται ένα αυτόνομο πρόγραμμα που επιδεικνύει όλα όσα συζητήσαμε. Αντιγράψτε, επικολλήστε και τρέξτε το· θα δημιουργηθεί το `wrap_demo.xlsx` στον φάκελο του έργου σας.

```java
import com.aspose.cells.*;

public class FullWrapExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣  Instantiate a new workbook – the starting point for create excel workbook java
        Workbook wb = new Workbook();

        // 2️⃣  Access the default worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // 3️⃣  Demonstrate WRAPCOLS – turning a simple list into a 3‑column matrix
        ws.getCells().get("A1").setFormula("=WRAPCOLS({10,20,30,40,50,60,70,80,90},3)"); // how to use wrapcols

        // 4️⃣  Demonstrate WRAPROWS – turning the same list into a 2‑row matrix
        ws.getCells().get("E1").setFormula("=WRAPROWS({10,20,30,40,50,60,70,80,90},2)"); // apply array formula excel

        // 5️⃣  Force calculation so the array results are materialized
        wb.calculateFormula();

        // 6️⃣  Save the file – you’ve now created an Excel workbook Java can open
        wb.save("full_wrap_demo.xlsx"); // create excel workbook java

        System.out.println("Excel file generated: full_wrap_demo.xlsx");
    }
}
```

**Αναμενόμενο αποτέλεσμα:**  

* Τα κελιά `A1:C3` θα περιέχουν τους αριθμούς 10‑90 διατεταγμένους κατά στήλη (3 στήλες).  
* Τα κελιά `E1:M2` θα κρατούν τους ίδιους αριθμούς διατεταγμένους κατά σειρά (2 σειρές).  

Ανοίξτε το αρχείο στο Excel και θα δείτε έναν καθαρό πίνακα χωρίς καμία χειροκίνητη αντιγραφή—απλώς τη δύναμη του **wrap list into columns** (και rows) που οδηγείται από τη Java.

---

## Συχνές Ερωτήσεις

**Ε: Χρειάζομαι άδεια για το Aspose.Cells;**  
Α: Η βιβλιοθήκη λειτουργεί σε δοκιμαστική λειτουργία, η οποία προσθέτει υδατογράφημα. Για παραγωγική χρήση θα χρειαστείτε εμπορική άδεια, αλλά η χρήση του API παραμένει η ίδια.

**Ε: Μπορώ να χρησιμοποιήσω το WRAPCOLS με ονομαστικές περιοχές αντί για κυριολεκτικούς πίνακες;**  
Α: Απόλυτα. Αντικαταστήστε το `{1,2,3}` με μια ονομαστική περιοχή όπως `MyNumbers`. Ο τύπος γίνεται `=WRAPCOLS(MyNumbers,3)`.

**Ε: Τι γίνεται αν χρησιμοποιώ Apache POI αντί για Aspose;**  
Α: Το POI δεν αξιολογεί τύπους πίνακα αυτόματα, οπότε θα χρειαστείτε έναν προσαρμοσμένο αξιολογητή ή να μεταβείτε σε Aspose για πλήρη υποστήριξη.

---

## Συμπέρασμα

Καλύψαμε **πώς να χρησιμοποιήσετε το WRAPCOLS** στη Java, σας δείξαμε πώς να **εφαρμόσετε τεχνικές array formula Excel**, και παρουσιάσαμε μια πρακτική μετατροπή **list to matrix Excel**. Το πλήρες εκτελέσιμο απόσπασμα επίσης απεικονίζει τη συνολική διαδικασία του **

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Aspose.Cells for Java&#58; How to Create and Format Excel Workbooks Efficiently](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [How to Create an Excel Data Validation List with Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [How to Apply Styles to Excel Cells Using Aspose.Cells for Java - Complete Guide](/cells/english/java/formatting/apply-styles-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}