---
category: general
date: 2026-10-20
description: Μάθετε πώς να χρησιμοποιείτε το wrapcols στο Aspose.Cells, να ενσωματώνετε
  γραμματοσειρές σε HTML και να αποθηκεύετε το Excel ως HTML με ένα πλήρες παράδειγμα
  C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- embed fonts in html
- save excel as html
- convert workbook to html
- use wrapcols function
language: el
lastmod: 2026-10-20
og_description: Πώς να χρησιμοποιήσετε το wrapcols στο Aspose.Cells, να ενσωματώσετε
  γραμματοσειρές σε HTML και να μετατρέψετε ένα βιβλίο εργασίας σε HTML με έναν σαφή
  οδηγό C# για προγραμματιστές.
og_image_alt: Screenshot of an Excel workbook saved as HTML with embedded fonts using
  Aspose.Cells
og_title: Πώς να χρησιμοποιήσετε το wrapcols και να ενσωματώσετε γραμματοσειρές κατά
  την εξαγωγή του Excel σε HTML
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to use wrapcols in Aspose.Cells, embed fonts in HTML, and
    save Excel as HTML with a complete C# example.
  headline: How to use wrapcols and embed fonts saving Excel to HTML
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel to HTML
- Smart Markers
title: Πώς να χρησιμοποιήσετε το wrapcols και να ενσωματώσετε γραμματοσειρές κατά
  την αποθήκευση του Excel σε HTML
url: /el/net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χρησιμοποιήσετε το wrapcols και να ενσωματώσετε γραμματοσειρές αποθηκεύοντας το Excel σε HTML

Αν χρειάζεστε **πώς να χρησιμοποιήσετε το wrapcols** σε έναν τύπο Aspose.Cells, αυτός ο οδηγός σας δείχνει τα ακριβή βήματα. Θα μάθετε επίσης πώς να **ενσωματώσετε γραμματοσειρές σε HTML** και **αποθηκεύσετε το Excel ως HTML** ώστε το αποτέλεσμα να φαίνεται ταυτόσημο σε όλα τα προγράμματα περιήγησης.  

Το σεμινάριο καλύπτει τρία πρακτικά σενάρια: χρήση της συνάρτησης `WRAPCOLS`, εξαγωγή ενός βιβλίου εργασίας με ενσωματωμένες γραμματοσειρές, και δημιουργία αναφοράς master‑detail με Smart Markers. Στο τέλος θα έχετε ένα ενιαίο, εκτελέσιμο πρόγραμμα C# που επιδεικνύει όλες αυτές τις δυνατότητες.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 (ή νεότερη) εγκατεστημένο.  
* Aspose.Cells for .NET προστέθηκε στο έργο σας (`dotnet add package Aspose.Cells`).  
* Βασική εξοικείωση με C# και τύπους Excel.  

Δεν απαιτούνται πρόσθετες βιβλιοθήκες τρίτων· το Aspose.Cells διαχειρίζεται τη μετατροπή σε HTML και την ενσωμάτωση γραμματοσειρών εσωτερικά.

## Βήμα 1: Επιδείξτε τη λειτουργία **πώς να χρησιμοποιήσετε το wrapcols** σε έναν τύπο

Η συνάρτηση `WRAPCOLS` χωρίζει μια μονοδιάστατη περιοχή σε έναν δισδιάστατο πίνακα, γεμίζοντας πρώτα τις στήλες. Αυτό είναι χρήσιμο όταν χρειάζεται να αναδιαμορφώσετε δεδομένα για αναφορές ή γραφήματα.

```csharp
using Aspose.Cells;
using System;

class WrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Populate a vertical range A1:A3
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // Apply WRAPCOLS(A1:A3, 2) – this creates a 2‑column array {1,2}
        sheet.Cells["B1"].Formula = "=WRAPCOLS(A1:A3, 2)";

        // Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // Output the result to verify the function works
        Console.WriteLine("Result of WRAPCOLS: " + sheet.Cells["B1"].Value);
        // Expected output: Result of WRAPCOLS: 1
    }
}
```

