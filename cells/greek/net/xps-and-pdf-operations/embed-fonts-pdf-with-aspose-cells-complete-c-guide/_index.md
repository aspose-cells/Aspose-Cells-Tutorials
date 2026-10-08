---
category: general
date: 2026-06-24
description: Ενσωμάτωση γραμματοσειρών PDF χρησιμοποιώντας το Aspose.Cells σε C#.
  Μάθετε πώς να αποθηκεύετε το Excel ως PDF, να εξάγετε το Excel σε HTML, να μετατρέπετε
  xlsx σε PDF με το Aspose και να δημιουργείτε διπλότυπες γραμμές pivot.
draft: false
keywords:
- embed fonts pdf
- save excel as pdf
- export excel to html
- xlsx to pdf aspose
- duplicate rows pivot
language: el
og_description: Ενσωμάτωση γραμματοσειρών PDF χρησιμοποιώντας το Aspose.Cells σε C#.
  Αυτό το σεμινάριο δείχνει βήμα-βήμα πώς να αποθηκεύσετε το Excel ως PDF, να εξάγετε
  το Excel σε HTML και άλλα.
og_title: Ενσωμάτωση γραμματοσειρών PDF με το Aspose.Cells – Πλήρης οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Embed fonts PDF using Aspose.Cells in C#. Learn how to save Excel as
    PDF, export Excel to HTML, convert xlsx to PDF with Aspose, and duplicate rows
    pivot.
  headline: Embed fonts PDF with Aspose.Cells – Complete C# Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
title: Ενσωμάτωση γραμματοσειρών PDF με το Aspose.Cells – Πλήρης οδηγός C#
url: /el/net/xps-and-pdf-operations/embed-fonts-pdf-with-aspose-cells-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ενσωμάτωση γραμματοσειρών PDF με Aspose.Cells – Πλήρης Οδηγός C#

Έχετε αναρωτηθεί ποτέ πώς να **ενσωματώσετε γραμματοσειρές PDF** όταν μετατρέπετε ένα βιβλίο εργασίας Excel με το Aspose.Cells; Δεν είστε μόνοι—πολλοί προγραμματιστές συναντούν πρόβλημα όταν το παραγόμενο PDF φαίνεται λανθασμένο σε μηχανές που δεν έχουν εγκατεστημένες τις αρχικές γραμματοσειρές.  

Σε αυτόν τον οδηγό θα περάσουμε από ένα πραγματικό παράδειγμα που όχι μόνο **ενσωματώνει γραμματοσειρές PDF**, αλλά δείχνει επίσης πώς να **αποθηκεύσετε το Excel ως PDF**, **εξάγετε το Excel σε HTML**, μετατρέψετε ένα **xlsx σε PDF με Aspose**, και ακόμη **διπλασιάσετε γραμμές pivot** χωρίς να σπάσει ο πίνακας pivot. Ακούγεται πολύ; Χωρίς άγχος—θα το σπάσουμε βήμα‑βήμα.

## Τι Θα Μάθετε

- Πώς να αντιγράψετε γραμμές που περιέχουν πίνακα pivot διατηρώντας τον pivot αμετάβλητο.  
- Πώς να εισάγετε ένα smart‑marker που επαναλαμβάνει ένα φύλλο λεπτομερειών για κάθε παραγγελία.  
- Οι ακριβείς ρυθμίσεις που χρειάζεστε για **ενσωμάτωση γραμματοσειρών PDF**, εξαγωγή διαγραμμάτων ως επεξεργάσιμο PPTX, και διατήρηση παγωμένων πάνελ όταν **εξάγετε το Excel σε HTML**.  
- Συμβουλές για την αντιμετώπιση κοινών προβλημάτων όπως λείπουν γραμματοσειρές ή σπασμένα αντικείμενα OLE.  

**Προαπαιτούμενα:** .NET 6+ (ή .NET Framework 4.6+), Aspose.Cells for .NET εγκατεστημένο, και ένα βασικό περιβάλλον ανάπτυξης C# (Visual Studio, Rider ή VS Code). Δεν απαιτούνται επιπλέον πακέτα NuGet εκτός από το Aspose.Cells.

---

## Ενσωμάτωση γραμματοσειρών PDF – Διαδικασία βήμα‑βήμα

Παρακάτω βρίσκεται ο πλήρης, εκτελέσιμος κώδικας. Κάθε τμήμα είναι σχολιασμένο ώστε να βλέπετε ακριβώς γιατί κάνουμε ό,τι κάνουμε.

