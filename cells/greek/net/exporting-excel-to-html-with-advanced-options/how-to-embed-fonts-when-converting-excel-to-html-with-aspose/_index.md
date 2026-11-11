---
category: general
date: 2026-10-01
description: Μάθετε πώς να ενσωματώνετε γραμματοσειρές σε HTML κατά τη μετατροπή του
  Excel σε HTML χρησιμοποιώντας το Aspose.Cells. Εξάγετε το Excel ως HTML με ενσωματωμένες
  γραμματοσειρές σε λίγα βήματα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- convert excel to html
- embed fonts in html
- how to export excel
- export excel as html
language: el
lastmod: 2026-10-01
og_description: Πώς να ενσωματώσετε γραμματοσειρές σε HTML κατά την εξαγωγή αρχείων
  Excel. Ακολουθήστε αυτόν τον οδηγό βήμα‑βήμα για να μετατρέψετε το Excel σε HTML
  με ενσωματωμένες γραμματοσειρές.
og_image_alt: Screenshot of Aspose.Cells code embedding fonts in exported HTML
og_title: Πώς να ενσωματώσετε γραμματοσειρές σε HTML από το Excel – Οδηγός Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  headline: How to embed fonts when converting Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  name: How to embed fonts when converting Excel to HTML with Aspose.Cells
  steps:
  - name: 'Edge case: unsupported fonts'
    text: If the workbook uses a font that is not installed on the server, Aspose.Cells
      falls back to a default system font. To avoid this, install the required fonts
      on the server or embed them manually after export.
  - name: Converting multiple worksheets
    text: If you need to **convert Excel to HTML** for all worksheets, set `ExportActiveWorksheetOnly
      = false` (the default). Aspose.Cells will create a separate HTML file for each
      sheet.
  - name: Controlling CSS output
    text: 'You can reduce the HTML size by disabling inline CSS:'
  - name: Using a stream instead of a file
    text: 'When integrating into a web API, write the HTML to a `MemoryStream` and
      return it directly:'
  type: HowTo
tags:
- Aspose.Cells
- .NET
- Excel conversion
title: Πώς να ενσωματώσετε γραμματοσειρές κατά τη μετατροπή του Excel σε HTML με το
  Aspose.Cells
url: /el/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-converting-excel-to-html-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ενσωματώσετε γραμματοσειρές κατά τη μετατροπή του Excel σε HTML με το Aspose.Cells

Η ενσωμάτωση γραμματοσειρών σε HTML κατά τη μετατροπή ενός βιβλίου εργασίας Excel είναι απαραίτητη για τη διατήρηση της αρχικής εμφάνισης σε όλα τα προγράμματα περιήγησης. Εάν χρειάζεται να μετατρέψετε το Excel σε HTML διατηρώντας τις προσαρμοσμένες γραμματοσειρές, αυτός ο οδηγός παρουσιάζει τη διαδικασία από την αρχή μέχρι το τέλος. Θα δείτε επίσης πώς να εξάγετε το Excel ως HTML και γιατί η ενσωμάτωση γραμματοσειρών σε HTML είναι σημαντική για συνεπή απόδοση.

Αυτό το tutorial καλύπτει όλα όσα χρειάζεστε: τις απαιτούμενες βιβλιοθήκες, τη ρύθμιση του κώδικα και την επαλήθευση του παραγόμενου αρχείου HTML. Στο τέλος, θα μπορείτε να εξάγετε το Excel ως HTML με ενσωματωμένες γραμματοσειρές με λίγες μόνο γραμμές C#.

## Τι θα χρειαστείτε

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* **.NET 6.0 ή νεότερο** – ο κώδικας στοχεύει στο .NET 6, αλλά οποιαδήποτε έκδοση του .NET που υποστηρίζει το Aspose.Cells λειτουργεί.
* **Aspose.Cells for .NET** – αποκτήστε άδεια ή χρησιμοποιήστε τη δωρεάν έκδοση αξιολόγησης από την ιστοσελίδα της Aspose.
* Ένα **περιβάλλον ανάπτυξης C#** (Visual Studio, Rider ή VS Code) – οποιοδήποτε IDE που μπορεί να μεταγλωττίσει έργα .NET.
* Ένα βιβλίο εργασίας Excel (`Styled.xlsx`) που χρησιμοποιεί προσαρμοσμένες γραμματοσειρές που θέλετε να διατηρήσετε.

## Βήμα 1: Ρυθμίστε το Aspose.Cells στο .NET project σας

Πρώτα, προσθέστε το πακέτο NuGet Aspose.Cells στο project σας:

```bash
dotnet add package Aspose.Cells
```

Στη συνέχεια, συμπεριλάβετε το namespace στην κορυφή του αρχείου C#:

```csharp
using Aspose.Cells;
```

Η προσθήκη του πακέτου καθιστά διαθέσιμες τις κλάσεις `Workbook`, `HtmlSaveOptions` και τις σχετικές κλάσεις.

