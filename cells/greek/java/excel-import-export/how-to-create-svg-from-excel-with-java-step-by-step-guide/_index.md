---
category: general
date: 2026-11-22
description: Μάθετε πώς να δημιουργείτε SVG από το Excel χρησιμοποιώντας το Aspose.Cells
  for Java. Εξάγετε το Excel σε SVG, αποθηκεύστε το βιβλίο εργασίας ως SVG και δείτε
  πλήρες παράδειγμα κώδικα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create svg from excel
- export excel to svg
- how to export excel as svg
- save excel file as svg
- save workbook as svg
language: el
lastmod: 2026-11-22
og_description: Δημιουργήστε SVG από το Excel χρησιμοποιώντας το Aspose.Cells για
  Java. Αυτό το σεμινάριο δείχνει πώς να εξάγετε το Excel σε SVG, να αποθηκεύσετε
  το βιβλίο εργασίας ως SVG και περιλαμβάνει ένα πλήρες εκτελέσιμο παράδειγμα.
og_image_alt: Screenshot showing an Excel worksheet exported as an SVG file
og_title: Δημιουργήστε SVG από το Excel με Java – πλήρης οδηγός εξαγωγής
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to create SVG from Excel using Aspose.Cells for Java. Export
    Excel to SVG, save workbook as SVG, and see full code example.
  headline: How to create SVG from Excel with Java – step‑by‑step guide
  type: TechArticle
tags:
- Excel
- SVG
- Java
- Aspose.Cells
- Export
title: Πώς να δημιουργήσετε SVG από το Excel με τη Java – οδηγός βήμα‑προς‑βήμα
url: /el/java/excel-import-export/how-to-create-svg-from-excel-with-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε SVG από Excel με Java – οδηγός βήμα‑βήμα

Αν χρειάζεστε **create SVG from Excel**, αυτό το tutorial σας δείχνει ακριβώς πώς να το κάνετε. Θα μάθετε πώς να **export Excel to SVG**, να αποθηκεύσετε το βιβλίο εργασίας ως αρχείο SVG και να επαληθεύσετε το αποτέλεσμα—όλα με ένα ενιαίο, αυτόνομο πρόγραμμα Java.

Η εξαγωγή δεδομένων υπολογιστικού φύλλου ως scalable vector graphics είναι χρήσιμη όταν θέλετε καθαρά διαγράμματα για ιστοσελίδες, εκτυπώσιμα διαγράμματα ή μικρογραφίες υψηλής ανάλυσης. Ο οδηγός καλύπτει όλα όσα χρειάζεστε, από τη ρύθμιση του έργου μέχρι τη διαχείριση edge cases, ώστε να μπορείτε να αρχίσετε να χρησιμοποιείτε τη λύση αμέσως.

## Τι θα χρειαστείτε

* Java Development Kit (JDK) 8 ή νεότερο  
* Maven ή Gradle για διαχείριση εξαρτήσεων (το παράδειγμα χρησιμοποιεί Maven)  
* Ένα έγκυρο license για **Aspose.Cells for Java** (η βιβλιοθήκη προσφέρει δωρεάν δοκιμή)  
* Ένα αρχείο Excel (`sample.xlsx`) που περιέχει τα δεδομένα που θέλετε να μετατρέψετε  

Αυτές οι προαπαιτήσεις εξασφαλίζουν ότι ο κώδικας θα μεταγλωττιστεί και θα εκτελεστεί χωρίς πρόσθετη ρύθμιση.

## Βήμα 1: Ρυθμίστε το έργο Maven και προσθέστε το Aspose.Cells

Δημιουργήστε ένα νέο έργο Maven ή προσθέστε την ακόλουθη εξάρτηση στο υπάρχον `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

Η προσθήκη της εξάρτησης κατεβάζει τη βιβλιοθήκη **Aspose.Cells**, η οποία παρέχει την κλάση `ImageOrPrintOptions` που χρησιμοποιείται για **save workbook as SVG**. Το Maven επιλύει αυτόματα τις διαμεταβιβάσιμες εξαρτήσεις, οπότε δεν απαιτούνται επιπλέον JAR.

> **Συμβουλή επαγγελματία:** Αν χρησιμοποιείτε Gradle, η ισοδύναμη εγγραφή είναι  
> `implementation 'com.aspose:aspose-cells:23.12'`.

## Βήμα 2: Φορτώστε το βιβλίο εργασίας Excel

Το πρώτο μπλοκ κώδικα δημιουργεί μια παρουσία `Workbook` που αντιπροσωπεύει το αρχείο Excel που θέλετε να μετατρέψετε. Αντικαταστήστε το `"sample.xlsx"` με τη διαδρομή του πηγαίου σας αρχείου.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.LoadOptions;

public class ExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Load the Excel workbook from disk
        LoadOptions loadOptions = new LoadOptions();
        Workbook workbook = new Workbook("sample.xlsx", loadOptions);
        // Continue with export steps...
    }
}
```