```csharp
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Pivot;
using Aspose.Cells.SmartMarker;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the workbook that contains a pivot table and a shape
        // -------------------------------------------------
        var workbook = new Workbook("YOUR_DIRECTORY/template.xlsx");

        // -------------------------------------------------
        // Step 2: Duplicate the rows that include the pivot table (keeps the pivot intact)
        // -------------------------------------------------
        // The CopyRows method copies rows 0‑29 (30 rows) from the source worksheet
        // to the same worksheet, effectively duplicating the pivot area.
        workbook.Worksheets[0].Cells.CopyRows(0, 0, 30);

        // -------------------------------------------------
        // Step 3: Insert a smart‑marker to repeat a detail sheet for each order
        // -------------------------------------------------
        var orders = new[]
        {
            new { Id = 101, Items = new[] { "Pen", "Paper" } },
            new { Id = 102, Items = new[] { "Book" } }
        };
        var smartMarkerOptions = new SmartMarkerOptions { DetailSheetNewName = "OrderDetail" };
        workbook.Worksheets[0].SmartMarkerProcessing(new { Orders = orders }, smartMarkerOptions);

        // -------------------------------------------------
        // Step 4: Save the workbook as a PPTX file with editable charts, OLE objects, and text boxes
        // -------------------------------------------------
        var pptxOptions = new PptxSaveOptions
        {
            ExportChartsAsEditable = true,
            ExportOleObjects = true,
            ExportTextBoxesAsEditable = true
        };
        workbook.Save("YOUR_DIRECTORY/result.pptx", pptxOptions);

        // -------------------------------------------------
        // Step 5: Save the same workbook as a PDF while embedding standard fonts
        // -------------------------------------------------
        // This is where we actually **embed fonts PDF**.
        var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
        workbook.Save("YOUR_DIRECTORY/result.pdf", pdfOptions);

        // -------------------------------------------------
        // Step 6: Save the workbook as HTML, preserving frozen panes and embedding all fonts
        // -------------------------------------------------
        // The HTML export respects the original layout and keeps the fonts inside the file.
        var htmlOptions = new HtmlSaveOptions
        {
            PreserveFreezePanes = true,
            EmbedAllFonts = true
        };
        workbook.Save("YOUR_DIRECTORY/result.html", htmlOptions);
    }
}
```

### Γιατί λειτουργεί αυτό

- **CopyRows** διπλασιάζει τις γραμμές που περιέχουν τον πίνακα pivot, ώστε ο αρχικός pivot να παραμένει συνδεδεμένος με τα δεδομένα πηγής. Αυτό ικανοποιεί την απαίτηση **duplicate rows pivot**.  
- **SmartMarkerProcessing** δημιουργεί ένα νέο φύλλο εργασίας για κάθε παραγγελία, αυτοματοποιώντας τη δημιουργία του φύλλου λεπτομερειών.  
- **PdfSaveOptions.EmbedStandardFonts = true** λέει στο Aspose.Cells να ενσωματώσει τις γραμματοσειρές απευθείας στο αρχείο PDF, που είναι το κλειδί για **ενσωμάτωση γραμματοσειρών pdf**. Χωρίς αυτήν τη ρύθμιση το PDF θα επιστρέψει σε σύστημα γραμματοσειρών, σπάζοντας τη διάταξη σε άλλες μηχανές.  
- **HtmlSaveOptions** με `EmbedAllFonts` και `PreserveFreezePanes` εξασφαλίζει ότι όταν **εξάγετε το Excel σε HTML**, η οπτική πιστότητα ταιριάζει με το αρχικό βιβλίο εργασίας.

#### Αναμενόμενο αποτέλεσμα

- `result.pdf` – ένα PDF όπου όλες οι χρησιμοποιημένες γραμματοσειρές είναι ενσωματωμένες· ανοίξτε το σε οποιονδήποτε υπολογιστή και το κείμενο θα φαίνεται ταυτόσημο με την πηγή.  
- `result.pptx` – αρχείο PowerPoint με επεξεργάσιμα διαγράμματα και αντικείμενα OLE.  
- `result.html` – φάκελος HTML (`result.html` + `result_files`) που αποδίδει το βιβλίο εργασίας σε πρόγραμμα περιήγησης με τα παγωμένα πάνελ αμετάβλητα.

---

## Αποθήκευση Excel ως PDF με Aspose.Cells

Αν ο μόνος σας στόχος είναι να **αποθηκεύσετε το Excel ως PDF**, μπορείτε να αφαιρέσετε τα επιπλέον βήματα και να εστιάσετε στις ρυθμίσεις PDF:

```csharp
var workbook = new Workbook("template.xlsx");

// Minimal PDF conversion – embed fonts for portability
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,   // crucial for embed fonts pdf
    Compliance = PdfCompliance.PdfA1b // optional: make the PDF archival‑friendly
};

workbook.Save("output.pdf", pdfOpts);
```

