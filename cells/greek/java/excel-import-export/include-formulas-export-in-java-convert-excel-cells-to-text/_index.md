---
category: general
date: 2026-07-03
description: Συμπεριλάβετε την εξαγωγή τύπων σε Java για τη μετατροπή κελιών Excel
  σε κείμενο χρησιμοποιώντας το Aspose.Cells. Μάθετε πώς να εκτυπώνετε ένα εύρος Excel
  και να λαμβάνετε αποτελεσματικά τις τιμές των κελιών ως συμβολοσειρά.
draft: false
keywords:
- include formulas export
- convert excel cells text
- print excel range
- export table options
- get cell values string
language: el
og_description: Συμπεριλάβετε την εξαγωγή τύπων σε Java για να μετατρέψετε τα κελιά
  του Excel σε κείμενο. Οδηγός βήμα‑προς‑βήμα που δείχνει πώς να εκτυπώσετε μια περιοχή
  Excel και να ανακτήσετε τις τιμές των κελιών ως συμβολοσειρά.
og_title: Συμπερίληψη εξαγωγής τύπων σε Java – Μετατροπή κελιών Excel σε κείμενο
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  headline: Include Formulas Export in Java – Convert Excel Cells to Text
  type: TechArticle
- description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  name: Include Formulas Export in Java – Convert Excel Cells to Text
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles with older versions but we’ll stick
      to the latest LTS). - Aspose.Cells for Java 23.10 (or any recent release)—you
      can grab it from Maven Central. - A sample `input.xlsx` placed in a folder you
      control (the path is hard‑coded in the example for clarity).'
  - name: Optional Tweaks
    text: '- `eto.setExportHiddenRows(true);` – include rows hidden in Excel. - `eto.setExportHiddenColumns(true);`
      – same for columns. - `eto.setExportAsHTML(true);` – get HTML instead of plain
      text.'
  - name: Expected Output (sample)
    text: '``` =SUM(A2:A3) 42 Hello =IF(B1>10,"Yes","No") =AVERAGE(C1:C3) =VLOOKUP(A1,Sheet2!A:B,2,FALSE)
      ```'
  - name: What if the range contains merged cells?
    text: Merged cells are treated as the value of the top‑left cell. The rest of
      the merged area will appear as empty strings. If you need the merged region’s
      address, query `Cell.getMergedRange()` before export.
  - name: Can I export a massive sheet (hundreds of thousands of rows)?
    text: Yes, but beware of memory consumption. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to let Aspose.Cells stream data to disk. Also, consider exporting in chunks
      (e.g., 10 000 rows at a time) to keep the string manageable.
  - name: How do I change the column delimiter?
    text: '`ExportTableOptions` exposes `setSeparator(char separator)`. For CSV‑style
      output, set it to `'',''`:'
  - name: Do formulas respect external references?
    text: If a formula points to another workbook, Aspose.Cells will keep the reference
      text (`='[Other.xlsx]Sheet1'!A1`). It won’t evaluate the external value unless
      you load that workbook as well.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Export
title: Συμπερίληψη Εξαγωγής Τύπων σε Java – Μετατροπή Κελιών Excel σε Κείμενο
url: /el/java/excel-import-export/include-formulas-export-in-java-convert-excel-cells-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Συμπερίληψη Εξαγωγής Τύπων σε Java – Μετατροπή Κελιών Excel σε Κείμενο

Έχετε χρειαστεί ποτέ να **συμπεριλάβετε εξαγωγή τύπων** όταν εξάγετε δεδομένα από ένα βιβλίο εργασίας Excel; Ίσως δημιουργείτε μια υπηρεσία αναφορών που πρέπει να διατηρεί τους αρχικούς τύπους ενώ παράλληλα παρέχει ένα καθαρό κείμενο. Σε αυτήν την περίπτωση, βρίσκεστε στο σωστό μέρος. Αυτός ο οδηγός σας καθοδηγεί στη μετατροπή κελιών Excel σε απλό κείμενο—*συμπεριλαμβανομένων* τυχόν ενσωματωμένων τύπων—χρησιμοποιώντας το Aspose.Cells for Java.

Θα δούμε επίσης πώς να **εκτυπώσετε το εύρος Excel**, να προσαρμόσετε τις **επιλογές εξαγωγής πίνακα**, και τελικά να **λάβετε τη συμβολοσειρά τιμών κελιών** που μπορείτε να καταγράψετε, να στείλετε μέσω API ή να αποθηκεύσετε σε μια βάση δεδομένων. Στο τέλος θα έχετε ένα πλήρως εκτελέσιμο απόσπασμα κώδικα και μια σαφή κατανόηση του «γιατί» πίσω από κάθε κλήση.

## Τι Θα Κερδίσετε

- Ένα πλήρες, έτοιμο για αντιγραφή‑επικόλληση πρόγραμμα Java που διαβάζει ένα αρχείο `.xlsx`, επιλέγει ένα εύρος και το εξάγει ως μορφοποιημένη συμβολοσειρά.
- Κατανόηση της κλάσης `ExportTableOptions` και του γιατί η εναλλαγή των `setExportAsString` και `setIncludeFormula` είναι σημαντική.
- Συμβουλές για τη διαχείριση μεγάλων φύλλων εργασίας, την αντιμετώπιση διαφορετικών τύπων δεδομένων και την προσαρμογή της μορφής εξόδου.
- Μια γρήγορη λίστα ελέγχου για κοινές παγίδες (π.χ. συγχωνευμένα κελιά, κρυφές γραμμές και μορφές αριθμών ειδικές για την περιοχή).

### Προαπαιτούμενα

- Java 17 ή νεότερη (ο κώδικας μεταγλωττίζεται με παλαιότερες εκδόσεις, αλλά θα χρησιμοποιήσουμε την πιο πρόσφατη LTS).
- Aspose.Cells for Java 23.10 (ή οποιαδήποτε πρόσφατη έκδοση) — μπορείτε να το αποκτήσετε από το Maven Central.
- Ένα δείγμα `input.xlsx` τοποθετημένο σε φάκελο που ελέγχετε (η διαδρομή είναι σκληρά κωδικοποιημένη στο παράδειγμα για σαφήνεια).

Αν έχετε ήδη αυτά, ας ξεκινήσουμε.

## Βήμα 1: Ρύθμιση του Έργου και Προσθήκη Εξαρτήσεων

Αρχικά, δημιουργήστε ένα έργο Maven (ή Gradle, αν προτιμάτε). Προσθέστε την εξάρτηση Aspose.Cells στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Συμβουλή:** Εάν χρησιμοποιείτε εταιρικό proxy, βεβαιωθείτε ότι το αποθετήριο είναι προσβάσιμο· διαφορετικά η διαδικασία κατασκευής θα αποτύχει με σφάλμα «Could not resolve dependencies».

Μόλις το Maven ολοκληρώσει τη λήψη, είστε έτοιμοι να γράψετε Java.

## Βήμα 2: Φόρτωση του Workbook και Λήψη του Επιθυμητού Φύλλου

Η πρώτη γραμμή του παραδείγματος κώδικα δείχνει πώς να ανοίξετε ένα υπάρχον workbook:

```java
// Step 1: Load the workbook
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Αντικαταστήστε το `YOUR_DIRECTORY` με την απόλυτη ή σχετική διαδρομή προς το αρχείο σας. Ο κατασκευαστής `Workbook` ανιχνεύει αυτόματα τη μορφή του αρχείου (XLS, XLSX, CSV κ.λπ.), οπότε δεν χρειάζεται να την καθορίσετε.

