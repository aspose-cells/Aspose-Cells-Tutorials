---
category: general
date: 2026-08-04
description: Εξαγωγή γραφήματος Excel σε PowerPoint χρησιμοποιώντας το Aspose.Cells
  σε C#. Ακολουθήστε αυτόν τον οδηγό βήμα‑βήμα για τη μετατροπή από Excel σε PowerPoint
  και διατηρήστε τα σχήματα επεξεργάσιμα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel chart to powerpoint
- Aspose.Cells PPTX export
- editable shapes in PowerPoint
- Excel to PowerPoint conversion
- C# chart export
language: el
lastmod: 2026-08-04
og_description: Εξαγωγή γραφήματος Excel σε PowerPoint με το Aspose.Cells σε C#. Μάθετε
  πώς να δημιουργήσετε ένα επεξεργάσιμο PPTX, να διατηρήσετε τα δεδομένα του γραφήματος
  και να αυτοματοποιήσετε τη μετατροπή από Excel σε PowerPoint.
og_image_alt: Screenshot of an Excel chart rendered as an editable PowerPoint slide
og_title: Εξαγωγή γραφήματος Excel σε PowerPoint με C# – πλήρες σεμινάριο Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  headline: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  type: TechArticle
- description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  name: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  steps:
  - name: Expected output
    text: '| File name | Content on slide | |--------------------------|------------------------------------------|
      | `ShapesExport.pptx` | The chart from `Shapes.xlsx` rendered as an editable
      PowerPoint chart, with axis labels, legends, and data series intact. |'
  - name: Exporting multiple worksheets
    text: If you need a slide for each worksheet, loop through `workbook.Worksheets`
      and call `Save` with a unique file name for each iteration.
  - name: Controlling slide layout
    text: Aspose.Slides lets you add a custom slide layout after the export. Create
      a new presentation, import the generated slide, and then apply a master theme.
  - name: Handling charts with external data sources
    text: If a chart references a data range outside the defined print area, extend
      the `PrintArea` to include those cells. Otherwise the chart may lose data series
      during export.
  - name: Licensing considerations
    text: 'Aspose libraries work in evaluation mode with a watermark. To remove the
      watermark, set the license before any API call:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- PowerPoint
title: Εξαγωγή γραφήματος Excel σε PowerPoint με C# – πλήρης οδηγός Aspose.Cells
url: /el/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή γραφήματος Excel σε PowerPoint με C# – πλήρης οδηγός Aspose.Cells

Αν χρειάζεστε **εξαγωγή γραφήματος Excel σε PowerPoint**, αυτό το tutorial σας δείχνει πώς να το κάνετε με το Aspose.Cells και το Aspose.Slides σε C#. Θα λάβετε ένα πλήρως επεξεργάσιμο PPTX που διατηρεί τα δεδομένα και τα σχήματα του γραφήματος, καθιστώντας τη μετατροπή έτοιμη για περαιτέρω σχεδιαστική εργασία.

Η εξαγωγή γραφημάτων από το Excel στο PowerPoint είναι κοινή απαίτηση όταν δημιουργείτε αυτοματοποιημένες ροές αναφορών, παρουσιάσεις πωλήσεων ή εκπαιδευτικό υλικό. Σε αυτόν τον οδηγό θα μάθετε τα ακριβή βήματα για να εκτελέσετε μια **μετατροπή Excel σε PowerPoint** που διατηρεί όλα τα στοιχεία του γραφήματος επεξεργάσιμα. Δεν απαιτείται χειροκίνητη αντιγραφή‑επικόλληση και ο κώδικας λειτουργεί με .NET 6+ καθώς και με το κλασικό .NET Framework.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

- Έγκυρη άδεια Aspose.Cells (ή ένα δωρεάν κλειδί αξιολόγησης)  
- Aspose.Slides for .NET προστέθηκε στο έργο (η βιβλιοθήκη διαχειρίζεται την έξοδο PPTX)  
- .NET 6 SDK ή νεότερο εγκατεστημένο  
- Ένα βιβλίο εργασίας Excel που περιέχει τουλάχιστον ένα γράφημα (για αυτό το παράδειγμα χρησιμοποιούμε `Shapes.xlsx`)  

Μπορείτε να εγκαταστήσετε τα πακέτα NuGet με τις παρακάτω εντολές:

```bash
dotnet add package Aspose.Cells
dotnet add package Aspose.Slides
```

## Βήμα 1: Φόρτωση του βιβλίου εργασίας Excel

Η πρώτη ενέργεια είναι το άνοιγμα του βιβλίου εργασίας που περιέχει το γράφημα που θέλετε να εξάγετε. Η κλάση `Workbook` αντιπροσωπεύει ολόκληρο το αρχείο Excel.

```csharp
using Aspose.Cells;
using Aspose.Slides;   // required for PPTX output

// Load the Excel workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

**Γιατί είναι σημαντικό:** Η φόρτωση του βιβλίου εργασίας σας δίνει πρόσβαση στα φύλλα εργασίας, τα γραφήματα και τη μορφοποίηση. Το Aspose.Cells διαβάζει το αρχείο χωρίς να απαιτείται εγκατάσταση του Microsoft Office, κάτι που κρατά τη λύση ελαφριά και φιλική προς τον διακομιστή.

## Βήμα 2: Επιλογή φύλλου εργασίας και ορισμός περιοχής εκτύπωσης

Ένα φύλλο εργασίας μπορεί να περιέχει πολλά γραφήματα, αλλά συνήθως εξάγετε μια συγκεκριμένη περιοχή. Ορίζοντας το `PrintArea` λέτε στο Aspose.Cells ποιες κυψέλες (συμπεριλαμβανομένων των γραφημάτων) πρέπει να αποδοθούν.

```csharp
// Choose the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Define the area that contains the chart and any supporting data
worksheet.PageSetup.PrintArea = "A1:G30";
```

**Γιατί είναι σημαντικό:** Περιορίζοντας την εξαγωγή σε μια καθορισμένη περιοχή εκτύπωσης αποφεύγετε περιττές κενές διαφάνειες και κρατάτε το μέγεθος του αρχείου PPTX μικρό. Η περιοχή μπορεί να προσαρμοστεί ώστε να ταιριάζει ακριβώς με το εύρος του γραφήματος.

## Βήμα 3: Διαμόρφωση επιλογών εξαγωγής για επεξεργάσιμο PPTX

Το Aspose.Cells χρησιμοποιεί την κλάση `ImageOrPrintOptions` για να ελέγξει τη μορφή εξόδου και την επεξεργασιμότητα. Ορίζοντας `ImageFormat` σε `ImageFormat.Pptx` δημιουργείται αρχείο PowerPoint, ενώ `ExportEditableShapes = true` διατηρεί τα αντικείμενα του γραφήματος ως επεξεργάσιμα σχήματα.

```csharp
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Pptx,   // Target format
    ExportEditableShapes = true       // Keep shapes/textboxes editable
};

