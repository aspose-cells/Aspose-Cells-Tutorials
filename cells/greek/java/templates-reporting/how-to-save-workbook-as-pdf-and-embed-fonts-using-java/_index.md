---
category: general
date: 2026-11-22
description: Αποθήκευση βιβλίου εργασίας ως PDF με ενσωματωμένες γραμματοσειρές σε
  Java. Μάθετε πώς να ενσωματώνετε γραμματοσειρές σε PDF κατά τη μετατροπή ενός βιβλίου
  εργασίας Excel σε PDF σε μόλις τρία βήματα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save workbook as pdf
- how to embed fonts in pdf
- convert excel workbook to pdf
- embed fonts when exporting pdf
- how to save workbook as pdf
language: el
lastmod: 2026-11-22
og_description: Αποθήκευση βιβλίου εργασίας ως PDF με ενσωματωμένες γραμματοσειρές
  σε Java. Αυτός ο οδηγός δείχνει πώς να ενσωματώσετε γραμματοσειρές σε PDF κατά τη
  μετατροπή ενός βιβλίου εργασίας Excel σε PDF, εξασφαλίζοντας αξιόπιστη απόδοση του
  εγγράφου.
og_image_alt: Screenshot of Java code that saves an Excel workbook as a PDF with embedded
  fonts
og_title: Αποθήκευση βιβλίου εργασίας ως PDF με ενσωματωμένες γραμματοσειρές – Οδηγός
  Java βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Save workbook as PDF with embedded fonts in Java. Learn how to embed
    fonts in PDF while converting an Excel workbook to PDF in just three steps.
  headline: How to save workbook as PDF and embed fonts using Java
  type: TechArticle
tags:
- Java
- Excel
- PDF
- Aspose.Cells
- Export
title: Πώς να αποθηκεύσετε το βιβλίο εργασίας ως PDF και να ενσωματώσετε τις γραμματοσειρές
  χρησιμοποιώντας Java
url: /el/java/templates-reporting/how-to-save-workbook-as-pdf-and-embed-fonts-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αποθηκεύσετε ένα βιβλίο εργασίας ως PDF και να ενσωματώσετε γραμματοσειρές χρησιμοποιώντας Java

Αν χρειάζεστε **αποθήκευση βιβλίου εργασίας ως PDF** και θέλετε να εγγυηθείτε ότι το παραγόμενο αρχείο εμφανίζει τις ίδιες γραμματοσειρές σε οποιαδήποτε συσκευή, αυτό το tutorial σας δείχνει ακριβώς πώς. Η ενσωμάτωση γραμματοσειρών αποτρέπει προβλήματα ελλιπών γλυφών όταν το PDF ανοίγει σε σύστημα που δεν έχει εγκατεστημένες τις αρχικές γραμματοσειρές. Στον οδηγό αυτό θα μάθετε επίσης **πώς να ενσωματώσετε γραμματοσειρές σε PDF** ενώ **μετατρέπετε ένα Excel workbook σε PDF** με μόλις τρεις γραμμές κώδικα.

Θα περάσετε από το πλήρες, εκτελέσιμο παράδειγμα, θα κατανοήσετε γιατί κάθε ρύθμιση είναι σημαντική και θα δείτε πώς να αντιμετωπίζετε κοινές περιπτώσεις όπως προσαρμοσμένες γραμματοσειρές και μεγάλα βιβλία εργασίας. Δεν απαιτείται εξωτερική τεκμηρίωση — όλα όσα χρειάζεστε είναι εδώ.

## Τι θα πετύχετε

* Μετατροπή ενός Excel workbook (`Workbook` object) σε αρχείο PDF.  
* Ενσωμάτωση των τυπικών γραμματοσειρών TrueType ώστε το PDF να αποδίδει σωστά παντού.  
* Λήψη μιας έτοιμης κλάσης Java που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Maven ή Gradle.

**Προαπαιτούμενα**

