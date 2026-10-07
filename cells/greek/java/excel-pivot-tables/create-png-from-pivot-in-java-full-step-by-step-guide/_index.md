---
category: general
date: 2026-06-18
description: Δημιουργήστε PNG από συγκεντρωτικό πίνακα γρήγορα με Java. Μάθετε πώς
  να εξάγετε εικόνα δεδομένων Excel, να εξάγετε εικόνα συγκεντρωτικού πίνακα και να
  αποθηκεύσετε την περιοχή ως αρχείο PNG.
draft: false
keywords:
- create png from pivot
- export excel data image
- export pivot table image
- export excel range image
- export pivot table file
language: el
og_description: Δημιουργία PNG από pivot σε Java. Αυτός ο οδηγός δείχνει πώς να εξάγετε
  εικόνα δεδομένων Excel, να εξάγετε εικόνα πίνακα pivot και να δημιουργήσετε αρχείο
  PNG από μια περιοχή pivot.
og_title: Δημιουργία PNG από Pivot σε Java – Πλήρης Οδηγός Εξαγωγής
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Create PNG from pivot quickly with Java. Learn how to export Excel
    data image, export pivot table image, and save the range as a PNG file.
  headline: Create PNG from Pivot in Java – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create PNG from pivot quickly with Java. Learn how to export Excel
    data image, export pivot table image, and save the range as a PNG file.
  name: Create PNG from Pivot in Java – Full Step‑by‑Step Guide
  steps:
  - name: '**File exists** – `new File(outputPath).exists()` should return `true`.'
    text: '**File exists** – `new File(outputPath).exists()` should return `true`.'
  - name: '**Image dimensions** – Open the PNG; the width/height should match the
      range’s visual size.'
    text: '**Image dimensions** – Open the PNG; the width/height should match the
      range’s visual size.'
  - name: '**Data fidelity** – Compare a screenshot of the Excel sheet with the PNG;
      they should be identical pixel‑for‑pixel.'
    text: '**Data fidelity** – Compare a screenshot of the Excel sheet with the PNG;
      they should be identical pixel‑for‑pixel.'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Δημιουργία PNG από Pivot σε Java – Πλήρης Οδηγός Βήμα‑προς‑Βήμα
url: /el/java/excel-pivot-tables/create-png-from-pivot-in-java-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία PNG από Pivot σε Java – Πλήρης Οδηγός Βήμα‑βήμα

Έχετε αναρωτηθεί ποτέ πώς να **δημιουργήσετε PNG από pivot** χωρίς να ανοίξετε το Excel χειροκίνητα; Ίσως χρειάζεται να ενσωματώσετε ένα γράφημα pivot σε μια αναφορά, ή να δημιουργείτε έναν πίνακα ελέγχου που αντλεί ζωντανά δεδομένα από ένα αρχείο .xlsx. Τα καλά νέα είναι ότι δεν χρειάζεται να παλέψετε με αντικείμενα COM ή screen‑scraping—η Java μπορεί να το κάνει καθαρά.

Σε αυτό το tutorial θα περάσουμε βήμα προς βήμα από μια πλήρη λύση που **εξάγει μια εικόνα περιοχής Excel**, συγκεκριμένα έναν πίνακα pivot, σε αρχείο PNG. Θα δείτε ακριβώς πώς να **εξάγετε εικόνα δεδομένων Excel**, γιατί το `ImageOrPrintOptions` είναι σημαντικό, και τι πρέπει να προσέξετε όταν **εξάγετε αρχείο πίνακα pivot**. Στο τέλος θα έχετε ένα έτοιμο προς εκτέλεση πρόγραμμα Java που γράφει το `pivot.png` ακριβώς δίπλα στο βιβλίο εργασίας σας.

## Προαπαιτούμενα

