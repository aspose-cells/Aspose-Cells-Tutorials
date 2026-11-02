---
category: general
date: 2026-08-20
description: Μάθετε πώς να εξάγετε γράφημα σε docx και να μετατρέψετε ένα βιβλίο εργασίας
  Excel σε docx με το Aspose.Cells σε Java. Οδηγός βήμα‑βήμα με πλήρες κώδικα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export chart to docx
- convert excel workbook to docx
- Aspose.Cells Java
- editable chart DOCX
- Excel to Word conversion
language: el
lastmod: 2026-08-20
og_description: Εξαγωγή γραφήματος σε docx και μετατροπή βιβλίου εργασίας Excel σε
  docx χρησιμοποιώντας το Aspose.Cells for Java. Ακολουθήστε αυτόν τον πλήρη, εκτελέσιμο
  οδηγό.
og_image_alt: Screenshot showing a Java code editor exporting an Excel chart to a
  DOCX file
og_title: Εξαγωγή γραφήματος σε docx με το Aspose.Cells – Οδηγός Java
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to export chart to docx and convert Excel workbook to docx
    with Aspose.Cells in Java. Step‑by‑step guide with complete code.
  headline: How to export chart to docx from Excel using Aspose.Cells for Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- DOCX
- Excel
title: Πώς να εξάγετε γράφημα σε docx από το Excel χρησιμοποιώντας το Aspose.Cells
  for Java
url: /el/java/integration-interoperability/how-to-export-chart-to-docx-from-excel-using-aspose-cells-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή γραφήματος σε docx από βιβλίο εργασίας Excel χρησιμοποιώντας Java

Αν χρειάζεστε **εξαγωγή γραφήματος σε docx** απευθείας από αρχείο Excel, αυτό το tutorial σας παρουσιάζει μια έτοιμη λύση. Στο τέλος του οδηγού θα γνωρίζετε επίσης πώς να **μετατρέψετε βιβλίο εργασίας Excel σε docx** διατηρώντας ένα επεξεργάσιμο γράφημα, ώστε το παραγόμενο έγγραφο Word να μπορεί να τροποποιηθεί χωρίς απώλεια πιστότητας.

Η εξαγωγή γραφημάτων είναι συχνή όταν δημιουργείτε αναφορές που συνδυάζουν υπολογισμούς σε φύλλα εργασίας με πλούσιες διατάξεις Word. Το Aspose.Cells for Java κάνει τη μετατροπή απλή, και το API σας επιτρέπει να διατηρήσετε το γράφημα επεξεργάσιμο — χωρίς στατική εικόνα.

## Τι καλύπτει αυτό το tutorial

* Φόρτωση υπάρχοντος βιβλίου εργασίας που περιέχει γράφημα.  
* Διαμόρφωση του `ImageOrPrintOptions` για στόχο τη μορφή DOCX.  
* Ενεργοποίηση της σημαίας `ExportEditableCharts` (διαθέσιμη από την έκδοση 25.10).  
* Αποθήκευση του βιβλίου εργασίας ως αρχείο DOCX που διατηρεί επεξεργάσιμο γράφημα.  

Δεν απαιτούνται εξωτερικά εργαλεία πέρα από το Aspose.Cells JAR. Ο κώδικας λειτουργεί με Java 8+ και οποιαδήποτε πρόσφατη έκδοση του Aspose.Cells.

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντική |
|-------------|----------------|
| **Aspose.Cells for Java** (v25.10 ή νεότερη) | Η δυνατότητα `setExportEditableCharts` εισήχθη σε αυτή την έκδοση. |
| **Java Development Kit (JDK) 8 ή νεότερο** | Παρέχει το runtime για τη μεταγλώττιση και εκτέλεση του παραδείγματος. |
| **Βιβλίο εργασίας Excel (`.xlsx`) που περιέχει τουλάχιστον ένα γράφημα** | Το γράφημα είναι το αντικείμενο που θα εξαχθεί σε DOCX. |
| **IDE Java ή εργαλείο κατασκευής (π.χ., Maven, Gradle)** | Απλοποιεί τη διαχείριση εξαρτήσεων και την εκτέλεση. |

