---
category: general
date: 2026-11-25
description: Μάθετε πώς να εξάγετε το Excel σε PPTX με επεξεργάσιμα σχήματα. Αυτός
  ο οδηγός δείχνει επίσης πώς να ορίσετε την περιοχή εκτύπωσης και να μετατρέψετε
  το γράφημα του Excel για παρουσιάσεις.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel
- set print area
- how to convert xlsx
- set print area excel
- convert excel chart
language: el
lastmod: 2026-11-25
og_description: Πώς να εξάγετε το Excel σε PPTX με επεξεργάσιμα σχήματα χρησιμοποιώντας
  το Aspose.Cells, καθώς και συμβουλές για ορισμό περιοχής εκτύπωσης και μετατροπή
  γραφήματος Excel για παρουσιάσεις.
og_image_alt: Screenshot showing how to export Excel to PPTX with editable shapes
og_title: Πώς να εξάγετε το Excel σε PPTX με επεξεργάσιμα σχήματα
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to export Excel to PPTX with editable shapes. This guide
    also shows how to set print area and convert Excel chart for presentations.
  headline: How to export Excel to PPTX with editable shapes
  type: TechArticle
- description: Learn how to export Excel to PPTX with editable shapes. This guide
    also shows how to set print area and convert Excel chart for presentations.
  name: How to export Excel to PPTX with editable shapes
  steps:
  - name: '**Dependency** – Aspose.Cells provides the `ImageOrPrintOptions` class
      that can render worksheets as PPTX slides. Adding it via Maven ensures the library
      is on the classpath.'
    text: '**Dependency** – Aspose.Cells provides the `ImageOrPrintOptions` class
      that can render worksheets as PPTX slides. Adding it via Maven ensures the library
      is on the classpath.'
  - name: '**Imports** – Importing the right classes keeps the code clean and avoids
      fully‑qualified names.'
    text: '**Imports** – Importing the right classes keeps the code clean and avoids
      fully‑qualified names.'
  - name: '**Loading the workbook** – You must point to the exact file that contains
      the objects you want to export. The path can be absolute or relative to the
      project root.'
    text: '**Loading the workbook** – You must point to the exact file that contains
      the objects you want to export. The path can be absolute or relative to the
      project root.'
  - name: '**Export options** – Setting `setEditable(true)` is the key to **how to
      export Excel** so that the resulting PowerPoint shapes remain editable. Without
      this flag, text boxes become static images.'
    text: '**Export options** – Setting `setEditable(true)` is the key to **how to
      export Excel** so that the resulting PowerPoint shapes remain editable. Without
      this flag, text boxes become static images.'
  - name: '**Print area** – The `setPrintArea` call limits the export to the region
      you care about, which reduces file size and removes unwanted rows/columns. This
      directly addresses the **set print area excel** requirement.'
    text: '**Print area** – The `setPrintArea` call limits the export to the region
      you care about, which reduces file size and removes unwanted rows/columns. This
      directly addresses the **set print area excel** requirement.'
  - name: '**Saving** – The `SaveFormat.PPTX` constant tells Aspose.Cells to generate
      a PowerPoint file rather than an image or PDF.'
    text: '**Saving** – The `SaveFormat.PPTX` constant tells Aspose.Cells to generate
      a PowerPoint file rather than an image or PDF.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Πώς να εξάγετε το Excel σε PPTX με επεξεργάσιμα σχήματα
url: /el/java/excel-import-export/how-to-export-excel-to-pptx-with-editable-shapes/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εξάγετε το Excel σε PPTX με επεξεργάσιμα σχήματα

Αν χρειάζεστε να **how to export Excel** αρχεία σε PowerPoint διατηρώντας επεξεργάσιμα πλαίσια κειμένου και σχήματα, αυτός ο οδηγός σας καθοδηγεί στη διαδικασία. Θα μάθετε επίσης πώς να **set print area** για μια εστιασμένη διαφάνεια και πώς να **convert Excel chart** αντικείμενα ώστε να παραμένουν πλήρως επεξεργάσιμα μετά την εξαγωγή.

Η εξαγωγή Excel σε PPTX είναι συνηθισμένη όταν δημιουργείτε παρουσιάσεις από αναφορές με δεδομένα. Χρησιμοποιώντας το Aspose.Cells for Java αποφεύγετε την χειροκίνητη αντιγραφή‑επικόλληση, διατηρείτε τη μορφοποίηση αμετάβλητη και αποκτάτε προγραμματιστικό έλεγχο του αποτελέσματος.

## Τι θα μάθετε

* Φορτώστε ένα υπάρχον βιβλίο εργασίας XLSX που περιέχει πλαίσιο κειμένου ή διάγραμμα.  
* Διαμορφώστε τις επιλογές εξαγωγής ώστε το παραγόμενο αρχείο PPTX να περιέχει **editable shapes**.  
* **Set the print area** για να περιορίσετε την εξαγόμενη περιοχή στα κελιά που χρειάζεστε.  
* Αποθηκεύστε το φύλλο εργασίας ως αρχείο PPTX και επαληθεύστε ότι τα πλαίσια κειμένου και τα διαγράμματα μπορούν να επεξεργαστούν στο PowerPoint.  

