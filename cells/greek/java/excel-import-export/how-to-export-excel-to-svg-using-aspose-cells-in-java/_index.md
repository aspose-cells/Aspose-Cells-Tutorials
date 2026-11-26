---
category: general
date: 2026-11-25
description: Εξαγωγή Excel σε SVG με το Aspose.Cells σε Java – ένας οδηγός βήμα‑προς‑βήμα
  για την αποθήκευση του Excel ως SVG και τη δημιουργία εικόνας διανύσματος.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to svg
- save excel as svg
- excel to vector image
- convert excel to svg
- export excel as svg
language: el
lastmod: 2026-11-25
og_description: Εξαγωγή Excel σε SVG με το Aspose.Cells σε Java. Μάθετε πώς να αποθηκεύετε
  το Excel ως SVG και να δημιουργείτε υψηλής ποιότητας διανυσματικές εικόνες με λίγες
  γραμμές κώδικα.
og_image_alt: Screenshot of an Excel worksheet exported to SVG format
og_title: Εξαγωγή Excel σε SVG σε Java – πλήρες σεμινάριο Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Export Excel to SVG with Aspose.Cells in Java – a step‑by‑step guide
    to save Excel as SVG and create a vector image.
  headline: How to export Excel to SVG using Aspose.Cells in Java
  type: TechArticle
- description: Export Excel to SVG with Aspose.Cells in Java – a step‑by‑step guide
    to save Excel as SVG and create a vector image.
  name: How to export Excel to SVG using Aspose.Cells in Java
  steps:
  - name: Load the workbook containing the data
    text: '```java import com.aspose.cells.Workbook;'
  - name: Set up image export options for SVG
    text: '```java import com.aspose.cells.ImageOrPrintOptions; import com.aspose.cells.ImageFormat;'
  - name: Save the workbook as an SVG file
    text: '```java import com.aspose.cells.SaveFormat;'
  - name: What to explore next
    text: '* **Export Excel as PNG or JPEG** – change `exportOptions.setImageFormat(ImageFormat.PNG)`
      for raster output. * **Convert Excel to PDF** – use `PdfSaveOptions` for printable
      documents. * **Batch processing** – combine the above code with a file‑system
      watcher to automatically **convert Excel to SVG*'
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
- Excel
title: Πώς να εξάγετε το Excel σε SVG χρησιμοποιώντας το Aspose.Cells σε Java
url: /el/java/excel-import-export/how-to-export-excel-to-svg-using-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εξάγετε το Excel σε SVG χρησιμοποιώντας το Aspose.Cells σε Java

Αν χρειάζεστε **εξαγωγή Excel σε SVG**, αυτός ο οδηγός σας δείχνει πώς να το κάνετε με το Aspose.Cells για Java. Θα μάθετε πώς να **αποθηκεύσετε το Excel ως SVG** και να δημιουργήσετε μια υψηλής ποιότητας **διανυσματική εικόνα** με λίγες μόνο γραμμές κώδικα.

Η εξαγωγή ενός βιβλίου εργασίας Excel σε αρχείο SVG σας επιτρέπει να ενσωματώσετε το φύλλο σε ιστοσελίδες, αναφορές ή οποιοδήποτε περιβάλλον που προτιμά κλιμακώσιμα γραφικά. Η μορφή SVG διατηρεί τις γραμματοσειρές, τα χρώματα και τα περιθώρια των κελιών χωρίς την εικονοστοιχειοποίηση που εμφανίζεται σε raster εικόνες.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Java 17 ή νεότερη εγκατεστημένη.
* Ένα ενεργό άδεια χρήσης Aspose.Cells για Java (ή ένα προσωρινό κλειδί αξιολόγησης).
* Ένα έργο Maven ή Gradle όπου μπορείτε να προσθέσετε την εξάρτηση Aspose.Cells.

Προσθέστε τη βιβλιοθήκη Aspose.Cells στο έργο σας:

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

```gradle
// Gradle
implementation 'com.aspose:aspose-cells:24.10'
```

## Εξαγωγή Excel σε SVG – βήμα‑βήμα

Η διαδικασία αποτελείται από τρία απλά βήματα: φόρτωση του βιβλίου εργασίας, ρύθμιση των επιλογών εξαγωγής SVG και αποθήκευση του αποτελέσματος. Κάθε βήμα εξηγείται παρακάτω.