- Java 17 (ή οποιοδήποτε πρόσφατο JDK) – ο κώδικας χρησιμοποιεί τις τυπικές δυνατότητες της γλώσσας, χωρίς ανάγκη για lambdas.
- Βιβλιοθήκη Aspose.Cells for Java (δωρεάν δοκιμή ή επί πληρωμή άδεια). Προσθέστε την εξάρτηση Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version>
</dependency>
```

- Ένα βιβλίο εργασίας Excel (`pivots.xlsx`) που περιέχει ήδη τουλάχιστον έναν πίνακα pivot.
- Βασική εξοικείωση με τις μεθόδους `main` της Java· δεν απαιτούνται επιπλέον frameworks.

> **Συμβουλή επαγγελματία:** Αν χρησιμοποιείτε Gradle, αντικαταστήστε το απόσπασμα XML με `implementation "com.aspose:aspose-cells:24.9"`.

## Βήμα 1: Φόρτωση του Βιβλίου Εργασίας που Περιέχει τον Πίνακα Pivot

Το πρώτο που κάνουμε είναι να ανοίξουμε το βιβλίο εργασίας. Η Aspose.Cells αφαιρεί τη χαμηλού επιπέδου διαχείριση αρχείων, έτσι μια μόνο γραμμή σας παρέχει ένα πλήρες αντικείμενο `Workbook`.

```java
import com.aspose.cells.*;

