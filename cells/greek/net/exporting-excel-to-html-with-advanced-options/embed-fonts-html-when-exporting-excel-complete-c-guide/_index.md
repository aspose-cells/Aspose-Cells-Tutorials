---
category: general
date: 2026-02-28
description: Μάθετε πώς να ενσωματώνετε γραμματοσειρές HTML κατά την εξαγωγή του Excel
  σε HTML χρησιμοποιώντας το Aspose.Cells. Περιλαμβάνει αποθήκευση ως HTML, εξαγωγή
  Excel σε HTML και συμβουλές για μετατροπή υπολογιστικών φύλλων σε HTML.
draft: false
keywords:
- embed fonts html
- export excel html
- save as html
- save excel html
- convert spreadsheet html
language: el
og_description: Η ενσωμάτωση γραμματοσειρών σε HTML είναι απαραίτητη για τέλεια μετατροπή
  Excel‑σε‑HTML. Αυτός ο οδηγός σας δείχνει πώς να εξάγετε το Excel σε HTML με ενσωματωμένες
  γραμματοσειρές χρησιμοποιώντας το Aspose.Cells.
og_title: Ενσωμάτωση γραμματοσειρών HTML κατά την εξαγωγή Excel – Πλήρης οδηγός C#
tags:
- Aspose.Cells
- C#
- HTML export
- Excel automation
title: Ενσωμάτωση γραμματοσειρών HTML κατά την εξαγωγή Excel – Πλήρης οδηγός C#
url: /el/net/exporting-excel-to-html-with-advanced-options/embed-fonts-html-when-exporting-excel-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# embed fonts html κατά την εξαγωγή Excel – Πλήρης οδηγός C#

Σας έχει συμβεί ποτέ να χρειάζεται να **embed fonts html** κατά τη μετατροπή ενός βιβλίου εργασίας Excel σε μια ιστοσελίδα έτοιμη για web; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν πρόβλημα όταν το παραγόμενο HTML φαίνεται σωστό στον υπολογιστή τους αλλά χάνει την ακριβή τυπογραφία σε άλλο πρόγραμμα περιήγησης. Τα καλά νέα; Με λίγες γραμμές C# και Aspose.Cells μπορείτε να **export excel html** που μεταφέρει τις αρχικές γραμματοσειρές μέσα στο αρχείο.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα τη διαδικασία για **save as html** με ενσωματωμένες γραμματοσειρές, θα συζητήσουμε γιατί ίσως θέλετε επίσης να **save excel html** χωρίς γραμματοσειρές, και θα δείξουμε ακόμη έναν γρήγορο τρόπο για **convert spreadsheet html** για ενημερωτικά δελτία email. Χωρίς εξωτερικά εργαλεία, μόνο καθαρός κώδικας που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET.

## Τι Θα Χρειαστεί

- **Aspose.Cells for .NET** (τελευταία έκδοση, 2025‑R2 τη στιγμή της συγγραφής).  
- Ένα περιβάλλον ανάπτυξης .NET (Visual Studio 2022 ή VS Code).  
- Ένα βιβλίο εργασίας Excel που θέλετε να εξάγετε (οποιοδήποτε αρχείο *.xlsx*).

Αυτό είναι όλο—χωρίς επιπλέον πακέτα, χωρίς περίπλοκες τεχνάσματα JavaScript. Μόλις έχετε την βιβλιοθήκη αναφορά, το υπόλοιπο είναι απλό.

## Βήμα 1: Ρύθμιση του Έργου και Προσθήκη Aspose.Cells

Για αρχή, δημιουργήστε μια νέα εφαρμογή console (ή ενσωματώστε σε υπάρχουσα υπηρεσία). Προσθέστε το πακέτο NuGet:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Αν χρησιμοποιείτε εταιρική πηγή, βεβαιωθείτε ότι η πηγή του πακέτου είναι ρυθμισμένη· διαφορετικά η εντολή θα αποτύχει σιωπηρά.

Τώρα συμπεριλάβετε το namespace στην αρχή του αρχείου C#:

```csharp
using Aspose.Cells;
using Aspose.Cells.Saving;
```

Αυτές οι δηλώσεις using σας δίνουν πρόσβαση στην κλάση `Workbook` και στο `HtmlSaveOptions` που θα χρειαστούμε αργότερα.

## Βήμα 2: Φόρτωση του Excel Workbook

