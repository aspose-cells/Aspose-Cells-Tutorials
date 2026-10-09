---
category: general
date: 2026-03-18
description: Μάθετε πώς να ορίζετε τις επιλογές PDF σε C# και να αποθηκεύετε το βιβλίο
  εργασίας ως PDF. Αυτός ο οδηγός καλύπτει επίσης την εξαγωγή του Excel σε PDF, τη
  μετατροπή του υπολογιστικού φύλλου σε PDF και την αποθήκευση του Excel ως PDF αποδοτικά.
draft: false
keywords:
- how to set pdf
- save workbook as pdf
- export excel to pdf
- convert spreadsheet pdf
- save excel pdf
language: el
og_description: Πώς να ορίσετε επιλογές PDF σε C# και να αποθηκεύσετε το βιβλίο εργασίας
  ως PDF. Ακολουθήστε αυτόν τον οδηγό βήμα‑προς‑βήμα για να εξάγετε το Excel σε PDF,
  να μετατρέψετε το φύλλο εργασίας σε PDF και να αποθηκεύσετε το Excel ως PDF.
og_title: Πώς να ορίσετε επιλογές PDF σε C# – Εξαγωγή Excel σε PDF
tags:
- C#
- Aspose.Cells
- PDF export
- Excel automation
title: Πώς να ορίσετε επιλογές PDF σε C# – Εξαγωγή Excel σε PDF με πλήρη έλεγχο
url: /el/net/conversion-to-pdf/how-to-set-pdf-options-in-c-export-excel-to-pdf-with-full-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ορίσετε επιλογές PDF σε C# – Εξαγωγή Excel σε PDF

Έχετε αναρωτηθεί **πώς να ορίσετε παραμέτρους PDF** όταν χρειάζεται να εξάγετε ένα βιβλίο εργασίας Excel από C#; Δεν είστε οι μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν η προεπιλεγμένη έξοδος PDF φαίνεται εντάξει αλλά αποτυγχάνει σε ελέγχους συμμόρφωσης ή χάνει λεπτομέρειές μορφοποίησης.  

Τα καλά νέα; Με λίγες μόνο γραμμές κώδικα μπορείτε να ελέγξετε τα πάντα—από τη συμμόρφωση PDF/A‑2b μέχρι τα περιθώρια σελίδας—ώστε το εξαγόμενο PDF του φύλλου εργασίας να μοιάζει ακριβώς όπως το περιμένετε. Αυτό το tutorial δείχνει **πώς να ορίσετε επιλογές PDF**, στη συνέχεια **να αποθηκεύσετε το βιβλίο εργασίας ως PDF** χρησιμοποιώντας τη δημοφιλή βιβλιοθήκη Aspose.Cells.

Θα αγγίξουμε επίσης σχετικές εργασίες όπως **εξαγωγή Excel σε PDF**, **μετατροπή PDF φύλλου εργασίας**, και **αποθήκευση Excel PDF** με συμβουλές βέλτιστης πρακτικής. Στο τέλος, θα έχετε ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+)
- Visual Studio 2022 ή οποιοδήποτε IDE συμβατό με C#
- Aspose.Cells for .NET (το δωρεάν trial πακέτο NuGet είναι επαρκές)
- Ένα δείγμα αρχείου Excel (`sample.xlsx`) στον φάκελο του έργου σας

Δεν απαιτείται επιπλέον διαμόρφωση—απλώς η αναφορά NuGet και μια βασική εφαρμογή console.

## Τι καλύπτει αυτός ο οδηγός

- **Πώς να ορίσετε επιλογές PDF** για συμμόρφωση και ποιότητα
- Χρήση του `PdfSaveOptions` για έλεγχο της διαδικασίας εξαγωγής
- Αποθήκευση του βιβλίου εργασίας ως PDF με μία κλήση μεθόδου
- Επαλήθευση του αποτελέσματος και αντιμετώπιση κοινών προβλημάτων
- Επέκταση του παραδείγματος για πολλαπλά φύλλα, προσαρμοσμένα περιθώρια και προστασία με κωδικό

Έτοιμοι; Ας ξεκινήσουμε.