* Java 17 ή νεότερη.  
* Aspose.Cells for Java (ή μια παρόμοια βιβλιοθήκη που παρέχει `PdfSaveOptions`).  
* Βασικές γνώσεις Java και διαχείρισης εξαρτήσεων με Maven/Gradle.

---

## Βήμα 1: Ρύθμιση του έργου και προσθήκη της απαιτούμενης εξάρτησης

Πρώτα, συμπεριλάβετε το Aspose.Cells στο αρχείο κατασκευής σας. Η βιβλιοθήκη παρέχει `Workbook`, `PdfSaveOptions` και τη μέθοδο `setEmbedStandardFonts` που θα χρησιμοποιηθεί αργότερα.

```xml
<!-- Maven pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
    <classifier>jdk17</classifier>
</dependency>
```

Αν προτιμάτε Gradle:

```groovy
implementation 'com.aspose:aspose-cells:24.9:jdk17'
```

> **Pro tip:** Επιλέξτε πάντα την πιο πρόσφατη έκδοση για να επωφεληθείτε από διορθώσεις σφαλμάτων και βελτιωμένη διαχείριση γραμματοσειρών.

## Βήμα 2: Δημιουργία δείγματος workbook (προαιρετικό αλλά χρήσιμο για δοκιμές)

Παρακάτω υπάρχει ένα ελάχιστο πρόγραμμα που δημιουργεί ένα workbook με μερικά κελιά. Μπορείτε να αντικαταστήσετε αυτήν την ενότητα με τη δική σας λογική φόρτωσης workbook (π.χ., `new Workbook("input.xlsx")`).

```java
import com.aspose.cells.*;

public class ExcelToPdfDemo {

    public static void main(String[] args) throws Exception {
        // Create a new workbook with one worksheet
        Workbook wb = new Workbook();
        Worksheet sheet = wb.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Populate some data to illustrate formatting
        cells.get("A1").putValue("Product");
        cells.get("B1").putValue("Price");
        cells.get("A2").putValue("Coffee");
        cells.get("B2").putValue(3.99);
        cells.get("A3").putValue("Tea");
        cells.get("B3").putValue(2.49);

        // Apply a simple style so the PDF shows bold headers
        Style headerStyle = wb.createStyle();
        Font headerFont = headerStyle.getFont();
        headerFont.setBold(true);
        cells.get("A1").setStyle(headerStyle);
        cells.get("B1").setStyle(headerStyle);

        // -------------------------------------------------
        // Save workbook as PDF with embedded fonts
        // -------------------------------------------------
        saveWorkbookAsPdfWithEmbeddedFonts(wb, "output/WorkbookWithFonts.pdf");
    }

    /**
     * Saves the given workbook as a PDF file while embedding standard fonts.
     *
     * @param workbook   The Aspose.Cells workbook to export.
     * @param outputPath Full path where the PDF should be written.
     */
    private static void saveWorkbookAsPdfWithEmbeddedFonts(Workbook workbook, String outputPath) throws Exception {
        // Step 1: Create PDF save options
        PdfSaveOptions pdfOptions = new PdfSaveOptions();

        // Step 2: Enable embedding of standard fonts in the PDF
        // This ensures the PDF displays correctly on machines without the original fonts.
        pdfOptions.setEmbedStandardFonts(true);

        // Step 3: Save the workbook as a PDF file
        workbook.save(outputPath, pdfOptions);
        System.out.println("PDF saved to " + outputPath);
    }
}
```

### Γιατί ενσωματώνουμε γραμματοσειρές