public class ExportPivotToPng {
    public static void main(String[] args) throws Exception {
        // Adjust the path to point at your actual file location
        String workbookPath = "YOUR_DIRECTORY/pivots.xlsx";
        Workbook workbook = new Workbook(workbookPath);
```

> **Γιατί είναι σημαντικό:** Η φόρτωση του βιβλίου εργασίας επικυρώνει τη μορφή του αρχείου και προετοιμάζει το εσωτερικό μοντέλο, κάτι που είναι απαραίτητο πριν μπορέσετε να ερωτήσετε οποιονδήποτε πίνακα pivot.

## Βήμα 2: Πρόσβαση στο Πρώτο Φύλλο Εργασίας

Οι περισσότερες λογιστικές φύλλα διατηρούν τα pivots στο πρώτο φύλλο, αλλά μπορείτε να αλλάξετε το δείκτη αν χρειάζεται. Εδώ απλώς ανακτούμε το πρώτο φύλλο εργασίας.

```java
        // Grab the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
```

> **Περίπτωση άκρης:** Αν το βιβλίο εργασίας σας περιέχει κρυφά φύλλα, η Aspose τα επιστρέφει ακόμη· ίσως χρειαστεί να ελέγξετε `sheet.isVisible()` πριν προχωρήσετε.

## Βήμα 3: Ανάκτηση της Περιοχής που Καλύπτει ο Πρώτος Πίνακας Pivot

Τώρα έρχεται η καρδιά της λειτουργίας: η εντοπισμός της περιοχής του πίνακα pivot. Η συλλογή `getPivotTables()` μας επιτρέπει να επιλέξουμε το pivot που θέλουμε, μετά το `getRange()` επιστρέφει ένα αντικείμενο `Range` που αντιπροσωπεύει τα ακριβή κελιά.

```java
        // Assume the workbook has at least one pivot table
        PivotTable pivot = sheet.getPivotTables().get(0);
        Range pivotRange = pivot.getRange();
```

> **Γιατί αυτό το βήμα είναι κρίσιμο:** Το αντικείμενο `Range` γνωρίζει τις διαστάσεις, τη μορφοποίηση και τα δεδομένα του pivot. Όταν αργότερα καλέσουμε `toImage`, χρησιμοποιεί αυτά τα μεταδεδομένα για να αποδώσει ένα pixel‑perfect PNG.

## Βήμα 4: Διαμόρφωση Επιλογών Εξαγωγής Εικόνας – Μορφή PNG

Η Aspose σας παρέχει λεπτομερή έλεγχο της εικόνας εξόδου: DPI, κλίμακα, περιθώρια και φυσικά τη μορφή αρχείου. Επειδή θέλουμε PNG, ορίζουμε `ImageFormat.PNG`. Μπορείτε επίσης να ρυθμίσετε `setTransparent(true)` αν χρειάζεστε κανάλι άλφα.

```java
        // Set up export options for a high‑quality PNG
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setImageFormat(ImageFormat.PNG);
        // Optional: increase resolution for sharper output
        options.setResolution(300);
```

> **Συχνή ερώτηση:** *Μπορώ να εξάγω σε JPEG ή BMP αντί για αυτό;* Ναι—απλώς αντικαταστήστε το `ImageFormat.PNG` με `ImageFormat.JPEG` ή `ImageFormat.BMP`.

## Βήμα 5: Εξαγωγή της Περιοχής του Πίνακα Pivot σε Αρχείο Εικόνας

Τέλος, καλούμε το `toImage` στο `Range`. Η μέθοδος παίρνει τη διαδρομή προορισμού και τις επιλογές που μόλις διαμορφώσαμε. Η λειτουργία γράφει το αρχείο στο δίσκο με μία μόνο γραμμή.

```java
        // Define the output file path
        String outputPath = "YOUR_DIRECTORY/pivot.png";

        // Export the pivot range as a PNG image
        pivotRange.toImage(outputPath, options);

        System.out.println("Pivot table exported successfully to " + outputPath);
    }
}
```

> **Αναμενόμενο αποτέλεσμα:** Μετά την εκτέλεση του προγράμματος, θα δείτε το `pivot.png` στον καθορισμένο φάκελο. Ανοίξτε το με οποιονδήποτε προβολέα εικόνας και θα πρέπει να δείτε την ακριβή διάταξη του αρχικού πίνακα pivot του Excel, συμπεριλαμβανομένων των κεφαλίδων στηλών, των γραμμών υποσυνολικών και τυχόν εφαρμοσμένων στυλ.

## Επαλήθευση του Αποτελέσματος – Γρήγορη Λίστα Ελέγχου

1. **Το αρχείο υπάρχει** – `new File(outputPath).exists()` πρέπει να επιστρέφει `true`.
2. **Διαστάσεις εικόνας** – Ανοίξτε το PNG· το πλάτος/ύψος πρέπει να ταιριάζει με το οπτικό μέγεθος της περιοχής.
3. **Ακρίβεια δεδομένων** – Συγκρίνετε ένα στιγμιότυπο της σελίδας Excel με το PNG· πρέπει να είναι ταυτόσημα pixel‑for‑pixel.

Αν κάποιος από αυτούς τους ελέγχους αποτύχει, ελέγξτε ξανά ότι η διαδρομή του βιβλίου εργασίας είναι σωστή και ότι ο πίνακας pivot δεν είναι κρυμμένος ή φιλτραρισμένος.

## Εξαγωγή Εικόνας Περιοχής Excel vs. Εξαγωγή Εικόνας Πίνακα Pivot

Μπορεί να αναρωτιέστε αν υπάρχει διαφορά μεταξύ **export excel range image** και **export pivot table image**. Στην πράξη:

| Στόχος | Μέθοδος | Τυπική Χρήση‑Περίπτωση |
|--------|---------|------------------------|
| Εξαγωγή οποιασδήποτε αυθαίρετης περιοχής (π.χ., A1:D20) | `sheet.getCells().createRange("A1:D20").toImage(...)` | Καταγραφή μιας στατικής περιοχής πίνακα ή γραφήματος |
| Εξαγωγή ενός πίνακα pivot συγκεκριμένα | `pivot.getRange().toImage(...)` | Διατήρηση της δυναμικής διάταξης, των υποσυνολικών και των φίλτρων |

Και οι δύο προσεγγίσεις χρησιμοποιούν το ίδιο API `toImage`; το κλειδί είναι η επιλογή του σωστού αντικειμένου `Range`. Όταν **εξάγετε αρχείο πίνακα pivot** ουσιαστικά αποθηκεύετε την οπτική αναπαράσταση αντί για τα ίδια τα δεδομένα.

## Διαχείριση Πολλαπλών Πινάκων Pivot

Αν το βιβλίο εργασίας σας περιέχει πολλαπλά pivots, απλώς κάντε επανάληψη πάνω στη συλλογή:

```java
        for (int i = 0; i < sheet.getPivotTables().getCount(); i++) {
            PivotTable pt = sheet.getPivotTables().get(i);
            String out = "YOUR_DIRECTORY/pivot_" + i + ".png";
            pt.getRange().toImage(out, options);
            System.out.println("Exported pivot #" + i + " to " + out);
        }