## Βήμα 1: Εγκατάσταση Aspose.Cells και Προσθήκη Namespaces

Πρώτα, προσθέστε το πακέτο Aspose.Cells. Ανοίξτε το **Package Manager Console** και εκτελέστε:

```powershell
Install-Package Aspose.Cells
```

Στη συνέχεια, συμπεριλάβετε τα απαραίτητα namespaces στο αρχείο C#:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
```

> **Pro tip:** Αν χρησιμοποιείτε .NET Core, μπορείτε επίσης να προσθέσετε το πακέτο μέσω `dotnet add package Aspose.Cells`.

## Βήμα 2: Φόρτωση του Workbook που Θέλετε να Εξάγετε

Υποθέτοντας ότι έχετε το `sample.xlsx` στον ίδιο φάκελο με το εκτελέσιμο, φορτώστε το ως εξής:

```csharp
// Step 2: Load the source Excel workbook
Workbook wb = new Workbook("sample.xlsx");
```

> **Γιατί είναι σημαντικό:** Η φόρτωση του workbook πρώτα σας δίνει πρόσβαση στα φύλλα, τα στυλ και τυχόν ενσωματωμένες εικόνες—όλα όσα θα εμφανιστούν αργότερα στο PDF.

## Βήμα 3: Διαμόρφωση PDF Save Options – Πώς να Ορίσετε Ρυθμίσεις PDF

Τώρα έρχεται η καρδιά του tutorial: **πώς να ορίσετε επιλογές PDF**. Θα ρυθμίσουμε το αντικείμενο `PdfSaveOptions` ώστε να πληροί τα πρότυπα αρχειοθέτησης PDF/A‑2b, που είναι κοινή απαίτηση για νομικές ή μακροπρόθεσμες αποθηκεύσεις.

```csharp
// Step 3: Configure PDF save options for PDF/A‑2b compliance
PdfSaveOptions pdfOpts = new PdfSaveOptions
{
    // Ensures the output meets PDF/A‑2b archival standards
    Compliance = PdfCompliance.PdfA2b,

    // Optional: set page orientation, margins, or image quality
    // Uncomment and adjust as needed
    // PageOrientation = PageOrientationType.Landscape,
    // ImageQuality = 90,
    // AllColumnsInOnePagePerSheet = true
};
```

### Γιατί να Χρησιμοποιήσετε PDF/A‑2b;

Το PDF/A‑2b εγγυάται ότι το έγγραφο θα αποδοθεί με τον ίδιο τρόπο σε οποιονδήποτε μελλοντικό προβολέα—χωρίς ελλιπή γραμματοσειρές ή χρώματα. Αν θέλετε μόνο μια γρήγορη εξαγωγή, μπορείτε να παραλείψετε τη γραμμή `Compliance`, αλλά για PDFs παραγωγικής ποιότητας, αξίζει η επιπλέον γραμμή.

> **Κοινή ερώτηση:** *Τι γίνεται αν χρειάζομαι PDF/A‑1b αντί για PDF/A‑2b;*  
> Απλώς αντικαταστήστε το `PdfCompliance.PdfA2b` με `PdfCompliance.PdfA1b`. Το υπόλοιπο του κώδικα παραμένει το ίδιο.

## Βήμα 4: Αποθήκευση του Workbook ως PDF – Η Τελική Εξαγωγή

Με τις επιλογές ρυθμισμένες, μπορείτε τώρα **να αποθηκεύσετε το workbook ως PDF**. Αυτή η μοναδική κλήση μεθόδου διαχειρίζεται ολόκληρη τη διαδικασία μετατροπής.

```csharp
// Step 4: Save the workbook as a PDF using the configured options
string outputPath = "output/compatible.pdf";
wb.Save(outputPath, pdfOpts);
Console.WriteLine($"PDF saved successfully to {outputPath}");
```

> **Συμβουλή:** Βεβαιωθείτε ότι ο φάκελος `output` υπάρχει εκ των προτέρων, ή χρησιμοποιήστε `Directory.CreateDirectory("output");` για να αποφύγετε `DirectoryNotFoundException`.

### Αναμενόμενο Αποτέλεσμα

Μετά την εκτέλεση του προγράμματος, ανοίξτε το `compatible.pdf`. Θα πρέπει να δείτε μια πιστή αναπαράσταση του `sample.xlsx`, συμπεριλαμβανομένης της μορφοποίησης κελιών, των διαγραμμάτων και των εικόνων. Αν ανοίξετε το PDF στο Adobe Acrobat και ελέγξετε **File → Properties → Description**, θα δείτε ότι η σημαία **PDF/A‑2b** είναι ενεργοποιημένη.

## Βήμα 5: Επαλήθευση του PDF – Σωστή Μετατροπή Spreadsheet PDF

Η επαλήθευση συχνά παραβλέπεται, αλλά είναι κρίσιμη όταν χρειάζεται να **μετατρέψετε spreadsheet PDF** για ελέγχους συμμόρφωσης.

```csharp
// Step 5: Quick verification using Aspose.PDF (optional)
using Aspose.Pdf;