Όταν **ενσωματώνετε γραμματοσειρές κατά την εξαγωγή PDF**, τα δεδομένα της γραμματοσειράς γίνονται μέρος του αρχείου PDF. Χωρίς ενσωμάτωση, ο προβολέας αντικαθιστά τις ελλιπείς γραμματοσειρές, κάτι που μπορεί να αλλάξει τη διάταξη, τις αλλαγές γραμμής ή ακόμη και να προκαλέσει μη αναγνώσιμους χαρακτήρες. Η ενσωμάτωση είναι ιδιαίτερα σημαντική για εταιρικές αναφορές, τιμολόγια ή οποιοδήποτε έγγραφο που πρέπει να φαίνεται ακριβώς το ίδιο σε όλες τις πλατφόρμες.

## Βήμα 3: Εκτέλεση του προγράμματος και επαλήθευση του αποτελέσματος

Τρέξτε τη μέθοδο `main` από το IDE σας ή από τη γραμμή εντολών:

```bash
mvn compile exec:java -Dexec.mainClass=ExcelToPdfDemo
```

Μετά την εκτέλεση θα πρέπει να δείτε:

```
PDF saved to output/WorkbookWithFonts.pdf
```

Ανοίξτε το `WorkbookWithFonts.pdf` σε οποιονδήποτε αναγνώστη PDF. Θα παρατηρήσετε:

* Η γραμμή κεφαλίδας εμφανίζεται έντονη, ακριβώς όπως μορφοποιήθηκε στο Excel.  
* Όλο το κείμενο χρησιμοποιεί τις ενσωματωμένες τυπικές γραμματοσειρές (π.χ., Arial, Times New Roman).  
* Δεν εμφανίζονται προειδοποιήσεις ελλιπών γλυφών, ακόμη και σε μηχάνημα που δεν διαθέτει αυτές τις γραμματοσειρές.

### Αναμενόμενη λήψη στιγμιότυπου (εννοιολογική)

> *Image placeholder: a PDF viewer window showing the exported table with proper fonts.*

*(Alt text for SEO: "PDF viewer displaying a table exported from Excel with embedded fonts")*

## Πώς να ενσωματώσετε γραμματοσειρές σε PDF για προσαρμοσμένες γραμματοσειρές

Το παραπάνω παράδειγμα ενσωματώνει **τυπικές γραμματοσειρές** αυτόματα. Αν το workbook σας χρησιμοποιεί μια προσαρμοσμένη γραμματοσειρά TrueType ή OpenType, πρέπει να πείτε στο Aspose.Cells να τις ενσωματώσει επίσης:

```java
pdfOptions.setEmbedAllFonts(true);          // Embeds every font used in the workbook
pdfOptions.setCustomFontsFolder("fonts/"); // Folder that contains your custom .ttf/.otf files
```

Τοποθετήστε τα αρχεία των προσαρμοσμένων γραμματοσειρών στον φάκελο `fonts/` σχετικά με τη ρίζα του έργου σας. Αυτή η προσέγγιση ικανοποιεί την απαίτηση **embed fonts when exporting pdf** για μη‑τυπικές γραμματοσειρές.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| Το PDF εμφανίζει την προεπιλεγμένη γραμματοσειρά του συστήματος αντί της γραμματοσειράς που ορίσατε στο Excel | `setEmbedStandardFonts` ενσωματώνει μόνο τις 14 βασικές γραμματοσειρές PDF. Οι προσαρμοσμένες γραμματοσειρές αγνοούνται εκτός αν κληθεί `setEmbedAllFonts(true)`. | Ενεργοποιήστε `setEmbedAllFonts` και υποδείξτε το φάκελο που περιέχει τις προσαρμοσμένες γραμματοσειρές. |
| Μεγάλα workbooks παράγουν τεράστια PDFs | Κάθε γλύφο κάθε ενσωματωμένης γραμματοσειράς προσθέτει στο μέγεθος του αρχείου. | Χρησιμοποιήστε `pdfOptions.setCompressImages(true)` και εξετάστε την υπο-επιλογή γραμματοσειρών με `pdfOptions.setSubsetFonts(true)`. |
| `FileNotFoundException` κατά την αποθήκευση | Ο φάκελος προορισμού δεν υπάρχει. | Βεβαιωθείτε ότι ο φάκελος υπάρχει (`new File("output").mkdirs();`) πριν καλέσετε `save`. |
| Οι γραμματοσειρές δεν εμφανίζονται σε παλαιούς προβολείς PDF | Κάποιοι προβολείς αγνοούν ενσωματωμένες γραμματοσειρές αν η έκδοση PDF είναι πολύ χαμηλή. | Ορίστε `pdfOptions.setCompliance(PdfCompliance.PDF_A_1B);` για να επιβάλετε ένα σύγχρονο πρότυπο PDF/A. |

