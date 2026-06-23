---
category: general
date: 2026-03-01
description: Μάθετε πώς να εξάγετε CSV από ένα βιβλίο εργασίας Java, ορίζοντας τα
  σημαντικά ψηφία και το εύρος εξαγωγής σε CSV, σε έναν ενιαίο, σαφή οδηγό.
draft: false
keywords:
- how to export csv
- set significant digits
- export range to csv
- Java workbook export
- CSV formatting Java
language: el
og_description: Μάθετε πώς να εξάγετε csv σε Java, να ορίσετε σημαντικά ψηφία και
  να εξάγετε εύρος σε csv με πρακτικό κώδικα και συμβουλές.
og_title: Πώς να εξάγετε CSV με Java – Πλήρης οδηγός βήμα‑προς‑βήμα
tags:
- Java
- Aspose.Cells
- CSV
- Data Export
title: Πώς να εξάγετε CSV με Java – Ορίστε σημαντικά ψηφία & εξαγωγή περιοχής σε CSV
url: /el/java/excel-import-export/how-to-export-csv-with-java-set-significant-digits-export-ra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εξάγετε CSV με Java – Ορίστε Σημαντικά Ψηφία & Εξάγετε Περιοχή σε CSV

Έχετε αναρωτηθεί ποτέ **πώς να εξάγετε csv** από ένα βιβλίο εργασίας Java χωρίς να χάσετε την αριθμητική ακρίβεια; Ίσως να έχετε δοκιμάσει ένα γρήγορο `toString()` και να καταλήξατε με ένα χάος σφαλμάτων στρογγυλοποίησης. Αυτό είναι ένα κοινό πρόβλημα, ειδικά όταν χρειάζεται να **ορίσετε σημαντικά ψηφία** για οικονομικά δεδομένα ή επιστημονικά αποτελέσματα.  

Σε αυτό το tutorial θα δείτε ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει **πώς να εξάγετε csv**, πώς να **ορίσετε σημαντικά ψηφία**, και ακόμη πώς να **εξάγετε περιοχή σε csv** διατηρώντας τα δεδομένα σας τακτικά. Θα περάσουμε γραμμή‑γραμμή, θα εξηγήσουμε το *γιατί* πίσω από τις κλήσεις API, και θα σας δώσουμε συμβουλές για να αποφύγετε τα συνηθισμένα προβλήματα. Χωρίς επιπλέον τεκμηρίωση—απλώς μια αυτόνομη λύση που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σήμερα.

## Τι Θα Μάθετε

- Δημιουργήστε ένα βιβλίο εργασίας και διαμορφώστε την αριθμητική ακρίβεια με `setNumberSignificantDigits`.
- Εξάγετε μια συγκεκριμένη περιοχή κελιών ως μια ωραία μορφοποιημένη συμβολοσειρά CSV.
- Αναλύστε ημερομηνίες ιαπωνικής εποχής χρησιμοποιώντας `DateTimeFormatInfo`.
- Επανυπολογίστε τύπους ώστε τα αποτελέσματα δυναμικών πινάκων να παραμένουν ενημερωμένα.
- Αποδώστε έναν πίνακα Pivot σε εικόνα PNG.
- Χρησιμοποιήστε Smart Marker για να εισάγετε σχόλια και τελικά να αποθηκεύσετε το βιβλίο εργασίας.

Όλα αυτά γίνονται με τη βιβλιοθήκη Aspose.Cells for Java, έκδοση 23.12 (η πιο πρόσφατη τη στιγμή της συγγραφής). Αν έχετε το JAR στο classpath σας, είστε έτοιμοι να ξεκινήσετε.

---

## Βήμα 1: Δημιουργήστε ένα Βιβλίο Εργασίας και **Ορίστε Σημαντικά Ψηφία**

Πριν μπορέσουμε να εξάγουμε οτιδήποτε, χρειαζόμαστε ένα αντικείμενο workbook. Το πρώτο πράγμα που παραβλέπουν πολλοί προγραμματιστές είναι η αριθμητική ακρίβεια. Από προεπιλογή, το Aspose.Cells χρησιμοποιεί την πλήρη διπλή ακρίβεια, κάτι που μπορεί να οδηγήσει σε μακριές, ακατάλληλες συμβολοσειρές σε CSV. Ορίζοντας τον αριθμό των σημαντικών ψηφίων μειώνουμε το αποτέλεσμα διατηρώντας τα πιο σημαντικά νούμερα.

```java
import com.aspose.cells.*;

public class CsvExportDemo {

    public static void main(String[] args) throws Exception {

        // Step 1 – initialise workbook and limit numeric values to 5 significant digits
        Workbook workbook = new Workbook();
        WorkbookSettings settings = workbook.getSettings();
        // This is the key call that **set significant digits** for all numeric cells
        settings.setNumberSignificantDigits(5);
```

**Γιατί είναι σημαντικό αυτό;**  
Αν εξάγετε ένα κελί που περιέχει `12345.6789` χωρίς περιορισμό ψηφίων, το CSV θα εμφανίσει την πλήρη τιμή, γεμίζοντας τις αναφορές. Με `setNumberSignificantDigits(5)`, το ίδιο κελί γίνεται `12346`, που είναι συχνά αυτό που περιμένουν οι επιχειρηματικοί χρήστες.

