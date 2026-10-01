---
category: general
date: 2026-10-01
description: Προσθέστε γράφημα στο Word με το Aspose σε λίγα λεπτά. Μάθετε πώς να
  ενσωματώσετε γράφημα Excel στο Word, να εξάγετε γράφημα Excel σε Word, να δημιουργήσετε
  έγγραφο Word με το Aspose και να αποθηκεύσετε το γράφημα σε έγγραφο Word.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add chart to word
- embed excel chart word
- export chart excel word
- create word document aspose
- save chart word document
language: el
lastmod: 2026-10-01
og_description: Προσθέστε διάγραμμα στο Word με το Aspose σε λίγα λεπτά. Αυτός ο οδηγός
  δείχνει πώς να ενσωματώσετε διάγραμμα Excel στο Word, να εξάγετε διάγραμμα Excel
  σε Word, να δημιουργήσετε έγγραφο Word με το Aspose και να αποθηκεύσετε το διάγραμμα
  σε έγγραφο Word.
og_image_alt: Screenshot illustrating how to add chart to Word using Aspose
og_title: Προσθήκη γραφήματος στο Word με το Aspose – ενσωμάτωση γραφήματος Excel
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  headline: How to add chart to Word with Aspose – embed Excel chart
  type: TechArticle
- description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  name: How to add chart to Word with Aspose – embed Excel chart
  steps:
  - name: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
    text: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
  - name: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
    text: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
  - name: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
    text: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
  - name: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
    text: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
  - name: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
    text: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
  type: HowTo
tags:
- Aspose
- C#
- Word automation
title: Πώς να προσθέσετε γράφημα στο Word με το Aspose – ενσωμάτωση γραφήματος Excel
url: /el/net/chart-rendering-and-conversion/how-to-add-chart-to-word-with-aspose-embed-excel-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να προσθέσετε γράφημα στο Word με το Aspose – ενσωμάτωση γραφήματος Excel

Αν χρειάζεστε να **add chart to Word** γρήγορα, αυτό το tutorial σας παρέχει μια πλήρη, έτοιμη‑για‑εκτέλεση λύση. Θα δείτε πώς να ενσωματώσετε ένα γράφημα Excel σε ένα αρχείο Word, να εξάγετε το γράφημα από το Excel στο Word, και τελικά **save chart Word document** με μόνο μερικές γραμμές C#.

Η ενσωμάτωση γραφημάτων είναι μια κοινή απαίτηση όταν δημιουργείτε αναφορές, τιμολόγια ή πίνακες ελέγχου προγραμματιστικά. Στο τέλος αυτού του οδηγού θα μπορείτε να **create Word document Aspose** που περιέχει οποιοδήποτε γράφημα από ένα βιβλίο εργασίας Excel, χωρίς χειροκίνητο copy‑paste.

## Prerequisites

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7+)
- Πακέτα NuGet Aspose.Cells και Aspose.Words (εγκατάσταση μέσω `dotnet add package Aspose.Cells` και `dotnet add package Aspose.Words`)
- Ένα υπάρχον αρχείο Excel (`Chart.xlsx`) που περιέχει τουλάχιστον ένα γράφημα
- Ένα περιβάλλον ανάπτυξης όπως Visual Studio 2022 ή VS Code

## Add chart to Word with Aspose

Παρακάτω βρίσκεται το πλήρες, αυτόνομο πρόγραμμα. Αντιγράψτε το σε ένα νέο έργο console, επαναφέρετε τα πακέτα και τρέξτε το. Το πρόγραμμα φορτώνει το βιβλίο εργασίας Excel, δημιουργεί ένα έγγραφο Word, εισάγει το πρώτο γράφημα και αποθηκεύει το αποτέλεσμα.

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