### Βήμα 1: Φορτώστε το βιβλίο εργασίας που περιέχει τα δεδομένα

```java
import com.aspose.cells.Workbook;

public class ExcelToSvgDemo {
    public static void main(String[] args) throws Exception {
        // Load the Excel file you want to convert.
        Workbook workbook = new Workbook("C:/Data/Report.xlsx");
        // Continue with export options...
    }
}
```

**Γιατί είναι σημαντικό:**  
`Workbook` είναι το κεντρικό αντικείμενο στο Aspose.Cells. Η φόρτωση του αρχείου μία φορά σας δίνει πρόσβαση σε όλα τα φύλλα εργασίας, τα στυλ και τα ενσωματωμένα αντικείμενα, τα οποία ο εξαγωγέας SVG θα αποδώσει αργότερα.

### Βήμα 2: Ρυθμίστε τις επιλογές εξαγωγής εικόνας για SVG

```java
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.ImageFormat;

ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
exportOptions.setImageFormat(ImageFormat.SVG); // Guarantees a vector output
exportOptions.setOnePagePerSheet(true);       // Export each sheet as a single SVG page
exportOptions.setTransparent(true);           // Preserve transparent backgrounds
```

**Γιατί είναι σημαντικό:**  
`ImageOrPrintOptions` σας επιτρέπει να ελέγξετε τη μορφή εξόδου. Η επιλογή `ImageFormat.SVG` εξασφαλίζει ότι το αποτέλεσμα είναι μια **διανυσματική εικόνα** αντί για bitmap. Η ενεργοποίηση του `OnePagePerSheet` αποτρέπει τις διακοπές σελίδας μέσα σε ένα φύλλο, κάτι που συνήθως προτιμάται όταν το SVG θα εμφανιστεί σε web view.

### Βήμα 3: Αποθηκεύστε το βιβλίο εργασίας ως αρχείο SVG

```java
import com.aspose.cells.SaveFormat;

workbook.save("C:/Output/Report.svg", exportOptions);
System.out.println("Excel workbook successfully exported to SVG.");
```

**Γιατί είναι σημαντικό:**  
Η μέθοδος `save` συνδυάζει το φορτωμένο βιβλίο εργασίας με τις ρυθμισμένες `exportOptions`. Η κλήση γράφει ένα πλήρως συμβατό αρχείο SVG που μπορεί να ανοιχθεί σε προγράμματα περιήγησης, Inkscape ή οποιονδήποτε επεξεργαστή που υποστηρίζει διανυσματικά γραφικά.

## Πλήρες εκτελέσιμο παράδειγμα

Συνδυάζοντας τα τρία βήματα παίρνετε ένα αυτόνομο πρόγραμμα που μπορείτε να μεταγλωττίσετε και να εκτελέσετε αμέσως:

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook
        Workbook workbook = new Workbook("C:/Data/FontVariation.xlsx");

        // 2. Configure SVG export options
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setImageFormat(ImageFormat.SVG);
        exportOptions.setOnePagePerSheet(true);
        exportOptions.setTransparent(true);

        // 3. Export to SVG
        workbook.save("C:/Output/WithVariationSelectors.svg", exportOptions);
        System.out.println("Export complete: Excel saved as SVG.");
    }
}
```

**Αναμενόμενη έξοδος**

Η εκτέλεση του προγράμματος εκτυπώνει:

```
Export complete: Excel saved as SVG.
```

Θα βρείτε το `WithVariationSelectors.svg` στο `C:/Output`. Το άνοιγμα του αρχείου σε πρόγραμμα περιήγησης εμφανίζει το φύλλο εργασίας ως κλιμακώσιμα γραφικά, με το κείμενο, τα περιθώρια και τα χρώματα των κελιών διατηρημένα.

## Συνηθισμένες παραλλαγές και ειδικές περιπτώσεις

| Κατάσταση | Συνιστώμενη προσαρμογή |
|-----------|------------------------|
| **Πολλαπλά φύλλα εργασίας** | Επανάληψη μέσω `workbook.getWorksheets()` και κλήση `save` για κάθε φύλλο, προαιρετικά προσθέτοντας το όνομα του φύλλου στο όνομα του αρχείου. |
| **Μεγάλα βιβλία εργασίας** | Αυξήστε το `exportOptions.setRenderThreadCount(int)` για χρήση παράλληλης απόδοσης, μειώνοντας το χρόνο μετατροπής. |
| **Προσαρμοσμένο DPI** | Κλήση `exportOptions.setHorizontalResolution(int)` και `exportOptions.setVerticalResolution(int)` για έλεγχο της κλίμακας viewBox του SVG. |
| **Ενσωμάτωση γραμματοσειρών** | Ορίστε `exportOptions.setExportFontAsSVG(true)` για ενσωμάτωση των ορισμών γραμματοσειράς απευθείας στο SVG, εξασφαλίζοντας οπτική πιστότητα σε μηχανές χωρίς τις αρχικές γραμματοσειρές. |
| **Αρχεία με κωδικό πρόσβασης** | Παρέχετε τον κωδικό κατά τη φόρτωση: `Workbook workbook = new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("pwd"); }});` |

## Pro tips

* **Αποφύγετε την εναλλαγή σε raster** – Αν ένα φύλλο περιέχει σύνθετα διαγράμματα, ελέγξτε ότι εμφανίζονται ως διανυσματικά στοιχεία στο SVG. Αν όχι, ενεργοποιήστε `exportOptions.setExportChartAsSVG(true)`.
* **Απόδοση** – Για μαζικές μετατροπές, επαναχρησιμοποιήστε ένα μόνο αντικείμενο `ImageOrPrintOptions` αντί να δημιουργείτε νέο για κάθε αρχείο.
* **Δοκιμή** – Επικυρώστε το παραγόμενο SVG με έναν online validator (π.χ., W3C SVG Validator) για να εντοπίσετε τυχόν λανθασμένο markup νωρίς.

## Επαληθεύστε τη μετατροπή

Μπορείτε προγραμματιστικά να επιβεβαιώσετε ότι το αρχείο εξόδου είναι πράγματι SVG:

```java
import java.nio.file.Files;
import java.nio.file.Paths;

