---
category: general
date: 2026-07-03
description: Εξαγωγή εικόνας πίνακα Pivot του Excel χρησιμοποιώντας Java. Μάθετε πώς
  να ορίσετε τη μορφή εικόνας PNG με το Aspose.Cells βήμα‑βήμα.
draft: false
keywords:
- excel pivot table image
- set image format png
- Aspose.Cells export
- Java Excel automation
- pivot table to image
language: el
og_description: Εξήγηση εξαγωγής εικόνας πίνακα Pivot του Excel σε Java. Ακολουθήστε
  αυτό το σεμινάριο για να ορίσετε τη μορφή εικόνας PNG γρήγορα και αξιόπιστα.
og_title: εικόνα πίνακα Pivot του Excel – Οδηγός Java για εξαγωγή PNG
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Export an excel pivot table image using Java. Learn how to set image
    format png with Aspose.Cells step‑by‑step.
  headline: 'excel pivot table image: Export to PNG with Java'
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel
- ImageExport
title: 'Εικόνα πίνακα Pivot του Excel: Εξαγωγή σε PNG με Java'
url: /el/java/excel-pivot-tables/excel-pivot-table-image-export-to-png-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# excel pivot table image – Εξαγωγή Πίνακα Περιστροφής ως PNG σε Java

Έχετε χρειαστεί ποτέ να μετατρέψετε μια **excel pivot table image** σε PNG έτοιμο για κοινή χρήση αλλά δεν ήξερατε από πού να ξεκινήσετε; Δεν είστε μόνοι. Σε πολλά pipelines αναφορών ο πίνακας περιστροφής είναι το αστέρι, ενώ η υπόλοιπη ομάδα θέλει μόνο μια στατική εικόνα. Τα καλά νέα; Με λίγες γραμμές Java και Aspose.Cells μπορείτε να **set image format png** και να πάρετε ακριβώς αυτό που χρειάζεστε.

Σε αυτόν τον οδηγό θα περάσουμε από τη διαδικασία από την αρχή: φόρτωση ενός workbook, λήψη του πρώτου pivot table, ρύθμιση των επιλογών εξαγωγής και τελικά εγγραφή μιας καθαρής PNG εικόνας στο δίσκο. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Java.

## What You’ll Learn

- Πώς να φορτώσετε ένα Excel workbook από το σύστημα αρχείων.
- Πώς να εντοπίσετε έναν συγκεκριμένο pivot table σε ένα φύλλο εργασίας.
- Τα ακριβή βήματα για **set image format png** για την εξαγόμενη εικόνα.
- Συνηθισμένα προβλήματα (πολλαπλοί pivot tables, μεγάλα σύνολα δεδομένων) και πώς να τα αποφύγετε.
- Μια έτοιμη‑για‑εκτέλεση κλάση Java που μπορείτε να αντιγράψετε‑και‑επικολλήσετε.

### Prerequisites

- Java 8 ή νεότερη εγκατεστημένη.
- Βιβλιοθήκη Aspose.Cells for Java (η πιο πρόσφατη έκδοση μέχρι 2026‑07‑03).
- Ένα αρχείο Excel (`input.xlsx`) που περιέχει τουλάχιστον έναν pivot table.
- Βασική εξοικείωση με Maven ή Gradle για διαχείριση εξαρτήσεων.

---

## Step 1: Add Aspose.Cells to Your Project

Πρώτα απ’ όλα—βεβαιωθείτε ότι το JAR του Aspose.Cells βρίσκεται στο classpath. Αν χρησιμοποιείτε Maven, προσθέστε αυτό στο `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- latest at time of writing -->
</dependency>
```

Για Gradle, είναι εξίσου απλό:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **Pro tip:** Η Aspose προσφέρει δωρεάν κλειδί αξιολόγησης 30 ημερών. Εγγραφείτε στον ιστότοπό τους, έπειτα προσθέστε `License.setLicense("Aspose.Cells.lic");` στην αρχή του προγράμματός σας για να ξεκλειδώσετε όλες τις λειτουργίες.

## Step 2: Load the Workbook and Access the Pivot Table

Τώρα θα ανοίξουμε το αρχείο Excel και θα πάρουμε τον πρώτο pivot table. Ο κώδικας παρακάτω κάνει ακριβώς αυτό, και είναι σκόπιμα αμυντικός—αν το workbook δεν έχει φύλλα ή το φύλλο δεν περιέχει pivot table, θα ρίξει μια σαφή εξαίρεση.

