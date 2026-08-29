---
category: general
date: 2026-07-03
description: Αποθήκευση βιβλίου εργασίας ως CSV με ελεγχόμενα δεκαδικά ψηφία – μάθετε
  πώς να εξάγετε το Excel σε CSV, να ορίσετε σημαντικά ψηφία και να περιορίσετε τα
  δεκαδικά ψηφία σε Java.
draft: false
keywords:
- save workbook as csv
- export excel to csv
- set significant digits
- limit decimal places
- write number to cell
language: el
og_description: Αποθηκεύστε το βιβλίο εργασίας ως CSV γρήγορα. Αυτός ο οδηγός σας
  δείχνει πώς να εξάγετε το Excel σε CSV, να ορίσετε σημαντικά ψηφία και να περιορίσετε
  τα δεκαδικά ψηφία χρησιμοποιώντας τη Java.
og_title: Αποθήκευση βιβλίου εργασίας ως CSV – Java Εξαγωγή Excel σε CSV Εγχειρίδιο
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: save workbook as csv with controlled decimal places – learn how to
    export Excel to CSV, set significant digits, and limit decimal places in Java.
  headline: Save Workbook as CSV – Complete Java Guide to Export Excel to CSV
  type: TechArticle
- description: save workbook as csv with controlled decimal places – learn how to
    export Excel to CSV, set significant digits, and limit decimal places in Java.
  name: Save Workbook as CSV – Complete Java Guide to Export Excel to CSV
  steps:
  - name: Expected Output
    text: 'When you run the program, the console prints:'
  - name: Multiple Numbers in One Sheet
    text: 'If you have a table with many columns, each cell will inherit the same
      rounding rule unless you apply a custom format per cell. To **set significant
      digits** only for specific columns, you can create a `Style` object:'
  - name: Large Datasets
    text: When exporting millions of rows, memory usage can become a concern. Aspose.Cells
      offers a **streaming API** (`WorkbookDesigner`) that writes rows directly to
      the CSV without holding the entire workbook in memory. The same `CsvSaveOptions`
      can be attached to the stream.
  - name: Different Locale Settings
    text: 'CSV files sometimes need a comma (`'',''`) as the decimal separator. Use:'
  - name: Verify the Result
    text: 'Open `output/sigDigits.csv` in any text editor or spreadsheet program.
      You should see:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- CSV
- Excel
title: Αποθήκευση βιβλίου εργασίας ως CSV – Πλήρης οδηγός Java για εξαγωγή Excel σε
  CSV
url: /el/java/excel-import-export/save-workbook-as-csv-complete-java-guide-to-export-excel-to/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αποθήκευση Βιβλίου Εργασίας ως CSV – Πλήρης Οδηγός Java για Εξαγωγή Excel σε CSV

Έχετε ποτέ χρειαστεί να **save workbook as csv** αλλά αντιμετωπίζετε προβλήματα στρογγυλοποίησης; Δεν είστε μόνοι σας. Όταν εξάγετε Excel σε CSV, αυτά τα ενοχλητικά επιπλέον δεκαδικά μπορούν να μετατρέψουν μια καθαρή αναφορά σε ένα χάος αριθμών.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα ένα πρακτικό παράδειγμα που σας δείχνει ακριβώς πώς να **export Excel to CSV**, **set significant digits**, και **limit decimal places** ενώ **writing a number to a cell**. Στο τέλος θα έχετε ένα έτοιμο για εκτέλεση Java snippet που αποθηκεύει ένα βιβλίο εργασίας ως CSV με τέλεια στρογγυλοποιημένες τιμές.

## Τι Θα Μάθετε

- Πώς να δημιουργήσετε ένα νέο βιβλίο εργασίας από το μηδέν.
- Ο τρόπος για **write number to cell** A1 χρησιμοποιώντας Aspose.Cells.
- Γιατί η μέθοδος `CsvSaveOptions.setSignificantDigits` είναι το κλειδί για τη στρογγυλοποίηση.
- Πώς να **limit decimal places** όταν **save workbook as csv**.
- Ένα πλήρες, εκτελέσιμο δείγμα κώδικα που μπορείτε να αντιγράψετε‑επικολλήσετε στο IDE σας.