Στη συνέχεια, λαμβάνουμε το πρώτο φύλλο:

```java
// Step 2: Get the first worksheet
Worksheet ws = wb.getWorksheets().get(0);
```

Γιατί το πρώτο φύλλο; Σε πολλά πρότυπα τα δεδομένα βρίσκονται στην πρώτη καρτέλα, αλλά μπορείτε να περάσετε οποιονδήποτε δείκτη ή ακόμη και να χρησιμοποιήσετε `get("SheetName")` εάν προτιμάτε προσέγγιση με όνομα.

## Βήμα 3: Ορισμός του Εύρους που Θέλετε να Εξάγετε

Τώρα έρχεται η καρδιά της λειτουργίας **convert excel cells text**. Ενημερώνετε το Aspose.Cells ποια κελιά να εξάγει δημιουργώντας ένα αντικείμενο `Range`:

```java
// Step 3: Create a range covering cells A1 to C3
Range rng = ws.getCells().createRange("A1:C3");
```

Η συμβολοσειρά `"A1:C3"` είναι μια κλασική διεύθυνση στυλ A1. Μπορεί επίσης να δημιουργηθεί προγραμματιστικά:

```java
int firstRow = 0, firstCol = 0, totalRows = 3, totalCols = 3;
Range rng = ws.getCells().createRange(firstRow, firstCol, totalRows, totalCols);
```

