---
category: general
date: 2026-11-19
description: Μάθετε πώς να αποθηκεύετε ένα βιβλίο εργασίας ως CSV χρησιμοποιώντας
  C#. Αυτός ο οδηγός καλύπτει τη μετατροπή του Excel σε CSV, την εξαγωγή του υπολογιστικού
  φύλλου σε CSV και τις επιλογές ακρίβειας.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save workbook as csv
- convert excel to csv
- export excel to csv
- export spreadsheet to csv
- how to convert xlsx to csv
language: el
lastmod: 2026-11-19
og_description: Αποθήκευση βιβλίου εργασίας ως CSV σε C# με πλήρες παράδειγμα κώδικα.
  Μετατροπή Excel σε CSV, εξαγωγή φύλλου εργασίας σε CSV και έλεγχος ακρίβειας αριθμητικών
  τιμών.
og_image_alt: Screenshot of C# code that saves a workbook as CSV
og_title: Αποθήκευση βιβλίου εργασίας ως CSV σε C# – πλήρης οδηγός προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to save workbook as CSV using C#. This guide covers convert
    Excel to CSV, export spreadsheet to CSV and precision options.
  headline: How to save workbook as CSV in C# – step‑by‑step guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- CSV export
title: Πώς να αποθηκεύσετε το βιβλίο εργασίας ως CSV σε C# – οδηγός βήμα‑προς‑βήμα
url: /el/net/csv-file-handling/how-to-save-workbook-as-csv-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αποθηκεύσετε ένα βιβλίο εργασίας ως CSV σε C# – βήμα‑βήμα οδηγός

Αν χρειάζεστε να **αποθηκεύσετε ένα βιβλίο εργασίας ως CSV** γρήγορα, αυτό το tutorial σας δείχνει ακριβώς πώς. Θα δείτε ένα πλήρες, εκτελέσιμο παράδειγμα που μετατρέπει ένα αρχείο Excel σε αρχείο CSV ενώ περιορίζει την αριθμητική ακρίβεια.  

Ο οδηγός καλύπτει επίσης σχετικές εργασίες όπως **convert Excel to CSV**, **export Excel to CSV**, και **export spreadsheet to CSV**, ώστε να μπορείτε να επιλέξετε την προσέγγιση που ταιριάζει στο έργο σας.

## Τι θα χρειαστείτε

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί με .NET Core και .NET Framework)
* Μια αναφορά στο πακέτο NuGet **Aspose.Cells for .NET** (το API που χρησιμοποιείται στο παράδειγμα)
* Ένα αρχείο εισόδου με όνομα `input.xlsx` τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε από τον κώδικα
* Ένα περιβάλλον ανάπτυξης όπως το Visual Studio 2022 ή το VS Code

> **Συμβουλή:** Αν προτιμάτε μια δωρεάν εναλλακτική, η ίδια λογική ισχύει για τη βιβλιοθήκη `ClosedXML`; απλώς αντικαταστήστε τους τύπους `Workbook` και `CsvSaveOptions` με τα αντίστοιχα ClosedXML.

