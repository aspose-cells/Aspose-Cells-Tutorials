---
category: general
date: 2026-08-04
description: Εξαγωγή επιλεγμένων κελιών σε CSV σε Java με το Aspose.Cells. Μάθετε
  πώς να εξάγετε μια περιοχή Excel σε CSV χρησιμοποιώντας προσαρμοσμένες επιλογές
  ψηφίων και ανθεκτικό κώδικα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export selected cells to csv
- export excel range to csv
- Aspose.Cells CSV export
- Java Excel automation
- CSV formatting options
language: el
lastmod: 2026-08-04
og_description: Εξαγωγή επιλεγμένων κελιών σε CSV σε Java χρησιμοποιώντας το Aspose.Cells.
  Αυτό το σεμινάριο δείχνει πώς να εξάγετε μια περιοχή Excel σε CSV με ακριβή έλεγχο
  ψηφίων.
og_image_alt: Screenshot of Java code exporting selected cells to CSV
og_title: Εξαγωγή επιλεγμένων κελιών σε CSV στη Java – οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Export selected cells to CSV in Java with Aspose.Cells. Learn how to
    export Excel range to CSV using custom digit options and robust code.
  headline: Export selected cells to CSV in Java – complete guide
  type: TechArticle
tags:
- CSV
- Java
- Aspose.Cells
- Excel
title: Εξαγωγή επιλεγμένων κελιών σε CSV στη Java – πλήρης οδηγός
url: /el/java/excel-import-export/export-selected-cells-to-csv-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή επιλεγμένων κελιών σε CSV σε Java – πλήρης οδηγός

Αν χρειάζεστε να **εξάγετε επιλεγμένα κελιά σε CSV** από ένα βιβλίο εργασίας Excel, αυτό το tutorial σας παρουσιάζει μια έτοιμη λύση. Στο τέλος του οδηγού θα μπορείτε να **εξάγετε περιοχή Excel σε CSV** με προσαρμοσμένη ακρίβεια ψηφίων, καθιστώντας το αποτέλεσμα καθαρό για επεξεργασία downstream. Θα δείτε πώς να φορτώσετε ένα βιβλίο εργασίας, να διαμορφώσετε τις επιλογές εξαγωγής, να επιλέξετε μια συγκεκριμένη περιοχή και να γράψετε το αρχείο CSV—όλα με σαφή κώδικα Java. Δεν απαιτούνται εξωτερικά scripts ή χειροκίνητα βήματα copy‑paste. Η μόνη προαπαιτούμενη προϋπόθεση είναι ένα περιβάλλον ανάπτυξης Java και η βιβλιοθήκη Aspose.Cells for Java.

## Προαπαιτούμενα

* JDK 17 ή νεότερο εγκατεστημένο.
* Maven ή Gradle για διαχείριση εξαρτήσεων.
* Ένα IDE όπως IntelliJ IDEA ή Eclipse (οποιοσδήποτε επεξεργαστής λειτουργεί).
* Το JAR του Aspose.Cells for Java (διαθέσιμο από Maven Central).

Αυτές οι απαιτήσεις διασφαλίζουν ότι ο κώδικας εκτελείται χωρίς πρόσθετη ρύθμιση.

## Βήμα 1: Προσθήκη Aspose.Cells στο έργο σας

Το πρώτο βήμα είναι η προσθήκη της βιβλιοθήκης Aspose.Cells. Εάν χρησιμοποιείτε Maven, προσθέστε την ακόλουθη εξάρτηση στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

Για Gradle, τοποθετήστε αυτή τη γραμμή στο `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:24.9'
```

Η προσθήκη της βιβλιοθήκης καθιστά διαθέσιμες τις κλάσεις `Workbook`, `ExportTableOptions` και `Range` για χρήση.

## Βήμα 2: Φόρτωση του βιβλίου εργασίας που θέλετε να επεξεργαστείτε

Τώρα φορτώστε το αρχείο Excel που περιέχει τα δεδομένα που θέλετε να εξάγετε. Αντικαταστήστε το `YOUR_DIRECTORY/Numbers.xlsx` με την πραγματική διαδρομή του βιβλίου εργασίας σας.

```java
import com.aspose.cells.*;

public class CsvExportExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Load the workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Numbers.xlsx");
```

