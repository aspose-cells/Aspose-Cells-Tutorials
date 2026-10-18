---
category: general
date: 2026-08-14
description: Ενσωμάτωση γραμματοσειρών σε SVG κατά την εξαγωγή του Excel σε SVG χρησιμοποιώντας
  το Aspose.Cells. Μάθετε πώς να ορίζετε την περιοχή εκτύπωσης, να ρυθμίζετε τις επιλογές
  εκτύπωσης και να χρησιμοποιείτε τη λειτουργία WRAPCOLS.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in svg
- export excel to svg
- set print area
- set print options
- use wrapcols function
language: el
lastmod: 2026-08-14
og_description: Ενσωμάτωση γραμματοσειρών σε SVG κατά την εξαγωγή του Excel σε SVG
  με το Aspose.Cells. Αυτός ο οδηγός δείχνει πώς να ορίσετε την περιοχή εκτύπωσης,
  να διαμορφώσετε τις επιλογές εκτύπωσης και να εφαρμόσετε τη λειτουργία WRAPCOLS.
og_image_alt: Screenshot of Java code exporting an Excel sheet to SVG with embedded
  fonts
og_title: Ενσωμάτωση γραμματοσειρών σε SVG κατά την εξαγωγή του Excel σε SVG – βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  headline: Embed fonts in SVG while exporting Excel to SVG
  type: TechArticle
- description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  name: Embed fonts in SVG while exporting Excel to SVG
  steps:
  - name: Run the program.
    text: Run the program.
  - name: Open `output.svg` in a web browser.
    text: Open `output.svg` in a web browser.
  - name: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
    text: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
  - name: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
    text: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
title: Ενσωμάτωση γραμματοσειρών σε SVG κατά την εξαγωγή του Excel σε SVG
url: /el/java/excel-import-export/embed-fonts-in-svg-while-exporting-excel-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ενσωμάτωση γραμματοσειρών σε SVG κατά την εξαγωγή Excel σε SVG

Αν χρειάζεστε **ενσωμάτωση γραμματοσειρών σε SVG κατά την εξαγωγή Excel σε SVG**, αυτό το tutorial σας δείχνει ακριβώς πώς να το κάνετε με το Aspose.Cells for Java. Θα καλύψουμε επίσης πώς να **ορίσετε περιοχή εκτύπωσης**, **ορίσετε επιλογές εκτύπωσης**, και **να χρησιμοποιήσετε τη συνάρτηση WRAPCOLS** για μορφοποίηση δεδομένων χωρίς να χάσετε τη διάταξη.

Θα περάσετε από ένα πλήρες, εκτελέσιμο παράδειγμα που φορτώνει ένα υπάρχον βιβλίο εργασίας, εφαρμόζει τον τύπο `WRAPCOLS`, ρυθμίζει τις επιλογές εικόνας‑σχετικές με SVG, ορίζει την περιοχή εκτύπωσης και, τέλος, αποθηκεύει το αρχείο ως SVG με ενσωματωμένες γραμματοσειρές. Δεν απαιτείται εξωτερική τεκμηρίωση — απλώς αντιγράψτε τον κώδικα, τρέξτε τον και ελέγξτε το παραγόμενο SVG.

## Ενσωμάτωση γραμματοσειρών σε SVG – ρύθμιση ImageOrPrintOptions

Η ενσωμάτωση γραμματοσειρών εξασφαλίζει ότι το SVG αποδίδει ακριβώς όπως εμφανίζεται στο Excel, ακόμη και σε μηχανές που δεν έχουν εγκατεστημένες τις αρχικές γραμματοσειρές.

```java
// Create ImageOrPrintOptions for SVG output
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);          // Target format
imgOptions.setEmbedFonts(true);                     // <-- embed fonts in SVG
imgOptions.setFontVariationSelectors(true);        // Preserve variation selectors
```

*Γιατί είναι σημαντικό*: Όταν είναι ενεργοποιημένο το `setEmbedFonts(true)`, το Aspose.Cells γράφει τα δεδομένα της γραμματοσειράς απευθείας στην ενότητα `<defs>` του SVG. Το αποτέλεσμα είναι ένα αυτόνομο αρχείο που φαίνεται ταυτόσημο σε όλα τα προγράμματα περιήγησης και πλατφόρμες.

## Εξαγωγή Excel σε SVG – πλήρης ροή εργασίας

Τα παρακάτω βήματα απεικονίζουν τη διαδικασία από το φόρτωμα του βιβλίου εργασίας μέχρι την αποθήκευση του αρχείου SVG.

