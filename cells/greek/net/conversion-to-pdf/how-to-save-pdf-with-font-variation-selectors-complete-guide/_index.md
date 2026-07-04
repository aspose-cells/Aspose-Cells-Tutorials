---
category: general
date: 2026-07-03
description: πώς να αποθηκεύσετε PDF με ενεργοποιημένους επιλογείς παραλλαγής γραμματοσειράς
  χρησιμοποιώντας το Aspose.Words. Μάθετε πώς να εξάγετε το έγγραφο σε PDF και να
  αποθηκεύσετε το έγγραφο ως PDF αποδοτικά.
draft: false
keywords:
- how to save pdf
- save document as pdf
- export document to pdf
- how to enable selectors
- export word to pdf
language: el
og_description: πώς να αποθηκεύσετε PDF με επιλογείς παραλλαγής γραμματοσειράς χρησιμοποιώντας
  το Aspose.Words. Κύρια εξαγωγή εγγράφου σε PDF και αποθήκευση εγγράφου ως PDF σε
  C#.
og_title: πώς να αποθηκεύσετε PDF με επιλογείς παραλλαγής γραμματοσειράς – βήμα‑βήμα
  οδηγός
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: how to save pdf with font variation selectors enabled using Aspose.Words.
    Learn to export document to pdf and save document as pdf efficiently.
  headline: how to save pdf with font variation selectors – complete guide
  type: TechArticle
- description: how to save pdf with font variation selectors enabled using Aspose.Words.
    Learn to export document to pdf and save document as pdf efficiently.
  name: how to save pdf with font variation selectors – complete guide
  steps:
  - name: Install the library.
    text: Install the library.
  - name: Load your Word document.
    text: Load your Word document.
  - name: Create `PdfSaveOptions` and set `FontVariationSelectors = true`.
    text: Create `PdfSaveOptions` and set `FontVariationSelectors = true`.
  - name: Call `Document.Save` with `SaveFormat.Pdf` and the configured options.
    text: Call `Document.Save` with `SaveFormat.Pdf` and the configured options.
  type: HowTo
tags:
- Aspose.Words
- PDF
- C#
title: πώς να αποθηκεύσετε PDF με επιλογείς παραλλαγής γραμματοσειράς – πλήρης οδηγός
url: /el/net/conversion-to-pdf/how-to-save-pdf-with-font-variation-selectors-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# πώς να αποθηκεύσετε pdf με επιλογείς παραλλαγής γραμματοσειράς – πλήρης οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να αποθηκεύσετε pdf** διατηρώντας κάθε μικρή τυπογραφική λεπτομέρεια; Σε αυτό το tutorial θα σας καθοδηγήσουμε βήμα‑βήμα για να **αποθηκεύσετε pdf** χρησιμοποιώντας το Aspose.Words, με *επιλογείς παραλλαγής γραμματοσειράς* ενεργοποιημένους ώστε το εξαγόμενο έγγραφο σε pdf να φαίνεται pixel‑perfect.  

Αν έχετε κυνηγήσει τη λειτουργία “export document to pdf” για κάποιο διάστημα, βρίσκεστε στο σωστό μέρος. Στο τέλος αυτού του οδηγού δεν θα γνωρίζετε μόνο πώς να **αποθηκεύσετε το έγγραφο ως pdf**, αλλά θα καταλάβετε επίσης **πώς να ενεργοποιήσετε τους επιλογείς** και γιατί είναι σημαντικοί για τις σύγχρονες γραμματοσειρές.

## Τι θα μάθετε

- Οι ελάχιστες προαπαιτήσεις (runtime, πακέτο NuGet, ένα δείγμα αρχείου Word).  
- Πώς να διαμορφώσετε το `PdfSaveOptions` ώστε η σημαία **font variation selectors** να είναι true.  
- Η ακριβής γραμμή κώδικα που **εξάγει το word σε pdf** με ενεργοποιημένους επιλογείς.  
- Πώς να επαληθεύσετε το αποτέλεσμα και να αντιμετωπίσετε κοινά προβλήματα.

Καμία ασαφής αναφορά, χωρίς συντομεύσεις “δείτε τα docs” — μόνο ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο Visual Studio.