```java
import com.aspose.cells.*;

import java.io.File;

public class PivotTableToPng {

    public static void main(String[] args) {
        // Adjust these paths to match your environment
        String inputPath = "YOUR_DIRECTORY/input.xlsx";
        String outputPath = "YOUR_DIRECTORY/pivot.png";

        try {
            // Load the workbook from disk
            Workbook wb = new Workbook(inputPath);

            // Ensure there is at least one worksheet
            if (wb.getWorksheets().getCount() == 0) {
                throw new IllegalStateException("The workbook contains no worksheets.");
            }

            // Grab the first worksheet (index 0)
            Worksheet ws = wb.getWorksheets().get(0);

            // Verify that the worksheet actually has a pivot table
            if (ws.getPivotTables().getCount() == 0) {
                throw new IllegalStateException("No pivot tables found on the first worksheet.");
            }

            // Retrieve the first pivot table
            PivotTable pt = ws.getPivotTables().get(0);

            // -------------------------------------------------
            // Step 3: Configure image export options (PNG)
            // -------------------------------------------------
            ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
            // This is where we **set image format png**
            imgOpt.setImageFormat(ImageFormat.PNG);
            // Optional: increase the DPI for sharper output (default is 96)
            imgOpt.setResolution(300);

            // -------------------------------------------------
            // Step 4: Export the pivot table as an image file
            // -------------------------------------------------
            pt.toImage(outputPath, imgOpt);

            System.out.println("Successfully exported the excel pivot table image to: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### Why These Steps Matter

- **Loading the workbook** μας δίνει πρόσβαση στις υποκείμενες δομές δεδομένων· το Aspose.Cells αφαιρεί την ανάγκη χαμηλού επιπέδου ανάλυσης OpenXML.
- **Accessing the worksheet** είναι απαραίτητο επειδή οι pivot tables συνδέονται με ένα συγκεκριμένο φύλλο. Αν έχετε πολλά φύλλα, μπορείτε να κάνετε βρόχο στο `wb.getWorksheets()` και να επιλέξετε αυτό που περιέχει τον επιθυμητό pivot.
- **Retrieving the pivot table** είναι η καρδιά της λειτουργίας. Το `ws.getPivotTables().get(0)` φέρνει τον πρώτο, αλλά μπορείτε επίσης να ψάξετε με όνομα χρησιμοποιώντας `ws.getPivotTables().get("MyPivot")`.
- **Setting image format png** (η δευτερεύουσα λέξη‑κλειδί) λέει στο Aspose.Cells να αποδώσει το αποτέλεσμα ως lossless PNG. Αυτή η μορφή διατηρεί τις καθαρές γραμμές και το κείμενο, ιδανική για αναφορές.
- **Exporting with `toImage`** γράφει το αρχείο με μία κλήση, διαχειριζόμενο αυτόματα την σελιδοποίηση και την κλιμάκωση.

## Step 3: Verify the Output

Αφού τρέξετε το πρόγραμμα, μεταβείτε στο `YOUR_DIRECTORY` και θα δείτε το `pivot.png`. Ανοίξτε το με οποιονδήποτε προβολέα εικόνας—σημειώστε τις καθαρές γραμμές πλέγματος και τη διάταξη που βλέπετε στο Excel. Αν η εικόνα φαίνεται θολή, αυξήστε το DPI στο `imgOpt.setResolution()`· 300‑600 λειτουργούν καλά για εκτυπώσεις υψηλής ποιότητας.

![excel pivot table image exported as PNG](excel-pivot-table-image.png "excel pivot table image exported as PNG")

*Image alt text:* **excel pivot table image exported as PNG**

## Handling Multiple Pivot Tables

Τι γίνεται αν το φύλλο σας περιέχει περισσότερους από έναν pivot table; Το παραπάνω snippet παίρνει τον πρώτο, αλλά μπορείτε να επαναλάβετε:

```java
for (int i = 0; i < ws.getPivotTables().getCount(); i++) {
    PivotTable pt = ws.getPivotTables().get(i);
    String outFile = "YOUR_DIRECTORY/pivot_" + i + ".png";
    pt.toImage(outFile, imgOpt);
}
```

Αυτός ο βρόχος θα δημιουργήσει `pivot_0.png`, `pivot_1.png`, κ.λπ., καθένα αντιπροσωπεύοντας διαφορετικό pivot table. Θυμηθείτε να **set image format png** μία φορά πριν τον βρόχο· η ίδια παρουσία `ImageOrPrintOptions` μπορεί να επαναχρησιμοποιηθεί.

## Edge Cases & Tips

| Situation | What to Watch For | Suggested Fix |
|-----------|-------------------|---------------|
| **Large pivot (many rows/columns)** | Το PNG μπορεί να γίνει τεράστιο, προκαλώντας πίεση μνήμης. | Χρησιμοποιήστε `imgOpt.setOnePagePerSheet(false)` για διαίρεση σε πολλές σελίδες, ή μειώστε το DPI. |
| **Hidden rows/columns** | Το Aspose σέβεται την ορατότητα· κρυφά δεδομένα δεν εμφανίζονται. | Αποκρύψτε προγραμματιστικά με `ws.showRows(start, count, true)`. |
| **Custom styles (fonts, colors)** | Ορισμένες εταιρικές γραμματοσειρές μπορεί να μην αποδοθούν αν δεν είναι εγκατεστημένες στον server. | Ενσωματώστε τη γραμματοσειρά στο JVM ή χρησιμοποιήστε fallback σε σύστημα μέσω `imgOpt.setFontEmbeddingMode(FontEmbeddingMode.EMBED_ALL)`. |
| **Different output format needed later** | Μπορεί να θέλετε JPEG ή BMP. | Αλλάξτε σε `imgOpt.setImageFormat(ImageFormat.JPEG)`—ο ίδιος κώδικας λειτουργεί, απλώς με διαφορετική τιμή enum. |

## Full Working Example (Copy‑Paste)

Παρακάτω είναι ολόκληρη η κλάση, έτοιμη για μεταγλώττιση. Επικολλήστε την στο `PivotTableToPng.java`, προσαρμόστε τις διαδρομές και τρέξτε `javac PivotTableToPng.java && java PivotTableToPng`.

```java
import com.aspose.cells.*;

