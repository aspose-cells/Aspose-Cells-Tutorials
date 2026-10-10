---
category: general
date: 2026-10-10
description: Μάθετε πώς να ενσωματώνετε γραμματοσειρές κατά την εξαγωγή του Excel
  σε HTML με C#. Αυτός ο οδηγός καλύπτει την εξαγωγή Excel σε HTML, τη μετατροπή Excel
  σε HTML και πώς να αποθηκεύσετε το Excel με ενσωματωμένες γραμματοσειρές.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- export excel html
- convert excel html
- how to save excel
- embed fonts html
language: el
lastmod: 2026-10-10
og_description: Πώς να ενσωματώσετε γραμματοσειρές κατά την εξαγωγή του Excel σε HTML
  με C#. Ακολουθήστε αυτό το πλήρες σεμινάριο για να εξάγετε Excel σε HTML, να μετατρέψετε
  Excel σε HTML και να μάθετε πώς να αποθηκεύετε το Excel με ενσωματωμένες γραμματοσειρές.
og_image_alt: Screenshot showing exported HTML file that demonstrates how to embed
  fonts from Excel
og_title: Πώς να ενσωματώσετε γραμματοσειρές κατά την εξαγωγή του Excel σε HTML –
  βήμα‑βήμα οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to embed fonts while exporting Excel to HTML in C#. This
    guide covers export excel html, convert excel html, and how to save Excel with
    embedded fonts.
  headline: How to embed fonts when exporting Excel to HTML with C#
  type: TechArticle
tags:
- Excel
- HTML export
- Font embedding
- C#
title: Πώς να ενσωματώσετε γραμματοσειρές κατά την εξαγωγή του Excel σε HTML με C#
url: /el/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-exporting-excel-to-html-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ενσωματώσετε γραμματοσειρές κατά την εξαγωγή του Excel σε HTML με C#

Αν χρειάζεστε **how to embed fonts** σε ένα αρχείο HTML που δημιουργείται από ένα βιβλίο εργασίας Excel, αυτό το tutorial δείχνει τα ακριβή βήματα. Η εξαγωγή του Excel σε HTML συχνά αφαιρεί τις προσαρμοσμένες γραμματοσειρές, κάτι που διασπά την οπτική πιστότητα του αρχικού φύλλου. Με τη σωστή διαμόρφωση των επιλογών μπορείτε να διατηρήσετε κάθε γραμματοσειρά απευθείας στην έξοδο HTML.

Σε αυτόν τον οδηγό θα μάθετε πώς να **export excel html**, **convert excel html**, και **how to save Excel** με ενσωματωμένες γραμματοσειρές, χρησιμοποιώντας τη βιβλιοθήκη Aspose.Cells για .NET. Η λύση λειτουργεί με .NET 6+ και απαιτεί μόνο λίγες γραμμές κώδικα C#.

## Τι θα πετύχετε

- Ένα πλήρες, εκτελέσιμο πρόγραμμα C# που φορτώνει ένα υπάρχον αρχείο `.xlsx`.
- Έξοδος HTML όπου όλες οι χρησιμοποιημένες γραμματοσειρές ενσωματώνονται ως κανόνες `@font-face` κωδικοποιημένοι σε Base64.
- Σιγουριά ότι το εξαγόμενο HTML φαίνεται ταυτόσημο με το αρχικό βιβλίο εργασίας σε οποιονδήποτε φυλλομετρητή.

## Προαπαιτούμενα

| Απαίτηση | Αιτία |
|-------------|--------|
| .NET 6 SDK or later | Παρέχει το runtime για το έργο C#. |
| Visual Studio 2022 (or any IDE) | Διευκολύνει τη δημιουργία και εκτέλεση της εφαρμογής console. |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | Παρέχει την κλάση `HtmlSaveOptions` και τη δυνατότητα `EmbedFonts`. |
| An Excel file (`sample.xlsx`) that uses a custom font (e.g., *Calibri* or a downloaded TrueType font) | Δείχνει το αποτέλεσμα της ενσωμάτωσης γραμματοσειρών. |

> **Συμβουλή επαγγελματία:** Αν εργάζεστε πίσω από εταιρικό proxy, ρυθμίστε το NuGet να χρησιμοποιεί το proxy πριν εγκαταστήσετε το πακέτο.

## Βήμα 1: Εγκατάσταση Aspose.Cells

Ανοίξτε ένα τερματικό στον φάκελο του έργου και εκτελέστε:

```bash
dotnet add package Aspose.Cells
```