Η φόρτωση του βιβλίου εργασίας δημιουργεί μια αναπαράσταση στη μνήμη που μπορείτε να ερωτήσετε και να επεξεργαστείτε. Αυτό το βήμα είναι απαραίτητο για οποιαδήποτε λειτουργία **εξαγωγής επιλεγμένων κελιών σε CSV** επειδή η βιβλιοθήκη λειτουργεί άμεσα με το αντικείμενο του βιβλίου εργασίας.

## Βήμα 3: Διαμόρφωση επιλογών εξαγωγής – περιορισμός σημαντικών ψηφίων

Συχνά τα αρχεία CSV καταναλώνονται από συστήματα που αναμένουν σταθερό αριθμό δεκαδικών θέσεων. Η κλάση `ExportTableOptions` σας επιτρέπει να ελέγξετε αυτήν την ακρίβεια. Το παρακάτω παράδειγμα διατηρεί μόνο πέντε σημαντικά ψηφία:

```java
        // Step 3: Create export options and limit the number of significant digits
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setSignificantDigits(5); // keep only 5 significant digits
```

Ο ορισμός του `significantDigits` μειώνει τον θόρυβο στο αποτέλεσμα και αποτρέπει τα artefacts κινητής υποδιαστολής από το να διαφθείρουν τους υπολογισμούς downstream.

## Βήμα 4: Ορισμός της ακριβούς περιοχής που θέλετε να εξάγετε

Μπορείτε να εξάγετε οποιοδήποτε ορθογώνιο μπλοκ κελιών. Η μέθοδος `createRange` δέχεται μια διεύθυνση σε μορφή A1. Σε αυτό το παράδειγμα στοχεύουμε στα κελιά **A1:C10** στο πρώτο φύλλο εργασίας:

```java
        // Step 4: Define the range to export (e.g., cells A1 to C10 on the first worksheet)
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Range range = worksheet.getCells().createRange("A1:C10");
```

Η επιλογή μιας ακριβούς περιοχής είναι ο πυρήνας της **εξαγωγής επιλεγμένων κελιών σε CSV**. Εάν χρειάζεστε διαφορετική περιοχή, απλώς αλλάξτε τη συμβολοσειρά διεύθυνσης.

## Βήμα 5: Εξαγωγή της περιοχής σε αρχείο CSV

Με την περιοχή και τις επιλογές έτοιμες, καλέστε το `exportCsv`. Η μέθοδος γράφει το αρχείο CSV στην τοποθεσία που καθορίζετε:

```java
        // Step 5: Export the selected range to CSV using the configured options
        range.exportCsv("YOUR_DIRECTORY/LimitedDigits.csv", exportOptions);
    }
}
```

Το παραγόμενο αρχείο, `LimitedDigits.csv`, περιέχει μόνο τα δεδομένα από A1 έως C10, μορφοποιημένα με πέντε σημαντικά ψηφία. Αυτό ολοκληρώνει τη ροή εργασίας **εξαγωγής περιοχής Excel σε CSV**.

## Βήμα 6: Επαλήθευση του αποτελέσματος και διαχείριση κοινών περιπτώσεων άκρων

Μετά την εκτέλεση, ανοίξτε το αρχείο CSV σε έναν επεξεργαστή κειμένου ή πρόγραμμα λογιστικού φύλλου για να επιβεβαιώσετε:

```
Header1,Header2,Header3
12.345,67.890,0.12345
...
```

### Συνηθισμένα εμπόδια και πώς να τα αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Εμφανίζονται κενές γραμμές** | Η περιοχή περιλαμβάνει κενές γραμμές. | Κόψτε την περιοχή ή φιλτράρετε τις γραμμές πριν την εξαγωγή. |
| **Δεκαδικοί διαχωριστές ανάλογα με την τοπική ρύθμιση** | Η Java χρησιμοποιεί την προεπιλεγμένη τοπική ρύθμιση, η οποία μπορεί να εμφανίζει κόμματα αντί για τελείες. | Ορίστε `exportOptions.setSeparator(',')` ή διαμορφώστε την τοπική ρύθμιση του JVM. |
| **Μεγάλα αρχεία προκαλούν πίεση μνήμης** | Η εξαγωγή εκατομμυρίων γραμμών τα φορτώνει στη μνήμη. | Χρησιμοποιήστε `ExportTableOptions.setExportDataOnly(true)` και επεξεργαστείτε σε παρτίδες. |

