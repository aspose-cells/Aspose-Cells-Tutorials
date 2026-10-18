---
category: general
date: 2026-06-30
description: Εξαγωγή γραφήματος ως εικόνα και μάθετε πώς να εξάγετε γράφημα, να αποθηκεύσετε
  το Excel ως Word, να μετατρέψετε το Excel σε Word και να μετατρέψετε το XLSX σε
  DOCX σε λίγα εύκολα βήματα.
draft: false
keywords:
- export chart as image
- how to export chart
- save excel as word
- convert excel to word
- convert xlsx to docx
language: el
og_description: Εξαγωγή διαγράμματος ως εικόνα και γρήγορη μετατροπή Excel σε Word.
  Ακολουθήστε αυτόν τον οδηγό για να αποθηκεύσετε το Excel ως Word, να εξάγετε διαγράμματα
  και να μετατρέψετε το XLSX σε DOCX.
og_title: Εξαγωγή διαγράμματος ως εικόνα – Βήμα‑βήμα μετατροπή Excel σε Word
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Export chart as image and learn how to export chart, save Excel as
    Word, convert Excel to Word, and convert XLSX to DOCX in a few easy steps.
  headline: Export Chart as Image – Complete Guide to Convert Excel to Word
  type: TechArticle
- description: Export chart as image and learn how to export chart, save Excel as
    Word, convert Excel to Word, and convert XLSX to DOCX in a few easy steps.
  name: Export Chart as Image – Complete Guide to Convert Excel to Word
  steps:
  - name: What if my workbook has multiple charts?
    text: You don’t need to change anything—setting `setExportChartAsImage(true)`
      applies to **all** charts in the workbook. If you only want specific charts
      as images, you’ll have to export them manually using `chart.toImage()` and then
      insert them into the Word file yourself.
  - name: Can I control the image format (PNG vs JPEG)?
    text: 'Aspose.Cells uses PNG by default for chart‑as‑image exports. To switch
      to JPEG, you can adjust the `ImageOrPrintOptions` before saving:'
  - name: Does this work with older Excel files (.xls)?
    text: Absolutely. The same code works for both `.xls` and `.xlsx`. Aspose.Cells
      auto‑detects the format, so you can **save Excel as Word** regardless of the
      source version.
  - name: How does this differ from “convert Excel to Word” with native Office interop?
    text: Native interop often requires a Windows machine with Office installed, and
      charts may lose fidelity. Using Aspose.Cells is platform‑agnostic, works on
      Linux/macOS, and preserves chart quality by rasterizing them.
  type: HowTo
tags:
- Excel
- Word
- Chart
- Java
- Aspose.Cells
title: Εξαγωγή γραφήματος ως εικόνα – Πλήρης οδηγός για τη μετατροπή του Excel σε
  Word
url: /el/java/excel-import-export/export-chart-as-image-complete-guide-to-convert-excel-to-wor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Διαγράμματος ως Εικόνα – Πλήρης Οδηγός για τη Μετατροπή Excel σε Word

Αναρωτηθήκατε ποτέ πώς να εξάγετε ένα διάγραμμα ως εικόνα από ένα βιβλίο εργασίας Excel και να το τοποθετήσετε απευθείας σε ένα έγγραφο Word; Δεν είστε ο μόνος—οι προγραμματιστές ρωτούν συνεχώς, «Πώς μπορώ να εξάγω διάγραμμα από XLSX και να το ενσωματώσω σε DOCX χωρίς να χάσει την ποιότητα;»

Τα καλά νέα είναι ότι με λίγες γραμμές κώδικα Java μπορείτε να **export chart as image**, στη συνέχεια **save Excel as Word** σε μια αδιάσπαστη ροή. Σε αυτόν τον οδηγό θα περάσουμε από όλη τη διαδικασία, καλύπτοντας τα πάντα από τη φόρτωση του βιβλίου εργασίας μέχρι τη διαμόρφωση των επιλογών αποθήκευσης που μετατρέπουν τα διαγράμματά σας σε καθαρά PNG μέσα σε αρχείο DOCX.