byte[] data = Files.readAllBytes(Paths.get("C:/Output/Report.svg"));
String content = new String(data, "UTF-8");
if (content.contains("<svg")) {
    System.out.println("File is a valid SVG.");
}
```

Η παρουσία του ριζικού στοιχείου `<svg>` υποδεικνύει μια επιτυχημένη **μετατροπή Excel σε SVG**.

## Συμπέρασμα

Αυτό το tutorial έδειξε πώς να **εξάγετε το Excel σε SVG** χρησιμοποιώντας το Aspose.Cells για Java. Φορτώνοντας το βιβλίο εργασίας, ρυθμίζοντας το `ImageOrPrintOptions` για SVG και καλώντας το `save`, μπορείτε να **αποθηκεύσετε το Excel ως SVG** και να αποκτήσετε μια καθαρή **μετατροπή Excel σε διανυσματική εικόνα**. Από εδώ μπορείτε να ενσωματώσετε το SVG σε ιστοσελίδες, να το συμπεριλάβετε σε τεκμηρίωση ή να το επεξεργαστείτε περαιτέρω με οποιοδήποτε εργαλείο διανυσματικών γραφικών.

### Τι να εξερευνήσετε στη συνέχεια

* **Εξαγωγή Excel ως PNG ή JPEG** – αλλάξτε σε `exportOptions.setImageFormat(ImageFormat.PNG)` για raster έξοδο.
* **Μετατροπή Excel σε PDF** – χρησιμοποιήστε `PdfSaveOptions` για έγγραφα εκτυπώσιμα.
* **Μαζική επεξεργασία** – συνδυάστε τον παραπάνω κώδικα με έναν παρατηρητή συστήματος αρχείων για αυτόματη **μετατροπή Excel σε SVG** για κάθε νέο βιβλίο εργασίας σε έναν φάκελο.

Πειραματιστείτε με τις επιλογές και αφήστε την ευελιξία του Aspose.Cells να μετατρέψει τα δεδομένα Excel σας σε οποιαδήποτε οπτική μορφή χρειάζεστε. Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να εξάγετε διαγράμματα Excel ως SVG χρησιμοποιώντας το Aspose.Cells Java για κλιμακώσιμα διανυσματικά γραφικά](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Πώς να δημιουργήσετε και να αποθηκεύσετε ένα βιβλίο εργασίας Excel ως SVG χρησιμοποιώντας το Aspose.Cells για Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Πώς να εξάγετε το Excel σε SVG – Οδηγός βήμα‑βήμα για Java](/cells/english/java/excel-import-export/how-to-export-excel-to-svg-step-by-step-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}