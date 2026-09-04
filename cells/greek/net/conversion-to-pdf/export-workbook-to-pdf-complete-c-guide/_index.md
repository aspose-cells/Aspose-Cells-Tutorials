---
category: general
date: 2026-02-26
description: Εξαγωγή βιβλίου εργασίας σε PDF με ενσωματωμένες γραμματοσειρές και επίσης
  εξαγωγή διαγραμμάτων σε PowerPoint με C#. Μάθετε πώς να αντιγράψετε το φύλλο εργασίας
  με πίνακα Pivot και να αποθηκεύσετε το βιβλίο εργασίας ως PPTX.
draft: false
keywords:
- export workbook to pdf
- export charts to powerpoint
- copy pivot table worksheet
- embed fonts pdf export
- save workbook as pptx
language: el
og_description: Εξαγωγή βιβλίου εργασίας σε PDF με ενσωματωμένες γραμματοσειρές και
  επίσης εξαγωγή διαγραμμάτων σε PowerPoint με C#. Ακολουθήστε τον οδηγό βήμα‑προς‑βήμα
  για αντιγραφή πινάκων Pivot και αποθήκευση ως PPTX.
og_title: Εξαγωγή βιβλίου εργασίας σε PDF – Πλήρης οδηγός C#
tags:
- Aspose.Cells
- Aspose.Slides
- C#
- Reporting
title: Εξαγωγή βιβλίου εργασίας σε PDF – Πλήρης οδηγός C#
url: /el/net/conversion-to-pdf/export-workbook-to-pdf-complete-c-guide/
---

.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Φύλλου Εργασίας σε PDF – Πλήρης Οδηγός C#

Η εξαγωγή φύλλου εργασίας σε PDF είναι μια συχνή απαίτηση όταν χρειάζεται να μοιραστείτε αναφορές με ενδιαφερόμενους που ενδέχεται να μην έχουν εγκατεστημένο το Excel. Σε αυτό το tutorial θα σας δείξουμε επίσης πώς να **εξάγετε διαγράμματα σε PowerPoint**, να αντιγράψετε ένα **φύλλο εργασίας PivotTable**, και να ενσωματώσετε γραμματοσειρές ώστε το PDF να φαίνεται ακριβώς όπως το σχέδιο στην οθόνη.  

Έχετε αναρωτηθεί ποτέ γιατί μερικά PDF χάνουν την αρχική διάταξη ή γιατί οι διαφάνειες PowerPoint εμφανίζουν ελλιπή σχήματα; Η απάντηση συνήθως κρύβεται σε ελλιπείς επιλογές κατά τη διαδικασία εξαγωγής. Στο τέλος αυτού του οδηγού θα έχετε μια ενιαία, επαναχρησιμοποιήσιμη μέθοδο C# που αντιμετωπίζει όλα αυτά τα προβλήματα — χωρίς χειροκίνητο copy‑pasting ή παρεμβάσεις στις ρυθμίσεις εξαγωγής.

## Τι Θα Μάθετε

- Πώς να δημιουργήσετε ένα φύλλο εργασίας, να προσθέσετε εκφράσεις Smart Marker και να τις επεξεργαστείτε.  
- Πώς να **αντιγράψετε ένα φύλλο εργασίας PivotTable** χωρίς να διακόψετε την πηγή δεδομένων.  
- Πώς να **εξάγετε διαγράμματα, σχήματα και πλαίσια κειμένου** σε παρουσίαση PowerPoint διατηρώντας τα επεξεργάσιμα.  
- Πώς να **ενσωματώσετε τυπικές γραμματοσειρές** κατά την εξαγωγή PDF για συνεπή απόδοση σε οποιονδήποτε υπολογιστή.  
- Πώς να **αποθηκεύσετε το φύλλο εργασίας ως PPTX** χρησιμοποιώντας τη μέθοδο `save workbook as pptx`.  

Όλα αυτά λειτουργούν με τις τελευταίες βιβλιοθήκες Aspose.Cells και Aspose.Slides .NET (έκδοση 23.11 τη στιγμή της συγγραφής). Χωρίς εξωτερικά εργαλεία, χωρίς scripts επεξεργασίας μετά‑εξαγωγής — μόνο καθαρό C#.

