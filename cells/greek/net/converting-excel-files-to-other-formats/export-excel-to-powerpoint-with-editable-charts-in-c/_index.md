---
category: general
date: 2026-09-21
description: Εξαγωγή Excel σε PowerPoint με επεξεργάσιμα γραφήματα χρησιμοποιώντας
  το Aspose.Cells. Ακολουθήστε αυτόν τον οδηγό βήμα‑βήμα για να μετατρέψετε ένα φύλλο
  εργασίας σε PPTX διατηρώντας τα γραφήματα επεξεργάσιμα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- worksheet to powerpoint
- export excel chart pptx
- editable charts pptx
language: el
lastmod: 2026-09-21
og_description: Εξαγωγή Excel σε PowerPoint με επεξεργάσιμα γραφήματα χρησιμοποιώντας
  το Aspose.Cells. Μάθετε πώς να μετατρέψετε ένα φύλλο εργασίας σε PPTX διατηρώντας
  πλήρη επεξεργασιμότητα των γραφημάτων.
og_image_alt: Screenshot of a PowerPoint slide showing an editable Excel chart after
  export
og_title: Εξαγωγή Excel σε PowerPoint με επεξεργάσιμα διαγράμματα – Εγχειρίδιο C#
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  headline: Export Excel to PowerPoint with editable charts in C#
  type: TechArticle
- description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  name: Export Excel to PowerPoint with editable charts in C#
  steps:
  - name: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
    text: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
  - name: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
    text: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
  - name: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
    text: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
  - name: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
    text: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel‑to‑PowerPoint
- PPTX export
title: Εξαγωγή Excel σε PowerPoint με επεξεργάσιμα διαγράμματα σε C#
url: /el/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-editable-charts-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Excel σε PowerPoint με επεξεργάσιμα διαγράμματα σε C#

Η εξαγωγή Excel σε PowerPoint με επεξεργάσιμα διαγράμματα είναι μια κοινή απαίτηση όταν χρειάζεται να επαναχρησιμοποιήσετε τις οπτικές του υπολογιστικού φύλλου σε παρουσιάσεις. Αυτός ο οδηγός δείχνει πώς να **export Excel to PowerPoint** διατηρώντας την επεξεργασιμότητα των διαγραμμάτων, χρησιμοποιώντας το Aspose.Cells for .NET.

Θα μάθετε πώς να:

* Φορτώνετε ένα υπάρχον βιβλίο εργασίας που περιέχει διαγράμματα και πλαίσια κειμένου.  
* Διαμορφώνετε τις επιλογές εξαγωγής PPTX ώστε τα διαγράμματα και τα σχήματα να παραμένουν επεξεργάσιμα.  
* Μετατρέπετε ένα συγκεκριμένο φύλλο εργασίας σε αρχείο PowerPoint που μπορεί να ανοιχθεί και να επεξεργαστεί στο Microsoft PowerPoint.

Ο οδηγός υποθέτει ότι έχετε βασικές γνώσεις C# και μια πρόσφατη έκδοση του .NET (≥ .NET 6). Δεν απαιτείται προηγούμενη εμπειρία με το Aspose.Cells.

---

## Εξαγωγή Excel σε PowerPoint – επισκόπηση

Η βασική ιδέα πίσω από **export Excel to PowerPoint** είναι να αντιμετωπίζετε κάθε φύλλο εργασίας ως πηγή εικόνας που μπορεί να αποδοθεί σε μια διαφάνεια PPTX. Με την ενεργοποίηση των σημαιών `ExportChartAsEditableText` και `ExportShapeAsEditableText`, το Aspose.Cells γράφει τα υποκείμενα δεδομένα του διαγράμματος ως αντικείμενα σχεδίασης του PowerPoint αντί για επίπεδο bitmap. Αυτό κάνει τη διαφάνεια πλήρως επεξεργάσιμη — όπως ένα διάγραμμα που δημιουργείται απευθείας στο PowerPoint.

> **Γιατί να χρησιμοποιείτε επεξεργάσιμα διαγράμματα;**  
> Τα επεξεργάσιμα διαγράμματα επιτρέπουν στους παρουσιαστές να προσαρμόζουν δεδομένα, χρώματα ή ετικέτες χωρίς να επιστρέψουν στο αρχικό αρχείο Excel, επιταχύνοντας τις αλλαγές της τελευταίας στιγμής και διατηρώντας την ροή εργασίας της παρουσίασης ομαλή.

---

