---
category: general
date: 2026-06-18
description: Πώς να εξάγετε αρχεία Excel γρήγορα – μάθετε να μετατρέπετε xlsx σε csv,
  να εξάγετε περιοχή σε csv και να γράφετε csv σε αρχείο χρησιμοποιώντας Java. Απλή,
  αξιόπιστη λύση.
draft: false
keywords:
- how to export excel
- convert xlsx to csv
- write csv to file
- export range to csv
- export excel to csv
language: el
og_description: Πώς να εξάγετε αρχεία Excel σε Java. Μετατρέψτε xlsx σε csv, εξάγετε
  περιοχή σε csv και γράψτε csv σε αρχείο με ένα έτοιμο παράδειγμα προς εκτέλεση.
og_title: Πώς να εξάγετε το Excel – Πλήρης οδηγός μετατροπής σε CSV
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: How to export Excel files quickly – learn to convert xlsx to csv, export
    range to csv, and write csv to file using Java. Simple, reliable solution.
  headline: 'How to Export Excel: Step‑by‑Step Guide to CSV Conversion'
  type: TechArticle
tags:
- Java
- Excel
- CSV
- File I/O
title: 'Πώς να εξάγετε το Excel: Οδηγός βήμα‑βήμα για τη μετατροπή σε CSV'
url: /el/java/excel-import-export/how-to-export-excel-step-by-step-guide-to-csv-conversion/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εξάγετε Excel: Πλήρης Οδηγός Μετατροπής σε CSV

Έχετε αναρωτηθεί **πώς να εξάγετε δεδομένα Excel** χωρίς να ανοίξετε το φύλλο χειροκίνητα; Δεν είστε μόνοι—πολλοί προγραμματιστές χρειάζονται έναν γρήγορο, προγραμματιζόμενο τρόπο για να μετατρέψουν ένα βιβλίο εργασίας *.xlsx* σε ένα απλό αρχείο CSV. Σε αυτόν τον οδηγό θα περάσουμε από τη μετατροπή ενός βιβλίου εργασίας Excel σε CSV, την εξαγωγή ενός συγκεκριμένου εύρους και, τέλος, τη γραφή του CSV σε αρχείο. Στο τέλος θα έχετε ένα αυτόνομο απόσπασμα Java που κάνει ακριβώς αυτό.

Θα προσθέσουμε επίσης χρήσιμες συμβουλές όπως το **πώς να μετατρέψετε xlsx σε csv** με προσαρμοσμένες μορφές αριθμών και ημερομηνιών, και γιατί μπορεί να προτιμάτε την εξαγωγή ενός εύρους αντί ολόκληρου του φύλλου. Χωρίς περιττές πληροφορίες, μόνο μια πρακτική λύση που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

- Java 17 ή νεότερη (ο κώδικας χρησιμοποιεί το σύγχρονο API `Files.writeString`).
- Τη βιβλιοθήκη Aspose.Cells for Java (ή οποιαδήποτε συμβατή βιβλιοθήκη που παρέχει `ExportTableOptions`). Μπορείτε να την κατεβάσετε από το Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

- Ένα απλό αρχείο Excel (`input.xlsx`) τοποθετημένο σε φάκελο που ελέγχετε (αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή).

Τα έχετε; Τέλεια—ας ξεκινήσουμε.

## Βήμα 1: Ρύθμιση Επιλογών Εξαγωγής (Export Range to CSV)

Το πρώτο που πρέπει να κάνετε είναι να πείτε στη βιβλιοθήκη **πώς να εξάγει δεδομένα Excel**. Το `ExportTableOptions` σας επιτρέπει να ορίσετε την έξοδο ως συμβολοσειρά, τη μορφοποίηση αριθμών και τη μορφοποίηση ημερομηνιών σε ένα τακτοποιημένο αντικείμενο.

```java
// Configure export options for the table
ExportTableOptions exportOptions = new ExportTableOptions();
exportOptions.setExportAsString(true);               // Export as a plain string
exportOptions.setNumberFormat("#,##0.00");           // Two‑decimal numbers
exportOptions.setDateFormat("yyyy-MM-dd");           // ISO‑style dates
```