**Προαπαιτούμενα**

* Εγκατεστημένο Java 17 ή νεότερο.  
* Maven ή Gradle για διαχείριση εξαρτήσεων.  
* Βασική κατανόηση βιβλίων εργασίας Excel και προγραμματισμού Java.

---

## Πώς να εξάγετε το Excel σε PPTX με επεξεργάσιμα σχήματα

Αυτή η ενότητα παρέχει τον βασικό κώδικα που εκτελεί την εξαγωγή. Το παράδειγμα χρησιμοποιεί Aspose.Cells 23.9 (την πιο πρόσφατη έκδοση τη στιγμή της συγγραφής) και δείχνει κάθε απαιτούμενο βήμα.

```java
// ------------------------------------------------------------
// 1. Add Aspose.Cells dependency (Maven example)
// ------------------------------------------------------------
/*
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
*/

// ------------------------------------------------------------
// 2. Import required classes
// ------------------------------------------------------------
import com.aspose.cells.*;

public class ExcelToPptxExporter {

    public static void main(String[] args) throws Exception {
        // --------------------------------------------------------
        // 3. Load the workbook that contains a text box or chart
        // --------------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/WithTextBox.xlsx");

        // --------------------------------------------------------
        // 4. Set up export options for PPTX and enable shape editing
        // --------------------------------------------------------
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setFormat(ImageFormat.PPTX);          // output format
        exportOptions.setExportType(ExportType.PPTX);      // explicit PPTX export
        exportOptions.setEditable(true);                   // makes text boxes/shapes editable

        // --------------------------------------------------------
        // 5. Define the print area to limit the exported range
        // --------------------------------------------------------
        // This is the **set print area** step. Adjust the range as needed.
        workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:H30");

        // --------------------------------------------------------
        // 6. Save the first worksheet as an editable PPTX file
        // --------------------------------------------------------
        workbook.save("YOUR_DIRECTORY/EditableShapes.pptx", SaveFormat.PPTX);

        System.out.println("Export completed: EditableShapes.pptx");
    }
}
```

### Γιατί κάθε γραμμή είναι σημαντική

1. **Dependency** – Το Aspose.Cells παρέχει την κλάση `ImageOrPrintOptions` που μπορεί να αποδίδει φύλλα εργασίας ως διαφάνειες PPTX. Η προσθήκη της μέσω Maven εξασφαλίζει ότι η βιβλιοθήκη βρίσκεται στο classpath.  
2. **Imports** – Η εισαγωγή των σωστών κλάσεων διατηρεί τον κώδικα καθαρό και αποφεύγει πλήρως προσδιορισμένα ονόματα.  
3. **Loading the workbook** – Πρέπει να δείξετε στο ακριβές αρχείο που περιέχει τα αντικείμενα που θέλετε να εξάγετε. Η διαδρομή μπορεί να είναι απόλυτη ή σχετική με τη ρίζα του έργου.  
4. **Export options** – Η ρύθμιση `setEditable(true)` είναι το κλειδί για **how to export Excel** ώστε τα παραγόμενα σχήματα PowerPoint να παραμένουν επεξεργάσιμα. Χωρίς αυτή τη σημαία, τα πλαίσια κειμένου γίνονται στατικές εικόνες.  
5. **Print area** – Η κλήση `setPrintArea` περιορίζει την εξαγωγή στην περιοχή που σας ενδιαφέρει, μειώνοντας το μέγεθος του αρχείου και αφαιρώντας ανεπιθύμητες γραμμές/στήλες. Αυτό ανταποκρίνεται άμεσα στην απαίτηση **set print area excel**.  
6. **Saving** – Η σταθερά `SaveFormat.PPTX` ενημερώνει το Aspose.Cells να δημιουργήσει αρχείο PowerPoint αντί για εικόνα ή PDF.

#### Αναμενόμενο αποτέλεσμα

Μετά την εκτέλεση του προγράμματος, ανοίξτε το `EditableShapes.pptx` στο PowerPoint. Θα πρέπει να δείτε μια διαφάνεια που αντικατοπτρίζει την επιλεγμένη περιοχή του Excel, και οποιαδήποτε πλαίσια κειμένου ή υπομνήματα διαγραμμάτων μπορούν να διπλο‑κλικάρετε και να επεξεργαστείτε όπως τα εγγενή αντικείμενα του PowerPoint.

---

## Ορισμός της περιοχής εκτύπωσης στο Excel

Όταν χρειάζεστε μόνο ένα υποσύνολο του φύλλου εργασίας, ο ορισμός μιας **print area** βελτιώνει τόσο την απόδοση όσο και την οπτική σαφήνεια.