Μπορείτε να φορτώσετε ένα workbook από δίσκο, ροή ή ακόμη και από πίνακα byte. Ακολουθεί η πιο απλή έκδοση που διαβάζει από αρχείο:

```csharp
// Load the source Excel file
Workbook wb = new Workbook(@"C:\Files\SampleData.xlsx");

// Optional: adjust settings like calculation mode if needed
wb.CalculateFormula();
```

Γιατί να καλέσετε το `CalculateFormula()`; Αν το φύλλο σας περιέχει τύπους, η βιβλιοθήκη θα υπολογίσει τις τιμές τους πριν την εξαγωγή, διασφαλίζοντας ότι το HTML εμφανίζει τους ίδιους αριθμούς όπως στο Excel.

## Βήμα 3: Διαμόρφωση των HTML Save Options για Ενσωμάτωση Γραμματοσειρών

Αυτή είναι η καρδιά του tutorial. Από προεπιλογή, το Aspose.Cells δημιουργεί ένα αρχείο HTML που αναφέρει εξωτερικά CSS και αρχεία γραμματοσειρών. Για να **embed fonts html**, ενεργοποιήστε τη σημαία `EmbedFonts`:

```csharp
// Step 3: Configure HTML save options to embed fonts in the output
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // Embeds all used fonts directly into the HTML as Base64‑encoded data URIs
    EmbedFonts = true,

    // Optional: keep the original cell formatting
    ExportActiveWorksheetOnly = true,

    // Optional: generate a single HTML file (no separate CSS folder)
    ExportToSingleFile = true
};
```

Ορίζοντας `EmbedFonts = true` λέτε στο Aspose.Cells να πάρει κάθε γραμματοσειρά που αναφέρεται στο workbook, να τη μετατρέψει σε συμβολοσειρά Base64 και να την ενσωματώσει σε ένα μπλοκ `<style>`. Αυτό εγγυάται ότι όποιος ανοίξει το `Result.html` θα δει την ακριβή ίδια τυπογραφία, ανεξάρτητα από το αν η γραμματοσειρά είναι εγκατεστημένη στο σύστημά του.

## Βήμα 4: Αποθήκευση του Workbook ως HTML

Τώρα συνδυάζουμε το workbook και τις επιλογές για να παραχθεί το τελικό αρχείο:

```csharp
// Step 4: Save the document as an HTML file using the configured options
string outputPath = @"C:\Files\Result.html";
wb.Save(outputPath, SaveFormat.Html, htmlOptions);
```

Μετά την εκτέλεση αυτής της γραμμής, το `Result.html` βρίσκεται δίπλα σε τυχόν υποστηρικτικούς πόρους (αν δεν ενεργοποιήσατε το `ExportToSingleFile`). Ανοίξτε το σε Chrome, Edge ή Firefox—θα παρατηρήσετε ότι οι γραμματοσειρές είναι ταυτόσημες με την αρχική προβολή στο Excel.

### Γρήγορη επαλήθευση

Για να βεβαιωθείτε ότι οι γραμματοσειρές είναι πράγματι ενσωματωμένες, ανοίξτε το αρχείο HTML σε επεξεργαστή κειμένου και ψάξτε για `@font-face`. Θα πρέπει να δείτε ένα μπλοκ παρόμοιο με:

```css
@font-face {
    font-family: 'Calibri';
    src: url(data:font/ttf;base64,AAEAAA...);
}
```

Αν το χαρακτηριστικό `src` περιέχει μια μακριά διεύθυνση `data:` URL, έχετε επιτύχει.

## Βήμα 5: Τι Αν Δεν Θέλετε Ενσωματωμένες Γραμματοσειρές;

Μερικές φορές προτιμάτε ένα πιο ελαφρύ αρχείο HTML και δε σας πειράζει ο περιηγητής να χρησιμοποιήσει τις προεπιλεγμένες γραμματοσειρές του συστήματος. Απλώς αλλάξτε τη σημαία:

```csharp
htmlOptions.EmbedFonts = false; // This will generate a normal CSS reference
```

Αυτή η προσέγγιση είναι χρήσιμη όταν δημιουργείτε **export excel html** για εσωτερικά dashboards όπου ελέγχετε το περιβάλλον, ή όταν χρειάζεται να **convert spreadsheet html** για email χαμηλού εύρους ζώνης όπου το μέγεθος μετράει.

## Βήμα 6: Διαχείριση Ακραίων Περιπτώσεων και Συνηθισμένων Παγίδων

