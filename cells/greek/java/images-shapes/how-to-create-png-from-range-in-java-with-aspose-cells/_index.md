---
category: general
date: 2026-10-07
description: Μάθετε πώς να δημιουργήσετε PNG από περιοχή και να εξάγετε δεδομένα ως
  PNG σε Java. Αυτός ο οδηγός σας δείχνει πώς να αποθηκεύσετε την εικόνα περιοχής
  του Excel χρησιμοποιώντας το Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create png from range
- export data as png
- save excel range image
- convert worksheet to png
- save cells as png
language: el
lastmod: 2026-10-07
og_description: Δημιουργήστε PNG από περιοχή σε Java και εξάγετε τα δεδομένα ως PNG
  με το Aspose.Cells. Ακολουθήστε αυτό το πλήρες σεμινάριο για να αποθηκεύσετε αμέσως
  την εικόνα της περιοχής του Excel.
og_image_alt: Screenshot of Java code that creates a PNG from an Excel range
og_title: Δημιουργία PNG από περιοχή σε Java – βήμα‑βήμα οδηγός Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  headline: How to create PNG from range in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  name: How to create PNG from range in Java with Aspose.Cells
  steps:
  - name: Maven dependency
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-cells</artifactId>
      <version>23.12</version> </dependency> ```'
  - name: Expected output
    text: '* A file named `PivotImage.png` located in `YOUR_DIRECTORY`. * The image
      shows the exact layout, fonts, colors, and borders from the selected range.
      * If the source range contains a pivot table, the rendered image includes the
      same styling and calculated values as displayed in Excel.'
  - name: Exporting a non‑contiguous range
    text: Aspose.Cells does not render disjoint ranges in a single image. To export
      multiple areas, create separate images for each range and combine them later
      with an image‑processing library (e.g., ImageIO).
  - name: Saving a large worksheet as PNG
    text: 'Rendering an entire sheet that spans thousands of rows can consume significant
      memory. Mitigate this by:'
  - name: Preserving cell formulas
    text: A PNG image is a raster format; formulas are not retained. If downstream
      consumers need the raw data, also export the range as CSV or JSON using `Range.exportDataTable()`.
  - name: Next steps
    text: '* Experiment with different `Resolution` values to balance quality and
      file size. * Use `ImageOrPrintOptions.setTransparent(true)` if you need a PNG
      with a transparent background. * Combine multiple range images into a single
      PDF using `PdfSaveOptions` for multi‑page reports. * Explore exporting to '
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Πώς να δημιουργήσετε PNG από περιοχή σε Java με το Aspose.Cells
url: /el/java/images-shapes/how-to-create-png-from-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε PNG από περιοχή σε Java με Aspose.Cells

Αν χρειάζεστε **να δημιουργήσετε PNG από περιοχή** σε ένα βιβλίο εργασίας Excel, αυτό το tutorial σας δείχνει ακριβώς πώς να το κάνετε. Στο τέλος του οδηγού θα μπορείτε να **εξάγετε δεδομένα ως PNG**, να αποθηκεύσετε μια εικόνα περιοχής Excel και να επαναχρησιμοποιήσετε το αρχείο σε αναφορές ή ιστοσελίδες.

Θα δείτε ένα πλήρες, εκτελέσιμο πρόγραμμα Java που φορτώνει ένα βιβλίο εργασίας, επιλέγει τα επιθυμητά κελιά, τα αποδίδει ως PNG και αποθηκεύει το αποτέλεσμα στο δίσκο. Δεν απαιτούνται εξωτερικά εργαλεία — το Aspose.Cells διαχειρίζεται τα πάντα εσωτερικά.

## Τι καλύπτει αυτό το tutorial

* Προαπαιτούμενα και ρύθμιση Maven για Aspose.Cells
* Φόρτωση βιβλίου εργασίας που περιέχει πίνακα Pivot ή οποιαδήποτε περιοχή δεδομένων
* Ορισμός της ακριβούς περιοχής κελιών που θέλετε να μετατρέψετε
* Διαμόρφωση επιλογών εικόνας για έξοδο PNG
* Απόδοση της περιοχής και αποθήκευση του αρχείου PNG
* Κοινά προβλήματα και συμβουλές για εικόνες υψηλής ποιότητας

Μετά την ολοκλήρωση αυτών των βημάτων, θα μπορείτε να **μετατρέψετε φύλλο εργασίας σε PNG** για οποιαδήποτε περιοχή, είτε πρόκειται για απλός πίνακα είτε για πολύπλοκο γράφημα Pivot.

## Προαπαιτούμενα

* Java 17 ή νεότερη (ο κώδικας μεταγλωττίζεται με JDK 11+)
* Maven 3.6+ (ή Gradle αν προτιμάτε)
* Aspose.Cells for Java 23.12 ή νεότερη – προσθέστε την εξάρτηση που φαίνεται παρακάτω
* Ένα υπάρχον αρχείο Excel (`PivotWithStyle.xlsx`) που περιέχει την περιοχή που θέλετε να καταγράψετε

> **Pro tip:** Αν δεν έχετε άδεια, μπορείτε να ζητήσετε ένα προσωρινό κλειδί αξιολόγησης από το Aspose. Η βιβλιοθήκη λειτουργεί σε λειτουργία αξιολόγησης χωρίς πρόσθετη διαμόρφωση.

### Maven dependency

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

## Βήμα 1: Φόρτωση του βιβλίου εργασίας που περιέχει την επιθυμητή περιοχή

Η πρώτη ενέργεια είναι το άνοιγμα του αρχείου Excel. Το Aspose.Cells διαβάζει το αρχείο στη μνήμη χωρίς να απαιτεί Microsoft Office.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the data you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");
```