namespace AddChartToWordDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the Excel workbook that contains the chart
            var workbookPath = @"YOUR_DIRECTORY\Chart.xlsx";
            var workbook = new Workbook(workbookPath);

            // Step 2: Create a new Word document that will receive the chart
            var wordDoc = new Document();

            // Step 3: Initialise a DocumentBuilder for the Word document
            var builder = new DocumentBuilder(wordDoc);

            // Step 4: Insert the first chart from the first worksheet into the Word document
            // This uses Aspose.Words' InsertChart overload that accepts an Aspose.Cells chart object
            builder.InsertChart(workbook.Worksheets[0].Charts[0]);

            // Step 5: Save the resulting Word document
            var outputPath = @"YOUR_DIRECTORY\Chart.docx";
            wordDoc.Save(outputPath);

            Console.WriteLine($"Chart successfully added and saved to '{outputPath}'.");
        }
    }
}
```

### Why each line matters

1. **Loading the workbook** – `Workbook` αναλύει το αρχείο Excel και σας παρέχει προγραμματιστική πρόσβαση στα φύλλα εργασίας και τα γραφήματα του.  
2. **Creating the Word document** – `Document` είναι το σημείο εισόδου του Aspose.Words για οποιαδήποτε εργασία επεξεργασίας Word.  
3. **DocumentBuilder** – Αυτή η βοηθητική κλάση σας επιτρέπει να εισάγετε περιεχόμενο (κείμενο, εικόνες, γραφήματα) στη τρέχουσα θέση του δρομέα.  
4. **InsertChart** – Η υπερφόρτωση που δέχεται ένα αντικείμενο `Aspose.Cells.Chart` αντιγράφει τα δεδομένα, τη μορφοποίηση και τις σειρές του γραφήματος απευθείας στο αρχείο Word. Δεν απαιτείται ενδιάμεση μετατροπή εικόνας, διατηρώντας την ποιότητα του διανύσματος.  
5. **Save** – `Save` γράφει το πακέτο .docx στο δίσκο, ολοκληρώνοντας το βήμα **save chart word document**.

#### Expected output

Μετά την εκτέλεση του προγράμματος, ανοίξτε το `Chart.docx`. Θα δείτε το ακριβές γράφημα που ήταν αποθηκευμένο στο `Chart.xlsx`, τοποθετημένο εκεί που τοποθετήθηκε ο builder (στην αρχή του εγγράφου). Το γράφημα παραμένει πλήρως επεξεργάσιμο μέσα στο Word (μπορείτε να αλλάξετε το μέγεθος, τα χρώματα ή να τροποποιήσετε την πηγή δεδομένων).

## Embed Excel chart in Word

Αν χρειάζεστε να ενσωματώσετε περισσότερα από ένα γραφήματα, επαναλάβετε την κλήση `InsertChart` για κάθε αντικείμενο γραφήματος. Για παράδειγμα, για να ενσωματώσετε όλα τα γραφήματα από το πρώτο φύλλο εργασίας:

```csharp
var sheet = workbook.Worksheets[0];
foreach (Chart chart in sheet.Charts)
{
    builder.InsertChart(chart);
    builder.Writeln(); // add a line break between charts
}
```

**Pro tip:** Χρησιμοποιήστε `builder.Writeln()` για να εισάγετε ένα διάλειμμα παραγράφου, εξασφαλίζοντας ότι κάθε γράφημα ξεκινά σε νέα γραμμή.

## Export chart Excel Word – handling multiple worksheets

Όταν τα γραφήματα είναι διασκορπισμένα σε πολλά φύλλα εργασίας, επαναλάβετε τη συλλογή `Worksheets` του βιβλίου εργασίας:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    foreach (Chart chart in ws.Charts)
    {
        builder.InsertChart(chart);
        builder.Writeln();
    }
}
```

Αυτή η προσέγγιση **export chart Excel Word** για οποιαδήποτε διάταξη βιβλίου εργασίας, καθιστώντας τη λύση ανθεκτική για σύνθετες αναφορές.

## Create Word document Aspose – customizing appearance

Μπορείτε να ελέγξετε το μέγεθος και τη θέση κάθε εισαχθέντος γραφήματος τροποποιώντας το `Shape` που επιστρέφεται από το `InsertChart`:

```csharp
Shape chartShape = builder.InsertChart(chart);
chartShape.Width = 500;   // width in points
chartShape.Height = 300;  // height in points
chartShape.WrapType = WrapType.Inline; // make the chart flow with text
```

Η ρύθμιση του `WrapType` σε `Inline` εξασφαλίζει ότι το γράφημα συμπεριφέρεται όπως μια κανονική παράγραφος, κάτι που συχνά είναι επιθυμητό για αυτοματοποιημένη δημιουργία εγγράφων.

## Save chart Word document – best practices

- **Use a descriptive file name** (`Report_Q1_2026.docx`) για να κάνετε πιο εύκολη τη διαχείριση εκδόσεων.
- **Dispose objects** όταν τελειώσετε, ειδικά σε μεγάλες διαδικασίες παρτίδας:

```csharp
wordDoc.Dispose();
workbook.Dispose();
```

- **Validate the result** προγραμματιστικά εάν δημιουργείτε πολλά αρχεία:

```csharp
if (System.IO.File.Exists(outputPath))
{
    Console.WriteLine("File saved successfully.");
}
else
{
    Console.Error.WriteLine("Failed to save the document.");
}
```

