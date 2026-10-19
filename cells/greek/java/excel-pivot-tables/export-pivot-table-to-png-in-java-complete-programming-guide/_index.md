---
category: general
date: 2026-06-27
description: Εξαγωγή πίνακα pivot ως εικόνα pivot του Excel σε Java. Μάθετε πώς να
  ορίσετε μορφή PNG, να διαμορφώσετε τις επιλογές και να αποθηκεύσετε το αρχείο σε
  λίγα μόνο βήματα.
draft: false
keywords:
- export pivot table
- excel pivot image
- set png format
language: el
og_description: Εξαγωγή πίνακα Pivot ως εικόνα Pivot του Excel χρησιμοποιώντας Java.
  Αυτός ο οδηγός δείχνει πώς να ορίσετε τη μορφή PNG και να αποθηκεύσετε την εικόνα
  με σιγουριά.
og_title: Εξαγωγή συγκεντρωτικού πίνακα σε PNG στη Java – Οδηγός βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Export pivot table as an Excel pivot image in Java. Learn how to set
    PNG format, configure options, and save the file in just a few steps.
  headline: Export pivot table to PNG in Java – Complete Programming Guide
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Εξαγωγή συγκεντρωτικού πίνακα σε PNG στη Java – Πλήρης Οδηγός Προγραμματισμού
url: /el/java/excel-pivot-tables/export-pivot-table-to-png-in-java-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export pivot table to PNG in Java – Complete Programming Guide

Ποτέ χρειάστηκε να **εξάγετε έναν πίνακα pivot** από ένα βιβλίο εργασίας Excel αλλά δεν ήξερες πώς να πάρεις ένα καθαρό αρχείο εικόνας; Δεν είσαι μόνος – πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν δημιουργούν πίνακες αναφορών. Τα καλά νέα είναι ότι με μερικές γραμμές κώδικα Java μπορείς να μετατρέψεις οποιονδήποτε πίνακα pivot σε μια καθαρή **εικόνα pivot Excel** αποθηκευμένη ως PNG.  

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: ανάγνωση του βιβλίου εργασίας, εντοπισμός του πρώτου πίνακα pivot, ρύθμιση της εξαγωγής για **ορισμό μορφής PNG**, και τέλος εγγραφή της εικόνας στο δίσκο. Στο τέλος θα έχεις ένα επαναχρησιμοποιήσιμο snippet που μπορείς να ενσωματώσεις σε οποιοδήποτε έργο.

## What You’ll Learn

- Πώς να φορτώσεις ένα αρχείο Excel με Aspose.Cells (ή Apache POI αν προτιμάς).
- Τα ακριβή API calls που απαιτούνται για **εξαγωγή πίνακα pivot** ως PNG.
- Γιατί η ρύθμιση της μορφής εικόνας είναι σημαντική και πώς να **ορίσεις τη μορφή PNG** σωστά.
- Συνηθισμένα προβλήματα – όπως η διαχείριση πολλαπλών πινάκων pivot ή ελλιπών φύλλων εργασίας – και πώς να τα αποφύγεις.
- Ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα Java που μπορείς να αντιγράψεις‑και‑επικολλήσεις.

> **Prerequisites**  
> • Java 17 ή νεότερη (ο κώδικας λειτουργεί και με παλαιότερες εκδόσεις, αλλά συνιστάται η 17).  
> • Βιβλιοθήκη Aspose.Cells for Java (η δωρεάν δοκιμή λειτουργεί κανονικά).  
> • Βασική εξοικείωση με αρχεία Excel και Java I/O.

---

## Step 1: Add Aspose.Cells Dependency

Αν χρησιμοποιείς Maven, πρόσθεσε την παρακάτω εξάρτηση στο `pom.xml`. Διαφορετικά, κατέβασε το JAR από την ιστοσελίδα της Aspose και πρόσθεσέ το στο classpath σου.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- latest as of June 2026 -->
</dependency>
```

*Pro tip:* Κράτα τις εκδόσεις των βιβλιοθηκών σου συγχρονισμένες με τις επίσημες σημειώσεις κυκλοφορίας για να αποφύγεις απρόσμενα σφάλματα.

## Step 2: Load the Workbook and Locate the Pivot Table

Πρώτα ανοίγουμε το αρχείο Excel, μετά παίρνουμε τον πρώτο πίνακα pivot στο πρώτο φύλλο εργασίας. Αν το βιβλίο εργασίας δεν περιέχει πίνακες pivot, τερματίζουμε ήρεμα.

```java
import com.aspose.cells.*;

public class PivotTableExporter {