*Γιατί είναι σημαντικό*: Η φόρτωση του βιβλίου εργασίας σας δίνει πρόσβαση στα φύλλα εργασίας, τα κελιά και τις ιδιότητες ρύθμισης σελίδας που απαιτούνται για την απόδοση.

## Βήμα 2: Πρόσβαση στο φύλλο εργασίας που περιέχει την περιοχή

Τα περισσότερα βιβλία εργασίας έχουν προεπιλεγμένο φύλλο στο δείκτη 0, αλλά μπορείτε επίσης να χρησιμοποιήσετε το όνομα του φύλλου.

```java
        // Retrieve the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Αν τα δεδομένα σας βρίσκονται σε διαφορετικό φύλλο, αντικαταστήστε το `0` με τον κατάλληλο δείκτη ή χρησιμοποιήστε `workbook.getWorksheets().get("SheetName")`.

## Βήμα 3: Ορισμός της περιοχής κελιών που θέλετε να μετατρέψετε

Μπορείτε να ορίσετε οποιαδήποτε ορθογώνια περιοχή χρησιμοποιώντας τη σημειογραφία A1. Σε αυτό το παράδειγμα καταγράφουμε το `A1:D15`, το οποίο μπορεί να είναι πίνακας Pivot ή ένα κανονικό μπλοκ δεδομένων.

```java
        // Create a range object for cells A1:D15
        Range pivotRange = worksheet.getCells().createRange("A1:D15");
```

*Περίπτωση άκρης*: Όταν η περιοχή περιλαμβάνει συγχωνευμένα κελιά, το Aspose.Cells επεκτείνει αυτόματα την εικόνα ώστε να συμπεριλάβει την συγχωνευμένη περιοχή.

## Βήμα 4: Προετοιμασία επιλογών εικόνας PNG

`ImageOrPrintOptions` σας επιτρέπει να ελέγχετε τη μορφή, την ανάλυση και άλλες λεπτομέρειες απόδοσης. Ορίζοντας τη μορφή αποθήκευσης σε PNG εξασφαλίζει ποιότητα χωρίς απώλειες.

```java
        // Configure image options – we want a PNG file
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        // Optional: increase DPI for sharper output (default is 96)
        imageOptions.setImageFormat(ImageFormat.getPng());
        imageOptions.setResolution(150); // 150 DPI for clearer text
