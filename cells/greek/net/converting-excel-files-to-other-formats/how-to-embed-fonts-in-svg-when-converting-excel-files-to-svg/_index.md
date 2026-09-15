---
category: general
date: 2026-09-15
description: Μάθετε πώς να ενσωματώνετε γραμματοσειρές σε SVG και να εξάγετε γράφημα
  Excel σε PowerPoint, καλύπτοντας τη μετατροπή XLSX σε SVG και τη μετατροπή XLSX
  σε PPTX με πλήρη παραδείγματα κώδικα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in SVG
- export excel chart to powerpoint
- convert xlsx to svg
- convert xlsx to pptx
- save workbook as svg
language: el
lastmod: 2026-09-15
og_description: Ενσωματώστε γραμματοσειρές σε SVG και εξάγετε διάγραμμα Excel σε PowerPoint
  με βήμα‑βήμα κώδικα C#. Μετατρέψτε XLSX σε SVG και XLSX σε PPTX γρήγορα και αξιόπιστα.
og_image_alt: Screenshot showing an Excel chart exported to PowerPoint with embedded
  fonts in the resulting SVG file
og_title: Ενσωμάτωση γραμματοσειρών σε SVG και εξαγωγή γραφήματος Excel σε PowerPoint
  – πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  headline: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  type: TechArticle
- description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  name: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  steps:
  - name: Open `EditableChart.pptx` in PowerPoint.
    text: Open `EditableChart.pptx` in PowerPoint.
  - name: Locate the slide containing the chart.
    text: Locate the slide containing the chart.
  - name: Choose **Chart Tools → Design → Edit Data**.
    text: Choose **Chart Tools → Design → Edit Data**.
  - name: Confirm that the Excel‑style data grid appears and that you can change values.
    text: Confirm that the Excel‑style data grid appears and that you can change values.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Πώς να ενσωματώσετε γραμματοσειρές σε SVG κατά τη μετατροπή αρχείων Excel σε
  SVG και PowerPoint
url: /el/net/converting-excel-files-to-other-formats/how-to-embed-fonts-in-svg-when-converting-excel-files-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ενσωματώσετε γραμματοσειρές σε SVG κατά τη μετατροπή αρχείων Excel σε SVG και PowerPoint  

Αν χρειάζεστε **ενσωμάτωση γραμματοσειρών σε SVG** κατά τη μετατροπή ενός βιβλίου εργασίας Excel, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε. Θα μάθετε επίσης πώς να **εξάγετε διάγραμμα Excel σε PowerPoint**, και πώς να **μετατρέψετε XLSX σε SVG** και **μετατρέψετε XLSX σε PPTX** με επεξεργάσιμα διαγράμματα.  

Η εργασία με δεδομένα Excel προγραμματιστικά συχνά σημαίνει ότι πρέπει να μεταφέρετε το ίδιο οπτικό περιεχόμενο μεταξύ διαφορετικών μορφών αρχείων. Η χειροκίνητη αναδημιουργία ενός διαγράμματος σε PowerPoint ή η επανεφαρμογή γραμματοσειρών σε SVG είναι επιρρεπής σε σφάλματα και χρονοβόρα. Στο τέλος αυτού του tutorial θα έχετε ένα ενιαίο, επαναχρησιμοποιήσιμο απόσπασμα C# που:

* Αποθηκεύει ένα βιβλίο εργασίας ως αρχείο SVG με ενσωματωμένες γραμματοσειρές και επιλογείς παραλλαγής γραμματοσειρών.  
* Εξάγει το ίδιο βιβλίο εργασίας σε αρχείο PPTX όπου το διάγραμμα παραμένει επεξεργάσιμο.  

Η μόνη προϋπόθεση είναι μια πρόσφατη έκδοση του **Aspose.Cells for .NET** (2024‑x ή νεότερη) και ένα περιβάλλον ανάπτυξης .NET όπως το Visual Studio 2022.

---