## Πώς να αποθηκεύσετε workbook ως PDF (εναλλακτικά APIs)

Αν προτιμάτε μια εντολή μίας γραμμής χωρίς ρητές `PdfSaveOptions`, το Aspose.Cells παρέχει επίσης μια βολική υπερφόρτωση:

```java
workbook.save("output/SimpleExport.pdf", SaveFormat.PDF);
```

Ωστόσο, **αυτό δεν ενσωματώνει γραμματοσειρές** εκτός αν διαμορφώσετε τις προεπιλεγμένες επιλογές παγκοσμίως, έτσι η τρι-βήμα προσέγγιση που παρουσιάστηκε νωρίτερα παραμένει η προτεινόμενη όταν χρειάζεστε αξιόπιστη ενσωμάτωση γραμματοσειρών.

## Ανακεφαλαίωση της πλήρους λύσης

```java
import com.aspose.cells.*;

public class SaveWorkbookAsPdf {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("input/Report.xlsx"); // Or create programmatically

        PdfSaveOptions options = new PdfSaveOptions();
        options.setEmbedStandardFonts(true);   // Primary requirement: embed fonts
        // options.setEmbedAllFonts(true);     // Uncomment for custom fonts
        // options.setCustomFontsFolder("fonts/");

        wb.save("output/Report.pdf", options);
        System.out.println("Workbook saved as PDF with embedded fonts.");
    }
}
```

Η εκτέλεση αυτής της κλάσης παράγει ένα PDF που **save workbook as pdf** διατηρώντας την ακριβή οπτική εμφάνιση του αρχικού αρχείου Excel.

---

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **save workbook as PDF** και να εγγυηθείτε ότι οι γραμματοσειρές ενσωματώνονται, εξαλείφοντας τις εκπλήξεις στην απόδοση σε οποιαδήποτε συσκευή. Με τη διαμόρφωση του `PdfSaveOptions` — ειδικά του `setEmbedStandardFonts(true)` — ικανοποιείτε την απαίτηση **how to embed fonts in pdf** και δημιουργείτε ένα φορητό, επαγγελματικό έγγραφο.  

Από εδώ μπορείτε να εξερευνήσετε:

* **Convert Excel workbook to PDF** σε λειτουργία παρτίδας για μεγάλα σύνολα δεδομένων.  
* Χρήση του **embed fonts when exporting pdf** μαζί με συμπίεση εικόνων για μικρότερα αρχεία.  
* Πειραματισμό με συμμόρφωση PDF/A για αρχεία αρχείου υψηλής ποιότητας.

Αισθανθείτε ελεύθεροι να προσαρμόσετε τον κώδικα στα δικά σας έργα, να αντικαταστήσετε τα δείγμα δεδομένων με πραγματικά φύλλα εργασίας και να μοιραστείτε τα αποτελέσματά σας. Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικά θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Embed Fonts in PDF – Save Workbook as PDF in C#](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-in-pdf-save-workbook-as-pdf-in-c/)
- [how to embed fonts when converting Excel to PDF with Java](/cells/english/java/integration-interoperability/how-to-embed-fonts-when-converting-excel-to-pdf-with-java/)
- [How to Export PDF from Excel – Complete Guide to Save Workbook as PDF](/cells/english/net/conversion-to-pdf/how-to-export-pdf-from-excel-complete-guide-to-save-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}