// Attach the options to the worksheet's print settings
worksheet.PageSetup.PrintOptions = exportOptions;
```

**Γιατί είναι σημαντικό:** Η σημαία `ExportEditableShapes` είναι το κλειδί για ένα αποτέλεσμα **επεξεργάσιμων σχημάτων σε PowerPoint**. Χωρίς αυτήν, το γράφημα θα μετατραπεί σε εικόνα raster, χάνοντας τη δυνατότητα τροποποίησης των σημείων δεδομένων ή του στυλ αργότερα.

## Βήμα 4: Αποθήκευση του φύλλου εργασίας ως παρουσίαση PowerPoint

Τέλος, καλέστε τη μέθοδο `Save` στο αντικείμενο `Workbook`. Το enum `SaveFormat.Pptx` λέει στο Aspose.Cells να παραγάγει αρχείο PowerPoint.

```csharp
// Export the selected worksheet to a PPTX file
workbook.Save("YOUR_DIRECTORY/ShapesExport.pptx", SaveFormat.Pptx);
```

Όταν ολοκληρωθεί ο κώδικας, ανοίξτε το `ShapesExport.pptx` στο PowerPoint. Θα δείτε μια διαφάνεια που περιέχει το αρχικό γράφημα Excel ως εγγενές αντικείμενο γραφήματος PowerPoint. Κάντε διπλό‑κλικ στο γράφημα για να επεξεργαστείτε τα δεδομένα, να αλλάξετε χρώματα ή να προσθέσετε εφέ—όπως αν το είχατε δημιουργήσει απευθείας στο PowerPoint.

### Αναμενόμενο αποτέλεσμα

| Όνομα αρχείου            | Περιεχόμενο στη διαφάνεια                |
|--------------------------|------------------------------------------|
| `ShapesExport.pptx`      | Το γράφημα από το `Shapes.xlsx` αποδομένο ως επεξεργάσιμο γράφημα PowerPoint, με ετικέτες αξόνων, υπομνήματα και σειρές δεδομένων αμετάβλητες. |

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε, επικολλήσετε και εκτελέσετε. Περιλαμβάνει όλες τις απαραίτητες δηλώσεις `using`, διαχείριση σφαλμάτων και σχόλια.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;   // Required for PPTX output

class ExcelToPowerPoint
{
    static void Main()
    {
        // Path to the source Excel file – adjust as needed
        const string excelPath = "YOUR_DIRECTORY/Shapes.xlsx";
        // Path for the generated PowerPoint file
        const string pptxPath = "YOUR_DIRECTORY/ShapesExport.pptx";

        try
        {
            // Load the workbook
            Workbook workbook = new Workbook(excelPath);

            // Use the first worksheet (you can change the index or name)
            Worksheet worksheet = workbook.Worksheets[0];

            // Define the area that contains the chart
            worksheet.PageSetup.PrintArea = "A1:G30";

            // Set export options for PPTX with editable shapes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Pptx,
                ExportEditableShapes = true
            };
            worksheet.PageSetup.PrintOptions = exportOptions;

            // Save as PPTX
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export successful. PPTX saved to: {pptxPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**Επεξήγηση κάθε τμήματος**

| Τμήμα | Σκοπός |
|-------|--------|
| `using` directives | Εισάγει τα namespaces του Aspose.Cells και Aspose.Slides. |
| `Workbook workbook = new Workbook(excelPath);` | Φορτώνει το αρχείο Excel χωρίς να απαιτείται εγκατάσταση του Office. |
| `worksheet.PageSetup.PrintArea = "A1:G30";` | Περιορίζει την εξαγωγή στην περιοχή που περιέχει το γράφημα. |
| `ImageOrPrintOptions` | Διαμορφώνει την έξοδο PPTX και ενεργοποιεί την **εξαγωγή PPTX του Aspose.Cells** με επεξεργάσιμα σχήματα. |
| `workbook.Save(pptxPath, SaveFormat.Pptx);` | Γράφει το αρχείο PowerPoint στο δίσκο. |
| `try / catch` | Παρέχει βασική διαχείριση σφαλμάτων για ελλιπή αρχεία ή προβλήματα άδειας. |

Εκτελώντας αυτό το πρόγραμμα παράγεται μια διαφάνεια PowerPoint που μπορείτε να ανοίξετε στο Microsoft PowerPoint, Google Slides (μετά τη μετατροπή) ή σε οποιονδήποτε συμβατό προβολέα.

## Κοινές παραλλαγές και ειδικές περιπτώσεις

### Εξαγωγή πολλαπλών φύλλων εργασίας

Αν χρειάζεστε μια διαφάνεια για κάθε φύλλο εργασίας, κάντε βρόχο μέσω του `workbook.Worksheets` και καλέστε `Save` με μοναδικό όνομα αρχείου για κάθε επανάληψη.

```csharp
int index = 1;
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.PageSetup.PrintOptions = exportOptions;
    string fileName = $"Slide{index++}.pptx";
    workbook.Save(fileName, SaveFormat.Pptx);
}
```

### Έλεγχος διάταξης διαφάνειας

Το Aspose.Slides σας επιτρέπει να προσθέσετε προσαρμοσμένη διάταξη διαφάνειας μετά την εξαγωγή. Δημιουργήστε μια νέα παρουσίαση, εισάγετε τη δημιουργημένη διαφάνεια και, στη συνέχεια, εφαρμόστε ένα master theme.

```csharp
using Aspose.Slides.Export;

// Load the PPTX created by Aspose.Cells
Presentation pres = new Presentation(pptxPath);

// Apply a built‑in layout (e.g., Title and Content)
pres.Slides[0].LayoutSlide = pres.LayoutSlides[(int)SlideLayoutType.TitleAndContent];