Δεν απαιτείται προηγούμενη εμπειρία με Aspose.Cells· απλώς μια βασική ρύθμιση Java και περιέργεια για καθαρές εξαγωγές CSV.

## Προαπαιτούμενα

- Java 17 ή νεότερη (ο κώδικας λειτουργεί επίσης με Java 8+).
- Βιβλιοθήκη Aspose.Cells for Java (μπορείτε να την κατεβάσετε από το Maven Central):
  ```xml
  <dependency>
      <groupId>com.aspose</groupId>
      <artifactId>aspose-cells</artifactId>
      <version>23.12</version>
  </dependency>
  ```
- Ένα IDE ή κειμενογράφο με τον οποίο αισθάνεστε άνετα (IntelliJ IDEA, Eclipse, VS Code…).

Τα έχετε; Τέλεια—ας βουτήξουμε.

## Βήμα 1: Δημιουργία Νέου Workbook

Πρώτα απ' όλα. Χρειαζόμαστε ένα νέο αντικείμενο `Workbook` που θα κρατά τα δεδομένα μας. Σκεφτείτε το ως ένα κενό αρχείο Excel που περιμένει περιεχόμενο.

```java
import com.aspose.cells.*;

public class CsvExportDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();
```

> **Pro tip:** Η δημιουργία ενός `Workbook` χωρίς διαδρομή αρχείου δημιουργεί αυτόματα ένα μόνο κενό φύλλο εργασίας, το οποίο είναι ιδανικό για προγραμματισμένη εισαγωγή δεδομένων.

## Βήμα 2: Λήψη του Πρώτου Worksheet

Τώρα που έχουμε ένα βιβλίο εργασίας, ας πάρουμε το πρώτο φύλλο ώστε να αρχίσουμε να γεμίζουμε τα κελιά.

```java
        // Step 2: Get the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);
```

Αν χρειαστείτε ποτέ περισσότερα από ένα φύλλα, απλώς καλέστε `workbook.getWorksheets().add()` και κρατήστε μια αναφορά σε κάθε αντικείμενο `Worksheet`.

## Βήμα 3: Εγγραφή Αριθμού στο Κελί A1

Εδώ συμβαίνει το τμήμα **write number to cell**. Θα τοποθετήσουμε μια τιμή κινητής υποδιαστολής με πολλά δεκαδικά ψηφία—ιδανική για την επίδειξη στρογγυλοποίησης.

```java
        // Step 3: Write a number to cell A1
        sheet.getCells().putValue("A1", 1234.56789);
```

Γιατί το A1; Είναι το κλασικό σημείο εκκίνησης και οι περισσότεροι αναγνώστες το αναγνωρίζουν αμέσως. Φυσικά, μπορείτε να γράψετε σε οποιαδήποτε διεύθυνση (`B2`, `C3`, κλπ.) αλλάζοντας τη συμβολοσειρά.

## Βήμα 4: Ορισμός CSV Save Options για Περιορισμό Δεκαδικών Ψηφίων

Η Aspose.Cells μας παρέχει την κλάση `CsvSaveOptions` που ελέγχει τον τρόπο γραφής του CSV. Η μέθοδος `setSignificantDigits` είναι το μαγικό ραβδί για τη στρογγυλοποίηση. Ορίζοντάς την σε **4** σημαίνει «διατήρηση τεσσάρων σημαντικών ψηφίων», κάτι που μετατρέπει το `1234.56789` σε `1235`.

```java
        // Step 4: Set CSV save options to limit decimal places
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        csvOptions.setSignificantDigits(4); // Rounds to 1235
```