Αυτή η ευελιξία βοηθά όταν το μέγεθος του εύρους είναι δυναμικό—π.χ., διαβάζετε την τελευταία χρησιμοποιημένη γραμμή με `ws.getCells().getMaxDataRow()`.

## Βήμα 4: Διαμόρφωση Επιλογών Εξαγωγής Πίνακα για Συμπερίληψη Τύπων

Εδώ βρίσκεται η μαγεία του **include formulas export**. Από προεπιλογή, το Aspose.Cells επιστρέφει τις *εμφανιζόμενες* τιμές. Εάν ένα κελί περιέχει `=SUM(A1:A3)`, θα λάβετε τον υπολογισμένο αριθμό, όχι το κείμενο του τύπου. Για να το αλλάξετε, ρυθμίστε το `ExportTableOptions`:

```java
// Step 4: Set up export options to return the range as a string and include formulas
ExportTableOptions eto = new ExportTableOptions();
eto.setExportAsString(true);      // Forces the result to be a single string
eto.setIncludeFormula(true);      // Includes the underlying formula instead of the evaluated value
```

Γιατί και οι δύο σημαίες; Το `setExportAsString(true)` λέει στο API να συνενώσει τα κελιά χρησιμοποιώντας το προεπιλεγμένο διαχωριστικό (tab για στήλες, newline για γραμμές). Το `setIncludeFormula(true)` αλλάζει την πηγή τιμής από «εμφανιζόμενη τιμή» σε «ακατέργαστο τύπο». Εάν θέλετε μόνο τιμές, αφήστε το `false`.

### Προαιρετικές Ρυθμίσεις

- `eto.setExportHiddenRows(true);` – συμπερίληψη κρυφών γραμμών στο Excel.  
- `eto.setExportHiddenColumns(true);` – ίδιο για στήλες.  
- `eto.setExportAsHTML(true);` – λήψη HTML αντί για απλό κείμενο.

Νιώστε ελεύθεροι να πειραματιστείτε· η κλάση επιλογών είναι ένα **playground export table options**.

## Βήμα 5: Ανάκτηση του Εύρους ως Μορφοποιημένη Συμβολοσειρά

Τώρα εξάγουμε τα δεδομένα:

```java
// Step 5: Retrieve the range values as a formatted string using the options
String txt = rng.getValueAsString(eto);
```

Το επιστρεφόμενο `txt` μοιάζει κάπως έτσι (υποθέτοντας ότι το A1:C3 περιέχει μίγμα τιμών και τύπων):

```
=SUM(A2:A3)	42	"Hello"
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Παρατηρήστε το tab (`\t`) που διαχωρίζει τις στήλες και το newline (`\n`) που διαχωρίζει τις γραμμές. Μπορείτε να διαχωρίσετε τη συμβολοσειρά αργότερα αν χρειάζεστε έναν δισδιάστατο πίνακα:

```java
String[] rows = txt.split("\n");
for (String row : rows) {
    String[] cells = row.split("\t");
    // Process each cell...
}
```

## Βήμα 6: Εκτύπωση του Αποτελέσματος – «Print Excel Range» Απλοποιημένο

Τέλος, εκτυπώνουμε τη συμβολοσειρά στην κονσόλα:

```java
// Step 6: Print the resulting string
System.out.println(txt);
```

Η εκτέλεση του προγράμματος εκτυπώνει την ακριβή έξοδο που φαίνεται παραπάνω. Από εδώ μπορείτε να γράψετε τη συμβολοσειρά σε αρχείο καταγραφής, να τη στείλετε μέσω HTTP ή να την αποθηκεύσετε σε έγγραφο NoSQL.

## Πλήρες, Έτοιμο‑για‑Εκτέλεση Παράδειγμα

Συνδυάζοντας όλα, εδώ είναι το πλήρες πρόγραμμα. Αντιγράψτε, επικολλήστε και πατήστε **Run**—χωρίς ελλιπείς εισαγωγές.

```java
import com.aspose.cells.*;

