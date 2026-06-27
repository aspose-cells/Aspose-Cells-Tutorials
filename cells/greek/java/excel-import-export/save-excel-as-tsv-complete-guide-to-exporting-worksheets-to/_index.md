---
category: general
date: 2026-06-27
description: Αποθηκεύστε το Excel ως TSV γρήγορα χρησιμοποιώντας Java. Μάθετε πώς
  να εξάγετε το φύλλο εργασίας σε κείμενο, να εξάγετε το φύλλο ως απλό κείμενο και
  να εξάγετε τη συμβολοσειρά δεδομένων του Excel με το Aspose.Cells.
draft: false
keywords:
- save excel as tsv
- export worksheet to text
- export sheet plain text
- export excel data string
language: el
og_description: Αποθήκευση Excel ως TSV με Java. Αυτό το σεμινάριο δείχνει πώς να
  εξάγετε το φύλλο εργασίας σε κείμενο, να εξάγετε το φύλλο ως απλό κείμενο και να
  εξάγετε το string δεδομένων του Excel αποδοτικά.
og_title: Αποθήκευση Excel ως TSV – Οδηγός εξαγωγής βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Save Excel as TSV quickly using Java. Learn how to export worksheet
    to text, export sheet plain text, and export Excel data string with Aspose.Cells.
  headline: Save Excel as TSV – Complete Guide to Exporting Worksheets to Text
  type: TechArticle
- description: Save Excel as TSV quickly using Java. Learn how to export worksheet
    to text, export sheet plain text, and export Excel data string with Aspose.Cells.
  name: Save Excel as TSV – Complete Guide to Exporting Worksheets to Text
  steps:
  - name: Pro tip
    text: If you’re dealing with password‑protected files, call `new Workbook("file.xlsx",
      new LoadOptions(LoadFormat.XLSX) {{ setPassword("yourPassword"); }})`.
  - name: 'Edge case: Custom delimiters'
    text: 'If your downstream system expects a pipe (`|`) instead of a tab, just change
      the delimiter:'
  - name: Pro tip
    text: 'After exporting, you can also capture the string directly:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
title: Αποθήκευση του Excel ως TSV – Πλήρης Οδηγός για την Εξαγωγή Φύλλων Εργασίας
  σε Κείμενο
url: /el/java/excel-import-export/save-excel-as-tsv-complete-guide-to-exporting-worksheets-to/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αποθήκευση Excel ως TSV – Πλήρης Οδηγός Εξαγωγής Φύλλων Εργασίας σε Κείμενο

Έχετε χρειαστεί ποτέ να **αποθηκεύσετε Excel ως TSV** αλλά δεν ήξερες ποιο κάλεσμα API να χρησιμοποιήσεις; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν εμπόδια όταν προσπαθούν να μετατρέψουν ένα υπολογιστικό φύλλο σε αρχείο με διαχωριστικό καρτέλας για επεξεργασία. Τα καλά νέα; Με λίγες γραμμές Java και Aspose.Cells μπορείτε να εξάγετε ένα φύλλο εργασίας σε κείμενο, να εξάγετε το φύλλο ως απλό κείμενο και ακόμη να εξάγετε τη συμβολοσειρά δεδομένων Excel χωρίς καμία δυσκολία.

Σε αυτό το tutorial θα περάσουμε από όλη τη ροή εργασίας — από τη φόρτωση ενός βιβλίου εργασίας μέχρι τη διαμόρφωση των επιλογών εξαγωγής και, τέλος, τη γραφή ενός αρχείου TSV στον δίσκο. Στο τέλος θα μπορείτε να **αποθηκεύσετε Excel ως TSV** σε οποιοδήποτε έργο Java, είτε επεξεργάζεστε ένα μόνο φύλλο είτε κάνετε batch δεκάδες αρχεία.

## Τι Καλύπτει Αυτός ο Οδηγός

* Φόρτωση βιβλίου εργασίας Excel από δίσκο  
* Επιλογή του κατάλληλου φύλλου εργασίας (ή επανάληψη σε πολλά)  
* Διαμόρφωση του `ExportTableOptions` για παραγωγή εξόδου απλού κειμένου  
* Γραφή των δεδομένων ως αρχείο τιμών διαχωρισμένων με καρτέλα (TSV)  
* Συμβουλές για διαχείριση μεγάλων περιοχών, διαφορετικών διαχωριστικών και χαρακτήρων Unicode  

Δεν απαιτούνται εξωτερικά εργαλεία — μόνο Aspose.Cells για Java και ένα runtime Java 8+.

---

## Βήμα 1: Ρύθμιση του Έργου και Φόρτωση του Βιβλίου Εργασίας

Πριν βουτήξουμε στον κώδικα, βεβαιωθείτε ότι έχετε προσθέσει το JAR του Aspose.Cells στο classpath του έργου σας. Αν χρησιμοποιείτε Maven, η εξάρτηση είναι η εξής:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

Τώρα μπορούμε να φορτώσουμε το βιβλίο εργασίας:

```java
// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Quick sanity check – print the number of worksheets
System.out.println("Worksheets count: " + workbook.getWorksheets().getCount());
```

> **Γιατί είναι σημαντικό:** Η φόρτωση του αρχείου είναι το πρώτο βήμα σε οποιαδήποτε ροή εργασίας **export Excel data string**. Αν το αρχείο δεν μπορεί να ανοιχθεί, τίποτα άλλο δεν θα λειτουργήσει.

### Pro tip
Αν εργάζεστε με αρχεία προστατευμένα με κωδικό, καλέστε `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("yourPassword"); }})`.

---

## Βήμα 2: Επιλογή του Φύλλου Εργασίας που Θέλετε να Εξάγετε

Μπορείτε να πάρετε το πρώτο φύλλο, ένα φύλλο με όνομα ή να επαναλάβετε όλα. Εδώ είναι η πιο απλή περίπτωση — εξαγωγή του πρώτου φύλλου εργασίας:

```java
// Step 2: Access the first worksheet (or any specific sheet)
Worksheet ws = workbook.getWorksheets().get(0);
System.out.println("Exporting sheet: " + ws.getName());
```

Αν χρειάζεται να **export worksheet to text** για κάθε φύλλο, τυλίξτε το παραπάνω σε βρόχο `for`:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    // Export each sheet separately...
}
```

---

## Βήμα 3: Δημιουργία και Διαμόρφωση Επιλογών Εξαγωγής

Η καρδιά του **export sheet plain text** βρίσκεται στο `ExportTableOptions`. Με την αλλαγή μερικών ιδιοτήτων μετατρέπουμε την περιοχή σε συμβολοσειρά απλού κειμένου με διαχωριστικό καρτέλας:

```java
// Step 3: Create export options for the table
ExportTableOptions exportOptions = new ExportTableOptions();

// Step 4: Configure the options – export as plain text and use a tab delimiter
exportOptions.setExportAsString(true);   // Returns a string instead of binary Excel format
exportOptions.setDelimiter('\t');        // Tab character makes it TSV
```

> **Γιατί να χρησιμοποιήσετε `setExportAsString(true)`;**  
> Ενημερώνει το Aspose.Cells να αντιμετωπίζει την έξοδο ως ακατέργαστο κείμενο, που είναι ακριβώς αυτό που χρειάζεστε όταν θέλετε να **save Excel as TSV**. Η εναλλακτική θα ήταν εξαγωγή CSV ή HTML, που δεν παρέχουν καθαρό διαχωρισμό με καρτέλα.

### Edge case: Προσαρμοσμένα διαχωριστικά
Αν το σύστημα προορισμού σας απαιτεί σωλήνα (`|`) αντί για καρτέλα, απλώς αλλάξτε το διαχωριστικό:

```java
exportOptions.setDelimiter('|');
```

---

## Βήμα 4: Εξαγωγή της Επιλεγμένης Περιοχής σε Αρχείο Κειμένου

Τώρα γράφουμε το αρχείο TSV. Η μέθοδος `exportTable` δέχεται τρία ορίσματα: την περιοχή κελιών, τη διαδρομή εξόδου και το `ExportTableOptions` που μόλις διαμορφώσαμε.

```java
// Step 5: Export the range A1:D20 to a text file using the configured options
ws.getCells().exportTable("A1:D20", "YOUR_DIRECTORY/out.tsv", exportOptions);
System.out.println("TSV file created successfully!");
```

Αν θέλετε να εξάγετε ολόκληρη την χρησιμοποιούμενη περιοχή, αντικαταστήστε το `"A1:D20"` με `ws.getCells().getMaxDisplayRange()`:

```java
String fullRange = ws.getCells().getMaxDisplayRange();
ws.getCells().exportTable(fullRange, "out.tsv", exportOptions);
```

### Pro tip
Μετά την εξαγωγή, μπορείτε επίσης να καταγράψετε τη συμβολοσειρά απευθείας:

```java
String tsvContent = ws.getCells().exportTable("A1:D20", exportOptions);
System.out.println(tsvContent); // Handy for debugging or sending over a network
```

Αυτό σας δίνει τη ακατέργαστη **export Excel data string** χωρίς να αγγίξετε το σύστημα αρχείων.

---

## Βήμα 5: Διαχείριση Μεγάλων Αρχείων και Συμβουλές Απόδοσης

Όταν εργάζεστε με τεράστια υπολογιστικά φύλλα (εκατοντάδες χιλιάδες γραμμές), σκεφτείτε τις εξής βελτιστοποιήσεις:

| Πρόβλημα | Λύση |
|----------|------|
| Πίεση μνήμης | Χρησιμοποιήστε `WorkbookFactory.create(InputStream)` για ροή του αρχείου αντί για πλήρη φόρτωση. |
| Αργό I/O | Γράψτε σε `BufferedWriter` ή χρησιμοποιήστε NIO `Files.newBufferedWriter`. |
| Χαρακτήρες Unicode | Βεβαιωθείτε ότι το αρχείο εξόδου γράφεται με UTF‑8: `exportTable(..., "out.tsv", exportOptions, Encoding.getUTF8())`. |

Παρακάτω υπάρχει ένα απόσπασμα που συνδυάζει ροή και κωδικοποίηση UTF‑8:

```java
try (InputStream is = Files.newInputStream(Paths.get("input.xlsx"));
     BufferedWriter writer = Files.newBufferedWriter(Paths.get("out.tsv"), StandardCharsets.UTF_8)) {

    Workbook wb = new Workbook(is);
    Worksheet sheet = wb.getWorksheets().get(0);
    ExportTableOptions opts = new ExportTableOptions();
    opts.setExportAsString(true);
    opts.setDelimiter('\t');

    String tsv = sheet.getCells().exportTable("A1:D20", opts);
    writer.write(tsv);
}
```

---

## Συνηθισμένα Πόνα και Πώς να τα Αποφύγετε

1. **Ξεχάσατε να ορίσετε `setExportAsString(true)`.**  
   Χωρίς αυτή τη σημαία το Aspose θα δημιουργήσει δυαδικό αρχείο Excel, σπάζοντας τον στόχο σας **export worksheet to text**.

2. **Χρήση λανθασμένου διαχωριστικού.**  
   Κόμμα αντί για καρτέλα θα σας δώσει CSV, όχι TSV. Ελέγξτε ξανά `setDelimiter('\t')`.

3. **Λανθασμένη σύνταξη περιοχής.**  
   Το `"A1:D20"` είναι σωστό, αλλά το `"A1:D20:"` (πρόσθετο άνω-κάτω τελεία) θα προκαλέσει `IllegalArgumentException`.  

4. **Δικαιώματα αρχείου.**  
   Βεβαιωθείτε ότι ο φάκελος προορισμού είναι εγγράψιμος. Σε Linux, το `chmod 755` συχνά λύνει το πρόβλημα.

---

## Συνοψίζοντας – Πλήρες Παράδειγμα Εργασίας

Ακολουθεί το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα που δείχνει **save Excel as TSV** από την αρχή μέχρι το τέλος:

```java
import com.aspose.cells.*;