Η αντιμετώπιση αυτών των σεναρίων διασφαλίζει ότι η λειτουργία **εξαγωγής επιλεγμένων κελιών σε CSV** παραμένει αξιόπιστη στην παραγωγή.

## Πλήρες λειτουργικό παράδειγμα

Παρακάτω βρίσκεται το πλήρες, αυτόνομο πρόγραμμα Java που μπορείτε να αντιγράψετε, επικολλήσετε και να εκτελέσετε:

```java
import com.aspose.cells.*;

public class CsvExportExample {
    public static void main(String[] args) throws Exception {
        // Load the workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Numbers.xlsx");

        // Configure export options: keep 5 significant digits
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setSignificantDigits(5);

        // Define the range A1:C10 on the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Range range = worksheet.getCells().createRange("A1:C10");

        // Export the range to CSV
        range.exportCsv("YOUR_DIRECTORY/LimitedDigits.csv", exportOptions);

        System.out.println("Export completed successfully.");
    }
}
```

Η εκτέλεση αυτού του προγράμματος παράγει το `LimitedDigits.csv` στον φάκελο προορισμού. Η κονσόλα θα εμφανίσει *Export completed successfully.* υποδεικνύοντας ότι η διαδικασία **εξαγωγής επιλεγμένων κελιών σε CSV** ολοκληρώθηκε χωρίς σφάλματα.

## Καλές πρακτικές για εξαγωγή δεδομένων Excel σε CSV

* **Πάντα κλείστε τους πόρους** – αν και το Aspose.Cells διαχειρίζεται τα streams εσωτερικά, η ρητή κλήση του `workbook.dispose()` σε ένα μπλοκ `finally` μπορεί να ελευθερώσει τη φυσική μνήμη.
* **Επικυρώστε την περιοχή** – χρησιμοποιήστε `Range.getRowCount()` και `Range.getColumnCount()` για να διασφαλίσετε ότι η περιοχή δεν είναι κενή πριν την εξαγωγή.
* **Χρησιμοποιήστε κωδικοποίηση UTF‑8** – τα αρχεία CSV είναι απλό κείμενο· ορίστε `exportOptions.setEncoding(Encoding.getUTF8())` εάν τα δεδομένα σας περιέχουν μη‑ASCII χαρακτήρες.
* **Αυτοματοποιήστε τις δοκιμές** – γράψτε μονάδες δοκιμών που συγκρίνουν το παραγόμενο CSV με ένα αναμενόμενο αρχείο για να εντοπίσετε παλινδρομήσεις νωρίς.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **εξάγετε επιλεγμένα κελιά σε CSV** σε Java χρησιμοποιώντας το Aspose.Cells, και έχετε δει έναν πρακτικό τρόπο **εξαγωγής περιοχής Excel σε CSV** με έλεγχο επιπέδου ψηφίων. Το tutorial κάλυψε τη ρύθμιση του έργου, τη φόρτωση του βιβλίου εργασίας, τη διαμόρφωση επιλογών, τον ορισμό της περιοχής και την εξαγωγή αρχείου, καθώς και συμβουλές για τη διαχείριση περιπτώσεων άκρων. Στη συνέχεια, εξερευνήστε συναφή θέματα όπως **εξαγωγή Excel σε TSV**, **streaming μεγάλων αρχείων CSV**, ή **εφαρμογή προσαρμοσμένης μορφοποίησης κελιών πριν την εξαγωγή**. Πειραματιστείτε με διαφορετικές ρυθμίσεις `ExportTableOptions` για να προσαρμόσετε το αποτέλεσμα CSV στα downstream συστήματά σας.

Καλό κώδικα, και μη διστάσετε να προσαρμόσετε το παράδειγμα ώστε να ταιριάζει στις δικές σας ροές δεδομένων!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Excel σε CSV με Κενές Γραμμές Χρησιμοποιώντας Aspose.Cells για .NET](/cells/english/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)
- [Εξαγωγή Excel Csv Κενές Γραμμές Aspose Cells Net](/cells/german/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)
- [Πώς να Εξάγετε Προσαρμοσμένες Ιδιότητες Excel σε PDF Χρησιμοποιώντας Aspose.Cells για Java](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}