Document pdfDoc = new Document(outputPath);
bool isPdfA2b = pdfDoc.IsPdfA2bCompliant;
Console.WriteLine($"Is PDF/A‑2b compliant? {isPdfA2b}");
```

Αν το `isPdfA2b` εμφανίζει `True`, έχετε επιτυχώς **μετατρέψει spreadsheet PDF** με τις σωστές ρυθμίσεις.

## Προχωρημένες Παραλλαγές (Προαιρετικό)

### Αποθήκευση Excel PDF με Προστασία Κωδικού

Αν χρειάζεται να **αποθηκεύσετε Excel PDF** με ασφάλεια, προσθέστε κωδικό:

```csharp
pdfOpts.Password = "StrongP@ssw0rd!";
wb.Save("output/protected.pdf", pdfOpts);
```

### Εξαγωγή Πολλαπλών Φύλλων ως Ξεχωριστά PDFs

Μερικές φορές θέλετε κάθε φύλλο ως ξεχωριστό αρχείο. Κάντε βρόχο στα φύλλα:

```csharp
for (int i = 0; i < wb.Worksheets.Count; i++)
{
    Worksheet sheet = wb.Worksheets[i];
    sheet.PageSetup.PrintArea = sheet.Cells.MaxDisplayRange.Reference; // Fit content
    wb.Save($"output/{sheet.Name}.pdf", pdfOpts);
}
```

### Προσαρμογή Περιθωρίων και Διάταξης Σελίδας

Βελτιώστε τη διάταξη ρυθμίζοντας το `PageSetup` πριν την αποθήκευση:

```csharp
foreach (Worksheet ws in wb.Worksheets)
{
    ws.PageSetup.LeftMargin = 0.5;   // inches
    ws.PageSetup.RightMargin = 0.5;
    ws.PageSetup.TopMargin = 0.75;
    ws.PageSetup.BottomMargin = 0.75;
}
```

## Πλήρες Παράδειγμα Εφαρμογής

Παρακάτω βρίσκεται η πλήρης, έτοιμη προς εκτέλεση εφαρμογή console που ενσωματώνει όλα τα βήματα που συζητήθηκαν. Αντιγράψτε‑και‑επικολλήστε το στο `Program.cs` και πατήστε **F5**.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using Aspose.Pdf; // Optional, for verification

class Program
{
    static void Main()
    {
        // Ensure output directory exists
        Directory.CreateDirectory("output");

        // 1️⃣ Load the Excel workbook
        Workbook wb = new Workbook("sample.xlsx");

        // 2️⃣ (Optional) Adjust page setup for each sheet
        foreach (Worksheet ws in wb.Worksheets)
        {
            ws.PageSetup.LeftMargin = 0.5;
            ws.PageSetup.RightMargin = 0.5;
            ws.PageSetup.TopMargin = 0.75;
            ws.PageSetup.BottomMargin = 0.75;
        }

        // 3️⃣ Configure PDF save options – how to set PDF compliance
        PdfSaveOptions pdfOpts = new PdfSaveOptions
        {
            Compliance = PdfCompliance.PdfA2b, // PDF/A‑2b archival standard
            // Uncomment to set additional options
            // ImageQuality = 95,
            // AllColumnsInOnePagePerSheet = true
        };

        // 4️⃣ Save the workbook as PDF – save workbook as PDF
        string pdfPath = "output/compatible.pdf";
        wb.Save(pdfPath, pdfOpts);
        Console.WriteLine($"✅ PDF saved to {pdfPath}");

        // 5️⃣ Verify PDF/A‑2b compliance – convert spreadsheet PDF check
        Document pdfDoc = new Document(pdfPath);
        Console.WriteLine($"PDF/A‑2b compliant? {pdfDoc.IsPdfA2bCompliant}");

        // 6️⃣ (Optional) Save a password‑protected version – save Excel PDF securely
        pdfOpts.Password = "StrongP@ssw0rd!";
        wb.Save("output/protected.pdf", pdfOpts);
        Console.WriteLine("🔐 Protected PDF created.");
    }
}
```