Μπορείτε να κατεβάσετε το τελευταίο Aspose.Cells JAR από την [ιστοσελίδα Aspose](https://products.aspose.com/cells/java/).

## Βήμα 1: Ρύθμιση του έργου και προσθήκη της εξάρτησης Aspose.Cells

Αν χρησιμοποιείτε Maven, προσθέστε την παρακάτω εξάρτηση στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version> <!-- use the latest version -->
</dependency>
```

Για Gradle, προσθέστε:

```gradle
implementation 'com.aspose:aspose-cells:25.10'
```

> **Συμβουλή:** Χρησιμοποιήστε ακριβώς την έκδοση που εισήγαγε το `ExportEditableCharts` (25.10) ή οποιαδήποτε νεότερη. Παλαιότερες εκδόσεις θα αγνοήσουν τη σημαία και θα παράγουν στατική εικόνα.

## Βήμα 2: Φόρτωση του βιβλίου εργασίας που περιέχει το γράφημα

Η κλάση `Workbook` αντιπροσωπεύει ολόκληρο το αρχείο Excel. Η φόρτωσή του είναι μια εντολή μιας γραμμής:

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Load the workbook with the chart you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");
```

> **Γιατί είναι σημαντικό:** Το βιβλίο εργασίας πρέπει να είναι πλήρως φορτωμένο πριν εφαρμόσετε οποιεσδήποτε επιλογές εξαγωγής. Αν η διαδρομή του αρχείου είναι λανθασμένη, το Aspose.Cells θα ρίξει `FileNotFoundException`.

## Βήμα 3: Διαμόρφωση επιλογών εικόνας/εκτύπωσης για έξοδο DOCX

Το `ImageOrPrintOptions` ελέγχει πώς θα αποδοθεί το βιβλίο εργασίας. Ορίζοντας τη μορφή αποθήκευσης σε `DOCX` λέτε στο Aspose.Cells να δημιουργήσει έγγραφο Word αντί για εικόνα.

```java
        // Create options and specify DOCX as the target format
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);
```

Μπορείτε επίσης να ρυθμίσετε το μέγεθος σελίδας, DPI ή ποιότητα εικόνας εδώ, αλλά είναι προαιρετικά για την εξαγωγή γραφήματος.

## Βήμα 4: Ενεργοποίηση εξαγωγής επεξεργάσιμων γραφημάτων

Από την έκδοση 25.10 και μετά, το Aspose.Cells μπορεί να ενσωματώσει γραφήματα ως εγγενή αντικείμενα γραφήματος του Word. Αυτό τα κάνει πλήρως επεξεργάσιμα στο Microsoft Word.

```java
        // Turn on the editable chart export flag
        options.setExportEditableCharts(true);
```

> **Ακραία περίπτωση:** Αν ορίσετε αυτή τη σημαία σε `false` (ή την παραλείψετε), το γράφημα θα αποδοθεί ως στατική εικόνα. Χρησιμοποιήστε `true` μόνο όταν το κοινό-στόχος χρειάζεται να επεξεργαστεί το γράφημα μετά τη μετατροπή.

## Βήμα 5: Αποθήκευση του βιβλίου εργασίας ως αρχείο DOCX

Τέλος, καλέστε το `Workbook.save` με τις διαμορφωμένες επιλογές:

```java
        // Save the workbook as a DOCX document that contains an editable chart
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

Όταν το πρόγραμμα ολοκληρωθεί, ανοίξτε το `ChartEditable.docx` στο Microsoft Word. Θα πρέπει να δείτε το αρχικό γράφημα, και αν κάνετε δεξί‑κλικ, η επιλογή **Edit Data** θα είναι διαθέσιμη — επιβεβαιώνοντας ότι το γράφημα είναι πραγματικά επεξεργάσιμο.

## Πλήρες, εκτελέσιμο παράδειγμα

Ακολουθεί το πλήρες αρχείο πηγαίου κώδικα. Αντιγράψτε το στο IDE σας, αντικαταστήστε το `YOUR_DIRECTORY` με απόλυτη ή σχετική διαδρομή, και τρέξτε το.

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the chart
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");

        // Step 2: Create image/print options and set the target format to DOCX
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);

        // Step 3: Enable exporting of editable charts (available from version 25.10)
        options.setExportEditableCharts(true);

        // Step 4: Save the workbook as a DOCX document with the configured options
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

**Αναμενόμενο αποτέλεσμα**

* Ένα αρχείο με όνομα `ChartEditable.docx` στον καθορισμένο φάκελο.  
* Ανοίγοντας το αρχείο στο Word, το γράφημα εμφανίζεται ακριβώς όπως στο Excel, και μπορείτε να κάνετε διπλό‑κλικ για να επεξεργαστείτε τις σειρές δεδομένων του.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Συμπτωμα | Αιτία | Διόρθωση |
|---------|-------|----------|
| Το Word εμφανίζει **στατική εικόνα** αντί για επεξεργάσιμο γράφημα | Η μέθοδος `setExportEditableCharts` δεν κλήθηκε ή χρησιμοποιείται έκδοση < 25.10 | Βεβαιωθείτε ότι η σημαία είναι `true` και ότι χρησιμοποιείτε Aspose.Cells 25.10 ή νεότερη. |
| Το παραγόμενο DOCX είναι **κενό** | Λανθασμένη διαδρομή αρχείου για το πηγαίο βιβλίο εργασίας ή ανεπαρκή δικαιώματα | Επαληθεύστε τη διαδρομή του βιβλίου εργασίας και ότι η εφαρμογή έχει πρόσβαση ανάγνωσης/εγγραφής. |
| Η διάταξη του γραφήματος φαίνεται **παραμορφωμένη** | Η ρύθμιση σελίδας στο Excel (π.χ., κρυμμένες γραμμές/στήλες) διαφέρει από τις προεπιλογές του Word | Ρυθμίστε το `ImageOrPrintOptions` (π.χ., `setOnePagePerSheet(true)`) για έλεγχο κλιμάκωσης. |
| **Απόδοση** μειώνεται σε μεγάλα βιβλία εργασίας | Εξαγωγή πολλών γραφημάτων ή μεγάλων συνόλων δεδομένων | Εξάγετε μόνο τα απαραίτητα φύλλα ή χρησιμοποιήστε `setSheetIndex` για περιορισμό επεξεργασίας. |

## Επέκταση της λύσης

* **Πολλαπλά γραφήματα:** Επανάληψη σε όλα τα φύλλα εργασίας και κλήση `worksheet.getCharts()` για εξαγωγή κάθε γραφήματος ξεχωριστά.  
* **Προσαρμοσμένο στυλ DOCX:** Μετά την αποθήκευση, χρησιμοποιήστε το Aspose.Words για προσθήκη κεφαλίδων, υποσέλιδων ή στυλ στο παραγόμενο έγγραφο.  
* **Μετατροπή σε παρτίδες:** Τυλίξτε τον κώδικα σε βρόχο που επεξεργάζεται έναν φάκελο `.xlsx` αρχείων, παράγοντας DOCX για το καθένα.

## Συμπέρασμα

Τώρα έχετε μια αξιόπιστη μέθοδο για **εξαγωγή γραφήματος σε docx** και **μετατροπή βιβλίου εργασίας Excel σε docx** διατηρώντας πλήρη επεξεργασιμότητα του γραφήματος. Τα βασικά βήματα είναι η φόρτωση του βιβλίου εργασίας, η διαμόρφωση του `ImageOrPrintOptions` για DOCX, η ενεργοποίηση του `ExportEditableCharts` και η αποθήκευση του αποτελέσματος.

Πειραματιστείτε με επιπλέον επιλογές — όπως ορισμός περιθωρίων σελίδας ή ενσωμάτωση των τύπων του βιβλίου εργασίας — για να προσαρμόσετε την έξοδο στη ροή εργασίας αναφορών σας. Όταν χρειάζεται να δημιουργείτε αναφορές Word από δεδομένα Excel προγραμματιστικά, αυτή η προσέγγιση προσφέρει μια καθαρή, συντηρήσιμη λύση.

--- 

*Έτοιμοι να το δοκιμάσετε; Κλωνοποιήστε το παράδειγμα, ενημερώστε τις διαδρομές αρχείων και τρέξτε το πρόγραμμα. Αν αντιμετωπίσετε προβλήματα, συμβουλευτείτε την τεκμηρίωση Aspose.Cells for Java ή εξερευνήστε τα συναφή θέματα παρακάτω.*  

### Σχετικά θέματα που μπορείτε να εξερευνήσετε στη συνέχεια

* **μετατροπή βιβλίου εργασίας Excel σε pdf** – δημιουργία PDF αναφορών από το ίδιο βιβλίο εργασίας.  
* **Aspose.Cells μορφοποίηση γραφήματος** – προσαρμογή χρωμάτων, σημείων και αξόνων πριν την εξαγωγή.  
* **Ενσωμάτωση εικόνων σε DOCX με Aspose.Words** – συνδυασμός γραφημάτων με άλλο περιεχόμενο Word.  

Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [How to Create Excel Chart with Trendline and Export to Image using Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Automate Excel Chart Access Using Aspose.Cells Java: A Step-by-Step Guide](/cells/english/java/charts-graphs/excel-charts-access-aspose-cells-java/)
- [Customize Excel Chart Data Labels Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}