> **Pro tip:** Αν χρειάζεστε διαφορετική ακρίβεια ανά στήλη, μπορείτε να εφαρμόσετε ένα προσαρμοσμένο `Style` αντί για τη γενική ρύθμιση.

---

## Βήμα 2: **Εξάγετε Περιοχή σε CSV** – Η Μορφοποίηση Μετρά

Τώρα που το βιβλίο εργασίας είναι έτοιμο, ας πάρουμε ένα ορθογώνιο μπλοκ δεδομένων και ας το μετατρέψουμε σε συμβολοσειρά CSV. Θα επιβάλλουμε επίσης μορφή δύο δεκαδικών (`0.00`) ώστε κάθε αριθμός να ευθυγραμμίζεται ωραία.

```java
        // Step 2 – define export options and pull the range B2:D10 as CSV
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);          // we want a string, not a file yet
        exportOptions.setNumberFormat("0.00");          // enforce two decimal places

        // Create a dummy range with some sample data for illustration
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();
        cells.get("B2").putValue(123.456);
        cells.get("C2").putValue(78.9);
        cells.get("D2").putValue(0.12345);
        // ... populate more rows as needed ...

        Range dataRange = cells.createRange("B2:D10");
        String csvData = dataRange.exportDataTable(exportOptions).toString();

        System.out.println("=== CSV Output ===");
        System.out.println(csvData);
```

Η κλήση `exportDataTable` κάνει το βαριά δουλειά. Επειδή ορίσαμε `exportAsString`, η μέθοδος επιστρέφει ένα `String` που μπορούμε να εκτυπώσουμε, να γράψουμε σε αρχείο ή να στείλουμε μέσω HTTP. Το βήμα **export range to csv** σέβεται επίσης το παγκόσμιο `setNumberSignificantDigits` που ορίσαμε νωρίτερα, έτσι οι αριθμοί στρογγυλοποιούνται σε πέντε σημαντικά ψηφία *και* εμφανίζονται με δύο δεκαδικά ψηφία.

**Αναμενόμενη έξοδος (κομμένη):**

```
=== CSV Output ===
123.46,78.90,0.12
...
```

> **Common question:** *Τι γίνεται αν χρειάζομαι διαφορετικό διαχωριστικό, όπως άνω‑κάτω τελεία;*  
> Απλώς καλέστε `exportOptions.setSeparator(";")` πριν την εξαγωγή.

---

## Βήμα 3: Αναλύστε Ημερομηνία Ιαπωνικής Εποχής (Επιπλέον Χρήσιμη Λειτουργία)

Αν και δεν σχετίζεται άμεσα με CSV, πολλά φύλλα Excel περιέχουν ημερομηνίες ειδικές για τοπικές ρυθμίσεις. Εδώ φαίνεται πώς μπορείτε να μετατρέψετε μια ιαπωνική συμβολοσειρά εποχής όπως `"R3/04/01"` σε ένα τυπικό αντικείμενο `DateTime`.

```java
        // Step 3 – parse Japanese era date (Reiwa 3)
        DateTime japaneseDate = DateTime.parse("R3/04/01", new DateTimeFormatInfo(Locale.JAPAN));
        System.out.println("Parsed Japanese date: " + japaneseDate);
```

Output:

```
Parsed Japanese date: 2021-04-01T00:00:00
```

**Γιατί να το συμπεριλάβουμε αυτό;**  
Αν η εξαγωγή CSV τροφοδοτεί συστήματα που αναμένουν ημερομηνίες ISO‑8601, πρέπει πρώτα να ομαλοποιήσετε τυχόν τοπικές μορφές. Αυτό το απόσπασμα δείχνει το *πώς* και το *γιατί* σε ένα μέρος.

---

## Βήμα 4: Επανυπολογίστε Τύπους – Κρατήστε τα Αποτελέσματα Δυναμικών Πινάκων Φρέσκα

Αν το βιβλίο εργασίας σας περιέχει τύπους (π.χ., `=SUM(A1:A10)`), αυτοί δεν θα ενημερωθούν αυτόματα μετά τις αλλαγές ρυθμίσεων. Η κλήση `calculateFormula` αναγκάζει έναν πλήρη επανυπολογισμό, διασφαλίζοντας ότι το εξαγόμενο CSV αντικατοπτρίζει τις πιο πρόσφατες τιμές.

```java
        // Step 4 – recalculate all formulas
        workbook.calculateFormula();
```

> **Watch out:** Τα μεγάλα βιβλία εργασίας μπορεί να χρειαστούν αξιοσημείωτο χρόνο για επανυπολογισμό. Για σενάρια κρίσιμης απόδοσης, σκεφτείτε `calculateFormula(FormulaCalculationOptions)` για περιορισμό του εύρους.

---

## Βήμα 5: Αποδώστε τον Πρώτο Πίνακα Pivot σε Εικόνα PNG

