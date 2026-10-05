---
category: general
date: 2026-04-07
description: Μάθετε πώς να ανανεώσετε το pivot, να εισάγετε εικόνα στο Excel και να
  αποθηκεύσετε το βιβλίο εργασίας του Excel με έναν χώρο κράτησης εικόνας σε λίγα
  μόνο βήματα.
draft: false
keywords:
- how to refresh pivot
- insert image into excel
- save excel workbook
- add picture placeholder
- refresh pivot table
language: el
og_description: Πώς να ανανεώσετε το pivot στο Excel, να εισάγετε εικόνα στο Excel
  και να αποθηκεύσετε το βιβλίο εργασίας Excel χρησιμοποιώντας C# με θέση κράτησης
  εικόνας. Παράδειγμα κώδικα βήμα‑βήμα.
og_title: Πώς να ανανεώσετε τον συγκεντρωτικό πίνακα και να εισάγετε εικόνα στο Excel
  – Πλήρης Οδηγός
tags:
- Aspose.Cells
- C#
- Excel automation
title: Πώς να ανανεώσετε τον πίνακα Pivot και να εισάγετε εικόνα στο Excel – Πλήρης
  Οδηγός
url: /el/net/pivot-tables/how-to-refresh-pivot-and-insert-image-into-excel-complete-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ανανεώσετε το pivot και να εισάγετε εικόνα στο Excel – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να ανανεώσετε το pivot** όταν αλλάζουν τα δεδομένα προέλευσης και, στη συνέχεια, να τοποθετήσετε μια φρέσκια εικόνα γραφήματος ή πίνακα στο ίδιο φύλλο; Δεν είστε ο μόνος. Σε πολλές αλυσίδες αναφοράς τα δεδομένα βρίσκονται σε μια βάση δεδομένων, ο πίνακας pivot τα αντλεί, και το τελικό αρχείο Excel πρέπει να εμφανίζει τους πιο πρόσφατους αριθμούς ως εικόνα—ώστε οι επόμενοι χρήστες να μην μπορούν να επεξεργαστούν τυχαία την πηγή.  

Σε αυτό το σεμινάριο θα περάσουμε ακριβώς από αυτό: **πώς να ανανεώσετε το pivot**, **να εισάγετε εικόνα στο Excel**, και τέλος **να αποθηκεύσετε το βιβλίο εργασίας Excel** χρησιμοποιώντας ένα **placeholder εικόνας**. Στο τέλος θα έχετε ένα ενιαίο, εκτελέσιμο πρόγραμμα C# που κάνει τα πάντα, και θα καταλάβετε γιατί κάθε γραμμή είναι σημαντική.

> **Συμβουλή:** Η προσέγγιση λειτουργεί με Aspose.Cells 2024 ή νεότερη έκδοση, πράγμα που σημαίνει ότι δεν χρειάζεται να έχετε εγκατεστημένο το Excel στον διακομιστή.

---

## Τι Θα Χρειαστεί

- **Aspose.Cells for .NET** (πακέτο NuGet `Aspose.Cells`).  
- .NET 6.0 SDK ή νεότερο (ο κώδικας μεταγλωττίζεται επίσης με .NET 8).  
- Ένα βασικό αρχείο Excel (`input.xlsx`) που ήδη περιέχει έναν πίνακα pivot και ένα placeholder εικόνας (το πρώτο αντικείμενο εικόνας στο φύλλο).  
- Λίγη περιέργεια για τα μοντέλα αντικειμένων του Excel.

Χωρίς επιπλέον COM interop, χωρίς εγκατάσταση Office, μόνο καθαρό C#.

---

## Πώς να Ανανεώσετε το Pivot και να Καταγράψετε τα Πιο Πρόσφατα Δεδομένα

Το πρώτο που πρέπει να κάνετε είναι να πείτε στο Excel (ή μάλλον στο Aspose.Cells) ότι ο πίνακας pivot πρέπει να επανυπολογιστεί με βάση το πιο πρόσφατο εύρος προέλευσης. Η παράλειψη αυτού του βήματος αφήνει παλαιά αριθμητικά δεδομένα, κάτι που αναιρεί ολόκληρο το σκοπό της αυτοματοποίησης.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// 1️⃣ Load the workbook and grab the first worksheet
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelDemo\input.xlsx");
Worksheet worksheet = workbook.Worksheets[0];

