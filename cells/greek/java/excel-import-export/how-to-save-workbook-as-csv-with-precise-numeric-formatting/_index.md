---
category: general
date: 2026-11-22
description: Μάθετε πώς να αποθηκεύετε ένα βιβλίο εργασίας ως CSV χρησιμοποιώντας
  το Aspose.Cells για Java. Αυτός ο οδηγός καλύπτει επίσης την εξαγωγή του Excel σε
  CSV και τη μετατροπή του βιβλίου εργασίας σε CSV με προσαρμοσμένη ακρίβεια.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save workbook as csv
- export excel to csv
- export workbook to csv
- how to export csv
- convert workbook to csv
language: el
lastmod: 2026-11-22
og_description: Αποθηκεύστε το βιβλίο εργασίας ως CSV με το Aspose.Cells για Java.
  Ακολουθήστε αυτό το σεμινάριο για να εξάγετε το Excel σε CSV, να ελέγχετε την ακρίβεια
  των αριθμών και να μετατρέπετε το βιβλίο εργασίας σε CSV αποδοτικά.
og_image_alt: Screenshot showing the save workbook as csv dialog in a Java IDE
og_title: Αποθήκευση βιβλίου εργασίας ως CSV σε Java – πλήρης οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to save workbook as CSV using Aspose.Cells for Java. This
    guide also covers export excel to CSV and convert workbook to CSV with custom
    precision.
  headline: How to save workbook as CSV with precise numeric formatting in Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- CSV export
- Excel automation
title: Πώς να αποθηκεύσετε το βιβλίο εργασίας ως CSV με ακριβή μορφοποίηση αριθμών
  σε Java
url: /el/java/excel-import-export/how-to-save-workbook-as-csv-with-precise-numeric-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αποθηκεύσετε ένα βιβλίο εργασίας ως CSV με ακριβή αριθμητική μορφοποίηση σε Java

Αν χρειάζεται να **αποθηκεύσετε ένα βιβλίο εργασίας ως CSV** και να διατηρήσετε τις αριθμητικές τιμές υπό έλεγχο, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε. Είτε εξάγετε Excel σε CSV για downstream pipelines δεδομένων είτε μετατρέπετε ένα βιβλίο εργασίας σε CSV για αναφορές, τα παρακάτω βήματα σας παρέχουν μια πλήρη, έτοιμη προς εκτέλεση λύση.

Θα δείτε επίσης πώς να **εξάγετε excel σε CSV** με προσαρμοσμένο αριθμό σημαντικών ψηφίων, γιατί η κλάση `TxtSaveOptions` είναι η σωστή επιλογή, και τι πρέπει να προσέξετε όταν διαχειρίζεστε μεγάλα φύλλα εργασίας. Δεν απαιτείται εξωτερική τεκμηρίωση – απλώς αντιγράψτε τον κώδικα, εκτελέστε τον και επαληθεύστε το αποτέλεσμα.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Java 17 ή νεότερη έκδοση εγκατεστημένη  
* Maven ή Gradle για διαχείριση εξαρτήσεων  
* Άδεια Aspose.Cells for Java (η δωρεάν αξιολόγηση λειτουργεί για δοκιμές)  

Αν λείπει κάποιο από αυτά, εγκαταστήστε το JDK, ρυθμίστε ένα εργαλείο κατασκευής και αποκτήστε κλειδί άδειας από τον ιστότοπο της Aspose.

## Βήμα 1: Προσθέστε το Aspose.Cells στο έργο σας

Προσθέστε την εξάρτηση Aspose.Cells στο `pom.xml` (Maven) ή στο `build.gradle` (Gradle). Η βιβλιοθήκη παρέχει τις κλάσεις `Workbook` και `TxtSaveOptions` που χρησιμοποιούνται αργότερα.

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version>
</dependency>
```

```gradle
// Gradle
implementation 'com.aspose:aspose-cells:24.9'
```

> **Συμβουλή:** Χρησιμοποιήστε τον πιο πρόσφατο αριθμό έκδοσης τη στιγμή της συγγραφής (24.9) για να επωφεληθείτε από διορθώσεις σφαλμάτων και νέες δυνατότητες CSV.

## Βήμα 2: Δημιουργήστε ένα δείγμα βιβλίου εργασίας

Ο παρακάτω κώδικας δημιουργεί ένα μικρό βιβλίο εργασίας στη μνήμη. Μπορείτε να αντικαταστήσετε τα δεδομένα με τη δική σας πηγή (βάση δεδομένων, API κ.λπ.).

```java
import com.aspose.cells.*;