> **Why use `setSignificantDigits`?**  
> Σε αντίθεση με την απλή μορφοποίηση συμβολοσειράς, αυτή η μέθοδος σέβεται το μέγεθος του αριθμού, εξασφαλίζοντας ότι μεγάλες και μικρές τιμές στρογγυλοποιούνται σταθερά. Είναι ο προτεινόμενος τρόπος για **limit decimal places** όταν **save workbook as csv**.

Αν προτιμάτε έναν σταθερό αριθμό δεκαδικών ψηφίων αντί για σημαντικά ψηφία, μπορείτε επίσης να χρησιμοποιήσετε `csvOptions.setDecimalSeparator('.')` μαζί με προσαρμοσμένη μορφοποίηση στο κελί, αλλά το `setSignificantDigits` καλύπτει τις περισσότερες περιπτώσεις χρήσης με μία κλήση.

## Βήμα 5: Αποθήκευση του Workbook ως Αρχείο CSV

Τέλος, καλούμε τη μέθοδο `save`, περνώντας τη διαδρομή και τις ρυθμισμένες επιλογές μας. Αυτή είναι η στιγμή που πραγματικά **save workbook as csv**.

```java
        // Step 5: Save the workbook as a CSV file
        String outputPath = "output/sigDigits.csv";
        workbook.save(outputPath, csvOptions);
        System.out.println("Workbook successfully saved as CSV at: " + outputPath);
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Όταν εκτελέσετε το πρόγραμμα, η κονσόλα εκτυπώνει:

```
Workbook successfully saved as CSV at: output/sigDigits.csv
```

Και το δημιουργημένο `sigDigits.csv` περιέχει μια μόνο γραμμή:

```
1235
```

Παρατηρήστε πώς το αρχικό `1234.56789` στρογγυλοποιήθηκε σε `1235`—ακριβώς αυτό που ζητήσαμε με το `setSignificantDigits(4)`.

## Διαχείριση Ακραίων Περιπτώσεων

### Πολλοί Αριθμοί σε Ένα Φύλλο

Αν έχετε έναν πίνακα με πολλές στήλες, κάθε κελί θα κληρονομήσει τον ίδιο κανόνα στρογγυλοποίησης εκτός εάν εφαρμόσετε προσαρμοσμένη μορφή ανά κελί. Για να **set significant digits** μόνο για συγκεκριμένες στήλες, μπορείτε να δημιουργήσετε ένα αντικείμενο `Style`:

```java
Style style = workbook.createStyle();
style.setNumber(4); // 4 decimal places
StyleFlag flag = new StyleFlag();
flag.setNumber(true);
sheet.getCells().get("B2").setStyle(style, flag);
```

### Μεγάλα Σύνολα Δεδομένων

Κατά την εξαγωγή εκατομμυρίων γραμμών, η χρήση μνήμης μπορεί να γίνει πρόβλημα. Η Aspose.Cells προσφέρει ένα **streaming API** (`WorkbookDesigner`) που γράφει τις γραμμές απευθείας στο CSV χωρίς να κρατά ολόκληρο το βιβλίο εργασίας στη μνήμη. Το ίδιο `CsvSaveOptions` μπορεί να προσαρμοστεί στη ροή.

### Διαφορετικές Ρυθμίσεις Τοπικής

Τα αρχεία CSV μερικές φορές χρειάζονται κόμμα (`','`) ως διαχωριστικό δεκαδικών. Χρησιμοποιήστε:

```java
csvOptions.setDecimalSeparator(',');
```

Τώρα το `1234.56789` θα γίνει `1235` (ακόμη στρογγυλοποιημένο) αλλά το αρχείο θα χρησιμοποιεί κόμματα όπου είναι κατάλληλο.

## Πλήρες, Έτοιμο‑για‑Εκτέλεση Παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα, συμπεριλαμβανομένων των imports και σχολίων, ώστε να το ενσωματώσετε σε ένα νέο έργο Java και να το εκτελέσετε αμέσως.

```java
import com.aspose.cells.*;