```java
// Step 1: Load a workbook and access the first worksheet
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = workbook.getWorksheets().get(0);

// Step 2: Apply the WRAPCOLS formula to cell A1
Cell cell = ws.getCells().get("A1");
cell.setFormula("=WRAPCOLS(A2:A10,3)");

// Step 3: Configure image options (see previous section)
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);
imgOptions.setEmbedFonts(true);
imgOptions.setFontVariationSelectors(true);

// Step 4: Define the print area and assign the image options
ws.getPageSetup().setPrintArea("A1:H30");           // <-- set print area
ws.getPageSetup().setPrintOptions(imgOptions);     // <-- set print options

// Step 5: Save the worksheet as an SVG file
ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);
```

**Αναμενόμενο αποτέλεσμα**: Το `output.svg` εμφανίζεται στο `YOUR_DIRECTORY`. Ανοίγοντάς το σε έναν περιηγητή, βλέπετε το φύλλο εργασίας με όλες τις γραμματοσειρές ενσωματωμένες, τα δεδομένα τυλιγμένα σε τρεις στήλες (ευχαριστώντας το `WRAPCOLS`), και μόνο τα κελιά εντός του `A1:H30` αποδίδονται.

## Ορισμός περιοχής εκτύπωσης για το φύλλο εργασίας

Ο καθορισμός περιοχής εκτύπωσης περιορίζει το εξαγόμενο SVG σε ένα συγκεκριμένο εύρος, μειώνοντας το μέγεθος του αρχείου και εστιάζοντας τον θεατή στα σχετικά δεδομένα.

```java
// Define a rectangular region that will be exported
ws.getPageSetup().setPrintArea("A1:H30");   // you can change the range as needed
```

*Συμβουλή*: Το εύρος ακολουθεί τη σημειογραφία A1 του Excel. Αν χρειάζεστε δυναμικό εύρος, μπορείτε να το υπολογίσετε προγραμματιστικά με `ws.getCells().getMaxDisplayRange()`.

## Ορισμός επιλογών εκτύπωσης για έξοδο SVG

Οι επιλογές εκτύπωσης ελέγχουν πώς το Aspose.Cells μετατρέπει το φύλλο εργασίας σε εικόνα. Εκτός από την ενσωμάτωση γραμματοσειρών, μπορείτε να ρυθμίσετε την ανάλυση, την κλιμάκωση και τη διάταξη σελίδας.

```java
// Assign the previously configured ImageOrPrintOptions
ws.getPageSetup().setPrintOptions(imgOptions);
```

*Γιατί πρέπει να ορίσετε επιλογές εκτύπωσης*: Χωρίς ρητές επιλογές, το Aspose.Cells χρησιμοποιεί προεπιλογές που μπορεί να παραλείψουν την ενσωμάτωση γραμματοσειρών ή να εφαρμόσουν ανεπιθύμητο συντελεστή κλιμάκωσης, οδηγώντας σε θολά ή λανθασμένα μορφοποιημένα SVG.

## Χρήση της συνάρτησης WRAPCOLS για τυλίξιμο δεδομένων στήλης

Το `WRAPCOLS` είναι ένας τύπος του Excel που διανέμει μια κάθετη περιοχή σε καθορισμένο αριθμό στηλών. Είναι χρήσιμο όταν θέλετε να εμφανίσετε μια μακριά λίστα σε ένα συμπαγές πλέγμα.

```java
// Insert the WRAPCOLS formula into cell A1
cell.setFormula("=WRAPCOLS(A2:A10,3)");
```

Όταν αποθηκευτεί το βιβλίο εργασίας, το Aspose.Cells αξιολογεί τον τύπο, παράγοντας μια διάταξη τριών στηλών μέσα στην ορισμένη περιοχή εκτύπωσης. Αυτή η τεχνική λειτουργεί για οποιοδήποτε μέγεθος περιοχής — απλώς προσαρμόστε το δεύτερο όρισμα στον επιθυμητό αριθμό στηλών.

## Πλήρες εκτελέσιμο παράδειγμα