    public static void main(String[] args) {
        try {
            // Load the workbook (replace with your actual path)
            Workbook workbook = new Workbook("C:/data/report.xlsx");

            // Access the first worksheet – you can also loop through all sheets
            Worksheet ws = workbook.getWorksheets().get(0);

            // Verify that the sheet actually contains pivot tables
            if (ws.getPivotTables().getCount() == 0) {
                System.out.println("No pivot tables found on the first sheet.");
                return;
            }

            // Retrieve the first pivot table (this is the target for export)
            PivotTable pivotTable = ws.getPivotTables().get(0);
```

> **Why this step matters** – Το αντικείμενο `PivotTable` είναι το σημείο εισόδου για οποιαδήποτε εξαγωγή εικόνας. Η κλήση `toImage` σε έναν μη‑υπάρχοντα πίνακα pivot θα προκαλέσει `NullPointerException`, γι’ αυτό ελέγχουμε πρώτα τον αριθμό.

## Step 3: Configure Image Export Options (Set PNG Format)

Τώρα δημιουργούμε μια παρουσία `ImageOrPrintOptions` και ορίζουμε ρητά **τη μορφή PNG**. Το PNG είναι loss‑less, διατηρώντας την ευκρίνεια των γραμμών πλέγματος και των γραμματοσειρών.

```java
            // Step 3: Configure image export options – we want PNG
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
            imgOptions.setImageFormat(ImageFormat.PNG);   // <-- set png format
            imgOptions.setOnePagePerSheet(true);          // optional: force single‑page output
            imgOptions.setTransparent(true);              // optional: keep background transparent
```

*Note:* Αν χρειάζεσαι JPEG αντί για PNG, απλώς αντικατέστησε το `ImageFormat.PNG` με `ImageFormat.JPEG`. Το ίδιο αντικείμενο επιλογών λειτουργεί και για τις δύο μορφές.

## Step 4: Export the Pivot Table as an Image File

Με τις επιλογές έτοιμες, καλούμε το `toImage`. Η μέθοδος γράφει το αρχείο άμεσα, χωρίς επιπλέον ροές.

```java
            // Step 4: Export the pivot table as an image file
            String outputPath = "C:/exports/pivot.png";
            pivotTable.toImage(outputPath, imgOptions);

            System.out.println("Pivot table exported successfully to: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

Η εκτέλεση του προγράμματος παράγει ένα αρχείο με όνομα `pivot.png` που φαίνεται ακριβώς όπως ο πίνακας pivot στο Excel. Άνοιξέ το με οποιονδήποτε προβολέα εικόνων για επαλήθευση.

### Expected Output

```
Pivot table exported successfully to: C:/exports/pivot.png
```

Η παραγόμενη εικόνα θα ταιριάζει με τη διάταξη στην οθόνη, συμπεριλαμβανομένων των πλάτους στηλών, ύψους γραμμών και τυχόν conditional formatting που έχεις εφαρμόσει.

## Handling Multiple Pivot Tables (Advanced)

Τι γίνεται αν το φύλλο εργασίας σου περιέχει πολλούς πίνακες pivot και θέλεις μόνο έναν συγκεκριμένο; Μπορείς να κάνεις βρόχο στο `ws.getPivotTables()` και να επιλέξεις με βάση το όνομα:

```java
PivotTable target = null;
for (int i = 0; i < ws.getPivotTables().getCount(); i++) {
    PivotTable pt = ws.getPivotTables().get(i);
    if ("SalesByRegion".equals(pt.getName())) {
        target = pt;
        break;
    }
}
if (target == null) {
    System.out.println("Desired pivot table not found.");
    return;
}
target.toImage("C:/exports/sales_by_region.png", imgOptions);
```

*Why this is useful*: Σε πραγματικές αναφορές συχνά υπάρχει ένας συνοπτικός πίνακας pivot και ένας λεπτομερής. Η επιλογή με όνομα αποτρέπει τυχαίες αντικαταστάσεις.

## Common Pitfalls & How to Avoid Them

| Issue | Symptom | Fix |
|------|----------|-----|
| **Missing worksheet** | `IndexOutOfBoundsException` κατά την πρόσβαση στο `ws` | Επαλήθευσε ότι `workbook.getWorksheets().getCount() > 0` πριν κάνεις indexing. |
| **No pivot tables** | Σιωπηλή αποτυχία ή κενή εικόνα | Χρησιμοποίησε έλεγχο `ws.getPivotTables().getCount()` (δες το Βήμα 2). |
| **Wrong image format** | Η έξοδος φαίνεται θολή ή με τεχνουργήματα | Πάντα `setImageFormat(ImageFormat.PNG)` για lossless έξοδο· απέφυγε JPEG για πίνακες με πολύ κείμενο. |
| **File path not writable** | `IOException` στο `toImage` | Βεβαιώσου ότι ο φάκελος υπάρχει (`new File(outputPath).getParentFile().mkdirs()`). |

## Pro Tip: Export to a Byte Array for Web Apps

Αν χτίζεις μια web υπηρεσία που επιστρέφει το PNG απευθείας στον browser, μπορείς να γράψεις σε ένα `ByteArrayOutputStream` αντί για αρχείο:

```java
ByteArrayOutputStream baos = new ByteArrayOutputStream();
pivotTable.toImage(baos, imgOptions);
byte[] pngBytes = baos.toByteArray();
// Send pngBytes as HTTP response with Content-Type: image/png
```

Αυτό αφαιρεί την ανάγκη για προσωρινά αρχεία και επιταχύνει την απόκριση.

---

## Full Working Example (All Steps Combined)

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑αντιγραφή‑και‑επικόλληση πρόγραμμα που περιλαμβάνει όλες τις βέλτιστες πρακτικές που συζητήθηκαν.

```java
import com.aspose.cells.*;
import java.io.*;

public class PivotTableExporter {

    public static void main(String[] args) {
        // 1️⃣ Load workbook
        Workbook workbook;
        try {
            workbook = new Workbook("C:/data/report.xlsx");
        } catch (Exception e) {
            System.err.println("Failed to load workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Get first worksheet and ensure a pivot exists
        if (workbook.getWorksheets().getCount() == 0) {
            System.out.println("Workbook contains no worksheets.");
            return;
        }
        Worksheet ws = workbook.getWorksheets().get(0);
        if (ws.getPivotTables().getCount() == 0) {
            System.out.println("No pivot tables on the first sheet.");
            return;
        }
        PivotTable pivotTable = ws.getPivotTables().get(0); // export pivot table

        // 3️⃣ Configure export options – set png format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.PNG); // <-- set png format
        imgOptions.setOnePagePerSheet(true);
        imgOptions.setTransparent(true);

        // 4️⃣ Prepare output directory
        String outDir = "C:/exports";
        new File(outDir).mkdirs(); // create if missing

        // 5️⃣ Export the image
        String outPath = outDir + "/pivot.png";
        try {
            pivotTable.toImage(outPath, imgOptions);
            System.out.println("Pivot table exported successfully to: " + outPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

Η εκτέλεση αυτής της κλάσης θα δημιουργήσει το `pivot.png` μέσα στο `C:/exports`. Άνοιξε το αρχείο και θα δεις μια ακριβή οπτική αναπαράσταση του αρχικού πίνακα pivot – ιδανική για ενσωμάτωση σε αναφορές, email ή ιστοσελίδες.

![Exported pivot table saved as PNG – example of an excel pivot image](https://example.com/images/pivot-export.png "παράδειγμα εξαγωγής πίνακα pivot")

*Image alt text:* **παράδειγμα εξαγωγής πίνακα pivot που δείχνει μια εικόνα PNG πίνακα pivot Excel**

---

## Conclusion

Μόλις σου δείξαμε πώς να **εξάγεις δεδομένα πίνακα pivot** από το Excel σε PNG υψηλής ποιότητας χρησιμοποιώντας Java. Τα βασικά βήματα είναι η φόρτωση του βιβλίου εργασίας, ο εντοπισμός του pivot, η ρύθμιση του `ImageOrPrintOptions` για **ορισμό μορφής PNG**, και τέλος η κλήση του `toImage`.  

Με αυτή τη γνώση μπορείς τώρα να αυτοματοποιήσεις τη δημιουργία αναφορών, να ενσωματώνεις στιγμιότυπα pivot σε dashboards, ή να τα σερβίρεις απευθείας από ένα web API. Στο επόμενο βήμα μπορείς να εξερευνήσεις επιλογές κλιμάκωσης **excel pivot image**, να προσθέσεις υδατογραφήματα, ή ακόμη και να μετατρέψεις το PNG σε PDF για εκτυπώσιμες αναφορές.  

Έχεις ερωτήσεις σχετικά με τη διαχείριση μεγαλύτερων βιβλίων εργασίας ή την ενσωμάτωση με Spring Boot; Άφησε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

## What Should You Learn Next?

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σε βοηθήσουν να κυριαρχήσεις πρόσθετα χαρακτηριστικά του API και να εξερευνήσεις εναλλακτικές προσεγγίσεις στα δικά σου έργα.

- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Automate Excel Pivot Table Styling and Saving with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-styling-saving-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}