public class CsvExportDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook (blank Excel file)
        Workbook workbook = new Workbook();

        // Access the first worksheet (default sheet)
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Write a high‑precision number to cell A1
        sheet.getCells().putValue("A1", 1234.56789);

        // Configure CSV options to round to 4 significant digits
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        csvOptions.setSignificantDigits(4); // This will round 1234.56789 to 1235

        // Define output path (ensure the folder exists)
        String outputPath = "output/sigDigits.csv";

        // Save the workbook as CSV using the options above
        workbook.save(outputPath, csvOptions);

        System.out.println("Workbook successfully saved as CSV at: " + outputPath);
    }
}
```

### Επαλήθευση του Αποτελέσματος

Ανοίξτε το `output/sigDigits.csv` σε οποιονδήποτε επεξεργαστή κειμένου ή πρόγραμμα λογιστικού φύλλου. Θα πρέπει να δείτε:

```
1235
```

Αν αλλάξετε το `setSignificantDigits(2)` και ξανατρέξετε, το αρχείο θα περιέχει `12`. Πειραματιστείτε με διαφορετικές τιμές για να δείτε πώς η στρογγυλοποίηση συμπεριφέρεται τόσο σε μεγάλα όσο και σε μικρά νούμερα.

## Συχνές Ερωτήσεις & Προβλήματα

- **“Will this also affect dates or text?”**  
  Όχι. Η στρογγυλοποίηση εφαρμόζεται μόνο σε αριθμητικά κελιά. Το κείμενο, οι ημερομηνίες και οι τύποι γράφονται όπως είναι.

- **“What if I need a custom delimiter, like a semicolon?”**  
  Χρησιμοποιήστε `csvOptions.setSeparator(';')` πριν από την αποθήκευση.

- **“Can I export an existing .xlsx file instead of creating a new workbook?”**  
  Απόλυτα. Αντικαταστήστε το `new Workbook()` με `new Workbook("input.xlsx")` και τα υπόλοιπα βήματα παραμένουν τα ίδια.

- **“Does this work on Android?”**  
  Η Aspose.Cells for Java υποστηρίζει Android, αλλά πρέπει να χρησιμοποιήσετε την έκδοση της βιβλιοθήκης συμβατή με Android και να εξασφαλίσετε ότι έχετε δικαιώματα εγγραφής για το φάκελο εξόδου.

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για να **save workbook as csv** διατηρώντας τους αριθμούς σας τακτικούς. Από τη δημιουργία ενός workbook, **writing number to cell**, τη ρύθμιση του **set significant digits**, μέχρι τελικά το **export Excel to CSV** με περιορισμένα δεκαδικά ψηφία—όλη η διαδικασία είναι τώρα στα χέρια σας.

Στη συνέχεια, ίσως θέλετε να εξερευνήσετε:

- Προσθήκη πολλαπλών worksheets και εξαγωγή καθενός ως ξεχωριστό CSV.
- Χρήση του `CsvSaveOptions` για έλεγχο της κωδικοποίησης (UTF‑8, UTF‑16) για διεθνή δεδομένα.
- Συνδυασμός αυτής της προσέγγισης με μια υπηρεσία web ώστε οι χρήστες να μπορούν να κατεβάζουν CSV κατά απαίτηση.

Δοκιμάστε τα και θα γίνετε γρήγορα το άτομο-αναφορά για καθαρές εξαγωγές CSV στην ομάδα σας. Καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Φορτώσετε και Αποθηκεύσετε Excel ως CSV Χρησιμοποιώντας Aspose.Cells για Java: Ένας Πλήρης Οδηγός](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [Excel Aspose Cells Java Trim Save Csv](/cells/hongkong/java/workbook-operations/excel-aspose-cells-java-trim-save-csv/)
- [Αποθήκευση Workbook σε Μορφή Text Csv](/cells/hongkong/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}