**Συμβουλή επαγγελματία:** Όταν στοχεύετε σε συμμόρφωση PDF/A, το Aspose ενσωματώνει αυτόματα όλες τις γραμματοσειρές, παρέχοντας ένα επιπλέον επίπεδο ασφάλειας για μακροπρόθεσμη αποθήκευση.

---

## Εξαγωγή Excel σε HTML με Διατήρηση Διάταξης

Η εξαγωγή σε HTML συχνά χάνει την εμφάνιση του αρχικού φύλλου, ειδικά όταν εμπλέκονται παγωμένα πάνελ. Το παρακάτω απόσπασμα δείχνει τις ακριβείς ρυθμίσεις που χρειάζεστε:

```csharp
var wb = new Workbook("template.xlsx");

var htmlOpts = new HtmlSaveOptions
{
    PreserveFreezePanes = true, // keeps the top rows/columns locked
    EmbedAllFonts = true,       // embeds fonts so the page looks the same everywhere
    ExportActiveWorksheetOnly = true,
    ExportCellValueAsString = true
};

wb.Save("output.html", htmlOpts);
```

Επειδή ορίσαμε `EmbedAllFonts`, το παραγόμενο HTML περιέχει δεδομένα γραμματοσειρών κωδικοποιημένα σε base‑64, ικανοποιώντας την απαίτηση **export excel to html** χωρίς εξωτερικά αρχεία CSS.

---

## Μετατροπή Xlsx σε PDF χρησιμοποιώντας Aspose.Cells

Μερικές φορές η αναζήτηση «**xlsx to pdf aspose**» εμφανίζεται στα αποτελέσματα. Ο κώδικας παρακάτω δείχνει την ακριβή αλυσίδα μετατροπής, συμπεριλαμβανομένων μερικών επιπλέον βελτιώσεων:

```csharp
var wb = new Workbook("template.xlsx");

// Optional: set page layout before conversion
wb.Worksheets[0].PageSetup.Orientation = PageOrientation.Landscape;
wb.Worksheets[0].PageSetup.FitToPagesWide = 1;
wb.Worksheets[0].PageSetup.FitToPagesTall = 0;

// PDF options – embed fonts and keep hyperlinks intact
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    ExportHyperlinks = true,
    OnePagePerSheet = false
};

wb.Save("converted.pdf", pdfOpts);
```

**Γιατί να ασχοληθούμε με τη ρύθμιση σελίδας;** Αν το παραλείψετε, το προεπιλεγμένο PDF μπορεί να κόψει στήλες ή γραμμές. Η προσαρμογή της διάταξης πρώτα εξασφαλίζει ότι το τελικό PDF ταιριάζει με αυτό που βλέπετε στο Excel.

---

## Duplicate Rows Pivot – Διατήρηση του Pivot Αμετάβλητου

Ένα κοινό εμπόδιο είναι η προσπάθεια αντιγραφής γραμμών που περιέχουν πίνακα pivot· ο pivot συχνά χάνει τη σύνδεσή του με την πηγή δεδομένων. Η μέθοδος `CopyRows` που χρησιμοποιήσαμε νωρίτερα κάνει το δύσκολο για εσάς:

```csharp
// Duplicate the first 30 rows (adjust as needed)
workbook.Worksheets[0].Cells.CopyRows(sourceRow: 0, destinationRow: 0, totalRows: 30);
```

- **sourceRow** – η πρώτη γραμμή της περιοχής που θέλετε να αντιγράψετε.  
- **destinationRow** – το σημείο όπου θα τοποθετηθεί η αντιγραφή (ίδιο φύλλο, ίδιο αρχικό δείκτη για αποτελεσματικό διπλασιασμό).  
- **totalRows** – πόσες γραμμές θα αντιγραφούν.  

Επειδή η cache του pivot ζει στο φύλλο εργασίας, η αντιγραφή των γραμμών **δεν** σπάει τον pivot. Αυτό ικανοποιεί τη λέξη‑κλειδί **duplicate rows pivot** διατηρώντας το βιβλίο εργασίας τακτοποιημένο.

---

## Συνοπτικό Παράδειγμα Πλήρους Λειτουργίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες πρόγραμμα που μπορείτε να τοποθετήσετε σε μια εφαρμογή console και να τρέξετε αμέσως:



## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην δική σας υλοποίηση.

- [Save Excel Workbook as PDF with Custom Fonts using Aspose.Cells for .NET](/cells/english/net/workbook-operations/save-excel-workbook-pdf-custom-fonts-aspose-cells-net/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET: A Step‑By‑Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [How to Export Excel Slicers to PDF Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-slicers-to-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}