```java
// Example: set print area to the first 10 rows and columns A‑J
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.getPageSetup().setPrintArea("A1:J10");
```

*Tip:* Εάν αργότερα αλλάξετε την περιοχή δεδομένων, καλέστε ξανά το `setPrintArea` πριν από την εξαγωγή. Η εξαγωγή σέβεται την πιο πρόσφατη ρύθμιση.

---

## Μετατροπή διαγράμματος XLSX σε επεξεργάσιμο διάγραμμα PowerPoint

Το Aspose.Cells αντιμετωπίζει τα διαγράμματα ως αντικείμενα σχεδίασης. Ενεργοποιώντας το `setEditable(true)`, το διάγραμμα μετατρέπεται σε εγγενές διάγραμμα PowerPoint που μπορεί να επεξεργαστεί (π.χ., αλλαγή σειρών, τίτλων αξόνων).

```java
// No extra code needed – the same exportOptions handle chart conversion.
// Just ensure the workbook contains a chart object.
```

Εάν χρειάζεστε να **how to convert xlsx** αρχεία που περιέχουν πολλαπλά διαγράμματα, επαναλάβετε την εξαγωγή για κάθε φύλλο εργασίας ή χρησιμοποιήστε `Workbook.save` με `SaveFormat.PPTX` μετά την προσαρμογή του ενεργού φύλλου.

---

## Πώς να μετατρέψετε το XLSX προγραμματιστικά (bonus)

Πέρα από το PPTX, ίσως θέλετε επίσης να μετατρέψετε το βιβλίο εργασίας σε άλλη μορφή όπως PDF ή PNG. Η ίδια κλάση `ImageOrPrintOptions` λειτουργεί για αυτούς τους στόχους:

```java
exportOptions.setFormat(ImageFormat.PDF);   // for PDF output
workbook.save("Converted.pdf", SaveFormat.PDF);
```

Αυτό δείχνει τη μεγαλύτερη δυνατότητα **how to convert xlsx** του Aspose.Cells.

---

## Συνηθισμένα προβλήματα και συμβουλές βέλτιστων πρακτικών

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| Τα σχήματα γίνονται εικόνες | `setEditable(false)` (default) | Call `exportOptions.setEditable(true)` |
| Η εξαγόμενη διαφάνεια είναι κενή | Η περιοχή εκτύπωσης δεν περιλαμβάνει δεδομένα | Επαληθεύστε τη συμβολοσειρά περιοχής που περνιέται στο `setPrintArea` |
| Το διάγραμμα χάνει μορφοποίηση | Χρήση παλιάς έκδοσης Aspose.Cells | Αναβαθμίστε στη νεότερη βιβλιοθήκη (≥ 23.9) |
| Μεγάλο μέγεθος αρχείου | Εξαγωγή ολόκληρου του φύλλου εργασίας | Περιορίστε την περιοχή εκτύπωσης ή κρύψτε τις αχρησιμοποίητες γραμμές/στήλες |

---

## Συμπέρασμα

Τώρα γνωρίζετε **how to export Excel** βιβλία εργασίας σε PPTX με πλήρως επεξεργάσιμα σχήματα και διαγράμματα, πώς να **set print area** για να εστιάσετε το αποτέλεσμα, και πώς να **convert Excel chart** αντικείμενα για απρόσκοπτη επεξεργασία παρουσίασης. Το πλήρες, εκτελέσιμο παράδειγμα Java παραπάνω μπορεί να ενσωματωθεί σε οποιοδήποτε έργο που χρησιμοποιεί ήδη το Aspose.Cells.

**Επόμενα βήματα**

* Εξερευνήστε τις επιλογές **convert excel chart** στο PowerPoint (π.χ., αλλαγή τύπου διαγράμματος).  
* Συνδυάστε αυτήν την εξαγωγή με αυτοματοποίηση **set print area excel** για να δημιουργήσετε πολλαπλές διαφάνειες από ένα μόνο βιβλίο εργασίας.  
* Δοκιμάστε την εξαγωγή σε άλλες μορφές (PDF, PNG) χρησιμοποιώντας το ίδιο πρότυπο `ImageOrPrintOptions`.

Μη διστάσετε να πειραματιστείτε με διαφορετικές περιοχές, πολλαπλά φύλλα εργασίας ή προσαρμοσμένες διατάξεις διαφάνειας. Καλό κώδικα!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε σε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να ορίσετε περιοχή εκτύπωσης excel και να εξάγετε σε PowerPoint](/cells/english/java/excel-import-export/how-to-set-print-area-excel-and-export-to-powerpoint/)
- [Μετατροπή Excel σε PowerPoint και ορισμός περιοχής εκτύπωσης](/cells/english/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/)
- [Ορισμός περιοχής εκτύπωσης στο Excel και εξαγωγή σε PowerPoint – Οδηγός βήμα‑βήμα](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}