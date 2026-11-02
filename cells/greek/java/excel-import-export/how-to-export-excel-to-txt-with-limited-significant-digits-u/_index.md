---
category: general
date: 2026-08-17
description: Εξαγωγή Excel σε TXT με περιορισμό των σημαντικών ψηφίων – μάθετε πώς
  να ορίζετε τα ψηφία και να μετατρέπετε το Excel σε κείμενο σε Java με ένα πλήρες
  παράδειγμα Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- how to set digits
- convert excel to text
- how to limit decimals
- limit significant digits
language: el
lastmod: 2026-08-17
og_description: Εξαγωγή Excel σε TXT με περιορισμό των σημαντικών ψηφίων. Αυτό το
  εκπαιδευτικό δείχνει πώς να ορίσετε τα ψηφία και να μετατρέψετε το Excel σε κείμενο
  χρησιμοποιώντας το Aspose.Cells για Java.
og_image_alt: Java code exporting Excel to TXT with 4 significant digits
og_title: Εξαγωγή Excel σε TXT με περιορισμένα σημαντικά ψηφία – Οδηγός Java
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  headline: How to export Excel to TXT with limited significant digits using Java
  type: TechArticle
- description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  name: How to export Excel to TXT with limited significant digits using Java
  steps:
  - name: Prerequisites
    text: '- Java 17 or later (the code compiles with Java 8 as well). - Aspose.Cells
      for Java 25.10 or newer. Download the JAR from the [Aspose website](https://products.aspose.com/cells/java)
      and add it to your project’s classpath. - An IDE or a simple text editor and
      command‑line build tool (Maven/Gradle).'
  - name: How the setting differs from “limit decimals”
    text: '- **limit decimals** (`setDecimalPlaces`) trims digits *after* the decimal
      point, regardless of the integer part. - **significant digits** (`setSignificantDigits`)
      counts digits from the first non‑zero digit, which is useful when numbers vary
      in magnitude.'
  - name: Expected output
    text: '| Cell | Original value | Exported (4 significant digits) | |------|----------------|---------------------------------|
      | A1 | 123.456789 | 123.5 |'
  - name: Exporting a whole range
    text: 'If you want to export more than one cell, simply fill the range before
      saving:'
  - name: Handling locale‑specific decimal separators
    text: 'Aspose.Cells respects the system locale when writing text. To force a dot
      (`.`) as the decimal separator, set the `TxtSaveOptions` culture:'
  - name: Overwriting existing files
    text: 'The `save` method overwrites the target file by default. If you need to
      avoid accidental data loss, check for file existence first:'
  - name: Large workbooks and memory usage
    text: 'When exporting very large worksheets, consider streaming the output:'
  - name: Next steps
    text: "- Explore other `TxtSaveOptions` properties such as `setDelimiter('\t')`
      to customize column separators. - Combine the exporter with `CsvSaveOptions`
      if you need comma‑separated values instead of plain text. - Integrate the routine
      into a web service that accepts uploaded Excel files and returns tri"
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel export
- TXT conversion
title: Πώς να εξάγετε το Excel σε TXT με περιορισμένα σημαντικά ψηφία χρησιμοποιώντας
  Java
url: /el/java/excel-import-export/how-to-export-excel-to-txt-with-limited-significant-digits-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Excel σε TXT με περιορισμένο αριθμό σημαντικών ψηφίων χρησιμοποιώντας Java

Αν χρειάζεστε **εξαγωγή Excel σε TXT** ενώ ελέγχετε τον αριθμό των σημαντικών ψηφίων, αυτός ο οδηγός παρέχει μια έτοιμη προς εκτέλεση λύση. Θα δείτε πώς να ορίσετε τα ψηφία, να μετατρέψετε το Excel σε κείμενο και να διατηρήσετε το αποτέλεσμα καθαρό με μια μόνο αλλαγή ρύθμισης.

Το παράδειγμα χρησιμοποιεί το Aspose.Cells for Java 25.10, το οποίο εισάγει την επιλογή `setSignificantDigits`. Στο τέλος του οδηγού θα μπορείτε να δημιουργήσετε ένα αρχείο TXT που περιέχει μόνο τα ψηφία που θέλετε, χωρίς πρόσθετο κώδικα στρογγυλοποίησης.

## Τι θα επιτύχετε

- Δημιουργία βιβλίου εργασίας προγραμματιστικά.
- Εισαγωγή αριθμητικής τιμής σε κελί.
- Διαμόρφωση επιλογών αποθήκευσης TXT για περιορισμό των σημαντικών ψηφίων.
- Αποθήκευση του βιβλίου εργασίας ως αρχείο απλού κειμένου.
- Κατανόηση του τρόπου λειτουργίας της ρύθμισης `significantDigits` και πώς να την προσαρμόσετε σε άλλες περιπτώσεις.

### Προαπαιτούμενα

- Java 17 ή νεότερη (ο κώδικας μεταγλωττίζεται επίσης με Java 8).
- Aspose.Cells for Java 25.10 ή νεότερη. Κατεβάστε το JAR από την [ιστοσελίδα Aspose](https://products.aspose.com/cells/java) και προσθέστε το στο classpath του έργου σας.
- Ένα IDE ή ένας απλός επεξεργαστής κειμένου και εργαλείο κατασκευής γραμμής εντολών (Maven/Gradle).

## Βήμα 1: Ρύθμιση του έργου και εισαγωγή του Aspose.Cells

Δημιουργήστε ένα νέο έργο Java και προσθέστε το JAR του Aspose.Cells στο μονοπάτι κατασκευής. Εάν χρησιμοποιείτε Maven, προσθέστε την ακόλουθη εξάρτηση στο `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Συμβουλή:** Χρησιμοποιήστε τον ταξινομητή `jdk17` για το πιο πρόσφατο runtime της Java· μειώνει τον κίνδυνο προειδοποιήσεων συμβατότητας.

## Βήμα 2: Δημιουργία βιβλίου εργασίας και εγγραφή τιμής

Το βιβλίο εργασίας αντιπροσωπεύει ένα αρχείο Excel στη μνήμη. Μπορείτε να προσθέσετε δεδομένα σε οποιοδήποτε κελί χρησιμοποιώντας τη μέθοδο `putValue`.

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Put a numeric value into cell A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue(123.456789);
```

Ο αριθμός `123.456789` θα είναι η πηγή για την εξαγωγή μας σε TXT. Από προεπιλογή, το Aspose.Cells θα γράψει όλα τα δεκαδικά ψηφία, κάτι που συχνά παράγει θορυβώδη αρχεία κειμένου.

## Βήμα 3: Διαμόρφωση επιλογών αποθήκευσης TXT για περιορισμό των σημαντικών ψηφίων

Το Aspose.Cells παρέχει το `TxtSaveOptions` για λεπτομερή έλεγχο της εξόδου απλού κειμένου. Η μέθοδος `setSignificantDigits` λέει στον εξαγωγέα πόσα ψηφία να διατηρήσει **συνολικά**, όχι μόνο μετά το δεκαδικό σημείο.

```java
        // Configure TXT save options to keep only 4 significant digits
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4); // new option in 25.10
```

Όταν το `significantDigits` οριστεί σε `4`, ο εξαγωγέας στρογγυλοποιεί την τιμή `123.456789` σε `123.5`. Αυτή η συμπεριφορά ταιριάζει με τον μαθηματικό ορισμό των σημαντικών ψηφίων: τα πρώτα τέσσερα μη μηδενικά ψηφία διατηρούνται.

### Πώς η ρύθμιση διαφέρει από το “περιορισμό δεκαδικών”

- **limit decimals** (`setDecimalPlaces`) κόβει ψηφία *μετά* το δεκαδικό σημείο, ανεξάρτητα από το ακέραιο μέρος.
- **significant digits** (`setSignificantDigits`) μετρά ψηφία από το πρώτο μη μηδενικό ψηφίο, κάτι που είναι χρήσιμο όταν οι αριθμοί διαφέρουν σε μέγεθος.

Αν χρειάζεστε σταθερό αριθμό δεκαδικών ψηφίων, αντικαταστήστε τη γραμμή παραπάνω με:

```java
saveOptions.setDecimalPlaces(2); // keeps two digits after the decimal point
```

## Βήμα 4: Αποθήκευση του βιβλίου εργασίας ως αρχείο TXT

Τώρα γράψτε το βιβλίο εργασίας στο δίσκο χρησιμοποιώντας τις ρυθμισμένες επιλογές.

```java
        // Save the workbook as a TXT file using the configured options
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

Η εκτέλεση του προγράμματος δημιουργεί το `significant_digits.txt` στον τρέχοντα φάκελο. Το αρχείο περιέχει μία μόνο γραμμή:

```
123.5
```

### Αναμενόμενη έξοδος

| Κελί | Αρχική τιμή | Εξαγόμενο (4 σημαντικά ψηφία) |
|------|------------|------------------------------|
| A1   | 123.456789 | 123.5                        |

Αν αλλάξετε το `setSignificantDigits(4)` σε `6`, η έξοδος γίνεται `123.457`. Πειραματιστείτε με διαφορετικές τιμές για να δείτε πώς προσαρμόζεται η στρογγυλοποίηση.

## Βήμα 5: Συνηθισμένες παραλλαγές και ειδικές περιπτώσεις

### Εξαγωγή ολόκληρης περιοχής

Αν θέλετε να εξάγετε περισσότερα από ένα κελιά, απλώς γεμίστε την περιοχή πριν την αποθήκευση:

```java
worksheet.getCells().get("B1").putValue(0.0012345);
worksheet.getCells().get("C1").putValue(98765.4321);
```

Η ίδια ρύθμιση `significantDigits` εφαρμόζεται σε κάθε αριθμητικό κελί, εξασφαλίζοντας συνεπή ακρίβεια σε όλο το αρχείο.

### Διαχείριση διαχωριστών δεκαδικών ανάλογα με την τοπική ρύθμιση

Το Aspose.Cells σέβεται την τοπική ρύθμιση του συστήματος κατά τη γραφή κειμένου. Για να εξαναγκάσετε την τελεία (`.`) ως διαχωριστή δεκαδικών, ορίστε την πολιτιστική ρύθμιση του `TxtSaveOptions`:

```java
saveOptions.setCultureInfo(java.util.Locale.US);
```

Αυτό είναι χρήσιμο όταν η εφαρμογή-στόχος αναμένει συγκεκριμένη μορφή, όπως αναλυτές CSV που δέχονται μόνο `.`.

### Αντικατάσταση υπαρχόντων αρχείων

Η μέθοδος `save` αντικαθιστά το αρχείο προορισμού από προεπιλογή. Εάν χρειάζεται να αποφύγετε τυχαία απώλεια δεδομένων, ελέγξτε πρώτα αν το αρχείο υπάρχει:

```java
java.io.File outFile = new java.io.File("significant_digits.txt");
if (outFile.exists()) {
    throw new IllegalStateException("File already exists. Choose a different name or delete the existing file.");
}
workbook.save(outFile.getPath(), saveOptions);
```

### Μεγάλα βιβλία εργασίας και χρήση μνήμης

Κατά την εξαγωγή πολύ μεγάλων φύλλων εργασίας, σκεφτείτε τη ροή εξόδου:

```java
saveOptions.setEnableMemorySaving(true);
```

Αυτή η επιλογή μειώνει την κατανάλωση heap γράφοντας τις σειρές σταδιακά.

## Πλήρες λειτουργικό παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε, επικολλήσετε και εκτελέσετε αμέσως:

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 2: Put numeric values into cells
        worksheet.getCells().get("A1").putValue(123.456789);
        worksheet.getCells().get("B1").putValue(0.0012345);
        worksheet.getCells().get("C1").putValue(98765.4321);

        // Step 3: Configure TXT save options
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4);          // limit to 4 significant digits
        saveOptions.setCultureInfo(java.util.Locale.US); // enforce dot as decimal separator
        saveOptions.setEnableMemorySaving(true);      // optional for large files

        // Step 4: Save the workbook as a TXT file
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

Η εκτέλεση αυτού του κώδικα παράγει το `significant_digits.txt` με το παρακάτω περιεχόμενο (στήλες χωρισμένες με καρτέλα):

```
123.5	0.001235	98770
```

Κάθε αριθμός τηρεί τον κανόνα των **4 σημαντικών ψηφίων**, δείχνοντας ότι η ρύθμιση λειτουργεί σε διαφορετικές κλίμακες.

## Συμπέρασμα

Τώρα ξέρετε πώς να **εξάγετε Excel σε TXT** ενώ ελέγχετε τον αριθμό των σημαντικών ψηφίων. Χρησιμοποιώντας το `TxtSaveOptions.setSignificantDigits`, μπορείτε να **ορίσετε ψηφία**, **περιορίσετε δεκαδικά** και **περιορίσετε σημαντικά ψηφία** με μια μόνο, συντηρήσιμη γραμμή κώδικα. Η προσέγγιση λειτουργεί για μεμονωμένα κελιά, πλήρεις περιοχές και μεγάλα βιβλία εργασίας.

### Επόμενα βήματα

- Εξερευνήστε άλλες ιδιότητες του `TxtSaveOptions` όπως το `setDelimiter('\t')` για προσαρμογή των διαχωριστών στηλών.
- Συνδυάστε τον εξαγωγέα με το `CsvSaveOptions` εάν χρειάζεστε τιμές διαχωρισμένες με κόμμα αντί για απλό κείμενο.
- Ενσωματώστε τη ρουτίνα σε μια υπηρεσία web που δέχεται ανεβασμένα αρχεία Excel και επιστρέφει άμεσα το περικομμένο αποτέλεσμα TXT.

Μη διστάσετε να πειραματιστείτε με διαφορετικούς περιορισμούς ψηφίων και τοπικές ρυθμίσεις. Εάν αντιμετωπίσετε μια κατάσταση όπου οι ενσωματωμένες επιλογές δεν καλύπτουν μια ειδική απαίτηση, μπορείτε πάντα να επεξεργαστείτε μεταγενέστερα το παραγόμενο αρχείο TXT με τις τυπικές βοηθητικές λειτουργίες I/O της Java.

Καλό προγραμματισμό!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να μετατρέψετε κείμενο σε αριθμούς στο Excel χρησιμοποιώντας το Aspose.Cells for Java](/cells/english/java/cell-operations/convert-text-to-numbers-excel-aspose-cells-java/)
- [Πώς να δημιουργήσετε και να εξάγετε Excel σε HTML χρησιμοποιώντας το Aspose.Cells Java | Οδηγός λειτουργιών βιβλίου εργασίας](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Πώς να εξάγετε προσαρμοσμένες ιδιότητες Excel σε PDF χρησιμοποιώντας το Aspose.Cells for Java](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}