```

Η αύξηση του DPI είναι χρήσιμη όταν τα κελιά προέλευσης περιέχουν μικρές γραμματοσειρές ή λεπτομερή γραφήματα.

## Βήμα 5: Περιορισμός της περιοχής απόδοσης στην επιλεγμένη περιοχή

Αναθέτοντας την περιοχή ως περιοχή εκτύπωσης, το Aspose.Cells αποδίδει μόνο αυτά τα κελιά και αγνοεί το υπόλοιπο του φύλλου.

```java
        // Set the print area so only the defined range is rendered
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());
```

Αν παραλείψετε αυτό το βήμα, ολόκληρο το φύλλο εργασίας θα μετατραπεί σε raster, κάτι που μπορεί να σπαταλήσει μνήμη και να δημιουργήσει μεγαλύτερη εικόνα.

## Βήμα 6: Απόδοση της περιοχής και προσθήκη της εικόνας στο φύλλο εργασίας (προαιρετικό)

Αν θέλετε να ενσωματώσετε το παραγόμενο PNG πίσω στο βιβλίο εργασίας (για σκοπούς προεπισκόπησης), μπορείτε να το προσθέσετε ως εικόνα. Αυτό το βήμα είναι προαιρετικό για καθαρά σενάρια εξαγωγής.

```java
        // Add the rendered image back to the worksheet at cell (0,0) – optional
        worksheet.getPictures().add(0, 0, imageOptions);
```

*Γιατί μπορεί να το κάνετε αυτό*: Ορισμένες ροές εργασίας απαιτούν η εικόνα να είναι μέρος του βιβλίου εργασίας πριν από τη διανομή, όπως η δημιουργία εκτυπώσιμης αναφοράς που συνδυάζει εγγενή κελιά και εικόνες.

## Βήμα 7: Αποθήκευση του αρχείου PNG στο δίσκο

Τέλος, γράψτε την εικόνα σε αρχείο. Η μέθοδος `save` σέβεται τη μορφή που έχει οριστεί στο `imageOptions`.

```java
        // Save the rendered PNG image to the specified path
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Όταν το πρόγραμμα ολοκληρωθεί, το `PivotImage.png` θα περιέχει ένα pixel‑perfect στιγμιότυπο των κελιών `A1:D15`.

### Αναμενόμενο αποτέλεσμα

* Ένα αρχείο με όνομα `PivotImage.png` τοποθετημένο στο `YOUR_DIRECTORY`.
* Η εικόνα εμφανίζει την ακριβή διάταξη, γραμματοσειρές, χρώματα και περιγράμματα από την επιλεγμένη περιοχή.
* Αν η πηγή περιοχής περιέχει πίνακα Pivot, η αποδοθείσα εικόνα περιλαμβάνει το ίδιο στυλ και τις υπολογισμένες τιμές όπως εμφανίζονται στο Excel.

## Διαχείριση κοινών σεναρίων

### Εξαγωγή μη συνεχούς περιοχής

Το Aspose.Cells δεν αποδίδει διασπασμένες περιοχές σε μία μόνο εικόνα. Για να εξάγετε πολλαπλές περιοχές, δημιουργήστε ξεχωριστές εικόνες για κάθε περιοχή και συνδυάστε τις αργότερα με μια βιβλιοθήκη επεξεργασίας εικόνας (π.χ., ImageIO).

```java
Range first = worksheet.getCells().createRange("A1:B10");
Range second = worksheet.getCells().createRange("D1:E10");
// Render each range individually using the same ImageOrPrintOptions
```

### Αποθήκευση μεγάλου φύλλου εργασίας ως PNG

Η απόδοση ενός ολόκληρου φύλλου που εκτείνεται σε χιλιάδες σειρές μπορεί να καταναλώσει σημαντική μνήμη. Μετριάστε το αυτό με:

* Μείωση του DPI (`imageOptions.setResolution(72)`) για μικρότερο αρχείο.
* Χρήση του `setPageCount` για περιορισμό του αριθμού των σελίδων που αποδίδονται.
* Εξαγωγή μιας εκτυπώσιμης σελίδας τη φορά μέσω `worksheet.getPageSetup().setPrintArea(...)`.

### Διατήρηση τύπων κελιών

Μια εικόνα PNG είναι μορφή raster· οι τύποι δεν διατηρούνται. Αν οι επόμενοι χρήστες χρειάζονται τα ακατέργαστα δεδομένα, εξάγετε επίσης την περιοχή ως CSV ή JSON χρησιμοποιώντας το `Range.exportDataTable()`.

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω βρίσκεται η πλήρης κλάση Java που μπορείτε να αντιγράψετε‑επικολλήσετε στο IDE σας. Αντικαταστήστε το `YOUR_DIRECTORY` με απόλυτη ή σχετική διαδρομή στο σύστημά σας.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the workbook containing the data
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");

        // 2️⃣ Access the first worksheet (adjust index or name as needed)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Define the exact cell range you want to convert (A1:D15 in this case)
        Range pivotRange = worksheet.getCells().createRange("A1:D15");

        // 4️⃣ Prepare PNG image options – set format and optional resolution
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        imageOptions.setResolution(150); // sharper output

        // 5️⃣ Restrict rendering to the selected range
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());

        // 6️⃣ (Optional) Add the rendered image back to the worksheet for preview
        worksheet.getPictures().add(0, 0, imageOptions);

        // 7️⃣ Save the PNG file – this creates the final image on disk
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Εκτελέστε το πρόγραμμα με `mvn compile exec:java` (ή το προτιμώμενο εργαλείο κατασκευής σας). Μετά την εκτέλεση, ανοίξτε το `PivotImage.png` για να επαληθεύσετε το αποτέλεσμα.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **δημιουργήσετε PNG από περιοχή** σε Java χρησιμοποιώντας το Aspose.Cells, αποδίδοντας αποτελεσματικά **εξαγωγή δεδομένων ως PNG** και **αποθήκευση εικόνας περιοχής Excel** για οποιοδήποτε σενάριο αναφοράς ή κοινής χρήσης. Τα βήματα — φόρτωση του βιβλίου εργασίας, ορισμός της περιοχής, διαμόρφωση επιλογών εικόνας, ορισμός της περιοχής εκτύπωσης και αποθήκευση του αρχείου — καλύπτουν ολόκληρη τη ροή εργασίας για **μετατροπή φύλλου εργασίας σε PNG** και **αποθήκευση κελιών ως PNG**.

### Επόμενα βήματα

* Δοκιμάστε διαφορετικές τιμές `Resolution` για να ισορροπήσετε την ποιότητα και το μέγεθος του αρχείου.
* Χρησιμοποιήστε `ImageOrPrintOptions.setTransparent(true)` αν χρειάζεστε PNG με διαφανές φόντο.
* Συνδυάστε πολλαπλές εικόνες περιοχών σε ένα ενιαίο PDF χρησιμοποιώντας το `PdfSaveOptions` για αναφορές πολλαπλών σελίδων.
* Εξερευνήστε την εξαγωγή σε άλλες μορφές raster (JPEG, BMP) αλλάζοντας το `setSaveFormat`.

Μη διστάσετε να προσαρμόσετε αυτό το πρότυπο σε γραφήματα, πίνακες ή ακόμη και ολόκληρα φύλλα εργασίας. Καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σύντομη Μελλοντική;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να εξάγετε ένα φύλλο εργασίας Excel σε PNG χρησιμοποιώντας Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Μετατροπή Excel σε PNG χρησιμοποιώντας Aspose.Cells για Java: Οδηγός βήμα‑βήμα](/cells/english/java/workbook-operations/convert-excel-to-png-aspose-cells-java/)
- [Δημιουργία Ενωμένης Περιοχής σε Excel χρησιμοποιώντας Aspose.Cells Java: Αναλυτικός Οδηγός](/cells/english/java/range-management/create-union-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}