Θα αγγίξουμε επίσης συναφή εργασίες όπως **convert Excel to Word**, **save Excel as Word**, και **convert XLSX to DOCX**—όλα ενώ διατηρούμε τον κώδικα σαφή και εκτελέσιμο. Χωρίς περιττές λεπτομέρειες, μόνο μια πρακτική λύση που μπορείτε να αντιγράψετε‑επικολλήσετε σήμερα.

---

## Τι Θα Χρειαστείτε

- **Java Development Kit (JDK) 8+** – ο κώδικας εκτελείται σε οποιοδήποτε σύγχρονο JDK.
- **Aspose.Cells for Java** library (version 23.10 ή νεότερη). Μπορείτε να την αποκτήσετε από το Maven Central ή να κατεβάσετε το JAR απευθείας.
- Ένα **Excel file** (`charts.xlsx`) που περιέχει τουλάχιστον ένα διάγραμμα που θέλετε να εξάγετε.
- Ένα **Java IDE** (IntelliJ IDEA, Eclipse ή VS Code) – όποιοδήποτε είναι εντάξει.
- Βασική εξοικείωση με Java και Maven/Gradle (προαιρετικό αλλά χρήσιμο).

Αυτό είναι όλο. Χωρίς πρόσθετα plugins, χωρίς COM interop, μόνο καθαρή Java.

---

## Βήμα 1: Φόρτωση του Βιβλίου Εργασίας Excel και Εντοπισμός του Διαγράμματος

Το πρώτο που πρέπει να κάνουμε είναι να ανοίξουμε το βιβλίο εργασίας που περιέχει το διάγραμμα. Η Aspose.Cells το κάνει παιχνιδάκι—απλώς δείξτε το στο μονοπάτι του αρχείου.

```java
// Step 1: Load the Excel workbook that contains the chart
Workbook workbook = new Workbook("YOUR_DIRECTORY/charts.xlsx");

// Grab the first worksheet (index 0) and its first chart (index 0)
Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
```

> **Γιατί είναι σημαντικό:** Η φόρτωση του βιβλίου εργασίας μας δίνει πρόσβαση στο αντικείμενο διαγράμματος, το οποίο θα πούμε αργότερα στην Aspose να το αποδώσει ως εικόνα. Αν το βιβλίο εργασίας περιέχει πολλαπλά φύλλα ή διαγράμματα, μπορείτε να προσαρμόσετε τα δείκτες ή να τα επαναλάβετε.

---

## Βήμα 2: Διαμόρφωση Επιλογών Αποθήκευσης DOCX για Εξαγωγή Διαγραμμάτων ως Εικόνες

Η Aspose.Cells παρέχει μια κλάση `DocxSaveOptions` που σας επιτρέπει να ελέγχετε πώς συμπεριφέρεται η μετατροπή. Η ρύθμιση `setExportChartAsImage(true)` λέει στη βιβλιοθήκη να μετατρέπει κάθε διάγραμμα σε εικόνα πριν το ενσωματώσει στο αρχείο Word.

```java
// Step 2: Create DOCX save options and enable chart‑as‑image export
DocxSaveOptions saveOptions = new DocxSaveOptions();
saveOptions.setExportChartAsImage(true); // This is the key line
```

> **Pro tip:** Αν προτιμάτε διανυσματικά γραφικά (EMF/WMF) μπορείτε να αφήσετε αυτή τη σημαία απενεργοποιημένη, αλλά οι ραστερ εικόνες συνήθως αποδίδουν πιο σταθερά σε διαφορετικές εκδόσεις του Word.

---

## Βήμα 3: Αποθήκευση του Βιβλίου Εργασίας ως Αρχείο DOCX

Τώρα που οι επιλογές έχουν οριστεί, απλώς αποθηκεύουμε το βιβλίο εργασίας. Η βιβλιοθήκη φροντίζει για τη μετατροπή όλων των φύλλων εργασίας, πινάκων και—ευχαριστώντας τη σημαία που θέσαμε—διαγραμμάτων ως εικόνες.