Η φόρτωση του βιβλίου εργασίας είναι απαραίτητη επειδή η διαδικασία **export excel to SVG** λειτουργεί πάνω σε μια αναπαράσταση του υπολογιστικού φύλλου στη μνήμη. Το αντικείμενο `LoadOptions` σας επιτρέπει να ελέγξετε πώς θα αναλυθεί το αρχείο, αλλά οι προεπιλεγμένες ρυθμίσεις λειτουργούν για τις περισσότερες περιπτώσεις.

## Βήμα 3: Διαμορφώστε το `ImageOrPrintOptions` για έξοδο SVG

`ImageOrPrintOptions` ενημερώνει το Aspose.Cells ποια μορφή να δημιουργήσει. Η ρύθμιση `SaveFormat.SVG` υποδεικνύει στη βιβλιοθήκη να παράγει scalable vector graphics αντί για raster images.

```java
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.SaveFormat;

ImageOrPrintOptions options = new ImageOrPrintOptions();
options.setSaveFormat(SaveFormat.SVG);   // Export Excel as SVG
options.setOnePagePerSheet(true);        // Optional: one SVG per sheet
```

Η σημαία `setOnePagePerSheet(true)` εξασφαλίζει ότι κάθε φύλλο εργασίας γίνεται ένα μοναδικό αρχείο SVG, το οποίο είναι η πιο κοινή απαίτηση όταν **save excel file as SVG** για δημοσίευση στο web.

## Βήμα 4: Αποθηκεύστε το βιβλίο εργασίας (ή ένα μόνο φύλλο) ως SVG

Μπορείτε να εξάγετε ολόκληρο το βιβλίο εργασίας ή μόνο ένα συγκεκριμένο φύλλο. Το παρακάτω παράδειγμα αποθηκεύει το πρώτο φύλλο εργασίας σε ένα αρχείο SVG με όνομα `output.svg`.

```java
import com.aspose.cells.Worksheet;
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.SheetRender;

// Choose the first worksheet (index 0)
Worksheet sheet = workbook.getWorksheets().get(0);

// Render the worksheet to SVG using the configured options
SheetRender render = new SheetRender(sheet, options);
render.toImage(0, "output.svg");   // Saves as SVG
```

Αν προτιμάτε να **save workbook as SVG** (όλα τα φύλλα σε ένα SVG), χρησιμοποιήστε `workbook.save("output.svg", options);` αντί για `SheetRender`. Η βιβλιοθήκη συνενώνει αυτόματα τα φύλλα σε ένα ενιαίο έγγραφο SVG.

## Βήμα 5: Επαληθεύστε το παραγόμενο αρχείο SVG

Μετά το τέλος του προγράμματος, θα πρέπει να δείτε το `output.svg` στον φάκελο εργασίας του έργου. Ανοίξτε το σε έναν web browser ή σε έναν επεξεργαστή που υποστηρίζει SVG για να επιβεβαιώσετε ότι η οπτική διάταξη ταιριάζει με το αρχικό φύλλο Excel.

```text
✅ SVG file created: output.svg
```

Αν το SVG εμφανίζεται κενό, ελέγξτε τα εξής:

* Το βιβλίο εργασίας περιέχει πραγματικά δεδομένα στο εξαγόμενο φύλλο.  
* `setOnePagePerSheet(true)` ταιριάζει με τις προσδοκίες της διάταξής σας.  
* Η άδεια Aspose.Cells έχει οριστεί σωστά (η λειτουργία χωρίς άδεια προσθέτει υδατογράφημα).

### Διαχείριση κοινών edge cases

| Κατάσταση                                 | Λύση                                                                                         |
|-------------------------------------------|----------------------------------------------------------------------------------------------|
| Πολλαπλά φύλλα εργασίας χρειάζονται ξεχωριστά SVGs    | Κάντε επανάληψη μέσω `workbook.getWorksheets()` και καλέστε `SheetRender.toImage` για κάθε φύλλο.          |
| Μεγάλα φύλλα εργασίας υπερβαίνουν τα όρια μνήμης     | Ενεργοποιήστε `options.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` για χρήση προσωρινής αποθήκευσης σε δίσκο. |
| Προσαρμοσμένες γραμματοσειρές δεν αποδίδονται σωστά   | Καταχωρίστε το φάκελο γραμματοσειρών με `FontConfigs.setFontFolder("path/to/fonts")`.                     |
| Απαιτείται διαφάνεια φόντου               | Καλέστε `options.setTransparent(true)` πριν από την αποθήκευση.                                               |