// Save the final presentation
pres.Save("FinalPresentation.pptx", SaveFormat.Pptx);
```

### Διαχείριση γραφημάτων με εξωτερικές πηγές δεδομένων

Αν ένα γράφημα αναφέρεται σε εύρος δεδομένων εκτός της καθορισμένης περιοχής εκτύπωσης, επεκτείνετε το `PrintArea` ώστε να περιλαμβάνει αυτά τα κελιά. Διαφορετικά το γράφημα μπορεί να χάσει σειρές δεδομένων κατά την εξαγωγή.

### Θεωρήσεις αδειοδότησης

Οι βιβλιοθήκες Aspose λειτουργούν σε λειτουργία αξιολόγησης με υδατογράφημα. Για να αφαιρέσετε το υδατογράφημα, ορίστε την άδεια πριν από οποιαδήποτε κλήση API:

```csharp
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

Κάντε το ίδιο και για το Aspose.Slides εάν χρησιμοποιείτε τις προχωρημένες του δυνατότητες.

## Pro tips

- **Επαναχρησιμοποίηση επιλογών εξαγωγής:** Δημιουργήστε ένα μόνο αντικείμενο `ImageOrPrintOptions` και αντιστοιχίστε το σε κάθε φύλλο εργασίας για να διατηρήσετε τον κώδικα DRY.  
- **Επεξεργασία παρτίδας:** Για μεγάλης κλίμακας αναφορές, συνδυάστε αυτή τη λογική εξαγωγής με ένα background worker ή Azure Function για δημιουργία αρχείων PPTX κατ' απαίτηση.  
- **Απόδοση:** Αν χρειάζεστε μόνο την εικόνα του γραφήματος (μη επεξεργάσιμη), ορίστε `ExportEditableShapes = false`. Αυτό μειώνει τη χρήση μνήμης και επιταχύνει τη μετατροπή.  
- **Δοκιμή:** Επαληθεύστε το παραγόμενο PPTX τόσο σε εγκαταστάσεις PowerPoint Windows όσο και macOS, καθώς ορισμένα προβλήματα απόδοσης διαφέρουν μεταξύ των πλατφορμών.

## Συμπέρασμα

Τώρα έχετε μια πλήρη, end‑to‑end λύση για **εξαγωγή γραφήματος Excel σε PowerPoint** χρησιμοποιώντας C#. Ο οδηγός κάλυψε τη φόρτωση του βιβλίου εργασίας, την επιλογή της περιοχής εκτύπωσης, τη διαμόρφωση **εξαγωγής PPTX του Aspose.Cells** με **επεξεργάσιμα σχήματα σε PowerPoint**, και την αποθήκευση του αποτελέσματος ως πλήρως επεξεργάσιμο αρχείο PPTX.  

Από εδώ μπορείτε να εξερευνήσετε επιπλέον **σενάρια μετατροπής Excel σε PowerPoint** όπως εξαγωγή παρτίδας, προσαρμοσμένες διατάξεις διαφάνειας ή ενσωμάτωση της διαδικασίας σε web API. Πειραματιστείτε με διαφορετικούς τύπους γραφημάτων, προσθέστε εικόνες ή συνδυάστε πολλαπλά φύλλα εργασίας σε μία παρουσίαση για να προσαρμόσετε το αποτέλεσμα στις επιχειρηματικές σας ανάγκες.

Έτοιμοι να αυτοματοποιήσετε τη ροή εργασίας αναφορών σας; Δοκιμάστε να αλλάξετε το αρχείο προέλευσης, να ρυθμίσετε την περιοχή εκτύπωσης και να ενσωματώσετε τον κώδικα στις υπάρχουσες .NET υπηρεσίες σας. Καλό κώδικα!

## Τι πρέπει να μάθετε στη συνέχεια;

Οι παρακάτω οδηγίες καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Μετατρέψετε Excel σε PowerPoint Χρησιμοποιώντας Aspose.Cells για .NET: Πλήρης Οδηγός](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Πώς να Εξάγετε Γραφήματα Excel σε PDF Χρησιμοποιώντας Aspose.Cells για .NET: Οδηγός Βήμα-Βήμα](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Εξαγωγή Κελιών Excel σε Εικόνα Χρησιμοποιώντας Aspose.Cells .NET: Οδηγός Βήμα-Βήμα](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}