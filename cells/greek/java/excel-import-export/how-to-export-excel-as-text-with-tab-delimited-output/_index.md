---
category: general
date: 2026-11-22
description: Μάθετε πώς να εξάγετε το Excel ως κείμενο και να δημιουργήσετε ένα αρχείο
  με διαχωρισμό κατά καρτέλα. Αυτός ο οδηγός δείχνει πώς να ορίσετε την παράθεση όλων
  των πεδίων και να αποθηκεύσετε το κείμενο του φύλλου εργασίας αποδοτικά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel as text
- quote all fields
- create tab-delimited file
- save spreadsheet text
- export spreadsheet tab-delimited
language: el
lastmod: 2026-11-22
og_description: Εξάγετε το Excel ως κείμενο και δημιουργήστε αρχείο διαχωρισμένο με
  καρτέλες. Ακολουθήστε αυτόν τον βήμα‑βήμα οδηγό για να βάλετε εισαγωγικά σε όλα
  τα πεδία και να αποθηκεύσετε το κείμενο του υπολογιστικού φύλλου με τη Java.
og_image_alt: Screenshot showing Java code that exports an Excel workbook as a tab‑delimited
  text file
og_title: Εξαγωγή Excel ως κείμενο – οδηγός αρχείου διαχωρισμένου με καρτέλες
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to export Excel as text and create a tab‑delimited file.
    This guide shows setting quote all fields and saving spreadsheet text efficiently.
  headline: How to export Excel as text with tab‑delimited output
  type: TechArticle
- description: Learn how to export Excel as text and create a tab‑delimited file.
    This guide shows setting quote all fields and saving spreadsheet text efficiently.
  name: How to export Excel as text with tab‑delimited output
  steps:
  - name: Prepare the workbook and sample data
    text: Creating a workbook gives you something to export. In a real project you
      would load an existing file with `new Workbook("input.xlsx")`; here we generate
      a tiny sheet so the example runs out‑of‑the‑box.
  - name: Configure export options – delimiter, quoting, and output mode
    text: The core of **export spreadsheet tab‑delimited** lies in `ExportTableOptions`.
      You set the delimiter to a tab (`'\t'`) and enable `setQuoteAllFields(true)`
      so every cell is wrapped in double quotes. This eliminates ambiguity when a
      cell itself contains a tab or newline.
  - name: Save the workbook as a tab‑delimited text file
    text: Now you actually **export excel as text**. The `save` method takes the target
      path and the `ExportOptions` you configured.
  type: HowTo
tags:
- export excel as text
- quote all fields
- tab-delimited file
- spreadsheet export
- Java
title: Πώς να εξάγετε το Excel ως κείμενο με διαχωρισμό κατά καρτέλα
url: /el/java/excel-import-export/how-to-export-excel-as-text-with-tab-delimited-output/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εξάγετε το Excel ως κείμενο με έξοδο διαχωρισμένη με tabs

Αν χρειάζεστε **να εξάγετε το Excel ως κείμενο**, αυτό το σεμινάριο σας καθοδηγεί μέσα από τη διαδικασία δημιουργίας ενός αρχείου διαχωρισμένου με tabs από ένα βιβλίο εργασίας. Είτε χτίζετε μια γραμμή μεταφοράς δεδομένων είτε χρειάζεστε μια γρήγορη εξαγωγή τύπου CSV για επεξεργασία σε επόμενο στάδιο, τα παρακάτω βήματα σας επιτρέπουν να **αποθηκεύσετε το κείμενο του φύλλου** με πλήρη έλεγχο των διαχωριστών και των εισαγωγικών.

Η εξαγωγή δεδομένων φύλλου εργασίας ως απλό κείμενο είναι συχνά πιο φορητή από τη διατήρηση της εγγενής μορφής `.xlsx`. Σε αυτόν τον οδηγό θα μάθετε επίσης πώς να **εγγυημένα να βάλετε εισαγωγικά σε όλα τα πεδία**, κάτι που εξασφαλίζει ότι οι τιμές που περιέχουν tabs, κόμματα ή αλλαγές γραμμής είναι ασφαλώς περιτυλιγμένες.

## Τι θα χρειαστείτε

* Εγκατεστημένο Java 17 ή νεότερο.
* Η βιβλιοθήκη Aspose.Cells for Java (ο κώδικας χρησιμοποιεί `ExportOptions` και `ExportTableOptions` από αυτή τη βιβλιοθήκη). Μπορείτε να την προσθέσετε μέσω Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

* Ένα IDE ή έναν απλό επεξεργαστή κειμένου για να μεταγλωττίσετε και να εκτελέσετε το πρόγραμμα Java.

## Εξαγωγή Excel ως κείμενο – βήμα‑βήμα

