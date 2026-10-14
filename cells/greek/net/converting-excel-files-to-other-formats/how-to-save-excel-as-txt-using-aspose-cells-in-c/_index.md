---
category: general
date: 2026-10-13
description: Μάθετε πώς να αποθηκεύετε το Excel ως TXT με το Aspose.Cells. Αυτός ο
  οδηγός καλύπτει την εξαγωγή του Excel σε TXT, τη γραφή τιμής σε κελί και τον ορισμό
  σημαντικών ψηφίων σε λίγα μόνο βήματα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as txt
- export excel to txt
- write value to cell
- set significant digits
- export spreadsheet as txt
language: el
lastmod: 2026-10-13
og_description: Αποθηκεύστε το Excel ως TXT με το Aspose.Cells. Μάθετε πώς να εξάγετε
  το Excel σε TXT, να γράψετε τιμή σε κελί και να ορίσετε σημαντικά ψηφία με λίγες
  μόνο γραμμές κώδικα C#.
og_image_alt: Screenshot showing a workbook saved as a TXT file using save excel as
  txt
og_title: Αποθήκευση Excel ως TXT – βήμα‑βήμα οδηγός για προγραμματιστές .NET
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to save Excel as TXT with Aspose.Cells. This guide covers
    export Excel to TXT, write value to cell, and set significant digits in just a
    few steps.
  headline: How to save Excel as TXT using Aspose.Cells in C#
  type: TechArticle
- questions:
  - answer: It rounds to the nearest value based on the specified number of significant
      digits, ensuring the output is mathematically accurate to that precision.
    question: Does `SignificantDigits` round or truncate?
  - answer: 'Yes. Replace the file path with a `MemoryStream` instance: `workbook.Save(stream,
      txtOptions);`. This is handy for web APIs that need to return the TXT content
      without touching the file system.'
    question: Can I export directly to a memory stream?
  - answer: 'Use `txtOptions.ExportFormattedValues = true`. This forces Aspose.Cells
      to write the cell’s displayed text rather than the raw value. ## Conclusion
      You now know how to **save Excel as TXT** with full control over precision,
      formatting, and output location. By following the four steps—create a workbo'
    question: What if I need to keep the original formatting (e.g., dates)?
  type: FAQPage
tags:
- Excel
- TXT
- Aspose.Cells
- .NET
title: Πώς να αποθηκεύσετε το Excel ως TXT χρησιμοποιώντας το Aspose.Cells σε C#
url: /el/net/converting-excel-files-to-other-formats/how-to-save-excel-as-txt-using-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αποθηκεύσετε το Excel ως TXT χρησιμοποιώντας το Aspose.Cells σε C#

Εάν χρειάζεστε γρήγορη **αποθήκευση του Excel ως TXT**, αυτό το tutorial δείχνει τη διαδικασία ολοκληρωμένα σε λιγότερο από πέντε λεπτά. Θα δείτε πώς να εξάγετε το Excel σε TXT, να γράψετε τιμή σε κελί και να ορίσετε σημαντικά ψηφία ώστε το αρχείο κειμένου να περιέχει ακριβώς τα δεδομένα που αναμένετε.

Η εξαγωγή ενός υπολογιστικού φύλλου ως TXT είναι χρήσιμη όταν τα συστήματα downstream δέχονται μόνο απλό‑κείμενο, όταν χρειάζεται να δημιουργήσετε αρχεία καταγραφής, ή όταν θέλετε μια ανθρώπινα αναγνώσιμη αποτύπωση των υπολογισμών. Το παρακάτω παράδειγμα λειτουργεί με Aspose.Cells v25.10 ή νεότερη και εκτελείται σε οποιοδήποτε runtime .NET 6+.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Ένα αδειοδοτημένο αντίγραφο του **Aspose.Cells for .NET** (η δωρεάν δοκιμαστική έκδοση λειτουργεί για δοκιμές).
* .NET 6 SDK ή νεότερο εγκατεστημένο.
* Ένα IDE όπως το Visual Studio 2022, VS Code ή Rider.
* Βασικές γνώσεις C# — δεν απαιτείται προχωρημένη εμπειρία αυτοματοποίησης Excel.

Μπορείτε να εγκαταστήσετε το πακέτο NuGet Aspose.Cells με:

```bash
dotnet add package Aspose.Cells
```

## Βήμα 1: Δημιουργία βιβλίου εργασίας και πρόσβαση στο πρώτο φύλλο (αποθήκευση excel ως txt)

Το πρώτο βήμα όταν θέλετε να **αποθηκεύσετε το Excel ως TXT** είναι να δημιουργήσετε ένα αντικείμενο `Workbook`. Αυτό το αντικείμενο αντιπροσωπεύει ολόκληρο το αρχείο Excel στη μνήμη.

```csharp
using Aspose.Cells;