## Τι θα χρειαστείτε  

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.8).  
* Πακέτο NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`).  
* Ένα αρχείο Excel (`input.xlsx`) που περιέχει τουλάχιστον ένα διάγραμμα.  
* Δικαίωμα εγγραφής στον φάκελο εξόδου.  

---

## Ενσωμάτωση γραμματοσειρών σε SVG κατά τη μετατροπή XLSX σε SVG  

Η ενσωμάτωση γραμματοσειρών εξασφαλίζει ότι το SVG αποδίδει σωστά σε οποιαδήποτε συσκευή, ακόμη και αν το σύστημα-στόχος δεν διαθέτει τις αρχικές γραμματοσειρές. Η κλάση `SvgSaveOptions` παρέχει δύο σημαίες που το καθιστούν δυνατό: `EmbedFonts` και `FontVariationSelectors`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// OPTIONAL: Use WRAPCOLS to reshape data before export (demonstrates a formula)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)"; // 2 columns per wrap
sheet.Calculate(); // Force calculation so the formula result appears

// Configure SVG options to embed fonts
SvgSaveOptions svgOptions = new SvgSaveOptions
{
    EmbedFonts = true,                // embed fonts in the SVG
    FontVariationSelectors = true    // include variation selectors for better Unicode handling
};

// Save the workbook as an SVG file
string svgPath = @"YOUR_DIRECTORY\WithFonts.svg";
workbook.Save(svgPath, svgOptions);
```

**Γιατί λειτουργεί αυτό:**  
* `EmbedFonts = true` αντιγράφει τα αρχεία γραμματοσειρών στην ενότητα `<defs>` του SVG, εξαλείφοντας τις εξωτερικές εξαρτήσεις.  
* `FontVariationSelectors = true` προσθέτει τους απαραίτητους επιλογείς για γραμματοσειρές που υποστηρίζουν χαρακτηριστικά OpenType, διατηρώντας τις παραλλαγές γλυφών όπως οι συνδέσεις.  

**Αναμενόμενο αποτέλεσμα:** Ανοίξτε το `WithFonts.svg` σε οποιονδήποτε σύγχρονο περιηγητή· το κείμενο μέσα στο διάγραμμα ή στα κελιά εμφανίζεται με την ακριβή γραμματοσειρά που χρησιμοποιείται στο Excel, ακόμη και σε μηχανές που δεν έχουν εγκατεστημένη τη γραμματοσειρά.

---

## Εξαγωγή διαγράμματος Excel σε PowerPoint με επεξεργάσιμα διαγράμματα  

Όταν χρειάζεται να ενσωματώσετε ένα διάγραμμα σε μια διαφάνεια PowerPoint αλλά να επιτρέψετε στον παραλήπτη να επεξεργαστεί τα δεδομένα του διαγράμματος, το `PptxSaveOptions` του Aspose.Cells προσφέρει τη σημαία `ExportEditableChart`.

```csharp
// Configure PPTX options to keep charts editable after export
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableChart = true   // allow chart editing in PowerPoint
};

// Save the same workbook as a PPTX file
string pptxPath = @"YOUR_DIRECTORY\EditableChart.pptx";
workbook.Save(pptxPath, pptxOptions);
```

**Γιατί είναι σημαντικό:**  
Ορίζοντας `ExportEditableChart` σε `true` αποθηκεύει το διάγραμμα ως αντικείμενο Office Open XML αντί για στατική εικόνα. Όταν ανοίξετε το `EditableChart.pptx` στο PowerPoint, μπορείτε να κάνετε δεξί‑κλικ στο διάγραμμα → **Edit Data** και να τροποποιήσετε τις σειρές όπως σε ένα εγγενές διάγραμμα PowerPoint.

**Βήματα επαλήθευσης:**  

1. Ανοίξτε το `EditableChart.pptx` στο PowerPoint.  
2. Εντοπίστε τη διαφάνεια που περιέχει το διάγραμμα.  
3. Επιλέξτε **Chart Tools → Design → Edit Data**.  
4. Επιβεβαιώστε ότι εμφανίζεται το πλέγμα δεδομένων σε στυλ Excel και ότι μπορείτε να αλλάξετε τις τιμές.

---