Οι παρακάτω ενότητες χωρίζουν την εργασία σε τρία λογικά βήματα. Κάθε βήμα εξηγεί **γιατί** είναι σημαντικό, όχι μόνο **τι** πρέπει να πληκτρολογήσετε.

### Βήμα 1: Προετοιμασία του βιβλίου εργασίας και των δείγματων δεδομένων

Η δημιουργία ενός βιβλίου εργασίας σας παρέχει κάτι για εξαγωγή. Σε ένα πραγματικό έργο θα φορτώνατε ένα υπάρχον αρχείο με `new Workbook("input.xlsx")`; εδώ δημιουργούμε ένα μικρό φύλλο ώστε το παράδειγμα να λειτουργεί αμέσως.

```java
import com.aspose.cells.*;

public class ExportExcelAsText {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook or create a new one
        Workbook wb = new Workbook();
        Worksheet sheet = wb.getWorksheets().get(0);

        // Populate sample data – this will be part of the exported text
        sheet.getCells().get("A1").setValue("Name");
        sheet.getCells().get("B1").setValue("Age");
        sheet.getCells().get("A2").setValue("Alice");
        sheet.getCells().get("B2").setValue(30);
        sheet.getCells().get("A3").setValue("Bob, Jr."); // contains a comma
        sheet.getCells().get("B3").setValue(25);
```

*Γιατί αυτό το βήμα;*  
Ένα βιβλίο εργασίας είναι το αντικείμενο προέλευσης για οποιαδήποτε λειτουργία εξαγωγής. Προσθέτοντας μερικές γραμμές μπορείτε να επαληθεύσετε ότι η επιλογή **quote all fields** προστατεύει πραγματικά τα κόμματα και άλλους ειδικούς χαρακτήρες.

### Βήμα 2: Διαμόρφωση επιλογών εξαγωγής – διαχωριστής, εισαγωγικά και τρόπος εξόδου

Ο πυρήνας της **export spreadsheet tab‑delimited** βρίσκεται στο `ExportTableOptions`. Ορίζετε το διαχωριστικό σε tab (`'\t'`) και ενεργοποιείτε το `setQuoteAllFields(true)` ώστε κάθε κελί να περιβάλλεται από διπλά εισαγωγικά. Αυτό εξαλείφει την ασάφεια όταν ένα κελί περιέχει ίδιο το tab ή αλλαγή γραμμής.

```java
        // Step 2: Create table export options and configure delimiter and quoting
        ExportTableOptions tableExportOptions = new ExportTableOptions();
        tableExportOptions.setDelimiter('\t');            // Use a tab as the field separator
        tableExportOptions.setQuoteAllFields(true);      // Quote every field for safety

        // Create overall export options and attach the table options
        ExportOptions exportOptions = new ExportOptions();
        exportOptions.setExportTableOptions(tableExportOptions);
        exportOptions.setExportAsString(true);            // Produce plain‑text output
```

*Γιατί αυτό το βήμα;*  
- **Delimiter** καθορίζει πώς χωρίζονται οι στήλες. Ένα tab (`\t`) δημιουργεί ένα **tab‑delimited file** που αποδέχονται πολλά εργαλεία επεξεργασίας δεδομένων.  
- **Quote all fields** εγγυάται ότι ακόμη και αν ένα κελί περιέχει διαχωριστικό, το παραγόμενο κείμενο παραμένει αναγνώσιμο.  
- Η ρύθμιση `ExportAsString` λέει στο Aspose.Cells να δημιουργήσει μια συμβολοσειρά αντί για ένα δυαδικό βιβλίο εργασίας, κάτι που είναι ακριβώς αυτό που χρειάζεστε για **save spreadsheet text**.

### Βήμα 3: Αποθήκευση του βιβλίου εργασίας ως αρχείο κειμένου διαχωρισμένο με tabs

Τώρα πραγματικά **εξάγετε το excel ως κείμενο**. Η μέθοδος `save` λαμβάνει τη διαδρομή προορισμού και τις `ExportOptions` που διαμορφώσατε.

```java
        // Step 3: Save the workbook as a tab‑delimited text file
        wb.save("output/table.txt", exportOptions);
    }
}
```

Όταν το πρόγραμμα ολοκληρωθεί, θα βρείτε το `output/table.txt` που περιέχει:

```
"Name"	"Age"
"Alice"	"30"
"Bob, Jr."	"25"
```

*Γιατί αυτό το βήμα;*  
Η κλήση `save` γράφει το **tab‑delimited file** στο δίσκο, αποθηκεύοντας ουσιαστικά **spreadsheet text** σε μορφή που μπορεί να ανοίξει το Excel, το Notepad ή οποιοδήποτε εργαλείο εισαγωγής δεδομένων που καταλαβαίνει tabs.