> **Γιατί είναι σημαντικό:** Εξάγοντας ως συμβολοσειρά αποφεύγετε την επεξεργασία ενδιάμεσων ροών byte, και οι προσαρμοσμένες μορφές εξασφαλίζουν ότι το CSV θα φαίνεται ακριβώς όπως το περιμένετε—ιδιαίτερα όταν αργότερα **write csv to file**.

## Βήμα 2: Φόρτωση του Βιβλίου Εργασίας (Convert XLSX to CSV)

Στη συνέχεια, ανοίξτε το πηγαίο βιβλίο εργασίας. Αυτό είναι το σημείο όπου πραγματικά **convert xlsx to csv**—η μετατροπή θα γίνει αργότερα, αλλά η φόρτωση του αρχείου είναι το πρώτο βήμα.

```java
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Grab the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);
```

Αν χρειάζεστε να εργαστείτε με διαφορετικό φύλλο, απλώς αλλάξτε το δείκτη ή χρησιμοποιήστε `get("SheetName")`. Η βιβλιοθήκη διαχειρίζεται τόσο μορφές `.xlsx` όσο και κληρονομημένες `.xls`, οπότε καλύπτετε τις περισσότερες περιπτώσεις.

## Βήμα 3: Εξαγωγή Συγκεκριμένου Εύρους (Export Range to CSV)

Συχνά δεν χρειάζεστε ολόκληρο το φύλλο—ίσως μόνο τον πίνακα πωλήσεων στα κελιά `A1:D10`. Εδώ έρχεται το **export range to csv**. Η μέθοδος επιστρέφει μια μοναδική `String` που περιέχει τα δεδομένα CSV.

```java
// Export the range A1:D10 as a CSV string using the options defined above
String csvData = worksheet.getCells()
                          .exportTableAsString("A1:D10", exportOptions);
```

> **Pro tip:** Η συμβολοσειρά εύρους ακολουθεί τη σημειογραφία A1 του Excel, οπότε μπορείτε εύκολα να την προσαρμόσετε σε `"B2:F20"` ή σε οποιοδήποτε δυναμικό εύρος υπολογίζετε κατά την εκτέλεση.

## Βήμα 4: Γραφή της Συμβολοσειράς CSV σε Αρχείο (Write CSV to File)

Τώρα που έχουμε το κείμενο CSV στη μνήμη, το τελευταίο βήμα είναι η αποθήκευσή του. Η Java 11+ το κάνει με μία γραμμή κώδικα μέσω του `Files.writeString`.

```java
// Write the CSV string to an output text file
Files.writeString(Paths.get("YOUR_DIRECTORY/output.txt"), csvData);
```

Το αρχείο θα δημιουργηθεί αν δεν υπάρχει, και θα αντικατασταθεί αν υπάρχει—ιδανικό για εργασίες batch που επαναδημιουργούν αναφορές καθημερινά.

## Βήμα 5: Επαλήθευση του Αποτελέσματος (Export Excel to CSV)

Μια γρήγορη επιβεβαίωση εξοικονομεί ώρες εντοπισμού σφαλμάτων. Ανοίξτε το `output.txt` σε οποιονδήποτε επεξεργαστή κειμένου ή εισάγετέ το ξανά στο Excel για να βεβαιωθείτε ότι η μετατροπή πέτυχε.

```text
Product,Quantity,Price,Total
Widget A,10,12.50,125.00
Widget B,5,8.75,43.75
...
```

Αν οι αριθμοί εμφανίζονται με δύο δεκαδικά ψηφία και οι ημερομηνίες ακολουθούν το `yyyy‑MM‑dd`, έχετε επιτυχώς **export excel to csv** με τη ζητούμενη μορφοποίηση.

## Ακραίες Περιπτώσεις & Συνηθισμένα Πιθανά Σφάλματα