// Create a new workbook (an empty Excel file)
Workbook workbook = new Workbook();

// Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

> **Γιατί είναι σημαντικό:** Η κλάση `Workbook` είναι το σημείο εισόδου για όλες τις λειτουργίες του υπολογιστικού φύλλου. Ξεκινώντας με ένα νέο βιβλίο εργασίας αποφεύγετε τυχόν κρυφή μορφοποίηση που θα μπορούσε να επηρεάσει την έξοδο plain‑text.

## Βήμα 2: Εγγραφή αριθμού υψηλής ακρίβειας σε κελί (write value to cell)

Τώρα χρειάζεται να **write value to cell** A1. Η μέθοδος `PutValue` εντοπίζει αυτόματα τον τύπο δεδομένων και το αποθηκεύει ως αριθμητική τιμή.

```csharp
// Write a high‑precision number into cell A1
worksheet.Cells["A1"].PutValue(12345.6789012345);
```

> **Συμβουλή:** Αν αργότερα χρειαστεί να γράψετε συμβολοσειρές, ημερομηνίες ή τύπους, η ίδια μέθοδος `PutValue` λειτουργεί — απλώς περάστε τον κατάλληλο τύπο .NET.

## Βήμα 3: Διαμόρφωση επιλογών εξαγωγής για διατήρηση μόνο της απαιτούμενης ακρίβειας (set significant digits)

Κατά την εξαγωγή σε αρχείο TXT, συχνά θέλετε να περιορίσετε τον αριθμό των ψηφίων για να διατηρήσετε το μέγεθος του αρχείου μικρό ή για να ταιριάζει με προδιαγραφή downstream. Η κλάση `TxtSaveOptions` παρέχει την ιδιότητα `SignificantDigits` για αυτόν τον σκοπό.

```csharp
// Configure TXT save options to retain only 6 significant digits
TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
{
    SignificantDigits = 6   // New option in v25.10
};
```

> **Γιατί πρέπει να ορίσετε σημαντικά ψηφία:** Χωρίς αυτή τη ρύθμιση, το Aspose.Cells γράφει την πλήρη τιμή double‑precision, η οποία μπορεί να δημιουργήσει μακριές αλφαριθμητικές ακολουθίες όπως `12345.6789012345`. Ορίζοντας `SignificantDigits = 6` περικόπτει την έξοδο σε `12345.7`, ταιριάζοντας με τις περισσότερες απαιτήσεις αναφοράς.

## Βήμα 4: Εξαγωγή του βιβλίου εργασίας ως αρχείο TXT (export excel to txt)

Τέλος, **εξάγετε το Excel σε TXT** καλώντας το `Workbook.Save` με τις προηγουμένως διαμορφωμένες επιλογές.

```csharp
// Save the workbook as a TXT file using the configured options
string outputPath = @"C:\Temp\LimitedDigits.txt";
workbook.Save(outputPath, txtSaveOptions);
```

Όταν ολοκληρωθεί ο κώδικας, το `LimitedDigits.txt` περιέχει:

```
12345.7
```