public class PivotTableToPng {

    public static void main(String[] args) {
        // ----- Configuration -----
        String inputPath = "YOUR_DIRECTORY/input.xlsx";
        String outputPath = "YOUR_DIRECTORY/pivot.png";

        try {
            // Load workbook
            Workbook wb = new Workbook(inputPath);

            // Guard clauses
            if (wb.getWorksheets().getCount() == 0) {
                throw new IllegalStateException("Workbook has no worksheets.");
            }

            Worksheet ws = wb.getWorksheets().get(0);
            if (ws.getPivotTables().getCount() == 0) {
                throw new IllegalStateException("No pivot tables on the first worksheet.");
            }

            // Retrieve the first pivot table
            PivotTable pt = ws.getPivotTables().get(0);

            // ----- Set image format png -----
            ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
            imgOpt.setImageFormat(ImageFormat.PNG);   // <-- key line
            imgOpt.setResolution(300);                // optional, for sharper output

            // Export to PNG
            pt.toImage(outputPath, imgOpt);

            System.out.println("excel pivot table image exported successfully: " + outputPath);
        } catch (Exception ex) {
            System.err.println("Error during export:");
            ex.printStackTrace();
        }
    }
}
```

Τρέξτε το και θα έχετε μια **excel pivot table image** αποθηκευμένη ως αρχείο PNG—ακριβώς ό,τι υποσχέθηκε ο οδηγός.

---

## Conclusion

Καλύψαμε όλα όσα χρειάζεστε για να **export an excel pivot table image** χρησιμοποιώντας Java, και σας δείξαμε πώς να **set image format png** με το Aspose.Cells. Από τη φόρτωση του workbook μέχρι τη διαχείριση edge cases, η λύση είναι σύντομη, αξιόπιστη και έτοιμη για παραγωγή.

Τι ακολουθεί; Δοκιμάστε την εξαγωγή πολλαπλών pivot σε batch, πειραματιστείτε με διαφορετικές ρυθμίσεις DPI για εκτυπώσεις υψηλής ποιότητας, ή αλλάξτε τη μορφή σε JPEG για βέλτιστη απόδοση στο web. Μπορείτε επίσης να ενσωματώσετε το PNG σε αναφορά PDF—το Aspose.PDF το κάνει παιχνιδάκι.

Έχετε κάποια τροποποίηση στη ροή εργασίας ή κάποιο εμπόδιο; Αφήστε σχόλιο και θα το λύσουμε μαζί. Καλό κώδικα!

## What Should You Learn Next?

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κυριαρχήσετε σε πρόσθετα χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην δική σας υλοποίηση.

- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Create Excel Chart with Trendline and Export to Image using Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}