// 2️⃣ Refresh the first pivot table so it reflects the latest data
worksheet.PivotTables[0].Refresh();
```

**Γιατί είναι σημαντικό:**  
Όταν καλείτε `Refresh()`, η μηχανή του pivot εκτελεί ξανά τη λογική συγκέντρωσης. Αν αργότερα εξάγετε το pivot ως εικόνα, η εικόνα θα εμφανίζει τα *τρέχοντα* σύνολα, όχι εκείνα από την τελευταία αποθήκευση του αρχείου.

## Εισαγωγή Εικόνας στο Excel Χρησιμοποιώντας Placeholder Εικόνας

Τώρα που το pivot είναι φρέσκο, πρέπει να το μετατρέψουμε σε στατική εικόνα. Αυτό είναι χρήσιμο όταν θέλετε να κλειδώσετε το οπτικό για διανομή ή να το ενσωματώσετε σε διαφάνεια PowerPoint αργότερα.

```csharp
// 3️⃣ Set up image options – we want a PNG image
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png
};

// 4️⃣ Render the refreshed pivot table to an image using the options
Image pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);
```

Το αντικείμενο `ImageOrPrintOptions` σας επιτρέπει να ελέγχετε την ανάλυση, το φόντο και τη μορφή. Το PNG είναι χωρίς απώλειες και λειτουργεί εξαιρετικά για τις περισσότερες επιχειρηματικές αναφορές.

## Προσθήκη Placeholder Εικόνας σε Φύλλο Εργασίας

Τα περισσότερα πρότυπα Excel περιέχουν ήδη ένα σχήμα ή εικόνα που λειτουργεί ως “θέση” για δυναμικά γραφικά. Αν δεν έχετε κάποιο, απλώς εισάγετε μια κενή εικόνα στο Excel και αποθηκεύστε το πρότυπο—το Aspose.Cells θα το εκθέσει ως `Pictures[0]`.

```csharp
// 5️⃣ Place the rendered image into the first picture placeholder on the sheet
worksheet.Pictures[0].Image = pivotImage;
```

**Τι γίνεται αν έχετε πολλαπλά placeholders;**  
Απλώς αλλάξτε το δείκτη (`Pictures[1]`, `Pictures[2]`, …) ή κάντε βρόχο μέσω `worksheet.Pictures` για να βρείτε ένα με όνομα.

## Αποθήκευση Βιβλίου Εργασίας Excel μετά τις Τροποποιήσεις

Τέλος, διατηρούμε τις αλλαγές. Το βιβλίο εργασίας τώρα περιέχει ένα ανανεωμένο pivot, ένα πρόσφατα δημιουργημένο PNG, και το placeholder εικόνας ενημερωμένο με αυτήν την εικόνα.

```csharp
// 6️⃣ Save the workbook to see the result
workbook.Save(@"C:\MyProjects\ExcelDemo\output.xlsx");
```

Όταν ανοίξετε το `output.xlsx` θα δείτε τη θέση της εικόνας γεμάτη με το πιο πρόσφατο στιγμιότυπο του pivot. Δεν απαιτούνται χειροκίνητα βήματα.

## Πλήρες Παράδειγμα Εργασίας (Όλα τα Βήματα Μαζί)

Παρακάτω είναι το πλήρες, έτοιμο για αντιγραφή‑και‑επικόλληση πρόγραμμα. Περιλαμβάνει τις απαραίτητες δηλώσεις `using`, διαχείριση σφαλμάτων και σχόλια που εξηγούν κάθε μη‑προφανή γραμμή.

```csharp
using Aspose.Cells;
using System;
using System.Drawing.Imaging;