![Στιγμιότυπο οθόνης που δείχνει πώς να αποθηκεύσετε pdf με ενεργοποιημένους επιλογείς σε ένα έργο C#](/images/how-to-save-pdf-selectors.png){: .center-image alt="διάγραμμα πώς να αποθηκεύσετε pdf με επιλογείς"}

## Προαπαιτήσεις

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|------------------------|
| .NET 6.0 ή νεότερο | Το Aspose.Words 23.9+ στοχεύει στο .NET Standard 2.0+, έτσι το .NET 6 σας παρέχει τις πιο πρόσφατες δυνατότητες runtime. |
| Aspose.Words for .NET (NuGet) | Παρέχει τις κλάσεις `Document`, `SaveFormat` και `PdfSaveOptions` που θα χρησιμοποιήσουμε. |
| Ένα απλό αρχείο `.docx` (π.χ., *Sample.docx*) | Μας δίνει κάτι συγκεκριμένο για **εξάγει το word σε pdf**. |
| Ένα IDE (VS 2022, Rider, ή VS Code) | Κάνει τον εντοπισμό σφαλμάτων και τις δοκιμές χωρίς κόπο. |

Αν έχετε ήδη αυτά τα στοιχεία, υπέροχα—ας βουτήξουμε.

## Βήμα 1: Εγκατάσταση Aspose.Words

Ανοίξτε το φάκελο του έργου σας σε ένα τερματικό και εκτελέστε:

```bash
dotnet add package Aspose.Words
```

Αυτή η εντολή κατεβάζει το πιο πρόσφατο σταθερό πακέτο και προσθέτει τις απαραίτητες αναφορές στο `.csproj` σας.  

> **Pro tip:** κλειδώστε την έκδοση (π.χ., `Aspose.Words --version 23.9.0`) αν χρειάζεστε επαναλήψιμες κατασκευές.

## Βήμα 2: Διαμόρφωση επιλογών αποθήκευσης PDF – πώς να ενεργοποιήσετε τους επιλογείς

Η μαγεία βρίσκεται στο `PdfSaveOptions`. Από προεπιλογή η επιλογή `FontVariationSelectors` είναι `false`, πράγμα που σημαίνει ότι το παραγόμενο PDF **δεν** θα περιέχει τους πίνακες OpenType variation selector. Η ενεργοποίησή του γίνεται με μια εντολή ιδιότητας:

```csharp
using Aspose.Words;
using Aspose.Words.Saving;

// Load the source Word document
Document doc = new Document("Sample.docx");

// Create and configure PDF save options
PdfSaveOptions saveOptions = new PdfSaveOptions
{
    // Enable font variation selectors for better glyph fidelity
    FontVariationSelectors = true
};
```

**Why this matters:** Οι σύγχρονες μεταβλητές γραμματοσειρές (π.χ. “Roboto Flex” ή “Inter Variable”) βασίζονται στους επιλογείς παραλλαγής για να επιλέξουν το ακριβές βάρος, πλάτος ή κλίση που θέλετε. Χωρίς αυτούς το PDF επιστρέφει σε ένα στατικό γλύφο, και η οπτική ποιότητα μειώνεται. Η ενεργοποίηση της σημαίας λέει στο Aspose.Words να ενσωματώσει αυτούς τους επιλογείς, εξασφαλίζοντας μια πιστή **εξαγωγή εγγράφου σε pdf**.

## Βήμα 3: Αποθήκευση του εγγράφου ως PDF

Τώρα που οι επιλογές έχουν οριστεί, η πραγματική κλήση **αποθήκευσης εγγράφου ως pdf** είναι απλή:

```csharp
// Save the document as PDF with the configured options
doc.Save("VarSelectors.pdf", SaveFormat.Pdf, saveOptions);
```

Αυτή η μοναδική γραμμή γράφει το `VarSelectors.pdf` στον τρέχοντα φάκελο. Αν προτιμάτε απόλυτη διαδρομή, απλώς αντικαταστήστε τη συμβολοσειρά με κάτι όπως `@"C:\Exports\VarSelectors.pdf"`.

### Πλήρες παράδειγμα end‑to‑end

Συνδυάζοντας όλα, εδώ είναι ένα ελάχιστο πρόγραμμα κονσόλας που μπορείτε να εκτελέσετε αμέσως:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Saving;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source Word file (ensure the file exists!)
        Document doc = new Document("Sample.docx");

        // 2️⃣ Prepare PDF save options – enable selectors
        PdfSaveOptions saveOptions = new PdfSaveOptions
        {
            FontVariationSelectors = true
        };

        // 3️⃣ Export the document to PDF
        string outputPath = "VarSelectors.pdf";
        doc.Save(outputPath, SaveFormat.Pdf, saveOptions);

        Console.WriteLine($"PDF saved successfully to {outputPath}");
    }
}
```

**Αναμενόμενη έξοδος** (στην κονσόλα):

```
PDF saved successfully to VarSelectors.pdf
```

Ανοίξτε το `VarSelectors.pdf` σε έναν προβολέα PDF που υποστηρίζει OpenType variation selectors (Adobe Acrobat Reader DC ή το δωρεάν SumatraPDF). Θα πρέπει να δείτε τα ακριβή ίδια βάρη και στυλ γραμματοσειράς που υπήρχαν στο αρχικό αρχείο Word.

## Βήμα 4: Επαλήθευση ότι οι επιλογείς υπάρχουν (προαιρετικό αλλά χρήσιμο)

Αν θέλετε να είστε απολύτως σίγουροι ότι οι επιλογείς έχουν ενσωματωθεί στο αρχείο, μπορείτε να ελέγξετε το PDF με ένα εργαλείο όπως το **pdfinfo** (μέρος του Poppler) ή το **iText 7**:

```bash
pdfinfo -meta VarSelectors.pdf | grep "FontVariationSelector"
```

Αν η εντολή επιστρέψει μια μη κενή γραμμή, οι επιλογείς είναι ενσωματωμένοι. Αυτό το βήμα είναι ιδιαίτερα χρήσιμο όταν αυτοματοποιείτε μια αλυσίδα εξαγωγής παρτίδας και χρειάζεται να εγγυηθείτε τη συμμόρφωση.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Σύμπτωμα | Πιθανή αιτία | Διόρθωση |
|----------|--------------|----------|
| Το PDF φαίνεται *διαφορετικό* από την πηγή Word | `FontVariationSelectors` άφησε στην προεπιλογή `false`. | Ορίστε `saveOptions.FontVariationSelectors = true;`. |
| Εξαίρεση: *File not found* κατά την κλήση `new Document("Sample.docx")` | Η διαδρομή είναι σχετική με το *working directory*, όχι με το φάκελο του έργου. | Χρησιμοποιήστε απόλυτη διαδρομή ή `Path.Combine(Environment.CurrentDirectory, "Sample.docx")`. |
| Το μέγεθος του PDF αυξάνεται απροσδόκητα | Οι γραμματοσειρές ενσωματώνονται πλήρως αντί να υποσύνολο. | Προσθέστε `saveOptions.SubsetFonts = true;` (η προεπιλογή είναι true, αλλά ελέγξτε αν το αλλάξατε). |
| Ο προβολέας αναφέρει “unknown font” | Ο προβολέας δεν υποστηρίζει επιλογείς παραλλαγής. | Δοκιμάστε με σύγχρονο προβολέα, ή επιστρέψτε σε στατικές γραμματοσειρές αν απαιτείται συμβατότητα. |

## Επέκταση της λύσης – εξαγωγή word σε pdf μαζικά

Αν χρειάζεστε **εξαγωγή εγγράφου σε pdf** για δεκάδες αρχεία Word, τυλίξτε τη λογική σε μια βοηθητική μέθοδο:

```csharp
static void ExportWordToPdf(string sourcePath, string destPath)
{
    Document doc = new Document(sourcePath);
    PdfSaveOptions options = new PdfSaveOptions { FontVariationSelectors = true };
    doc.Save(destPath, SaveFormat.Pdf, options);
}
```

Στη συνέχεια, καλέστε την μέσα σε βρόχο `foreach` πάνω σε έναν φάκελο:

```csharp
string[] files = Directory.GetFiles(@"C:\WordDocs", "*.docx");
foreach (var file in files)
{
    string pdfName = Path.ChangeExtension(file, ".pdf");
    ExportWordToPdf(file, pdfName);
}
```

Αυτό το απόσπασμα δείχνει έναν καθαρό τρόπο για **αποθήκευση εγγράφου ως pdf** μαζικά ενώ διατηρεί τη σημαία επιλογέα ενεργοποιημένη.

## Σύνοψη

Συζητήσαμε όλα όσα χρειάζεται να γνωρίζετε για **πώς να αποθηκεύσετε pdf** με επιλογείς παραλλαγής γραμματοσειράς χρησιμοποιώντας το Aspose.Words:

1. Εγκαταστήστε τη βιβλιοθήκη.  
2. Φορτώστε το έγγραφο Word.  
3. Δημιουργήστε `PdfSaveOptions` και ορίστε `FontVariationSelectors = true`.  
4. Κλήστε `Document.Save` με `SaveFormat.Pdf` και τις ρυθμισμένες επιλογές.  

Τώρα έχετε μια αξιόπιστη μέθοδο για **εξαγωγή εγγράφου σε pdf**, **αποθήκευση εγγράφου ως pdf**, και **εξαγωγή word σε pdf** διατηρώντας την πλήρη τυπογραφική πλούσια των μεταβλητών γραμματοσειρών.

## Τι ακολουθεί;

- Πειραματιστείτε με άλλες `PdfSaveOptions` (π.χ., `Compliance = PdfCompliance.PdfA2b`).  
- Συνδυάστε αυτή την προσέγγιση με **συμπίεση εικόνας** για να μειώσετε το μέγεθος του αρχείου.  
- Εξερευνήστε την υποστήριξη **PDF/A** του Aspose.Words αν χρειάζεστε αρχειοθετημένα PDFs.  

Μη διστάσετε να τροποποιήσετε τον κώδικα, να δοκιμάσετε διαφορετικές γραμματοσειρές, ή να ενσωματώσετε το απόσπασμα σε μια μεγαλύτερη υπηρεσία δημιουργίας εγγράφων. Αν αντιμετωπίσετε πρόβλημα, αφήστε ένα σχόλιο παρακάτω—καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να αποθηκεύσετε συγκεκριμένες σελίδες ενός αρχείου Excel ως PDF χρησιμοποιώντας το Aspose.Cells για .NET](/cells/english/net/workbook-operations/save-specific-excel-pages-pdf-aspose-cells-net/)
- [Αποθήκευση βιβλίου εργασίας Excel ως PDF με προσαρμοσμένες γραμματοσειρές χρησιμοποιώντας το Aspose.Cells για .NET](/cells/english/net/workbook-operations/save-excel-workbook-pdf-custom-fonts-aspose-cells-net/)
- [Δημιουργία και αποθήκευση βιβλίου εργασίας Excel ως PDF σε ASP.NET χρησιμοποιώντας το Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}