Αυτές οι συμβουλές κάνουν τη διαδικασία **how to export Excel as SVG** ανθεκτική για περιβάλλοντα παραγωγής.

## Πλήρες εκτελέσιμο παράδειγμα

Παρακάτω υπάρχει ένα πλήρες πρόγραμμα Java που ενσωματώνει όλα τα προηγούμενα βήματα. Αντιγράψτε τον κώδικα στο `src/main/java/ExcelToSvg.java`, προσαρμόστε τις διαδρομές αρχείων και εκτελέστε `mvn compile exec:java -Dexec.mainClass=ExcelToSvg`.

```java
package com.example.excelsvg;

import com.aspose.cells.*;

public class ExcelToSvg {
    public static void main(String[] args) {
        try {
            // 1️⃣ Load the Excel workbook
            String excelPath = "sample.xlsx";          // ← replace with your file
            Workbook workbook = new Workbook(excelPath);

            // 2️⃣ Configure export options for SVG
            ImageOrPrintOptions options = new ImageOrPrintOptions();
            options.setSaveFormat(SaveFormat.SVG);
            options.setOnePagePerSheet(true);          // one SVG per worksheet
            options.setTransparent(true);              // optional: transparent background

            // 3️⃣ Export each worksheet as a separate SVG file
            for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
                Worksheet sheet = workbook.getWorksheets().get(i);
                String sheetName = sheet.getName().replaceAll("[^a-zA-Z0-9]", "_");
                String svgPath = "output_" + sheetName + ".svg";

                SheetRender render = new SheetRender(sheet, options);
                render.toImage(0, svgPath);            // 0 = first page of the sheet

                System.out.println("✅ Saved sheet \"" + sheetName + "\" as " + svgPath);
            }

        } catch (Exception e) {
            System.err.println("❌ Error during SVG export: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

**Αναμενόμενη έξοδος** (console):

```
✅ Saved sheet "Sheet1" as output_Sheet1.svg
✅ Saved sheet "Sheet2" as output_Sheet2.svg
```

Κάθε αρχείο SVG αντικατοπτρίζει την εμφάνιση του αντίστοιχου φύλλου εργασίας, διατηρώντας διαγράμματα, σχήματα και μορφοποίηση κελιών σε οποιοδήποτε επίπεδο ζουμ.

## Συμπέρασμα

Τώρα ξέρετε πώς να **create SVG from Excel** χρησιμοποιώντας το Aspose.Cells for Java. Ο οδηγός κάλυψε τα πάντα από τη ρύθμιση του έργου μέχρι τη διαχείριση τυπικών edge cases, και ο πλήρης κώδικας σας επιτρέπει να **export Excel to SVG** σε μια μόνο εκτέλεση.  

Από εδώ μπορείτε:

* **Save excel file as SVG** για web dashboards ή τεκμηρίωση.  
* Εξερευνήστε άλλες μορφές εξαγωγής (PDF, PNG) αλλάζοντας το `SaveFormat`.  
* Ενσωματώστε τη μετατροπή σε μια μεγαλύτερη υπηρεσία Java που επεξεργάζεται υπολογιστικά φύλλα σε πραγματικό χρόνο.  

Μη διστάσετε να πειραματιστείτε με τις επιλογές—διαφορετικές ρυθμίσεις `ImageOrPrintOptions` σας επιτρέπουν να ελέγξετε το μέγεθος σελίδας, DPI και χρώμα φόντου. Αν αντιμετωπίσετε προβλήματα, επιστρέψτε στον πίνακα edge‑case ή συμβουλευτείτε την αναφορά API του Aspose.Cells για πιο προχωρημένη προσαρμογή.

Καλό προγραμματισμό και απολαύστε τα καθαρά, κλιμακώσιμα γραφικά που παρέχει το SVG!

## Τι θα πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να δημιουργήσετε και να αποθηκεύσετε ένα βιβλίο εργασίας Excel ως SVG χρησιμοποιώντας Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Πώς να εξάγετε διαγράμματα Excel ως SVG χρησιμοποιώντας Aspose.Cells Java για Scalable Vector Graphics](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Πώς να μετατρέψετε SVG από διαγράμματα Excel χρησιμοποιώντας Aspose.Cells Java](/cells/english/java/charts-graphs/convert-excel-charts-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}