```java
// Step 3: Save the workbook as a DOCX file, applying the chart‑export option
workbook.save("YOUR_DIRECTORY/charts.docx", saveOptions);
```

> **Τι λαμβάνετε:** Ένα αρχείο `charts.docx` όπου το αρχικό διάγραμμα Excel εμφανίζεται ως PNG υψηλής ανάλυσης (ή JPEG, ανάλογα με τις ρυθμίσεις σας) μέσα στο έγγραφο Word. Ανοίξτε το στο Microsoft Word για να δείτε το αποτέλεσμα.

---

## Βήμα 4: Επαλήθευση του Αποτελέσματος (Προαιρετικό αλλά Συνιστάται)

Πάντα είναι καλή ιδέα να επαληθεύετε προγραμματιστικά ότι η μετατροπή πέτυχε, ειδικά όταν αυτοματοποιείτε διαδικασίες παρτίδας.

```java
// Optional: Verify that the DOCX file exists and is not empty
File docxFile = new File("YOUR_DIRECTORY/charts.docx");
if (docxFile.exists() && docxFile.length() > 0) {
    System.out.println("Success! DOCX created with chart as image.");
} else {
    System.err.println("Conversion failed – check the source file and options.");
}
```

Αν εκτελέσετε το απόσπασμα και δείτε το μήνυμα επιτυχίας, έχετε επιτυχώς **convert XLSX to DOCX** διατηρώντας τα γραφικά των διαγραμμάτων ως εικόνες.

---

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα Java που συνδυάζει όλα τα βήματα. Απλώς αντικαταστήστε το `YOUR_DIRECTORY` με το πραγματικό μονοπάτι στο σύστημά σας.