```

> **Γιατί επανάληψη;** Οι αυτοματοποιημένες γραμμές αναφοράς συχνά χρειάζονται να δημοσιεύσουν κάθε pivot σε ένα βιβλίο εργασίας. Η επανάληψη κάνει τη λύση επεκτάσιμη χωρίς επιπλέον κώδικα.

## Συνηθισμένα Πιθανά Προβλήματα και Πώς να τα Αποφύγετε

- **Λείπει άδεια** – Χωρίς έγκυρη άδεια Aspose.Cells η βιβλιοθήκη θα προσθέσει υδατογράφημα στο PNG. Καταχωρίστε την άδειά σας νωρίς: `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`.
- **Μεγάλα pivots προκαλούν πίεση μνήμης** – Αν το pivot καλύπτει χιλιάδες γραμμές, σκεφτείτε να αυξήσετε τη μνήμη heap της JVM (`-Xmx2g`) ή να εξάγετε σε ενότητες.
- **Λάθος μορφή εικόνας** – Η χρήση `ImageFormat.JPEG` ενώ αναμένετε διαφάνεια θα έχει ως αποτέλεσμα ένα στερεό φόντο. Παραμείνετε στο PNG όταν χρειάζεστε άλφα.

## Bonus: Εξαγωγή σε Byte Array για Web APIs

Μερικές φορές δεν θέλετε αρχείο στον δίσκο· χρειάζεστε τα bytes της εικόνας για αποστολή μέσω HTTP. Αντικαταστήστε την κλήση που βασίζεται σε αρχείο με ένα `MemoryStream` (το `ByteArrayOutputStream` της Aspose):

```java
        java.io.ByteArrayOutputStream stream = new java.io.ByteArrayOutputStream();
        pivotRange.toImage(stream, options);
        byte[] pngBytes = stream.toByteArray();
        // Now you can return pngBytes from a REST endpoint
```

> **Σενάριο πραγματικού κόσμου:** Ένας ελεγκτής Spring Boot μπορεί να επιστρέψει `ResponseEntity<byte[]>` με `Content-Type: image/png`, επιτρέποντας στα προγράμματα περιήγησης να εμφανίσουν το pivot άμεσα.

## Συμπέρασμα

Τώρα γνωρίζετε ακριβώς πώς να **δημιουργήσετε PNG από pivot** χρησιμοποιώντας Java και Aspose.Cells. Το tutorial κάλυψε τα πάντα, από τη φόρτωση του βιβλίου εργασίας, τον εντοπισμό της περιοχής pivot, τη διαμόρφωση επιλογών εξαγωγής PNG, και τελικά τη γραφή του αρχείου εικόνας. Εξερευνήσαμε επίσης συναφείς εργασίες όπως **export excel data image**, **export pivot table image**, και ακόμη πώς να **export excel range image** για μη‑pivot τμήματα.

Επόμενα βήματα; Δοκιμάστε να προσθέσετε προσαρμοσμένο στυλ στο PNG (π.χ., ορίζοντας χρώμα φόντου), ή ενσωματώστε τη διαδικασία εξαγωγής σε μια μεγαλύτερη εργασία batch που επεξεργάζεται δεκάδες βιβλία εργασίας κάθε βράδυ. Μπορείτε επίσης να πειραματιστείτε με άλλες μορφές εξόδου—PDF, SVG ή ακόμη και multi‑page TIFF—αλλάζοντας το enum `ImageFormat`.

Έχετε ερωτήσεις σχετικά με περιπτώσεις άκρης, άδειες ή βελτιστοποίηση απόδοσης; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Βιβλίου Εργασίας Excel ως Εικόνα Χρησιμοποιώντας Aspose.Cells για Java: Οδηγός Βήμα‑βήμα](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Προσαρμογή Παγκοσμιοποίησης Πίνακα Pivot & Εξαγωγή PDF σε Java με Aspose.Cells](/cells/english/java/data-analysis/customize-pivot-table-globalization-pdf-export-java/)
- [Πώς να Διαχειριστείτε τη Συμβατότητα Πίνακα Pivot Excel με Aspose.Cells για .NET | Οδηγός Ανάλυσης Δεδομένων](/cells/english/net/data-analysis/manage-excel-pivot-table-compatibility-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}