> **Επαλήθευση αποτελέσματος:** Ανοίξτε το αρχείο σε οποιονδήποτε επεξεργαστή κειμένου (Notepad, VS Code) για να επιβεβαιώσετε ότι υπάρχουν μόνο έξι σημαντικά ψηφία και ότι δεν εμφανίζονται επιπλέον κόμματα ή διαχωριστικά tab.

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω υπάρχει μια αυτόνομη εφαρμογή κονσόλας που μπορείτε να αντιγράψετε, επικολλήσετε και να εκτελέσετε αμέσως.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Write a high‑precision number to cell A1
            worksheet.Cells["A1"].PutValue(12345.6789012345);

            // 3️⃣ Set up TXT save options with 6 significant digits
            TxtSaveOptions txtOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                SignificantDigits = 6
            };

            // 4️⃣ Save as TXT
            string path = @"C:\Temp\LimitedDigits.txt";
            workbook.Save(path, txtOptions);

            Console.WriteLine($"Workbook exported to TXT at: {path}");
        }
    }
}
```

**Επεξήγηση κάθε μπλοκ**

| Block | Purpose |
|-------|---------|
| `using Aspose.Cells;` | Εισάγει το namespace Aspose.Cells που απαιτείται για `Workbook`, `Worksheet` και `TxtSaveOptions`. |
| `Workbook workbook = new Workbook();` | Δημιουργεί ένα κενό βιβλίο εργασίας Excel στη μνήμη. |
| `worksheet.Cells["A1"].PutValue(...);` | **write value to cell** A1 με αριθμό double‑precision. |
| `TxtSaveOptions` | Διαμορφώνει τη συμπεριφορά **set significant digits** για την εξαγωγή TXT. |
| `workbook.Save(..., txtOptions);` | Εκτελεί τη λειτουργία **export excel to txt**, δημιουργώντας το αρχείο plain‑text. |

## Περιπτώσεις άκρων και πρόσθετες συμβουλές

| Scenario | How to handle |
|----------|---------------|
| **Μεγάλα φύλλα εργασίας** (πολλές γραμμές/στήλες) | Χρησιμοποιήστε `txtOptions.Encoding = Encoding.UTF8` εάν χρειάζεστε υποστήριξη Unicode, και σκεφτείτε τη ροή του αρχείου με `Workbook.Save(Stream, txtOptions)` για αποφυγή υψηλής χρήσης μνήμης. |
| **Προσαρμοσμένοι διαχωριστές** (τιμές διαχωρισμένες με κόμμα) | `TxtSaveOptions` εκθέτει επίσης το `Separator` — ορίστε το σε `','` για παραγωγή εξόδου τύπου CSV ενώ χρησιμοποιείται ακόμη η μορφή TXT. |
| **Διατήρηση τύπων** | Ορίστε `txtOptions.ExportFormulas = true` για να γράψετε το κείμενο του τύπου αντί για την υπολογισμένη τιμή. |
| **Δεκαδικοί διαχωριστές ανάλογα με την τοπική ρύθμιση** | Ρυθμίστε `txtOptions.DecimalSeparator` σε `','` για ευρωπαϊκές τοπικές ρυθμίσεις. |
| **Πολλαπλά φύλλα εργασίας** | Κάντε βρόχο μέσω `workbook.Worksheets` και καλέστε `Save` για κάθε ένα, προσθέτοντας το όνομα του φύλλου στο όνομα του αρχείου. |

## Συχνές ερωτήσεις

**Ε: Το `SignificantDigits` στρογγυλοποιεί ή περικόπτει;**  
Α: Στρογγυλοποιεί στην πλησιέστερη τιμή βάσει του καθορισμένου αριθμού σημαντικών ψηφίων, διασφαλίζοντας ότι η έξοδος είναι μαθηματικά ακριβής σε εκείνη την ακρίβεια.

**Ε: Μπορώ να εξάγω απευθείας σε ροή μνήμης (memory stream);**  
Α: Ναι. Αντικαταστήστε τη διαδρομή αρχείου με μια παρουσία `MemoryStream`: `workbook.Save(stream, txtOptions);`. Αυτό είναι χρήσιμο για web APIs που χρειάζονται να επιστρέψουν το περιεχόμενο TXT χωρίς να αγγίξουν το σύστημα αρχείων.

**Ε: Τι γίνεται αν χρειαστεί να διατηρήσω την αρχική μορφοποίηση (π.χ., ημερομηνίες);**  
Α: Χρησιμοποιήστε `txtOptions.ExportFormattedValues = true`. Αυτό αναγκάζει το Aspose.Cells να γράψει το εμφανιζόμενο κείμενο του κελιού αντί για την ακατέργαστη τιμή.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **αποθηκεύσετε το Excel ως TXT** με πλήρη έλεγχο της ακρίβειας, της μορφοποίησης και της τοποθεσίας εξόδου. Ακολουθώντας τα τέσσερα βήματα — δημιουργία βιβλίου εργασίας, **write value to cell**, **set significant digits**, και **export Excel to TXT** — μπορείτε να ενσωματώσετε την εξαγωγή plain‑text σε οποιαδήποτε εφαρμογή .NET.

Στη συνέχεια, εξερευνήστε συναφή θέματα όπως **εξαγωγή υπολογιστικού φύλλου ως TXT με προσαρμοσμένους διαχωριστές**, **μετατροπή Excel σε CSV**, ή **χρήση Aspose.Cells για δημιουργία αναφορών JSON**. Κάθε ένα από αυτά βασίζεται στις ίδιες βασικές έννοιες που παρουσιάστηκαν εδώ, παρέχοντάς σας ένα ευέλικτο σύνολο εργαλείων για ανταλλαγή δεδομένων μεταξύ πλατφορμών.

Καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Save Excel as Text – Complete C# Guide to Export Excel to TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Create New Workbook and Export Excel to TXT with Precision](/cells/english/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/)
- [Create new workbook – Export Excel to TXT with Full Precision](/cells/english/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}