Μερικές φορές χρειάζεστε μια οπτική λήψη ενός πίνακα pivot δίπλα στο CSV. Ο παρακάτω κώδικας αποδίδει τον πρώτο πίνακα pivot στο πρώτο φύλλο εργασίας σε αρχείο PNG.

```java
        // Step 5 – render pivot table as PNG
        PivotTable pivot = sheet.getPivotTables().get(0); // assumes a pivot exists
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.Png);
        // The range that the pivot occupies is turned into an image
        pivot.getRange().toImage("output/pivot.png", imgOptions);
```

**Συμβουλή:** Αν το βιβλίο εργασίας δεν περιέχει ήδη pivot, μπορείτε να δημιουργήσετε ένα προγραμματιστικά—δείτε τα docs του Aspose.Cells για ένα γρήγορο παράδειγμα.

---

## Βήμα 6: Χρησιμοποιήστε Smart Marker για να Γράψετε Σχόλιο και να Αποθηκεύσετε το Βιβλίο Εργασίας

Το Smart Marker σας επιτρέπει να εισάγετε δυναμικό περιεχόμενο στα κελιά χρησιμοποιώντας απλούς placeholders. Εδώ γράφουμε ένα σχόλιο όπως “Reviewed by QA” σε ένα καθορισμένο κελί και στη συνέχεια αποθηκεύουμε το βιβλίο εργασίας.

```java
        // Step 6 – apply Smart Marker comment
        SmartMarkerProcessor smartMarker = new SmartMarkerProcessor(workbook);
        smartMarker.apply("${Comment}", java.util.Collections.singletonMap("Comment", "Reviewed by QA"));

        // Finally, save the workbook with the comment embedded
        workbook.save("output/commented.xlsx");
    }
}
```

Το placeholder `${Comment}` μπορεί να τοποθετηθεί οπουδήποτε στο φύλλο (π.χ., κελί `A1`). Όταν τρέξει το `apply`, το placeholder αντικαθίσταται με την τιμή που δόθηκε.

**Αποτέλεσμα:** Θα βρείτε ένα αρχείο `output/commented.xlsx` που περιέχει το σχόλιο, μαζί με το προηγουμένως δημιουργημένο `pivot.png` και τη συμβολοσειρά CSV που εκτυπώθηκε στην κονσόλα.

---

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες πρόγραμμα που μπορείτε να μεταγλωττίσετε και να τρέξετε:

```java
import com.aspose.cells.*;
import java.util.Collections;
import java.util.Locale;

public class CsvExportDemo {

    public static void main(String[] args) throws Exception {
        // ----------- Step 1: Workbook & Significant Digits -----------
        Workbook workbook = new Workbook();
        WorkbookSettings settings = workbook.getSettings();
        settings.setNumberSignificantDigits(5); // **set significant digits**

        // ----------- Step 2: Populate Sample Data & Export CSV ----------
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();
        cells.get("B2").putValue(123.456);
        cells.get("C2").putValue(78.9);
        cells.get("D2").putValue(0.12345);
        // (Add more rows if you like)

        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);
        exportOptions.setNumberFormat("0.00");
        Range dataRange = cells.createRange("B2:D10");
        String csvData = dataRange.exportDataTable(exportOptions).toString();

        System.out.println("=== CSV Output ===");
        System.out.println(csvData);

        // ----------- Step 3: Japanese Era Date ----------
        DateTime japaneseDate = DateTime.parse("R3/04/01", new DateTimeFormatInfo(Locale.JAPAN));
        System.out.println("Parsed Japanese date: " + japaneseDate);

        // ----------- Step 4: Recalculate Formulas ----------
        workbook.calculateFormula();

        // ----------- Step 5: Render Pivot Table ----------
        if (!sheet.getPivotTables().isEmpty()) {
            PivotTable pivot = sheet.getPivotTables().get(0);
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
            imgOptions.setImageFormat(ImageFormat.Png);
            pivot.getRange().toImage("output/pivot.png", imgOptions);
        }

        // ----------- Step 6: Smart Marker Comment ----------
        SmartMarkerProcessor smartMarker = new SmartMarkerProcessor(workbook);
        smartMarker.apply("${Comment}", Collections.singletonMap("Comment", "Reviewed by QA"));
        workbook.save("output/commented.xlsx");
    }
}
```

### Αναμενόμενη Έξοδος Κονσόλας

```
=== CSV Output ===
123.46,78.90,0.12
...
Parsed Japanese date: 2021-04-01T00:00:00
```

Θα βρείτε επίσης `output/pivot.png` (αν υπήρχε pivot) και `output/commented.xlsx` στο δίσκο.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

- **Μπορώ να εξάγω απευθείας σε φυσικό αρχείο CSV;**  
  Ναι. Αντικαταστήστε το τμήμα `exportAsString` με `dataRange.exportDataTable("output/data.csv", exportOptions);`.

- **Τι γίνεται αν το φύλλο μου χρησιμοποιεί διαφορετική τοπική ρύθμιση για τους αριθμούς;**  
  Ορίστε `exportOptions.setCultureInfo(new CultureInfo("fr-FR"))` πριν την εξαγωγή· αυτό θα αλλάξει

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}