- **Μεγάλα φύλλα εργασίας:** Η εξαγωγή ολόκληρου φύλλου μπορεί να καταναλώσει πολύ μνήμη. Προτιμήστε ένα συγκεκριμένο εύρος όποτε είναι δυνατόν.
- **Ειδικοί χαρακτήρες:** Το CSV χρησιμοποιεί κόμματα ως διαχωριστικά· αν τα δεδομένα σας περιέχουν κόμματα, τυλίξτε το πεδίο σε εισαγωγικά (`"value, with comma"`). Οι περισσότερες βιβλιοθήκες το διαχειρίζονται αυτόματα, αλλά ελέγξτε αν δείτε κατεστραμμένες γραμμές.
- **Κωδικοποίηση:** Το `Files.writeString` προεπιλογή είναι UTF‑8. Αν χρειάζεστε διαφορετικό charset (π.χ., Windows‑1252), περάστε ένα όρισμα `Charset`.
- **Κενά κελιά:** Μετατρέπονται σε κενές συμβολοσειρές στο CSV—δεν υπάρχει πρόβλημα εκτός αν βασίζεστε σε σταθερό αριθμό στηλών.

## Πλήρες, Έτοιμο‑για‑Εκτέλεση Παράδειγμα

Παρακάτω βρίσκεται η πλήρης κλάση Java που μπορείτε να αντιγράψετε, να επικολλήσετε και να τρέξετε. Αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή φακέλου στον υπολογιστή σας.

```java
import com.aspose.cells.*;
import java.nio.file.*;

public class ExcelToCsvExporter {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Configure export options
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);
        exportOptions.setNumberFormat("#,##0.00");
        exportOptions.setDateFormat("yyyy-MM-dd");

        // 2️⃣ Load the workbook (convert xlsx to csv later)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Export the desired range (export range to csv)
        String csvData = worksheet.getCells()
                                  .exportTableAsString("A1:D10", exportOptions);

        // 4️⃣ Write the CSV string to a file (write csv to file)
        Path outputPath = Paths.get("YOUR_DIRECTORY/output.txt");
        Files.writeString(outputPath, csvData);

        // 5️⃣ Simple verification message
        System.out.println("✅ CSV export complete! File saved to: " + outputPath);
    }
}
```

**Αναμενόμενη έξοδος στην κονσόλα**

```
✅ CSV export complete! File saved to: /path/to/YOUR_DIRECTORY/output.txt
```

Ανοίξτε το παραγόμενο `output.txt` και θα δείτε μια καθαρή, διαχωρισμένη με κόμμα προβολή του επιλεγμένου εύρους.

## Συμπέρασμα

Καλύψαμε **πώς να εξάγετε δεδομένα Excel** σε CSV με έναν καθαρό, επαναλαμβανόμενο τρόπο: ρυθμίστε τις επιλογές εξαγωγής, φορτώστε το βιβλίο εργασίας, εξάγετε ένα συγκεκριμένο εύρος και τέλος **write csv to file**. Αυτή η προσέγγιση σας δίνει πλήρη έλεγχο πάνω στις μορφές αριθμών και ημερομηνιών, καθιστώντας το παραγόμενο **export excel to csv** αρχείο έτοιμο για downstream συστήματα.

Στη συνέχεια, μπορείτε να εξερευνήσετε:

- Εξαγωγή πολλαπλών εύρων σε μία εκτέλεση (βρόχος πάνω σε ονομαστικά εύρη).
- Χρήση διαφορετικού διαχωριστικού (ερωτηματικό) για περιοχές που το προτιμούν.
- Ροή του CSV απευθείας σε HTTP response για λήψεις μέσω web.

Δοκιμάστε το, προσαρμόστε το εύρος, και αφήστε τη δημιουργία CSV να γίνει ένα αβίαστο κομμάτι του εργαλείου σας Java. Καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σειρά;

Οι παρακάτω οδηγοί καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Export Excel to CSV with Blank Rows Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)
- [Export Excel Csv Blank Rows Aspose Cells Net](/cells/german/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)
- [Export Excel Csv Blank Rows Aspose Cells Net](/cells/french/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}