## Μετατροπή φύλλου εργασίας σε PowerPoint (worksheet to PowerPoint)

Παρακάτω υπάρχει ένα πλήρες, εκτελέσιμο παράδειγμα που επιδεικνύει τη μετατροπή **worksheet to PowerPoint**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the chart and textbox
            // Replace YOUR_DIRECTORY with the actual folder path on your machine.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Configure PPTX export options to keep charts and shapes editable
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,               // Target format: PPTX
                ExportChartAsEditableText = true,           // Enable editable charts
                ExportShapeAsEditableText = true            // Enable editable shapes/textboxes
            };

            // Step 3: Export the first worksheet (index 0) to a PowerPoint file
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";
            workbook.Worksheets[0].ConvertToImage(exportOptions, outputPath);

            Console.WriteLine($"Worksheet successfully exported to {outputPath}");
        }
    }
}
```

### Επεξήγηση κάθε βήματος

| Step | What the code does | Why it matters for **export excel chart pptx** |
|------|-------------------|----------------------------------------------|
| 1️⃣   | Φορτώνει το `input.xlsx` σε ένα αντικείμενο `Aspose.Cells.Workbook`. | Το βιβλίο εργασίας παρέχει πρόσβαση στα διαγράμματα που θέλετε να εξάγετε. |
| 2️⃣   | Ορίζει το `ExportType` σε `Pptx` και ενεργοποιεί τα `ExportChartAsEditableText` & `ExportShapeAsEditableText`. | Αυτές οι σημαιές είναι το κλειδί για **editable charts pptx** – λένε στη βιβλιοθήκη να γράψει τη γεωμετρία του διαγράμματος ως αντικείμενα σχεδίασης του PowerPoint αντί για εικόνες raster. |
| 3️⃣   | Καλεί τη μέθοδο `ConvertToImage` στο πρώτο φύλλο εργασίας, δημιουργώντας το `Worksheet.pptx`. | Η μέθοδος εκτελεί τη λειτουργία **export excel to powerpoint** και γράφει ένα αρχείο PPTX που μπορεί να ανοιχθεί άμεσα στο PowerPoint. |

> **Pro tip:** Εάν χρειάζεται να εξάγετε *πολλά* φύλλα εργασίας, κάντε βρόχο πάνω στο `workbook.Worksheets` και καλέστε `ConvertToImage` για κάθε ένα, ονομάζοντας προαιρετικά τα αρχεία εξόδου `Sheet1.pptx`, `Sheet2.pptx`, κ.λπ.

---

## Ενεργοποίηση επεξεργάσιμων διαγραμμάτων στο PPTX (export excel chart pptx)

Όταν το `ExportChartAsEditableText` οριστεί σε `true`, το Aspose.Cells γράφει κάθε διάγραμμα ως μια συλλογή στοιχείων `<a:graphic>` μέσα στο XML του PPTX. Το PowerPoint τότε αντιμετωπίζει αυτά τα στοιχεία ως εγγενή αντικείμενα διαγράμματος, τα οποία μπορείτε να κάνετε διπλό‑κλικ για να ανοίξετε τον επεξεργαστή διαγράμματος.

**Συνηθισμένα προβλήματα**

* **Missing Aspose.Cells license** – Χωρίς άδεια η βιβλιοθήκη προσθέτει υδατογράφημα στην έξοδο. Καταχωρίστε άδεια νωρίς στο πρόγραμμα (`License license = new License(); license.SetLicense("Aspose.Cells.lic");`).  
* **Unsupported chart types** – Ενώ τα περισσότερα 2‑D διαγράμματα (στήλη, γραμμή, πίτα) είναι πλήρως επεξεργάσιμα, ορισμένα σύνθετα 3‑D ή συνδυαστικά διαγράμματα μπορεί να επιστρέψουν σε εικόνες. Δοκιμάστε τους συγκεκριμένους τύπους διαγραμμάτων αν βασίζεστε στην πλήρη επεξεργασιμότητα.  
* **Large worksheets** – Η εξαγωγή πολύ μεγάλων φύλλων εργασίας μπορεί να καταναλώσει σημαντική μνήμη. Σκεφτείτε τη χρήση των `ExportMaxRows` ή `ExportMaxColumns` στο `ImageOrPrintOptions` για να περιορίσετε την περιοχή που μετατρέπεται.

---

## Συμβουλές για διατήρηση επεξεργάσιμων διαγραμμάτων (editable charts pptx)

1. **Preserve chart data ranges** – Βεβαιωθείτε ότι η πηγή δεδομένων του διαγράμματος βρίσκεται στο ίδιο φύλλο εργασίας που εξάγετε. Οι αναφορές μεταξύ φύλλων μετατρέπονται σε στατικές τιμές στο PPTX.  
2. **Use the latest Aspose.Cells version** – Οι νέες εκδόσεις βελτιώνουν την υποστήριξη πρόσθετων λειτουργιών διαγράμματος και διορθώνουν σφάλματα άκρων που σχετίζονται με την εξαγωγή PPTX.  
3. **Validate the output** – Μετά τη μετατροπή, ανοίξτε το παραγόμενο PPTX στο PowerPoint και ελέγξτε ότι μπορείτε να επεξεργαστείτε τον τίτλο του διαγράμματος, τις σειρές και τις ετικέτες των αξόνων. Αν κάποιο στοιχείο εμφανίζεται ως εικόνα, ελέγξτε ξανά ότι το `ExportChartAsEditableText` είναι ενεργό και ότι ο τύπος διαγράμματος υποστηρίζεται.  
4. **Batch processing** – Για σενάρια αυτοματοποίησης (π.χ., δημιουργία παρουσίασης από πολλές αναφορές Excel), τυλίξτε τη λογική μετατροπής σε μια μέθοδο που δέχεται `Workbook`, `int worksheetIndex` και `string outputPath`. Αυτό απομονώνει τη ροή εργασίας **export excel to powerpoint** και την καθιστά επαναχρησιμοποιήσιμη.

---

## Συνοπτική παρουσίαση πλήρους παραδείγματος

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το ελάχιστο πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε ένα νέο .NET console project:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Register license (optional but removes evaluation watermark)
            // var license = new License();
            // license.SetLicense("Aspose.Cells.lic");

            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";

            Workbook workbook = new Workbook(inputPath);

            ImageOrPrintOptions options = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,
                ExportChartAsEditableText = true,
                ExportShapeAsEditableText = true
            };

            workbook.Worksheets[0].ConvertToImage(options, outputPath);

            Console.WriteLine($"Export complete: {outputPath}");
        }
    }
}
```