## Βήμα 2: Φορτώστε το βιβλίο εργασίας Excel

Η φόρτωση του βιβλίου εργασίας είναι το πρώτο συγκεκριμένο βήμα στο **πώς να εξάγετε δεδομένα Excel**. Ο κατασκευαστής `Workbook` διαβάζει το αρχείο από το δίσκο:

```csharp
// Step 1: Load the Excel workbook
var workbook = new Workbook("YOUR_DIRECTORY/Styled.xlsx");
```

*Γιατί είναι σημαντικό:* Το Aspose.Cells αναλύει το βιβλίο εργασίας, συμπεριλαμβανομένων των στυλ κελιών, των τύπων και των πληροφοριών γραμματοσειράς. Εάν το αρχείο δεν βρεθεί, θα προκληθεί εξαίρεση, οπότε βεβαιωθείτε ότι η διαδρομή είναι σωστή.

## Βήμα 3: Ρυθμίστε τις επιλογές αποθήκευσης HTML για ενσωμάτωση γραμματοσειρών

Ο πυρήνας του **ενσωμάτωσης γραμματοσειρών σε html** είναι η κλάση `HtmlSaveOptions`. Ορίστε το `EmbedFonts` σε `true` ώστε κάθε γραμματοσειρά που χρησιμοποιείται στο βιβλίο εργασίας να γραφτεί στην έξοδο HTML ως κανόνας `@font-face` κωδικοποιημένος σε Base64.

```csharp
// Step 2: Set HTML save options to embed fonts in the output
var htmlOptions = new HtmlSaveOptions
{
    EmbedFonts = true,
    // Optional: keep the original worksheet name as the HTML file name
    ExportActiveWorksheetOnly = true
};
```

*Γιατί είναι σημαντικό:* Από προεπιλογή, το Aspose.Cells αναφέρει εξωτερικά αρχεία γραμματοσειρών, τα οποία μπορεί να μην είναι διαθέσιμα στη μηχανή του χρήστη. Η ενεργοποίηση του `EmbedFonts` εγγυάται ότι το παραγόμενο HTML θα φαίνεται ακριβώς όπως το αρχικό φύλλο Excel, ανεξάρτητα από τις εγκατεστημένες γραμματοσειρές του θεατή.

### Edge case: μη υποστηριζόμενες γραμματοσειρές

Εάν το βιβλίο εργασίας χρησιμοποιεί μια γραμματοσειρά που δεν είναι εγκατεστημένη στον διακομιστή, το Aspose.Cells θα επιστρέψει σε προεπιλεγμένη σύστημα γραμματοσειράς. Για να το αποφύγετε, εγκαταστήστε τις απαιτούμενες γραμματοσειρές στον διακομιστή ή ενσωματώστε τις χειροκίνητα μετά την εξαγωγή.

## Βήμα 4: Αποθηκεύστε το βιβλίο εργασίας ως HTML χρησιμοποιώντας τις ρυθμισμένες επιλογές

Τώρα μπορείτε να γράψετε το αρχείο HTML. Η μέθοδος `Save` δέχεται τη διαδρομή εξόδου και το αντικείμενο `HtmlSaveOptions`:

```csharp
// Step 3: Save the workbook as an HTML file using the configured options
workbook.Save("YOUR_DIRECTORY/Styled.html", htmlOptions);
```

Μετά την εκτέλεση, το `Styled.html` περιέχει τα δεδομένα του φύλλου και ένα μπλοκ `<style>` με ορισμούς `@font-face` κωδικοποιημένους σε Base64 για κάθε προσαρμοσμένη γραμματοσειρά.

## Βήμα 5: Επαληθεύστε τις ενσωματωμένες γραμματοσειρές

Ανοίξτε το `Styled.html` σε έναν περιηγητή. Εξετάστε την ενότητα `<head>`· θα πρέπει να δείτε κάτι σαν:

```html
<style>
@font-face {
    font-family: 'Calibri';
    src: url(data:font/ttf;base64,AAEAAAARAQAABAA...);
}
...
</style>
```

Εάν οι γραμματοσειρές εμφανίζονται σωστά στον αποδοθέντα πίνακα, η ενσωμάτωση ήταν επιτυχής. Εάν παρατηρήσετε ελλιπή γλυφικά, ελέγξτε ξανά ότι τα αρχεία πηγής γραμματοσειρών είναι εγκατεστημένα στη μηχανή που εκτελεί τη μετατροπή.

## Συνηθισμένες παραλλαγές και πρόσθετες επιλογές

### Μετατροπή πολλαπλών φύλλων εργασίας

Εάν χρειάζεται να **μετατρέψετε το Excel σε HTML** για όλα τα φύλλα, ορίστε `ExportActiveWorksheetOnly = false` (η προεπιλογή). Το Aspose.Cells θα δημιουργήσει ξεχωριστό αρχείο HTML για κάθε φύλλο.