Η εντολή προσθέτει την πιο πρόσφατη σταθερή έκδοση του Aspose.Cells στο έργο σας, καθιστώντας διαθέσιμες τις κλάσεις `Workbook` και `HtmlSaveOptions`.

## Βήμα 2: Φόρτωση του βιβλίου εργασίας Excel

Δημιουργήστε μια νέα εφαρμογή console (`dotnet new console`) και προσθέστε τον παρακάτω κώδικα στο `Program.cs`:

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load an existing workbook. Replace the path with your actual file location.
        Workbook wb = new Workbook("sample.xlsx");
        // Continue with HTML export...
    }
}
```

**Γιατί αυτό το βήμα είναι σημαντικό:**  
Η φόρτωση του βιβλίου εργασίας σας δίνει πρόσβαση στα φύλλα εργασίας, τα στυλ και τις προσαρμοσμένες γραμματοσειρές που αναφέρονται μέσα στο αρχείο. Χωρίς ένα φορτωμένο αντικείμενο `Workbook` δεν μπορείτε να διαμορφώσετε τις επιλογές εξαγωγής.

## Βήμα 3: Διαμόρφωση των επιλογών αποθήκευσης HTML για ενσωμάτωση γραμματοσειρών

Η κλάση `HtmlSaveOptions` ελέγχει κάθε πτυχή της εξαγωγής HTML. Ορίζοντας `EmbedFonts = true` λέτε στο Aspose.Cells να ενσωματώνει κάθε γραμματοσειρά που χρησιμοποιείται στο βιβλίο εργασίας απευθείας στο παραγόμενο αρχείο HTML.

```csharp
// Configure HTML save options to embed fonts
HtmlSaveOptions opts = new HtmlSaveOptions
{
    // When true, the exporter creates @font-face rules with Base64 data.
    EmbedFonts = true,

    // Optional: keep the original folder structure for images.
    ExportImagesAsBase64 = true,

    // Optional: generate a single HTML file (no external CSS folder).
    ExportActiveWorksheetOnly = false
};
```

**Εξήγηση:**  
- `EmbedFonts` είναι η βασική σημαία που ικανοποιεί την απαίτηση **how to embed fonts**.  
- `ExportImagesAsBase64` εξασφαλίζει ότι τυχόν εικόνες επίσης γίνονται μέρος του μοναδικού αρχείου HTML, απλοποιώντας την ανάπτυξη.  
- `ExportActiveWorksheetOnly` ορισμένο σε `false` εγγυάται ότι όλα τα φύλλα εργασίας περιλαμβάνονται, κάτι που είναι χρήσιμο όταν το βιβλίο εργασίας εκτείνεται σε πολλά φύλλα.

## Βήμα 4: Αποθήκευση του βιβλίου εργασίας ως HTML με ενσωματωμένες γραμματοσειρές

Τώρα καλέστε τη μέθοδο `Save`, περνώντας τη ζητούμενη διαδρομή εξόδου και τις επιλογές που μόλις διαμορφώσατε:

```csharp
// Save the workbook as an HTML file with embedded fonts
wb.Save("Embedded.html", opts);
```

Το παραγόμενο αρχείο `Embedded.html` περιέχει:

- Τυπική σήμανση HTML για τα δεδομένα του φύλλου.  
- Ένα ή περισσότερα μπλοκ `<style>` με κανόνες `@font-face` που ενσωματώνουν τις προσαρμοσμένες γραμματοσειρές ως συμβολοσειρές Base64.  
- Όλες οι εικόνες κωδικοποιημένες απευθείας στο HTML (αν υπάρχουν).

## Βήμα 5: Επαλήθευση ότι οι γραμματοσειρές είναι πραγματικά ενσωματωμένες

Ανοίξτε το `Embedded.html` σε έναν φυλλομετρητή (Chrome, Edge, Firefox). Η σελίδα πρέπει να αποδίδει ακριβώς όπως το αρχικό βιβλίο εργασίας Excel, ακόμη και αν ο υπολογιστής προορισμού δεν έχει εγκατεστημένες τις προσαρμοσμένες γραμματοσειρές.

Για διπλό έλεγχο της ενσωμάτωσης:

1. Ανοίξτε τον πηγαίο κώδικα της σελίδας (`Ctrl+U` στα περισσότερα προγράμματα περιήγησης).  
2. Αναζητήστε `@font-face`. Θα δείτε ένα μπλοκ παρόμοιο με:

```css
@font-face {
    font-family: 'Calibri';
    src: url('data:font/ttf;base64,AAEAAAALAIAAAwAwT1Mv...') format('truetype');
    font-weight: normal;
    font-style: normal;
}
```

Αν το χαρακτηριστικό `src` περιέχει μια διεύθυνση `data:`, η γραμματοσειρά έχει ενσωματωθεί επιτυχώς.

## Συνηθισμένες παραλλαγές και ειδικές περιπτώσεις

| Κατάσταση | Προτεινόμενη προσαρμογή |
|-----------|----------------------|
| **Large workbook with many custom fonts** | Αυξήστε το `MaxFontEmbeddingSize` (αν είναι διαθέσιμο) ή χωρίστε την εξαγωγή σε πολλαπλά αρχεία HTML για να αποφύγετε το όριο μεγέθους των φυλλομετρητών. |
| **You need only a single worksheet** | Ορίστε `opts.ExportActiveWorksheetOnly = true` και ενεργοποιήστε το επιθυμητό φύλλο πριν την αποθήκευση (`wb.Worksheets[0].Activate();`). |
| **Embedding fonts is not allowed by corporate policy** | Ορίστε `opts.EmbedFonts = false` και βασιστείτε σε γραμματοσειρές ασφαλείς για το web ή παρέχετε τα αρχεία γραμματοσειρών μαζί με το HTML. |
| **Targeting older browsers that don’t support Base64 fonts** | Χρησιμοποιήστε `opts.FontEmbeddingMode = FontEmbeddingMode.FontFile;` (αν η έκδοση της βιβλιοθήκης το υποστηρίζει) για να δημιουργήσετε ξεχωριστά αρχεία `.ttf` και να τα αναφέρετε με κανονικές διευθύνσεις URL. |

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο `Program.cs`. Περιλαμβάνει όλες τις απαραίτητες δηλώσεις `using` και διαχείριση σφαλμάτων για ένα script έτοιμο για παραγωγή.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load the workbook (replace with your file path)
            Workbook wb = new Workbook("sample.xlsx");

            // 2️⃣ Configure HTML export options to embed fonts
            HtmlSaveOptions opts = new HtmlSaveOptions
            {
                EmbedFonts = true,               // ✅ Core requirement: how to embed fonts
                ExportImagesAsBase64 = true,     // Keep everything in one file
                ExportActiveWorksheetOnly = false
            };

            // 3️⃣ Save as HTML with embedded fonts
            string outputPath = "Embedded.html";
            wb.Save(outputPath, opts);

            Console.WriteLine($"HTML file with embedded fonts saved to: {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**Αναμενόμενη έξοδος:**  
Η εκτέλεση του προγράμματος εκτυπώνει τη γραμμή επιβεβαίωσης και δημιουργεί το `Embedded.html`. Το άνοιγμα του αρχείου σε οποιονδήποτε σύγχρονο φυλλομετρητή εμφανίζει το φύλλο εργασίας με όλες τις αρχικές γραμματοσειρές αμετάβλητες, εκπληρώνοντας τον στόχο **how to embed fonts**.

## Συμπέρασμα

Τώρα γνωρίζετε **how to embed fonts** κατά την εκτέλεση μιας λειτουργίας **export excel html**, πώς να **convert excel html** χωρίς να χάσετε τις γραμματοσειρές, και τα ακριβή βήματα για **how to save excel** ως αρχείο HTML με ενσωματωμένες γραμματοσειρές. Χρησιμοποιώντας `HtmlSaveOptions.EmbedFonts = true`, το παραγόμενο HTML γίνεται αυτόνομο, φορητό και οπτικά ταυτόσημο με το αρχικό βιβλίο εργασίας.

### Τι θα ακολουθήσει;

- Εξερευνήστε τις ιδιότητες του `HtmlSaveOptions` για να ελέγξετε το CSS, τη διαχείριση εικόνων και την επιλογή φύλλων εργασίας.  
- Συνδυάστε αυτήν την τεχνική με αυτοματοποίηση στο διακομιστή για να δημιουργείτε αναφορές HTML άμεσα.  
- Διερευνήστε το **embed fonts html** για άλλες μορφές εγγράφων (π.χ., PDF) χρησιμοποιώντας παρόμοια API του Aspose.

## Τι πρέπει να μάθετε στη συνέχεια;

- [Πώς να εξάγετε το Excel σε HTML – Πλήρης Οδηγός Προγραμματισμού](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-complete-programming-guide/)
- [Πώς να εξάγετε το Excel σε HTML – Οδηγός βήμα‑βήμα](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-step-by-step-guide/)
- [Πώς να ενσωματώσετε γραμματοσειρές κατά τη μετατροπή του Excel σε PDF – Πλήρης Οδηγός](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-complete-gui/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}