## Common questions & edge cases

| Ερώτηση | Απάντηση |
|----------|--------|
| *Μπορώ να εισάγω ένα γράφημα που δεν είναι το πρώτο στο φύλλο;* | Ναι. Πρόσβαση μέσω δείκτη: `sheet.Charts[2]` για το τρίτο γράφημα. |
| *Τι γίνεται αν το γράφημα Excel χρησιμοποιεί πηγή δεδομένων που δεν υπάρχει στο βιβλίο εργασίας;* | Το Aspose.Cells ενσωματώνει τα δεδομένα απευθείας στο αντικείμενο γραφήματος, έτσι το γράφημα παραμένει λειτουργικό ακόμη και αν η πηγή δεδομένων αφαιρεθεί. |
| *Χρειάζομαι άδεια για το Aspose;* | Μια δωρεάν αξιολόγηση λειτουργεί, αλλά μια άδεια έκδοση αφαιρεί το υδατογράφημα αξιολόγησης και ξεκλειδώνει όλες τις λειτουργίες. |
| *Θα είναι το γράφημα επεξεργάσιμο στο Word μετά την εισαγωγή;* | Το γράφημα εισάγεται ως εγγενές γράφημα Word, ώστε οι χρήστες να μπορούν να επεξεργαστούν σειρές, τίτλους και στυλ μέσω του UI του Word. |
| *Πώς να εισάγετε ένα γράφημα ως εικόνα αντί για εγγενές γράφημα;* | Χρησιμοποιήστε `builder.InsertImage(chart.ToImage())` για να ενσωματώσετε μια ραστερ εικόνα. Αυτό είναι χρήσιμο όταν θέλετε να διατηρήσετε την ακριβή οπτική απόδοση χωρίς δυνατότητα επεξεργασίας σε επίπεδο Word. |

## Full working example (copy‑paste)

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

class AddChartToWord
{
    static void Main()
    {
        // Load Excel workbook
        var wb = new Workbook(@"C:\Data\Chart.xlsx");

        // Create Word document
        var doc = new Document();
        var builder = new DocumentBuilder(doc);

        // Insert every chart from every worksheet
        foreach (Worksheet ws in wb.Worksheets)
        {
            foreach (Chart ch in ws.Charts)
            {
                Shape shape = builder.InsertChart(ch);
                shape.Width = 500;
                shape.Height = 300;
                builder.Writeln(); // separate charts
            }
        }

        // Save the document
        var outPath = @"C:\Data\ReportWithCharts.docx";
        doc.Save(outPath);
        Console.WriteLine($"Document saved to {outPath}");
    }
}
```

Η εκτέλεση του κώδικα παράγει ένα αρχείο Word (`ReportWithCharts.docx`) που περιέχει αποτελέσματα **add chart to word** για κάθε γράφημα στο πηγαίο βιβλίο εργασίας.

## Conclusion

Τώρα γνωρίζετε πώς να **add chart to Word** χρησιμοποιώντας Aspose.Cells και Aspose.Words, πώς να **embed Excel chart word**, **export chart Excel Word**, **create Word document Aspose**, και τελικά **save chart word document**. Η προσέγγιση λειτουργεί για σενάρια με ένα μόνο γράφημα καθώς και για σύνθετα βιβλία εργασίας με πολλά γραφήματα σε πολλαπλά φύλλα εργασίας.

- Εφαρμόστε προσαρμοσμένο στυλ στα εισαχθέντα γραφήματα (χρώματα, γραμματοσειρές) μέσω του API `Chart`.
- Συνδυάστε την εισαγωγή γραφήματος με τη δημιουργία κειμένου για την παραγωγή πλήρως αυτοματοποιημένων αναφορών.
- Use Aspose.Slides if you need

## What Should You Learn Next?

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να αποθηκεύσετε DOCX από Excel – Πλήρης οδηγός εξαγωγής γραφημάτων σε Word](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-docx-from-excel-complete-guide-to-export-charts/)
- [Δημιουργία βιβλίου εργασίας Excel με γράφημα πίτας χρησιμοποιώντας Aspose.Cells .NET - Αναλυτικός οδηγός](/cells/english/net/charts-graphs/create-excel-workbook-pie-chart-aspose-cells-net/)
- [Δημιουργία γραφήματος φυσαλίδας σε Excel χρησιμοποιώντας Aspose.Cells .NET&#58; Οδηγός βήμα‑βήμα](/cells/english/net/charts-graphs/create-bubble-chart-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}