![Illustration of a C# program saving a workbook as CSV](image-placeholder.png "save workbook as csv diagram")

## Βήμα 1: Εγκατάσταση Aspose.Cells

Ανοίξτε ένα τερματικό στον φάκελο του έργου σας και εκτελέστε:

```bash
dotnet add package Aspose.Cells
```

Το πακέτο προσθέτει το namespace `Aspose.Cells`, το οποίο παρέχει την κλάση `Workbook` και το αντικείμενο `CsvSaveOptions` που χρησιμοποιείται αργότερα.

## Βήμα 2: Εισαγωγή των απαιτούμενων namespaces

Δημιουργήστε ένα νέο έργο κονσόλας C# (`dotnet new console`) και προσθέστε τις παρακάτω δηλώσεις `using` στην κορυφή του `Program.cs`:

```csharp
using System;
using Aspose.Cells;
```

Αυτές οι δηλώσεις κάνουν τους τύπους `Workbook` και `CsvSaveOptions` διαθέσιμους χωρίς να χρειάζεται να τους προσδιορίζετε πλήρως κάθε φορά.

## Βήμα 3: Φόρτωση του βιβλίου εργασίας Excel

Η πρώτη ενέργεια είναι το άνοιγμα του πηγαίου αρχείου `.xlsx`. Ο κατασκευαστής `Workbook` δέχεται μια διαδρομή αρχείου, ώστε να μπορείτε να τον δείξετε σε οποιαδήποτε θέση στο δίσκο.

```csharp
// Step 1: Load the Excel workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Γιατί είναι σημαντικό*: Η φόρτωση του βιβλίου εργασίας δημιουργεί μια αναπαράσταση στη μνήμη όλων των φύλλων εργασίας, των τύπων και των μορφοποιήσεων κελιών. Εάν το αρχείο δεν βρεθεί, το `Workbook` ρίχνει ένα `FileNotFoundException`, το οποίο μπορείτε να πιάσετε για ένα πιο φιλικό μήνυμα σφάλματος.

## Βήμα 4: Διαμόρφωση επιλογών εξαγωγής CSV

Όταν **export Excel to CSV**, συχνά χρειάζεται να ελέγξετε πώς γράφονται οι αριθμοί. Η κλάση `CsvSaveOptions` σας επιτρέπει να καθορίσετε τον αριθμό των σημαντικών ψηφίων, το διαχωριστικό και αν θα συμπεριληφθεί UTF‑8 BOM.

```csharp
// Step 2: Configure CSV save options to limit precision
CsvSaveOptions csvOptions = new CsvSaveOptions
{
    // Keep only 5 significant digits to avoid overly long floating‑point strings
    SignificantDigits = 5,

    // Optional: change the delimiter from a comma to a semicolon for European locales
    // Separator = ';',

    // Optional: include a UTF‑8 BOM so Excel opens the file with the correct encoding
    // Encoding = Encoding.UTF8
};
```

*Γιατί είναι σημαντικό*: Από προεπιλογή το Aspose.Cells γράφει κάθε ψηφίο που αποθηκεύεται στο κελί, κάτι που μπορεί να παράγει ακατάλληλες αλφαριθμητικές ακολουθίες όπως `0.123456789`. Ορίζοντας `SignificantDigits` σε `5` περικοπεί η έξοδος σε πιο αναγνώσιμη μορφή (`0.12346`). Μπορείτε επίσης να προσαρμόσετε το `Separator` εάν το σύστημα προορισμού σας απαιτεί διαφορετικό διαχωριστικό.

## Βήμα 5: Αποθήκευση του βιβλίου εργασίας ως αρχείο CSV

Τέλος, καλέστε τη μέθοδο `Save`, περνώντας τη διαδρομή εξόδου και τις ρυθμισμένες επιλογές.

```csharp
// Step 3: Save the workbook as a CSV file using the configured options
workbook.Save("YOUR_DIRECTORY/output.csv", csvOptions);
```

Όταν η κλήση ολοκληρωθεί, το `output.csv` περιέχει το πρώτο φύλλο του `input.xlsx` ως απλό κείμενο. Εάν το βιβλίο εργασίας περιέχει πολλαπλά φύλλα και θέλετε μόνο ένα συγκεκριμένο, ορίστε `csvOptions.ExportActiveWorksheetOnly = true` πριν καλέσετε το `Save`.

## Πλήρες εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι ένα αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε, επικολλήσετε και να εκτελέσετε:

```csharp
using System;
using Aspose.Cells;

namespace ExcelToCsvDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Define file locations (adjust to your environment)
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            string outputPath = @"YOUR_DIRECTORY\output.csv";

            // Load the Excel workbook
            Workbook workbook = new Workbook(inputPath);

            // Configure CSV export options
            CsvSaveOptions csvOptions = new CsvSaveOptions
            {
                SignificantDigits = 5,               // limit numeric precision
                ExportActiveWorksheetOnly = true,    // export only the first sheet
                Separator = ',',                     // standard comma delimiter
                Encoding = System.Text.Encoding.UTF8 // ensure UTF‑8 output
            };

            // Save as CSV
            workbook.Save(outputPath, csvOptions);

            Console.WriteLine($"Workbook saved as CSV at: {outputPath}");
        }
    }
}
```

### Αναμενόμενο αποτέλεσμα

Η εκτέλεση του προγράμματος εκτυπώνει μια γραμμή επιβεβαίωσης:

```
Workbook saved as CSV at: YOUR_DIRECTORY\output.csv
```

Ανοίξτε το `output.csv` σε έναν επεξεργαστή κειμένου ή το Excel – θα δείτε τα δεδομένα από το πρώτο φύλλο, με τους αριθμούς στρογγυλοποιημένους σε πέντε σημαντικά ψηφία.

## Πώς να μετατρέψετε xlsx σε csv με προσαρμοσμένους οριοθέτες

Εάν το σύστημα downstream σας αναμένει ένα αρχείο διαχωρισμένο με tabs, απλώς αλλάξτε την ιδιότητα `Separator`:

```csharp
csvOptions.Separator = '\t';   // use a tab character
```

Αυτή η μικρή τροποποίηση σας επιτρέπει να **convert Excel to CSV** για οποιοδήποτε διαχωριστικό χωρίς να αλλάξετε τον υπόλοιπο κώδικα.

## Εξαγωγή φύλλου εργασίας σε CSV διατηρώντας τους τύπους ως τιμές

Το Aspose.Cells αξιολογεί τους τύπους αυτόματα κατά τη διάρκεια της αποθήκευσης, έτσι το CSV περιέχει τις **calculated values**, όχι τους ακατέργαστους τύπους. Εάν χρειάζεστε το ακατέργαστο κείμενο του τύπου, ορίστε `csvOptions.ExportFormulaValues = false`:

```csharp
csvOptions.ExportFormulaValues = false; // writes the formula string itself
```

Οι περισσότερες περιπτώσεις αναφοράς απαιτούν το αξιολογημένο αποτέλεσμα, γι' αυτό η προεπιλεγμένη συμπεριφορά ευθυγραμμίζεται με τη συνήθη χρήση **export spreadsheet to CSV**.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| Οι αριθμοί εμφανίζονται σε επιστημονική σημειογραφία | Μεγάλες ή πολύ μικρές τιμές μορφοποιούνται αυτόματα | Ορίστε `csvOptions.UseScientificNotation = false` ή προσαρμόστε το `SignificantDigits`. |
| Οι μη‑ASCII χαρακτήρες γίνονται ακατάληπτοι | Το CSV αποθηκεύεται με την προεπιλεγμένη κωδικοποίηση ANSI | Καθορίστε `Encoding = Encoding.UTF8` στο `CsvSaveOptions`. |
| Πολλαπλά φύλλα εργασίας συγχωνεύονται σε ένα CSV | Από προεπιλογή όλα τα φύλλα εργασίας συνενώνονται | Ορίστε `csvOptions.ExportActiveWorksheetOnly = true` και ενεργοποιήστε το επιθυμητό φύλλο μέσω `workbook.Worksheets[0].Activate()`. |
| Επιπλέον κενές γραμμές στο τέλος του αρχείου | Κάποιες βιβλιοθήκες προσθέτουν μια νέα γραμμή μετά την τελευταία εγγραφή | Κόψτε το αρχείο μετά την αποθήκευση ή ορίστε `csvOptions.AddTrailingNewLine = false`. |

Η αντιμετώπιση αυτών των ζητημάτων εκ των προτέρων σας εξοικονομεί χρόνο εντοπισμού σφαλμάτων αργότερα, όταν το CSV καταναλώνεται από άλλο σύστημα.

## Εξαγωγή Excel σε CSV σε web API (προαιρετικό)

Εάν χρειάζεται να εκθέσετε τη μετατροπή ως REST endpoint, μπορείτε να μεταφέρετε το CSV απευθείας στην HTTP response αντί να το γράψετε στο δίσκο:

```csharp
[HttpGet("api/convert")]
public IActionResult ConvertToCsv()
{
    var workbook = new Workbook("input.xlsx");
    var options = new CsvSaveOptions { SignificantDigits = 5 };
    using var stream = new MemoryStream();
    workbook.Save(stream, options);
    stream.Position = 0;
    return File(stream, "text/csv", "output.csv");
}
```

Αυτό το πρότυπο σας επιτρέπει να **export Excel to CSV** κατόπιν αιτήματος χωρίς τη δημιουργία προσωρινών αρχείων στον διακομιστή.

## Συμπέρασμα

Τώρα ξέρετε πώς να **save workbook as CSV** χρησιμοποιώντας C#. Ο οδηγός κάλυψε τη φόρτωση ενός αρχείου Excel, τη διαμόρφωση του `CsvSaveOptions` για ακρίβεια και διαχωριστικά, και τη γραφή του αποτελέσματος σε δίσκο ή σε ροή απόκρισης. Με αυτά τα βήματα μπορείτε επίσης να **convert Excel to CSV**, **export Excel to CSV**, και **export spreadsheet to CSV** για οποιοδήποτε downstream pipeline επεξεργασίας.

Στη συνέχεια, εξετάστε:

* **Πώς να μετατρέψετε xlsx σε CSV** με πολλαπλά φύλλα εργασίας (επανάληψη μέσω `workbook.Worksheets`).
* Προσθήκη προσαρμοσμένων κεφαλίδων ή υποσέλιδων πριν την εξαγωγή.
* Χρήση άλλων βιβλιοθηκών όπως **ClosedXML** ή **EPPlus** εάν έχετε περιορισμούς αδειοδότησης.

Νιώστε ελεύθεροι να πειραματιστείτε με τις επιλογές που παρουσιάστηκαν και να προσαρμόσετε τον κώδικα ώστε να ταιριάζει στις συγκεκριμένες απαιτήσεις του έργου σας. Καλός κώδικας!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικότα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Αποθήκευση Βιβλίου Εργασίας ως CSV – Πλήρης Οδηγός για Εξαγωγή Excel σε CSV σε C#](/cells/english/net/csv-file-handling/save-workbook-as-csv-complete-guide-to-export-excel-to-csv-i/)
- [Πώς να εξάγετε βιβλίο εργασίας Excel σε CSV με Aspose.Cells σε C#](/cells/english/net/csv-file-handling/how-to-export-excel-workbook-to-csv-with-aspose-cells-in-c/)
- [Πώς να αποθηκεύσετε βιβλίο εργασίας ως CSV με ακριβή μορφοποίηση χρησιμοποιώντας Aspose.Cells](/cells/english/net/csv-file-handling/how-to-save-workbook-as-csv-with-precise-formatting-using-as/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}