Ακολουθεί το πλήρες πρόγραμμα Java που μπορείτε να επικολλήσετε σε οποιοδήποτε IDE. Βεβαιωθείτε ότι έχετε τη βιβλιοθήκη Aspose.Cells for Java στο classpath σας.

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.getWorksheets().get(0);

        // Apply WRAPCOLS to reorganize data
        Cell wrapCell = ws.getCells().get("A1");
        wrapCell.setFormula("=WRAPCOLS(A2:A10,3)");

        // Configure SVG options with embedded fonts
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.SVG);
        imgOptions.setEmbedFonts(true);
        imgOptions.setFontVariationSelectors(true);

        // Set the region that will appear in the SVG
        ws.getPageSetup().setPrintArea("A1:H30");

        // Attach the image options to the worksheet
        ws.getPageSetup().setPrintOptions(imgOptions);

        // Export the worksheet as an SVG file
        ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);

        System.out.println("SVG exported successfully with embedded fonts.");
    }
}
```

**Βήματα επαλήθευσης**

1. Εκτελέστε το πρόγραμμα.  
2. Ανοίξτε το `output.svg` σε έναν web browser.  
3. Επιβεβαιώστε ότι το κείμενο χρησιμοποιεί την ίδια γραμματοσειρά με το αρχικό αρχείο Excel (οι γραμματοσειρές είναι ενσωματωμένες).  
4. Επαληθεύστε ότι εμφανίζονται μόνο τα κελιά εντός του `A1:H30` και ότι τα δεδομένα από το `A2:A10` εμφανίζονται σε τρεις στήλες.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|------------------|----------|
| Οι γραμματοσειρές λείπουν στο SVG | `setEmbedFonts(false)` ή το αρχείο γραμματοσειράς δεν είναι προσβάσιμο | Βεβαιωθείτε ότι `setEmbedFonts(true)` και ότι η γραμματοσειρά είναι εγκατεστημένη στη μηχανή που εκτελεί τον κώδικα |
| Το WRAPCOLS δεν αξιολογείται | Η μηχανή υπολογισμού είναι απενεργοποιημένη | Καλέστε `workbook.calculateFormula()` πριν την εξαγωγή, ή αφήστε το Aspose.Cells να αξιολογήσει κατά την αποθήκευση |
| Το εξαγόμενο SVG είναι κενό | Η περιοχή εκτύπωσης δεν περιλαμβάνει δεδομένα | Ελέγξτε ξανά το εύρος που δόθηκε στο `setPrintArea` |
| Το αρχείο SVG είναι τεράστιο | Δεν εφαρμόστηκε κλιμάκωση, μεγάλη ανάλυση εικόνας | Προσαρμόστε `imgOptions.setResolution(96)` ή παρόμοιο για έλεγχο DPI |

## Pro tip: επαναχρησιμοποίηση ImageOrPrintOptions για πολλαπλά φύλλα εργασίας

Αν το βιβλίο εργασίας σας περιέχει πολλά φύλλα που χρειάζονται τα ίδια SVG settings, δημιουργήστε μια ενιαία παρουσία `ImageOrPrintOptions` και αντιστοιχίστε την σε κάθε `PageSetup` φύλλου. Αυτό μειώνει τη χρήση μνήμης και εγγυάται συνεπή ενσωμάτωση γραμματοσειρών σε όλα τα εξαγόμενα αρχεία.

```java
ImageOrPrintOptions sharedOptions = new ImageOrPrintOptions();
sharedOptions.setImageFormat(ImageFormat.SVG);
sharedOptions.setEmbedFonts(true);
sharedOptions.setFontVariationSelectors(true);

for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    sheet.getPageSetup().setPrintOptions(sharedOptions);
    sheet.getPageSetup().setPrintArea("A1:H30");
    sheet.getPageSetup().save("YOUR_DIRECTORY/sheet" + i + ".svg", SaveFormat.SVG);
}
```

## Επόμενα βήματα

* **Εξαγωγή σε άλλες διανυσματικές μορφές** – Αλλάξτε το `ImageFormat.SVG` σε `ImageFormat.PDF` για PDF υψηλής ποιότητας.  
* **Επεξεργασία σε παρτίδες** – Επανάληψη μέσω φακέλου `.xlsx` αρχείων και αυτόματη δημιουργία SVG.  
* **Προσαρμοσμένη διαχείριση γραμματοσειρών** – Χρησιμοποιήστε το `FontSettings` για φόρτωση γραμματοσειρών από συγκεκριμένο φάκελο όταν οι συστημικές γραμματοσειρές δεν επαρκούν.  

Με την εξοικείωση με **embed fonts in SVG**, **export excel to svg**, **set print area**, **set print options**, και **use WRAPCOLS function**, μπορείτε να αυτοματοποιήσετε τη δημιουργία SVG υψηλής πιστότητας για αναφορές, dashboards και web visualizations απευθείας από δεδομένα Excel. Καλό κώδικα!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}