## Μετατροπή XLSX σε SVG – πλήρης επισκόπηση ροής εργασίας  

Παρακάτω υπάρχει μια συμπαγής έκδοση που συνδυάζει τη φόρτωση, την προαιρετική επεξεργασία δεδομένων και την αποθήκευση ως SVG. Χρησιμοποιήστε το όταν χρειάζεστε μόνο το αποτέλεσμα SVG.

```csharp
public void ConvertXlsxToSvg(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Example: apply a formula to demonstrate cell calculations
    Worksheet ws = wb.Worksheets[0];
    ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
    ws.Calculate();

    SvgSaveOptions opts = new SvgSaveOptions
    {
        EmbedFonts = true,
        FontVariationSelectors = true
    };

    wb.Save(outputPath, opts);
}
```

Καλέστε τη μέθοδο ως εξής:

```csharp
ConvertXlsxToSvg(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.svg");
```

**Συμβουλή για ειδικές περιπτώσεις:** Εάν το βιβλίο εργασίας σας περιέχει προσαρμοσμένες γραμματοσειρές που δεν είναι εγκατεστημένες στον διακομιστή, ενσωματώστε τις χειροκίνητα πριν καλέσετε το `Save`. Χρησιμοποιήστε το `FontInfoCollection` για να προσθέσετε τα αρχεία γραμματοσειρών στις `SvgSaveOptions` μέσω της ιδιότητας `CustomFonts` (διαθέσιμη σε νεότερες εκδόσεις Aspose.Cells).

---

## Μετατροπή XLSX σε PPTX – διατήρηση επεξεργασιμότητας διαγράμματος  

Η παρακάτω βοηθητική μέθοδος δείχνει τη διαδρομή **convert XLSX to PPTX** διασφαλίζοντας ότι το διάγραμμα παραμένει επεξεργάσιμο.

```csharp
public void ConvertXlsxToPptx(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Ensure any chart you want to keep editable is on the first worksheet
    // (Aspose.Cells exports only the first worksheet by default for PPTX)
    PptxSaveOptions opts = new PptxSaveOptions
    {
        ExportEditableChart = true
    };

    wb.Save(outputPath, opts);
}
```

Χρήση:

```csharp
ConvertXlsxToPptx(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.pptx");
```

**Συχνή ερώτηση:** *Τι γίνεται αν το βιβλίο εργασίας μου έχει πολλαπλά φύλλα εργασίας με διαγράμματα;*  
**Απάντηση:** Το Aspose.Cells εξάγει το πρώτο φύλλο εργασίας εξ ορισμού. Για να συμπεριλάβετε επιπλέον φύλλα, επαναλάβετε πάνω στο `workbook.Worksheets`, αντιγράψτε κάθε διάγραμμα σε νέα διαφάνεια και αποθηκεύστε κάθε διαφάνεια ξεχωριστά χρησιμοποιώντας αντικείμενα `Presentation` από το Aspose.Slides. Αυτό το προχωρημένο σενάριο υπερβαίνει τη βασική ροή “αποθήκευση βιβλίου εργασίας ως SVG” και “εξαγωγή διαγράμματος Excel σε PowerPoint”, αλλά οι βασικές σημαίες παραμένουν ίδιες.

---

## Πρακτικές συμβουλές και παγίδες  

* **Performance:** Η ενσωμάτωση γραμματοσειρών αυξάνει το μέγεθος του αρχείου SVG. Εάν το μέγεθος αποτελεί πρόβλημα, ορίστε `EmbedFonts = false` και βασιστείτε σε γραμματοσειρές web‑safe.  
* **Font licensing:** Βεβαιωθείτε ότι έχετε το δικαίωμα να ενσωματώσετε τις γραμματοσειρές που χρησιμοποιείτε· ορισμένες εμπορικές γραμματοσειρές περιορίζουν την ενσωμάτωση.  
* **Chart compatibility:** Τα επεξεργάσιμα διαγράμματα αποθηκεύονται ως τμήματα `chart.xml` μέσα στο PPTX. Πολύ σύνθετα διαγράμματα (π.χ. 3‑Δ ή συνδυαστικά) μπορεί να χάσουν κάποια στυλ όταν επεξεργαστούν στο PowerPoint. Δοκιμάστε τους πιο συνηθισμένους τύπους διαγραμμάτων που χρειάζεστε.  
* **Version mismatches:** Η σημαία `ExportEditableChart` απαιτεί Aspose.Cells 20.10 ή νεότερο. Η χρήση παλαιότερης έκδοσης θα επιστρέψει σιωπηλά σε εικόνα raster.  
* **Thread safety:** Τα αντικείμενα `Workbook` δεν είναι ασφαλή για πολλαπλά νήματα. Δημιουργήστε ένα νέο στιγμιότυπο `Workbook` ανά αίτηση σε σενάριο web service.  