**Expected result**

* Ένα αρχείο με όνομα `Worksheet.pptx` εμφανίζεται στο `YOUR_DIRECTORY`.  
* Το άνοιγμα του αρχείου στο Microsoft PowerPoint εμφανίζει μια διαφάνεια που περιέχει το αρχικό διάγραμμα και τυχόν πλαίσια κειμένου.  
* Κάνοντας διπλό‑κλικ στο διάγραμμα ανοίγει ο επεξεργαστής διαγράμματος του PowerPoint, επιτρέποντάς σας να αλλάξετε τις τιμές των σειρών, τα χρώματα ή τους τίτλους των αξόνων — επαληθεύοντας ότι η λειτουργία **editable charts pptx** λειτουργεί όπως προβλέπεται.

---

## Συμπέρασμα

Τώρα έχετε μια πλήρη λύση για **export Excel to PowerPoint** που διατηρεί τα διαγράμματα επεξεργάσιμα. Με τη διαμόρφωση του `ImageOrPrintOptions` με `ExportChartAsEditableText` και `ExportShapeAsEditableText`, η διαδικασία μετατροπής παράγει ένα εγγενές αρχείο PPTX όπου τα διαγράμματα συμπεριφέρονται όπως αυτά που δημιουργούνται απευθείας στο PowerPoint.  

Από εδώ μπορείτε:

* Να επεκτείνετε τον κώδικα για να διαχειρίζεται πολλαπλά φύλλα εργασίας (**worksheet to PowerPoint** για καθένα).  
* Να συνδυάσετε την εξαγωγή με άλλες δυνατότητες του Aspose.Cells, όπως η προσθήκη τίτλων διαφανειών ή η εισαγωγή εικόνων.  
* Να εξερευνήσετε συναφή θέματα όπως **export Excel chart PPTX** με προσαρμοσμένα θέματα ή την αυτοματοποίηση ολόκληρης της διαδικασίας δημιουργίας παρουσίασης.

Νιώστε ελεύθεροι να πειραματιστείτε με διαφορετικούς τύπους διαγραμμάτων, να προσθέσετε ετικέτες δεδομένων ή να ενσωματώσετε αυτή τη ροή εργασίας σε ένα μεγαλύτερο σύστημα αναφορών. Καλή προγραμματιστική δουλειά!

## Τι θα πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}