**Γιατί λειτουργεί αυτό:**  
`WRAPCOLS` δέχεται δύο ορίσματα – την πηγή περιοχής και τον αριθμό των στηλών. Η συνάρτηση γεμίζει τον πίνακα κατά στήλη, απορρίπτοντας τυχόν πλεονάζουσες τιμές (το `3` στο παράδειγμα). Το αποτέλεσμα εμφανίζεται στο κελί επάνω‑αριστερά της περιοχής προορισμού (`B1`), και μπορείτε να επεκτείνετε την περιοχή χειροκίνητα αν χρειάζεστε ολόκληρο τον πίνακα.

> **Συμβουλή:** Μετά τον ορισμό του τύπου, καλέστε `workbook.CalculateFormula()` για να εξασφαλίσετε ότι το αποτέλεσμα είναι ενημερωμένο πριν διαβάσετε τις τιμές των κελιών.

## Βήμα 2: **Μετατροπή βιβλίου εργασίας σε HTML** και **ενσωμάτωση γραμματοσειρών σε html**

Κατά την εξαγωγή ενός αρχείου Excel σε HTML, οι γραμματοσειρές συχνά αντικαθίστανται από τις προεπιλογές του προγράμματος περιήγησης, κάτι που μπορεί να διαταράξει τη διάταξη. Το Aspose.Cells σας επιτρέπει να ενσωματώσετε τις ακριβείς γραμματοσειρές που χρησιμοποιούνται στο βιβλίο εργασίας απευθείας στο αρχείο HTML.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for HtmlSaveOptions
using System;

class HtmlExportDemo
{
    static void Main()
    {
        // Re‑use the workbook from the previous step
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue("Hello");
        sheet.Cells["A2"].PutValue("World");

        // Configure HTML save options
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Embedding fonts ensures the output looks the same on any device
            EmbedFonts = true,
            // Optional: specify a folder for supporting files (images, CSS)
            ExportEmbeddedImages = true
        };

        // Save the workbook as an HTML file with embedded fonts
        string outputPath = @"C:\Temp\WorkbookWithFonts.html";
        workbook.Save(outputPath, htmlOptions);

        Console.WriteLine($"Workbook saved to HTML with embedded fonts at: {outputPath}");
    }
}
```

**Γιατί η ενσωμάτωση γραμματοσειρών είναι σημαντική:**  
Όταν το `EmbedFonts` είναι `true`, το Aspose.Cells μετατρέπει κάθε χρησιμοποιούμενη γραμματοσειρά TrueType/OpenType σε έναν κωδικοποιημένο Base64 κανόνα `@font-face` μέσα στο παραγόμενο HTML. Αυτό εξαλείφει την ανάγκη ο πελάτης να έχει εγκατεστημένες τις ίδιες γραμματοσειρές, εξασφαλίζοντας απόδοση pixel‑perfect.

> **Ακραία περίπτωση:** Εάν το πηγαίο βιβλίο εργασίας αναφέρει μια γραμματοσειρά που δεν είναι εγκατεστημένη στον διακομιστή, το Aspose.Cells θα επιστρέψει σε προεπιλεγμένη γραμματοσειρά και θα εμφανίσει προειδοποίηση. Βεβαιωθείτε ότι οι απαιτούμενες γραμματοσειρές είναι διαθέσιμες

## Τι Θα Πρέπει να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω σεμινάρια καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Χρησιμοποιήσετε το WRAPCOLS σε C# – Δημιουργία Βιβλίου Εργασίας Excel με Συναρτήσεις Περιτύλιξης](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Πώς να Ενσωματώσετε Γραμματοσειρές σε HTML – Μετατροπή Excel σε HTML με C#](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/)
- [Πώς να Μετατρέψετε Αρχεία Excel σε HTML Χρησιμοποιώντας το Aspose.Cells για .NET: Απόκρυψη Επικάλυψης Περιεχομένου](/cells/english/net/workbook-operations/excel-to-html-hide-overlaid-content-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}