| Situation | Recommended Fix |
|-----------|-----------------|
| **Μεγάλα workbooks** ( > 50 MB ) | Χρησιμοποιήστε `ExportToSingleFile = false` για να κρατήσετε το HTML και τα δεδομένα γραμματοσειρών ξεχωριστά· τα προγράμματα περιήγησης διαχειρίζονται άσχημα μεγάλες συμβολοσειρές Base64. |
| **Προσαρμοσμένες γραμματοσειρές δεν ενσωματώνονται** | Βεβαιωθείτε ότι η γραμματοσειρά είναι εγκατεστημένη στο μηχάνημα που εκτελεί τη μετατροπή· το Aspose.Cells μπορεί να ενσωματώσει μόνο τις γραμματοσειρές που μπορεί να εντοπίσει. |
| **Ελλιπείς χαρακτήρες (glyphs)** | Μερικές λειτουργίες OpenType μπορεί να χαθούν· σκεφτείτε να μετατρέψετε το φύλλο σε εικόνα (`SaveFormat.Png`) ως εναλλακτική λύση. |
| **Ανησυχίες για απόδοση** | Κρατήστε στην μνήμη (cache) το αντικείμενο `HtmlSaveOptions` αν μετατρέπετε πολλά αρχεία σε βρόχο· αποφύγετε τη δημιουργία του σε κάθε επανάληψη. |

## Βήμα 7: Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα, εδώ είναι ένα αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε και να εκτελέσετε:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Saving;

namespace ExcelToHtmlWithEmbeddedFonts
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string sourcePath = @"C:\Files\SampleData.xlsx";
            Workbook wb = new Workbook(sourcePath);
            wb.CalculateFormula(); // Ensure formulas are up‑to‑date

            // 2️⃣ Configure HTML options (embed fonts)
            HtmlSaveOptions htmlOptions = new HtmlSaveOptions
            {
                EmbedFonts = true,
                ExportActiveWorksheetOnly = true,
                ExportToSingleFile = true,
                // Optional: set a custom CSS class prefix to avoid clashes
                CssClassPrefix = "aspose_"
            };

            // 3️⃣ Save as HTML
            string outputPath = @"C:\Files\Result.html";
            wb.Save(outputPath, SaveFormat.Html, htmlOptions);

            Console.WriteLine($"✅ HTML file with embedded fonts created at: {outputPath}");
        }
    }
}
```

Εκτελέστε το πρόγραμμα, έπειτα ανοίξτε το `Result.html`. Θα πρέπει να δείτε το φύλλο να εμφανίζεται με τις ακριβώς ίδιες γραμματοσειρές όπως στο Excel—χωρίς ελλιπείς χαρακτήρες, χωρίς εναλλακτικές γραμματοσειρές.

![embed fonts html example](/images/embed-fonts-html.png){alt="αποτέλεσμα embed fonts html που δείχνει ακριβή τυπογραφία"}

## Συμπέρασμα

Τώρα έχετε μια πλήρη, ολοκληρωμένη λύση για **embed fonts html** κατά την εκτέλεση μιας λειτουργίας **export excel html** χρησιμοποιώντας Aspose.Cells. Με την εναλλαγή μιας μόνο ιδιότητας μπορείτε να μεταβείτε μεταξύ ενός βαρύ, πλήρως αυτόνομου αρχείου HTML και μιας ελαφρύτερης έκδοσης που βασίζεται σε εξωτερικές γραμματοσειρές. Αυτή η ευελιξία καθιστά εύκολο το **save as html**, **save excel html**, ή ακόμη και **convert spreadsheet html** για διάφορα σενάρια—από εσωτερικά dashboards αναφοράς μέχρι ενημερωτικά δελτία έτοιμα για email.

Τι ακολουθεί; Δοκιμάστε την εξαγωγή πολλαπλών φύλλων εργασίας σε μία σελίδα HTML, πειραματιστείτε με διαφορετικές επιλογές διαχείρισης εικόνων (`HtmlSaveOptions.ImageFormat`), ή συνδυάστε το με μετατροπή σε PDF για να προσφέρετε τόσο μορφές web όσο και εκτύπωσης. Ο ουρανός είναι το όριο, και τώρα έχετε την βασική τεχνική στα χέρια σας.

Καλή προγραμματιστική δουλειά, και μη διστάσετε να αφήσετε ένα σχόλιο αν συναντήσετε κάποιο πρόβλημα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}