> **Pro tip:** Αν ήδη χρησιμοποιείτε το Aspose στο έργο σας, μπορείτε να ενσωματώσετε τα αποσπάσματα κώδικα όπως είναι· διαφορετικά, προσθέστε πρώτα τα πακέτα NuGet `Aspose.Cells` και `Aspose.Slides`.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7.2).  
- Visual Studio 2022 (ή οποιοδήποτε IDE προτιμάτε).  
- Aspose.Cells .NET και Aspose.Slides .NET εγκατεστημένα μέσω NuGet.  
- Βασική εξοικείωση με C# και έννοιες του Excel όπως Smart Markers και PivotTables.  

---

![Διάγραμμα εξαγωγής φύλλου εργασίας σε PDF](export-workbook-to-pdf.png "Ροή εργασίας εξαγωγής φύλλου εργασίας σε PDF που δείχνει εξόδους PDF και PPTX")

## Εξαγωγή Φύλλου Εργασίας σε PDF – Υλοποίηση Βήμα‑βήμα

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα. Δημιουργεί ένα φύλλο εργασίας, ενσωματώνει εκφράσεις Smart Marker, τις επεξεργάζεται, αντιγράφει μια περιοχή PivotTable και τελικά αποθηκεύει τόσο ένα PDF όσο και ένα αρχείο PowerPoint.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides.Export;

namespace ReportExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Build the workbook and add Smart Markers
            // -------------------------------------------------
            var reportWorkbook = new Workbook();
            Worksheet dataSheet = reportWorkbook.Worksheets[0];

            // Header with a variable department name
            dataSheet.Cells["A1"].PutValue("Report for ${$dept=Department}");

            // Conditional text based on department
            dataSheet.Cells["A2"].PutValue("${if $dept == \"Sales\"}Sales Summary${else}Other Summary${/if}");

            // Table header for orders – this will be repeated for each order
            dataSheet.Cells["A5:D5"].PutValue("${Orders.Product}|${Orders.Quantity}|${Orders.Price}");

            // -------------------------------------------------
            // Step 2: Process Smart Markers and name the detail sheet
            // -------------------------------------------------
            reportWorkbook.SmartMarkerProcessor.Options.DetailSheetNewName = "Orders_${$dept}";
            reportWorkbook.SmartMarkerProcessor.Process();

            // -------------------------------------------------
            // Step 3: Copy the range that contains the pivot table
            // -------------------------------------------------
            // Assume the pivot table lives in A1:G30 on the original sheet
            Range sourceRange = dataSheet.Cells.CreateRange("A1", "G30");
            Worksheet copySheet = reportWorkbook.Worksheets.Add("Copy");
            sourceRange.Copy(copySheet.Cells["A1"]);   // Pivot table is duplicated intact

            // -------------------------------------------------
            // Step 4: Export to PowerPoint (keep charts, shapes, text boxes)
            // -------------------------------------------------
            var pptOptions = new PresentationOptions
            {
                ExportCharts = true,
                ExportShapes = true,
                ExportTextBoxes = true
            };
            string pptPath = @"C:\Temp\FinalPresentation.pptx";
            reportWorkbook.Save(pptPath, SaveFormat.Pptx, pptOptions);

            // -------------------------------------------------
            // Step 5: Export to PDF and embed standard fonts
            // -------------------------------------------------
            var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
            string pdfPath = @"C:\Temp\FinalReport.pdf";
            reportWorkbook.Save(pdfPath, pdfOptions);

            Console.WriteLine("Export completed:");
            Console.WriteLine($" • PDF saved to {pdfPath}");
            Console.WriteLine($" • PowerPoint saved to {pptPath}");
        }
    }
}
```

### Γιατί Λειτουργεί Αυτό

1. **Επεξεργασία Smart Marker** σας επιτρέπει να γεμίσετε το φύλλο εργασίας από οποιαδήποτε πηγή δεδομένων (JSON, DataTables κ.λπ.) χωρίς να γράψετε βρόχους.  
2. **DetailSheetNewName** δημιουργεί ξεχωριστό φύλλο για κάθε τμήμα, παρέχοντάς σας μια καθαρή καρτέλα ανά τμήμα.  
3. **Αντιγραφή της περιοχής** (`sourceRange.Copy`) διπλασιάζει το PivotTable *συμπεριλαμβανομένου* της κρυφής μνήμης (cache), ώστε το αντιγραμμένο φύλλο να συμπεριφέρεται ακριβώς όπως το αρχικό.  
4. **PresentationOptions** με `ExportCharts`, `ExportShapes` και `ExportTextBoxes` λέει στο Aspose να αποδώσει αυτά τα αντικείμενα ως εγγενή στοιχεία PowerPoint, διατηρώντας την επεξεργασιμότητα.  
5. **PdfSaveOptions.EmbedStandardFonts** εξασφαλίζει ότι το PDF φαίνεται πανομοιότυπο σε υπολογιστές που δεν έχουν εγκατεστημένες τις αρχικές γραμματοσειρές.  

Το αποτέλεσμα είναι δύο αρχεία—`FinalReport.pdf` και `FinalPresentation.pptx`—που μπορούν να σταλούν μέσω email, να αρχειοθετηθούν ή να προβληθούν σε οποιονδήποτε προβολέα χωρίς απώλεια πιστότητας.

## Εξαγωγή Διαγραμμάτων σε PowerPoint (Αποθήκευση Φύλλου Εργασίας ως PPTX)

Αν η αναφορά σας περιέχει διαγράμματα, πιθανότατα θέλετε να είναι επεξεργάσιμα στο PowerPoint. Η κλάση `PresentationOptions` είναι το κλειδί. Ακολουθεί ένα εστιασμένο απόσπασμα που δείχνει μόνο το τμήμα εξαγωγής διαγράμματος:

```csharp
// Assuming reportWorkbook already contains charts
var pptExportOptions = new PresentationOptions
{
    ExportCharts = true,      // Convert Excel charts to PowerPoint chart objects
    ExportShapes = false,    // Skip shapes if you don’t need them
    ExportTextBoxes = true   // Keep any text boxes editable
};