### Αναμενόμενη Εξαγωγή στην Κονσόλα

```
✅ PDF saved to output/compatible.pdf
PDF/A‑2b compliant? True
🔐 Protected PDF created.
```

Ανοίξτε τα παραγόμενα αρχεία για να επιβεβαιώσετε τη διάταξη, τη συμμόρφωση και την προστασία με κωδικό.

![πώς να ορίσετε επιλογές pdf στο Aspose.Cells](/images/how-to-set-pdf-options.png)

*Το στιγμιότυπο (placeholder) δείχνει τη σημαία PDF/A‑2b στο Adobe Acrobat.*

## Συχνές Ερωτήσεις

**Ε: Λειτουργεί αυτό με αρχεία .xlsx που περιέχουν μακροεντολές;**  
Α: Ναι, το Aspose.Cells αγνοεί τα VBA macros κατά τη μετατροπή, έτσι το PDF θα περιέχει μόνο τα εμφανιζόμενα δεδομένα.

**Ε: Τι κάνω αν χρειάζομαι PDF/A‑1b αντί για PDF/A‑2b;**  
Α: Αλλάξτε το `Compliance = PdfCompliance.PdfA2b` σε `PdfCompliance.PdfA1b`. Το υπόλοιπο του κώδικα παραμένει αμετάβλητο.

**Ε: Μπορώ να εξάγω σε PDF χωρίς να εγκαταστήσω το Acrobat στον server;**  
Α: Απόλυτα. Το Aspose.Cells εκτελεί τη μετατροπή εξ ολοκλήρου σε managed code—χωρίς εξωτερικές εξαρτήσεις.

**Ε: Πώς να διαχειριστώ πολύ μεγάλα workbooks που προκαλούν προβλήματα μνήμης;**  
Α: Χρησιμοποιήστε `PdfSaveOptions` με `EnableMemoryOptimization = true` και σκεφτείτε να εξάγετε ένα φύλλο τη φορά.

## Συμπέρασμα

Διασχίσαμε **πώς να ορίσετε επιλογές PDF** σε C#, παρουσιάσαμε τον ακριβή κώδικα για **αποθήκευση workbook ως PDF**, και καλύψαμε σχετικές εργασίες όπως **εξαγωγή Excel σε PDF**, **μετατροπή spreadsheet PDF**, και **αποθήκευση Excel PDF** με ασφάλεια. Το βασικό συμπέρασμα είναι ότι λίγες γραμμές ρυθμίσεων σας δίνουν πλήρη έλεγχο πάνω στη συμμόρφωση, την ασφάλεια και τη διάταξη—χωρίς ανάγκη εργαλείων μετα-επεξεργασίας.

Επόμενα βήματα που μπορείτε να εξερευνήσετε:

- Προσθήκη υδατογραφιών ή κεφαλίδων/υποσέλιδων (δείτε την ιδιότητα `PdfSaveOptions.Watermark` του Aspose.Cells)
- Μετατροπή του PDF σε μορφές εικόνας για μικρογραφίες προεπισκόπησης
- Αυτοματοποίηση μαζικών μετατροπών για ολόκληρους φακέλους αρχείων Excel

Πειραματιστείτε με τις επιλογές και ενημερώστε μας στα σχόλια ποια παραλλαγή σας εξοικονόμησε τον περισσότερο χρόνο. Καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}