## Πώς να βάλετε εισαγωγικά σε όλα τα πεδία κατά την εξαγωγή Excel ως κείμενο

Αν παραλείψετε το `setQuoteAllFields(true)`, τα κελιά που περιέχουν tabs, κόμματα ή αλλαγές γραμμής θα διασπάσουν τη δομή του αρχείου εξόδου. Για παράδειγμα, η γραμμή `Bob, Jr.` θα χωριστεί σε δύο στήλες, καταστρέφοντας το σύνολο δεδομένων. Πάντα ενεργοποιήστε τα εισαγωγικά όταν:

* Τα δεδομένα προέλευσης μπορεί να περιέχουν κόμματα, tabs ή νέες γραμμές.  
* Οι επόμενοι αναλυτές αναμένουν αρχεία CSV/TSV με εισαγωγικά.  
* Χρειάζεστε μια καθοριστική εξαγωγή ανεξάρτητα από το περιεχόμενο του κελιού.

## Δημιουργία αρχείου διαχωρισμένου με tabs χωρίς Aspose.Cells (προαιρετικό)

Αν προτιμάτε μια καθαρή λύση Java χωρίς βιβλιοθήκες τρίτων, μπορείτε να επαναλάβετε τις γραμμές και να τις γράψετε χειροκίνητα:

```java
try (PrintWriter pw = new PrintWriter(new FileWriter("output/manual.txt"))) {
    for (int r = 0; r < sheet.getCells().getMaxDataRow() + 1; r++) {
        List<String> rowValues = new ArrayList<>();
        for (int c = 0; c < sheet.getCells().getMaxDataColumn() + 1; c++) {
            String value = sheet.getCells().get(r, c).getStringValue();
            // Quote all fields manually
            rowValues.add('"' + value.replace("\"", "\"\"") + '"');
        }
        pw.println(String.join("\t", rowValues));
    }
}
```

Αυτό το απόσπασμα δείχνει την ίδια λογική **export spreadsheet tab‑delimited**: διαχωριστικό tab, εισαγωγικά σε κάθε πεδίο και εγγραφή του αποτελέσματος ως απλό κείμενο. Ωστόσο, η χρήση του Aspose.Cells απλοποιεί τη διαχείριση μεγάλων βιβλίων εργασίας, διατηρεί τη μορφοποίηση και μειώνει τον κώδικα επαναλήψεων.

## Συνηθισμένα προβλήματα και επαγγελματικές συμβουλές

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Λείπουν tabs στην έξοδο** | Ο διαχωριστής έμεινε στην προεπιλεγμένη τιμή κόμμα. | Καλέστε ρητά `setDelimiter('\t')`. |
| **Κόμματα χωρίς εισαγωγικά σπάζουν τις στήλες** | `quoteAllFields` δεν είναι ενεργοποιημένο. | Χρησιμοποιήστε `setQuoteAllFields(true)` ή προσθέστε εισαγωγικά χειροκίνητα. |
| **Το αρχείο δεν δημιουργείται** | Ο φάκελος εξόδου δεν υπάρχει. | Βεβαιωθείτε ότι υπάρχει ο φάκελος `output/` ή χρησιμοποιήστε `Files.createDirectories`. |
| **Προβλήματα κωδικοποίησης** | Η προεπιλεγμένη κωδικοποίηση πλατφόρμας μπορεί να αλλοιώσει χαρακτήρες εκτός ASCII. | Προσθέστε `ExportOptions.setEncoding(Encoding.getUTF8())` αν χρειάζεται. |

## Δοκιμή του αποτελέσματος

Μετά την εκτέλεση του προγράμματος:

1. Ανοίξτε το `output/table.txt` σε έναν επεξεργαστή απλού κειμένου. Θα πρέπει να δείτε κάθε τιμή να είναι περιτυλιγμένη σε διπλά εισαγωγικά και τις στήλες να χωρίζονται από έναν μόνο χαρακτήρα tab.  
2. Εισάγετε το αρχείο στο Excel (`Data → From Text/CSV`). Επιλέξτε **Tab** ως διαχωριστικό· το Excel θα τοποθετήσει σωστά κάθε τιμή με εισαγωγικά στο δικό της κελί.  
3. Επαληθεύστε ότι οι ειδικοί χαρακτήρες (κόμματα, αλλαγές γραμμής

## Τι θα πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω σεμινάρια καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [πώς να εξάγετε το excel – Οδηγός κειμένου διαχωρισμένου με Tab](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-tab-delimited-text-guide/)
- [Αποθήκευση Excel ως αρχείο κειμένου με προσαρμοσμένο διαχωριστικό χρησιμοποιώντας Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Πώς να αποθηκεύσετε το Excel ως κείμενο με Aspose.Cells – οδηγός βήμα‑βήμα](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-text-with-aspose-cells-step-by-step-gui/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}