import java.io.*;
import java.nio.charset.StandardCharsets;
import java.nio.file.*;

public class ExcelToTsv {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Choose worksheet (first sheet in this case)
        Worksheet ws = workbook.getWorksheets().get(0);

        // Set up export options for plain‑text TSV output
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);   // Export as string
        exportOptions.setDelimiter('\t');        // Tab delimiter for TSV

        // Define the range you want to export
        String range = "A1:D20"; // Change as needed or use ws.getCells().getMaxDisplayRange()

        // Export to a file
        ws.getCells().exportTable(range, "YOUR_DIRECTORY/out.tsv", exportOptions);
        System.out.println("Successfully saved Excel as TSV at YOUR_DIRECTORY/out.tsv");
    }
}
```

Η εκτέλεση αυτού του προγράμματος παράγει ένα αρχείο με τιμές διαχωρισμένες με καρτέλα (`out.tsv`) που οποιοδήποτε σύστημα προορισμού — είτε φορτωτής βάσης δεδομένων, σενάριο Unix `awk`, ή απλός προβολέας υπολογιστικών φύλλων — μπορεί να καταναλώσει.

---

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για να **save Excel as TSV** χρησιμοποιώντας Java και Aspose.Cells. Από τη φόρτωση του βιβλίου εργασίας, την επιλογή του σωστού φύλλου, τη διαμόρφωση του `ExportTableOptions`, μέχρι τη γραφή του αρχείου, έχετε τώρα ένα σταθερό, έτοιμο για παραγωγή πρότυπο για σενάρια **export worksheet to text**, **export sheet plain text**, και **export Excel data string**.

Τι έπεται; Δοκιμάστε την εξαγωγή πολλαπλών περιοχών, την αλλαγή διαχωριστικών εν κινήσει, ή τη ροή της εξόδου απευθείας σε HTTP response για λήψεις μέσω web. Οι ίδιες αρχές ισχύουν, και θα διαπιστώσετε ότι η διαχείριση δεδομένων Excel σε απλό κείμενο γίνεται παιχνιδάκι μόλις κατακτήσετε τα βασικά.

Έχετε ερωτήσεις ή αντιμετωπίζετε κάποιο παράξενο edge case; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σειρά Επόμενη;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη κώδικα με βήμα‑βήμα εξηγήσεις για να κυριαρχήσετε σε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Πώς να Εξάγετε Δεδομένα Excel σε HTML5 Χρησιμοποιώντας Aspose.Cells Java](/cells/english/java/import-export/aspose-cells-java-export-excel-html5/)
- [Απρόσκοπτη Εξαγωγή Δεδομένων από Excel με Aspose.Cells για Java](/cells/english/java/import-export/aspose-cells-java-excel-data-export/)
- [Πώς να Εξάγετε Φύλλο Εργασίας Excel σε PNG Χρησιμοποιώντας Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}