public class ExportCsvDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook with one worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Populate some numeric and text data
        Cells cells = sheet.getCells();
        cells.get("A1").setValue("Product");
        cells.get("B1").setValue("Price");
        cells.get("A2").setValue("Widget");
        cells.get("B2").setValue(1234.56789);
        cells.get("A3").setValue("Gadget");
        cells.get("B3").setValue(0.000123456);
    }
}
```

Η εκτέλεση αυτού του αποσπάσματος δημιουργεί ένα Excel αρχείο στη μνήμη με δύο σειρές δεδομένων. Το επόμενο βήμα θα **εξάγει το βιβλίο εργασίας σε CSV** διατηρώντας την αριθμητική ακρίβεια που χρειάζεστε.

## Βήμα 3: Διαμορφώστε τις επιλογές αποθήκευσης CSV – η καρδιά του **save workbook as CSV**

Για να ελέγξετε πώς γράφονται οι αριθμοί, δημιουργήστε ένα αντικείμενο `TxtSaveOptions` με την παράμετρο `SaveFormat.CSV`, και στη συνέχεια ορίστε τον αριθμό των σημαντικών ψηφίων.

```java
// Step 3: Configure CSV options
TxtSaveOptions csvOptions = new TxtSaveOptions(SaveFormat.CSV);

// Keep only five significant digits for all numeric values
csvOptions.setSignificantDigits(5);

// Optional: define a custom delimiter (comma is default)
csvOptions.setSeparator(',');