public class ExportFormulaRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook
        Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // Define the range A1:C3 (adjust as needed)
        Range rng = ws.getCells().createRange("A1:C3");

        // Configure export options: string output + include formulas
        ExportTableOptions eto = new ExportTableOptions();
        eto.setExportAsString(true);
        eto.setIncludeFormula(true);

        // Get the string representation of the range
        String txt = rng.getValueAsString(eto);

        // Print the resulting text
        System.out.println(txt);
    }
}
```

### Αναμενόμενη Έξοδος (δείγμα)

```
=SUM(A2:A3)	42	Hello
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Εάν το workbook σας περιέχει αριθμούς μορφοποιημένους ως ημερομηνίες, θα εμφανιστούν στη μορφή ειδική για την περιοχή (π.χ., `2026‑07‑03`). Για να επιβάλετε ISO ημερομηνίες, μπορείτε να ρυθμίσετε το `ExportTableOptions` με ένα προσαρμοσμένο `NumberFormat`.

## Διαχείριση Ακραίων Περιπτώσεων και Συχνών Ερωτήσεων

### Τι γίνεται αν το εύρος περιέχει συγχωνευμένα κελιά;

Τα συγχωνευμένα κελιά αντιμετωπίζονται ως η τιμή του πάνω‑αριστερού κελιού. Το υπόλοιπο της συγχωνευμένης περιοχής θα εμφανιστεί ως κενές συμβολοσειρές. Εάν χρειάζεστε τη διεύθυνση της συγχωνευμένης περιοχής, κάντε ερώτημα στο `Cell.getMergedRange()` πριν την εξαγωγή.

### Μπορώ να εξάγω ένα τεράστιο φύλλο (εκατοντάδες χιλιάδες γραμμές);

Ναι, αλλά προσέξτε τη χρήση μνήμης. Χρησιμοποιήστε το `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` για να επιτρέψετε στο Aspose.Cells να ρέει τα δεδομένα στο δίσκο. Επίσης, σκεφτείτε την εξαγωγή σε τμήματα (π.χ., 10 000 γραμμές τη φορά) ώστε η συμβολοσειρά να παραμένει διαχειρίσιμη.

### Πώς αλλάζω το διαχωριστικό στηλών;

Το `ExportTableOptions` εκθέτει τη μέθοδο `setSeparator(char separator)`. Για έξοδο τύπου CSV, ορίστε το σε `','`:

```java
eto.setSeparator(',');
```

### Οι τύποι σέβονται εξωτερικές αναφορές;

Εάν ένας τύπος δείχνει σε άλλο workbook, το Aspose.Cells θα διατηρήσει το κείμενο της αναφοράς (`='[Other.xlsx]Sheet1'!A1`). Δεν θα αξιολογήσει την εξωτερική τιμή εκτός εάν φορτώσετε και αυτό το workbook.

## Επαγγελματικές Συμβουλές για Κώδικα Έτοιμο για Παραγωγή

- **Cache the workbook** εάν διαβάζετε το

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Δημιουργήσετε και να Εξάγετε Excel σε HTML Χρησιμοποιώντας Aspose.Cells Java | Οδηγός Λειτουργιών Workbook](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Πώς να Μετατρέψετε Excel σε PDF σε Java Χρησιμοποιώντας Aspose.Cells&#58; Οδηγός Βήμα‑Βήμα](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Εξαγωγή Workbook Excel ως Εικόνα Χρησιμοποιώντας Aspose.Cells for Java&#58; Οδηγός Βήμα‑Βήμα](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}