```csharp
htmlOptions.ExportActiveWorksheetOnly = false;
workbook.Save("YOUR_DIRECTORY/AllSheets.html", htmlOptions);
```

### Έλεγχος εξόδου CSS

Μπορείτε να μειώσετε το μέγεθος του HTML απενεργοποιώντας το ενσωματωμένο CSS:

```csharp
htmlOptions.ExportCssSeparately = true; // Generates a .css file alongside the .html
```

### Χρήση ροής (stream) αντί αρχείου

Κατά την ενσωμάτωση σε ένα web API, γράψτε το HTML σε ένα `MemoryStream` και επιστρέψτε το απευθείας:

```csharp
using var stream = new MemoryStream();
workbook.Save(stream, htmlOptions);
stream.Position = 0; // Reset for reading
// Return stream as a file download in ASP.NET Core
```

## Pro tip: Αδειοδώστε το προϊόν για να αφαιρέσετε τα υδατογραφήματα αξιολόγησης

Εάν χρησιμοποιείτε την έκδοση αξιολόγησης, το παραγόμενο HTML μπορεί να περιέχει σχόλιο υδατογραφήματος. Εφαρμόστε την άδεια Aspose.Cells πριν φορτώσετε το βιβλίο εργασίας για να παράγετε καθαρή έξοδο:

```csharp
var license = new License();
license.SetLicense("Aspose.Total.lic");
```

## Πλήρες λειτουργικό παράδειγμα

Παρακάτω υπάρχει ένα πλήρες, εκτελέσιμο πρόγραμμα που δείχνει **πώς να ενσωματώσετε γραμματοσειρές**, **πώς να μετατρέψετε το excel σε html**, και **πώς να εξάγετε το excel ως html** σε ένα βήμα:

```csharp
using System;
using Aspose.Cells;

class ExcelToHtmlWithEmbeddedFonts
{
    static void Main()
    {
        // Apply license if you have one (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Total.lic");

        // 1️⃣ Load the Excel workbook
        var workbookPath = @"YOUR_DIRECTORY/Styled.xlsx";
        var workbook = new Workbook(workbookPath);

        // 2️⃣ Configure HTML save options to embed fonts
        var htmlOptions = new HtmlSaveOptions
        {
            EmbedFonts = true,
            ExportActiveWorksheetOnly = true, // Export only the first sheet
            ExportCssSeparately = false        // Keep CSS inline for a single file
        };

        // 3️⃣ Save as HTML
        var htmlPath = @"YOUR_DIRECTORY/Styled.html";
        workbook.Save(htmlPath, htmlOptions);

        Console.WriteLine($"Excel workbook '{workbookPath}' has been exported to HTML with embedded fonts at '{htmlPath}'.");
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Μετά την εκτέλεση του προγράμματος, το `Styled.html` εμφανίζεται στο `YOUR_DIRECTORY`. Ανοίγοντας το αρχείο σε οποιονδήποτε σύγχρονο περιηγητή, θα δείτε το φύλλο εργασίας με τις ίδιες γραμματοσειρές όπως στο αρχικό αρχείο Excel, ακόμη και σε μηχανές που δεν διαθέτουν αυτές τις γραμματοσειρές.

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να ενσωματώσετε γραμματοσειρές** όταν **μετατρέπετε το Excel σε HTML** χρησιμοποιώντας το Aspose.Cells, και έχετε δει τη πλήρη ροή από τη φόρτωση ενός βιβλίου εργασίας μέχρι την επαλήθευση των ενσωματωμένων γραμματοσειρών. Αυτή η προσέγγιση διασφαλίζει ότι η οπτική πιστότητα των αρχείων Excel διατηρείται στο παραγόμενο HTML, καθιστώντας το ιδανικό για αναφορές στο web, ενημερωτικά δελτία email ή οποιοδήποτε σενάριο όπου πρέπει να **εξάγετε το Excel ως HTML** με προσαρμοστική τυπογραφία.

Στη συνέχεια, εξερευνήστε σχετικά θέματα όπως **η εξαγωγή του Excel ως PDF**, **η διαμόρφωση της εξόδου HTML με προσαρμοσμένο CSS**, ή **η μαζική επεξεργασία πολλαπλών βιβλίων εργασίας**. Κάθε ένα από αυτά βασίζεται στο ίδιο μοτίβο `HtmlSaveOptions`, ώστε να μπορείτε να προσαρμόσετε τον κώδικα με ελάχιστες αλλαγές.

Καλή προγραμματιστική δουλειά!

## Τι πρέπει να μάθετε στη συνέχεια;

Οι παρακάτω οδηγίες καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [How to Export Excel to HTML – Step‑by‑Step Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-step-by-step-guide/)
- [How to Embed Fonts in HTML – Complete C# Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-complete-c-guide/)
- [How to embed fonts when converting Excel to PDF – Step‑by‑Step Guide](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}