```java
import com.aspose.cells.*;

import java.io.File;

public class ExportChartAsImageDemo {
    public static void main(String[] args) throws Exception {
        // Load the Excel workbook containing the chart
        Workbook workbook = new Workbook("YOUR_DIRECTORY/charts.xlsx");

        // Access the first worksheet and its first chart
        Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
        if (chart == null) {
            System.err.println("No chart found in the first worksheet.");
            return;
        }

        // Configure DOCX save options to export charts as images
        DocxSaveOptions saveOptions = new DocxSaveOptions();
        saveOptions.setExportChartAsImage(true);   // Export chart as image

        // Save as DOCX
        String outputPath = "YOUR_DIRECTORY/charts.docx";
        workbook.save(outputPath, saveOptions);

        // Verify the output file
        File outFile = new File(outputPath);
        if (outFile.exists() && outFile.length() > 0) {
            System.out.println("File saved successfully: " + outputPath);
        } else {
            System.err.println("Failed to create the DOCX file.");
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα όταν εκτελέσετε το πρόγραμμα:**

```
File saved successfully: YOUR_DIRECTORY/charts.docx
```

Ανοίξτε το `charts.docx` στο Microsoft Word, και θα δείτε το διάγραμμα να εμφανίζεται ως καθαρή εικόνα, τέλεια τοποθετημένη εκεί που θα ήταν το αρχικό διάγραμμα Excel.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν το βιβλίο εργασίας μου έχει πολλαπλά διαγράμματα;

Δεν χρειάζεται να αλλάξετε τίποτα—η ρύθμιση `setExportChartAsImage(true)` εφαρμόζεται σε **όλα** τα διαγράμματα στο βιβλίο εργασίας. Αν θέλετε μόνο συγκεκριμένα διαγράμματα ως εικόνες, θα πρέπει να τα εξάγετε χειροκίνητα χρησιμοποιώντας `chart.toImage()` και στη συνέχεια να τα εισάγετε στο αρχείο Word μόνοι σας.

### Μπορώ να ελέγξω τη μορφή της εικόνας (PNG vs JPEG);

Aspose.Cells χρησιμοποιεί PNG από προεπιλογή για εξαγωγές διαγράμματος‑ως‑εικόνα. Για να μεταβείτε σε JPEG, μπορείτε να προσαρμόσετε το `ImageOrPrintOptions` πριν την αποθήκευση:

```java
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.getJpeg());
saveOptions.setImageOrPrintOptions(imgOptions);
```

### Λειτουργεί αυτό με παλαιότερα αρχεία Excel (.xls);

Απολύτως. Ο ίδιος κώδικας λειτουργεί και για `.xls` και για `.xlsx`. Η Aspose.Cells ανιχνεύει αυτόματα τη μορφή, ώστε να μπορείτε να **save Excel as Word** ανεξαρτήτως της έκδοσης προέλευσης.

### Πώς διαφέρει αυτό από το “convert Excel to Word” με το εγγενές Office interop;

Το εγγενές interop συχνά απαιτεί μηχανή Windows με εγκατεστημένο το Office, και τα διαγράμματα μπορεί να χάσουν την πιστότητα. Η χρήση της Aspose.Cells είναι ανεξάρτητη από την πλατφόρμα, λειτουργεί σε Linux/macOS, και διατηρεί την ποιότητα των διαγραμμάτων ραστεροποιώντας τα.

---

## Συμβουλές για Υλοποιήσεις Έτοιμες για Παραγωγή

- **Batch processing:** Επανάληψη σε έναν φάκελο αρχείων XLSX, εφαρμόζοντας τις ίδιες `DocxSaveOptions`. Τυλίξτε τη μετατροπή σε μπλοκ try‑catch για να διαχειρίζεστε κατεστραμμένα αρχεία με χάρη.
- **Memory management:** Για πολύ μεγάλα βιβλία εργασίας, καλέστε `workbook.dispose()` μετά την αποθήκευση για να ελευθερώσετε τους εγγενείς πόρους.
- **Customization:** Μπορείτε επίσης να ορίσετε `saveOptions.setPreserveCellFormatting(true)` αν χρειάζεται να διατηρήσετε το στυλ των κελιών αμετάβλητο κατά τη μετατροπή.
- **Logging:** Ενσωματώστε ένα πλαίσιο καταγραφής (SLF4J, Log4j) για να καταγράψετε στατιστικά μετατροπής—χρήσιμο για ίχνη ελέγχου.

---

## Συμπέρασμα

Τώρα έχετε μια στέρεη, ολοκληρωμένη λύση που **export chart as image**, **save Excel as Word**, και **convert XLSX to DOCX** με μόνο λίγες δηλώσεις Java. Το βασικό συμπέρασμα είναι ότι το `DocxSaveOptions` της Aspose.Cells κάνει τη διαχείριση των διαγραμμάτων απλή—χωρίς χειροκίνητη εξαγωγή εικόνας, χωρίς COM interop, και πλήρη υποστήριξη πολλαπλών πλατφορμών.

Αισθανθείτε ελεύθεροι να πειραματιστείτε: δοκιμάστε την εξαγωγή πολλαπλών φύλλων εργασίας, ρυθμίστε τις αναλύσεις εικόνας, ή συνδυάστε αυτήν την προσέγγιση με άλλες βιβλιοθήκες Aspose (όπως Aspose.Words) για ακόμη πιο πλούσια έγγραφα Word. Ο ουρανός είναι το όριο όταν ξέρετε πώς να εξάγετε σωστά το διάγραμμα.

Έχετε περισσότερες ερωτήσεις σχετικά με τη μετατροπή αρχείων Excel, την ενσωμάτωση εικόνων ή τη βελτιστοποίηση απόδοσης; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Μετατροπή Διαγράμματος Excel σε Εικόνα με Aspose.Cells .NET](/cells/english/net/charts-graphs/convert-excel-chart-image-aspose-cells-dotnet/)
- [Πώς να Δημιουργήσετε Διάγραμμα Excel με Γραμμή Τάσης και να το Εξάγετε σε Εικόνα χρησιμοποιώντας Aspose.Cells για Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Μετατροπή Διάγραμμα Πίτας Excel σε Εικόνα Χρησιμοποιώντας Aspose.Cells .NET: Οδηγός Βήμα‑Βήμα](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}