string pptFile = @"C:\Temp\ChartsOnly.pptx";
reportWorkbook.Save(pptFile, SaveFormat.Pptx, pptExportOptions);
```

**Τι συμβαίνει στο παρασκήνιο;** Το Aspose μετατρέπει κάθε διάγραμμα Excel σε εγγενές διάγραμμα PowerPoint, διατηρώντας τις σειρές, τους τίτλους αξόνων και τη μορφοποίηση. Αυτό είναι πολύ καλύτερο από την εξαγωγή του διαγράμματος ως στατική εικόνα, επειδή το κοινό σας μπορεί να τροποποιήσει τα δεδομένα αργότερα.

## Αντιγραφή Φύλλου Εργασίας PivotTable Χωρίς Απώλεια Δεδομένων

Τα PivotTables είναι συχνά το πιο δύσκολο μέρος μιας εξαγωγής επειδή βασίζονται σε κρυφή μνήμη (cache). Η απλή μέθοδος `Copy` λειτουργεί επειδή το Aspose αντιγράφει τόσο την ορατή περιοχή **και** το υποκείμενο αντικείμενο cache.

```csharp
// Copy the whole sheet (including pivot table) to a new workbook
Workbook clone = new Workbook();
reportWorkbook.Worksheets[0].CopyTo(clone.Worksheets[0]);
clone.Save(@"C:\Temp\PivotCopy.xlsx", SaveFormat.Xlsx);
```

> **Note:** Αν χρειάζεστε το PivotTable μόνο σε νέο φύλλο εντός του ίδιου βιβλίου, η προηγούμενη προσέγγιση `sourceRange.Copy` είναι ελαφρύτερη και αποφεύγει τη δημιουργία ολόκληρου νέου βιβλίου.

## Ενσωμάτωση Γραμματοσειρών για Εξαγωγή PDF – Γιατί Είναι Σημαντικό

Όταν ανοίγετε ένα PDF σε υπολογιστή που δεν διαθέτει τις αρχικές γραμματοσειρές, το κείμενο μπορεί να μετατοπιστεί, οι αλλαγές γραμμής να διαφέρουν ή χαρακτήρες να εξαφανιστούν. Ορίζοντας `EmbedStandardFonts = true` λέτε στο Aspose να ενσωματώσει τις πιο κοινές γραμματοσειρές (Arial, Times New Roman κ.λπ.) απευθείας στο ρεύμα του PDF.

Αν χρησιμοποιείτε προσαρμοσμένες γραμματοσειρές, μεταβείτε σε `PdfSaveOptions.FontEmbeddingMode = FontEmbeddingMode.EmbedAll`. Εδώ ένα παράδειγμα:

```csharp
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    FontEmbeddingMode = FontEmbeddingMode.EmbedAll   // For custom fonts
};
reportWorkbook.Save(@"C:\Temp\CustomFontReport.pdf", pdfOpts);
```

Τώρα κάθε παραλήπτης βλέπει την ακριβώς ίδια διάταξη που σχεδιάσατε — χωρίς εκπλήξεις.

## Ανασκόπηση Πλήρους Παραδείγματος Εργασίας

Συνδυάζοντας όλα τα παραπάνω, το πλήρες πρόγραμμα (που εμφανίστηκε νωρίτερα) κάνει τα εξής:

1. **Δημιουργεί** ένα φύλλο εργασίας με placeholders Smart Marker.  
2. **Επεξεργάζεται** τα markers, δημιουργώντας ένα φύλλο λεπτομερειών με όνομα το τμήμα.  
3. **Αντιγράφει** μια περιοχή που περιέχει PivotTable σε νέο φύλλο εργασίας, διατηρώντας τη λειτουργικότητά του.  
4. **Εξάγει** το φύλλο εργασίας σε PowerPoint, διατηρώντας τα διαγράμματα, σχήματα και πλαίσια κειμένου επεξεργάσιμα.  
5. **Εξάγει** το ίδιο φύλλο εργασίας σε PDF ενώ ενσωματώνει τυπικές γραμματοσειρές για αξιόπιστη απόδοση.  

Τρέξτε το πρόγραμμα, ανοίξτε τα παραγόμενα αρχεία και θα δείτε:

- **PDF**: Καθαρούς πίνακες, ενσωματωμένες γραμματοσειρές και το ίδιο οπτικό στυλ με την πηγή Excel.  
- **PowerPoint**: Επεξεργάσιμα διαγράμματα που μπορείτε να κάνετε δεξί‑κλικ → *Edit Data* στο PowerPoint, και σχήματα που παραμένουν πλήρως διαχειρίσιμα.

---

## Συχνές Ερωτήσεις (FAQ)

**Q: Λειτουργεί αυτό με .NET Core;**  
Ναι — το Aspose.Cells και το Aspose.Slides είναι cross‑platform. Απλώς στοχεύστε .NET 6 ή νεότερο και ο ίδιος κώδικας εκτελείται σε Windows, Linux ή macOS.

**Q: Τι γίνεται αν χρειαστεί να εξάγω μόνο ένα υποσύνολο φύλλων;**  
Χρησιμοποιήστε `Workbook.Save` με `SaveOptions` που σας επιτρέπουν να καθορίσετε `SheetNames`. Παράδειγμα: `new PresentationOptions { SheetNames = new[] { "Copy" } }`.

**Q: Μπορώ να κρυπτογραφήσω το PDF;**  
Απολύτως. Ορίστε `PdfSaveOptions.EncryptionDetails` με κωδικό πρόσβασης πριν καλέσετε `Save`.

**Q: Το PivotTable μου χρησιμοποιεί εξωτερική πηγή δεδομένων — θα σπάσει ο σύνδεσμος κατά την αντιγραφή;**  
Η λειτουργία αντιγραφής περιλαμβάνει τη μνήμη cache, όχι τη εξωτερική σύνδεση. Το Pivot θα λειτουργεί offline, αλλά δεν θα ανανεώνεται από την αρχική πηγή. Αν χρειάζεστε ζωντανή ανανέωση, εξάγετε τα δεδομένα πηγής μαζί με το βιβλίο εργασίας.

## Επόμενα Βήματα & Σχετικά Θέματα

- **Δυναμικές Πηγές Δεδομένων** – Μάθετε πώς να τροφοδοτείτε JSON ή DataTable στα Smart Markers για αναφορές σε πραγματικό χρόνο.  
- **Advanced PDF Styling** – Explore `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}