---

## Πλήρες παράδειγμα end‑to‑end  

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class ExcelExportDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputFile = @"YOUR_DIRECTORY\input.xlsx";
        string svgFile   = @"YOUR_DIRECTORY\WithFonts.svg";
        string pptxFile  = @"YOUR_DIRECTORY\EditableChart.pptx";

        // 1. Load workbook
        Workbook workbook = new Workbook(inputFile);

        // 2. Optional: reshape data using WRAPCOLS
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
        sheet.Calculate();

        // 3. Save as SVG with embedded fonts
        SvgSaveOptions svgOpts = new SvgSaveOptions
        {
            EmbedFonts = true,
            FontVariationSelectors = true
        };
        workbook.Save(svgFile, svgOpts);
        Console.WriteLine($"SVG saved with embedded fonts to: {svgFile}");

        // 4. Save as PPTX with editable chart
        PptxSaveOptions pptxOpts = new PptxSaveOptions
        {
            ExportEditableChart = true
        };
        workbook.Save(pptxFile, pptxOpts);
        Console.WriteLine($"PPTX saved with editable chart to: {pptxFile}");
    }
}
```

Η εκτέλεση αυτού του προγράμματος παράγει δύο αρχεία:

* **WithFonts.svg** – ένα SVG που αποδίδει ακριβώς όπως η προβολή του Excel, με ενσωματωμένες γραμματοσειρές.  
* **EditableChart.pptx** – μια παρουσίαση PowerPoint όπου το διάγραμμα μπορεί να επεξεργαστεί άμεσα.

---

## Συμπέρασμα  

Τώρα γνωρίζετε πώς να **ενσωματώσετε γραμματοσειρές σε SVG** όταν **μετατρέπετε XLSX σε SVG**, και πώς να **εξάγετε διάγραμμα Excel σε PowerPoint** διατηρώντας το διάγραμμα επεξεργάσιμο. Ο ίδιος κώδικας δείχνει επίσης έναν καθαρό τρόπο να **αποθηκεύσετε το βιβλίο εργασίας ως SVG** και να **μετατρέψετε XLSX σε PPTX** με ελάχιστη προσπάθεια.  

Από εδώ μπορείτε να εξερευνήσετε περαιτέρω θέματα όπως:

* Προσθήκη προσαρμοσμένων γραμματοσειρών προγραμματιστικά (`svgOptions.CustomFonts`).  
* Επεξεργασία πολλαπλών βιβλίων εργασίας σε παρτίδες σε μια υπηρεσία παρασκηνίου.  
* Χρήση Aspose.Slides για δημιουργία πολυδιαφάνειας αρχείων PPTX που συνδυάζουν πολλά διαγράμματα Excel.  

Πειραματιστείτε με τις επιλογές, προσαρμόστε τα αποσπάσματα στο έργο σας και απολαύστε αξιόπιστες μετατροπές Excel‑to‑SVG/PPTX χωρίς χειροκίνητη επεξεργασία. Καλή προγραμματιστική δουλειά!

## Τι πρέπει να μάθετε στη συνέχεια;

Οι παρακάτω οδηγίες καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [Πώς να μετατρέψετε διαγράμματα Excel σε SVG χρησιμοποιώντας Aspose.Cells για .NET (Οδηγός βήμα προς βήμα)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/german/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/french/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}