namespace ExcelPivotImageDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath = @"C:\MyProjects\ExcelDemo\input.xlsx";
            string outputPath = @"C:\MyProjects\ExcelDemo\output.xlsx";

            try
            {
                // Load workbook
                Workbook workbook = new Workbook(inputPath);
                Worksheet sheet = workbook.Worksheets[0];

                // -------------------------------------------------
                // Refresh pivot table – this is the core of "how to refresh pivot"
                // -------------------------------------------------
                if (sheet.PivotTables.Count == 0)
                {
                    Console.WriteLine("No pivot tables found on the first worksheet.");
                    return;
                }
                sheet.PivotTables[0].Refresh();

                // -------------------------------------------------
                // Convert refreshed pivot to PNG image
                // -------------------------------------------------
                ImageOrPrintOptions imgOpts = new ImageOrPrintOptions
                {
                    ImageFormat = ImageFormat.Png,
                    // Optional: higher DPI for sharper images
                    HorizontalResolution = 150,
                    VerticalResolution = 150
                };
                Image pivotImg = sheet.PivotTables[0].ToImage(imgOpts);

                // -------------------------------------------------
                // Insert the image into the first picture placeholder
                // -------------------------------------------------
                if (sheet.Pictures.Count == 0)
                {
                    // If the template lacks a placeholder, we create one on the fly
                    int picIdx = sheet.Pictures.Add(0, 0, pivotImg);
                    sheet.Pictures[picIdx].Name = "PivotSnapshot";
                }
                else
                {
                    sheet.Pictures[0].Image = pivotImg;
                }

                // -------------------------------------------------
                // Save the updated workbook – this fulfills "save excel workbook"
                // -------------------------------------------------
                workbook.Save(outputPath);
                Console.WriteLine($"Workbook saved successfully to {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
                // In production you might log the stack trace or rethrow
            }
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα:**  
Ανοίξτε το `output.xlsx`. Το πρώτο αντικείμενο εικόνας τώρα εμφανίζει ένα PNG του ανανεωμένου πίνακα pivot. Αν αλλάξετε τα δεδομένα προέλευσης στο `input.xlsx` και εκτελέσετε ξανά το πρόγραμμα, η εικόνα ενημερώνεται αυτόματα—χωρίς ανάγκη χειροκίνητης αντιγραφής‑επικόλλησης.

## Συνηθισμένες Παραλλαγές & Ακραίες Περιπτώσεις

| Κατάσταση | Τι να Αλλάξετε |
|-----------|----------------|
| **Πολλαπλοί πίνακες pivot** | Κάντε βρόχο μέσω `sheet.PivotTables` και ανανεώστε καθέναν, στη συνέχεια επιλέξτε αυτόν που χρειάζεστε για την εικόνα. |
| **Διαφορετική μορφή εικόνας** | Ορίστε `ImageFormat = ImageFormat.Jpeg` (ή `Bmp`) στο `ImageOrPrintOptions`. |
| **Δυναμική επιλογή placeholder** | Χρησιμοποιήστε `sheet.Pictures["MyPlaceholderName"]` αντί για δείκτη. |
| **Μεγάλα βιβλία εργασίας** | Αυξήστε το `Workbook.Settings.CalculateFormulaEngine` σε `EngineType.Fast` για ταχύτερες ανανεώσεις. |
| **Εκτέλεση σε server χωρίς UI** | Το Aspose.Cells λειτουργεί πλήρως χωρίς UI, οπότε δεν απαιτείται επιπλέον διαμόρφωση. |

## Συχνές Ερωτήσεις

**Ε: Λειτουργεί αυτό με βιβλία εργασίας που υποστηρίζουν μακροεντολές (`.xlsm`);**  
Α: Ναι. Το Aspose.Cells τα αντιμετωπίζει όπως οποιοδήποτε άλλο βιβλίο εργασίας· τα μακροεντολές διατηρούνται αλλά δεν εκτελούνται κατά την ανανέωση.

**Ε: Τι γίνεται αν το pivot χρησιμοποιεί εξωτερική πηγή δεδομένων;**  
Α: Πρέπει να διασφαλίσετε ότι η συμβολοσειρά σύνδεσης είναι έγκυρη στο μηχάνημα που εκτελεί τον κώδικα. Καλέστε `pivotTable.CacheDefinition.ConnectionInfo` για να την προσαρμόσετε προγραμματιστικά.

**Ε: Μπορώ να τοποθετήσω την εικόνα σε συγκεκριμένο εύρος κελιών αντί για placeholder εικόνας;**  
Α: Απόλυτα. Χρησιμοποιήστε `sheet.Pictures.Add(row, column, pivotImg)` όπου `row` και `column` είναι δείκτες με βάση το μηδέν.

## Συμπέρασμα

Έχουμε καλύψει **πώς να ανανεώσετε το pivot**, **να εισάγετε εικόνα στο Excel**, **να προσθέσετε placeholder εικόνας**, και τέλος **να αποθηκεύσετε το βιβλίο εργασίας Excel**—όλα σε ένα κομψό απόσπασμα C#. Ανανεώνοντας πρώτα το pivot, εξασφαλίζετε ότι η εικόνα αντικατοπτρίζει τους πιο πρόσφατους αριθμούς, και χρησιμοποιώντας ένα placeholder διατηρείτε τα πρότυπά σας καθαρά και επαναχρησιμοποιήσιμα.

Στη συνέχεια, μπορείτε να εξερευνήσετε:

- Εξαγωγή της ίδιας εικόνας σε αναφορά PDF (`PdfSaveOptions`).  
- Αυτοματοποίηση μιας δέσμης αρχείων με διαφορετικά δεδομένα προέλευσης.  
- Χρήση Aspose.Slides για επικόλληση του PNG απευθείας σε διαφάνεια PowerPoint.

Νιώστε ελεύθεροι να πειραματιστείτε—αντικαταστήστε το PNG με JPEG, αλλάξτε το DPI, ή προσθέστε πολλαπλές εικόνες. Η βασική ιδέα παραμένει η ίδια: διατηρήστε τα δεδομένα φρέσκα, καταγράψτε τα ως εικόνα και ενσωματώστε τα όπου τα χρειάζεστε.

Καλό προγραμματισμό! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}