// Optional: force UTF‑8 encoding for better compatibility
csvOptions.setEncoding(Encoding.getUTF8());
```

`TxtSaveOptions` είναι η κλάση που κάνει το **how to export CSV** ευέλικτο. Η μέθοδος `setSignificantDigits` στρογγυλοποιεί κάθε αριθμητικό κελί στην καθορισμένη ακρίβεια, κάτι που είναι απαραίτητο όταν τα downstream συστήματα αναμένουν σταθερό αριθμό δεκαδικών.

## Βήμα 4: Αποθηκεύστε το βιβλίο εργασίας ως CSV

Τώρα μπορείτε τελικά να **αποθηκεύσετε το βιβλίο εργασίας ως CSV** χρησιμοποιώντας τις επιλογές που μόλις διαμορφώσατε.

```java
// Step 4: Save the workbook to a CSV file
String outputPath = "output/precise_output.csv";
workbook.save(outputPath, csvOptions);
System.out.println("Workbook successfully saved as CSV at: " + outputPath);
```

Όταν το πρόγραμμα ολοκληρωθεί, το `precise_output.csv` περιέχει:

```
Product,Price
Widget,1234.6
Gadget,0.00012346
```

Παρατηρήστε ότι:

* Η τιμή `1234.56789` στρογγυλοποιείται σε `1234.6` (πέντε σημαντικά ψηφία).  
* Η μικρή τιμή `0.000123456` γίνεται `0.00012346`, διατηρώντας το ίδιο επίπεδο σημασίας.

## Βήμα 5: Επαληθεύστε το αποτέλεσμα και αντιμετωπίστε τις ακραίες περιπτώσεις

### Επαλήθευση του CSV

Ανοίξτε το παραγόμενο αρχείο σε έναν επεξεργαστή κειμένου ή εισάγετέ το σε πρόγραμμα λογιστικού φύλλου. Η αριθμητική μορφοποίηση πρέπει να ταιριάζει με την ακρίβεια που ορίσατε.

### Συνηθισμένες ακραίες περιπτώσεις

| Situation                                 | Recommended handling |
|-------------------------------------------|----------------------|
| **Μεγάλοι αριθμοί (> 1 e+12)**            | Αυξήστε το `setSignificantDigits` ή χρησιμοποιήστε το `setNumberDecimalSeparator` για να αποφύγετε τη επιστημονική σημειογραφία. |
| **Διαχωριστές δεκαδικών ανάλογα με την τοπική ρύθμιση** | Χρησιμοποιήστε `csvOptions.setDecimalSeparator('.')` για τελεία ή `','` για κόμμα, ανάλογα με το σύστημα προορισμού. |
| **Κενά κελιά**                            | Γράφονται ως κενές συμβολοσειρές· δεν προστίθενται επιπλέον διαχωριστές. |
| **Προσαρμοσμένη σειρά στηλών**            | Αναδιατάξτε τα κελιά στο φύλλο εργασίας πριν την αποθήκευση, ή χρησιμοποιήστε το `CsvSaveOptions` (διαθέσιμο σε νεότερες εκδόσεις) για ρητή αντιστοίχιση στηλών. |

> **Προσοχή:** Αν ξεχάσετε να ορίσετε την κωδικοποίηση, το Excel μπορεί να ερμηνεύσει το αρχείο χρησιμοποιώντας την προεπιλεγμένη κωδικοποίηση του συστήματος, οδηγώντας σε ακατάλληλους χαρακτήρες για δεδομένα μη‑ASCII.

## Βήμα 6: Εναλλακτικές για **export excel to CSV** χωρίς έλεγχο ακρίβειας

Αν δεν χρειάζεστε προσαρμοσμένο στρογγυλοποίηση, μπορείτε να παραλείψετε την κλήση `setSignificantDigits` και να βασιστείτε στην προεπιλεγμένη μορφοποίηση του Aspose.Cells:

```java
TxtSaveOptions simpleOptions = new TxtSaveOptions(SaveFormat.CSV);
workbook.save("output/simple.csv", simpleOptions);
```

Αυτή η προσέγγιση είναι χρήσιμη όταν απλώς θέλετε να **μετατρέψετε το βιβλίο εργασίας σε CSV** για γρήγορη ανταλλαγή δεδομένων.

## Βήμα 7: Αυτοματοποίηση της διαδικασίας για πολλαπλά βιβλία εργασίας

Σε πραγματικά σενάρια μπορεί να χρειαστεί να επεξεργαστείτε δεκάδες αρχεία Excel. Τυλίξτε τη λογική σε μια επαναχρησιμοποιήσιμη μέθοδο:

```java
public static void exportToCsv(String excelPath, String csvPath, int precision) throws Exception {
    Workbook wb = new Workbook(excelPath);
    TxtSaveOptions opts = new TxtSaveOptions(SaveFormat.CSV);
    opts.setSignificantDigits(precision);
    wb.save(csvPath, opts);
}
```

Καλέστε `exportToCsv("data/input.xlsx", "data/output.csv", 5);` για κάθε αρχείο. Αυτό το πρότυπο απαντά στην ερώτηση “**how to export csv**” για εργασίες batch.

## Συμπέρασμα

Τώρα έχετε μια πλήρη, έτοιμη για παραγωγή συνταγή για **save workbook as CSV** σε Java:

* Δημιουργήστε ένα `Workbook` και γεμίστε το με δεδομένα.  
* Διαμορφώστε το `TxtSaveOptions` για να ορίσετε σημαντικά ψηφία, διαχωριστικό και κωδικοποίηση.  
* Καλέστε `workbook.save(..., csvOptions)` για να δημιουργήσετε το αρχείο CSV.

Με αυτή τη γνώση μπορείτε επίσης να **export excel to csv**, **export workbook to csv**, και **convert workbook to csv** για οποιοδήποτε downstream σύστημα, διατηρώντας την αριθμητική ακρίβεια υπό αυστηρό έλεγχο.

---

**Επόμενα βήματα**

* Εξερευνήστε το `CsvSaveOptions` (διαθέσιμο στο Aspose.Cells 24.10+) για αντιστοίχιση στηλών και προχωρημένη παράθεση.  
* Συνδυάστε αυτήν την εξαγωγή με το Apache POI αν χρειάζεται να διαβάσετε παλιά αρχεία `.xls` πριν τη μετατροπή.  
* Ενσωματώστε τη μέθοδο σε μια υπηρεσία Spring Boot για να εκθέσετε την εξαγωγή CSV μέσω ενός REST endpoint.

Καλή προγραμματιστική δουλειά, και μη διστάσετε να πειραματιστείτε με διαφορετικά επίπεδα ακρίβειας και διαχωριστές ώστε να ταιριάζουν στο pipeline δεδομένων σας!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Αποθήκευση βιβλίου εργασίας ως CSV – Πλήρης οδηγός Java για εξαγωγή Excel σε CSV](/cells/english/java/excel-import-export/save-workbook-as-csv-complete-java-guide-to-export-excel-to/)
- [Αποθήκευση βιβλίου εργασίας ως CSV χρησιμοποιώντας Aspose.Cells for Java – οδηγός βήμα‑βήμα](/cells/english/java/excel-import-export/save-workbook-as-csv-using-aspose-cells-for-java-step-by-ste/)
- [Πώς να φορτώσετε και να αποθηκεύσετε Excel ως CSV χρησιμοποιώντας Aspose.Cells for Java: Ένας ολοκληρωμένος οδηγός](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}